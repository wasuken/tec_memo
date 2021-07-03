# よくわかるgRPC

[【DL販売】よくわかるgRPC - castaneai - BOOTH](https://booth.pm/ja/items/1557285)

絵が可愛い。

1章スタート。

## 前調べ

[gRPC](https://grpc.io/)

> gRPC is a modern open source high performance RPC framework that can run in any environment.

多くの環境で動作する近代的なオープンソースの高性能RPCフレームワーク(?)

RPCってなんだろう。

[RPC - Wikipedia](https://ja.wikipedia.org/wiki/RPC)

[遠隔手続き呼出し - Wikipedia](https://ja.wikipedia.org/wiki/%E9%81%A0%E9%9A%94%E6%89%8B%E7%B6%9A%E3%81%8D%E5%91%BC%E5%87%BA%E3%81%97)

> リモートプロシージャコールのこと
> 引用元: [RPC - Wikipedia](https://ja.wikipedia.org/wiki/RPC)

>プログラムから別のアドレス空間（通常、共有ネットワーク上の別のコンピュータ上）にあるサブルーチンや手続きを実行することを可能にする技術。その際に遠隔相互作用の詳細を明示的にコーディングする必要がない。つまり、プログラマはローカルなサブルーチン呼び出しと基本的に同じコードをリモート呼び出しについても行う。
> 引用元: [遠隔手続き呼出し - Wikipedia](https://ja.wikipedia.org/wiki/%E9%81%A0%E9%9A%94%E6%89%8B%E7%B6%9A%E3%81%8D%E5%91%BC%E5%87%BA%E3%81%97)

なるほど。

プログラム外から別プログラムの関数を呼ぶみたいなやつか。

[gRPCって何？ - Qiita](https://qiita.com/oohira/items/63b5ccb2bf1a913659d6)

う~ん？中間言語って感じだろうか。そこからGoやらC++やらに変換できるって感じ？

[今さらProtocol Buffersと、手に馴染む道具の話 - Qiita](https://qiita.com/yugui/items/160737021d25d761b353)

中間言語がこのProtocol Buffersかな？

## 実際に進行した部分でわからなかったところ

わからぬ。

流れとしてはとりあえずprotoファイル書いて、そこからgoファイル生成して、

それを利用するclientからserverの関数呼び出すことができた。

仕組みはよくわからんけど、おお〜ってなった。

これを使いこなすと確かに、便利かもしれない。
