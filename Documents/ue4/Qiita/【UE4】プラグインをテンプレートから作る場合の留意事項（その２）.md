# 【UE4】プラグインをテンプレートから作る場合の留意事項（その２）

## ■はじめに

### ●この記事は何？

[【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]の続きです。
上記の記事で扱わなかった、以下の２点の対処方法について纏めたものです。

* 「ESWSample」タブが残る。
* ツールバー上に生成したボタンが、テキストのみのボタンになる（アイコンだけ消える）。


### ●対処方法？

結論から書いておきます。

* 「ESWSample」タブが残る。
	* タブを生成する際にタブのウィークポインタをモジュール側で保持しておき、モジュールの破棄の際にタブを閉じる関数を呼び出せばよいです。
* ツールバー上に生成したボタンが、テキストのみのボタンになる（アイコンだけ消える）。
	* アプローチを２つ挙げます。
		1. 一度ツールバーを作り直す。
		1. ツールバーの特定のボタンを破棄する。

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
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その１）]をすでに読んでいること

## ■「「ESWSample」タブが残る。」の対処方法

### ●行うこと

* ```FESWSampleImpl``` のコンストラクタとデストラクタを追加
* タブのウィークポインタを保持するメンバ変数 ```PluginTab``` を追加
* ```FESWSampleImpl::OnSpawnPluginTab()``` にてタブを生成する際、```SNew``` から ```SAssignNew``` に変更し、ウィークポインタを ```PluginTab``` に保持するよう変更
* デストラクタ内で ```PluginTab``` を利用してタブを閉じる関数 ```SDockTab::RequestCloseTab()``` の呼び出しを追加

### ●具体的なコード

```cpp:ESWSample.cpp
//省略...
class FESWSampleImpl
{
public:
	FESWSampleImpl()
	{
	}
	~FESWSampleImpl()
	{
		//ここから追加
		if (PluginTab.IsValid())
		{
			if (auto PluginTabPtr = PluginTab.Pin())
			{
				PluginTabPtr->RequestCloseTab();
			}
			PluginTab.Reset();
		}
		//ここまで追加
	}
	TSharedRef<SDockTab> OnSpawnPluginTab(const FSpawnTabArgs& SpawnTabArgs)
	{
		//return SNew(SDockTab) //これを
		return SAssignNew(PluginTab, SDockTab) //これに変更
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
//省略...
private:
	TWeakPtr<SDockTab> PluginTab; //これを追加
//省略...
};
//省略...
```

以上で、モジュールが破棄される際にタブが閉じられます。

## ■「ツールバー上に生成したボタンが、テキストのみのボタンになる（アイコンだけ消える）。」の対処方法

それぞれのアプローチについて説明します。

## ■「一度ツールバーを作り直す。」について

### ●行うこと

* ```FLevelEditorModule::GetLevelEditorTabManager``` を使用し、タブマネージャ（```FTabManager```）が取得できます。
* ```FTabManager::FindExistingLiveTab()``` を使用し、特定のタブ（```SDockTab```）が取得できます。
	* タブが表示されている場合のみ取得できます。
	* 今回は、ツールバーが表示されているときだけ再構築したいので、処理の分岐にも利用できます。
* ```SDockTab::RequestCloseTab()``` で自身を閉じることが出来ます。
* ```FTabManager::InvokeTab()``` を使用し、特定のタブ（```SDockTab```）を呼び出せます。

以上の機能を組み合わせることで対応可能です。

### ●具体的なコード

前述の関数を組み合わせて、ツールバーを再構築する関数を作ります。
```FESWSampleImpl``` の宣言の前で良いでしょう。

```cpp:ESWSample.cpp
//省略...
//ここから追加
void RefreshLevelEditorToolBar()
{
	const FName LevelEditorModuleName("LevelEditor");
	const FTabId ToolbarTabId(FName("LevelEditorToolBar"));
	FLevelEditorModule& LevelEditorModule = FModuleManager::LoadModuleChecked<FLevelEditorModule>(LevelEditorModuleName);
	if (auto TabManager = LevelEditorModule.GetLevelEditorTabManager())
	{
		if (auto Toolbar = TabManager->FindExistingLiveTab(ToolbarTabId))
		{
			Toolbar->RequestCloseTab();
			Toolbar.Reset();
			TabManager->InvokeTab(ToolbarTabId);
		}
	}
}
//ここまで追加
class FESWSampleImpl
//省略...
```

> **Technical Note:RequestCloseTab() の呼び出しと参照カウント**
> ```RequestCloseTab()``` の呼び出し前後で ```Toolbar.GetSharedReferenceCount()``` をログに出力するなどの方法で、
> 強参照数を確認すると 2->1 に変化するのが確認できます。
> 1 が残るのは変数 ```TabManager``` の分なので、エディタ内部からの参照元がなくなることが確認できます。

<!-- 引用を分けるためのダミーコメント -->

> **Technical Note:TabId について**
> UE 4.24.3 にて、 ```LevelEditorTabIds``` というクラスが追加されました。
> このクラスはレベルエディタモジュール内で利用している全てのタブ名が static FName で定義されています。
> この記事ではまだ利用していませんが、プラグイン側でもこちらを利用するようにしたほうが良いでしょう。
> そうすることで、たとえエディタ側のソースコードでタブ名が変更された場合に影響を抑えられます。

上記の関数をモジュール破棄時に呼び出します。
スタイルの破棄の前で良いでしょう。

```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::ShutdownModule()
{
//省略...
	RefreshLevelEditorToolBar(); //これを追加
	FESWSampleStyle::Shutdown();
//省略...
}
//省略...
```

以上で、モジュールが破棄される際にツールバーが再構築できます。

## ■「ツールバーの特定のボタンを破棄する。」について

### ●「作り直す」はやりすぎ？

先に挙げたアプローチ「一度ツールバーを作り直す。」が、やりすぎであると感じる方もいらっしゃるでしょう。
そこで、ツールバー上に生成したボタンを削除する方法についても一例をあげます。

### ●注意

ここで挙げる対処方法は「エディタのソースコードをいじらないでできる、かなり無理矢理な方法」です。
現在のエディタの実装方法に依存している部分が多いです。
その為、エディタの実装が変更されると使えなくなります。
よりよい方法をご存知な方はお知らせいただけると幸いです。

### ●行うこと

* ツールバーの構成を確認しておき、どのウイジェットを破棄すればよいか調査しておきます。
	* エディタの機能 ```Widget Reflector``` を利用することで、ウィジェットのツリー構造を確認することが出来ます。
	* 追加したボタンは ```SToolBarButtonBlock``` というクラスであることがわかります。
	* ```SToolBarButtonBlock``` の更に下位の階層に ```STextBlock``` があり、これがテキストを表示しています。
	* ```STextBlock::GetText()``` を使用して表示中のテキストが取得できます。
	* 今回はこのテキストを使用し、追加したボタンを特定します。
* ```FLevelEditorModule::GetLevelEditorTabManager()``` を使用し、タブマネージャ（```FTabManager```）が取得できます。
* ```FTabManager::FindExistingLiveTab()``` を使用し、特定のタブ（```SDockTab```）が取得できます。
	* ここまでは同じです。
* タブ内のルートの ```SWidget``` の参照が ```SDockTab::GetContent()``` から取得できます。
* ```SWidget::GetAllChildren()``` を利用することでウィジェットのツリー構造に従った ```SWidget``` の参照が取得できます。

> **Technical Note:テキストを使用したボタンの特定というアプローチに関して**
> この方法だと、同じテキストを持つボタンを誤認してしまいます。
> 可能であれば別のアプローチ（```FToolBarBuilder``` に渡している情報、もしくは取得できる情報の利用）をとりたかったです。
> ですが、エディタコードに手を入れずに取得可能な情報がこちらだけでした。

### ●ツールバーのウィジェット構成とやるべきこと

```Widget Reflector```の出力内容を見てみます。

![WidgetReflector.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/397453/5d5cf52e-0944-6261-fb03-5fb2216c659c.png)

ツリーの中身の要約は以下のような内容です。

```
├─SDockingTabStack	他のタブも含めたタブのルート
	└─SVerticalBox
		├─SBorder	タブ部分のルート
		└─SOverlay	タブの中身のルート
			├─SBorder	①SDockTab::GetContent()で取得できる場所
			│	└─SMultiBoxWidget
			│		└─SBorder
			│			└─SClippingHorizontalBox	②ボタンが入っている場所
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox
			│				├─SVerticalBox	③今回消したいESWSample用のボタンのルート
			│				│	└─STextBlock	④
			│				│	└─SToolBarButtonBlock	⑤
			│				│		└─SButton
			│				│			└─SHorizontalBox
			│				│				└─SVerticalBox
			│				│					├─SImage
			│				│					├─SImage
			│				│					└─STextBlock	⑥今回特定のために利用するボタン上のテキスト
			│				├─SVerticalBox
			│				├─SVerticalBox

```

* ```SDockTab::GetContent()``` を利用し①を取得
* ①の子供から②を検索
* ②の子供をループ処理
	* ③の直下に④があるが、空の ```STextBlock``` であるため、無視したいので⑤を検索
	* ⑤がある場合は⑥を検索
	* ⑥のテキストが検索対称（今回の場合は ```ESWSample```）の場合は②から③の削除

### ●具体的なコード

ウィジェットツリー内の特定の型を持つ子（または自身）を取得する関数を用意します。

```cpp:ESWSample.cpp
//省略...
template< typename ObjectType >
TSharedPtr<ObjectType> SearchWithType(const TSharedPtr<SWidget>& Widget, const FName& Type)
{
	if(Widget->GetType() == Type)
	{
		return StaticCastSharedPtr<ObjectType>(Widget);
	}
	else
	{
		if (auto Children = Widget->GetAllChildren())
		{
			const auto NumChildren = Children->Num();
			for (int32 ChildIndex = 0; ChildIndex < NumChildren; ChildIndex++)
			{
				auto Child = Children->GetChildAt(ChildIndex);
				if (auto ChildWidget = SearchWithType<ObjectType>(Child, Type))
				{
					return ChildWidget;
				}
			}
		}
	}
	return TSharedPtr<ObjectType>();
}
//省略...
```

> **Technical Note:型の特定方法**
> ```SWidget``` は ```UObject``` の派生ではないため、 ```Cast``` などの方法でダウンキャストが出来ません。
> その為、ここでは ```SWidget::GetType()``` で取得できる情報を利用しています。
> この情報の実体は ```SWidget::TypeOfWidget``` であり、 変数定義部分に以下のコメントがあります。
>> ```Debugging information on the type of widget we're creating for the Widget Reflector.```
> 
> ```Widget Reflector``` のための機能なので、あまり好ましい利用の方法ではありません。
> ですが、他に方法が見つからないので、今回はこちらを利用しています。

```SClippingHorizontalBox``` を探し、
その子供から ```SToolBarButtonBlock``` を探し、
その子供から ```STextBlock``` を探し、
```STextBlock::GetText()``` の結果と、
ボタンを追加した際に利用した ```FUICommandInfo``` から取得できる ```FUICommandInfo::GetLabel()```を比較し、
同じだった場合は ```SClippingHorizontalBox``` から ```SBoxPanel::RemoveSlot()``` する関数を用意します。

```cpp:ESWSample.cpp
//省略...
void SearchAndDestroyToolbarButton(const TSharedRef<SWidget>& Widget, const TSharedPtr< FUICommandInfo >& UICommandInfo)
{
	if (auto HorizontalBox = SearchWithType<SHorizontalBox>(Widget, FName("SClippingHorizontalBox")))
	{
		if (auto Children = HorizontalBox->GetAllChildren())
		{
			for (int32 ChildIndex = 0; ChildIndex < Children->Num(); ChildIndex++)
			{
				auto Child = Children->GetChildAt(ChildIndex);
				if (auto ToolBarButtonBlock = SearchWithType<SToolBarButtonBlock>(Child, FName("SToolBarButtonBlock")))
				{
					if (auto Children2 = ToolBarButtonBlock->GetAllChildren())
					{
						for (int32 ChildIndex2 = 0; ChildIndex2 < Children2->Num(); ChildIndex2++)
						{
							auto Child2 = Children2->GetChildAt(ChildIndex2);
							if (auto ToolBarTextBlock = SearchWithType<STextBlock>(Child2, FName("STextBlock")))
							{
								auto Text = ToolBarTextBlock->GetText();
								if (Text.EqualTo(UICommandInfo->GetLabel()))
								{
									HorizontalBox->RemoveSlot(Child);
									ChildIndex--;
									break;
								}
							}
						}
					}
				}
			}
		}
	}
}
//省略...
```

> **Technical Note:テキストの比較方法**
> ```ToolBarTextBlock->GetText()``` と ```UICommandInfo->GetLabel()``` を比較しています。
> これは ```ESWSampleCommands.cpp``` の ```UI_COMMAND()``` マクロの第２引数を変更することで正しく動作していることが確認できます。
> ループ内で ```UICommandInfo->GetLabel()``` を毎回呼び出すことが気になる方は関数の頭で一時変数に入れてしまっても問題ないです。
> そうしていないのは、そもそもテキスト同士を比較する方法は好ましくないと考えているためです。
> 可能であればボタンが内部で保持している ```UICommandInfo``` そのものを比較したいため、そのままにしています。

```FLevelEditorModule``` ＞ ```FTabManager``` ＞ ```SDockTab``` の順で取得していき、
```SearchAndDestroyToolbarButton``` を呼び出す関数を用意します。

```cpp:ESWSample.cpp
//省略...
void RemoveButtonFromLevelEditorToolBar(const TSharedPtr< FUICommandInfo >& UICommandInfo)
{
	const FName LevelEditorModuleName("LevelEditor");
	const FTabId ToolbarTabId(FName("LevelEditorToolBar"));
	FLevelEditorModule& LevelEditorModule = FModuleManager::LoadModuleChecked<FLevelEditorModule>(LevelEditorModuleName);
	if (auto TabManager = LevelEditorModule.GetLevelEditorTabManager())
	{
		if (auto Toolbar = TabManager->FindExistingLiveTab(ToolbarTabId))
		{
			SearchAndDestroyToolbarButton(Toolbar->GetContent(), UICommandInfo);
		}
	}
}
//省略...
```

```FESWSampleImpl``` のデストラクタで、 ```RemoveButtonFromLevelEditorToolBar()``` を呼び出します。

```cpp:ESWSample.cpp
//省略...
class FESWSampleImpl
{
//省略...
	~FESWSampleImpl()
	{
//省略...
		RemoveButtonFromLevelEditorToolBar();
//省略...
	}
//省略...
};
//省略...
```

以上で、モジュールが破棄される際にツールバー上に生成したボタンが消えます。

## ■結果

アンロード後に ESWSample タブとツールバー上に生成したボタンが消えるようになりました。

## ■あとがき

スレート関連のコードの追いかけ方がなんとなくわかったのではないでしょうか。

ここまで読んでいただきありがとうございました！

## ■もう少し突っ込んだ話

ところで、ツールバー上に生成したボタンを消す方法について、２つ例を上げましたが、どちらのアプローチをとるべきでしょうか？
その前に、ここで更にモジュールをロードするとどうなるかを見てみます。

* ツールバー上に生成したボタン
	* 消えたまま。
	* ツールバーを一度閉じ、メニューから再表示するとボタンが追加される。
* メニューに追加した項目
	* 消えたまま。
* ESWSample タブ
	* 消えたまま。
	* ツールバー上に生成したボタンのボタンを押せば再表示される。

### ●ツールバー上に生成したボタンについて

ツールバーについては、を開閉しなおせばボタンが生成されなおされます。
アンロード時は「ボタン単体を消す」、再ロード時は「ツールバーを開閉し直す」でも良いですが、
「ボタン単体を消す」のは前述の通りかなり無理矢理なので、
「ツールバーを開閉し直す」で統一してしまったほうがシンプルです。

具体的には ```RefreshLevelEditorToolBar()``` を ```FESWSampleModule::StartupModule()``` の末尾あたりで呼び出せば問題なく動作します。
エディタ起動時は ```FLevelEditorModule::GetLevelEditorTabManager()``` が空のシェアードポインタを返すため、うまい感じに動いてくれます。
詳しくは[【UE4】プラグインをテンプレートから作る場合の留意事項（その３）]で扱っていますのでそちらへどうぞ。とても短い記事です。

### ●メニューに追加した項目について

こちらは、エディタコードを変更しない限り、対処方法がありません。
どうしても対応したい場合は[【UE4】プラグインをテンプレートから作る場合の留意事項（その４）]で扱っていますのでそちらへどうぞ。ちょっと重い記事です。

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

