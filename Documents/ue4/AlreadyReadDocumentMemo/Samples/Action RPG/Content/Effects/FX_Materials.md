# ■ Effects/FX_Materials の内容
* Particle で使用されているマテリアルとマテリアルインスタンス、マテリアル関数が置かれている。
* 用途は下記の通りだが一貫性が見られない。

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

----
以上。
