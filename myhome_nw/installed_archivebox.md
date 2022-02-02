---
title: "ArchiveBox導入してみた"
description:
date: 2022-02-01
draft: false
categories:
  - "home-nw"
tags:
  - "linux"
  - "archivebox"
  - "archlinux"
  - "install"
---
# ArchiveBox導入してみた

[ArchiveBox | 🗃 Open source self-hosted web archiving. Takes URLs/browser history/bookmarks/Pocket/Pinboard/etc., saves HTML, JS, PDFs, media, and more…](https://archivebox.io/)

ちょっと前に導入した自宅のarch入りサーバに導入。


ほとんどなにも入ってなかったので以下をインストール

**パッケージリスト**

* python 3.10
* pip
* git
* ripgrep
* wget
* npm
  * nodejs
* docker

Pythonは3.10でも動いた。

## 試行錯誤

流れとしてはだいたい下になる。

1. curl -sSL 'https://get.archivebox.io' | sh
   -> 失敗
2. python,pip,dockerをいれてようやくインスコ完了
3. PATHの調整を行う。しかしまだ取得ができてないっぽいのであれこれ
4. archivebox addでサイト登録、しかしいろいろエラー、ワーニングで謎が深まる
5. あれこれ設定は下記コマンドである程度可能であると判明(helpとかででてくる)
   ```shell
   $ archivebox setup
   ```
   -> 最終的にパッケージリストの形に
6. ユーザのセットアップ
   ```shell
   $ archivebox manage createsuperuser
   ```
7. archivebox server 0.0.0.0:8000で確認完了
