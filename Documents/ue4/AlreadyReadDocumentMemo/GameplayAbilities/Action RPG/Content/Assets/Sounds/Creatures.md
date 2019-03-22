# ■ Assets/Sounds/Creatures の内容
敵の種類ごとにフォルダ分けされている。

# ■ Assets/Sounds/Creatures/Guardian の内容

## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Guardian_Attack01 | A_Guardian_Attack_Cue<br>A_Guardian_Spawn_Cue |
| A_Guardian_Attack02 | A_Guardian_Attack_Cue<br>A_Guardian_Spawn_Cue |
| A_Guardian_Cast01 | A_Guardian_Cast_Cue |
| A_Guardian_Cast03 | A_Guardian_Cast2_Cue |
| A_Guardian_Death01 | A_Guardian_Death_Cue |
| A_Guardian_Death02 | A_Guardian_Death_Cue |
| A_Guardian_Footstep01 | A_Guardian_Footstep_Cue |
| A_Guardian_Footstep02 | A_Guardian_Footstep_Cue |
| A_Guardian_Impact01 | A_Guardian_ImpactL_Cue |
| A_Guardian_Impact02 | A_Guardian_ImpactL_Cue |
| A_Guardian_Impact03 | A_Guardian_ImpactL_Cue |
| A_Guardian_Impact04 | A_Guardian_ImpactL_Cue |
| A_Guardian_Roar02 | A_Guardian_Roar_02_Cue |
| A_Guardian_Roar03 | A_Guardian_Roar_03_Cue |
| A_Guardian_Spawn01 | A_Guardian_Spawn_Cue |
| A_Guardian_Spawn02 | A_Guardian_Spawn_Cue |
| A_Guardian_Swing01 | A_Guardian_Attack_Cue |
| A_Guardian_Swing02 | A_Guardian_Attack_Cue |
| A_Guardian_Swing03 | A_Guardian_Attack_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_Guardian_Attack_Cue | Enemy_Anim_Sword_Combat_Swing | Notifiesで指定 |
| A_Guardian_Cast_Cue | SQ_Intro_Master | Audio で指定 |
| A_Guardian_Cast2_Cue | SQ_Intro_Master | Audio で指定 |
| A_Guardian_Death_Cue | Death | Notifiesで指定 |
| | Death_Small_03 | Notifiesで指定 |
| | Death_Small_05 | Notifiesで指定 |
| A_Guardian_Footstep_Cue | Gruntling_Run | Notifiesで指定(4回) |
| | Gruntling_Walk | Notifiesで指定(2回) |
| | Gruntling_Walk_Slow | Notifiesで指定(2回) |
| | Intro_ClimbingUp | Notifiesで指定(2回) |
| A_Guardian_ImpactL_Cue | React_Heavy_Front | Notifiesで指定 |
| | React_Knockback_Front | Notifiesで指定 |
| A_Guardian_Roar_02_Cue | AM_Guardian_Attack02 | Notifiesで指定 |
| | SQ_Intro_Master | Audio で指定(2回) |
| A_Guardian_Roar_03_Cue | SQ_Intro_Master | Audio で指定 |
| A_Guardian_Spawn_Cue | Intro_Summon | Notifiesで指定 |
| | SQ_Intro_Master | Audio で指定 |

# ■ Assets/Sounds/Creatures/Spider の内容

## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Spider_Attack01 | A_Spider_Attack_Cue |
| A_Spider_Attack02 | A_Spider_Attack_Cue |
| A_Spider_Attack03 | A_Spider_Attack_Cue |
| A_Spider_Attack04 | A_Spider_AttackVocal_Cue |
| A_Spider_Charge01 | A_Spider_Charge_Cue |
| A_Spider_Death01 | A_Spider_Death_Cue |
| A_Spider_Land01 | A_Spider_Land_Cue |
| A_Spider_LegLrg01 | A_Spider_LegLrg_Cue |
| A_Spider_LegLrg02 | A_Spider_LegLrg_Cue |
| A_Spider_LegLrg03 | A_Spider_LegLrg_Cue |
| A_Spider_LegLrg04 | A_Spider_LegLrg_Cue |
| A_Spider_React01 | A_Spider_React_Cue |
| A_Spider_React02 | A_Spider_React_Cue |
| A_Spider_React03 | A_Spider_React_Cue |
| A_Spider_Spawn01 | A_Spider_Spawn_Cue |
| A_Spider_Stun01 | A_Spider_Stun_Cue |
| A_Spider_WalkLoop02 | A_Spider_WalkLoop_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_Spider_Attack_Cue | ExoGame_Greater_Spider_Attack_Melee | Notifiesで指定 |
| | ExoGame_Greater_Spider_Attack_Melee_B | Notifiesで指定 |
| | ExoGame_Greater_Spider_Attack_Melee_C | Notifiesで指定 |
| A_Spider_AttackVocal_Cue | ExoGame_Greater_Spider_Attack_Melee | Notifiesで指定 |
| | ExoGame_Greater_Spider_Attack_Melee_B | Notifiesで指定 |
| | ExoGame_Greater_Spider_Attack_Melee_C | Notifiesで指定 |
| A_Spider_Charge_Cue | ExoGame_Greater_Spider_Charge | Notifiesで指定 |
| A_Spider_Death_Cue | ExoGame_Greater_Spider_Death | Notifiesで指定 |
| A_Spider_Land_Cue | ExoGame_Greater_Spider_Teleport | Notifiesで指定 |
| A_Spider_LegLrg_Cue | ExoGame_Greater_Spider_Attack_Melee | Notifiesで指定(3回) |
| | ExoGame_Greater_Spider_Attack_Melee_B | ExoGame_Greater_Spider_Attack_Melee | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_Attack_Melee_C | Notifiesで指定 |
| | ExoGame_Greater_Spider_Charge | Notifiesで指定(3回)  |
| | ExoGame_Greater_Spider_Death | Notifiesで指定 |
| | ExoGame_Greater_Spider_Idle | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_React_Heavy_Front | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_React_Stunned | Notifiesで指定(3回) |
| | ExoGame_Greater_Spider_React_Stunned_Enter | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_React_Stunned_Exit | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_Teleport | Notifiesで指定 |
| | ExoGame_Greater_Spider_Walk_Fwd | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_Walk_Left | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_Walk_Right | Notifiesで指定(2回) |
| A_Spider_React_Cue | ExoGame_Greater_Spider_Charge | Notifiesで指定 |
| | ExoGame_Greater_Spider_React_Heavy_Front | Notifiesで指定 |
| | ExoGame_Greater_Spider_React_Stunned | Notifiesで指定(2回) |
| | ExoGame_Greater_Spider_React_Stunned_Enter | Notifiesで指定 |
| | ExoGame_Greater_Spider_React_Stunned_Exit | Notifiesで指定 |
| A_Spider_Spawn_Cue | ExoGame_Greater_Spider_Teleport | Notifiesで指定 |
| A_Spider_Stun_Cue | ExoGame_Greater_Spider_React_Stunned | Notifiesで指定 |
| | ExoGame_Greater_Spider_React_Stunned_Idle | Notifiesで指定 |
| A_Spider_WalkLoop_Cue | ExoGame_Greater_Spider_Walk_Fwd | Notifiesで指定 |
| | ExoGame_Greater_Spider_Walk_Left | Notifiesで指定 |
| | ExoGame_Greater_Spider_Walk_Right | Notifiesで指定 |

----
以上。
