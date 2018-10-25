相关文章

*   [网络时间协议](/index.php/Network_Time_Protocol_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol (简体中文)")

**翻译状态：** 本文是英文页面 [System time](/index.php/System_time "System time") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-26，点击[这里](https://wiki.archlinux.org/index.php?title=System+time&diff=0&oldid=442442)可以查看翻译后英文页面的改动。

一个操作系统通过如下内容确定时间：时间数值、时间标准、时区和夏令时调节(中国已经废止)。本文分别介绍各个部分的定义及如何设置他们。要维护准确的系统时间，请参考 [网络时间协议](/index.php/Network_Time_Protocol_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Network Time Protocol (简体中文)") 一文。

## Contents

*   [1 硬件时钟和系统时钟](#.E7.A1.AC.E4.BB.B6.E6.97.B6.E9.92.9F.E5.92.8C.E7.B3.BB.E7.BB.9F.E6.97.B6.E9.92.9F)
    *   [1.1 读取时间](#.E8.AF.BB.E5.8F.96.E6.97.B6.E9.97.B4)
    *   [1.2 设置时间](#.E8.AE.BE.E7.BD.AE.E6.97.B6.E9.97.B4)
*   [2 时间标准](#.E6.97.B6.E9.97.B4.E6.A0.87.E5.87.86)
    *   [2.1 Windows 系统使用 UTC](#Windows_.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8_UTC)
    *   [2.2 UTC 在Ubuntu的设置](#UTC_.E5.9C.A8Ubuntu.E7.9A.84.E8.AE.BE.E7.BD.AE)
*   [3 时区](#.E6.97.B6.E5.8C.BA)
*   [4 时钟偏移](#.E6.97.B6.E9.92.9F.E5.81.8F.E7.A7.BB)
*   [5 时钟同步](#.E6.97.B6.E9.92.9F.E5.90.8C.E6.AD.A5)
*   [6 Per-user/会话或临时设置](#Per-user.2F.E4.BC.9A.E8.AF.9D.E6.88.96.E4.B8.B4.E6.97.B6.E8.AE.BE.E7.BD.AE)
*   [7 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [7.1 时间显示的既不是UTC也不是本地时间](#.E6.97.B6.E9.97.B4.E6.98.BE.E7.A4.BA.E7.9A.84.E6.97.A2.E4.B8.8D.E6.98.AFUTC.E4.B9.9F.E4.B8.8D.E6.98.AF.E6.9C.AC.E5.9C.B0.E6.97.B6.E9.97.B4)
*   [8 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [8.1 fake-hwclock](#fake-hwclock)
*   [9 外部资源](#.E5.A4.96.E9.83.A8.E8.B5.84.E6.BA.90)

## 硬件时钟和系统时钟

系统用两个时钟保存时间：硬件时钟和系统时钟。

**硬件时钟**(即实时时钟 RTC 或 CMOS 时钟)仅能保存：年、月、日、时、分、秒这些时间数值，无法保存时间标准(UTC 或 localtime)和是否使用夏令时调节。

**系统时钟**(即软件时间) 与硬件时间分别维护，保存了：时间、时区和夏令时设置。Linux 内核保存为自 UTC 时间 1970 年1月1日经过的秒数。初始系统时钟是从硬件时间计算得来，计算时会考虑`/etc/adjtime`的设置。系统启动之后，系统时钟与硬件时钟独立运行，Linux 通过时钟中断计数维护系统时钟。

因为系统时间是按 32 为整数保存的，最大只能记到 2038 年，所以 32 位 Linux 系统将在 2038 年停止工作。

大部分操作系统的时间管理包括如下方面：

*   启动时根据硬件时钟设置系统时间
*   运行时通过时间同步联网校正时间
*   关机时根据系统时间设置硬件时间

### 读取时间

下面命令可以获得硬件时间和系统时间(硬件时钟按 localtime 显示):

```
$ timedatectl

```

### 设置时间

设置系统时间的本地时间：

```
# timedatectl set-time "yyyy-MM-dd hh:mm:ss"

```

例如:

```
# timedatectl set-time "2014-05-26 11:13:54"

```

设置时间为2014年，5月26日，11时13分54秒。

## 时间标准

时间表示有两个标准：**localtime** 和 **UTC**(**C**oordinated **U**niversal **T**ime) 。UTC 是与时区无关的全球时间标准。尽管概念上有差别，UTC 和 GMT (格林威治时间) 是一样的。localtime 标准则依赖于当前时区。

时间标准由操作系统设定，Windows 默认使用 localtime，Mac OS 默认使用 UTC 而 UNIX 系列的操作系统两者都有。使用 Linux 时，最好将硬件时钟设置为 UTC 标准，并在所有操作系统中使用。这样 Linux 系统就可以自动调整夏令时设置，而如果使用 localtime 标准那么系统时间不会根据夏令时自动调整。

通过如下命令可以检查当前设置，**systemd** 默认硬件时钟为协调世界时（UTC）。

```
$ timedatectl status | grep local

```

硬件时间可以用 `hwclock` 命令设置，将硬件时间设置为 localtime：

```
# timedatectl set-local-rtc true

```

硬件时间设置成 UTC：

```
# timedatectl set-local-rtc false

```

上述命令会自动生成`/etc/adjtime`，无需单独设置。

**Note:** 如果不存在 `/etc/adjtime`，[systemd](/index.php/Systemd "Systemd") 会假定硬件时间按 UTC 设置。

系统启动装入 rtc 驱动时可能会根据系统时钟设置硬件时钟。是否设置依赖于平台、内核版本和内核编译选项。如果进行了设置，此时会假定硬件时钟为 UTC 标准，`/sys/class/rtc/rtcN/hctosys`(N=0,1,2,..) 会设置成 1。后面 systemd 会根据`/etc/adjtime`重新设置。

如果设置成本地时间，处理夏令时有些麻烦。如果夏令时调整发生在关机时，下次启动时时间会出现问题（[更多信息](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html)）。最新的内核直接从实时时钟芯片（RTC）读取时间，不使用 `hwclock`，内核把从 RTC 读取的时间当作 UTC 处理。所以如果硬件时间是地方时，系统启动一开始识别的时间是错误的，之后很快会进行矫正。这可能导致一些问题（尤其是时间倒退时）。

### Windows 系统使用 UTC

如果同时安装了 Windows 操作系统（[默认使用地方时](http://blogs.msdn.com/b/oldnewthing/archive/2004/09/02/224672.aspx)），那么一般 RTC 会被设置为地方时。Windows 其实也能处理 UTC，需要[修改注册表](#Windows_.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8_UTC)。建议让 Windows 使用 UTC，而非让 Linux 使用地方时。Windows 使用 UTC 后，请记得禁用 Windows 的时间同步功能，以防 Windows 错误设置硬件时间。如上文所说，Linux 可以使用[NTP服务](/index.php/NTP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NTP (简体中文)")来在线同步硬件时钟。

使用 `regedit`,新建如下 DWORD 值，并将其值设为十六进制的 `1`。

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\RealTimeIsUniversal

```

也可以用管理员权限启动命令行来完成：

```
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f

```

如果以上操作不起作用，并且你使用的是 Windows 64位系统，将 `DWORD` 修改为 `QWORD`。

如果 Windows 要求根据夏令时更新时钟，可以允许。时钟仍然是 UTC，仅是显示时间会改变。

设置时间标准后需要重新设置硬件时间和系统时间。 [updated](#Set_clock)。

如果你有时间偏移问题，重新安装 [tzdata](https://www.archlinux.org/packages/?name=tzdata) 并再次设置你的时区:

```
# timedatectl set-timezone America/Los_Angeles

```

### UTC 在Ubuntu的设置

Ubuntu及其衍生发行版会在安装时检测计算机上是否存在Windows，若存在则会默认使用localtime。这是为了让Windows用户能够在不修改注册表的情况下，在Ubuntu内看到正确的时间。

要改变Ubuntu的此问题，你需要做到以下几点。打开文件:

```
/etc/default/rcS

```

并改变 UTC 标记为 **UTC=yes**.

## 时区

检查当前时区：

```
$ timedatectl status

```

显示可用时区：

```
$ timedatectl list-timezones

```

修改时区：

```
# timedatectl set-timezone <Zone>/<SubZone>

```

例如：

```
# timedatectl set-timezone Asia/Shanghai

```

此命令会创建一个`/etc/localtime`软链接，指向`/usr/share/zoneinfo/`中的时区文件，如果手动创建此链接请确保是相对链接而不是绝对链接，参阅archlinux(7).

See [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1), [localtime(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localtime.5), and [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7) for more details.

**Note:** 如果pre-systemd配置的/etc/timezone仍然存在于你的系统，你可以放心地将其删除，因为它不再使用。

## 时钟偏移

最能代表“真实时间”的是[国际原子时钟](https://en.wikipedia.org/wiki/International_Atomic_Time "wikipedia:International Atomic Time"))，所有的时钟都是有误差的。电子时钟的时间是不准的，但是一般有固定的偏移。这种于基值的差称为“time skew”或“时间偏移”。用 `hwclock` 设置硬件时间时，会计算每天偏移的秒数。偏移值是原硬件时间与新设置硬件时间的差，并且考虑上次硬件时间设置时的偏移。新的偏移值会在设置时钟时写到文件 `/etc/adjtime` 。

**注意:** 如果硬件时间值与原值的差小于 24 小时，偏移量不会重新计算，因为时间过短，无法精确设置偏移。

如果硬件时钟总是过快或过慢，可能是计算了错误的偏移值。硬件时钟设置错误或者时间标准与其他操作系统不一致导致。删除文件 `/etc/adjtime` 可以删除偏移值，然后设置正确的硬件时钟和系统时钟，并检查时间标准是不是设置正确。

**注意:** 使用 Systemd 时，要使用 `/etc/adjtime`中的 drift 值(即无法或不想使用 NTP 时); 需要每次调用 `hwclock --adjust`命令，可以通过 cron 任务实现。

提高系统时间精度的方法有：

*   [NTP](/index.php/NTP "NTP") 可以通过网络时间协议同步 Linux 系统的时间。NTP 也会修正中断频率和每秒滴答数以减少时间偏移。并且每隔 11 分钟同步一次硬件时钟。

## 时钟同步

[网络时间协议](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) 是一个通过包交换和可变延迟网络来同步计算机系统时间的协议。下列为这个协议的实现：

*   [NTP 守护进程](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")是这个协议的[参考实现](https://en.wikipedia.org/wiki/reference_implementation "wikipedia:reference implementation")，推荐用于时间服务器。它也可以调节中断频率和每秒滴答次数以减少系统时钟误差，使得硬件时钟每隔11秒重新同步一次。
*   **sntp** 是 [ntp](https://www.archlinux.org/packages/?name=ntp) 包里附带的一个 [SNTP](https://en.wikipedia.org/wiki/Network_Time_Protocol#SNTP "wikipedia:Network Time Protocol") 客户端。它取代了 *ntpdate* ，并被推荐用于非服务器环境。
*   [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd") 是一个简单的 [SNTP](https://en.wikipedia.org/wiki/Network_Time_Protocol#SNTP "wikipedia:Network Time Protocol") 守护进程。它只实现了客户端，专用于从远程服务器查询时间，更适用于绝大部分安装的情形。
*   [OpenNTPD](/index.php/OpenNTPD "OpenNTPD") 是 OpenBSD 项目的一部分，同时实现了客户端和服务器。
*   [Chrony](/index.php/Chrony "Chrony") 是一个客户端和服务器，更适合漫游，是为不能始终保持在线的系统而特别设计。
*   [ntpclient](https://aur.archlinux.org/packages/ntpclient/) 是简单的命令行 NTP 客户端

## Per-user/会话或临时设置

For some use cases it may be useful to change the time settings without touching the global system values. For example to test applications relying on the time during development or adjusting the system time zone when logging into a server remotely from another zone.

To make an application "see" a different date/time than the system one, you can use the *faketime* (from [libfaketime](https://www.archlinux.org/packages/?name=libfaketime)) or the [datefudge](https://www.archlinux.org/packages/?name=datefudge) utilities.

If instead you want an application to "see" a different time zone than the system one, set the `TZ` [environment variable](/index.php/Environment_variable "Environment variable"), for example:

 `$ date && export TZ="/usr/share/zoneinfo/Pacific/Fiji" && date` 
```
Sa 24\. Mai 12:38:26 CEST 2014
Sa 24\. Mai 22:38:26 FJT 2014
```

This is different than just setting the time, as for example it allows to test the behaviour of a program with positive or negative UTC offset values, or the effects of DST changes when developing on systems in a non-DST time zone.

Another use case is having different time zones set for different users of the same system: this can be accomplished by setting the `TZ` variable in the shell's configuration file, see [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables") and [Autostarting#Shells](/index.php/Autostarting#Shells "Autostarting").

## 故障排除

### 时间显示的既不是UTC也不是本地时间

This might be caused by a number of reasons. For example, if your hardware clock is running on local time, but `timedatectl` is set to assume it is in UTC, the result would be that your timezone's offset to UTC effectively gets applied twice, resulting in wrong values for your local time and UTC.

To force your clock to the correct time, and to also write the correct UTC to your hardware clock, follow these steps:

*   Setup [ntpd](/index.php/Ntpd "Ntpd") (enabling it as a service is not necessary).
*   Set your [time zone](#Time_zone) correctly.
*   Run `ntpd -qg` to manually synchronize your clock with the network, ignoring large deviations between local UTC and network UTC.
*   Run `hwclock --systohc` to write the current software UTC time to the hardware clock.

## 提示和技巧

### fake-hwclock

[alarm-fake-hwclock](https://github.com/xanmanning/alarm-fake-hwclock) designed especially for system without battery backed up RTC, it includes a systemd service which on shutdown saves the current time and on startup restores the saved time, thus avoiding strange time travel errors.

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") [fake-hwclock-git](https://aur.archlinux.org/packages/fake-hwclock-git/), [start and enable](/index.php/Systemd#Using_units "Systemd") the service `fake-hwclock.service`.

## 外部资源

*   [Linux Tips - Linux, Clocks, and Time](http://sunnyan.tistory.com/entry/Linux-Clocks-and-Time)
*   [Sources for Time Zone and Daylight Saving Time Data](http://www.twinsun.com/tz/tz-link.htm) for [tzdata](https://www.archlinux.org/packages/?name=tzdata)
*   [Time Scales](http://www.ucolick.org/~sla/leapsecs/timescales.html)
*   [Wikipedia:Time](https://en.wikipedia.org/wiki/Time "wikipedia:Time")