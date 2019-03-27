# ■ Assets/Sounds/Music の内容
* BGM 関連が３曲置かれている。
* **Stingers という BGM だけなぜかフォルダ分けされている。わかりづらい。**
* **BGM の再生方法に一貫性がない。わかりづらい。**

## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| Dungeons_EndBossBattle | Dungeons_ThemeCue |
| ice_BossBattle01 | ice_BossBattle01_Cue |
| Stingers/A_Music_Stinger02 | Stingers/A_Music_Stinger02_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| Dungeons_ThemeCue | ActionRPG_P | EventGraph の BeginPlay 内で指定 |
| ice_BossBattle01_Cue | WB_Title | EventGraph の Construct 内で指定 |
| Stingers/A_Music_Stinger02_Cue | WB_WaveEnd | Timeline で指定 |

----
以上。
