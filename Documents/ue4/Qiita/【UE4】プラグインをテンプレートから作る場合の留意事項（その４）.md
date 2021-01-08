# 【UE4】プラグインをテンプレートから作る場合の留意事項（その４）

## ■はじめに

### ●この記事は何？

[【UE4】プラグインをテンプレートから作る場合の留意事項（その２）]の続きです。
（[その３]は独立してるので、[その２]であってます。）
上記の記事で扱わなかった、以下の点の対処方法について纏めたものです。

* モジュールアンロード後、再びロードしても「Window」メニューに項目が戻らない

### ●対処方法？

結論から書いておきます。

* エディタコードを編集して、メニューの再構築関数を実装する
* 必要なタイミングで呼び出す

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
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その２）]をすでに読んでいること

## ■対処方法

### ●行うこと

* クラス ```ILevelEditor``` 
	* メニューの再構築関数 ```RegenerateMenu()``` を純粋仮想で宣言
* 上記の派生クラス ```SLevelEditor```
	* ```RegenerateMenu()``` をオーバーライド宣言
	* メニューの配置先の ```SBox``` のウィークポインタ ```MenuWidgetBox``` を定義
	* 初期化処理 ```Initialize()``` を編集し、メニュー構築時に ```MenuWidgetBox``` を初期化するように編集
	* ```RegenerateMenu()``` を実装

### ●具体的なコード

外部モジュールからアクセス可能な、レベルエディタの基底クラスである ```ILevelEditor``` に、
```public``` で ```RegenerateMenu()``` を純粋仮想で宣言します。

```cpp:ILevelEditor.h
//省略...
class ILevelEditor : public SCompoundWidget, public IToolkitHost
{
//省略...
public:
	virtual void RegenerateMenu() = 0; // これを追加
};
//省略...
```

外部モジュールからアクセス不可能な、レベルエディタの実装クラスである ```SLevelEditor``` に、
```public``` で ```RegenerateMenu()``` をオーバーライドで宣言します。
また、```private``` でメンバ変数 ```MenuWidgetBox``` を定義します。

```cpp:SLevelEditor.h
//省略...
class SLevelEditor
	: public ILevelEditor
{
//省略...
	virtual void RegenerateMenu() override; // これを追加
//省略...
private:
	TWeakPtr<SBox> MenuWidgetBox; // これを追加
//省略...
};
//省略...
```

初期化処理 ```Initialize()``` を編集し、メニュー構築時に ```MenuWidgetBox``` を初期化するように編集

```cpp:SLevelEditor.cpp
//省略...
void SLevelEditor::Initialize( const TSharedRef<SDockTab>& OwnerTab, const TSharedRef<SWindow>& OwnerWindow )
{
//省略...
	TSharedRef<SWidget> Widget1 = FLevelEditorMenu::MakeLevelEditorMenu(LevelEditorCommands, SharedThis(this));

	ChildSlot
	[
		SNew( SVerticalBox )
		+SVerticalBox::Slot()
		.AutoHeight()
		[
			SNew( SOverlay )

			+SOverlay::Slot()
			[
//				SNew(SBox)	// ここを変更
				SAssignNew(MenuWidgetBox, SBox) // これを追加
				.AddMetaData<FTagMetaData>(FTagMetaData(TEXT("MainMenu")))
				[
					Widget1
				]
			]
//省略...
}
//省略...
```

> **Technical Note:このあたりの仕組みに関して**
> ```ILevelEditor``` は ```SCompoundWidget``` の派生クラスですので、```SLevelEditor``` 自体がウィジェットの一種となっています。
> ```SLevelEditor::Initialize()``` にて、 ```ChildSlot``` から始まるスレートの構成コードが含まれています。
> 必要な部分だけ読み解くと以下のようなツリー構成になっています。

```
SVerticalBox
	└─SOverlay
		└─SOverlay
			└─SBox	MenuWidgetBox でウィークポインタを保存
				└─Widget1	FLevelEditorMenu::MakeLevelEditorMenu() で構築されたメニュー本体
```

> ```SBox``` の子は ```SBox::SetContext()``` を使うことで差し替えられます。
> その為、 ```MenuWidgetBox``` で参照先を保持しておき、必要なタイミングで差し替えられようにしています。


```SLevelEditor::RegenerateMenu()``` を実装します。

```cpp:SLevelEditor.cpp
//省略...
void SLevelEditor::RegenerateMenu()
{
	if (LevelEditorCommands && MenuWidgetBox.IsValid())
	{
		if (auto MenuWidgetBoxPtr = MenuWidgetBox.Pin())
		{
			TSharedRef<SWidget> Widget1 = FLevelEditorMenu::MakeLevelEditorMenu(LevelEditorCommands, SharedThis(this));
			MenuWidgetBoxPtr->SetContent(Widget1);
		}
	}
}
//省略...
```

> **Technical Note:エディタコードの編集が必要だった理由**
> メニューを構築するための関数　```FLevelEditorMenu::MakeLevelEditorMenu()``` が外部モジュールからアクセスできないためです。
> それ以外の部分に関してはなんとかアクセスする方法があるため、上記関数だけアクセス経路を用意すれば、それ以外はモジュール側で書くことも可能です。
> ただ、それをしてしまうとエディタの内部実装に近い部分をモジュール側に置くことになるため、機能の分け方としてスッキリしません。
> いずれにせよエディタ側のコードを編集する必要があるのは変わらないため、今回はエディタコード側で実装しています。


エディタ側のコードの変更は以上です。
ビルドの方法等は割愛します。

用意した関数 ```RegenerateMenu()``` を必要なタイミングで呼び出すようにします。
```RefreshLevelEditorToolBar()``` を ```RefreshLevelEditorMenuAndToolBar()``` と改め、
```StartupModule()``` と ```ShutdownModule()``` の中で呼び出せばよいでしょう。

```cpp:SLevelEditor.cpp
//省略...
void RefreshLevelEditorMenuAndToolBar()
{
//省略...
	//ここから追加
	auto LevelEditorWeak = LevelEditorModule.GetLevelEditorInstance();
	if (LevelEditorWeak.IsValid())
	{
		if (auto LevelEditor = LevelEditorWeak.Pin())
		{
			LevelEditor->RegenerateMenu();
		}
	}
	//ここまで追加
}
//省略...
void FESWSampleModule::StartupModule()
{
//省略...
	RefreshLevelEditorMenuAndToolBar(); //これを追加
}
//省略...
void FESWSampleModule::ShutdownModule()
{
//省略...
	RefreshLevelEditorMenuAndToolBar(); //これを追加
	FESWSampleStyle::Shutdown();
//省略...
}
//省略...
```


以上で、モジュールアンロード後、再びロードした際「Window」メニューに項目が戻るようになります。

## ■結果

モジュールのアンロードとロードを繰り返し行った際にメニューやツールバーが再構築されるようになったので、
プラグイン作成中にメニュー項目やツールバー上のボタンの調整がやりやすくなりました。

## ■あとがき

[その１]から[その４]までの対応を行うことで、モジュール開発中の、ロードとアンロードした際のモヤモヤする部分が解消できました。
ここまでやっておけば、本来作ろうとしていたモジュール実装に専念できるでしょう。

ここまで読んでいただきありがとうございました！

## ■もう少し突っ込んだ話

[その１]の時に挙がっていた、「登録したデリゲート残りっぱなし」の件について、
ここまでの対応をした結果どうなっているのでしょうか？改善しているのでしょうか？
また、それ以外にも、モジュール側で確保したリソースが残っていたりしないのでしょうか？

実際問題、どちらにせよ動作に大きな影響はありませんが、気になる方は
[【UE4】プラグインをテンプレートから作る場合の留意事項（その５）]で扱っていますのでそちらへどうぞ。
繰り返しになりますが、このシリーズで一番重い記事です。

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

