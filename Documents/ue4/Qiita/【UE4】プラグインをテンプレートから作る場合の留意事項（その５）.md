# 【UE4】プラグインをテンプレートから作る場合の留意事項（その５）

## ■はじめに

### ●この記事は何？

[【UE4】プラグインをテンプレートから作る場合の留意事項（その４）]の続きです。
上記の記事で扱わなかった、以下の点の対処方法について纏めたものです。

* モジュールで確保したリソースのうち、アンロード時に開放しきれていないものについてその内容と破棄の方法

### ●対処方法？

まずは状況確認をしましょう。

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
* [【UE4】プラグインをテンプレートから作る場合の留意事項（その４）]をすでに読んでいること

## ■状況確認

まずはどのリソースを開放していないのか確認をします。
リソース確保に関する関数の戻り値をシェアードポインタ（もしくはウィークポインタ）を保持しておきます。
今回は、アンロード時に参照カウントを元に開放状況の確認がしたいため、シェアードポインタで保存しておくことにします。

開放されていないものがあった場合は、どのクラスが保持し続けているかの調査を行います。
具体的には ```Visual Studio Community 2017``` のデータブレークポイントを利用し、参照カウントが増えるタイミングから保持しているクラスを特定します。


### ●確保しているリソース

サンプルのテンプレートで確保しているリソース類は以下があります。

1. ```FESWSampleCommands::OpenPluginWindow```
1. ```FESWSampleModule::PluginCommands```
1. ```FESWSampleModule::StartupModule()``` の一時変数 ```MenuExtender```
1. ```FESWSampleModule::StartupModule()``` の関数呼び出し ```MenuExtender->AddMenuExtension()``` の戻り値 ```TSharedRef< const FExtensionBase >```
1. ```FESWSampleModule::StartupModule()``` の一時変数 ```ToolbarExtender```
1. ```FESWSampleModule::StartupModule()``` の関数呼び出し ```ToolbarExtender->AddToolBarExtension()``` の戻り値 ```TSharedRef< const FExtensionBase >```
1. ```FESWSampleModule::StartupModule()``` の４箇所で呼び出している ```CreateSP()``` で作成したデリゲート

１、２についてはクラスメンバ変数なので、そのままで良いでしょう。
３、５については一時変数になっているので、メンバ変数を用意してそちらに代入します。
４、６については戻り値を変数に入れていないので、メンバ変数を用意してそちらに代入します。
７については一旦そのままにしておきます。

３～６で確保しているリソースのシェアードポインタを ```FESWSampleModule``` のメンバ変数として用意します。

```cpp:ESWSample.h
//省略...
class FESWSampleModule : public IModuleInterface
{
//省略...
	TSharedPtr<FExtender> MenuExtender;
	TSharedPtr< const FExtensionBase > MenuExtension;
	TSharedPtr<FExtender> ToolbarExtender;
	TSharedPtr< const FExtensionBase > ToolbarExtension;
};
//省略...
```

確保の際、メンバ変数に代入するようにします。

```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::StartupModule()
{
//省略...
#if 0 //変更前
		TSharedPtr<FExtender> MenuExtender = MakeShareable(new FExtender());
		MenuExtender->AddMenuExtension("WindowLayout", EExtensionHook::After, PluginCommands, FMenuExtensionDelegate::CreateRaw(this, &FESWSampleModule::AddMenuExtension));
#else //変更後
		MenuExtender = MakeShareable(new FExtender());
		MenuExtension = MenuExtender->AddMenuExtension("WindowLayout", EExtensionHook::After, PluginCommands, FMenuExtensionDelegate::CreateSP(Impl.ToSharedRef(), &FESWSampleImpl::AddMenuExtension));
#endif
//省略...
#if 0 //変更前
		TSharedPtr<FExtender> ToolbarExtender = MakeShareable(new FExtender);
		ToolbarExtender->AddToolBarExtension("Settings", EExtensionHook::After, PluginCommands, FToolBarExtensionDelegate::CreateRaw(this, &FESWSampleModule::AddToolbarExtension));
#else //変更後
		ToolbarExtender = MakeShareable(new FExtender);
		ToolbarExtension = ToolbarExtender->AddToolBarExtension("Settings", EExtensionHook::After, PluginCommands, FToolBarExtensionDelegate::CreateSP(Impl.ToSharedRef(), &FESWSampleImpl::AddToolbarExtension));
#endif
//省略...
}
//省略...
```

アンロードの際、以下の処理を行います。
* ```FESWSampleCommands::OpenPluginWindow``` の参照カウントの確認のため、一時変数にコピーするようにしておきます。
* 追加したメンバ変数をクリアするようにしておきます。
* 状況確認のため、[その４]で追加した ```RefreshLevelEditorMenuAndToolBar()``` の呼び出しは一旦コメントアウトしておきます。

```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::StartupModule()
{
//省略...
	//ここから追加
	auto OpenPluginWindow = FESWSampleCommands::Get().OpenPluginWindow;
	MenuExtension.Reset();
	MenuExtender.Reset();
	ToolbarExtension.Reset();
	ToolbarExtender.Reset();
	//ここまで追加
	Impl.Reset(); //その１で追加したコード
	PluginCommands.Reset(); //その１で追加したコード
	OpenPluginWindow.Reset();//これを追加
	//RefreshLevelEditorMenuAndToolBar(); //その４で追加した関数を一時的にコメントアウト
	FESWSampleStyle::Shutdown();
//省略...
}
//省略...
```

以上の変更で、テンプレートから生成されたコードで確保したリソースの状況を追えるようになりました。

### ●参照カウントを確認してみる

```FESWSampleModule::ShutdownModule()``` の ```OpenPluginWindow``` のコピー後にブレークポイントを設定し、それぞれの参照カウントがどのように変化するか確認してみます。
```MenuExtension``` の参照カウントはビューポートのレイアウトにより異なりますが、ここでは ```Four Panes (2x2 grid)``` にしています。

参照カウントの変化

| 変数名 | OpenPluginWindow のコピー後 | ShutdownModule() を抜けた時 | その後 |
| ----- | ----- | ----- | ----- |
| OpenPluginWindow | 5 | 2 | 毎フレームの処理内で参照カウントの増減が発生 |
| PluginCommands | 5 | 4 | 毎フレームの処理内で参照カウントの増減が発生 |
| MenuExtender | 2 | 1 | 変化なし |
| MenuExtension | 8 | 7 | 変化なし |
| ToolbarExtender | 2 | 1 | 変化なし |
| ToolbarExtension | 3 | 2 | 変化なし |

残りまくりですね。

## ■対処方法

ここからは少しずつ参照カウントを減らしていきます。

### ●OpenPluginWindow について

```OpenPluginWindow``` は ```FESWSampleModule::StartupModule()``` にて、 ```PluginCommands->MapAction()``` の引数として渡されています。
この関数は対応した登録解除の関数 ```PluginCommands->UnmapAction()``` があるので、これを呼び出すようにしてみます。

```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::StartupModule()
{
//省略...
	auto OpenPluginWindow = FESWSampleCommands::Get().OpenPluginWindow;
	PluginCommands->UnmapAction(OpenPluginWindow); //これを追加
//省略...
}
//省略...
```

参照カウントの変化

| 変数名 | 初期 | 今回 | 変化 |
| ----- | ----- | ----- | ----- | ----- |
| OpenPluginWindow | 2 | **1** | **-1** |
| PluginCommands | 4 | 4 | |
| MenuExtender | 1 | 1 | |
| MenuExtension | 7 | 7 | |
| ToolbarExtender | 1 | 1 | |
| ToolbarExtension | 2 | 2 | |

### ●RefreshLevelEditorMenuAndToolBar() の呼び出し

コメントアウトした ```RefreshLevelEditorMenuAndToolBar()``` を戻してみます。

参照カウントの変化

| 変数名 | 初期 | | 今回 | 変化 |
| ----- | ----- | ----- | ----- | ----- |
| OpenPluginWindow | 2 | 1 | **0** | **-1** |
| PluginCommands | 4 | 4 | **2** | **-2** |
| MenuExtender | 1 | 1 | 1 | |
| MenuExtension | 7 | 7 | **8** | **+1** |
| ToolbarExtender | 1 | 1 | 1 | |
| ToolbarExtension | 2 | 2 | **3** | **+1** |

```Extension``` 系が増えました。
これは ```ExtensibilityManager``` 類に ```Extender``` が登録しっぱなしの状態で再構築した結果、参照回数が増えた為です。

### ●Extender の登録解除

```MenuExtender``` は ```FESWSampleModule::StartupModule()``` にて、 ```LevelEditorModule.GetMenuExtensibilityManager()->AddExtender()``` の引数として渡されています。
この関数は対応した登録解除の関数 ```LevelEditorModule.GetMenuExtensibilityManager()->RemoveExtender()``` があるので、これを呼び出すようにしてみます。
```ToolbarExtender``` についても同様のものがあるのでそちらも併せて呼び出します。


```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::StartupModule()
{
//省略...
	auto OpenPluginWindow = FESWSampleCommands::Get().OpenPluginWindow;
	PluginCommands->UnmapAction(OpenPluginWindow);
	//ここから追加
	FLevelEditorModule& LevelEditorModule = FModuleManager::LoadModuleChecked<FLevelEditorModule>("LevelEditor");
	LevelEditorModule.GetMenuExtensibilityManager()->RemoveExtender(MenuExtender);
	LevelEditorModule.GetToolBarExtensibilityManager()->RemoveExtender(ToolbarExtender);
	//ここまで追加
//省略...
}
//省略...
```

参照カウントの変化

| 変数名 | 初期 | | | 今回 | 変化 |
| ----- | ----- | ----- | ----- | ----- | ----- |
| OpenPluginWindow | 2 | 1 | 0 | 0 | |
| PluginCommands | 4 | 4 | 2 | 2 | |
| MenuExtender | 1 | 1 | 1 | **0** | **-1** |
| MenuExtension | 7 | 7 | 8 | **5** | **-3** |
| ToolbarExtender | 1 | 1 | 1 | **0** | **-1** |
| ToolbarExtension | 2 | 2 | 3 | **1** | **-2** |

参照カウントが残っているのが ```PluginCommands``` と ```Extension``` 類だけになりました。

### ●GC する

```FESWSampleModule::StartupModule()``` の末尾で、 ```GC``` の実行を登録しておきます。

```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::StartupModule()
{
//省略...
	if (GEngine)
	{
		GEngine->ForceGarbageCollection(true);
	}
}
//省略...
```

```GC``` による破棄処理は ```GEngine->ForceGarbageCollection()``` 呼び出しの後、エンジンが都合のいいタイミングで行われます。
ですので今回は ```Visual Studio Community 2017``` の **データブレークポイント** を利用して参照カウントの変化を確認します。

参照カウントの変化

| 変数名 | 初期 | | | | 今回 | 変化 |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| OpenPluginWindow | 2 | 1 | 0 | | |
| PluginCommands | 4 | 4 | 2 | 2 | **1** | **-1** |
| MenuExtender | 1 | 1 | 1 | 0 | |
| MenuExtension | 7 | 7 | 8 | 5 | **4** | **-1** |
| ToolbarExtender | 1 | 1 | 1 | 0 | |
| ToolbarExtension | 2 | 2 | 3 | 1 | **0** | **-1** |

**Toolbar** 関係のオブジェクトは全て破棄されたようです。

### ●残りは何？

```MenuExtension``` が４回参照され、そこから ```PluginCommands``` が参照されている状態です。
この４箇所から参照を剥がせれば、 ```PluginCommands``` も連動して剥がせます。
これは追いかけるのが大変ですが、**データブレークポイント** を利用して参照カウントの変化を追いかけることで調べることが可能です。

結論としては、 ```SLevelEditorViewportViewMenu``` という ```SWidget``` の派生クラスが保持しています。
どこにあるかと言うと、ビューポートの上部にある[ビューポートオプションメニュー](https://docs.unrealengine.com/ja/Engine/UI/LevelEditor/Viewports/ViewportOptions/index.html)がそれにあたります。

```SLevelEditorViewportViewMenu``` は ```SEditorViewportViewMenu``` の派生であり、
```SEditorViewportViewMenu::MenuExtenders``` で ```MenuExtension``` を持っています。
４回参照されているのは、ビューポートのレイアウトを ```Four Panes (2x2 grid)``` にしており、
```SLevelEditorViewportViewMenu``` が４つ存在する為です。

```Widget Reflector``` を利用してウィジェットのツリー構造を確認すると、
はるか根元、３０階層ほど上に ```SLevelEditor``` にいることが確認できます。
このクラスについては[その４]でも扱っています。
また、SWidget のツリー構造をたどる方法も[その２]で扱いました。
つまり、```SLevelEditor```から再帰的に子を巡って ```SLevelEditorViewportViewMenu``` を探し出し、
```MenuExtenders```を取得し、```FExtender::RemoveExtension()``` を呼び出せば、 ```MenuExtension``` を解除できます。

### ●エディタコードの変更（SEditorViewportViewMenu::GetMenuExtenders() の実装）

上記の手順を行うにあたって、一点エディタの改造が必要になります。
```SEditorViewportViewMenu``` は ```MenuExtenders``` のアクセサを用意していません。
ですので ```public``` で ```GetMenuExtenders()``` を用意します。

```cpp:SEditorViewportViewMenu.h
//省略...
class UNREALED_API SEditorViewportViewMenu : public SEditorViewportToolbarMenu
{
//省略...
	const TSharedPtr<class FExtender>& GetMenuExtenders()const{return MenuExtenders;} //これを追加

//省略...
};
//省略...

```

### ●MenuExtension の登録解除

前述したとおり、 ```SLevelEditor``` から再帰的に ```SLevelEditorViewportViewMenu``` を探し、
```SEditorViewportViewMenu``` に追加した関数 ```GetMenuExtenders()``` と ```FExtender::RemoveExtension()``` を利用し、
```MenuExtension``` を取り除きます。

```cpp:SEditorViewportViewMenu.h
//省略...
void SearchSLevelEditorViewportViewMenuAndRemoveExtension(const TSharedRef<SWidget>& Widget, const TSharedRef< const FExtensionBase >& MenuExtension)
{
	if (Widget->GetType() == FName("SLevelEditorViewportViewMenu"))
	{
		auto EditorViewportViewMenu = StaticCastSharedRef<SEditorViewportViewMenu>(Widget);
		const TSharedPtr<class FExtender>& MenuExtenders = EditorViewportViewMenu->GetMenuExtenders();
		MenuExtenders->RemoveExtension(MenuExtension);
	}
	else
	{
		if (auto Children = Widget->GetAllChildren())
		{
			for (int32 ChildIndex = 0; ChildIndex < Children->Num(); ChildIndex++)
			{
				auto Child = Children->GetChildAt(ChildIndex);
				SearchSLevelEditorViewportViewMenuAndRemoveExtension(Child, MenuExtension);
			}
		}
	}
}

void SearchSLevelEditorViewportViewMenuAndRemoveExtension(const TSharedRef< const FExtensionBase >& MenuExtension)
{
	const FName LevelEditorModuleName("LevelEditor");
	FLevelEditorModule& LevelEditorModule = FModuleManager::LoadModuleChecked<FLevelEditorModule>(LevelEditorModuleName);
	auto LevelEditorWeak = LevelEditorModule.GetLevelEditorInstance();
	if (LevelEditorWeak.IsValid())
	{
		if (auto LevelEditor = LevelEditorWeak.Pin())
		{
			SearchSLevelEditorViewportViewMenuAndRemoveExtension(LevelEditor.ToSharedRef(), MenuExtension);
		}
	}
}
//省略...

void FESWSampleModule::ShutdownModule()
{
	SearchSLevelEditorViewportViewMenuAndRemoveExtension(MenuExtension.ToSharedRef());
//省略...
}
//省略...

```

参照カウントの変化

| 変数名 | 初期 | | | | | 今回 | 変化 |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| OpenPluginWindow | 2 | 1 | 0 | | | |
| PluginCommands | 4 | 4 | 2 | 2 | 1 | **0** | **-1** |
| MenuExtender | 1 | 1 | 1 | 0 | |
| MenuExtension | 7 | 7 | 8 | 5 | 4 | **0** | **-4** |
| ToolbarExtender | 1 | 1 | 1 | 0 | |
| ToolbarExtension | 2 | 2 | 3 | 1 | 0 | |

これで、上記６つのリソースが開放できました。

### ●CreateSP で作成したデリゲート

* デリゲート作成時に渡したシェアードポインタ```Impl```の参照カウントを確認すると１です。```FESWSampleModule``` 以外は強参照を持っていないことがわかります。
* ```PluginCommands->MapAction()``` に渡した際は第一引数である ```FESWSampleCommands::Get().OpenPluginWindow``` に保持されており、これはここまでの手順で破棄できています。
* ```MenuExtender->AddMenuExtension()``` に渡した際は戻り値である ```MenuExtension``` に保持されており、これはここまでの手順で破棄できています。
* ```ToolbarExtender->AddToolBarExtension()``` に渡した際は戻り値である ```ToolbarExtension``` に保持されており、これはここまでの手順で破棄できています。
* ```FGlobalTabmanager::Get()->RegisterNomadTabSpawner()``` は対である ```FGlobalTabmanager::Get()->UnregisterNomadTabSpawner()``` で破棄できています。

> **Technical Note:```FUICommandList::MapAction()``` に関して**
> 構造体 ```FUIAction``` のメンバに格納後、```FUICommandList::UICommandBindingMap``` で保持されます。
> ```FUICommandList``` は ```FUIAction``` のポインタを返すメンバ関数しか持っておらず、保持している間、所有権を他に移すことはありません。
> ```FUICommandList::UnmapAction``` で ```FUICommandList::UICommandBindingMap```  から破棄されます。

<!-- 引用を分けるためのダミーコメント -->

> **Technical Note:```AddMenuExtension()/AddToolBarExtension()``` に関して**
> クラス ```FMenuExtension/FMenuBarExtension``` のメンバに格納後、```FExtender::Extensions``` で保持されます。
> クラス ```FMenuExtension/FMenuBarExtension``` は ```MultiBoxExtender.cpp``` でクラス宣言されており、それ以外の翻訳単位から使用できないようになっています。
> ```FExtender``` は ```Extensions``` へのアクセサを持っておらず、保持している間、所有権を他に移すことはありません。
> ```FExtender::RemoveExtension``` で ```FExtender::Extensions``` から放棄されます。
> つまり、 ```MenuExtension/ToolbarExtension``` の強参照数が0になっていれば破棄できている、ということになります。

<!-- 引用を分けるためのダミーコメント -->

> **Technical Note:```FTabManager::RegisterNomadTabSpawner``` に関して**
> クラス ```FTabSpawnerEntry``` のメンバ ```OnSpawnTab``` に格納後、```FTabManager::NomadTabSpawner``` で ```SharedRef``` で保持されます。
> ```FTabSpawnerEntry::OnSpawnTab``` は ```private``` 変数であり、 ```friend class``` である ```FTabManager``` 以外からは参照されません。
> つまり、 ```FTabManager::RegisterNomadTabSpawner``` で確保した ```FTabSpawnerEntry``` の強参照数が0になっていれば破棄できている、ということになります。
> **データブレークポイント** を利用して確認すると破棄できていることが確認できます。

以上で、モジュールアンロード後、プラグイン側で確保したリソースを破棄できました。

### ●別のアプローチ

もっとシンプルな方法はないのでしょうか？
という場合には、```EditorReinit()``` というな関数を呼べば、エディタウィンドウが再生成されます。

```cpp:ESWSample.cpp
//省略...
void FESWSampleModule::ShutdownModule()
{
//省略...
	EditorReinit();
	if (GEngine)
	{
		GEngine->ForceGarbageCollection(true);
	}
}
//省略...

```

エディタコードをいじれない状況ならば、こちらを試すのも良いでしょう。

## ■結果

モジュールのアンロード時に開放されていないリソースの内容を知ることができました。
またその対処も行えました。

## ■あとがき

本来はもっと違う記事を書きたかったのですが、ちょっと気になって調べ始めてしまい、とんだ寄り道となってしまいました。
後に迷い込んだ人が無事に出てこれるようにと、多少なりとも情報を纏めておきます。
どなたかの参考になれば幸いです。

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
