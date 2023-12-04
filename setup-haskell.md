---
title: "haskellのセットアップ"
description:
date: 2023-12-02
draft: false
categories:
  - "setup"
tags:
  - "setup"
  - "haskell"
  - "emacs"
  - "linux"
---

# 目標

- Emacs で色つけくらいはしてほしい。できれば補完、自動フォーマット、flymake?できればうれしい。
- パッケージはなるべくいれたくない。Arch のパッケージアップデートで haskell-\*の羅列をみるのはうんざりする。

# repl で random がつかえない

```bash
$ cabal install --lib random
```

# 最終的な Emacs Lisp 設定 Code

```lisp
(use-package haskell-mode
  :ensure t
  :init
  (progn
    (add-hook 'haskell-mode-hook 'turn-on-haskell-doc-mode)
    (add-hook 'haskell-mode-hook 'turn-on-haskell-indent)
    (add-hook 'haskell-mode-hook 'interactive-haskell-mode)
    (setq haskell-process-args-cabal-new-repl
    '("--ghc-options=-ferror-spans -fshow-loaded-modules"))
    ;; (setq haskell-process-type 'cabal-new-repl)
    (setq haskell-stylish-on-save 't)
    (setq haskell-tags-on-save 't)
    )
  :config
  (progn
    (defun insert-repl-start ()
      (interactive)
      (insert ":{"))
    (defun insert-repl-end ()
      (interactive)
      (insert ":}"))
    ;; TODO replのときだけ有効にする
    (define-key haskell-mode-map (kbd "C-c <tab> s") 'insert-repl-start)
    (define-key haskell-mode-map (kbd "C-c <tab> e") 'insert-repl-end)
    )
  )

(use-package flycheck-haskell
  :ensure t
  :config
  (add-hook 'flycheck-mode-hook #'flycheck-haskell-setup)
  (eval-after-load 'haskell-mode-hook 'flycheck-mode)
  )


(use-package flymake-hlint
  :ensure t
  :config
  (add-hook 'haskell-mode-hook 'flymake-hlint-load))

(use-package lsp-haskell
  :ensure t
  :config
  (add-hook 'haskell-mode-hook #'lsp)
  )
```

# install

[GHCup](https://www.haskell.org/ghcup/)

ghcup をインスコする

```bash
$ ghcup install hls
$ ghcup install hlint
```

ここらへんはいれといた。
