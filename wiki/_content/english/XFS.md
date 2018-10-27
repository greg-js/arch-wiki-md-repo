Related articles

*   [File systems](/index.php/File_systems "File systems")

XFS is a high-performance journaling file system created by Silicon Graphics, Inc. XFS is particularly proficient at parallel IO due to its allocation group based design. This enables extreme scalability of IO threads, filesystem bandwidth, file and filesystem size when spanning multiple storage devices.

## Contents

*   [1 Installation](#Installation)
*   [2 Data corruption](#Data_corruption)
    *   [2.1 Repair XFS Filesystem](#Repair_XFS_Filesystem)
    *   [2.2 Online Metadata Checking (scrub)](#Online_Metadata_Checking_.28scrub.29)
*   [3 Integrity](#Integrity)
*   [4 Performance](#Performance)
    *   [4.1 Stripe size and width](#Stripe_size_and_width)
    *   [4.2 Access time](#Access_time)
    *   [4.3 Defragmentation](#Defragmentation)
        *   [4.3.1 Inspect fragmentation levels](#Inspect_fragmentation_levels)
        *   [4.3.2 Perform defragmentation](#Perform_defragmentation)
    *   [4.4 Free inode btree](#Free_inode_btree)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Root file system quota](#Root_file_system_quota)
*   [6 See also](#See_also)

## Installation

The tools to manage XFS partions are in the [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) package, which is included in the default base installation.

## Data corruption

If for whatever reason you experience data corruption, you will need to repair the filesystem manually.

### Repair XFS Filesystem

First unmount the XFS filesystem.

```
# umount /dev/sda3

```

Once unmounted, run the [xfs_repair(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_repair.8) tool.

```
# xfs_repair -v /dev/sda3

```

### Online Metadata Checking (scrub)

**Warning:** This program is EXPERIMENTAL, which means that its behaviour and interface could change at any time, see [xfs_scrub(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_scrub.8).

`xfs_scrub` asks the kernel to scrub all metadata objects in the [filesystem](/index.php/Filesystem "Filesystem"). Metadata records are scanned for obviously bad values and then cross-referenced against other metadata. The goal is to establish a reasonable confidence about the consistency of the overall filesystem by examining the consistency of individual metadata records against the other metadata in the filesystem. Damaged metadata can be rebuilt from other metadata if there exists redundant data structures which are intact.

[Enable](/index.php/Enable "Enable") `xfs_scrub_all.timer` to periodic check online metadata for all filesystems. One may want to [edit](/index.php/Edit "Edit") `xfs_scrub_all.timer`, since it runs every Sunday at 3:10am.

## Integrity

xfsprogs 3.2.0 has introduced a new on-disk format (v5) that includes a metadata checksum scheme called [Self-Describing Metadata](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt). Based upon CRC32 it provides for example additional protection against metadata corruption during unexpected power losses. Checksum is enabled by default when using xfsprogs 3.2.3 or later. If you need read-write mountable xfs for older kernel, It can be easily disable using the `-m crc=0` switch when calling [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8).

```
# mkfs.xfs -m crc=0 /dev/*target_partition*

```

The XFS v5 on-disk format is considered stable for production workloads starting Linux Kernel 3.15.

**Note:** Unlike [Btrfs](/index.php/Btrfs "Btrfs") and [ZFS](/index.php/ZFS "ZFS"), the CRC32 checksum only applies to the metadata and not actual data.

## Performance

For optimal speed, just create an XFS file system with:

```
# mkfs.xfs /dev/*target_partition*

```

Yep, so simple - since all of the ["boost knobs" are already "on" by default](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E).

**Warning:** Disabling atime and other performance enhancements make data corruption and failure much more likely.

As per [XFS wiki](http://xfs.org/index.php/XFS_FAQ#Q:_I_want_to_tune_my_XFS_filesystems_for_.3Csomething.3E), consider changing the default CFQ [I/O scheduler](/index.php/Improving_performance#Input.2Foutput_schedulers "Improving performance") (for example to [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler"), [Noop](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler") or [BFQ](/index.php/Linux-ck#How_to_enable_the_BFQ_I.2FO_Scheduler "Linux-ck")) to enjoy all of the benefits of XFS, especially on [SSDs](/index.php/SSD "SSD").

### Stripe size and width

If this filesystem will be on a striped RAID you can gain significant speed improvements by specifying the stripe size to the [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) command.

See [How to calculate the correct sunit,swidth values for optimal performance](http://xfs.org/index.php/XFS_FAQ#Q:_How_to_calculate_the_correct_sunit.2Cswidth_values_for_optimal_performance)

### Access time

On some filesystems you can increase performance by adding the `noatime` mount option to the `/etc/fstab` file. For XFS filesystems the default atime behaviour is `relatime`, which has almost no overhead compared to noatime but still maintains sane atime values. All Linux filesystems use this as the default now (since around 2.6.30), but XFS has used relatime-like behaviour since 2006, so no-one should really need to ever use noatime on XFS for performance reasons.

Also, `noatime` implies `nodiratime`, so there is never a need to specify **nodiratime** when **noatime** is also specified.

### Defragmentation

Although the extent-based nature of XFS and the delayed allocation strategy it uses significantly improves the file system's resistance to fragmentation problems, XFS provides a filesystem defragmentation utility (*xfs_fsr*, short for XFS filesystem reorganizer) that can defragment the files on a mounted and active XFS filesystem. It can be useful to view XFS fragmentation periodically.

[xfs_fsr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_fsr.8) improves the organization of mounted filesystems. The reorganization algorithm operates on one file at a time, compacting or otherwise improving the layout of the file extents (contiguous blocks of file data).

#### Inspect fragmentation levels

To see how much fragmentation your file system currently has:

```
# xfs_db -c frag -r /dev/sda3

```

#### Perform defragmentation

To begin defragmentation, use the [xfs_fsr(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_fsr.8) command:

```
# xfs_fsr /dev/sda3

```

### Free inode btree

Starting Linux 3.16, XFS has added a btree that tracks free inodes. It is equivalent to the existing inode allocation btree with the exception that the free inode btree tracks inode chunks with at least one free inode. The purpose is to improve lookups for free inode clusters for inode allocation. It improves performance on aged filesystems i.e. months or years down the track when you have added and removed millions of files to/from the filesystem. Using this feature does not impact overall filesystem reliability level or recovery capabilities.

This feature relies on the new v5 on-disk format that has been considered stable for production workloads starting Linux Kernel 3.15\. It does not change existing on-disk structures, but adds a new one that must remain consistent with the inode allocation btree; for this reason older kernels will only be able to mount read-only filesystems with the free inode btree feature.

The feature enabled by default when using xfsprogs 3.2.3 or later. If you need writable filesystem for older kernel, it can be disable with `finobt=0` switch when formatting a XFS partition. You will need `crc=0` together.

```
# mkfs.xfs -m crc=0,finobt=0 /dev/*target_partition*

```

or shortly (`finobt` depends `crc`)

```
# mkfs.xfs -m crc=0 /dev/*target_partition*

```

## Troubleshooting

### Root file system quota

XFS quota mount options (`uquota`, `gquota`, `prjquota`, etc.) fail during re-mount of the file system. To enable quota for root file system, the mount option must be passed to initramfs as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `rootflags=`. Subsequently, it should not be listed among mount options in `/etc/fstab` for the root (`/`) filesystem.

**Note:** There are some differences of XFS Quota compared to standard Linux [Disk quota](/index.php/Disk_quota "Disk quota"), this article [http://inai.de/linux/adm_quota](http://inai.de/linux/adm_quota) may be worth reading.

## See also

*   [XFS FAQ](http://xfs.org/index.php/XFS_FAQ)
*   [Improving Metadata Performance By Reducing Journal Overhead](http://xfs.org/index.php/Improving_Metadata_Performance_By_Reducing_Journal_Overhead)
*   [XFS Wikipedia Entry](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS")