# ■ Characters の内容
* Player のモデル、テクスチャ、マテリアル、アニメーションに関するファイルが置かれている。

## ■ フォルダ一覧
| フォルダ名 | 用途 |
| ----- | ----- |
| Characters/ | Animation Blueprint<br>Skeleton<br>BlendSpace<br>PhysicsMaterial |
| Characters/Animations | Animation Montage<br>Animation Sequence |
| Characters/Barbarous | Skeletal Mesh |
| Characters/Barbarous/Texture_Material | Texture<br>Material |

## ■ ファイル一覧

| ファイル名 | Type | 参照元 |
| ----- | ----- | ----- |
| ABP_Player | Animation Blueprint | BP_PlayerCharacter<br>BP_RPGFunctionLibrary |
| BS_SwordIdle_Run | Blend Space 1D | ABP_Player |
| PA_Mannequin_Physics | Physics Asset | SK_CharM_Barbarous |
| SK_Mannequin_Physics | Skeleton | ABP_Player<br>BS_Sword_Idle_Run<br>AM_Attack_Axe<br>AM_Attack_FireAxe<br>AM_Attack_Hammer<br>AM_Attack_Sword<br>AM_Item_Potion<br>AM_Item_Potion_Mana<br>AM_React_Hit<br>AM_Rolling<br>AM_Skill_Combust<br>AM_Skill_Fireball<br>AM_Skill_Firewave<br>AM_Skill_Meteor<br>Anim_Blunt_Gound_Pound<br>Anim_Blunt_Gound_Pound_C<br>Anim_Blunt_Gound_Pound_Fire<br>Anim_Sword_Idle<br>Anim_Sword_Whirlwind<br>Attack<br>Attack02_Fire<br>Attack03<br>Axe_Male_Anim_Sword_Combat_Swing<br>Axe_Swing_Near_Lt<br>Blunt_Force_Circle1<br>Blunt_Swing_Near_Lt<br>Character_HitReact_Left<br>Character_HitReact_Right<br>Chestopen_Kick<br>Combat_Blade_Swing_Far<br>Death_Front<br>Dodge_Small_Forward_Roll<br>Dodge_Sprint_Blunt<br>Drink_Potion_Sword<br>Drink_Potion_Sword_Mana<br>Male_Anim_Axe_Combat_Swing<br>Sword_Cheer<br>Sword_Male_Anim_Level_Up_Transition<br>Sword_Male_Anim_Sword_Combat_Swing<br>Sword_Run_Forward<br>Sword_Walk_Foward<br>SK_CharM_Barbarous |

----
以上。
