# ■ ClassList

**このファイルは書きかけです。**

## ■ このファイルについて
クラス階層について調査したものです。

# ■ Ability 関連で特徴的なこと
* Ability のネイティブ基底クラスは「 RPGGameplayAbility 」
* AbilityEffect のネイティブ基底クラスは「 GameplayEffect 」
* Target のネイティブ基底クラスは「 RPGTargetType 」


# ■ クラス継承ツリー
Blueprint のものは名前の後に ```[BP]``` と記す。

* **★とりあえず関係しそうなものは全部書き出したけど、実際関係ないものも混ざっているはず。**

## ■ Actor サブクラス
```
Actor
├─BP_AbilityProjectileBase[BP]
│ │APRG::スキルの発射物用基底 Actor
│ │
│ ├─BP_Fireball[BP]
│ │  APRG::スキル用の火の玉
│ │
│ └─BP_SlimBall[BP]
│    APRG::スキル用のヘドロの玉
│
├─BP_Pickup_Hambone
│  APRG::Pickup 用の骨付きハム
│
├─BP_SoulItem
│  APRG::敵を倒すと落とす、アイテム交換などに使う Soul
│
├─Controller
│ ├─AIController
│ │ │ AIModule::★以下、 Ability から話がそれるので割愛
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
│        ARPG::HUD との連携や入力制御等
│
├─GameplayAbilityTargetActor
│ │GameplayAbilities::★ ARPG ではこのツリー以下未使用と思われる
│ │
│ ├─GameplayAbilityTargetActor_Radius
│ └─GameplayAbilityTargetActor_Trace
│   ├─GameplayAbilityTargetActor_GoundTrace
│   │ └─GameplayAbilityTargetActor_ActorPlacement
│   └─GameplayAbilityTargetActor_SingleLineTrace
│
├─GameplayAbilityWorldReticle
│ │GameplayAbilities::★ ARPG ではこのツリー以下未使用と思われる
│ │
│ └─GameplayAbilityWorldReticle_ActorVisualization
│
├─GameplayCueNotify_Actor
│  GameplayAbilities::★ ARPG では未使用と思われる
│
├─HUD
│ └─AbilitySystemDebugHUD
│    GameplayAbilities::★ ARPG では未使用と思われる
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
│ │ │ARPG::★以下、プレイヤーと敵の Character クラス
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
│      GameplayAbilities::★ ARPG では未使用と思われる
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

## ■  ブクラス
```
ActorComponent
└─GameplayTaskComponent
  │GameplayTasks(エンジン内)::GameplayAbilities System のインターフェイスクラス。
  │おそらくエンジン内で AbilitySystem と強調できるように派生クラス AbilitySystemComponent から階層の抽出をされたクラスだと思われる。
  │ARPG で直接使われることはない。
  │
  └─AbilitySystemComponent
    │GameplayAbilities::GameplayAbilities System のインターフェイスクラス。
    │
    └─RPGAbilitySystemComponent
       ARPG::独自の拡張を行った AbilitySystemComponent の派生クラス。
       Ability をつかう Actor はこのコンポーネントを持たせている。（ RPGCharacterBase 等。（のみ？））
       Blueprint 向けのメンバーは置かれていない。（ UPROPERTY/UFUNCTION を持たない）
```

## ■ AnimInstance サブクラス
```
AnimInstance
│ARPG::★以下、プレイヤーと敵のアニメーションＢＰ
│
├─ABP_Player[BP]
├─ABP_SpiderBoss[BP]
└─ABP_AnimBP_Base[BP]
```

## ■ AnimNotify サブクラス
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

## ■ AnimNotifyState サブクラス
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

## ■ AssetManager サブクラス
```
AssetManager
└─RPGAssetManager
   ARPG::★アセットマネージャ
```

## ■ AttributeSet サブクラス
```
AttributeSet
│GameplayAbilities::ゲーム用属性定義基底クラス
│
├─AbilitySystemTestAttributeSet
│  GameplayAbilities::★ ARPG では未使用と思われる
│
└─RPGAttributeSet
   ARPG::独自の拡張を行った AttributeSet の派生クラス。
   Ability をつかう Actor はこのクラスを持たせている。（ RPGCharacterBase 等。（のみ？））
   派生クラスを複数持つことは AbilitySystem 上の制限は特にないが、 ARPG ではこのクラスしか存在しない。
```

## ■ TNode サブクラス
```
BTNode
│ARPG::★ AI 用。 Ability から話がそれるので割愛
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

## ■ CameraShake サブクラス
```
CameraShake
│ARPG::★カメラのシェイク用。 Ability から話がそれるので割愛
│
├─BP_Camerashake
├─camera_shake_skill
└─camera_shake_small
```

## ■ DataAsset サブクラス
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
    │  ARPG::★トークン用データクラス（ Soul のみ）
    └─RPGWeaponItem
       ARPG::★武器用データクラス
```

## ■ GameInstance サブクラス
```
GameInstance
└─RPGGameInstanceBase
  └─BP_GameInstance
     ARPG::★ゲームを通して使う変数とそれらを扱うロジックの定義
```

## ■ GameplayAbility サブクラス
```
GameplayAbility
├─GameplayAbility_CharacterJump
│  GameplayAbilities::★ ARPG では未使用と思われる
├─GameplayAbility_Montage
│  GameplayAbilities::★ ARPG では未使用と思われる
│
└─RPGGameplayAbility
  │ARPG::★ゲームで使用可能な Ability
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

## ■ GameplayCueNotify_Static サブクラス
```
GameplayCueNotify_Static
│GameplayAbilities::★ ARPG では未使用と思われる
└─GameplayCueNotify_HitImpact
   GameplayAbilities::★ ARPG では未使用と思われる
```

## ■ GameplayCueTranslator サブクラス
```
GameplayCueTranslator
│GameplayAbilities::★ ARPG では未使用と思われる
└─GameplayCueTranslator_Test
   GameplayAbilities::★ ARPG では未使用と思われる
```

## ■ GameplayDebuggerConfig サブクラス
```
GameplayDebuggerConfig
 GameplayAbilities::★ ARPG では未使用と思われる
```

## ■ GameplayDebuggerLocalController サブクラス
```
GameplayDebuggerLocalController
 GameplayAbilities::★ ARPG では未使用と思われる
```

## ■ GameplayEffect サブクラス
```
GameplayEffect
├─GameplayEffectTemplate
│  GameplayAbilities::★ ARPG では未使用と思われる
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
│   ├─GE_PlayerAxeGoundPound
│   ├─GE_PlayerFireAxeBurstPound
│   ├─GE_PlayerFireAxeGoundPound
│   ├─GE_PlayerHammerBurstPound
│   ├─GE_PlayerHammerGoundPound
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

## ■ GameplayEffectCalculation サブクラス
```
GameplayEffectCalculation
├─GameplayEffectExecutionCalculation
│ └─RPGDamageExecution
│  ARPG::★ダメージ計算処理
│
└─GameplayModMagnitudeCalculation
   GameplayAbilities::★ ARPG では拡張していないと思われる
```

## ■ GameplayEffectCreationMenu サブクラス
```
GameplayEffectCreationMenu
 GameplayAbilities::★ ARPG では拡張していないと思われる
```

## ■ GameplayEffectCreationApplicationRequirement サブクラス
```
GameplayEffectCreationApplicationRequirement
 GameplayAbilities::★ ARPG では拡張していないと思われる
```

## ■ GameplayEffectUIData サブクラス
```
GameplayEffectUIData
└─GameplayEffectUIData_TextOnly
   GameplayAbilities::★ ARPG では拡張していないと思われる
```

## ■ GameplayTagsDeveloperSettings サブクラス
```
GameplayTagsDeveloperSettings
 GameplayTags::★ ARPG では拡張していないと思われる
```
## ■ GameplayTagsList サブクラス
```
GameplayTagsList
└─GameplayTagsSetting
   GameplayTags::★ ARPG では拡張していないと思われる
```

## ■ GameplayTagsManager サブクラス
```
GameplayTagsManager
 GameplayTags::★ ARPG では拡張していないと思われる
```

## ■ GameplayTask サブクラス
```
GameplayTask
└─AbilityTask
  └─RPGAbilityTask_PlayMontageAndWaitForEvent
     ARPG::★ PlayMontageAndWait と WaitGameplayEvent の複合処理
```

## ■ GameplayTaskResource サブクラス
```
GameplayTaskResource
├─AIResource_Logic
└─AIResource_Movement
   GameplayTags::★ ARPG では拡張していないと思われる
```

## ■ RPGTargetType サブクラス
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
  ├─RPGTargetType_FAGoundPound[BP]
  ├─RPGTargetType_FireWave[BP]
  ├─RPGTargetType_FrontalAttack[BP]
  ├─RPGTargetType_GoundPound[BP]
  ├─RPGTargetType_HammerBurstPound[BP]
  ├─RPGTargetType_HammerGoundPound[BP]
  ├─RPGTargetType_JumpSlam[BP]
  ├─RPGTargetType_Metor[BP]
  └─RPGTargetType_MetroStorm[BP]
```

## ■ SaveGame サブクラス
```
SaveGame
└─RPGSaveGame
   ARPG::★特にコメントなし
```

----
以上。
