# ■ Effects/FX_Mobile の内容
* ParticleSystem/Material Instance ファイルが置かれている。
* 用途は下記の通りだがフォルダの分け方に一貫性が見られない。
* おそらく動き回るものを置くフォルダ。

## ■ ParticleSystem ファイル一覧

| ファイル名 | 用途 | 参照元 |
| ----- | ----- | ----- |
| Fire | player スキルの炎 | AM_Skill_Firewave<br>AM_Skill_Meteor<br>Anim_Blunt_Gound_Pound_Fire |
| P_WaterSplash_Foam | ２番目のレベルで利用している | ActionRPG_Dungeon02_Asset |
| Fire/combat/P_DmgField_Fire_Activate_01_Loop | Meteor で利用 | AM_Skill_Meteor |
| Fire/combat/P_FireBall_Strong | 火の玉で利用 | BP_Fireball |
| Fire/combat/P_SlimeBall | ヘドロ玉で利用 | BP_SlimeBall |

## ■ Material Instance ファイル一覧

| ファイル名 | 用途 | 参照元 | 参照先マテリアル |
| ----- | ----- | ----- | ----- |
| Fire/MI_Fireball_01_8X8 | Meteor 着弾の爆発の炎 | P_DmgField_Fire_Activate_01_Loop | Effects/Masters/M_Trans_Sprite_SubUV_Master |

----
以上。
