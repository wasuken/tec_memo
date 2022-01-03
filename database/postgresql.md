---
title: "PostgreSQL"
date: 2022-1-3T10:00:00+08:00
draft: false
---
# PostgreSQL



仕事ではMySQLしか使ってない。



趣味でも同じ。



だから調べる(?)



## ざっくり概要



以下のほとんどは基本的にMySQLと比較した上での評価が多い。



* psqlというCLIがある。



* RDBMSではなくオブジェクトリレーショナルデータベース



* 多機能、拡張性が高い



* 複雑なクエリに強い



	* 読み取り専用の用途(マスタみたいなやつ？)だとMySQLの方が強い場合が多い。

	

* 大規模なシステムにも強い。



* 全ソート全取得みたいなクエリは速い。



* updateはinsertみたいな処理をするため遅いそうだ。



* joinは結合方法が豊富

	* ネステッドループ結合

	* ハッシュ結合

	* ソートマージ結合

	

* ストアドプロシージャはPython等のプログラミング言語で定義できる。



# 参考



[初心者・学習用にも！PostgreSQL入門（2021年版）](https://postgresweb.com/introduction-to-postgresql)



[PostgreSQL vs MySQL: その違いとは](https://www.integrate.io/jp/blog/postgresql-vs-mysql-which-one-is-better-for-your-use-case-ja/)



[MySQL と PostgreSQL の違いを知る](https://www.superbusinessman.biz/mysql-vs-postgresql/)
