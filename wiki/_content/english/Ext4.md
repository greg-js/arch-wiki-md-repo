Related articles

*   [File systems](/index.php/File_systems "File systems")
*   [Ext3](/index.php/Ext3 "Ext3")

From [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4):

	Ext4 is the evolution of the most used Linux filesystem, Ext3\. In many ways, Ext4 is a deeper improvement over Ext3 than Ext3 was over Ext2\. Ext3 was mostly about adding journaling to Ext2, but Ext4 modifies important data structures of the filesystem such as the ones destined to store the file data. The result is a filesystem with an improved design, better performance, reliability, and features.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Create a new ext4 filesystem](#Create_a_new_ext4_filesystem)
    *   [1.1 Bytes-per-inode ratio](#Bytes-per-inode_ratio)
    *   [1.2 Reserved blocks](#Reserved_blocks)
*   [2 Migrating from ext2/ext3 to ext4](#Migrating_from_ext2/ext3_to_ext4)
    *   [2.1 Mounting ext2/ext3 partitions as ext4 without converting](#Mounting_ext2/ext3_partitions_as_ext4_without_converting)
        *   [2.1.1 Rationale](#Rationale)
        *   [2.1.2 Procedure](#Procedure)
    *   [2.2 Converting ext2/ext3 partitions to ext4](#Converting_ext2/ext3_partitions_to_ext4)
        *   [2.2.1 Rationale](#Rationale_2)
        *   [2.2.2 Procedure](#Procedure_2)
*   [3 Improving performance](#Improving_performance)
    *   [3.1 E4rat](#E4rat)
    *   [3.2 Disabling access time update](#Disabling_access_time_update)
    *   [3.3 Increasing commit interval](#Increasing_commit_interval)
    *   [3.4 Turning barriers off](#Turning_barriers_off)
    *   [3.5 Disabling journaling](#Disabling_journaling)
    *   [3.6 Use external journal to optimize performance](#Use_external_journal_to_optimize_performance)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Using file-based encryption](#Using_file-based_encryption)
    *   [4.2 Enabling metadata checksums](#Enabling_metadata_checksums)
        *   [4.2.1 New filesystem](#New_filesystem)
        *   [4.2.2 Convert existing filesystem](#Convert_existing_filesystem)
*   [5 See also](#See_also)

## Create a new ext4 filesystem

To format a partition do:

```
# mkfs.ext4 /dev/*partition*

```

**Tip:**

*   See [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8) for more options; edit `/etc/mke2fs.conf` to view/configure default options.
*   If supported, you may want to enable [metadata checksums](#Enabling_metadata_checksums).

### Bytes-per-inode ratio

From [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8):

	***mke2fs** creates an inode for every* bytes-per-inode *bytes of space on the disk. The larger the* bytes-per-inode *ratio, the fewer inodes will be created.*

Creating a new file, directory, symlink etc. requires at least one free [inode](https://en.wikipedia.org/wiki/Inode "wikipedia:Inode"). If the inode count is too low, no file can be created on the filesystem even though there is still space left on it.

Because it is not possible to change either the bytes-per-inode ratio or the inode count after the filesystem is created, `mkfs.ext4` uses by default a rather low ratio of one inode every 16384 bytes (16 KiB) to avoid this situation.

However, for partitions with size in the hundreds or thousands of GB and average file size in the megabyte range, this usually results in a much too large inode number because the number of files created never reaches the number of inodes.

This results in a waste of disk space, because all those unused inodes each take up 256 bytes on the filesystem (this is also set in `/etc/mke2fs.conf` but should not be changed). 256 * several millions = quite a few gigabytes wasted in unused inodes.

This situation can be evaluated by comparing the `{I}Use%` figures provided by `df` and `df -i`:

 `$ df -h /home` 
```
Filesystem              Size    Used   Avail  **Use%**   Mounted on
/dev/mapper/lvm-home    115G    56G    59G    **49%**    /home

```
 `$ df -hi /home` 
```
Filesystem              Inodes  IUsed  IFree  **IUse%**  Mounted on
/dev/mapper/lvm-home    1.8M    1.1K   1.8M   **1%**     /home

```

To specify a different bytes-per-inode ratio, you can use the `-T *usage-type*` option which hints at the expected usage of the filesystem using types defined in `/etc/mke2fs.conf`. Among those types are the bigger `largefile` and `largefile4` which offer more relevant ratios of one inode every 1 MiB and 4 MiB respectively. It can be used as such:

```
# mkfs.ext4 -T largefile /dev/*device*

```

The bytes-per-inode ratio can also be set directly via the `-i` option: *e.g.* use `-i 2097152` for a 2 MiB ratio and `-i 6291456` for a 6 MiB ratio.

**Tip:** Conversely, if you are setting up a partition dedicated to host millions of small files like emails or newsgroup items, you can use smaller *usage-type* values such as `news` (one inode for every 4096 bytes) or `small` (same plus smaller inode and block sizes).

**Warning:** If you make a heavy use of symbolic links, make sure to keep the inode count high enough with a low bytes-per-inode ratio, because while not taking more space every new symbolic link consumes one new inode and therefore the filesystem may run out of them quickly.

### Reserved blocks

By default, 5% of the filesystem blocks will be reserved for the super-user, to avoid fragmentation and "*allow root-owned daemons to continue to function correctly after non-privileged processes are prevented from writing to the filesystem*" (from [mke2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mke2fs.8)).

For modern high-capacity disks, this is higher than necessary if the partition is used as a long-term archive or not crucial to system operations (like `/home`). See [this email](http://www.redhat.com/archives/ext3-users/2009-January/msg00026.html) for the opinion of ext4 developer Ted Ts'o on reserved blocks.

It is generally safe to reduce the percentage of reserved blocks to free up disk space when the partition is either:

*   Very large (for example > 50G)
*   Used as long-term archive, i.e., where files will not be deleted and created very often

The `-m` option of ext4-related utilities allows to specify the percentage of reserved blocks.

To totally prevent reserving blocks upon filesystem creation, use:

```
# mkfs.ext4 -m 0 /dev/*device*

```

To change it to 1% afterwards, use:

```
# tune2fs -m 1 /dev/*device*

```

You can use [findmnt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/findmnt.8) to find the device name:

```
$ findmnt */the/mount/point*

```

## Migrating from ext2/ext3 to ext4

### Mounting ext2/ext3 partitions as ext4 without converting

#### Rationale

A compromise between fully converting to ext4 and simply remaining with ext2/ext3 is to mount the partitions as ext4.

**Pros:**

*   Compatibility (the filesystem can continue to be mounted as ext3) – This allows users to still read the filesystem from other operating systems without ext4 support (e.g. Windows with ext2/ext3 drivers)
*   Improved performance (though not as much as a fully-converted ext4 partition).[[1]](http://kernelnewbies.org/Ext4) [[2]](http://events.linuxfoundation.org/slides/2010/linuxcon_japan/linuxcon_jp2010_fujita.pdf)

**Cons:**

*   Fewer features of ext4 are used (only those that do not change the disk format such as multiblock allocation and delayed allocation)

**Note:** Except for the relative novelty of ext4 (which can be seen as a risk), **there is no major drawback to this technique**.

#### Procedure

1.  Edit `/etc/fstab` and change the 'type' from ext2/ext3 to ext4 for any partitions you would like to mount as ext4.
2.  Re-mount the affected partitions.

### Converting ext2/ext3 partitions to ext4

#### Rationale

To experience the benefits of ext4, an irreversible conversion process must be completed.

**Pros:**

*   Improved performance and new features.[[3]](http://kernelnewbies.org/Ext4) [[4]](http://events.linuxfoundation.org/slides/2010/linuxcon_japan/linuxcon_jp2010_fujita.pdf)

**Cons:**

*   Partitions that contain mostly static files, such as a `/boot` partition, may not benefit from the new features. Also, adding a journal (which is implied by moving a ext2 partition to ext3/4) always incurs performance overhead.
*   Irreversible (ext4 partitions cannot be 'downgraded' to ext2/ext3\. It is, however, backwards compatible until extent and other unique options are enabled)

#### Procedure

These instructions were adapted from [Kernel documentation](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) and an [BBS thread](https://bbs.archlinux.org/viewtopic.php?id=61602).

**Warning:**

*   If you convert the system's root filesystem, ensure that the 'fallback' initramfs is available at reboot. Alternatively, add `ext4` according to [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") before starting.
*   If you decide to convert a separate `/boot` partition, ensure the [bootloader](/index.php/Bootloader "Bootloader") supports booting from ext4.

In the following steps `/dev/sdxX` denotes the path to the partition to be converted, such as `/dev/sda1`.

1.  [Back up](/index.php/Backup_programs "Backup programs") all data on any ext3 partitions that are to be converted to ext4\. A useful package, especially for root partitions, is [clonezilla](https://www.archlinux.org/packages/?name=clonezilla).
2.  Edit `/etc/fstab` and change the 'type' from ext3 to ext4 for any partitions that are to be converted to ext4.
3.  Boot the live medium (if necessary). The conversion process with [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) must be done when the drive is not mounted. If converting a root partition, the simplest way to achieve this is to boot from some other live medium.
4.  Ensure the partition is *not* mounted
5.  If you want to convert a ext2 partition, the first conversion step is to add a [journal](/index.php/File_systems#Journaling "File systems") by running `tune2fs -j /dev/sdxX` as root; making it a ext3 partition.
6.  Run `tune2fs -O extent,uninit_bg,dir_index /dev/sdxX` as root. This command converts the ext3 filesystem to ext4 (irreversibly).
7.  Run `fsck -f /dev/sdxX` as root.
    *   This step is necessary, otherwise the filesystem **will be unreadable**. This *fsck* run is needed to return the filesystem to a consistent state. It will find checksum errors in the group descriptors - this is expected. The `-f` option asks *fsck* to force checking even if the file system seems clean. The `-p` option may be used on top to "automatically repair" (otherwise, the user will be asked for input for each error).
8.  Recommended: mount the partition and run `e4defrag -c -v /dev/sdxX` as root.
    *   Even though the filesystem is now converted to ext4, all files that have been written before the conversion do not yet take advantage of the extent option of ext4, which will improve large file performance and reduce fragmentation and filesystem check time. In order to fully take advantage of ext4, all files would have to be rewritten on disk. Use *e4defrag* to take care of this problem.
9.  Reboot

## Improving performance

### E4rat

[E4rat](/index.php/E4rat "E4rat") is a preload application designed for the ext4 filesystem. It monitors files opened during boot, optimizes their placement on the partition to improve access time, and preloads them at the very beginning of the boot process. *E4rat* does not offer improvements with [SSDs](/index.php/SSD "SSD"), whose access time is negligible compared to hard disks.

### Disabling access time update

The *ext4* file system records information about when a file was last accessed and there is a cost associated with recording it. With the `noatime` option, the access timestamps on the filesystem are not updated.

 `/etc/fstab` 
```
/dev/sda5    /    ext4    defaults,**noatime**    0    1

```

Doing so breaks applications that rely on access time, see [fstab#atime options](/index.php/Fstab#atime_options "Fstab") for possible solutions.

### Increasing commit interval

The sync interval for data and metadata can be increased by providing a higher time delay to the `commit` option.

The default 5 sec means that if the power is lost, one will lose as much as the latest 5 seconds of work. It forces a full sync of all data/journal to physical media every 5 seconds. The filesystem will not be damaged though, thanks to the journaling. The following [fstab](/index.php/Fstab "Fstab") illustrates the use of `commit`:

 `/etc/fstab`  `/dev/sda5    /    ext4    defaults,noatime,**commit=60**    0    1` 

### Turning barriers off

**Warning:** Disabling barriers for disks without battery-backed cache is not recommended and can lead to severe file system corruption and data loss.

*Ext4* enables write barriers by default. It ensures that file system metadata is correctly written and ordered on disk, even when write caches lose power. This goes with a performance cost especially for applications that use *fsync* heavily or create and delete many small files. For disks that have a write cache that is battery-backed in one way or another, disabling barriers may safely improve performance.

To turn barriers off, add the option `barrier=0` to the desired filesystem. For example:

 `/etc/fstab`  `/dev/sda5    /    ext4    noatime,**barrier=0**    0    1` 

### Disabling journaling

**Warning:** Using a filesystem without journaling can result in data loss in case of sudden dismount like power failure or kernel lockup.

Disabling the journal with *ext4* can be done with the following command on an unmounted disk:

```
# tune2fs -O "^has_journal" /dev/sdXN

```

### Use external journal to optimize performance

For those with concerns about both data integrity and performance, the journaling can be significantly sped up with the `journal_async_commit` mount option. Note that it [does not work with](https://patchwork.ozlabs.org/patch/414750/) the balanced default of `data=ordered`, so this is only recommended when the filesystem is already cautiously using `data=journal`.

You can then format a dedicated device to journal to with `mke2fs -O journal_dev /dev/journal_device`. Use `tune2fs -J device=/dev/journal_device /dev/ext4_fs` to assign the journal to an existing device, or replace `tune2fs` with `mkfs.ext4` if you are making a new filesystem.

## Tips and tricks

### Using file-based encryption

Since Linux 4.1, ext4 natively supports file encryption. Encryption is applied at the directory level, and different directories can use different encryption keys. This is different from both [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), which is block-device level encryption, and from [eCryptfs](/index.php/ECryptfs "ECryptfs"), which is a stacked cryptographic filesystem. To use ext4's native encryption support, see the [fscrypt](/index.php/Fscrypt "Fscrypt") article.

### Enabling metadata checksums

When a filesystem has been created with [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) 1.44 or later, metadata checksums should already be enabled by default. Existing filesystems may be converted to enable metadata checksum support.

If the CPU supports SSE 4.2, make sure the `crc32c_intel` [kernel module](/index.php/Kernel_module "Kernel module") is loaded in order to enable the hardware accelerated CRC32C algorithm [[5]](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums#Benchmarking). If not, load the `crc32c_generic` module instead.

To read more about metadata checksums, see the [ext4 wiki](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums).

**Tip:** Use `dumpe2fs` to check the features that are enabled on the filesystem:
```
# dumpe2fs */dev/path/to/disk*

```

#### New filesystem

To enable support for ext4 metadata checksums on creating a new file system:

```
# mkfs.ext4 -O metadata_csum */dev/path/to/disk*

```

#### Convert existing filesystem

**Note:** The filesystem should not be mounted.

First the partition needs to be checked and optimized using `e2fsck`:

```
# e2fsck -Df */dev/path/to/disk*  

```

Convert the filesystem to 64bit:

```
# resize2fs -b */dev/path/to/disk* 

```

Finally enable checksums support:

```
# tune2fs -O metadata_csum */dev/path/to/disk*

```

## See also

*   [Official Ext4 wiki](https://ext4.wiki.kernel.org/)
*   [Ext4 Disk Layout](https://ext4.wiki.kernel.org/index.php/Ext4_Disk_Layout) described in its wiki
*   [Ext4 Encryption](http://lwn.net/Articles/639427/) LWN article
*   Kernel commits for ext4 encryption [[6]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=6162e4b0bedeb3dac2ba0a5e1b1f56db107d97ec) [[7]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=8663da2c0919896788321cd8a0016af08588c656)
*   [e2fsprogs Changelog](http://e2fsprogs.sourceforge.net/e2fsprogs-release.html)
*   [Ext4 Metadata Checksums](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums)