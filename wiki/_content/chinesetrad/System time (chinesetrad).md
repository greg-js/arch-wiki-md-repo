Related articles

*   [Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")
*   [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")
*   [Chrony](/index.php/Chrony "Chrony")
*   [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")

作業系統中，時間（時鐘）由以下部分決定：時間值（本地時間、協調世界時或其他）、時區和夏令日光節約時間（daylight saving time, DST）。本文將介紹了這些東西是什麼以及如何進行設置，在系統上的時鐘分為兩個：硬體時鐘（hardware clock）和系統時鐘（system clock），本文也會詳細介紹。

大多數作業系統的標準行為是：

*   啟動時，使用硬體時鐘（hardware clock）來設定系統時鐘（system clock）。
*   保持系統時鐘的準確性，詳細內容參閱 [#時間同步](#時間同步)。
*   關機時，使用系統時鐘（system clock）來設定硬體時鐘（hardware clock）。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 硬體時鐘（Hardware Clock）](#硬體時鐘（Hardware_Clock）)
    *   [1.1 Read hardware clock](#Read_hardware_clock)
    *   [1.2 Set hardware clock from system clock](#Set_hardware_clock_from_system_clock)
*   [2 系統時鐘（System clock）](#系統時鐘（System_clock）)
    *   [2.1 Read clock](#Read_clock)
    *   [2.2 Set system clock](#Set_system_clock)
*   [3 時間標準（Time Standard）](#時間標準（Time_Standard）)
    *   [3.1 UTC in Windows](#UTC_in_Windows)
        *   [3.1.1 Historical notes](#Historical_notes)
    *   [3.2 UTC in Ubuntu](#UTC_in_Ubuntu)
*   [4 Time zone](#Time_zone)
    *   [4.1 Setting based on geolocation](#Setting_based_on_geolocation)
        *   [4.1.1 Update timezone every time NetworkManager connects to a network](#Update_timezone_every_time_NetworkManager_connects_to_a_network)
*   [5 Time skew](#Time_skew)
*   [6 Time synchronization](#Time_synchronization)
*   [7 Per-user/session or temporary settings](#Per-user/session_or_temporary_settings)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Clock shows a value that is neither UTC nor local time](#Clock_shows_a_value_that_is_neither_UTC_nor_local_time)
*   [9 Tips and tricks](#Tips_and_tricks)
    *   [9.1 fake-hwclock](#fake-hwclock)
*   [10 See also](#See_also)

## 硬體時鐘（Hardware Clock）

**硬體時鐘（hardware clock）** 又稱為實時時鐘（Real-time clock, RTC）或 CMOS 時鐘（CMOS clock），存儲的時間值包含了：年、月、日、時、分、秒。從 2016 年之後，才開始將時區資訊儲存於 [UEFI](/index.php/UEFI "UEFI") 韌體，並且採用夏令日光節約時間（daylight saving time, DST）。

### Read hardware clock

```
# hwclock --show

```

### Set hardware clock from system clock

The following sets the hardware clock from the system clock. Additionally it updates `/etc/adjtime` or creates it if not present. See [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) section "The Adjtime File" for more information on this file as well as the [#Time skew](#Time_skew) section.

```
# hwclock --systohc

```

## 系統時鐘（System clock）

The **system clock** (a.k.a. the software clock) keeps track of: time, time zone, and DST if applicable. It is calculated by the Linux kernel as the number of seconds since midnight January 1st 1970, UTC. The initial value of the system clock is calculated from the hardware clock, dependent on the contents of `/etc/adjtime`. After boot-up has completed, the system clock runs independently of the hardware clock. The Linux kernel keeps track of the system clock by counting timer interrupts.

### Read clock

To check the current system clock time (presented both in local time and UTC) as well as the RTC (hardware clock):

```
$ timedatectl

```

### Set system clock

To set the local time of the system clock directly:

```
# timedatectl set-time "yyyy-MM-dd hh:mm:ss"

```

For example:

```
# timedatectl set-time "2014-05-26 11:13:54"

```

sets the time to May 26th, year 2014, 11:13 and 54 seconds.

## 時間標準（Time Standard）

There are two time standards: **localtime** and [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") (**UTC**). The localtime standard is dependent on the current *time zone*, while UTC is the *global* time standard and is independent of time zone values. Though conceptually different, UTC is also known as GMT (Greenwich Mean Time).

The standard used by the hardware clock (CMOS clock, the BIOS time) is set by the operating system. By default, *Windows* uses localtime, *macOS* uses UTC, and *UNIX-like* systems vary. An OS that uses the UTC standard will generally consider the hardware clock as UTC and make an adjustment to it to set the OS time at boot according to the time zone.

If multiple operating systems are installed on a machine, they will all derive the current time from the same hardware clock: it is recommended to adopt a unique standard for the hardware clock to avoid conflicts across systems and set it to UTC. Otherwise, if the hardware clock is set to *localtime*, more than one operating system may adjust it after a [DST](https://en.wikipedia.org/wiki/Daylight_saving_time "wikipedia:Daylight saving time") change for example, thus resulting in an over-correction; problems may also arise when traveling between different time zones and using one of the operating systems to reset the system/hardware clock.

The hardware clock can be queried and set with the `timedatectl` command. You can see the current hardware clock time standard of the Arch system using:

 `$ timedatectl | grep local`  `RTC in local TZ: no` 

To change the hardware clock time standard to localtime, use:

```
# timedatectl set-local-rtc **1**

```

To revert to the hardware clock being in UTC, type:

```
# timedatectl set-local-rtc **0**

```

These generate `/etc/adjtime` automatically and update the RTC accordingly; no further configuration is required.

During kernel startup, at the point when the RTC driver is loaded, the system clock may be set from the hardware clock. Whether this occurs depends on the hardware platform, the version of the kernel and kernel build options. If this does occur, at this point in the boot sequence, the hardware clock time is assumed to be UTC and the value of `/sys/class/rtc/rtc*N*/hctosys` (N=0,1,2,..) will be set to 1\.

Later, the system clock is set again from the hardware clock by systemd, dependent on values in `/etc/adjtime`. Hence, having the hardware clock using localtime may cause some unexpected behavior during the boot sequence; e.g system time going backwards, which is always a bad idea ([there is a lot more to it](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html)). To avoid it systemd [will only synchronize back](https://mailman.archlinux.org/pipermail/arch-dev-public/2014-August/026577.html), if the hardware clock is set to UTC and keep the kernel uninformed about the local timezone. As a consequence timestamps on a FAT filesystem touched by the Linux system will be in UTC.

**Note:**

*   The use of `timedatectl` requires an active dbus. Therefore, it may not be possible to use this command under a chroot (such as during installation). In these cases, you can revert back to the hwclock command.
*   If `/etc/adjtime` is not present, [systemd](/index.php/Systemd "Systemd") assumes the hardware clock is set to UTC.

### UTC in Windows

To [dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") it is recommended to configure Windows to use UTC, rather than Linux to use localtime. (Windows by default uses localtime [[1]](https://devblogs.microsoft.com/oldnewthing/20040902-00/?p=37983).)

It can be done by a simple registry fix: Open `regedit` and add a `DWORD` value for *32-bit* Windows, or `QWORD` for *64-bit* one, with hexadecimal value `1` to the registry:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\RealTimeIsUniversal

```

You can do this from an Administrator Command Prompt running:

```
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_QWORD /f

```

(Replace `QWORD` with `DWORD` for 32-bit Windows.)

Alternatively, create a `*.reg` file (on the desktop) with the following content and double-click it to import it into registry:

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
     "RealTimeIsUniversal"=qword:00000001

```

(Replace `qword` with `dword` for 32-bit Windows.)

Should Windows ask to update the clock due to DST changes, let it. It will leave the clock in UTC as expected, only correcting the displayed time.

The [#Hardware clock](#Hardware_clock) and [#System clock](#System_clock) time may need to be updated after setting this value.

If you are having issues with the offset of the time, try reinstalling [tzdata](https://www.archlinux.org/packages/?name=tzdata) and then setting your time zone again:

```
# timedatectl set-timezone America/Los_Angeles

```

#### Historical notes

For *really old* Windows, the above method fails, due to Windows bugs. More precisely,

*   Before Vista SP2, there is a bug that resets the clock to *localtime* after resuming from the suspend/hibernation state.
*   For XP and older, there's a bug related to the daylight saving time. See [[2]](https://support.microsoft.com/en-us/kb/2687252) for details.
*   For *even older* versions of Windows, you might want to read [http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html) - the functionality was not even documented nor officially supported then.

For these operating systems, it is recommended to use *localtime*.

### UTC in Ubuntu

Ubuntu and its derivatives have the hardware clock set to be interpreted as in "localtime" if Windows was detected on any disk during Ubuntu installation. This is apparently done deliberately to allow new Linux users to try out Ubuntu on their Windows computers without editing the registry.

For changing this behavior, see above.

## Time zone

To check the current zone defined for the system:

```
$ timedatectl status

```

To list available zones:

```
$ timedatectl list-timezones

```

To set your time zone:

```
# timedatectl set-timezone *Zone*/*SubZone*

```

Example:

```
# timedatectl set-timezone Canada/Eastern

```

This will create an `/etc/localtime` symlink that points to a zoneinfo file under `/usr/share/zoneinfo/`. In case you choose to create the link manually (for example during [chroot](/index.php/Chroot "Chroot") where `timedatectl` won't work), keep in mind that it must be a symbolic link, as specified in [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7):

```
# ln -sf /usr/share/zoneinfo/*Zone*/*SubZone* /etc/localtime

```

**Tip:** The time zone can also be selected interactively with *tzselect*.

See [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1), [localtime(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localtime.5) and [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7) for details.

### Setting based on geolocation

**Note:** Some desktop environments have support for automatic time zone selection (e.g. see [GNOME#Date & time](/index.php/GNOME#Date_&_time "GNOME")).

To set the timezone automatically based on the IP address location, one can use a geolocation API to retrieve the timezone, for example `curl https://ipapi.co/timezone`, and pass the output to `timedatectl set-timezone` for automatic setting. Some geo-IP APIs that provide free or partly free services are listed below:

*   [https://freegeoip.app](https://freegeoip.app)
*   [https://ipapi.co/](https://ipapi.co/)
*   [http://ip-api.com/](http://ip-api.com/)
*   [https://ipstack.com/](https://ipstack.com/)
*   [https://timezoneapi.io/](https://timezoneapi.io/)
*   [https://ipdata.co](https://ipdata.co)

#### Update timezone every time NetworkManager connects to a network

Create a [NetworkManager dispatcher script](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager"):

 `/etc/NetworkManager/dispatcher.d/09-timezone` 
```
#!/bin/sh
case "$2" in
    up)
        timedatectl set-timezone "$(curl --fail https://ipapi.co/timezone)"
    ;;
esac

```

Alternatively, the tool [tzupdate](https://aur.archlinux.org/packages/tzupdate/) automatically sets the timezone based on the geolocation of the IP address. This [comparison of the most popular IP geolocation apis](https://medium.com/@ipdata_co/what-is-the-best-commercial-ip-geolocation-api-d8195cda7027) may be helpful in deciding which API to use in production.

## Time skew

Every clock has a value that differs from *real time* (the best representation of which being [International Atomic Time](https://en.wikipedia.org/wiki/International_Atomic_Time "wikipedia:International Atomic Time")); no clock is perfect. A quartz-based electronic clock keeps imperfect time, but maintains a consistent inaccuracy. This base 'inaccuracy' is known as 'time skew' or 'time drift'.

When the hardware clock is set with `hwclock`, a new drift value is calculated in seconds per day. The drift value is calculated by using the difference between the new value set and the hardware clock value just before the set, taking into account the value of the previous drift value and the last time the hardware clock was set. The new drift value and the time when the clock was set is written to the file `/etc/adjtime` overwriting the previous values. The hardware clock can therefore be adjusted for drift when the command `hwclock --adjust` is run; this also occurs on shutdown but only if the `hwclock` daemon is enabled, hence for Arch systems which use systemd, this does not happen.

**Note:** If the hwclock has been set again less than 24 hours after a previous set, the drift is not recalculated as `hwclock` considers the elapsed time period too short to accurately calculate the drift.

If the hardware clock keeps losing or gaining time in large increments, it is possible that an invalid drift has been recorded (but only applicable, if the hwclock daemon is running). This can happen if you have set the hardware clock time incorrectly or your [time standard](#Time_standard) is not synchronized with a Windows or macOS install. The drift value can be removed by first removing the file `/etc/adjtime`, then setting the correct hardware clock and system clock time. You should then check if your time standard is correct.

**Note:** If you wish to make use of the drift value stored in `/etc/adjtime` even when using systemd, (e.g. you cannot or do not want to use NTP), you must call `hwclock --adjust` on a regular basis, perhaps by creating a [cron](/index.php/Cron "Cron") job.

The software clock is very accurate but like most clocks is not perfectly accurate and will drift as well. Though rarely, the system clock can lose accuracy if the kernel skips interrupts. There are some tools to improve software clock accuracy:

*   See [#Time synchronization](#Time_synchronization).

## Time synchronization

The [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) is a protocol for synchronizing the clocks of computer systems over packet-switched, variable-latency data networks. The following are implementations of NTP available for Arch Linux:

*   **[Chrony](/index.php/Chrony "Chrony")** — A client and server that is roaming friendly and designed specifically for systems that are not online all the time.

	[https://chrony.tuxfamily.org/](https://chrony.tuxfamily.org/) || [chrony](https://www.archlinux.org/packages/?name=chrony)

*   **[ConnMan](/index.php/ConnMan "ConnMan")** — A lightweight network manager with NTP support.

	[https://01.org/connman](https://01.org/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **[Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")** — The [reference implementation](https://en.wikipedia.org/wiki/reference_implementation "wikipedia:reference implementation") of the protocol, especially recommended to be used on time servers. It can also adjust the interrupt frequency and the number of ticks per second to decrease system clock drift, and will cause the hardware clock to be re-synchronised every 11 minutes.

	[http://www.ntp.org/](http://www.ntp.org/) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **ntpclient** — A simple command-line NTP client.

	[http://doolittle.icarus.com/ntpclient/](http://doolittle.icarus.com/ntpclient/) || [ntpclient](https://aur.archlinux.org/packages/ntpclient/)

*   **[NTPSec](/index.php/NTPSec "NTPSec")** — A fork of NTPd, focused on security.

	[https://ntpsec.org/](https://ntpsec.org/) || [ntpsec](https://aur.archlinux.org/packages/ntpsec/)

*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** — Part of the OpenBSD project and implements both a client and a server.

	[http://www.openntpd.org/](http://www.openntpd.org/) || [openntpd](https://www.archlinux.org/packages/?name=openntpd)

*   **sntp** — An [SNTP](https://en.wikipedia.org/wiki/Network_Time_Protocol#SNTP "wikipedia:Network Time Protocol") client that comes with NTPd. It supersedes *ntpdate* and is recommended in non-server environments.

	[http://www.ntp.org/](http://www.ntp.org/) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **[systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")** — A simple [SNTP](https://en.wikipedia.org/wiki/Network_Time_Protocol#SNTP "wikipedia:Network Time Protocol") daemon that only implements a client side, focusing only on querying time from one remote server. It should be more than appropriate for most installations.

	[https://www.freedesktop.org/wiki/Software/systemd/](https://www.freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

## Per-user/session or temporary settings

For some use cases it may be useful to change the time settings without touching the global system values. For example to test applications relying on the time during development or adjusting the system time zone when logging into a server remotely from another zone.

To make an application "see" a different date/time than the system one, you can use the *faketime* (from [libfaketime](https://www.archlinux.org/packages/?name=libfaketime)) or the [datefudge](https://www.archlinux.org/packages/?name=datefudge) utilities.

If instead you want an application to "see" a different time zone than the system one, set the `TZ` [environment variable](/index.php/Environment_variable "Environment variable"), for example:

 `$ date && export TZ=":/usr/share/zoneinfo/Pacific/Fiji" && date` 
```
Tue Nov  1 14:34:51 CET 2016
Wed Nov  2 01:34:51 FJT 2016
```

This is different than just setting the time, as for example it allows to test the behavior of a program with positive or negative UTC offset values, or the effects of DST changes when developing on systems in a non-DST time zone.

Another use case is having different time zones set for different users of the same system: this can be accomplished by setting the `TZ` variable in the shell's configuration file, see [Environment variables#Defining variables](/index.php/Environment_variables#Defining_variables "Environment variables").

## Troubleshooting

### Clock shows a value that is neither UTC nor local time

This might be caused by a number of reasons. For example, if your hardware clock is running on local time, but `timedatectl` is set to assume it is in UTC, the result would be that your timezone's offset to UTC effectively gets applied twice, resulting in wrong values for your local time and UTC.

To force your clock to the correct time, and to also write the correct UTC to your hardware clock, follow these steps:

*   Setup [ntpd](/index.php/Ntpd "Ntpd") (enabling it as a service is not necessary).
*   Set your [time zone](#Time_zone) correctly.
*   Run `ntpd -qg` to manually synchronize your clock with the network, ignoring large deviations between local UTC and network UTC.
*   Run `hwclock --systohc` to write the current software UTC time to the hardware clock.

## Tips and tricks

### fake-hwclock

[alarm-fake-hwclock](https://github.com/xanmanning/alarm-fake-hwclock) designed especially for system without battery backed up RTC, it includes a systemd service which on shutdown saves the current time and on startup restores the saved time, thus avoiding strange time travel errors.

[Install](/index.php/Arch_User_Repository#Installing_packages "Arch User Repository") [fake-hwclock-git](https://aur.archlinux.org/packages/fake-hwclock-git/), [start and enable](/index.php/Systemd#Using_units "Systemd") the service `fake-hwclock.service`.

## See also

*   [Linux Tips - Linux, Clocks, and Time](http://sunnyan.tistory.com/entry/Linux-Clocks-and-Time)
*   [An introduction to timekeeping in Linux VMs](https://opensource.com/article/17/6/timekeeping-linux-vms)
*   [Sources for Time Zone and Daylight Saving Time Data](https://data.iana.org/time-zones/tz-link.html) for [tzdata](https://www.archlinux.org/packages/?name=tzdata)
*   [Time Scales](https://www.ucolick.org/~sla/leapsecs/timescales.html)
*   [Gentoo: System time](https://wiki.gentoo.org/wiki/System_time "gentoo:System time")
*   [Wikipedia:Time](https://en.wikipedia.org/wiki/Time "wikipedia:Time")