**翻译状态：** 本文是英文页面 [PPTP_Server](/index.php/PPTP_Server "PPTP Server") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-10-19，点击[这里](https://wiki.archlinux.org/index.php?title=PPTP_Server&diff=0&oldid=229578)可以查看翻译后英文页面的改动。

点对点隧道协议(PPTP)是一种实现虚拟专用网(VPN)的方法。PPTP 在TCP之上使用一个控制通道和 GRE 隧道操作加密 PPP 数据包。

本条目说明如何在 Arch 中创建 PPTP 服务器。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 iptables 防火墙配置](#iptables_.E9.98.B2.E7.81.AB.E5.A2.99.E9.85.8D.E7.BD.AE)
    *   [2.2 ufw 防火墙配置](#ufw_.E9.98.B2.E7.81.AB.E5.A2.99.E9.85.8D.E7.BD.AE)
*   [3 启动](#.E5.90.AF.E5.8A.A8)

## 安装

[安装](/index.php/Pacman "Pacman")位于[官方软件仓库](/index.php/Official_repositories "Official repositories")的软件包[pptpd](https://www.archlinux.org/packages/?name=pptpd)。

## 配置

然后编辑文件`/etc/pptpd.conf`

 `/etc/pptpd.conf` 

```
option /etc/ppp/pptpd-options
localip 172.16.36.1
remoteip 172.16.36.2-254

```

接着编辑文件`/etc/ppp/pptpd-options`

 `/etc/ppp/pptpd-options` 

```
name pptpd
refuse-pap
refuse-chap
refuse-mschap
require-mschap-v2
require-mppe-128
proxyarp
lock
nobsdcomp
novj
novjccomp
nologfd
ms-dns 8.8.8.8
ms-dns 8.8.4.4

```

在 `/etc/ppp/chap-secrets`中添加用户名和密码：

 `/etc/ppp/chap-secrets` 

```
<username>     pptpd     <password>   *

```

在 `/etc/sysctl.d/99-sysctl.conf`中启用IP转发：

 `/etc/sysctl.d/99-sysctl.conf`  `net.ipv4.ip_forward=1` 

应用 sysctl.conf 修改：

```
# sysctl --system

```

### iptables 防火墙配置

配置 iptables 设置，允许 PPTP 客户端访问：

```
iptables -A INPUT -i ppp+ -j ACCEPT
iptables -A OUTPUT -o ppp+ -j ACCEPT

iptables -A INPUT -p tcp --dport 1723 -j ACCEPT
iptables -A INPUT -p 47 -j ACCEPT
iptables -A OUTPUT -p 47 -j ACCEPT

iptables -F FORWARD
iptables -A FORWARD -j ACCEPT

iptables -A POSTROUTING -t nat -o eth0 -j MASQUERADE
iptables -A POSTROUTING -t nat -o ppp+ -j MASQUERADE

```

使用下面命令保存新的 iptables 规则：

```
# rc.d save iptables

```

systemd 用户需要使用：

```
# iptables-save > /etc/iptables/iptables.rules

```

阅读 [Iptables](/index.php/Iptables "Iptables") 条目获得更多信息。

### ufw 防火墙配置

在 `/etc/default/ufw`中，修改默认的转发规则

 `/etc/default/ufw`  `DEFAULT_FORWARD_POLICY=”ACCEPT”` 

修改`/etc/ufw/before.rules`，添加如下配置到 *filter 之前

 `/etc/ufw/before.rules` 

```
# nat Table rules
*nat
:POSTROUTING ACCEPT [0:0]

# Allow traffic from clients to eth0
-A POSTROUTING -s 172.16.36.0/24 -o eth0 -j MASQUERADE

# don.t delete the .COMMIT. line or these nat table rules won.t be processed
COMMIT

```

代开端口 1723：

```
ufw allow 1723

```

重启ufw

```
ufw disable
ufw enable

```

## 启动

pptpd 软件包已经提供了 service 文件.

启动服务：

```
# systemctl start pptpd.service

```

开机自动启动：

```
# systemctl enable pptpd.service

```