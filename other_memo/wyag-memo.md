# 「Write yourself a git」を写経しつつ、読んだときのメモ

これはQrunchにも投稿してる([「Write yourself a git」を写経しつつ、読んだときのメモ | Qrunch（クランチ）](https://qrunch.net/@HFyNkCtgmtrR4P5h/entries/uKavehRaKfOzYckb?ref=qrunch))。

## 注意

まずこれは翻訳記事ではない。

また、本家を見ればわかるが完成途中である。

途中から自力で継ぎ足していくなり、一から書くのもよいかもしれないが、

今回は本家に沿って、記事を作成することにした。

故にこちらも本家以上のことは書かない。

## 本家リンク

サイト:[Write yourself a Git!](https://wyag.thb.lt/)

リポジトリ:[GitHub - thblt/write-yourself-a-git: Learn Git by reimplementing it from scratch](https://github.com/thblt/write-yourself-a-git)

## 1~2

特に書くことはなかった。

## 3(.gitの生成)

initを実装する。

ここでは、GitRepositoryというクラスを作成している。

このクラスは<project-root>/.git/configのデータやら、バージョン管理対象のファイルパスやら持ってるクラス(適当)

ここらへんは当然だけど.git付近のファイル/ディレクトリのIOやらチェックやらがほとんど。

あと、repo_findはここから先しばらくでてくるんじゃないんすかね。

git管理下のプロジェクトルート下ならどこからでも簡単にGitRepositoryクラスが手に入るからね。

## 4(Gitオブジェクトの読み書き)

cat-fileとhash-objectを書いていく。

それぞれ、実際のgitコマンドではあまり使わないと思う。少なくとも私は使ったことないし、

wyag記事中でも低レベルな、いわゆる配管と呼ばれているコマンド。

逆にユーザフレンドリなコマンドは磁器と呼ばれている。

aGitのObjectには種類があり、blob, commit, tag, treeとある。

最初に書いとくけど、git cat-file -p <hash>で簡単に内容を確認できるし、

-tオプションでオブジェクトの種類を出力してくれる。

---

以下、各オブジェクトの説明とか。

### blob

blobはファイルを圧縮したもの、つまり、ファイルの中身そのものが入ってる。

treeはファイルシステムっぽい木構造のやつ。こんな感じ。

```shell

$ git cat-file -p 25fe1f9884c17c70b8784d15e35298fd8003f8ad
100644 blob 51176886f037d0e412d37e3ca560f595b11b7dc7	2020-01-13.md
100644 blob d4bd4b60cf209519773d5cfb4106672efe4a969b	2020-01-14.md
100644 blob 100b90bc2a3519e7a4ce8294d9b7564db1aa34b7	2020-01-15.md
100644 blob 5fe5034197d41be8876aaf5f1f1b8a06614c7ecc	2020-01-16.md
100644 blob 757f1c543932efa9e69c429b7ce6092ec7a81989	2020-01-17.md
100644 blob 4dbf80551f3293f854635b9bbbdcffa919076146	docker-dev-audio-thinking.md
100644 blob fbb54a8f5d089145396e26fd41f72545e7561a4f	lisp-music-1.md
100644 blob 20b6c51c7a4d283bb10235a4a9193db5d73099b9	lisp-music-2.md
040000 tree 6c67859c318caeb208ad430727c3b7cb5bfe4469	nippo_backup
100644 blob 2add9b9ba68ffb7b0698fe23adc458d10f22e561	output-technique-reading-impressions-3.md

```

### commit

commitは、保存するtree、author、committer、そしてコミットメッセージを保存する。

ちなみにこんな感じ。

```shell

$ git cat-file -p 2503fd4a11b5a314fed13eb82abde74fab348f6d
tree cc9d74a956f62d53990acd85fb7e50b749b2ab3c
parent 61491c8ff9e29085e85e374100ded91ad4f58df3
author wasuken <wevorence@gmail.com> 1580568991 +0900
committer wasuken <wevorence@gmail.com> 1580568991 +0900

c.

```

### tag

ここの検証？で少し時間かかった。


というのも、git tag testで作成したtagのオブジェクトをみようとしても

思った通りのフォーマットにはならなかったからだ。

```shell

$ git cat-file -p test
tree 2139ef4ba96cabe84cef034b9e28adf7a2a63210
parent bd94f6c1071c81e5f363d4f7629a9b8cb5320bef
author wasuken <wevorence@gmail.com> 1594825062 +0900
committer wasuken <wevorence@gmail.com> 1594825062 +0900

commit.

```

なんでじゃぁ＾〜。

と思いながらいろいろやってたらできた。

どうやらメッセージをいれないといかんらしい。なぜ？

```shell

$ git tag test2 -m "This is test2"
$ git cat-file -p test2
object 0fc0fda19e7fc7df09195d70e56e166eddee896b
type commit
tag test2
tagger wasuken <wevorence@gmail.com> 1594910197 +0900

This is test2

```

### タグの種類

これは後の章に書いてあるやつだけど、タグにはいくつか種類がある。

#### 軽量タグ

commitオブジェクトの参照をそのまま保存したやつ。

cat-fileしても参照してるcommitオブジェクトの内容がでてくる。

#### 注釈付きのタグ

丁寧にtagオブジェクトまで拵えて、誰が作ったタグなのかと、そのメッセージまで書いてあるやつ。

cat-fileするとtagオブジェクトの内容がでてくる。

---

## 5(commitの読み込みとかパースとか)

この章では、commitオブジェクト、またlogコマンドの実装について書いてある。

原文のタイトルにもある通り、ここと次の章では主にcommitオブジェクトの読み取りが主題となる。

### commitオブジェクト

コミットオブジェクトを保存する際のフォーマットはRFC2822。

細かいルールはRFC2822読んでないし、ここで語る必要はないので省略するが、

実装するにおいて気をつける点は以下が主だと思う。

ここで、わかりやすいように(?)" "は{space}と書いている。

* だいたい「{key}{space}{value}」の形式。

わかりにくいので例えを出すが、

```

tree 8b180ed3fdc94dc75c4314d3f1db373bd8aae75d

```

ここででてくる{key}は上でいうところの"tree"であり、

{value}は"8b180ed3fdc94dc75c4314d3f1db373bd8aae75d"となる。

* 複数行ある場合、二行目以降は「{space}\\n」、

#### 構成

ちなみに、私の某リポジトリで試したが、

git cat-file -p {commit-object}

は

```

tree 8b180ed3fdc94dc75c4314d3f1db373bd8aae75d
parent c3cecac8d6423caef8befbf9a72bcc2e2d2049b1
author wasuken <wevorence@gmail.com> 1594997012 +0900
committer wasuken <wevorence@gmail.com> 1594997012 +0900

commit.

```

となった。

gpgsigはないようだ。

署名をいれたくば、設定が必要だが今回はやらない。

##### tree

treeオブジェクトへの参照。

##### parent

親への参照。

##### author

リポジトリの作者。

##### committer

コードをコミットした人。

wyagの記事には書いてない。なぜだろう。

##### gpgsig

pgp署名。

----

ところで、committerとauthorの違いってなんだろう。

なんとなくイメージはつくけど調べてみた。

> You may be wondering what the difference is between author and committer. The author is the person who originally wrote the work, whereas the committer is the person who last applied the work. So, if you send in a patch to a project and one of the core members applies the patch, both of you get credit — you as the author, and the core member as the committer.

> 引用元:[Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

つまり、リポジトリを作った人がauthorで、最後にパッチを当てた人(今コードを書いてる人)がcommitterということになるらしい。

----

#### その他

文字通り、kvlm_parseという関数がパースする。

逆にkvlm_serializeでは、kvlm(OrderdDict)を文字列に変換する。

特に難しい処理はしてない。

### logコマンド

このコマンドは簡単にいえば、コミットログをわかりやすく...

ではなく、graphviz形式のデータを吐き出すコマンド。

## 6(treeの読み込みとかパースとか)

### treeの解析

wyag曰く、treeオブジェクトを書き込む際ののフォーマットがあるとのこと。

> [mode] space [path] 0x00 [sha-1]

> 引用元:[Write yourself a Git!](https://wyag.thb.lt/#orga708f5f)

ここで、恒例のコマンド結果の確認をしよう。

以下コマンド結果一部貼り付け。

```shell

$ git cat-file -p 8b180ed3fdc94dc75c4314d3f1db373bd8aae75d
100644 blob d1596f73e6ac5cd9270ff066ea282917b8e1bb1b	2020-02-01.md
100644 blob 201318ca1f479f66017be26e1a4a13d598fcba4f	2020-02-02.md
100644 blob 8da5d60d645996d99910d10d97d489fe97570976	2020-02-03.md
100644 blob f21a86d02187152a7474bc4a3bdb7095355e40b6	2020-02-05.md
...

```

あれ、なんかちがくね。

調べてみると、これらは左からモード、タイプ、ファイル名へのsha1ポインタとのこと。

----

余談だけど、(参考:[Git - Gitオブジェクト](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-Git%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88))のページで以下のようなコマンドを見つけた。

> git cat-file -p master^{tree}

> 引用元:[Git - Gitオブジェクト](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-Git%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)

曰く、

> master^{tree} のシンタックスは、master ブランチ上での最後のコミットが指しているツリーオブジェクトを示します。

> 引用元:[Git - Gitオブジェクト](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-Git%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)

...えっ。もっと早く知りたかった。

これ知るまで頑張ってtreeやらcommitオブジェクトを手動で探してた...。辛い。

----

モードだけがよくわからんかった。調べてみたら以下の通りだった。

> モード

> 100644などの数値部分。そのデータがどのようなものかを示す。例えば、100644はファイル、100755は実行可能ファイル、120000はシンボリックリンクを表します。

> 引用元:[Gitの内部（ツリーオブジェクト）- YoheiM .NET](https://www.yoheim.net/blog.php?q=20140301)

## 7(refs,その中でもタグやブランチについて)

タグとブランチの実装。

タグに関しては行ってしまえばただの参照。

### ブランチとタグの違い

ブランチとタグは簡単に表現しまえばお互い"コミットへの参照"。

ただし、ブランチの参照はコミットごとに更新される可能性がある。

なお、参照については二種類存在するようだ。

直接参照と間接参照について説明しておく。

#### 間接参照

ref: path/to/hogeみたいな書き方がされてる。

良い例がHEADファイル。

```shell

$ cat .git/HEAD
ref: refs/heads/master

```

#### 直接参照

```shell

$ cat .git/refs/heads/master
5f943586b9360f8e59e481688843bc391eadab01

```

ハッシュ値がそのまま入ってるやつ。

### tagの作成(本家サイトにはない)

よくみてみると、tag_createという関数が利用されているのに、実装については書いてない。

ちょっとリポジトリをみてみるとtag_createブランチ

[write-yourself-a-git/write-yourself-a-git.org at tag_create · thblt/write-yourself-a-git · GitHub](https://github.com/thblt/write-yourself-a-git/blob/tag_create/write-yourself-a-git.org#the-tag-command)

に実装があった(taggerがsoul eaterだけどこれって例のアニメネタなんだろうか)。

みるとわかるけど、制作途中なのかメッセージやらtaggerまわりが固定値になってる。

## 8(ステージングとインデックスファイル?)

作りかけっぽいので割愛。

## 感想

commitとaddはまだ作ってない。できればそこらへんを一番理解したかったが、

まあここからは自分の力で頑張る。多分。

Clojureか他の言語になるかは知らんがリライトはまたやりたいと思ってる。

## 蛇足:以前にClojureでリライトしようとして断念した話

リポジトリのリンク

[GitHub - wasuken/clj-wyag](https://github.com/wasuken/clj-wyag)

### 個人的にキツかった点

まず、PythonのクラスをClojureのクラスっぽいもので代用しようとすると結構きつかった。

また、Pythonの手続き処理をClojureでも手続き処理チックに書こうとして悲しくなった。

何か別の言語でリライトするなら、そのまま写すのではなく、一度バラして考え直す必要があるという

小学生でもわかることを作成途中で気がついたのでさらに悲しくなって、しばらく手を止めてしまった。

あとはPythonって結構標準ライブラリが充実してると思った。

当たり前だけどClojureの標準ライブラリにはないものが結構あった。

特にzlibとargparse。zlibは別にいいんだけど、argparseは便利。

# 参考

[Write yourself a Git!](https://wyag.thb.lt/)

[GitHub - thblt/write-yourself-a-git: Learn Git by reimplementing it from scratch](https://github.com/thblt/write-yourself-a-git)

[Git - Packfile](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-Packfile)

[Git - Gitオブジェクト](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-Git%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)

[Git - タグ](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E5%9F%BA%E6%9C%AC-%E3%82%BF%E3%82%B0)

[Git - Viewing the Commit History](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)

[Git - 作業内容への署名](https://git-scm.com/book/ja/v2/Git-%E3%81%AE%E3%81%95%E3%81%BE%E3%81%96%E3%81%BE%E3%81%AA%E3%83%84%E3%83%BC%E3%83%AB-%E4%BD%9C%E6%A5%AD%E5%86%85%E5%AE%B9%E3%81%B8%E3%81%AE%E7%BD%B2%E5%90%8D)

[Git - Gitオブジェクト](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-Git%E3%82%AA%E3%83%96%E3%82%B8%E3%82%A7%E3%82%AF%E3%83%88)

[Gitの内部（ツリーオブジェクト）- YoheiM .NET](https://www.yoheim.net/blog.php?q=20140301)

[write-yourself-a-git/write-yourself-a-git.org at tag_create · thblt/write-yourself-a-git · GitHub](https://github.com/thblt/write-yourself-a-git/blob/tag_create/write-yourself-a-git.org#the-tag-command)

[Git - 配管（Plumbing）と磁器（Porcelain）](https://git-scm.com/book/ja/v2/Git%E3%81%AE%E5%86%85%E5%81%B4-%E9%85%8D%E7%AE%A1%EF%BC%88Plumbing%EF%BC%89%E3%81%A8%E7%A3%81%E5%99%A8%EF%BC%88Porcelain%EF%BC%89)
