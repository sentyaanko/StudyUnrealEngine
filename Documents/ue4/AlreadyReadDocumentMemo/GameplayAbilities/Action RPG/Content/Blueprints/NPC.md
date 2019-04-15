# ■ Brueprints/NPC の内容
Goblin 用の BlendSpace/Animation Blueprint/Blueprint/スポーン用の Actor が置いてある。

## ■ BlendSpace 一覧

| ファイル名 | 型 | 参照元 |
| ----- | ----- | ----- |
| Idle_Run_Guardian_1D | Blend Space 1D | NPC_AnimBP_Base |

## ■ BP 一覧

| ファイル名 | ネイティブ親クラス | 親クラス | 参照元 |
| ----- | ----- | ----- | ----- |
| NPC_SpawnBox | Actor | Actor | BP_GameMode<br>ActionRGP_P |
| NPC_AnimBP_Base | AnimInstance | AnimInstance | NPC_GoblinBP |
| NPC_GoblinBP | RPGCharacterBase | BP_EnemyCharacter | BTService_RandomMoveSpeed<br>NPC_Goblin_Level_01<br>NPC_Goblin_Level_02<br>NPC_Goblin_Level_03 |
| NPC_Goblin_Level_01 | RPGCharacterBase | NPC_GoblinBP | WaveProgression |
| NPC_Goblin_Level_02 | RPGCharacterBase | NPC_GoblinBP | WaveProgression |
| NPC_Goblin_Level_03 | RPGCharacterBase | NPC_GoblinBP | WaveProgression |

## ■ NPC_SpawnBox
* 敵の出現場所を設定するための Actor 。
* Level に配置されている。
* BP_GamoMode にてレベル内の NPC_SpawnBox を取得し、敵の出現場所として利用されている。
* コリジョンイベントもイベントを一切持たない、単に場所を決めるための Actor 。

## ■ Idle_Run_Guardian_1D
* Goblin の歩行用の 1D Blend Space 。

## ■ NPC_AnimBP_Base
* Goblin 用の Animation Blueprint 。

## ■ NPC_GoblinBP
* Goblin 用の基底クラス。
* Begin Play にて構築時の共通処理（武器の設定）を行っている
* On Damage にて被ダメージ時の共通処理（ダメージの原因からの再生するモンタージュの判定、ダメージを与えた Actor へ向くように回転）を行っている

## ■ 設定内容の差異

### ■ Default グループ
| グループ | 名前 | NPC_Goblin_Level_01 | NPC_Goblin_Level_02 | NPC_Goblin_Level_03 |
| ----- | ----- | ----- | ----- | ----- |
| Default | Weapon | GoblinWeapon_Base | GoblinWeapon_Axe | GoblinWeapon_Torch |
| Default | Is Weapon Attacked |  | ✓ | ✓ |
| Default | Time Bonus Per Kill | 2.0 | 3.0 | 4.0 |
| Default | Soal MIN | 1 | 2 | 3 |
| Default | Soul MAX | 3 | 4 | 5 |
| Abilities | Character Level | 1 | 2 | 3 |
| Abilities | Default Slotted Abilityies | GA_GoblinMelee | GA_GoblineRange01 | GA_GoblinMelee |
| Character<br>/Mesh<br>/Mesh | Mesh | SK_Exodus_Gruntling | SK_Exodus_Gruntling_Guardian | SK_Exodus_Gruntling_Avalanche |
| Character<br>/Mesh<br>/Transform | Relative Scale 3D | 1.25 | 1.5 | 1.661105 |
| Character<br>/Character Movement<br>/Custom Movement | Max Walk Speed | 200 | 150 | 200 |
| Character | Capsule Component | NPC_Gobline_Level_01<br>:CollisionCylinder | NPC_Gobline_Level_02<br>:CollisionCylinder | NPC_Gobline_Level_03<br>:CollisionCylinder |
| Pawn | AI Controller Class | AIC_NPC | AIC_NPC_Range | AIC_NPC |

----
以上。
