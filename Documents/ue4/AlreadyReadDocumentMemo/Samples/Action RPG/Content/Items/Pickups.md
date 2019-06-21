# ■ Items/Pickups の内容
* モデルやテクスチャが Assets フォルダに置かれている。
* マップに配置するための BP が置かれている。
* ポーションの Enumeration が置かれている。

## ■ フォルダ一覧

| フォルダ名 | 内容 |
| ----- | ----- |
| PosionPickups/Assets/DeathsDoor | マップに配置する DeathsDoor のアセット置き場 |
| PosionPickups/Assets/Hambone | マップに配置する骨付き肉のアセット置き場 |
| PosionPickups/Assets/Sucker | マップに配置する棒付きキャンディーのアセット置き場 |

## ■ ファイル PosionPickups/BP_Potion_PickUp
* 内容
	* マップに配置するための BP
* 親クラス
	* Actor
* 参照元
	* BP_EnemyCharacter
	* ActionRPG_Dungeon02_Asset

## ■ ファイル PosionPickups/PotionList
* 内容
	* Postion の種類の一覧
	* 敵がドロップする骨付き肉の効果をランダムで決める際の候補の一覧として利用
* 参照元
	* BP_EnemyCharacter
	* BP_Potion_PickUp

## ■ ファイル一覧 PosionPickups/Assets/DeathsDoor/

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_DeathDoorSkulls | Material | 骨付き肉用 | BP_Potion_PickUp<br>M_DeathDoorSkulls_Inst |
| M_DeathDoorSkulls_Inst | Materia lInstance | DeathsDoor 用 | SM_DeathDoorSkulls<br><br>ActionRPG_Dungeon02_Asset |
| SM_DeathDoorSkulls | StaticMesh | DeathsDoor 用<br>BP_Potion_PickUp の<br>呼び出されないノードで指定されている<br>おそらく利用されていない | BP_Potion_PickUp |
| SM_DeathDoorSkulls_2 | StaticMesh | DeathsDoor 用<br>配置はこちらを利用 | BP_Potion_PickUp<br>ActionRPG_Dungeon02_Asset |
| T_DeathDoorSkulls_BC | Texture | DeathsDoor のベースカラー<br>RGB:ベースカラー<br>R:ラフネス値の要素 | M_DeathDoorSkulls |
| T_DeathDoorSkulls_N | Texture | DeathsDoor のノーマルマップ | M_DeathDoorSkulls |

## ■ ファイル一覧 PosionPickups/Assets/Hambone/

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Hambone | Material | 骨付き肉・棒付きキャンディー用 | M_Hambone_Inst<br>M_Sucker_Inst |
| M_Hambone_Inst | Material　Instance | 骨付き肉・棒付きキャンディー用 | BP_Potion_PickUp<br>SM_Sucker<br>ActionRPG_Dungeon02_Asset |
| SM_Hambone | StaticMesh | 骨付き肉用 | BP_Potion_PickUp<br>ActionRPG_Dungeon02_Asset<br>M_Hambone |
| T_Hambone1_D | Texture | 骨付き肉用ベースカラー<br>RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Hambone<br>M_Hambone_Inst |
| T_Hambone1_N | Texture | 骨付き肉用ノーマルマップ | M_Hambone<br>M_Hambone_Inst |
| T_Hambone2_D | Texture | 骨付き肉用ベースカラー<br>RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Hambone<br>M_Hambone_Inst |
| T_Hambone2_N | Texture | 骨付き肉用ノーマルマップ | M_Hambone<br>M_Hambone_Inst |

## ■ ファイル一覧 PosionPickups/Assets/Sucker/

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Sucker_Inst | Material Instance | 棒付きキャンディー用 | BP_Potion_PickUp<br>SM_Sucker<br>ActionRPG_Dungeon02_Asset |
| SM_Sucker | StaticMesh | 棒付きキャンディー用 | BP_Potion_PickUp<br>ActionRPG_Dungeon02_Asset |
| T_Sucker1_D | Texture | 棒付きキャンディー用ベースカラー<br>RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Sucker_Inst<br>ActionRPG_Dungeon02_Asset |
| T_Sucker1_N | Texture | 棒付きキャンディー用ノーマルマップ | M_Sucker_Inst<br>ActionRPG_Dungeon02_Asset |
| T_Sucker2_D | Texture | 棒付きキャンディー用ベースカラー<br>RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Sucker_Inst<br>ActionRPG_Dungeon02_Asset |
| T_Sucker2_N | Texture | 棒付きキャンディー用ノーマルマップ | M_Sucker_Inst<br>ActionRPG_Dungeon02_Asset |


----
以上。

