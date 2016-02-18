**翻译状态：** 本文是英文页面 [Udisks](/index.php/Udisks "Udisks") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-08，点击[这里](https://wiki.archlinux.org/index.php?title=Udisks&diff=0&oldid=403663)可以查看翻译后英文页面的改动。

[udisks](http://www.freedesktop.org/wiki/Software/udisks/) 提供了 *udisksd* 守护进程，它实现了用于查询和管理存储设备的 D-Bus 接口；还提供了一个命令行工具 *udisksctl*，用于查询和使用该守护进程。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 挂载助手](#.E6.8C.82.E8.BD.BD.E5.8A.A9.E6.89.8B)
    *   [3.1 Devmon](#Devmon)
    *   [3.2 inotify](#inotify)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 禁止隐藏设备（udisks2）](#.E7.A6.81.E6.AD.A2.E9.9A.90.E8.97.8F.E8.AE.BE.E5.A4.87.EF.BC.88udisks2.EF.BC.89)
    *   [4.2 挂载到 /media (udisks2)](#.E6.8C.82.E8.BD.BD.E5.88.B0_.2Fmedia_.28udisks2.29)
    *   [4.3 挂载 ISO 镜像](#.E6.8C.82.E8.BD.BD_ISO_.E9.95.9C.E5.83.8F)
    *   [4.4 隐藏选中的分区](#.E9.9A.90.E8.97.8F.E9.80.89.E4.B8.AD.E7.9A.84.E5.88.86.E5.8C.BA)
*   [5 排错](#.E6.8E.92.E9.94.99)
    *   [5.1 udisks: Devices do not remain unmounted](#udisks:_Devices_do_not_remain_unmounted)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

有两个版本的 *udisks*，分别称为 [udisks](https://www.archlinux.org/packages/?name=udisks) 和 [udisks2](https://www.archlinux.org/packages/?name=udisks2)。*udisks* 的开发已终止以利于 *udisks2*。[[1]](http://davidz25.blogspot.be/2012/03/simpler-faster-better.html)

*udisksd* ([udisks2](https://www.archlinux.org/packages/?name=udisks2)) 和 *udisks-daemon* ([udisks](https://www.archlinux.org/packages/?name=udisks)) 都是由 [D-Bus](/index.php/D-Bus "D-Bus") 在后台启动，并且不应该被显式地启用。（参阅 `man udisksd` 和 `man udisks-daemon`）。它们分别可以通过 *udisksctl* 和 *udisks* 以命令行方式管控。详情参阅 `man udisksctl` 和 `man udisks`。

## 配置

用户通过 udisks 可执行的动作受限于 [Polkit](/index.php/Polkit "Polkit")。If your [session](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") is not activated or present, configure policykit manually. The following file sets common udisks permissions for the `storage` group. [[2]](https://github.com/coldfix/udiskie#permissions)

 `/etc/polkit-1/rules.d/50-udisks.rules` 
```
polkit.addRule(function(action, subject) {
  var YES = polkit.Result.YES;
  var permission = {
    // only required for udisks1:
    "org.freedesktop.udisks.filesystem-mount": YES,
    "org.freedesktop.udisks.filesystem-mount-system-internal": YES,
    "org.freedesktop.udisks.luks-unlock": YES,
    "org.freedesktop.udisks.drive-eject": YES,
    "org.freedesktop.udisks.drive-detach": YES,
    // only required for udisks2:
    "org.freedesktop.udisks2.filesystem-mount": YES,
    "org.freedesktop.udisks2.filesystem-mount-system": YES,
    "org.freedesktop.udisks2.encrypted-unlock": YES,
    "org.freedesktop.udisks2.eject-media": YES,
    "org.freedesktop.udisks2.power-off-drive": YES,
    // required for udisks2 if using udiskie from another seat (e.g. systemd):
    "org.freedesktop.udisks2.filesystem-mount-other-seat": YES,
    "org.freedesktop.udisks2.encrypted-unlock-other-seat": YES,
    "org.freedesktop.udisks2.eject-media-other-seat": YES,
    "org.freedesktop.udisks2.power-off-drive-other-seat": YES
  };
  if (subject.isInGroup("storage")) {
    return permission[action.id];
  }
});
```

See [[3]](https://gist.github.com/grawity/3886114#file-udisks2-allow-mount-internal-js) for a more restrictive example. Note the `org.freedesktop.udisks2.filesystem-*` settings, which are required to start udiskie from a [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") service.

## 挂载助手

Automatic mounting of devices is easily achieved with [udisks wrappers](/index.php/List_of_applications#Udisks "List of applications"). See also [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications") and [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality").

### Devmon

[udevil](https://www.archlinux.org/packages/?name=udevil) includes [devmon](http://igurublog.wordpress.com/downloads/script-devmon), which is compatible to *udisks* and *udisks2*. It uses mount helpers with the following priority:

1.  [udevil](http://ignorantguru.github.io/udevil/) (SUID)
2.  pmount (SUID)
3.  udisks
4.  udisks2

To mount devices with *udisks* or *udisks2*, remove the SUID permission from *udevil*:

```
# chmod -s /usr/bin/udevil

```

**Note:** `chmod -x /usr/bin/udevil` as root causes devmon to use *udisks* for device monitoring

**Tip:** To run devmon in the background and automatically mount devices, [enable](/index.php/Enable "Enable") it with `devmon@.service`, taking the user name as argument: `devmon@*user*.service`. Keep in mind services run outside the [session](/index.php/Session "Session"). Adjust Polkit rules where appropriate, or run `devmon` from the user session (see [Autostart](/index.php/Autostart "Autostart")).

### inotify

You may use [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) to monitor `/dev`, and mount drives when a new block device is created. Stale mount points are automatically removed by *udisksd*, such that no special action is required on deletion.

```
#!/bin/bash
pattern='sd[b-z][1-9]$'
coproc inotifywait --monitor --event create,delete --format '%e %w%f' /dev

while read -r -u "${COPROC[0]}" event file; do
    if [[ $file =~ $pattern ]]; then
	case $event in
	    CREATE)
		echo "Settling..."; sleep 1
		udisksctl mount --block-device $file --no-user-interaction
		;;
	    DELETE)
		;;
	esac
    fi
done

```

## 提示与技巧

### 禁止隐藏设备（udisks2）

Udisks2 hides certain devices from the user by default. If this is undesired or otherwise problematic, copy `/usr/lib/udev/rules.d/80-udisks2.rules` to `/etc/udev/rules.d/80-udisks2.rules` and remove the following section in the copy:

```
# ------------------------------------------------------------------------
# ------------------------------------------------------------------------
# ------------------------------------------------------------------------
# Devices which should not be display in the user interface
[...]

```

### 挂载到 /media (udisks2)

默认情况下， udisks2 在 ACL 控制下将可移动设备挂载到 `/run/media/$USER/` 目录下。如果你希望改为挂载到 `/media` 目录下，应用这条规则：

 `/etc/udev/rules.d/99-udisks2.rules` 
```
# UDISKS_FILESYSTEM_SHARED
# ==1: mount filesystem to a shared directory (/media/VolumeName)
# ==0: mount filesystem to a private directory (/run/media/$USER/VolumeName)
# See udisks(8)
ENV{ID_FS_USAGE}=="filesystem|other|crypto", ENV{UDISKS_FILESYSTEM_SHARED}="1"

```

### 挂载 ISO 镜像

To easily mount ISO images, use the following command:

```
$ udisksctl loop-setup -r -f *image.iso*

```

This will create a loop device and show the ISO image ready to mount. Once unmounted, the loop device will be terminated by [udev](/index.php/Udev "Udev").

### 隐藏选中的分区

If you wish to prevent certain partitions or drives appearing on the desktop, you can create a udev rule, for example `/etc/udev/rules.d/10-local.rules`:

```
KERNEL=="sda1", ENV{UDISKS_PRESENTATION_HIDE}="1"
KERNEL=="sda2", ENV{UDISKS_PRESENTATION_HIDE}="1"

```

shows all partitions with the exception of `sda1` and `sda2` on your desktop. Notice if you are using [udisks2](https://www.archlinux.org/packages/?name=udisks2) the above will not work as `UDISKS_PRESENTATION_HIDE` is no longer supported. Instead use `UDISKS_IGNORE` as follows:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

## 排错

### udisks: Devices do not remain unmounted

*udisks* remounts devices after a given period, or *polls* those devices. This can cause unexpected behaviour, for example when formatting drives, sharing them in a [virtual machine](/index.php/Virtual_machine "Virtual machine"), power saving, or removing a drive that was not detached with `--detach` before.

To disable polling for a given device, for example a CD/DVD device:

```
# udisks --inhibit-polling /dev/sr*0*

```

or for all devices:

```
# udisks --inhibit-all-polling

```

See `man udisks` for more information.

## 参阅

*   [gentoo wiki: udisks](http://wiki.gentoo.org/wiki/Udisks)
*   [Udisks 介绍](http://blog.fpmurphy.com/2011/08/introduction-to-udisks.html?output=pdf)