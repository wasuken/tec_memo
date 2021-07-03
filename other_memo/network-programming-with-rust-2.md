# Rustで始めるネットワークプログラミング

[Rustで始めるネットワークプログラミング]( https://booth.pm/ja/items/1410513)

2章だよ。

## buildエラー

```shell
$ sw_vers
ProductName:	Mac OS X
ProductVersion:	10.15.2
BuildVersion:	19C57

$ cargo version
cargo 1.37.0 (9edd08916 2019-08-02)
```

環境はこんな感じで、[teru01/packet-capture](https://github.com/teru01/packet-capture/blob/web-version/Cargo.toml)

のリポジトリの通りに書いてcargo build実行したらエラー吐いた。

ログ見てみるとpnetのインストール時にipなんたらとpnet_なんたらみたいなの色々取り込んでるんだけど、

pnet系のバージョンがあってない。tomlでは0.22.0入れようとしてるのに一部のpnet系crateがおそらく最新の0.25.0を入れようとして

案の定そんな関数ないよってエラーが出て死んでる。微妙に似てないエラーもissue報告されてる。

[Firecracker unittests are not compiling (external dependency problem) #190](https://github.com/firecracker-microvm/firecracker/issues/190)

これって結局pnet_macrosとpnet_packetのバージョンを合わせてないことが原因のやつっぽいので

私のところでもそれっぽいことが発生してるだけではないのかという認識。

多分直す方法はpnet系のバージョンを全て0.22.0とかに揃えれてやれば動くんだろうけど、

めんどくさいのでpnetを0.25.0にあげた。そしたら通った。cargo cleanを忘れて少し焦ったのは内緒。

## 頑張って改良してみる。

```rust
fn ipv4_handler(ethernet: &EthernetPacket){
	if let Some(packet) = Ipv4Packet::new(ethernet.payload()){
		match packet.get_next_level_protocol(){
			IpNextHeaderProtocols::Tcp => {
				tcp_handler(&packet);
			}
			IpNextHeaderProtocols::Udp => {
				udp_handler(&packet);
			}
			_ => {
				info!("Not a TCP or UDP packet");
			}
		}
	}
}

fn ipv6_handler(ethernet: &EthernetPacket){
	if let Some(packet) = Ipv6Packet::new(ethernet.payload()){
		match packet.get_next_header(){
			IpNextHeaderProtocols::Tcp => {
				tcp_handler(&packet);
			}
			IpNextHeaderProtocols::Udp => {
				udp_handler(&packet);
			}
			_ => {
				info!("Not a TCP or UDP packet");
			}
		}
	}
}
```

このコード、最初にインスタンスを生成するクラスが違うだけであとはほぼ同じっぽいので

抽象化できるのではと思ったので挑戦はしてみる。

### ipv4Packet

[Struct pnet::packet::ipv4::Ipv4Packet](https://docs.rs/pnet/0.12.0/pnet/packet/ipv4/struct.Ipv4Packet.html)

なんとなく、ipはipででっかいtraitみたいなのがあって、それをmixinして?ipv4,ipv6と書いているのかなと思ったけど、

その儚い希望はdocsを見て消えた。できるのかもしれないけど、そこまでして共通化したいものでもない上に

大抵の場合速度を犠牲にしたり、処理が余計に長くなりそうでもあるので今回はここまでとする。

## Rustでわからなかったところ

### Option、Result

[RustでOption値やResult値を上手に扱う](https://qiita.com/tatsuya6502/items/cd41599291e2e5f38a4a)

Rustの基礎わかるって言っといてこれわからんやつは一からやり直した方がいい(自己紹介)。

とりあえず記事読んで多少補完した。


# 所感

ほとんど写経だけじゃねえか。
