本文中介绍了基于 IPsec 的 VPN 服务器的基本的安装与配置过程。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 设置 IPsec 默认参数](#.E8.AE.BE.E7.BD.AE_IPsec_.E9.BB.98.E8.AE.A4.E5.8F.82.E6.95.B0)
    *   [2.2 打开 psk aggressive 模式](#.E6.89.93.E5.BC.80_psk_aggressive_.E6.A8.A1.E5.BC.8F)
    *   [2.3 配置虚拟 IP 地址池和 DNS](#.E9.85.8D.E7.BD.AE.E8.99.9A.E6.8B.9F_IP_.E5.9C.B0.E5.9D.80.E6.B1.A0.E5.92.8C_DNS)
        *   [2.3.1 打开虚拟 IP 地址功能](#.E6.89.93.E5.BC.80.E8.99.9A.E6.8B.9F_IP_.E5.9C.B0.E5.9D.80.E5.8A.9F.E8.83.BD)
        *   [2.3.2 配置客户端虚拟 IP 地址池](#.E9.85.8D.E7.BD.AE.E5.AE.A2.E6.88.B7.E7.AB.AF.E8.99.9A.E6.8B.9F_IP_.E5.9C.B0.E5.9D.80.E6.B1.A0)
        *   [2.3.3 配置 DNS](#.E9.85.8D.E7.BD.AE_DNS)
    *   [2.4 允许一个用户多个连接](#.E5.85.81.E8.AE.B8.E4.B8.80.E4.B8.AA.E7.94.A8.E6.88.B7.E5.A4.9A.E4.B8.AA.E8.BF.9E.E6.8E.A5)
    *   [2.5 用户认证](#.E7.94.A8.E6.88.B7.E8.AE.A4.E8.AF.81)
        *   [2.5.1 设定用户认证后端](#.E8.AE.BE.E5.AE.9A.E7.94.A8.E6.88.B7.E8.AE.A4.E8.AF.81.E5.90.8E.E7.AB.AF)
            *   [2.5.1.1 使用 radius 服务](#.E4.BD.BF.E7.94.A8_radius_.E6.9C.8D.E5.8A.A1)
        *   [2.5.2 设定 IKE 交换算法](#.E8.AE.BE.E5.AE.9A_IKE_.E4.BA.A4.E6.8D.A2.E7.AE.97.E6.B3.95)
            *   [2.5.2.1 IKEv1(Cisco IPsec)](#IKEv1.28Cisco_IPsec.29)
            *   [2.5.2.2 IKEv2](#IKEv2)
    *   [2.6 设置防火墙和 NAT](#.E8.AE.BE.E7.BD.AE.E9.98.B2.E7.81.AB.E5.A2.99.E5.92.8C_NAT)
        *   [2.6.1 打开 IP 转发](#.E6.89.93.E5.BC.80_IP_.E8.BD.AC.E5.8F.91)
        *   [2.6.2 iptables](#iptables)
        *   [2.6.3 (可选)自动添加FORWARD到iptables](#.28.E5.8F.AF.E9.80.89.29.E8.87.AA.E5.8A.A8.E6.B7.BB.E5.8A.A0FORWARD.E5.88.B0iptables)
*   [3 启动](#.E5.90.AF.E5.8A.A8)
    *   [3.1 直接启动](#.E7.9B.B4.E6.8E.A5.E5.90.AF.E5.8A.A8)
    *   [3.2 使用 systemd](#.E4.BD.BF.E7.94.A8_systemd)

## 安装

安装位于[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")的 [strongswan](https://aur.archlinux.org/packages/strongswan/)。

或者，可以从 [strongSwan](http://www.strongswan.org/download.html) 官方网站下载源码包自行编译安装：

```
$ ./configure --enable-eap-identity --enable-eap-md5 \
--enable-eap-mschapv2 --enable-eap-tls --enable-eap-ttls --enable-eap-peap \
--enable-eap-tnc --enable-eap-dynamic --enable-eap-radius --enable-xauth-eap \
--enable-xauth-pam --enable-dhcp --enable-openssl --enable-addrblock --enable-unity \
--enable-certexpire --enable-radattr --enable-tools --enable-openssl --disable-gmp
# make
# make install

```

## 配置

### 设置 IPsec 默认参数

可参考以下内容修改`/etc/ipsec.conf`：

 `/etc/ipsec.conf ` 
```
config setup

    conn %default
        ikelifetime=60m  
        keylife=20m  
        rekeymargin=3m  
        rekey=no  
        keyingtries=1  
        keyexchange=ike
        leftsubnet=0.0.0.0/0  
        leftfirewall=yes
        rightsourceip=192.168.99.128/25
        right=%any 
        dpdaction=clear
        dpddelay=300s
        dpdtimeout=1h

```

### 打开 psk aggressive 模式

**注意:** 这一步只对 strongswan>=5.0.1 有效，没有它的话将不支持在很多客户的上 IKEv1 使用的 aggressive 模式。这意味着很多 CISCO IPsec 客户端将无法登录。
 `/etc/strongswan.conf` 
```
...
charon {
    ...
    i_dont_care_about_security_and_use_aggressive_mode_psk = yes
    ...

```

### 配置虚拟 IP 地址池和 DNS

客户端连接后需要一个虚拟 IP 地址和 DNS 服务器，此处设定了用于分配的 IP 地址范围和 DNS 服务器。

#### 打开虚拟 IP 地址功能

 `/etc/strongswan.conf` 
```
...
charon {
    ...
    install_virtual_ip = yes
    ...

```

#### 配置客户端虚拟 IP 地址池

设置 IP 地址池范围：

 `/etc/ipsec.conf ` 
```
config setup
    ...
    conn %default
        ...   
        rightsourceip=192.168.99.0/24  
        ...

```

你可以随意指定一个[私有IP地址](https://en.wikipedia.org/wiki/Private_network "wikipedia:Private network")范围内的地址池，这里我们指定了192.168.99.1~254。

设置客户端虚拟 IP 清理策略：

 `/etc/ipsec.conf ` 
```
config setup
    ...
    conn %default
    ...
        dpdaction=clear
        dpddelay=300s
        dpdtimeout=1h
    ...

```

#### 配置 DNS

 `/etc/strongswan.conf` 
```
...
charon {
    ...
    dns1=208.67.222.222
    dns2=8.8.8.8
    ...

```

此处指定了 208.67.222.222 和 8.8.8.8 两个公用 DNS 服务器，你可以根据自己的需要来设置。

### 允许一个用户多个连接

这一步不是必要的，如果不做配置，一个用户默认只能有一个在线连接。不过非常建议配置这一步，因为限制用户连接个数可以交给[用户认证后端](#.E8.AE.BE.E5.AE.9A.E7.94.A8.E6.88.B7.E8.AE.A4.E8.AF.81.E5.90.8E.E7.AB.AF)来实现。

修改配置文件，在如下位置添加`duplicheck.enable = no`和`uniqueids=never`：

 `/etc/strongswan.conf` 
```
...
charon {
    ...
    duplicheck.enable = no
    ...

```
 `/etc/ipsec.conf ` 
```
...
config setup
    ...
    uniqueids=never

    conn %default
        ...

```

### 用户认证

#### 设定用户认证后端

##### 使用 radius 服务

 `/etc/strongswan.conf` 
```
...
charon {
    ...
    plugins {
        ...
        eap-radius {
        #eap_start = yes  
        accounting = yes  
            servers {
                primary {  
                    address = 127.0.0.1
                    secret = testing123
                    auth_port = 1812  
                    acct_port = 1813  
                }
            }
        }
    ...

```

在 servers {} 内层，你可以指定多个 Radius 服务器，例如 primary,2nd,last1，这里随意起了个名字：primary。

为了支持[IKEv1(Cisco IPsec)](#IKEv1.28Cisco_IPsec.29)，你还需要添加以下内容：

 `/etc/strongswan.conf` 
```
...
charon {
    ...
    plugins {
        ... 
        xauth-eap {  
            backend = radius
        }
    ...

```

#### 设定 IKE 交换算法

以下的交换算法至少需要配置一种，也可以两者并存。

##### IKEv1(Cisco IPsec)

在`/etc/ipsec.conf`中添加下面的内容：

 `/etc/ipsec.conf ` 
```
...
    conn %default
    ...
    conn CiscoIPSec  
        keyexchange=ikev1  
        auto=add  
        aggressive=yes  
        compress=yes  
        ike=aes256-sha1-modp1024!  
        esp=aes256-sha1!   
        leftid=GROUPID
        type=tunnel 
        xauth=server
        leftauth=psk
        rightauth=psk   
        rightauth2=xauth-eap

```

其中`leftid=GROUPID`对应 xauth-psk 验证方式下的 Group ID，可以设定为你想要的值。

在`/etc/ipsec.secrets`中添加下面的内容：

```
%any %any : PSK "GROUPPASS"

```

其中`GROUPPASS`对应 xauth-psk 验证方式下的 Group Password，可以设定为你想要的值。

##### IKEv2

**警告:** IKEv2 这部分还不完整

在`/etc/ipsec.conf`中添加下面的内容：

 `/etc/ipsec.conf` 
```
...
    conn %default
    ...
    conn IPSec-IKEv2  
        keyexchange=ikev2  
        auto=add  
        leftauth=pubkey  
        leftcert=serverCert.pem  
        rightauth=eap-radius  
        rightsendcert=never  
        eap_identity=%identity  
        compress=yes
...

```

### 设置防火墙和 NAT

#### 打开 IP 转发

```
# echo "1" > /proc/sys/net/ipv4/ip_forward

```

修改`/etc/sysctl.d/10-ip-forward.conf`，使配置在每次系统启动时生效:

```
net.ipv4.ip_forward = 1

```

#### iptables

1.  你需要将[rightsourceip](#.E9.85.8D.E7.BD.AE.E5.AE.A2.E6.88.B7.E7.AB.AF.E8.99.9A.E6.8B.9F_IP_.E5.9C.B0.E5.9D.80.E6.B1.A0)加入 MASQUERADE 或者 SNAT；
2.  你需要将[rightsourceip](#.E9.85.8D.E7.BD.AE.E5.AE.A2.E6.88.B7.E7.AB.AF.E8.99.9A.E6.8B.9F_IP_.E5.9C.B0.E5.9D.80.E6.B1.A0)加入 FORWARD；
3.  你需要放行 UDP 500 和 UDP 4500 端口；
4.  你需要放行 ESP。

*   下面是一个完成的例子，如果你不需要 ssh 和 IPsec 以外的服务的话，可以直接套用:

 `/etc/iptables/iptables.rules` 
```
*nat
:PREROUTING ACCEPT [0:0]
:INPUT ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 192.168.99.0/24 -o eth0 -j MASQUERADE
COMMIT
# Completed on Mon Jul 22 14:53:31 2013
# Generated by iptables-save v1.4.18 on Mon Jul 22 14:53:31 2013
*filter
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
:OUTPUT ACCEPT [432:67301]
-A INPUT -p tcp -m tcp --dport 22 -j ACCEPT
-A INPUT -p udp -m udp --dport 500 -j ACCEPT
-A INPUT -p udp -m udp --dport 4500 -j ACCEPT
-A INPUT -p icmp -j ACCEPT
-A INPUT -p esp -j ACCEPT
-A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
-A INPUT -s 127.0.0.0/24 -d 127.0.0.0/24 -j ACCEPT
-A INPUT -p tcp -j REJECT --reject-with tcp-reset
-A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
-A INPUT -j REJECT --reject-with icmp-proto-unreachable
-A FORWARD -s 192.168.99.0/24 -j ACCEPT
COMMIT

```

重新启动 iptables：

```
# systemctl restart iptables

```

*   关于iptables的设定，请参考[Iptables (简体中文)](/index.php/Iptables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Iptables (简体中文)")

#### (可选)自动添加FORWARD到iptables

在需要的ConnSection中添加 `leftfirewall=yes`:

 `/etc/ipsec.conf ` 
```
config setup
    ...
    conn %default
        ...
        leftfirewall=yes
        ...

```

这个选项的作用是当客户端连上后，执行strongswan默认的_updown脚本，自动在iptalbes添加对于客户端虚拟地址的FORWARD规则。所以如果设置了它，可以删除`/etc/iptables/iptables.rules`中的`-A FORWARD -s 192.168.99.0/24 -j ACCEPT`。

## 启动

### 直接启动

让 strongswan 在前台运行：

```
# ipsec start --nofork

```

### 使用 systemd

[AUR](/index.php/Arch_User_Repository_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch User Repository (简体中文)")的 [strongswan](https://aur.archlinux.org/packages/strongswan/) 包含了 service 文件。

启动服务：

```
# systemctl start strongswan.service

```

开机自动启动：

```
# systemctl enable strongswan.service

```

**小贴士:**

可以使用：

```
# journalctl -u strongswan -f

```

显示进程打印的信息，你会看到和[直接启动](#.E7.9B.B4.E6.8E.A5.E5.90.AF.E5.8A.A8)一样的信息。 具体参见[systemd (简体中文)#过滤输出](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BF.87.E6.BB.A4.E8.BE.93.E5.87.BA "Systemd (简体中文)")