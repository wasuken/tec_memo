# LazyBlogを更新した

## 現時点で行った修正

### 記事取得をAPI化

/api/pageにパラメタをいれてやると絞り込みだったり、ソートできるようにした。

トップページを読み込む際にサーバサイドでの処理がほぼ消えた(非同期処理は除く)ので

Controllers/PageControllerはほとんど消した。

しかし、それ以上にApi/PageControllerがめちゃくちゃ太った。

あと前より細かい検索ができるようになった分、検索処理が重くなった。

### トップページのVue.js化

上記APIから非同期で記事データを取得。

とりあえず思うがままに書いてみようとしたら、いくつかの箇所で状態を共有したほうがいいかな？ってところがあったので、

Vuexを採用した。思ったよりもきつくなかった。ReactとReduxの組み合わせよりよっぽど楽(規模も規模だしね)。

### 記事更新機能を追加

実装自体は楽だったんだけど、テスト書いてるときのテーブルの結合処理で

テーブル名クッソ間違えてイライラしてた。

### JSテストのための環境の構築をしたり、テストを書いた

ほんの少ししかかけてないけど、

ここが一番の難所だったかもしれない。

テスト自体というよりは、babelやらnode周りがきつかった。

#### どのパッケージをいれればいいんだ問題

当然全然わからんので、ぐぐったものを真似しようとしても、動かない。

最初の一行(import)でエラー吐いた。トランスパイルの問題かなって思ったので、ググっていくと

babel-jestを入れ炉みたいなこと書いてあったので、それをいれてみるが、ダメッ...!

紆余曲折を経て、ようやく動くようになった。

説明はめんどいのでソースから抜粋する。

> package.json

```

~
"jest": {
    "moduleFileExtensions": [
        "js",
        "json",
        "vue"
    ],
    "transform": {
        "^.+\\.vue$": "<rootDir>/node_modules/vue-jest",
        "^.+\\.js$": "<rootDir>/node_modules/babel-jest"
    },
    "testRegex": "resources/js/test/.*.js$"
},
~

```

> .babelrc

```

{
  "presets": [["env", { "modules": false }]],
  "env": {
    "test": {
      "presets": [["env", { "targets": { "node": "current" } }]]
    }
  },
  "plugins": [
    ["transform-object-rest-spread"]
  ]
}

```

このソースを元に以下より私がうっざ！と思ったところだけを記載していく。

##### スプレッド構文のエラー

```

{
	...hoge
}

```

みたいな構文はもはや当たり前に使うわけだが、なんかbabel-preset-es2015をいれた程度じゃ

使えないみたいだ。いや、es2016以降のどっかにはあるかもしらんが。

この構文を有効にする方法の一つには、

```

~
"plugins": [
  ["transform-object-rest-spread"]
]
~

```

を.babelrcに追加する方法がある。

これは

[reactjs - IE / EdgeのBabel 7スプレッド構文が機能しない - ITツールウェブ](https://ja.coder.work/so/reactjs/1531530)

ここを参考にした。

##### fetchが見つからない

これもbabelの場合に発生した。正直JS全然わからんってなってる。

これに対する私の対処法は、すごい力技なんだけど、

まず、node-fetchをインストールして、

テストコードの一番上で

```

global.fetch = require('node-fetch');

```

をするだけ。

まあ、こんなのがいやならaxios使ったほうがいいと思う。日本では圧倒的に人気っぽいからね。

----

こんな感じで適当にぱぱっとやったら動いた。Vuexのテストは知らん。まだ書いてない。

## これから行う予定の修正

* まともな検索エンジンの実装(Grep検索になってたりいろいろひどい)

* JSテストの追加(特にVuex周り)

* リファクタリング(厳密には入らないかもしれないけど、APIのレスポンスがバラバラなのはまずいのでそれの修正)

* 右側の要素(今はタグ一覧とTOP10のみ)の充実

* 全画面Vue.js化(SPAには多分しないと思う)

* 統計データをSlackに送信する

* 固定ページみたいなの(全然考えてない)

* パフォーマンスチューニング(上記以外にもいろいろやばそうなところに心当たりがある)