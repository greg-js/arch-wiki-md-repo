**翻译状态：** 本文是英文页面 [Dnsmasq](/index.php/Dnsmasq "Dnsmasq") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-24，点击[这里](https://wiki.archlinux.org/index.php?title=Dnsmasq&diff=0&oldid=442246)可以查看翻译后英文页面的改动。

[Dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) 提供 DNS 缓存和 DHCP 服务功能。作为域名解析服务器(DNS)，dnsmasq可以通过缓存 DNS 请求来提高对访问过的网址的连接速度。作为DHCP 服务器，[dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq) 可以用于为局域网电脑分配内网ip地址和提供路由。DNS和DHCP两个功能可以同时或分别单独实现。dnsmasq轻量且易配置，适用于个人用户或少于50台主机的网络。此外它还自带了一个 [PXE](/index.php/PXE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PXE (简体中文)") 服务器。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
*   [3 DNS 缓存设置](#DNS_缓存设置)
    *   [3.1 DNS 地址文件](#DNS_地址文件)
        *   [3.1.1 resolv.conf](#resolv.conf)
            *   [3.1.1.1 三个以上域名服务器](#三个以上域名服务器)
        *   [3.1.2 使用dhcpcd](#使用dhcpcd)
        *   [3.1.3 使用dhclient](#使用dhclient)
    *   [3.2 使用NetworkManager](#使用NetworkManager)
        *   [3.2.1 IPv6](#IPv6)
        *   [3.2.2 其他方式](#其他方式)
*   [4 DHCP 服务器设置](#DHCP_服务器设置)
*   [5 启动守护进程](#启动守护进程)
*   [6 测试](#测试)
    *   [6.1 DNS 缓存](#DNS_缓存)
    *   [6.2 DHCP 服务器](#DHCP_服务器)
*   [7 小技巧](#小技巧)
    *   [7.1 阻止 OpenDNS 重定向 Google 请求](#阻止_OpenDNS_重定向_Google_请求)
    *   [7.2 查看租约](#查看租约)
    *   [7.3 添加自定义域](#添加自定义域)
    *   [7.4 Override addresses](#Override_addresses)
    *   [7.5 多个 Dnsmasq](#多个_Dnsmasq)
        *   [7.5.1 静态](#静态)
        *   [7.5.2 动态](#动态)

## 安装

从[官方仓库](/index.php/%E5%AE%98%E6%96%B9%E4%BB%93%E5%BA%93 "官方仓库")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [dnsmasq](https://www.archlinux.org/packages/?name=dnsmasq)。

## 配置

编辑 dnsmasq 的配置文件 `/etc/dnsmasq.conf` 。这个文件包含大量的选项注释。

**警告:** dnsmasq 默认启用其 DNS 服务器。如果不需要，必须明确地将其 DNS 端口设置为 `0` 禁用它： `/etc/dnsmasq.conf`  `port=0` 

**提示：** 查看配置文件语法是否正确，可执行下列命令：
```
$ dnsmasq --test

```

## DNS 缓存设置

要在单台电脑上以守护进程方式启动dnsmasq做DNS缓存服务器，编辑`/etc/dnsmasq.conf`，添加监听地址：

```
listen-address=127.0.0.1

```

如果用此主机为局域网提供默认 DNS，请用为该主机绑定固定 IP 地址，设置：

```
listen-address=192.168.x.x

```

这种情况建议配置静态IP

多个ip地址设置:

```
listen-address=127.0.0.1,192.168.x.x 

```

### DNS 地址文件

在配置好dnsmasq后，你需要编辑`/etc/resolv.conf`让DHCP客户端首先将本地地址(localhost)加入 DNS 文件(`/etc/resolv.conf`)，然后再通过其他DNS服务器解析地址。配置好DHCP客户端后需要重新启动网络来使设置生效。

#### resolv.conf

一种选择是一个纯粹的 `resolv.conf` 配置。要做到这一点，才使第一个域名服务器在`/etc/resolv.conf` 中指向localhost：

 `/etc/resolv.conf` 
```
nameserver 127.0.0.1
# External nameservers
...

```

现在，DNS查询将首先解析dnsmasq，只检查外部的服务器如果DNSMasq无法解析查询. [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), 不幸的是，往往默认覆盖 `/etc/resolv.conf`, 所以如果你使用DHCP，这里有一个好主意来保护 `/etc/resolv.conf`,要做到这一点，追加 `nohook resolv.conf`到dhcpcd的配置文件：

 `/etc/dhcpcd.conf` 
```
...
nohook resolv.conf
```

也可以保护您的resolv.conf不被修改：

```
# chattr +i /etc/resolv.conf

```

##### 三个以上域名服务器

Linux 处理 DNS 请求时有个限制，在 `resolv.conf` 中最多只能配置三个域名服务器（nameserver）。作为一种变通方法,可以在 `resolv.conf` 文件中只保留 localhost 作为域名服务器，然后为外部域名服务器另外创建 `resolv-file` 文件。首先，为 dnsmasq 新建一个域名解析文件：

 `/etc/resolv.dnsmasq.conf` 
```
# Google's nameservers, for example
nameserver 8.8.8.8
nameserver 8.8.4.4

```

然后编辑 `/etc/dnsmasq.conf` 让 dnsmasq 使用新创建的域名解析文件：

 `/etc/dnsmasq.conf` 
```
...
resolv-file=/etc/resolv.dnsmasq.conf
...

```

#### 使用dhcpcd

[dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) 可以是通过创建（或编辑）`/etc/resolv.conf.head`文件或 `/etc/resolv.conf.tail`文件来指定dns服务器，使`/etc/resolv.conf`不会被每次都被dhcpcd重写

```
echo "nameserver 127.0.0.1" > /etc/resolv.conf.head #设置dns服务器为127.0.0.1

```

#### 使用dhclient

要使用 dhclient， 取消 `/etc/dhclient.conf` 文件中如下行的注释：

```
prepend domain-name-servers 127.0.0.1;

```

### 使用NetworkManager

[NetworkManager](/index.php/NetworkManager "NetworkManager") 可以靠自身配置文件的设置项启动 *dnsmasq* 。在 `NetworkManager.conf` 文件的 `[main]` 节段添加 `dns=dnsmasq` 配置语句，然后禁用由 [systemd](/index.php/Systemd "Systemd") 启动的 `dnsmasq.service`:

 `/etc/NetworkManager/NetworkManager.conf` 
```
[main]
plugins=keyfile
dns=dnsmasq

```

可以在 `/etc/NetworkManager/dnsmasq.d/` 目录下为 *dnsmasq* 创建自定义配置文件。例如，调整 DNS 缓存大小（保存在内存中）：

 `/etc/NetworkManager/dnsmasq.d/cache`  `cache-size=1000` 

*dnsmasq* 被 `NetworkManager` 启动后，此目录下配置文件中的配置将取代默认配置。

**提示：** 这种方法可以让你启用特定域名的自定义DNS设置。例如: `server=/example1.com/exemple2.com/xx.xxx.xxx.x` 改变第一个DNS地址，浏览以下网站`example1.com, example2.com`使用`xx.xxx.xxx.xx`。This method is preferred to a global DNS configuration when using particular DNS nameservers which lack of speed, stability, privacy and security.

#### IPv6

启用 `dnsmasq` 在 NetworkManager 可能会中断仅持IPv6的DNS查询 (例如 `dig -6 [hostname]`) 否则将工作。 为了解决这个问题，创建以下文件将配置 *dnsmasq* 总是监听IPv6的loopback：

 `/etc/NetworkManager/dnsmasq.d/ipv6_listen.conf`  `listen-address=::1` 

此外， `dnsmasq`不优先考虑上游IPv6的DNS。不幸的是NetworkManager已不这样做 ([Ubuntu Bug](https://bugs.launchpad.net/ubuntu/+source/network-manager/+bug/936712))。 一种解决方法是将禁用IPv4 DNS的NetworkManager的配置，假设存在。

#### 其他方式

另一种选择是在NetworkManagers“设置（通常通过右键单击小程序）和手动输入设置。设置将取决于前端中使用的类型;这个过程通常涉及右击小程序，编辑（或创建）一个配置文件，然后选择DHCP类型为“自动（指定地址）。”DNS地址将需要输入，通常以这种形式：`127.0.0.1, DNS-server-one, ...`.

## DHCP 服务器设置

dnsmasq默认关闭DHCP功能，如果该主机需要为局域网中的其他设备提供IP和路由，应该对dnsmasq 配置文件(`/etc/dnsmasq.conf`)必要的配置如下：

```
# Only listen to routers' LAN NIC.  Doing so opens up tcp/udp port 53 to
# localhost and udp port 67 to world:
interface=<LAN-NIC>

# dnsmasq will open tcp/udp port 53 and udp port 67 to world to help with
# dynamic interfaces (assigning dynamic ips). Dnsmasq will discard world
# requests to them, but the paranoid might like to close them and let the 
# kernel handle them:
bind-interfaces

# Dynamic range of IPs to make available to LAN pc
dhcp-range=192.168.111.50,192.168.111.100,12h

# If you’d like to have dnsmasq assign static IPs, bind the LAN computer's
# NIC MAC address:
dhcp-host=aa:bb:cc:dd:ee:ff,192.168.111.50

```

## 启动守护进程

设置为开机启动：

```
# systemctl enable dnsmasq.service

```

立即启动 dnsmasq：

```
# systemctl start dnsmasq.service

```

查看dnsmasq是否启动正常，查看系统日志：

```
# journalctl -u dnsmasq.service

```

需要重启网络服务以使 DHCP 客户端重建一个新的 `/etc/resolv.conf`。

## 测试

### DNS 缓存

要测试查询速度，请访问一个 dnsmasq 启动后没有访问过的网站，执行 (`dig` (位于 [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) 软件包):

```
$ dig archlinux.org | grep "Query time"

```

再次运行命令，因为使用了缓存，查询时间应该大大缩短。

### DHCP 服务器

从一个连接到使用了 dnsmasq 的计算机的计算机，配置它使用 DHCP 自动获取 IP 地址，然后尝试连接到你平时使用的网络。

## 小技巧

### 阻止 OpenDNS 重定向 Google 请求

要避免 OpenDNS 重定向所有 Google 请求到他们自己的搜索服务器，添加以下内容到 `/etc/dnsmasq.conf`：

```
server=/www.google.com/<ISP DNS IP>

```

用你的互联网服务供应商（ISP）的 DNS 服务器/路由器的 IP 替换 <ISP DNS IP> 。

**Note:** 因为众所周知的原因，ISP的DNS服务器可能会污染或劫持Google的DNS [[1]](https://github.com/lifetyper/FreeRouter/wiki/3-DNS%E6%B1%A1%E6%9F%93%E4%B8%8E%E5%BA%94%E5%AF%B9)，请自行搜索解决办法。

### 查看租约

```
cat /var/lib/misc/dnsmasq.leases

```

### 添加自定义域

它可以将一个自定义域添加到主机中的（本地）网络：

```
local=/home.lan/
domain=home.lan

```

在这个例子中可以ping主机/设备 (例如:您的主机文件中的定义) `hostname.home.lan`.

取消扩展主机添加自定义域的主机条目：存在

```
expand-hosts

```

如果没有这个设置，你必须将域添加到 `/etc/hosts` 中。

### Override addresses

In some cases, such as when operating a captive portal, it can be useful to resolve specific domains names to a hard-coded set of addresses. This is done with the `address` config:

```
address=/example.com/1.2.3.4

```

Furthermore, it's possible to return a specific address for all domain names that are not answered from `/etc/hosts` or DHCP by using a special wildcard:

```
address=/#/1.2.3.4

```

### 多个 Dnsmasq

#### 静态

要让每个 interface 有独立的 dnsmasq，用 `interface` 和 `bind-interface` 选项来实现。

#### 动态

像下面这样可以指定排除某个 interface，而其他的 interface 将会拥有各自的 dnsmasq。

```
except-interface=lo
bind-dynamic

```

**Note:** [libvirt](/index.php/Libvirt "Libvirt") 默认就是这样做的。