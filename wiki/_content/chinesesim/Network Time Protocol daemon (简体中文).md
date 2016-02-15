**翻译状态：** 本文是英文页面 [Network_Time_Protocol_daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-19，点击[这里](https://wiki.archlinux.org/index.php?title=Network_Time_Protocol_daemon&diff=0&oldid=390018)可以查看翻译后英文页面的改动。

[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") （网络时间协议）是 GNU/Linux 系统通过Internet 时间服务器同步系统[软件时钟](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)")的最常见方法。设计时考虑到了各种网络延迟，通过公共网络同步时，误差可以降低到10毫秒以内；通过本地网络同步时，误差可以降低到 1 毫秒。

[NTP 项目](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project)提供了一个名为简单 NTP 的参考实现。本文介绍如何设置和运行服务器和客户端 NTP 进程。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 连接到 NTP 服务器](#.E8.BF.9E.E6.8E.A5.E5.88.B0_NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [2.2 NTP 服务器模式](#NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.A8.A1.E5.BC.8F)
    *   [2.3 其他关于配置 NTP 的资源](#.E5.85.B6.E4.BB.96.E5.85.B3.E4.BA.8E.E9.85.8D.E7.BD.AE_NTP_.E7.9A.84.E8.B5.84.E6.BA.90)
*   [3 不以守护进程使用](#.E4.B8.8D.E4.BB.A5.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E4.BD.BF.E7.94.A8)
    *   [3.1 启动时同步一次时钟](#.E5.90.AF.E5.8A.A8.E6.97.B6.E5.90.8C.E6.AD.A5.E4.B8.80.E6.AC.A1.E6.97.B6.E9.92.9F)
*   [4 作为守护进程运行](#.E4.BD.9C.E4.B8.BA.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E8.BF.90.E8.A1.8C)
    *   [4.1 启动 ntpd](#.E5.90.AF.E5.8A.A8_ntpd)
    *   [4.2 NetworkManager](#NetworkManager)
    *   [4.3 Running in a chroot](#Running_in_a_chroot)
*   [5 Alternatives](#Alternatives)
*   [6 参见](#.E5.8F.82.E8.A7.81)
*   [7 外部链接](#.E5.A4.96.E9.83.A8.E9.93.BE.E6.8E.A5)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [ntp](https://www.archlinux.org/packages/?name=ntp) 软件包。如果不做任何配置， _ntpd_ 默认工作于客户端模式。如果使用 Arch Linux 默认的配置，请跳转到 [#使用](#.E4.BD.BF.E7.94.A8)。作为服务器的配置，请参阅 [#NTP 服务器模式](#NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.A8.A1.E5.BC.8F)。

## 配置

主要的后台进程是 _ntpd_, 可以通过 `/etc/ntp.conf` 配置。详细信息可以参考手册 `man ntp.conf` 和相关的 `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`.

### 连接到 NTP 服务器

NTP 服务器通过一个层级系统进行分类，不同的层级称为 _strata_: 独立的时间源为_stratum 0_; 直接连接到 _stratum 0_ 的设备为 _stratum 1_;直接连接到 _stratum 1_ 的源为 _stratum 2_，以此类推。

服务器的 stratum 并不能完全等同于它的精度和可靠度。通常的时间同步都使用 stratum 2 服务器。通过[pool.ntp.org](http://www.pool.ntp.org/) 服务器或[这个链接](http://support.ntp.org/bin/view/Servers/NTPPoolServers) 可以选择比较近的服务器池。

下面几行仅仅是例子：

 `/etc/ntp.conf` 

```
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst

```

推荐使用`iburst`选项,如果第一次尝试无法建立连接，程序会发送一系列的包。`burst` 选项则总是发送一系列的包，即使第一次也是这样。如果没有明确的允许的话不要使用 _burst_ 选项，有可能被封禁。

### NTP 服务器模式

如果建立一个 NTP 服务器，你需要添加 [_local clock_](http://www.ntp.org/ntpfaq/NTP-s-refclk.htm#Q-LOCAL-CLOCK) 作为一个服务器，这样，即便它失去网络连接，它也可以继续为网络提供服务;添加 _local clock_ 作为一个 stratum 10 服务器 (使用 _fudge_ 命令)这样它就只会在失去连接时使用本地时钟：

```
server 127.127.1.0
fudge  127.127.1.0 stratum 10

```

下一步，定义规则允许客户端连接你的服务(_localhost_ 也被认为是一个客户端)。使用 _restrict_ 命令；你应该在文件中已经有一行：

```
restrict default nomodify nopeer noquery

```

这限制了每个人做任何修改并阻止每个人请求你的时间服务器状态：`nomodify` 防止重新配置你的ntpd（使用_ntpq_ 或 _ntpdc_ ），`noquery` 防止从你的nptd（或是_ntpq_ 和 _ntpdc_）获取状态数据。

你也能添加其它选项：

```
restrict default kod nomodify notrap nopeer noquery

```

**注意:** 这会允许其他人查询你的时间服务器。你需要添加 `noserve` 来停止提供时间。

"restrict"选项的完整文档可以从 `man ntp_acc` 中查找到。详见 [https://support.ntp.org/bin/view/Support/AccessRestrictions](https://support.ntp.org/bin/view/Support/AccessRestrictions) 。

你需要在这一行之后告诉 _ntpd_ 什么可以访问你的服务器；如果你不是在配置一台 NTP 服务器的话，下面一行就足够了。

```
restrict 127.0.0.1

```

如果你想要强制DNS解析到IPv6域名，在IP地址或域名前写上 `-6`（`-4` 则强制使用IPv4域名），例如:

```
restrict -6 default kod nomodify notrap nopeer noquery
restrict -6 ::1    # ::1 is the IPv6 equivalent for 127.0.0.1

```

最后，指定drift文件（它能时刻监控你的时钟的时间漂移）和log文件的位置：

```
driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

一份基础的配置文件是这样的 （**为了清晰起见，已删掉了所有的注释**）：

 `/etc/ntp.conf` 

```
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

restrict default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery

restrict 127.0.0.1
restrict -6 ::1  

driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

**注意:** 定义日志文件不是必须的，但是它对于反馈 _ntpd_ 操作是有好处的。

### 其他关于配置 NTP 的资源

总之，永远不要忘记手册页： `man ntp.conf` 有可能可以回答你仍旧有的任何疑问。（见相关的手册页： `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`）。

## 不以守护进程使用

想要仅仅同步时钟一次，不想启动守护进程的话，运行：

```
# ntpd -qg
# hwclock -w

```

`ntpd -qg` 与 `ntpdate` 程序效果相同，而ntpdate 已经[不推荐使用](http://support.ntp.org/bin/view/Dev/DeprecatingNtpdate). `hwclock -w` 把时间存储到硬件时钟上，这样重启的时候就不会丢失了。

`ntpd` 的 `-g` 选项允许时钟漂移大于警报级别(默认是 15 分钟)而不发出警告。注意这种误差是不正常的，也许意味着失去设置错误，时钟芯片错误，或仅仅是长时间的忽略。如果在这些情况下你不想设置时钟而且输出错误到 syslog，删除 `-g`：

```
# ntpd -q

```

### 启动时同步一次时钟

**警告:** 这种方法不推荐在服务器上或是需要连续运行2到3天的普通机器上使用，因为系统时钟仅会在启动时更新一次。

写一个 _oneshot_ [systemd](/index.php/Systemd "Systemd") 模块：

 `/etc/systemd/system/ntp-once.service` 

```
[Unit]
Description=Network Time Service (once)
After=network.target nss-lookup.target 

[Service]
Type=oneshot
ExecStart=/usr/bin/ntpd -q -g -u ntp:ntp ; /sbin/hwclock -w

[Install]
WantedBy=multi-user.target
```

并启动它: `# systemctl enable ntp-once` 

## 作为守护进程运行

### 启动 ntpd

启动：

```
# systemctl start ntpd

```

开机启动：

```
# systemctl enable ntpd

```

或者使用：

```
# timedatectl set-ntp 1

```

### NetworkManager

**Note:** ntpd should still be running when the network is down if the hwclock daemon is disabled, so you should not use this.

_ntpd_ can be brought up/down along with a network connection through the use of [NetworkManager's dispatcher scripts](/index.php/NetworkManager#Network_Services_with_NetworkManager_Dispatcher "NetworkManager"). You can install the needed script from [community]:

 `# pacman -S networkmanager-dispatcher-ntpd` 

### Running in a chroot

**Note:** Before attempting this, complete the previous section on running as non-root, since chroots are relatively useless at securing processes running as root.

Edit `/etc/conf.d/ntpd.conf` and change

```
NTPD_ARGS="-g -u ntp:ntp"

```

to

```
NTPD_ARGS="-g -i /var/lib/ntp -u ntp:ntp"

```

Then, edit `/etc/ntp.conf` to change the driftfile path such that it is relative to the chroot directory, rather than to the real system root. Change:

```
driftfile       /var/lib/ntp/ntp.drift

```

to

```
driftfile       /ntp.drift

```

Create a suitable chroot environment so that getaddrinfo() will work by creating pertinent directories and files (as root):

```
# mkdir /var/lib/ntp/etc /var/lib/ntp/lib /var/lib/ntp/proc
# touch /var/lib/ntp/etc/resolv.conf /var/lib/ntp/etc/services
```

and by bind-mounting the aformentioned files:

 `/etc/fstab` 

```
...
#ntpd chroot mounts
/etc/resolv.conf  /var/lib/ntp/etc/resolv.conf none bind 0 0
/etc/services	  /var/lib/ntp/etc/services none bind 0 0
/lib		          /var/lib/ntp/lib none bind 0 0
/proc		  /var/lib/ntp/proc none bind 0 0

```

 `# mount -a` 

Finally, restart the daemon again:

 `# rc.d restart ntpd` 

It is relatively difficult to be sure that your driftfile configuration is actually working without waiting a while, as ntpd does not read or write it very often. If you get it wrong, it will log an error; if you get it right, it will update the timestamp. If you do not see any errors about it after a full day of running, and the timestamp is updated, you should be confident of success.

## Alternatives

Available alternative to NTPd are [Chrony](/index.php/Chrony "Chrony"), a dial-up friendly and specifically designed for systems that are not online all the time, and [OpenNTPD](/index.php/OpenNTPD "OpenNTPD"), part of the OpenBSD project and currently not maintained for Linux.

## 参见

*   [Time (简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)") (更多关于计算机计时的信息)

## 外部链接

*   [http://www.ntp.org/](http://www.ntp.org/)
*   [http://support.ntp.org/](http://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [http://www.eecis.udel.edu/~mills/ntp/html/index.html](http://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)