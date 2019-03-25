Related articles

*   [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution")

[Unbound](https://unbound.net/) 是一个具有验证，递归和缓存等功能的 DNS 解析器。根据[Wikipedia](https://en.wikipedia.org/wiki/Unbound_(DNS_Server) "wikipedia:Unbound (DNS Server)")：

	Unbound has supplanted the Berkeley Internet Name Domain ([BIND](/index.php/BIND "BIND")) as the default, base-system name server in several open source projects, where it is perceived as smaller, more modern, and more secure for most applications.

**翻译状态：** 本文是英文页面 [Unbound](/index.php/Unbound "Unbound") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-24，点击[这里](https://wiki.archlinux.org/index.php?title=Unbound&diff=0&oldid=397940)可以查看翻译后英文页面的改动。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 配置](#配置)
    *   [2.1 本地DNS服务器](#本地DNS服务器)
    *   [2.2 访问控制](#访问控制)
    *   [2.3 使用DNS over TLS进行转发](#使用DNS_over_TLS进行转发)
    *   [2.4 根域名服务器](#根域名服务器)
    *   [2.5 DNSSEC验证](#DNSSEC验证)
        *   [2.5.1 测试DNSSEC](#测试DNSSEC)
    *   [2.6 转发查询](#转发查询)
        *   [2.6.1 允许本地网络使用DNS](#允许本地网络使用DNS)
            *   [2.6.1.1 使用openresolv](#使用openresolv)
            *   [2.6.1.2 手动制定DNS服务器](#手动制定DNS服务器)
                *   [2.6.1.2.1 包含本地DNS服务器](#包含本地DNS服务器)
        *   [2.6.2 转发所有其余的请求](#转发所有其余的请求)
            *   [2.6.2.1 使用openresolv](#使用openresolv_2)
            *   [2.6.2.2 手动指定DNS服务器](#手动指定DNS服务器)
*   [3 使用](#使用)
    *   [3.1 启动unbound](#启动unbound)
    *   [3.2 远程控制unbound](#远程控制unbound)
        *   [3.2.1 配置unbound-control](#配置unbound-control)
        *   [3.2.2 使用unbound-control](#使用unbound-control)
*   [4 提示与技巧](#提示与技巧)
    *   [4.1 域名黑名单](#域名黑名单)
    *   [4.2 添加一个authoritative DNS服务器](#添加一个authoritative_DNS服务器)
    *   [4.3 WAN facing DNS](#WAN_facing_DNS)
    *   [4.4 根域名服务器与systemd timer](#根域名服务器与systemd_timer)
*   [5 疑难解答](#疑难解答)
    *   [5.1 有关num-threads的问题](#有关num-threads的问题)
*   [6 参阅](#参阅)

## 安装

安装 [unbound](https://www.archlinux.org/packages/?name=unbound) 软件包。 此外, [expat](https://www.archlinux.org/packages/?name=expat) 是使用[DNSSEC](/index.php/DNSSEC "DNSSEC")验证请求所必须的。

## 配置

默认配置已经位于`/etc/unbound/unbound.conf`文件中。此外，`/etc/unbound/unbound.conf.example`文件包含了其他的可配置设置项，并以注释的形式给出了示范设置。以下章节重点解释和默认配置文件不同的设置项。如需了解更多细节，参见[unbound.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unbound.conf.5)。

除非特别声明，这一节列出的选项都是放置在配置文件的`server`节中，类似这样：

 `/etc/unbound/unbound.conf` 
```
server:
  ...
  *setting*: *value*
  ...

```

**Note:** 请确保你的配置文件中已经设置了`do-daemonize: no`,否则`unbound.service`会无法启动.

### 本地DNS服务器

如果你想要使用*unbound*作为本地DNS服务器，请把[resolv.conf](/index.php/Resolv.conf "Resolv.conf")中的域名服务器（nameserver）设置到回环地址`::1`和`127.0.0.1`。你可能想要让你的配置[Domain name resolution (简体中文)#给/etc/resolv.conf添加写保护](/index.php/Domain_name_resolution_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#给/etc/resolv.conf添加写保护 "Domain name resolution (简体中文)")。

**Tip:** 实现这个目的的一个简便方法是安装[openresolv](/index.php/Openresolv "Openresolv")，然后取消文件`/etc/resolvconf.conf`中包含`name_servers="::1 127.0.0.1"`的那一行的注释。然后运行`resolvconf -u`来重新生成`/etc/resolv.conf`。

要了解如何测试设置项，参见[Domain name resolution#Lookup utilities](/index.php/Domain_name_resolution#Lookup_utilities "Domain name resolution")。

在把[resolv.conf](/index.php/Resolv.conf "Resolv.conf")中的设置更改为持久化设置后，请特别注意检查正在使用的服务器是`::1`或`127.0.0.1`。

你还需要对“unbound”进行设置，以使它[#转发查询](#转发查询)到你所选择的DNS服务器。

### 访问控制

你可以通过IP地址来指定响应请求的端口。默认监听的是*localhost*。

为了在所有端口上监听，使用以下配置：

```
interface: 0.0.0.0

```

为了通过IP地址来控制可以访问服务器的系统，使用`access-control`选项：

```
access-control: *subnet* *action*

```

例如:

```
access-control: 192.168.1.0/24 allow

```

*action*可以是`deny` (drop message), `refuse` (polite error reply), `allow` (recursive ok), or `allow_snoop` (recursive and nonrecursive ok)中的任意一个。默认除了localhost之外的所有东西都会被拒绝。

### 使用DNS over TLS进行转发

为了使用这个功能，你需要设置`tls-cert-bundle`选项来指定本地系统的根证书认证包，以使得unbound可以转发TLS请求并指定允许DNS over TLS的服务器数量。

对每个服务器你都需要用 @ 来指定连接的端口，同时你也要用 # 来指明它的域名是什么。虽然它看起来像注释，the hashtag name allows for the TLS authentication name to be set for stub-zones and with `unbound-control forward control` command。在 @ 和 # 之间不应该有空格。

 `/etc/unbound/unbound.conf` 
```
...
server:
...
	tls-cert-bundle: /etc/ssl/certs/ca-certificates.crt
...
forward-zone:
        name: "."
        forward-tls-upstream: yes
        forward-addr: 1.1.1.1@853#cloudflare-dns.com

```

### 根域名服务器

为了查询一个没有被缓存成地址的主机，解释器需要从服务器树的根开始、对根服务器进行请求来知道去哪里找到目标地址的顶级域名。Unbound内置了一些根节点，但是推荐你提供一个根节点文件给它以免内置的过于老旧。

首先，告诉*unbound*使用`root.hints`文件：

```
root-hints: root.hints

```

然后把你的*root hints*文件放进*unbound*的配置文件夹。实现这个目标最简单的方法是运行下面的命令：

 `# curl -o /etc/unbound/root.hints https://www.internic.net/domain/named.cache` 

建议每六个月更新一次`root.hints`来保持根服务器列表是最新的。你可以手动完成这个任务，也可以使用[Systemd/Timers](/index.php/Systemd/Timers "Systemd/Timers")。详情参见[#根域名服务器与systemd timer](#根域名服务器与systemd_timer)。

### DNSSEC验证

为了使用[DNSSEC](/index.php/DNSSEC "DNSSEC")验证，你需要在`server:`节中添加以下设置来告诉*unbound*服务器根证书文件的位置：

 `/etc/unbound/unbound.conf`  `trust-anchor-file: trusted-key.key` 

`/etc/unbound/trusted-key.key`是从依赖项[dnssec-anchors](https://www.archlinux.org/packages/?name=dnssec-anchors)所提供的的`/etc/trusted-key.key`复制而来的，它的[PKGBUILD](/index.php/PKGBUILD "PKGBUILD")按照[unbound-anchor(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unbound-anchor.8)生成了`/etc/trusted-key.key`。

如果总的[#转发查询](#转发查询)设置到了不支持DNSSEC的DNS服务器，那么请确保已经把这些DNS服务器注释掉，否则DNS请求会失败。DNSSEC验证只会在被请求的DNS服务器支持它的时候成功完成。

**Note:** 如果使用DNSSEC，在地址被缓存之前DNS查询时间将会显著增加。

#### 测试DNSSEC

为了测试DNSSEC是否工作，在[starting](/index.php/Starting "Starting") `unbound.service`之后：

```
$ unbound-host -C /etc/unbound/unbound.conf -v sigok.verteiltesysteme.net

```

得到的回应应该是附带`(secure)`字样的ip地址。

```
$ unbound-host -C /etc/unbound/unbound.conf -v sigfail.verteiltesysteme.net

```

这次的回应应该包含`(BOGUS (security failure))`字样。

另外你也可以使用“drill”来测试：

```
$ drill sigok.verteiltesysteme.net
$ drill sigfail.verteiltesysteme.net

```

第一个命令应该返回`NOERROR`的`rcode`；而第二个命令应该返回`SERVFAIL`的`rcode`。

### 转发查询

如果你只想转发请求到外部的DNS服务器，请跳到[#转发所有其余的请求](#转发所有其余的请求)。

#### 允许本地网络使用DNS

##### 使用openresolv

如果你的网络管理器支持[openresolv](/index.php/Openresolv "Openresolv")，你可以通过设置来使它提供本地DNS服务器、使用unbound来查询域名。 [[2]](https://roy.marples.name/projects/openresolv/config)

 `/etc/resolvconf.conf` 
```
...
private_interfaces="*"

# Write out unbound configuration file
unbound_conf=/etc/unbound/resolvconf.conf
```

运行`resolvconf -u`来生成文件。

配置unbound读取openresolv生成的文件并允许回应[private IP address ranges](https://en.wikipedia.org/wiki/Private_network "wikipedia:Private network")：

 `/etc/unbound/unbound.conf` 
```
include: "/etc/unbound/resolvconf.conf"
...
server:
...
   private-domain: "intranet"
   private-domain: "internal"
   private-domain: "private"
   private-domain: "corp"
   private-domain: "home"
   private-domain: "lan"

   unblock-lan-zones: yes
   insecure-lan-zones: yes
   ...

```

另外你可能想要对私有DNS域名空间禁用DNSSEC[[3]](https://tools.ietf.org/html/rfc6762#appendix-G)：

 `/etc/unbound/unbound.conf` 
```

...
server:
...
   domain-insecure: "intranet"
   domain-insecure: "internal"
   domain-insecure: "private"
   domain-insecure: "corp"
   domain-insecure: "home"
   domain-insecure: "lan"
...

```

##### 手动制定DNS服务器

如果你有一个需要DNS请求的本地网络，同时你想要把请求都转发给一个本地的DNS服务器，那么你需要添加这一行：

```
private-address: *本地子网/子网掩码*

```

例如:

```
private-address: 10.0.0.0/24

```

**Note:** 你可以使用私有地址来防止DNS劫持攻击。为了达到这个目的，你可能需要允许RFC1918网络(10.0.0.0/8 172.16.0.0/12 192.168.0.0/16 169.254.0.0/16 fd00::/8 fe80::/10)。 Unbound的未来版本可能会默认启用这个功能。

###### 包含本地DNS服务器

为了包含一个本地DNS服务器，以用于转发和反代本地地址，类似下面的一组配置是必要的（请把下面的10.0.0.1替换为本地网络中提供DNS服务的服务器的地址）：

```
local-zone: "10.in-addr.arpa." transparent

```

上面这一行对于让反向查询正常工作是非常重要的。

```
forward-zone:
name: "mynetwork.com."
forward-addr: 10.0.0.1
forward-zone:
local-data: "1.0.0.127.in-addr.arpa. 10800 IN PTR localhost."

```

**Note:** 转发空间和根空间之间的区别是，根空间只有在直接连接到一个authoritative DNS服务器的时候才能正常工作。如果一个[BIND](/index.php/BIND "BIND")DNS服务器提供authoritative DNS，那么这个特性对于来自于它的请求有用——但是如果你在把请求指向一个*unbound*服务器（内部查询都被转发到另一个DNS服务器），那么把这个指向定义为该机器上的根空间是不会起作用的。在这种情况下，你必须把它定义为上面所说的转发空间，因为转发空间可以通过链式查询去到别的DNS服务器上，亦即转发空间可以把请求指向递归DNS服务器。这个区别是很重要的，因为如果你不恰当地使用根空间，你不会得到能够说明问题的错误信息。

你可以通过下面的配置来设定localhost的前向和反向查询：

```
local-zone: "localhost." static
local-data: "localhost. 10800 IN NS localhost."
local-data: "localhost. 10800 IN SOA localhost. nobody.invalid. 1 3600 1200 604800 10800"
local-data: "localhost. 10800 IN A 127.0.0.1"
local-zone: "127.in-addr.arpa." static
local-data: "127.in-addr.arpa. 10800 IN NS localhost."
local-data: "127.in-addr.arpa. 10800 IN SOA localhost. nobody.invalid. 2 3600 1200 604800 10800"
local-data: "1.0.0.127.in-addr.arpa. 10800 IN PTR localhost."

```

#### 转发所有其余的请求

##### 使用openresolv

如果你的网络管理器支持[openresolv](/index.php/Openresolv "Openresolv")，你可以通过配置使它提供上游DNS服务器给unbound。 [[4]](https://roy.marples.name/projects/openresolv/config)

 `/etc/resolvconf.conf` 
```
...
# Write out unbound configuration file
unbound_conf=/etc/unbound/resolvconf.conf
```

运行`resolvconf -u`来生成文件。

最后配置unound读取openresolv生成的文件：

```
include: "/etc/unbound/resolvconf.conf"

```

##### 手动指定DNS服务器

为了使本地机器之外的、本地网络外部的默认转发区域使用指定的服务器，请在配置文件中添加一个名字是`.`的转发区域。在这个例子里，所有的请求都被转发到谷歌的DNS服务器：

```
 forward-zone:
 forward-addr: 8.8.8.8
 forward-addr: 8.8.4.4

```

## 使用

### 启动unbound

[Start/enable](/index.php/Start/enable "Start/enable") `unbound.service` systemd服务。

### 远程控制unbound

*unbound*安装的时候自带了`unbound-control`工具，利用这个工具我们可以远程控制unbound服务器。它和[pdnsd](https://www.archlinux.org/packages/?name=pdnsd)的[pdnsd-ctl](/index.php/Pdnsd#pdnsd-ctl "Pdnsd")命令很类似。

#### 配置unbound-control

在能够使用它之前你需要做下面的事情：

1) 首先，运行：

```
# unbound-control-setup

```

来为你的服务器和客户端生成一个self-signed的证书和private key。生成的文件位于`/etc/unbound`文件夹。

2) 然后，把下面的内容放进`/etc/unbound/unbound.conf`文件。`control-enable: yes`是一定要有的，其余的内容可以按照所需进行调整。

```
remote-control:
   # Enable remote control with unbound-control(8) here.
   # 用unbound-control-setup生成的keys and certificates进行配置。
   control-enable: yes
   # 设定监听哪个地址.
   # give 0.0.0.0 and ::0 to listen to all interfaces.
   control-interface: 127.0.0.1
   # 远程控制用的端口.
   control-port: 8953
   # unbound server key file.
   server-key-file: "/etc/unbound/unbound_server.key"
   # unbound server certificate file.
   server-cert-file: "/etc/unbound/unbound_server.pem"
   # unbound-control key file.
   control-key-file: "/etc/unbound/unbound_control.key"
   # unbound-control certificate file.
   control-cert-file: "/etc/unbound/unbound_control.pem"

```

#### 使用unbound-control

下面是*unbound-control*可以使用的一部分命令：

*   不重置数据的情况下查看统计数据

```
 # unbound-control stats_noreset

```

*   把cache dump到stdout

```
 # unbound-control dump_cache

```

*   清空cache并且重新加载配置

```
 # unbound-control reload

```

请参考[unbound-control(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/unbound-control.8)来了解*unbound-control*支持的操作。

## 提示与技巧

### 域名黑名单

你可以打开这个网页[adservers](https://pgl.yoyo.org/adservers/serverlist.php?hostformat=unbound&showintro=0&startdate%5Bday%5D=&startdate%5Bmonth%5D=&startdate%5Byear%5D=&mimetype=plaintext)，把它的内容保存到`/etc/unbound/adservers`，然后把下面的配置直接添加到unbound配置文件里就可以了：

 `/etc/unbound/unbound.conf` 
```
server:
...
  include: /etc/unbound/adservers

```

**Tip:**

*   为了在查询这些hosts的时候返回OK状态指示，你可以更改默认的127.0.0.1重定向，改成重定向到你所控制的服务器并让那台服务器返回空的204回应，参考[[5]](http://www.shadowandy.net/2014/04/adblocking-nginx-serving-1-pixel-gif-204-content.htm)
*   如果需要把其他格式的hosts文件转换成unbound的格式的，请运行这个命令: `$ grep '^0\.0\.0\.0' *hostsfile* | awk '{print "local-zone: \""$2"\" always_nxdomain"}' > /etc/unbound/adservers` 

### 添加一个authoritative DNS服务器

对于想要在一台机器上同时两个DNS服务器（一个是提供验证、递归、缓存功能的DNS服务器，另一个是authoritative DNS服务器）的用户来说，参考[NSD](/index.php/NSD "NSD")的维基页面可能会有所帮助。那个页面提供了一个示范配置。一个服务器专门响应authoritative DNS请求，另一个服务器提供验证、递归、缓存等DNS功能，这样会比一个服务器提供所有功能会更安全。很多用户已经在使用Bind作为DNS服务器，而针对从Bind变成Bind和NSD协同工作的过程的帮助在[NSD](/index.php/NSD "NSD")页面有提供。

### WAN facing DNS

通过更改配置文件和服务器所监听的接口（地址）来允许来自本地网络之外的机器的DNS请求进入本地网络（LAN）内的某台特定机器，这个想法是可行的。这个功能对于公开的网站服务器和邮件服务器是非常有用的。这个在bind上已经实现了多年的技术，通过正确配置防火墙机器上的端口转发——转发这些请求到正确的机器上——也可以在unbound上实现。

### 根域名服务器与systemd timer

下面是一个systemd服务和timer的示例文件，它用来每隔一个月更新一次`root.hints`，所用的方法与[#根域名服务器](#根域名服务器)中的相同：

 `/etc/systemd/system/roothints.service` 
```
[Unit]
Description=Update root hints for unbound
After=network.target

[Service]
ExecStart=/usr/bin/curl -o /etc/unbound/root.hints https://www.internic.net/domain/named.cache
```
 `/etc/systemd/system/roothints.timer` 
```
[Unit]
Description=Run root.hints monthly

[Timer]
OnCalendar=monthly
Persistent=true

[Install]
WantedBy=timers.target
```

最后[Start/enable](/index.php/Start/enable "Start/enable") `roothints.timer` systemd timer就可以了。

## 疑难解答

### 有关num-threads的问题

`unbound.conf`的man page提到：

```
     outgoing-range: <number>
           Number of ports to open. This number of file  descriptors  can  be  opened  per thread.

```

网上的一些人建议`num-threads`这个参数应该设置成你的CPU的核心数量。示范配置文件`unbound.conf.example`里关于这个选项只有下面这两行：

```
       # number of threads to create. 1 disables threading.
       # num-threads: 1

```

但是人为地把`num-threads`提高到比`1`就一定会造成*unbound*在启动的时候在log里写一个warning提示说exceeding the number of file descriptors。实际上对于大多数在小型网络或是单机上运行unbound的用户来说，通过让`num-threads`超过`1`来得到性能提升是徒劳的。如果你一定要这么做，那么请参考[official documentation](http://www.unbound.net/documentation/howto_optimise.html)。下面这条经验法则应该对你有所帮助：

	*Set `num-threads` equal to the number of CPU cores on the system. E.g. for 4 CPUs with 2 cores each, use 8.*

把`outgoing-range`设置得尽可能大，参考上面的链接来突破总数是`1024`这个限制。这样就会使得unbound可以同时为更多客户端提供服务。1个核心设置`950`，2个核心设置`450`，四个核心设置`200`。`num-queries-per-thread`最好设置成`outgoing-range`的一半。

因为`outgoing-range`是有限制的，同时`num-queries-per-thread`也因此受到了限制，所以最好在编译的时候带上[libevent](https://www.archlinux.org/packages/?name=libevent)，这样就不会有`1024`限制了。如果你有一个高负荷DNS服务器使得你不得不这样编译，你需要从源码编译unbound而不是直接安装[unbound](https://www.archlinux.org/packages/?name=unbound)。

## 参阅

*   [Fedora change to Unbound](https://fedoraproject.org/wiki/Changes/Default_Local_DNS_Resolver)
*   [Block hosts that contain advertisements](https://github.com/jodrell/unbound-block-hosts/)