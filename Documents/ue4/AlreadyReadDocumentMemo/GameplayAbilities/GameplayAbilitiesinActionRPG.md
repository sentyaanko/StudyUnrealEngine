# ■ Gameplay Abilities in Action RPG

**このファイルは書きかけです。**

## ■ このファイルは何？
公式の サンプル ActionRPG の解説ページについて簡単にまとめたもの。

# ■ GameplayAbilitiesinActionRPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG

## ■ 概要
* 公式のドキュメント。
* ドキュメントツリー上では配下に以下の12のドキュメントが置かれている。
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
* ActionRPGサンプルがどのように Gamplay Ability System を利用していて、同様のシステムを作る場合の例としての説明を述べている。
* コードの概要としてどのソースがどのような役割化を述べている。
* 所持アイテムとそれに紐づくアセットについてどのように管理しているか簡単に述べている。
* セーブデータの管理方法についてUE4の仕組みとともに述べている。
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
	* リソースを大量に持つようなBrueprintへのキャストを避ける。
	* 過度な循環参照を行うBlueprintを避ける。
	* C++ から直接アセットを参照するのを避ける。
	* 文字によるアセットの参照を避ける。
	* Blueprintでの enum/struct の定義を避ける。
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
**未着手**

# ■ Melee Abilities In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/MeleeAbilitiesInARPG

## ■ 概要
**未着手**

# ■ Skill Abilities In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/SkillAbilitiesInARPG

## ■ 概要
**未着手**

# ■ Executingg Abilities In ARPG
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG/ExecutingAbilitiesInARPG

## ■ 概要
**未着手**

# ■ Adding a Random Amount of Soules Per Kill
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddSoulsPerKill

## ■ 概要
**未着手**

# ■ Adding A Pick Up
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddingAPickUp

## ■ 概要
**未着手**

# ■ Migrating Countent
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/MigratingContent

## ■ 概要
**未着手**

# ■ Adding a New Weapon
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddingaNewWeapon

## ■ 概要
**未着手**

# ■ Adding a New Potion
https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/AddingaNewPotion

## ■ 概要
**未着手**


----
以上。
