# 【UE4】GENERATED_BODY() とアクセス指定子

----
## はじめに
### 環境

| | |
| ---- | ---- |
| UE4 バージョン | 4.26.1 |
| Visual Studio | 2017 |

### この記事は何？
この記事は、`GENERATED_BODY()` 等がアクセス指定子をどのように変更しているかをまとめたものです。

ピュアな C++ しか触ったことがない人にとって、マクロで自動生成されたコードが何をしているかは気になるところだと思います。
`GENERATED_BODY()` のアクセス指定子の扱いを見ることで、その他のマクロが何をしているか調査する際にも参考になると思います。


### 想定している読者
* UE C++ の初心者
* `GENERATED_BODY()` が何なのか気になる方

----
## 結論

`GENERATED_BODY()` は保護レベル（アクセス指定子）を変更しません。
正確には、 `GENERATED_BODY()` は内部でアクセス指定子を使用しますが、抜ける前に記述した時点の保護レベル（アクセス指定子）に戻します。
（`struct` の場合は全く使用しません。）

----
## もう少し詳しく

`GENERATED_BODY()` に関しては、 4.6 のリリースドキュメントに記述されています。

[Unreal Engine 4.6 リリース!](https://www.unrealengine.com/ja/blog/unreal-engine-46-released?lang=ja)
> ユーザーが設定した保護レベルが GENERATED_BODY によってリセットされなくなりました。ユーザーの設定が保存されるようになります。

[Unreal Engine 4.6 Released!](https://www.unrealengine.com/en-US/blog/unreal-engine-46-released?lang=en-US)
> "GENERATED_BODY" no longer resets your protection level to "public". It will preserve your settings.
> "GENERATED_BODY" は保護レベルを "public" に再設定しなくなりました。設定は保持されます。

公式の日本語訳だとよくわかりませんが、英語の方を見ると、 `GENERATED_BODY()` を記述した際の保護レベル（アクセス指定子）を記憶して、元に戻しているように読み取れます。
実際に `GENERATED_BODY()` の前に `protected:` などを記述すると、 `GENERATED_BODY()` の展開の際に利用される [`generated.h`](#generatedh) の該当のマクロの末尾にあるアクセス指定子がマクロの呼び出し時のものに変わることが確認できます。

また、4.8 の際に、 `GENERATED_BODY` を場所（ `UCLASS`/`USTRUCT`/`UINTERFACE`/`IINTERFACE` ）に関わらず使用できるようになっているようです。

[Unreal Engine 4.8 Release Notes](https://docs.unrealengine.com/en-US/WhatsNew/Builds/ReleaseNotes/2015/4_8/index.html)
> New: Now UnrealHeaderTool will accept GENERATED_BODY macro in every place you had to insert a type specific GENERATED*BODY macros (e.g. GENERATED_UINTERFACE_BODY)! It will figure out the context without your help.
> New: UnrealHeaderTool は型固有の GENERATED*BODY マクロ（例 GENERATED_UINTERFACE_BODY ）を挿入しなければならなかったすべての場所で GENERATED_BODY マクロを受け入れるようになりました！あなたの助けなしに文脈を理解します。


----
## 確認する過程のメモ

### generated.h

元のファイルが極端に大きくなければ100行程度なので、見たことが無い方は一度みておくことをおすすめします。

UE4 の C++ は、たとえば `MyObject.cpp/.h` の場合、 `MyObject.generated.h` というヘッダファイルを指定するように公式ドキュメントにも記載されています。
 [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > プログラミング ガイド > UE4 の C++ プログラミング入門](https://docs.unrealengine.com/ja/ProgrammingAndScripting/ProgrammingWithCPP/IntroductionToCPP/index.html)
> まず最初に MyObject.generated.h をインクルードしていることが分かります。
> UE4 は、リフレクション データをすべて生成し、それをこのファイルに入れます。
> タイプを宣言するヘッダファイルの中で、このファイルを一番最後にインクルードします。

以下でも取り上げられています。
* [`アンリアルのプロパティ システム (リフレクション)`](https://www.unrealengine.com/ja/blog/unreal-property-system-reflection?lang=ja) 


### GENERATED_BODY() とはコード的に言うと実際は何なのか

[Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/index.html)
> すべてのゲームプレイ クラスは、適切に実装するために GENERATED_BODY マクロを使用しなければなりません。

[Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > プログラミング ガイド > UE4 の C++ プログラミング入門](https://docs.unrealengine.com/ja/ProgrammingAndScripting/ProgrammingWithCPP/IntroductionToCPP/index.html)
> GENERATED_BODY() - UE4 は、タイプ用に生成されたすべての必要なボイラープレート コードにこれを置き換えます。

具体的に何に置き換わるのでしょうか？
結局の所、 C++ のコードであるので、 `Visual Studio` の `定義へ移動(G) F12` などを利用すれば比較的簡単に追いかけることが出来ます。

`GENERATED_BODY()` 自体は `Engine\Source\Runtime\CoreUObject\Public\UObject\ObjectMacros.h` で定義されているのが確認できます。
その定義によると、ファイル名や行数などを組み合わせた別のマクロを呼び出しています。
この別のマクロというのが前述の [`generated.h`](#generatedh) で定義されています。

`GENERATED_BODY()` にはいくつかの古いバージョンのバリエーションがあります。
通常、ユーザーがクラス定義の際に使うのは `GENERATED_BODY()` になります。


### GENERATED_BODY() と古いバージョン

[`generated.h`](#generatedh) を覗いてみると、マクロ後のアクセス指定子は概ね以下のように変わります。

| 名前                            | アクセス指定子 | 備考                                      |
| ------------------------------- | -------------- | ----------------------------------------- |
| `GENERATED_BODY()`              | 元に戻す       |                                           |
| `GENERATED_BODY_LEGACY()`       | `public`       |                                           |
| `GENERATED_USTRUCT_BODY()`      | 指定子ない     | 中で `GENERATED_BODY()` を呼び出す        |
| `GENERATED_UCLASS_BODY()`       | 備考参照       | 中で `GENERATED_BODY_LEGACY()` を呼び出す |
| `GENERATED_UINTERFACE_BODY()`   | 備考参照       | 中で `GENERATED_BODY_LEGACY()` を呼び出す |
| `GENERATED_IINTERFACE_BODY()`   | 備考参照       | 中で `GENERATED_BODY_LEGACY()` を呼び出す |

UE4 側のヘッダだと `GENERATED_UCLASS_BODY()` などが利用されてるケースが多くあります。

> MEMO: `GENERATED_BODY()` の仕組みは後から追加されたものなので、ライブラリ側は互換性のために前の状態のままになっているものと考えられます。

UE4 側のヘッダはこれらのマクロの後にメンバのアクセス指定子がないケースが多いので、注意が必要です。

`GENERATED_BODY()` と `GENERATED_BODY_LEGACY()` は、その他（特にコンストラクタまわり）も色々違うようです。
`GENERATED_BODY()` が導入されたときのリリースのドキュメントが比較的詳しいです。
[Unreal Engine 4.6 リリース!](https://www.unrealengine.com/ja/blog/unreal-engine-46-released?lang=ja)
[Unreal Engine 4.6 Released!](https://www.unrealengine.com/en-US/blog/unreal-engine-46-released?lang=en-US)
> クラス宣言の簡略化
> 
> 現在、作成するクラスには通常の C++ のコンストラクタが定義および使用されています。これからは、引数のないコンストラクタも使用できるようになりました！
> エディタまたはブループリントにプロパティをエクスポーズするために、プロパティのためのカテゴリを供給する必要がなくなりました。デフォルトのカテゴリも取得できるようになりました。
> FPostContructInitializeProperties が非推奨になり、FObjectInitializer に置き換えられました。これは本当に必要な場合にのみ指定します。
> ユーザーが設定した保護レベルが GENERATED_BODY によってリセットされなくなりました。ユーザーの設定が保存されるようになります。
> GENERATED_UCLASS_BODY の代わりに新たな "GENERATED_BODY" 指定子を使用するようにしてください。これらの新たな改善の多くはこの指定子によって可能になります。

`GENERATED_BODY()` で挿入されるコードの更に詳しい情報が必要な場合は [`generated.h`](#generatedh) を確認することをおすすめします。


## あとがき

もともとは、エンジン側のクラスを派生し、仮想関数をオーバーライドする際に（ `GENERATED_BODY()` 類の直後のアクセス指定子が省略されているケースが多かった為）どのアクセス指定子が正しいのかの確認に手間取ったのが調査のきっかけでした。
各種マクロで何が行われているか、 [`generated.h`](#generatedh) とは何なのか、なんとなく想像できるようになったと思います。
どなたかの参考になれば幸いです。

ここまで読んでいただきありがとうございました！

----
## 参考リンク

* [Unreal Engine 4 ドキュメント > プロダクション パイプラインをセットアップする > ビルド ツール > UnrealHeaderTool](https://docs.unrealengine.com/ja/ProductionPipelines/BuildTools/UnrealHeaderTool/index.html)
* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/index.html)
* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > Structs](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Structs/index.html)
* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > ゲームプレイ クラス](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Classes/index.html)
* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > インターフェース](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Interfaces/index.html)
* [アンリアルのプロパティ システム (リフレクション)](https://www.unrealengine.com/ja/blog/unreal-property-system-reflection?lang=ja)
* [Unreal Engine 4.6 リリース!](https://www.unrealengine.com/ja/blog/unreal-engine-46-released?lang=ja)
* [Unreal Engine 4.6 Released!](https://www.unrealengine.com/en-US/blog/unreal-engine-46-released?lang=en-US)
* [Unreal Engine 4.8 Release Notes](https://docs.unrealengine.com/en-US/WhatsNew/Builds/ReleaseNotes/2015/4_8/index.html)


----
おしまい。
