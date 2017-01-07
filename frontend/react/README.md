# Reactの開発に必要なもの


## パッケージ

必要なnpmパッケージをインストール。

```
$ npm install -S react react-dom
```


## ビルド

ビルドについて。ファイルのバンドル、JSXのプリコンパイル、ES2015のトランスパイラ、などが必要になる。

順序としては、```babelify```のインストール、プリセットのインストール、プリセットの設定、となる。

```
$ npm install -D babelify babel-preset-es2015 babel-preset-react
```

この後、ルートディレクトリでプリセットの設定を行う。

```
$ echo '{ "presets": ["react", "es2015"] }' > .babelrc
```

そうすると、以下のコマンドでビルドできる。

```
$ browserify -t babelify 元となるファイル -o ビルドするファイル
```

ビルドを```npm scripts```のみで行うのなら、```.babelrc```を作成しなくても、```package.json```に記載すればよい。

```json
"babel": {
  "presets": [
  	"react",
    "es2015"
  ]
},
```


### watchify

現実的には、```watchify```を登録して使うのが簡便。

まずはインストール。
```
$ npm install -D watchify
```

その後、```package.json```に、以下の記述を追加。

```json
{
  ･･･
  "scripts": {
	  ･･･
    "watch": "watchify -t babelify 元となるファイル -o ビルドするファイル",
	  ･･･
  },
  ･･･
}
```

そうすると```npm run watch```を実行しておけば、ファイルを保存する度に自動的にビルドしてくれる。  
また、シンタックスエラーがあれば、ビルドの段階でエラーを出してくれる。


### 本番環境へのビルド

必要なパッケージ、```envify```と```uglify-js```をインストール。

```
$ npm install -D envify uglify-js
```

その後、```package.json```の```script```に、以下の記述を追加。

```json
"product": "NODE_ENV=production browserify 元となるファイル -t babelify -t envify | uglifyjs -c warnings=false > ビルドするファイル",
```

これで、```npm run product```を実行すると製品版としてビルドしてくれる。


## テスト

テストツール```jest```をインストール。

```
$ npm install jest -D
```

次に、```package.json```を編集。
```json
{
  ･･･
  "scripts": {
	  ･･･
    "test": "jest",
	  ･･･
  },
  ･･･
}
```

- ```shallow()```や```mount()```、```simulate('click')```を使うために必要な```enzyme```
- ```enzyme```を使うために必要な```react-addons-test-utils```

この２つをインストール。

```
$ npm install -D enzyme react-addons-test-utils
```

そして```jest```のスナップショットを使うために、```enzyme-to-json```をインストール。

```
$ npm install -D enzyme-to-json
```