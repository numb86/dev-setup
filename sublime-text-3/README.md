# Sublime Textの設定

## package control

まずはこれを入れないと話にならない。

ここからダウンロードする。  
[https://packagecontrol.io/installation](https://packagecontrol.io/installation)

そしてそれを、
```
~/Library/Application Support/Sublime Text 3/Installed Packages
```
に置く。

参考：  
[http://sumikko.hateblo.jp/entry/2015/04/02/151142](http://sumikko.hateblo.jp/entry/2015/04/02/151142)

## インストールすべきパッケージ

- [https://github.com/timonwong/OmniMarkupPreviewer](https://github.com/timonwong/OmniMarkupPreviewer)
- [https://github.com/babel/babel-sublime](https://github.com/babel/babel-sublime)
- [https://github.com/odyssomay/sublime-lispindent](https://github.com/odyssomay/sublime-lispindent)


## キーバインドの設定ファイル

編集済みのキーバインドの設定ファイル```Default (OSX).sublime-keymap```を、このディレクトリに置いておく。  
これを
```
~/Library/Application Support/Sublime Text 3/Packages/Default/Default (OSX).sublime-keymap
```
と配置すると、下記の設定を全て行った状態になる。


## キーバインド

デフォルトだと、日本語の入力に支障が出る。そのため、キーバインドの設定変更が不可欠。  
具体的には、タブキーが使えないので、それを変更する。

コマンドパレット（```cmd+shift+p```）から```key bindings```を選ぶ。  
開いたファイルを保存すると、
```
~/Library/Application Support/Sublime Text 3/Packages/Default/Default (OSX).sublime-keymap
```
が出来る。  
それを編集していくことで、キーバインドを変えられる。

タブキーに関する部分を、コメントアウト。```insert_best_completion```で検索すると、見つけやすい。

```json
	{ "keys": ["tab"], "command": "insert_best_completion", "args": {"default": "\t", "exact": true} },
	{ "keys": ["tab"], "command": "insert_best_completion", "args": {"default": "\t", "exact": false},
		"context":
		[
			{ "key": "setting.tab_completion", "operator": "equal", "operand": true },
			{ "key": "preceding_text", "operator": "regex_match", "operand": ".*[^0-9]$", "match_all": true },
		]
	},
```

これで完了。  
もし動かなかったら、Sublime Textを再起動してみる。


### ctrl+k

さらに、先程のファイルの683行付近にある```ctrl+k```に関する部分をコメントアウト。

```json
{ "keys": ["ctrl+k"], "command": "run_macro_file", "args": {"file": "res://Packages/Default/Delete to Hard EOL.sublime-macro"} },
```


### 検索での日本語入力の有効化

検索ボックスで日本語入力が出来ない。

これも、先程のファイルを編集する。  
該当箇所は3箇所。```Find panel key bindings```、```Replace panel key bindings```、```Incremental find panel key bindings```。  
それぞれ、エンターに関する3行の記述があるので、そこをコメントアウトする。

こうすると日本語入力は出来るが、エンターで次を検索することが出来ない。これは、```cmd+g```で代用できる。