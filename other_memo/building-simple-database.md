# 「Let's Build a Simple Database」を読みながら写経しつつ、メモを取る

wyagやって案外楽しかったので、次にこれをやっていく。

言語はC。

## 本家リンク

サイト:[How Does a Database Work? | Let’s Build a Simple Database](https://cstack.github.io/db_tutorial/)

リポジトリ:[GitHub - cstack/db_tutorial: Writing a sqlite clone from scratch in C](https://github.com/cstack/db_tutorial)

## Part1

ここでは、おそらく動作確認もかねてか、replを書いていくそうだ。

また、このデータベースはSqliteをモデルに作成し、

データベースを一つのファイルに保存するらしい。

アーキテクチャは以下リンク右あたりにある図の通り。

[Zipvfs: How ZIPVFS Works](https://www.sqlite.org/zipvfs/doc/trunk/www/howitworks.wiki)

入力はSQLであり、

### フロントエンド

* tokenizer

* parser

* code generator

コードジェネレータって何？って思って調べたけど全然出てこなかったのでなんもわからんかった。

とにかく、ここではSQLを解析して、何かのコード(VM向け)を生成するってことなのかな？

### バックエンド

これらは説明があった。

#### vm

virtual machine。

フロントエンドから送られてきたバイトコードをテーブルまたはインデックスのb-treeに変換して?格納する。

#### b-tree

データ構造...のはずだが、ここではそれ以外にもpagerにコマンドを発行してディスクからデータを取得したり保存したりできる。

#### pager

データのページを読み書きしたりするコマンドを受け取り、解釈する。

それにより、オフセットを用いてRead/Writeを行う。

また、解釈中には最近アクセスしたページについてはキャッシュとしてメモリに保存したり、いつ消したり等の

ページのキャッシュの管理も行う。

#### os-interface

文字通り。ちなみに今回は複数OSのサポートはないらしい。当たり前やが。

## Part2

enum型を使ってコマンドの実行結果を表現する。

この章ではそれくらいしか変更してない。

## Part3

この章では、インメモリでinsertのみ有効で、単一のテーブルのデータベースとして機能するように実装する。

ここで単一のテーブルとは、コード中にハードコーディングするものとする。

しかもまともなinsert文ともいえない実装である。

内部実装的にも、例えばSqliteはデータの保存にはb-treeを使うが、今回は配列で実装する。

## Part4

テストを書くフェーズ。ただしテストコードはC言語ではなくRuby(RSpec)。

## 知らんかったCの関数とか用語

### sscanf

scanfの文字列変数バージョン?意味わからんゴミみたいな説明はやめろ。

第一引数に入力元の文字列のポインタを渡して、あとはscanfとだいたい同じ。

### strtok

splitの変化球っぽいやつ(野球ではない)。

```c

char hoge[100] = "unchi unchi";
char* fuga = strtok(hoge, " ");
char* foo = strtok(NULL, " ");

```

１回目は普通に第一引数に対象となる文字列変数(文字列をそのまま渡したらセグフォった)とdelimとなる文字列を渡して、

delimで区切った文字の一文字目を取得する。それ以降の文字列が欲しい場合は

第一引数にNULLをいれてやると返ってくる。

NULLを入れた場合の挙動は、おそらく以前の文字列を分割したあまりをそのまま使い回すという意味になるので、

delimを変えた場合はその新たなdelimで分割した結果が返ってくる。

### 汎用ポインタ

void*みたいなやつ。

要するにポインタにならなんでも変換できるやつ。

## 参考

[sscanf](http://www9.plala.or.jp/sgwr-t/lib/sscanf.html)

[汎用ポインタ](http://wisdom.sakura.ne.jp/programming/c/c47.html)
