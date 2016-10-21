**翻译状态：** 本文是英文页面 [Network_Time_Protocol_daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-10-21，点击[这里](https://wiki.archlinux.org/index.php?title=Network_Time_Protocol_daemon&diff=0&oldid=446540)可以查看翻译后英文页面的改动。

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
    *   [4.1 Start ntpd on network connection](#Start_ntpd_on_network_connection)
    *   [4.2 Using ntpd with GPS](#Using_ntpd_with_GPS)
    *   [4.3 Running in a chroot](#Running_in_a_chroot)
*   [5 排错](#.E6.8E.92.E9.94.99)
    *   [5.1 无法分配请求地址](#.E6.97.A0.E6.B3.95.E5.88.86.E9.85.8D.E8.AF.B7.E6.B1.82.E5.9C.B0.E5.9D.80)
*   [6 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [ntp](https://www.archlinux.org/packages/?name=ntp) 软件包。如果不做任何配置， *ntpd* 默认工作于客户端模式。如果使用 Arch Linux 默认的配置，请跳转到 [#使用](#.E4.BD.BF.E7.94.A8)。作为服务器的配置，请参阅 [#NTP 服务器模式](#NTP_.E6.9C.8D.E5.8A.A1.E5.99.A8.E6.A8.A1.E5.BC.8F)。

## 配置

主要的后台进程是 *ntpd*, 可以通过 `/etc/ntp.conf` 配置。详细信息可以参考手册 `man ntp.conf` 和相关的 `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`.

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

"restrict"选项的完整文档可以从 `man ntp_acc` 中查找到。详见 [https://support.ntp.org/bin/view/Support/AccessRestrictions](https://support.ntp.org/bin/view/Support/AccessRestrictions) 。

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

**注意:** 定义日志文件不是必须的，但是它对于反馈 *ntpd* 操作是有好处的。

## 使用

软件包默认包含客户端模式的配置，并且使用单独的用户和群组，启动时就会移除 root 权限。如果在终端中启动，请使用 `-u` 选项:

```
# ntpd -u ntp:ntp

```

systemd 服务默认使用 `-u` 选项和 `-g` 选项禁用一个阈值(*panic-gate*). 这样即使 ntp-server 的时间和系统时间的差异超过阈值，依然会同步时间。

**Warning:** 使用 panic-gate 的原因是某些后台任务或服务会引起时间跳跃. 如果系统的时间从来没有同步过，请考虑先禁用其他服务再进行同步。

两个服务都依赖系统网络状况，会在检测到网络连接时开始同步。

### 启动时启用 ntpd

[启用](/index.php/Enable "Enable") `ntpd.service` 服务.

**Note:** systemd 命令 *timedatectl* 仅可以控制 [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd"), 用 root 执行 `timedatectl set-ntp 1` 会停止运行中的 `ntpd.service`.[[1]](http://lists.freedesktop.org/archives/systemd-devel/2015-April/030277.html)

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

### Start ntpd on network connection

*ntpd* can be started by your network manager, so that the daemon only runs when the computer is online.

	Netctl

Append the following lines to your [netctl](/index.php/Netctl "Netctl") profile:

```
ExecUpPost='/usr/bin/ntpd || true'
ExecDownPre='killall ntpd || true'

```

	NetworkManager

The *ntpd* daemon can be brought up/down along with a network connection through the use of NetworkManager's [dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") scripts. The [networkmanager-dispatcher-ntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-ntpd) package installs one, pre-configured to start and stop the [ntpd service](#Start_ntpd_at_boot) with a connection.

	Wicd

For [Wicd](/index.php/Wicd "Wicd"), create a start script in the `postconnect` directory and a stop script in the `predisconnect` directory. Remember to make them executable:

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

**Note:** You are advised to customize the options for the *ntpd* command as explained in [#Usage](#Usage).

See also [Wicd#Scripts](/index.php/Wicd#Scripts "Wicd").

	KDE

KDE can use NTP (ntp must be installed) by right clicking the clock and selecting *Adjust date/time*. However, this requires the ntp daemon to be [disabled](/index.php/Disable "Disable") before configuring KDE to use NTP. [[2]](https://bugs.kde.org/show_bug.cgi?id=178968)

### Using ntpd with GPS

Most of the articles online about configuring *ntpd* to receive time from a GPS suggest to use the SHM (shared memory) method. However, at least since *ntpd* version 4.2.8 a *much better* method is available. It connects directly to *gpsd*, so [gpsd](https://www.archlinux.org/packages/?name=gpsd) needs to be installed.

Add these lines to your `/etc/ntp.conf`:

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

This will work as long as you have *gpsd* working. It connects to *gpsd* via the local socket and queries the "gpsd_json" object that is returned.

To test the setup, first ensure that *gpsd* is working by running:

```
 $ cgps -s 

```

Then wait a few minutes and run `ntpq -p`. This will show if *ntpd* is talking to *gpsd*:

 `$ ntpq -p` 
```
remote           refid            st t when poll reach   delay   offset  jitter
 ==================================================================================
*GPSD_JSON(0)    .GPS.            0 l   55   64  377    0.000    2.556  14.109
```

**Tip:** If the *reach* column is 0, it means *ntpd* has not been able to talk to *gpsd*. Wait a few minutes and try again. Sometimes it takes *ntpd* a while.

### Running in a chroot

**Note:** *ntpd* should be started as non-root (default in the Arch Linux package) before attempting to jail it in a chroot, since chroots are relatively useless at securing processes running as root.

Create a new directory `/etc/systemd/system/ntpd.service.d/` if it does not exist and a file named `customexec.conf` inside with the following content:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -g -i /var/lib/ntp -u ntp:ntp -p /run/ntpd.pid

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
/lib		  /var/lib/ntp/lib none bind 0 0
/proc		  /var/lib/ntp/proc none bind 0 0

```

```
# mount -a

```

Finally, restart `ntpd` daemon again. Once it restarted you can verify that the daemon process is chrooted by checking where `/proc/{PID}/root` symlinks to:

```
# ps -C ntpd | awk '{print $1}' | sed 1d | while read -r PID; do ls -l /proc/$PID/root; done

```

should now link to `/var/lib/ntp` instead of `/`.

It is relatively difficult to be sure that your driftfile configuration is actually working without waiting a while, as *ntpd* does not read or write it very often. If you get it wrong, it will log an error; if you get it right, it will update the timestamp. If you do not see any errors about it after a full day of running, and the timestamp is updated, you should be confident of success.

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