---
title: "ddskk設定"
date: 2022-01-03
draft: false
---
# ddskk設定



時間: 2021-12-29(水) 06:16:51



環境：Arch Linux



## 概要



Emacsで日本語入力がつらかったので、調べたところddskkにたどりついた。



## 作業



### shell



```shell

$ wget https://github.com/skk-dev/ddskk/archive/refs/tags/ddskk-17_Neあ ppu.tar.gz

$ tar xzf ddskk-17.1_Neppu.tar.gz

$ cd ddskk-17.1_Neppu

$ make what-where

$ sudo make install

```

### Emacs



```lisp

(setq default-input-method "japanese-skk")

(global-set-key (kbd "C-c C-j") 'skk-mode)

(global-set-key (kbd "C-x j") 'skk-auto-fill-mode)

(global-set-key (kbd "C-x t") 'skk-tutorial)

(setq skk-large-jisyo "/path/to/SKK-JISYO.L")

```



pathについては、make what-whereを実行する



## 参考



[SKK (Simple Kana to Kanji conversion program) Manual](https://ddskk.readthedocs.io/ja/latest/index.html)
