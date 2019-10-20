**翻译状态：** 本文是英文页面 [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-06，点击[这里](https://wiki.archlinux.org/index.php?title=Domain+name+resolution&diff=0&oldid=348234)可以查看翻译后英文页面的改动。

DNS 解析的配置文件是 `/etc/resolv.conf`，根据[resolv.conf(5) 手册页面](http://www.kernel.org/doc/man-pages/online/pages/man5/resolv.conf.5.html):

	*"解析器(reslover)是C库中用于提供DNS接口的程序集,某个进程调用这些程序时将同时读入解析器的配置文件.这个文件具有可读性并且包含大量可用的解析参数."*

	*"在普通用途的系统里这个文件不是必须的.需要查询的只有本地主机名；主机名决定域名,域名将构成域搜索路径."*

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 DNS 解析](#DNS_解析)
*   [2 选择其它 DNS 服务器](#选择其它_DNS_服务器)
    *   [2.1 OpenNIC](#OpenNIC)
    *   [2.2 OpenDNS](#OpenDNS)
    *   [2.3 Google](#Google)
    *   [2.4 Comodo](#Comodo)
    *   [2.5 Yandex](#Yandex)
    *   [2.6 UncensoredDNS](#UncensoredDNS)
*   [3 保护 DNS 设置](#保护_DNS_设置)
    *   [3.1 修改dhcpcd配置](#修改dhcpcd配置)
    *   [3.2 使用resolv.conf.head](#使用resolv.conf.head)
    *   [3.3 给/etc/resolv.conf添加写保护](#给/etc/resolv.conf添加写保护)
    *   [3.4 使用 timeout 选项减少主机名查找时间](#使用_timeout_选项减少主机名查找时间)

## DNS 解析

网络供应商通常都会提供 [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") 服务器，如果您有自己的服务器缓存，路由器可能会增加额外的 DNS。Windows 系统中，如果一个 DNS 很慢，会自动切换到更好的服务器。在 Linux 系统中，超时时间一般比较长。使用 [dnsutils](https://www.archlinux.org/packages/?name=dnsutils) 软件包提供的 **dig** 命令可以查看域名解析的状况：

```
$ dig www5.yahoo.com

```

指定域名服务器:

```
$ dig @ip.of.name.server www5.yahoo.com

```

## 选择其它 DNS 服务器

要使用 DNS 服务器，请编辑 `/etc/resolv.conf`，把要使用的服务器放到文件的开头，修改是立即生效的。

### OpenNIC

[OpenNIC](http://www.opennicproject.org/) 提供了不受监管的域名解析服务。

**Tip:** OpenNIC 在不同的国家提供了[多个域名服务器](http://wiki.opennicproject.org/Tier2)，可以在 [最新的域名服务器](http://www.opennicproject.org/nearest-servers/) 列表中选择。

```
# OpenNIC IPv4 nameservers (US)
nameserver 107.170.95.180
nameserver 75.127.14.107

```

### OpenDNS

[OpenDNS](https://opendns.com) 提供了可选的域名解析服务器:

```
# OpenDNS IPv4 nameservers
nameserver 208.67.222.222
nameserver 208.67.220.220

```

```
# OpenDNS IPv6 nameservers
nameserver 2620:0:ccc::2
nameserver 2620:0:ccd::2

```

### Google

[Google 域名服务器](https://developers.google.com/speed/public-dns/):

```
# Google IPv4 nameservers
nameserver 8.8.8.8
nameserver 8.8.4.4

```

```
# Google IPv6 nameservers
nameserver 2001:4860:4860::8888
nameserver 2001:4860:4860::8844

```

### Comodo

[Comodo](http://securedns.dnsbycomodo.com/) 提供了IPv4 解析，付费版还可以进行网络过滤(它会劫持查询).

```
# Comodo nameservers 
nameserver 8.26.56.26 
nameserver 8.20.247.20

```

### Yandex

[Yandex.DNS](http://dns.yandex.ru/) 有三种模式：

```
# Basic Yandex.DNS - Quick and reliable DNS
nameserver 77.88.8.8
nameserver 77.88.8.1

```

```
# Safe Yandex.DNS - 屏蔽病毒和不安全网站
nameserver 77.88.8.88
nameserver 77.88.8.2

```

```
# Family Yandex.DNS - 屏蔽成人网站
nameserver 77.88.8.7
nameserver 77.88.8.3

```

### UncensoredDNS

[UncensoredDNS](http://censurfridns.dk) 是一个免费的非监控 DNS 解析服务，如果您的防火墙屏蔽了端口 53,可以在端口 5353 进行应答。

```
# censurfridns.dk IPv4 nameservers
nameserver 91.239.100.100    ## anycast.censurfridns.dk
nameserver 89.233.43.71      ## ns1.censurfridns.dk

```

```
# censurfridns.dk IPv6 nameservers
nameserver 2001:67c:28a4::             ## anycast.censurfridns.dk
nameserver 2002:d596:2a92:1:71:53::    ## ns1.censurfridns.dk

```

## 保护 DNS 设置

[dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), [NetworkManager](/index.php/NetworkManager "NetworkManager"), 以及许多别的程序能够覆盖 `/etc/resolv.conf`里的内容. 这样的行为通常是可取的, 但是有些时候DNS设置需要手动配置(比如使用静态IP时). 有几种方法可以实现. 如果你使用NetworkManager, 参见 [this thread](https://bbs.archlinux.org/viewtopic.php?id=45394) .

### 修改dhcpcd配置

可以修改dhcpcd的配置文件以避免dhcpcd进程修改`/etc/resolv.conf`. 只需要在`/etc/dhcpcd.conf`最后添加:

```
nohook resolv.conf

```

### 使用resolv.conf.head

另外, 可以创建文件`/etc/resolv.conf.head`，并在其中包含DNS信息。dhcpcd将把这个文件插入到`/etc/resolv.conf`文件头。使用OpenDNS的`/etc/resolv.conf.head`例子：

```
# OpenDNS servers
nameserver 208.67.222.222
nameserver 208.67.220.220

```

也可以使用google的DNS [Google's nameservers](https://developers.google.com/speed/public-dns/)。

```
# Google nameservers
nameserver 8.8.8.8
nameserver 8.8.4.4

```

### 给/etc/resolv.conf添加写保护

这样可以避免配置信息被任何程序修改:

```
chattr +i /etc/resolv.conf

```

### 使用 timeout 选项减少主机名查找时间

如果出现长时间域名查找问题，可以定义一个超时时间，超过之后会使用备用域名服务器。配置方法： 创建文件 `/etc/resolv.conf.tail`并加入

```
options timeout:1

```

重启network进程即可.