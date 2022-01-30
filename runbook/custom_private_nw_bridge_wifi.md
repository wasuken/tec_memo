---
title: "検証NWに少し手を加えた"
description:
date: 2022-01-30
draft: false
categories:
  - "home-nw"
tags:
  - "network"
  - "raspi"
  - "linux"
  - "dnsmasq"
  - "hostapd"
  - "bridge"
---
# 検証NWに少し手を加えた

* Wifi復活

	* 有線接続したときと同じようにIPをふるように

	* dhcpcdを無効にした

これだけなんだが、ハマったよね。。。

## 環境

* OS: Raspberrypi OS
* wifiルータ: hostapd
* DHCP、DNSサーバ: dnsmasq

## ブリッジ接続したwifiインタフェースと有線インタフェースに等しく？DHCP傘下に含める

クソ長いこと書いてるけど同じようにIPふりたいってだけ。

### install

ラズパイのRaspberrypi OSなのでbridge-utilsはいれた。

その上でeth0に振っていたIP関連の情報を

ブリッジ用のネットワークインタフェース(br0と設定した)の方に振る。

### hostapd設定

bridge=br0
を入れただけだった。

### dnsmasq

こいつはinterfaceをbr0へ変更した。

### ipup

/etc/network/interface周りの動きって実は全然理解してなかったりする。

ここでは有線、無線インタフェースを立ち上げつつ、

br0にIP振って、

```
bridge_ports <有線IF> <無線IF>
```

IF=インタフェース

これくらいか。
