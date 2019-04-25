* 書きかけです。

# ■ Environment/Materials の内容
* Material/Material Instance/Texture ファイルが置かれている。
* Unreal Engine 4.21.2 だと、EngineContents 以下のいくつかの Material Function でエラーが出ているため、4.22.0 に更新しました。

## ■ ファイル一覧

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_SoulCollectible | Material | Soul の収集用目印 | P_Summon_Parent_Startup |
| M_CaveLandscape_Mobile | Material | Landscape 用 Material<br>Shader Graph は複雑 | M_CaveLandscape_Inst |
| M_CaveLandscape_Inst | Material Instance | Landscape 用 Material Instance |ActionRPG_Dungeon02_Asset  |
| T_LandscapeES2_BC_00 | Texture | Landscape 用ベースカラー | M_SoulCollectible<br>M_CaveLandscape_Mobile |
| T_LandscapeES2_N_00 | Texture | Landscape 用ノーマルマップ | M_SoulCollectible<br>M_CaveLandscape_Mobile |
| T_LandscapeES2_R_00 | Texture | Landscape 用ラフネス | M_SoulCollectible<br>M_CaveLandscape_Mobile |
| Building/M_Slums_Wood_ | Material | 朽ちた木の扉 | SM_Slums_WoodWall_01e_OP |
| Building/M_Soul_Glowstick | Material | 地面に刺さった棒状のライト | SM_glowstick02 |
| etc/M_Ice_Fort_Iron_1_Glow | Material | かがり火 | SM_Ice_Fort_Brazier_1_Glow |
| etc/MAT_Skydome_01 | Material | skydome 用 | SM_Skydome_01 |
| Foliage/M_Aspen_Tree_Bark | Material | 白木の幹<br>**枝葉(foliage)ではあるが、Unreal の Foliage 用ではない** | SM_Aspen_Tree_01 |
| Foliage/M_LV_SoulGrass_01M | Material | 地面の草<br>Foliage で利用<br>speed3 で揺れるスピードを指定可能<br>ColorMod で Base Color/Emissive Color の係数が指定可能<br> | SM_LV_SoulGrass_01 |
| Foliage/M_Aspen_Tree_Unlit_Blowing | Material | 白木の紅葉<br>**枝葉(foliage)ではあるが、Unreal の Foliage 用ではない** | MI_Aspen_Tree_Lit_Blowing |
| Foliage/MI_Aspen_Tree_Lit_Blowing | Material Instance | 上記の Material Instance | SM_Aspen_Tree_01 |
| Foliage/M_Cave_Leaf_Piles | Material | 落ち葉の集まり<br>**枝葉(foliage)ではあるが、Unreal の Foliage 用ではない** | MI_Cave_Leaf_Piles_Wave<br>SM_Cave_Leaf_Pile01<br>SM_Cave_Leaf_Pile02 |
| Foliage/MI_Cave_Leaf_Piles_Wave | Material Instance | 上記の Material Instance<br>SM_Cave_Leaf_Pile01 の Material として利用<br>**枝葉(foliage)ではあるが、Unreal の Foliage 用ではない** | ActionRPG_Dungeon02_Asset |
| Functions/MF_FuzzyShading_JM| Material Function |  | M_Cave_Rock_MASTER<br>M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Functions/MF_GroundWetnessAlpha_JM| Material Function |  | M_CaveLandscape_Mobile |
| Functions/MF_ML_Dirt_Wet_JM| Material Function |  | M_CaveLandscape_Mobile |
| Functions/MF_ML_Mud_Wet_JM| Material Function |  | M_CaveLandscape_Mobile |
| Functions/MF_VertexBlend_JM| Material Function |  | M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Functions/MF_Wetness| Material Function |  | M_Cave_Rock_MASTER<br>M_Cave_Rock_MASTER_VertexPaint_MOSS |
| MaterialLayers/ |  |  |
| Natures/ |  |  |
| Natures/ |  |  |
| Natures/ |  |  |
| Natures/ |  |  |
| Natures/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |
| Rocks/ |  |  |


# ■ マテリアルの内容について
## ■ M_CaveLandscape_Mobile
* 複雑

## ■ Building/M_Slums_Wood_
* _D の利用方法が独特

## ■ Building/M_Soul_Glowstick
* _D.A を Emissive Color に利用している

## ■ etc/M_Ice_Fort_Iron_1_Glow
* _D.R を Roughness に利用している

## ■ Foliage/M_Aspen_Tree_Bark
* Vertex Color 1 ～ 0 で _D ～ pow(_D,2) の値をとる
* SM_Aspen_Tree_01 では Vertex Color がすべて 1 のため、 _D がそのまま表示されている

## ■ Foliage/M_LV_SoulGrass_01M
* speed3 で揺れるスピードを指定可能
* ColorMod で _D との係数が指定可能
* ColorMod と _D をかけ合わせた後、 Desaturation ノードにて彩度を抑制
* 最終的に Base Color/Emissive Color で同じ値を利用

----
以上。

