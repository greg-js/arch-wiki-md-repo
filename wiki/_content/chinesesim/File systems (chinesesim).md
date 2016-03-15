**翻译状态：** 本文是英文页面 [File_Systems](/index.php/File_Systems "File Systems") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-09-29，点击[这里](https://wiki.archlinux.org/index.php?title=File_Systems&diff=0&oldid=335883)可以查看翻译后英文页面的改动。

根据 [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	*文件系统是数据组织方式，定义数据在磁盘上的保存、读取和更新方法。不同的文件系统可以根据存储设备的不同进行优化，提高效率*。

Arch Linux支持许多文件系统类型，我们可以为每个磁盘分区设置不同的文件系统。每种文件系统有自己的优缺点和独有特性。以下内容是关于Arch Linux支持的文件系统类型的概述，左侧的链接地址指向Wikipedia以提供更丰富的信息。

磁盘需要首先[分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")，然后再在格式化成指定文件系统。

## Contents

*   [1 文件系统类型](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E7.B1.BB.E5.9E.8B)
    *   [1.1 文件系统日志](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E6.97.A5.E5.BF.97)
    *   [1.2 文件系统支持](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E6.94.AF.E6.8C.81)
*   [2 基于 FUSE 的文件系统支持](#.E5.9F.BA.E4.BA.8E_FUSE_.E7.9A.84.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E6.94.AF.E6.8C.81)
*   [3 创建文件系统](#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [4 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)

## 文件系统类型

*   [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - 也被称作"Better FS", 是一种**具备与Sun/Oracle的ZFS相近特性的新文件系统**。特性包括快照，多磁盘条带化，多盘镜像（不需要mdadm即可组成软RAID），数据校验，增量备份，以及能同时提升性能并节省空间的透明压缩功能（目前支持zlib和LZO）。截止2014年4月，Btrfs虽然已经合并到主干内核中，但仍被标记为实验性质。Btrfs被认为是 GNU/Linux 文件系统的未来，并被所有主流发行版的安装程序设置为root分区文件系统选项。
*   [exFAT](https://en.wikipedia.org/wiki/exFAT "wikipedia:exFAT") - **Microsoft file system optimized for flash drives**。和 NTFS 不同，exFAT 不能通过将磁盘空间标记为“已分配”就为文件预分配磁盘空间。和 FAT 一样，exFAT在创建一个已知长度的文件时，需要完整的执行与文件体积相等的物理写入。
*   [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") - **Second Extended Filesystem**。古老、可靠的 GNU/Linux 文件系统。非常稳定，一个缺点是不支持日志记录或隔离。不支持日志会导致在突然断电或当机时可能导致数据丢失。因为文件系统检查的时间很长，**不适合**用于根 (`/`) 和 `/home` 分区。ext2 可以容易地[转换成 ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3")。
*   [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") - **Third Extended Filesystem**。基于 ext2 系统, 并添加了日志记录功能。 ext3 向前兼容 ext2 ，非常成熟稳定。
*   [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") - **Fourth Extended Filesystem**。一种新的文件系统，向前兼容 ext2 和 ext3 ，最大支持 1EB (1,048,576 TB) 分区，支持单个 16TB 的文件。子目录最大个数支持 64,000， ext3 只支持 32,000。支持在线碎片处理。
*   [F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") - **Flash-Friendly File System**。由Samsung的Kim Jaegeuk（韩文：김재극）为Linux编写的适用于Flash设备的文件系统。F2FS的设计初衷是为了针对NAND闪存设备（包括SSD，eMMC和SD卡）的特性打造一个新的文件系统。这些设备目前在从移动设备到服务器的范畴内被广泛使用。
*   [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) - IBM 的**日志文件系统（ Journaled File System ）**。这是第一个支持日志的文件系统。它在 IBM AIX® 操作系统中开发了多年，然后被移植到GNU/Linux上。JFS 效率非常高并且 CPU 资源占用率比 GNU/Linux 上的其他任何一个文件系统都要低。并且在格式化、挂载和磁盘检测的时候都非常快，在各方面的表现都非常突出,尤其是与 deadline I/O 调度器结合。不如ext系列或者ReiserFS那样广泛支持，但非常成熟稳定。
*   [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") - **New Implementation of a Log-structured File System**。由 NTT 开发。该文件系统将所有数据以连续的类似日志的结构储存，新数据只添加不改写。这种设计减少了寻址时间，相对传统的 Linux 文件系统能防止在崩溃发生后的数据丢失。
*   [NTFS](https://en.wikipedia.org/wiki/NTFS "wikipedia:NTFS") - **Windows使用的文件系统**。 NTFS 相比 FAT 和 HPFS（High Performance File System）在技术作了若干改进，例如，支持元数据，并且使用了高级数据结构，以便于改善性能、可靠性和磁盘空间利用率，并提供了若干附加扩展功能，如访问控制列表和文件系统日志。
*   [Reiser4](https://en.wikipedia.org/wiki/Reiser4 "wikipedia:Reiser4") - **ReiserFS 的继任者**。由 Namesys 开发， DARPA 和 Linspire 赞助。使用 B*-tree 辅以 Dancing Tree，这样的机制使得稀疏的节点通常不会被合并，除非因为内存压力触发刷盘或对应的事务已经完成。这样的机制同时也保证了 Reiser4 在创建文件和目录的时候不需要浪费时间和Fixed Block（Such a system also allows Reiser4 to create files and directories without having to waste time and space through fixed blocks）。
*   [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") - **Hans Reiser主持开发的高性能日志文件系统 ReiserFS(v3)**。使用一种非常独特有趣的数据存储检索方法。ReiserFS 效率非常高, 特别在处理很多小文件的时候更是如此。ReiserFS 格式化的时候很快，但在挂载的时候相对比较慢。性能稳定。 ReiserFS 现在的开发并不活跃(最新的版本是Reiser4)。通常是 `/var` 目录的好选择。
*   [VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "wikipedia:File Allocation Table") - **Virtual File Allocation Table（虚拟文件分配表）**。这种文件系统技术简单，受各种系统广泛支持。这种格式常用于固态存储卡，便于系统间文件交换。VFAT支持长文件名。
*   [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") - **由 Silicon Graphics 开发的历史悠久的日志文件系统**，最初是为 IRIX 操作系统开发，后来移植到 GNU/Linux。在处理大文件的时候能够提供高吞吐能力，格式化和挂载都非常快。对比测试显示 XFS 在处理数量较多的小文件时比较慢。 XFS 非常稳定，支持在线碎片整理。
*   [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS") - **由 Sun Microsystems 设计开发的文件系统和卷管理器综合体**。ZFS的特性包括数据错误保护，支持大容量存储（文件系统大小和单个文件大小支持16 EB，单个文件系统支持2个文件，zpool最大支持128 ZB），集成文件系统和卷管理，快照，写时拷贝，持续的完整性检查和自动修复，RAID-Z，原生 NFSV4 ACLs。

### 文件系统日志

以上除了 ext2 和 FAT16/32（即VFAT）以外的文件系统都支持[文件系统日志](https://en.wikipedia.org/wiki/zh:%E6%97%A5%E5%BF%97%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F "wikipedia:zh:日志文件系统")。文件系统日志通过在数据实际变更前写入日志记录变更来提供故障恢复能力。当出现系统崩溃或掉电故障的时候，这些文件系统能够更快的恢复到可用状态，并且在恢复过程中更不容易出现错误。文件系统日志将会占用文件系统中的一部分空间。

并非所有的文件系统日志技术都相同。只有 ext3 和 ext4 提供 data-mode journaling，同时记录数据本身和元数据。由于对性能影响很大，这个功能默认是禁用的。其它文件系统仅提供记录元数据日志的ordered-mode journaling。尽管都能在系统崩溃后将系统返回正常状态，data-mode journaling 提供了最大程度的数据安全防护，但性能有所降低，因为数据会被写两次(第一次到日志，第二次到磁盘)。可以根据数据的重要性选择文件系统。

### 文件系统支持

*   **btrfs-progs** — [Btrfs](/index.php/Btrfs "Btrfs") 支持.

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **dosfstools** — VFAT 支持.

	[http://www.daniel-baumann.ch/software/dosfstools/](http://www.daniel-baumann.ch/software/dosfstools/) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **exfat-utils** — exFAT 支持.

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **f2fs-tools** — [F2FS](/index.php/F2fs "F2fs") support.

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **e2fsprogs** — ext2, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4") 支持.

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **jfsutils** — [JFS](/index.php/JFS "JFS") 支持.

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **nilfs-utils** — NILFS 支持.

	[http://nilfs.sourceforge.net/](http://nilfs.sourceforge.net/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **ntfs-3g** — [NTFS](/index.php/NTFS "NTFS") 支持.

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **reiser4progs** — [ReiserFSv4](/index.php/Reiser4 "Reiser4") 支持.

	[http://sourceforge.net/projects/reiser4/](http://sourceforge.net/projects/reiser4/) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)

*   **reiserfsprogs** — ReiserFSv3 支持.

	[https://www.kernel.org/](https://www.kernel.org/) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **xfsprogs** — [XFS](/index.php/XFS "XFS") 支持.

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **zfs** — [ZFS](/index.php/ZFS "ZFS") 支持.

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs-git](https://aur.archlinux.org/packages/zfs-git/)

## 基于 FUSE 的文件系统支持

[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") （FUSE） 是 Unix 类操作系统中一种允许非特权用户在不修改内核代码的前提下创建自己的文件系统的一种机制。文件系统相关的代码会在*用户空间*运行，FUSE 内核模块仅仅是提供一个通往内核接口的“桥梁”。

一些值得注意的基于 FUSE 的文件系统如下：

*   **acd-fuse** — Amazon cloud drives 支持

	[https://github.com/handyman5/acd_fuse](https://github.com/handyman5/acd_fuse) || [acdfuse-git](https://aur.archlinux.org/packages/acdfuse-git/)

*   **adbfs-git** — Android 设备文件系统挂载支持

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **cddfs** — 音乐 CD 挂载支持

	[http://castet.matthieu.free.fr/](http://castet.matthieu.free.fr/) || [cddfs](https://aur.archlinux.org/packages/cddfs/)

*   **fuse-exfat** — exFAT 支持

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [fuse-exfat](https://www.archlinux.org/packages/?name=fuse-exfat)

*   **fuseiso** — 以普通用户身份挂载ISO文件系统

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **wiifuse** — 只读挂载 Gamecube 或 Wii DVD 镜像

	[http://wiibrew.org/wiki/Wiifuse](http://wiibrew.org/wiki/Wiifuse) || [wiifuse](https://aur.archlinux.org/packages/wiifuse/)

*   **xbfuse-git** — 挂载 Xbox (360) ISO 镜像

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — 将 XML 文件以目录树的形式挂载

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   **zfs-fuse** — [基于 FUSE 的 ZFS 支持](/index.php/ZFS_on_FUSE "ZFS on FUSE").

	[http://zfs-fuse.net/](http://zfs-fuse.net/) || [zfs-fuse](https://aur.archlinux.org/packages/zfs-fuse/)

请参考 [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace") 以获得更多信息。

## 创建文件系统

**注意:**

*   如果你想要改变分区划分，请参考 [分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")。
*   如果你想要创建一个交换分区，请参考 [Swap](/index.php/Swap "Swap")。

在开始前，你需要知道 Linux 给你的设备起了什么名字。硬盘和U盘使用 `/dev/sd*x*` 这样的名字，其中 *x* 是一个或多个小写字母。文件系统被命名为 `/dev/sd*xY*`，其中 *Y* 是一个数字。

通常来说，文件系统是在一个分区上创建的，不过也可以在逻辑容器如[LVM](/index.php/LVM "LVM")，[RAID](/index.php/RAID "RAID")，或者 [dm-crypt](/index.php/Dm-crypt "Dm-crypt") 上创建文件系统。

创建文件系统之前，目标分区必须处于未挂载状态。

如果你想要进行格式化的分区包含了一个已挂载的文件系统，在 lsblk 命令的 *MOUNTPOINT* 列中可以看到它。

```
$ lsblk

```

你可以使用 *umount* 加上分区的挂载点来卸载这个文件系统：

```
# umount /mountpoint

```

使用一下命令来创建一个 ext4 文件系统：

**警告:** 创建新文件系统之后，之前存放在该分区的数据会丢失且通常无法找回。请对你想要保留的数据做好备份。

```
# mkfs.ext4 /dev/*partition*

```

此外，你可以使用 `mkfs`。这是 `mkfs.*fstype*` 工具的统一入口。

```
# mkfs -t ext4 /dev/*partition*

```

## 参考资料

*   [wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems")