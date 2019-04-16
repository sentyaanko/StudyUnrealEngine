# ■ Abilities/Player の内容
## ■ アビリティエフェクトクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GE_PlayerStats | GE_StatsBase | Spawn 時のパラメータの初期化用。★呼び出し元確認 |

### ■ GE_PlayerStats
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
      Record: "PlayerMaxHealth" #毒湧
  - Attrivute: "RPGAttributeSet_MaxMana"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "PlayerMaxMana" #毒湧
  - Attrivute: "RPGAttributeSet_AttackPower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "PlayerAttackPower" #毒湧
  - Attrivute: "RPGAttributeSet_DefencePower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "PlayerDefencePower" #毒湧
  - Attrivute: "RPGAttributeSet_MoveSpeed"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      Curve-Table: "StartingStats"
      Record: "PlayerMoveSpeed" #毒湧
```

# ■ Abilities/Player/Axe の内容
## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_PlayerAxeMelee | GA_MeleeBase | ★登録先の確認 |

### ■ GA_PlayerAxeMelee
```yaml
Default:
 Montage-to-Play: "AM_Attack_Axe"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.WeaponHit"
    Value:
     Target-Type: "RPGTargetType_UseEventData"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerAxeMelee"
  - Key: "Event.Montage.Player.Combo.BurstPound"
    Value:
     Target-Type: "TargetType_BurstPound"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerAxeBurstPound"
  - Key: "Event.Montage.Player.Combo.GroundPound"
    Value:
     Target-Type: "TargetType_GroundPound"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerAxeGroundPound"
Tags:
 Ability-Tags: "Ability.Melee"
```

## ■ アビリティエフェクトクラス
* 登録先 Ability: **GA_PlayerAxeMelee** 固定

| 名前 | 親クラス | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| GE_PlayerAxeBurstPound | GE_RangeBase | [Event.Montage.Player.Combo.BurstPound] |
| GE_PlayerAxeGroundPound | GE_RangeBase | [Event.Montage.Player.Combo.GroundPound] |
| GE_PlayerAxeMelee | GE_MeleeBase | [Event.Montage.Shared.WeaponHit] |


### ■ GE_PlayerAxeBurstPound
GE_PlayerAxeGroundPound も全く同じ設定。
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
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerAxeMelee
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

## ■ ターゲットタイプクラス
* 登録先 Ability: **GA_PlayerAxeMelee** 固定
* 親クラス: **TargetType_SphereTrace** 固定

| 名前 | 登録先 EffectContainerMap のキー名 |
| ----- | ----- |
| TargetType_BurstPound | [Event.Montage.Player.Combo.BurstPound] |
| TargetType_GroundPound | [Event.Montage.Player.Combo.GroundPound] |

**※他と異なり、「 TargetType_ 」の後に武器の名前が入っておらず、わかりづらい。**

### ■ TargetType_BurstPound
```yaml
Default:
 Trace-Length: "300" #特有
```

### ■ TargetType_GroundPound
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Trace-Length: "600" #特有
```

# ■ Abilities/Player/FireAxe の内容
つくりはほぼ Axe と一緒。

## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_PlayerFireAxeMelee | GA_MeleeBase | ★登録先の確認 |

### ■ GA_PlayerFireAxeMelee
```yaml
Default:
 Montage-to-Play: "AM_Attack_FireAxe"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.WeaponHit"
    Value:
     Target-Type: "RPGTargetType_UseEventData"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerFireAxeMelee"
  - Key: "Event.Montage.Player.Combo.BurstPound"
    Value:
     Target-Type: "TargetType_FABurstPound"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerFireAxeBurstPound"
  - Key: "Event.Montage.Player.Combo.GroundPound"
    Value:
     Target-Type: "TargetType_FAGroundPound"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerFireAxeGroundPound"
Tags:
 Ability-Tags: "Ability.Melee"
```

## ■ アビリティエフェクトクラス
* 登録先 Ability: **GA_PlayerFireAxeMelee** 固定

| 名前 | 親クラス| 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| GE_PlayerFireAxeBurstPound | GE_RangeBase | [Event.Montage.Player.Combo.BurstPound] |
| GE_PlayerFireAxeGroundPound | GE_RangeBase | [Event.Montage.Player.Combo.GroundPound] |
| GE_PlayerFireAxeMelee | GE_MeleeBase | [Event.Montage.Shared.WeaponHit] |

### ■ GE_PlayerFireAxeBurstPound
GE_PlayerFireAxeGroundPound も全く同じ設定。
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
         Curve-Table: "AttackDamage_Fire" #特有
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerFireAxeMelee
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
         Curve-Table: "AttackDamage_Fire" #特有
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

## ■ ターゲットタイプクラス
* 登録先 Ability: **GA_PlayerFireAxeMelee** 固定
* 親クラス: **TargetType_SphereTrace** 固定

| 名前 | 登録先 EffectContainerMap のキー名 |
| ----- | ----- |
| TargetType_FABurstPound | [Event.Montage.Player.Combo.BurstPound] |
| TargetType_FAGroundPound | [Event.Montage.Player.Combo.GroundPound] |

**FA は FireAxe の略らしいが、この略語を使っているのはここが初めて。わかりにくい。**

### ■ TargetType_FABurstPound
```yaml
Default:
 Sphere-Radius: "120" #特有
 Trace-Length: "300" #特有
```

### ■ TargetType_FAGroundPound
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "120" #特有
 Trace-Length: "600" #特有
```

# ■ Abilities/Player/Hammer の内容
## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_PlayerHammerMelee | GA_MeleeBase | ★登録先の確認 |

### ■ GA_PlayerHammerMelee
```yaml
Default:
 Montage-to-Play: "AM_Attack_Hammer"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.WeaponHit"
    Value:
     Target-Type: "RPGTargetType_UseEventData"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerHammerMelee"
  - Key: "Event.Montage.Player.Combo.BurstPound"
    Value:
     Target-Type: "TargetType_HammerBurstPound"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerHammerBurstPound"
  - Key: "Event.Montage.Player.Combo.GroundPound"
    Value:
     Target-Type: "TargetType_HammerGroundPound"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerHammerGroundPound"
Tags:
 Ability-Tags: "Ability.Melee"
```

## ■ アビリティエフェクトクラス
* 登録先 Ability: **GA_PlayerHammerMelee** 固定

| 名前 | 親クラス | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| GE_PlayerHammerBurstPound | GE_RangeBase | [Event.Montage.Player.Combo.BurstPound] |
| GE_PlayerHammerGroundPound | GE_RangeBase | [Event.Montage.Player.Combo.GroundPound] |
| GE_PlayerHammerMelee | GE_MeleeBase | [Event.Montage.Shared.WeaponHit] |

### ■ GE_PlayerHammerBurstPound
GE_PlayerHammerGroundPound も全く同じ設定。
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
         Curve-Table: "AttackDamage_Hammer" #特有
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerHammerMelee
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
         Curve-Table: "AttackDamage_Hammer" #特有
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

## ■ ターゲットタイプクラス
* 登録先 Ability: **GA_PlayerHammerMelee** 固定
* 親クラス: **TargetType_SphereTrace** 固定

| 名前 | 登録先 EffectContainerMap のキー名 |
| ----- | ----- |
| TargetType_HammerBurstPound | [Event.Montage.Player.Combo.BurstPound] |
| TargetType_HammerGroundPound | [Event.Montage.Player.Combo.GroundPound] |

### ■ TargetType_HammerBurstPound
```yaml
Default:
 Sphere-Radius: "120" #特有
 Trace-Length: "300" #特有
```

### ■ TargetType_HammerGroundPound
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "150" #特有
 Trace-Length: "600" #特有
```


# ■ Abilities/Player/Sword の内容
## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_PlayerSwordMelee | GA_MeleeBase | ★登録先の確認 |

### ■ GA_PlayerSwordMelee
```yaml
Default:
 Montage-to-Play: "AM_Attack_Sword"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.WeaponHit"
    Value:
     Target-Type: "RPGTargetType_UseEventData"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSwordMelee"
  - Key: "Event.Montage.Player.Combo.ChestKick"
    Value:
     Target-Type: "TargetType_ChestKick"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSwordChestKick"
  - Key: "Event.Montage.Player.Combo.FrontalAttack"
    Value:
     Target-Type: "TargetType_FrontalAttack"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSwordFrontalAttack"
  - Key: "Event.Montage.Player.Combo.JumpSlam"
    Value:
     Target-Type: "TargetType_JumpSlam"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSwordJumpSlam"
Tags:
 Ability-Tags: "Ability.Melee"
```

## ■ アビリティエフェクトクラス
* 登録先 Ability: **GA_PlayerSwordMelee** 固定

| 名前 | 親クラス | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| GE_PlayerSwordChestKick | GE_RangeBase | [Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSwordFrontalAttack | GE_RangeBase | [Event.Montage.Player.Combo.FrontalAttack] |
| GE_PlayerSwordJumpSlam | GE_RangeBase | [Event.Montage.Player.Combo.JumpSlam] |
| GE_PlayerSwordMelee | GE_MeleeBase | [Event.Montage.Shared.WeaponHit] |

### ■ GE_PlayerSwordChestKick
GE_PlayerSwordFrontalAttack/GE_PlayerSwordJumpSlam も全く同じ設定。
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
         Curve-Table: "AttackDamage_Sword" #特有
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerSwordMelee
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
         Curve-Table: "AttackDamage_Sword" #特有
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```


## ■ ターゲットタイプクラス
* 登録先 Ability: **GA_PlayerSwordMelee** 固定
* 親クラス: **TargetType_SphereTrace** 固定

| 名前 | 登録先 EffectContainerMap のキー名 |
| ----- | ----- |
| TargetType_ChestKick | [Event.Montage.Player.Combo.ChestKick] |
| TargetType_FrontalAttack | [Event.Montage.Player.Combo.FrontalAttack] |
| TargetType_JumpSlam | [Event.Montage.Player.Combo.JumpSlam] |

**※他と異なり、「 TargetType_ 」の後に武器の名前が入っておらず、わかりづらい。**

### ■ TargetType_ChestKick
```yaml
Default:
 Offset-from-Actor:
  x: "150" #特有
 Sphere-Radius: "200" #特有
 Trace-Length: "100" #特有
```

### ■ TargetType_FrontalAttack
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "90" #特有
 Trace-Length: "400" #特有
```

### ■ TargetType_JumpSlam
```yaml
Default:
 Offset-from-Actor:
  x: "0"
 Sphere-Radius: "300" #特有
 Trace-Length: "0"
```

# ■ Abilities/Player/Skill の内容
## ■ Actor クラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| BP_Fireball | BP_AbilityProjectileBase | 火の玉 |
| BP_SlimBall | BP_AbilityProjectileBase | ヘドロ玉 |

**★詳細は後で調べる**

## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_PlayerSkillFireball | GA_SpawnProjectileBase | ★登録先の確認 |
| GA_PlayerSkillFireWave | GA_SkillBase | ★登録先の確認 |
| GA_PlayerSkillMeteor | GA_SkillBase | ★登録先の確認 |
| GA_PlayerSkillMeteorStorm | GA_SkillBase | ★登録先の確認 |

### ■ GA_PlayerSkillFireball
```yaml
Default:
 Montage-to-Play: "AM_Skill_Fireball"
 Projectile-Class: "BP_Fireball"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseSkill"
    Value:
     Target-Type: "None"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSkillFireball"
Tags:
 Ability-Tags: "Ability.Skill"
Costs:
 Cost-Gameplay-Effect-Class: "GE_PlayerSkillManaCost"
Cooldowns:
 Cooldown-Gameplay-Effect-Class: "GE_PlayerSkillCooldown"
```

### ■ GA_PlayerSkillFireWave

**Animation Montage の名前が FireWave じゃない。わかりにくい。**

```yaml
Default:
 Montage-to-Play: "AM_Skill_Firewave"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseSkill"
    Value:
     Target-Type: "TargetType_FireWave"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSkillFireWave"
Tags:
 Ability-Tags: "Ability.Skill"
Costs:
 Cost-Gameplay-Effect-Class: "GE_PlayerSkillManaCost"
Cooldowns:
 Cooldown-Gameplay-Effect-Class: "GE_PlayerSkillCooldown"
```

### ■ GA_PlayerSkillMeteor
```yaml
Default:
 Montage-to-Play: "AM_Skill_Combust"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseSkill"
    Value:
     Target-Type: "TargetType_Meteor"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSkillMeteor"
Tags:
 Ability-Tags: "Ability.Skill"
Costs:
 Cost-Gameplay-Effect-Class: "GE_PlayerSkillManaCost"
Cooldowns:
 Cooldown-Gameplay-Effect-Class: "GE_PlayerSkillCooldown"
```

### ■ GA_PlayerSkillMeteorStorm
```yaml
Default:
 Montage-to-Play: "AM_Skill_Meteor"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseSkill"
    Value:
     Target-Type: "TargetType_MeteorStorm"
     Target-Gameplay-Effect-Classes:
      - "GE_PlayerSkillMeteorStorm"
Tags:
 Ability-Tags: "Ability.Skill"
Costs:
 Cost-Gameplay-Effect-Class: "GE_PlayerSkillManaCost"
Cooldowns:
 Cooldown-Gameplay-Effect-Class: "GE_PlayerSkillCooldown"
```

## ■ アビリティエフェクトクラス
* 親クラス: **GE_RangeBase** 固定

| 名前 | 登録先 Ability | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| GE_PlayerSkillFireball | GA_PlayerSkillFireball | [Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillFireWave | GA_PlayerSkillFireWave | [Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillMeteor | GA_PlayerSkillMeteor | [Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillMeteorStorm | GA_PlayerSkillMeteorStorm | [Event.Montage.Player.Combo.ChestKick] |

| 名前 | 登録先 Ability | 登録先属性 |
| ----- | ----- | ----- |
| GE_PlayerSkillCooldown | GA_PlayerSkillFireball<br>GA_PlayerSkillFireWave<br>GA_PlayerSkillMeteor<br>GA_PlayerSkillMeteorStorm | Cooldown |
| GE_PlayerSkillManaCost | GA_PlayerSkillFireball<br>GA_PlayerSkillFireWave<br>GA_PlayerSkillMeteor<br>GA_PlayerSkillMeteorStorm | Cost |

### ■ GE_PlayerSkillFireball
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
         Raw: "1.5" #特有
         Curve-Table: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerSkillFireWave
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
         Raw: "1.0" #特有
         Curve-Table: "AttackDamage"
         Record: "HeavyAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerSkillMeteor
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
         Raw: "1.0" #特有
         Curve-Table: "AttackDamage"
         Record: "MediumAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerSkillMeteorStorm
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
         Raw: "1.0" #特有
         Curve-Table: "AttackDamage"
         Record: "HeavyAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

### ■ GE_PlayerSkillCooldown
```yaml
Gameplay-Effect:
 Duration-Policy: "Has Duration"
 Duration-Magnitude:
  Magnitude-Calculation-Type: "Scalabe Float"
  Scalable-Float-Magnitude:
   Raw: "2.0"
   Curve-Table: "None"
 Executions: #特有
Tags:
 GrantedTags:
  Combined-Tags: "Cooldown.skill"
  Added: "Cooldown.Skill"
```

### ■ GE_PlayerSkillManaCost
```yaml
Gameplay-Effect:
 Modifiers:
  - Attribute: "RPGAttributeSet.Mana"
    Modifier-Op: "Add"
    Modifier-Magnitude:
     Magmotide-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "-10.0"
      Curve-Table: "None"
    Source-Tags:
     Require-Tags: ""
     Ignore-Tags: ""
    Target-Tags:
     Require-Tags: ""
     Ignore-Tags: ""
 Executions: #特有
```

## ■ ターゲットタイプクラス
* 親クラス: **TargetType_SphereTrace** 固定

| 名前 | 登録先 Ability | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| TargetType_FireWave | GA_PlayerSkillFireWave | [Event.Montage.Shared.UseSkill] |
| TargetType_Meteor | GA_PlayerSkillMeteor | [Event.Montage.Shared.UseSkill] |
| TargetType_MeteorStorm | GA_PlayerSkillMeteorStorm | [Event.Montage.Shared.UseSkill] |

### ■ TargetType_FireWave
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "100" #特有
 Trace-Length: "600" #特有
```

### ■ TargetType_Meteor
```yaml
Default:
 Offset-from-Actor:
  x: "0"
 Sphere-Radius: "300" #特有
 Trace-Length: "0"
```

### ■ TargetType_MeteorStorm
```yaml
Default:
 Offset-from-Actor:
  x: "0"
 Sphere-Radius: "600" #特有
 Trace-Length: "0"
```


# ■ Abilities/Player/Potion の内容
## ■ アビリティクラス
| 名前 | 親クラス | 用途 |
| ----- | ----- | ----- |
| GA_DeathsDoor | GA_PotionBase | ★登録先の確認 |
| GA_PotionHealth | GA_PotionBase | ★登録先の確認 |
| GA_PotionMana | GA_PotionBase | ★登録先の確認 |

### ■ GA_DeathsDoor
```yaml
Default:
 Montage-to-Play: "AM_Item_Potion"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseItem"
    Value:
     Target-Type: "RPGTargetType_UseOwner" #特有
     Target-Gameplay-Effect-Classes:
      - "GE_DeathsDoor"
Tags:
 Ability-Tags: "Ability.Item"
```

### ■ GA_PotionHealth
```yaml
Default:
 Montage-to-Play: "AM_Item_Potion"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseItem"
    Value:
     Target-Type: "RPGTargetType_UseOwner" #特有
     Target-Gameplay-Effect-Classes:
      - "GE_PotionHealth"
Tags:
 Ability-Tags: "Ability.Item"
```

### ■ GA_PotionMana
```yaml
Default:
 Montage-to-Play: "AM_Item_Potion"
Gameplay-Effect:
 Effect-Container-Map:
  - Key: "Event.Montage.Shared.UseItem"
    Value:
     Target-Type: "RPGTargetType_UseOwner" #特有
     Target-Gameplay-Effect-Classes:
      - "GE_PotionMana"
Tags:
 Ability-Tags: "Ability.Item"
```


## ■ アビリティエフェクトクラス
* 親クラス: **GE_HealBase** 固定

| 名前 | 登録先 Ability | 登録先 EffectContainerMap のキー名 |
| ----- | ----- | ----- |
| GE_DeathsDoor | GA_DeathsDoor | [Event.Montage.Shared.UseItem] |
| GE_PotionHealth | GA_PotionHealth | [Event.Montage.Shared.UseItem] |
| GE_PotionMana | GA_PotionMana | [Event.Montage.Shared.UseItem] |

### ■ GE_DeathsDoor
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
  - Attribute: "RPGAttributeSet.Mana"
    Modifier-Op: "Add"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "2.0"
      Curve-Table: "AttackDamage"
      Record: "HeavyAttack"
```

### ■ GE_PotionHealth
```yaml
Gameplay-Effect:
 Modifiers:
  - Attribute: "RPGAttributeSet.Health"
    Modifier-Op: "Add"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "2.0"
      Curve-Table: "AttackDamage"
      Record: "HeavyAttack"
```

### ■ GE_PotionMana
```yaml
Gameplay-Effect:
 Modifiers:
  - Attribute: "RPGAttributeSet.Mana"
    Modifier-Op: "Add"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "0.18"
      Curve-Table: "AttackDamage"
      Record: "HeavyAttack"
```

----
以上。
