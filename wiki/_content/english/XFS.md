Related articles

*   [File systems](/index.php/File_systems "File systems")

XFS is a high-performance journaling file system created by Silicon Graphics, Inc. XFS is particularly proficient at parallel IO due to its allocation group based design. This enables extreme scalability of IO threads, filesystem bandwidth, file and filesystem size when spanning multiple storage devices.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Data corruption](#Data_corruption)
    *   [2.1 Repair XFS Filesystem](#Repair_XFS_Filesystem)
    *   [2.2 Online Metadata Checking (scrub)](#Online_Metadata_Checking_(scrub))
*   [3 Integrity](#Integrity)
*   [4 Performance](#Performance)
    *   [4.1 Stripe size and width](#Stripe_size_and_width)
    *   [4.2 Access time](#Access_time)
    *   [4.3 Defragmentation](#Defragmentation)
        *   [4.3.1 Inspect fragmentation levels](#Inspect_fragmentation_levels)
        *   [4.3.2 Perform defragmentation](#Perform_defragmentation)
    *   [4.4 Free inode btree](#Free_inode_btree)
    *   [4.5 External XFS Journal](#External_XFS_Journal)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Root file system quota](#Root_file_system_quota)
    *   [5.2 xfs_scrub_all fails if user "nobody" can not access the mountpoint](#xfs_scrub_all_fails_if_user_"nobody"_can_not_access_the_mountpoint)
*   [6 See also](#See_also)

## Installation

The tools to manage XFS partitions are in the [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) package, which is included in the default base installation.

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

**Warning:** This program is EXPERIMENTAL, which means that its behavior and interface could change at any time, see [xfs_scrub(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_scrub.8).

`xfs_scrub` asks the kernel to scrub all metadata objects in the XFS filesystem. Metadata records are scanned for obviously bad values and then cross-referenced against other metadata. The goal is to establish a reasonable confidence about the consistency of the overall filesystem by examining the consistency of individual metadata records against the other metadata in the filesystem. Damaged metadata can be rebuilt from other metadata if there exists redundant data structures which are intact.

[Enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") `xfs_scrub_all.timer` to periodic check online metadata for all XFS filesystems.

**Note:** One may want to [edit](/index.php/Edit "Edit") `xfs_scrub_all.timer`: the timer runs every Sunday at 3:10am and will be [triggered immediately](/index.php/Systemd/Timers#Realtime_timer "Systemd/Timers") if it missed the last start time, i.e. due to the system being powered off.

## Integrity

[xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) 3.2.0 has introduced a new on-disk format (v5) that includes a metadata checksum scheme called [Self-Describing Metadata](https://www.kernel.org/doc/Documentation/filesystems/xfs-self-describing-metadata.txt). Based upon CRC32 it provides for example additional protection against metadata corruption during unexpected power losses. Checksum is enabled by default when using [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) 3.2.3 or later. If you need read-write mountable xfs for older kernel, It can be easily disabled using the `-m crc=0` switch when calling [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8).

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

Also see [xfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs.5) for details of all available mount options.

**Tip:** When using the XFS filesystem on [RAID](/index.php/RAID "RAID") devices, performance improvements may be possible by using `largeio`, `swalloc`, increased `logbsize` and `allocsize` values, etc. The following articles may provide additional details about those flags:

*   [https://www.beegfs.io/wiki/StorageServerTuning](https://www.beegfs.io/wiki/StorageServerTuning)
*   [https://help.marklogic.com/Knowledgebase/Article/View/505/0/recommended-xfs-settings-for-marklogic-server](https://help.marklogic.com/Knowledgebase/Article/View/505/0/recommended-xfs-settings-for-marklogic-server)

### Stripe size and width

If this filesystem will be on a striped RAID you can gain significant speed improvements by specifying the stripe size to the [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) command.

XFS can sometimes detect the geometry under software RAID, but in case you reshape it or you are using hardware RAID see [how to calculate the correct sunit,swidth values for optimal performance](http://xfs.org/index.php/XFS_FAQ#Q:_How_to_calculate_the_correct_sunit.2Cswidth_values_for_optimal_performance)

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

### External XFS Journal

Using an external log (metadata journal) on for instance a [SSD](/index.php/SSD "SSD") may be useful to improve performance [[1]](https://docs.oracle.com/cd/E37670_01/E37355/html/ol_extjnl_xfs.html). See [mkfs.xfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.xfs.8) for details about the `logdev` parameter.

**Warning:** Beware using flash-memory may wear-out the drive. See [Improving performance#Reduce disk reads/writes](/index.php/Improving_performance#Reduce_disk_reads/writes "Improving performance") for SSD wear-out details.

To reserve an external journal with a specified size when you create an XFS file system, specify the `-l logdev=device,size=size` option to the `mkfs.xfs` command. If you omit the `size` parameter, a journal size based on the size of the file system is used. To mount the XFS file system so that it uses the external journal, specify the `-o logdev=device` option to the [mount](/index.php/Mount "Mount") command.

## Troubleshooting

### Root file system quota

XFS quota mount options (`uquota`, `gquota`, `prjquota`, etc.) fail during re-mount of the file system. To enable quota for root file system, the mount option must be passed to initramfs as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `rootflags=`. Subsequently, it should not be listed among mount options in `/etc/fstab` for the root (`/`) filesystem.

**Note:** There are some differences of XFS Quota compared to standard Linux [Disk quota](/index.php/Disk_quota "Disk quota"), this article [http://inai.de/linux/adm_quota](http://inai.de/linux/adm_quota) may be worth reading.

### xfs_scrub_all fails if user "nobody" can not access the mountpoint

When running `xfs_scrub_all`, it will launch `xfs_scrub@.service` for each mounted XFS file system. The service is run as user `nobody`, so if `nobody` can not navigate to the directory, it will fail with the error:

```
xfs_scrub@*mountpoint*.service: Changing to the requested working directory failed: Permission denied
xfs_scrub@*mountpoint*.service: Failed at step CHDIR spawning /usr/bin/xfs_scrub: Permission denied
xfs_scrub@*mountpoint*.service: Main process exited, code=exited, status=200/CHDIR

```

To allow the service to run, change the [permissions](/index.php/Permissions "Permissions") of the mountpoint so that user `nobody` has execute permissions.

## See also

*   [XFS FAQ](http://xfs.org/index.php/XFS_FAQ)
*   [Improving Metadata Performance By Reducing Journal Overhead](http://xfs.org/index.php/Improving_Metadata_Performance_By_Reducing_Journal_Overhead)
*   [XFS Wikipedia Entry](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS")