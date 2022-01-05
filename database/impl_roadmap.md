---
title: "DB自作ロードマップ"
date: 2022-01-03
draft: false
---
# DB自作ロードマップ



具体的にDB自体よく理解してないので、他人の成果を元にロードマップ的なものを作成して、



それを元にDBを自作してみる。



## 構成一覧



* データモデル

  * リレーショナルモデル

  * ドキュメント

  * key/value

* ストレージモデル

  * n-array

  * decomposition

* クエリ言語

  * SQL

* ストレージアーキテクチャ

  * ヒープ構造

  * ログ指向

* インデックス

  * btree

  * ハッシュテーブル

* トランザクション処理

  * ACID

  * 並列処理

* 回復処理

  * ロギング

  * チェックポイント

* クエリ処理

  * ジョイン

  * ソート

  * 集約

  * 最適化

* 並列処理

  * マルチコア対応

  * 分散DB



参考: [DBMSをGoで実装してみた](https://buildersbox.corp-sansan.com/entry/2019/10/24/110000)



上記よりほぼすべてになるが、一部抜粋した。



## わからん用語リスト



### ストレージモデル



* n-array

  CSVみたいに保存する?



* decomposition

  属性単位でデータを保存する方式

  DBサイズの削減が期待できる

  列操作に弱い

  シンプルなデータ構造

  見た感じPrimaryKey,attrみたいな感じで保存されている。



[Decomposition Storage Model (DSM)](https://studylib.net/doc/9763113/decomposition-storage-model--dsm-)



# 参考



[DBMSをGoで実装してみた](https://buildersbox.corp-sansan.com/entry/2019/10/24/110000)



[CMU Database Systems をひたすら追っていく ~03,04 Database Storage ~](https://rabbitfoot141.hatenablog.com/entry/2019/12/03/000000)
