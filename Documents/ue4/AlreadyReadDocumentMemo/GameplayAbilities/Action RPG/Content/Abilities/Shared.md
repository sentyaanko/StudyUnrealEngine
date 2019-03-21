# ■ Abilities/Shared の内容

## ■ Actorクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| BP_AbilityProjectileBase | Actor | Actor | 発射物の基底 |

**★EventGrapの内容確認**

## ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_MeleeBase | RPGGameplayAbility | RPGGameplayAbility | 近接攻撃の基底|
| GA_PotionBase | RPGGameplayAbility | RPGGameplayAbility | ポーションの基底 |
| GA_SkillBase | RPGGameplayAbility | RPGGameplayAbility | スキルの基底 |
| GA_SpawnProjectileBase | RPGGameplayAbility | RPGGameplayAbility | 発射物をSpawnさせる基底 |

**★EventGrapの内容確認**

### ■ GA_MeleeBase
```yaml
Default:
 Montage-to-Play: "None"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.WeaponHit"
    Value:
     Target-Type: "RPGTargetType_UseEventData"
     Target-Gameplay-Effect-Classes:
      - "GE_MeleeBase"
Tags:
 Ability-Tags: "Ability.Melee"
```

### ■ GA_PotionBase
```yaml
Default:
 Montage-to-Play: "None"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseItem"
    Value:
     Target-Type: "RPGTargetType_UseOwner"
     Target-Gameplay-Effect-Classes:
      - "GE_HealBase"
Tags:
 Ability-Tags: "Ability.Item"
```

### ■ GA_SkillBase
```yaml
Default:
 Montage-to-Play: "None"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseSkill"
    Value:
     Target-Type: "None"
     Target-Gameplay-Effect-Classes:
      - "GE_RangedBase"
Tags:
 Ability-Tags: "Ability.Skill"
```

### ■ GA_SpawnProjectileBase

* Skill の一種。
* このクラスを派生し、BP Ability Projectile の変数を設定することでFireballのような飛び道具を扱える。

```yaml
Default:
 Montage-to-Play: "None"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseSkill"
    Value:
     Target-Type: "None"
     Target-Gameplay-Effect-Classes:
      - "GE_RangedBase"
Tags:
 Ability-Tags: "Ability.Skill"
```

## ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_DamageBase | GameplayEffect | GameplayEffect |  |
| GE_DamageImmune | GameplayEffect | GameplayEffect |  |
| GE_HealBase | GameplayEffect | GameplayEffect |  |
| GE_MeleeBase | GE_DamageBase | GameplayEffect |  |
| GE_RangedBase | GE_DamageBase | GameplayEffect |  |
| GE_StatsBase | GameplayEffect | GameplayEffect |  |

### ■ GE_DamageBase

* GE_MeleeBase/GE_RangedBase も全く同じ設定。
* GE_Range**d**Base、これだけd付き。わかりづらい。

```yaml
Gameplay-Effect:
 Executions:
  - Calculation-Class: "RPGDamageExecution"
    Calculation-Modifiers:
     - Backing-Capture-Definition:
        Capture-Attribute: "Damage"
        Capture-Source: "Source"
        Capture-Status: "Snapshotted"
       Modify-Op: "Add"
       Modify-Magnitude:
        Magnitude-Calculation-Type: "Scalabe Float"
        Scalable-Float-Magnitude:
         Raw: "1.0"
         Curve-Table: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "Status.DamageImmune"
```

### ■ GE_DamageImmune
```yaml
Tags:
 GrantedTags:
  Combined-Tags: "Status.DamageImmune"
  Added: "Status.DamageImmune"
```

### ■ GE_HealBase
```yaml
Gameplay-Effect:
 Modifiers:
  - Attribute: "RPGAttributeSet.Health"
    Modifier-Op: "Add"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "AttackDamage"
      Record: "HeavyAttack"
```

### ■ GE_StatsBase
```yaml
Gameplay-Effect:
 Modifiers:
  - Attrivute: "RPGAttributeSet_MaxHealth"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "DefaultMaxHealth"
  - Attrivute: "RPGAttributeSet_MaxMana"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "DefaultMaxMana"
  - Attrivute: "RPGAttributeSet_AttackPower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "DefaultAttackPower"
  - Attrivute: "RPGAttributeSet_DefencePower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "DefaultDefencePower"
  - Attrivute: "RPGAttributeSet_MoveSpeed"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "DefaultMoveSpeed"
```

## ■ ターゲットタイプクラス

| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_SphereTrace | RPGTargetType | RPGTargetType | SphereTraceをするターゲット選択基底 |

**★EventGrapの内容確認**


----
以上。
