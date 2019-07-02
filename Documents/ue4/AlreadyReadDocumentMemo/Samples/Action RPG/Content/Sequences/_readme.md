# ■ Sequences の内容
* レベルシークエンス関連のファイルが置かれている。
* ファイルはすべて LevelSequence 。

## ■ ファイル一覧
### ■ メインメニュー（タイトル画面）用

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| SQ_MainMenu | メインメニュー（タイトル画面）用。<br>炎の揺らめきを表現するために<br>ライトの強さをアニメーションさせている。 | ActionRPG_MAIN |

### ■ イントロ用
#### ■ シーン

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| Intro/SQ_Intro_Master | イントロ用レベルシークエンス本体。| ActionRPG_P |

#### ■ サブシーン
* SQ_Intro_Master で使用されているサブシーン。

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| Intro/SQ_Intro_Enemy_AnimData | Goblin の出現アニメーション。 | SQ_Intro_Master |
| Intro/SQ_Intro_Warrior_AnimData | Player の登場アニメーション。 | SQ_Intro_Master |

#### ■ ショット
* SQ_Intro_Master で使用されているショット。

| ファイル名 | 内容 | 参照元 |
| ----- | ----- | ----- |
| Intro/shots/SQ_Intro_Shot_001 | Player が入場するところを横から映すショット。 | SQ_Intro_Master |
| Intro/shots/SQ_Intro_Shot_002 | Player が立ち止まり、 Goblin のカメラの向きを変えるショット。 | SQ_Intro_Master |
| Intro/shots/SQ_Intro_Shot_003 | Goblin のスポーンアニメを映すショット。 | SQ_Intro_Master |


----
以上。

