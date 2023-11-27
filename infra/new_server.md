---
title: "新自宅サーバキッティング"
description:
date: 2022-01-08
draft: false
categories:
  - "home-network"
tags:
  - "network"
  - "private"
  - "archlinux"
  - "setup"
---

廃棄PCもらったので、セットアップした。

SSD購入して取り付け。

インストールUSB用意して、Arch起動して、

[インストールガイド](https://wiki.archlinux.jp/index.php/%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%82%AC%E3%82%A4%E3%83%89)

だいたい上記みたいなことしつつ、

追加パッケージとしてはnet-tools,vim,sudo,htop,dhcpcdをいれた。

また、ブート関連についてはbootctlが全然動かなかったのでgrubとefibootmgrを入れつつ、

chrootで以下の処理で対応した上で再起動し、

```shell
# grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=arch
# grub-mkconfig -o /boot/grub/grub.cfg
```

無事ArchLinuxが起動した。

あとはメモリ増設やdockerいれたりするかもしれないが、

確定ではないので一旦このメモは閉じる。

---

# バックアップの保存

ファイルサーバのデータ保存をおこなった。

ついでに可能であればこのまま移行してもよいとおもった。
