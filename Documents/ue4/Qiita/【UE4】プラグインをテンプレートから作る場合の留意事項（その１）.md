# 【UE4】プラグインをテンプレートから作る場合の留意事項（その１）

## ■はじめに

### ●この記事は何？

UE4 は C++ を利用して様々なことが出来ます。
定番だとブループリントクラスの基底クラスを C++ で実装することでしょう。
上級者だとエンジン自体に手を入れることもあるでしょう。
また、エディタの利便性向上のためプラグインを作成しエディタを拡張することもあるでしょう。

この記事は一番最後の「プラグインによるエディタの拡張」に関する内容となります。

具体的には、
***「Editor Standalone Window」テンプレートから新規作成したプラグインをアンロードした後に「Window」メニューを開くとハングアップする、***
という問題について、直接的な原因と対処方法を纏めたものです。

### ●直接的な原因と対処方法？

結論から書いておきますが、モジュールのアンロード時に破棄したクラスへのダングリングポインタをメニュー構築クラスが保持しており、
メニューを開いた際に行われるアクセスが原因でハングアップしています。
そこを対処できればハングアップは発生しなくなります。

### ●環境

| ツール名 | バージョン |
| ---- | ---- |
| UE4 | 4.24.2 |
| Visual Studio | Community 2017 |

* 記事内の UE4 Editor のメニュー項目名は言語設定が English 状態の内容となっています。
* 必要であれば言語設定を変更しておいてください。
	* 「エディタの環境設定 > 国際化 > 言語設定」を「English」に変更

### ●想定している読者

* エディタ拡張初心者
* プラグイン作成初心者
* C++ が使える方

## ■プラグイン作成の導入部分

詳細については割愛します。
ヒストリア様のブログが詳しいのでそちらを参照ください。

* 「プラグイン」に関する参考リンク
	* 公式ドキュメント
		* [プラグイン:](https://docs.unrealengine.com/ja/Programming/Plugins/index.html)
	* ヒストリア様のサイトへのリンク
		* [[UE4] プラグインによるエディタ拡張(1)　空のプラグインを追加する](http://historia.co.jp/archives/367/)
		* [[UE4] プラグインによるエディタ拡張(2)　エディタのメニューに項目を追加する](http://historia.co.jp/archives/370/)
		* [[UE4] プラグインによるエディタ拡張(3)　SlateUIを使用してウィンドウを作成する](http://historia.co.jp/archives/373/)
		* [[UE4] プラグインによるエディタ拡張(4)　自作ツールに画像を利用する](http://historia.co.jp/archives/476/)

## ■テンプレートを利用したプラグインの下準備

ここからは実際の例も交えていきます。
まずは新規のプラグインを用意します。

1. 「Edit」メニューから「Plugins」を選択し、「Plugins」ウィンドウを表示します。
1. 「Plugins」ウィンドウの「New Plugin」ボタンを押します。
1. 「New Plugin」ウィンドウで任意の設定をします。
	* ここでは説明の為、以下の設定をします。
		* テンプレートは「Editor Standalone Window」を利用します。
		* 名前を「Editor Standalone Window」の頭文字から「ESWSample」とします。
	* 設定が済んだら「Create Plugin」ボタンを押します。
		* テンプレートからコードが自動生成され、 Visual Studio のプロジェクトファイルが更新されます。
1. プラグインをメニューやツールバーに反映させるためエディタを立ち上げ直します。
	* エディタに以下の様な変化があります。
		* 「Window」メニューに「ESWSample」 が追加
		* ツールバーに「ESWSample」 ボタンが追加
	* 選択することで「ESWSample」タブを含んだウィンドウが表示されます。

## ■ホットリロードについて

UE4 のプラグインにはホットリロードの仕組みがあります。

* 「Modules」タブ
	* 「Window」メニュー > 「Developer Tools」 > 「Modules」を選ぶと「Modules」タブが表示されます。
	* 「Modules」タブにはエディタが認識しているモジュールの一覧が表示されます。
	* モジュール毎に「Load」「Unload」「Reload」「Recompile」が実行できます。
	* 検索ボックスで表示するモジュールにフィルターを掛けることが出来ます。
		* 先ほど作成した「ESWSample」を入力するとモジュールが認識されていることが確認できます。

これらを使うことで、エディタを立ち上げたままモジュールを修正し、再ロードが可能です。

## ■モジュールのアンロード後の問題について

### ●手順と発生する問題

* 手順
	1. 「ESWSample」プラグインを用意する。
	1. エディタを起動し、「ESWSample」プラグインがロードされた状態にする
	1. 「Window」メニュー ＞ 「ESWSample」を選択し、「ESWSample」タブを表示する。
	1. 「Modules」タブで「ESWSample」プラグインの「Unload」ボタンを押し、アンロードする。
	1. 「Window」メニューを開く。
* 発生する問題
	1. 「ESWSample」タブが残る。
	1. ツールバーに生成したボタンが、テキストのみのボタンになる（アイコンだけ消える）。
	1. エディタがハングアップする。

### ●それぞれの問題について簡単な解説

* 「ESWSample」タブが残る。
	* 手順 4. の時点で発生します。
	* メニューやボタンに登録した処理内でタブを構築していますが、これを破棄していない為に残っています。
* ツールバーに生成したボタンが、テキストのみのボタンになる（アイコンだけ消える）。
	* 手順 4. の時点で発生します。
	* アイコンはアンロードされる（スタイルが破棄される）ために消えます。
	* ボタンが残るのはボタンの破棄処理を行っていないためです。
* エディタがハングアップする。
	* 手順 5. の時点で発生します。
	* メニューの拡張処理として登録したデリゲート処理内でダングリングポインタへアクセスしているのが原因です。

> **Technical Note:もう少し正確に**
> 実際にハングアップするのは以下のような理由です。
> 
> * メニュー構築クラスに登録されたデリゲート内にてシングルトンクラス　```FESWSampleCommands``` に対してアクセスしている。
> * その際、```FESWSampleCommands``` が破棄されているか確認していない。
> * モジュールアンロード後は ```FESWSampleCommands``` が破棄されている。
> * その状態で ```FESWSampleCommands::Get()``` を呼び出している。
> * ```FESWSampleCommands::Get()``` 内は以下の流れ。
> 	* 参照カウントがゼロのウィークポインタに対し ```Pin()``` を呼び出して空のシェアードポインタを生成
> 	* 空のシェアードポインタに対し ```operator*``` を呼び出し
> 	* ```check( IsValid() )``` に引っかかりアサーション発生
> 
> デリゲートとしては ```FESWSampleModule``` へのポインタと ```FESWSampleModule``` の非仮想メンバ関数が指定されています。
> また、指定された関数内では自身のメンバにアクセスしていません。
> その為、```FESWSampleModule``` が破棄された後ではありますが、メンバ関数が呼び出された段階ではハングアップしていません。
> ただ、アンロード済みのモジュール内の関数へアクセスしている、という悪い状態です。
> この記事ではダングリングポインタを解消し、そもそも関数にアクセスされないようにする形で纏めています。

この記事ではエディタのハングアップについてのみ扱います。
残りの２つの問題については[【UE4】プラグインをテンプレートから作る場合の留意事項（その２）]で扱います。

## ■対処方法

### ●方針

```ESWSample.cpp``` の中で ```this``` からデリゲートを作っているコードが４箇所あります。
ハングアップの直接的な問題となっているのは１箇所ですが、４箇所ともシェアードポインタを利用するように変更します。

### ●デリゲートで使用するクラスの用意

```FESWSampleModule``` は ```IModuleInterface``` 派生クラスであり ```UObject``` 派生ではありません。
その為、 ```FESWSampleModule``` 自体をシェアードポインタにはし難いです。
そこで、デリゲートの処理のみを行う小さいクラス```FESWSampleImpl```を用意し、 
```FESWSampleModule``` にシェアードポインタで持たせる形にします。
```PluginCommands``` の次辺りで良いでしょう。

```cpp:ESWSample.h
//省略...
class FESWSampleModule : public IModuleInterface
{
//省略...
	TSharedPtr<class FUICommandList> PluginCommands;
	TSharedPtr<class FESWSampleImpl> Impl; //これを追加
};
//省略...
```

```class FESWSampleImpl``` の実装です。
```class FESWSampleModule``` 内にあったデリゲートに登録されている関数をそのまま持ってきています。
ここでは対処方法の説明のため、 ```ESWSample.cpp``` の ```FESWSampleModule::StartupModule()``` の前に書いています。
実際にプラグイン作成する場合はファイルを分けたほうが良いでしょう。

```cpp:ESWSample.cpp
//省略...
class FESWSampleImpl
{
public:
	void PluginButtonClicked()
	{
		FGlobalTabmanager::Get()->InvokeTab(ESWSampleTabName);
	}
	TSharedRef<SDockTab> OnSpawnPluginTab(const FSpawnTabArgs& SpawnTabArgs)
	{
		return SNew(SDockTab)
			.TabRole(ETabRole::NomadTab)
			[
				// Put your tab content here!
				SNew(SBox)
				.HAlign(HAlign_Center)
				.VAlign(VAlign_Center)
				[
					SNew(STextBlock)
					.Text(WidgetText)
				]
			];
	}
	void AddMenuExtension(FMenuBuilder& Builder)
	{
		Builder.AddMenuEntry(FESWSampleCommands::Get().OpenPluginWindow);
	}
	void AddToolbarExtension(FToolBarBuilder& Builder)
	{
		Builder.AddToolBarButton(FESWSampleCommands::Get().OpenPluginWindow);
	}
};
//省略...
```

モジュールの初期化時に```class FESWSampleImpl``` を ```new``` します。
```PluginCommands``` の ```new``` の次辺りで良いでしょう。

```cpp:ESWSample.cpp
//...省略
void FESWSampleModule::StartupModule()
{
//...省略
	PluginCommands = MakeShareable(new FUICommandList);
	Impl = MakeShareable(new FESWSampleImpl); //これを追加
//...省略
}
//...省略
```

モジュールの破棄時に```class FESWSampleImpl``` を ```delete``` します。
```FESWSampleModule::ShutdownModule()``` の先頭辺りで良いでしょう。
```PluginCommands``` も併せて ```delete``` しておきます。（ハングアップとの関連性は特にないです）

```cpp:ESWSample.cpp
//...省略
void FESWSampleModule::ShutdownModule()
{
	// This function may be called during shutdown to clean up your module.  For modules that support dynamic reloading,
	// we call this function before unloading the module.
	Impl.Reset(); //これを追加
	PluginCommands.Reset(); //これを追加
//...省略
}
//...省略
```

> **Technical Note:```PluginCommands``` を ```delete``` しなくてもハングアップに影響しない理由**
> 前述のとおり、ハングアップの直接的な原因はダングリングポインタへのアクセスですが、 ```PluginCommands``` 自体はその問題に絡んでいません。
> また、 ここで delete しなくとも、直後に ```FESWSampleModule``` 自体が ```delete``` されます。
> その為、（破棄処理が多少前後しますが）挙動には影響しません。
>> ```IModuleInterface::ShutdownModule()``` は ```FModuleManager::AbandonModule()``` 等から呼び出されますが、
>> 直後に ```IModuleInterface``` 派生クラスを ```delete``` しています。
>> ですので、 ***```FModuleManager``` の実装が変更されなければ*** 挙動に影響はしません。
>> ```IModuleInterface::ShutdownModule()``` には以下のようなコメントが書かれています。
>>> Called before the module is unloaded, right before the module object is destroyed.
>> 
>> ですので、実装が変更される可能性は低いです。
>
> ```StartupModule()``` と ```ShutdownModule()``` は対の関数であり、前者の中で確保したリソースは後者の中で開放したほうが自然と考えられますので、
> ここではそのように変更しています。


ここまででデリゲート作成時に使用するクラスの準備ができました。
次にデリゲート作成方法の変更をします。

### ●デリゲートの作成方法の変更

４箇所ありますが纏めています。
変更方法は全て同じで以下のとおりです。

| デリゲート生成関数 | 変更前 | 変更後 |
| ----- | ----- | ----- |
| デリゲート生成関数 | CreateRaw | CreateSP |
| 第１引数 | this | Impl.ToSharedRef() |
| 第２引数 | &FESWSampleModule::FunctionName | &FESWSampleImpl::FunctionName |

```cpp:ESWSample.cpp
//...省略
void FESWSampleModule::StartupModule()
{
//...省略
#if 0 //変更前
	PluginCommands->MapAction(
		FESWSampleCommands::Get().OpenPluginWindow,
		FExecuteAction::CreateRaw(this, &FESWSampleModule::PluginButtonClicked),
		FCanExecuteAction());
#else //変更後
	PluginCommands->MapAction(
		FESWSampleCommands::Get().OpenPluginWindow,
		FExecuteAction::CreateSP(Impl.ToSharedRef(), &FESWSampleImpl::PluginButtonClicked),
		FCanExecuteAction());
#endif
//...省略
#if 0 //変更前
		MenuExtender->AddMenuExtension("WindowLayout", EExtensionHook::After, PluginCommands, FMenuExtensionDelegate::CreateRaw(this, &FESWSampleModule::AddMenuExtension));
#else //変更後
		MenuExtender->AddMenuExtension("WindowLayout", EExtensionHook::After, PluginCommands, FMenuExtensionDelegate::CreateSP(Impl.ToSharedRef(), &FESWSampleImpl::AddMenuExtension));
#endif
//...省略
#if 0 //変更前
		ToolbarExtender->AddToolBarExtension("Settings", EExtensionHook::After, PluginCommands, FToolBarExtensionDelegate::CreateRaw(this, &FESWSampleModule::AddToolbarExtension));
#else //変更後
		ToolbarExtender->AddToolBarExtension("Settings", EExtensionHook::After, PluginCommands, FToolBarExtensionDelegate::CreateSP(Impl.ToSharedRef(), &FESWSampleImpl::AddToolbarExtension));
#endif
//...省略
#if 0 //変更前
	FGlobalTabmanager::Get()->RegisterNomadTabSpawner(ESWSampleTabName, FOnSpawnTab::CreateRaw(this, &FESWSampleModule::OnSpawnPluginTab))
		.SetDisplayName(LOCTEXT("FESWSampleTabTitle", "ESWSample"))
		.SetMenuType(ETabSpawnerMenuType::Hidden);
#else //変更後
	FGlobalTabmanager::Get()->RegisterNomadTabSpawner(ESWSampleTabName, FOnSpawnTab::CreateSP(Impl.ToSharedRef(), &FESWSampleImpl::OnSpawnPluginTab))
		.SetDisplayName(LOCTEXT("FESWSampleTabTitle", "ESWSample"))
		.SetMenuType(ETabSpawnerMenuType::Hidden);
#endif
//...省略
}
//...省略
```

以上で変更箇所は終了です。
```class FESWSampleModule``` に残っているデリゲート用の関数群は呼ばれなくなるので消してしまっても良いです。

## ■結果

アンロード後に「Window」メニューを開いてもハングアップしなくなりました。

## ■あとがき

そもそも今回変更したあたりは、自前のプラグインを作る際に大幅に変える部分でもあります。
アンロードを試さなければ気づかない間に問題ないように修正してしまうケースもあるでしょう。

ですが、例えばプラグイン作成に初挑戦しようと UE4 のコードを触り始めた方がこの問題に出会ってしまうと、
本来作りたかった機能に着手する前に結構な労力を取られてしまいかねないと考え、この記事をまとめました。
どなたかの参考になれば幸いです。

ここまで読んでいただきありがとうございました！

## ■もう少し突っ込んだ話

でもでも、それっておかしくね？
そもそも、登録したデリゲート残りっぱなしってことだよね？

・・・と思った方、
挙動を理解していて対処ができるのであれば、それは仕様として認めてしまうのも１つの方法です。

現実的にも、モジュールのアンロードを行うのはプラグイン開発者ぐらいですので、
「実行バイナリに影響しない、かつエディタのモジュールのアンロード時にしか発生しない、開放されていないオブジェクトを減らす作業」
に割ける予算があるか考えてみてください。

それでも納得できない方は[【UE4】プラグインをテンプレートから作る場合の留意事項（その５）]で扱っていますのでそちらへどうぞ。このシリーズで一番重い記事です。

## ■関連記事

* [【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その２）]
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その３）]
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その４）]
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その５）]

[【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]:https://qiita.com/sentyaanko/items/23b0919af4b6fabd8378
[【UE4】プラグインをテンプレートから作る場合の留意事項（その２）]:https://qiita.com/sentyaanko/items/a639dc9b2e56690ca9f2
[【UE4】プラグインをテンプレートから作る場合の留意事項（その３）]:https://qiita.com/sentyaanko/items/6b13158a71c2a83d9296
[【UE4】プラグインをテンプレートから作る場合の留意事項（その４）]:https://qiita.com/sentyaanko/items/4874f092b764ac213ba6
[【UE4】プラグインをテンプレートから作る場合の留意事項（その５）]:https://qiita.com/sentyaanko/items/e44b146b7cbc8ce46be7
[その１]:https://qiita.com/sentyaanko/items/23b0919af4b6fabd8378
[その２]:https://qiita.com/sentyaanko/items/a639dc9b2e56690ca9f2
[その３]:https://qiita.com/sentyaanko/items/6b13158a71c2a83d9296
[その４]:https://qiita.com/sentyaanko/items/4874f092b764ac213ba6
[その５]:https://qiita.com/sentyaanko/items/e44b146b7cbc8ce46be7

----
おしまい。
