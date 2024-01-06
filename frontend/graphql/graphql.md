---
title: "GraphQL"
date: 2022-01-03
draft: false
---

# GraphQL

いくつかの記事及びそこからとぴっくを切抜いていく style で text を作成。

# [GraphQL の基礎の基礎](https://qiita.com/shotashimura/items/3f9e04b93e79592030a4)

## URL

endpoint は一つだけ。

## 構成

### query

取得系

GET みたいなやつ

### mutation

更新系

GET 以外

### subscription

通知系

Websocket みたいなやつ

### schema 言語

API 自体の仕様記述作成言語。

こいつを元に response を作成。

### resolver

実際の Data 操作を行うのが resolver.

# [GraphQL API について](https://docs.github.com/ja/enterprise-cloud@latest/graphql/overview/about-the-graphql-api)

## 型

強く型付けされている。

SQL に付随して mapper かいて定義するみたいなのやってると、例えば歪みが発生すると能力のない team の場合どこかでずれたりするんだけど

そもそも一体であればずれはなさそう。

## あくまで application layer

data がどのように保存されているかは GraphQL は存ぜぬということ。

# 参考

[GraphQL とは](https://www.redhat.com/ja/topics/api/what-is-graphql)

[GraphQL の基礎の基礎](https://qiita.com/shotashimura/items/3f9e04b93e79592030a4)

[GraphQL API について](https://docs.github.com/ja/enterprise-cloud@latest/graphql/overview/about-the-graphql-api)
