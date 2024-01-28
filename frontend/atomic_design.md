---
title: "atomic design"
description:
date: 2024-01-27
draft: false
categories:
  - "frontend"
tags:
  - "design"
  - "learn"
  - "atomic_design"
  - "frontend"
---

# Atomic Design

## 知ってるつもり

### 分割基準

ちいさい順

1. 部品、ボタン
2. 分子、フォーム一組
3. フォーム一式
4. ページ、テンプレート

### storybook と相性がよい

一塊で動かして確認できるから。

## 事前：知りたいこと

### どうやって directory を分割するか

```
-src/components
    ---/atom
    ---/mol
    ---/org
    ---/tmpl
    /page
```

### 採用してうれしいこと

storybook と相性がよい

->部品単位で対話、段階的に実装ができる。

### テストがやりやすくなるのか？

### React のコンポーネント単位の引数

基準だけでもつかめることができたら勝利。

### 共通化しても結局個別ページが多くなる場合、利用はさけるべきか

-> 引数を柔軟にする?
