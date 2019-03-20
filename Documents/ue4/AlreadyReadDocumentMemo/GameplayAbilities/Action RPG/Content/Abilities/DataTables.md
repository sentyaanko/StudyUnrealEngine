# ■ Abilities/DataTables の内容
## ■ パターン１（ダメージ計算用？）
| 名前 | 用途 | カラム | レコード |
| ----- | ----- | ----- | ----- |
| AttackDamage | ★ダメージ計算用？<br>Axe の BurstPound/GroundPound/Melee にて利用。<br>Goblin の Melee/Range にて利用。| 1-10 | 後述 |
| AttackDamage_Fire | ★炎ダメージ計算用？<br>FireAxe のダメージ計算で利用。<br>**※Axeを略しているのがここだけなので分かりにくい。** | 1-10 | 後述 |
| AttackDamage_Hammer | ★ハンマーダメージ計算用？<br>Hammer の BurstPound/GroundPound/Melee にて利用。 | 1-10 | 後述 |
| AttackDamage_Sword | ★剣ダメージ計算用？ | 1-10 | 後述 |

| レコードの名前 | 用途 |
| ----- | ----- |
| DefaultAttack | ★通常威力攻撃？<br>Axe/FireAxe/Hammer の Melee にて利用。<br>Goblin の Melee/Range にて利用。 |
| MediumAttack | ★中威力攻撃？ |
| HeavyAttack | ★大威力攻撃？<br>Axe/FireAxe/Hammer の BurstPound/GroundPound にて利用。 |

## ■ パターン２（キャラクターのレベルごとの初期ステータス用？）

| 名前 | 用途 | カラム | レコード |
| ----- | ----- | ----- | ----- |
| StartingStats | ★キャラクターのレベルごとの初期ステータス用？ | 1-10 | 後述 |

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
