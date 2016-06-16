**翻译状态：** 本文是英文页面 [StrongSwan](/index.php/StrongSwan "StrongSwan") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-07，点击[这里](https://wiki.archlinux.org/index.php?title=StrongSwan&diff=0&oldid=437545)可以查看翻译后英文页面的改动。

IPSec 是一个加密和认证标准，可以组建安全虚拟专用网路(VPN).

Linux kernel 已经支持这个标准，但是用户需要配置加密密钥。IPSec VPN 使用 [IKE](https://en.wikipedia.org/wiki/Internet_Key_Exchange "wikipedia:Internet Key Exchange") 协议自动协商密钥的交换，交换方式包括认证、提前共享或同时使用。

通常用服务器上的一个后台进程实现，[strongSwan](https://strongswan.org/) 是一个完全支持 IKEv1 和 IKEv2 的 IKE 后台进程。大部分现代的客户端都支持，包括 Linux, Windows 7, Apple iOS, Mac OSX, FreeBSD and BlackBerry OS.

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 证书](#.E8.AF.81.E4.B9.A6)
    *   [2.1 认证机构](#.E8.AE.A4.E8.AF.81.E6.9C.BA.E6.9E.84)
    *   [2.2 主机证书](#.E4.B8.BB.E6.9C.BA.E8.AF.81.E4.B9.A6)
    *   [2.3 客户端证书](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E8.AF.81.E4.B9.A6)
*   [3 不同的 VPN 模式](#.E4.B8.8D.E5.90.8C.E7.9A.84_VPN_.E6.A8.A1.E5.BC.8F)
    *   [3.1 IPSec 隧道模式](#IPSec_.E9.9A.A7.E9.81.93.E6.A8.A1.E5.BC.8F)
    *   [3.2 IPSec in transport mode](#IPSec_in_transport_mode)
    *   [3.3 IPSec/L2TP](#IPSec.2FL2TP)
*   [4 Secrets](#Secrets)
*   [5 Networking](#Networking)
    *   [5.1 在容器中运行 Strongswan](#.E5.9C.A8.E5.AE.B9.E5.99.A8.E4.B8.AD.E8.BF.90.E8.A1.8C_Strongswan)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 参阅](#.E5.8F.82.E9.98.85)

## 安装

安装软件包 [strongswan](https://aur.archlinux.org/packages/strongswan/)。

## 证书

第一步是生成 X.509 认证，包括一个认证机构(CA)证书，一个服务器证书和至少一个客户端证书。

### 认证机构

首先创建一个自己签名的根 CA 证书:

生成 4096 位 RSA 私钥 `strongswanKey.pem`:

```
$ cd /etc/ipsec.d/
$ ipsec pki --gen --type rsa --size 4096 --outform pem > private/strongswanKey.pem
$ chmod 600 private/strongswanKey.pem

```

生成自签名的 CA 证书 `strongswanCert.pem`，期限是 10 年(3650天),用 PEM 编码格式保存：

```
$ ipsec pki --self --ca --lifetime 3650 --in private/strongswanKey.pem --type rsa --dn "C=CH, O=strongSwan, CN=strongSwan Root CA" \
	   --outform pem > cacerts/strongswanCert.pem

```

可以根据需要修改 Distinguished Name (DN)，country (C), organization (O), and common name (CN)。

通过下面命令查看新生成的证书：

```
$ ipsec pki --print --in cacerts/strongswanCert.pem

```

输出:

```
cert:      X509
subject:  "C=CH, O=strongSwan, CN=strongSwan Root CA"
issuer:   "C=CH, O=strongSwan, CN=strongSwan Root CA"
validity:  not before Nov 22 11:55:41 2013, ok
           not after  Nov 20 11:55:41 2023, ok (expires in 3649 days)
serial:    65:39:93:df:a0:f8:40:03
flags:     CA CRLSign self-signed
authkeyId: 45:30:11:da:a4:0e:0b:0a:a3:41:a5:81:41:ab:d8:04:7a:40:6c:c0
subjkeyId: 45:30:11:da:a4:0e:0b:0a:a3:41:a5:81:41:ab:d8:04:7a:40:6c:c0
pubkey:    RSA 4096 bits
keyid:     dc:15:91:95:04:07:a5:13:69:5f:77:65:26:d7:02:3f:60:ec:73:c8
subjkey:   45:30:11:da:a4:0e:0b:0a:a3:41:a5:81:41:ab:d8:04:7a:40:6c:c0

```

**警告:** CA 的私钥 `/etc/ipsec.d/private/strongswanKey.pem` 必须保存在安全位置，最好放在一个没有网络访问的签名专用服务器。如果此密钥泄露，整个公钥系统就土崩瓦解了。

### 主机证书

此证书被用来认证 VPN 服务器，运行下面命令：

生成 2048 位 RSA 私钥：

```
$ cd /etc/ipsec.d/
$ ipsec pki --gen --type rsa --size 2048 --outform pem > private/vpnHostKey.pem
$ chmod 600 private/vpnHostKey.pem

```

导出公钥并生成被 CA 签名的 `vpnHostCert.pem`，证书有效期是两年(730天),使用完整域名 `vpn.example.com` 作为身份

```
$ ipsec pki --pub --in private/vpnHostKey.pem --type rsa | \
	 ipsec pki --issue --lifetime 730 \
	  --cacert cacerts/strongswanCert.pem \
	  --cakey private/strongswanKey.pem \
	  --dn "C=CH, O=strongSwan, CN=vpn.example.com" \
	  --san vpn.example.com \
	  --flag serverAuth --flag ikeIntermediate \
	  --outform pem > certs/vpnHostCert.pem

```

后面的客户端连接配置中，会使用 VPN 服务器的域名或 IP 地址，必须将其加入 Distinguished Name 或 Alternative Name (line11), 最好都包含。请注意把 vpn.example.com 修改为 VPN 的主机名 - 否则客户端和服务器的连接会失败。

**注意:** 如果要使用 Win7 内置的 VPN 客户端，必须按上面例子在主机证书中添加 `serverAuth` 标记。OS X 10.7.3 和更早的版本需要 `ikeIntermediate` 标记。这些标记不影响其它功能，可以放心使用。

查看新生成的证书：

```
$ ipsec pki --print --in certs/vpnHostCert.pem

```

Output:

```
cert:      X509
subject:  "C=CH, O=strongSwan, CN=vpn.example.com"
issuer:   "C=CH, O=strongSwan, CN=strongSwan Root CA"
validity:  not before Nov 22 21:16:51 2013, ok
           not after  Nov 22 21:16:51 2015, ok (expires in 729 days)
serial:    0c:05:d7:d5:57:0e:d9:48
altNames:  vpn.zeitgeist.se
flags:     serverAuth iKEIntermediate 
authkeyId: 9b:57:35:fb:cd:9e:2d:20:37:1d:61:4c:e7:c4:5b:5e:dc:64:ad:fc
subjkeyId: 5f:12:c2:06:ee:2b:1e:cc:5f:78:54:ff:f0:f3:7b:a0:2b:c0:b4:d6
pubkey:    RSA 2048 bits
keyid:     6f:a7:99:60:27:27:09:96:02:c1:b9:d9:7d:c1:b0:10:e3:e1:d5:45
subjkey:   5f:12:c2:06:ee:2b:1e:cc:5f:78:54:ff:f0:f3:7b:a0:2b:c0:b4:d6

```

### 客户端证书

客户端需要个人证书再能使用 VPN. 和生成主机证书类似，只是这里用客户端的电子邮件而不是主机名:

生成 2048 位 RSA 私钥:

```
$ cd /etc/ipsec.d/
$ ipsec pki --gen --type rsa --size 2048 --outform pem > private/ClientKey.pem
$ chmod 600 private/ClientKey.pem

```

导出公钥并用 CA 签名，证书时间是两年。

```
$ ipsec pki --pub --in private/ClientKey.pem --type rsa | \
	 ipsec pki --issue --lifetime 730 \
	  --cacert cacerts/strongswanCert.pem \
	  --cakey private/strongswanKey.pem \
	  --dn "C=CH, O=strongSwan, CN=myself@example.com" \
	  --san myself@example.com \
	  --outform pem > certs/ClientCert.pem

```

将所有证书和密钥用密码打包成 PKCS#12 文件，以方便客户端使用。

```
$ openssl pkcs12 -export -inkey private/ClientKey.pem \
	  -in certs/ClientCert.pem -name "My own VPN client certificate" \
	  -certfile cacerts/strongswanCert.pem \
	  -caname "strongSwan Root CA" \
	  -out Client.p12

```

## 不同的 VPN 模式

最简单的配置方式是用隧道模式运行 IPSec。

### IPSec 隧道模式

可以在 `/etc/ipsec.conf` 找到 VPN 配置，下面配置包含了基本 VPN 服务器需要的选项：

 `/etc/ipsec.conf` 
```
# ipsec.conf - strongSwan IPsec configuration file
config setup

  # By default only one client can connect at the same time with an identical
  # certificate and/or password combination. Enable this option to disable
  # this behavior.
  # uniqueids=never

  # Slightly more verbose logging. Very useful for debugging.
  charondebug="cfg 2, dmn 2, ike 2, net 2"

# Default configuration options, used below if an option is not specified.
# See: https://wiki.strongswan.org/projects/strongswan/wiki/ConnSection
conn %default

  # Use IKEv2 by default
  keyexchange=ikev2

  # Prefer modern cipher suites that allow PFS (Perfect Forward Secrecy)
  ike=aes128-sha256-ecp256,aes256-sha384-ecp384,aes128-sha256-modp2048,aes128-sha1-modp2048,aes256-sha384-modp4096,aes256-sha256-modp4096,aes256-sha1-modp4096,aes128-sha256-modp1536,aes128-sha1-modp1536,aes256-sha384-modp2048,aes256-sha256-modp2048,aes256-sha1-modp2048,aes128-sha256-modp1024,aes128-sha1-modp1024,aes256-sha384-modp1536,aes256-sha256-modp1536,aes256-sha1-modp1536,aes256-sha384-modp1024,aes256-sha256-modp1024,aes256-sha1-modp1024!
  esp=aes128gcm16-ecp256,aes256gcm16-ecp384,aes128-sha256-ecp256,aes256-sha384-ecp384,aes128-sha256-modp2048,aes128-sha1-modp2048,aes256-sha384-modp4096,aes256-sha256-modp4096,aes256-sha1-modp4096,aes128-sha256-modp1536,aes128-sha1-modp1536,aes256-sha384-modp2048,aes256-sha256-modp2048,aes256-sha1-modp2048,aes128-sha256-modp1024,aes128-sha1-modp1024,aes256-sha384-modp1536,aes256-sha256-modp1536,aes256-sha1-modp1536,aes256-sha384-modp1024,aes256-sha256-modp1024,aes256-sha1-modp1024,aes128gcm16,aes256gcm16,aes128-sha256,aes128-sha1,aes256-sha384,aes256-sha256,aes256-sha1!

  # Dead Peer Discovery
  dpdaction=clear
  dpddelay=300s

  # Do not renegotiate a connection if it is about to expire
  rekey=no

  # Server side
  left=%any
  leftsubnet=0.0.0.0/0
  leftcert=vpnHostCert.pem

  # Client side
  right=%any
  rightdns=8.8.8.8,8.8.4.4
  rightsourceip=%dhcp

# IKEv2: Newer version of the IKE protocol
conn IPSec-IKEv2
  keyexchange=ikev2
  auto=add

# IKEv2-EAP
conn IPSec-IKEv2-EAP
  also="IPSec-IKEv2"
  rightauth=eap-mschapv2
  rightsendcert=never
  eap_identity=%any

# IKEv1 (Cisco-compatible version)
conn CiscoIPSec
  keyexchange=ikev1
  # forceencaps=yes
  rightauth=pubkey
  rightauth2=xauth
  auto=add

```

### IPSec in transport mode

### IPSec/L2TP

[L2TP/IPsec VPN client setup](/index.php/L2TP/IPsec_VPN_client_setup "L2TP/IPsec VPN client setup") 页面包含了如何建立一个连接到 IPSec/L2TP 服务器的客户端。这种 IPSec VPN 和纯 IPSec 相比，可以将隧道用于非 IP 包，缺点是需要运行一个额外的 L2TP 后台进程。

## Secrets

strongSwan 需要知道哪些客户端是允许连接到 VPN 的，通过 `/etc/ipsec.secrets` 文件进行配置：

 `/etc/ipsec.secrets` 
```
# This file holds shared secrets or RSA private keys for authentication.

# RSA private key for this host, authenticating it to any other host
# which knows the public part.  Suitable public keys, for ipsec.conf, DNS,
# or configuration of other implementations, can be extracted conveniently
# with "ipsec showhostkey".

: RSA ClientKey.pem
user1 : EAP "topsecretpassword"
user2 : XAUTH "evenmoretopsecretpassword"

```

当 strongSwan 运行时，如果编辑了 /etc/ipsec.secrets，需要重新加载：

```
$ ipsec rereadsecrets

```

## Networking

需要执行下面设备让 VPN 服务器正常的进行 VPN 隧道传输：

 `/etc/sysctl.d/10-net-forward.conf` 
```
# VPN
net.ipv4.ip_forward = 1
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.all.send_redirects = 0

```

上面的 VPN 配置用 DHCP 自动给客户端分配 IP 地址，所以需要一个 DHCP 服务，如果这个服务是运行在 strongSwan 相同的服务器上，需要编辑 `/etc/strongswan.d/charon/dhcp.conf`:

 `/etc/strongswan.d/charon/dhcp.conf` 
```
dhcp {
 force_server_address = yes
 server = 192.168.0.255
}

```

在防火墙中开放如下协议：

*   ESP (Encrypted Secure Payload): Standard IPSec traffic
*   UDP 4500: IPSec traffic in "NAT Traversal" mode
*   UDP 500: Key exchanges (IKE)

最后，[start](/index.php/Start "Start") 并 [enable](/index.php/Enable "Enable") `strongswan` 服务。

### 在容器中运行 Strongswan

要在容器中运行 `strongswan`，比如在 [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") 中，需要类似下面的服务文件：

 `/etc/systemd/system/systemd-nspawn@.service.d/override.conf}` 
```
[Service]
ExecStart=
ExecStart=/usr/bin/systemd-nspawn --quiet --keep-unit --boot --link-journal=try-guest --settings=override --machine=%I --capability=CAP_NET_ADMIN --network-veth 

```

## Troubleshooting

## 参阅

*   [strongSwan 5: How to create your own VPN](https://www.zeitgeist.se/2013/11/22/strongswan-howto-create-your-own-vpn/) — 初始版本的参考，获得作者授权。