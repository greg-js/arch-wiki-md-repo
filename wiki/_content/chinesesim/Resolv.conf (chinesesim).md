**翻译状态：** 本文是英文页面 [Resolv.conf](/index.php/Resolv.conf "Resolv.conf") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-06，点击[这里](https://wiki.archlinux.org/index.php?title=Resolv.conf&diff=0&oldid=348234)可以查看翻译后英文页面的改动。

DNS 解析的配置文件是 `/etc/resolv.conf`，根据[resolv.conf(5) 手册页面](http://www.kernel.org/doc/man-pages/online/pages/man5/resolv.conf.5.html):

	*"解析器(reslover)是C库中用于提供DNS接口的程序集,某个进程调用这些程序时将同时读入解析器的配置文件.这个文件具有可读性并且包含大量可用的解析参数."*

	*"在普通用途的系统里这个文件不是必须的.需要查询的只有本地主机名；主机名决定域名,域名将构成域搜索路径."*

## Contents

*   [1 DNS 解析](#DNS_.E8.A7.A3.E6.9E.90)
*   [2 选择其它 DNS 服务器](#.E9.80.89.E6.8B.A9.E5.85.B6.E5.AE.83_DNS_.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [2.1 给/etc/resolv.conf添加写保护](#.E7.BB.99.2Fetc.2Fresolv.conf.E6.B7.BB.E5.8A.A0.E5.86.99.E4.BF.9D.E6.8A.A4)
    *   [2.2 使用 timeout 选项减少主机名查找时间](#.E4.BD.BF.E7.94.A8_timeout_.E9.80.89.E9.A1.B9.E5.87.8F.E5.B0.91.E4.B8.BB.E6.9C.BA.E5.90.8D.E6.9F.A5.E6.89.BE.E6.97.B6.E9.97.B4)

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

要使用 DNS 服务器，请编辑 `/etc/resolv.conf.head`例子:

```
# OpenDNS servers
nameserver 208.67.222.222
nameserver 208.67.220.220

```

也可以使用google的DNS[Google's nameservers](https://developers.google.com/speed/public-dns/).

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