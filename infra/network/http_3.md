---
title: "http/3"
date: 2022-01-03
draft: false
---
# http/3



## 参考になりそうLinks



[HTTP/3 とは？｜BLOG｜サイバートラスト](https://www.cybertrust.co.jp/blog/ssl/knowledge/about-http3.html)



[curl作者のOnline公開本?](https://http3-explained.haxx.se/ja)



[Webの最新プロトコル「HTTP/3」、高速な処理を実現する仕組み | 日経クロステック（xTECH）](https://xtech.nikkei.com/atcl/nxt/column/18/01606/032400004/)



## 調査



### [HTTP/3とは何か？−UDPベースの高速新プロトコルの概要](https://kinsta.com/jp/blog/http3/)



UDP上に作成されており、そのため再送待ちの際にStream全体が停止しない。



つまり、transport層Protocol。



しかし、UDP層より上で再送や順序付制御を提供している。



UDPは上記の理由により高速である反面、CPU負荷が非常に高くなる傾向がある。



QUICは接続確立時に固有のCIDを発行し、それで識別する。



これにより通信中にNetworkが変更されても通信が中断されない。



### [UDP上の転送Protocol](https://http3-explained.haxx.se/ja/the-protocol/feature-udp)



QUICはUDPのUser空間に実装された転送Protocol。



QUICではStream到着順序は保証されない。



故にStreamAがこけても、Bは関係なしに継続される。



従来のProtocolではAでPacket Lossが起きるとBも止るようになっていた。



QUICはTLSv1.3の0-RTThand shake時にdataを含めることができる。



通常よりはやくStart Dashがキレるので、時間短縮できそう。



---



[素早いHandShake](https://http3-explained.haxx.se/ja/the-protocol/feature-handshakes)



ここまで。



---



## load balancing



[インフラエンジニアなら気になるQUICのロードバランサ (方式編)](https://medium.com/nttlabs/quic-load-balancer-design-82c5fbae8305)



clientから見るとconnectionを張っているend hostはlayer7。



### layer4による分散を行った場合



client - lb - srv



にて、lb -> srvにてconnectionを伸ばした場合、



通常UDPのlbは4タプル情報(送信先IPアドレス, 送信元IPアドレス, 送信先ポート番号, 送信元ポート番号)



にて分けますが、QUICでは同一のconnectionでもこれが一致するとは限らない。



quicはclientのIP address, portが変更されてもconnection維持は可能。



また、変更時のnegotiation内部は暗号化されているので、追跡も不可能。https://mintblog.hatenablog.com/?_ga=2.66752366.15256710.1632532426-1977540149.1625879509
