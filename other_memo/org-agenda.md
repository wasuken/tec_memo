# org-modeでタスク管理してみた。

これがまた割と便利だった。

ただ一つだけめんどくさいことがあって、

org-agendaで読み込むファイルはディレクトリ下のファイル全部読み込むみたいなことできないっぽかったので

そうするためのコードを書いた。

```
(setq org-agenda-files (mapcar #'(lambda (x) (concatenate 'string "~/todo/" x))
							   (remove-if #'(lambda (x) (< (length x) 3))
										  (directory-files "~/todo/"))))
```

"~/todo/"のとこは変数にしてもよかったかもしれない。

org-modeっていうか、やることTODO化＋その日分のタスク終わるまではツイート禁止は割と効いてるみたいで、

かなりハイペース(当社比)で進んでいる。

まだ二日しか経ってないけどね。

まあこのままやっていきである。
