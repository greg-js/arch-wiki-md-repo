Related articles

*   [File systems](/index.php/File_systems "File systems")

**翻译状态：** 本文是英文页面 [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-02-10，点击[这里](https://wiki.archlinux.org/index.php?title=NTFS-3G&diff=0&oldid=510372)可以查看翻译后英文页面的改动。

Linux内核目前只支持对微软NTFS文件系统的读取。 [NTFS-3G](http://www.tuxera.com/community/ntfs-3g-download/) 是微软 NTFS 文件系统的一个开源实现，同时支持读和写。NTFS-3G 开发者使用 FUSE 文件系统来辅助开发，同时对可移植性有益。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 手动挂载](#.E6.89.8B.E5.8A.A8.E6.8C.82.E8.BD.BD)
*   [3 格式化](#.E6.A0.BC.E5.BC.8F.E5.8C.96)
*   [4 配置](#.E9.85.8D.E7.BD.AE)
    *   [4.1 默认配置](#.E9.BB.98.E8.AE.A4.E9.85.8D.E7.BD.AE)
    *   [4.2 Linux权限兼容](#Linux.E6.9D.83.E9.99.90.E5.85.BC.E5.AE.B9)
    *   [4.3 允许组/用户](#.E5.85.81.E8.AE.B8.E7.BB.84.2F.E7.94.A8.E6.88.B7)
    *   [4.4 基本的 ntfs-3g 选项](#.E5.9F.BA.E6.9C.AC.E7.9A.84_ntfs-3g_.E9.80.89.E9.A1.B9)
    *   [4.5 允许用户挂载](#.E5.85.81.E8.AE.B8.E7.94.A8.E6.88.B7.E6.8C.82.E8.BD.BD)
    *   [4.6 ntfs-config](#ntfs-config)
*   [5 缩放NTFS分区](#.E7.BC.A9.E6.94.BENTFS.E5.88.86.E5.8C.BA)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 损坏的NTFS文件系统](#.E6.8D.9F.E5.9D.8F.E7.9A.84NTFS.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [6.2 元数据保存在Windows中，拒绝挂载](#.E5.85.83.E6.95.B0.E6.8D.AE.E4.BF.9D.E5.AD.98.E5.9C.A8Windows.E4.B8.AD.EF.BC.8C.E6.8B.92.E7.BB.9D.E6.8C.82.E8.BD.BD)
    *   [6.3 挂载失败](#.E6.8C.82.E8.BD.BD.E5.A4.B1.E8.B4.A5)
*   [7 参见](#.E5.8F.82.E8.A7.81)

## 安装

[安装](/index.php/Install "Install")位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的软件包 [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)。

## 手动挂载

你有两个选择。传统方法是：

```
# mount /dev/*your_NTFS_partition* */mount/point*

```

挂载类型 `ntfs-3g` 不需要显式指定。 `mount` 命令默认会调用 `/usr/bin/mount.ntfs` ，它在安装了 [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) 之后被符号连接到 `/usr/bin/ntfs-3g`。

第二个选择是直接调用 `ntfs-3g`：

```
# ntfs-3g /dev/*your_NTFS_partition* */mount/point*

```

其他可用参数请查看[ntfs-3g(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntfs-3g.8)。

## 格式化

**警告:** 和以前一样，再次检查设备路径。

```
# mkfs.ntfs -Q -L diskLabel /dev/sd*XY*

```

**Note:** `-Q` 选项不向驱动器填充0且不检查坏扇区，以加快格式化速度。

## 配置

你的 NTFS 分区可以被配置成自动挂载，或者预先配置好来安装你想要的方式挂载。配置可以在文件系统配置文件 [fstab](/index.php/Fstab "Fstab") 中指定或者使用 udev 规则。

### 默认配置

使用默认配置会在启动时挂载 NTFS 分区。使用这种方法，如果挂载位置的父文件夹有合适的用户或组[权限](/index.php/Users_and_groups "Users and groups")，用户或组就可以读写这个分区。

把以下内容写入`/etc/fstab`:

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
/dev/*NTFS-part*  /mnt/windows  ntfs-3g   defaults		  0       0

```

### Linux权限兼容

Linux系统通常将目录的权限设为755，将文件的权限设为644。如果您经常使用NTFS分区，建议保留这些权限。下面的示例将上述权限分配给普通用户：

```
# 安装具有 linux 兼容权限的内部 Windows 分区，即权限755用于目录（dmask=022）和权限644用于文件（fmask=133）
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g uid=*username*,gid=users,dmask=022,fmask=133 0 0

```

### 允许组/用户

在`/etc/fstab`中，您还可以指定其他选项，如允许访问（读取）分区的用户。例如，您允许`users`组中的人员具有访问权限：

```
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g   gid=users,umask=0022    0       0

```

默认情况下, 上述命令仅为root用户启用写支持。若要为其他用户启用，必须显示指定应授予写入权限的用户。使用`uid`参数加您的用户名以启用用户写支持：

```
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g   uid=*username*,gid=users,umask=0022    0       0

```

如果您在一个单用户计算机上运行，您可能希望自己拥有该文件系统并授予所有可能的权限：

```
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g   uid=*username*,gid=users    0       0

```

### 基本的 ntfs-3g 选项

对大多数人来说，上面的设置已经足够了。这是一些其他的对于不同的Linux文件系统的通用选项。完整列表参见[这里](http://www.tuxera.com/community/ntfs-3g-manual/#6)

	[umask](/index.php/Umask "Umask")

	umask 是一个嵌入的 shell 命令，可以自动设置新创建的文件的权限。对于 Arch Linux，对于 root 和 user 默认的 umask 是 0022。设为 0022 将使新目录有目录权限755，新文件有权限644。你可以在[这里](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html)查看更多关于 umask 权限的信息：。

	noauto

	如果设置了 `noauto`，`/etc/fstab` 中的 NTFS 条目不会在启动时自动挂载。

	uid

	用户 id 号码。这允许指定用户具有完全的访问权限。你的uid可以用 `id` 命令获得。

	fmask and dmask

	与 `umask` 类似但是分别定义的是文件和目录的权限。

### 允许用户挂载

默认情况下，*ntfs-3g*需要 root 权限以装载文件系统, 即使在`/etc/fstab`中有“user”选项。有关详细信息，请参阅 [ntfs-3g-faq](http://www.tuxera.com/community/ntfs-3g-faq/#useroption)。仍然需要 fstab 中的用户选项。

**Note:**

*   [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)包没有内置FUSE支持。使用[ABS](/index.php/ABS "ABS")重新构建包 或安装[ntfs-3g-fuse](https://aur.archlinux.org/packages/ntfs-3g-fuse/)。
*   卸载权限似乎存在问题，因此如果需要卸载文件系统，则仍需要 root 权限。您还可以使用`fusermount -u /mnt/*mountpoint*`来卸载文件系统并避免使用root权限。此外, 如果在`/etc/fstab`中使用`*users*`（复数）而不是`user`选项，您可以使用`mount`和`umount`命令装卸载文件系统。

### ntfs-config

如果其他方法不生效，[ntfs-config](https://aur.archlinux.org/packages/ntfs-config/)程序也许能帮助您配置NTFS分区。

## 缩放NTFS分区

**Note:** 对重要数据请提前做好备份！

大多数已购买的系统已经有[Windows](https://en.wikipedia.org/wiki/Windows "wikipedia:Windows")安装在其上，有些人希望在进行 Arch Linux 安装时不要完全擦除它。因此，在某些方面，调整现有 Windows 分区的大小以为 Linux 分区腾出空间是很有用的。这经常通过[Live CD](https://en.wikipedia.org/wiki/Live_CD "wikipedia:Live CD")或可引导的USB闪存驱动器完成。

对于Live CD，典型的创建过程是下载ISO文件，刻录到CD，然后从它启动。[InfraRecorder](http://infrarecorder.org/)是一个免费（通过GPL3）的Windows上的CD/DVD刻录应用程序，这是很合适的方法。如果您想要使用可引导的USB驱动器，请参阅[USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media")中创建可引导的USB驱动器的方法。

有许多可引导的CD/USB映像可用。此列表不是详尽无遗的, 但是是个很好的开始：

*   **[GParted](https://en.wikipedia.org/wiki/GParted "wikipedia:GParted")** — 为x86计算机设计的小型GNU/Linux发行版。允许你使用最新版GParted应用的所有功能。不包括额外的软件包System Rescue CD，并且磁盘加密可能不受支持。

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) ||

*   **[Parted Magic](https://en.wikipedia.org/wiki/Parted_Magic "wikipedia:Parted Magic")** — 非常好的完整的硬盘管理解决方案。使用分区编辑器可以调整大小、复制和移动分区。您可以增长或收缩您的 C: 驱动器，为新操作系统创建空间。尝试从丢失的分区中进行数据抢救。

	[http://partedmagic.com/](http://partedmagic.com/) ||

*   **[SystemRescueCD](https://en.wikipedia.org/wiki/SystemRescueCD "wikipedia:SystemRescueCD")** — 良好的工具, 并在大多数情况下无缝工作。一旦启动, 运行 GParted, 其余应该是相当明显的。

	[http://www.sysresccd.org/](http://www.sysresccd.org/) ||

请注意, 调整 NTFS 分区大小的重要程序包括 ntfs-3g 和类似于 (G)parted 或 fdisk 的实用程序，由[util-linux](https://www.archlinux.org/packages/?name=util-linux)包提供。除非您是高级用户，否则最好使用像 GParted 这样的工具来执行任何调整大小操作，以尽量减少由于用户错误而导致数据丢失的可能性。

如果您的系统上已经安装了 Arch Linux，并且只想调整现有 NTFS 分区的大小，则可以使用 parted 和 ntfs-3g 包来完成。或者，在安装 [GParted](/index.php/GParted "GParted") 包后, 可以使用 GParted GUI。

## 疑难解答

### 损坏的NTFS文件系统

如果NTFS文件系统有错，ntfs-3g会以只读方式挂载它。要修复NTFS系统，启动Windows并使用它的磁盘检查程序，chkdsk。考虑到 ntfsfix 只能修复一些错误，如果失败，chkdsk 可能会成功。

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

要启用对其他操作系统的系统分区写入，请确保禁用快速重启。通过以管理员身份执行命令:

```
powercfg /h off

```

你可以在 *控制面板 >硬件与声音> 电源选项 > 系统设置 > 当电源键按下时做什么*， 去掉勾选*启用快速启动*

### 挂载失败

如果你按本指南内容操作也无法挂载你的 NTFS 分区，可以尝试一下在 `fstab` 中的所有 ntfs 分区里加上 [UUID](/index.php/UUID "UUID")。参见 [示例](/index.php/Fstab#UUIDs "Fstab").

## 参见

*   [官方 NTFS-3G 指南](http://www.tuxera.com/community/ntfs-3g-manual/)