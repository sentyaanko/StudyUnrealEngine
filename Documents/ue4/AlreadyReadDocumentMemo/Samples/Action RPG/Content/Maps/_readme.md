# ■ Maps の内容
* レベルファイルとそれに依存するものが置かれている。
	* 依存するものについて、具体的には Landscape と HLOD 。

## ■ レベルファイル一覧

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| ActionRPG_Dungeon02_Asset | ゲーム画面のアセット用レベル | ActionRPG_P<br>ActionRPG_Dungeon02_Asset_0_HLOD |
| ActionRPG_Dungeon02_Lights | ゲーム画面のライト用レベル | ActionRPG_P |
| ActionRPG_Main | タイトル画面用シーン | SQ_MainMenu |
| ActionRPG_P | ゲーム画面のパーシスタントレベル | SQ_Intro_Warrior_AnimData |

## ■ ライトマップデータファイル一覧

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| ActionRPG_Dungeon02_Asset_BuiltData | ActionRPG_Dungeon02_Asset 用 | ActionRPG_Dungeon02_Asset |
| ActionRPG_Dungeon02_Lights_BuiltData | ActionRPG_Dungeon02_Lights 用 | ActionRPG_Dungeon02_Lights |
| ActionRPG_Main_BuiltData | ActionRPG_Main 用 | ActionRPG_Main |
| ActionRPG_P_BuiltData | ActionRPG_P 用 | ActionRPG_P |

## ■ ファイル一覧 ActionRPG_P_sharedassets
* ActionRPG_P で利用している Landscape のレイヤー情報置き場
* ファイルはすべて　Landscape Layer

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| CaveDirt_LayerInfo | 濡れた泥用 | ActionRPG_P |
| CaveMud_LayerInfo | 泥用 | ActionRPG_P |
| Wetness_LayerInfo | 濡れ用 | ActionRPG_P |

## ■ ファイル一覧 HLOD
* ActionRPG_Dungeon02_Asset で利用している HLOD に関するファイル置き場

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| ActionRPG_Dungeon02_Asset_0_HLOD | HLOD Proxy | HLOD の設定ファイル | ActionRPG_Dungeon02_Asset |
| ActionRPG_Dungeon02_Asset_0_SM_* | Static Mesh | HLOD 用<br>２１ファイル | ActionRPG_Dungeon02_Asset |
| M_ActionRPG_Dungeon02_Asset_0_SM_\* | Material Instance | ActionRPG_Dungeon02_Asset_0_SM_* 用<br>２１ファイル | ActionRPG_Dungeon02_Asset |
| T_ActionRPG_Dungeon02_Asset_0_SM_\*_Diffuse | Texture | ActionRPG_Dungeon02_Asset_0_SM_* 用<br>ベースカラー<br>２１ファイル | ActionRPG_Dungeon02_Asset |
| T_ActionRPG_Dungeon02_Asset_0_SM_\*_Normal | Texture | ActionRPG_Dungeon02_Asset_0_SM_* 用<br>ノーマルマップ<br>２１ファイル | ActionRPG_Dungeon02_Asset |

----
以上。

