From [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	A file system (or filesystem) is a means to organize data expected to be retained after a program terminates by providing procedures to store, retrieve and update data, as well as manage the available space on the device(s) which contain it. A file system organizes data in an efficient manner and is tuned to the specific characteristics of the device.

Individual drive partitions can be setup using one of the many different available filesystems. Each has its own advantages, disadvantages, and unique idiosyncrasies. A brief overview of supported filesystems follows; the links are to Wikipedia pages that provide much more information.

Before being formatted, a drive should be [partitioned](/index.php/Partitioning "Partitioning").

## Contents

*   [1 Types of file systems](#Types_of_file_systems)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 FUSE-based file systems](#FUSE-based_file_systems)
    *   [1.3 Special purpose file systems](#Special_purpose_file_systems)
*   [2 Create a file system](#Create_a_file_system)
*   [3 See also](#See_also)

## Types of file systems

See also [w:Comparison_of_file_systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "w:Comparison of file systems").

*   **[Btrfs](/index.php/Btrfs "Btrfs")** — the B-tree file system is "a new copy on write (CoW) filesystem for Linux aimed at implementing advanced features while focusing on fault tolerance, repair and easy administration." [[1]](https://btrfs.wiki.kernel.org/index.php/Main_Page) It has been merged into the mainline kernel Btrfs and has a stable filesystem disk format. [[2]](https://btrfs.wiki.kernel.org/index.php/Main_Page#Stability_status)

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **[VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "w:File Allocation Table")** — **Virtual File Allocation Table** is technically simple and supported by virtually all existing operating systems. This makes it a useful format for solid-state memory cards and a convenient way to share data between operating systems. VFAT supports long file names.

	[https://github.com/dosfstools/dosfstools](https://github.com/dosfstools/dosfstools) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **[exFAT](https://en.wikipedia.org/wiki/exFAT "w:exFAT")** — **Microsoft file system optimized for flash drives**. Like NTFS, exFAT can pre-allocate disk space for a file by just marking arbitrary space on disk as 'allocated'.

	[https://github.com/relan/exfat](https://github.com/relan/exfat) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **[F2FS](/index.php/F2FS "F2FS")** — **Flash-Friendly File System** is a flash file system created by Kim Jaegeuk (Hangul: 김재극) at Samsung for the Linux operating system kernel. The motivation for F2FS was to build a file system which takes into account the characteristics of NAND flash memory-based storage devices (such as solid-state disks, eMMC, and SD cards).

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **[ext](https://en.wikipedia.org/wiki/Extended_file_system "w:Extended file system")** — **Second Extended Filesystem** does not have journaling support or barriers. Lack of journaling can result in data loss in the event of a power failure or system crash. When used on larger partitions, file/system checks may take a long time. An ext2 filesystem can be [converted to ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3"). **Third Extended Filesystem** is essentially the ext2 system with journaling support and write barriers. It is backward compatible with ext2\. **Fourth Extended Filesystem** is a newer filesystem that is also compatible with ext2 and ext3\. It provides support for volumes with sizes up to 1 exabyte (i.e. 1,048,576 terabytes) and files sizes up to 16 terabytes. It increases the 32,000 subdirectory limit in ext3 to unlimited. It also offers online defragmentation capability.

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **[HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "w:Hierarchical File System")** — **Hierarchical File System** is a proprietary file system developed by Apple Inc. for use in computer systems running Mac OS.

	[http://www.opensource.apple.com](http://www.opensource.apple.com) || [hfsprogs](https://www.archlinux.org/packages/?name=hfsprogs)

*   **[JFS](/index.php/JFS "JFS")** — IBM's **Journaled File System** was the first filesystem to offer journaling. It was developed in the IBM AIX® operating system before being ported to GNU/Linux.

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **[NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS")** — **New Implementation of a Log-structured File System** was developed by NTT. It records all data in a continuous log-like format that is only appended to and never overwritten. It is designed to reduce seek times and minimize the type of data loss that occurs after a crash with conventional Linux filesystems.

	[http://nilfs.sourceforge.net/](http://nilfs.sourceforge.net/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **[NTFS](/index.php/NTFS "NTFS")** — **File system used by Windows**. NTFS has several technical improvements over FAT and HPFS (High Performance File System), such as improved support for metadata, and the use of advanced data structures to improve performance, reliability, and disk space utilization, plus additional extensions, such as security access control lists (ACL) and file system journaling.

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **[Reiser4](/index.php/Reiser4 "Reiser4")** — **Successor to the ReiserFS file system**, developed from scratch by Namesys and sponsored by DARPA as well as Linspire, it uses B*-trees in conjunction with the dancing tree balancing approach, in which underpopulated nodes will not be merged until a flush to disk except under memory pressure or when a transaction completes. Such a system also allows Reiser4 to create files and directories without having to waste time and space through fixed blocks.

	[https://reiser4.wiki.kernel.org/index.php/Main_Page](https://reiser4.wiki.kernel.org/index.php/Main_Page) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)

*   **[ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "w:ReiserFS")** — **Hans Reiser's high-performance journaling FS (v3)** is touted as very fast, especially when dealing with many small files. ReiserFS is fast at formatting, yet comparatively slow at mounting. ReiserFSv3 is not being actively developed at this time. Generally regarded as a good choice for `/var`.

	[https://reiser4.wiki.kernel.org/index.php/Main_Page](https://reiser4.wiki.kernel.org/index.php/Main_Page) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **[XFS](/index.php/XFS "XFS")** — **Early journaling filesystem originally developed by Silicon Graphics** for the IRIX operating system and ported to GNU/Linux. It provides very fast throughput on large files and filesystems and is very fast at formatting and mounting. Comparative benchmark testing has shown it to be slower when dealing with many small files. XFS is very mature and offers online defragmentation capability.

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **[ZFS](/index.php/ZFS "ZFS")** — **Combined file system and logical volume manager designed by Sun Microsystems**. The features of ZFS include protection against data corruption, support for high storage capacities, integration of the concepts of filesystem and volume management, snapshots and copy-on-write clones, continuous integrity checking and automatic repair, RAID-Z and native NFSv4 ACLs.

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/), [zfs-linux-git](https://aur.archlinux.org/packages/zfs-linux-git/)

### Journaling

All the above filesystems with the exception of ext2, FAT16/32, use [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling provides fault-resilience by logging changes before they are committed to the filesystem. In the event of a system crash or power failure, such file systems are faster to bring back online and less likely to become corrupted. The logging takes place in a dedicated area of the filesystem.

Not all journaling techniques are the same. Ext3 and ext4 offer data-mode journaling, which logs both data and meta-data, as well as possibility to journal only meta-data changes. Data-mode journaling comes with a speed penalty and is not enabled by default. In the same vein, [Reiser4](/index.php/Reiser4 "Reiser4") offers so-called ["transaction models"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models), which include pure journaling (equivalent to ext4's data-mode journaling), pure Copy-on-Write approach (equivalent to btrfs' default) and a combined approach which heuristically alternates between the two former. *It should be noted that reiser4 does not provide an equivalent to ext4's default journaling behavior (meta-data only).*

The other filesystems provide ordered-mode journaling, which only logs meta-data. While all journaling will return a filesystem to a valid state after a crash, data-mode journaling offers the greatest protection against corruption and data loss. There is a compromise in system performance, however, because data-mode journaling does two write operations: first to the journal and then to the disk. The trade-off between system speed and data safety should be considered when choosing the filesystem type.

### FUSE-based file systems

[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (FUSE) is a mechanism for Unix-like operating systems that lets non-privileged users create their own file systems without editing kernel code. This is achieved by running file system code in *user space*, while the FUSE kernel module provides only a "bridge" to the actual kernel interfaces.

Some FUSE-based file systems:

*   **acd-fuse** — FUSE filesystem driver for Amazon's Cloud Drive.

	[https://github.com/handyman5/acd_fuse](https://github.com/handyman5/acd_fuse) || [acdfuse-git](https://aur.archlinux.org/packages/acdfuse-git/)

*   **adbfs-git** — Mount an Android device filesystem.

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **cddfs** — Mount audio CDs.

	[http://castet.matthieu.free.fr/](http://castet.matthieu.free.fr/) || [cddfs](https://aur.archlinux.org/packages/cddfs/)

*   **fuseiso** — Mount an ISO as a regular user.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **vdfuse** — Mounting VirtualBox disk images (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

*   **wiifuse** — Mount a Gamecube or Wii DVD disc image read-only.

	[http://wiibrew.org/wiki/Wiifuse](http://wiibrew.org/wiki/Wiifuse) || [wiifuse](https://aur.archlinux.org/packages/wiifuse/)

*   **xbfuse-git** — Mount an Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — Represent an XML file as a directory structure for easy access.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   **zfs-fuse** — [ZFS support via FUSE](/index.php/ZFS_on_FUSE "ZFS on FUSE").

	[http://zfs-fuse.net/](http://zfs-fuse.net/) || [zfs-fuse](https://aur.archlinux.org/packages/zfs-fuse/)

*   **[EncFS](/index.php/EncFS "EncFS")** — EncFS is a userspace stackable cryptographic file-system.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **[gitfs](/index.php/Gitfs "Gitfs")** — gitfs is a FUSE file system that fully integrates with git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

See [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace") for more.

### Special purpose file systems

*   **[CramFS](https://en.wikipedia.org/wiki/cramfs "wikipedia:cramfs")** — **Compressed ROM filesystem** is a read only filesystem designed with simplicity and efficiency in mind. Its maximum file size is less 16MB and the maximum file system size is around 272MB.

	[http://sourceforge.net/projects/cramfs/](http://sourceforge.net/projects/cramfs/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[eCryptfs](/index.php/ECryptfs "ECryptfs")** — **Enterprise Cryptographic Filesystem** is a package of disk encryption software for Linux. It is implemented as a POSIX-compliant filesystem-level encryption layer, aiming to offer functionality similar to that of GnuPG at the operating system level.

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")** — **SquashFS** is a compressed read only filesystem. SquashFS compresses files, inodes and directories, and supports block sizes up to 1 MB for greater compression.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

## Create a file system

**Note:**

*   If you want to change the partition layout, see [Partitioning](/index.php/Partitioning "Partitioning").
*   If you want to create a swap partition, see [Swap](/index.php/Swap "Swap").

First, identify the device where the file system will be created, for example with [lsblk](/index.php/Lsblk "Lsblk"). File systems are usually created on a partition, but they can also be created inside of logical containers like [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID"), or [dm-crypt](/index.php/Dm-crypt "Dm-crypt").

To create a new filesystem on a partition, the existing filesystem located on the partition must not be mounted. If the partition you want to format contains a mounted filesystem, it will show up in the *MOUNTPOINT* column of lsblk.

To unmount it, you can use *umount* on the directory where the filesystem was mounted to:

```
# umount /mountpoint

```

To create a new file system of type *fstype* on a partition do:

**Warning:** After creating a new filesystem, data previously stored on this partition can likely not be recovered. Make a backup of any data you want to keep.

```
# mkfs.*fstype* /dev/*partition*

```

See the article in [#Types of file systems](#Types_of_file_systems) corresponding to file system you wish to create for the exact command as well as userspace utilities you may wish to install for a particular file system.

For example, to create a new file system of type [ext4](/index.php/Ext4 "Ext4") on a partition do:

```
# mkfs.ext4 /dev/*partition*

```

## See also

*   [wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems")