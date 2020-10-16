# ■ BluePrints/AnimNotifies の内容
* AnimNotify と AnimNotifyState が格納されている
* **ファイルの命名規則が整っておらず、わかりづらい。**
* **AnimNotify の Recieved_NotifyBegin 等の戻り値の効果について、要確認**
* AnimNotify と AnimNotifyState で、似たようなものがあるケースについて
	* 例： SlomoNotify と SlomoNS
		* いきなり変えたい場合は SlomoNotify
		* 徐々に変えたい場合は SlomoNS
		* なお、SlomoNS という名前で Skeleton Notify のものがいくつかある。
		* **用途不明（ EventGraph にて Notify Event も作られていない）。要確認。**
			* Anim_Sword_Whirlwind
			* Combat_Blade_Swing_Far
			* Chestopen_kick
			* Death_Front
			* ExoGame_Greater_Spider_Death
* その他の問題
	* モンタージュセクションを利用した再生を行う場合の問題
		* 前置きとして、AnimNotifies にあるファイルの問題ではない
		* あるセクションを再生すると、次のセクションの先頭付近にある AnimNotify がまれに発生してしまう。
		* 具体例： AM_Atack_Sword の Combo3 を再生すると、 Combo4(に設定している Chestopen_Kick の 0 レーム（0.007 秒）)の SlomoNotify(AnimNotify)が発生する。


## ■ AnimNotify 一覧
| 名前 | 用途 | 参照元 |
| ----- | ----- | ----- |
| SlomoNotify | SetGlobalTimeDilation して、スロー再生にする<br>プレイヤー用 | AM_Skill_Combust(２回)<br>AM_Skill_Firewave(２回)<br>AM_Skill_Meteor(２回)<br>Anim_Sword_Whirlwind<br>**↑ 1.0 に設定している。ここでやるべきか要確認**<br>Chestopen_Kick<br>**↑ 1.0 に設定している。ここでやるべきか要確認**<br> |
| AN_MaterialEffect | マテリアルのパラメータ EffectColor の変更<br>プレイヤー用 | AM_Item_Potion<br>AM_Item_Potion_Mana |
| MoveForwardNotify | 指定量だけ前方に移動<br>プレイヤー用 | AM_Attack_Sword(Combo3/Combo4/Combo5) |
| Hit_Notify | マテリアルのパラメータ Target_Switch_On の変更<br>Goblin 用 | AM_Guardian_Falldown(0(２回)/1(２回))<br>React_Heavy_Front(２回)<br>React_Knockback_Front(２回) |
| Death_Notify | 自身に対して DelayDestroy の呼び出し<br>Goblin 用 | Death |
| CameraShakeNotify | 指定した CameraShake の PlayWorldCameraShake の呼び出し<br>Enemy_Anim_Sword_Combat_Swing は Goblin 用<br>上記以外はプレイヤー用 | AM_Attack_Axe(Combo3/Combo5)<br>AM_Attack_FireAxe(Combo3/Combo5)<br>AM_Attack_Hammer(Combo3)<br>AM_Skill_Combust<br>AM_Skill_Fireball<br>AM_Skill_Firewave(２回)<br>AM_Skill_Meteor(６回)<br>Anim_Blunt_Gound_Pound<br>Anim_Blunt_Gound_Pound_Fire<br>Anim_Sword_Whirlwind(２回)<br>Attack<br>Attack02_Fire<br>Attack03<br>Axe_Male_Anim_Sword_Combat_Swing<br>Axe_Swing_Near_Lt<br>Blunt_Swing_NearLT<br>Chestopen_Kick<br>Combat_Blade_Swing_Far(２回)<br>Male_Anim_Axe_Combat_Swing<br>Sword_Male_Anim_Level_Up_Transition(３回)<br>Sword_Male_Anim_Sword_Combat_Swing<br>Enemy_Anim_Sword_Combat_Swing |
| UseItemNS | 自身に対して指定の EventTag で SendGameplayEventToActor の呼び出し<br>プレイヤー用 | AM_Item_Potion<br>AM_Item_Potion_Mana |

## ■ AnimNotifyState 一覧
| 名前 | 用途 | 参照元 |
| ----- | ----- | ----- |
| StopAndStartAI_NS | 武器攻撃を受けた時に使用<br>**実行ノードが接続されていない。** 何かしらの理由で使用されていない模様。<br>繋がっていれば、 AI 動作の一時停止、移動の停止のように組まれている。<br>敵用 | AM_Spider_Hit<br>AM_Gradian_Falldown<br>AM_Guardian_Hit<br>React_Heaby_Front |
| WeaponAttackNS | 武器の WeaponAttack イベント呼び出し<br>(武器コリジョンの有効化、ヒット時処理用パラメータの引き渡し)<br>EventTag ： 武器が当たった際に発生させるイベント<br>AttackDelayCount ： hit 時にスロー再生になる回数<br>AttackDelayTime ： 未使用<br>プレイヤー・敵兼用 | AM_Attack_Axe(Combo1/Combo2/Combo4)<br>AM_Attack_FireAxe(Combo1/Combo2/Combo4)<br>AM_Attack_Hammer(Combo1/Combo2/Combo4)<br>AM_Attack_Sword(Combo1/Combo1-1/Combo2)<br>AM_Guardian_Attack |
| SlomoNS | SetGlobalTimeDilation によるスロー再生を行う<br>BeginSpeed ： 開始時の速度<br>EndSpeed ： 終了時の速度<br>bForceSlomo ： false かつ BP_PlayerCharacter::bEnableSlomo が false の場合、<br>begin 時に何もせず、 end 時に再生速度を 1.0 に戻す<br>ただし、現状では BP_PlayerCharacter::bEnableSlomo は常に true <br>(一度もセッターを呼ばれていないのでデフォルト値の true のまま)であるし、<br>そもそも現状の SlomoNS の呼び出しはすべて bForceSlomo=true のため、<br>この変数は機能していない。<br>プレイヤー用 | AM_Attack_Sword(Combo3/Combo4)<br>AM_Skill_Fireball(２回)<br>Attack02_Fire<br>Attack03 |
| MoveForwardNS | Tick にて指定された量を毎フレーム移動する<br>プレイヤー用 | AM_Attack_Sword(Combo1/Combo1-1/Combo2) |
| ShieldNS | 期間中、プレイヤーにアビリティエフェクト GE_DamageImmune を付与する<br>GE_DamageImmune は AbilityTag Status.DamageImmune を付与する。<br>AbilityTag Status.DamageImmune は GE_DamageBase の TargetTags::IgnoreTags に指定されている<br>GE_DamageBase の派生ではこの値の変更をしていない<br>つまり、期間中ダメージ処理用の AbilityEffect を受けなくなる<br>また、 BP_PlayerCharacter の OnDamaged 処理で、ダメージモーションに移行しない(ハイパーアーマー)<br>プレイヤー用 | AM_Attack_Axe(Cobo3/Cobo4)<br>AM_Attack_FireAxe(Cobo3/Cobo5)<br>AM_Attack_Hammer(Cobo3/Cobo4)<br>AM_Attack_Sword(Cobo3/Cobo4/Cobo5)<br>AM_Attack_Fireball<br>AM_Skill_Firewave |
| RangeAttackNS | 自身に対して指定の EventTag で SendGameplayEventToActor の呼び出し<br>**期間の処理があるわけでもないので、 UseItemNS と全く同じ（ EventTag のデフォルト値ぐらい）要確認**<br>プレイヤー・敵兼用 | AM_Attack_Axe(Combo3/Combo4)<br>AM_Attack_FireAxe(Combo3/Combo5)<br>AM_Attack_Hammer(Combo3/Combo4)<br>AM_Attack_Sword(Combo3/Combo4/Combo5)<br>AM_Skill_Combust(２回)<br>AM_Skill_Fireball<br>AM_Skill_Firewave<br>AM_Skill_Meteor<br>AM_Guadian_Attack02<br>AM_Spider_Melee(0/1/2) |
| JumpSectionNS | コンボ処理用<br>アニメーションモンタージュで期間中に別のセクションに再生を切り替えるための情報を設定する<br>開始時、自身に対してコンボ可能なことと、コンボの遷移先情報を渡し、終了時に解除する<br>オートプレイの場合は Tick 処理にて、自身に対して JumpSectionForCombo の呼び出し<br>プレイヤー用 | BP_PlayerCharacter<br>AM_Attack_Axe(Combo1->2/Combo2->3/Combo3->4.5)<br>**↑ Combo5 は存在しない。要確認**<br>AM_Attack_FireAxe(Combo1->2/Combo2->3/Combo3->4/Combo4->5)<br>AM_Attack_Hammer(Combo2->1/Combo1->3/Combo3->4/Combo4->4,5)<br>↑Combo4 へのルートが無い。<br>**Combo4 の設定が同じ 4 と存在しない 5 を指定している。要確認**<br>AM_Attack_Sword(Combo1->1-1/Combo1-1->2/Combo2->3,4,5) |
| BlockMoveInputNS | 期間中、プレイヤーに対して指定の BlockedMovement を true に変更<br>BlockedMovement==true の場合、BP_PlayerController の Tick 処理での移動処理が行われなくなる<br>プレイヤー用 | AM_Attack_Axe(Combo3)<br>AM_Attack_FireAxe(Combo3)<br>AM_Attack_Hammer(Combo3)<br>AM_Attack_Sword(Combo2)<br>AM_Item_Potion<br>AM_Item_Potion_Mana<br>AM_React_Hit(0/1)<br>AM_Skill_Combust<br>AM_Skill_Fireball<br>AM_Skill_Firewave<br>AM_Skill_Meteor |
| AN_VisibilityEffect | 敵の出現と消滅の際の処理<br>Tick 処理にてマテリアルパラメータ Visibility をカーブ Spawn に従って設定する<br>敵用 | ExoGame_Greater_Spider_Death<br>Death<br>Intro_Summon |

----
以上。
