# ■ Brueprints/Boss の内容
* ActionRPG 上のボスキャラであるクモに関する Blueprint が置いてある。

| ファイル名 | ネイティブ親クラス | 親クラス | 参照元 |
| ----- | ----- | ----- | ----- |
| NPC_SpiderBoss | RPGCharacterBase | BP_EnemyCharacter | WavesProgression |
| ABP_SpiderBoss | AnimInstance | 同じ | NPC_SpiderBoss |
| BS_SpiderBoss | BlendSpace | 同じ | ABP_SpiderBoss |


## ■ NPC_SpiderBoss
* クモの制御用 BP 。
* Data Table である WavesProgression の４レコード目に設定されている。
	* WavesProgression は５レコードあるが設定されているのは４レコード目のみ。
	* これで何故ボスなのか、要確認。
* ダメージを受けた際のマテリアルによる色変更処理をこの中で行っている。
	* Goblin は AnimNotify で行っているのに何故こちらは制御用の BP で行っているのか、要確認。
* 死亡時の Actor の Destroy を OnDeathEvent の中で行っている。
	* Goblin は AnimNotify で行っているのに何故こちらは制御用の BP で行っているのか、要確認。

## ■ ABP_SpiderBoss
* クモのアニメーション Blieprint 。
* UpdateAnimation イベントで以下のことを行っている。
	* 現在の移動量から移動アニメーションで使用する Speed の設定をしている。
	* Control と Actor の Yaw の差分から移動アニメーションで使用する Rotation Rate の設定をしている。
	* BP_Character から生存状態を取得し、 bDead に反映している。
* Goblin が持たない Stun という状態がある。利用していないようだが要確認。

## ■ BS_SpiderBoss
* クモの移動用 BlendSpace 。

----
以上。
