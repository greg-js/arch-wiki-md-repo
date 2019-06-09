相关文章

*   [分区](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")
*   [Device file#lsblk](/index.php/Device_file#lsblk "Device file")
*   [File permissions and attributes (简体中文)](/index.php/File_permissions_and_attributes_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "File permissions and attributes (简体中文)")
*   [fsck](/index.php/Fsck "Fsck")
*   [fstab (简体中文)](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")
*   [List of applications (简体中文)#挂载](/index.php/List_of_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#挂载 "List of applications (简体中文)")
*   [QEMU#Mounting a partition inside a raw disk image](/index.php/QEMU#Mounting_a_partition_inside_a_raw_disk_image "QEMU")
*   [udev (简体中文)](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")
*   [udisks (简体中文)](/index.php/Udisks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udisks (简体中文)")
*   [umask](/index.php/Umask "Umask")
*   [USB storage devices](/index.php/USB_storage_devices "USB storage devices")

**翻译状态：** 本文是英文页面 [File_Systems](/index.php/File_Systems "File Systems") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-04-19，点击[这里](https://wiki.archlinux.org/index.php?title=File_Systems&diff=0&oldid=571607)可以查看翻译后英文页面的改动。

根据 [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	文件系统控制数据的读和写。如果没有文件系统，储存介质里的信息就会变成一块无法理解的数据。通过把数据分块、命名，不同的信息就可以被隔离、分辨。每组数据被命名为“文件”是取自纸质信息系统的命名方式。而“文件系统”是指用于管理信息的分组和命名的结构和逻辑规则。

文件系统有很多，每个磁盘分区可以而且只可以使用其中的某一个。每种文件系统有自己的优缺点和独有特性。以下内容是目前所支持的文件系统类型的概述，相应的维基链接提供更加详细的信息。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 文件系统类型](#文件系统类型)
    *   [1.1 文件系统日志](#文件系统日志)
    *   [1.2 基于 FUSE 的文件系统](#基于_FUSE_的文件系统)
    *   [1.3 堆栈式文件系统](#堆栈式文件系统)
    *   [1.4 只读文件系统](#只读文件系统)
    *   [1.5 集群文件系统](#集群文件系统)
*   [2 查看现有文件系统](#查看现有文件系统)
*   [3 创建文件系统](#创建文件系统)
*   [4 挂载文件系统](#挂载文件系统)
    *   [4.1 列出挂载的文件系统](#列出挂载的文件系统)
    *   [4.2 卸载文件系统](#卸载文件系统)
*   [5 参阅](#参阅)

## 文件系统类型

[filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5) 包含一个简单介绍，详细比较参考 [Wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems")。 内核支持的文件系统可以通过 `/proc/filesystems` 查看。

| 文件系统 | 创建命令 | 工具 | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | 内核文档 [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | 说明 |
| [Btrfs](/index.php/Btrfs "Btrfs") | [mkfs.btrfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.btrfs.8) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Yes | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [可靠性](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](/index.php/VFAT "VFAT") | [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Yes | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/exFAT "w:exFAT") | [mkexfatfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkexfatfs.8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Yes | N/A (FUSE-based) |
| [F2FS](/index.php/F2FS "F2FS") | [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Yes | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | 基于闪存的设备 |
| [ext3](/index.php/Ext3 "Ext3") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4 "Ext4") | [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "w:Hierarchical File System") | mkfs.hfsplus(8) | [hfsprogs](https://aur.archlinux.org/packages/hfsprogs/) | No | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | [macOS](https://en.wikipedia.org/wiki/macOS "w:macOS") (8.x-10.12.x) 文件系统 |
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
| [ZFS](/index.php/ZFS "ZFS") | [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) | No | N/A ([OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "w:OpenZFS") 移植) |

**Note:** 内核中有 NTFS 驱动(参考[ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt))，但是文件写入支持很有限。

### 文件系统日志

以上除了 ext2 、FAT16/32（即VFAT）、Reiser4（可选开启）、Btrfs 和 ZFS 以外的文件系统都使用[文件系统日志](https://en.wikipedia.org/wiki/zh:%E6%97%A5%E5%BF%97%E6%96%87%E4%BB%B6%E7%B3%BB%E7%BB%9F "wikipedia:zh:日志文件系统")。文件系统日志通过在数据更改写入储存设备前把变更写入日志来提供故障恢复能力。当出现系统崩溃或电源故障的时候，这些文件系统能够更快的恢复到可用状态，并且在恢复过程中更不容易出现错误。日志活动在文件系统中专用的一部分空间里进行。

并非所有的日志技术都相同。ext3 和 ext4 提供 data-mode journaling，同时记录数据本身和元数据（也有可以只记录元数据变化）。这个模式对性能影响很大，默认是禁用的。

与此类似，[Reiser4](/index.php/Reiser4 "Reiser4") 的名为 ["transaction models"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models) 的模式不仅改变了它所提供的功能，也改变了它的日志模式。这种日志记录模式使用了特别的日志技术，[wandering logs](https://reiser4.wiki.kernel.org/index.php/V4#Wandering_Logs)，来确定使用哪种写入策略：写入储存器两次； **write-anywhere**，纯粹的 copy-on-write（和 btrfs 的类似，不过用的是另一种树设计）；**hybrid**，在前两种之间智能切换。

**注意:** Reiser4 通过 **node41** 插件提供类似 ext4 的只记录元数据的日志模式，同时这个插件还实现了元数据和内联校验和，并且可根据其挂载的时候所选择的 transaction model 来确定它所提供的 wandering logs 行为。

其它文件系统提供仅提供记录元数据日志的 ordered-mode journaling。尽管都能在崩溃后将文件系统恢复到正常状态，data-mode journaling 提供了最大程度的数据安全防护，但代价是性能有所降低，因为数据会被写两次(第一次到日志，第二次到磁盘)——而 Reiser4 通过 “wandering logs" 避免了这样的重复。可以根据数据的重要性选择文件系统。

Reiser4 是仅有的被设计成所有的操作都是完全 atomic 的同时还提供元数据和内联数据的校验和的文件系统——文件操作要么完全完成，要么就根本没有发生，所以不会因为操作执行到一半而导致数据损坏。因此它发生数据丢失的可能性相比其他文件系统要低得多。

基于 copy-on-write （也叫 write-anywhere）的文件系统，比如Reiser4、Btrfs 和 ZFS 不需要用传统的日志保护元数据，因为元数据永远不会被原地更新。虽然 Btrfs 还在使用日志树，但这个树仅仅是为了加快 fdatasync/fsync 的速度。

### 基于 FUSE 的文件系统

参考 [FUSE](/index.php/FUSE "FUSE")。

### 堆栈式文件系统

*   **aufs** — Advanced Multi-layered Unification Filesystem, 基于 FUSE 的联合文件系统（union filesystem）, 完全重构版本的 Unionfs, 但是被 Linux mainline 拒绝merge（而OverlayFS 进入了 Linux Kernel）

	[http://aufs.sourceforge.net](http://aufs.sourceforge.net) || [aufs](https://aur.archlinux.org/packages/aufs/)

*   **[eCryptfs](/index.php/ECryptfs "ECryptfs")** — The Enterprise Cryptographic Filesystem，一个 Linux 磁盘加密软件。它被设计为与POSIX兼容的文件系统级加密层，目标是在操作系统级别提供类似 GnuPG 的功能。

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **mergerfs** — 基于 FUSE 的联合文件系统。

	[https://github.com/trapexit/mergerfs](https://github.com/trapexit/mergerfs) || [mergerfs](https://aur.archlinux.org/packages/mergerfs/)

*   **mhddfs** — 多机械硬盘 FUSE 文件系统, 基于 FUSE 的联合文件系统。

	[http://mhddfs.uvw.ru](http://mhddfs.uvw.ru) || [mhddfs](https://aur.archlinux.org/packages/mhddfs/)

*   **[overlayfs](/index.php/Overlayfs "Overlayfs")** — OverlayFS 是为 Linux 设计的联合文件系统服务，实现了联合挂载其他文件系统的功能。

	[https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt](https://www.kernel.org/doc/Documentation/filesystems/overlayfs.txt) || [linux](https://www.archlinux.org/packages/?name=linux)

*   Unionfs：为 Linux、FreeBSD and NetBSD 设计的文件系统服务, 实现了联合挂载其他文件系统的功能。[[3]](http://unionfs.filesystems.org/)

*   **unionfs-fuse** — Unionfs 的用户空间实现.

	[https://github.com/rpodgorny/unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) || [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)

### 只读文件系统

*   **[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")** — SquashFS 是一个压缩的只读文件系统，它压缩文件、inodes和目录，而且最高支持 1 MB 大小的 block 来实现更强力的压缩。

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

### 集群文件系统

*   **[Ceph](/index.php/Ceph "Ceph")** — 统一的分布式存储系统，旨在实现出色的性能，可靠性和可扩展性。

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **[Glusterfs](/index.php/Glusterfs "Glusterfs")** — 支持扩展到几PB的集群文件系统。

	[https://www.gluster.org/](https://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **[IPFS](/index.php/IPFS "IPFS")** — 一种点对点超媒体协议，使网络更快，更安全，更开放。 IPFS旨在取代HTTP并为我们所有人构建更好的网络。 它使用 block 来存储文件的一部分，每个网络节点仅存储它感兴趣的内容，提供去重的、分布式的可扩展文件系统。 (alpha阶段)

	[https://ipfs.io/](https://ipfs.io/) || [go-ipfs](https://www.archlinux.org/packages/?name=go-ipfs)

*   **[MooseFS](https://en.wikipedia.org/wiki/MooseFS "wikipedia:MooseFS")** — MooseFS 是一个容错、高可用性和高性能的向外扩展的扩展网络分布式文件系统。

	[https://moosefs.com](https://moosefs.com) || [moosefs](https://www.archlinux.org/packages/?name=moosefs)

*   **[OpenAFS](/index.php/OpenAFS "OpenAFS")** — AFS分布式文件系统的开源实现

	[http://www.openafs.org](http://www.openafs.org) || [openafs](https://aur.archlinux.org/packages/openafs/)

*   [OrangeFS](https://en.wikipedia.org/wiki/OrangeFS "wikipedia:OrangeFS")：OrangeFS 是一个向外扩展的网络文件系统，为透明、并行地访问基于多个服务器的磁盘储存而设计。它为并行分布式应用提供了优化的 MPI-IO。它使 Linux 客户端、Windows、Hadoop 和 WebDAV 使用并列储存器变得简便。它与POSIX兼容，而且是 Linux kernel （4.6+）的一部分。[[4]](http://www.orangefs.org/)
*   Sheepdog：用于卷和容器服务的分布式对象存储系统，能智能地管理磁盘和节点。[[5]](https://sheepdog.github.io/sheepdog/)
*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem 是一个免费、开放、安全、去中心化、容错、点对点的分布式 data store 和分布式文件系统。

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

## 查看现有文件系统

用 [lsblk](/index.php/Lsblk "Lsblk") 查看:

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb                                                          
└─sdb1 vfat   Transcend 4A3C-A9E9
```

如果文件系统存在，那 `FSTYPE` 列会显示它的名字；如果它被[mount](/index.php/Mount "Mount")了，挂载点会显示在 `MOUNTPOINT` 那一列。

## 创建文件系统

文件系统可以创建在一个分区上、逻辑容器如 [LVM](/index.php/LVM "LVM")，[RAID](/index.php/RAID "RAID")，或者 [dm-crypt](/index.php/Dm-crypt "Dm-crypt") 上或普通文件上(参考 [Loop设备](https://en.wikipedia.org/wiki/zh:Loop_device "w:zh:Loop device"))。这里描述创建在分区上的情况。

**注意:** 文件系统可以直接写入到设备上，这样的设备叫做 *superfloppy* 或者 [无分区磁盘](/index.php/Partitioning#Partitionless_disk "Partitioning")。这样做会带来一些约束，特别是用它来 [启动](/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch boot process (简体中文)") 系统。

**警告:**

*   创建新文件系统之后，之前存放在该分区的数据会丢失且通常无法找回。**请备份所有要保留的数据**.
*   某个分区用来干什么通常会限制能用什么文件系统，比如 [EFI分区](/index.php/EFI_system_partition "EFI system partition") 就只能用 `mkfs.vfat` 创建的 [FAT32](/index.php/FAT32 "FAT32")，而包含 `/boot` 的分区的文件系统要考虑 [boot loader](/index.php/Arch_boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#启动加载器 "Arch boot process (简体中文)") 是否支持。

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

查看挂载了的所有文件系统，参考[#列出挂载的文件系统](#列出挂载的文件系统)。

用 [mkfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.8) 创建新的文件系统，类型参见[#文件系统类型](#文件系统类型)。如果安装了其他特殊的工具，按照它们的说明来做。比如，以下命令在 `/dev/sda1` 上创建了一个 [ext4](/index.php/Ext4 "Ext4") 文件系统：

```
# mkfs.ext4 /dev/sda1

```

此外，你可以使用 `mkfs`。这是 `mkfs.*fstype*` 工具的统一入口。上面的命令等价于：

```
# mkfs -t ext4 /dev/sda1

```

**Tip:**

*   用 `mkfs.ext4` 的时候可以用 `-L` 选项来给文件系统设置一个 [标签](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming")。`e2label` 用来对已经存在的文件系统改标签。
*   文件系统在创建之后是有条件地 *改变大小*（resized）的。比如 [XFS](/index.php/XFS "XFS") 可以扩容，但是不能缩小。参考 [Resize capabilities](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Resize_capabilities "w:Comparison of file systems")。

创建完成之后新的文件系统就可以挂载到某个目录了。

## 挂载文件系统

如果要手动挂载一个设备上的文件系统到某个目录，用 [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)。下面这个例子把 `/dev/sda1` 挂载到 `/mnt`：

```
# mount /dev/sda1 /mnt

```

挂载之后，在 `/mnt` 下面就能看见 `/dev/sda1` 里面的内容。挂载之前 `/mnt` 文件夹里的内容在挂载之后将会变得不可见，直到 unmount 掉 `/dev/sda1`。

[fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)") 描述了如果某个设备存在的话系统应该怎么自动挂载它。如果要修改 `/etc/fstab`，请阅读 [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")。

如果 `/etc/fstab` 里描述了一个设备的挂载参数，而用 `mount` 时只给了设备名字或者挂载点，*fstab* 里的参数就会自动补上。比如，`/etc/fstab` 里指示 `/dev/sda1` 应该挂载到 `/mnt`，那下面的命令就会把 `/dev/sda1` 挂载到 `/mnt`，即使你没有显式指明：

```
# mount /dev/sda1

```

或者

```
# mount /mnt

```

*mount* 接受很多参数，这些参数依赖于文件系统是否支持。要改变这些参数的话，可以通过以下形式：

*   `mount ... ... **-o** *options*`
*   修改 [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")
*   创建 [udev 规则](/index.php/Udev#Mounting_drives_in_rules "Udev")
*   使用针对不同文件系统的 mount 脚本（`/usr/bin/mount.*`）
*   [自己编译内核](/index.php/Kernels/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels/Arch Build System (简体中文)")

### 列出挂载的文件系统

用 [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8) :

```
$ findmnt

```

*findmnt* 支持很多参数，可以利用它们来筛选输出或者获得更多信息。比如把某个挂载点或者设备作为参数，它就会只输出这个下面挂载了什么。

```
$ findmnt /dev/sda1

```

*findmnt* 从 `/etc/fstab`、`/etc/mtab` 和 `/proc/self/mounts` 文件里收集信息。

### 卸载文件系统

用 [umount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/umount.8) 来卸载文件系统。参数可以是包含文件系统的设备（比如`/dev/sda1`），也可以是挂载点（比如`/mnt`）：

```
# umount /dev/sda1

```

或者

```
# umount /mnt

```

## 参阅

*   [filesystems(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/filesystems.5)
*   [systemd-mount(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-mount.1)
*   [Documentation of file systems supported by linux](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Wikipedia:File systems](https://en.wikipedia.org/wiki/File_systems "wikipedia:File systems")
*   [Wikipedia:Mount (Unix)](https://en.wikipedia.org/wiki/Mount_(Unix) "wikipedia:Mount (Unix)")