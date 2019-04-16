# ■ Assets/Sounds/Weapons の内容
* 武器の種類ごとにフォルダ分けされている。
* Swing 音だけこの階層に置いてある。

## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Weapon_FireSwing01 | A_Weapon_FireSwing_Cue |
| A_Weapon_FireSwing02 | A_Weapon_FireSwing_Cue |
| A_Weapon_FireSwing03 | A_Weapon_FireSwing_Cue |
| A_Weapon_FireSwing04 | A_Weapon_FireSwing_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_Weapon_FireSwing_Cue | AM_Skill_Metor | Notifies で指定(２回) |
| | Axe_Male_Anim_Sword_Combat_Swing | Notifies で指定(１回) |
| | Axe_Swing_Near_Lt | Notifies で指定(１回) |
| | Blunt_Swing_Near_Lt | Notifies で指定(１回) |
| | Combat_Blade_Swing_Far | Notifies で指定(２回) |
| | Death_Front | Notifies で指定(１回) |
| | Dodge_Small_Forward_Roll | Notifies で指定(１回) |
| | Male_Anim_Axe_Combat_Swing | Notifies で指定(１回) |
| | Sword_Male_Anim_Level_Up_Transition | Notifies で指定(１回) |
| | Sword_Male_Anim_Combat_Swing | Notifies で指定(１回) |
| | SQ_Intro_Master | Audio で指定(２回) |

# ■ Assets/Sounds/Weapons/Axe の内容
## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Axe_Swing01 | A_Axe_Swing_Cue |
| A_Axe_Swing02 | A_Axe_Swing_Cue |
| A_Axe_Swing03 | A_Axe_Swing_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_Axe_Swing_Cue | Attack02_Fire | Notifies で指定(１回) |
| | Attack03 | Notifies で指定(１回) |

# ■ Assets/Sounds/Weapons/Hammer の内容
## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Hammer_Impact01 | A_Hammer_Impact_Cue<br>A_UI_Box_Confirm<br>Attack02_Fire の Notifies で指定<br>Attack03 の Notifies で指定(１回) |
| A_Hammer_Impact02 | A_Hammer_Impact_Cue<br>A_UI_Box_Confirm |
| A_Hammer_Impact03 | A_Hammer_Impact_Cue<br>A_UI_Box_Confirm |
| A_Hammer_Swing01 | A_Hammer_Swing_Cue |
| A_Hammer_Swing02 | A_Hammer_Swing_Cue |
| A_Hammer_Swing03 | A_Hammer_Swing_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_Hammer_Impact_Cue | WB_OnScreenInput | Notifies で指定(１回) |
| | Anim_Blunt_Gound_Pound | Notifies で指定(１回) |
| | Anim_Blunt_Gound_Pound_Fire | Notifies で指定(１回) |
| | Sword_Male_Anim_Level_Up_Transition | Notifies で指定(１回) |
| A_Hammer_Swing_Cue | WB_InGame_Finish | Timeline の BonusAnim で指定(２回) |
| | WB_Title | Timeline の TitleAnimation で指定 |
| | WB_WaveStart | Timeline の NewWaveAppear で指定 |
| | AM_Skill_Firewave | Notifies で指定(１回) |
| | Anim_Blunt_Gound_Pound | Notifies で指定(１回) |
| | Anim_Blunt_Gound_Pound_Fire | Notifies で指定(１回) |
| | ExoGame_Greater_Spider_Teleport | Notifies で指定(１回) |

# ■ Assets/Sounds/Weapons/Sword の内容
## ■ SoundWave 一覧
| ファイル名 | 用途 |
| ----- | ----- |
| A_Sword_Swing01 | A_Sword_Swing_Cue<br>WB_Title の TitleAnimation で指定 |
| A_Sword_Swing02 | A_Sword_Swing_Cue |
| A_Sword_Swing03 | A_Sword_Swing_Cue |

## ■ SoundCue 一覧
| ファイル名 | 呼び出し元 | 属性 |
| ----- | ----- | ----- |
| A_Sword_Swing_Cue | WB_InventoryItem | プロパティ「 Appearance ＞ Style ＞ Pressed Sound 」 で指定 |
| | Anim_Sword_Whirlwind | Notifies で指定(２回) |
| | Attack | Notifies で指定(１回) |
| | Axe_Male_Anim_Sword_Combat_Swing | Notifies で指定(１回) |
| | Axe_Swing_Near_Lt | Notifies で指定(１回) |
| | Blunt_Swing_Near_Lt | Notifies で指定(１回) |
| | Combat_Blade_Swing_Far | Notifies で指定(１回) |
| | Male_Anim_Axe_Combat_Swing | Notifies で指定(１回) |
| | Sword_Male_Anim_Sword_Combat_Swing | Notifies で指定(１回) |

----
以上。
