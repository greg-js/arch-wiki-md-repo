**翻译状态：** 本文是英文页面 [BIND](/index.php/BIND "BIND") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-09-02，点击[这里](https://wiki.archlinux.org/index.php?title=BIND&diff=0&oldid=271792)可以查看翻译后英文页面的改动。

伯克利互联网名称服务 Berkeley Internet Name Daemon (BIND) 是 DNS 协议的一个参考实现。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 缓存 DNS 服务器](#.E7.BC.93.E5.AD.98_DNS_.E6.9C.8D.E5.8A.A1.E5.99.A8)
*   [3 权威 DNS 服务器](#.E6.9D.83.E5.A8.81_DNS_.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [3.1 1\. 设置一个 zone 文件](#1._.E8.AE.BE.E7.BD.AE.E4.B8.80.E4.B8.AA_zone_.E6.96.87.E4.BB.B6)
    *   [3.2 2\. 配置主服务器](#2._.E9.85.8D.E7.BD.AE.E4.B8.BB.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [3.3 3\. 配置从服务器](#3._.E9.85.8D.E7.BD.AE.E4.BB.8E.E6.9C.8D.E5.8A.A1.E5.99.A8)
*   [4 仅转发 DNS 服务器](#.E4.BB.85.E8.BD.AC.E5.8F.91_DNS_.E6.9C.8D.E5.8A.A1.E5.99.A8)
*   [5 Running BIND in a chrooted environment](#Running_BIND_in_a_chrooted_environment)
*   [6 Configuring BIND to serve DNSSEC signed zones](#Configuring_BIND_to_serve_DNSSEC_signed_zones)
*   [7 Automatically listen on new interfaces without chroot and root privileges](#Automatically_listen_on_new_interfaces_without_chroot_and_root_privileges)
*   [8 参阅](#.E5.8F.82.E9.98.85)
*   [9 BIND 资源](#BIND_.E8.B5.84.E6.BA.90)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")[官方源](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")中的 [bind](https://www.archlinux.org/packages/?name=bind)。

[启动](/index.php/Daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.AE.A1.E7.90.86.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B "Daemon (简体中文)") **named** 守护进程。

## 缓存 DNS 服务器

BIND 的默认配置即为缓存 DNS 服务器，可以直接使用。

你可以编辑 `/etc/named.conf` 并且在 *options* 中加上下面的这一行，来只允许来自 localhost 的查询。

```
listen-on { 127.0.0.1; };

```

如果你想开放外网的查询，你需要编译 `/etc/named.conf` 并且将

```
allow-recursion { 127.0.0.1; };

```

修改为

```
allow-recursion { any; };

```

你可以编辑 `/etc/resolv.conf` 让其使用本机作为 DNS 服务器。

```
nameserver 127.0.0.1

```

[重启](/index.php/Daemon_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E7.AE.A1.E7.90.86.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B "Daemon (简体中文)") **named** 守护进程。

## 权威 DNS 服务器

下面是一个如何设置自己的权威域的简单教程，假设我们要用的权威域为 "domain.tld" （请替换成自己真实的域）

更详尽的教程参见 [Two-in-one DNS server with BIND9](http://www.howtoforge.com/two_in_one_dns_bind9_views).

### 1\. 设置一个 zone 文件

```
# nano /var/named/domain.tld.zone

```

```
$TTL 7200
; domain.tld
@       IN      SOA     ns01.domain.tld. postmaster.domain.tld. (
                                        2007011601 ; Serial
                                        28800      ; Refresh
                                        1800       ; Retry
                                        604800     ; Expire - 1 week
                                        86400 )    ; Minimum
                IN      NS      ns01
                IN      NS      ns02
ns01            IN      A       0.0.0.0
ns02            IN      A       0.0.0.0
localhost       IN      A       127.0.0.1
@               IN      MX 10   mail
imap            IN      CNAME   mail
smtp            IN      CNAME   mail
@               IN      A       0.0.0.0
www             IN      A       0.0.0.0
mail            IN      A       0.0.0.0
@               IN      TXT     "v=spf1 mx"

```

$TTL 定义了这个文件里面的记录在未指定情况下默认的 TTL, 单位是秒。在这个例子中，默认 TTL 为2小时

每次修改 zone 文件的时候，都需要将 Serial 加一，然后再重启 named, 否则 BIND 主服务器不会将 zone 文件的变更发送给从服务器。让主服务器将变更发送给从服务器的条件是主服务器上的 zone 文件的 Serial 比从服务器的大。

### 2\. 配置主服务器

将你的 zone 文件加到 `/etc/named.conf`:

```
zone "domain.tld" IN {
        type master;
        file "domain.tld.zone";
        allow-update { none; };
        notify no;
};

```

如果你想让 BIND 仅仅作为权威服务器使用，不做递归查询，你可以在 `/etc/named.conf` 的 "options" 中关掉递归查询:

```
recursion no;

```

重启 "named"

### 3\. 配置从服务器

TODO

## 仅转发 DNS 服务器

If you have problems with, for example, VPN connections, they can sometimes be solved by setting-up a forwarding DNS server. This is very simple with BIND. Add these lines to `/etc/named.conf`, and change IP address according to your setup.

```
listen-on { 192.168.66.1; };
forwarders { 8.8.8.8; 8.8.4.4; };

```

Don't forget to restart the service!

## Running BIND in a chrooted environment

Running in a [chroot](/index.php/Chroot "Chroot") environment is not required but improves security. See [BIND (chroot)](/index.php/BIND_(chroot) "BIND (chroot)") for how to do this.

## Configuring BIND to serve DNSSEC signed zones

See [DNSSEC#BIND (serving signed DNS zones)](/index.php/DNSSEC#BIND_.28serving_signed_DNS_zones.29 "DNSSEC")

## Automatically listen on new interfaces without chroot and root privileges

Add

```
 interface-interval <rescan-timeout-in-minutes>;

```

parameter into `named.conf` options. Then you should modify rc-script:

```
     stat_busy "Starting DNS"
-    [ -z "$PID" ] && /usr/sbin/named ${NAMED_ARGS}
+    setcap cap_net_bind_service=eip /usr/sbin/named
+    NAMED_ARGS=`echo ${NAMED_ARGS} | sed 's#-u [[:alnum:]]*##'`
+    [ -z "$PID" ] && sudo -u named /usr/sbin/named ${NAMED_ARGS}

```

So your `/etc/rc.d/named` should look like this:

```
     stat_busy "Starting DNS"
     setcap cap_net_bind_service=eip /usr/sbin/named
     NAMED_ARGS=`echo ${NAMED_ARGS} | sed 's#-u [[:alnum:]]*##'`
     [ -z "$PID" ] && sudo -u named /usr/sbin/named ${NAMED_ARGS}

```

Change user name in last line (with "... sudo -u named ...") if your named user is not 'named'.

## 参阅

*   [BIND (chroot)](/index.php/BIND_(chroot) "BIND (chroot)")

## BIND 资源

*   [BIND 9 DNS Administration Reference Book](http://www.reedmedia.net/books/bind-dns/)
*   [Pro DNS and BIND](http://www.netwidget.net/books/apress/dns/intro.html)
*   [Internet Systems Consortium, Inc. (ISC)](http://www.isc.org/)
*   [DNS Glossary](http://www.menandmice.com/knowledgehub/dnsglossary)