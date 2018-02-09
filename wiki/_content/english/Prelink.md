**Warning:** Using prelink may corrupt system libraries, resulting in an unbootable system: [FS#54820](https://bugs.archlinux.org/task/54820). Performance benefits are neglible. [[2]](https://pagure.io/fesco/issue/1183) [[3]](http://lwn.net/Articles/341244/)

Most programs require libraries to function. Libraries can be integrated into a program once, by a linker, when it is compiled (static linking) or they can be integrated when the program is run by a loader, (dynamic linking). Dynamic linking has advantages in code size and management, but every time a program is run, the loader needs to find the relevant libraries. Because the libraries can move around in memory, this causes a performance penalty, and the more libraries that need to be resolved, the greater the penalty. [Prelink](https://en.wikipedia.org/wiki/Prelink "w:Prelink") reduces this penalty by using the system's dynamic linker to reversibly perform this linking in advance ("prelinking" the executable file) by relocating. Afterward, the program only needs to spend time finding the relevant libraries on being run if, for some reason (perhaps an upgrade), the libraries have changed since being prelinked.

## Contents

*   [1 Installing](#Installing)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
    *   [3.1 Prelinking](#Prelinking)
    *   [3.2 Exclude list](#Exclude_list)
    *   [3.3 Removing prelink](#Removing_prelink)
*   [4 Daily cron job](#Daily_cron_job)
*   [5 KDE](#KDE)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 segfault, kernel panic](#segfault.2C_kernel_panic)
*   [7 See also](#See_also)

## Installing

[Install](/index.php/Install "Install") the [prelink](https://aur.archlinux.org/packages/prelink/) package.

## Configuration

All settings are in `/etc/prelink.conf`.

**Note:** Some proprietary binaries will crash with prelink (such as Flash, Nvidia proprietary driver). You can add these to the exclude list in `/etc/prelink.conf`.

## Usage

### Prelinking

The following command prelinks all the binaries in the directories given by `/etc/prelink.conf`:

```
# prelink -amR

```

**Warning:** It has been observed that if you are low on disk space and you prelink your entire system then there is a possibility that your binaries may be truncated, the result being a broken install. Use the file or readelf command to check the state of a binary file. Alternatively, check the amount of free space on your harddrive ahead of time with df -h.

### Exclude list

Taken from the [discussion page](/index.php/Talk:Prelink#Exclude_list "Talk:Prelink"):

 `/etc/prelink.conf` 
```
# Flash Player Plugin
-b /usr/lib/mozilla/plugins/libflashplayer.so

# NVIDIA
-b /usr/lib/libGL.so*
-b /usr/lib32/libGL.so*
-b //usr/lib/libOpenCL.so*
-b //usr/lib32/libOpenCL.so*
-b /usr/lib32/vdpau/
-b /usr/lib/vdpau/
-b /usr/lib/xorg/modules/drivers/nvidia_drv.so
-b /usr/lib/xorg/modules/extensions/libglx.so*
-b /usr/lib/libnvidia-*
-b /usr/lib32/libnvidia-*

# Catalyst
-b /usr/lib/libati*
-b /usr/lib/fglrx*
-b /usr/lib/libAMDXvBA*
-b /usr/lib/libGL.so*
-b /usr/lib/libfglrx*
-b /usr/lib/xorg/modules/dri/fglrx_dri.so
-b /usr/lib/xorg/modules/drivers/fglrx_drv.so
-b /usr/lib/xorg/modules/extensions/fglrx/
-b /usr/lib/xorg/modules/linux/libfglrxdrm.so
-b /usr/lib/xorg/modules/extensions/libglx.so

```

### Removing prelink

Remove prelinking from all binaries:

```
# prelink -au

```

## Daily cron job

This is recommended (and included in other distros packages) as it has to be done in order to get speed benefits from updates.

 `/etc/cron.daily/prelink` 
```
#!/bin/sh
if [ -x /usr/bin/prelink ]; then
  /usr/bin/prelink -amR >/dev/null 2>&1
fi

```

and give it the necessary ownership and permissions:

```
# chmod 755 /etc/cron.daily/prelink

```

Alternatively, install the [prelink-systemd](https://aur.archlinux.org/packages/prelink-systemd/) package for a daily [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") with the same effect as the above cron script.

## KDE

KDE knows about prelinking and it will start faster if you tell it you have it. It is best to stick this in where all the users can use it.

 `/etc/profile.d/kde-is-prelinked.sh` 
```
export KDE_IS_PRELINKED=1

```

and give it the necessary ownership and permissions:

```
# chmod 755 /etc/profile.d/kde-is-prelinked.sh

```

## Troubleshooting

### segfault, kernel panic

In case you suddenly get a boot failure with errors like [segfault, kernel panic](https://forum.manjaro.org/t/kernel-panic-after-todays-update/32130), it's a very good chance the prelink has caused this.

[Follow this forum in order to restore the functionality of the system.](https://bbs.archlinux.org/viewtopic.php?id=112484,)

## See also

*   [Prelink man page](http://linux.die.net/man/8/prelink)
*   [Gentoo Linux Prelink Guide](http://www.gentoo.org/doc/en/prelink-howto.xml)
*   [ELF Prelinking and what it can do for you](http://crast.us/james/articles/prelink.php)