# ■ Items/Potions の内容
* Potion 用の DataAsset ファイルが置かれている。

## ■ ファイル一覧
* 親クラスはすべて RPGPotionItem

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| Potion_DeathsDoor | DeathsDoor 用のデータアセット | BP_Potion_PickUp<br>ActionRPG_Dungeon02_Asset |
| Potion_Health | HealthPotion 用のデータアセット<br>プレイヤーのオートプレイ時の BehaviorTree にて、<br>体力減少時に使用するアイテムとして参照される | BP_Potion_PickUp<br>BT_Player |
| Potion_Mana | ManahPotion 用のデータアセット | BP_Potion_PickUp<br>ActionRPG_Dungeon02_Asset |


----
以上。

