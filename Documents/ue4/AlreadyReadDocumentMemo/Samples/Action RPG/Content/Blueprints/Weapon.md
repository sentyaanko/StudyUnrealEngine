# ■ BluePrints/Weapon の内容
* 直下にプレイヤー用の武器が置かれている。
* サブフォルダ Goblin 以下にそれ用の武器が置かれている。

## ■ BP 一覧
* すべてのネイティブ親クラスは Actor になっている。

| 名前 | 親クラス | 用途 | 参照元 |
| ----- | ----- | ----- | ----- |
| WeaponActor | Actor | 武器の基底<br>Sword 用 | Weapon_Sword<br>BP_Character<br>BP_EnemyCharacter<br>BP_PlayerCharacter<br>WeaponAttackNS<br>NPC_GoblinBP<br>BladeTalonActor<br>FireAxeActor<br>GreateBladeActor<br>HammerActor<br>GuardianWeaponActor<br>GoblinWeapon_Base<br>WB_InputButton |
| BladeTalonActor | WeaponActor | Talon 用 | Weapon_Talon |
| GreateBladeActor | WeaponActor | Axe 用 | Weapon_Axe |
| FireAxeActor | WeaponActor | FireAxe 用 | Weapon_Axe_2 |
| HammerActor | WeaponActor | Hammer 用 | Weapon_Hammer |
| GuardianWeaponActor | WeaponActor | 敵用のデフォルト設定用 | NPC_GoblinBP |
| GoblinWeapon_Base | WeaponActor | Goblin 用の武器の基底<br>NPC_Goblin_Level_01 用の武器 | NPC_Goblin_Level_01<br>GoblinWeapon_Axe<br>GoblinWeapon_Torch |
| GoblinWeapon_Axe | GoblinWeapon_Base | NPC_Goblin_Level_02 用の武器 | NPC_Goblin_Level_02 |
| GoblinWeapon_Torch | GoblinWeapon_Base | NPC_Goblin_Level_03 用の武器 | NPC_Goblin_Level_03 |

* コンポーネント「 CapsuleCpllision 」のプロパティ「 Shape/Capsule Half Height 」「 Shape/Capsule Redius 」を  
  それぞれのメッシュの大きさに合うようにに変更している。

## ■ 見た目の設定について
* Player 用はコンポーネント「 SkeltalMesh 」のプロパティ「 Mesh/Skeltal Mesh 」をそれぞれのスケルタルメッシュに変更している。  
* Goblin 用は GoblinWeapon_Base にて。

## ■ WeaponActor
* 武器の基底。
* Player 用の武器である BladeTalon/Axe/FireAxe/Hammer はこれを派生した BP となっている。
* Player 用の武器である Sword 用の BP でもある。
* NPC_GoblinBP の設定で利用されている GuardianWeaponActor の基底でもある。
* Goblin 用の武器の基底の GoblinWeapon_Base の基底でもある。

## ■ GuardianWeaponActor
* NPC_GoblinBP のプロパティ「 Default/Weapon 」 のデフォルト値。  
  この設定は NPC_Goblin_Level_* にて上書きされているため、利用されてはいない。  
  GuardianWeaponActor がなくても平気か要確認。

## ■ GoblinWeapon_Base
* Goblin 用の武器である GoblinWeapon_Axe/GoblinWeapon_Torch はこれを派生した BP となっている。
* Goblin 用の武器であるとげ付きこん棒？用の BP でもある。
* コンポーネント「 SkeltalMesh 」のプロパティ「 Mesh/Skeltal Mesh 」を None に設定している。  
  コンポーネント「 StaticMesh 」を追加していて、そちらでスタティックメッシュを指定している。  
* プロパティ「 Weapon Defaults/Enable Attack Delay 」のデフォルト値 true を false に変更している。

## ■ GoblinWeapon_Torch
* コンポーネント「 ParticleSystem 」 を追加している。


----
以上。
