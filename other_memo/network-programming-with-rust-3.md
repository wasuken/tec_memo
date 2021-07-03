# Rustで始めるネットワークプログラミング

[Rustで始めるネットワークプログラミング](https://booth.pm/ja/items/1410513)

3章やよ。

## FINスキャン

[FINスキャン]( https://wa3.i-3-i.info/word15555.html)

FINパケットを対象ホストの各ポートに片っ端から送りつけて、

RSTパケットが返ってきたらそこは空いてると判断できるわけか。

ちなみに、本にはこれについてもう少し詳しく、わかりやすく書いてあるが、

私はその方面に関する詳細は書かないので知りたければ買うべきだよ。

## NULLスキャン

[TCP Nullスキャン]( https://www.wdic.org/w/WDIC/TCP%20NULL%E3%82%B9%E3%82%AD%E3%83%A3%E3%83%B3)

[NULLスキャン]( https://www.shadan-kun.com/blog/measure/772/#03_e)

フラグを何にも立てない状態でパケットを送信する。RSTが返ってきたらそのポートでサービスが動いていないことがわかる。

何も返ってこなければ稼働している。

## X-masスキャン

[Tcp X-masスキャン]( https://www.hotfix.jp/archives/word/2006/word06-07.html)

コネクションが確立してない状態で、FIN,URG,PSHを立てたパケットを送り、何も返ってこなければ開いている、

RSTが返ってきたら閉じていると判断できる。

## macOSのみ注意

.envに追加で必要なものが出てくる。

```config
MY_IPADDR = <my ip address>
MY_PORT = 33333
MAXIMUM_PORT_NUM = 1023
```

ここから追加

```config
DEFAULT_GATEWAY = <default gateway mac address>
IFACE = <target newtork interface>
MY_MACADDR = <my mac address>
```

まあ、実行時エラーで吐くからすぐわかるんだけどね。

## datalink, transport

[web-version:main.rs]( https://github.com/teru01/port-scanner/blob/web-version/src/main.rs)
と
[macOS:main.rs]( https://github.com/teru01/port-scanner/blob/macOS/src/main.rs)両方を眺めて気がついたんだけど、

web-versionがpnet::transport使ってて、

macOSはpnet::datalink使ってる。

なんで使い分けてんだろう。

ソースコードも当然変わってくるんだけど、

大きく違うのはbuild_packet関数で、

macOSの方はdatalink層から頑張って組み立ててるのに対して、

web-versionはいきなりtcpの組み立てから始まって、それ未満は何も触れてない。

receive_packetsもざっとみた感じ違う。けど流れは同じっぽい。

気づいた点一部挙げてみると、macOSには手抜きの部分がない。できなかったのかそれとも忘れていたのか。

あとweb-version,transportにはinterfaceいらないっぽい。

## いつものbuildではなく、実行時エラー

macOSブランチのコード丸パクリしても

	thread '<unnamed>' panicked at 'invalid default gateway: InvalidComponent', src/libcore/result.rs:999:5

みたいなエラーが出てダメだった。

.envが原因ぽいよね〜とアドバイスをいただいたりしたので、それを頭に入れつつ

default gateway周りのソースコードを再度読み直しつつ、ちゃんと設定読み込めてるのかな〜と確認用のコードを入れてると

ふと気になる内容が、

shell「これタイプ不一致だぜ。MacAddressなんたらの型で渡せ。」(エラーログ探しても見つからなかったのでそれっぽくかいた)

IPアドレス形式じゃないのか!?

というわけで、MacAddress形式に変更して再度動かしてみると。

動きました。クソが。

## Rustコードでわからなかったところ。

ぞい君さぁ、Rustわからないんなら並行して自転車本読み直すとかしようよ！ガキじゃないんだからさぁ！

### parse

MacAddress周りのコード見てる時になんやこれって思った。

[Rust メモ 文字列](https://totem3.hatenablog.jp/entry/2016/10/14/084900)

いい感じに変換してくれる関数っぽい?

これだけの理解はちょっと怖いな。

こういう時はdoc.rust-lang.orgでしょ。

[parse](https://doc.rust-lang.org/std/primitive.str.html#method.parse)

ここからソースに飛べるんだけど、

[mod.rs.html#4047-4049]( https://doc.rust-lang.org/src/core/str/mod.rs.html#4047-4049)

なるほど、FromStr::from_strを読んでいると

[Trait std::str::FromStr](https://doc.rust-lang.org/std/str/trait.FromStr.html)

んでFromStrの説明を見ると、strを解析するみたいな子とかいてある。

だからやっぱりいい感じ変換ってのは間違ってないっぽい。

これ以上深掘りすると時間が足りないのでここまでにしておく。
