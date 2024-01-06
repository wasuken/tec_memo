---
title: "Emacsのキーバインド"
description: Emacsのキーバインドを設定するために関数書いたりしたよ。
date: 2022-01-16
draft: false
categories:
  - "Emacs"
tags:
  - "EmacsLisp"
---
分割バッファのサイズ変更

縦サイズ広げる: C-x ^

左右を広げる: C-x }

もっと楽に調整したいなり...。

楽にしたいとは具体的に何をさすのか。

今のバッファサイズの半分増減して欲しい。

もしくは切り替えて欲しい。

## 作った

```lisp
;; 縦サイズをcntで分割して、小さい方の割合と、残ったサイズを返却
(defun window-height-div (
					   cnt				;分割数
					   sm-ratio			;小さい方の割合
					   )
  (let* ((fh (frame-height))
		 (fh-one (/ fh cnt))
		 (small (* fh-one sm-ratio))
		 (big (* fh-one (- cnt sm-ratio))))
	`(,small ,big)
	)
  )

(defun window-adjust (f)
  (let* ((sm-big (window-height-div 3 1)))
	(funcall f sm-big)))

(defun adjust-height (hei)
  (- hei (window-height)))

(defun window-adjust-sm ()
  (interactive)
  (enlarge-window (window-adjust #'(lambda (x) (- (car x) (window-height))))))

(defun window-adjust-big ()
  (interactive)
  (enlarge-window (window-adjust #'(lambda (x) (- (cadr x) (window-height))))))

(global-set-key (kbd "C-c w s") #'window-adjust-sm)
(global-set-key (kbd "C-c w b") #'window-adjust-big)
```

細かい要求など脳内に存在してなかったので、1/3か2/3でサイズ調整するよみたいな実装にした。

smは多分そこまで使わんのかな。

bigの方はもうちょっと高くならんのか！？っとなったときに使えそう。多分。

このコマンドを書くにあたって、以下の本が非常に参考になった。

[Emacs Lispテクニックバイブル | るびきち |本 | 通販 | Amazon](https://www.amazon.co.jp/Emacs-Lisp%E3%83%86%E3%82%AF%E3%83%8B%E3%83%83%E3%82%AF%E3%83%90%E3%82%A4%E3%83%96%E3%83%AB-%E3%82%8B%E3%81%B3%E3%81%8D%E3%81%A1/dp/4774148970)

いつものだね。

基本的に僕の検索ではあまりEmacs Lisp情報は欲しいものは出てこないので、

こういった本には非常に助けられている。

親と本と彼女(nil)にマジ感謝。

## 参考

[emacsで分割した画面の幅や高さを変更する](http://emacs.clickyourstyle.com/articles/262)
