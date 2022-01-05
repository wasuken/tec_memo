---
title: "自宅NW開発メモ"
date: 2022-01-03
draft: false
---
# 自宅NW開発メモ



自宅の中と、VPSとかサービスとか合わせて書いてる。



## 今の構成



サーバの名前は艦これやらガヴドロやら動物の名前をつけてるけどあえて伏せておく。



### 回線



J:COMのクソおそうんこうんこ契約。



理由は金がないのと、親の家だから。



### 自宅内



#### A



* Raspberry pi OS



* raspberry pi 3+



* DHCP



* DNS



	dnsmasqで両方まとめて管理してる。



* ゲートウェイ



* VPNクライアント



	設定が楽だからwireguard使ってる。



#### B



* Raspberry pi OS



* raspberry pi 3+



* wi-fi



* samba



	もう使ってない。



#### C



* Raspberry pi OS



* raspberry pi 3+



旧DBサーバ。移行した。



#### D



* Raspberry pi OS



* raspberry pi 3+



旧なんでもサーバ。



自動処理はcronでだいたいここに入れてる。



#### E



* Arch Linux



* raspberry pi 3+



Arch Linuxを試したかったので入れてみたやつ。



前はgitbacket?やらいれてたけど、おもすぎてやめた。



#### F



* Raspberry pi OS



* raspberry pi 4(8GiB)



なろう系ラズパイ。なんでもしてくれる。そのくせ余裕がある。



giteaとNextCloud動かしてるけど涼しい(物理)顔して動いてくれてる。



SSDとHDDいれてる。SSDにgiteaとNextCloudのデータいれてる程度しか活用してないけど、



いずれは定期バックアップとしてHDDにデータを保存していく所存。



#### G



* やっすいタワー型PC



	* Mem: 16GiB



	* CPU: Intel(R) Core(TM) i5-7400 CPU @ 3.00GHz



### 自宅外



#### londone.net



* さくらのVPSで動いてる。



* Arch Linux



* Mem: 512MiB



* CPU: 1 core



* Storage: 25~30GiBくらいだった気がする。



ドメイン通して、ブログ立ててる。それだけ。



MySQLにはしてない。いずれVPNつないで、自宅NWのDBとやり取りするようにできたらいいかもしれない。



たぶんやるとしても最後の方。



#### VPS-VPN



* VPNサーバを立ててるサーバ。



* さくらのVPSで動いてる。



* Arch Linux



* Mem: 2GiB



* CPU: 3 core (lscpuだとIntel(R) Xeon(R) Gold 6212U CPU @ 2.40GHzってなってた)



* Storage: 25~30 + 200GiB



VPNサーバなのでいろいろ情報を集約したいなーとか考えたりした結果、



londone.netよりリッチな構成になった。



なお、情報は自宅NWに集めた模様。



そろそろ200GiB活用したい。
