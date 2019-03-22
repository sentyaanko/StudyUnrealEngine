# ■ Summary

**このファイルは書きかけです。**

## ■ このファイルについて
「 Gameplay Abiliity System 」について実作業にあたってまとめた資料。

# ■ クラス

## ■ AbilitySystemComponent
### ■ tooltip
```
The core ActorComponent for interfacing with the GameplayAbilities System.
GameplayAbilities システムのインターフェイス用のコア ActorComponent 。
```
### ■ 使い方
* Actor に AbilitySystemComponent を AddComponent する。  
  その結果、プロパティ Abilities グループが追加される。
* プロパティ Abilities グループの Ability List に  
  GameplayAbility のサブクラスが登録できるようになる。  
  GameplayAbility については後述。
* Actor に AddComponent した AbilitySystemComponent に対して  
  GameplayAbility のサブクラスを指定してイベントを発火できる。  
  プロパティ Abilities グループの Ability List に登録されていないものは発火されない。  
  が、特にエラーとしても扱われない。

## ■ GameplayAbility
### ■ tooltip
```
Abilities define custom gameplay logic that can be activated be player pf external game logic.
能力はカスタムゲームプレイロジックを定義します。 定義した能力はプレイヤーや外部のゲームロジックによって起動することができます。
```

### ■ 内容
* Actor が使用可能な能力を GameplayAbility サブクラスとして定義する。
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
