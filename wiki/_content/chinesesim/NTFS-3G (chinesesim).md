Related articles

*   [File systems](/index.php/File_systems "File systems")

**翻译状态：** 本文是英文页面 [NTFS-3G](/index.php/NTFS-3G "NTFS-3G") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-10-06，点击[这里](https://wiki.archlinux.org/index.php?title=NTFS-3G&diff=0&oldid=573885)可以查看翻译后英文页面的改动。

Linux内核目前只支持对微软NTFS文件系统的读取。 [NTFS-3G](http://www.tuxera.com/community/ntfs-3g-download/) 是微软 NTFS 文件系统的一个开源实现，同时支持读和写。NTFS-3G 开发者使用 FUSE 文件系统来辅助开发，同时对可移植性有益。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 手动挂载](#手动挂载)
*   [3 格式化](#格式化)
*   [4 配置](#配置)
    *   [4.1 默认配置](#默认配置)
    *   [4.2 Linux权限兼容](#Linux权限兼容)
    *   [4.3 允许组/用户](#允许组/用户)
    *   [4.4 基本的 ntfs-3g 选项](#基本的_ntfs-3g_选项)
    *   [4.5 允许用户挂载](#允许用户挂载)
*   [5 缩放NTFS分区](#缩放NTFS分区)
*   [6 疑难解答](#疑难解答)
    *   [6.1 已压缩的文件](#已压缩的文件)
    *   [6.2 损坏的NTFS文件系统](#损坏的NTFS文件系统)
    *   [6.3 元数据保存在Windows中，拒绝挂载](#元数据保存在Windows中，拒绝挂载)
    *   [6.4 删除Windows休眠元数据](#删除Windows休眠元数据)
    *   [6.5 挂载失败](#挂载失败)
    *   [6.6 Windows mount failure](#Windows_mount_failure)
*   [7 Beta features & releases](#Beta_features_&_releases)
*   [8 参见](#参见)

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

	windows_names

	prevents files, directories and extended attributes to be created with a name not allowed by windows.

### 允许用户挂载

默认情况下，*ntfs-3g*需要 root 权限以装载文件系统, 即使在`/etc/fstab`中有“user”选项。有关详细信息，请参阅 [ntfs-3g-faq](http://www.tuxera.com/community/ntfs-3g-faq/#useroption)。仍然需要 fstab 中的用户选项。

**Note:**

*   [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)包没有内置FUSE支持。使用[ABS](/index.php/ABS "ABS")重新构建包 或安装[ntfs-3g-fuse](https://aur.archlinux.org/packages/ntfs-3g-fuse/)。
*   卸载权限似乎存在问题，因此如果需要卸载文件系统，则仍需要 root 权限。您还可以使用`fusermount -u /mnt/*mountpoint*`来卸载文件系统并避免使用root权限。此外, 如果在`/etc/fstab`中使用`*users*`（复数）而不是`user`选项，您可以使用`mount`和`umount`命令装卸载文件系统。

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

### 已压缩的文件

若您在读取Windows 10分区中的文件和文件夹时出现以下情形：

1.  出现链接到“不支持的重解析点”（unsupported reparse point）的损坏的符号链接，或
2.  出现错误信息：“cannot access <*filename*>: Input/output error” （此时/var/log/messages中会出现“Could not load plugin /usr/lib64/ntfs-3g/ntfs-plugin-80000017.so: Success”)

请安装[ntfs-3g-system-compression](https://aur.archlinux.org/packages/ntfs-3g-system-compression/)插件，之后便可读取已压缩的文件了。

NTFS-3G默认不支持某些类型的[重解析点](https://en.wikipedia.org/wiki/NTFS_reparse_points "wikipedia:NTFS reparse points")。[点击此处](https://jp-andre.pagesperso-orange.fr/junctions.html#other)查看可用的插件列表。

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

当与 Windows 8 或 10双引导时,试图挂载一个可见的Windows可能会出现如下错误:

```
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
Failed to mount '/dev/sdc1': Operation not permitted
The NTFS partition is in an unsafe state. Please resume and shutdown
Windows fully (no hibernation or fast restarting), or mount the volume
read-only with the 'ro' mount option.

```

问题是因为Windows 8中引入"快速启动"特性。启用快速启动后，所有分区的元数据的一部分被还原到它们在以前关闭的状态。因此，在 Linux 上所做的更改可能会丢失。这会发生在任何选择"关闭"或"休眠" NTFS 分区的Windows 8 或 10 下。然而，通过选择"重新启动"关闭 Windows 是安全的。

要启用对其他操作系统的系统分区写入，请确保禁用快速重启。通过以管理员身份执行命令:

```
powercfg /h off

```

你可以在 *控制面板 >硬件与声音> 电源选项 > 系统设置 > 当电源键按下时做什么*， 去掉勾选*启用快速启动*

### 删除Windows休眠元数据

作为一个以上干净关机方法的替代方法，有一个办法可以彻底删除休眠后保存的 NTFS 元数据。这个方法只适用于当你不能或不想启动至 Windows，并希望它完全关闭。这个办法是在使用 ntfs-3g 挂载 NTFS 分区时使用 **remove_hiberfile** 选项。

```
# mount -t ntfs-3g -o remove_hiberfile /dev/*your_NTFS_partition* */mount/point*

```

**警告:** 这个方法意味着已保存的 Windows 会话将彻底丢失。使用该选项后果自负。

### 挂载失败

如果你按本指南内容操作也无法挂载你的 NTFS 分区，可以尝试一下在 `fstab` 中的所有 ntfs 分区里加上 [UUID](/index.php/UUID "UUID")。参见 [示例](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#UUID "Fstab (简体中文)").

### Windows mount failure

Windows will not recognize a NTFS partition that does not have a corresponding partition type. A common pitfall when creating an NTFS partition to work with Windows is forgetting to set the partition type as NTFS. See [fdisk](/index.php/Fdisk "Fdisk") or one of the [partitioning tools](/index.php/Partitioning_tools "Partitioning tools").

## Beta features & releases

There is a [web page](http://jp-andre.pagesperso-orange.fr/advanced-ntfs-3g.html) on "advanced features" (add-ons) [1], maintained by Jean-Pierre André, one of the ntfs-3g authors. That page also provides new versions, not yet incorporated to the official releases.

Currently these add-ons support:

*   System compression
*   OneDrive
*   Duplicated files

In the page [1] there is a pointer to the "updated version" of the system compression plugin [mentioned above](#Compressed_files). In fact, the update is small; all updates are in:

*   README.md
*   configure.ac, with slight modification. See the attachment

The web page [1] is surely written by J.-P. André. The page [NTFS-3G Advanced](https://www.tuxera.com/community/ntfs-3g-advanced/) in the official site in tuxera.com has a link to the [OpenIndiana page](http://jp-andre.pagesperso-orange.fr/openindiana-ntfs-3g.html), which in turn links to [1].

## 参见

*   [官方 NTFS-3G 指南](http://www.tuxera.com/community/ntfs-3g-manual/)