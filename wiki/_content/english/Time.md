In an operating system, the time (clock) is determined by four parts: time value, time standard, time zone, and Daylight Saving Time (DST) if applicable. This article explains what they are and how to read/set them.

## Contents

*   [1 Hardware clock and system clock](#Hardware_clock_and_system_clock)
    *   [1.1 Read clock](#Read_clock)
    *   [1.2 Set clock](#Set_clock)
*   [2 Time standard](#Time_standard)
    *   [2.1 UTC in Windows](#UTC_in_Windows)
    *   [2.2 UTC in Ubuntu](#UTC_in_Ubuntu)
*   [3 Time zone](#Time_zone)
*   [4 Time skew](#Time_skew)
*   [5 Time synchronization](#Time_synchronization)
*   [6 Per-user/session or temporary settings](#Per-user.2Fsession_or_temporary_settings)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Clock shows a value that is neither UTC nor local time](#Clock_shows_a_value_that_is_neither_UTC_nor_local_time)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 fake-hwclock](#fake-hwclock)
*   [9 See also](#See_also)

## Hardware clock and system clock

A computer has two clocks that need to be considered: the "Hardware clock" and the "System/software clock".

**Hardware clock** (a.k.a. the Real Time Clock (RTC) or CMOS clock) stores the values of: Year, Month, Day, Hour, Minute, and the Seconds. It does not have the ability to store the time standard (localtime or UTC), nor whether DST is used.

**System clock** (a.k.a. the software clock) keeps track of: time, time zone, and DST if applicable. It is calculated by the Linux kernel as the number of seconds since midnight January 1st 1970, UTC. The initial value of the system clock is calculated from the hardware clock, dependent on the contents of `/etc/adjtime`. After boot-up has completed, the system clock runs independently of the hardware clock. The Linux kernel keeps track of the system clock by counting timer interrupts.

Standard behavior of most operating systems is:

*   Set the system clock from the hardware clock on boot.
*   Keep accurate time of the system clock with an NTP daemon, see [#Time synchronization](#Time_synchronization).
*   Set the hardware clock from the system clock on shutdown.

### Read clock

To check the current system clock time (presented both in local time and UTC) as well as the RTC:

```
$ timedatectl

```

### Set clock

To set the local time of the system clock directly:

```
# timedatectl set-time "yyyy-MM-dd hh:mm:ss"

```

For example:

```
# timedatectl set-time "2014-05-26 11:13:54"

```

sets the time to May 26th, year 2014, 11:13 and 54 seconds.

## Time standard

There are two time standards: **localtime** and [Coordinated Universal Time](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") (**UTC**). The localtime standard is dependent on the current *time zone*, while UTC is the *global* time standard and is independent of time zone values. Though conceptually different, UTC is also known as GMT (Greenwich Mean Time).

The standard used by hardware clock (CMOS clock, the time that appears in BIOS) is defined by the operating system. By default, Windows uses localtime, macOS uses UTC, and UNIX-like operating systems vary. An OS that uses the UTC standard, generally, will consider CMOS (hardware clock) time a UTC time (GMT, Greenwich time) and make an adjustment to it while setting the System time on boot according to your time zone.

**Note:** If `/etc/adjtime` is not present, [systemd](/index.php/Systemd "Systemd") assumes the hardware clock is set to UTC.

If you have multiple operating systems installed in the same machine, they will all derive the current time from the same hardware clock: for this reason you must make sure that all of them see the hardware clock as providing time in the same chosen standard, or some of them will perform the time zone adjustement for the system clock, while others will not. In particular, it is recommended to set the hardware clock to UTC, in order to avoid conflicts between the installed operating systems. For example, if the hardware clock was set to *localtime*, more than one operating system may adjust it after a [DST](https://en.wikipedia.org/wiki/Daylight_saving_time "wikipedia:Daylight saving time") change, thus resulting in an overcorrection; more problems may arise when travelling between different time zones and using one of the operating systems to reset the system/hardware clock.

You can set the hardware clock time standard through the command line. You can check what you have set your Arch Linux install to use by:

```
$ timedatectl | grep local

```

The hardware clock can be queried and set with the `timedatectl` command. To change the hardware clock time standard to localtime, use:

```
# timedatectl set-local-rtc 1

```

If you want to revert to the hardware clock being in UTC, do:

```
# timedatectl set-local-rtc 0

```

These will generate `/etc/adjtime` automatically and update the RTC accordingly; no further configuration is required.

During kernel startup, at the point when the RTC driver is loaded, the system clock may be set from the hardware clock. Whether this occurs depends on the hardware platform, the version of the kernel and kernel build options. If this does occur, at this point in the boot sequence, the hardware clock time is assumed to be UTC and the value of `/sys/class/rtc/rtcN/hctosys` (N=0,1,2,..) will be set to 1\.

Later, the system clock is set again from the hardware clock by systemd, dependent on values in `/etc/adjtime`. Hence, having the hardware clock using localtime may cause some unexpected behavior during the boot sequence; e.g system time going backwards, which is always a bad idea ([there is a lot more to it](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html)). To avoid it systemd [will only synchronize back](https://mailman.archlinux.org/pipermail/arch-dev-public/2014-August/026577.html), if the hardware clock is set to UTC and keep the kernel uninformed about the local timezone. As a consequence timestamps on a FAT filesystem touched by the Linux system will be in UTC.

**Note:** The use of `timedatectl` requires an active dbus. Therefore, it may not be possible to use this command under a chroot (such as during installation). In these cases, you can revert back to the hwclock command.

### UTC in Windows

**Warning:** This method uses functionality that is buggy in old Windows versions (pre-7) and Microsoft recommends not to use it. See [[1]](https://support.microsoft.com/en-us/kb/2687252) for details. Another bug exists on Windows before Vista SP2 that resets the clock to *localtime* after resuming from the suspend/hibernation state. For *even older* versions of Windows, you might want to read [http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html](http://www.cl.cam.ac.uk/~mgk25/mswish/ut-rtc.html) - the functionality was not even documented nor officially supported then. For these operating systems, it is recommended to use *localtime*. If you are using newer versions of Windows, you may safely disregard this warning.

One reason users often set the RTC in localtime is to [dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows") ([which uses localtime](http://blogs.msdn.com/b/oldnewthing/archive/2004/09/02/224672.aspx)). However, Windows is able to deal with the RTC being in UTC with a simple registry fix. It is recommended to configure Windows to use UTC, rather than Linux to use localtime.

Using `regedit`, add a `DWORD` value with hexadecimal value `1` to the registry:

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\RealTimeIsUniversal

```

You can do this from an Administrator Command Prompt running:

```
reg add "HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation" /v RealTimeIsUniversal /d 1 /t REG_DWORD /f

```

Alternatively, create a `*.reg` file (on the desktop) with the following content and double-click it to import it into registry:

```
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
     "RealTimeIsUniversal"=dword:00000001

```

If the above appears to have no effect, and a 64-bit variant of Windows is being used, using a `QWORD` value instead of a `DWORD` value may resolve the issue.

Should Windows ask to update the clock due to DST changes, let it. It will leave the clock in UTC as expected, only correcting the displayed time.

The hardware clock and system clock time may need to be [updated](#Set_clock) after setting this value.

If you are having issues with the offset of the time, try reinstalling [tzdata](https://www.archlinux.org/packages/?name=tzdata) and then setting your time zone again:

```
# timedatectl set-timezone America/Los_Angeles

```

### UTC in Ubuntu

Ubuntu and its derivatives have the hardware clock set to be interpreted as in "localtime" if Windows was detected on any disk during Ubuntu installation. This is apparently done deliberately to allow new Linux users to try out Ubuntu on their Windows computers without editing the registry.

To change this behaviour in Ubuntu you need to do the following. Open the file:

```
/etc/default/rcS

```

and change UTC flag to **UTC=yes**.

## Time zone

To check the current zone defined for the system:

```
$ timedatectl

```

To list available zones:

```
$ timedatectl list-timezones

```

To change your time zone:

```
# timedatectl set-timezone *Zone*/*SubZone*

```

Example:

```
# timedatectl set-timezone Canada/Eastern

```

This will create an `/etc/localtime` symlink that points to a zoneinfo file under `/usr/share/zoneinfo/`. In case you choose to create the link manually, keep in mind that it must be a symbolic link, as specified in `archlinux(7)`:

```
# ln -sf /usr/share/zoneinfo/*Zone*/*SubZone* /etc/localtime

```

**Tip:** The time zone can also be selected interactively with *tzselect*.

See [timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html), [localtime(5)](http://man7.org/linux/man-pages/man5/localtime.5.html) and archlinux(7) for details.

**Note:** If the pre-systemd configuration file `/etc/timezone` still exists in your system, you can remove it safely, since it is no longer used.

## Time skew

Every clock has a value that differs from *real time* (the best representation of which being [International Atomic Time](https://en.wikipedia.org/wiki/International_Atomic_Time "wikipedia:International Atomic Time")); no clock is perfect. A quartz-based electronic clock keeps imperfect time, but maintains a consistent inaccuracy. This base 'inaccuracy' is known as 'time skew' or 'time drift'.

When the hardware clock is set with `hwclock`, a new drift value is calculated in seconds per day. The drift value is calculated by using the difference between the new value set and the hardware clock value just before the set, taking into account the value of the previous drift value and the last time the hardware clock was set. The new drift value and the time when the clock was set is written to the file `/etc/adjtime` overwriting the previous values. The hardware clock can therefore be adjusted for drift when the command `hwclock --adjust` is run; this also occurs on shutdown but only if the `hwclock` daemon is enabled (hence for systems using systemd, this does not happen).

**Note:** If the hwclock has been set again less than 24 hours after a previous set, the drift is not recalculated as `hwclock` considers the elapsed time period too short to accurately calculate the drift.

If the hardware clock keeps losing or gaining time in large increments, it is possible that an invalid drift has been recorded (but only applicable, if the hwclock daemon is running). This can happen if you have set the hardware clock time incorrectly or your [time standard](#Time_standard) is not synchronized with a Windows or macOS install. The drift value can be removed by removing the file `/etc/adjtime`, then set the correct hardware clock and system clock time, and check if your time standard is correct.

**Note:** For those using systemd, but wish to make use of the drift value stored in `/etc/adjtime` (i.e. perhaps cannot or do not want to use NTP); they need to call `hwclock --adjust` on a regular basis, perhaps by creating a cron job.

The software clock is very accurate but like most clocks is not perfectly accurate and will drift as well. Though rarely, the system clock can lose accuracy if the kernel skips interrupts. There are some tools to improve software clock accuracy:

*   See [#Time synchronization](#Time_synchronization).

## Time synchronization

The [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) is a protocol for synchronizing the clocks of computer systems over packet-switched, variable-latency data networks. The following are implementations of such protocol:

*   **[Network Time Protocol daemon](/index.php/Network_Time_Protocol_daemon "Network Time Protocol daemon")** — The [reference implementation](https://en.wikipedia.org/wiki/reference_implementation "wikipedia:reference implementation") of the protocol, especially recommended to be used on time servers. It can also adjust the interrupt frequency and the number of ticks per second to decrease system clock drift, and will cause the hardware clock to be re-synchronised every 11 minutes.

	[http://www.ntp.org/](http://www.ntp.org/) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **sntp** — An [SNTP](https://en.wikipedia.org/wiki/Network_Time_Protocol#SNTP "wikipedia:Network Time Protocol") client that comes with NTPd. It supersedes *ntpdate* and is recommended in non-server environments.

	[http://www.ntp.org/](http://www.ntp.org/) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **[systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")** — A simple [SNTP](https://en.wikipedia.org/wiki/Network_Time_Protocol#SNTP "wikipedia:Network Time Protocol") daemon that only implements a client side, focusing only on querying time from one remote server. It should be more than appropriate for most installations.

	[https://www.freedesktop.org/wiki/Software/systemd/](https://www.freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** — Part of the OpenBSD project and implements both a client and a server.

	[http://www.openntpd.org/](http://www.openntpd.org/) || [openntpd](https://www.archlinux.org/packages/?name=openntpd)

*   **[Chrony](/index.php/Chrony "Chrony")** — A client and server that is roaming friendly and designed specifically for systems that are not online all the time.

	[http://chrony.tuxfamily.org/](http://chrony.tuxfamily.org/) || [chrony](https://www.archlinux.org/packages/?name=chrony)

*   **ntpclient** — A simple command-line NTP client.

	[http://doolittle.icarus.com/ntpclient/](http://doolittle.icarus.com/ntpclient/) || [ntpclient](https://aur.archlinux.org/packages/ntpclient/)

## Per-user/session or temporary settings

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
*   [Sources for Time Zone and Daylight Saving Time Data](http://www.twinsun.com/tz/tz-link.htm) for [tzdata](https://www.archlinux.org/packages/?name=tzdata)
*   [Time Scales](http://www.ucolick.org/~sla/leapsecs/timescales.html)
*   [Wikipedia:Time](https://en.wikipedia.org/wiki/Time "wikipedia:Time")