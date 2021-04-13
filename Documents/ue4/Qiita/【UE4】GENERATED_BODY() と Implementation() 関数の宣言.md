# 【UE4】GENERATED_BODY() と Implementation() 関数の宣言

----
## はじめに
### 環境

| | |
| ---- | ---- |
| UE4 バージョン | 4.26.1 |
| Visual Studio | 2017 |

### この記事は何？
この記事は、`_Implementaion()` 関数の宣言についてまとめたものです。

関数指定子 `Server` / `Client` / `NetMulticast` （要は `RPC` 用） と、 `BlueprintNativeEvent` を使用する場合、 `_Implementation()` というサフィックスが付く関数を使うことになりますが、 `GENERATED_BODY()` 等が絡む部分があったのでそれをまとめました。
この記事では前述の4つの関数指定子を使用している場合のみについて言及します。
（他の関数指定子の場合は `_Implementation()` は使用しない思いますが、念の為。）


### 想定している読者
* UE C++ の初心者
* `_Implementation()` 関数が気になる方
* `GENERATED_BODY()` が何なのか気になる方

----
## 結論

| 関数指定子 | `GENERATED_BODY()` 内での `_Implementation()` 関数の宣言 | `GENERATED_UCLASS_BODY()`  内での `_Implementation()` 関数の宣言 |
|-----|-----|-----|
| `Server` / `Client` / `NetMulticast` | されない | される |
| `BlueprintNativeEvent` | されない | される |

全体ひっくるめると以下の通り :
* `GENERATED_BODY()` を使用しているのであれば、`_Implementation()` 関数の宣言は自前で**書かなければならない**。
* `GENERATED_UCLASS_BODY()` を使用しているのであれば、`_Implementation()` 関数の宣言は自前で**書いてはいけない**。


----
## 公式ドキュメントの記述

[Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > プログラミング ガイド > UE4 の C++ プログラミング入門](https://docs.unrealengine.com/ja/ProgrammingAndScripting/ProgrammingWithCPP/IntroductionToCPP/index.html)
の `BlueprintNativeEvent` の説明の際に、以下のような記載があります。

> 前のバージョンのビルドツールでは、_Implementation() 宣言は自動的に生成されました。
> 4.8 以降のビルド ツールでは、ヘッダにそれを明示的に追加しなければなりません。

`GENERATED_BODY()` の導入の際に変わった感じですね。


----
## `_Implementation()` 関数の呼び出しの仕組み

`generated.h` と同様に `gen.cpp` というソースが生成されますが、`_Implementation()` はそこから呼ばれていることが確認できます。

```c++:SampleCharacter.h
// 例。簡略化のために定義をインラインで書いている。
UCLASS()
class SAMPLE_API ASampleCharacter : public ACharacter
{
//...
	UFUNCTION(BlueprintNativeEvent)
	void CalledFromCpp();
	void CalledFromCpp_Implementation(){}

//...
};
```

このような定義をしている場合、以下のようなコードが生成されます。

```c++:SampleCharacter.gen.cpp
//...
	DEFINE_FUNCTION(ASampleCharacter::execCalledFromCpp)
	{
		P_FINISH;
		P_NATIVE_BEGIN;
		P_THIS->CalledFromCpp_Implementation();
		P_NATIVE_END;
	}
	static FName NAME_ASampleCharacter_CalledFromCpp = FName(TEXT("CalledFromCpp"));
	void ASampleCharacter::CalledFromCpp()
	{
		ProcessEvent(FindFunctionChecked(NAME_ASampleCharacter_CalledFromCpp),NULL);
	}

//...
```

`gen.cpp` の中身を見たことがないのであれば、一度眺めてみると良いと思います。


----
## 名前の指定

[Unreal Engine 4 ドキュメント > 新機能 > リリースノート > Unreal Engine 4.8 リリースノート](https://docs.unrealengine.com/ja/WhatsNew/Builds/ReleaseNotes/2015/4_8/index.html)
> New: Now you can specify your own function names for Implementation and Validate methods using keywords! E.g. UFUNCTION(Server="MyServerImplementationMethodName", WithValidation="MyServerValidateMethodName").
> New: ImplementationメソッドやValidateメソッドに、キーワードを使って独自の関数名を指定できるようになりました。例： UFUNCTION(Server="MyServerImplementationMethodName", WithValidation="MyServerValidateMethodName").

4.8 の時点で `_Implementation()` 関数に名前を指定できるようになりました。
ですが、対応しているのは `Server` / `Client` のみのようです。
`NetMulticast` /`BlueprintNativeEvent` で指定してもエラーにはなりませんが、 `gen.cpp` での呼び出しには利用されません。

```c++:SampleCharacter.h
// 例。簡略化のために定義をインラインで書いている。
UCLASS()
class SAMPLE_API ASampleCharacter : public ACharacter
{
//...
	UFUNCTION(Server="ServerTest_Implementation2")
	void ServerTest();
	void ServerTest_Implementation2(){}								// 問題ない。 gen.cpp で利用される。

	UFUNCTION(Client="ClientTest_Implementation2")
	void ClientTest();
	void ClientTest_Implementation2(){}								// 問題ない。 gen.cpp で利用される。

	UFUNCTION(NetMulticast="NetMulticastTest_Implementation2")
	void NetMulticastTest();
	void NetMulticastTest_Implementation2(){}						// 無意味。gen.cpp では NetMulticastTest_Implementation() が利用される

	UFUNCTION(BlueprintNativeEvent="CalledFromCpp_Implementation2")
	void CalledFromCpp();
	void CalledFromCpp_Implementation2(){}							// 無意味。gen.cpp では CalledFromCpp_Implementation() が利用される
//...
};
```


----
## あとがき

頭の整理のためにまとめておきました。
どなたかの参考になれば幸いです。

ここまで読んでいただきありがとうございました！


----
## 参考リンク

* 関数指定子の説明
	* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > UFunction](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Functions/index.html)
* `BlueprintNativeEvent` の説明
	* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > プログラミング ガイド > UE4 の C++ プログラミング入門](https://docs.unrealengine.com/ja/ProgrammingAndScripting/ProgrammingWithCPP/IntroductionToCPP/index.html)
	* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > インターフェース](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Interfaces/index.html)
* `RPC` の説明
	* [Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > マルチプレイヤー プログラミングのクイック スタート ガイド](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/QuickStart/index.html)
	* [Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > ネットワーキングの概要](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/Overview/index.html)
* `_Implementation()` 関数の名前入指定の説明
	* [Unreal Engine 4 ドキュメント > 新機能 > リリースノート > Unreal Engine 4.8 リリースノート](https://docs.unrealengine.com/ja/WhatsNew/Builds/ReleaseNotes/2015/4_8/index.html)


----
おしまい。
