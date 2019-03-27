# ■ Assets/Sounds/UI の内容
* UI 用の SE が置かれている。
* **呼び出し方がまちまち( EventGraph / プロパティ内で指定 / Timeline （これはしょうがない）)。わかりづらい。**
* **このフォルダの SoundWave に対応した Cue は用意されていない。**

## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_UI_Select01 | WB_InGame_Finish の WB_ButtonText 内(２回)<br>WB_Title の EventGraph の Onclicked(StartGameBUttion)<br>WB_Title の Timeline の BonusAnim で指定 <br>WB_WaveEnd の Timeline の Anim_WaveComplete で指定 |
| A_UI_Select02 | WB_OnScreenControls の EventGraph の Update Timer<br>… BP_GameMode の Timer Event の UpdatePlayTimer 経由<br>… BP_GameMode の Increase NPC Kill Count 内<br>… BP_GameMode の SpawnNewWave 内<br>WB_Title の Timeline の TitleAnimation で指定 |
| A_UI_WavEnd | WB_InGame_Finish の EventGraph の PlayAllAnimation 内 |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_UI_Box_Confirm | WB_ButtonText<br>WB_Title | ボタンのプロパティ「 Appearance ＞ Style ＞ Pressed Sound 」で指定<br>ボタンのプロパティ「 Appearance ＞ Style ＞ Pressed Sound 」で指定(３箇所) |
| A_UI_UI_Hover | WB_ButtonText<br>WB_Title<br>WB_InveentryItem | ボタンのプロパティ「 Appearance ＞ Style ＞ Hovered Sound 」で指定<br>ボタンのプロパティ「 Appearance ＞ Style ＞ Hovered Sound 」で指定(３箇所)<br> ボタンのプロパティ「 Appearance ＞ Style ＞ Hovered Sound 」で指定 |


SoundQue の参照 SoundWave （このフォルダ外なので参考までに）

| ファイル名 | 参照 SoundWave |
| ----- | ----- |
| A_UI_Box_Confirm | A_Hammer_Impact01<br>A_Hammer_Impact02<br>A_Hammer_Impact03 |
| A_UI_Hover | A_Character_Step01<br>A_Character_Step02<br>A_Character_Step03<br>A_Character_Step04<br>A_Character_Step05 |

----
以上。
