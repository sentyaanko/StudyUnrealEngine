# ■ ActionRPGReview

**このファイルは書きかけです。**

* **★EventGrapの内容確認は後でまとめて行う。**

## ■ このファイルは何？
 「Gameplay Abiliity System」のサンプルである「Action RPG（以降ARPG）」の実装内容について調査したものです。

# ■ クラス継承ツリー
Blueprintのものは名前の後に```[BP]```と記す。

* **★とりあえず関係しそうなものは全部書き出したけど、実際関係ないものも混ざっているはず。**
* **★後ほどコンテンツブラウザと突き合わせて内容を精査する。**

## ■ Actorサブクラス
```
Actor
├─BP_AbilityProjectileBase[BP]
│ │APRG::スキルの発射物用基底Actor
│ │
│ ├─BP_Fireball[BP]
│ │  APRG::スキル用の火の玉
│ │
│ └─BP_SlimBall[BP]
│    APRG::スキル用のヘドロの玉
│
├─BP_Pickup_Hambone
│  APRG::Pickup用の骨付きハム
│
├─BP_SoulItem
│  APRG::敵を倒すと落とす、アイテム交換などに使うSoul
│
├─Controller
│ ├─AIController
│ │ │ AIModule::★以下、Ability から話がそれるので割愛
│ │ │
│ │ ├─AIC_Boss[BP]
│ │ ├─AIC_NPC[BP]
│ │ │ └─AIC_NPC_Range[BP]
│ │ └─AIC_Player[BP]
│ │
│ └─PlayerController
│   └─RPGPlayerController
│     │  ARPG::インベントリ関係のアクセスがこのクラスから可能になっている。
│     │
│     └─BP_PlayerControllerBase[BP]
│        ARPG::HUDとの連携や入力制御等
│
├─GameplayAbilityTargetActor
│ │GameplayAbilities::★ARPGではこのツリー以下未使用と思われる
│ │
│ ├─GameplayAbilityTargetActor_Radius
│ └─GameplayAbilityTargetActor_Trace
│   ├─GameplayAbilityTargetActor_GroundTrace
│   │ └─GameplayAbilityTargetActor_ActorPlacement
│   └─GameplayAbilityTargetActor_SingleLineTrace
│
├─GameplayAbilityWorldReticle
│ │GameplayAbilities::★ARPGではこのツリー以下未使用と思われる
│ │
│ └─GameplayAbilityWorldReticle_ActorVisualization
│
├─GameplayCueNotify_Actor
│  GameplayAbilities::★ARPGでは未使用と思われる
│
├─HUD
│ └─AbilitySystemDebugHUD
│    GameplayAbilities::★ARPGでは未使用と思われる
│
├─Info
│ │─GameModeBase
│ │ └─RPGGameModeBase
│ │   │ARPG::★特にコメントなし
│ │   │
│ │   └─BP_GameModeBase[BP]
│ │      ARPG::ポーズやゲームオーバー、敵出現管理等のロジックが実装されている。
│ │
│ └─GameStateBase
│   └─RPGGameStateBase
│     └─BP_GameState
│        ARPG::★特に変更なし
│
├─NPC_SpawnBox
│  ARPG::敵の出現位置設定用
│
├─Pawn
│ ├─Character
│ │ │ARPG::★以下、プレイヤーと敵のCharacterクラス
│ │ │
│ │ └─RPGCharacterBase
│ │   └─BP_Character[BP]
│ │     ├─BP_EnemyCharacter[BP]
│ │     │ ├─NPC_GoblinBP[BP]
│ │     │ │ ├─NPC_GoblinBP_Level_01[BP]
│ │     │ │ ├─NPC_GoblinBP_Level_02[BP]
│ │     │ │ └─NPC_GoblinBP_Level_03[BP]
│ │     │ └─NPC_SpiderBoss[BP]
│ │     └─BP_PlayerCharacter[BP]
│ │
│ └─DefaultPawn
│   └─AbilitySystemTestPawn
│      GameplayAbilities::★ARPGでは未使用と思われる
└─WeaponActor
  │ARPG::★以下、プレイヤーと敵の武器クラス
  │
  ├─BladeActor
  ├─FireAxeActor
  ├─GoblinWeapon_Base
  │ ├─GoblinWeapon_Axe
  │ └─GoblinWeapon_Torch
  ├─GreateBladeActor
  ├─GuradianWeaponActor
  └─HammerActor
```

## ■ ActorComponentサブクラス
```
ActorComponent
└─GameplayTaskComponent
  │GameplayTasks(エンジン内)::GameplayAbilities System のインターフェイスクラス。
  │おそらくエンジン内で AbilitySystem と強調できるように派生クラス AbilitySystemComponent から階層の抽出をされたクラスだと思われる。
  │ARPGで直接使われることはない。
  │
  └─AbilitySystemComponent
    │GameplayAbilities::GameplayAbilities System のインターフェイスクラス。
    │
    └─RPGAbilitySystemComponent
       ARPG::独自の拡張を行った AbilitySystemComponent の派生クラス。
       Ability をつかうActor はこのコンポーネントを持たせている。（RPGCharacterBase等。（のみ？））
       Blueprint 向けのメンバーは置かれていない。（UPROPERTY/UFUNCTION を持たない）
```

## ■ AnimInstanceサブクラス
```
AnimInstance
│ARPG::★以下、プレイヤーと敵のアニメーションBP
│
├─ABP_Player[BP]
├─ABP_SpiderBoss[BP]
└─ABP_AnimBP_Base[BP]
```

## ■ AnimNotifyサブクラス
```
AnimNotify
│ARPG::★以下、アニメーション通知
│
├─AN_MaterialEffect[BP]
├─CameraShakeNotify[BP]
├─Death_Notify[BP]
├─Hit_Notify[BP]
├─SlomoNotify[BP]
└─UseItemNS[BP]
```

## ■ AnimNotifyStateサブクラス
```
AnimNotifyState
│ARPG::★以下、アニメーション通知ステート
│
├─AN_VisibilityEffect[BP]
├─BlockMoveInputNS[BP]
├─JumpSectionNS[BP]
├─MoveForwardNS[BP]
├─RangeAttackNS[BP]
├─ShieldNS[BP]
├─SlomoNS[BP]
├─StopAndStartAI_NS[BP]
└─WeaponAttackNS[BP]
```

## ■ AssetManagerサブクラス
```
AssetManager
└─RPGAssetManager
   ARPG::★アセットマネージャ
```

## ■ AttributeSetサブクラス
```
AttributeSet
│GameplayAbilities::ゲーム用属性定義基底クラス
│
├─AbilitySystemTestAttributeSet
│  GameplayAbilities::★ARPGでは未使用と思われる
│
└─RPGAttributeSet
   ARPG::独自の拡張を行った AttributeSet の派生クラス。
   Ability をつかうActor はこのクラスを持たせている。（RPGCharacterBase等。（のみ？））
   派生クラスを複数持つことは AbilitySystem 上の制限は特にないが、ARPGではこのクラスしか存在しない。
```

## ■ TNodeサブクラス
```
BTNode
│ARPG::★AI用。Ability から話がそれるので割愛
│
└─BTAuxiliaryNode
  ├─BTDecorator
  │ └─BTDecorator_BlueprintBase
  │   ├─BTDec_CheckHealth[BP]
  │   ├─BTDec_CheckItem[BP]
  │   ├─BTDec_IsAlive[BP]
  │   ├─BTTask_IsPlayingHighPriorityMontage[BP]
  │   └─BTTask_IsTargetSurrounded[BP]
  ├─BTService
  │ └─BTService_BlueprintBase
  │   ├─BTService_DistanceToTarget[BP]
  │   ├─BTService_FindNearestTarget[BP]
  │   └─BTService_RandomMoveSpeed[BP]
  └─BTTaskNode
    └─BTTask_BlueprintBase
      ├─BTTask_AttackMelee[BP]
      ├─BTTask_AttackSkill[BP]
      ├─BTTask_GoAroundTarget[BP]
      ├─BTTask_StopAndRotate[BP]
      ├─BTTask_StopAttack[BP]
      └─BTTask_UseItem[BP]
```

## ■ CameraShakeサブクラス
```
CameraShake
│ARPG::★カメラのシェイク用。Ability から話がそれるので割愛
│
├─BP_Camerashake
├─camera_shake_skill
└─camera_shake_small
```

## ■ DataAssetサブクラス
```
DataAsset
└─PrimaryDataAsset
  └─RPGItem
    │ARPG::★アイテム用データクラス
    ├─RPGPosionItem
    │  ARPG::★ポーション用データクラス
    ├─RPGSkillItem
    │  ARPG::★スキル用データクラス
    ├─RPGTokenItem
    │  ARPG::★トークン用データクラス（Soulのみ）
    └─RPGWeaponItem
       ARPG::★武器用データクラス
```

## ■ GameInstanceサブクラス
```
GameInstance
└─RPGGameInstanceBase
  └─BP_GameInstance
     ARPG::★ゲームを通して使う変数とそれらを扱うロジックの定義
```

## ■ GameplayAbilityサブクラス
```
GameplayAbility
├─GameplayAbility_CharacterJump
│  GameplayAbilities::★ARPGでは未使用と思われる
├─GameplayAbility_Montage
│  GameplayAbilities::★ARPGでは未使用と思われる
│
└─RPGGameplayAbility
  │ARPG::★ゲームで使用可能なAbility
  ├─GA_MeleeBase[BP]
  │ ├─GA_GoblinMelee[BP]
  │ ├─GA_PlayerAxeMelee[BP]
  │ ├─GA_PlayerFireAxeMelee[BP]
  │ ├─GA_PlayerHammerMelee[BP]
  │ └─GA_PlayerSwordMelee[BP]
  ├─GA_PotionBase[BP]
  │ ├─GA_DeathsDoor[BP]
  │ ├─GA_PotionHealth[BP]
  │ └─GA_PotionMana[BP]
  ├─GA_SkillBase[BP]
  │ ├─GA_PlayerSkillFireWave[BP]
  │ ├─GA_PlayerSkillMeteor[BP]
  │ ├─GA_PlayerSkillMeteorStorm[BP]
  │ └─GA_SpiderMelee[BP]
  └─GA_SpawnProjectileBase[BP]
    ├─GA_GoblinRange01[BP]
    └─GA_PlayerSkillFireBall[BP]
```

## ■ GameplayCueNotify_Staticサブクラス
```
GameplayCueNotify_Static
│GameplayAbilities::★ARPGでは未使用と思われる
└─GameplayCueNotify_HitImpact
   GameplayAbilities::★ARPGでは未使用と思われる
```

## ■ GameplayCueTranslatorサブクラス
```
GameplayCueTranslator
│GameplayAbilities::★ARPGでは未使用と思われる
└─GameplayCueTranslator_Test
   GameplayAbilities::★ARPGでは未使用と思われる
```

## ■ GameplayDebuggerConfigサブクラス
```
GameplayDebuggerConfig
 GameplayAbilities::★ARPGでは未使用と思われる
```

## ■ GameplayDebuggerLocalControllerサブクラス
```
GameplayDebuggerLocalController
 GameplayAbilities::★ARPGでは未使用と思われる
```

## ■ GameplayEffectサブクラス
```
GameplayEffect
├─GameplayEffectTemplate
│  GameplayAbilities::★ARPGでは未使用と思われる
│
│  ARPG::★以下はプレイヤーと敵のスキルエフェクト
├─GE_DamageBase
│ ├─GE_MeleeBase
│ │ ├─GE_GoblinMelee
│ │ ├─GE_GoblinRange
│ │ ├─GE_PlayerAxeMelee
│ │ ├─GE_PlayerFireAxeMelee
│ │ ├─GE_PlayerHammerMelee
│ │ └─GE_PlayerSwordMelee
│ └─GE_RangedBase
│   ├─GE_PlayerAxeBurstPound
│   ├─GE_PlayerAxeGroundPound
│   ├─GE_PlayerFireAxeBurstPound
│   ├─GE_PlayerFireAxeGroundPound
│   ├─GE_PlayerHammerBurstPound
│   ├─GE_PlayerHammerGroundPound
│   ├─GE_PlayerSkillCooldown
│   ├─GE_PlayerSkillFireball
│   ├─GE_PlayerFireWave
│   ├─GE_PlayerManaCost
│   ├─GE_PlayerMeteor
│   ├─GE_PlayerMeteorStorm
│   ├─GE_PlayerSwordChestKick
│   ├─GE_PlayerSwordFrontalAttack
│   └─GE_PlayerSwordJumpSlam
├─GE_DamageImmune
├─GE_HealBase
│ ├─GE_DeathsDoor
│ ├─GE_PotionHealth
│ └─GE_PotionMana
└─GE_StatsBase
  ├─GE_GoblinStats
  ├─GE_PlayerStats
  └─GE_SpiderStats
```

## ■ GameplayEffectCalculationサブクラス
```
GameplayEffectCalculation
├─GameplayEffectExecutionCalculation
│ └─RPGDamageExecution
│  ARPG::★ダメージ計算処理
│
└─GameplayModMagnitudeCalculation
   GameplayAbilities::★ARPGでは拡張していないと思われる
```

## ■ GameplayEffectCreationMenuサブクラス
```
GameplayEffectCreationMenu
 GameplayAbilities::★ARPGでは拡張していないと思われる
```

## ■ GameplayEffectCreationApplicationRequirementサブクラス
```
GameplayEffectCreationApplicationRequirement
 GameplayAbilities::★ARPGでは拡張していないと思われる
```

## ■ GameplayEffectUIDataサブクラス
```
GameplayEffectUIData
└─GameplayEffectUIData_TextOnly
   GameplayAbilities::★ARPGでは拡張していないと思われる
```

## ■ GameplayTagsDeveloperSettingsサブクラス
```
GameplayTagsDeveloperSettings
 GameplayTags::★ARPGでは拡張していないと思われる
```
## ■ GameplayTagsListサブクラス
```
GameplayTagsList
└─GameplayTagsSetting
   GameplayTags::★ARPGでは拡張していないと思われる
```

## ■ GameplayTagsManagerサブクラス
```
GameplayTagsManager
 GameplayTags::★ARPGでは拡張していないと思われる
```

## ■ GameplayTaskサブクラス
```
GameplayTask
└─AbilityTask
  └─RPGAbilityTask_PlayMontageAndWaitForEvent
     ARPG::★PlayMontageAndWait と WaitGameplayEvent の複合処理
```

## ■ GameplayTaskResourceサブクラス
```
GameplayTaskResource
├─AIResource_Logic
└─AIResource_Movement
   GameplayTags::★ARPGでは拡張していないと思われる
```

## ■ RPGTargetTypeサブクラス
```
RPGTargetType
│ARPG::★スキルのターゲット選択判定型
│
├─RPGTargetType_UseEventData
├─RPGTargetType_UseOwner
└─RPGTargetType_ShapeTrace[BP]
  ├─RPGTargetType_BurstPound[BP]
  ├─RPGTargetType_ChestKick[BP]
  ├─RPGTargetType_Claw[BP]
  ├─RPGTargetType_FABurstPound[BP]
  ├─RPGTargetType_FAGroundPound[BP]
  ├─RPGTargetType_FireWave[BP]
  ├─RPGTargetType_FrontalAttack[BP]
  ├─RPGTargetType_GroundPound[BP]
  ├─RPGTargetType_HammerBurstPound[BP]
  ├─RPGTargetType_HammerGroundPound[BP]
  ├─RPGTargetType_JumpSlam[BP]
  ├─RPGTargetType_Metor[BP]
  └─RPGTargetType_MetroStorm[BP]
```

## ■ SaveGameサブクラス
```
SaveGame
└─RPGSaveGame
   ARPG::★特にコメントなし
```

# ■ アセット一覧

## ■ Abilitiesフォルダ
```
Abilities
├─DataTables
│  アビリティ用のデータテーブル。詳細は後述の表参照
│
├─Enemies
│ │敵をカテゴリごとにフォルダ分けしたものを置くためのプレースホルダ
│ │
│ ├─Goblin
│ │  ゴブリン用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│ │
│ └─Spider
│    クモ用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│
├─Player
│ │武器後のにフォルダ分けしたものを置くためのプレースホルダ。
│ │スキルもフォルダしてある。
│ │パラメータ初期化のための GameplayEffect も置いてある
│ │
│ ├─Axe
│ │  Axe用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─FireAxe
│ │  FireAxe用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─Hammer
│ │  Hammer用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─Potions
│ │  ポーション用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─Skills
│ │  スキル用のアビリティ用BP(Actor/GameplayAbility/GameplayEffect)置き場
│ │
│ └─Sword
│    Sword用のアビリティ用BP(GameplayAbility/GameplayEffect)置き場
│
└─Shared
   ★プレイヤー、敵で共用のものを置くためのプレースホルダ？
```

### ■ Abilities/DataTables の内容
#### ■ パターン１（ダメージ計算用？）
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

#### ■ パターン２（キャラクターのレベルごとの初期ステータス用？）

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

### ■ Abilities/Enemies/Goblin の内容
#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_GoblinMelee | GA_MeleeBase | RPGGameplayAbility | ★登録先の確認 |
| GA_GoblinRange01 | GA_SpawnProjectileBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_GoblinMelee
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

■ GA_GoblinRange01
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_GoblinMelee | GE_MeleeBase | GameplayEffect | GA_GoblinMelee の EffectContainerMap[Event.Montage.Shared.WeaponHit] |
| GE_GoblinRange | GE_MeleeBase | GameplayEffect | GA_GoblinRange01 の Cooldown |
| GE_GoblinStats | GE_StatsBase | GameplayEffect | Spawn時のパラメータの初期化用。★呼び出し元確認 |

■ GE_GoblinMelee
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
         CurveTable: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "Status.DamageImmune"
```

■ GE_GoblinRange
```yaml
Gameplay-Effect:
 Duration-Policy: "Has Duration"
 Duration-Magnitude:
  Magnitude-Calculation-Type: "Scalable Float"
  Scalable-Float-Magnitude:
   Raw: "2"
   CurveTable: "None"
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
         CurveTable: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_GoblinStats
```yaml
Gameplay-Effect:
 Modifiers:
  - Attrivute: "RPGAttributeSet_MaxHealth"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultMaxHealth"
  - Attrivute: "RPGAttributeSet_MaxMana"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultMaxMana"
  - Attrivute: "RPGAttributeSet_AttackPower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultAttackPower"
  - Attrivute: "RPGAttributeSet_DefencePower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultDefencePower"
  - Attrivute: "RPGAttributeSet_MoveSpeed"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultMoveSpeed"
```

### ■ Abilities/Enemies/Spider の内容
#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_SpiderMelee | GA_SkillBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_SpiderMelee
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_SpiderStats | GE_StatsBase | GameplayEffect | Spawn時のパラメータの初期化用。★呼び出し元確認 |

■ GE_SpiderStats
```yaml
Gameplay-Effect:
 Modifiers:
  - Attrivute: "RPGAttributeSet_MaxHealth"
    Modifier-Op: "Multiply" #特有
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "3.0" #特有
      CurveTable: "StartingStats"
      Record: "DefaultMaxHealth"
  - Attrivute: "RPGAttributeSet_MaxMana"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0" 
      CurveTable: "StartingStats"
      Record: "DefaultMaxMana"
  - Attrivute: "RPGAttributeSet_AttackPower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "2.0" #特有
      CurveTable: "StartingStats"
      Record: "DefaultAttackPower"
  - Attrivute: "RPGAttributeSet_DefencePower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultDefencePower"
  - Attrivute: "RPGAttributeSet_MoveSpeed"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.5" #特有
      CurveTable: "StartingStats"
      Record: "DefaultMoveSpeed"
```

#### ■ ターゲットタイプクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_Claw | TargetType_SphereTrace | RPGTargetType | GA_SpiderMelee の EffectContainerMap[Event.Montage.Shared.UseSkill] |

■ TargetType_Claw
```yaml
Default:
 Offset-from-Actor:
  x: "400" #特有
 Sphere-Radius: "150" #特有
```

### ■ Abilities/Player の内容
#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_PlayerStats | GE_StatsBase | GameplayEffect | Spawn時のパラメータの初期化用。★呼び出し元確認 |


■ GE_GoblinStats
```yaml
Gameplay-Effect:
 Modifiers:
  - Attrivute: "RPGAttributeSet_MaxHealth"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "PlayerMaxHealth" #毒湧
  - Attrivute: "RPGAttributeSet_MaxMana"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "PlayerMaxMana" #毒湧
  - Attrivute: "RPGAttributeSet_AttackPower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "PlayerAttackPower" #毒湧
  - Attrivute: "RPGAttributeSet_DefencePower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "PlayerDefencePower" #毒湧
  - Attrivute: "RPGAttributeSet_MoveSpeed"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "PlayerMoveSpeed" #毒湧
```

### ■ Abilities/Player/Axe の内容
#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_PlayerAxeMelee | GA_MeleeBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_PlayerAxeMelee
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_PlayerAxeBurstPound | GE_RangeBase | GameplayEffect | GA_PlayerAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.BurstPound] |
| GE_PlayerAxeGroundPound | GE_RangeBase | GameplayEffect | GA_PlayerAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.GroundPound] |
| GE_PlayerAxeMelee | GE_MeleeBase | GameplayEffect | GA_PlayerAxeMelee の EffectContainerMap[Event.Montage.Shared.WeaponHit] |

■ GE_PlayerAxeBurstPound
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
         CurveTable: "AttackDamage"
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerAxeMelee
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
         CurveTable: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "Status.DamageImmune"
```


#### ■ ターゲットタイプクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_BurstPound | TargetType_SphereTrace | RPGTargetType | GA_PlayerAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.BurstPound] |
| TargetType_GroundPound | TargetType_SphereTrace | RPGTargetType | GA_PlayerAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.GroundPound] |

**※他と異なり、「TargetType_」の後に武器の名前が入っておらず、わかりづらい。**

■ TargetType_BurstPound
```yaml
Default:
 Trace-Length: "300" #特有
```

■ TargetType_GroundPound
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Trace-Length: "600" #特有
```

### ■ Abilities/Player/FireAxe の内容
つくりはほぼ Axe と一緒。

#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_PlayerFireAxeMelee | GA_MeleeBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_PlayerFireAxeMelee
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_PlayerFireAxeBurstPound | GE_RangeBase | GameplayEffect | GA_PlayerFireAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.BurstPound] |
| GE_PlayerFireAxeGroundPound | GE_RangeBase | GameplayEffect | GA_PlayerFireAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.GroundPound] |
| GE_PlayerFireAxeMelee | GE_MeleeBase | GameplayEffect | GA_PlayerFireAxeMelee の EffectContainerMap[Event.Montage.Shared.WeaponHit] |


■ GE_PlayerFireAxeBurstPound
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
         CurveTable: "AttackDamage_Fire" #特有
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerFireAxeMelee
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
         CurveTable: "AttackDamage_Fire" #特有
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

#### ■ ターゲットタイプクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_FABurstPound | TargetType_SphereTrace | RPGTargetType | GA_PlayerFireAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.BurstPound] |
| TargetType_FAGroundPound | TargetType_SphereTrace | RPGTargetType | GA_PlayerFireAxeMelee の EffectContainerMap[Event.Montage.Player.Combo.GroundPound] |

**FA は FireAxe の略らしいが、この略語を使っているのはここが初めて。わかりにくい。**

■ TargetType_FABurstPound
```yaml
Default:
 Sphere-Radius: "120" #特有
 Trace-Length: "300" #特有
```

■ TargetType_FAGroundPound
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "120" #特有
 Trace-Length: "600" #特有
```

### ■ Abilities/Player/Hammer の内容
#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_PlayerHammerMelee | GA_MeleeBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_PlayerHammerMelee
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_PlayerHammerBurstPound | GE_RangeBase | GameplayEffect | GA_PlayerHammerMelee の EffectContainerMap[Event.Montage.Player.Combo.BurstPound] |
| GE_PlayerHammerGroundPound | GE_RangeBase | GameplayEffect | GA_PlayerHammerMelee の EffectContainerMap[Event.Montage.Player.Combo.GroundPound] |
| GE_PlayerHammerMelee | GE_MeleeBase | GameplayEffect | GA_PlayerHammerMelee の EffectContainerMap[Event.Montage.Shared.WeaponHit] |


■ GE_PlayerHammerBurstPound
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
         CurveTable: "AttackDamage_Hammer" #特有
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerHammerMelee
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
         CurveTable: "AttackDamage_Hammer" #特有
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

#### ■ ターゲットタイプクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_HammerBurstPound | TargetType_SphereTrace | RPGTargetType | GA_PlayerHammerMelee の EffectContainerMap[Event.Montage.Player.Combo.BurstPound] |
| TargetType_HammerGroundPound | TargetType_SphereTrace | RPGTargetType | GA_PlayerHammerMelee の EffectContainerMap[Event.Montage.Player.Combo.GroundPound] |

■ TargetType_HammerBurstPound
```yaml
Default:
 Sphere-Radius: "120" #特有
 Trace-Length: "300" #特有
```

■ TargetType_HammerGroundPound
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "150" #特有
 Trace-Length: "600" #特有
```


### ■ Abilities/Player/Sword の内容
#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_PlayerSwordMelee | GA_MeleeBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_PlayerSwordMelee
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_PlayerSwordChestKick | GE_RangeBase | GameplayEffect | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSwordFrontalAttack | GE_RangeBase | GameplayEffect | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Player.Combo.FrontalAttack] |
| GE_PlayerSwordJumpSlam | GE_RangeBase | GameplayEffect | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Player.Combo.JumpSlam] |
| GE_PlayerSwordMelee | GE_MeleeBase | GameplayEffect | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Shared.WeaponHit] |

■ GE_PlayerSwordChestKick
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
         CurveTable: "AttackDamage_Sword" #特有
         Record: "HeavyAttack" #特有
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerSwordMelee
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
         CurveTable: "AttackDamage_Sword" #特有
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```


#### ■ ターゲットタイプクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_ChestKick | TargetType_SphereTrace | RPGTargetType | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Player.Combo.ChestKick] |
| TargetType_FrontalAttack | TargetType_SphereTrace | RPGTargetType | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Player.Combo.FrontalAttack] |
| TargetType_JumpSlam | TargetType_SphereTrace | RPGTargetType | GA_PlayerSwordMelee の EffectContainerMap[Event.Montage.Player.Combo.JumpSlam] |

**※他と異なり、「TargetType_」の後に武器の名前が入っておらず、わかりづらい。**

■ TargetType_ChestKick
```yaml
Default:
 Offset-from-Actor:
  x: "150" #特有
 Sphere-Radius: "200" #特有
 Trace-Length: "100" #特有
```

■ TargetType_FrontalAttack
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "90" #特有
 Trace-Length: "400" #特有
```

■ TargetType_JumpSlam
```yaml
Default:
 Offset-from-Actor:
  x: "0"
 Sphere-Radius: "300" #特有
 Trace-Length: "0"
```

### ■ Abilities/Player/Skill の内容
#### ■ Actorクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| BP_Fireball | BP_AbilityProjectileBase | Actor | 火の玉 |
| BP_SlimBall | BP_AbilityProjectileBase | Actor | ヘドロ玉 |

**★詳細は後で調べる**

#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_PlayerSkillFireball | GA_SpawnProjectileBase | RPGGameplayAbility | ★登録先の確認 |
| GA_PlayerSkillFireWave | GA_SkillBase | RPGGameplayAbility | ★登録先の確認 |
| GA_PlayerSkillMeteor | GA_SkillBase | RPGGameplayAbility | ★登録先の確認 |
| GA_PlayerSkillMeteorStorm | GA_SkillBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_PlayerSkillFireball
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

■ GA_PlayerSkillFireWave

**Animation Montageの名前がFireWaveじゃない。わかりにくい。**

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

■ GA_PlayerSkillMeteor
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

■ GA_PlayerSkillMeteorStorm
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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_PlayerSkillFireball | GE_RangeBase | GameplayEffect | GA_PlayerSkillFireball の EffectContainerMap[Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillFireWave | GE_RangeBase | GameplayEffect | GA_PlayerSkillFireWave の EffectContainerMap[Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillMeteor | GE_RangeBase | GameplayEffect | GA_PlayerSkillMeteor の EffectContainerMap[Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillMeteorStorm | GE_RangeBase | GameplayEffect | GA_PlayerSkillMeteorStorm の EffectContainerMap[Event.Montage.Player.Combo.ChestKick] |
| GE_PlayerSkillCooldown | GE_RangeBase | GameplayEffect | GA_PlayerSkillFireball/GA_PlayerSkillFireWave/GA_PlayerSkillMeteor/GA_PlayerSkillMeteorStorm の Cooldown |
| GE_PlayerSkillManaCost | GE_RangeBase | GameplayEffect | GA_PlayerSkillFireball/GA_PlayerSkillFireWave/GA_PlayerSkillMeteor/GA_PlayerSkillMeteorStorm の Cost |

■ GE_PlayerSkillFireball
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
         CurveTable: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerSkillFireWave
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
         CurveTable: "AttackDamage"
         Record: "HeavyAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerSkillMeteor
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
         CurveTable: "AttackDamage"
         Record: "MediumAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerSkillMeteorStorm
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
         CurveTable: "AttackDamage"
         Record: "HeavyAttack"
       Target-Tags:
        Ignore-Tags: "" #特有
```

■ GE_PlayerSkillCooldown
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

■ GE_PlayerSkillManaCost
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

#### ■ ターゲットタイプクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_FireWave | TargetType_SphereTrace | RPGTargetType | GA_PlayerSkillFireWave の EffectContainerMap[Event.Montage.Shared.UseSkill] |
| TargetType_Meteor | TargetType_SphereTrace | RPGTargetType | GA_PlayerSkillMeteor の EffectContainerMap[Event.Montage.Shared.UseSkill] |
| TargetType_MeteorStorm | TargetType_SphereTrace | RPGTargetType | GA_PlayerSkillMeteorStorm の EffectContainerMap[Event.Montage.Shared.UseSkill] |

■ TargetType_FireWave
```yaml
Default:
 Offset-from-Actor:
  x: "200" #特有
 Sphere-Radius: "100" #特有
 Trace-Length: "600" #特有
```

■ TargetType_Meteor
```yaml
Default:
 Offset-from-Actor:
  x: "0"
 Sphere-Radius: "300" #特有
 Trace-Length: "0"
```

■ TargetType_MeteorStorm
```yaml
Default:
 Offset-from-Actor:
  x: "0"
 Sphere-Radius: "600" #特有
 Trace-Length: "0"
```


### ■ Abilities/Player/Potion の内容
#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_DeathsDoor | GA_PotionBase | RPGGameplayAbility | ★登録先の確認 |
| GA_PotionHealth | GA_PotionBase | RPGGameplayAbility | ★登録先の確認 |
| GA_PotionMana | GA_PotionBase | RPGGameplayAbility | ★登録先の確認 |

■ GA_DeathsDoor
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

■ GA_PotionHealth
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

■ GA_PotionMana
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


#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_DeathsDoor | GE_HealBase | GameplayEffect | GA_DeathsDoor の EffectContainerMap[Event.Montage.Shared.UseItem] |
| GE_PotionHealth | GE_HealBase | GameplayEffect | GA_PotionHealth の EffectContainerMap[Event.Montage.Shared.UseItem] |
| GE_PotionMana | GE_HealBase | GameplayEffect | GA_PotionMana の EffectContainerMap[Event.Montage.Shared.UseItem] |

■ GE_DeathsDoor
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

■ GE_PotionHealth
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

■ GE_PotionMana
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

### ■ Abilities/Shared の内容

#### ■ Actorクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| BP_AbilityProjectileBase | Actor | Actor | 発射物の基底 |

**★EventGrapの内容確認**

#### ■ アビリティクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GA_MeleeBase | RPGGameplayAbility | RPGGameplayAbility | 近接攻撃の基底|
| GA_PotionBase | RPGGameplayAbility | RPGGameplayAbility | ポーションの基底 |
| GA_SkillBase | RPGGameplayAbility | RPGGameplayAbility | スキルの基底 |
| GA_SpawnProjectileBase | RPGGameplayAbility | RPGGameplayAbility | 発射物をSpawnさせる基底 |

**★EventGrapの内容確認**

■ GA_MeleeBase
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

■ GA_PotionBase
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

■ GA_SkillBase
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

■ GA_SpawnProjectileBase

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

#### ■ アビリティエフェクトクラス
| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| GE_DamageBase | GameplayEffect | GameplayEffect |  |
| GE_DamageImmune | GameplayEffect | GameplayEffect |  |
| GE_HealBase | GameplayEffect | GameplayEffect |  |
| GE_MeleeBase | GE_DamageBase | GameplayEffect |  |
| GE_RangedBase | GE_DamageBase | GameplayEffect |  |
| GE_StatsBase | GameplayEffect | GameplayEffect |  |

■ GE_DamageBase

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
         CurveTable: "AttackDamage"
         Record: "DefaultAttack"
       Target-Tags:
        Ignore-Tags: "Status.DamageImmune"
```

■ GE_DamageImmune
```yaml
Tags:
 GrantedTags:
  Combined-Tags: "Status.DamageImmune"
  Added: "Status.DamageImmune"
```

■ GE_HealBase
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

■ GE_StatsBase
```yaml
Gameplay-Effect:
 Modifiers:
  - Attrivute: "RPGAttributeSet_MaxHealth"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultMaxHealth"
  - Attrivute: "RPGAttributeSet_MaxMana"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultMaxMana"
  - Attrivute: "RPGAttributeSet_AttackPower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultAttackPower"
  - Attrivute: "RPGAttributeSet_DefencePower"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultDefencePower"
  - Attrivute: "RPGAttributeSet_MoveSpeed"
    Modifier-Op: "Override"
    Modifier-Magnitude:
     Magnitude-Calculation-Type: "Scalable Float"
     Scalable-Float-Magnitude:
      Raw: "1.0"
      CurveTable: "StartingStats"
      Record: "DefaultMoveSpeed"
```

#### ■ ターゲットタイプクラス

| 名前 | 親クラス | ネイティブ親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| TargetType_SphereTrace | RPGTargetType | RPGTargetType | SphereTraceをするターゲット選択基底 |

**★EventGrapの内容確認**


----
以上。
