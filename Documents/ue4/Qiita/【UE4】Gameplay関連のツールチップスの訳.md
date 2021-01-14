
# UGameplayEffect

カテゴリ別

## GameplayEffect
* 説明
	* GameplayEffect
	* ゲームプレイ効果

### DurationPolicy
* 型
	* [EGameplayEffectDurationType]
* 説明
	* Policy for the duration of this effect
	* この効果の持続期間のポリシー

### DurationMagnitude
* 条件
	* DurationPolicy が HasDuration の時のみ有効
* 型
	* [FGameplayEffectModifierMagnitude]
* 説明
	* Duration in seconds. 0.0 for instantaneous effects; -1.0 for infinite duration.
	* 秒単位の期間。 瞬間効果の場合は 0.0。 無限の期間の場合は-1.0。

### Modifiers
* 型
	* [FGameplayModifierInfo]
* 説明
	* Array of modifiers that will affect the target of this effect
	* この効果の対象に影響を与える修飾子の配列

### Executions
* 型
	* [FGameplayEffectExecutionDefinition]
* 説明
	* 無し

### ConditionalGameplayEffects
* 型
	* TArray<[FConditionalGameplayEffect]>
* 説明
	* other gameplay effects that will be applied to the target of this effect if this effect applies
	* 

## Period
* 説明
	* Period
	* 期間

### Period
* 型
	* FScalableFloat
* 説明
	* Period in seconds. 0.0 for non-periodic effects
	* 秒単位の期間。 非周期的効果の場合は0.0

### bExecutePeriodicEffectOnApplication
* 型
	* bool
* 説明
	* If true, the effect executes on application and then at every period interval. If false, no execution occurs until the first period elapses.
	* trueの場合、エフェクトはアプリケーションで実行され、その後、すべての期間間隔で実行されます。 falseの場合、最初の期間が経過するまで実行は行われません。

### PeriodicInhibitionPolicy
* 型
	* [EGameplayEffectPeriodInhibitionRemovedPolicy]
* 説明
	* なし

## Application
* 説明
	* Application
	* 応用

### ChanceToApplyToTarget
* 型
	* FScalableFloat
* 説明
	* Probability that this gameplay effect will be applied to the target actor (0.0 for never, 1.0 for always)
	* このゲームプレイ効果がターゲットアクターに適用される確率（0.0で非適用、1.0で常に適用）

### Application Requirement(ApplicationRequirements)
* 型
	* TArray<TSubclassOf<[UGameplayEffectCustomApplicationRequirement]>>
* 説明
	* なし

## Overflow
* 説明
	* Overflow
	* オーバーフロー

### OverflowEffects
* 型
	* TArray<TSubclassOf<[UGameplayEffect]>>
* 説明
	* Effects to apply when a stacking effect "overflows" its stack count through another attempted application. 
	Added whether the overflow application succeeds or not.
	* スタック効果が別の試行されたアプリケーションを介してスタックカウントを「オーバーフロー」したときに適用される効果。 
	オーバーフローアプリケーションが成功するかどうかを追加しました。（？オーバーフローアプリケーションの成否によらず追加されます。？）

### bDenyOverflowApplication
* 型
	bool
* 説明
	* If true, stacking attempts made while at the stack count will fail, resulting in the duration and context not being refreshed
	* trueの場合、スタックカウント中に行われたスタックの試行は失敗し、その結果、期間とコンテキストが更新されません。

### bClearStackOnOverflow
* 型
	bool
* 説明
	* If true, the entire stack of the effect will be cleared once it overflows
	* trueの場合、エフェクトのスタック全体がオーバーフローするとクリアされます

## Expiration
* 説明
	* Expiration
	* 有効期限

### PrematureExpirationEffectClasses
* 型
	TArray<TSubclassOf<[UGameplayEffect]>>
* 説明
	* Effects to apply when this effect is made to expire prematurely (like via a forced removal, clear tags, etc.); Only works for effects with a duration
	* この効果が時期尚早に期限切れになったときに適用される効果（強制的な削除、タグのクリアなど）。 持続時間のあるエフェクトでのみ機能します

### RoutineExpirationEffectClasses
* 型
	TArray<TSubclassOf<[UGameplayEffect]>>
* 説明
	* Effects to apply when this effect expires naturally via its duration; Only works for effects with a duration
	* この効果がその持続時間によって自然に期限切れになったときに適用される効果。 持続時間のあるエフェクトでのみ機能します


## Display
* 説明
	* Display
	* 表示

### bRequireModifierSuccessToTriggerCues
* 型
	bool
* 説明
	* If true, cues will only trigger when GE modifiers succeed being applied (whether through modifiers or executions)
	* trueの場合、キューは、GE(GameplayEffect)修飾子の適用が成功した場合にのみトリガーされます（修飾子または実行のいずれかを介して）

### bSuppressStackingCues
* 型
	bool
* 説明
	* If true, GameplayCues will only be triggered for the first instance in a stacking GameplayEffect.
	* trueの場合、GameplayCuesは、スタッキングGameplayEffectの最初のインスタンスに対してのみトリガーされます。

### GameplayCues
* 型
	TArray<[FGameplayEffectCue]>
* 説明
	* Cues to trigger non-simulated reactions in response to this GameplayEffect such as sounds, particle effects, etc
	* サウンド、パーティクルエフェクトなど、このGameplayEffectに応答してシミュレートされていない反応をトリガーするキュー

### UIData
* 型
	* class UGameplayEffectUIData*
* 説明
	* Data for the UI representation of this effect. This should include things like text, icons, etc. Not available in server-only builds.
	* この効果のUI表現のデータ。 これには、テキストやアイコンなどを含める必要があります。サーバーのみのビルドでは使用できません。

## Tags
* 説明
	* Tag Containers
	* タグコンテナ
	
### GameplayEffectAssetTag(InheritableGameplayEffectTags)
* 型
	* [FInheritedTagContainer]
* 説明
	* The GameplayEffect's Tags: tags the the GE "has" and DOES NOT give to the actor.
	* GameplayEffectのタグ：GEが「持っている」タグであり、アクターには与えません。

### GrantedTags(InheritableOwnedTagsContainer)
* 型
	* [FInheritedTagContainer]
* 説明
	* These tags are applied to the actor I am applied to
	* これらのタグは、私が適用されているアクターに適用されます
	
### OngoingTagRequirements
* 型
	* [FGameplayTagRequirements]
* 説明
	* Once Applied, these tags requirements are used to determined if the GameplayEffect is "on" or "off". A GameplayEffect can be off and do nothing, but still applied.
	* 適用されると、これらのタグ要件は、GameplayEffectが「オン」か「オフ」かを判断するために使用されます。 GameplayEffectはオフにして何もしないことができますが、それでも適用されます。

### ApplicationTagRequirements
* 型
	* [FGameplayTagRequirements]
* 説明
	* Tag requirements for this GameplayEffect to be applied to a target. This is pass/fail at the time of application. If fail, this GE fails to apply.
	* このGameplayEffectをターゲットに適用するためのタグ要件。 申請時の合格/不合格です。 失敗した場合、このGE(GameplayEffect)は適用に失敗します。

### RemovalTagRequirements
* 型
	* [FGameplayTagRequirements]
* 説明
	* Tag requirements that if met will remove this effect. Also prevents effect application.
	* 満たされた場合にこの影響を取り除くタグ要件。 また、エフェクトの適用を防ぎます。

### RemoveGameplayEffectsWithTags
* 型
	* [FInheritedTagContainer]
* 説明
	* GameplayEffects that "have" tags in this container will be cleared upon effect application.
	* このコンテナに「ある」タグがあるGameplayEffectsは、エフェクトの適用時にクリアされます。

### RemoveGameplayEffectQuery
* 型
	* [FGameplayEffectQuery]
* 説明
	* On Application of an effect, any active effects with this this query that matches against the added effect will be removed. Queries are more powerful but slightly slower than RemoveGameplayEffectsWithTags.
	* エフェクトの適用時に、このクエリで追加されたエフェクトと一致するアクティブなエフェクトはすべて削除されます。 クエリは、RemoveGameplayEffectsWithTagsよりも強力ですが、少し遅くなります。

## Immunity
### GrantedApplicationImmunityTags(GrantedApplicationImmunityTags)
* 型
	* [FGameplayTagRequirements]
* 説明
	* Grants the owner immunity from these source tags.
	* これらのソースタグからの耐性を所有者に付与します。

### GrantedApplicationImmunityQuery
* 型
	* [FGameplayEffectQuery]
* 説明
	* Grants immunity to GameplayEffects that match this query. Queries are more powerful but slightly slower than GrantedApplicationImmunityTags.
	* このクエリに一致するGameplayEffectsに耐性を付与します。 クエリはGrantedApplicationImmunityTagsよりも強力ですが、少し遅くなります。

## Stacking
* 説明
	* Stacking
	* スタッキング

### StackingType
* 型
	* [EGameplayEffectStackingType]
* 説明
	* How this GameplayEffect stacks with other instances of this same GameplayEffect
	* このGameplayEffectがこの同じGameplayEffectの他のインスタンスとどのようにスタックするか

### StackLimitCount
* 型
	* int32
* 説明
	* Stack limit for StackingType
	* StackingTypeのスタック制限数

### StackDurationRefreshPolicy
* 型
	* [EGameplayEffectStackingDurationPolicy]
* 説明
	* Policy for how the effect duration should be refreshed while stacking
	* スタック中に効果の持続時間を更新する方法に関するポリシー

### StackPeriodResetPolicy
* 型
	* [EGameplayEffectStackingPeriodPolicy]
* 説明
	* Policy for how the effect period should be reset (or not) while stacking
	* スタッキング中に効果期間をリセットする（またはリセットしない）方法に関するポリシー

### StackExpirationPolicy
* 型
	* [EGameplayEffectStackingExpirationPolicy]
* 説明
	* Policy for how to handle duration expiring on this gameplay effect
	* このゲームプレイ効果で期限切れになる期間を処理する方法に関するポリシー

## Granted Abilities
* 説明
	* Granted abilities
	* 付与される能力
	
### GrantedAbilities
* 型
	* TArray<[FGameplayAbilitySpecDef]>
* 説明
	* なし

----
# EGameplayEffectDurationType
* 説明
	* Gameplay effect duration policies
	* ゲームプレイ効果の継続時間ポリシー
* 値
	* Instant
		* This effect applies instantly
		* この効果は即座に適用されます
	* Infinite
		* This effect lasts forever
		* この効果は永遠に続きます
	* HasDuration
		* The duration of this effect will be specified by a magnitude
		* この効果の持続時間は大きさによって指定されます

# FGameplayEffectModifierMagnitude
* 説明
	* Struct representing the magnitude of a gameplay effect modifier, potentially calculated in numerous different ways
	* ゲームプレイ効果修飾子の大きさを表す構造体。さまざまな方法で計算される可能性があります。

### MagnitudeCalculationType
* 型
	* [EGameplayEffectMagnitudeCalculation]
* 説明
	* Type of calculation to perform to derive the magnitude
	* 大きさを導出するために実行する計算のタイプ

### ScalableFloatMagnitude
* 条件
	* MagnitudeCalculationType が ScalableFloat の時のみ有効
* 説明
	* Magnitude value represented by a scalable float
	* スケーラブルなフロートで表される大きさの値

### AttributeBasedMagnitude
* 条件
	* MagnitudeCalculationType が AttributeBased の時のみ有効
* 型
	* [FAttributeBasedFloat]
* 説明
	* Magnitude value represented by an attribute-based float
	(Coefficient * (PreMultiplyAdditiveValue + [Eval'd Attribute Value According to Policy])) + PostMultiplyAdditiveValue
	* 属性ベースの浮動小数点数で表される大きさの値
	（係数 *（PreMultiplyAdditiveValue + [ポリシーに従って評価された属性値]））+ PostMultiplyAdditiveValue

### CustomMagnitude
* 条件
	* MagnitudeCalculationType が CustomCalculationClass の時のみ有効
* 型
	* [FCustomCalculationBasedFloat]
* 説明
	* Magnitude value represented by a custom calculation class
	* カスタム計算クラスで表される大きさの値

### SetByCallerMagnitude
* 条件
	* MagnitudeCalculationType が SetByCaller の時のみ有効
* 型
	* [FSetByCallerFloat]
* 説明
	* Magnitude value represented by a SetByCaller magnitude
	* SetByCaller の大きさによって表される大きさの値

# EGameplayEffectMagnitudeCalculation
* 説明
	* Enumeration outlining the possible gameplay effect magnitude calculation policies.
	* 可能なゲームプレイ効果の大きさの計算ポリシーの概要を示す列挙。
* 値
	* ScalableFloat
		* Use a simple, scalable float for the calculation.
		* 計算には、シンプルでスケーラブルなフロートを使用します。
	* AttributeBased
		* Perform a calculation based upon an attribute.
		* 属性に基づいて計算を実行します。
	* CustomCalculationClass
		* Perform a custom calculation, capable of capturing and acting on multiple attributes, in either BP or native.
		* BP またはネイティブのいずれかで、複数の属性をキャプチャして操作できるカスタム計算を実行します。
	* SetByCaller
		* This magnitude will be set explicitly by the code/blueprint that creates the spec.
		* この大きさは、仕様を作成するコード/ブループリントによって明示的に設定されます。


# FGameplayEffectAttributeCaptureDefinition
* 説明
	* Struct defining gameplay attribute capture options for gameplay effects
	* ゲームプレイ効果のゲームプレイ属性キャプチャオプションを定義する構造体

### AttributeToCapture
* 説明
	* Gameplay attribute to capture
	* キャプチャするゲームプレイ属性

### AttributeSource
* 型
	* [EGameplayEffectAttributeCaptureSource]
* 説明
	* Source of the gameplay attribute
	* ゲームプレイ属性のソース

### bSnapshot
* 説明
	* Whether the attribute should be snapshotted or not
	* 属性をスナップショットする必要があるかどうか

# EGameplayEffectAttributeCaptureSource
* 説明
	* Enumeration for options of where to capture gameplay attributes from for gameplay effects.
	* ゲームプレイ効果のためにゲームプレイ属性をキャプチャする場所のオプションの列挙。
* 値
	* Source
		* Source (caster) of the gameplay effect.
		* ゲームプレイ効果のソース（キャスター）。
	* Target	
		* Target (recipient) of the gameplay effect.
		* ゲームプレイ効果のターゲット（受信者）。


# EAttributeBasedFloatCalculationType
* 説明
	* Enumeration outlining the possible attribute based float calculation policies.
	* 可能な属性ベースのフロート計算ポリシーの概要を示す列挙。
* 値
	* AttributeMagnitude
		* Use the final evaluated magnitude of the attribute.
		* 属性の最終的に評価された大きさを使用します。
	* AttributeBaseValue
		* Use the base value of the attribute.
		* 属性の基本値を使用します。
	* AttributeBonusMagnitude
		* Use the "bonus" evaluated magnitude of the attribute: Equivalent to (FinalMag - BaseValue).
		* 属性の「ボーナス」評価された大きさを使用します：（FinalMag-BaseValue）と同等です。
	* AttributeMagnitudeEvaluatedUpToChannel
		* Use a calculated magnitude stopping with the evaluation of the specified "Final Channel"
		* 指定された「最終チャネル」の評価で停止する計算された大きさを使用します
		* 条件
			* ```AbilitySystemGlobalsCDO::ShouldAllowGameplayModEvaluationChannels()``` が true を返さない場合は表示されない

# FGameplayTagContainer
* 説明
	* A Tag Container holds a collection of FGameplayTags, tags are included explicitly by adding them, and implicitly from adding child tags
	* タグコンテナはFGameplayTagのコレクションを保持し、タグはそれらを追加することによって明示的に含まれ、子タグの追加から暗黙的に含まれます

# UGameplayModMagnitudeCalculation
* 説明
	* Class used to perform custom gameplay effect modifier calculations, either via blueprint or native code
	* ブループリントまたはネイティブコードを介して、カスタムゲームプレイ効果修飾子の計算を実行するために使用されるクラス

# FGameplayModifierInfo
* 説明
	* Tells us "Who/What we" modify. Does not tell us how exactly.
	* 「誰が/何を」変更するかを教えてくれます。具体的には教えてくれません。

### Attribute
* 型
	* [FGameplayAttribute]
* 説明
	* The Attribute we modify or the Gameplay Effect we modify modifies.
	* 変更する属性または変更するゲームプレイ効果が変更されます。

### ModifierOp
* 型
	* [EGameplayModOp::Type]
* 説明
	* The numeric operation of this modifier: Override, Add, Multiply, etc
	* この修飾子の数値演算：オーバーライド、追加、乗算など

### ModifierMagnitude
* 型
	* [FGameplayEffectModifierMagnitude]
* 説明
	* Magnitude of the modifier
	* モディファイアの大きさ

### EvaluationChannelSettings
* 条件
	* ***不明な条件、要調査*** の時のみ有効
* 型
	* [FGameplayModEvaluationChannelSettings]
* 説明
	* Evaluation channel settings of the modifier
	* モディファイアの評価チャネル設定

### SourceTags
* 型
	* [FGameplayTagRequirements]
* 説明
	* 無し

### TargetTags
* 型
	* [FGameplayTagRequirements]
* 説明
	* 無し

# FGameplayAttribute
* 説明
	* Describes a FGameplayAttributeData or float property inside an attribute set. Using this provides editor UI and helper functions
	* 属性セット内の FGameplayAttributeData または float プロパティについて説明します。 これを使用すると、エディター UI とヘルパー関数が提供されます

# EGameplayModOp::Type
* 説明
	* Defines the ways that mods will modify attributes. Numeric ones operate on the existing value, override ignores it
	* modが属性を変更する方法を定義します。 数値は既存の値を操作し、オーバーライドはそれを無視します
* 値
	* Add(Additive)
		* 加算
	* Multiply(Multiplicitive)
		* 乗算
	* Divide(Division)
		* 除算
	* Override
		* This should always be the first non numeric ModOp
		* これは常に最初の非数値ModOpである必要があります


# FGameplayModEvaluationChannelSettings
* 説明
	* Struct representing evaluation channel settings for a gameplay modifier
	* ゲームプレイ修飾子の評価チャネル設定を表す構造体

### Channel
* 型
	* [EGameplayModEvaluationChannel]
* Channel the settings would prefer to use, if possible/valid
	* 可能/有効な場合、設定が使用することを好むチャネル

# EGameplayModEvaluationChannel
* 説明
	* Valid gameplay modifier evaluation channels; Displayed and renamed via game-specific aliases and options
	* 有効なゲームプレイ修飾子の評価チャネル。 ゲーム固有のエイリアスとオプションを介して表示および名前変更

# FGameplayEffectExecutionDefinition
* 説明
	* Struct representing the definition of a custom execution for a gameplay effect.
	Custom executions run special logic from an outside class each time the gameplay effect executes.
	* ゲームプレイ効果のカスタム実行の定義を表す構造体。
	カスタム実行は、ゲームプレイエフェクトが実行されるたびに、外部クラスから特別なロジックを実行します。

### CalculationClass
* 型
	* [UGameplayEffectExecutionCalculation]
* 説明
	* Custom execution calculation class to run when the gameplay effect executes
	* ゲームプレイエフェクトの実行時に実行するカスタム実行計算クラス

### PassedInTags
* 条件
	* CalculationClass で指定された class にて DoesRequirePassedInTags() の戻り値を true にしている時のみ有効
* 型
	* [FGameplayTagContainer]
* 説明
	* These tags are passed into the execution as is, and may be used to do conditional logic
	* これらのタグはそのまま実行に渡され、条件付きロジックを実行するために使用できます。

### CalculationModifiers
* 条件
	* CalculationClass で指定された class にて 以下のどちらかを満たしている時のみ有効
		* GetValidScopedModifierAttributeCaptureDefinitions() の第一引数で一つ以上の FGameplayEffectAttributeCaptureDefinition 配列を返す
		* GetValidTransientAggregatorIdentifiers() の戻り値で一つ以上の FGameplayTag を持つ FGameplayTagContainer を返す
* 型
	* [FGameplayEffectExecutionScopedModifierInfo]
* 説明
	* Modifiers that are applied "in place" during the execution calculation
	* 実行計算中に「インプレース」で適用される修飾子

### ConditionalGameplayEffects
* 型
	* TArray<[FConditionalGameplayEffect]>
* 説明
	* Other Gameplay Effects that will be applied to the target of this execution if the execution is successful. Note if no execution class is selected, these will always apply.
	* 実行が成功した場合にこの実行のターゲットに適用されるその他のゲームプレイ効果。 実行クラスが選択されていない場合、これらは常に適用されることに注意してください。

# UGameplayEffectCalculation
* 説明
	* Abstract base for specialized gameplay effect calculations; Capable of specifing attribute captures
	* 特殊なゲームプレイ効果計算の抽象的なベース。 属性キャプチャを指定できます

### RelevantAttributesToCapture
* 型
	* [FGameplayEffectAttributeCaptureDefinition]
* 説明
	* Attributes to capture that are relevant to the calculation
	* 計算に関連するキャプチャする属性
	
# UGameplayEffectExecutionCalculation
* 基底型
	* [UGameplayEffectCalculation]
* 説明
	* 無し



# FGameplayEffectExecutionScopedModifierInfo
* 説明
	* Struct representing modifier info used exclusively for "scoped" executions that happen instantaneously. These are
	folded into a calculation only for the extent of the calculation and never permanently added to an aggregator.
	* 瞬時に発生する「スコープ付き」実行専用に使用される修飾子情報を表す構造体。 これらは
	計算の範囲でのみ計算に組み込まれ、アグリゲーターに永続的に追加されることはありません。


### CapturedAttribute
* 型
	* [FGameplayEffectAttributeCaptureDefinition]
* 説明
	* Backing attribute that the scoped modifier is for
	* スコープ修飾子の対象となるバッキング属性

### TransientAggregatorIdentifier;
* 型
	* [FGameplayTag]
* 説明
	* Identifier for aggregator if acting as a transient "temporary variable" aggregator
	* 一時的な「一時変数」アグリゲーターとして機能する場合のアグリゲーターの識別子

### AggregatorType
* 型
	* [EGameplayEffectScopedModifierAggregatorType]
* 説明
	* Type of aggregator backing the scoped mod
	* スコープ付きmodをサポートするアグリゲーターのタイプ

### ModifierOp
* 型
	* TEnumAsByte<[EGameplayModOp::Type]>
* 説明
	* Modifier operation to perform
	* 実行する修飾子操作

### ModifierMagnitude;
* 型
	* [FGameplayEffectModifierMagnitude]
* 説明
	* Magnitude of the scoped modifier
	* スコープ修飾子の大きさ

### EvaluationChannelSettings
* 型
	* [FGameplayModEvaluationChannelSettings]
* 説明
	* Evaluation channel settings of the scoped modifier
	* スコープ修飾子の評価チャネル設定

### SourceTags
* 型
	* [FGameplayTagRequirements]
* 説明
	* Source tag requirements for the modifier to apply
	* 適用する修飾子のソースタグ要件

### TargetTags
* 型 
	* [FGameplayTagRequirements]
* 説明
	* Target tag requirements for the modifier to apply
	* 適用する修飾子のターゲットタグ要件


# FGameplayTag
* 説明
	* A single gameplay tag, which represents a hierarchical name of the form x.y that is registered in the GameplayTagsManager
	You can filter the gameplay tags displayed in the editor using, meta = (Categories = "Tag1.Tag2.Tag3"))
	* GameplayTagsManagerに登録されているフォームx.yの階層名を表す単一のゲームプレイタグ
	エディターに表示されるゲームプレイタグは、meta =（Categories = "Tag1.Tag2.Tag3"））を使用してフィルタリングできます。

### TagName
* 型
	* FName
* 説明
	* This Tags Name
	* このタグ名

# EGameplayEffectScopedModifierAggregatorType
* 説明
	* Enumeration representing the types of scoped modifier aggregator usages available
	* 使用可能なスコープ付き修飾子アグリゲーターの使用法のタイプを表す列挙
* 値
	* CapturedAttributeBacked
		* Aggregator is backed by an attribute capture
		* アグリゲーターは属性キャプチャに支えられています
	* Transient
		* Aggregator is entirely transient (acting as a "temporary variable") and must be identified via gameplay tag
		* アグリゲーターは完全に一時的であり（「一時変数」として機能）、ゲームプレイタグを介して識別される必要があります

# FGameplayTagRequirements
* 説明
	* Encapsulate require and ignore tags
	* 「require」タグと「ignore」タグをカプセル化します。

### RequireTags
* 型
	* [FGameplayTagContainer]
* 説明
	* All of these tags must be present
	* これらのタグのすべてが存在しなければなりません

### IgnoreTags
* 型
	* [FGameplayTagContainer]
* 説明
	* None of these tags may be present
	* これらのタグはいずれも存在しない可能性があります

# FConditionalGameplayEffect
* 説明
	* Struct for gameplay effects that apply only if another gameplay effect (or execution) was successfully applied.
	* 別のゲームプレイ効果（または実行）が正常に適用された場合にのみ適用されるゲームプレイ効果の構造体。

### EffectClass
* 型
	* TSubclassOf<[UGameplayEffect]>
* 説明
	* gameplay effect that will be applied to the target
	* ターゲットに適用されるゲームプレイ効果

### RequiredSourceTags
* 型
	* [FGameplayTagContainer]
* 説明
	* Tags that the source must have for this GE to apply
	* このGE(ゲームプレイ効果)を適用するためにソースが持つ必要のあるタグ

# EGameplayEffectPeriodInhibitionRemovedPolicy
* 説明
	* Enumeration of policies for dealing with the period of a gameplay effect when inhibition is removed
	* 抑制が解除されたときのゲームプレイ効果の期間を処理するためのポリシーの列挙
* 値
	* NeverReset
		* Does not reset. The period timing will continue as if the inhibition hadn't occurred.
		* リセットされません。 期間のタイミングは、抑制が発生しなかったかのように継続します。
	* ResetPeriod
		* Resets the period. The next execution will occur one full period from when inhibition is removed.
		* 期間をリセットします。 次の実行は、抑制が解除されてから1期間にわたって行われます。
	* ExecuteAndResetPeriod
		* Executes immediately and resets the period.
		* すぐに実行され、期間がリセットされます。

# UGameplayEffectCustomApplicationRequirement
* 説明
	* Class used to perform custom gameplay effect modifier calculations, either via blueprint or native code
	* ブループリントまたはネイティブコードを介して、カスタムゲームプレイ効果修飾子の計算を実行するために使用されるクラス

# FGameplayEffectCue
* 説明
	* This is a cosmetic cue that can be tied to a UGameplayEffect. 
	This is essentially a GameplayTag + a Min/Max level range that is used to map the level of a GameplayEffect to a normalized value used by the GameplayCue system.
	* これは、UGameplayEffectに関連付けることができる化粧的なキューです。
	これは基本的に、GameplayTag + 最小/最大レベル範囲であり、GameplayEffectのレベルをGameplayCueシステムで使用される正規化された値にマップするために使用されます。

### MagnitudeAttribute
* 型
	* FGameplayAttribute
* 説明
	* The attribute to use as the source for cue magnitude. If none use level
	* キューの大きさのソースとして使用する属性。 レベルが使用されてない場合

### MinLevel
* 型
	* float
* 説明
	* The minimum level that this Cue supports
	* このキューがサポートする最小レベル

### MaxLevel
* 型
	* float
* 説明
	* The maximum level that this Cue supports
	* このキューがサポートする最大レベル

### GameplayCueTags
* 型
	* FGameplayTagContainer
* 説明
	* Tags passed to the gameplay cue handler when this cue is activated
	* このキューがアクティブ化されたときにゲームプレイキューハンドラーに渡されるタグ

# FGameplayEffectQuery
* 説明
	* Every set condition within this query must match in order for the query to match. i.e. individual query elements are ANDed together.
	* クエリが一致するためには、このクエリ内のすべての設定条件が一致する必要があります。 つまり、個々のクエリ要素はANDで結合されます。

### CustomMatchDelegate_BP
* 型
	* FActiveGameplayEffectQueryCustomMatch_Dynamic
* 説明
	* BP-exposed delegate for providing custom matching conditions.
	* カスタムマッチング条件を提供するためのBP公開デリゲート。

### OwningTagQuery
* 型
	* [FGameplayTagQuery]
* 説明
	* Query that is matched against tags this GE gives
	* このGE(GameplayEffect)が提供するタグと照合されるクエリ

### EffectTagQuery
* 型
	* [FGameplayTagQuery]
* 説明
	* Query that is matched against tags this GE has
	* このGE(GameplayEffect)が持つタグと照合されるクエリ

### SourceTagQuery
* 型
	* [FGameplayTagQuery]
* 説明
	* Query that is matched against tags the source of this GE has
	* このGE(GameplayEffect)のソースが持つタグと照合されるクエリ

### ModifyingAttribute
* 型
	* [FGameplayAttribute]
* 説明
	* Matches on GameplayEffects which modify given attribute.
	* 指定された属性を変更するGameplayEffectsで一致します。

### EffectSource
* 型
	* const UObject*
* 説明
	* Matches on GameplayEffects which come from this source
	* このソースからのGameplayEffectsで一致します。

### EffectDefinition
* 型
	* TSubclassOf<[UGameplayEffect]>
* 説明
	* Matches on GameplayEffects with this definition
	* この定義のGameplayEffectsで一致します。


# EGameplayEffectStackingType
* 説明
	* Enumeration for ways a single GameplayEffect asset can stack.
	* 単一のGameplayEffectアセットをスタックできる方法の列挙。
* 値
	* None
		* No stacking. Multiple applications of this GameplayEffect are treated as separate instances.
		* スタッキングなし。 このGameplayEffectの複数のアプリケーションは、個別のインスタンスとして扱われます。
	* AggregateBySource
		* Each caster has its own stack.
		* 各キャスターが独自のスタックを持ちます。
	* AggregateByTarget
		* Each target has its own stack.
		* 各ターゲットが独自のスタックを持ちます。

# EGameplayEffectStackingDurationPolicy
* 説明
	* Enumeration of policies for dealing with duration of a gameplay effect while stacking
	* スタッキング中にゲームプレイ効果の持続時間を処理するためのポリシーの列挙
* 値
	* RefreshOnSuccessfulApplication
		* The duration of the effect will be refreshed from any successful stack application
		* 効果の持続時間は、成功したスタックアプリケーションから更新されます
	* NeverRefresh
		* The duration of the effect will never be refreshed
		* 効果の持続時間は決して更新されません

# EGameplayEffectStackingPeriodPolicy
* 説明
	* Enumeration of policies for dealing with the period of a gameplay effect while stacking
	* スタック中のゲームプレイ効果の期間を処理するためのポリシーの列挙
* 値
	* ResetOnSuccessfulApplication
		* Any progress toward the next tick of a periodic effect is discarded upon any successful stack application
		* 定期的な効果の次のティックに向けた進行状況は、スタックアプリケーションが成功すると破棄されます
	* NeverReset
		* The progress toward the next tick of a periodic effect will never be reset, regardless of stack applications
		* スタックアプリケーションに関係なく、周期的効果の次のティックに向けた進行状況がリセットされることはありません。

# UGameplayAbility
* 説明
	* Abilities define custom gameplay logic that can be activated by players or external game logic
	* 能力は、プレーヤーまたは外部のゲームロジックによってアクティブ化できるカスタムゲームプレイロジックを定義します

# FGameplayAbilitySpecDef
* 説明
	* This is data that can be used to create an FGameplayAbilitySpec. Has some data that is only relevant when granted by a GameplayEffect
	* これは、[FGameplayAbilitySpec] を作成するために使用できるデータです。 GameplayEffectによって付与された場合にのみ関連するデータがいくつかあります

### Ability
* 型
	* TSubclassOf<[UGameplayAbility]>
* 説明
	* What ability to grant
	* 付与する能力
	
### Level(LevelScalableFloat)
* 型
	* FScalableFloat
* 説明
	* What level to grant this ability at
	* この能力を付与するレベル

### InputID
* 型
	* int32
* 説明
	* Input ID to bind this ability to
	* この機能をバインドするための入力ID

### RemovalPolicy
* 型
	* [EGameplayEffectGrantedAbilityRemovePolicy]
* 説明
	* What will remove this ability later
	* 後でこの能力を削除するもの

# FGameplayAbilitySpec
* 基底型
	* FFastArraySerializerItem
* 説明
	* An activatable ability spec, hosted on the ability system component. 
	This defines both what the ability is (what class, what level, input binding etc)
	and also holds runtime state that must be kept outside of the ability being instanced/activated.
	* 能力システムコンポーネントでホストされる、アクティブ化可能な能力仕様。 
	これは、能力が何であるか（どのクラス、どのレベル、入力バインディングなど）の両方を定義します
	また、インスタンス化/アクティブ化される機能の範囲外に保持する必要があるランタイム状態も保持します。

# FGameplayTagQuery
* 説明
```
An FGameplayTagQuery is a logical query that can be run against an FGameplayTagContainer.
A query that succeeds is said to "match".
Queries are logical expressions that can test the intersection properties of another tag container (all, any, or none), 
or the matching state of a set of sub-expressions(all, any, or none). 
This allows queries to be arbitrarily recursive and very expressive.
For instance, if you wanted to test if a given tag container contained tags ((A && B) || (C)) && (!D), 
you would construct your query in the form ALL( ANY( ALL(A,B), ALL(C) ), NONE(D) )

You can expose the query structs to Blueprints and edit them with a custom editor, 
or you can construct them natively in code. 

Example of how to build a query via code:
	FGameplayTagQuery Q;
	Q.BuildQuery(
		FGameplayTagQueryExpression()
 		.AllTagsMatch()
		.AddTag(FGameplayTag::RequestGameplayTag(FName(TEXT("Animal.Mammal.Dog.Corgi"))))
		.AddTag(FGameplayTag::RequestGameplayTag(FName(TEXT("Plant.Tree.Spruce"))))
		);

Queries are internally represented as a byte stream that is memory-efficient and can be evaluated quickly at runtime.
Note: these have an extensive details and graph pin customization for editing, 
so there is no need to expose the internals to Blueprints.
Note: Properties need to be editable to allow FComponentPropertyWriter to serialize them, 
but are hidden in the editor by the customizations mentioned above.
```

[FGameplayTagQuery] は、 [FGameplayTagContainer] に対して実行できる論理クエリです。
成功したクエリは「一致」すると言われます。
クエリは、別のタグコンテナの共通部分のプロパティ（all、any、またはnone）、または一連のサブ式の一致状態（all、any、またはnone）をテストできる論理式です。
これにより、クエリを任意に再帰的で非常に表現力豊かにすることができます。

たとえば、特定のタグコンテナにタグ((A && B) || (C)) && (!D)が含まれているかどうかをテストする場合は、
ALL( ANY( ALL(A,B), ALL(C) ), NONE(D) )の形式でクエリを作成します。

クエリ構造体をブループリントに公開してカスタムエディターで編集することも、コードでネイティブに作成することもできます。

コードを介してクエリを作成する方法の例：


クエリは、メモリ効率が高く、実行時にすばやく評価できるバイトストリームとして内部的に表されます。
注：これらには、編集用の詳細とグラフピンのカスタマイズが含まれているため、内部をブループリントに公開する必要はありません。
注：[FComponentPropertyWriter] がプロパティをシリアル化できるようにするには、プロパティを編集可能にする必要がありますが、上記のカスタマイズによってエディターで非表示になります。


### TokenStreamVersion
* 型
	* int32
* 説明
	* Versioning for future token stream protocol changes. See EGameplayTagQueryStreamVersion.
	* 将来のトークンストリームプロトコルの変更のためのバージョン管理。 [EGameplayTagQueryStreamVersion] を参照してください。

### TagDictionary
* 型
	* TArray<[FGameplayTag]>
* 説明
	* List of tags referenced by this entire query. Token stream stored indices into this list.
	* このクエリ全体で参照されるタグのリスト。 トークンストリームは、インデックスをこのリストに保存します。

### QueryTokenStream
* 型
	* TArray<uint8>
* 説明
	* Stream representation of the actual hierarchical query
	* 実際の階層クエリのストリーム表現

### UserDescription
* 型
	* FString
* 説明
	* User-provided string describing the query
	* クエリを説明するユーザー提供の文字列

### AutoDescription
* 型
	* FString
* 説明
	* Auto-generated string describing the query
	* クエリを説明する自動生成された文字列

# FComponentPropertyWriter
* 説明
	* なし

# EGameplayTagQueryStreamVersion
* 説明
	* なし
* 値
	* InitialVersion
		* (new versions can be added before this line)
		* (この行の前に新しいバージョンを追加できます)
		* this needs to be the last line (see note below)
		* これは最後の行である必要があります（以下の注を参照）
	* VersionPlusOne
	* LatestVersion = VersionPlusOne - 1

# EGameplayEffectGrantedAbilityRemovePolicy
* 説明
	* Describes what happens when a GameplayEffect, that is granting an active ability, is removed from its owner.
	* アクティブな能力を付与しているGameplayEffectが所有者から削除されたときに何が起こるかを説明します。
* 値

	* CancelAbilityImmediately
		* Active abilities are immediately canceled and the ability is removed.
		* アクティブな能力はすぐにキャンセルされ、能力は削除されます。
	* RemoveAbilityOnEnd
		* Active abilities are allowed to finish, and then removed.
		* アクティブな能力は終了することが許可され、その後削除されます。
	* DoNothing
		* Granted abilities are left lone when the granting GameplayEffect is removed.
		* 付与されたGameplayEffectが削除されると、付与された能力は孤立したままになります。


# EGameplayEffectStackingExpirationPolicy
* 説明
	* Enumeration of policies for dealing gameplay effect stacks that expire (in duration based effects).
	* 期限切れのゲームプレイ効果スタックを処理するためのポリシーの列挙（期間ベースの効果）。
* 値
	* ClearEntireStack
		* The entire stack is cleared when the active gameplay effect expires
		* アクティブなゲームプレイ効果が期限切れになると、スタック全体がクリアされます
	* RemoveSingleStackAndRefreshDuration
		* The current stack count will be decremented by 1 and the duration refreshed. The GE is not "reapplied", just continues to exist with one less stacks.
		* 現在のスタックカウントは1ずつ減らされ、期間が更新されます。 GEは「再適用」されず、スタックが1つ少ない状態で存在し続けます。
	* RefreshDuration
		* The duration of the gameplay effect is refreshed. This essentially makes the effect infinite in duration. This can be used to manually handle stack decrements via OnStackCountChange callback
		* ゲームプレイ効果の持続時間が更新されます。 これは本質的に効果の持続時間を無限にします。 これは、OnStackCountChangeコールバックを介してスタックの減少を手動で処理するために使用できます

# FAttributeBasedFloat
* 説明
	* Struct representing a float whose magnitude is dictated by a backing attribute and a calculation policy, follows basic form of:
	 (Coefficient * (PreMultiplyAdditiveValue + [Eval'd Attribute Value According to Policy])) + PostMultiplyAdditiveValue
	* 大きさがバッキング属性と計算ポリシーによって決定されるフロートを表す構造体は、次の基本形式に従います。
  （係数*（PreMultiplyAdditiveValue + [ポリシーに従って評価された属性値]））+ PostMultiplyAdditiveValue

### Coefficient
* 説明
	* Coefficient to the attribute calculation
	* 属性計算の係数

### PreMultiplyAdditiveValue
* 説明
	* Additive value to the attribute calculation, added in before the coefficient applies
	* 係数が適用される前に追加される、属性計算への加算値

### PostMultiplyAdditiveValue
* 説明
	* Additive value to the attribute calculation, added in after the coefficient applies
	* 係数が適用された後に追加される、属性計算への加算値

### BackingAttribute
* 型
	* [FGameplayEffectAttributeCaptureDefinition]
* 説明
	* Attribute backing the calculation
	* 計算を裏付ける属性

### AttributeCurve
* 説明
	* If a curve table entry is specified, the attribute will be used as a lookup into the curve instead of using the attribute directly.
	* 曲線テーブルエントリが指定されている場合、属性は、属性を直接使用する代わりに、曲線へのルックアップとして使用されます。

### AttributeCalculationType
* 型
	* [EAttributeBasedFloatCalculationType]
* 説明
	* Calculation policy in regards to the attribute
	* 属性に関する計算方針

### FinalChannel
* 条件
	* AttributeCalculationType が AttributeMagnitudeEvaluatedUpToChannel の時のみ有効
* 説明
	* Channel to terminate evaluation on when using AttributeEvaluatedUpToChannel calculation type
	* AttributeEvaluatedUpToChannel 計算タイプを使用するときに評価を終了するチャネル

### SourceTagFilter
* 型
	* [FGameplayTagContainer]
* 説明
	* Filter to use on source tags; If specified, only modifiers applied with all of these tags will factor into the calculation
	* ソースタグで使用するフィルター。 指定した場合、これらのタグすべてに適用された修飾子のみが計算に考慮されます

### TargetTagFilter
* 型
	* [FGameplayTagContainer]
* 説明
	* Filter to use on target tags; If specified, only modifiers applied with all of these tags will factor into the calculation
	* ターゲットタグで使用するフィルター。 指定した場合、これらのタグすべてに適用された修飾子のみが計算に考慮されます

# FCustomCalculationBasedFloat
* 説明
	* Structure to encapsulate magnitudes that are calculated via custom calculation
	* カスタム計算によって計算された大きさをカプセル化する構造体

### Calculation Class(CalculationClassMagnitude)
* 型
	* [UGameplayModMagnitudeCalculation]
* 説明
	* 無し

### Coefficient
* 説明
	* Coefficient to the custom calculation
	* カスタム計算の係数

### PreMultiplyAdditiveValue
* 説明
	* Additive value to the attribute calculation, added in before the coefficient applies
	* 係数が適用される前に追加される、属性計算への加算値

### PostMultiplyAdditiveValue
* 説明
	* Additive value to the attribute calculation, added in after the coefficient applies
	* 係数が適用された後に追加される、属性計算への加算値

### FinalLookupCurve
* 説明
	* If a curve table entry is specified, the OUTPUT of this custom class magnitude (including the pre and post additive values) lookup into the curve instead of using the attribute directly.
	* 曲線テーブルのエントリが指定されている場合、このカスタムクラスの大きさの出力（事前及び事後の加算値を含む）は、属性を直接使用する代わりに、曲線を検索します。

# FSetByCallerFloat
* 説明
	* Struct for holding SetBytCaller data
	* SetBytCaller データを保持するための構造

### DataName
* 説明
	* The Name the caller (code or blueprint) will use to set this magnitude by.
	* 呼び出し元（コードまたはブループリント）がこの大きさを設定するために使用する名前。

### DataTag
* 説明
	* 無し

# FInheritedTagContainer
* 説明
	* Structure that is used to combine tags from parent and child blueprints in a safe way
	* 親と子のブループリントからのタグを安全な方法で組み合わせるために使用される構造

### CombinedTags
* 型
	* [FGameplayTagContainer]
* 説明
	* Tags that I inherited and tags that I added minus tags that I removed
	* 継承したタグと追加したタグから削除したタグを差し引いたもの

### Added
* 型
	* [FGameplayTagContainer]
* 説明
	* Tags that I have in addition to my parent's tags
	* 親のタグに加えて持っているタグ

### Removed
* 型
	* [FGameplayTagContainer]
* 説明
	* Tags that should be removed if my parent had them
	* 親が持っていた場合に削除する必要のあるタグ

----
[UGameplayEffect]:#UGameplayEffect
[EGameplayEffectDurationType]:#EGameplayEffectDurationType
[FGameplayEffectModifierMagnitude]:#FGameplayEffectModifierMagnitude
[EGameplayEffectMagnitudeCalculation]:#EGameplayEffectMagnitudeCalculation
[FGameplayEffectAttributeCaptureDefinition]:#FGameplayEffectAttributeCaptureDefinition
[EGameplayEffectAttributeCaptureSource]:#EGameplayEffectAttributeCaptureSource
[FGameplayTagContainer]:#FGameplayTagContainer
[UGameplayModMagnitudeCalculation]:#UGameplayModMagnitudeCalculation
[FGameplayModifierInfo]:#FGameplayModifierInfo
[FGameplayAttribute]:#FGameplayAttribute
[EGameplayModOp::Type]:#EGameplayModOp::Type
[FGameplayModEvaluationChannelSettings]:#FGameplayModEvaluationChannelSettings
[EGameplayModEvaluationChannel]:#EGameplayModEvaluationChannel
[FGameplayEffectExecutionDefinition]:#FGameplayEffectExecutionDefinition
[UGameplayEffectCalculation]:#UGameplayEffectCalculation
[UGameplayEffectExecutionCalculation]:#UGameplayEffectExecutionCalculation
[FGameplayEffectExecutionScopedModifierInfo]:#FGameplayEffectExecutionScopedModifierInfo
[FGameplayTag]:#FGameplayTag
[EGameplayEffectScopedModifierAggregatorType]:#EGameplayEffectScopedModifierAggregatorType
[FGameplayTagRequirements]:#FGameplayTagRequirements
[FConditionalGameplayEffect]:#FConditionalGameplayEffect
[UGameplayEffect]:#UGameplayEffect
[EGameplayEffectPeriodInhibitionRemovedPolicy]:#EGameplayEffectPeriodInhibitionRemovedPolicy
[UGameplayEffectCustomApplicationRequirement]:#UGameplayEffectCustomApplicationRequirement
[FGameplayEffectCue]:#FGameplayEffectCue
[FGameplayEffectQuery]:#FGameplayEffectQuery
[EGameplayEffectStackingType]:#EGameplayEffectStackingType
[EGameplayEffectStackingDurationPolicy]:#EGameplayEffectStackingDurationPolicy
[EGameplayEffectStackingPeriodPolicy]:#EGameplayEffectStackingPeriodPolicy
[EGameplayEffectStackingExpirationPolicy]:#EGameplayEffectStackingExpirationPolicy
[UGameplayAbility]:#UGameplayAbility
[FGameplayAbilitySpecDef]:#FGameplayAbilitySpecDef
[FGameplayAbilitySpec]:#FGameplayAbilitySpec
[FGameplayTagQuery]:#FGameplayTagQuery
[FComponentPropertyWriter]:#FComponentPropertyWriter
[EGameplayTagQueryStreamVersion]:#EGameplayTagQueryStreamVersion
[EGameplayEffectGrantedAbilityRemovePolicy]:#EGameplayEffectGrantedAbilityRemovePolicy

[FAttributeBasedFloat]:#FAttributeBasedFloat
[FCustomCalculationBasedFloat]:#FCustomCalculationBasedFloat
[FSetByCallerFloat]:#FSetByCallerFloat
[FInheritedTagContainer]:#FInheritedTagContainer


----
おしまい。
