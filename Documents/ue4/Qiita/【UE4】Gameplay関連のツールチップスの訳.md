
#  Gameplay Effect

カテゴリ別

## GameplayEffect
* GameplayEffect
	* ゲームプレイ効果

### DurationPolicy
* Policy for the duration of this effect
	* この効果の持続期間のポリシー
* 値
	* [EGameplayEffectDurationType] を参照

### DurationMagnitude
DurationPolicy が HasDuration の時のみ有効

* Duration in seconds. 0.0 for instantaneous effects; -1.0 for infinite duration.
	* 秒単位の期間。 瞬間効果の場合は 0.0。 無限の期間の場合は-1.0。
* 値
	* [FGameplayEffectModifierMagnitude] を参照

### Modifiers
* Array of modifiers that will affect the target of this effect
	* この効果の対象に影響を与える修飾子の配列
* 値
	* [FGameplayModifierInfo] を参照

ここから
### 
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = GameplayEffect)
	TArray<FGameplayEffectExecutionDefinition>	Executions;

### 
	/** other gameplay effects that will be applied to the target of this effect if this effect applies */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = GameplayEffect)
	TArray<FConditionalGameplayEffect> ConditionalGameplayEffects;


## Period
### 
	/** Period in seconds. 0.0 for non-periodic effects */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Period)
	FScalableFloat	Period;
	
### 
	/** If true, the effect executes on application and then at every period interval. If false, no execution occurs until the first period elapses. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Period)
	bool bExecutePeriodicEffectOnApplication;

### 
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Period)
	EGameplayEffectPeriodInhibitionRemovedPolicy PeriodicInhibitionPolicy;


## Application
### 
	/** Probability that this gameplay effect will be applied to the target actor (0.0 for never, 1.0 for always) */
	UPROPERTY(EditDefaultsOnly, Category=Application, meta=(GameplayAttribute="True"))
	FScalableFloat	ChanceToApplyToTarget;

### 
	UPROPERTY(EditDefaultsOnly, Category=Application, DisplayName="Application Requirement")
	TArray<TSubclassOf<UGameplayEffectCustomApplicationRequirement> > ApplicationRequirements;

## Overflow
### 
	/** Effects to apply when a stacking effect "overflows" its stack count through another attempted application. Added whether the overflow application succeeds or not. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Overflow)
	TArray<TSubclassOf<UGameplayEffect>> OverflowEffects;

### 
	/** If true, stacking attempts made while at the stack count will fail, resulting in the duration and context not being refreshed */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Overflow)
	bool bDenyOverflowApplication;

### 
	/** If true, the entire stack of the effect will be cleared once it overflows */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Overflow, meta=(EditCondition="bDenyOverflowApplication"))
	bool bClearStackOnOverflow;


## Expiration
### 
	/** Effects to apply when this effect is made to expire prematurely (like via a forced removal, clear tags, etc.); Only works for effects with a duration */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Expiration)
	TArray<TSubclassOf<UGameplayEffect>> PrematureExpirationEffectClasses;

### 
	/** Effects to apply when this effect expires naturally via its duration; Only works for effects with a duration */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=Expiration)
	TArray<TSubclassOf<UGameplayEffect>> RoutineExpirationEffectClasses;


## Display
### 
	/** If true, cues will only trigger when GE modifiers succeed being applied (whether through modifiers or executions) */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Display)
	bool bRequireModifierSuccessToTriggerCues;

### 
	/** If true, GameplayCues will only be triggered for the first instance in a stacking GameplayEffect. */
	UPROPERTY(EditDefaultsOnly, Category = Display)
	bool bSuppressStackingCues;

### 
	/** Cues to trigger non-simulated reactions in response to this GameplayEffect such as sounds, particle effects, etc */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Display)
	TArray<FGameplayEffectCue>	GameplayCues;

### 
	/** Data for the UI representation of this effect. This should include things like text, icons, etc. Not available in server-only builds. */
	UPROPERTY(EditDefaultsOnly, Instanced, BlueprintReadOnly, Category = Display)
	class UGameplayEffectUIData* UIData;

## Tags
	// ----------------------------------------------------------------------
	//	Tag Containers
	// ----------------------------------------------------------------------
	
### 
	/** The GameplayEffect's Tags: tags the the GE *has* and DOES NOT give to the actor. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta = (DisplayName = "GameplayEffectAssetTag", Categories="GameplayEffectTagsCategory"))
	FInheritedTagContainer InheritableGameplayEffectTags;
	
### 
	/** "These tags are applied to the actor I am applied to" */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta=(DisplayName="GrantedTags", Categories="OwnedTagsCategory"))
	FInheritedTagContainer InheritableOwnedTagsContainer;
	
### 
	/** Once Applied, these tags requirements are used to determined if the GameplayEffect is "on" or "off". A GameplayEffect can be off and do nothing, but still applied. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta=(Categories="OngoingTagRequirementsCategory"))
	FGameplayTagRequirements OngoingTagRequirements;

### 
	/** Tag requirements for this GameplayEffect to be applied to a target. This is pass/fail at the time of application. If fail, this GE fails to apply. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta=(Categories="ApplicationTagRequirementsCategory"))
	FGameplayTagRequirements ApplicationTagRequirements;

### 
	/** Tag requirements that if met will remove this effect. Also prevents effect application. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta=(Categories="ApplicationTagRequirementsCategory"))
	FGameplayTagRequirements RemovalTagRequirements;

### 
	/** GameplayEffects that *have* tags in this container will be cleared upon effect application. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta=(Categories="RemoveTagRequirementsCategory"))
	FInheritedTagContainer RemoveGameplayEffectsWithTags;

### 
	/** On Application of an effect, any active effects with this this query that matches against the added effect will be removed. Queries are more powerful but slightly slower than RemoveGameplayEffectsWithTags. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Tags, meta = (DisplayAfter = "RemovalTagRequirements"))
	FGameplayEffectQuery RemoveGameplayEffectQuery;


## Immunity
### 
	/** Grants the owner immunity from these source tags.  */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Immunity, meta = (DisplayName = "GrantedApplicationImmunityTags", Categories="GrantedApplicationImmunityTagsCategory"))
	FGameplayTagRequirements GrantedApplicationImmunityTags;

### 
	/** Grants immunity to GameplayEffects that match this query. Queries are more powerful but slightly slower than GrantedApplicationImmunityTags. */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Immunity)
	FGameplayEffectQuery GrantedApplicationImmunityQuery;

## Stacking
	// ----------------------------------------------------------------------
	//	Stacking
	// ----------------------------------------------------------------------
	
### 
	/** How this GameplayEffect stacks with other instances of this same GameplayEffect */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Stacking)
	EGameplayEffectStackingType	StackingType;

### 
	/** Stack limit for StackingType */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Stacking)
	int32 StackLimitCount;

### 
	/** Policy for how the effect duration should be refreshed while stacking */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Stacking)
	EGameplayEffectStackingDurationPolicy StackDurationRefreshPolicy;

### 
	/** Policy for how the effect period should be reset (or not) while stacking */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Stacking)
	EGameplayEffectStackingPeriodPolicy StackPeriodResetPolicy;

### 
	/** Policy for how to handle duration expiring on this gameplay effect */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = Stacking)
	EGameplayEffectStackingExpirationPolicy StackExpirationPolicy;

## Granted Abilities
	// ----------------------------------------------------------------------
	//	Granted abilities
	// ----------------------------------------------------------------------
	
### 
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category = "Granted Abilities")
	TArray<FGameplayAbilitySpecDef>	GrantedAbilities;



----
# EGameplayEffectDurationType
* Gameplay effect duration policies
	* ゲームプレイ効果の継続時間ポリシー

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
* Struct representing the magnitude of a gameplay effect modifier, potentially calculated in numerous different ways
	* ゲームプレイ効果修飾子の大きさを表す構造体。さまざまな方法で計算される可能性があります。

### MagnitudeCalculationType
* Type of calculation to perform to derive the magnitude
	* 大きさを導出するために実行する計算のタイプ
* 値
	* [EGameplayEffectMagnitudeCalculation] を参照

### ScalableFloatMagnitude
MagnitudeCalculationType が ScalableFloat の時のみ有効

* Magnitude value represented by a scalable float
	* スケーラブルなフロートで表される大きさの値

### AttributeBasedMagnitude
MagnitudeCalculationType が AttributeBased の時のみ有効

* Magnitude value represented by an attribute-based float
(Coefficient * (PreMultiplyAdditiveValue + [Eval'd Attribute Value According to Policy])) + PostMultiplyAdditiveValue
	* 属性ベースの浮動小数点数で表される大きさの値
	（係数*（PreMultiplyAdditiveValue + [ポリシーに従って評価された属性値]））+ PostMultiplyAdditiveValue
* 値
	* [FAttributeBasedFloat] を参照

### CustomMagnitude
MagnitudeCalculationType が CustomCalculationClass の時のみ有効

* Magnitude value represented by a custom calculation class
	* カスタム計算クラスで表される大きさの値
* 値
	* [FCustomCalculationBasedFloat] を参照

### SetByCallerMagnitude
MagnitudeCalculationType が SetByCaller の時のみ有効

* Magnitude value represented by a SetByCaller magnitude
	* SetByCaller の大きさによって表される大きさの値
* 値
	* [FSetByCallerFloat] を参照

# EGameplayEffectMagnitudeCalculation
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


# FAttributeBasedFloat
* Struct representing a float whose magnitude is dictated by a backing attribute and a calculation policy, follows basic form of:
 (Coefficient * (PreMultiplyAdditiveValue + [Eval'd Attribute Value According to Policy])) + PostMultiplyAdditiveValue
	* 大きさがバッキング属性と計算ポリシーによって決定されるフロートを表す構造体は、次の基本形式に従います。
  （係数*（PreMultiplyAdditiveValue + [ポリシーに従って評価された属性値]））+ PostMultiplyAdditiveValue

### Coefficient
* Coefficient to the attribute calculation
	* 属性計算の係数

### PreMultiplyAdditiveValue
* Additive value to the attribute calculation, added in before the coefficient applies
	* 係数が適用される前に追加される、属性計算への加算値

### PostMultiplyAdditiveValue
* Additive value to the attribute calculation, added in after the coefficient applies
	* 係数が適用された後に追加される、属性計算への加算値

### BackingAttribute
* Attribute backing the calculation
	* 計算を裏付ける属性
* 値
	* [FGameplayEffectAttributeCaptureDefinition] を参照

### AttributeCurve
* If a curve table entry is specified, the attribute will be used as a lookup into the curve instead of using the attribute directly.
	* 曲線テーブルエントリが指定されている場合、属性は、属性を直接使用する代わりに、曲線へのルックアップとして使用されます。

### AttributeCalculationType
* Calculation policy in regards to the attribute
	* 属性に関する計算方針
* 値
	* [EAttributeBasedFloatCalculationType] を参照

### FinalChannel
AttributeCalculationType が AttributeMagnitudeEvaluatedUpToChannel の時のみ有効

* Channel to terminate evaluation on when using AttributeEvaluatedUpToChannel calculation type
	* AttributeEvaluatedUpToChannel 計算タイプを使用するときに評価を終了するチャネル

### SourceTagFilter
* Filter to use on source tags; If specified, only modifiers applied with all of these tags will factor into the calculation
	* ソースタグで使用するフィルター。 指定した場合、これらのタグすべてに適用された修飾子のみが計算に考慮されます
* 値
	* [FGameplayTagContainer] を参照

### TargetTagFilter
* Filter to use on target tags; If specified, only modifiers applied with all of these tags will factor into the calculation
	* ターゲットタグで使用するフィルター。 指定した場合、これらのタグすべてに適用された修飾子のみが計算に考慮されます
* 値
	* [FGameplayTagContainer] を参照


# FGameplayEffectAttributeCaptureDefinition
* Struct defining gameplay attribute capture options for gameplay effects
	* ゲームプレイ効果のゲームプレイ属性キャプチャオプションを定義する構造体

### AttributeToCapture
* Gameplay attribute to capture
	* キャプチャするゲームプレイ属性

### AttributeSource
* Source of the gameplay attribute
	* ゲームプレイ属性のソース
* 値
	* [EGameplayEffectAttributeCaptureSource] を参照

### bSnapshot
* Whether the attribute should be snapshotted or not
	* 属性をスナップショットする必要があるかどうか

# EGameplayEffectAttributeCaptureSource
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
		* ```AbilitySystemGlobalsCDO::ShouldAllowGameplayModEvaluationChannels()``` が true を返さない場合は表示されない

# FGameplayTagContainer
* A Tag Container holds a collection of FGameplayTags, tags are included explicitly by adding them, and implicitly from adding child tags
	* タグコンテナはFGameplayTagのコレクションを保持し、タグはそれらを追加することによって明示的に含まれ、子タグの追加から暗黙的に含まれます

# FCustomCalculationBasedFloat

* Structure to encapsulate magnitudes that are calculated via custom calculation
	* カスタム計算によって計算された大きさをカプセル化する構造体

### CalculationClassMagnitude
* 表示名は Calculation Class
* 説明無し
* 値
	* [UGameplayModMagnitudeCalculation] を参照

### Coefficient
* Coefficient to the custom calculation
	* カスタム計算の係数

### PreMultiplyAdditiveValue
* Additive value to the attribute calculation, added in before the coefficient applies
	* 係数が適用される前に追加される、属性計算への加算値

### PostMultiplyAdditiveValue
* Additive value to the attribute calculation, added in after the coefficient applies
	* 係数が適用された後に追加される、属性計算への加算値

### FinalLookupCurve
* If a curve table entry is specified, the OUTPUT of this custom class magnitude (including the pre and post additive values) lookup into the curve instead of using the attribute directly.
	* 曲線テーブルのエントリが指定されている場合、このカスタムクラスの大きさの出力（事前及び事後の加算値を含む）は、属性を直接使用する代わりに、曲線を検索します。


# FSetByCallerFloat
* Struct for holding SetBytCaller data
	* SetBytCaller データを保持するための構造

### DataName
* The Name the caller (code or blueprint) will use to set this magnitude by.
	* 呼び出し元（コードまたはブループリント）がこの大きさを設定するために使用する名前。

### DataTag
* 説明無し

# UGameplayModMagnitudeCalculation
* Class used to perform custom gameplay effect modifier calculations, either via blueprint or native code
	* ブループリントまたはネイティブコードを介して、カスタムゲームプレイ効果修飾子の計算を実行するために使用されるクラス

# FGameplayModifierInfo
* Tells us "Who/What we" modify. Does not tell us how exactly.
	* 「誰が/何を」変更するかを教えてくれます。具体的には教えてくれません。

### Attribute
* The Attribute we modify or the Gameplay Effect we modify modifies.
	* 変更する属性または変更するゲームプレイ効果が変更されます。
* 値
	* [FGameplayAttribute] を参照

### ModifierOp
* The numeric operation of this modifier: Override, Add, Multiply, etc
	* この修飾子の数値演算：オーバーライド、追加、乗算など
* 値
	* [EGameplayModOp::Type] を参照

### ModifierMagnitude
* Magnitude of the modifier
	* モディファイアの大きさ
* 値
	* [FGameplayEffectModifierMagnitude] を参照

### EvaluationChannelSettings
***不明な条件、要調査*** の時のみ有効

* Evaluation channel settings of the modifier
	* モディファイアの評価チャネル設定
* 値
	* [FGameplayModEvaluationChannelSettings] を参照

### SourceTags
* 説明無し
* 値
	* [FGameplayTagRequirements] を参照

### TargetTags
* 説明無し
* 値
	* [FGameplayTagRequirements] を参照

# FGameplayAttribute
* Describes a FGameplayAttributeData or float property inside an attribute set. Using this provides editor UI and helper functions
	* 属性セット内の FGameplayAttributeData または float プロパティについて説明します。 これを使用すると、エディター UI とヘルパー関数が提供されます

# EGameplayModOp::Type
* Defines the ways that mods will modify attributes. Numeric ones operate on the existing value, override ignores it
	* modが属性を変更する方法を定義します。 数値は既存の値を操作し、オーバーライドはそれを無視します
* 値
	* Additive
		* 表示名 はAdd
		* 加算
	* Multiplicitive
		* 表示名 はMultiply
		* 乗算
	* Division
		* 表示名 はDivide
		* 除算
	* Override
		* This should always be the first non numeric ModOp
			* これは常に最初の非数値ModOpである必要があります


# FGameplayModEvaluationChannelSettings
* Struct representing evaluation channel settings for a gameplay modifier
	* ゲームプレイ修飾子の評価チャネル設定を表す構造体

### Channel
* Channel the settings would prefer to use, if possible/valid
	* 可能/有効な場合、設定が使用することを好むチャネル
* 値
	* [EGameplayModEvaluationChannel] を参照

# EGameplayModEvaluationChannel
* Valid gameplay modifier evaluation channels; Displayed and renamed via game-specific aliases and options
	* 有効なゲームプレイ修飾子の評価チャネル。 ゲーム固有のエイリアスとオプションを介して表示および名前変更


----
[EGameplayEffectDurationType]:#EGameplayEffectDurationType
[FGameplayEffectModifierMagnitude]:#FGameplayEffectModifierMagnitude
[EGameplayEffectMagnitudeCalculation]:#EGameplayEffectMagnitudeCalculation
[FAttributeBasedFloat]:#FAttributeBasedFloat
[FGameplayEffectAttributeCaptureDefinition]:#FGameplayEffectAttributeCaptureDefinition
[EGameplayEffectAttributeCaptureSource]:#EGameplayEffectAttributeCaptureSource
[FGameplayTagContainer]:#FGameplayTagContainer
[FCustomCalculationBasedFloat]:#FCustomCalculationBasedFloat
[FSetByCallerFloat]:#FSetByCallerFloat
[UGameplayModMagnitudeCalculation]:#UGameplayModMagnitudeCalculation
[FGameplayModifierInfo]:#FGameplayModifierInfo
[FGameplayAttribute]:#FGameplayAttribute
[EGameplayModOp::Type]:#EGameplayModOp::Type
[FGameplayModEvaluationChannelSettings]:#FGameplayModEvaluationChannelSettings
[EGameplayModEvaluationChannel]:#EGameplayModEvaluationChannel


----
おしまい。
