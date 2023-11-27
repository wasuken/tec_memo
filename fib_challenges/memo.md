---
title: "ChatGPTに問題をだしてもらって、それにこたえる"
description:
  date: 2023-11-27
  draft: false
  categories:
    - "learn"
    tags:
      - "learn"
---

問題：フィボナッチ数列の偶数値の和

フィボナッチ数列は、次のように定義されます…。各数は、直前の 2 つの数の和となる

    0, 1, 1, 2, 3, 5, 8, 13, 21, 34, ...

このフィボナッチ数列において、4 百万（4,000,000）以下の値であるすべての偶数値の和を計算する。

```lisp
(defparameter *memo* (make-hash-table))
(defun calc (n)
(let ((fv (fib n)))
(cond ((< fv 4000000)
       (+ (if (evenp fv)
                fv
                0)
            (calc (1+ n))
            )
       )
        (t 0))
)
)
(defun fib (n)
(cond ((gethash n *memo*)
         (gethash n *memo*))
        ((< n 2)
         n)
        (t
         (let ((v (+ (fib (1- n)) (fib (- n 2)))))
           (setf (gethash n *memo*) v)
           v)
         )
        )
)

```
