# ■ GameplayAbilitySystem

**このファイルは ActionRPG のサンプルを見る前に書いたものなので不完全です。**

## ■ このファイルについて
公式の GameplayAbilitySystem の概要ページについて簡単にまとめたもの。

# ■ GameplayAbiliitySystem
https://docs.unrealengine.com/en-us/Gameplay/GameplayAbilitySystem

## ■ 概要
* 公式のドキュメント。システムの概要とプラグインの導入方法がまとめられている。
* ドキュメントツリー上では配下に以下の３つのドキュメントが置かれている。

# ■ GameplayAttributesAndGameplayEffects
https://docs.unrealengine.com/en-us/Gameplay/GameplayAbilitySystem/GameplayAttributesAndGameplayEffects

## ■ 概要
* GameplayAttributes と GameplayEffects の概要がまとめられている。
* GameplayAttributes は「ゲームルール内の属性値である」「C++ で実装する必要がある」といったことがまとめられている。
* GameplayEffects については「ゲームルール内の属性値に影響をあたるものである」「 BluePrint 上の主なプロパティの意味」といったことがまとめられている。

## ■ BluePrint 上の主なプロパティの意味
* Duration
	* そのまま、継続時間。
	* エフェクト等のタイミング制御にも利用。
* Modifiers
	* GameplayEffects がどのように GameplayAttributies に影響するかを設定する。
* Executions
	* Modifiers のプリセット的な機能では表現できない GameplayAttributies の操作を行いたい場合はこちらを使用する。
* Application Requirements
	* GameplayEffects の効果を適用するかの制限を行えるらしい。
	* 拡張するには C++ で UGameplayEffectCustomApplicationRequirement から派生させて実装する。
	* どのように制限をかけることができるかは要調査。
		* サンプルを見るのがよさげ。
* Granted Abilities
	* 例えば「火炎攻撃」は「オイルを被った状態の敵」に対して「燃焼ダメージ（パーティクル等のエフェクト付き）」を付与（ Grant ）する為の設定を行うもの、らしい。
		* 「火炎攻撃」自体はこの Gameplay Effects の特性、それとも Gameplay Abilities を見て判断、のどちらか。
			* （通常攻撃に火炎属性を付与されている状態か、など）
		* 「オイルを被った状態の敵」という判断はどこで行うのか。受け側か？
		* 「燃焼ダメージ（パーティクル等のエフェクト付き）」を Granted Abilities で設定するのか？
	* 上にあげた例をどのようにすれば表現できるのか、要調査。
		* サンプルを見るのがよさげ。
* Stacking
	* いわゆる毒など、スタックがたまり切った時に何かを行うなどを表現するときに利用するらしい。
	* が、スタックだけを表して毒ダメージ自体を別にするにはどうするのかなど、具体的な方法が（ドキュメント、プロパティ内容いずれからも）読み取れない。
		* サンプルを見るのがよさげ。
* Gameplay Cue Display
	* ネットワークを考慮した、(パーティクルや音の)エフェクト制御の仕組みを Gameplay Ability System で行うための設定項目。
	* GameplayEffects の設定の中で Gameplay Cue の設定を行う際、タグの命名規則として「"GameplayCue."から始めること」とある。
		* 現状作成済みのサンプルではそれに沿っていないので調整すること。
		* GameplayCueNotify_Actor 派生クラスを利用しているので、反応できているのだろうか？
	* GameplayCue Manager や IGameplayCueInterface が関連しているらしい。シングル、マルチでも状況が異なるらしい。要調査。
		* サンプルを見るのがよさげ。

## ■ USimpleAttributeSet のインタフェースの用途
* PreAttributeChange/PreAttributeBaseChange
	* Attribute を変更する直前に呼ばれる。
	* 値の範囲チェックなどを行う場合に利用する。(0-255 に抑制する、など)
	* ゲームの反応を起こしてはいけない。(エフェクトを発生させる、など)
* PreGameplayEffectExecute
	* 値を反映する直前に呼ばれる。
	* 提案された変更を拒否または変更が可能。
* PostGameplayEffectExecute
	* 変更の結果、何らかの反応を起こすために利用する（死亡処理、エフェクト処理など）。

# ■ GameplayAbility

## ■ 概要
* https://docs.unrealengine.com/en-us/Gameplay/GameplayAbilitySystem/GameplayAbility
* AbilitySystemComponent のインタフェースについての説明。
* GameplayAbility のプロパティについての説明。

## ■ AbilitySystemComponent のインタフェース
* 追加
	* GiveAbility
* 削除
	* ClearAbility
	* SetRemoveAbilityOnEnd
	* ClearAllAbilities

## ■ AbilitySystemComponent に付与された Ability のライフサイクルについての説明。
* CanActivateAbility
	* Ability が実行可能かを調べるために呼ぶことができる。実際には実行されない。
* CallActivateAbility
	* Ability を実行するために呼ぶことができる。その際、利用可能かなどのチェックは行われない。
		* サンプルを見るのがよさげ。
* TryActivateAbility
	* CanActivateAbility => CallActivateAbility と呼び出す。
* EndAbility
	* Ability が正常に終了した場合に開発者が自主的に呼び出す。
	* 異常終了以外はこれを呼ばないと完了した扱いにならない。

## ■ GameplayAbility のタグについての説明
アビリティを実行できるかどうかを判断するためのタグの仕組みの説明。

| Gameplay Tag Variable(s) | Purpose |
| ----- | ----- |
| Cancel Abilities With Tag | ここで指定したタグを持つ実行中のアビリティをキャンセルする |
| Block Abilities With Tag | ここで指定したタグを持つアビリティの実行を防ぐ |
| Activation Owner Tags | ここで指定したタグをアビリティ実行中 Owner Actor に持たせる |
| Activation Required Tags | ここで指定したすべてのタグを、 Owner Actor or Component が持っているときに限り実行できる |
| Activation Block Tags | ここで指定したいずれかのタグを、 Owner Actor or Component が持っているとき実行を防ぐ |
| Target Required Tags | ここで指定したすべてのタグを、 Target Actor or Component が持っているときに限り実行できる |
| Target Blocked Tags | ここで指定したいずれかのタグを、 Target Actor or Component が持っているとき実行を防ぐ |

## ■ GameplayAbility の Replication と Gameplay Net Execution Policy
ネットワーク帯域と CPU 占有率調整のための Gameplay Ability の複製ポリシーの仕組みの説明。

| Advanced/Net Execution Policy の各値 | 意味 |
| ---- | ---- |
| Local Predicted | ローカルでも予測して処理する方法。サーバーから予測を反した返答がない限りはスムーズに見える。 |
| Local Only | ローカルで実行する方法。サーバーからの修正を受ける可能性もありその場合は通常のレプリケーションプロトコルに従う。 |
| Server Initiated | サーバーで実行を開始する方法。素早く実行される行動は遅延を感じる可能性がある。 |
| Server Only | サーバーでのみ実行する。クライアントはサーバーから伝播された複製された変数を観察する。 |

## ■ GameplayAbility の Instancing Policy
GameplayAbility 実行 Actor が多い場合のオブジェクト生成負荷調整のためのインスタンス化ポリシーの仕組みの説明。

| Advanced/Instancing Policy の各値 | 意味 |
| ---- | ---- |
| Instanced per Execution | 実行ごとにインスタンス化する方法。まれに実行するアビリティ（ Ult とか)に向く。 |
| Instanced per Actor | インスタンス化した Actor を使いまわす方法。 |
| Non-Instanced | インスタンス化しない Actor を使う方法。 ClassDefaultObject を利用する。プロパティ値を個別に設定できない。 BasicAttack 等に向く。 |

## ■ Gameplay の Event について
* GameplayAbility 直接 Ablity をトリガーする方法と、その際に渡すことができる FGameplayEventData ついての説明。  
	* 独自のデータを渡したい場合は FGameplayEventData::ContextHandle polymorphic を利用する。
	* その場合、 ActivateAbility を使わずその代わりに ActivateAbilityFromEvent を使うことになるらしい。
		* 正直に何のどこを指しているのか不明瞭。
		* サンプルを見るのがよさげ。

# ■ AbilityTasks
https://docs.unrealengine.com/en-us/Gameplay/GameplayAbilitySystem/AbilityTasks

## ■ 概要
* C++ の UAbilityTask の解説
* 主にアビリティのロジックを非同期実行する際に利用するもの。
* 入力とアニメーションを別のタスクにしてどちらかが終了したらアビリティを完了するなどの利用例が記載されているが、ドキュメントが少ない。
	* サンプルを見るのがよさげ。

----
以上。
