---
title: "graphql採用時のperformance関連のめも"
date: 2022-01-03
draft: false
---
# graphql採用時のperformance関連のめも



## [GraphQL APIのパフォーマンステスト](https://blog.testrail.techmatrix.jp/graphql-performance-testing/)



### API-Client間の往復を減らせる可能性があるが...



記事の例にもでている反復的なrequesetによる



いわゆる無駄なrequest及びresponse bodyの削減が可能だが、



反面、netflixのような事件？が起きる可能性もでてくるようだ。



## [GraphQLを使って実装してみよう](https://qiita.com/haradakunihiko/items/a91a66e35031212023e3)



application層未満はしらんと別めもにかいていた。



しかしよくわかってなかった。そしてnetflixの事件の紹介をみてなおさらわからなくなったが、

	

この記事をみて、Storage, REST API, RDBMSいずれも制限はないということをしった。



## まとめ



graphqlは現時点でものうはうが十分に蓄積しているようには見えない。



故に導入する際にはperformance分析基盤をそれなりに整る必要がある。



あるが、これはそもそもそれなりの規模になるとRDBMS運用時にもそうなるので当たり前じゃんとなる。
