# XFS

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [File systems](/index.php/File_systems "File systems")

XFS is a high-performance journaling file system created by Silicon Graphics, Inc. XFS is particularly proficient at parallel IO due to its allocation group based design. This enables extreme scalability of IO threads, filesystem bandwidth, file and filesystem size when spanning multiple storage devices.

## Contents

*   [1 Installation](#Installation)
*   [2 Data corruption](#Data_corruption)
    *   [2.1 Repair XFS Filesystem](#Repair_XFS_Filesystem)
*   [3 Integrity](#Integrity)
*   [4 Performance](#Performance)
    *   [4.1 Stripe size and width](#Stripe_size_and_width)
    *   [4.2 Disable barrier](#Disable_barrier)
    *   [4.3 Access time](#Access_time)
    *   [4.4 Defragmentation](#Defragmentation)
        *   [4.4.1 Inspect fragmentation levels](#Inspect_fragmentation_levels)
        *   [4.4.2 Perform defragmentation](#Perform_defragmentation)
    *   [4.5 Free inode btree](#Free_inode_btree)
*   [5 See also](#See_also)

## Installation

**Warning:** XFS version 5 has problems with GRUB. Use a separate boot partition or install [grub-git](https://aur.archlinux.org/packages/grub-git/)<sup><small>AUR</small></sup> instead as a workaround.

The tools to manage XFS partions are in the [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) package from the [official repositories](/index.php/Official_repositories "Official repositories"), which is included in the default base installation.

## Data corruption

If for whatever reason you experience data corruption, you will need to repair the filesystem manually.

### Repair XFS Filesystem

First unmount the XFS filesystem.

```
# umount /dev/sda3

```

Once unmounted, run the _xfs_repair_ tool.

```
# xfs_repair -v /dev/sda3

```

## Integrity

xfsprogs 3.2.0 has introduced a new on-disk format (v5) that includes a metadata checksum scheme called [Self-Describing Metadata](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt). Based upon CRC32 it provides for example additional protection against metadata corruption during unexpected power losses. Checksum is not enabled by default when using _mkfs.xfs_ tool. It can be easily done using the `-m crc=1` switch when calling _mkfs.xfs_.

```
# mkfs.xfs -m crc=1 /dev/_target_partition_

```

The XFS v5 on-disk format is considered stable for production workloads starting Linux Kernel 3.15.

**Warning:** Unlike [Btrfs](/index.php/Btrfs "Btrfs") and [ZFS](/index.php/ZFS "ZFS"), the CRC32 checksum only applies to the metadata and not actual data.

## Performance

For optimal speed, just create an XFS file system with:

```
# mkfs.xfs /dev/_target_partition_

```

Yep, so simple - since all of the ["boost knobs" are already "on" by default](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E).

**Warning:** Disabling barriers, disabling atime, and other performance enhancements make data corruption and failure much more likely.

As per [XFS wiki](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E), consider changing the default CFQ [I/O scheduler](/index.php/Solid_State_Drives#I.2FO_scheduler "Solid State Drives") (for example to [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler"), [Noop](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler") or [BFQ](/index.php/Linux-ck#How_to_enable_the_BFQ_I.2FO_Scheduler "Linux-ck")) to enjoy all of the benefits of XFS, especially on [SSDs](/index.php/SSD "SSD").

### Stripe size and width

If this filesystem will be on a striped RAID you can gain significant speed improvements by specifying the stripe size to the `mkfs.xfs` command.

See [How to calculate the correct sunit,swidth values for optimal performance](http://xfs.org/index.php/XFS_FAQ#Q:_How_to_calculate_the_correct_sunit.2Cswidth_values_for_optimal_performance)

### Disable barrier

You can increase performance by disabling barrier usage for the filesystem by adding the _nobarrier_ mount option to the `/etc/fstab` file.

### Access time

On some filesystems you can increase performance by adding the `noatime` mount option to the `/etc/fstab` file. For XFS filesystems the default atime behaviour is `relatime`, which has almost no overhead compared to noatime but still maintains sane atime values. All Linux filesystems use this as the default now (since around 2.6.30), but XFS has used relatime-like behaviour since 2006, so no-one should really need to ever use noatime on XFS for performance reasons.

Also, `noatime` implies `nodiratime`, so there is never a need to specify **nodiratime** when **noatime** is also specified.

### Defragmentation

Although the extent-based nature of XFS and the delayed allocation strategy it uses significantly improves the file system's resistance to fragmentation problems, XFS provides a filesystem defragmentation utility (xfs_fsr, short for XFS filesystem reorganizer) that can defragment the files on a mounted and active XFS filesystem. It can be useful to view XFS fragmentation periodically.

**xfs_fsr** improves the organization of mounted filesystems. The reorganization algorithm operates on one file at a time, compacting or otherwise improving the layout of the file extents (contiguous blocks of file data).

#### Inspect fragmentation levels

To see how much fragmentation your file system currently has:

```
# xfs_db -c frag -r /dev/sda3

```

#### Perform defragmentation

To begin defragmentation, use the `xfs_fsr` command which is included with the _xfsprogs_ package.

```
# xfs_fsr /dev/sda3

```

### Free inode btree

Starting Linux 3.16, XFS has added a btree that tracks free inodes. It is equivalent to the existing inode allocation btree with the exception that the free inode btree tracks inode chunks with at least one free inode. The purpose is to improve lookups for free inode clusters for inode allocation. It improves performance on aged filesystems i.e. months or years down the track when you have added and removed millions of files to/from the filesystem. Using this feature doesn't impact overall filesystem reliability level or recovery capabilities.

This feature relies on the new v5 on-disk format that has been considered stable for production workloads starting Linux Kernel 3.15\. It does not change existing on-disk structures, but adds a new one that must remain consistent with the inode allocation btree; for this reason older kernels will only be able to mount read-only filesystems with the free inode btree feature.

The feature can be enabled with _finobt=1_ switch when formatting a XFS partition but requires the metadata checksum to be enabled as well via the _crc=1_ switch. Therefore the following options are required to take advantage of both the free inode btree and metadata checksum

```
 # mkfs.xfs -m crc=1,finobt=1 /dev/_target_partition_

```

According to the developers, the above _-m crc=1,finobt=1_ option will be the default mkfs option with the upcoming xfsprogs 3.3 release.

## See also

*   [XFS FAQ](http://xfs.org/index.php/XFS_FAQ)
*   [Improving Metadata Performance By Reducing Journal Overhead](http://xfs.org/index.php/Improving_Metadata_Performance_By_Reducing_Journal_Overhead)
*   [XFS Wikipedia Entry](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS")

Retrieved from "[https://wiki.archlinux.org/index.php?title=XFS&oldid=412024](https://wiki.archlinux.org/index.php?title=XFS&oldid=412024)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")