# 開発環境構築の手引書

# Macにインストールすべきもの

- Chrome
- Firefox
- Sublime Text
- Google日本語入力
- Slack

# ターミナルを通して揃えるもの

- homebrew
- nodebrew
- MySQL
- npmパッケージ
- sshの設定


## homebrew

以下のコマンドでインストールできる。

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

参考：  
[http://brew.sh/index_ja.html](http://brew.sh/index_ja.html)


## nodebrew

フロントエンドをやる上で必須。  
以下のコマンドでインストール。

```
$ curl -L git.io/nodebrew | perl - setup
$ echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> ~/.bash_profile && source ~/.bash_profile
```

参考：  
[http://gin0606.hatenablog.com/entry/2013/11/25/163607](http://gin0606.hatenablog.com/entry/2013/11/25/163607)

後は、設定していくだけ。```nodebrew -V```で使い方が表示される。


## MySQL

homebrewでインストール。Node.jsで使うのなら、npmパッケージもインストールする。

```
$ brew install mysql
$ npm install -S mysql
```

起動
```
$ mysql.server start
```

停止
```
$ mysql.server stop
```

## npmパッケージ

必要なパッケージをグローバルインストールしておく。以下は一例。

```
$ npm install -g mocha forever nodemon
```

その他、必要に応じてインストールしていく。```frontend```ディレクトリを参照。


## sshの設定

GitHubとの通信に必須。

まず、鍵を入れるフォルダに移動。そして、まだ鍵が存在しないことを確認。

```
$ cd ~/.ssh
$ ls
```

鍵を生成。

```
$ ssh-keygen -t rsa
```

このコマンドの後、エンターを押す。続いて、パスフレーズを2回求められるので、入力する。

これで、```id_rsa```と```id_rsa.pub```が生成される。

GitHubの設定ページにて、sshを登録。```id_rsa.pub```の中身を貼り付ければよい。  
以下のコマンドで、接続を確認できる。

```
$ ssh -T git@github.com
```

### macOS Sierra の場合

macOS Sierra では、sshを使ったリモートとの接続を行うために、さらに手続きが必要になる。```~/.ssh```に、```config```というファイルを作成し、以下のように記述する。

```
HostKeyAlgorithms +ssh-dss
Host *  
    UseKeychain yes
    AddKeysToAgent yes
```

参考：

- [gitHubでssh接続する手順~公開鍵・秘密鍵の生成から~ - Qiita](http://qiita.com/shizuma/items/2b2f873a0034839e47ce)
- [macOS Sierra で git pull できなかった話 - Qiita](http://qiita.com/totem2048/items/ec9d104a486e7a7f6243)
- [ssh鍵認証で毎回パスワードを求められた](http://blog.ikenie3.org/xibhuairunorokaraizu/)

### プロジェクト開始時のGitHubの設定

1. ```git init```でローカルリポジトリを作成
1. GitHubのページで、対応するリモートリポジトリを作成
1. ```git remote add origin リモートリポジトリのパス```
	- こうすると、リモートリポジトリを、```origin```という識別子で登録できる。
1. ```git push -u origin リモートリポジトリのブランチ名```
	- こうすると、現在のブランチの内容を、リモートリポジトリにプッシュする。
	- ```-u```オプションをつけることで、ローカルとリモートを上手く紐付けてくれる。
1. ```vim .gitignore```で、```ignore```の設定を行う

