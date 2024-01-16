---
title: "状態"
date: 2022-01-03
draft: false
---

# 状態

「Programming Clojure」第二版の 5 章の内容の Memo.

## ref による更新

名前の通り、参照を操作する関数である。

ref は参照の作成、(ref 10)みたいな感じで作成。大抵は bind する。

deref は参照から Data を取得する関数。

set-ref は参照先を変更する関数。

ただし、変考時には dosync 関数で包まないと変更はできない。

また、参照先変更に関しては既存の参照先に追加する程度であれば、set-ref ではなく

alter を使ったほうがいいかもしれない。

alter は引数に指定した値を関数を使って更新する。

また、commute という関数もある。こちらは alter と同じよびかただが、

更新順序が保証されない。その分高速に処理できることもある。

当然、bug が入りやすくなったりするので、

基本的には alter を使ったほうがいい。

### atom による更新

ref - atom

set-ref - reset!