# 【UE4】関数指定子、とくに RPC に関わるものについて

## はじめに
### 環境

| | |
| ---- | ---- |
| UE4 バージョン | 4.26.1 |
| Visual Studio | 2017 |

### この記事は何？
関数指定子、とくに RPC に関わるものについてをまとめたものです。

ほとんど公式ドキュメントからの引用であり、特に情報がまばらになっていると感じた部分を中心にまとめています。


### 想定している読者
* UE C++ の初心者
* RPC したい人


## FunctionSpecifiers
`FunctionSpecifiers` （関数指定子）
[Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > UFunction > 関数指定子](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Functions/Specifiers/index.html)

ドキュメントより一部引用 :

| 関数指定子     | 効果                                                                                                                                                                                                                                                                |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| NetMulticast   | この関数は、アクタの NetOwner に関わらず、サーバー上でローカルで実行、および全てのクライアントにレプリケートされます。                                                                                                                                              |
| Reliable       | この関数はネットワーク上でレプリケートされ、帯域幅やネットワーク エラーに関係なく届くことが保証されます。Client または Server と併用時のみ有効です。                                                                                                                |
| Unreliable     | この関数はネットワーク上でレプリケートされますが、帯域幅の制約やネットワーク エラーが原因で失敗することがあります。Client または Server と併用時のみ有効です。                                                                                                      |
| WithValidation | メインの関数と同じ名前の関数を追加で宣言しますが、最後に _Validate が付加されます。この関数は同じパラメータを取り、`bool`を戻して、メイン関数への呼び出しを続行するかどうかを示します。                                                                             |
| Server         | この関数はサーバー上でのみ実行されます。メインの関数と同じ名前の関数を追加で宣言しますが、最後に _Implementation が付加されます。これは、どこにコードが書き込まれるかを示しています。自動生成されたコードは、必要に応じて、_Implementation メソッドを呼び出します。 |
| Client         | この関数は、関数が呼び出されるオブジェクトを所有するクライアント上でのみ実行されます。メインの関数と同じ名前の関数を追加で宣言しますが、最後に _Implementation が付加されます。自動生成されたコードは、必要に応じて、_Implementation メソッドを呼び出します。       |


### FunctionSpecifiers._Implementation
`NetMulticast` の説明で、 `_Implementation` について言及されていませんが、 `Server` / `Client` と同様の仕組みです。

別のドキュメントで説明されています。

[Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > ネットワーキングの概要](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/Overview/index.html)
> C++ で関数を RPC として指定するには、UFUNCTION マクロで Server、Client、NetMulticast のいずれかの指定子を指定します。
> それらのコード実装では、_Implementation サフィックスを使用します。

日本語訳が微妙なので翻訳元の方も載せます。

[Unreal Engine 4 Documentation > Making Interactive Experiences > Networking and Multiplayer > Networking Overview](https://docs.unrealengine.com/en-US/InteractiveExperiences/Networking/Overview/index.html)
> You can designate a function in C++ as being an RPC by providing either the Server, Client, or NetMulticast specificer in its UFUNCTION macro. 
> Their implementations use the suffix _Implementation in their code implementations.
> C++ では、 UFINCTION マクロに Server 、 Client 、 NetMulticast のいずれかの指定子を与えることで、関数を RPC として指定することが出来ます。
> これらの実装では、コードの実装に _Implementation というサフィックスが使わていれます。


### FunctionSpecifiers.Reliability
`Reliable` / `Unreliable` の説明で、 `NetMulticast` について言及されていませんが、同様に必須です。

別のドキュメントで説明されています。

[Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > ネットワーキングの概要](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/Overview/index.html)
> 信頼性
> RPC は「信頼できる」または「信頼できない」として指定する必要があります。
> デフォルトでは、ブループリントでの関数およびイベントは「信頼できない」と見なされます。
> 関数を「信頼できる」に設定するには、[Details (詳細)] パネルで [Reliable (信頼できる)] 設定を true に設定します。
> C++ では、RPC の UFUNCTION マクロに Reliable または Unreliable のいずれかの指定子を追加して、そのステータスを Server、Client、NetMulticast のいずれかに指定します。

日本語訳が微妙なので翻訳元の方も載せます。

[Unreal Engine 4 Documentation > Making Interactive Experiences > Networking and Multiplayer > Networking Overview](https://docs.unrealengine.com/en-US/InteractiveExperiences/Networking/Overview/index.html)

> Reliability
> You must designate RPCs as being reliable or unreliable. 
> In Blueprint, functions and events are assumed to be unreliable by default. 
> By setting the Reliable setting in the Details Panel to true, you can designate the function as being reliable. 
> In C++, you must add either the Reliable or Unreliable specifier to any RPC's UFUNCTION macro alongside its status as a Server, Client, or NetMulticast function.
> 信頼性
> RPC を「信頼できる」または「信頼できない」として指定する必要があります。
> ブループリントでは、関数やイベントはデフォルトで「信頼できない」とみなされます。
> [Details (詳細)] パネルの [Reliable (信頼できる)] を true にすることで、関数を「信頼できる」ものとして指定することが出来ます。
> C++ では、任意の RPC の UFUNCTION マクロに、 Server 、 Client 、 NetMulticast 関数としてのステータスと一緒に Reliable または Unreliable の指定子を追加する必要があります。


### FunctionSpecifiers.NetMulticast
* 利用する場合 :
	* Reliable/Unreliable のどちらかの指定をしないとエラーとなります。
	* _Implementation() を宣言/定義しないとエラーとなります。
	* メインの関数は自動生成されるため、独自で定義するとエラーとなります。

```c++
// 例。簡略化のために定義をインラインで書いている。
UCLASS()
class SAMPLE_API ASampleCharacter : public ACharacter
{
//...

	UFUNCTION(NetMulticast)
	void NetMulticastTestError00();						//エラー。 Reliable/Unreliable の指定がない。どちらかの指定をする必要がある。

	UFUNCTION(NetMulticast, Reliable)
	void NetMulticastTestError01();						//エラー。 _Implementation() の宣言/定義がない。 _Implementation() を宣言/定義する必要がある。

	UFUNCTION(NetMulticast, Reliable)
	void NetMulticastTestError02(){};					//エラー。 メインの関数の定義がある。 メインの関数は自動生成されるため、定義しない必要がある。
	void NetMulticastTestError02_Implementation(){};

	UFUNCTION(NetMulticast, Reliable)
	void NetMulticastTestError03();
	void NetMulticastTestError03_Implementation();		//エラー。 _Implementation() 関数の定義がない。 _Implementation() を定義する必要がある。

	UFUNCTION(NetMulticast, Reliable)
	void NetMulticastTestOk();							//問題なし。 メインの関数の宣言だけしている。
	void NetMulticastTestOk_Implementation(){};			//問題なし。 _Implementation() 関数の宣言/定義をしている。

//...
};
```

### FunctionSpecifiers.Server
[Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > アクタのレプリケーション > RPC について](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/Actors/RPCs/index.html)
> 最近、UHT に変更が加えられ、 クライアント-> サーバー RPC が _Validate 関数を持つことを必要としています。
> これは、安全なサーバー RPC 関数を促すためであり、可能な限り簡単にコードを追加、チェックし、 すべてのパラメータが既知の入力の制約に対して有効になるようにしました。

**最近** とはいつの事でしょうか？
`Server` は `WithValidation` が必須、のように読めますが、 `4.26.1` では指定しなくともエラーは出ません。

```c++
// 例。簡略化のために定義をインラインで書いている。
UCLASS()
class SAMPLE_API ASampleCharacter : public ACharacter
{
//...

	UFUNCTION(Server, Reliable)
	void ServerTestError01(int32 value);				// 問題なし。 WithValidation 無しでもエラーは出ません。
	void ServerTestError01_Implementation(int32 value) {}

	UFUNCTION(Server, Reliable, WithValidation)
	void ServerTestOK(int32 value);						// 問題なし。
	void ServerTestOK_Implementation(int32 value) {}
	bool ServerTestOK_Validate(int32 value) { return true; }

//...
};
```

[Unreal Engine 4.23 リリース ノート](https://docs.unrealengine.com/ja/WhatsNew/Builds/ReleaseNotes/4_23/index.html)
> New: Made the WithValidation tag for server RPCs optional.
> New: Server RPC の WithValidation タグをオプションにしました。

おそらく、 `4.23` の時点で、必須ではなくなっているようです。
`Answers` や `Forums` の過去のやり取りからの想像ですが、コンシューマ機やアーケード機などのチート対策が不要なケースであっても、すべての `Server RPC` に `Validate` 関数が必須となることが不評だったようです。


## あとがき

ドキュメントは１つのだけでなく全体を見ていく必要があることや、日本語訳が微妙なケースは翻訳元を参照する必要があることがわかると思います。
どなたかの参考になれば幸いです。

ここまで読んでいただきありがとうございました！

----
## 参考リンク

* [Unreal Engine 4 ドキュメント > プログラミングとスクリプト処理 > ゲームプレイのアーキテクチャ > UFunction > 関数指定子](https://docs.unrealengine.com/ja/ProgrammingAndScripting/GameplayArchitecture/Functions/Specifiers/index.html)
* [Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > アクタのレプリケーション > RPC について](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/Actors/RPCs/index.html)
* [Unreal Engine 4 ドキュメント > インタラクティブな体験をつくりだす > ネットワークの構築とマルチプレイヤー > ネットワーキングの概要](https://docs.unrealengine.com/ja/InteractiveExperiences/Networking/Overview/index.html)
* [Unreal Engine 4 Documentation > Making Interactive Experiences > Networking and Multiplayer > Networking Overview](https://docs.unrealengine.com/en-US/InteractiveExperiences/Networking/Overview/index.html)
* [Unreal Engine 4.23 リリース ノート](https://docs.unrealengine.com/ja/WhatsNew/Builds/ReleaseNotes/4_23/index.html)


----
おしまい。
