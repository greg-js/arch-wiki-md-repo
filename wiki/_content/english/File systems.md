From [Wikipedia](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	In computing, a file system (or filesystem) is used to control how data is stored and retrieved. Without a file system, information placed in a storage medium would be one large body of data with no way to tell where one piece of information stops and the next begins. By separating the data into pieces and giving each piece a name, the information is easily isolated and identified.

	Taking its name from the way paper-based information systems are named, each group of data is called a "file". The structure and logic rules used to manage the groups of information and their names is called a "file system".

Individual drive partitions can be setup using one of the many different available filesystems. Each has its own advantages, disadvantages, and unique idiosyncrasies. A brief overview of supported filesystems follows; the links are to Wikipedia pages that provide much more information.

## Contents

*   [1 Types of file systems](#Types_of_file_systems)
    *   [1.1 Journaling](#Journaling)
    *   [1.2 FUSE-based file systems](#FUSE-based_file_systems)
    *   [1.3 Stackable file systems](#Stackable_file_systems)
    *   [1.4 Read-only file systems](#Read-only_file_systems)
    *   [1.5 Clustered file systems](#Clustered_file_systems)
*   [2 Identify existing file systems](#Identify_existing_file_systems)
*   [3 Create a file system](#Create_a_file_system)
*   [4 Mount a filesystem](#Mount_a_filesystem)
    *   [4.1 List mounted file systems](#List_mounted_file_systems)
    *   [4.2 Umount a file system](#Umount_a_file_system)
*   [5 See also](#See_also)

## Types of file systems

See [filesystems(5)](http://man7.org/linux/man-pages/man5/filesystems.5.html) for a general overview, and [Wikipedia:Comparison of file systems](https://en.wikipedia.org/wiki/Comparison_of_file_systems "wikipedia:Comparison of file systems") for a detailed feature comparison. File systems supported by the kernel are listed in `/proc/filesystems`.

| File system | Creation command | Userspace utilities | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | Kernel documentation [[2]](https://www.kernel.org/doc/Documentation/filesystems/) | Notes |
| [Btrfs](/index.php/Btrfs "Btrfs") | [mkfs.btrfs(8)](http://man7.org/linux/man-pages/man8/mkfs.btrfs.8.html) | [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | Yes | [btrfs.txt](https://www.kernel.org/doc/Documentation/filesystems/btrfs.txt) | [Stability status](https://btrfs.wiki.kernel.org/index.php/Status) |
| [VFAT](/index.php/VFAT "VFAT") | [mkfs.vfat(8)](https://linux.die.net/man/8/mkfs.vfat) | [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | Yes | [vfat.txt](https://www.kernel.org/doc/Documentation/filesystems/vfat.txt) |
| [exFAT](https://en.wikipedia.org/wiki/exFAT "w:exFAT") | mkfs.exfat(8) | [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | Optional | N/A (FUSE-based) |
| [F2FS](/index.php/F2FS "F2FS") | mkfs.f2fs(8) | [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | Yes | [f2fs.txt](https://www.kernel.org/doc/Documentation/filesystems/f2fs.txt) | Flash-based devices |
| [ext3](/index.php/Ext3 "Ext3") | [mke2fs(8)](http://man7.org/linux/man-pages/man8/mke2fs.8.html) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext3.txt](https://www.kernel.org/doc/Documentation/filesystems/ext3.txt) |
| [ext4](/index.php/Ext4 "Ext4") | [mke2fs(8)](http://man7.org/linux/man-pages/man8/mke2fs.8.html) | [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [ext4.txt](https://www.kernel.org/doc/Documentation/filesystems/ext4.txt) |
| [HFS](https://en.wikipedia.org/wiki/Hierarchical_File_System "w:Hierarchical File System") | mkfs.hfsplus(8) | [hfsprogs](https://www.archlinux.org/packages/?name=hfsprogs) | Optional | [hfs.txt](https://www.kernel.org/doc/Documentation/filesystems/hfs.txt) | [macOS](https://en.wikipedia.org/wiki/macOS "w:macOS") file system |
| [JFS](/index.php/JFS "JFS") | mkfs.jfs(8) | [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | [jfs.txt](https://www.kernel.org/doc/Documentation/filesystems/jfs.txt) |
| [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") | mkfs.nilfs2(8) | [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils) | Yes | [nilfs2.txt](https://www.kernel.org/doc/Documentation/filesystems/nilfs2.txt) |
| [NTFS](/index.php/NTFS "NTFS") | [mkfs.ntfs(8)](https://linux.die.net/man/8/mkfs.ntfs) | [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | Yes | N/A (FUSE-based) | [Windows](https://en.wikipedia.org/wiki/Microsoft_Windows "w:Microsoft Windows") file system |
| [Reiser4](/index.php/Reiser4 "Reiser4") | mkfs.reiser4(8) | [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | No |
| [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "w:ReiserFS") | mkfs.reiserfs(8) | [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) |
| [XFS](/index.php/XFS "XFS") | [mkfs.xfs(8)](http://man7.org/linux/man-pages/man8/mkfs.xfs.8.html) | [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | Yes ([base](https://www.archlinux.org/groups/x86_64/base/)) | 

[xfs.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs.txt)
[xfs-delayed-logging-design.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-delayed-logging-design.txt)
[xfs-self-describing-metadata.txt](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt)

 |
| [ZFS](/index.php/ZFS "ZFS") | [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) | No | N/A ([OpenZFS](https://en.wikipedia.org/wiki/OpenZFS "w:OpenZFS") port) |

**Note:** The kernel has its own NTFS driver (see [ntfs.txt](https://www.kernel.org/doc/Documentation/filesystems/ntfs.txt)), but it has limited support for writing files.

### Journaling

All the above filesystems with the exception of ext2, FAT16/32, use [journaling](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system"). Journaling provides fault-resilience by logging changes before they are committed to the filesystem. In the event of a system crash or power failure, such file systems are faster to bring back online and less likely to become corrupted. The logging takes place in a dedicated area of the filesystem.

Not all journaling techniques are the same. Ext3 and ext4 offer data-mode journaling, which logs both data and meta-data, as well as possibility to journal only meta-data changes. Data-mode journaling comes with a speed penalty and is not enabled by default. In the same vein, [Reiser4](/index.php/Reiser4 "Reiser4") offers so-called ["transaction models"](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models), which include pure journaling (equivalent to ext4's data-mode journaling), pure Copy-on-Write approach (equivalent to btrfs' default) and a combined approach which heuristically alternates between the two former.

**Note:** Reiser4 does not provide an equivalent to ext4's default journaling behavior (meta-data only).

The other filesystems provide ordered-mode journaling, which only logs meta-data. While all journaling will return a filesystem to a valid state after a crash, data-mode journaling offers the greatest protection against corruption and data loss. There is a compromise in system performance, however, because data-mode journaling does two write operations: first to the journal and then to the disk. The trade-off between system speed and data safety should be considered when choosing the filesystem type.

### FUSE-based file systems

[Filesystem in Userspace](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace") (FUSE) is a mechanism for Unix-like operating systems that lets non-privileged users create their own file systems without editing kernel code. This is achieved by running file system code in *user space*, while the FUSE kernel module provides only a "bridge" to the actual kernel interfaces.

Some FUSE-based file systems:

*   **adbfs-git** — Mount an Android device filesystem.

	[http://collectskin.com/adbfs/](http://collectskin.com/adbfs/) || [adbfs-git](https://aur.archlinux.org/packages/adbfs-git/)

*   **[EncFS](/index.php/EncFS "EncFS")** — EncFS is a userspace stackable cryptographic file-system.

	[https://vgough.github.io/encfs/](https://vgough.github.io/encfs/) || [encfs](https://www.archlinux.org/packages/?name=encfs)

*   **fuseiso** — Mount an ISO as a regular user.

	[http://sourceforge.net/projects/fuseiso/](http://sourceforge.net/projects/fuseiso/) || [fuseiso](https://www.archlinux.org/packages/?name=fuseiso)

*   **[gitfs](/index.php/Gitfs "Gitfs")** — gitfs is a FUSE file system that fully integrates with git.

	[https://www.presslabs.com/gitfs/](https://www.presslabs.com/gitfs/) || [gitfs](https://aur.archlinux.org/packages/gitfs/)

*   **xbfuse-git** — Mount an Xbox (360) ISO.

	[http://multimedia.cx/xbfuse/](http://multimedia.cx/xbfuse/) || [xbfuse-git](https://aur.archlinux.org/packages/xbfuse-git/)

*   **xmlfs** — Represent an XML file as a directory structure for easy access.

	[https://github.com/halhen/xmlfs](https://github.com/halhen/xmlfs) || [xmlfs](https://aur.archlinux.org/packages/xmlfs/)

*   **vdfuse** — Mounting VirtualBox disk images (VDI/VMDK/VHD).

	[https://github.com/muflone/virtualbox-includes](https://github.com/muflone/virtualbox-includes) || [vdfuse](https://aur.archlinux.org/packages/vdfuse/)

See [Wikipedia:Filesystem in Userspace#Example uses](https://en.wikipedia.org/wiki/Filesystem_in_Userspace#Example_uses "wikipedia:Filesystem in Userspace") for more.

### Stackable file systems

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

	[http://unionfs.filesystems.org/](http://unionfs.filesystems.org/) || [linux](https://www.archlinux.org/packages/?name=linux)

*   **unionfs-fuse** — A user space Unionfs implementation.

	[https://github.com/rpodgorny/unionfs-fuse](https://github.com/rpodgorny/unionfs-fuse) || [unionfs-fuse](https://www.archlinux.org/packages/?name=unionfs-fuse)

### Read-only file systems

*   **[SquashFS](https://en.wikipedia.org/wiki/SquashFS "wikipedia:SquashFS")** — SquashFS is a compressed read only filesystem. SquashFS compresses files, inodes and directories, and supports block sizes up to 1 MB for greater compression.

	[http://squashfs.sourceforge.net/](http://squashfs.sourceforge.net/) || [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools)

### Clustered file systems

*   **[Ceph](https://en.wikipedia.org/wiki/Ceph "wikipedia:Ceph")** — Ceph is a unified, distributed storage system designed for excellent performance, reliability and scalability.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **[GlusterFS](/index.php/GlusterFS "GlusterFS")** — GlusterFS is a scalable network file system.

	[https://www.gluster.org/](https://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **[MooseFS](https://en.wikipedia.org/wiki/MooseFS "wikipedia:MooseFS")** — MooseFS is a fault tolerant, highly available and high performance scale-out network distributed file system.

	[https://www.gluster.org/](https://www.gluster.org/) || [moosefs](https://www.archlinux.org/packages/?name=moosefs)

*   **[OrangeFS](https://en.wikipedia.org/wiki/OrangeFS "wikipedia:OrangeFS")** — OrangeFS is a scale-out network file system designed for transparently accessing multi-server-based disk storage, in parallel. Has optimized MPI-IO support for parallel and distributed applications. Simplifies the use of parallel storage not only for Linux clients, but also for Windows, Hadoop, and WebDAV. POSIX-compatible. Part of Linux kernel since version 4.6\.

	[http://www.orangefs.org/](http://www.orangefs.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

## Identify existing file systems

To identify existing file systems, you can use [lsblk](/index.php/Lsblk "Lsblk"):

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL     UUID                                 MOUNTPOINT
sdb                                                          
└─sdb1 vfat   Transcend 4A3C-A9E9
```

An existing file system, if present, will be shown in the `FSTYPE` column. If [mounted](/index.php/Mount "Mount"), it will appear in the `MOUNTPOINT` column.

## Create a file system

File systems are usually created on a [partition](/index.php/Partition "Partition"), inside logical containers such as [LVM](/index.php/LVM "LVM"), [RAID](/index.php/RAID "RAID") and [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), or on a regular file (see [w:Loop device](https://en.wikipedia.org/wiki/Loop_device "w:Loop device")). This section describes the partition case.

**Note:** File systems can be written directly to a disk, known as a [superfloppy](https://msdn.microsoft.com/en-us/library/windows/hardware/dn640535(v=vs.85).aspx#gpt_faq_superfloppy) or *partitionless disk*. Certain limitations are involved with this method, particularly if [booting](/index.php/Arch_boot_process "Arch boot process") from such a drive. See [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") for an example.

**Warning:**

*   After creating a new filesystem, data previously stored on this partition can unlikely be recovered. **Create a backup of any data you want to keep**.
*   The purpose of a given partition may restrict the choice of file system. For example, an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") must contain a FAT32 (`mkfs.vfat`) file system, and the file system containing the `/boot` directory must be supported by the [boot loader](/index.php/Category:Boot_loaders "Category:Boot loaders").

Before continuing, [identify the device](/index.php/Lsblk "Lsblk") where the file system will be created and whether or not it is mounted. For example:

 `$ lsblk -f` 
```
NAME   FSTYPE   LABEL       UUID                                 MOUNTPOINT
sda
├─sda1                      C4DA-2C4D                            
├─sda2 ext4                 5b1564b2-2e2c-452c-bcfa-d1f572ae99f2 /mnt
└─sda3                      56adc99b-a61e-46af-aab7-a6d07e504652 

```

Mounted file systems **must** be [unmounted](#Unmount_a_file_system) before proceeding. In the above example an existing filesystem is on `/dev/sda2` and is mounted at `/mnt`. It would be unmounted with:

```
# umount /dev/sda2

```

To find just mounted file systems, see [#Listing mounted file systems](#Listing_mounted_file_systems).

To create a new file system, use [mkfs(8)](http://man7.org/linux/man-pages/man8/mkfs.8.html). See [#Types of file systems](#Types_of_file_systems) for the exact type, as well as userspace utilities you may wish to install for a particular file system.

For example, to create a new file system of type [ext4](/index.php/Ext4 "Ext4") (common for Linux data partitions) on `/dev/sda1`, run:

```
# mkfs.ext4 /dev/sda1

```

**Tip:**

*   Use the `-L` flag of *mkfs.ext4* to specify a [file system label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming"). *e2label* can be used to change the label on an existing file system.
*   File systems may be *resized* after creation, with certain limitations. For example, an [XFS](/index.php/XFS "XFS") filesystem's size can be increased, but it cannot reduced. See [Resize capabilities](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "w:Comparison of file systems") and the respective file system documentation for details.

The new file system can now be mounted to a directory of choice.

## Mount a filesystem

To manually mount filesystem located on a device (e.g., a partition) to a directory, use [mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html). This example mounts `/dev/sda1` to `/mnt`.

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

To list all mounted file systems, use [findmnt(8)](http://man7.org/linux/man-pages/man8/findmnt.8.html):

```
$ findmnt

```

*findmnt* takes a variety of arguments which can filter the output and show additional information. For example, it can take a device or mount point as an argument to show only information on what is specified:

```
$ findmnt /dev/sda1

```

*findmnt* gathers information from `/etc/fstab`, `/etc/mtab`, and `/proc/self/mounts`.

### Umount a file system

To unmount a file system use [umount(8)](http://man7.org/linux/man-pages/man8/umount.8.html). Either the device containing the file system (e.g., `/dev/sda1`) or the mount point (e.g., `/mnt`) can be specified:

```
# umount /dev/sda1

```

Or

```
# umount /mnt

```

## See also

*   [filesystems(5)](http://man7.org/linux/man-pages/man5/filesystems.5.html)
*   [Documentation of file systems supported by linux](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Wikipedia:File systems](https://en.wikipedia.org/wiki/File_systems "wikipedia:File systems")
*   [Wikipedia:Mount (Unix)](https://en.wikipedia.org/wiki/Mount_(Unix) "wikipedia:Mount (Unix)")