# ■ Gameplay Abilities in Action RPG

## ■ このファイルについて
公式のサンプル ActionRPG の解説ページについて簡単にまとめたもの。

# ■ GameplayAbilitiesinActionRPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG

## ■ 概要
* 公式のドキュメント。
* ドキュメントツリー上では配下に以下の 12 のドキュメントが置かれている。
	* GameplayAbilitiesinActionRPG
		* Setup(導入手順などの説明)
			* Building GamePlay in C++ and for Action RPG
			* Balancing Blueprint and C++
		* Ability System Breakdown(ActionRPG サンプル での AbilitySystem の利用方法についての解説)
			* Gameplay Abilities in Action PRG
				* Attributes and effects In ARPG
				* Melee Abilities In ARPG
				* Skill Abilities In ARPG
				* Executingg Abilities In ARPG
		* Guides(拡張方法についての解説)
			* Adding a Random Amount of Soules Per Kill
			* Adding A Pick Up
			* Migrating Countent
			* Adding a New Weapon
			* Adding a New Potion


# ■ Building GamePlay in C++ and for Action RPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/BuildingGameplayInCPPforActionRPG

## ■ 概要
* ActionRPG サンプルがどのように Gamplay Ability System を利用していて、同様のシステムを作る場合の例としての説明を述べている。
* コードの概要としてどのソースがどのような役割化を述べている。
* 所持アイテムとそれに紐づくアセットについてどのように管理しているか簡単に述べている。
* セーブデータの管理方法について UE4 の仕組みとともに述べている。
* Android/iOS などへのパブリッシュの方法についてパッケージに含めるアセットの抑え方や大きいアセットの調査方法について述べている。


# ■ Balancing Blueprint and C++
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/BalancingBlueprintAndCPP

## ■ 概要
* Blueprint/C++ をどのような配分で利用するべきかの考え方をデータ駆動のゲームシステム構築を通じて述べている。
* UE4 でのロジックとデータの保持の方法について述べている。
* Blueprint/C++ のそれぞれの利点を述べている。
* Blueprint から C++ への変換方法を述べている。
* Blueprint/C++ の性能の違いについて述べている。
* ここまでを踏まえたうえで避けるべき設計に関するいくつかの事柄について述べている。
	* リソースを大量に持つような Brueprint へのキャストを避ける。
	* 過度な循環参照を行う Blueprint を避ける。
	* C++ から直接アセットを参照するのを避ける。
	* 文字によるアセットの参照を避ける。
	* Blueprint での enum/struct の定義を避ける。
	* プロトタイプが済んだ後、ネットワークアーキテクチャについて考慮する。
	* リソースが増えてきたら、非同期ロードについて考える。


# ■ Gameplay Abilities in Action PRG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG

## ■ 概要
* ARPG にて Gameplay Ability System を何故使用しているかを述べている。
* Gameplay Ability System のどの機能をどのように使用しているかを述べている。


# ■ Attributes and effects In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/AttributesandEffects

## ■ 概要
* ARPG において、 Attribute と Effect を何に使用しているか述べている。
* どのような Attribute を定義しているか述べている。
* AbilitySystem の処理の流れについて簡単に述べている。
* Attribute の初期化を Effect で行う方法について述べている。
* ダメージ計算のようなロジックが必要な Effect では Modifier ではなく Execution を使用していることを述べている。
* Effect ついて、ベースクラスを作りサブクラスで特殊化していることを述べている。

# ■ Melee Abilities In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/MeleeAbilitiesInARPG

**Melee 関連のみ、そのうえ部分的にしか見ていないため、全体を見終わったのちに利用例や内容についての精査が必要**

## ■ 概要
* ARPG の近接攻撃をどのように実装しているか述べている。
* Ability は GA_MeleeBase をもとにし、ここから武器ごとなどに派生していることを述べている。
* Ability 用のノードについての説明をしている。
	* CommitAbility ：コストと Cooldown のコミット
	* EndAbility ： Ability が終了したことをシステムに通知
* 処理の流れについて述べている
	* URPGAbilityTask_PlayMontageAndWaitForEvent にて
		* PlayMontageAndWait の処理を行うことで、 Montage が実行される
		* 例： GA_MeleeBase
			* EventTag 「 Event.Montage 」 を指定することで WaitGameplayEvent のイベントをフィルタしている
	* Montage 内で AnimNotify を利用して、 EventTag の設定を行う
		* 例： AM_AttackAxe
			* WeaponAttackNS を Notifies に登録している。
		* 例： WeaponAttackNS
			* EventTag 「 Event.Montage.Shared.WeaponHit 」 を WeaponActor に設定している。
	* イベントの呼び出し
		* 例： WeaponActor::ActorBeginOverlap
			* ターゲットが攻撃可能な Actor だった場合、 Send Gameplay Event to Actor を発行する
			* その際、ペイロードとして GameplayEventData で 「 AnimNotify で設定した EventTag 」「攻撃側の Actor 」「ターゲット側の Actor 」を渡している。
	* URPGAbilityTask_PlayMontageAndWaitForEvent の中で AbilitySystemComponent からイベントを受け取る
		* フィルタに含まれるイベントだった場合は Event Recieved が実行される。
		* 例： GA_MeleeBase
			* EventTag 「 Event.Montage 」 を指定しているので、 例えば WeaponActor::ActorBeginOverlap の場合、「 Event Recieved 」の実行ピンが呼び出される。
	* Apply Effect Container ノードにてエフェクトを実行している。
		* 例： GA_PlayerAxeMelee
			* key 「 Event.Montage.Shared.WeaponHit 」に RPGTargetType_UseEventData/GE_PlayerAxeMelee が設定されている。
			* ターゲット RPGTargetType_UseEventData に、イベント GE_PlayerAxeMelee を発行するための FRPGGameplayEffectContainerSpec を生成する。
			* 生成後、適用する。
* 自作の 「 PlayMontage and Wait for Event 」ノードについて述べている
	* C++ のソースは URPGAbilityTask_PlayMontageAndWaitForEvent である事
	* UAbilityTask_PlayMontageAndWait と UAbilityTask_WaitGameplayEvent を組み合わせて実装している事
	* ゲーム特有の Ability Task を自作する際のサンプルとなる事
* 自作の 「 Apply Effect Container 」ノードについて述べている
	* C++ のソースは URPGGameplayAbility::ApplyEffectContainer である事
	* 行っている２つのこと
		1. 渡された ContainerTag がプロパティ「 GameplayEffect ＞ Effect Container Map 」の key に設定されているタグか判定する。  
		  設定されている場合、対応した value を元に FRPGGameplayEffectContainerSpec を生成する。
		1. 生成した FRPGGameplayEffectContainerSpec を適用し、実際のダメージを与える
* RPGTargetType_UseEventData について
	* RPGTargetType.cpp で実装されている。
	* RPGTargetType_UseEventData では ContextHandle ＞ Target のみを先の順番で参照する。
	* 例： WeaponActor
		* Instigator と Target しか設定されていない。
		* そのため、ターゲットは ActorBeginOverlap のトリガとなった Actor のみが利用される。


# ■ Skill Abilities In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/SkillAbilitiesInARPG

## ■ 概要
* ARPG のスキルをどのように実装しているか述べている。
* 近接攻撃との違いを述べている。
	* ターゲッティング
		* TargetType をプロパティ「 GameplayEffect ＞ Effect Container Map 」 に設定。
	* コスト
		* コスト処理する Gameplay Effect をプロパティ「 Costs ＞ Cost Gameplay Effect Class 」 に設定。
	* Cooldown
		* Cooldown 処理する Gameplay Effect をプロパティ「 Cooldowns ＞ Cooldown Gameplay Effect Class 」 に設定。
	* 例： GA_PlayerSkillWave
		* ダメージエフェクトとして GE_PlayerSkillFireWave を設定している
		* コストエフェクトとして GE_PlayerSkillManaCost を設定している
			* mana がなければ実行できず、あれば減らして実行するというシンプルなもの
		* コストエフェクトとして GE_PlayerSkillCooldown を設定している
			* 一定期間動作し、その間 GameplayTag を適用する
* TargetType について述べている。
	* インスタンス化されない const Blueprints(or native classes) である事
	* スキルで使用しているのは TargetType_SphereTrace を基底にしている事
	* TargetType は ARPG で独自に作ったものである事
	* ゲーム特有のターゲッティングを実装する際のサンプルとなる事
* Cooldown について述べている。
	* 同じ Effect を使用することで複数の機能間でクールダウンを共有する事
		* **Cooldown を分けたい場合は「別のタグを指定した別の Effect 」？**
		* **Cooldown を共有したいが時間が違う場合は「同じタグを指定した別の Duration を指定した Effect 」？**
		* **テストコードを書いたほうがよさそう。**
	* UI システムから問い合わせできる事
* 発射物に関して述べている。
	* 直接攻撃と異なり、 Effect をいきなり適用しない。 EffectContainerSpec を生成し、 Spawn させた 発射物（ BP_AbilityProjectileBase ）に設定している事
	* 発射物が Actor と重なったのちに EffectContainerSpec をもとに Effect を適用している事


# ■ Executingg Abilities In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/ExecutingAbilitiesInARPG

## ■ 概要
* Ability の処理の実行の流れについて述べている。
	* TAG と Item Slot を用いている事
	* エンジンの機能である ActivateAbilitiesWithTags を使用して有効化している事
		* 使用した際、「 Ability.Skill 」を含むアビリティ対象となっていること。
	* アイテムを装備する場合は　 AddSlottedGameplayAbilities を使用して AbilitySystemComponent にアイテム固有の Ability を追加している事
* Weapon と Potion で利用している ARPG で独自に実装した ARPGCharacterBase::ActivateAbilitiesWithItemSlot について述べている。
	* BP_Character と BP_PlayerCharacter から呼ばれている。
* 装備による Ability の追加の流れについて述べている。
	* ARPGCharacterBase::AddSlottedGameplayAbilities にて行って事
	* プロパティ「 Inventory ＞ Sloted Abilities 」に FGameplayAbilitySpec として追加している事
* プレイヤーと敵それぞれのアイテムスロットは異なる方法を用いていることについて述べている。
	* 敵
		* プロパティ「 Abilities ＞ Default Sloted Abilities 」から入力される事
	* プレイヤ
		* 実際のインベントリから入力される事
		* ARPGCharacterBase の中でかなり複雑なロジックを持つ
			* インベントリにアクセスするためのインタフェースクラス IRPGInventoryInterface がある。
			* ARPGCharacterBase::InventorySource は IRPGInventoryInterface への参照。
			* ARPGPlayerControllerBase は IRPGInventoryInterface の派生クラス。
			* ARPGCharacterBase::PossessedBy にて渡される AController を InventorySource に保持する。
				* プレイヤは Cast が成功して保持され、敵は nullptr となる。
			* アビリティの適用処理の際、プロパティ「 Inventory ＞ Sloted Abilities 」と InventorySource の参照先のインベントリの内容を反映させる。
			* これにより、プレイヤと敵のロジックの共通化を行っている。
			* また、そのため、敵にインベントリを持たせようと思えばそれも可能。
* 移動や GameplaySystem の相互作用について述べている。
	* 主に BP_Character::CanUseAnyAbility にてゲーム中の状態をもとに Ability の実行をしてよいか判断している事。
	* この部分はゲーム特有である事。
	* GameplayAbility のプロパティ「 Tags ＞ ActivationRequiredTags 」「 Tags ＞ ActivationBlockedTags 」は有益な可能性がある事。
* UI から AbilitySystem に問い合わせる方法について述べている。
	* **2019/02/28ごろに取得した ActionRPG のサンプルと2019/03/19現在のドキュメントの内容がマッチしていない**
		* **WB_OnSCreenControls には示された GrapNode はなく、 WB_OnScreenInput の On Click(ButtonSkill) がそれにあたると思われる。**
	* スキルを使用するボタンを押した後、クールダウンの情報を取得し、 UI に反映させている。


# ■ Adding a Random Amount of Soules Per Kill
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddSoulsPerKill

## ■ 概要
* 敵をキルした際に落とすソウルの数をランダムにするための拡張方法のサンプル。
* 現時点でダウンロードできるプロジェクトには **適用済みの内容** 。
* 説明している内容自体は AbilitySystem とは特に関係しない。
* Unreal Engine4 についてある程度知っているなら、読まなくても問題ないドキュメント。
	* コードを読む前にどこで何をしているか当たりをつけるために見ておくのもよい。

# ■ Adding A Pick Up
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddingAPickUp

## ■ 概要
* 回復用のアイテム配置用のアクターを追加する拡張方法のサンプル。
* 現時点でダウンロードできるプロジェクトには **適用されていない内容**。
* 説明している内容自体は AbilitySystem とは特に関係しない。
* Unreal Engine4 についてある程度知っているなら、読まなくても問題ないドキュメント。
	* コードを読む前にどこで何をしているか当たりをつけるために見ておくのもよい。
* 解説している流れはおおむね以下の通り
	1. Infinity Blade Weapons から骨付き肉のスケルタルメッシュをマイグレートしてくる
	1. Blueprint を Actor をベースに新規作成
	1. コンポーネントにコリジョンとスケルタルメッシュを追加、変数にポーションの種類を追加
	1. プレイヤーが触れたらインベントリにポーションを追加し、アイテムスロットに設定する処理を追加
	1. その他コリジョン関係の処理、アクターは期の処理の追加
	1. レベルに配置し動作を確認

# ■ Migrating Countent
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/MigratingContent

## ■ 概要
* マイグレーションの手順。
* 説明している内容自体は AbilitySystem とは特に関係しない。
* Unreal Engine4 についてある程度知っているなら、読まなくても問題ないドキュメント。

# ■ Adding a New Weapon
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddingaNewWeapon

## ■ 概要
* 武器を追加する拡張方法のサンプル。
* 現時点でダウンロードできるプロジェクトには **適用されていない内容**。
* AbilitySystem について少しだけ説明している。
	* 武器で使用できるアビリティの設定の GameplayAbility アセットの指定。
* Unreal Engine4 についてある程度知っているなら、読まなくても問題ないドキュメント。
	* コードを読む前にどこで何をしているか当たりをつけるために見ておくのもよい。
* 解説している流れはおおむね以下の通り
	1. Infinity Blade Weapons から「 SK_Dual_Blad**e**_Talon 」のスケルタルメッシュをマイグレートしてくる
		* 本文で **e** が抜けているので注意
	1. Blueprint を WeaponActor をベースに新規作成。
	1. スケルタルメッシュの指定、コリジョンのサイズの調整。
		* 解説に含まれないが、以下も行ったほうがよいと思われる。
			* CapsuleCollision (Inherited) のプロパティ「 Transform ＞ Location.z 」を 50 > **30**
	1. 作成した WeaponActor 派生 Blueprint をほかのデータと関連付けるための Data Asset の新規作成。
		1. Data Asset を RPGWeaponItem をベースに新規作成。
		1. 作成した WeaponActor 派生 Blueprint を関連付け
		1. ショップに表示する情報を設定
		1. ゲームルールに沿うように所持数上限などの設定
		1. 使用できるアビリティの指定（ほかの剣と同じ GA_PlayerSwordMelee を指定）
	1. レベルで動作を確認(ソウルをメニューで増やし購入、装備変更して使用できるかどうかの確認ができる)


# ■ Adding a New Potion
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddingaNewPotion

## ■ 概要
* 回復用のアイテムを追加する拡張方法のサンプル。
* 現時点でダウンロードできるプロジェクトには **適用されていない内容**。
* AbilitySystem について少しだけ説明している。
	* 新規の GameplayAbility と GameplayEffect を追加している。
* Unreal Engine4 についてある程度知っているなら、読まなくても問題ないドキュメント。
	* コードを読む前にどこで何をしているか当たりをつけるために見ておくのもよい。
* 解説している流れはおおむね以下の通り
	1. Asset Manager を利用しているため、アセットの配置パスに制限がある旨の説明がある。
	1. Blueprint を GA_PotionBase をベースに新規作成
	1. Blueprint を GE_PotionBase をベースに新規作成
	1. GA_PotionBase の設定
		1. 実行時の Montage の指定
		1. 実行時の Effect の指定（先ほど作成した GE_PotionBase の派生）
	1. GE_PotionBase の設定
		1. Modifier を追加し、対象を Mana に変更、回復量の指定
	1. 作成した GA_PotionBase 派生 Blueprint をほかのデータと関連付けるための Data Asset の新規作成。
		1. Data Asset を RPGPotionItem  をベースに新規作成。
		1. ショップに表示する情報を設定
		1. ゲームルールに沿うように所持数上限などの設定
		1. 使用できるアビリティの指定（先ほど作成した GA_PotionBase 派生）
	1. レベルで動作を確認(ソウルをメニューで増やし購入、装備変更して使用できるかどうかの確認ができる)


----
以上。
