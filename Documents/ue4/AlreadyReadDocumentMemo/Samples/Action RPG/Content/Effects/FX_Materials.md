# ■ Effects/FX_Materials の内容
* Particle で使用されている Material/Material Instance/Material Function ファイルが置かれている。
* 用途は下記の通りだがフォルダの分け方に一貫性が見られない。
* サブフォルダ以下はすべてマテリアルインスタンス。

## ■ ファイル一覧

| ファイル名 | Type | 用途 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Axe_Trail | Material | Axe の軌跡用のマテリアル | P_Axe_Trail |
| M_Fire | Material | メインメニューレベル（タイトル画面）に配置している<br>効果不明 | MI_Fire_Inst |
| M_Fire_SubUV | Material | uv アニメを行うマテリアル<br>Player のスキル(Firewave/Meteor/GroundPound)用 | P_Fire |
| M_PC_Shadow_Mat | Material | 影用のマテリアル | BP_PlayerCharacter<br>SM_CharM_Shadow |
| M_Radial_Gradient | Material | 中心から円形にグラデーションのマテリアル | P_Fire<br>P_Goblin_Death<br>P_Skill_03<br>P_Sword_Trail_F<br>P_Title_Main_Effect<br> |
| M_RippleFoam | Material | 波紋を泡立たせるマテリアル | MI_RippleFoam |
| M_smoke_subUV | Material | 煙用のテクスチャの uv アニメを行うマテリアル | P_Fire<br>P_Goblin_Death |
| M_SplashFoam | Material | 湧き出す水を表現するマテリアル | P_WaterSplash_Foam |
| M_Sword_Trail | Material | Player と敵の武器の軌跡用のマテリアル<br>名前に反して Sword に限らず利用 | P_Sword_Trail_F |
| MI_Fire_Inst | MaterialInstance | メインメニューレベル（タイトル画面）に配置している<br>効果不明 | ActioRPG_Main |
| MI_RippleFoam | MaterialInstance | 波紋を泡立たせるマテリアルインスタンス<br>２番目のレベルで利用しているが、配置場所がおかしく用途不明 | ActionRPG_Dungeon02_Asset |
| MI_Shockwave_01_ADD | MaterialInstance | 円形の衝撃波を表現するマテリアルインスタンス | P_Env_Fire_PP_01<br>P_Skill_001<br>P_Attack_ComboFX<br>P_Skill_Leap_Base_Velocity_Impact |
| MI_Shockwave_03_Add | MaterialInstance | 円形が崩れた煙のようなものを表現するマテリアルインスタンス | P_Impact01<br>P_Skill_001<br>P_Skill_002<br>P_Skill_Leap_Base_Velocity_Impact |
| MF_DissolveEffect | MaterialFunction | 敵の出現、消滅時のディゾルブ用マテリアル関数 | CharM_Greater_Spider<br>CharM_Gruntling_Base |

* テクスチャの参照先は主に以下
	* /Engine
	* Effects/FX_Textures
	* Effects/Textures
	* Effects/Masters
	* Enviroment/Textures
	* UI/Texture

# ■ Effects/FX_Materials/Damage の内容

| ファイル名 | 用途 | 参照元 | 参照先マテリアル |
| ----- | ----- | ----- | ----- |
| Damage/MI_CrackedGround_01 | 地面のひび割れ<br>地面を叩くスキル時 | P_Skill_Leap_Base_Velocity_Impact | Effects/Masters/M_Trans_Sprite_Master_Surface |
| Damage/MI_RockDebris_Trans | 岩の破片<br>地面を叩くスキル時 | P_Skill_Leap_Base_Velocity_Impact | Effects/Masters/M_Trans_Sprite_Lit_SubUV_Master |
| Damage/MI_RockDebrisFire_Trans | 火柱<br>Player のスキル時<br>Goblin03 の死亡時 | P_Env_Fire_PP_01 | Effects/Masters/M_Trans_Sprite_SubUV_Master |
| Env/MI_Jagged_rock_01 | 落石の軌跡<br>Trail ではなく Static Mesh<br>Meteor 用 | P_DmgField_Fire_Activate_01_Loop | Effects/Masters/M_Trans_MeshEmit_Master |
| Env/MI_Jagged_Rock_01_Lit | 落石<br>Meteor 用 | P_DmgField_Fire_Activate_01_Loop | Effects/Masters/M_Opaque_MeshEmit_Lit_Emis_Master |
| Fire/MI_Fire_01_Add_6X6 | 炎 | P_Fire_NeverEnding<br>P_Fire_TrapBossEnd_mobile<br>P_FireBall_Strong<br>P_Env_Fire_Grate_01<br>P_Env_Fire_PP_01 | Effects/Masters/M_Add_Sprite_SubUV_Master |
| Fire/MI_Fire_Sheet_01 | FireBall<br>SlimeBall | P_FireBall_Strong<br>P_SlimeBall | Effects/Masters/M_Add_Trail_2Sided_Pan_Master |
| Fire/MI_Fire_Shock_01_5x5_SubUV | はじける炎 | P_PP | Effects/Masters/M_Add_Sprite_SubUV_Master |
| Gradient/M_Flare_03_INST | Soul の浮遊する光点 | P_Summon_Parent_Startup | Effects/Masters/M_Add_Sprite_Master_DepthFade |
| Gradient/MI_Flare_01 | 放射状の光 | P_PP | Effects/Masters/M_Add_Sprite_Master_DepthFade |
| Gradient/MI_Flare_03 | 地面の円形の白熱光<br>FireBall の白熱光 | P_DmgField_Fire_Activate_01_Loop<br>P_FireBall_Strong | Effects/Masters/M_Add_Sprite_Master_DepthFade |
| Gradient/MI_Flare_09 | Soul の浮かび上がる光点<br>火の粉<br>雷光 | P_Summon_Parent_Startup<br>P_Env_Fire_Grate_01<br>P_Env_Fire_PP_01<br>P_Attack_ComboFX | Effects/Masters/M_Add_Sprite_Master_DepthFade |
| Gradient/MI_Flare_Streak_01 | 放射状に斑に広がる光筋<br> | P_Ability_MeteorStormFX01<br>P_Attack_ComboFX | Effects/Masters/M_Add_Sprite_Master |
| Lightning/MI_Lightning_Arc_01_Trans_4X1 | 放射状に斑に広がる稲光<br> | P_Ability_MeteorStormFX01<br>P_Attack_ComboFX | Effects/Masters/M_Trans_Sprite_SubUV_Master |
| Lightning/MI_Lightning_Bolt_01_Add_4X1 | 下方に走る稲光 | P_Ability_MeteorStormFX01<br>P_Attack_ComboFX | Effects/Masters/M_Add_Sprite_SubUV_Master |
| Liquid/MI_Liquid_Spray_01_4X6 | 液体の噴出 | P_Attack_ComboFX<br>P_Skill_Leap_Base_Velocity_Impact | Effects/Masters/M_Trans_Sprite_Master_DepthFade |
| Noise/MI_Tile_Noise_Tendril_01_in | 回転斬りの衝撃波のノイズ | P_RBurst_Lightning_Pull_01 | Effects/Masters/M_Trans_MeshEmit_2Sided_Pan_Mask_Master |
| Smoke/MI_Smoke_01_8X8 | 回転しながら広がる煙<br>上昇する煙 | P_Impact01<br>P_Skill_001<br>P_Skill_002<br>P_Skill_03<br>P_Spit<br>P_Skill_Leap_Base_Velocity_Impact<br>P_RBurst_Lightning_Pull_01 | Effects/Masters/M_Add_Sprite_SubUV_Master |
| Smoke/MI_Smoke_02_Trans_6X6 | 素早く広がる煙<br>大きく広がる煙 | P_Ability_MeteorStormFX01<br>P_Attack_ComboFX | Effects/Masters/M_Trans_Sprite_SubUV_Master_DepthFade |
| Spark/MI_Spark_03_1_4 | 落下する光の粒子 | P_DmgField_Fire_Activate_01_Loop | Effects/Masters/M_Add_Sprite_SubUV_Master |
| Spark/MI_Spark_04_SubUV_1_4 | ゆっくり上昇する光の粒子<br>中心に集まる光の粒子 | P_Fire_TrapBossEnd_mobile<br>P_RBurst_Lightning_Pull_01 | Effects/Masters/M_Add_Sprite_SubUV_Master |
| Trails/M_Swipe_Mesh_Add_2Sided_01_INST | 渦巻く光の軌跡 | P_Summon_Parent_Startup | Effects/Masters/M_Add_Sprite_Master |
| Trails/MI_Swipe_Mesh_Add_2Sided_01 | 回転斬りの光の軌跡<br> | P_Skill_03<br>P_RBurst_Lightning_Pull_01 | Effects/Masters/M_Add_Sprite_2Sided_Master |


----
以上。
