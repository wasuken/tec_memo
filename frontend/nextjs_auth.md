---
title: "nextjs認証関連"
description:
date: 2022-03-27
draft: false
categories:
  - "frontend"
tags:
  - "nextjs"
  - "laravel"
  - "react"
  - "sanctum"
---

# nextjs認証関連 Laravelでやる

認証ってどうやる？

Laravel側で制御するのも良いと思うけど、

SPAとかの選択肢は取れるようになっておきたいということで

今回チャレンジした。

# ライブラリ

## Laravel

sanctumを使った。

[GitHub - laravel/sanctum: Laravel Sanctum provides a featherweight authentication system for SPAs and simple APIs.](https://github.com/laravel/sanctum)

## Next.js

axiosで

withCredentials: true

を入れる。

[AxiosでCookieを送信してSessionを共有する](https://i-407.com/blog/tech/n1/)

SessionCookieをそのまま送信する際に利用するらしい。

## ログインセッションを維持し続けるにはどうしたらいいんだろう。
