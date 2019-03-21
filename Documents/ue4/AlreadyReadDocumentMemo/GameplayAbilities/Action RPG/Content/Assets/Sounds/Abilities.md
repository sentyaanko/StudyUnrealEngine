# ■ Assets/Sounds/Abilities の内容

## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Ability_FireBallCast01 | A_Ability_FireBallCast_Cue |
| A_Ability_FireBallCast02 | A_Ability_FireBallCast_Cue |
| A_Ability_FireWaveCast01 | A_Ability_FireWaveCast_Cue |
| A_Ability_FireWavePowerup01 | A_Ability_FireWavePowerup_Cue |
| A_Ability_FireWavePowerup02 | A_Ability_FireWavePowerup_Cue |
| A_Ability_MeteorCast01 | AM_Skill_Meteor |
| A_Ability_MeteorImpact01 | A_Ability_MeteorImpact_Cue |
| A_Ability_MeteorImpact02 | A_Ability_MeteorImpact_Cue |
| A_Ability_MeteorWhoosh | A_Ability_MeteorWhoosh_Cue |
| A_Ability_TimeSlow01 | A_Ability_TimeSlow_Cue |

* 以下、他と違い、Fire**B**all 大文字になっている。わかりづらい。
	* A_Ability_Fire**B**allCast01
	* A_Ability_Fire**B**allCast02
	* A_Ability_Fire**B**allCast_Cue
* A_Ability_MeteorCast01 **これだけCueを用意していない。わかりづらい。**

## ■ SoundCue 一覧
| ファイル名 | 用途 | 用途 |
| ----- | ----- | ----- |
| A_Ability_FireBallCast_Cue | NPC_Gobline_Level03 | 死亡時の時のエフェクトとしてEventGraphで指定 |
|  | AM_SkillFireball | Notifiesで指定 |
| A_Ability_FireWaveCast_Cue | AM_SkillFirewave | Notifiesで指定 |
| A_Ability_FireWavePowerup_Cue | AM_SkillFirewave | Notifiesで指定 |
| A_Ability_MeteorImpact_Cue | AM_Skill_Meteor | Notifiesで指定(4回) |
|  | Attack02_Fire | Notifiesで指定 |
|  | Attack03 | Notifiesで指定 |
| A_Ability_MeteorWhoosh_Cue | AM_Skill_Meteor | Notifiesで指定 |
| | BP_SlimeBall | AudioComponentのソースで指定 |
| A_Ability_TimeSlow_Cue | AM_Attack_Sword | Notifiesで指定(Combo3とCombo4) |
|  | Attack02_Fire | Notifiesで指定 |
|  | Attack03 | Notifiesで指定 |

* AM_SkillFire**w**ave ここだけ小文字になっている。わかりづらい。

----
以上。
