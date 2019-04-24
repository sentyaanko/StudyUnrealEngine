# ■ Environment/Foliage の内容
* Foliage Type ファイルが置かれている。
* レベル ActionRPG_Dungeon02_Asset に置かれている。
* レベル ActionRPG_P には設定だけされて利用はされていない。

## ■ ファイル一覧

| ファイル名 | 内容 | 配置数 | 参照元 |
| ----- | ----- | ----- | ----- |
| SM_Cave_Leaf_Pile_01_FoliageType | 散らばっている落ち葉 | 448 | ActionRPG_P<br>ActionRPG_Dungeon02_Asset |
| SM_Cave_Leaf_Pile_02_FoliageType | 固まっている落ち葉 | 113 | ActionRPG_P<br>ActionRPG_Dungeon02_Asset |
| SM_Cave_Rock_Medium01_FoliageType | 岩<br>使用されていない | 0 | ActionRPG_P |
| Soul_FoliageType1 | ムギのような植物 | 69 | ActionRPG_P<br>ActionRPG_Dungeon02_Asset |
| Soul_FoliageType2 | シダのような植物 | 61 | ActionRPG_P<br>ActionRPG_Dungeon02_Asset |

## ■ 変更しているプロパティ一覧

| ファイル名 | Mesh/<br>Mesh | Painting/<br>Density/1Kuu | Painting/<br>Density Adjustment Factor | Painting/<br>Scale X Min | Painting/<br>Scale X Max | Placement/<br>Ground Slope Angle Max | Placement/<br>Height Min | Placement/<br>Height Max | Reapply/<br>Reapply Density |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SM_Cave_Leaf_Pile_01_FoliageType | SM_Cave_Leaf_Pile_01 | 60 | 0.75 | 0.9 | 1.1 | 45 | -262144 | 262144 | True |
| SM_Cave_Leaf_Pile_02_FoliageType | SM_Cave_Leaf_Pile_02 | 100 | 1.00 | 1.0 | 1.0 | 25 | -3000 | 0 | False |
| SM_Cave_Rock_Medium01_FoliageType | SM_Cave_Rock_Medium01 | 100 | 1.00 | 1.0 | 1.0 | 45 | -262144 | 262144 | False |
| Soul_FoliageType1 | SM_LV_SoulGrass_01 | 50 | 1.00 | 1.5 | 2.0 | 45 | -262144 | 262144 | False |
| Soul_FoliageType2 | SM_LV_Soul_Foliage021SM | 50 | 1.00 | 1.0 | 1.5 | 45 | -262144 | 262144 | False |

* Mesh はすべて Environment/Meshes/Natures/ に置かれている。

----
以上。
