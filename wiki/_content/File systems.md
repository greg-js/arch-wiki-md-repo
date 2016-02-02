# File systems

From [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	_A file system (or filesystem) is a means to organize data expected to be retained after a program terminates by providing procedures to store, retrieve and update data, as well as manage the available space on the device(s) which contain it. A file system organizes data in an efficient manner and is tuned to the specific characteristics of the device._

Individual drive partitions can be setup using one of the many different available filesystems. Each has its own advantages, disadvantages, and unique idiosyncrasies. A brief overview of supported filesystems follows; the links are to Wikipedia pages that provide much more information.

Before being formatted, a drive should be [partitioned](/index.php/Partitioning "Partitioning").

## Contents

*   [1 Types of file systems](#Types_of_file_systems)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 Arch Linux support](#Arch_Linux_support)
    *   [1.3 FUSE-based file systems](#FUSE-based_file_systems)
*   [2 Create a filesystem](#Create_a_filesystem)
*   [3 See also](#See_also)

## Types of file systems

*   [Btrfs](/index.php/Btrfs "Btrfs") — Also known as "Better FS", is a **new filesystem with powerful features similar to Sun/Oracle's excellent ZFS**. These include snapshots, multi-disk striping and mirroring (software RAID without mdadm), checksums, incremental backup, and on-the-fly compression that can give a significant performance boost as well as save space. Although it has been merged into the mainline kernel, as of April 2014, Btrfs is not considered stable, with an experimental status. Btrfs appears to be the future of GNU/Linux filesystems and is offered as a root filesystem option in all major distribution installers.
*   **exFAT** — **Microsoft file system optimized for flash drives**. Like NTFS, exFAT can pre-allocate disk space for a file by just marking arbitrary space on disk as 'allocated'.
*   [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") — **Second Extended Filesystem** is an established, mature GNU/Linux filesystem that is very stable. A drawback is that it does not have journaling support or barriers. Lack of journaling can result in data loss in the event of a power failure or system crash. It may also be **not** convenient for root (`/`) and `/home` partitions because file-system checks can take a long time. An ext2 filesystem can be [converted to ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3").
*   [ext3](/index.php/Ext3 "Ext3") — **Third Extended Filesystem** is essentially the ext2 system with journaling support and write barriers. It is backward compatible with ext2, well tested, and extremely stable.
*   [ext4](/index.php/Ext4 "Ext4") — **Fourth Extended Filesystem** is a newer filesystem that is also compatible with ext2 and ext3\. It provides support for volumes with sizes up to 1 exabyte (i.e. 1,048,576 terabytes) and files sizes up to 16 terabytes. It increases the 32,000 subdirectory limit in ext3 to unlimited. It also offers online defragmentation capability.
*   [F2FS](/index.php/F2FS "F2FS") — **Flash-Friendly File System** is a flash file system created by Kim Jaegeuk (Hangul: 김재극) at Samsung for the Linux operating system kernel. The motivation for F2FS was to build a file system that from the start takes into account the characteristics of NAND flash memory-based storage devices (such as solid-state disks, eMMC, and SD cards), which have been widely being used in computer systems ranging from mobile devices to servers.
*   [HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "wikipedia:Hierarchical File System") — **Hierarchical File System** is a proprietary file system developed by Apple Inc. for use in computer systems running Mac OS.
*   [JFS](/index.php/JFS "JFS") — IBM's **Journaled File System** was the first filesystem to offer journaling. It had many years of development in the IBM AIX® operating system before being ported to GNU/Linux. JFS makes the smallest demand on CPU resources of any GNU/Linux filesystem. It is very fast at formatting, mounting, and filesystem checks (fsck). JFS offers very good all-around performance especially in conjunction with the deadline I/O scheduler. It is not as widely supported as the ext series or ReiserFS, but still very mature and stable.
*   [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") — **New Implementation of a Log-structured File System** was developed by NTT. It records all data in a continuous log-like format that is only appended to and never overwritten. It is designed to reduce seek times and minimize the type of data loss that occurs after a crash with conventional Linux filesystems.
*   [NTFS](/index.php/NTFS "NTFS") — **File system used by Windows**. NTFS has several technical improvements over FAT and HPFS (High Performance File System), such as improved support for metadata, and the use of advanced data structures to improve performance, reliability, and disk space utilization, plus additional extensions, such as security access control lists (ACL) and file system journaling.
*   [Reiser4](/index.php/Reiser4 "Reiser4") — **Successor to the ReiserFS file system**, developed from scratch by Namesys and sponsored by DARPA as well as Linspire, it uses B*-trees in conjunction with the dancing tree balancing approach, in which underpopulated nodes will not be merged until a flush to disk except under memory pressure or when a transaction completes. Such a system also allows Reiser4 to create files and directories without having to waste time and space through fixed blocks.
*   [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") — **Hans Reiser's high-performance journaling FS (v3)** uses a very interesting method of data throughput based on an unconventional and creative algorithm. ReiserFS is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. Quite mature and stable. ReiserFSv3 is not being actively developed at this time. Generally regarded as a good choice for `/var`.
*   [VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "wikipedia:File Allocation Table") — **Virtual File Allocation Table** is technically simple and supported by virtually all existing operating systems. This makes it a useful format for solid-state memory cards and a convenient way to share data between operating systems. VFAT supports long file names.
*   [XFS](/index.php/XFS "XFS") — **Early journaling filesystem originally developed by Silicon Graphics** for the IRIX operating system and ported to GNU/Linux. It provides very fast throughput on large files and filesystems and is very fast at formatting and mounting. Comparative benchmark testing has shown it to be slower when dealing with many small files. XFS is very mature and offers online defragmentation capability.
*   [ZFS](/index.php/ZFS "ZFS") — **Combined file system and logical volume manager designed by Sun Microsystems**. The features of ZFS include protection against data corruption, support for high storage capacities, integration of the concepts of filesystem and volume management, snapshots and copy-on-write clones, continuous integrity checking and automatic repair, RAID-Z and native NFSv4 ACLs.

### Journaling

All the above filesystems with the exception of ext2, FAT16/32, use [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling provides fault-resilience by logging changes before they are committed to the filesystem. In the event of a system crash or power failure, such file systems are faster to bring back online and less likely to become corrupted. The logging takes place in a dedicated area of the filesystem.

Not all journaling techniques are the same. Ext3 and ext4 offer data-mode journaling, which logs both data and meta-data, as well as possibility to journal only meta-data changes. Data-mode journaling comes with a speed penalty and is not enabled by default. In the same vein, [Reiser4](/index.php/Reiser4 "Reiser4") offers so-called ["transaction models"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models), which include pure journaling (equivalent to ext4's data-mode journaling), pure Copy-on-Write approach (equivalent to btrfs' default) and a combined approach which heuristically alternates between the two former. _It should be noted that reiser4 does not provide an equivalent to ext4's default journaling behavior (meta-data only)._

The other filesystems provide ordered-mode journaling, which only logs meta-data. While all journaling will return a filesystem to a valid state after a crash, data-mode journaling offers the greatest protection against corruption and data loss. There is a compromise in system performance, however, because data-mode journaling does two write operations: first to the journal and then to the disk. The trade-off between system speed and data safety should be considered when choosing the filesystem type.

### Arch Linux support

*   **btrfs-progs** — [Btrfs](/index.php/Btrfs "Btrfs") support.

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **dosfstools** — VFAT support.

	[https://github.com/dosfstools/dosfstools](https://github.com/dosfstools/dosfstools) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **exfat-utils** — exFAT support.

	[https://github.com/relan/exfat](https://github.com/relan/exfat) || [fuse-exfat](https://www.archlinux.org/packages/?name=fuse-exfat), [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **f2fs-tools** — [F2FS](/index.php/F2FS "F2FS") support.

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **e2fsprogs** — ext2, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4") support.

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **hfsprogs** — HFS support.

	[http://www.opensource.apple.com](http://www.opensource.apple.com) || [hfsprogs](https://www.archlinux.org/packages/?name=hfsprogs)

*   **jfsutils** — [JFS](/index.php/JFS "JFS") support.

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **nilfs-utils** — NILFS support.

	[http://nilfs.sourceforge.net/](http://nilfs.sourceforge.net/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **ntfs-3g** — [NTFS](/index.php/NTFS "NTFS") support.

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **reiser4progs** — [ReiserFSv4](/index.php/Reiser4 "Reiser4") support.

	[http://sourceforge.net/projects/reiser4/](http://sourceforge.net/projects/reiser4/) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)<sup><small>AUR</small></sup>

*   **reiserfsprogs** — ReiserFSv3 support.

	[https://www.kernel.org/](https://www.kernel.org/) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **xfsprogs** — [XFS](/index.php/XFS "XFS") support.

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **zfs** — [ZFS](/index.php/ZFS "ZFS") support.

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs-git](https://aur.archlinux.org/packages/zfs-git/)<sup><small>AUR</small></sup>

### FUSE-based file systems

[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (FUSE) is a mechanism for Unix-like operating systems that lets non-privileged users create their own file systems without editing kernel code. This is achieved by running file system code in _user space_, while the FUSE kernel module provides only a "bridge" to the actual kernel interfaces.

Some FUSE-based file systems:

*   **acd-fuse** — FUSE filesystem driver for Amazon's Cloud Drive.

	[https://github.com/handyman5/acd_fuse](https://github.com/handyman5/acd_fuse) || [acdfuse-git](https://aur.archlinux.org/packages/acdfuse-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/acdfuse-git)]</sup>

*   **adbfs-git** — Mount an Android device filesystem.

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)<sup><small>AUR</small></sup>

*   **cddfs** — Mount audio CDs.

	[http://castet.matthieu.free.fr/](http://castet.matthieu.free.fr/) || [cddfs](https://aur.archlinux.org/packages/cddfs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cddfs)]</sup>

*   **fuse-exfat** — exFAT mount support.

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [fuse-exfat](https://www.archlinux.org/packages/?name=fuse-exfat)

*   **fuseiso** — Mount an ISO as a regular user.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **vdfuse** — Mounting VirtualBox disk images (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)<sup><small>AUR</small></sup>

*   **wiifuse** — Mount a Gamecube or Wii DVD disc image read-only.

	[http://wiibrew.org/wiki/Wiifuse](http://wiibrew.org/wiki/Wiifuse) || [wiifuse](https://aur.archlinux.org/packages/wiifuse/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/wiifuse)]</sup>

*   **xbfuse-git** — Mount an Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xbfuse-git)]</sup>

*   **xmlfs** — Represent an XML file as a directory structure for easy access.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)<sup><small>AUR</small></sup>

*   **zfs-fuse** — [ZFS support via FUSE](/index.php/ZFS_on_FUSE "ZFS on FUSE").

	[http://zfs-fuse.net/](http://zfs-fuse.net/) || [zfs-fuse](https://aur.archlinux.org/packages/zfs-fuse/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/zfs-fuse)]</sup>

See [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace") for more.

## Create a filesystem

**Note:**

*   If you want to change the partition layout, see [Partitioning](/index.php/Partitioning "Partitioning").
*   If you want to create a swap partition, see [Swap](/index.php/Swap "Swap").

Before starting, you need to know which name Linux gave to your device. Hard drives and USB sticks show up as `/dev/sd_x_`, where _x_ is a lowercase letter, while partitions show up as `/dev/sd_xY_`, where _Y_ is a number.

Usually filesystems are created on a partition, but they can also be created inside of logical containers like [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID"), or [dm-crypt](/index.php/Dm-crypt "Dm-crypt").

To create a new filesystem on a partition, the existing filesystem located on the partition must not be mounted.

If the partition you want to format contains a mounted filesystem, it will show up in the _MOUNTPOINT_ column of lsblk.

```
$ lsblk

```

To unmount it, you can use _umount_ on the directory where the filesystem was mounted to:

```
# umount /mountpoint

```

To create a new file system of type ext4 on a partition do:

**Warning:** After creating a new filesystem, data previously stored on this partition can likely not be recovered. Make a backup of any data you want to keep.

```
# mkfs.ext4 /dev/_partition_

```

Alternatively, you can use `mkfs` which is just a unified front-end for the different `mkfs._fstype_` tools.

```
# mkfs -t ext4 /dev/_partition_

```

## See also

*   [wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems")

Retrieved from "[https://wiki.archlinux.org/index.php?title=File_systems&oldid=418619](https://wiki.archlinux.org/index.php?title=File_systems&oldid=418619)"