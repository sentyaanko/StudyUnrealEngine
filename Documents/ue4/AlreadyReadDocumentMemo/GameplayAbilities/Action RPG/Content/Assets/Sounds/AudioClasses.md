# ■ Assets/Sounds/AudioClasses の内容

## ■ SoundClass 一覧
### ■ PassiveSoundMix 名 一覧
| SoundClass 名 | PassiveSoundMix 名 | 用途 |
| ----- | ----- | ----- |
| SC_RPG_Master | SM_Mixer | |
| SC_SFX | None | |
| SC_Player | | |
| SC_Abilities | SM_Abilities | |
| SC_Slomo | SM_Slomo | |
| SC_Hero | | |
| SC_Items | SM_Items | |
| SC_Weapons | | |
| SC_Enemy | SM_Enemies | |
| SC_UI | | |
| SC_Music | None | |

### ■ SoundWave/SoundCue 名 一覧
| SoundClass 名 | SoundCue 名 | SoundWave 名 |
| ----- | ----- | ----- |
| SC_RPG_Master | |
| SC_SFX | A_Ambient_Fire01_Cue | A_Ambient_Fire01 |
| | A_Ambient_Wind02_Cue | A_Ambient_Wind02 |
| SC_Player | |
| SC_Abilities | A_Ability_FireballCast_Cue | A_Ability_FireBallCast01<br>A_Ability_FireBallCast02 |
| | A_Ability_FireWaveCast_Cue | A_Ability_FireWaveCast01 |
| | A_Ability_FireWavePowerup_Cue | A_Ability_FireWavePowerup_01<br>A_Ability_FireWavePowerup_02 |
| | | A_Ability_MeteorCast01 |
| | A_Ability_MeteorImpact_Cue | A_Ability_MeteorImpact01<br>A_Ability_MeteorImpact02 |
| | A_Ability_MeteorWhoosh_Cue | A_Ability_MeteorWhoosh_01 |
| | | A_Ability_TimeSlow01 |
| SC_Slomo | A_Ability_TimeSlow01_Cue | |
| SC_Hero | A_Character_Collapse_Cue | A_Character_Collapse01 |
| | A_Character_Effort_Cue | A_Character_Effort01<br>A_Character_Effort03<br>A_Character_Effort04 |
| | A_Character_Expire_Cue | A_Character_Expire01<br>A_Character_Expire02<br>A_Character_Expire03 |
| | A_Character_Grunt_Cue | A_Character_Grunt01<br>A_Character_Grunt02<br>A_Character_Grunt03 |
| | A_Character_Heal_Cue | A_Character_Heal01 |
| | A_Character_Heal_Mana_Cue | A_Character_Heal01_Mana |
| | A_Character_Hit_Cue | A_Character_Hit01<br>A_Character_Hit02<br>A_Character_Hit03 |
| | A_Character_Potion_Cue | A_Character_Potion01<br>A_Character_Potion02 |
| | A_Character_Powerup_Cue | A_Character_Powerup01 |
| | A_Character_Step_Cue | A_Character_Step01<br>A_Character_Step02<br>A_Character_Step03<br>A_Character_Step04<br>A_Character_Step05 |
| | A_Character_Yell_Cue | A_Character_Yell01<br>A_Character_Yell02 |
| SC_Items | |
| SC_Weapons | A_Weapon_FireSwing_Cue | |
| | A_Axe_Swing_Cue | A_Axe_Swing01<br>A_Axe_Swing02<br>A_Axe_Swing03 |
| | A_Hammer_Impact_Cue | A_Hammer_Impact01<br>A_Hammer_Impact02<br>A_Hammer_Impact03 |
| | A_Hammer_Swing_Cue | A_Hammer_Swing01<br>A_Hammer_Swing02<br>A_Hammer_Swing03 |
| | A_Sword_Swing_Cue | A_Sword_Swing01<br>A_Sword_Swing02<br>A_Sword_Swing03 |
| SC_Enemy | A_Guardian_Attack_Cue | A_Guardian_Attack01<br>A_Guardian_Attack02 |
| | A_Guardian_Cast_Cue | A_Guardian_Cast01 |
| | A_Guardian_Cast2_Cue | A_Guardian_Cast03 |
| | A_Guardian_Death_Cue | A_Guardian_Death01<br>A_Guardian_Death02 |
| | A_Guardian_Footstep_Cue | A_Guardian_Footstep01<br>A_Guardian_Footstep02 |
| | A_Guardian_ImpactL_Cue | A_Guardian_Impact01<br>A_Guardian_Impact02<br>A_Guardian_Impact03<br>A_Guardian_Impact04 |
| | A_Guardian_Roar_02_Cue | A_Guardian_Roar02 |
| | A_Guardian_Roar_03_Cue | A_Guardian_Roar03 |
| | A_Guardian_Spawn_Cue | A_Guardian_Spawn01<br>A_Guardian_Spawn02 |
| | | A_Guardian_Swin01<br>A_Guardian_Swin02<br>A_Guardian_Swin03 |
| | A_Spider_Attack_Cue | A_Spider_Attack01<br>A_Spider_Attack02<br>A_Spider_Attack03 |
| | A_Spider_AttackVocal_Cue | A_Spider_Attack04 |
| | A_Spider_Charge_Cue | A_Spider_Charge01 |
| | A_Spider_Death_Cue | A_Spider_Death01 |
| | A_Spider_Land_Cue | A_Spider_Land01 |
| | A_Spider_LegLrg_Cue | A_Spider_LegLrg01<br>A_Spider_LegLrg02<br>A_Spider_LegLrg03<br>A_Spider_LegLrg04 |
| | A_Spider_React_Cue | A_Spider_React01<br>A_Spider_React02<br>A_Spider_React03 |
| | A_Spider_Spawn_Cue | A_Spider_Spawn01 |
| | A_Spider_Stun_Cue | A_Spider_Stun01 |
| | A_Spider_WalkLoop_Cue | A_Spider_WalkLoop02 |
| SC_UI | A_UI_Box_Confirm | |
| | A_UI_Hover | |
| | | A_UI_Select01<br>A_UI_Select02<br>A_UI_WaveEnd |
| SC_Music | Dungeons_ThemeCue | Dungeons_EndBossBattle |
| | Ice_BossBattle01_Cue | Ice_BossBattle01 |
| | A_Music_Stinger02_Cue | A_Music_Stinger02 |

* **A_Ability_TimeSlow01 は SC_Abilities を使用し、 A_Ability_TimeSlow01_Cue は SC_Slomo を使用する。想定通り？**
* **A_Weapon_FireSwing01-04 は SC_RPG_Master を使用し、 A_Weapon_FireSwing_Cue は SC_Weapons を使用する。想定通り？**
* A_Guardian_Impact**L**_Cue の L は必要なのか？
* A_UI_Box_Confirm は A_Hammer_Impact01-03 を使用。
* A_UI_Hover は A_Character_Step01-05 を使用。

## ■ SoundMix 一覧
| PassiveSoundMix 名 | 用途 |
| ----- | ----- |
| SM_Mixer | SC_SFX Volume 1.0<br>SC_Music Volume 0.65 |
| SM_Abilities | SC_Music Volume 0.45<br>SC_Enemy Volume 0.6 |
| SM_Slomo | SC_Music Volume 0.25 |
| SM_Items | SC_Music Volume 0.5<br>SC_Enemy Volume 0.5<br>SC_UI Volume 0.2<br>SC_Abilities Volume 0.5 |
| SM_Enemies | SC_Music Volume 0.8 |

## ■ SoundClass 構造
```
SC_RPG_Master
├─SC_SFX
│ ├─SC_Player
│ │ ├─SC_Abilities
│ │ │ └─SC_Slomo
│ │ ├─SC_Hero
│ │ ├─SC_Items
│ │ └─SC_Weapons
│ ├─SC_Enemy
│ └─SC_UI
└─SC_Music
```

----
以上。
