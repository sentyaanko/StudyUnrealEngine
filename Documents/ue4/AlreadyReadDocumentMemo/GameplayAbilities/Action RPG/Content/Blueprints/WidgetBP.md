# ■ BluePrints/WidgetBP の内容
* Widget Blueprint が置かれている。
* WidgetComponent Blueprint が置かれている。
* チェックボックスとボタンの設定が置かれている。
* 装備品や購入関連は Inventory フォルダ以下に置かれている。

## ■ BP 一覧
* すべてのネイティブ親クラスと親クラスは同じ。

| 名前 | 親クラス | 用途 | 参照元 |
| ----- | ----- | ----- | ----- |
| WB_CheckBox | CheckBox | チェックボックス基底 | WB_OptionsScreen |
| WB_GenericButton | Button | ボタン基底 | WB_EquipmentSlot<br>WB_InventoryItem<br>WB_InventoryList<br>WB_PurchaseItem |
| WB_DamageNumber | UserWidget | ダメージテキスト Widget | WC_DamageText |
| WC_DamageText | WidgetComponent | ダメージテキスト WidgetComponent<br>ゲームワールド表示用 | BP_EnemyCharacter |
| WB_EnemyHP | UserWidget | 体力バー Widget | BP_EnemyCharacter |
| WB_Target | UserWidget | チェック画像 Widget<br>用途不明<br>敵の頭上に表示 | BP_EnemyCharacter |
| WB_ButtonText | UserWidget | テキストボタン Widget | WB_Ingame_Finish<br>WB_OptionsScreen<br>WB_PauseMenu<br>WB_Equipment<br>WB_PurchaseConfirm |
| WB_PointsLabel | UserWidget | 所持ソウルパネル Widget | WB_OnScreenControls<br>WB_Equipment |
| WB_InputButton | UserWidget | 操作用ボタン Widget | WB_OnScreenControls<br>WB_OnScreenInput |
| WB_OnScreenInput | UserWidget | 操作用ボタンパネル Widget | WB_OnScreenControls |
| WB_OnScreenControls | UserWidget | 操作用 UI | BP_GameMode<br>BP_PlayerCharacter<br>BP_PlayerController |
| WB_SkipIntro | UserWidget | デモスキップ用 UI | BP_PlayerController |
| WB_OptionsScreen | UserWidget | オプション画面 | WB_Title<br>WB_PauseMenu |
| WB_Title | UserWidget | タイトル画面 | BP_MainMenuGameMode |
| WB_PauseMenu | UserWidget | ポーズ画面 | BP_GameMode |
| WB_WaveStart | UserWidget | Wave 開始画面 | BP_GameMode |
| WB_WaveEnd | UserWidget | Wave 終了画面 | BP_GameMode |
| WB_InGame_Finish | UserWidget | ゲーム終了画面 | BP_GameMode |
| Debug_UI | UserWidget | InGame Debug UI | BP_GameMode |
| WB_EquipmentSlot | UserWidget | 装備スロット用複合ボタン Widget | WB_Equipment<br>WB_InventoryItem<br>WB_InventoryList<br>WB_PurchaseItem |
| WB_InventoryItem | UserWidget | 所持アイテム用複合ボタン Widget | WB_InventoryList |
| WB_PurchaseItem | UserWidget | 購入アイテム用複合ボタン Widget | WB_InventoryList<br>WB_PurchaseConfirm |
| WB_InventoryList | UserWidget | 所持アイテム画面 | WB_EquipmentSlot<br>WB_InventoryItem<br>WB_PurchaseItem<br>WB_PurchaseConfirm |
| WB_PurchaseConfirm | UserWidget | 購入確認画面 | WB_InventoryItem<br>WB_PurchaseItem |
| WB_Equipment | UserWidget | 装備画面 | BP_PlayerController |

* 便宜上、用途については以下のルールで記載
	* ～～～基底： UMG で用意されてる UI パーツの設定（チェックボックスとボタン）
	* ～～～ Widget ：他の Widget から UI パーツとして利用されている Widget
	* ～～～ UI ：主としてインゲームに重ねて表示されている Widget
	* ～～～画面：利用時に画面を占有する形で利用されている Widget
	* ～～～ WidgetComponent ： BP 内で動的に生成する際のパラメータとして利用されている WidgetComponent

----
以上。
