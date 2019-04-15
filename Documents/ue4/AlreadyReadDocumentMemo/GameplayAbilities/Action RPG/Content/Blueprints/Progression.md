# ■ Brueprints/Progression の内容
敵の出現テーブルとその型の定義が置いてある。

## ■ ファイル一覧

| ファイル名 | 型 | 参照元 |
| ----- | ----- | ----- |
| SpawnGroupStruct | Structure | BP_GameMode<br>WaveStruct |
| WaveStruct | Structure | BP_GameMode<br>WaveProgression |
| WaveProgression | DataTable | BP_GameMode |

## ■ SpawnGroupStruct
```cpp
struct SpawnGroupStruct
{
 TArray< BP_Enemy_Character > enemies; //!< 一度に出現する敵の組み合わせ
};
```

## ■ WaveStruct
```cpp
struct WaveStruct
{
 TArray< SpawnGroupStruct > SpawnGroup; //!< 敵の組み合わせの配列
 integer WaveTime; //!< 制限時間
};
```

## ■ WaveProgression
* WaveStruct の DataTable 。
* BP_GameMode の StartNewWave イベントにて敵の出現テーブルを更新する多彩に参照。

| レコード名 | WaveTime | SpawnGroup[0] | SpawnGroup[1] | SpawnGroup[2] |
| ----- | ----- | ----- | ----- | ----- |
| Wave_1 | 60 | NPC_Goblin_Level_01 x1 | NPC_Goblin_Level_01 x2 | NPC_Goblin_Level_01 x2 |
| Wave_2 | 60 | NPC_Goblin_Level_01 x2 | NPC_Goblin_Level_02 x1<br>NPC_Goblin_Level_01 x1 | NPC_Goblin_Level_02 x2<br>NPC_Goblin_Level_01 x1 |
| Wave_3 | 60 | NPC_Goblin_Level_02 x3 |　NPC_Goblin_Level_03 x1<br>NPC_Goblin_Level_02 x2 |　NPC_Goblin_Level_02 x2<br>NPC_Goblin_Level_03 x2 |
| Wave_4 | 60 | NPC_Goblin_Level_02 x3<br>NPC_Goblin_Level_03 x1 |　NPC_Goblin_Level_03 x3 |　NPC_Goblin_Level_03 x2<br>NPC_SpiderBoss x1 |
| Wave_5 | 60 | NPC_Goblin_Level_01 x6 |　NPC_Goblin_Level_02 x4 |　NPC_Goblin_Level_03 x3 |


----
以上。
