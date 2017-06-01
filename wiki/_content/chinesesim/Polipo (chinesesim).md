**警告:** Polipo 已经停止维护，建议使用 squid, privoxy 等其它方案.

来自[Polipo's site](http://www.pps.jussieu.fr/~jch/software/polipo/):

	"*Polipo 是一个小而快速的缓存 web 代理程序(web 缓存, HTTP 代理, 代理服务器)。尽管 Polipo 是为一个人或一小群人使用而设计的，但并不妨碍它为一大群人所使用。*"

下面包括了 Polipo 的安装和设置：

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 优化 Polipo](#.E4.BC.98.E5.8C.96_Polipo)
    *   [2.1 作为指定的用户运行](#.E4.BD.9C.E4.B8.BA.E6.8C.87.E5.AE.9A.E7.9A.84.E7.94.A8.E6.88.B7.E8.BF.90.E8.A1.8C)
*   [3 启动守护进程](#.E5.90.AF.E5.8A.A8.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [3.1 多线程](#.E5.A4.9A.E7.BA.BF.E7.A8.8B)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 浏览器](#.E6.B5.8F.E8.A7.88.E5.99.A8)
    *   [4.2 隧道](#.E9.9A.A7.E9.81.93)
    *   [4.3 Privoxy](#Privoxy)
    *   [4.4 Tor](#Tor)
    *   [4.5 DansGuardian](#DansGuardian)

## 安装

[安装](/index.php/Install "Install") 软件包 [polipo](https://www.archlinux.org/packages/?name=polipo)。

## 优化 Polipo

### 作为指定的用户运行

Polipo 需要使用普通用户运行。这个用户可以建立新的也可以使用旧的：

```
# mkdir /var/cache/polipo
# groupadd -r polipo
# useradd -d /var/cache/polipo -g polipo -r -s /bin/false polipo

```

为了在用特定用户运行之前确保所有的文件和目录都已经被建立，启动然后停止 Polipo。

```
# /etc/rc.d/polipo start
# /etc/rc.d/polipo stop

```

与其他的守护程序以root运行然后尽快的降低权限不同，polipo 是以启动它的用户权限运行的。如果 polipo 是在`/etc/rc.d/polipo`调用的，改变调用行

```
[[ ! -d /var/run/$DAEMON ]] && install -d $DAEMON /var/run/$DAEMON
/usr/bin/$DAEMON $ARGS >/dev/null 2>&1

```

为

```
[[ ! -d /var/run/$DAEMON ]] && install -d $DAEMON --group=polipo --owner=polipo /var/run/$DAEMON
su -c "/usr/bin/$DAEMON $ARGS" -s /bin/sh polipo >/dev/null 2>&1

```

然后也有必要改变几个 polipo 需要写入的目录的所有者/权限：

```
# chown polipo:polipo /var/log/polipo
# chown -R polipo:polipo /var/run/polipo
# chown -R polipo:polipo /var/cache/polipo

```

尽管更好的选择是建立一个被指定用户所有的目录 `/var/log/polipo` 然后通过配置文件的 logFile 变量设置 polipo 的 log 文件到 `/var/log/polipo/polipo.log` 。

## 启动守护进程

以下命令启动 Polipo 守护进程：

```
# /etc/rc.d/polipo start

```

将它添加到 `/etc/rc.conf` 使它在启动时自动运行：

```
DAEMONS=(syslog-ng network netfs **polipo** crond)

```

### 多线程

Polipo 也可以不需要超级用户权限即可运行。想要这样的话，首先复制 `/etc/polipo/config.sample` 到一个合适的目录：

```
$ cp /etc/polipo/config.sample ~/.poliporc

```

编辑并将 `/var/cache/polipo` 替换成一个可写入的目录:

```
# Uncomment this if you want to put the on-disk cache in a
# non-standard location:
diskCacheRoot = "~/.polipo-cache/"

```

创建 cache 目录：

```
$ mkdir ~/.polipo-cache

```

最后，使用新配置文件启动：

```
$ polipo -c ~/.poliporc

```

## 配置

管理通常是在 `/etc/polipo/config` 进行。大多数用户可以选择使用示例配置文件，它适合大多数情况，注释很详细。

```
# cd /etc/polipo; cp config.sample config

```

必须要提到的 Polipo 配置中的一个要素是 polipo 的默认行为是通过端口屏蔽外部连接。Polipo 的配置文件有两个变量控制允许的外部端口。`allowedPorts` 制定外部HTTP连接的端口。默认是 80-100 和 1024-65535\. `tunnelAllowedPorts` 制定 Polipo 隧道流量允许的端口，以及 HTTPS 流量的端口。默认它是更严格的限制的："*它默认允许 ssh, HTTP, https, rsync, IMAP, imaps, POP, pops, Jabber, CVS 和 Git 流量。*"

如果你看到来自 Polipo 的 "403 Forbidden Port" 错误信息，你需要配置polipo接收更多 HTTP 或 HTTPS的端口。要设定全都允许，添加下面的几行到 `/etc/polipo/config`:

```
allowedPorts = 1-65535
tunnelAllowedPorts = 1-65535

```

与其他代理软件不同，Polipo 需要重启后才能应用改变。

### 浏览器

设置浏览器，让它使用 `localhost:8123` 作为代理。确保禁用浏览器的磁盘缓存来避免冗余的 IO 操作以及低下的性能。

### 隧道

**注意:** 按照 [Polipo FAQ](http://www.pps.jussieu.fr/~jch/software/polipo/faq.html) 关于 "intercepting proxy" 这是不被支持的！

**注意:** 这需要用 Polipo 自己的用户运行它。

除了手动配置每个浏览器和其他程序使用 Polipo 的缓存之外，也可以使用 [iptables](/index.php/Iptables "Iptables") 来通过 polipo 路由。

在安装了 iptables 之后，添加合适的规则到 `/etc/iptables/iptables.rules`：

```
*nat
:PREROUTING ACCEPT [0:0]
:POSTROUTING ACCEPT [0:0]
:OUTPUT ACCEPT [0:0]
*-A OUTPUT -p tcp --dport 80 -m owner ! --uid-owner polipo -j ACCEPT*
*-A OUTPUT -p tcp --dport 80 -j REDIRECT --to-ports 8123*
COMMIT

```

这会通过 Polipo 路由所有的 HTTP 流量。移除浏览器的所有代理设置，然后重新启动 iptables。

### Privoxy

[Privoxy](/index.php/Privoxy "Privoxy") 是一个可以有效拦截广告和其他恶意程序的代理软件。

按照 Polipo 开发人员的建议，为了得到 Privoxy 的隐私性和 Polipo 的大部分性能，你需要把 Polipo 放在 Privoxy 的上游。

也就是说：

*   浏览器指向 Privoxy: `localhost:8118`
*   然后将 Privoxy 流量通过 Polipo: `forward / localhost:8123` 在 Privoxy 配置文件设置。

### Tor

[Tor](/index.php/Tor "Tor")是一个匿名代理网络。

与 Tor 一起使用 Polipo，需要在 `/etc/polipo/config` 取消注释下面的几行：

```
socksParentProxy = localhost:9050
socksProxyType = socks5

```

### DansGuardian

[DansGuardian](/index.php/DansGuardian "DansGuardian") 是一个 web 内容过滤器。 [DansGuardian](/index.php/DansGuardian "DansGuardian") 和 Polipo (而不是 squid 或者 tinyproxy) 共同使用，唯一的不同是在 `dansguardian.conf` 中 proxyport 需要设定为 polipo 的 8123:

```
# the port DansGuardian connects to proxy on
proxyport = 8123

```