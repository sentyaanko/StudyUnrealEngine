# ■ BluePrints/AI の内容
* Blackboard 等、 AI モジュール類が置かれている。
* 敵 (Spider/Goblin) 、プレイヤー用の AIController と BehaviorTree はそれぞれのサブフォルダに格納されている。

## ■ フォルダ一覧
| フォルダ名 | 用途 |
| ----- | ----- |
| BossAI | Spider 用  |
| GruntAI | Goblin 用  |
| PlayerAI | プレイヤー用 |

## ■ BP 一覧
* すべてのネイティブ親クラスと親クラスはおなじになっている。

| 名前 | 親クラス | 用途 | 参照元 |
| ----- | ----- | ----- | ----- |
| BTTask_IsTargetSurrounded | BTDecorator_BlueprintBase | **中身は Decorator なのにファイル名は Task になっている。要確認**<br>指定の Actor の指定距離内に指定以上の Actor がいる場合に真を返す | BT_Player |
| BTTask_IsPlayingHighOriorityMontage | BTDecorator_BlueprintBase | **中身は Decorator なのにファイル名は Task になっている。要確認**<br>高い優先順位の AnimationMontage が再生中の場合は真を返す | BT_Player |
| BTDesc_CheckHealth | BTDecorator_BlueprintBase | Player 自身の HP が指定された割合**以下**の場合は真を返す<br>**Blackboard にプレイヤーの HP の割合を置いた方が実装として素直なように感じる** | BT_Player |
| BTDesc_IsAlive | BTDecorator_BlueprintBase | 自身が生きている場合は真を返す | BT_NPC |
| BTDesc_CheckItem | BTDecorator_BlueprintBase | 指定スロットに指定のアイテムを設定していた場合に真を返す | BT_Player |
| BTService_RandomMoveSpeed | BTService_BlueprintBase | 自身の移動速度を指定範囲内のランダムに設定 | BT_NPC |
| BTService_FindNearestTarget | BTService_BlueprintBase | 自身と反する Player/Enemy Tag を持つ最も近い Actor とその距離を Blackboard に書き込む<br>**Actor は毎ループ Blackboard へ書き込み、 Distance はループ終了後に Blackboard に書き込む**  | BT_Boss<br>BT_NPC<br>BT_Player |
| BTService_DistanceToTarget | BTService_BlueprintBase | BTService_FindNearestTarget で設定した Actor までの距離を測りなおして Blackboard に書き込む | BT_Boss<br>BT_NPC |
| BTTask_GoAroundTarget | BTTask_BlueprintBase | BTService_FindNearestTarget で設定した Actor の周辺でランダムな位置を Blackboard に書き込む | BT_NPC<br>BT_Player |
| BTTask_AttackSkill | BTTask_BlueprintBase | 自身に対して DoSkillAtack を呼び出す<br>**Delay が固定なので、 DoSkillAtack から適切な値を返せないか要確認** | BT_Boss<br>BT_Player |
| BTTask_AttackMelee | BTTask_BlueprintBase | 自身に対して DoMeleeAtack を呼び出す<br>**Delay が固定なので、 DoSkillAtack から適切な値を返せないか要確認** | BT_NPC<br>BT_Player |
| BTTask_StopAndRotate | BTTask_BlueprintBase | 移動を止めて、ターゲットの方向を向かせる | BT_Player |
| BTTask_StopAttack | BTTask_BlueprintBase | 現在有効になっているアビリティをすべてキャンセルする<br>**AbilityTag の指定をしていない。要確認** | BT_Player |
| BTTask_UseItem | BTTask_BlueprintBase | 自身に対して UseItemPotion を呼び出す<br>**Delay していない。要確認** | BT_Player |
| EQS_PlayerCVontext | EnvQueryContext_BlueprintBase | BP_PlayerCharacter を探す環境クエリ | GruntAI/EQ_FindPlayer |

## ■ その他のファイル一覧
| 名前 | 型 | 用途 |
| ----- | ----- | ----- |
| BB_Base | Blackboard | AI 用データ格納用 |


# ■ BluePrints/AI/BossAI の内容
## ■ AIC_Boss
* Spider 用の AI Controller
* ネイティブ親クラス： AIController
* 親クラス： 同じ
* 参照元： Blueprints/Boss/NPC_SpiderBoss

## ■ BT_Boss
* Behavior Tree
* Spider 用のビヘイビアツリー
* 参照元： AIC_Boss

# ■ BluePrints/AI/GruntAI の内容
## ■ AIC_NPC
* 近接攻撃 Goblin 用の AI Controller
* ネイティブ親クラス： AIController
* 親クラス： 同じ
* 参照元： Blueprints/NPC/NPC_GoblinBP

## ■ AIC_NPC_Range
* 間接攻撃 Goblin 用の AI Controller
* ネイティブ親クラス： AIController
* 親クラス： AIC_NPC
* 参照元： Blueprints/NPC/NPC_Goblin_Level_02

## ■ BT_NPC
* Behavior Tree
* Goblin 用のビヘイビアツリー
* 参照元： AIC_NPC

## ■ EQ_FindPlayer
* Environmemt Query 
* 距離が一番近い BP_PlayerCharacter を探す環境クエリ
* 参照元： BT_NPC


# ■ BluePrints/AI/PlayerAI の内容
## ■ AIC_Player
* Player 用の AI Controller
* ネイティブ親クラス： AIController
* 親クラス： 同じ
* 参照元： Blueprints/BP_GameMode

## ■ BT_Player
* Behavior Tree
* Player 用のビヘイビアツリー
* 参照元： AIC_Player


----
以上。
