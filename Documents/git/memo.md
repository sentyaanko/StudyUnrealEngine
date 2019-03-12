# ■ git の設定メモ

## ■ 前提
* 以下のみを使って作業する場合のメモ
	* sourcetree
		* gitのGUIおよび各ツールとして
	* TortoiseGit
		* gitのGUIとして
	* vs code
		* gitのGUIとして
		* エディタとして
	* windows
		* クライアントPCのOSとして
	* github
		* gitのサーバーとして

## ■ 実際に利用するものと、設定内容
* sourcetree
	* 同梱のgitを利用する
	* 同梱のPuTTYツールを利用する
	* 同梱のpagent.exe を立ち上げ、githubに登録してある公開鍵に対応したppkを登録しておく
		* TortoiseGit/vs code にてsshを使用する際に参照される。
	* global setting は利用しない。（自分の用途だとリポジトリごとにユーザを分けたりする必要があるため）
* TortoiseGit
	* 「全般＞Git for Windows＞Git.exeへのパス」はsourcetree同梱の git.exe があるパスを指定
	* 「sshクライアント」はsourcetree同梱の TortoiseGitPlink.exe を指定
* vs code
	* 「settings.json＞git.path」はsourcetree同梱の git.exe を指定
* windows
	* 環境変数「GIT_SSH」はsourcetree同梱の TortoiseGitPlink.exe を指定
		* vs code にてgitコマンド実行時に参照される
* github
	* 公開鍵は適当に作って登録

## ■ 前提
* クローン時は「Clone with SSH」を指定
* クローンを sourcetree/TortoiseGit でした後、ユーザの指定をしておく。（global setting を利用しないため。）
	* git.exe config --local user.name "my_user_name"
	* git.exe config --local user.email "my_mail_address@exsample.com"
* ここまでやっておけば、sourcetree/TortoiseGit/vs code いずれからも git の操作ができる、はず。

----
以上。
