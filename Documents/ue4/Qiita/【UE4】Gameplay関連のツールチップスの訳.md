
#  Gameplay Effect

カテゴリ別

## GameplayEffect
* GameplayEffect
	* ゲームプレイ効果

### DurationPolicy
* Policy for the duration of this effect
	* この効果の持続期間のポリシー

値は [EGameplayEffectDurationType] を参照

### DurationMagnitude
DurationPolicy が HasDuration の時のみ有効

* Duration in seconds. 0.0 for instantaneous effects; -1.0 for infinite duration.
	* 秒単位の期間。 瞬間効果の場合は 0.0。 無限の期間の場合は-1.0。

値は FGameplayEffectModifierMagnitude を参照

### FGameplayEffectModifierMagnitude

	/** Type of calculation to perform to derive the magnitude */
	UPROPERTY(EditDefaultsOnly, Category=Magnitude)
	EGameplayEffectMagnitudeCalculation MagnitudeCalculationType;

	/** Magnitude value represented by a scalable float */
	UPROPERTY(EditDefaultsOnly, Category=Magnitude)
	FScalableFloat ScalableFloatMagnitude;

	/** Magnitude value represented by an attribute-based float
	(Coefficient * (PreMultiplyAdditiveValue + [Eval'd Attribute Value According to Policy])) + PostMultiplyAdditiveValue */
	UPROPERTY(EditDefaultsOnly, Category=Magnitude)
	FAttributeBasedFloat AttributeBasedMagnitude;

	/** Magnitude value represented by a custom calculation class */
	UPROPERTY(EditDefaultsOnly, Category=Magnitude)
	FCustomCalculationBasedFloat CustomMagnitude;

	/** Magnitude value represented by a SetByCaller magnitude */
	UPROPERTY(EditDefaultsOnly, Category=Magnitude)
	FSetByCallerFloat SetByCallerMagnitude;




### 
	/** Array of modifiers that will affect the target of this effect */
	UPROPERTY(EditDefaultsOnly, BlueprintReadOnly, Category=GameplayEffect)
	TArray<FGameplayModifierInfo> Modifiers;

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
### EGameplayEffectDurationType
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


----
[EGameplayEffectDurationType]:#EGameplayEffectDurationType


----
おしまい。
