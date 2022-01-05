---
title: "GraphQL"
date: 2022-1-3
draft: false
---
# GraphQL



いくつかの記事及びそこからとぴっくを切抜いていくstyleでtextを作成。



# [GraphQLの基礎の基礎](https://qiita.com/shotashimura/items/3f9e04b93e79592030a4)



## URL



endpointは一つだけ。



## 構成



### query



取得系



GETみたいなやつ



### mutation



更新系



GET以外



### subscription



通知系



Websocketみたいなやつ



### schema言語



API自体の仕様記述作成言語。



こいつを元にresponseを作成。



### resolver



実際のData操作を行うのがresolver.



# [GraphQL APIについて](https://docs.github.com/ja/enterprise-cloud@latest/graphql/overview/about-the-graphql-api)



## 型



強く型付けされている。



SQLに付随してmapperかいて定義するみたいなのやってると、例えば歪みが発生すると能力のないteamの場合どこかでずれたりするんだけど



そもそも一体であればずれはなさそう。



## あくまでapplication layer



dataがどのように保存されているかはGraphQLは存ぜぬということ。



# 参考



[GraphQL とは](https://www.redhat.com/ja/topics/api/what-is-graphql)



[GraphQLの基礎の基礎](https://qiita.com/shotashimura/items/3f9e04b93e79592030a4)



[GraphQL APIについて](https://docs.github.com/ja/enterprise-cloud@latest/graphql/overview/about-the-graphql-api)
