# ■ Brueprints/CameraShake の内容
カメラを揺らすための Blueprint が置いてある。

## ■ BP 一覧
* すべてのネイティブ親クラスと親クラスは CameraShake になっている。

| 名前 | Notifies での指定 |
| ----- | ----- |
| BP_CameraShake | AM_SkillFirewave(１回)<br>AM_Skill_Meteor(２回)<br>Anim_Blunt_Gound_Pound(１回)<br>Anim_Blunt_Gound_Pound_Fire(１回)<br>Attack02_Fire(１回)<br>Attack03(１回)<br>Sword_MaleAnim_Level_Up_Transition(４回) |
| camera_shake_Skill | AM_Skill_Firewave(１回) |
| camera_shake_small | AM_Skill_Combust(１回)<br>AM_Skill_Fireball(１回)<br>AM_Skill_Meteor(４回)<br>Anim_Sword_Whirlwind(２回)<br>Attack(１回)<br>Axe_Male_Anim_Sword_Combat_Swing(１回)<br>Axe_Swing_Near_Lt(１回)<br>Blunt_Swing_Near_Lt(１回)<br>Chestopen_Kick(１回)<br>Combat_Blade_Swing_Far(２回)<br>Male_Anim_Axe_Combat_Swing(１回)<br>Sword_Male_Anim_Sword_Combat_Swing(１回)<br>Enemy_Anim_Sword_Combat_Swing(１回) |

## ■ 設定内容の差異

| 名前 | Oscillation<br>Duration | Oscillation<br>Blend in Time | Oscillation<br>Blend Out Time | Rot Oscillation | FOVOscillation |
| ----- | ----- | ----- | ----- | ----- | ----- |
| BP_CameraShake | 0.8 | 0.5 | 0.2 | Pitch Amplitude:5.0<br>Pitch Frequency:50.0 | Amplitude:2.0<br>Frequency:3.0<br>Initial Offset:Random |
| camera_shake_Skill | 1.15 | 1.0 | 0.3 | | Amplitude:60.0<br>Frequency:1.0<br>Initial Offset:Zero |
| camera_shake_small | 0.3 | 1.0  | 0.2 | Pitch Amplitude:2.0<br>Pitch Frequency:100.0<br>Yaw Amplitude:2.0<br>Yaw Frequency:100.0<br>Roll Amplitude:2.0<br>Roll Frequency:100.0 | Amplitude:1.0<br>Frequency:1000.0<br>Initial Offset:Random |

* camera_shake_Skill は画角による振動（FOVOscillation）のみの設定。
* BP_CameraShake はそれに加えてピッチの回転（Rot Oscillation）も行う。
* camera_shake_small はそれに加えてヨー・ロールの回転も行う。

----
以上。
