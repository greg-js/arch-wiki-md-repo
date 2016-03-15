**翻译状态：** 本文是英文页面 [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-06-26，点击[这里](https://wiki.archlinux.org/index.php?title=NTFS-3G&diff=0&oldid=211242)可以查看翻译后英文页面的改动。

[NTFS-3G](http://www.tuxera.com/community/ntfs-3g-download/) 是微软 NTFS 文件系统的一个开源实现，包括读写支持。NTFS-3G 开发者使用 FUSE 文件系统来辅助开发，同时对可移植性有益。本文介绍如何使用ntfs-3g来读写NTFS分区

## Contents

*   [1 安装ntfs-3g](#.E5.AE.89.E8.A3.85ntfs-3g)
*   [2 手动挂载](#.E6.89.8B.E5.8A.A8.E6.8C.82.E8.BD.BD)
*   [3 配置](#.E9.85.8D.E7.BD.AE)
    *   [3.1 默认配置](#.E9.BB.98.E8.AE.A4.E9.85.8D.E7.BD.AE)
    *   [3.2 允许组/用户](#.E5.85.81.E8.AE.B8.E7.BB.84.2F.E7.94.A8.E6.88.B7)
    *   [3.3 基本的 ntfs-3g 选项](#.E5.9F.BA.E6.9C.AC.E7.9A.84_ntfs-3g_.E9.80.89.E9.A1.B9)
*   [4 其他配置](#.E5.85.B6.E4.BB.96.E9.85.8D.E7.BD.AE)
    *   [4.1 KDE 4](#KDE_4)
    *   [4.2 NTFS-config](#NTFS-config)
*   [5 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [5.1 损坏的NTFS文件系统](#.E6.8D.9F.E5.9D.8F.E7.9A.84NTFS.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [5.2 元数据保存在Windows中，拒绝挂载](#.E5.85.83.E6.95.B0.E6.8D.AE.E4.BF.9D.E5.AD.98.E5.9C.A8Windows.E4.B8.AD.EF.BC.8C.E6.8B.92.E7.BB.9D.E6.8C.82.E8.BD.BD)
    *   [5.3 挂载失败](#.E6.8C.82.E8.BD.BD.E5.A4.B1.E8.B4.A5)
*   [6 其他资源](#.E5.85.B6.E4.BB.96.E8.B5.84.E6.BA.90)

## 安装ntfs-3g

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的软件包 [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)。

## 手动挂载

你有两个选择。传统方法是：

```
# mount -t ntfs-3g /dev/<your-NTFS-partition> /{mnt,...}/<folder>

```

挂载类型 `ntfs-3g` 不需要显式指定。 `mount` 命令默认会调用 `/sbin/mount.ntfs` ，它在安装了 [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) 之后被符号连接到 `/bin/ntfs-3g`。

第二个选择是直接调用 `ntfs-3g`：

```
# ntfs-3g /dev/sda1 /mnt/<mount point>

```

## 配置

你的 NTFS 分区可以被配置成自动挂载，或者预先配置好来安装你想要的方式挂载。配置可以在文件系统配置文件 [fstab](/index.php/Fstab "Fstab") 中指定或者使用 udev 规则。

### 默认配置

使用默认配置会在启动时挂载 NTFS 分区。使用这种方法，如果挂载位置的父文件夹有合适的用户或组权限，用户或组就可以读写这个分区。

把以下内容放置在`/etc/fstab`中:

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
<partition>  <mount point>  ntfs-3g  defaults  0 0

```

### 允许组/用户

你也可以告诉 `/etc/fstab` (the NTFS-3G driver) 其他的选项，例如谁运行访问(读)分区。例如，对于允许 `users` 组访问：

```
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   gid=users,umask=0022    0       0

```

默认情况下，ntfs-3g 驱动只允许 root 用户写入。为了允许用户写入，使用 `dmask` 参数允许用户写入：

```
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   gid=users,fmask=113,dmask=002    0       0

```

如果你运行一个单用户机器，你也许想要自己拥有整个文件系统：

```
/dev/<NTFS-part>  /mnt/windows  ntfs-3g   uid=USERNAME,gid=users    0       0

```

### 基本的 ntfs-3g 选项

对大多数人来说，上面的设置已经足够了。这是一些其他的对于不同的Linux文件系统的通用选项。完整列表参见[这里](http://www.tuxera.com/community/ntfs-3g-manual/#6)

	umask

	umask 是一个嵌入的 shell 命令，可以自动设置新创建的文件的权限。对于 Arch Linux，对于 root 和 user 默认的 umask 是 0022。对于 0022 新目录有目录权限755，新文件有权限 644。你可以在[这里](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html)查看更多关于 umask 权限的信息：。

	noauto

	如果设置了 `noauto`，`/etc/fstab` 中的 NTFS 条目不会在启动时自动挂载。

	uid

	用户 id 号码。这允许指定用户具有完全的访问权限。你的uid可以用 `id` 命令获得。

	fmask and dmask

	与 `umask` 类似但是分别定义的是文件和目录的权限。

	locale

	(2009.1.1 之后可忽略) - ~~一些 locales 需要指定区域选项才能正确显示本地字符。~~

## 其他配置

一些其他帮助您设置 NTFS 分区。

### KDE 4

对于 [KDE](/index.php/KDE "KDE") >= 4.4，右击 Device Notifier applet 选择 **Device Notifier Settings** 然后在 **Removable Devices** 选择你的分区选择 **Automount on login**.

### NTFS-config

[ntfs-config](https://aur.archlinux.org/packages/ntfs-config/) 是一个程序，如果其他方法不奏效的话，可以帮助您配置 NTFS 分区。

## 疑难解答

### 损坏的NTFS文件系统

如果NTFS文件系统有错，ntfs-3g会以只读方式挂载它。要修复NTFS系统，你得启动Windows并使用它的磁盘检查程序。

想要修复 NTFS 文件系统，该设备必须已经被卸载。例如，想要修复 `/dev/sda2` 中的 NTFS 文件系统：

```
# umount /dev/sda2
# ntfsfix /dev/sda2
Mounting volume... OK
Processing of $MFT and $MFTMirr completed successfully.
NTFS volume version is 3.1.
NTFS partition /dev/sda2 was processed successfully.
# mount /dev/sda2

```

如果顺利的话，该分区已经可以写入了。

### 元数据保存在Windows中，拒绝挂载

当与Windows 8 或 10双引导时,试图挂载一个可见的Windows可能会出现如下错误:

```
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
Failed to mount '/dev/sdc1': Operation not permitted
The NTFS partition is in an unsafe state. Please resume and shutdown
Windows fully (no hibernation or fast restarting), or mount the volume
read-only with the 'ro' mount option.

```

问题是因为Windows 8中引入"快速启动"特性。启用快速启动后，所有分区的元数据的一部分被还原到它们在以前关闭的状态。因此，在 Linux 上所做的更改可能会丢失。这会发生在任何选择"关闭"或"休眠" NTFS 分区的Windows 8 或 10 下。然而，通过选择"重新启动"，离开 Windows 是看似安全的。

要启用对其他操作系统的系统分区写入，请确保禁用快速重启。要做到这一点通过以管理员身份执行命令:

```
powercfg /h off

```

你可以在 *控制面板 >硬件与声音> 电源选项 > 系统设置 > 当电源键按下时做什么*， 去掉勾选*启用快速启动*

### 挂载失败

如果你按本指南内容操作也无法挂载你的 NTFS 分区，可以尝试一下在 `fstab` 中的所有 ntfs 分区里加上 [UUID](/index.php/UUID "UUID")。参见 [example](/index.php/Fstab#UUID "Fstab").

## 其他资源

*   [官方 NTFS-3G 指南](http://www.tuxera.com/community/ntfs-3g-manual/)