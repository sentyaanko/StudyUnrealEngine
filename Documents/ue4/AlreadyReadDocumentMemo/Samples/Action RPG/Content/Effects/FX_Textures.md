# ■ Effects/FX_Textures の内容
* Particle で使用されている Texture ファイルが置かれている。
* 用途は下記の通りだがフォルダの分け方に一貫性が見られない。
 
## ■ ファイル一覧

| ファイル名 | 用途 | 参照元 |
| ----- | ----- | ----- |
| T_PC_Shadow_M | 円形 | M_PC_Shadow_Mat |
| Damage/T_cracks_01_N | ひび割れ | MI_CrackedGround_01 |
| Damage/T_cracks_03_M | ひび割れ | MI_CrackedGround_01 |
| Damage/T_Rocks_3_3_D | 岩 | MI_RockDebris_Trans |
| Damage/T_Rocks_Fire_3_3_D | 燃えている岩 | MI_RockDebrisFire_Trans |
| Fire/T_Fire_Shock_01_D | 5x5 の爆炎のアニメーションパターン | MI_Fire_Shock_01_5x5_SubUV |
| Fire/T_Fire_subUV_6X6_M | 6x6 の炎のアニメーションパターン | MI_Fire_01_Add_6X6 |
| Fire/T_FireBlastTile_D | 炎<br>Trail/Mesh で利用されている | M_Axe_Trail<br>M_Sword_Trail<br>MI_Fire_Sheet_01 |
| Gradient/T_BlastWave_D | 衝撃波 | MI_Shockwave_01_ADD |
| Gradient/T_Flare_Streaks_02_M | 放射状の熱線 | MI_Flare_Streak_01 |
| Gradient/T_FX_Glow_12alpha_M | 火の粉<br>光の粉<br>UI 上の武器のアイコン（動作していない？要確認） | MI_Flare_09<br>M_SoulCollectible<br>M_RPG_UI_Button01 |
| Gradient/T_GlowNoise_01_M | 消えかけた衝撃波 | MI_Shockwave_03_Add |
| Gradient/T_SoftFallOff | 円形の薄いグラデーション<br>Soul のエフェクトで使用 | M_Flare_03_INST |
| Gradient/T_SoftFallOff_M | ↑と全く同じに見える<br>FireBall/Meteor のエフェクトで使用 | MI_Flare_03 |
| Gradient/T_starFlare_01_M | 星形のグラデーション | MI_Flare_01 |
| Gradient/T_SwipeTrail | 横方向にぶれたようなグラデーション<br>Soul のエフェクトで使用 | M_Swipe_Mesh_Add_2Sided_01_INST |
| Gradient/T_SwipeTrail_M | ↑と全く同じに見える<br>回避・回転斬りのエフェクトで使用 | MI_Swipe_Mesh_Add_2Sided_01 |
| Lightning/T_Lightning_Arc_4x1_D | 稲光のアニメーションパターン<br>放射状に広がる雷光で利用されている<br>_D となっているが、α以外はすべて１になっている<br>_M にしたほうがいいか要確認 | MI_Lightning_Arc_01_Trans_4X1 |
| Lightning/T_Lightning_Bolt_01_D | 稲光のアニメーションパターン<br>落雷で利用されている<br>_D となっているが、 rgba すべて同値<br>_M にしたほうがいいか要確認 | MI_Lightning_Bolt_01_Add_4X1<br>M_Char_Barbrous |
| Liquid/T_bloodTest_4X6_D | 4x6 の水しぶきのアニメーションパターン | MI_Liquid_Spray_01_4X6 |
| Noise/T_Tile_Noise_Tendril_01_M | ノイズ画像 | MI_Tile_Noise_Tendril_01_in |
| Smoke/T_Smoke_subUV_01_M | 6x6 の煙のアニメーションパターン | MI_Smoke_02_Trans_6X6 |
| Smoke/T_SmokeBall_01_8_8_M | 8x8 の煙のアニメーションパターン | MI_Smoke_01_8X8 |
| Spark/T_Sparks_03_SubUV_1_4_D | 4x1 の火の粉のアニメーションパターン<br>Preserve Border の設定は false | MI_Spark_03_1_4 |
| Spark/T_Sparks_04_SubUV_1_4_M | 4x1 の火の粉のアニメーションパターン<br>↑と設定がほぼ同じ<br>Preserve Border の設定は false | MI_Spark_04_SubUV_1_4 |
| TextureT_FireBall_01B_8_8_D | 8x8 の爆発のアニメーションパターン | MI_Fireball_01_8X8 |
| Tile/T_Black_32_D | 黒塗り<br>主に Effects/Masters の初期テクスチャで利用されている | M_Add_Trail_2Sided_Pan_Master<br>M_Trans_Sprite_Master_DepthFade<br>M_Trans_Sprite_Master_Surface |

参考：suffix
 | suffix | 意味 |
 | ----- | ----- |
 | _D | Diffuse/Albedo |
 | _N | Normal |
 | _M | Mask |

----
以上。
