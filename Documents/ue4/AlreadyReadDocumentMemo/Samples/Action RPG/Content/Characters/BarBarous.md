# ■ Characters/Barbarous の内容
* Player のモデル、テクスチャ、マテリアルに関するファイルが置かれている。

## ■ ファイル一覧
| ファイル名 | type | 用途 | 参照元 |
| ----- | ----- | ----- | ----- |
| SK_CharM_Barbarous | Skeletal Mesh | player 用スケルタルメッシュ | BP_PlayerCharacter<br>PA_Mannequin_Physics<br>SK_Mannequin_Skeleton<br>SQ_Intro_Warrior_AnimData |
| M_Char_Barbrous | Material | SK_CharM_Barbarous 用マテリアル<br>**typo が気になる** | SK_CharM_Barbarous |
| T_CharM_Barbarous_D | Texture | Diffuse | M_Char_Barbrous |
| T_CharM_Barbarous_MetalMask | Texture | MetalMask | M_Char_Barbrous |
| T_CharM_Barbarous_N | Texture | NormalMap | M_Char_Barbrous |

## ■ M_Char_Barbrous

| 出力 | 計算内容 |
| ----- |  ----- |
| Base Color | lerp(Diffuse, Diffuse x2, MetalMask.b) |
| Metallic | MetalMask.b |
| Roughness | clamp(0.5, 0.95, lerp(0.9, 0.85, MetalMask.r+MetalMask.g) - lerp(0.1, 0.5, MetalMask.b)) |
| Normal | Normal |
| Emissive Color | 下記参照 |

* Emissive Color について
	* Emissive Color だけ、ゲーム中の状態により変更される。他はすべて固定。
	* 計算用に以下のテクスチャを参照
		* T_Lightning_Bolt_01_D
		* T_Dissolve_Mob_M
	* 計算用に以下のマテリアルパラメータを参照
		* GameEffect/EffectColor
		* GameEffect/EffectLength
		* GameEffect/EffectTexture(T_Lightning_Bolt_01_D)
		* GameEffect/StartTime

## ■ T_CharM_Barbarous_MetalMask

| ファイル名 | channel | 用途 | 利用箇所 | 
| ----- | ----- |  ----- | ----- |
| T_CharM_Barbarous_D | rgb | Diffuse | Base Color |
| T_CharM_Barbarous_N | rgb | NormalMap | Normal |
| T_CharM_Barbarous_MetalMask | r | Skin | Roughness |
| T_CharM_Barbarous_MetalMask | g | Bread | Roughness |
| T_CharM_Barbarous_MetalMask | b | Metallic | Base Color<br>Metallic |


----
以上。
