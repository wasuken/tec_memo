# Rustで始めるネットワークプログラミング

[Rustで始めるネットワークプログラミング]( https://booth.pm/ja/items/1410513)

やっていき。例によって、1章ずつやるよ。

[teru01/socket-programming]( https://github.com/teru01/socket-programming/)

公開されてた。

後書いたか覚えてないけど、本の文章については引用等はしないよ。

本の内容をみた上で、それに近いか等しいものを公開されているWebページを引っ張って、

所感等を入れていくスタイルでやるよ。

しっかりした情報を知りたかったら**[買ってください]( https://booth.pm/ja/items/1410513)**。

# ソケット通信

[知ったかぶりをしていたソケット通信の基礎を改めて学んでみる](https://qiita.com/megadreams14/items/32a3eed4661e55419e1c)

どうやらサーバとクライアントそれぞれライフサイクルは決まっているそうだ。

~~まだよく理解してないんだが、UDPもTCPもこの流れは共通してるのか?~~

これはTCPのことをいってるね。

[IC221: Systems Programming (SP16)]( https://www.usna.edu/Users/cs/aviv/classes/ic221/s16/lec/27/lec.html#orgheadline1)

英語記事を頑張って解釈してた。

[RFC: 793]( https://tools.ietf.org/html/rfc793)

結局RFCの仕様書をみたりなんかもした。

## TCPクライアントのライフサイクル

### 1. create

わからん。

### 2. bind

socketに対して、ipaddressとportをbindするフェーズ。

### 3. connect

指定した接続先にconnectするフェーズかな。

### 4. read/write

socketファイルを読んだり、書き込んだりするフェーズ。

### 5. close

通信を終わるフェーズ。


## TCPサーバのライフサイクル

### 1. create

わからん。

### 2. bind

socketに対して、ipaddressとportをbindする。

### 3. listen

bindしたソケットがサーバソケットであることをOSに伝える。

ここら辺はLinuxについてわかってないのでよくわからぬ。

### 4. accept

接続要求があったclientの通信を受け入れる。

### 5. read/write

socketファイルを読んだり、書き込んだりするフェーズ。

### 6. close

通信を終わるフェーズ。

## UDP

[UDPプロトコル]( http://www.picfun.com/lan08a.html)

>２つの機器間の論理的な通信を実行する機能を持っていますが、通信手順は

>単純になっていて相手をアドレスで特定して単純に送受信するだけになって

>います。

>　つまり、相手との間の論理的な通信路を確立する手順を必要としないので、

>複雑な手順が無く、単純な送受信となっています。

>その代わり、誤りチェックや再送手順が無いので、高信頼な通信が必要な場合

>には、アプリケーション側でそれを組み込む必要があります。

なるほどな。

ライフサイクルとか無いっぽい。そりゃそうか。

---

本読みながらコード写経してる時はあんまりわかんなかったけど、

ライフサイクルを知った後だと以前よりは頭に入ってくる。

しかしながら、所々わからない点はあったので調べて書いてみる。

## buf?

下記箇所なんだけど

[socket-programming/src/udp_server.rs]( https://github.com/teru01/socket-programming/blob/web-version/src/udp_server.rs#L7)

```rust
let server_socket = UdpSocket::bind(address)?;
loop{
	let mut buf = [0u8; 1024]; // ここ！
	let (size, src) = server_socket.recv_from(&mut buf)?;
	debug!("Handling data from {}", src);
	print!("{}", str::from_utf8(&buf[..size])?);
	server_socket.send_to(&buf, src)?;
}
```

読み込むサイズかなと思ったけど0がよくわからなかった。

[Rustにっき/10日目・UDP]( https://cha-shu00.hatenablog.com/entry/2019/03/05/194700)

tcpではないんだけどなるほどってなった記述があって、

>bufのサイズとして1024を指定していますが、この値は想定する受信データによって適当に決定します。今回の場合は1024バイトを超えるデータを受信した場合は1025バイト目以降のデータは破棄されます。

そういうことか。tcpは確か分割して送信するみたいなことどこかに書いてあった気がするので破棄はされないんじゃないんですかね。

けど0はなんなのかわからない。なら試してみよう。

が、だめ。全然わからん。8にしたり、1にしたり、128にしたりしたけどわからんかった。

才能がない。ゴミ。努力も足りない。

開始位置とかかと思ってたけど、違うっぽい。公式とかに解説とかも書いてない。みてるとこが悪いのかも知れない。

ソースコード読もうと思ったけどself.0ってどこ挿してるのかわけわからなすぎて泣いた。

カフェで何度か叫びそうになった。理性君に負けたので叫ばなかったけど。

[mod.rs.html#1604]( https://doc.rust-lang.org/src/std/io/mod.rs.html#1604)

これが実装に近いやつかも知れない。けどパッとみただけじゃ内容わからん。

## thread

[Function std::thread::spawn]( https://doc.rust-lang.org/std/thread/fn.spawn.html)

serverはclientごとにsocket()しないといけないみたいなのでthread::spawnで並行に処理するのはわかる。

一方でudpは一つで捌いている。う〜ん？ここよくわからん。

# 所感

割と時間かかった。特にRFCとかRustのコード追いかけたあたり。なお結果には結びつかんかった模様。

この本、結構わかりやすくて良いと思った。まだ1章だけど。

1周目であり、まだ入門程度で深掘りしすぎて潰れてもあれなので今はこれくらいにしておく。

負け惜しみじゃん。
