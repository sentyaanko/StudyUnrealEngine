# ■ git の設定メモ

## ■ 前提
* 以下のみを使って作業する場合のメモ
	* sourcetree
		* git の GUI および各ツールとして
	* TortoiseGit
		* git の GUI として
	* vs code
		* git の GUI として
		* エディタとして
	* windows
		* クライアント PC の OS として
	* github
		* git のサーバーとして

## ■ 実際に利用するものと、設定内容
* sourcetree
	* 同梱の git を利用する
	* 同梱の PuTTY ツールを利用する
	* 同梱の pagent.exe を立ち上げ、 github に登録してある公開鍵に対応した ppk を登録しておく
		* TortoiseGit/vs code にて ssh を使用する際に参照される。
	* global setting は利用しない。（自分の用途だとリポジトリごとにユーザを分けたりする必要があるため）
* TortoiseGit
	* 「全般＞ Git for Windows ＞ Git.exe へのパス」は sourcetree 同梱の git.exe があるパスを指定
	* 「 ssh クライアント」は sourcetree 同梱の TortoiseGitPlink.exe を指定
* vs code
	* 「 settings.json ＞ git.path 」は sourcetree 同梱の git.exe を指定
* windows
	* 環境変数「 GIT_SSH 」は sourcetree 同梱の TortoiseGitPlink.exe を指定
		* vs code にて git コマンド実行時に参照される
* github
	* 公開鍵は適当に作って登録

## ■ 前提
* クローン時は「 Clone with SSH 」を指定
* クローンを sourcetree/TortoiseGit でした後、ユーザの指定をしておく。（ global setting を利用しないため。）
	* たとえば vs code のターミナルでやる場合。
		* git.exe config --local user.name "my_user_name"
		* git.exe config --local user.email "my_mail_address@example.com"
	* sourcetree/TortoiseGit で GUI 上でやっても多分一緒。
* ここまでやっておけば、 sourcetree/TortoiseGit/vs code いずれからも git の操作ができる、はず。

## ■ git flow について

### ■ develop の過去のコミットに対してのリリース

例： 過去の `develop` のコミット `1234567` に対して `v0.0.1` のリリースをする場合

#### ■ SourceTree の GUI
`SourceTree` 上の `GitFlow` の `GUI` を利用すると、 `develop` の最新からのリリースしか行なえません。

#### ■ git flow を直に使う
`git flow` 自体の機能としては、 [git-flow-cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.ja_JP.html) によると、

> ```
> git flow release start RELEASE [BASE]
> ```
> `[BASE]` はオプションで 'develop'ブランチの特定のCommitのハッシュ値を指定します。指定がない場合はHEADが使われます。

とあり、今回の場合ならば

> git flow release start v0.0.1 1234567

とすれば、コミットを指定してリリース作業ができそうですが、 `SourceTree` に含まれる `git low` のバージョンの問題なのか、以下のようなエラーが発生します。

> Fatal: Base '1234567' needs to be a branch. It does not exist and is required.

それでは、と、 HEAD をコミット `1234567` にしておいた状態で `BASE` を省略すると

```
$ git flow release start --showcommands v0.0.1
git config --local gitflow.branch.release/v0.0.1.base develop
git checkout -b release/v0.0.1 develop
Previous HEAD position was 1234567 Merge branch 'feature/Update-0.0.1' into develop
Switched to a new branch 'release/v0.0.1'
```
`--showcommands` をつけて実際に動作させた `git` のコマンドを見ると、 現在の `HEAD` を無視して `develop` からリリース用のブランチを作成しています。

つまり、 `SourceTree` で利用できる `git flow` では特定のコミットからのリリースが出来ない、ということです。

> Note:追記  
> [git-flow-cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/index.ja_JP.html) はオリジナルの git flow のドキュメントです。  
> git flow のオリジナルはここ10年ほど更新されていません。  
> sourcetree に同梱されている git flow は avh 版と呼ばれているものです。  
> この辺りは問題というより、様々な問題に対応するための仕様の変更のようです。  
> ※そもそも過去のコミットに対する release は git flow のサポートの範疇外だったりします。  
> 　（特に既に master が進んでしまっている場合）  
> 　というのも、release finish は　master にマージをかけた後にタグを打ちます。  
> 　過去のコミットから作られたリリースを master のマージした後に打つタグに意味があるのか、という話になります。  
> ここで書かれている手順が利用できるケースを例に上げると、  
> 　v3 をリリースした後に develop にいくつかコミットした後、最後以外のコミットに対して v4 をリリースしたいケース、  
> となります。  
> もし、 v4 をリリースした後に v3.1 を作りたい、というケースでは support を使うのが良いようです。  
> [gitflow-avhのFAQ](https://github.com/petervanderdoes/gitflow-avh/wiki/FAQ) の一番下を参考にすると良いです。  

#### ■ 代替方法

```
# git flow release start v0.0.1 1234567 相当
git checkout -b release/v0.0.1 1234567

# git flow release finish v0.0.1 相当
git checkout master
git merge --no-ff release/v0.0.1
git checkout master
git tag -a v0.0.1
git checkout develop
git merge --no-ff v0.0.1
git branch -d release/v0.0.1

```

* `git merge` と `git tag` はメッセージ入力のため `vi` などが起動する。
    * `i` で挿入モード開始
    * 適当なメッセージを設定
    * `Esc` で挿入モード終了
    * `:wq` で保存終了
* 一部は `SourceTree` 上でも可能な操作。
    * というより、 `git merge --no-ff v0.0.1` 以外は可能。（ `SourceTree` 上ではタグを指定してのマージ操作ができない。）
* こういった `SourceTree` が想定していない手順を踏むケースでは `git flow` の `GUI` を使用しないほうがいい。
* 使用するとタグが作成されなかったり色々状態がおかしなことになる。


----
以上。
