# 【UE4】C++のバージョン

----
## はじめに
### 環境

| | |
| ---- | ---- |
| UE4 バージョン | 4.26.2 |
| Visual Studio | 2017 |

### この記事は何？
この記事は、 `UE4` の `C++` のバージョンについてまとめたものです。

ビルドの際の利用する `C++` のバージョンについて、指定しなかった場合どうなるのかや、仕組みについてまとめています。
ついでに `C++` のバージョンの指定方法についてもまとめています。

なお、この記事は各ツールのバージョンに依存しますので、ご留意ください。


### 想定している読者
* UE C++ の初心者
* `C++17` を愛して止まないお方

### 扱わないこと
* プラグインの設定


----
## 結論

`C++` のバージョンは、デフォルトでは `C++14` が使用されます。
`C++` のバージョンの指定方法は、プロジェクトの **YourProjectName.Build.cs** で以下いずれかを指定します。

```C#:YourProjectName.Build.cs
		//以下のいずれかを指定する。
		//CppStandard = CppStandardVersion.Cpp14;
		//CppStandard = CppStandardVersion.Cpp17;
		//CppStandard = CppStandardVersion.Latest;
```
> NOTE: 以降、 `YourProjectName` はご自分のプロジェクト名に置き換えて読んでください。


----
## 公式ドキュメントの記述

4.22 のリリースノートに記載されています。

[Unreal Engine 4 ドキュメント > 新機能 > リリースノート > Unreal Engine 4.22 リリース ノート](https://docs.unrealengine.com/ja/WhatsNew/Builds/ReleaseNotes/4_22/index.html)
> # 新機能：Visual Studio 2019 のサポート
> ![画像代替テキスト](https://docs.unrealengine.com/Images/WhatsNew/Builds/ReleaseNotes/4_22/image_11.png)
> 
> Visual Studio 2019 のサポートが追加されました。
> デフォルトで Visual Studio 2019 を使用するには、エディタのソース管理設定から「Visual Studio 2019」を IDE として選択します。
> 
> また、新しい C++ 標準バージョンへの切り替えのサポートも追加されました。
> プロジェクトがサポートしている C++ 標準のバージョンを変更するには、｢CppStandard｣プロパティを｢.target.cs｣ファイルから次のいずれかの値に設定します。
> 
> | バージョン | 値 |
> |-----|-----|
> | C++14 | CppStandardVersion.Cpp14 |
> | C++17 | CppStandardVersion.Cpp17 |
> | 最新 | CppStandardVersion.Latest |
>
> 同時に、UE4 では、Visual Studio 2015 のサポートを廃止しました。
> プロジェクトを Visual Studio 2015 コンパイラで強制的にコンパイルする場合は、プロジェクトの｢.target.cs｣ファイルから｢WindowsPlatform.Compiler = WindowsCompiler.VisualStudio2015｣を設定できます。
> Epic Games Launcher からダウンロードしたエンジンのバージョンは Visual Studio 2015 をサポートしていないため、内部でのテストは行われません。

公式ドキュメントでは **.target.cs** と記載されています。
先程、私が結論に書いたのは **YourProjectName.Build.cs** です。

…おかしいですね…？

> NOTE: **YourProjectName.Target.cs** と **ProjectNameEditor.Target.cs**
> 詳しくは割愛しますが、前者がスタンドアロン起動時に使われ、後者がエディタ起動時に使われます。
> （ `Visual Studio` のターゲット的に言えば、`Shipping` 等と `Development Editor` 等）
> ですので、どちらか片方だけ変える、というのは意味がないことだとわかると思います。
> 
> 編集した場合について。
> `Visual Studio` のプロジェクトファイル `Intermediate/ProjectFiles/ProjectName.vcxproj` の更新が必要です。
> エクスプローラーで `YourProjectName.uproject` を右クリックして `Generate Visual Studio project files` を選択することで行えます。
> アンリアルエディタの `ファイル ＞ Visual Studio 2017 プロジェクトを更新` では**更新されない**ので注意が必要です。
> 更新しないと、例えば `CppStandard` の設定が `IntelliSense` の設定に反映されません。
> **YourProjectName.Build.cs** の更新時についても同様です。

----
## 試してみる

やってみましょう。
`YourProjectName.Target.cs` に `CppStandard = CppStandardVersion.Cpp17;` を追記します。

```C#:YourProjectName.Target.cs
		CppStandard = CppStandardVersion.Cpp17;
```

`Visual Studio` で `Shipping` でビルドします。すると、以下のエラーが発生します。

> YourProjectName modifies the value of CppStandard. 
> This is not allowed, as YourProjectName has build products in common with UE4Game.
> Remove the modified setting, 
> change YourProjectName to use a unique build environment by setting 'BuildEnvironment = TargetBuildEnvironment.Unique;' in the CppVerTarget constructor, 
> or set bOverrideBuildEnvironment = true to force this setting on.
> YourProjectName が CppStandard の値を変更しています。
> YourProjectName には UE4Game と共通のビルドプロダクトがあるため、これは許可されていません。
> 変更した設定を削除するか、
> 「 BuildEnvironment = TargetBuildEnvironment.Unique; 」を指定することで YourProjectName を 独自のビルド環境を使用するようにするか、
> さもなければ「 bOverrideBuildEnvironment = true 」を指定することで、強制的にこの設定をオンにしてください。

エンジン側と設定が異なるので、これだけではビルドできないよ、と言われています。

* 1. 変更した設定を削除する
	* `C++17` を諦める。
* 2. 「 BuildEnvironment = TargetBuildEnvironment.Unique; 」を指定する
	* 独自のビルド環境を使用するようにする。  
* 3. 「 bOverrideBuildEnvironment = true 」を指定する
	* 警告を無視して押し通る。

1 は却下です。

2 をやってみましょう。
`YourProjectName.Target.cs` に `BuildEnvironment = TargetBuildEnvironment.Unique;` を追記します。

```C#:YourProjectName.Target.cs
		CppStandard = CppStandardVersion.Cpp17;
		BuildEnvironment = TargetBuildEnvironment.Unique;
```

`Visual Studio` で `Shipping` でビルドします。すると、以下のエラーが発生します。

> Targets with a unique build environment cannot be built an installed engine.
> 独自のビルド環境を持つターゲットは、インストールされたエンジンではビルドできません。

インストール版ではビルドできないよ、と言われています。

ここから先は省略しますが、エンジンをソースをダウンロードしてビルドした環境であれば、この設定でもビルドを完了することは出来ます。
ですが、環境ごとにエンジンソースをビルドすることになるのはしんどいですよね…？
（プロジェクトフォルダごとに 50GB ほどディスク容量持っていかれるはずですし、ビルド時間も必要です。）

3 はちょっと恐ろしげですが、やってみましょう。
`YourProjectName.Target.cs` に `bOverrideBuildEnvironment = true;` を追記します。

```C#:YourProjectName.Target.cs
		CppStandard = CppStandardVersion.Cpp17;
		bOverrideBuildEnvironment = true;
```

`Visual Studio` で `Shipping` でビルドします。すると、ビルドが成功します。
詳しくは [`UnrealBuildTool.TargetRules.bOverrideBuildEnvironment`](#unrealbuildtooltargetrulesboverridebuildenvironment) にて。


----
## FORUMS や ANSWERHUB でのやり取り

公式ドキュメントでぱっと分かる方法でやってみましたがなにかしっくり来ません。
`FORUMS` や `ANSWERHUB` でのやり取りを確認して見ます。


### FORUMS
* [Issues with 4.22 C++17 Support](https://forums.unrealengine.com/t/issues-with-4-22-c-17-support/125442)
	* **YourProjectName.Target.cs** 及び **ProjectNameEditor.Target.cs** で `BuildEnvironment` を指定する方法が提案されています。前述のとおりです。
* [What’s needed for using C++17](https://forums.unrealengine.com/t/whats-needed-for-using-c-17/124529)
	* **YourProjectName.Build.cs** で `PCHUsage` と `PrivatePCHHeaderFile` を指定する方法が提案されています。後述します。
	* **YourProjectName.Build.cs** で `PCHUsage` を指定し、 `UnrealBuildTool` をカスタマイズする方法が提案されています。後述します。
* [C++17 was disabled in PCH file but is currently enabled](https://forums.unrealengine.com/t/c-17-was-disabled-in-pch-file-but-is-currently-enabled/139539)
	* `Linux` 環境の話なので詳しくは説明しませんが参考に。
	* `4.23.1-release` では **YourProjectName.Build.cs** で指定するだけで動作するが `4.24.3-release` では同じ方法でもエラーが発生するという情報があります。
	* `4.25` では **YourProjectName.Build.cs** で `PCHUsage` と `PrivatePCHHeaderFile` を指定することで動作するという情報があります。

### ANSWERHUB
* [How to enable c++17 in uproject, VS requires compiler flag /std:c++17](https://answers.unrealengine.com/questions/820557/view.html)
	* 2019年の話なので詳しくは説明しませんが参考に。
	* `UnrealBuildTool` をカスタマイズする方法が提案されています。 
* [How to build UE4.22 Plugins with C++17?](https://answers.unrealengine.com/questions/898017/view.html)
	* 2019年の話なので詳しくは説明しませんが参考に。
	* 同様の問題にあたっていますが、具体的な解決策等までたどり着かないまま放置されています。

----
## FORUMS にあった情報詳細

**YourProjectName.Build.cs** を変更するアプローチについての情報がありましたので、それを試してみましょう。

ただ、そもそもここまで **YourProjectName.Build.cs** を変更していなかったので、まずは `CppStandard = CppStandardVersion.Cpp17;` だけ指定してみます。

```C#:YourProjectName.Build.cs
		CppStandard = CppStandardVersion.Cpp17;
```

`Visual Studio` で `Shipping` でビルドします。すると、ビルドが成功します。
…工事完了では…？

### **YourProjectName.Build.cs** で `PCHUsage` と `PrivatePCHHeaderFile` を指定する方法

[What’s needed for using C++17 の該当のリプライ](https://forums.unrealengine.com/t/whats-needed-for-using-c-17/124529/3)

具体的には以下のような指定をしています。

```C#:YourProjectName.Build.cs
		PCHUsage = PCHUsageMode.NoSharedPCHs;
		PrivatePCHHeaderFile = "YourProjectUniquePCH.h";
		CppStandard = CppStandardVersion.Cpp17;
```

```C#:YourProjectName.Build.cs
	//Never use shared PCHs.  Always generate a unique PCH for this module if appropriate
	//どの 共有 PCH も使用しません。必要に応じて、常にこのモジュール用のユニークな PCH を生成します。
	//補足： PrivatePCHHeaderFile の指定が必須となる。
	//指定されているものをプライベート PCH として使用し、 共有 PCH は使用しない。
	PCHUsage = PCHUsageMode.NoSharedPCHs;
```
上記のように設定を変えていますが、デフォルトでは下記のようになっています。

```C#:YourProjectName.Build.cs
	//Shared PCHs may be used if an explicit private PCH is not set through PrivatePCHHeaderFile. 
	//In either case, none of the source files manually include a module PCH, and should include a matching header instead.
	//PrivatePCHHeaderFile で明示的なプライベート PCH を指定していない場合は、共有 PCH が使用されます。
	//いずれの場合も、どのソースファイルも手動でモジュール PCH をインクルードせず、代わりに一致するヘッダをインクルードする必要があります。
	//補足： PrivatePCHHeaderFile の指定が任意。
	//指定されている場合はその内容をプライベート PCH として使用し、 共有 PCH は使用しない。
	//指定されていない場合は共有 PCH を使用する。
	PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;
```

`PrivatePCHHeaderFile` を指定するのであれば挙動は大体同じになります。

> NOTE:
> 更に正確な挙動を知りたい場合は `UnrealBuildTool` のソースを読むことをおすすめします。
> エンジンのコードに比べればソース数が少ない上、 `C#` なので `Visual Studio` 上で呼び出し階層などで追いかけ易いので、読み易いと思います。


`Visual Studio` で `Shipping` でビルドします。すると、ビルドが成功します。

テンプレートで生成したばかりのプロジェクトでは、 `PrivatePCHHeaderFile` を、指定をしても、元のままでも、ビルドが通ります。
規模が大きくなっていて、独自の `PCH` を使う状態になっているのであれば指定するようにすると良いです。


### **YourProjectName.Build.cs** で `PCHUsage` を指定し、 `UnrealBuildTool` をカスタマイズする方法

[What’s needed for using C++17 の該当のリプライ](https://forums.unrealengine.com/t/whats-needed-for-using-c-17/124529/4)

これは `C++17` ではなく、更に新しい最新の環境を使うための設定です。
`Visual Studio` のコンパイラである `cl` のオプション `/std:c++latest` を指定するための設定です。
ただ、単純に `C++17` に読み替えればそのまま利用できます。

具体的には以下のような指定をしています。

```C#:YourProjectName.Build.cs
	PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;
	CppStandard = CppStandardVersion.Latest;
```

これについては前項のとおりです。

`UnrealBuildTool` の変更点については、 `/std:c++latest` を追加する方法の説明となっています。

ですが、 `/std:c++latest` も `/std:c++17` も、現在の `UnrealBuildTool` で問題なく指定されるようになっています。
そのため、これは過去の情報だと思うので、このリプライについてはここまでにしておきます。


----
## ここまでのまとめ

```C#:YourProjectName.Build.cs
		// PCHUsage の設定
		// 最近のテンプレートで記載されているのでそのままでよい。
		PCHUsage = PCHUsageMode.UseExplicitOrSharedPCHs;

		// CppStandard の設定
		// 任意のバージョンを指定する。
		//CppStandard = CppStandardVersion.Default;	//既定値。C++14が使われる。
		//CppStandard = CppStandardVersion.Cpp14;
		CppStandard = CppStandardVersion.Cpp17;
		//CppStandard = CppStandardVersion.Latest;

		// PrivatePCHHeaderFile の設定
		// 初期状態のプロジェクトであれば指定しなくてもエラーにならない。
		// 必要に応じて指定する。
		PrivatePCHHeaderFile = "YourProjectUniquePCH.h";
```


----
## もう一つのお題、デフォルト時

`CppStandard` を指定しなかった場合の挙動については以下のとおりです。

* `IntelliSense` の設定は明示的に `C++14` が指定されます。
	* `Intermediate/ProjectFiles/ProjectName.vcxproj` の `/PropertyGroup/AdditionalOptions` にて指定されています。
	* `Visual Studio` 上ではプロジェクトのプロパティの `構成プロパティ > NMAKE > IntelliSense > その他のオプション` に `/std::c++14` が指定されています。
* コンパイラオプションは指定されません。
	* コンパイラに渡すオプションは、ソースファイルごとにレスポンスファイルが生成され、その内で指定されます。
	* `Intermediate/Build/Win64/UE4Editor/Development/YourProjectName/YourSourceFile.cpp.obj.response` 等
	* （パスはビルドターゲット毎に異なります。）
	* `CppStandard = CppStandardVersion.Default` （既定値）の場合は何も記述されません。
	* つまりは `Visual Studio` の既定値である `C++14` となります。
	* `CppStandard = CppStandardVersion.Cpp14` を指定した場合は明示的に `/std:c++14` が記述されます。
	* 詳しくは [Visual Studio 2017 の言語バージョン](#visualstudio2017languagestandardversion) を参照してください。


## 設定で利用した各種値について

### UnrealBuildTool.CppStandardVersion

```C#:Engine\Source\Programs\UnrealBuildTool\System\CppCompileEnvironment.cs

namespace UnrealBuildTool
{
//...
	/// <summary>
	/// Specifies which language standard to use. This enum should be kept in order, so that toolchains can check whether the requested setting is >= values that they support.
	/// 使用する言語規格を指定します。この列挙体はツールチェーンが要求された設定がサポートしている以上の値であるかどうかがチェックできるように、順番に並べる必要があります。
	/// </summary>
	public enum CppStandardVersion
	{
		/// <summary>
		/// Use the default standard version
		/// </summary>
		Default,

		/// <summary>
		/// Supports C++14
		/// </summary>
		Cpp14,

		/// <summary>
		/// Supports C++17
		/// </summary>
		Cpp17,

		/// <summary>
		/// Latest standard supported by the compiler
		/// </summary>
		Latest,
	}
//...
}
```

### UnrealBuildTool.TargetBuildEnvironment

```C#:Engine\Source\Programs\UnrealBuildTool\Configuration\TargetRules.cs
namespace UnrealBuildTool
{
//...
	/// <summary>
	/// Specifies whether to share engine binaries and intermediates with other projects, or to create project-specific versions. By default,
	/// editor builds always use the shared build environment (and engine binaries are written to Engine/Binaries/Platform), but monolithic builds
	/// and programs do not (except in installed builds). Using the shared build environment prevents target-specific modifications to the build
	/// environment.
	/// エンジンのバイナリや中間ファイルを他のプロジェクトと共有するか、プロジェクト固有のバージョンを作成するかを指定します。
	/// デフォルトではエディタビルドは常に共有ビルド環境を使用します（エンジンバイナリは Engine/Binaries/Platform に書き込まれます）が、
	/// モノリシックビルドやプログラムは使用しません（インストール済みのビルドを除く）。
	/// 共有ビルド環境を使用することで、ターゲット固有のビルド環境の変更を防ぐことが出来ます。
	/// </summary>
	[Serializable]
	public enum TargetBuildEnvironment
	{
		/// <summary>
		/// Engine binaries and intermediates are output to the engine folder. Target-specific modifications to the engine build environment will be ignored.
		/// エンジンのバイナリと中間ファイルは engine フォルダに出力されます。エンジンのビルド環境に対するターゲット固有の変更は無視されます。
		/// </summary>
		Shared,

		/// <summary>
		/// Engine binaries and intermediates are specific to this target
		/// エンジンのバイナリや中間ファイルはこのターゲットに特化したものです。
		/// </summary>
		Unique,
	}
//...
}
```

### UnrealBuildTool.PCHUsageMode

```C#:Engine\Source\Programs\UnrealBuildTool\Configuration\ModuleRules.cs

namespace UnrealBuildTool
{
//...
	/// <summary>
	/// ModuleRules is a data structure that contains the rules for defining a module
	/// </summary>
	public class ModuleRules
	{
		/// <summary>
		/// What type of PCH to use for this module.
		/// このモジュールに使用する PCH の種類。
		/// </summary>
		public enum PCHUsageMode
		{
			/// <summary>
			/// Default: Engine modules use shared PCHs, game modules do not
			/// Default: エンジンモジュールは共有 PCH を使用し、ゲームモジュールは使用しません。
			/// </summary>
			Default,

			/// <summary>
			/// Never use any PCHs.
			/// どの PCH も使用しません
			/// </summary>
			NoPCHs,

			/// <summary>
			/// Never use shared PCHs.  Always generate a unique PCH for this module if appropriate
			/// どの 共有 PCH も使用しません。必要に応じて、常にこのモジュール用のユニークな PCH を生成します。
			/// </summary>
			NoSharedPCHs,

			/// <summary>
			/// Shared PCHs are OK!
			/// 共有 PCH は OK!
			/// </summary>
			UseSharedPCHs,

			/// <summary>
			/// Shared PCHs may be used if an explicit private PCH is not set through PrivatePCHHeaderFile. In either case, none of the source files manually include a module PCH, and should include a matching header instead.
			/// PrivatePCHHeaderFile で明示的なプライベート PCH を指定していない場合は、共有 PCH が使用されます。いずれの場合も、どのソースファイルも手動でモジュール PCH をインクルードせず、代わりに一致するヘッダをインクルードする必要があります。
			/// </summary>
			UseExplicitOrSharedPCHs,
		}
//...
	}
}
```

### UnrealBuildTool.ModuleRules.PCHUsage

```C#:Engine\Source\Programs\UnrealBuildTool\Configuration\ModuleRules.cs

namespace UnrealBuildTool
{
	/// <summary>
	/// ModuleRules is a data structure that contains the rules for defining a module
	/// ModuleRules はモジュールを定義するためのルールを含むデータ構造です。
	/// </summary>
	public class ModuleRules
	{
		/// <summary>
		/// Precompiled header usage for this module
		/// このモジュールのプリコンパイルヘッダの使い方
		/// </summary>
		public PCHUsageMode PCHUsage
		{
			get
			{
				if (PCHUsagePrivate.HasValue)
				{
					// Use the override
					// オーバーライドされたものを使用します。
					return PCHUsagePrivate.Value;
				}
				else if(Target.bIWYU || DefaultBuildSettings >= BuildSettingsVersion.V2)
				{
					// Use shared or explicit PCHs, and enable IWYU
					// 共有、又は明示された PCH を使用し、 IWYU を可能にします。
					return PCHUsageMode.UseExplicitOrSharedPCHs;
				}
				else if(Plugin != null)
				{
					// Older plugins use shared PCHs by default, since they aren't typically large enough to warrant their own PCH.
					// 古いプラグインでは、独自の PCH を使用するほど大きくないので、共有 PCH をデフォルトで使用しています。
					return PCHUsageMode.UseSharedPCHs;
				}
				else
				{
					// Older game modules do not enable shared PCHs by default, because games usually have a large precompiled header of their own.
					// 古いゲームモジュールは、デフォルトでは共有 PCH を有効にしていません。なぜなら、ゲームは通常、独自の大きなプリコンパイルヘッダを持っているからです。
					return PCHUsageMode.NoSharedPCHs;
				}
			}
			set { PCHUsagePrivate = value; }
		}
		private PCHUsageMode? PCHUsagePrivate;
	}
}
```


## もっと詳しい話

### UnrealBuildTool.TargetRules.bOverrideBuildEnvironment

```C#:Engine\Source\Programs\UnrealBuildTool\Configuration\TargetRules.cs
namespace UnrealBuildTool
{
//...
	/// <summary>
	/// TargetRules is a data structure that contains the rules for defining a target (application/executable)
	/// TargetRules は、ターゲット（アプリケーション／実行可能ファイル）を定義するためのルールを含むデータ構造です。
	/// </summary>
	public abstract partial class TargetRules
	{
//...
		/// <summary>
		/// Whether to ignore violations to the shared build environment (eg. editor targets modifying definitions)
		/// 共有ビルド環境への違反を無視するかどうか（例：エディタターゲットによる定義の変更）
		/// </summary>
		[CommandLine("-OverrideBuildEnvironment")]
		public bool bOverrideBuildEnvironment = false;
//...
	}
//...
}
```

`UnrealBuildTool` の以下の箇所で使われています。

```C#:Engine\Source\Programs\UnrealBuildTool\Configuration\UEBuildTarget.cs
//...
namespace UnrealBuildTool
{
//...
	/// <summary>
	/// A target that can be built
	/// </summary>
	class UEBuildTarget
	{
		/// <summary>
		/// Validates that the build environment matches the shared build environment, by comparing the TargetRules instance to the vanilla target rules for the current target type.
		/// TargetRules インスタンスを現在のターゲットタイプのバニラ（オリジナルの状態）のターゲットルールと比較することで、ビルド環境が共通ビルド環境と一致するかどうかを検証します。
		/// </summary>
		static void ValidateSharedEnvironment(RulesAssembly RulesAssembly, string ThisTargetName, CommandLineArguments Arguments, TargetRules ThisRules)
		{
			// Allow disabling these checks
			if(ThisRules.bOverrideBuildEnvironment)
			{
				return;
			}
//...
		}
	}
}

```

共通ビルド環境と異なる状態でのビルドを許可するか、とのことです。
今回の場合は共通 PCH の使用状況の差ですが、他の項目もチェックしてくれています。
具体的なチェック項目についてはここでは割愛します。

> NOTE:
> 更に正確な挙動を知りたい場合は `UnrealBuildTool` のソースを読むことをおすすめします。


### VisualStudio2017LanguageStandardVersion
Visual Studio 2017 の言語バージョン

[/std (Specify Language Standard Version)](https://docs.microsoft.com/ja-jp/cpp/build/reference/std-specify-language-standard-version?view=msvc-150)
`Visual Studio 2017` の言語バージョンの指定オプションのドキュメントです。
一部を引用します。（日本語訳版が微妙な機械翻訳なので英語版から翻訳し直しています。）

> By default, /std:c++14 is specified, which disables language and standard library features found in later versions of the C++ language standard. Use /std:c++17 to enable C++17 standard-specific features and behavior. To explicitly enable the currently implemented compiler and standard library features proposed for the next draft standard, use /std:c++latest . All C++20 features require /std:c++latest ; when the implementation is complete, a new /std:c++20 option will be enabled.
> 
> The default /std:c++14 option enables the set of C++14 features implemented by the MSVC compiler. This option disables compiler and standard library support for features that are changed or new in more recent versions of the language standard. It doesn't disable some C++17 features already implemented in previous releases of the MSVC compiler. To avoid breaking changes for users who have already taken dependencies on the features available in or before Visual Studio 2015 Update 2, these features remain enabled when the /std:c++14 option is specified:

> デフォルトでは、/std:c++14が指定されており、C++言語規格の後続バージョンに見られる言語および標準ライブラリの機能が無効になっています。C++17 規格固有の機能や動作を有効にするには、/std:c++17 を使用します。次期標準案で提案されている、現在実装されているコンパイラおよび標準ライブラリ機能を明示的に有効にするには、/std:c++latest を使用します。C++20 のすべての機能には /std:c++latest が必要です。実装が完了したら、新しい /std:c++20 オプションが有効になります。
>
> デフォルトの /std:c++14 オプションは、MSVC コンパイラに実装されている C++14 機能のセットを有効にします。このオプションは、言語標準のより最近のバージョンで変更または新規に追加された機能に対するコンパイラおよび標準ライブラリのサポートを無効にします。MSVC コンパイラーの以前のリリースですでに実装されている一部の C++17 機能は無効になりません。Visual Studio 2015 Update 2 以前で利用可能な機能に既に依存しているユーザーの変更を回避するため、/std:c++14 オプションを指定してもこれらの機能は有効なままです。

「**デフォルトでは、/std:c++14が指定されており**」、とのことなので、ツールとして `Visual Studio 2017` を使用している場合のデフォルトは `C++14` となるようです。

> NOTE:
> `Visual Studio 2019` でも同様です。


----
## あとがき

特に利用する予定はありませんでしたが、気になったので情報を探してみましたが、まとまっていなかったのでまとめてみました。
どなたかの参考になれば幸いです。

ここまで読んでいただきありがとうございました！


----
## 参考リンク

* Unreal Engine 4 ドキュメント
	* [Unreal Engine 4 ドキュメント > 新機能 > リリースノート > Unreal Engine 4.22 リリース ノート](https://docs.unrealengine.com/ja/WhatsNew/Builds/ReleaseNotes/4_22/index.html)
	* [Unreal Engine 4 ドキュメント > プロダクション パイプラインをセットアップする > ビルド ツール > UnrealBuildTool](https://docs.unrealengine.com/en-US/ProductionPipelines/BuildTools/UnrealBuildTool/IWYU/index.html)
	* [Unreal Engine 4 ドキュメント > プロダクション パイプラインをセットアップする > ビルド ツール > UnrealBuildTool > ターゲット](https://docs.unrealengine.com/ja/ProductionPipelines/BuildTools/UnrealBuildTool/TargetFiles/index.html)
	* [Unreal Engine 4 ドキュメント > プロダクション パイプラインをセットアップする > ビルド ツール > UnrealBuildTool > モジュール](https://docs.unrealengine.com/ja/ProductionPipelines/BuildTools/UnrealBuildTool/ModuleFiles/index.html)
* ANSWERHUB
	* [How to enable c++17 in uproject, VS requires compiler flag /std:c++17](https://answers.unrealengine.com/questions/820557/view.html)
	* [How to build UE4.22 Plugins with C++17?](https://answers.unrealengine.com/questions/898017/view.html)
* FORUMS
	* [Issues with 4.22 C++17 Support](https://forums.unrealengine.com/t/issues-with-4-22-c-17-support/125442)
	* [What’s needed for using C++17](https://forums.unrealengine.com/t/whats-needed-for-using-c-17/124529)
	* [C++17 was disabled in PCH file but is currently enabled](https://forums.unrealengine.com/t/c-17-was-disabled-in-pch-file-but-is-currently-enabled/139539)
* Visual Studio ドキュメント
	* [/std (Specify Language Standard Version)](https://docs.microsoft.com/ja-jp/cpp/build/reference/std-specify-language-standard-version?view=msvc-150)


----
おしまい。
