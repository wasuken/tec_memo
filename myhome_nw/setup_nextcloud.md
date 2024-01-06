---
title: "setup nextcloud"
description:
date: 2022-01-11
draft: false
categories:
  - "home-network"
tags:
  - "network"
  - "private"
  - "archlinux"
  - "setup"
  - "database"
  - "mariadb"
  - "php"
---

OS: Arch Linux

httpd: 2.4.52
php: 8.0.14
mariadb: mariadb  Ver 15.1 Distrib 10.6.5-MariaDB, for Linux (x86_64) using readline 5.1


# おハマりポイント

## mariadb

dumpファイルからrestoreしてみたがうまくいかない。

みてみるとテーブルが一つもない。

？

### 解決

[MariaDBデータベースサーバのインストール](https://digitalmania.info/linux/debian-11/install-mariadb-server/)

```config
innodb_read_only_compressed
```


により、読取専用になっているようなので、

設定ファイルを編集し、再度dumpからrestoreしてみると、

無事データがはいった。

## httpd

とりあえずinstallしてみた。

初期設定でも動作したが、php周りでガチャガチャして再起動したらエラーでとまった。

## 原因 and 解決

[PHPインストール時のMPMのエラーを手っ取り早く解消する](https://www.kmr-blog.com/mpm-error/)

マルチスレッドにしようとしたのが原因?。

とりあえずはシングルスレッドでいいかということで暫定処理。
