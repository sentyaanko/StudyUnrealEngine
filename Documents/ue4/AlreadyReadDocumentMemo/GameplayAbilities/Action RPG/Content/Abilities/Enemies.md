
# ■ Abilities/Enemies/Goblin の内容
## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_GoblinMelee | GA_MeleeBase | ★登録先の確認 |
| GA_GoblinRange01 | GA_SpawnProjectileBase | ★登録先の確認 |

### ■ GA_GoblinMelee
```yaml
Default:
 Montage-to-Play: "AM_Guardian_Attack"
 Projectile-class: "BP_Slimeball"
Gameplay-Effect:
 Effect Container Map:
  - Key: "Event.Montage.Shared.WeaponHit"
    Value:
     Target-Type: "RPGTargetType_UseEventData"
     Target-Gameplay-Effect-Classes:
      - "GE_GoblinMelee"
Tags:
 Abilitiy-Tags: "Ability.Melee"
Cooldowns:
  Cooldown-Gameplay-Effect-Class: "None"
```

### ■ GA_GoblinRange01
```yaml
Default:
 Montage-to-Play: "AM_Guardian_Attack02"
 Projectile-class: "BP_Slimeball"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: Event.Montage.Shared.UseSkill
    Value: 
      Target-Type: "None"
      Target-Gameplay-Effect-Classes:
       - "GE_PlayerSkillFireball"
Tags:
 Abilitiy-Tags: "Ability.Skill"
Cooldowns:
 Cooldown-Gameplay-Effect-Class: "GE_GoblinRange"
```

## ■ アビリティエフェクトクラス
| 名前 | 親クラス | 登録先 Ability | 登録先 属性 | 用途 |
| ----- | ----- | ----- | ----- | ----- |
| GE_GoblinMelee | GE_MeleeBase | GA_GoblinMelee | EffectContainerMap | |
| GE_GoblinRange | GE_MeleeBase | GA_GoblinRange01 | Cooldown | クールダウン |
| GE_GoblinStats | GE_StatsBase | | | Spawn時のパラメータの初期化用。★登録先確認  |

| 名前 | 登録先 EffectContainerMap のキー名 |
| ----- | ----- |
| GE_GoblinMelee | [Event.Montage.Shared.WeaponHit] |


### ■ GE_GoblinMelee
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

### ■ GE_GoblinRange
```yaml
Gameplay-Effect:
 Duration-Policy: "Has Duration"
 Duration-Magnitude:
  Magnitude-Calculation-Type: "Scalable Float"
  Scalable-Float-Magnitude:
   Raw: "2"
   Curve-Table: "None"
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
         Raw: "1.5" #特有
         Curve-Table: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_GoblinStats
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

# ■ Abilities/Enemies/Spider の内容
## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_SpiderMelee | GA_SkillBase | ★登録先の確認 |

### ■ GA_SpiderMelee
```yaml
Default:
 Montage-to-Play: "AM_Spider_Melee"
 Gameplay-Effect:
  Effect-Container-Map:
   - Key: "Event.Montage.Shared.UseSkill"
     Value:
      Target-Type: "TargetType_Claw"
      Target-Gameplay-Effect-Classes:
       - "GE_RangeBase"
Tags:
 Abilitiy-Tags: "Ability.Skill"
Cooldowns:
 Cooldown-Gameplay-Effect-Class: "None"
```

## ■ アビリティエフェクトクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GE_SpiderStats | GE_StatsBase | Spawn時のパラメータの初期化用。★登録先確認 |

### ■ GE_SpiderStats
```yaml
Gameplay-Effect:
 Modifiers:
  - Attrivute: "RPGAttributeSet_MaxHealth"
    Modifier-Op: "Multiply" #特有
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "3.0" #特有
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
      Raw: "2.0" #特有
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
      Raw: "1.5" #特有
      Curve-Table: "StartingStats"
      Record: "DefaultMoveSpeed"
```

## ■ ターゲットタイプクラス
| 名前 | 登録先 Ability | 親クラス | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- | ----- |
| TargetType_Claw | TargetType_SphereTrace |GA_SpiderMelee |  [Event.Montage.Shared.UseSkill] |

### ■ TargetType_Claw
```yaml
Default:
 Offset-from-Actor:
  x: "400" #特有
 Sphere-Radius: "150" #特有
```


----
以上。
