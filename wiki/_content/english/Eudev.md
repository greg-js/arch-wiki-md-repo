**Warning:** This package will remove [systemd](/index.php/Systemd "Systemd") as it replaces udev. Therefore, you should install an alternative [init](/index.php/Init "Init") system and have it boot successfully under that init system **prior** to installing eudev.

`eudev` is a fork of [udev](/index.php/Udev "Udev") started by the Gentoo project, with the goal of isolation from the [init](/index.php/Init "Init") system. It is primarily designed and tested with [OpenRC](/index.php/OpenRC "OpenRC"), but is agnostic to any other init systems.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 libsystemd](#libsystemd)
*   [2 Replacing the systemd package](#Replacing_the_systemd_package)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Fails to start](#Fails_to_start)
    *   [3.2 netctl](#netctl)
    *   [3.3 Device naming](#Device_naming)
    *   [3.4 sysctl](#sysctl)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [eudev](https://aur.archlinux.org/packages/eudev/) package. Alternatively, install [eudev-git](https://aur.archlinux.org/packages/eudev-git/) for the development version.

**Note:** One may not be able to install the eudev packages directly from the AUR due to conflicts when installing; to circumvent it, [eudev](https://aur.archlinux.org/packages/eudev/) can be built and added to a [local repository](/index.php/Local_repository "Local repository"), and then [eudev-systemdcompat](https://aur.archlinux.org/packages/eudev-systemdcompat/) can be built and installed from the AUR with `makepkg -di` (**-d** to ignore build dependencies), which pulls in eudev as package dependency.

### libsystemd

This package will also remove [libsystemd](https://www.archlinux.org/packages/?name=libsystemd) as it replaces a part of it. The missing libraries are available from:

*   [libsystemd-standalone](https://aur.archlinux.org/packages/libsystemd-standalone/) — a package group with libraries separated into a package each.
*   [eudev-systemdcompat](https://aur.archlinux.org/packages/eudev-systemdcompat/) — a package that guts the official libsystemd package and installs the missing libraries.

You also probably want [systemd-dummy](https://aur.archlinux.org/packages/systemd-dummy/) to satisfy the missing systemd dependency.

Alternatively, you may rebuild packages linked to libsystemd using [ABS](/index.php/ABS "ABS"), or install `nosystemd` variants from the [AUR](/index.php/AUR "AUR").

## Replacing the systemd package

The *systemd* packages include several components besides the init system and systemd-udev:

*   systemd libraries [linked](https://en.wikipedia.org/wiki/Dynamic_linker "wikipedia:Dynamic linker") against software such as [Xorg](/index.php/Xorg "Xorg"). See [#libsystemd](#libsystemd).
*   *systemd-tmpfiles* to create temporary files on system startup. Some rc scripts reimplement this, for example [tmpfiles.sh](https://github.com/OpenRC/openrc/blob/master/sh/tmpfiles.sh.in).
*   *systemd-sysusers* to allocate system users and groups in [pacman](/index.php/Pacman "Pacman") `.install` files

If you have removed systemd without booting to the new init, a reboot is not possible in regular ways. Enable [SysRq keys](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key"):

```
# sysctl kernel.sysrq=1

```

and press `Alt-SysRq-S`, `Alt-SysRq-U` and `Alt-SysRq-B` in succession. This syncs all mounted file systems, remounts all disk as read-only, and reboots the system, respectively. If latter is not possible, press `Alt-SysRq-O` to poweroff). In case the system is a remote box, you must sync and remount read-only its filesystems before triggering an immediate reboot (edit your filesystems accordingly):

```
# sync; mount -f /home -o remount,ro ; sync; mount -f / -o remount,ro
# echo b >| /proc/sysrq-trigger

```

## Troubleshooting

### Fails to start

Check the init script for eudev (aliased to udev, so /etc/openrc/init.d/udev on an OpenRC setup for example) and ensure the command points to /usr/bin/udevd.

### netctl

netctl is not compatible due to dependency on systemd libs, instead, use [netcfg](https://aur.archlinux.org/packages/netcfg/), avaliable in the AUR.

### Device naming

Your net devices will follow the pre-systemd pattern: from example `wlp1s0` should be renamed to `wlan0`. You have to set your net configuration properly.

### sysctl

Your files in `/etc/sysctl.d/` might disappear after removing [systemd](https://www.archlinux.org/packages/?name=systemd). OpenRC reads `/etc/sysctl.conf`.

## See also

*   [Github: Eudev](https://github.com/gentoo/eudev)