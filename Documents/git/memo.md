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

----
以上。
