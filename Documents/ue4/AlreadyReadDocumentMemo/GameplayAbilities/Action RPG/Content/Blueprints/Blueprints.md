# ■ BluePrints の内容
* 用途によっていくつかのフォルダ分けがされている。
* この階層にもいくつか置かれている。

## ■ フォルダ一覧
| フォルダ名 | 用途 |
| ----- | ----- |
| AI | Blackboard 等、 AI モジュール類が置かれている。 |
| AnimNotifies | AnimNotify/AnimNotifyStats の派生が置かれている。 |
| Boss | Spider 用の BP が置かれている。 |
| CameraShake | Camera Shake の設定用の BP が置かれている。 |
| NPC | Goblin 用の BP が置かれている。 |
| Progression | インゲーム進行管理用のデータテーブルと BP structure が置かれている。 |
| SaveGame | SaveGame の派生と BP structure が置かれている。 |
| Weapon | 直下にプレイヤー用の、 Goblin フォルダ以下に Gobline 用の武器の BP が置かれている。 |
| WidgetBP | WidgetBP が置かれている。 |

## ■ BP 一覧
| 名前 | ネイティブ親クラス | 親クラス | 用途 |
| ----- | ----- | ----- | ----- |
| BP_Character | RPGCharacterBase | 同じ |
| BP_PlayerCharacter | RPGCharacterBase | BP_Character |
| BP_EnemyCharacter | RPGCharacterBase | BP_Character |
| BP_GameInstance | RPGGameInstanceBase | 同じ |
| BP_GameMode | RPGGameModeBase | 同じ |
| BP_GameState | RPGGameStateBase | 同じ |
| BP_MainMenuGameMode | GameMode | 同じ |
| BP_PlayerController | RPGPlayerControllerBase | 同じ |
| BP_RPGFunctionLibrary | BlueprintFunctionLibrary | 同じ |
| BP_SoulItem | Actor | 同じ |
| BP_SpectatorPawn | SpectorPawn | 同じ |


# ■  BP_Character
* プレイヤー・敵共用の Character BP 基底。
* プレイヤー・敵で共通のロジックを実装するための BP 。
* プレイヤー・敵用の Character はこの BP を派生している。

# ■  BP_PlayerCharacter
* プレイヤー用の Character BP 。
* モデル、カメラ、インベントリ画面用のカメラとライトなどのコンポーネントの設定をしている。
* EventGraph にて入力制御、武器の付け替え制御等を行っている。

# ■  BP_EnemyCharacter
* 敵用の Character BP 。
* HP ゲージ (WB_EnemyHP) やターゲットカーソル (WB_Target) 等のウィジェットコンポーネントの設定をしている。
* EventGraph にてウィジェット制御、 Soul のスポーン制御等を行っている。

# ■  BP_GameInstance
* アプリを通して保持しておくデータを管理するクラス。
* EventGraph にてインゲームのレベルロード、セーブデータの読み書き等を行っている。

# ■  BP_GameMode
* EventGraph にてアウトゲーム周りの状態遷移、敵の出現管理、一部の UMG の管理等を行っている。

# ■  BP_GameState
* 特に実装はない

# ■  BP_MainMenuGameMode
* MainMenu （起動直後のタイトル）用の GameMode BP 。
* EventGraph にて WB_Title のキャッシュの管理、オプション内容の反映等を行っている。

# ■  BP_PlayerController
* PlayerController クラス。
* EventGraph にてキャラクタ操作以外の入力制御、Tick にてキャラクタの移動処理、カットシーンの制御、攻撃用の UI の生成等を行っている。

# ■  BP_RPGFunctionLibrary
* BP Function Library 。
* 主に派生型へのキャスト処理が置かれている。

# ■  BP_SoulItem
* 敵を倒したときに出現する Soul 用の BP 。
* EventGraph にて出現後、プレイヤーに向かって移動する処理等を行っている。

# ■  BP_SpectatorPawn
* 観戦用の Pawn 。
* EventGraph にて視点の制御等を行っている。



----
以上。
