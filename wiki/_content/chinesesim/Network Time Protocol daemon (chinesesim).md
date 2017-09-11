相关文章

*   [Time (简体中文)](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)")
*   [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")
*   [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")
*   [Chrony](/index.php/Chrony "Chrony")

**翻译状态：** 本文是英文页面 [Network_Time_Protocol_daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-04-22，点击[这里](https://wiki.archlinux.org/index.php?title=Network_Time_Protocol_daemon&diff=0&oldid=446540)可以查看翻译后英文页面的改动。

[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") （网络时间协议）是 GNU/Linux 系统通过互联网时间服务器同步系统[软件时钟](/index.php/Time_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Time (简体中文)")的最常见方法。设计时考虑到了各种网络延迟，通过公共网络同步时，误差可以降低到10毫秒以内；通过本地网络同步时，误差可以降低到 1 毫秒。

[NTP 项目](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project)提供了一个名为简单 NTP 的参考实现。本文介绍如何设置和运行服务器和客户端 NTP 进程。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 连接到 NTP 服务器](#.E8.BF.9E.E6.8E.A5.E5.88.B0_NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [2.2 NTP 服务器模式](#NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.A8.A1.E5.BC.8F)
*   [3 使用](#.E4.BD.BF.E7.94.A8)
    *   [3.1 启动时启用 ntpd](#.E5.90.AF.E5.8A.A8.E6.97.B6.E5.90.AF.E7.94.A8_ntpd)
    *   [3.2 每次启动同步一次](#.E6.AF.8F.E6.AC.A1.E5.90.AF.E5.8A.A8.E5.90.8C.E6.AD.A5.E4.B8.80.E6.AC.A1)
*   [4 技巧](#.E6.8A.80.E5.B7.A7)
    *   [4.1 有网络连接的时候启动ntpd](#.E6.9C.89.E7.BD.91.E7.BB.9C.E8.BF.9E.E6.8E.A5.E7.9A.84.E6.97.B6.E5.80.99.E5.90.AF.E5.8A.A8ntpd)
    *   [4.2 在GPS中使用NTP](#.E5.9C.A8GPS.E4.B8.AD.E4.BD.BF.E7.94.A8NTP)
    *   [4.3 在 chroot 底下运行](#.E5.9C.A8_chroot_.E5.BA.95.E4.B8.8B.E8.BF.90.E8.A1.8C)
*   [5 排错](#.E6.8E.92.E9.94.99)
    *   [5.1 无法分配请求地址](#.E6.97.A0.E6.B3.95.E5.88.86.E9.85.8D.E8.AF.B7.E6.B1.82.E5.9C.B0.E5.9D.80)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [ntp](https://www.archlinux.org/packages/?name=ntp) 软件包。如果不做任何配置， *ntpd* 默认工作于客户端模式。如果使用 Arch Linux 默认的配置，请跳转到 [#使用](#.E4.BD.BF.E7.94.A8)。作为服务器的配置，请参阅 [#NTP 服务器模式](#NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.A8.A1.E5.BC.8F)。

## 配置

主要的后台进程是 *ntpd*, 可以通过 `/etc/ntp.conf` 配置。详细信息可以参考手册 [ntp.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ntp.conf.5) 和相关的 `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`.

### 连接到 NTP 服务器

NTP 服务器通过一个层级系统进行分类，不同的层级称为 *strata*: 独立的时间源为*stratum 0*; 直接连接到 *stratum 0* 的设备为 *stratum 1*;直接连接到 *stratum 1* 的源为 *stratum 2*，以此类推。

服务器的 stratum 并不能完全等同于它的精度和可靠度。通常的时间同步都使用 stratum 2 服务器。通过[pool.ntp.org](http://www.pool.ntp.org/) 服务器或[这个链接](http://support.ntp.org/bin/view/Servers/NTPPoolServers) 可以选择比较近的服务器池。

下面几行仅仅是例子：

 `/etc/ntp.conf` 
```
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst

```

推荐使用`iburst`选项,如果第一次尝试无法建立连接，程序会发送一系列的包。`burst` 选项则总是发送一系列的包，即使第一次也是这样。如果没有明确的允许的话不要使用 *burst* 选项，有可能被封禁。

### NTP 服务器模式

如果建立一个 NTP 服务器，你需要添加 [*local clock*](http://www.ntp.org/ntpfaq/NTP-s-refclk.htm#Q-LOCAL-CLOCK) 作为一个服务器，这样，即便它失去网络连接，它也可以继续为网络提供服务;添加 *local clock* 作为一个 stratum 10 服务器 (使用 *fudge* 命令)这样它就只会在失去连接时使用本地时钟：

```
server 127.127.1.0
fudge  127.127.1.0 stratum 10

```

下一步，定义规则允许客户端连接你的服务(*localhost* 也被认为是一个客户端)。使用 *restrict* 命令；你应该在文件中已经有一行：

```
restrict default nomodify nopeer noquery

```

这限制了每个人做任何修改并阻止每个人请求你的时间服务器状态：`nomodify` 防止重新配置你的ntpd（使用*ntpq* 或 *ntpdc* ），`noquery` 防止从你的nptd（或是*ntpq* 和 *ntpdc*）获取状态数据。

你也能添加其它选项：

```
restrict default kod nomodify notrap nopeer noquery

```

**注意:** 这会允许其他人查询你的时间服务器。你需要添加 `noserve` 来停止提供时间。

"restrict"选项的完整文档可以从 [ntp_acc()](http://jlk.fjfi.cvut.cz/arch/manpages/man/ntp_acc.) 中查找到。详见 [https://support.ntp.org/bin/view/Support/AccessRestrictions](https://support.ntp.org/bin/view/Support/AccessRestrictions) 。

你需要在这一行之后告诉 *ntpd* 什么可以访问你的服务器；如果你不是在配置一台 NTP 服务器的话，下面一行就足够了。

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

一份基础的配置文件是这样的：

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

**注意:** 定义日志文件不是必须的，但是它对于反馈 *ntpd* 操作是有好处的。

## 使用

软件包默认包含客户端模式的配置，并且使用单独的用户和群组，启动时就会移除 root 权限。如果在终端中启动，请使用 `-u` 选项:

```
# ntpd -u ntp:ntp

```

systemd 服务默认使用 `-u` 选项和 `-g` 选项禁用一个阈值(*panic-gate*). 这样即使 ntp-server 的时间和系统时间的差异超过阈值，依然会同步时间。

**警告:** 使用 panic-gate 的原因是某些后台任务或服务会引起时间跳跃. 如果系统的时间从来没有同步过，请考虑先禁用其他服务再进行同步。

两个服务都依赖系统网络状况，会在检测到网络连接时开始同步。

### 启动时启用 ntpd

[启用](/index.php/Enable "Enable") `ntpd.service` 服务.

**注意:** systemd 命令 *timedatectl* 仅可以控制 [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd"), 用 root 执行 `timedatectl set-ntp 1` 会停止运行中的 `ntpd.service`.[[1]](http://lists.freedesktop.org/archives/systemd-devel/2015-April/030277.html)

用 *ntpq* 可以查看同步的状态：

```
$ ntpq -p

```

delay, offset 和 jitter 不应该为零，*ntpd* 同步的服务器前有星号，*ntpd* 可能等待很多分钟后才会进行同步，请等 17 分钟 (1024 秒).

### 每次启动同步一次

另一种方式是 [启用](/index.php/Enable "Enable") `ntpdate.service` 服务，每次启动都同步一次(`-q`) 并且是 non-forking (`-n`), 进程不会在后台运行。如果是服务器或者很多天才会重启一次，不建议使用此方式。

如果需要把同步到的时间写入硬件时钟，请按照 [这里](/index.php/Systemd#Editing_provided_units "Systemd") 的说明修改服务并启动:

 `/etc/systemd/system/ntpdate.service.d/hwclock.conf` 
```
[Service]
ExecStart=/usr/bin/hwclock -w
```

## 技巧

### 有网络连接的时候启动ntpd

*ntpd* 可以由你的网络管理器启动, 所以ntp这个守护进程只有在计算机有网络连接的时候才会启动.

	Netctl

给你的 [netctl](/index.php/Netctl "Netctl") 配置文件添加如下这几行:

```
ExecUpPost='/usr/bin/ntpd || true'
ExecDownPre='killall ntpd || true'

```

	NetworkManager

通过网络管理器的 [dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") 脚本，可以同网络连接一起启动/终止*ntpd* 守护进程。 安装[networkmanager-dispatcher-ntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-ntpd) 预配置包 [ntpd service](#Start_ntpd_at_boot) 来让网络连接同步ntp启动/终止.

	Wicd

对 [Wicd](/index.php/Wicd "Wicd") 来说, 要在 `postconnect` 目录创建一个启动脚本，在 `predisconnect` 目录创建一个终止脚本。 记住要把他们设为可执行的哦:

 `/etc/wicd/scripts/postconnect/ntpd` 
```
#!/bin/bash
systemctl start ntpd &

```
 `/etc/wicd/scripts/predisconnect/ntpd` 
```
#!/bin/bash
systemctl stop ntpd &

```

**注意:** 根据 [#Usage](#Usage) 对*ntpd* 这个命令的说明，你可以自由设置自己的配置选项。

参照 [Wicd#Scripts](/index.php/Wicd#Scripts "Wicd").

	KDE

在KDE中，通过右击桌面选择 *Adjust date/time*，可以使用 NTP (别忘了安装NTP)。 注意, 在配置KDE中配置NTP之前，先要把 ntp 守护进程设置为 [disabled](/index.php/Disable "Disable") 状态. [[2]](https://bugs.kde.org/show_bug.cgi?id=178968)

### 在GPS中使用NTP

大多数联网的交通工具要通过(共享内存) 方式让 *ntpd* 从GPS中接收时间。 但是, 从 *ntpd* 4.2.8版本开始，一个 *更好* 的办法出现了----直接与 *gpsd*守护进程交互。这个要先安装 [gpsd](https://www.archlinux.org/packages/?name=gpsd) .

在 `/etc/ntp.conf` 配置文件中添加下面这几行:

 `/etc/ntp.conf` 
```
#=========================================================
#  GPSD native ntpd driver
#=========================================================
# This driver exists from at least ntp version 4.2.8
# Details at
#   [https://www.eecis.udel.edu/~mills/ntp/html/drivers/driver46.html](https://www.eecis.udel.edu/~mills/ntp/html/drivers/driver46.html)
server 127.127.46.0 
fudge 127.127.46.0 time1 0.0 time2 0.0 refid GPS
```

只要 *gpsd* 一直起着，ntp就会一直正常运行。 ntp会通过一个本地套接字同 *gpsd* 连接, 搜索 *gpsd* 返回的 "gpsd_json" 对象.

要检验安装的话, 首先要检查 *gpsd* 是不是正常运行:

```
 $ cgps -s 

```

然后等个几分钟运行 `ntpq -p`. 这个会显示 *ntpd* 是否已经跟 *gpsd* 建立连接了:

 `$ ntpq -p` 
```
remote           refid            st t when poll reach   delay   offset  jitter
 ==================================================================================
*GPSD_JSON(0)    .GPS.            0 l   55   64  377    0.000    2.556  14.109
```

**提示：** 如果 *reach* 这列是0的话, 这就说明 *ntpd* 还没有同 *gpsd* 建立连接。 等几分钟再试一次。 有时 *ntpd* 要花点时间来跟*gpsd* 建立连接。

### 在 chroot 底下运行

**注意:** 在试图把 *ntpd* 放到chroot目录下面之前，*ntpd* 应该在正常路径下启动 (默认在 Arch Linux 安装路径下)。 因为在相对以root身份运行的进程，chroots的用户相对没有啥权限的。

创建一个新目录（如果还没创建的话） `/etc/systemd/system/ntpd.service.d/`，并添加在里面添加文件 `customexec.conf` ,内容如下:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -g -i /var/lib/ntp -u ntp:ntp -p /run/ntpd.pid

```

然后, 编辑 `/etc/ntp.conf` 来改变 driftfile 路径来让跟它跟 chroot 路径保持一致, 而不是还用原先的普通路径。修改

```
driftfile       /var/lib/ntp/ntp.drift

```

为

```
driftfile       /ntp.drift

```

通过root创建永久目录和文件，作为一个合适的 chroot 环境来支持 getaddrinfo() :

```
# mkdir /var/lib/ntp/etc /var/lib/ntp/lib /var/lib/ntp/proc
# touch /var/lib/ntp/etc/resolv.conf /var/lib/ntp/etc/services

```

然后通过修改 *fstab* 绑定前面提到的文件:

 `/etc/fstab` 
```
...
#ntpd chroot mounts
/etc/resolv.conf  /var/lib/ntp/etc/resolv.conf none bind 0 0
/etc/services	  /var/lib/ntp/etc/services none bind 0 0
/lib		  /var/lib/ntp/lib none bind 0 0
/proc		  /var/lib/ntp/proc none bind 0 0

```

```
# mount -a

```

最后, 再一次重启 `ntpd` 监控进程。 一旦重启完成你就可以通过检查 `/proc/{PID}/root` 的软连接来判断监控进程是不是在 chrooted 下面工作:

```
# ps -C ntpd | awk '{print $1}' | sed 1d | while read -r PID; do ls -l /proc/$PID/root; done

```

正常应该链接到 `/var/lib/ntp` 而不是 `/`.

不用等一段时间就要确定 driftfile 配置是否工作正常是比较困难的, 因为 *ntpd* 不会经常读写。 如果配置错误的话，log里面会打印一个error; 如果配置正确的话, 时间戳会更新的。 可以通过等一天来判断，如果没有log中没有错误打印，并且log的时间戳还更新了，那么说明配置成功了。

## 排错

### 无法分配请求地址

如果收到下列*无法分配请求地址*的报错信息：

 `$ journalctl -u ntpd` 
```
ntpd[2130]: bind(21) AF_INET6 fe80::6ef0:49ff:fe51:4946%2#123 flags 0x11 failed: Cannot assign requested address
ntpd[2130]: unable to create socket on eth0 (5) for fe80::6ef0:49ff:fe51:4946%2#123
ntpd[2130]: failed to init interface for address fe80::6ef0:49ff:fe51:4946%2
```

可以禁用 IPv6 解决。做法是：[编辑](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BF.AE.E6.94.B9.E7.8E.B0.E5.AD.98.E5.8D.95.E5.85.83.E6.96.87.E4.BB.B6 "Systemd (简体中文)") `ntpd.service` 添加 `-4` 参数：

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -g -u ntp:ntp **-4**

```

## 参见

*   [http://www.ntp.org/](http://www.ntp.org/)
*   [http://support.ntp.org/](http://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [http://www.eecis.udel.edu/~mills/ntp/html/index.html](http://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)