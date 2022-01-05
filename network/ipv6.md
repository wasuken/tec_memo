---
title: "疑問点の抽出"
date: 2022-1-3
draft: false
---
# 疑問点の抽出



## IPアドレスの重複



[TCP/UDP - IPv6 の基本](https://www.itbook.info/study/ipv6.html)



> IPv6 アドレスをもらいたいノードがネットワークプレフィックスを

> 要求すれば、そのネットワーク上に存在している IPv6 ルータが

> ネットワークプレフィックスを提供してくれます。

> この情報を元にノードは自身の MAC アドレスや適当なランダムな値から

> 一意の IPv6 アドレスを自動的に設定します。

> この機能を実装することで、運用者は余計な運用コストが必要なくなりますし、

> 利用者も IP アドレスを意識することなく使用できるわけです。



> [TCP/UDP - IPv6 の基本](https://www.itbook.info/study/ipv6.html)



これIPアドレス被ったりしないんだろうか。



->DADという重複チェックみたいなのはあるみたい。



ipv4もarpによるチェック程度しかなさそうなので、そんなのりなのかもしれない。



## RAの際のルータ情報偽装は可能か



RA Guardみたいな対策してなかったらやばそう。



[RA Guard](https://techdocassets.pluribusnetworks.com/netvisor/nv1_611/CG/SupportforRouterAdvertisementRAG.html)



許可されてないデバイスからのRAを破棄するようだ。



# 参考



[ipv6](https://www.itbook.info/cat/ipv6.html)



[IPv6チュートリアル～IPv6化ことはじめ～](https://www.nic.ad.jp/sc-sendai/program/iwsc-sendai-d1-4.pdf)



[IPv6セキュリティ　はじめの一歩](https://www.slideshare.net/kenjiohira1/ipv6-73333661)
