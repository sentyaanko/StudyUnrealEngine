# ■ Animations/Boss の内容
* Content/BluePrints/Boss/ABP_SpiderBoss から参照

| ファイル名 | 用途 |
| ----- | ----- |
| AM_Spider_Hit | 被ダメージ用 |
| AM_Spider_Melee | 近接攻撃用 |

# ■ AM_Spider_Hit
* 被ダメージ用 Animation Montage 。
* ２種類ある。

| Section | Montage | Notifieies |
| ----- | ----- | ----- |
| 1 | ExoGame_Greater_Spider_React_Heavy_Front | 全区間 StopAndStartAI_NS |
| 2 | ExoGame_Greater_Spider_React_Stunned | 同上 |

# ■ AM_Spider_Melee
* 近接攻撃用 Animation Montage 。
* ３種類ある。

| Section | Montage | Notifieies | Event Tag |
| ----- | ----- | ----- | ----- |
| 1 | ExoGame_Greater_Spider_Attack_Melee_C | 攻撃判定の区間 RangeAttackNS | Event.Montage.Shared.UseSkill |
| 2 | ExoGame_Greater_Spider_Attack_Melee_B | 同上 | 同上 |
| 3 | ExoGame_Greater_Spider_Attack_Melee | 同上 | 同上 |

----
以上。
