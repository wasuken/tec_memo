---
title: "tinybaseのリポジトリとかみたりした"
description:
date: 2022-01-18
draft: false
categories:
  - "Database"
tags:
  - "TypeScript"
  - "Database"
---
# tinybase

hatenaでみて、興味をもったのでもうすこししらべた。

## ドキュメントをみながら感想

### Store

[Storeあたりのページをみるかぎりは](https://tinybase.org/api/store/interfaces/store/store/methods/getter/getcell/)
データ自体はMap<K,V>つかってる。

getCellはmapGet連打してた。

### Indexes

[Indexes | TinyBase](https://tinybase.org/api/indexes/interfaces/indexes/indexes/)

これよくわからんけどidsというglobal変数？にいれてる？

おもにJSがわからん。

---

きがむいたらつづきかくかも。

# 参考

[GitHub - tinyplex/tinybase: A tiny, reactive JavaScript library for structured state and tabular data.](https://github.com/tinyplex/tinybase)

[TinyBase](https://tinybase.org/)

べんり だった->[vscode.dev](https://vscode.dev/github/tinyplex/tinybase)
