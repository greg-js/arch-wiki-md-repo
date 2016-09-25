From [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	In computing, a file system (or filesystem) is used to control how data is stored and retrieved. Without a file system, information placed in a storage medium would be one large body of data with no way to tell where one piece of information stops and the next begins. By separating the data into pieces and giving each piece a name, the information is easily isolated and identified.

	Taking its name from the way paper-based information systems are named, each group of data is called a "file". The structure and logic rules used to manage the groups of information and their names is called a "file system".

Individual drive partitions can be setup using one of the many different available filesystems. Each has its own advantages, disadvantages, and unique idiosyncrasies. A brief overview of supported filesystems follows; the links are to Wikipedia pages that provide much more information.

## Contents

*   [1 Create a file system](#Create_a_file_system)
*   [2 Types of file systems](#Types_of_file_systems)
    *   [2.1 Journaling](#Journaling)
    *   [2.2 FUSE-based file systems](#FUSE-based_file_systems)
    *   [2.3 Special-type file systems](#Special-type_file_systems)

## Create a file system

File systems are usually created on a [partition](/index.php/Partition "Partition"), inside logical containers such as [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID") and [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), or on a regular file (see [w:Loop device](https://en.wikipedia.org/wiki/Loop_device "w:Loop device")). This section describe the partition case.

**Note:** File systems can be written directly to a disk, known as a [superfloppy](https://msdn.microsoft.com/en-us/library/windows/hardware/dn640535(v=vs.85).aspx#gpt_faq_superfloppy) or *partitionless disk*. Certain limitations are involved with this method, particularly if [booting](/index.php/Arch_boot_process "Arch boot process") from such a drive. See [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") for an example.

**Warning:** After creating a new filesystem, data previously stored on this partition can unlikely be recovered. **Create a backup of any data you want to keep**.

Identify the partition where the file system will be created, for example with [lsblk](/index.php/Lsblk "Lsblk"):

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb                                                          
└─sdb1 vfat   Transcend 4A3C-A9E9
```

An existing file system, if present, will be shown in the `FSTYPE` column. If [mounted](/index.php/Mount "Mount"), it will appear in the `MOUNTPOINT` column or in the output of [findmnt(8)](http://man7.org/linux/man-pages/man8/findmnt.8.html). For example:

```
$ findmnt */dev/sdb1*

```

Mounted file systems **must** be unmounted with [umount(8)](http://man7.org/linux/man-pages/man8/umount.8.html) before proceeding:

```
# umount */mountpoint*

```

To create a new file system, use [mkfs(8)](http://man7.org/linux/man-pages/man8/mkfs.8.html). See [#Types of file systems](#Types_of_file_systems) for the exact type, as well as userspace utilities you may wish to install for a particular file system.

**Warning:** The purpose of a given partition may restrict the choice of file system. For example, an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") must contain a FAT32 (`mkfs.vfat`) file system, and the file system containing the `/boot` directory must be supported by the [boot loader](/index.php/Category:Boot_loaders "Category:Boot loaders").

For example, to create a new file system of type [ext4](/index.php/Ext4 "Ext4") (common for Linux data partitions), run:

```
# mkfs.*ext4* /dev/*sdb1*

```

**Tip:**

*   Use the `-L` flag of *mkfs.ext4* to specify a [file system label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming"). *e4label* can be used to change the label on an existing file system.
*   File systems may be *resized* after creation, with certain limitations. For example, an [XFS](/index.php/XFS "XFS") volume can be increased, but not reduced in size. See [Resize capabilities](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "w:Comparison of file systems") and the respective file system documentation for details.

The new file system can now be mounted to a directory of choice.

## Types of file systems

See [filesystems(5)](http://man7.org/linux/man-pages/man5/filesystems.5.html) for a general overview, and [w:Comparison_of_file_systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "w:Comparison of file systems") for a detailed feature comparison.

| File system | Creation command | Userspace utilities | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | Kernel documentation [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | Notes |
| [Btrfs](/index.php/Btrfs "Btrfs") | [mkfs.btrfs(8)](http://man7.org/linux/man-pages/man8/mkfs.btrfs.8.html) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Yes | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [Stability status](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "w:File Allocation Table") | mkfs.vfat(8) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Yes | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/exFAT "w:exFAT") | mkfs.exfat(8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Optional | N/A (FUSE-based) |
| [F2FS](/index.php/F2FS "F2FS") | mkefs.f2fs(8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Yes | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | Flash-based devices |
| [ext3](/index.php/Ext3 "Ext3") | [mke2fs(8)](http://man7.org/linux/man-pages/man8/mke2fs.8.html) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4 "Ext4") | [mke2fs(8)](http://man7.org/linux/man-pages/man8/mke2fs.8.html) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "w:Hierarchical File System") | mkfs.hfsplus(8) | [hfsprogs](https://www.archlinux.org/packages/?name=hfsprogs) | Optional | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | [macOS](https://en.wikipedia.org/wiki/macOS "w:macOS") file system |
| [JFS](/index.php/JFS "JFS") | mkfs.jfs(8) | [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [jfs.txt](https://www.kernel.org/doc/Documentation/filesystems/jfs.txt) |
| [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") | mkfs.nilfs2(8) | [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils) | Yes | [nilfs2.txt](https://www.kernel.org/doc/Documentation/filesystems/nilfs2.txt) |
| [NTFS](/index.php/NTFS "NTFS") | mkfs.ntfs(8) | [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | Yes | N/A (FUSE-based) | [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "w:Microsoft Windows") file system |
| [Reiser4](/index.php/Reiser4 "Reiser4") | mkfs.reiser4(8) | [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | No |
| [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "w:ReiserFS") | mkfs.reiserfs(8) | [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) |
| [XFS](/index.php/XFS "XFS") | [mkfs.xfs(8)](http://man7.org/linux/man-pages/man8/mkfs.xfs.8.html) | [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | 

[xfs.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs.txt)
[xfs-delayed-logging-design.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-delayed-logging-design.txt)
[xfs-self-describing-metadata.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt)

 |
| [ZFS](/index.php/ZFS "ZFS") | [zfs-linux-git](https://aur.archlinux.org/packages/zfs-linux-git/) | No | N/A ([OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "w:OpenZFS") port) |

**Note:** The kernel has its own NTFS driver (see [ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt)), but it has limited support for writing files.

### Journaling

All the above filesystems with the exception of ext2, FAT16/32, use [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling provides fault-resilience by logging changes before they are committed to the filesystem. In the event of a system crash or power failure, such file systems are faster to bring back online and less likely to become corrupted. The logging takes place in a dedicated area of the filesystem.

Not all journaling techniques are the same. Ext3 and ext4 offer data-mode journaling, which logs both data and meta-data, as well as possibility to journal only meta-data changes. Data-mode journaling comes with a speed penalty and is not enabled by default. In the same vein, [Reiser4](/index.php/Reiser4 "Reiser4") offers so-called ["transaction models"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models), which include pure journaling (equivalent to ext4's data-mode journaling), pure Copy-on-Write approach (equivalent to btrfs' default) and a combined approach which heuristically alternates between the two former. *It should be noted that reiser4 does not provide an equivalent to ext4's default journaling behavior (meta-data only).*

The other filesystems provide ordered-mode journaling, which only logs meta-data. While all journaling will return a filesystem to a valid state after a crash, data-mode journaling offers the greatest protection against corruption and data loss. There is a compromise in system performance, however, because data-mode journaling does two write operations: first to the journal and then to the disk. The trade-off between system speed and data safety should be considered when choosing the filesystem type.

### FUSE-based file systems

[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (FUSE) is a mechanism for Unix-like operating systems that lets non-privileged users create their own file systems without editing kernel code. This is achieved by running file system code in *user space*, while the FUSE kernel module provides only a "bridge" to the actual kernel interfaces.

Some FUSE-based file systems:

*   **adbfs-git** — Mount an Android device filesystem.

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **fuseiso** — Mount an ISO as a regular user.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **vdfuse** — Mounting VirtualBox disk images (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

*   **xbfuse-git** — Mount an Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — Represent an XML file as a directory structure for easy access.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   **[EncFS](/index.php/EncFS "EncFS")** — EncFS is a userspace stackable cryptographic file-system.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **[gitfs](/index.php/Gitfs "Gitfs")** — gitfs is a FUSE file system that fully integrates with git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

See [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace") for more.

### Special-type file systems

*   **[CramFS](https://en.wikipedia.org/wiki/cramfs "wikipedia:cramfs")** — **Compressed ROM filesystem** is a read only filesystem designed with simplicity and efficiency in mind. Its maximum file size is less 16MB and the maximum file system size is around 272MB.

	[http://sourceforge.net/projects/cramfs/](http://sourceforge.net/projects/cramfs/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[eCryptfs](/index.php/ECryptfs "ECryptfs")** — **Enterprise Cryptographic Filesystem** is a package of disk encryption software for Linux. It is implemented as a POSIX-compliant filesystem-level encryption layer, aiming to offer functionality similar to that of GnuPG at the operating system level.

	[http://ecryptfs.org](http://ecryptfs.org) || [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils)

*   **[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")** — **SquashFS** is a compressed read only filesystem. SquashFS compresses files, inodes and directories, and supports block sizes up to 1 MB for greater compression.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)