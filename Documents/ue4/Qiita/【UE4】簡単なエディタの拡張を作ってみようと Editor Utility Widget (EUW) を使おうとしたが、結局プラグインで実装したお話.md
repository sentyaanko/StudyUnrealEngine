# 【UE4】マテリアルエディタ拡張サンプル


## ■はじめに
### ●環境

| | |
| ---- | ---- |
| UE4 バージョン | 4.24.2 |
| Internationalization > Editor Language<br>国際化 > 言語設定 |  English |

### ●この記事は何？
この記事は、プラグインによるマテリアルエディタの拡張方法とそのサンプルをまとめたものです。

簡単なエディタの拡張を作ってみようと Editor Utility Widget (EUW) を使おうとしましたが、
利用できずにプラグインと C++ で実装した際の情報となります。
EUW を利用できなかった理由と、プラグイン作成の導入部分までをまとめています。
これからマテリアルエディタ拡張を考えている方の参考になれば幸いです。

### ●想定している読者
* EUW 初心者
* Slate 初心者
* エディタ拡張初心者
* プラグイン作成初心者
* C++ が使える方
* レベルエディタではなく、 マテリアルエディタ等の拡張を考えている方

> **Note:レベルエディタとは？**
> ここでは「.uproject ファイルを開いた際に表示されるウィンドウ」を指しています。
> 説明のしやすさからレベルエディタ・マテリアルエディタ、と対称になるようそう呼んでいます。
> **（注：公式ドキュメントが指す「レベルエディタ」と同じ（はず）です。）**

### ●扱わない項目
* EUW の詳細な説明
* Slate の詳細な説明

### ●「Editor Utility Widget (EUW)」とは？
<!-- textlint-disable -->

> 公式からの引用
> > Editor Utility Widgets は、 Unreal Motion Graphics (UMG) をベースにしているので、他の UMG ウィジェット ブループリントと同じように、ウィジェットをブループリントで設定することができます。

<!-- textlint-enable -->

以降、引用以外では「EUW」と記します。

+ 「EUW」に関する参考リンク
	+ 公式ドキュメント
		+ [Editor Utility Widget](https://docs.unrealengine.com/ja/Engine/UMG/UserGuide/EditorUtilityWidgets/index.html)
	+ Qiita @EGJ-Kaz_Okada
		+ [[UE4]エディタ上で動作するツール・エディタ拡張をUMGで簡単に作れる Editor Utility Widget について](https://qiita.com/EGJ-Kaz_Okada/items/9f530db3b53d0fde3f20)

### ●「Slate」とは？
> 公式からの引用
> > スレート は完全にカスタマイズ可能でプラットフォームに依存しない UI フレームワーク

+ 「Slate」に関する参考リンク
	+ 公式ドキュメント
		+ [スレートの概要](https://docs.unrealengine.com/ja/Programming/Slate/Overview/index.html)

## ■EUW を利用できなかった理由
EUW で作れるのはレベルエディタにドッキング可能なウィンドウです。
今回、私が作ろうとしているのはマテリアルを開いた際に表示されるマテリアルエディタにある「Find Results」タブのようなものです。
「レベルエディタ以外にのみドッキングさせたい」「ウィンドウ毎に別の実体をもたせたい」といったケースでは EUW は利用することが出来ません。
そういった場合は、プラグインを C++ を使って作る必要があります。

## ■プラグイン作成の導入部分
ここでは割愛します。
ヒストリア様のブログが詳しいのでそちらを参照ください。

+ 「プラグイン」「Slate」に関する参考リンク
	+ 公式ドキュメント
		+ [プラグイン:](https://docs.unrealengine.com/ja/Programming/Plugins/index.html)
		+ [スレート UI フレームワーク](https://docs.unrealengine.com/ja/Programming/Slate/index.html)
	+ ヒストリア様のサイトへのリンク
		+ [[UE4] プラグインによるエディタ拡張(1)　空のプラグインを追加する](http://historia.co.jp/archives/367/)
		+ [[UE4] プラグインによるエディタ拡張(2)　エディタのメニューに項目を追加する](http://historia.co.jp/archives/370/)
		+ [[UE4] プラグインによるエディタ拡張(3)　SlateUIを使用してウィンドウを作成する](http://historia.co.jp/archives/373/)
		+ [[UE4] プラグインによるエディタ拡張(4)　自作ツールに画像を利用する](http://historia.co.jp/archives/476/)

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
1. プラグインを反映させるためエディタを立ち上げ直します。
	+ エディタに以下の様な変化があります。
		+ ツールバーに「ESWSample」 ボタンが追加
		+ 「Window」メニューに「ESWSample」 が追加
	+ 選択することで「ESWSample」タブを含んだウィンドウが表示されます。

ここまでの手順で「ESWSample」タブを作ることが出来ます。
このタブはレベルエディタだけでなくマテリアルエディタにもドッキング可能です。
ですがひとつだけしか表示されないタブです。
マテリアルエディタの「Find Results」タブのように、マテリアルエディタ専用のタブをマテリアルエディタ毎に作る場合はコードの変更が必要です。

## ■タブの生成タイミングの変更
### ●現在のコードの確認

```cpp:ESWSample.cpp
void FESWSampleModule::StartupModule()
{
//...省略
	PluginCommands = MakeShareable(new FUICommandList);

	PluginCommands->MapAction(
		FESWSampleCommands::Get().OpenPluginWindow,
		FExecuteAction::CreateRaw(this, &FESWSampleModule::PluginButtonClicked),
		FCanExecuteAction());
		
	FLevelEditorModule& LevelEditorModule = FModuleManager::LoadModuleChecked<FLevelEditorModule>("LevelEditor");
	
	{
		TSharedPtr<FExtender> MenuExtender = MakeShareable(new FExtender());
		MenuExtender->AddMenuExtension("WindowLayout", EExtensionHook::After, PluginCommands, FMenuExtensionDelegate::CreateRaw(this, &FESWSampleModule::AddMenuExtension));

		LevelEditorModule.GetMenuExtensibilityManager()->AddExtender(MenuExtender);
	}
	
	{
		TSharedPtr<FExtender> ToolbarExtender = MakeShareable(new FExtender);
		ToolbarExtender->AddToolBarExtension("Settings", EExtensionHook::After, PluginCommands, FToolBarExtensionDelegate::CreateRaw(this, &FESWSampleModule::AddToolbarExtension));
		
		LevelEditorModule.GetToolBarExtensibilityManager()->AddExtender(ToolbarExtender);
	}
	
	FGlobalTabmanager::Get()->RegisterNomadTabSpawner(ESWSampleTabName, FOnSpawnTab::CreateRaw(this, &FESWSampleModule::OnSpawnPluginTab))
		.SetDisplayName(LOCTEXT("FESWSampleTabTitle", "ESWSample"))
		.SetMenuType(ETabSpawnerMenuType::Hidden);
}
```

「ESWSample」モジュールの初期化の際に呼ばれる関数です。

* 「```FLevelEditorModule```」のメニューとツールバーに項目を追加しています。
* 「```FGlobalTabmanager```」の ```TabSpawner``` にタブの初期化関数を登録しています。

これらの登録先をマテリアルエディタに変更すればよさそうです。

### ●変更方法の調査の一例
どのように変更すればマテリアルエディタのみにドッキング可能なウィンドウを実現できるのか、その調査方法の一例です。
マテリアルエディタ以外を拡張したい場合の手順の参考にしてください。

今回は、目的の挙動はマテリアルエディタの中にある「Find Results」タブと同様なため、
該当のソースを探し、実装方法を確認してみます。
ここでは「Widget Reflector」を使って探します。

+ 「Widget Reflector」に関する参考リンク
	+ Qiita @EGJ-Ken_Kuwano
		+ [[UE4] Widget Reflectorを使ってリソースや設定を調べよう](https://qiita.com/EGJ-Ken_Kuwano/items/523c97697563751bcc71)

手順は以下のような流れになります。

1. 「Widget Reflector」を利用して該当のソースを探す。
	1. 「Content Browser」から適当なマテリアルを開き、マテリアルエディタを表示します。
	1. マテリアルエディタのツールバーの「Search」ボタンを押し、「Find Results」タブを表示します。
	1. レベルエディタの「Window」メニュー > 「Developer Tools」 > 「Widget Reflector」を選び、「Widget Reflector」ウィンドウを表示します。
	1. 「Widget Reflector」ウィンドウの「Pick Painted Widgets」ボタンを押します。
	1. 「Find Results」タブにマウスカーソルを合わせたら Esc キーを押します。
	1. 「Widget Reflector」ウィンドウを確認すると、ウィジェットのいくつかが「FindInMaterial.cpp」で作られていることが確認できます。
1. 「FindInMaterial.cpp」のソースからつくりを調べる。
	1. 「FindInMaterial.h」を見ると ```SFindInMaterial``` は ```SCompoundWidget``` の派生クラスなのでウィジェットであることがわかります。
	1. 「```SFindInMaterial```」で検索すると「```FMaterialEditor::CreateInternalWidgets()```」で構築している事がわかります。
		+ 呼び出し元
			1. 「```FMaterialEditor::CreateInternalWidgets()```」の呼び出し元を探すと「```FMaterialEditor::InitMaterialEditor()```」が見つかります。
			1. 「```FMaterialEditor::InitMaterialEditor()```」の呼び出し元を探すと「```FMaterialEditorModule::CreateMaterialEditor()```」が見つかります。
			1. 「```FMaterialEditorModule::CreateMaterialEditor()```」の呼び出し元を探すと「```FAssetTypeActions_MaterialFunction::OpenAssetEditor()```」・「```FAssetTypeActions_Material::OpenAssetEditor()```」が見つかります。
			+ **よって、「```FMaterialEditor::CreateInternalWidgets()```」はマテリアルやマテリアルファンクションを開いた際に呼び出されることがわかります。**
		+ 構築された「```SFindInMaterial```」の利用箇所
			+ 「```FMaterialEditor::CreateInternalWidgets()```」では「```FMaterialEditor::FindResults```」メンバとして保持しているだけでタブとしてはスポーンしていないこともわかります。
			+ 「```FMaterialEditor::FindResults```」メンバの利用箇所を確認すると「```FMaterialEditor::SpawnTab_Find()```」でスポーンさせていることもわかります。
			+ 「```FMaterialEditor::SpawnTab_Find()```」の呼び出し元を探すと「```FMaterialEditor::RegisterTabSpawners()```」にて「```FTabManager::RegisterTabSpawner()```」を呼び出しスポーンの登録をしていることもわかります。
			+ さらに「```FMaterialEditor::RegisterTabSpawners()```」では「```OnRegisterTabSpawners().Broadcast(InTabManager)```」を呼び出していることがわかります。
			+ **よって、ユーザーは「```IMaterialEditorModule::OnRegisterTabSpawners()```」を利用して任意のウィジェットのスポーン登録ができることがわかります。**

このようにコードを追っていくと、なんやかんやあって最終的にやらなければいけないことを調べていくことが可能です。
以下にその一部をあげます。

* 「```IMaterialEditorModule::OnMaterialEditorOpened()```」にマテリアルエディタが開いた時の独自のイベント処理を登録
* 「```IMaterialEditorModule::OnMaterialFunctionEditorOpened()```」にマテリアルファンクションエディタが開いた時の独自のイベント処理を登録
* 「```IMaterialEditor::OnMaterialEditorClosed()```」にマテリアルエディタが閉じた時の独自のイベント処理を登録
* マテリアルエディタはレベルエディタとは異なり、複数開く可能性があるため、個々のウィンドウ毎に処理を行うクラスの用意

## ■実際のコード
コード差分が２００行以上あるので、 github にて[コード差分]をご確認ください。
シンプルなので解説するより見ていただいたほうが良いです。

[ビルド用プロジェクト]も用意しておきました。
Plugins フォルダ内がサブプロジェクトになっていますので、ビルドを試したい方は download よりも clone したほうが楽です。

## ■注意点

### ●メニューとツールバー
* レベルエディタとは異なり、ややこしい対応をしなくてもリソースの開放漏れは発生しないようです。
	* レベルエディタについて気になる方は[【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]を参照してください。
* ```Extension``` 類と ```PluginCommands``` の未参照オブジェクトができてしまいます。
	* 破棄を目的に、モジュールのシャットダウン時に ```GEngine->ForceGarbageCollection(true);``` を呼び出しています。
		* なお、未参照オブジェクトが増えるのはウィンドウを閉じる毎となります。
		* 気になる場合は上記関数を ```FESWSampleModule::OnMaterialEditorClosed()``` の中で呼び出すと改善します。

### ●終了処理
* 以下の３つのタイミングで発生し、必要なことが異なります。

| タイミング | ```IMaterialEditor``` | ハンドラ等 | ```OnMaterialEditorClosed()``` | ```ShutdownModule()``` |
| ------ | ------ | ------ | ------ | ------ |
| モジュールアンロード時 | アクセス可能 | 解除が必要 | 呼び出されない | 呼び出される |
| UE4 エディタ終了時 | アクセス不可 | 解除が不要 | 呼び出される | 呼び出される |
| マテリアルエディタ終了時 | アクセス不可 | 解除が不要 | 呼び出される | 呼び出されない |

## ■結果
マテリアルエディタにプラグインで拡張可能なタブを追加できるようになりました。
このタブを好きなように変更することでマテリアルエディタを自由に拡張していけるでしょう。

## ■あとがき
今どきは EUW 押しですが、今回のように EUW が利用できないケースもあり、それは当面続くのでしょう。
ただ、プラグインの作成の取っ掛かりは EUW と比較すると情報が少ないと感じたので、今回情報をまとめてみました。
どなたかの参考になれば幸いです。

ここまで読んでいただきありがとうございました！

## ■関連記事

* [【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]

[【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]:https://qiita.com/sentyaanko/items/23b0919af4b6fabd8378
[ビルド用プロジェクト]:https://github.com/sample-of-sentyaanko-on-qiita/UE4PluginBuildSample/tree/v0.1.1
[コード差分]:https://github.com/sample-of-sentyaanko-on-qiita/UE4PluginForMaterialEditorSample/compare/d9ea74fb13e8b72c02c446c2ef3174e4042ae3da...b0105312bc674f239f285bf9af532be7fc9cf85b


----
おしまい。
