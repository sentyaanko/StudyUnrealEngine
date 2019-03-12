# ■ 概略

## ■ このファイルは何？
「Gameplay Abiliity System」についてのまとめ。

## ■ 「Gameplay Abiliity System」とは？
正確な内容は下記の公式Wikiを参照していただいたほうが良いが、端的に言うならば、「ネットワークゲーム化を前提として設計されたActionRPGにおけるキャラクターのスキルを実装するための仕組み」ということになる。


### ■ [(Unreal Engine Documentation/Sample and Tutorials/Example Game Projects/Action RPG Game)Gameplay Abilities in Action RPG](https://docs.unrealengine.com/en-us/Resources/SampleGames/ARPG/GameplayAbilitiesinActionRPG)

### ■ [(Unreal Engine Wiki)GameplayAbilities and You](https://wiki.unrealengine.com/GameplayAbilities_and_You)
* KZJ氏の Unreal Engine Forums へ投稿された内容を Wiki にまとめたもの。
* 概念や使用方法についてサンプルを交えてまとめられている。

### ■ [(おかわりのアンリアルなメモ)GameplayAbilitiesの使い方(セットアップ編)](https://okawari-hakumai.hatenablog.com/entry/2018/07/22/165242)
* 利用方法のサンプル等。
* 主に 2. の内容をベースにまとめられている模様。
* 英語がつらい場合はこちらを。

# ■ クラス

## ■ AbilitySystemComponent
### ■ tooltip
```
The core ActorComponent for interfacing with the GameplayAbilities System.
GameplayAbilitiesシステムのインターフェイス用のコアActorComponent。
```
### ■ 使い方
* Actor に AbilitySystemComponent を AddComponent する。  
  その結果、プロパティ Abilities グループが追加される。
* プロパティ Abilities グループ にある Ability List に  
  GameplayAbility のサブクラスが登録できるようになる。  
  GameplayAbility については後述。
* Actor に AddComponent した AbilitySystemComponent に対して  
  GameplayAbility のサブクラスを指定してイベントを発火できる。  
  プロパティ Abilities グループ の Ability List に登録されていないものは発火されない。  
  が、特にエラーとしても扱われない。

## ■ GameplayAbility
### ■ tooltip
```
Abilities define custom gameplay logic that can be activated be player pf external game logic.
能力はカスタムゲームプレイロジックを定義します。 定義した能力はプレイヤーや外部のゲームロジックによって起動することができます。
```

### ■ 内容
* Actorが使用可能な能力を GameplayAbility サブクラスとして定義する。
* 能力を定義するためのもの。
* タグによる能力自体の管理
* イベント ActivateAbility にアビリティ起動時のノードを記述する。  
  CommitAbility ノードや EndAbility ノードを呼ぶことが多いと思われる。
* イベント OnEndAbility にアビリティ終了時のノードを記述する


### ■ 用途の例
ゲーム内のアクター（キャラクターとか）の能力そのもの。攻撃や回避等々。


## ■ GameplayCueNotify_Actor
### ■ tooltip
```
An instantiated AActor that acts as a handler of a gameplayCue.
Since they are instantiated, they can maintain state and tick/update every frame if necessary.
```

### ■ 内容
確認中。


## ■ AnimNotify
### ■ tooltip
なし。

### ■ 内容
確認中。



## ■ AnimNotifyState
### ■ tooltip
なし。

### ■ 内容
確認中。

----
以上。
