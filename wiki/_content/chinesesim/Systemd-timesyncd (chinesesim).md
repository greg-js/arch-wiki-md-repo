Related articles

*   [System time](/index.php/System_time "System time")
*   [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")
*   [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")
*   [Chrony](/index.php/Chrony "Chrony")
*   [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")
*   [systemd](/index.php/Systemd "Systemd")

**翻译状态：** 本文是英文页面 [Systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-13，点击[这里](https://wiki.archlinux.org/index.php?title=Systemd-timesyncd&diff=0&oldid=435960)可以查看翻译后英文页面的改动。

来自于 [systemd mailing list](http://lists.freedesktop.org/archives/systemd-devel/2014-May/019537.html):

	*systemd-timesyncd* 是一个用于跨网络同步系统时钟的守护服务。它实现了一个 SNTP 客户端。与NTP的复杂实现相比，这个服务简单的多，它只专注于从远程服务器查询然后同步到本地时钟。除非你打算为客户端提供 NTP 服务器或者连接本地硬件时钟，否则这个简单的NTP客户端应该更适合大多数人。守护进程运行只需要尽可能小特权，并且会跟网络服务 networkd 挂钩，仅在网络连接可用时才工作。每次收到一个新的NTP同步请求时，后台服务就把当前时间保存到磁盘，并尽可能在系统启动时修正系统时间，这样处理的目的是为了适应像Raspberry Pi和嵌入式设备这种缺少 RTC 的系统，并确保这些系统时单点处理（即使它并不是总是正确的）。如果要使用这个守护进程，需要在安装系统时创建一个新的系统用户和组"systemd-timesync"。

## 安装

*systemd-timesyncd* 服务可以通过 [systemd](https://www.archlinux.org/packages/?name=systemd) 获取。 启动服务:

```
# timedatectl set-ntp true 

```

使用 `timedatectl status`检查服务状态：

 `$ timedatectl status` 
```
Local time: Thu 2015-07-09 18:21:33 CEST
Universal time: Thu 2015-07-09 16:21:33 UTC
RTC time: Thu 2015-07-09 16:21:33
Time zone: Europe/Amsterdam (CEST, +0200)
Network time on: yes
NTP synchronized: yes
RTC in local TZ: no
```

## 配置

*systemd-timesyncd* 启动时会读取 `/etc/systemd/timesyncd.conf` 配置文件,内容如下:

 `/etc/systemd/timesyncd.conf` 
```
[Time]
#NTP=
#FallbackNTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
```

要增加或者更改 [时间同步服务器](/index.php/Network_Time_Protocol_daemon#Connection_to_NTP_servers "Network Time Protocol daemon"), 取消上文的注释。例如，你可以使用 [NTP 项目](http://www.pool.ntp.org/) 或者 [Arch默认](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ntp&id=1b485f87c9e1384eaf069d031e415515e8ead92d) (NTP 也有这个站点) 提供的任何时间服务器：

 `/etc/systemd/timesyncd.conf` 
```
[Time]
NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
FallbackNTP=0.pool.ntp.org 1.pool.ntp.org 0.fr.pool.ntp.org
```

进一步讲, NTP 服务器也可以通过 [systemd-networkd](/index.php/Systemd-networkd#.5BNetDev.5D_section "Systemd-networkd") 提供，通过 `NTP=` 选项启用, 或者通过DHCP 服务动态加载.

NTP 服务器使用规则:

*   `systemd-networkd.service(8)` 中针对每个接口的配置，或者 DHCP 服务优先。
*   `/etc/systemd/timesyncd.conf` 中定义的 NTP服务器会在运行时被添加到针对每个接口的服务器列表中，守护进程会轮流连接这些服务器直到某个有应答。
*   如果上两步没有取到 NTP 服务器， 那么就是用 `FallbackNTP=` 中定义的服务器。

**警告:** 这个服务每次同步时会写入 /var/lib/systemd/clock 本地文件, 这个目录是硬编码的，不可以更换。这在只读的 root 分区或者最小化安装到 SD 卡时可能有问题。

## 参阅

*   [Forum: systemd-timesyncd is not syncing time](https://bbs.archlinux.org/viewtopic.php?id=182600)
*   [Forum: Using systemd-timesync instead of NTP](https://bbs.archlinux.org/viewtopic.php?id=182172)