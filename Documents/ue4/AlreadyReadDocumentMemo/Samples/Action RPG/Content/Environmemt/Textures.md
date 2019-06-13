# ■ Environment/Textures の内容
* 用途ごとにフォルダ分けされている。
* Texture ファイルが置かれている。

## Suffix

| Suffix | 用途 | Format |
| ----- | ----- | ----- |
| _M | マスク | DXT5 |
| _D | ディフューズ/カラーマップ | DXT1/DXT5 |
| _N | ノーマルマップ | BC5 |
| _E | エミッシブカラー | DXT1 |
| _A |  | DXT1 |

## ■ フォルダ一覧

| フォルダ名 | 内容 | ファイル数 |
| ----- | ----- | ----- |
| Bricks | レンガ | 2 |
| Building | 建造物 | 2 |
| etc | かがり火、天球 | 6 |
| Foliage | 植物 | 4 |
| Natures | 植物、岩 | 15 |
| Rock | 岩 | 17 |

## ■ ファイル一覧

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| Bricks/T_Cave_Bricks_M | レンガのマスク<br>R:苔のブレンド比<br>G:土壌のブレンド比<br>B:アンビエントオクルージョン値| MI_M_Cave_Rock_Bricks_Moss22<br>M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Bricks/T_Cave_Bricks_N | レンガのノーマルマップ | MI_M_Cave_Rock_Bricks_Moss22 |
| Building/T_Slums_Wood_D | 朽ちた木の扉の色情報<br>RGB:ベースカラーの要素<br>A:スペキュラの要素 | M_Slums_Wood_ |
| Building/T_Slums_Wood_N | 朽ちた木の扉のノーマルマップ | M_Slums_Wood_ |
| etc/T_Cave_Wood_Beam_D | 木材の色情報<br>RGB:ベースカラー<br>T_Cave_Wood_Beam_N を Composite Texutre に指定 | M_Cave_Wood_Beam |
| etc/T_Cave_Wood_Beam_N | 木材のノーマルマップ | M_Cave_Wood_Beam<br>T_Cave_Wood_Beam_D |
| etc/T_Iron_D | かがり火の色情報<br>RGB:ベースカラーの要素<br>R:ラフネスの要素 | M_Ice_Fort_Iron_1_Glow |
| etc/T_Iron_E | かがり火のエミッシブカラー | M_Ice_Fort_Iron_1_Glow |
| etc/T_Iron_N | かがり火のノーマルマップ | M_Ice_Fort_Iron_1_Glow |
| etc/T_Moss_D | 苔の色情報<br>RGB:ベースカラーの要素<br>A:ラフネスの要素 | MF_ML_Cave_Moss<br>MI_Cave_Rock_Pillar_Moss2<br>MI_Cave_Rock_Small_Moss02<br>MI_M_Cave_Rock_Bricks_Moss22 |
| Foliage/T_Cave_LeavePile_D | 落ち葉の色情報<br>RGB:ベースカラーの要素<br>A:オパシティマスク<br>T_Cave_LeavePile_N を Composite Texutre に指定 | M_Cave_Leaf_Piles<br>MI_Cave_Leaf_Piles_Wave |
| Foliage/T_Cave_LeavePile_N | 落ち葉のノーマルマップ | M_Cave_Leaf_Piles<br>T_Cave_LeavePile_D<br>MI_Cave_Leaf_Piles_Wave |
| Foliage/T_LV_Forest_Foliage02_D | シダのような植物の色情報<br>RGB:ベースカラーの要素<br>A:オパシティマスク | M_LV_Soul_Grass04M |
| Foliage/T_LV_Forest_Foliage02_N | シダのような植物のノーマルマップの要素 | M_LV_Soul_Grass04M |
| Natures/T_Cave_Dirt_D | 濡れた泥の色情報<br>RGB:ベースカラーの要素<br>A:ラフネスの要素 | MF_ML_Dirt_Wet_JM |
| Natures/T_Cave_Dirt_N | 濡れた泥のノーマルマップ | MF_ML_Dirt_Wet_JM |
| Natures/T_Fire_Lava_D | 溶岩（UI の炎エフェクト）の色情報<br>RGB:ベースカラーの要素 | M_RPG_UI_Button01 |
| Natures/T_Foliage_Leaves_D | 紅葉した白木の葉の色情報<br>RGB:エミッシブカラーの要素<br>A:オパシティマスク | M_Aspen_Tree_Unlit_Blowing<br>MI_Aspen_Tree_Lit_Blowing |
| Natures/T_JaggedRock_01_D | Meteor の岩の不透明部分の色情報<br>RGB:ベースカラーの要素・エミッシブカラーの要素 | MI_Jagged_Rock_01_Lit |
| Natures/T_JaggedRock_D | Meteor の岩の半透明部分の色情報<br>RGB:エミッシブカラーの要素<br>A:オパシティの要素 | MI_Jagged_rock_01 |
| Natures/T_LV_Soul_grass_D | イネのような植物の色情報<br>RGB:ベースカラーの要素<br>A:オパシティマスク | M_LV_SoulGrass_01M |
| Natures/T_Soul_Leaves_D | 落ち葉の色情報<br>RGB:ベースカラー<br>A:オパシティマスク | M_Soul_Leaves |
| Natures/T_Soul_Leaves_N | 落ち葉のノーマルマップ | M_Soul_Leaves |
| Natures/T_Soul_plants_D | シダのような植物（大）の色情報<br>RGB:ベースカラー<br>A:オパシティマスク | M_Soul_Plants |
| Natures/T_Soul_plants_N | シダのような植物（大）のノーマルマップ | M_Soul_Plants |
| Natures/T_Tree_Aspen_Bark_D | 紅葉した白木の幹の色情報<br>RGB:ベースカラーの要素 | M_Aspen_Tree_Bark |
| Natures/T_Tree_Aspen_Bark_N | 紅葉した白木の幹のノーマルマップ | M_Aspen_Tree_Bark |
| Natures/T_VINETEXTURE_D | 枯れ木の色情報<br>RGB:ベースカラーの要素 | M_Soul_Bush |
| Natures/T_VINETEXTURE_N | 枯れ木のノーマルマップ | M_Soul_Bush |
| Rock/T_Cave_Mud_D | 泥の色情報<br>RGB:ベースカラーの要素<br>G:ラフネスの要素 | MF_ML_Mud_Wet_JM<br>M_CaveLandscape_Inst<br>M_CaveLandscape_Mobile |
| Rock/T_Cave_Mud_N | 泥のノーマルマップ<br>MF_GroundWetnessAlpha_JM:Landscape の UVOffset の要素 | MF_GroundWetnessAlpha_JM<br>F_ML_Mud_Wet_JM<br>M_CaveLandscape_Inst<br>M_CaveLandscape_Mobile |
| Rock/T_Cave_Rock_01_D | MF_ML_Cave_Rock_01:岩の色情報<br>RGB:ベースカラーの要素<br>A:ラフネスの要素<br>M_Cave_Rock_MASTER_VertexPaint_MOSS:岩の色情報<br>RGB:ベースカラーの要素・ラフネスの要素<br>T_Cave_Rock_01_D を Composite Texutre に指定 | MF_ML_Cave_Rock_01<br>M_Cave_Rock_MASTER_VertexPaint_MOSS<br>MI_Cave_Rock_Flat<br>MI_Cave_Rock_Large02<br>MI_Cave_Rock_Pillar_Moss2<br>MI_Cave_Rock_Small_Moss02<br>MI_M_Cave_Rock_Bricks_Moss22<br>MI_M_Cave_Rock_Ceiling |
| Rock/T_Cave_Rock_01_N | MF_ML_Cave_Rock_01:岩のノーマルマップの要素<br>M_Cave_Rock_MASTER_VertexPaint_MOSS:岩のノーマルマップの要素<br>M_RippleFoam:波紋のノーマルマップの要素（ノーマルをみない設定なので無意味）<br>MF_ML_Cave_Moss:苔のノーマルマップの要素 | MF_ML_Cave_Rock_01<br>M_Cave_Rock_MASTER_VertexPaint_MOSS<br>MI_Cave_Rock_Flat<br>MI_Cave_Rock_Large02<br>MI_Cave_Rock_Pillar_Moss2<br>MI_Cave_Rock_Small_Moss02<br>MI_M_Cave_Rock_Bricks_Moss22<br>MI_M_Cave_Rock_Ceiling<br>M_RippleFoam<br>MF_ML_Cave_Moss<br>T_Cave_Rock_01_D |
| Rock/T_Cave_Rock_Large02_M | M_Cave_Rock_MASTER:岩のマスク<br>R:濡れた部分の乗算マスク<br>B:アンビエントオクルージョン値 | MI_Cave_Rock_Large02 |
| Rock/T_Cave_Rock_Large02_N | M_Cave_Rock_MASTER:岩のノーマルマップの要素 | MI_Cave_Rock_Large02 |
| Rock/T_Cave_Rock_Path_M | M_Cave_Rock_MASTER:岩のマスク<br>R:濡れた部分の乗算マスク<br>B:アンビエントオクルージョン値 | MI_M_Cave_Rock_Ceiling |
| Rock/T_Cave_Rock_Path_N | M_Cave_Rock_MASTER:岩のノーマルマップの要素 | MI_M_Cave_Rock_Ceiling |
| Rock/T_Cave_Rock_Pillar_M | M_Cave_Rock_MASTER_VertexPaint_MOSS:岩の色情報<br>RGB:ベースカラーの要素・ラフネスの要素 | MI_Cave_Rock_Pillar_Moss2 |
| Rock/T_Cave_Rock_Pillar_N | M_Cave_Rock_MASTER_VertexPaint_MOSS:岩のノーマルマップの要素 | MI_Cave_Rock_Pillar_Moss2 |
| Rock/T_Cave_Rock_Small_M | M_Cave_Rock_MASTER:岩のマスク<br>R:濡れた部分の乗算マスク<br>B:アンビエントオクルージョン値<br>M_Cave_Rock_MASTER_VertexPaint_MOSS:岩の色情報<br>RGB:ベースカラーの要素・ラフネスの要素 | MI_Cave_Rock_Flat<br>MI_Cave_Rock_Small_Moss<br>MI_Cave_Rock_Small_Moss02 |
| Rock/T_Cave_Rock_Small_N | M_Cave_Rock_MASTER:岩のノーマルマップの要素<br>M_Cave_Rock_MASTER_VertexPaint_MOSS:岩のノーマルマップの要素 | MI_Cave_Rock_Flat<br>MI_Cave_Rock_Small_Moss<br>MI_Cave_Rock_Small_Moss02 |
| Rock/T_Cave_Rock_Stalactite_M | M_Cave_Rock_MASTER:鍾乳石のマスク<br>R:濡れた部分の乗算マスク<br>B:アンビエントオクルージョン値<br>MF_GroundWetnessAlpha_JM:<br>R:ベースカラーの要素・ラフネスの要素・スペキュラの要素<br>MF_VertexBlend_JM:<br>R:出力のアルファ値の要素<br>MF_Wetness:<br>R:ベースカラーの要素・ノーマルマップの要素・ラフネスの要素・スペキュラの要素 | M_Cave_Rock_MASTER<br>M_CaveLandscape_Inst<br>M_CaveLandscape_Mobile<br>MF_GroundWetnessAlpha_JM<br>MF_VertexBlend_JM<br>MF_Wetness |
| Rock/T_Cave_Rock_Stalactite_N | M_Cave_Rock_MASTER:鍾乳石のノーマルマップの要素<br>M_Cave_Rock_MASTER_VertexPaint_MOSS:鍾乳石のノーマルマップの要素 | M_Cave_Rock_MASTER<br>M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Rock/T_Rock_Runes01 | 模様が刻まれた円柱のベースカラーの要素 | M_Cave_RuneRocks01 |
| Rock/T_Rock_Runes01_A | 模様が刻まれた円柱のスペキュラ・模様が刻まれた円柱のラフネスの要素 | M_Cave_RuneRocks01 |
| Rock/T_Rock_Runes01_N | 模様が刻まれた円柱のノーマルマップの要素 | M_Cave_RuneRocks01 |

----
以上。

