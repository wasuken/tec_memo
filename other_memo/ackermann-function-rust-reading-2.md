# ackermann-function-rust-reading(2020-01-19 15:49:27)

とりあえずRustの方は全部読んだ。

DDRの方はやるかわからないので、とりあえずここまでで終わる。

[アッカーマン関数の計算過程を表示する (その↑) / DDRの足運び最適化問題を解く](https://booth.pm/ja/items/1575590)

やっていきその2。

ソースコードのリポジトリはここらしい。

[esplo/ackprinter-book-supplements](https://github.com/esplo/ackprinter-book-supplements)

# 4章

## 知識がゴミすぎて読み取れない

対象読者に記載通りの進行なので、ところどころ端折られてよくわからないところがあったが、

そこはGithubのコードをみて頑張った。

一つ、気になったのがいくつかあって、

[ackprinter-book-supplements/src/bin/print_ary_no_memo.rs](https://github.com/esplo/ackprinter-book-supplements/blob/master/src/bin/print_ary_no_memo.rs)

ary_prefixerって本にコード載ってないけど、各自実装よろとか、Githubから引っ張ってきてみたいなこと

どっかに書かれてたの見落としたか...?

## ベンチマークの書き方

こことか

[ベンチマークテスト](https://doc.rust-jp.rs/the-rust-programming-language-ja/1.9/book/benchmark-tests.html)

こことか見て頑張った。

[非nightlyなRustプロジェクトでベンチマークを使用する方法](https://yamash.hateblo.jp/entry/2019/02/07/231211)

つまりこういうこと?

```rust
#[cfg(test)]
mod tests {
    use super::*;
    use test::Bencher;

	// Omitted test codes.

    #[bench]
    fn bench_a(b: &mut Bencher){
        // something test...
    }
    #[bench]
    fn bench_b(b: &mut Bencher){
		// something test...
    }
}
```

Githubに公開されてないっぽいコードなので省略するけど。

benchマークって同じファイルにガリガリ描く方式ならこれかな。

# 5章

タイトル通り、アッカーマン関数の実装で終わった。これ以上先に行かれると私がついていけないぞ。

メモ化用のテーブルもメモリに持つのはきつそうなのでリソースを増やすか、外部の遅い補助記憶に頼るか、

さらに遅いDBを経由したりするのか....これはないか。

アッカーマン関数は並列化は想像つかないけど、頑張ればいけるのかな。

# 6章

まあ、あとがきなので特に描くことはないけど、

寿司虚空編は以前から知っていたが、怖そうな内容だったので見てなかったが少し興味が湧いてきた。

ツイッターで紹介していただいた巨大数論に目を通してから見てみようと思う。

# 結局何を得たの

* アッカーマン関数、巨大数、ふぃっしゅ数等の存在。

* 簡単なアッカーマン関数の実装方法。

* Rust周辺知識(かなり断片的)
