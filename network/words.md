---
title: "わからん単語とか技術とか"
date: 2022-1-3T10:00:00+08:00
draft: false
---
# わからん単語とか技術とか



## SYN Flood



[【Linuxで実践】SYN Flood攻撃とSYN cookiesについて | MasaのITC Life](https://wireless-network.net/syn-flood-cookies/)



3 way handshakeの最初clientからSYNが送られた際に、SYN_backlogへ情報を保存する。



ここを溢れさせる目的の攻撃。



## TCP SYN cookie



TCP connectionを悪用したSYN Flood攻撃等の対策の一つ。



溢れた際に未確立接続, SYN_backlogのdataを順に破棄すpる。



今のLinuxではdefaultでSYN cookieが有効になっている。
