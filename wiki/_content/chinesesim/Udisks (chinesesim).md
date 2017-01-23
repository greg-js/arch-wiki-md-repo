**翻译状态：** 本文是英文页面 [Udisks](/index.php/Udisks "Udisks") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-05-27，点击[这里](https://wiki.archlinux.org/index.php?title=Udisks&diff=0&oldid=434397)可以查看翻译后英文页面的改动。

[udisks](http://www.freedesktop.org/wiki/Software/udisks/) 提供了 *udisksd* 守护进程，它实现了用于查询和管理存储设备的 D-Bus 接口；还提供了一个命令行工具 *udisksctl*，用于查询和使用该守护进程。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 挂载助手](#.E6.8C.82.E8.BD.BD.E5.8A.A9.E6.89.8B)
    *   [3.1 Devmon](#Devmon)
    *   [3.2 udevadm monitor](#udevadm_monitor)
    *   [3.3 udiskie](#udiskie)
        *   [3.3.1 udiskie freezing and configuration](#udiskie_freezing_and_configuration)
    *   [3.4 udisksvm](#udisksvm)
*   [4 提示与技巧](#.E6.8F.90.E7.A4.BA.E4.B8.8E.E6.8A.80.E5.B7.A7)
    *   [4.1 禁止隐藏设备（udisks2）](#.E7.A6.81.E6.AD.A2.E9.9A.90.E8.97.8F.E8.AE.BE.E5.A4.87.EF.BC.88udisks2.EF.BC.89)
    *   [4.2 挂载到 /media (udisks2)](#.E6.8C.82.E8.BD.BD.E5.88.B0_.2Fmedia_.28udisks2.29)
    *   [4.3 挂载 loop 设备](#.E6.8C.82.E8.BD.BD_loop_.E8.AE.BE.E5.A4.87)
    *   [4.4 隐藏选中的分区](#.E9.9A.90.E8.97.8F.E9.80.89.E4.B8.AD.E7.9A.84.E5.88.86.E5.8C.BA)
*   [5 排错](#.E6.8E.92.E9.94.99)
    *   [5.1 卸载的设备被自动挂载](#.E5.8D.B8.E8.BD.BD.E7.9A.84.E8.AE.BE.E5.A4.87.E8.A2.AB.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
    *   [5.2 物理设备移除后再连接，无法再次挂载](#.E7.89.A9.E7.90.86.E8.AE.BE.E5.A4.87.E7.A7.BB.E9.99.A4.E5.90.8E.E5.86.8D.E8.BF.9E.E6.8E.A5.EF.BC.8C.E6.97.A0.E6.B3.95.E5.86.8D.E6.AC.A1.E6.8C.82.E8.BD.BD)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 安装

有两个版本的 *udisks*，分别称为 [udisks](https://aur.archlinux.org/packages/udisks/) 和 [udisks2](https://www.archlinux.org/packages/?name=udisks2)。为了集中精力开发*udisks2*，*udisks* 的开发已终止 。[[1]](http://davidz25.blogspot.be/2012/03/simpler-faster-better.html)

*udisksd* ([udisks2](https://www.archlinux.org/packages/?name=udisks2)) 和 *udisks-daemon* ([udisks](https://aur.archlinux.org/packages/udisks/)) 都是由 [D-Bus](/index.php/D-Bus "D-Bus") 在后台启动，不应该被显式地启用。（参阅 `man udisksd` 和 `man udisks-daemon`）。可以通过 *udisksctl* 和 *udisks* 以命令行方式分别进行管控。详情参阅 `man udisksctl` 和 `man udisks`。

## 配置

用户通过 udisks 可执行的动作由 [Polkit](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Polkit (简体中文)") 控制。如果[会话](/index.php/Session "Session")不活跃或不存在，例如通过 [systemd/User](/index.php/Systemd/User_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd/User (简体中文)") 控制 udisks 时，需要手动配置 policykit.

[这里](https://github.com/coldfix/udiskie/wiki/Permissions) 包含 `storage` 群组的 udisk 配置， [这里](https://gist.github.com/grawity/3886114#file-udisks2-allow-mount-internal-js)有一个更严格的版本。

## 挂载助手

通过 [udisks 工具程序](/index.php/List_of_applications#Udisks "List of applications")也可以实现挂载，请参考 [List of applications#Mount tools](/index.php/List_of_applications#Mount_tools "List of applications") 和 [File manager functionality#Mounting](/index.php/File_manager_functionality#Mounting "File manager functionality")。

### Devmon

[udevil](https://www.archlinux.org/packages/?name=udevil) 包含 [devmon](http://igurublog.wordpress.com/downloads/script-devmon), 这个程序和 *udisks*/*udisks2* 兼容，按照下面的优先级选择挂载程序：

1.  [udevil](http://ignorantguru.github.io/udevil/) (SUID)
2.  pmount (SUID)
3.  udisks
4.  udisks2

要通过 *udisks* 或 *udisks2* 挂载，从 *udevil* 删除 SUID:

```
# chmod -s /usr/bin/udevil

```

**Note:** 用 root 执行 `chmod -x /usr/bin/udevil` 会让 devmon 使用 *udisks* 执行设备监控。

**Tip:** 要在后台执行 devmon 自动挂载，用 `devmon@.service` [启用服务](/index.php/Enable "Enable")，用户名作为参数: `devmon@*user*.service`. 请注意这里是在 [session](/index.php/Session "Session") 之外执行的，需要调整 Polkit 规则或从用户会话启动，参考 [自动启动](/index.php/Autostart "Autostart").

### udevadm monitor

可以使用 `udevadm monitor` 监测块设备事件并在新的块设备被创建时进行挂载。无用的挂载点会被 *udisksd* 自动删除，所以删除时不需要额外动作。

```
#!/bin/bash

pathtoname() {
    udevadm info -p "/sys/$1" | awk -v FS== '/DEVNAME/ {print $2}'
}

while read -r _ _ event devpath _; do
        if [[ $event == add ]]; then
            devname=$(pathtoname "$devpath")
            udisksctl mount --block-device "$devname" --no-user-interaction
        fi
done < <(stdbuf -o L udevadm monitor --udev -s block)

```

### udiskie

[udiskie](https://www.archlinux.org/packages/?name=udiskie) 是使用 [udisks](https://aur.archlinux.org/packages/udisks/) 或 [udisks2](https://www.archlinux.org/packages/?name=udisks2) 的挂载助手，支持密码保护的 [LUKS 设备](/index.php/Dm-crypt/Device_encryption "Dm-crypt/Device encryption"). 请参考[Wiki](https://github.com/coldfix/udiskie/wiki/Usage)。

#### udiskie freezing and configuration

[udiskie](https://www.archlinux.org/packages/?name=udiskie) may freeze/crash or not work in some situations/setups if you do not have some of the notification support installed. For [instance](https://bbs.archlinux.org/viewtopic.php?id=203164) xfce and udiskie may not work correctly. You may see udiskie freeze in xfce if you do not install [xfce4-notifyd](https://www.archlinux.org/packages/?name=xfce4-notifyd) and [notify-osd](https://www.archlinux.org/packages/?name=notify-osd) also.

if you do not source /etc/X11/xinit/xinitrc.d/50-systemd-user.sh in your .xinitrc you may have issues also.

### udisksvm

[udisksvm](https://aur.archlinux.org/packages/udisksvm) is a graphical udisks2 wrapper application written in Python3 and using the Qt5 framework. It uses only mouse clicks to mount, unmount removable devices or eject a CD/DVD. It is well adapted to light weight graphical environments, like Openbox with Tint2. It is a stand-alone mounting/automounting application running in background (see the README file in the package for details)

## 提示与技巧

### 禁止隐藏设备（udisks2）

Udisks2 在默认情况下会隐藏一些设备，如果不希望隐藏，可以将 `/usr/lib/udev/rules.d/80-udisks2.rules` 复制到 `/etc/udev/rules.d/80-udisks2.rules` 并删除不需要隐藏的设备：

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

### 挂载 loop 设备

要挂载 ISO 镜像，使用下面命令：

```
$ udisksctl loop-setup -r -f *image.iso*

```

这条命令会创建 loop 设备并显示可以挂载的 ISO 镜像，卸载后，loop 设备会被 [udev](/index.php/Udev "Udev") 删除.

**提示：** This mounts a read only image. To mount raw disk images, such as for [QEMU](/index.php/QEMU "QEMU"), remove the `-r` flag, and release the image after use with `udisksctl loop-delete -b */dev/loop0*`. Substitute `/dev/loop0` with the name of the loop device.

### 隐藏选中的分区

如果要在桌面中隐藏某些分区或设备，可以创建类似下面的 udev 规则 `/etc/udev/rules.d/10-local.rules`:

```
KERNEL=="sda1", ENV{UDISKS_PRESENTATION_HIDE}="1"
KERNEL=="sda2", ENV{UDISKS_PRESENTATION_HIDE}="1"

```

会隐藏 `sda1` 和 `sda2`，如果使用 [udisks2](https://www.archlinux.org/packages/?name=udisks2)，请使用 `UDISKS_IGNORE`:

```
KERNEL=="sda1", ENV{UDISKS_IGNORE}="1"
KERNEL=="sda2", ENV{UDISKS_IGNORE}="1"

```

Because block device names can change between reboots, it is also possible to use UUIDs (as gathered from executing the `blkid /dev/sdX` command) to hide partitions or whole devices:

For example:

```
# blkid /dev/sdX
/dev/sdX: LABEL="Filesystem Label" UUID="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXXX" UUID_SUB="YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY" TYPE="btrfs"

```

Then the following line can be used:

```
ENV{ID_FS_UUID}=="XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXXX", ENV{UDISKS_IGNORE}="1"

```

The above line is also useful to hide multi device btrfs filesystems, as all the devices from a single btrtfs filesystem will share the same UUID across the devices but will have different SUB_UUID for each individual device.

## 排错

### 卸载的设备被自动挂载

*udisks* 会定期检查设备并自动挂载，这会在格式化磁盘，[虚拟机](/index.php/Virtual_machine "Virtual machine") 共享时导致问题，不利于省电。

禁用设备定期检查，以 CD/DVD 设备为例:

```
# udisks --inhibit-polling /dev/sr*0*

```

要禁用所有设备的定期检查:

```
# udisks --inhibit-all-polling

```

详情请参考`man udisks`.

### 物理设备移除后再连接，无法再次挂载

当 udisk 和 [systemd](/index.php/Systemd "Systemd") 同时尝试卸载设备时可能会出现此问题，[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1588027#p1588027) [[3]](https://github.com/systemd/systemd/issues/1741) 错误信息:

```
Jan 16 18:46:04 thinkpad systemd[1]: media-ASMT_2105.mount: Unit is bound to inactive unit dev-sdc2.device. Stopping, too.
Jan 16 18:46:04 thinkpad systemd[1]: Unmounting /media/ASMT_2105...

```

重置设备挂载状态：

```
# systemctl reset-failed

```

## 参阅

*   [gentoo wiki: udisks](http://wiki.gentoo.org/wiki/Udisks)
*   [Udisks 介绍](http://blog.fpmurphy.com/2011/08/introduction-to-udisks.html?output=pdf)