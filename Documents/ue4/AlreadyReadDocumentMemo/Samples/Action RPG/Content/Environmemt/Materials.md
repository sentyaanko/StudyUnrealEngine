* 書きかけです。

# ■ Environment/Materials の内容
* Material/Material Instance/Texture ファイルが置かれている。
* Unreal Engine 4.21.2 だと、EngineContents 以下のいくつかの Material Function でエラーが出ているため、4.22.0 に更新しました。
* その直後に 4.22.1 がリリースされたのでそちらに更新しました。
* その後に 4.22.2 がリリースされたのでそちらに更新しました。
* Material Function で suffix に _JM とついているものがあるが意図不明。

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
| Functions/MF_FuzzyShading_JM | Material Function | 岩の Material から呼ばれる<br>FuzzyShading の独自実装？<br>FuzzyShading ノードの呼び出しはしていない<br>FuzzyShadingSwitch が false の時は何もしない<br>唯一利用している箇所でも false となっている | M_Cave_Rock_MASTER |
| Functions/MF_GroundWetnessAlpha_JM | Material Function | Landscape 用 Material から呼ばれる<br>地面の濡れをブレンドする計算部分 | M_CaveLandscape_Mobile |
| Functions/MF_ML_Dirt_Wet_JM | Material Function | Landscape 用 Material から呼ばれる<br> | M_CaveLandscape_Mobile |
| Functions/MF_ML_Mud_Wet_JM | Material Function | Landscape 用 Material から呼ばれる<br> | M_CaveLandscape_Mobile |
| Functions/MF_VertexBlend_JM | Material Function | 岩のマスターマテリアルから呼ばれる | M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Functions/MF_Wetness | Material Function | 岩のマスターマテリアルから呼ばれる | M_Cave_Rock_MASTER<br>M_Cave_Rock_MASTER_VertexPaint_MOSS |
| MaterialLayers/MF_ML_Solid_Color | Material Function | 岩のマスターマテリアルから呼ばれる<br>MaterialLayers というフォルダ名だが、<br>4.19 以降の MaterialLayers は使っていない。<br>（やっていることはほぼ同じ） | M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Natures/MI_Soul_Leaves_Water | Material Instance | 落ち葉用のマテリアルインスタンス | SM_Cave_Leaf_Pile_01 |
| Natures/M_Soul_Leaves | Material |  落ち葉用のマテリアル<br>foliage で利用 | MI_Soul_Leaves_Water<br>SM_Cave_Leaf_Pile_02 |
| Natures/M_LV_Soul_Grass04M | Material | シダに似た植物用のマテリアル<br>foliage で利用 | SM_LV_Soul_Foliage021SM |
| Natures/M_Soul_Bush | Material | 枯れ木用のマテリアル | SM_S_Soul_bush |
| Natures/M_Soul_Plants | Material | シダ（大）に似た植物用のマテリアル | SM_S_Soul_Plants_Fern2 |
| Rocks/MF_ML_Cave_Moss | Material Function | 岩のマスターマテリアルから呼ばれる<br>苔用 Material Layer | M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Rocks/MF_ML_Cave_Rock_01 | Material Function | 岩のマスターマテリアルから呼ばれる<br>岩用 Material Layer | M_Cave_Rock_MASTER<br>M_Cave_Rock_MASTER_VertexPaint_MOSS |
| Rocks/MI_Cave_Rock_Flat | Material Instance | M_Cave_Rock_MASTER のマテリアルインスタンス<br>Phys Material 付き。 | SM_Cave_Rock_Flat01 |
| Rocks/MI_Cave_Rock_Large02 | Material Instance | M_Cave_Rock_MASTER のマテリアルインスタンス | SM_Cave_Rock_01<br>SM_Cave_Rock_02<br>SM_Cave_Rock_03<br>ActionRPG_Dungeon02_Asset |
| Rocks/MI_Cave_Rock_Pillar_Moss2 | Material Instance | M_Cave_Rock_MASTER_VertexPaint_MOSS のマテリアルインスタンス | SM_Cave_Rock_Pillar01REDO |
| Rocks/MI_Cave_Rock_Small_Moss | Material Instance | M_Cave_Rock_MASTER_VertexPaint_MOSS のマテリアルインスタンス | SM_Cave_Tree01 |
| Rocks/MI_Cave_Rock_Small_Moss02 | Material Instance | M_Cave_Rock_MASTER_VertexPaint_MOSS のマテリアルインスタンス | SM_Cave_StoneCluster03 |
| Rocks/MI_M_Cave_Rock_Bricks_Moss22 | Material Instance | M_Cave_Rock_MASTER_VertexPaint_MOSS のマテリアルインスタンス<br>VertexPaintWetness_Switch を true に設定している。<br>Wetness は blue のチャンネルを使うが、どこも塗っていない。 | SM_Cave_Brick_01a2<br>SM_Cave_Brick_01e |
| Rocks/MI_M_Cave_Rock_Ceiling | Material Instance | M_Cave_Rock_MASTER のマテリアルインスタンス | SM_Cave_Rock_Medium01 |
| Rocks/M_Cave_Rock_MASTER | Material | 岩のマスターマテリアル | MI_Cave_Rock_Flat<br>MI_Cave_Rock_Large02<br>MI_M_Cave_Rock_Ceiling |
| Rocks/M_Cave_Rock_MASTER_VertexPaint_MOSS | Material | 岩のマスターマテリアル | MI_Cave_Rock_Pillar_Moss2<br>MI_Cave_Rock_Small_Moss<br>MI_Cave_Rock_Small_Moss02<br>MI_M_Cave_Rock_Bricks_Moss22 |
| Rocks/M_Cave_RuneRocks01 | Material | 柱用のマテリアル<br>頂点色の青が斑に塗られている。<br>ただ、マテリアルからは利用していないように見える。 | ActionRPG_Dungeon02_Asset |
| Rocks/M_Cave_Wood_Beam | Material | 木の角材用のマテリアル | SM_Cave_Wood_Beam |


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

## ■ Functions/MF_VertexBlend_JM
* 頂点色とハイトマップのブレンド(減算)結果を返す。
* パラメータの要約
	* Blend_Strength ：頂点色のブレンド強度
	* HeightMap_Only ： HeightMap のみをブレンドするか、 ModulationMask を加算するか
	* ModulationMask ： HeightMap への加算用。指定しない場合は T_Cave_Rock_Stalactite_M を利用
	* TextureTiling ： ModulationMask の代わりに T_Cave_Rock_Stalactite_M を利用する際のタイリング数
	* Blend_Sharpness ： 減算結果の除数
	* Invert Vertex Colors ： Output Plug Into Alpha の値を反転するか
* 演算内容の要約
	* Temp1 = (Vertex Color Channel * Blend_Strength)
	* Temp2 = (HeightMap_Only? HeightMap: (HeightMap + (ModulationMask? ModulationMask: (T_Cave_Rock_Stalactite_M * TextureTiling))))
	* Temp3 = (Temp1 - Temp2) / Blend_Sharpness
	* Temp4 = clamp(Temp3, 0, 1)
	* Output Plug Into Alpha = Invert Vertex Colors? Temp4: (1 - Temp4)
	* Output Unclamped Alpha = Temp3

## ■ Functions/MF_Wetness
* 頂点色と乗算用マスクから MaterialAttributes を算出して結果を返す。
	* 濡れ表現用
* パラメータの要約
	* Switch ： false の場合は超転職と城さん用マスクを参照しない。
	* Vertex Color Channel ： 使用する超転職のチャンネル
	* VBlendSharpness ： Vertex Color Channel の除数
	* ModulationMask ： 乗算マスク
	* WetnessRoughness ： ラフネス値
	* WetNormalBlend ： ノーマル値
	* Material ： 元となる MaterialAttributes 。省略した場合は固定値。
* 演算内容の要約
	* Temp1 = clamp((Vertex Color Channel * 2.5) - clamp(ModulationMask + 0.1, 0, 1) / VBlendSharpness, 0, 1)
	* BaseColor = Switch? LightmassReplace(Lerp(Material.BaseColor, (Material.BaseColor ^ 1.5), Temp1), Material.BaseColor * 1.5) : Material.BaseColor
	* Metallic = Material.Metallic
	* Specular = Lerp(Material.Specular, 1, Temp1)
	* Roughness = Switch? Lerp(Material.Roughness, WetnessRoughness, Temp1) : Material.Roughness
	* Normal = Switch? Lerp(Material.Normal, Normalize(Material.Normal + WetNormalBlend), Temp1) : Material.Normal


----
以上。

