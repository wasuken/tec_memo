---
title: "vlan"
date: 2022-01-03
draft: false
---
# vlan



授業以降ふれてなくて、実践でも全然使わなくてたまにでるときに調べなおすのめんどいので



少し時間かけて調べる。



[VLANとは](https://www.infraexpert.com/study/vlanz1.html)



物理とは別にL2で仮想的なLANSegmentを作る技術。



Portごとに設定されるVLANIDで識別する。



## Broadcastの範囲限定



通常のBroadcast送信はSegment全体に送信される。



VLANを設定し、分割することにより、同じ仮想Segment同士以外にBroadcastが飛ばなくなる。



単純に通信量が削減される。



## 複数SwitchをまたぐVLAN



複数SwitchでもVLAN設定可能。



## AccessPortとTrunkPort



[VLAN -AccessPortとTrunkPort](https://www.infraexpert.com/study/vlanz2.html)



### AccessPort



1Portに一つのVLANIDが設定可能。



設定方法にStatic VLANとDynamic VLANが存在する。



#### Static VLAN



手動割当て。楽。



#### Dynamic VLAN



> 接続するデバイスによってポートが動的に所属するVLANを変更できるVLANです。

> 接続するデバイスのMACアドレスにより決定するMACベースVLAN、IPアドレスにより決定するサブネット

> ベースVLAN、ユーザ名などの情報に基づいて決定するユーザベースVLANなど、大きく3種類があります。

引用元: https://www.infraexpert.com/study/vlanz2.html



### TrunkPort



1Portに複数のVLANIDを設定可能。



主にSwitch同士で接続する際に使用する。



そうすることにより、外部にでるVLANが複数ある場合にも同数のVLANPortを用意しなくてもよくなる。



#### Trunking Protocol



TrunkLinkでVLAN用のTag付するProtocolはいくつか存在する。



* IEEE802.1Q



	Ethernet Frameに4byteのVLAN用領域を追加。



* ISL



	Cisco独自のProtocol。Ethernet FrameをISL HeaderとFCSでCapsule化。



[native VLAN](https://e-words.jp/w/%E3%83%8D%E3%82%A4%E3%83%86%E3%82%A3%E3%83%96VLAN.html#:~:text=%E3%83%8D%E3%82%A4%E3%83%86%E3%82%A3%E3%83%96VLAN%E3%81%A8%E3%81%AF%E3%80%81IEEE,VLAN%E3%81%A8%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E3%80%82)



> ネイティブVLANはこのタグが付加されていない本来の形式のフレームを特定のVLANに所属しているとみなして処理する仕組みである。VLANを設定できないコンピュータなどを接続したり、経路上にVLANを理解しない中継機器がある場合でも通信ができるようになる。各ネットワークスイッチへ制御情報を流す管理用ネットワークとして利用されることが多い。

引用元: https://e-words.jp/w/%E3%83%8D%E3%82%A4%E3%83%86%E3%82%A3%E3%83%96VLAN.html#:~:text=%E3%83%8D%E3%82%A4%E3%83%86%E3%82%A3%E3%83%96VLAN%E3%81%A8%E3%81%AF%E3%80%81IEEE,VLAN%E3%81%A8%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E3%80%82



## VTP(VLAN Trunking Protocol)



> VTP（VLAN Trunking Protocol）はトランクポートからVTPアドバタイズメントと呼ばれるメッセージ

> を送信して、スイッチネットワーク全体で設定されているVLAN情報の同期をとるシスコ独自のプロトコル。

> VTPを利用することで、管理者は1台のスイッチに対してVLANの追加、名前変更、削除などを行うだけで

> 同じグループ（ 同じVTPドメイン ）の全てのスイッチにVLANの追加、変更、削除の情報が通知されます。

引用元: https://www.infraexpert.com/study/vlanz5.html



Cisco独自らしいのでどこでも使えるとは思わないほうがよさげだが、



一台の管理用Switch経由でGroup(VTP Domainと表現されてた)全体のSwitchのVLANを管理できるのは



かなり便利。
