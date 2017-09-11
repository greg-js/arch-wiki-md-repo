相关文章

*   [Privoxy](/index.php/Privoxy "Privoxy")
*   [Polipo](/index.php/Polipo "Polipo")

[Tor](https://www.torproject.org/download/download.html.en) 是一个开源实现，第二代洋葱路由匿名代理网络，提供免费访问。其首要目标是通过对流量分析攻击保护，使网上的匿名性。

## Contents

*   [1 介绍](#.E4.BB.8B.E7.BB.8D)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
*   [4 用法](#.E7.94.A8.E6.B3.95)
*   [5 网页浏览](#.E7.BD.91.E9.A1.B5.E6.B5.8F.E8.A7.88)
    *   [5.1 Firefox](#Firefox)
    *   [5.2 Chromium](#Chromium)
*   [6 即时通信](#.E5.8D.B3.E6.97.B6.E9.80.9A.E4.BF.A1)
    *   [6.1 Pidgin](#Pidgin)
*   [7 Irssi](#Irssi)
    *   [7.1 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)
*   [8 使用 HTTP 代理](#.E4.BD.BF.E7.94.A8_HTTP_.E4.BB.A3.E7.90.86)
    *   [8.1 Polipo](#Polipo)
    *   [8.2 Privoxy](#Privoxy)
        *   [8.2.1 在Firefox使用Tor 和 Privoxy](#.E5.9C.A8Firefox.E4.BD.BF.E7.94.A8Tor_.E5.92.8C_Privoxy)
        *   [8.2.2 在其他程序使用Tor 和Privoxy](#.E5.9C.A8.E5.85.B6.E4.BB.96.E7.A8.8B.E5.BA.8F.E4.BD.BF.E7.94.A8Tor_.E5.92.8CPrivoxy)
*   [9 运行Tor 服务](#.E8.BF.90.E8.A1.8CTor_.E6.9C.8D.E5.8A.A1)
    *   [9.1 配置](#.E9.85.8D.E7.BD.AE_2)
*   [10 运行 Tor 桥](#.E8.BF.90.E8.A1.8C_Tor_.E6.A1.A5)
*   [11 TorDNS](#TorDNS)
*   [12 Torify](#Torify)
*   [13 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [13.1 User value的问题](#User_value.E7.9A.84.E9.97.AE.E9.A2.98)
*   [14 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5_2)

## 介绍

使用Tor网络在他们的机器上运行洋葱代理。这个软件向外连接到Tor，定期的通过Tor网络连接一个虚拟的电子回路。Tor在一个分层方式采用加密(因此有了‘洋葱’的比喻),确保路由器之间的完全保密。 同时， 洋葱代理服务器软件，向客户端提出了SOCKS接口。SOCKS监听程序是Tor的特点，通过Tor的虚拟电路的流量，然后复。

**警告:** 仅仅使用Tor不能保证匿名。这里可以看出几个主要的误导 (see: [[1]](https://www.torproject.org/download/download.html.en#什么是Tor真正的工作))。

通过这个过程洋葱代理将会管理终端用户的匿名网络流量。它通过加密流量来保持用户的匿名， 通过Tor的其他节点来发送信息，在发送信息到你指定的服务器之前解密。虽然Tor相对的来说比一般的使用DNS目录连接安全(例如：没有使用代理), 由于大量的数据加密所以它相对来说比较慢。 此外，尽Tor阻止了流量分析但是Tor不能阻Tor网络边界流量的确认。(例如：例如流量进入或者退出网络)。

[Wikipedia:Tor (anonymity network)](https://en.wikipedia.org/wiki/Tor_(anonymity_network) "wikipedia:Tor (anonymity network)")

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的软件包 [tor](https://www.archlinux.org/packages/?name=tor)。

此外，还可以安装 [Qt](/index.php/Qt "Qt") 前端 [vidalia](https://aur.archlinux.org/packages/vidalia/)。除了控制 Tor 进程外，Vidalia 可以查看 Tor 的配置和状态、监控带宽使用并查看、过滤和搜索日志信息。

## 配置

为了跟好的理解Tor`/etc/tor/torrc`配置文件. 配置选项在 man tor[tor(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/tor.1)和[Tor website](https://www.torproject.org/docs/tor-manual.html.en)有介绍.

默认配置应该能够很好的为大多数Tor用户服务除了哪些是用Vidalia的用户, Vidalia是一Tor的图形界面。 在[AUR](/index.php/AUR "AUR")有可用包[Vidalia package](https://aur.archlinux.org/packages.php?ID=9731)。除了控制过程中的Vidalia允许您查看Tor状态监视带宽使用情况，查看，过滤，搜索日志消息;和配置Tor的某些方面。

使用`TOR_MAX_FD`变量，您可以设置自定义文件为Tor的描述ulimits`/etc/conf.d/tor`。

默认情况下的Tor记录在日志级别的通知“STDOUT”。如果你能够记录在自己的文件`torrc`, 他们默认为 `/usr/local/var/log/tor/`.

## 用法

可以通过命令行或 **vidalia** 等图形程序启动 Tor.

要永久连接，可以启动 **tor** [daemon](/index.php/Daemon "Daemon") 并将其加入 `DAEMONS` 数组。

程序配置成实验 127.0.0.1 或 localhost 作为 SOCKS5 代理就可以使用 Tor，端口要设置成 9050 (Tor 标准设置) 或 9051 (用 **vidalia**标准配置).

访问 [Tor](https://check.torproject.org/)、[Harvard](http://serifos.eecs.harvard.edu/cgi-bin/ipaddr.pl?tor=1) 或 [Xenobite.eu](https://torcheck.xenobite.eu/) 可以检查 Tor 是否正确运行。

## 网页浏览

Tor主要支持Firefox，但是也支持Chromium。

### Firefox

如果你使用Firefox, 你可以安装这个插件: [TorButton](https://www.torproject.org/torbutton/)。这将允许你很容易地在Tor的网络和正常网络切换。

如果你正在使用多代理(例如：如果你想使用 TOR 和 "ssh -D") 也有一个插件叫作 "[FoxyProxy](https://addons.mozilla.org/de/firefox/addon/foxyproxy-standard/)" 他允许你对于不同网址或者全部网址指定多个代理。只需将它指向localhost上的端口8118（polipo运行中）。

为了测试他, 在你的浏览器打开或者关闭Tor浏览这个网址[this website](https://check.torproject.org/)。 更多信息请查看这个网址[the official doc](https://www.torproject.org/docs/tor-doc-unix.html.en)。

### Chromium

当你使用Tor和Chromium时不需要polipo。只需要简单的运行Tor daemon,

然后运行：

```
$ chromium --proxy-server="socks://localhost:9050"

```

## 即时通信

要让即时通信程序使用 Tor，并不需要 [polipo](/index.php/Polipo "Polipo")/[privoxy](/index.php/Privoxy "Privoxy") 等 http 代理。直接使用 tor 守护进程监听的端口 9050 即可。

### Pidgin

通过 preferences -> proxy 进入编辑，设置为：

```
Proxy type 	SOCKS5
Host 	        127.0.0.1
Port 	        9050

```

之后 [pidgin](/index.php/Pidgin "Pidgin") 会使用 Tor 进行通信。有时根据不同账号的 IM 服务配置，需要修改代理设置。在 Accounts -> Manage Accounts 中选择要修改的账号，在 Proxy 标签页中选择：

```
Proxy type 	Use Global Proxy Settings

```

## Irssi

Freenode 不推荐使用 [Irssi](/index.php/Irssi "Irssi") 和 Privoxy。他们推荐 `mapaddress` 方式，通过运行 `torify irssi` 启动。将下行加入 `/etc/tor/torrc`:

```
mapaddress  10.40.40.40 p4fsi4ockecnea7l.onion

```

Freenode 需要 charybdis 和 ircd-seven 的 SASL 机制在连接时进行 nickserv 确认。从 Freenode 网站(即 [http://www.freenode.net/sasl/cap_sasl.pl](http://www.freenode.net/sasl/cap_sasl.pl)) 下载启用 SASL 的 `cap_sasl.pl`，保存到 `~/.irssi/scripts/cap_sasl.pl`

用 [pacman](/index.php/Pacman "Pacman") 安装需要的 perl 模块和 [AUR](/index.php/AUR "AUR") 中的 [perl-crypt-dh](https://aur.archlinux.org/packages/perl-crypt-dh/).

```
$ pacman -S perl-crypt-openssl-bignum perl-crypt-blowfish

```

也可以通过 perl 直接安装:

```
$ perl -MCPAN -e 'install Crypt::OpenSSL::Bignum Crypt::DH Crypt::Blowfish'

```

启动 irssi

```
$ torify irssi

```

加载使用 SASL 机制的脚本：

```
/script load cap_sasl.pl

```

将身份设置到 nickserv，连接时会读取这个值，支持的机制是 PLAIN 和 DH-BLOWFISH。

```
/sasl set <network> <username> <password> <mechanism>

```

连接到 Freenode:

```
/connect -network <network> 10.40.40.40

```

如果遇到问题，请访问 Arch 论坛上的 [Cannot Connect to Freenode IRC using Irssi & Tor](https://bbs.archlinux.org/viewtopic.php?pid=956467)。

### 外部链接

*   [Accessing freenode Via Tor](http://freenode.net/irc_servers.shtml#tor)
*   [SASL README](http://freenode.net/sasl/README.txt)
*   [IRC/SILC torproject.org 上的 Wiki](https://trac.torproject.org/projects/tor/wiki/doc/TorifyHOWTO/IrcSilc)

## 使用 HTTP 代理

如果你需要一个 HTTP 代理。

**注意:** 现在 Tor 开发组推荐在 Privoxy 上使用 Polipo. 

### Polipo

Polipo是一个轻量和快速的HTTP代理. 根据这篇文章来安装和配置[Polipo](/index.php/Polipo "Polipo")。Tor 项目创建了一个定制的[Polipo 配置文件](https://gitweb.torproject.org/torbrowser.git/blob_plain/HEAD:/build-scripts/config/polipo.conf) 来提供让 Polipo更好地匿名。

注意polipo不要求你是否能使用SOCKS 5代理，它自动在9050端口随Tor启动。如果你想在[Chromium](/index.php/Chromium "Chromium")运行Tor,你不需要polipo。查看 [below](#Chromium_and_tor) 如何在 [Chromium](/index.php/Chromium "Chromium") 使用 tor.

### Privoxy

Privoxy 是一个 HTTP 代理，它使用 SOCKS4a 代理进行 html/cookie 过滤。可以安装 [Privoxy](/index.php/Privoxy "Privoxy") 文章安装。

#### 在Firefox使用Tor 和 Privoxy

最简单的方法就是使用[Torbutton](https://www.torproject.org/torbutton) 扩展。

或者, 你可以使用[Foxyproxy](https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard)。然后重启Firefox你就会发现一个新的工具条。 点*Add*, 选*Standard proxy type*. 选 你要的*Proxy Label* , 例如*Tor*。进入“HTTP Proxy”和“SSL Proxy”区域：

```
Hostname: 127.0.0.1 Port: 8118

```

然后Firefox将会用代理连接。你也可以在*No Proxy for* 添加例外。

现在,返回 [http://whatsmyip.net/](http://whatsmyip.net/) 检查你的ip地址是否和以前不同了。

#### 在其他程序使用Tor 和Privoxy

你可以在像即时通信, Jabber, IRC,等软件使用这个方法。

你可以指定代理(127.0.0.1 port 8118)在那些支持HTTP代理的软件里面。

如果使用SOCKS 代理，你可以指定你的程序到Tor (127.0.0.1 port 9050)。用这种方法的一个问题是，虽然自己做DNS解析的应用程序可能会泄漏信息。

你可以考虑使用Socks4A (e.g. via privoxy)来取代他。

## 运行Tor 服务

### 配置

你的带宽必须至少20kb/s:

```
Nickname <tornickname>
ORPort 9001
BandwidthRate 20 KB            # Throttle traffic to 20KB/s
BandwidthBurst 50 KB           # But allow bursts up to 50KB/s

```

允许 Irc 在 6660-6667 端口输出：

```
ExitPolicy accept *:6660-6667,reject *:* # Allow irc ports but no more

```

Tor 作为输出节点:

```
ExitPolicy accept *:119        # Accept nntp as well as default exit policy

```

Tor 作为中间人：

```
ExitPolicy reject *:*

```

## 运行 Tor 桥

根据 [https://www.torproject.org/docs/bridges，将](https://www.torproject.org/docs/bridges，将) torrc 修改为：

```
SocksPort 0
ORPort 443
BridgeRelay 1
Exitpolicy reject *:*

```

如果在启动时出现如下错误：

```
Could not bind to 0.0.0.0:443: Permission denied errors on startup

```

需要选择一个更高的 ORPort (例如 8080) 或者在路由器中 [转发端口](http://www.portforward.com/)。

## TorDNS

Tor 0.2.x系列提供了一个内置的DNS转发器。在Tor配置文件添加如下文件来启动它。

 `/etc/tor/torrc` 
```
 DNSPort 9053
 AutomapHostsOnResolve 1
 AutomapHostsSuffixes .exit,.onion

```

然后重新启动 Tor 来加载更新过的配置文件：

```
/etc/rc.d/tor restart

```

这将让Tor接受DNS请求(在这个例子里面监听着9053端口)。并通过Tor网络域名。一个缺点是，它是仅能够解决一个记录的DNS查询； MX 和NS 请求没有回应。

更多信息请查看 [Debian-based introduction](https://techstdout.boum.org/TorDns/)。

DNS查询，也可以通过命令行`tor-resolve`来查询。例如：

```
$ tor-resolve archlinux.org
66.211.214.131

```

## Torify

`torify` 允许你的程序不需要更改配置来通过访问Tor网络。

man page:

```
 torify  is  a simple wrapper that calls tsocks with a tor specific configuration file.

 tsocks itself is a wrapper between the tsocks library and the  application  that
 you would like to run socksified

```

使用例子：

```
$ torify elinks checkip.dyndns.org
$ torify wget -qO- https://check.torproject.org/ | grep -i congratulations

```

Torify **不会**通过Tor网络来查询DNS。其中一种解决方法就是和`tor-resolve` 来解决(前文所述)。在这种情况下, 上面的例子程序将像这样

```
$ tor-resolve checkip.dyndns.org
208.78.69.70
$ torify elinks 208.78.69.70

```

## 问题解决

### User value的问题

如果*tor* daemon启动失败，你可以在root环境下运行一下命令(或者使用sudo)

```
# tor

```

如果你收到以下 error

```
May 23 00:27:24.624 [warn] Error setting groups to gid 43: "Operation not permitted".
May 23 00:27:24.624 [warn] If you set the "User" option, you must start Tor as root.
May 23 00:27:24.624 [warn] Failed to parse/validate config: Problem with User value. See logs for details.
May 23 00:27:24.624 [err] Reading config failed--see warnings above.

```

它意味着你的User value有问题。通过以下的步骤解决：

运行以下命令检查`/var/lib/tor`目录的权限

```
# ls -l /var/lib/

```

如果`/var/lib/tor`权限显示如下

```
drwx------ 2 tor    tor    4096 May 12 21:03 tor

```

这意味着它被*tor*用户和 *tor*组所拥有

通过以下命令把拥有者和组改为*root*, *root*

```
# chown -R root:root /var/lib/tor

```

如果你重新检查权限,他现在应该显示为

```
drwx------ 2 root   root   4096 May 12 21:03 tor

```

现在打开 `/etc/tor/torrc`找到以下文字

```
## Uncomment this to start the process in the background... or use
## --runasdaemon 1 on the command line.
RunAsDaemon 1
User tor
Group tor

```

注释掉*User tor* 和*Group tor*, 所以他应该显示为

```
## Uncomment this to start the process in the background... or use
## --runasdaemon 1 on the command line.
RunAsDaemon 1
#User tor
#Group tor

```

保存更改然后重启*tor* daemon, 他应该能够工作了

```
# /etc/rc.d/tor restart

```

## 外部链接

*   [Official Website](https://www.torproject.org/)
*   [Unix-based Tor Articles](https://trac.torproject.org/projects/tor/wiki#Unixish)
*   [Software commonly integrated with Tor](https://trac.torproject.org/projects/tor/wiki/doc/SupportPrograms)
*   [How to set up a Tor *Hidden Service*](https://www.torproject.org/docs/tor-hidden-service.html.en)