---
title: "Python gets a jit"
description:
date: 2024-01-09
draft: false
categories:
  - "learn_english"
tags:
  - "english"
  - "learn"
  - "limit25"
---

[Python 3.13 gets a JIT](https://tonybaloney.github.io/posts/python-gets-a-jit.html)

# 翻訳メモ

新年あけましておめでとう

主要開発者のBrandt BucherがJIT Compilerを追加する

小さなプルリクエストをCPythonの3.13ブランチに追加しました。

この変更は、一度うけいれられたら

CPythonインタプリタの中では、Python 3.11のSpecializing Apaptive Interpreter以来の大きな変化の一つになるでしょう。

このブログポストでは、JITとはなんなのか、どのように動作し、またなんの恩恵があるのかについてについて説明します。

**なにこれ**

JITまたは "Just in Time"とはコードがはじめて実行されるときに

オンデマンドでコンパイルが動作することを暗示するコンパイル設計です。

これは広義の用語であり、多くのことを意味する可能性があります。

I guess,

technically the Python compiler is already a JIT

技術的にはすでにコンパイラです。

because it compiles from Python code into Bytecode.

おそらく、Pythonコンパイラはすでにバイトコードへコンパイルするため、

# 単語

- In late December 2023 2023 12月下旬
- once accepted 一度うけいれられたら
- would be ~になるだろう
- one of the biggest 大きな~の一つに
- look at 説明する？
- compilation 編集 -> コンパイル？
- impiles 暗示する
- I guess おそらく？
- technically the Python compiler 技術的にはPythonコンパイラは

# 補足等

because itとかわからん。こういう文法ってか特殊イベントみたいなやつにかぎらず

基本的に読む順番がまったくわからん。
