相关文章

*   [fstab](/index.php/Fstab "Fstab")
*   [分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")
*   [Mount](/index.php/Mount "Mount")
*   [tmpfs](/index.php/Tmpfs "Tmpfs")
*   [NFS](/index.php/NFS "NFS")
*   [Samba](/index.php/Samba "Samba")
*   [List of applications/Internet#Distributed file systems](/index.php/List_of_applications/Internet#Distributed_file_systems "List of applications/Internet")

**翻译状态：** 本文是英文页面 [File_Systems](/index.php/File_Systems "File Systems") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-09-01，点击[这里](https://wiki.archlinux.org/index.php?title=File_Systems&diff=0&oldid=448724)可以查看翻译后英文页面的改动。

根据 [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	*文件系统是数据组织方式，定义数据在磁盘上的保存、读取和更新方法。不同的文件系统可以根据存储设备的不同进行优化，提高效率*。

可以为每个磁盘分区设置一个或多个不同的文件系统。每种文件系统有自己的优缺点和独有特性。以下内容是目前所支持文件系统类型的概述。

## Contents

*   [1 文件系统类型](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E7.B1.BB.E5.9E.8B)
    *   [1.1 文件系统日志](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E6.97.A5.E5.BF.97)
*   [2 基于 FUSE 的文件系统支持](#.E5.9F.BA.E4.BA.8E_FUSE_.E7.9A.84.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E6.94.AF.E6.8C.81)
    *   [2.1 可叠加文件系统](#.E5.8F.AF.E5.8F.A0.E5.8A.A0.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [2.2 Read-only file systems](#Read-only_file_systems)
    *   [2.3 Clustered file systems](#Clustered_file_systems)
*   [3 查看现有文件系统](#.E6.9F.A5.E7.9C.8B.E7.8E.B0.E6.9C.89.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [4 创建文件系统](#.E5.88.9B.E5.BB.BA.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [5 Mount a file system](#Mount_a_file_system)
    *   [5.1 List mounted file systems](#List_mounted_file_systems)
    *   [5.2 卸载文件系统](#.E5.8D.B8.E8.BD.BD.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
*   [6 参阅](#.E5.8F.82.E9.98.85)

## 文件系统类型

[filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5) 包含一个简单介绍，详细比较参考 [w:Comparison_of_file_systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "w:Comparison of file systems"). 内核支持的文件系统可以通过 `/proc/filesystems` 查看。

| 文件系统 | 创建命令 | 工具 | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | 内核文档 [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | 说明 |
| [Btrfs](/index.php/Btrfs "Btrfs") | [mkfs.btrfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.btrfs.8) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Yes | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [稳定状态](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](/index.php/VFAT "VFAT") | [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Yes | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/exFAT "w:exFAT") | [mkexfatfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkexfatfs.8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Yes | N/A (FUSE-based) |
| [F2FS](/index.php/F2FS "F2FS") | [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Yes | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | 基于闪存的设备 |
| [ext3](/index.php/Ext3 "Ext3") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4 "Ext4") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "w:Hierarchical File System") | mkfs.hfsplus(8) | [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) | No | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | [macOS](https://en.wikipedia.org/wiki/macOS "w:macOS") 文件系统 |
| [JFS](/index.php/JFS "JFS") | [mkfs.jfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.jfs.8) | [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [jfs.txt](https://www.kernel.org/doc/Documentation/filesystems/jfs.txt) |
| [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") | [mkfs.nilfs2(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.nilfs2.8) | [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils) | Yes | [nilfs2.txt](https://www.kernel.org/doc/Documentation/filesystems/nilfs2.txt) |
| [NTFS](/index.php/NTFS "NTFS") | [mkfs.ntfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.ntfs.8) | [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | Yes | N/A (FUSE-based) | [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "w:Microsoft Windows") 文件系统 |
| [Reiser4](/index.php/Reiser4 "Reiser4") | mkfs.reiser4(8) | [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | No |
| [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "w:ReiserFS") | [mkfs.reiserfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.reiserfs.8) | [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) |
| [UDF](https://en.wikipedia.org/wiki/Universal_Disk_Format "w:Universal Disk Format") | [mkfs.udf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.udf.8) | [udftools](https://www.archlinux.org/packages/?name=udftools) | Optional | [udf.txt](https://www.kernel.org/doc/Documentation/filesystems/udf.txt) |
| [XFS](/index.php/XFS "XFS") | [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) | [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | 

[xfs.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs.txt)
[xfs-delayed-logging-design.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-delayed-logging-design.txt)
[xfs-self-describing-metadata.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt)

 |
| [ZFS](/index.php/ZFS "ZFS") | [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) | No | N/A ([OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "w:OpenZFS")移植) |

*   **[Btrfs](/index.php/Btrfs "Btrfs")** — 基于 B-tree 的文件系统，是"写入时进行复制(CoW)的 Linux 文件系统，支持的高级数据校验，增量备份，以及能同时提升性能并节省空间的透明压缩功能。Btrfs 已经是稳定的文件系统，被认为是 GNU/Linux 文件系统的未来，被所有主流发行版的安装程序设置为 root 分区文件系统选项。[[3]](https://btrfs.wiki.kernel.org/index.php/Main_Page#Stability_status)

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **[VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "wikipedia:File Allocation Table")** — **Virtual File Allocation Table（虚拟文件分配表）**。这种文件系统技术简单，受各种系统广泛支持。这种格式常用于固态存储卡，便于系统间文件交换。VFAT支持长文件名。

	[https://github.com/dosfstools/dosfstools](https://github.com/dosfstools/dosfstools) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **[exFAT](https://en.wikipedia.org/wiki/exFAT "w:exFAT")** — **为 Flash 磁盘优化的 Microsoft 文件系统。**。和 NTFS 一样，exFAT 可以通过将磁盘空间标记为“已分配”就为文件预分配磁盘空间。

	[https://github.com/relan/exfat](https://github.com/relan/exfat) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **[F2FS](/index.php/F2FS "F2FS")** — **Flash-Friendly File System**。由Samsung的Kim Jaegeuk（韩文：김재극）为Linux编写的适用于Flash设备的文件系统。F2FS的设计初衷是为了针对NAND闪存设备（包括SSD，eMMC和SD卡）的特性打造一个新的文件系统。这些设备目前在从移动设备到服务器的范畴内被广泛使用。

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **[ext](https://en.wikipedia.org/wiki/Extended_file_system "w:Extended file system")** — **Second Extended Filesystem**。古老、可靠的 GNU/Linux 文件系统。非常稳定，一个缺点是不支持日志记录或隔离。不支持日志会导致在突然断电或当机时可能导致数据丢失。因为文件系统检查的时间很长，**不适合**用于根 (`/`) 和 `/home` 分区。ext2 可以容易地[转换成 ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3")。**Third Extended Filesystem**。基于 ext2 系统, 并添加了日志记录功能。 ext3 向前兼容 ext2 ，非常成熟稳定。**Fourth Extended Filesystem**。一种新的文件系统，向前兼容 ext2 和 ext3 ，最大支持 1EB (1,048,576 TB) 分区，支持单个 16TB 的文件。子目录最大个数支持 64,000， ext3 只支持 32,000。支持在线碎片处理。

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **[HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "w:Hierarchical File System")** — **Hierarchical File System** 是苹果公司开发的专有文件系统，在 Mac OS 系统中使用.

	[http://www.opensource.apple.com](http://www.opensource.apple.com) || [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/)

*   **[JFS](/index.php/JFS "JFS")** — IBM 的**日志文件系统（ Journaled File System ）**。这是第一个支持日志的文件系统。它在 IBM AIX® 操作系统中开发了多年，然后被移植到GNU/Linux上。JFS 效率非常高并且 CPU 资源占用率比 GNU/Linux 上的其他任何一个文件系统都要低。并且在格式化、挂载和磁盘检测的时候都非常快，在各方面的表现都非常突出,尤其是与 deadline I/O 调度器结合。不如ext系列或者ReiserFS那样广泛支持，但非常成熟稳定。

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **[NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS")** — **New Implementation of a Log-structured File System**。由 NTT 开发。该文件系统将所有数据以连续的类似日志的结构储存，新数据只添加不改写。这种设计减少了寻址时间，相对传统的 Linux 文件系统能防止在崩溃发生后的数据丢失。

	[http://nilfs.sourceforge.net/](http://nilfs.sourceforge.net/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **[NTFS](/index.php/NTFS "NTFS")** — **Windows使用的文件系统**。 NTFS 相比 FAT 和 HPFS（High Performance File System）在技术作了若干改进，例如，支持元数据，并且使用了高级数据结构，以便于改善性能、可靠性和磁盘空间利用率，并提供了若干附加扩展功能，如访问控制列表和文件系统日志。

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **[Reiser4](/index.php/Reiser4 "Reiser4")** — **ReiserFS 的继任者**。由 Namesys 开发， DARPA 和 Linspire 赞助。使用 B*-tree 辅以 Dancing Tree，这样的机制使得稀疏的节点通常不会被合并，除非因为内存压力触发刷盘或对应的事务已经完成。这样的机制同时也保证了 Reiser4 在创建文件和目录的时候不需要浪费时间和Fixed Block（Such a system also allows Reiser4 to create files and directories without having to waste time and space through fixed blocks）。

	[https://reiser4.wiki.kernel.org/index.php/Main_Page](https://reiser4.wiki.kernel.org/index.php/Main_Page) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)

*   **[ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "w:ReiserFS")** — **Hans Reiser主持开发的高性能日志文件系统 ReiserFS(v3)**。使用一种非常独特有趣的数据存储检索方法。ReiserFS 效率非常高, 特别在处理很多小文件的时候更是如此。ReiserFS 格式化的时候很快，但在挂载的时候相对比较慢。性能稳定。 ReiserFS 现在的开发并不活跃(最新的版本是Reiser4)。通常是 `/var` 目录的好选择。

	[https://reiser4.wiki.kernel.org/index.php/Main_Page](https://reiser4.wiki.kernel.org/index.php/Main_Page) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **[XFS](/index.php/XFS "XFS")** — **由 Silicon Graphics 开发的历史悠久的日志文件系统**，最初是为 IRIX 操作系统开发，后来移植到 GNU/Linux。在处理大文件的时候能够提供高吞吐能力，格式化和挂载都非常快。对比测试显示 XFS 在处理数量较多的小文件时比较慢。 XFS 非常稳定，支持在线碎片整理。

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **[ZFS](/index.php/ZFS "ZFS")** — **由 Sun Microsystems 设计开发的文件系统和卷管理器综合体**。ZFS的特性包括数据错误保护，支持大容量存储（文件系统大小和单个文件大小支持16 EB，单个文件系统支持2个文件，zpool最大支持128 ZB），集成文件系统和卷管理，快照，写时拷贝，持续的完整性检查和自动修复，RAID-Z，原生 NFSV4 ACLs。

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/), [zfs-linux-git](https://aur.archlinux.org/packages/zfs-linux-git/)

**Note:** 内核中有 NTFS 驱动(参考[ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt))，但是文件写入支持很有限。

### 文件系统日志

以上除了 ext2 和 FAT16/32（即VFAT）以外的文件系统都支持[文件系统日志](https://en.wikipedia.org/wiki/zh:%E6%97%A5%E5%BF%97%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F "wikipedia:zh:日志文件系统")。文件系统日志通过在数据实际变更前写入日志记录变更来提供故障恢复能力。当出现系统崩溃或掉电故障的时候，这些文件系统能够更快的恢复到可用状态，并且在恢复过程中更不容易出现错误。文件系统日志将会占用文件系统中的一部分空间。

并非所有的文件系统日志技术都相同。ext3 和 ext4 提供 data-mode journaling，同时记录数据本身和元数据。由于对性能影响很大，这个功能默认是禁用的。其它文件系统仅提供记录元数据日志的ordered-mode journaling。尽管都能在系统崩溃后将系统返回正常状态，data-mode journaling 提供了最大程度的数据安全防护，但性能有所降低，因为数据会被写两次(第一次到日志，第二次到磁盘)。可以根据数据的重要性选择文件系统。

基于 copy-on-write 的文件系统比如 Btrfs 和 ZFS 不需要用传统的日志保护元数据，因为这些信息不会被原地更新。虽然 Btrfs 还在使用日志树，这个树仅仅是为了加快 fdatasync/fsync 的速度。

## 基于 FUSE 的文件系统支持

[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") （FUSE） 是 Unix 类操作系统中一种允许非特权用户在不修改内核代码的前提下创建自己的文件系统的一种机制。文件系统相关的代码会在*用户空间*运行，FUSE 内核模块仅仅是提供一个通往内核接口的“桥梁”。

一些基于 FUSE 的文件系统如下：

*   **acd-fuse** — FUSE filesystem driver for Amazon's Cloud Drive.

	[https://github.com/handyman5/acd_fuse](https://github.com/handyman5/acd_fuse) || [acdfuse-git](https://aur.archlinux.org/packages/acdfuse-git/)

*   **adbfs-git** — Android 设备文件系统挂载支持

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **cddfs** — 音乐 CD 挂载支持

	[http://castet.matthieu.free.fr/](http://castet.matthieu.free.fr/) || [cddfs](https://aur.archlinux.org/packages/cddfs/)

*   **fuseiso** — 以普通用户身份挂载ISO文件系统

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **vdfuse** — Mounting VirtualBox disk images (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

*   **wiifuse** — 只读挂载 Gamecube 或 Wii DVD 镜像

	[http://wiibrew.org/wiki/Wiifuse](http://wiibrew.org/wiki/Wiifuse) || [wiifuse](https://aur.archlinux.org/packages/wiifuse/)

*   **xbfuse-git** — 挂载 Xbox (360) ISO 镜像

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — 将 XML 文件以目录树的形式挂载

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   **zfs-fuse** — [基于 FUSE 的 ZFS 支持](/index.php/ZFS_on_FUSE "ZFS on FUSE").

	[http://zfs-fuse.net/](http://zfs-fuse.net/) || [zfs-fuse](https://aur.archlinux.org/packages/zfs-fuse/)

*   **[EncFS](/index.php/EncFS "EncFS")** — EncFS is a userspace stackable cryptographic file-system.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **[gitfs](/index.php/Gitfs "Gitfs")** — gitfs is a FUSE file system that fully integrates with git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

请参考 [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace") 以获得更多信息。

### 可叠加文件系统

*   **aufs** — Advanced Multi-layered Unification Filesystem, a FUSE based union filesystem, a complete rewrite of Unionfs, was rejected from Linux mainline and instead OverlayFS was merged into the Linux Kernel.

	[http://aufs.sourceforge.net](http://aufs.sourceforge.net) || [aufs](https://aur.archlinux.org/packages/aufs/)

*   **[eCryptfs](/index.php/ECryptfs "ECryptfs")** — The Enterprise Cryptographic Filesystem is a package of disk encryption software for Linux. It is implemented as a POSIX-compliant filesystem-level encryption layer, aiming to offer functionality similar to that of GnuPG at the operating system level.

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **mergerfs** — a FUSE based union filesystem.

	[https://github.com/trapexit/mergerfs](https://github.com/trapexit/mergerfs) || [mergerfs](https://aur.archlinux.org/packages/mergerfs/)

*   **mhddfs** — Multi-HDD FUSE filesystem, a FUSE based union filesystem.

	[http://mhddfs.uvw.ru](http://mhddfs.uvw.ru) || [mhddfs](https://aur.archlinux.org/packages/mhddfs/)

*   **[overlayfs](/index.php/Overlayfs "Overlayfs")** — OverlayFS is a filesystem service for Linux which implements a union mount for other file systems.

	[https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **Unionfs** — Unionfs is a filesystem service for Linux, FreeBSD and NetBSD which implements a union mount for other file systems.

	[http://unionfs.filesystems.org/](http://unionfs.filesystems.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **unionfs-fuse** — A user space Unionfs implementation.

	[https://github.com/rpodgorny/unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) || [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)

### Read-only file systems

*   **[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")** — SquashFS is a compressed read only filesystem. SquashFS compresses files, inodes and directories, and supports block sizes up to 1 MB for greater compression.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

### Clustered file systems

*   **[Ceph](/index.php/Ceph "Ceph")** — Unified, distributed storage system designed for excellent performance, reliability and scalability.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **[Glusterfs](/index.php/Glusterfs "Glusterfs")** — Cluster file system capable of scaling to several peta-bytes.

	[https://www.gluster.org/](https://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **[IPFS](/index.php/IPFS "IPFS")** — A peer-to-peer hypermedia protocol to make the web faster, safer, and more open. IPFS aims replace HTTP and build a better web for all of us. Uses blocks to store parts of a file, each network node stores only content it is interested, provides deduplication, distribution, scalable system limited only by users. (currently in aplha)

	[https://ipfs.io/](https://ipfs.io/) || [go-ipfs](https://www.archlinux.org/packages/?name=go-ipfs)

*   **[MooseFS](https://en.wikipedia.org/wiki/MooseFS "wikipedia:MooseFS")** — MooseFS is a fault tolerant, highly available and high performance scale-out network distributed file system.

	[https://moosefs.com](https://moosefs.com) || [moosefs](https://www.archlinux.org/packages/?name=moosefs)

*   **[OpenAFS](/index.php/OpenAFS "OpenAFS")** — Open source implementation of the AFS distributed file system

	[http://www.openafs.org](http://www.openafs.org) || [openafs](https://aur.archlinux.org/packages/openafs/)

*   **[OrangeFS](https://en.wikipedia.org/wiki/OrangeFS "wikipedia:OrangeFS")** — OrangeFS is a scale-out network file system designed for transparently accessing multi-server-based disk storage, in parallel. Has optimized MPI-IO support for parallel and distributed applications. Simplifies the use of parallel storage not only for Linux clients, but also for Windows, Hadoop, and WebDAV. POSIX-compatible. Part of Linux kernel since version 4.6\.

	[http://www.orangefs.org/](http://www.orangefs.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Sheepdog** — Distributed object storage system for volume and container services and manages the disks and nodes intelligently.

	[https://sheepdog.github.io/sheepdog/](https://sheepdog.github.io/sheepdog/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

## 查看现有文件系统

To identify existing file systems, you can use [lsblk](/index.php/Lsblk "Lsblk"):

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb                                                          
└─sdb1 vfat   Transcend 4A3C-A9E9
```

An existing file system, if present, will be shown in the `FSTYPE` column. If [mounted](/index.php/Mount "Mount"), it will appear in the `MOUNTPOINT` column.

## 创建文件系统

首先，确认系统的安装位置，可以创建在一个分区上、逻辑容器如[LVM](/index.php/LVM "LVM")，[RAID](/index.php/RAID "RAID")，或者 [dm-crypt](/index.php/Dm-crypt "Dm-crypt") 上或普通文件上(参考 [Wikipedia:Loop device](https://en.wikipedia.org/wiki/Loop_device "wikipedia:Loop device"))。这里描述创建在分区上的情况。

**Warning:**

*   创建新文件系统之后，之前存放在该分区的数据会丢失且通常无法找回。**请备份所有要保留的数据**.
*   The purpose of a given partition may restrict the choice of file system. For example, an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") must contain a [FAT32](/index.php/FAT32 "FAT32") (`mkfs.vfat`) file system, and the file system containing the `/boot` directory must be supported by the [boot loader](/index.php/Boot_loader "Boot loader").

创建文件系统之前，目标分区必须处于未挂载状态。如果你要格式化的分区包含了一个已挂载的文件系统，在 [lsblk](/index.php/Lsblk "Lsblk") 命令的 *MOUNTPOINT* 列中可以看到它。

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1                      C4DA-2C4D                            
├─sda2 ext4                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 /mnt
└─sda3                      56adc99b-a61e-46af-aab7-a6d07e504652 

```

你可以使用 *umount* 加上分区的挂载点来卸载这个文件系统：

```
# umount /mountpoint

```

使用一下命令来创建一个 *fstype* 文件系统：

```
# mkfs.*fstype* /dev/*partition*

```

此外，你可以使用 `mkfs`。这是 `mkfs.*fstype*` 工具的统一入口。

```
# mkfs -t ext4 /dev/*partition*

```

**Tip:**

*   Use the `-L` flag of *mkfs.ext4* to specify a [file system label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming"). *e2label* can be used to change the label on an existing file system.
*   File systems may be *resized* after creation, with certain limitations. For example, an [XFS](/index.php/XFS "XFS") filesystem's size can be increased, but it cannot reduced. See [Resize capabilities](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Resize_capabilities "w:Comparison of file systems") and the respective file system documentation for details.

The new file system can now be mounted to a directory of choice.

## Mount a file system

To manually mount filesystem located on a device (e.g., a partition) to a directory, use [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8). This example mounts `/dev/sda1` to `/mnt`.

```
# mount /dev/sda1 /mnt

```

This attaches the filesystem on `/dev/sda1` at the directory `/mnt`, making the contents of the filesystem visible. Any data that existed at `/mnt` before this action is made invisible until the device is unmounted.

[fstab](/index.php/Fstab "Fstab") contains information on how devices should be automatically mounted if present. See the [fstab](/index.php/Fstab "Fstab") article for more information on how to modify this behavior.

If a device is specified in `/etc/fstab` and only the device or mount point is given on the command line, that information will be used in mounting. For example, if `/etc/fstab` contains a line indicating that `/dev/sda1` should be mounted to `/mnt`, then the following will automatically mount the device to that location:

```
# mount /dev/sda1

```

Or

```
# mount /mnt

```

*mount* contains several options, many of which depend on the file system specified. The options can be changed, either by:

*   using flags on the command line with *mount*
*   editing [fstab](/index.php/Fstab "Fstab")
*   creating [udev](/index.php/Udev "Udev") rules
*   [compiling the kernel yourself](/index.php/Arch_Build_System "Arch Build System")
*   or using filesystem-specific mount scripts (located at `/usr/bin/mount.*`).

See these related articles and the article of the filesystem of interest for more information.

### List mounted file systems

To list all mounted file systems, use [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8):

```
$ findmnt

```

*findmnt* takes a variety of arguments which can filter the output and show additional information. For example, it can take a device or mount point as an argument to show only information on what is specified:

```
$ findmnt /dev/sda1

```

*findmnt* gathers information from `/etc/fstab`, `/etc/mtab`, and `/proc/self/mounts`.

### 卸载文件系统

To unmount a file system use [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8). Either the device containing the file system (e.g., `/dev/sda1`) or the mount point (e.g., `/mnt`) can be specified:

```
# umount /dev/sda1

```

Or

```
# umount /mnt

```

## 参阅

*   [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5)
*   [Documentation of file systems supported by linux](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Wikipedia:File systems](https://en.wikipedia.org/wiki/File_systems "wikipedia:File systems")
*   [Wikipedia:Mount (Unix)](https://en.wikipedia.org/wiki/Mount_(Unix) "wikipedia:Mount (Unix)")