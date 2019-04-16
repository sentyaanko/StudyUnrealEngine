# ■ FileList

## ■ このファイルについて
 フォルダ構成について調査したものです。

# ■ 階層ごとのドキュメント一覧
* Content
	* Abilities
		* [DataTables](Content/Abilities/DataTables.md)
		* [Enemies](Content/Abilities/Enemies.md)
		* [Player](Content/Abilities/Player.md)
		* [Shared](Content/Abilities/Shared.md)
	* Animations
		* [Boss.md](Content/Animations/Boss.md)
		* [NPC.md](Content/Animations/NPC.md)
	* Assets
		* Sounds
			* [Abilities.md](Content/Assets/Sounds/Abilities.md)
			* [Ambient.md](Content/Assets/Sounds/Ambient.md)
			* [AudioClasses.md](Content/Assets/Sounds/AudioClasses.md)
			* [Character.md](Content/Assets/Sounds/Character.md)
			* [Concurrency.md](Content/Assets/Sounds/Concurrency.md)
			* [Creatures.md](Content/Assets/Sounds/Creatures.md)
			* [Music.md](Content/Assets/Sounds/Music.md)
			* [UI.md](Content/Assets/Sounds/UI.md)
			* [Weapons.md](Content/Assets/Sounds/Weapons.md)
	* Blueprints
		* [_readme.md](Content/Blueprints/_readme.md)
		* [AI.md](Content/Blueprints/AI.md)
		* [AnimNotifies.md](Content/Blueprints/AnimNotifies.md)
		* [Boss.md](Content/Blueprints/Boss.md)
		* [CameraShake.md](Content/Blueprints/CameraShake.md)
		* [NPC.md](Content/Blueprints/NPC.md)
		* [Progression.md](Content/Blueprints/Progression.md)
		* [SaveGame.md](Content/Blueprints/SaveGame.md)
		* [Weapon.md](Content/Blueprints/Weapon.md)
		* [WidgetBP.md](Content/Blueprints/WidgetBP.md)
	* Characters
		* [_readme.md](Content/Characters/_readme.md)
		* [Animations.md](Content/Characters/Animations.md)
		* [Barbarous.md](Content/Characters/Barbarous.md)

# ■ ファイル一覧
## ■ Content/Abilities フォルダ
```
Abilities
├─DataTables
│  アビリティ用のデータテーブル置き場
│
├─Enemies
│ │敵をカテゴリごとにフォルダ分けしたものを置くための場所
│ │
│ ├─Goblin
│ │  ゴブリン用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│ │
│ └─Spider
│    クモ用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│
├─Player
│ │武器毎にフォルダ分けしたものを置くための場所
│ │スキル・ポーションのフォルダもある。
│ │パラメータ初期化のための GameplayEffect も置いてある
│ │
│ ├─Axe
│ │  Axe 用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─FireAxe
│ │  FireAxe 用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─Hammer
│ │  Hammer 用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─Potions
│ │  ポーション用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│ │
│ ├─Skills
│ │  スキル用のアビリティ用ＢＰ(Actor/GameplayAbility/GameplayEffect)置き場
│ │
│ └─Sword
│    Sword 用のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
│
└─Shared
   プレイヤー、敵で共用のものや基底のアビリティ用ＢＰ(GameplayAbility/GameplayEffect)置き場
```

## ■ Content/Animations フォルダ
```
Animations
├─Boss
│  Spider の Animation Montage 置き場。
│
└─NPC
   Guardian(=Goblin) の Animation Montage 置き場。
```

## ■ Content/Assets フォルダ
```
Assets
└─Sounds
  ├─Abilities
  │  Fireball 等のプレイヤースキル用の Sound Wave と Sound Cue
  │
  ├─Ambient
  │  松明や風などの環境陰陽の Sound Wave と Sound Cue と Sound Attenuation
  │
  ├─AudioClasses
  │  ボリューム等制御用の Sound Class と Sound Mix
  │
  ├─Character
  │  プレイヤーキャラクターのアクション時のボイスや、足音やポーション等の SE の Sound Wave と Sound Cue
  │
  ├─Concurrency
  │  同時再生数などを制御する Sound Concurrency
  │
  ├─Creatures
  │ ├─Guardian
  │ │  Guardian(=Goblin)のアクション時のボイスや、足音や攻撃、被ダメージ等の SE の Sound Wave と Sound Cue
  │ │
  │ └─Spider
  │    Spider のアクション時のボイスや、足音や攻撃、被ダメージの等 SE の Sound Wave と Sound Cue
  │
  ├─Music
  │ │  タイトルとゲーム中の BGM の Sound Wave と Sound Cue
  │ │
  │ └─Stingers
  │    ゲームオーバー時の BGM の Sound Wave と Sound Cue
  │
  ├─UI
  │  UI 用の Sound Wave と Sound Cue
  │
  └─Weapons
    │  炎を纏った剣のスイング用の Sound Wave と Sound Cue
    │  サブフォルダにある音はその武器専用というわけではなく、モーション側から合う音を再生している
    │  Widget からも再生している
    │
    ├─Axe
    │  Axe のスイング用の Sound Wave と Sound Cue
    │
    ├─Hammer
    │  Hammer スイング用の Sound Wave と Sound Cue
    │
    └─Sword
       Sword のスイング用の Sound Wave と Sound Cue
```

## ■ Content/Blueprints フォルダ
```
Blueprints
│ GameMode/GameState/Character 基底等
│
├─AI
│ │  Blackboard 等、 AI モジュール類
│ │
│ ├─BossAI
│ │  Spider 用
│ │
│ ├─GruntAI
│ │  Goblin 用
│ │
│ └─PlayerAI
│    Player 用（オートプレイ時）
│
├─AnimNotifies
│  アニメーション通知関連
│
├─Boss
│  Spider 用の Blueprint
│
├─CameraShake
│  カメラを揺らす設定関連
│
├─NPC
│  Goblin 用の Blueprint
│
├─Progression
│  敵の出現テーブルとその型
│
├─SaveGame
│  ストレージへの保存の際の型関連
│
├─Weapon
│ │  Player 用、基底用
│ │
│ └─Goblin
│    Goblin 用（オートプレイ時）
│
└─WidgetBP
  │  共用 Widget
  │
  └─Inventory
     装備・購入関連
```

## ■ Content/Characters フォルダ
```
Characters
│  Player の Animation Blueprint/Skeleton/BlendSpace/PhysicsMaterial など
│
├─Animations
│  Player のアニメーションモンタージュ、アニメーションシーケンスなど
│
└─Barbarous
  │  Player のスケルタルメッシュ
  │
  └─Texture_Material
     Player のテクスチャとマテリアル
```




----
以上。
