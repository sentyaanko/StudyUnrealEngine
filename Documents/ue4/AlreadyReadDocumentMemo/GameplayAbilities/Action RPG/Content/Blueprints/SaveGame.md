# ■ Brueprints/SaveGame の内容
ストレージに保存するための型の定義と Blueprint が置いてある。

## ■ Structure 一覧

| ファイル名 | 参照元 |
| ----- | ----- |
| GlobalOptionsStruct | BP_GameInstance<br>BP_MainMenuGameMode<br>GlobalOptionSaveGame<br>WB_OptionScreen |

## ■ BP 一覧

| ファイル名 | ネイティブ親クラス | 親クラス | 参照元 |
| ----- | ----- | ----- | ----- |
| GlobalOptionsSaveGame | SaveGame | SaveGame | BP_GameInstance |

## ■ GlobalOptionsStruct
```cpp
struct SpawnGroupStruct
{
 Boolean bMusic; //!< BGMを再生するか
 Boolean bSoundFX; //!< SEを再生するか
 Boolean bVibration; //!< 振動を有効にするか（未使用）
 Boolean bCameraShake; //!< カメラシェイクを有効にするか（未使用）
};
```

| 変数名 | 用途 |
| ----- | ----- |
| bMusic | SM_Mixer に SC_Music のボリュームを(true/false)で(1.0/0.001)を指定する。 |
| bSoundFX | SM_Mixer に SC_SFX のボリュームを(true/false)で(1.0/0.0)を指定する。 |

## ■ GlobalOptionsSaveGame
* BP_GameInstance にてストレージを利用したセーブロードを行う際に使用されている。

----
以上。
