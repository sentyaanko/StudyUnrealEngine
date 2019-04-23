# ■ Effects/Masters の内容
* Particle で使用されている Material ファイルが置かれている。
* いわゆる「マスターマテリアル」置き場。

## ■ ファイル一覧

| ファイル名 | 参照元 |
| ----- | ----- |
| M_Add_Sprite_2Sided_Master | MI_Swipe_Mesh_Add_2Sided_01 |
| M_Add_Sprite_Master | MI_Shockwave_01_ADD<br>MI_Shockwave_03_Add<br>MI_Flare_Streak_01<br>M_Swipe_Mesh_Add_2Sided_01_INST |
| M_Add_Sprite_Master_DepthFade | MI_Flare_01<br>MI_Flare_03<br>MI_Flare_09<br>M_Flare_03_INST |
| M_Add_Sprite_SubUV_Master | MI_Fire_01_Add_6X6<br>MI_Fire_Shock_01_5x5_SubUV<br>MI_Lightning_Bolt_01_Add_4X1<br>MI_Smoke_01_8X8<br>MI_Spark_03_1_4<br>MI_Spark_04_SubUV_1_4 |
| M_Add_Trail_2Sided_Pan_Master | MI_Fire_Sheet_01 |
| M_Opaque_MeshEmit_Lit_Emis_Master | MI_Jagged_Rock_01_Lit |
| M_Trans_MeshEmit_2Sided_Pan_Mask_Master | MI_Tile_Noise_Tendril_01_in |
| M_Trans_MeshEmit_Master | MI_Jagged_rock_01 |
| M_Trans_Sprite_Lit_SubUV_Master | MI_RockDebris_Trans |
| M_Trans_Sprite_Master_DepthFade | MI_Liquid_Spray_01_4X6 |
| M_Trans_Sprite_Master_Surface | MI_CrackedGround_01 |
| M_Trans_Sprite_SubUV_Master | MI_RockDebrisFire_Trans<br>MI_Lightning_Arc_01_Trans_4X1<br>MI_Fireball_01_8X8 |
| M_Trans_Sprite_SubUV_Master_DepthFade | MI_Smoke_02_Trans_6X6 |

## ■ M_Add_Sprite_2Sided_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 加算合成したい
		* 光らせたい
		* ライティング利用しない
		* 両面描画したい
	* Emitter に Mesh Data を追加し、そのマテリアルとして利用されている。
* 出力
	* Emissive Color

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Additive |
| Material/ShadingModel | Unlit |
| Material/Two sided | true |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Beam Trails | true |
| Usage/Used with Mesh Particles | true |
| Mobile/Use Full Precision | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | Particle Color と乗算しさらに 20 倍したものを Emissive Color で利用 |

## ■ M_Add_Sprite_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 加算合成したい
		* 光らせたい
		* ライティング利用しない
		* 光らす強度を指定したい
		* 半透明の指定をしたい
	* 光らせたいかつ、 Particle Color のα値で半透明にする物で用途で利用されている。
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Additive |
| Material/ShadingModel | Unlit |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[1].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | Particle Color と乗算しさらに PP 倍したものを Emissive Color で利用 |
| PP | Emissive Color の係数 |

## ■ M_Add_Sprite_Master_DepthFade
* 概要
	* 以下のことを行いたいもので利用されている。
		* 加算合成したい
		* 光らせたい
		* ライティング利用しない
		* Depth Fade を利用したい
	* 粒子が大きく不透明なオブジェクトと重なるケースが多いもので利用されている。
* 出力
	* Emissive Color

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Additive |
| Material/ShadingModel | Unlit |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | Particle Color と乗算しさらに Depth Fade したものを Emissive Color で利用 |

## ■ M_Add_Sprite_SubUV_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 加算合成したい
		* 光らせたい
		* ライティング利用しない
		* 光らす強度を指定したい
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Opaque |
| Material/ShadingModel | Default Lit |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Usage/Use Static Lighting | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[1].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Emissive Color で利用 |
| EMISS | エミッシブテクスチャ<br>Emissive Color で利用 |
| IsPannerDIFF | DIFF のパンを行うか |
| IsVirticalPanner | EMISS のパンを縦方向にするか（しない場合は横方向） |
| IsVirticalPannerDIFF | DIFF のパンを縦方向にするか（しない場合は横方向） |
| UTile | EMISS の横方向のタイリング数 |
| UTileDiff | DIFF の横方向のタイリング数 |
| VTile | EMISS の縦方向のタイリング数 |
| VTileDiff | DIFF の縦方向のタイリング数 |


## ■ M_Add_Trail_2Sided_Pan_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 加算合成したい
		* 光らせたい
		* ライティング利用しない
		* 両面描画したい
		* Depth Fade したい
		* テクスチャの UV スクロール(Panner)をしたい
		* ディフューズテクスチャとは別に発光のためのテクスチャを指定したい
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Additive |
| Material/ShadingModel | Unlit |
| Material/Two sided | true |
| Usage/Used with Beam Trails | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[1].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[2].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[3].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[4].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[5].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[6].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[7].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[8].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Emissive Color で利用 |
| EMISS | エミッシブテクスチャ<br>Emissive Color で利用 |
| IsPannerDIFF | DIFF のパンを行うか |
| IsVirticalPanner | EMISS のパンを縦方向にするか（しない場合は横方向） |
| IsVirticalPannerDIFF | DIFF のパンを縦方向にするか（しない場合は横方向） |
| UTile | EMISS の横方向のタイリング数 |
| UTileDiff | DIFF の横方向のタイリング数 |
| VTile | EMISS の縦方向のタイリング数 |
| VTileDiff | DIFF の縦方向のタイリング数 |

## ■ M_Opaque_MeshEmit_Lit_Emis_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 光らせたい
		* ライティング利用する
		* ディフューズテクスチャとは別に発光のためのテクスチャを指定したい
	* 現状では EMISS に有効なテクスチャを指定しているマテリアルインスタンスは存在しない
* 出力
	* Base Color
	* Emissive Color

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Opaque |
| Material/ShadingModel | Default Lit |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Usage/Use Static Lighting | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[1].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Base Color で利用 |
| EMISS | エミッシブテクスチャ<br>Emissive Color で利用 |

## ■ M_Trans_MeshEmit_2Sided_Pan_Mask_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 光らせたい
		* 透過させたい（鏡面反射指定できなくてよい）
		* ライティング利用しない
		* 両面描画したい
		* パンの速度を指定したい
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Unlit |
| Material/Two sided | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[1].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Emissive Color で利用 |
| PannnerSpeed | パンの速度<br>Emissive Color/Opacity で利用 |

## ■ M_Trans_MeshEmit_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 光らせたい
		* 透過させたい（鏡面反射指定できなくてよい）
		* ライティング利用しない
	* Meteor の落石の軌跡部分で利用
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Unlit |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Emissive Color/Opacity で利用 |


## ■ M_Trans_Sprite_Lit_SubUV_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 透過させたい（鏡面反射指定できなくてよい）
	* 岩の破片で利用
* 出力
	* Base Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Default Lit |
| Usage/Used with Particle Sprites | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Base Color/Opacity で利用 |

## ■ M_Trans_Sprite_Master_DepthFade
* 概要
	* 以下のことを行いたいもので利用されている。
		* 光らせたい
		* 透過させたい（鏡面反射指定できなくてよい）
		* ライティング利用しない
		* Depth Fade したい
	* 液体の噴出で利用
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Unlit |
| Usage/Used with Particle Sprites | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Base Color/Opacity で利用 |

## ■ M_Trans_Sprite_Master_Surface
* 概要
	* 以下のことを行いたいもので利用されている。
		* 透過させたい（鏡面反射指定できなくてよい）
		* 法線出力したい
		* Depth Fade したい
	* 地面の亀裂エフェクトで利用
* 出力
	* Base Color
	* Opacity
	* Normal

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Default Lit |
| Translucency/Lighting Mode | Surface TranslucencyVolume |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |
| Group Sorting/Parameter Group Data[1].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Base Color/Opacity で利用 |
| NORM | ノーマルマップ<br>Normal で利用 |

## ■ M_Trans_Sprite_SubUV_Master
* 概要
	* 以下のことを行いたいもので利用されている。
		* 光らせたい
		* 透過させたい（鏡面反射指定できなくてよい）
		* ライティング利用しない
	* UV アニメーションがあるパーティクルで利用
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Unlit |
| Usage/Used with Particle Sprites | true |
| Usage/Used with Mesh Particles | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Emissive Color/Opacity で利用 |

## ■ M_Trans_Sprite_SubUV_Master_DepthFade
記載中

* 概要
	* 以下のことを行いたいもので利用されている。
		* 光らせたい
		* 透過させたい（鏡面反射指定できなくてよい）
		* ライティング利用しない
		* Depth Fade したい
	* UV アニメーションがあるパーティクルで利用
* 出力
	* Emissive Color
	* Opacity

Details
| プロパティ名 | 値 |
| ----- | ----- |
| Material/BlendMode | Translucent |
| Material/ShadingModel | Unlit |
| Usage/Used with Particle Sprites | true |
| Group Sorting/Parameter Group Data[0].Group Sort Priority | 0 |

パラメータ
| パラメータ名 | 用途 |
| ----- | ----- |
| DIFF | ディフューズテクスチャ<br>Emissive Color/Opacity で利用 |


----
以上。
