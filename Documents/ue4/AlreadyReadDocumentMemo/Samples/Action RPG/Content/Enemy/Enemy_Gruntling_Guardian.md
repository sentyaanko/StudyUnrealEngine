# ■ Enemy/Enemy_Gruntling_Guardian の内容
* Goblin ３体のモデル、テクスチャ、マテリアル、アニメーションに関するファイルが置かれている。

ここに置かれていない関連ファイルの置き場所
| Type | 置き場 |
| ----- | ----- |
| Animation Montage | /Animations/NPC |
| Animation Blueprint | /Blueprints/NPC |
| Blend Space | /Blueprints/NPC |

## ■ フォルダ一覧
| フォルダ名 | 用途 |
| ----- | ----- |
| Enemy_Gruntling_Guardian/ | Skeletal Mesh<br>Skeleton<br>Phisics Asset<br>Animation Sequnce |
| Enemy_Gruntling_Guardian/Enemy_Gruntling_Guardian_Animation/ | Animation Sequence |
| Enemy_Gruntling_Guardian/Materials/ | Material<br>Material Instance |
| Enemy_Gruntling_Guardian/Textures/ | Texture |

## ■ ファイル一覧

| ファイル名 | Type | 参照元 |
| ----- | ----- | ----- |
| SK_Exodus_Gruntling | SkeletalMesh | NPC_Goblin_Level_01<br>SK_Exodus_Gruntling_PhysicsAsset |
| SK_Gruntling_Avalanche | SkeletalMesh | NPC_Goblin_Level_03 |
| SK_Gruntling_Guardian | SkeletalMesh | NPC_GoblinBP<br>SQ_Intro_Enemy_AnimData<br>SK_Gruntling_Guardian_Skeleton<br>CharM_Gruntling |
| SK_Gruntling_Guardian_Skeleton | Skeleton | AM_Guardian_Attack<br>AM_Guardian_Attack02<br>AM_Guardian_Falldown<br>AM_Guardian_Hit<br>Idle_Run_Guardian_1D<br>NPC_AnimBP_Base<br>Enemy_Anim_Sword_Combat_Swing<br>SK_Exodus_Gruntling<br>SK_Gruntling_Avalanche<br>SK_Gruntling_Guardian<br>Aggro_A<br>Cast<br>Death<br>Death_Small_03<br>Death_Small_05<br>Gruntling_Run<br>Gruntling_Walk<br>Gruntling_Walk_Slow<br>Idle_Grunt<br>Intro_ClimbingUp<br>Intro_Summon<br>React_Heavy_Front<br>React_Knockback_Front |
| SK_Exodus_Gruntling_PhysicsAsset | PhysicsAsset | SK_Exodus_Gruntling<br>SK_Gruntling_Avalanche<br>SK_Gruntling_Guardian |
| Enemy_Anim_Sword_Combat_Swing | Animation Sequence | AM_Guardian_Attack<br>SQ_Intro_Enemy_AnimData |

# ■ Enemy/Enemy_Gruntling_Guardian/Enemy_SpiderGreater_Animation ファイル一覧
* すべて Animation Sequence

| ファイル名 | 参照元 |
| ----- | ----- |
| Aggro_A | SQ_Intro_Enemy_AnimData |
| Cast | AM_Guardian_Attack02<br>SQ_Intro_Enemy_AnimData |
| Death | NPC_AnimBP_Base |
| Death_Small_03 | AM_Guardian_Falldown |
| Death_Small_05 | AM_Guardian_Falldown |
| Gruntling_Run | Idle_Run_Guardian_1D |
| Gruntling_Walk | Idle_Run_Guardian_1D |
| Gruntling_Walk_Slow | Idle_Run_Guardian_1D |
| Idle_Grunt | Idle_Run_Guardian_1D<br>SQ_Intro_Enemy_AnimData |
| Intro_ClimbingUp | SQ_Intro_Enemy_AnimData |
| Intro_Summon | NPC_AnimBP_Base |
| React_Heavy_Front | AM_Guardian_Hit |
| React_Knockback_Front | AM_Guardian_Hit |

# ■ Enemy/Enemy_Gruntling_Guardian/Materials ファイル一覧
* Material と Material Instance

| ファイル名 | Type | 参照元 |
| ----- | ----- | ----- |
| CharM_Gruntling | Material Instance | SK_Gruntling_Guardian<br>CharM_Gruntling_Avalanche<br>SQ_Intro_Enemy_AnimData |
| CharM_Gruntling_Avalanche | Material Instance | SK_Gruntling_Avalanche |
| CharM_Gruntling_Base | Material | SK_Exodus_Gruntling<br>CharM_Gruntling |

# ■ Enemy/Enemy_Gruntling_Guardian/Textures ファイル一覧
* すべて Texture

| ファイル名 | 参照元 |
| ----- | ----- |
| T_Gruntling_Avalanche_D | CharM_Gruntling_Avalanche |
| T_Gruntling_Avalanche_E | CharM_Gruntling_Avalanche |
| T_Gruntling_Avalanche_M | CharM_Gruntling<br>CharM_Gruntling_Avalanche |
| T_Gruntling_Avalanche_N | CharM_Gruntling_Avalanche |
| T_Gruntling_D | CharM_Gruntling |
| T_Gruntling_E | CharM_Gruntling |
| T_Gruntling_Guardian_D | CharM_Gruntling_Base |
| T_Gruntling_Guardian_E | CharM_Gruntling_Base |
| T_Gruntling_Guardian_M | CharM_Gruntling_Base |
| T_Gruntling_Guardian_N | CharM_Gruntling_Base<br>CharM_Gruntling |

参照先の組み合わせ
|  | CharM_Gruntling_Base | CharM_Gruntling | CharM_Gruntling_Avalanche |
| ----- | ----- | ----- | ----- |
| T_Gruntling_Avalanche_D | | | 〇 |
| T_Gruntling_Avalanche_E | | | 〇 |
| T_Gruntling_Avalanche_M | | 〇 | 〇 |
| T_Gruntling_Avalanche_N | | | 〇 |
| T_Gruntling_D | | 〇 | |
| T_Gruntling_E | | 〇 | |
| T_Gruntling_Guardian_D | 〇 | | |
| T_Gruntling_Guardian_E | 〇 | | |
| T_Gruntling_Guardian_M | 〇 | | |
| T_Gruntling_Guardian_N | 〇 | 〇 | |


----
以上。
