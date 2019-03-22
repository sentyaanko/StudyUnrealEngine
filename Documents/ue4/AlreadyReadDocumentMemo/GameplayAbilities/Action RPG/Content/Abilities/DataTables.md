# ■ Abilities/DataTables の内容
## ■ Curve Table の用途
| 名前 | 用途 |
| ----- | ----- |
| AttackDamage | ダメージ計算用 |
| AttackDamage_Fire | ダメージ計算用 |
| AttackDamage_Hammer | ダメージ計算用 |
| AttackDamage_Sword | ダメージ計算用 |
| StartingStats | キャラクターのレベルごとの初期ステータス用 |

## ■ ダメージ計算用
| 名前 | 用途 |
| ----- | ----- |
| AttackDamage |  ★ Axe と Goblin のダメージ計算用？<br>Axe の BurstPound/GroundPound/Melee にて利用。<br>Goblin の Melee/Range にて利用。<br>Fireball/FireWave/Meteor/MeteorStorm にて利用。<br>DamageBase/RangedBase/MeleeBase にて利用<br>HealBase にて利用。 |
| AttackDamage_Fire | ★ FireAxe のダメージ計算用？<br>FireAxe  の BurstPound/GroundPound/Melee にて利用。<br>**※ Axe を略しているのがここだけなので分かりにくい。** |
| AttackDamage_Hammer | ★ Hammer のダメージ計算用？<br>Hammer の BurstPound/GroundPound/Melee にて利用。 |
| AttackDamage_Sword | ★ Sword のダメージ計算用？<br>Sword の ChestKick/FrontalAttack/JumpSlam にて利用。 |

* カラムはすべて1-10
* レコードは3行で下記の表のとおり。

| レコードの名前 | 用途 |
| ----- | ----- |
| DefaultAttack | ★通常威力攻撃？<br>Axe/FireAxe/Hammer の Melee にて利用。<br>Goblin の Melee/Range にて利用。<br>Fireball にて利用。<br>DamageBase/RangedBase/MeleeBase にて利用 |
| MediumAttack | ★中威力攻撃？<br>PlayerSkill の Meteor にて利用。 |
| HeavyAttack | ★大威力攻撃？<br>Axe/FireAxe/Hammer の BurstPound/GroundPound にて利用。<br>Sword の ChestKick/FrontalAttack/JumpSlam にて利用。<br>PlayerSkill の FireWave/MeteorStorm にて利用。<br>Potion の DeathsDoor/PotionHealth/PotionMana にて利用。<br>HealBase にて利用。 |

* Spider は Clow を使用するが、 RangedBase を利用している為、「 Curve Table:AttackDamage 、 Record:DefaultAttack 」を参照する。
* 結局どういうことかというと以下の通り。

| 分類 | 武器 | スキル | 使用テーブル | DefaultAttack | MediumAttack | HeavyAttack |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| 基底 | Base | DamageBase | AttackDamage | 〇 | | |
|  | | MeleeBase | AttackDamage | 〇 | | |
|  | | RangedBase | AttackDamage | 〇 | | |
|  | | HealBase | AttackDamage | | | 〇 |
| ポーション | Potion | DeathsDoor | AttackDamage | | | 〇 |
|  | | HealthPotion | AttackDamage | | | 〇 |
|  | | ManaPotion | AttackDamage | | | 〇 |
| プレイヤースキル | Skill | Fireball | AttackDamage | 〇 | | |
|  | | FireWave | AttackDamage | | | 〇 |
|  | | Meteor | AttackDamage | | 〇 | |
|  | | MeteorStorm | AttackDamage | | | 〇 |
| プレイヤー | Axe | Melee | AttackDamage | 〇 | | |
|  | | BurstPound | AttackDamage | | | 〇 |
|  | | GroundPound | AttackDamage | | | 〇 |
|  | FireAxe | Melee | AttackDamage_Fire | 〇 | | |
|  | | BurstPound | AttackDamage_Fire | | | 〇 |
|  | | GroundPound | AttackDamage_Fire | | | 〇 |
|  | Hammer | Melee | AttackDamage_Hammer | 〇 | | |
|  | | BurstPound | AttackDamage_Hammer | | | 〇 |
|  | | GroundPound | AttackDamage_Hammer | | | 〇 |
|  | Sword | Melee | AttackDamage_Sword | 〇 | | |
|  | | ChestKick | AttackDamage_Sword | | | 〇 |
|  | | FrontalAttack | AttackDamage_Sword | | | 〇 |
|  | | JumpSlam | AttackDamage_Sword | | | 〇 |
| 敵 | Goblin | Melee | AttackDamage | 〇 | | |
|  | | Range | AttackDamage | 〇 | | |
|  | Spider | Clow | AttackDamage | 〇 | | |

## ■ キャラクターのレベルごとの初期ステータス用
| 名前 | 用途 |
| ----- | ----- |
| StartingStats | キャラクターのレベルごとの初期ステータス用 |

* カラムはすべて1-10
* レコードは3行で下記の表のとおり。

| レコードの名前 | 用途 |
| ----- | ----- |
| DefaultMaxHealth | ★デフォルトの最大ヘルス |
| DefaultMaxMana | ★デフォルトの最大マナ |
| DefaultAttackPower | ★デフォルトの攻撃力 |
| DefaultDefensePower | ★デフォルトの防御力 |
| DefaultMoveSpeed | ★デフォルトの移動力 |
| PlayerMaxHealth | ★プレイヤーの最大ヘルス |
| PlayerMaxMana | ★プレイヤーの最大マナ |
| PlayerAttackPower | ★プレイヤーの攻撃力 |
| PlayerDefensePower | ★プレイヤーの防御力 |
| PlayerMoveSpeed | ★プレイヤーの移動力 |

----
以上。
