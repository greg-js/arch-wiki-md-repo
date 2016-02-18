本文中介绍了 [OpenVPN](http://openvpn.net) 的基本的安装与配置过程，适用于个人使用与小型商业使用。要了解更多信息，请访问官方网站 [HOWTO](http://openvpn.net/index.php/open-source/documentation/howto.html)、[OpenVPN 2.3 手册页](https://community.openvpn.net/openvpn/wiki/Openvpn23ManPage) 以及 [Manual](http://openvpn.net/index.php/open-source/documentation/manuals.html)。

OpenVPN 是一个健壮的、高度灵活的 [VPN](https://en.wikipedia.org/wiki/VPN "wikipedia:VPN") 守护进程。它支持 [SSL/TLS](https://en.wikipedia.org/wiki/SSL/TLS "wikipedia:SSL/TLS") 安全、[Ethernet bridging](https://en.wikipedia.org/wiki/Bridging_(networking) "wikipedia:Bridging (networking)")、经由[代理](https://en.wikipedia.org/wiki/Proxy_server "wikipedia:Proxy server")的 [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol "wikipedia:Transmission Control Protocol") 或 [UDP](https://en.wikipedia.org/wiki/User_Datagram_Protocol "wikipedia:User Datagram Protocol") [隧道](https://en.wikipedia.org/wiki/Tunneling_protocol "wikipedia:Tunneling protocol")和 [NAT](https://en.wikipedia.org/wiki/Network_address_translation "wikipedia:Network address translation")。另外，它也支持动态 IP 地址以及 [DHCP](https://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol "wikipedia:Dynamic Host Configuration Protocol")，可伸缩性足以支持数百或数千用户的使用场景，同时可移植至大多数主流操作系统平台上。

OpenVPN 与 [OpenSSL](http://www.openssl.org) 库紧密相关，并由此获得许多加密功能。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 内核配置](#.E5.86.85.E6.A0.B8.E9.85.8D.E7.BD.AE)
*   [3 准备证书和密钥数据](#.E5.87.86.E5.A4.87.E8.AF.81.E4.B9.A6.E5.92.8C.E5.AF.86.E9.92.A5.E6.95.B0.E6.8D.AE)
*   [4 配置服务器](#.E9.85.8D.E7.BD.AE.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [4.1 复制默认服务器配置文件](#.E5.A4.8D.E5.88.B6.E9.BB.98.E8.AE.A4.E6.9C.8D.E5.8A.A1.E5.99.A8.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
    *   [4.2 使用 PAM 和密码认证](#.E4.BD.BF.E7.94.A8_PAM_.E5.92.8C.E5.AF.86.E7.A0.81.E8.AE.A4.E8.AF.81)
    *   [4.3 使用证书认证](#.E4.BD.BF.E7.94.A8.E8.AF.81.E4.B9.A6.E8.AE.A4.E8.AF.81)
    *   [4.4 通过服务器路由](#.E9.80.9A.E8.BF.87.E6.9C.8D.E5.8A.A1.E5.99.A8.E8.B7.AF.E7.94.B1)
*   [5 客户端配置](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.85.8D.E7.BD.AE)
    *   [5.1 使用密码认证](#.E4.BD.BF.E7.94.A8.E5.AF.86.E7.A0.81.E8.AE.A4.E8.AF.81)
    *   [5.2 证书验证](#.E8.AF.81.E4.B9.A6.E9.AA.8C.E8.AF.81)
    *   [5.3 DNS](#DNS)
*   [6 启动 OpenVPN](#.E5.90.AF.E5.8A.A8_OpenVPN)
    *   [6.1 手动启动](#.E6.89.8B.E5.8A.A8.E5.90.AF.E5.8A.A8)
    *   [6.2 systemd 服务配置](#systemd_.E6.9C.8D.E5.8A.A1.E9.85.8D.E7.BD.AE)
    *   [6.3 让 NetworkManager 启动连接](#.E8.AE.A9_NetworkManager_.E5.90.AF.E5.8A.A8.E8.BF.9E.E6.8E.A5)
    *   [6.4 Gnome 配置](#Gnome_.E9.85.8D.E7.BD.AE)
*   [7 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [openvpn](https://www.archlinux.org/packages/?name=openvpn)。

**Note:** 该软件包同时包含服务器和客户端软件，故你应该在所有需要创建 VPN 连接的机器上安装它。

## 内核配置

OpenVPN 需要 TUN/TAP 的支持，默认内核已经进行了正确的配置。

自定义的内核需要启用 `tun` 模块，详情参阅 [Kernel modules](/index.php/Kernel_modules "Kernel modules")

 `Kernel config file` 
```
 Device Drivers
  --> Network device support
    [M] Universal TUN/TAP device driver support
```

## 准备证书和密钥数据

现在要创建所需的证书和密钥，可以在任何机器上完成，即使没有联网也可以进行。 设置证书和密钥生成脚本的默认值。编辑 `/etc/openvpn/easy-rsa/vars`，设置 KEY_COUNTRY, KEY_PROVINCE, KEY_CITY, KEY_ORG 和 KEY_EMAIL 参数(不要留空任何参数)，然后导出环境变量。

```
# source ./vars

```

清理之前的密钥：

```
# ./clean-all

```

build-ca 脚本创建了 certificate authority (CA) ca.key，密钥认证机器需要这个密钥。服务器和客户端需要 ca.crt 证书。

```
# ./build-ca

```

`build-key-server` 为服务器创建一个证书和密钥对。使用中不要输入简单的密码或公司名。

```
# ./build-key-server <server-name>

```

`build-dh` 脚本创建服务器需要的 Diffie-Hellman pem 文件。

```
# ./build-dh

```

`build-key` 脚本创建客户端证书和密钥对。可以生成任意多个以给不同的客户端使用。只要保证客户端名 <client> 是唯一的。如果要用密码认证客户端，请使用 `build-key-pass` 脚本。

```
# ./build-key <client1>
# ./build-key <client2>

```

生成的文件都保存在 `/etc/openvpn/easy-rsa/keys`。如果有错误，可以通过运行 `clean-all` 脚本，然后从头开始。注意这将删除之前生成的证书和密钥。

```
# ./clean-all

```

最后一步是将所有需要的文件通过安全通道放到正确的机器上。`ca.crt` 需要放到所有服务器和客户端。`server.crt`, `server.key` 和 `dh{n}.pem` 文件放到服务器， `client.crt` 和 `client.key` 文件放到客户端。

## 配置服务器

### 复制默认服务器配置文件

```
# cp /usr/share/openvpn/examples/server.conf /etc/openvpn/openvpn.conf

```

### 使用 PAM 和密码认证

```
port 1194
proto udp
dev tap
ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/<MYSERVER>.crt
key /etc/openvpn/easy-rsa/keys/<MYSERVER>.key
dh /etc/openvpn/easy-rsa/keys/dh1024.pem
server 192.168.56.0 255.255.255.0
ifconfig-pool-persist ipp.txt
;learn-address ./script
client-to-client
;duplicate-cn
keepalive 10 120
;tls-auth ta.key 0
comp-lzo
;max-clients 100
;user nobody
;group nobody
persist-key
persist-tun
status /var/log/openvpn-status.log
verb 3
client-cert-not-required
username-as-common-name
plugin /usr/lib/openvpn/openvpn-auth-pam.so login

```

### 使用证书认证

```
port 1194
proto tcp
dev tun0

ca /etc/openvpn/easy-rsa/keys/ca.crt
cert /etc/openvpn/easy-rsa/keys/<MYSERVER>.crt
key /etc/openvpn/easy-rsa/keys/<MYSERVER>.key
dh /etc/openvpn/easy-rsa/keys/dh1024.pem

server 10.8.0.0 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
comp-lzo
user nobody
group nobody
persist-key
persist-tun
status /var/log/openvpn-status.log
verb 3

log-append /var/log/openvpn
status /tmp/vpn.status 10

```

### 通过服务器路由

将下面内容写入服务器的 `openvpn.conf` 配置文件，"192.168.1.1" 修改为外部 DNS IP 地址。

```
push "dhcp-option DNS 192.168.1.1"
push "redirect-gateway def1"

```

使用 iptable 进行 NAT 转发：

```
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o eth0 -j MASQUERADE

```

如果运行在 OpenVZ VPS 环境，参见 [[1]](http://thecodeninja.net/linux/openvpn-archlinux-openvz-vps/):

```
iptables -t nat -A POSTROUTING -s 10.8.0.0/24 -o venet0 -j SNAT --to (venet0 ip)

```

如果一切正常，保存修改，编辑 `/etc/conf.d/iptables` 设置 IPTABLES_FORWARD=1

```
/etc/rc.d/iptables save

```

## 客户端配置

配置客户端的 .conf 文件

### 使用密码认证

```
client
dev tap
proto udp
remote <address> 1194
resolv-retry infinite
nobind
persist-tun
comp-lzo
verb 3
auth-user-pass passwd
ca ca.crt

```

被 `auth-user-pass` 引用的 `passwd` 文件必须包含如下两行:

*   第一行 - username
*   第二行 - password

### 证书验证

```
client
remote <MYSERVER> 1194
dev tun0
proto tcp
resolv-retry infinite
nobind
persist-key
persist-tun
verb 2
ca ca.crt
cert client1.crt
key client1.key
comp-lzo

```

将`ca.crt`, `client1.crt` 和 `client1.key`复制到远程计算机：

安装隧道模块:

```
 # sudo modprobe tun

```

要让 **tun** 模块自动启动，请将其加入 `/etc/rc.conf` 的 Modules 行。

### DNS

系统使用的 DNS 服务器定义在`/etc/resolv.conf`。通常此文件由控制系统网络的模块(Wicd, NetworkManager 等)维护。然而，如果希望通过远程服务器解析地址，OpenVPN 需要修改这个文件。

安装 **openresolv**软件包，它可以实现多个程序互不影响的修改 `resolv.conf`。安装后通过重启网络连接，保证 resolv.conf 是由 "resolvconf" 创建而且 DNS 解析工作正常。openresolv 不需要配置，它会自动检测和使用网络系统。

然后将如下脚本保存到`/usr/share/openvpn/update-resolv-conf`:

```
#!/bin/bash
#
# Parses DHCP options from openvpn to update resolv.conf
# To use set as 'up' and 'down' script in your openvpn *.conf:
# up /etc/openvpn/update-resolv-conf
# down /etc/openvpn/update-resolv-conf
#
# Used snippets of resolvconf script by Thomas Hood <jdthood@yahoo.co.uk>
# and Chris Hanson
# Licensed under the GNU GPL.  See /usr/share/common-licenses/GPL.
#
# 05/2006 chlauber@bnc.ch
#
# Example envs set from openvpn:
# foreign_option_1='dhcp-option DNS 193.43.27.132'
# foreign_option_2='dhcp-option DNS 193.43.27.133'
# foreign_option_3='dhcp-option DOMAIN be.bnc.ch'

[ -x /usr/sbin/resolvconf ] || exit 0

case $script_type in

up)
   for optionname in ${!foreign_option_*} ; do
      option="${!optionname}"
      echo $option
      part1=$(echo "$option" | cut -d " " -f 1)
      if [ "$part1" == "dhcp-option" ] ; then
         part2=$(echo "$option" | cut -d " " -f 2)
         part3=$(echo "$option" | cut -d " " -f 3)
         if [ "$part2" == "DNS" ] ; then
            IF_DNS_NAMESERVERS="$IF_DNS_NAMESERVERS $part3"
         fi
         if [ "$part2" == "DOMAIN" ] ; then
            IF_DNS_SEARCH="$part3"
         fi
      fi
   done
   R=""
   if [ "$IF_DNS_SEARCH" ] ; then
           R="${R}search $IF_DNS_SEARCH
"
   fi
   for NS in $IF_DNS_NAMESERVERS ; do
           R="${R}nameserver $NS
"
   done
   echo -n "$R" | /usr/sbin/resolvconf -a "${dev}.inet"
   ;;
down)
   /usr/sbin/resolvconf -d "${dev}.inet"
   ;;
esac

```

设置脚本可执行属性：

```
$ chmod +x /usr/share/openvpn/update-resolv-conf

```

然后将下面内容加入 OpenVPN 客户端的配置文件：

```
script-security 2
up /usr/share/openvpn/update-resolv-conf
down /usr/share/openvpn/update-resolv-conf

```

现在再启动 OpenVPN 连接，就能发现 `resolv.conf` 文件已经更新，关闭连接后恢复正常。

## 启动 OpenVPN

### 手动启动

如需对 VPN 连接进行调试，可以以 root 身份手动运行 `openvpn /etc/openvpn/client.conf` 以启动客户端守护程序。服务器端同样可以如此启动，只需替换为服务器端的配置文件（例，`openvpn /etc/openvpn/server.conf`）。

### systemd 服务配置

若需在系统启动时自动启动 OpenVPN，对服务器端与客户端，都可以采用在对应机器上 [启用](/index.php/Enable "Enable") `openvpn@*<configuration>*.service` 的方式配置。

例如，如果客户端配置文件是 `/etc/openvpn/client.conf`，则服务名称应为 `openvpn@client.service`。或者，如果服务器端配置文件是 `/etc/openvpn/server.conf`，则服务名称应为 `openvpn@server.service`。

### 让 NetworkManager 启动连接

在客户端，您可能并不需要一直运行 VPN 隧道，或者您仅仅想要为特定的 NetworkManager 连接建立隧道。要实现这一点，您可以向 `/etc/NetworkManager/dispatcher.d/` 添加脚本。在下列示例中，"Provider" 是 NetworkManager 连接的名称：

 `/etc/NetworkManager/dispatcher.d/10-openvpn` 
```
#!/bin/bash

case "$2" in
  up)
    if [ "$CONNECTION_ID" == "Provider" ]; then
      systemctl start openvpn@client
    fi
  ;;
  down)
    systemctl stop openvpn@client
  ;;
esac
```

请查看 [NetworkManager#Network services with NetworkManager dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") 以了解详情。

### Gnome 配置

如果您想要经由 Gnome 内置的网络配置来连接到一个 OpenVPN 服务器，请按照如下步骤进行配置： 首先，安装 `networkmanager-openvpn`。 然后，go to the Settings menu and choose Network. Click the plus sign to add a new connection and choose VPN. From there you can choose OpenVPN and manually enter the settings, or you can choose to import [#The client configuration file](#The_client_configuration_file) if you have already created one. If you followed the instructions in this article then it will be located at `/etc/openvpn/client.conf`. To connect to the VPN simply turn the connection on.

## 参见

*   [OpenVPN 官方站点](https://openvpn.net/index.php/open-source.html)
*   [Airvpn](/index.php/Airvpn "Airvpn")