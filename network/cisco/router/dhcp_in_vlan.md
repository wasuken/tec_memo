# 特定のVLAN内でDHCPを配布する。

show running-configだとここらへんが該当する。

switch port周り

```cisco
~~
interface FastEthernet2
 switchport access vlan 10
 no ip address
!
interface FastEthernet3
 switchport access vlan 10
 no ip address
!
~~
```

dhcp周り

```cisco
~~~
ip dhcp excluded-address 192.168.25.151 192.168.25.254
!
ip dhcp pool hackers.me
 import all
 network 192.168.25.0 255.255.255.0
 default-router 192.168.25.254
 dns-server 192.168.25.254
 domain-name hackers.me
 lease 0 6
!

~~~
```

## 作業内容要約

やりたいことの手順がほぼ全部かいてあるPage。

[Configure DHCP Server for multiple VLANs on the Switch](https://www.computernetworkingnotes.com/ccna-study-guide/configure-dhcp-server-for-multiple-vlans-on-the-switch.html)

1. switchportにvlanを設定

2. dhcp設定

3. vlanでdhcpと対応するIP Addressを設定。

### 1. switchportにvlanを設定

vlanの作成、10を指定。vlan 10は適当。

```cisco
(config)# vlan 10
```

対象interfaceにaccess modeで指定して、vlan 10を設定。

```cisco
(config-if)# switchport mode access
(config-if)# switchport access vlan 10
```

### 2. dhcp設定

```cisco
(config)# ip dhcp pool unchi
(config-dhcp)# import all
(config-dhcp)# network 192.168.100.0 255.255.255.0
(config-dhcp)# default-router 192.168.100.254
(config-dhcp)# dns-server 192.168.100.253
(config-dhcp)# domain-name unchi.com
```

### 3. vlanでdhcpと対応するIP Addressを設定。

vlan 10にIP Addressを設定。

IP Addressは適当。

```cisco
(config)# interface vlan 10
(config-if)# ip address 192.168.100.254 255.255.255.0
```
