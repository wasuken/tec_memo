---
title: "graphql採用時のperformance関連のめも"
date: 2022-01-03
draft: false
---

# graphql 採用時の performance 関連のめも

## [GraphQL API のパフォーマンステスト](https://blog.testrail.techmatrix.jp/graphql-performance-testing/)

### API-Client 間の往復を減らせる可能性があるが...

記事の例にもでている反復的な requeset による

いわゆる無駄な request 及び response body の削減が可能だが、

反面、netflix のような事件？が起きる可能性もでてくるようだ。

## [GraphQL を使って実装してみよう](https://qiita.com/haradakunihiko/items/a91a66e35031212023e3)

application 層未満はしらんと別めもにかいていた。

しかしよくわかってなかった。そして netflix の事件の紹介をみてなおさらわからなくなったが、

この記事をみて、Storage, REST API, RDBMS いずれも制限はないということをしった。

## まとめ

graphql は現時点でものうはうが十分に蓄積しているようには見えない。

故に導入する際には performance 分析基盤をそれなりに整る必要がある。

あるが、これはそもそもそれなりの規模になると RDBMS 運用時にもそうなるので当たり前じゃんとなる。
