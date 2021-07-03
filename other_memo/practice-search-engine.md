# 検索エンジン開発練習

なぜ練習か、人様のプロジェクトを思いっきりパクったから。

[takatori/go-tinysearch](https://github.com/takatori/go-tinysearch)

というのも、先日[【電子版】Goで検索エンジンに入門する本](https://booth.pm/ja/items/1576277)という本を購入したが、

Goより学びたい言語が存在したので(Clojure)、じゃあ書き換えてみようということで挑戦した。

これ私の書いたやつね[wasuken/clj-tinysearch](https://github.com/wasuken/clj-tinysearch)。

本の解説とかはしない。気になったら買おう。

* 実装がかなり違う

そりゃそうだ。Go側は割と手続きチック?Goチック?に書かれてるが、私はClojureでそういう風に書くの苦手なので意図的に変えてる。

## 実装がかなり違う(エラー対処がない)

ごめん。

その他に次いては、私のリポジトリのれどめに書いてる。

## 辛かったとこ

### 型をうまく設定できない

とりあえず自作の型作ってそれを型として書くとエラーになるんすよね。は？

んでそれは対処できたんすけど、今度はdefrecordの返り値の型設定の時になぜか返り値はObjectだボケって怒られるんすわ。は？は？は？

->諦めました。

### エラー祭り(searcher)

[searcher.clj#L43](https://github.com/wasuken/clj-tinysearch/blob/master/src/clj_tinysearch/searcher.clj#L43)

この見るからにゴミみたいな関数あるじゃないっすか。

最初書いた時ここバグだらけでコンパイルエラー出まくりだったんすね。

んでやっとコンパイルエラー消えたと思ったら今度は結果がnilだらけ。

それも直したら結果がかなり違う。~~ざけんな~~
