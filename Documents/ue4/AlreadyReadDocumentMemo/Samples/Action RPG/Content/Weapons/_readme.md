# ■ Weapons の内容
* Player と Goblin の武器の Material / Skeltal Mesh / Skelton / Static Mesh が置かれている。
	* Player 用は Skeltal Mesh / Skelton
	* Goblin 用は Static Mesh
* Player 用は武器ごとにフォルダ分けされている。
	* プレイヤー用のマテリアルはほぼ同じ内容なので１つにまとめられそう。
	* その場合、現在省かれている全面白のテクスチャをわざわざ用意したり、 Composite Texture をどうにかする必要はある。
* Goblin 用は Material / Texture を共用しており、 Enemy_Gruntling_Weapons フォルダに格納されている。

## ■ フォルダ一覧

| フォルダ名 | 内容 |
| ----- | ----- |
| Blade_BlackKnight | Knight Sword 用のファイル置き場 |
| Blade_GreatBlade | Molten Axe 用のファイル置き場 |
| Blade_Hatchet02 | Cleaver 用のファイル置き場 |
| Blade_Talon | Talon Sword 用のファイル置き場 |
| Blunt_SpikedClub | Spiked Blunt 用のファイル置き場 |
| Weapon_ForgingHammers | War Hammer 用のファイル置き場 |
| Enemy_Gruntling_Weapons | Goblin 用のファイル置き場 |


## ■ ファイル一覧
### ■ ファイル一覧(Blade_BlackKnight)

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Blade_BlackKnight | Material |  | SK_Blade_BlackKnight |
| SK_Blade_BlackKnight | Skeletal Mesh |  | BP_Weapon_Sword_BlackKnight<br>SK_Blade_BlackKnight_Skeleton<br>SK_Mannequin_Skeleton<br>M_Blade_BlackKnight |
| SK_Blade_BlackKnight_Skeleton | Skeleton |  | SK_Blade_BlackKnight |
| T_Blade_BlackKnight_Sword1_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_BlackKnight |
| T_Blade_BlackKnight_Sword2_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_BlackKnight |
| T_Blade_BlackKnight_Sword1_M | Texture | RGB:メタリック | M_Blade_BlackKnight |
| T_Blade_BlackKnight_Sword2_M | Texture | RGB:メタリック | M_Blade_BlackKnight |
| T_Blade_BlackKnight_Sword1_N | Texture | RGB:ノーマルマップ | M_Blade_BlackKnight |
| T_Blade_BlackKnight_Sword2_N | Texture | RGB:ノーマルマップ | M_Blade_BlackKnight |

### ■ ファイル一覧(Blade_GreatBlade)

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Blade_FireAxe | Material | | FireAxeActor |
| M_Blade_GreatBlade | Material | M_Blade_FireAxe とほぼ同じ<br>（エミッシブカラーのみ異なる）<br>Material Instance にしていない理由は不明。<br>Intro デモ中のプレイヤーの武器のマテリアル。 | SK_Blade_GreatBlade |
| SK_Blade_GreatBlade | Skeletal Mesh | | FireAxeActor<br>SQ_Intro_Warrior_AnimData<br>M_Blade_FireAxe<br>M_Blade_GreatBlade<br>SK_Blade_GreatBlade_Skeleton |
| SK_Blade_GreatBlade_Skeleton | Skeleton | | SK_Blade_GreatBlade |
| T_Blade_GreatBlade1_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_FireAxe<br>M_Blade_GreatBlade |
| T_Blade_GreatBlade2_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_FireAxe<br>M_Blade_GreatBlade |
| T_Blade_GreatBlade1_M | Texture | RGB:メタリック | M_Blade_FireAxe<br>M_Blade_GreatBlade |
| T_Blade_GreatBlade2_M | Texture | RGB:メタリック | M_Blade_FireAxe<br>M_Blade_GreatBlade |
| T_Blade_GreatBlade1_N | Texture | RGB:ノーマルマップ | M_Blade_FireAxe<br>M_Blade_GreatBlade |
| T_Blade_GreatBlade2_N | Texture | RGB:ノーマルマップ | M_Blade_FireAxe<br>M_Blade_GreatBlade |

### ■ ファイル一覧(Blade_Hatchet02)

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Blade_Hatchet02 | Material |  | SK_Blade_Hatchet02 |
| SK_Blade_Hatchet02 | Skeletal Mesh |  | GreateBladeActor<br>SK_Blade_Hatchet02_Skeleton |
| SK_Blade_Hatchet02_Skeleton | Skeleton |  | SK_Blade_Hatchet02 |
| T_Blade_Hatchet021_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_Hatchet02 |
| T_Blade_Hatchet022_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_Hatchet02 |
| T_Blade_Hatchet021_M | Texture | RGB:メタリック | M_Blade_Hatchet02 |
| T_Blade_Hatchet022_M | Texture | RGB:メタリック | M_Blade_Hatchet02 |
| T_Blade_Hatchet021_N | Texture | RGB:ノーマルマップ | M_Blade_Hatchet02 |
| T_Blade_Hatchet022_N | Texture | RGB:ノーマルマップ | M_Blade_Hatchet02 |

### ■ ファイル一覧(Blade_Talon)
* 上部が全て金属のため、メタリック用のテクスチャが省略されている。

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Blade_Talon | Material |  | SK_Blade_Talon |
| SK_Blade_Talon | Skeletal Mesh |  | BP_Weapon_Sword_Talon<br>SK_Blade_Talon_Skeleton |
| SK_Blade_Talon_Skeleton | Skeleton |  | SK_Blade_Talon |
| T_Blade_Talon1_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_Talon |
| T_Blade_Talon2_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blade_Talon |
| T_Blade_Talon2_M | Texture | RGB:メタリック | M_Blade_Talon |
| T_Blade_Talon1_N | Texture | RGB:ノーマルマップ | M_Blade_Talon |
| T_Blade_Talon2_N | Texture | RGB:ノーマルマップ | M_Blade_Talon |

### ■ ファイル一覧(Blunt_SpikedClub)
* 上部が全て金属のため、メタリック用のテクスチャが省略されている。

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Blunt_SpikedClub | Material |  | SK_Blunt_SpikedClub |
| SK_Blunt_SpikedClub | Skeletal Mesh |  | BP_Weapon_Hammer_1<br>GuardianWeaponActor<br>SK_Blunt_SpikedClub_Skeleton<br>SQ_Intro_Enemy_AnimData<br>SK_Gruntling_Guardian_Skeleton |
| SK_Blunt_SpikedClub_Skeleton | Skeleton |  | SK_Blunt_SpikedClub |
| T_Blunt_SpikedClub1_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blunt_SpikedClub |
| T_Blunt_SpikedClub2_D | Texture | RGB:ベースカラーの要素<br>R:ラフネス値の要素 | M_Blunt_SpikedClub |
| T_Blunt_SpikedClub2_M | Texture | RGB:メタリック | M_Blunt_SpikedClub |
| T_Blunt_SpikedClub1_N | Texture | RGB:ノーマルマップ | M_Blunt_SpikedClub |
| T_Blunt_SpikedClub2_N | Texture | RGB:ノーマルマップ | M_Blunt_SpikedClub |

### ■ ファイル一覧(Weapon_ForgingHammers)

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| M_Forging_Mallet_02and3_D_Mat | Material |  | SK_Forging_Mallet_02 |
| SK_Forging_Mallet_02 | Skeletal Mesh |  | BP_Weapon_Hammer_3<br>M_Forging_Mallet_02and3_D_Mat |
| SK_Forging_Mallet_03_Skeleton | Skeleton |  | SK_Forging_Mallet_02 |
| T_Forging_Mallet_02_M | Texture |  RGB:メタリック・エミッシブカラーの要素 | M_Forging_Mallet_02and3_D_Mat |
| T_Forging_Mallet_02and3_D | Texture | RGB:ベースカラー・エミッシブカラーの要素<br>A:ラフネス値 | M_Forging_Mallet_02and3_D_Mat |
| T_Forging_Mallet_02and3_N | Texture | RGB:ノーマルマップ | M_Forging_Mallet_02and3_D_Mat |

### ■ ファイル一覧(Enemy_Gruntling_Weapons)

| ファイル名 | Type | 内容 | 参照元 |
| ----- | ----- | ----- | ----- |
| Materials/M_Gruntling_weapons | Material |  | SM_Gruntling_Torch_Internal<br>SM_Gruntling_Weapon01_Internal<br>SM_Gruntling_Weapon02_Internal |
| Meshes/SM_Gruntling_Torch_Internal | Static Mesh |  | GoblinWeapon_Torch |
| Meshes/SM_Gruntling_Weapon01_Internal | Static Mesh |  | GoblinWeapon_Base |
| Meshes/SM_Gruntling_Weapon02_Internal | Static Mesh |  | GoblinWeapon_Axe |
| Textures/T_PickAxe_D | Texture | RGB:ベースカラー<br>R:ラフネス値の要素<br>T_PickAxe_N を Composite Texutre に指定 | M_Gruntling_weapons |
| Textures/T_PickAxe_E | Texture | R:エミッシブカラーの要素 | M_Gruntling_weapons |
| Textures/T_PickAxe_M | Texture | R:メタリック | M_Gruntling_weapons |
| Textures/T_PickAxe_N | Texture | RGB:ノーマルマップ | M_Gruntling_weapons<br>T_PickAxe_D |

----
以上。

