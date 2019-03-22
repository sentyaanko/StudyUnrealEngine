# ■ Animations/NPC の内容
* Content/BluePrints/NPC/NPC_AnimBP_Base から参照

| ファイル名 | 用途 |
| ----- | ----- |
| AM_Guardian_Attack | 近接攻撃用 |
| AM_Guardian_Attack02 | 遠隔攻撃用 |
| AM_Guardian_Falldown | 死亡用 |
| AM_Guardian_Hit | 被ダメージ用 |

# ■ AM_Guardian_Attack
* 近接攻撃用 Animation Montage 。
* １種類ある。

| Section | Montage | Notifieies | Event Tag |
| ----- | ----- | ----- | ----- |
| 1 | Enemy_Anim_Sword_Combat_Swing | 攻撃判定の区間 WeaponAttackNS | Event.Montage.Shared.WeaponHit |

# ■ AM_Guardian_Attack02
* 遠隔攻撃用 Animation Montage 。
* １種類ある。

| Section | Montage | Notifieies | Event Tag |
| ----- | ----- | ----- | ----- |
| 1 | Cast | 攻撃判定の区間 RangeAttackNS<br>攻撃判定の開始時に Particle P_Spit 再生<br>Sound Cue A_Guradian_Roar_02_Cue 再生 | Event.Montage.Shared.UseSkill<br><br><br> |

# ■ AM_Guardian_Falldown
* 死亡用 Animation Montage 。
* ２種類ある。

| Section | Montage | Notifieies |
| ----- | ----- | ----- |
| 1 | Death_Small_03 | 全区間 StopAndStartAI_NS<br>途中２回 Hit_Notify |
| 2 | Death_Small_05 | 同上 |

# ■ AM_Guardian_Hit
* 被ダメージ用 Animation Montage 。
* ３種類ある。

| Section | Montage | Notifieies |
| ----- | ----- | ----- |
| 1 | React_Heavy_Front | 全区間 StopAndStartAI_NS |
| 2 | React_Knockback_Front | 同上 |

----
以上。
