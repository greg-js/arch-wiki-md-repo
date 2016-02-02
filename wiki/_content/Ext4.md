# Ext4

Related articles

*   [File systems](/index.php/File_systems "File systems")
*   [Ext3](/index.php/Ext3 "Ext3")

Ext4 is the evolution of the most used Linux filesystem, Ext3\. In many ways, Ext4 is a deeper improvement over Ext3 than Ext3 was over Ext2\. Ext3 was mostly about adding journaling to Ext2, but Ext4 modifies important data structures of the filesystem such as the ones destined to store the file data. The result is a filesystem with an improved design, better performance, reliability, and features.

Source: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

## Contents

*   [1 Create a new ext4 filesystem](#Create_a_new_ext4_filesystem)
    *   [1.1 Bytes-per-inode ratio](#Bytes-per-inode_ratio)
    *   [1.2 Reserved blocks](#Reserved_blocks)
*   [2 Migrating from ext2/ext3 to ext4](#Migrating_from_ext2.2Fext3_to_ext4)
    *   [2.1 Mounting ext2/ext3 partitions as ext4 without converting](#Mounting_ext2.2Fext3_partitions_as_ext4_without_converting)
        *   [2.1.1 Rationale](#Rationale)
        *   [2.1.2 Procedure](#Procedure)
    *   [2.2 Converting ext2/ext3 partitions to ext4](#Converting_ext2.2Fext3_partitions_to_ext4)
        *   [2.2.1 Rationale](#Rationale_2)
        *   [2.2.2 Procedure](#Procedure_2)
*   [3 Using ext4 per directory encryption](#Using_ext4_per_directory_encryption)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 E4rat](#E4rat)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Barriers and Performance](#Barriers_and_Performance)

## Create a new ext4 filesystem

To format a partition do:

```
# mkfs.ext4 /dev/_partition_

```

**Tip:** See the mkfs.ext4 [man page](/index.php/Man_page "Man page") for more options; edit `/etc/mke2fs.conf` to view/configure default options.

### Bytes-per-inode ratio

From `man mkfs.ext4`:

	_**mke2fs** creates an inode for every_ bytes-per-inode _bytes of space on the disk. The larger the_ bytes-per-inode _ratio, the fewer inodes will be created._

Creating a new file, directory, symlink etc. requires at least one free inode. If the inode count is too low, no file can be created on the filesystem even though there is still space left on it.

Because it is not possible to change this value or the inode count after the filesystem is created, `mkfs.ext4` uses by default a rather low ratio of one inode every 16384 bytes (16 Kb) to avoid this situation.

However, for partitions with size in the hundreds or thousands of GB and average file size in the megabyte range, this usually results in a much too large inode number because the number of files created never reaches the number of inodes.

This results in a waste of disk space, because all those unused inodes each take up 256 bytes on the filesystem (this is also set in `/etc/mke2fs.conf` but should not be changed). 256 * several millions = quite a few gigabytes wasted in unused inodes.

This can be evaluated by comparing the `{I}Use%` figures provided by `df` and `df -i`:

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

Here comes the `-T _usage-type_` option, which specifies the expected usage of the filesystem using types defined in `/etc/mke2fs.conf`. Among those types are the bigger `largefile` and `largefile4`, which offer more relevant ratios for bigger disks of 1 MiB and 4 MiB respectively. They can be used as such:

```
# mkfs.ext4 -T largefile /dev/_device_

```

This ratio can also be set directly via the `-i` option: _e.g._ use `-i 2097152` for a 2 MiB ratio and `-i 6291456` for a 6 MiB ratio.

**Tip:** Conversely, if you are setting up a partition dedicated to host millions of small files like emails or newsgroup items, you can use smaller _usage-type_ values such as `news` (one inode for every 4096 bytes) or `small` (same plus smaller inode and block sizes).

**Warning:** If you make a heavy use of symbolic or hard links, _e.g._ you use a backup scheme leveraging [rsync](/index.php/Rsync "Rsync") `--link-dest` feature ([rsnapshot](/index.php/Rsnapshot "Rsnapshot"), [BackupPC](/index.php/BackupPC "BackupPC"), [backintime](https://aur.archlinux.org/packages/backintime/)<sup><small>AUR</small></sup>...), you may want to keep your inode number high enough because while not taking more space, every new hardlink consumes one new inode and therefore inode use may grow dramatically.

### Reserved blocks

By default, 5% of the filesystem blocks will be reserved for the super-user, to avoid fragmentation and "_allow root-owned daemons to continue to function correctly after non-privileged processes are prevented from writing to the filesystem_" (from `man mkfs.ext4`).

For modern high-capacity disks, this is higher than necessary if the partition is used as a long-term archive or not crucial to system operations (like `/home`). See [this email](http://www.redhat.com/archives/ext3-users/2009-January/msg00026.html) for the opinion of ext4 developer Ted Ts'o on reserved blocks.

It is generally safe to reduce the percentage of reserved blocks to free up disk space when the partition is either:

*   Very large (for example > 50G)
*   Used as long-term archive, i.e., where files will not be deleted and created very often

The `-m` option of ext4-related utilities allows to specify the percentage of reserved blocks.

To totally prevent reserving blocks upon filesystem creation, use:

```
# mkfs.ext4 -m 0 /dev/_device_

```

To reduce it to 1% afterwards, use:

```
# tune2fs -m 1 /dev/_device_

```

You can use `findmnt(8)` to find the device name:

```
$ findmnt _/the/mount/point_

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

*   If you convert the system's root filesystem, ensure that the 'fallback' initramfs is available at reboot. Alternatively, add `ext4` according to [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and re-create the 'default' initial ramdisk with `mkinitcpio -p linux` before starting.
*   If you decide to convert a separate `/boot` partition, ensure the [bootloader](/index.php/Bootloader "Bootloader") supports booting from ext4.

In the following steps `/dev/sdxX` denotes the path to the partition to be converted, such as `/dev/sda1`.

1.  **[BACK-UP!](/index.php/Backup_programs "Backup programs")** Back-up all data on any ext3 partitions that are to be converted to ext4\. A useful package, especially for root partitions, is [Clonezilla](http://clonezilla.org).
2.  Edit `/etc/fstab` and change the 'type' from ext3 to ext4 for any partitions that are to be converted to ext4.
3.  Boot the live medium (if necessary). The conversion process with [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) must be done when the drive is not mounted. If converting a root partition, the simplest way to achieve this is to boot from some other live medium.
4.  Ensure the partition is **NOT** mounted
5.  If you want to convert a ext2 partition, the first conversion step is to add a [journal](/index.php/File_systems#Journaling "File systems") by running `tune2fs -j /dev/sdxX` as root; making it a ext3 partition.
6.  Run `tune2fs -O extent,uninit_bg,dir_index /dev/sdxX` as root. This command converts the ext3 filesystem to ext4 (irreversibly).
7.  Run `fsck -f /dev/sdxX` as root.
    *   The user **must _fsck_** the filesystem, or it **will be unreadable**! This _fsck_ run is needed to return the filesystem to a consistent state. It **will** find checksum errors in the group descriptors - this **is** expected. The `-f` option asks _fsck_ to force checking even if the file system seems clean. The `-p` option may be used on top to 'automatically repair' (otherwise, the user will be asked for input for each error).
8.  Recommended: mount the partition and run `e4defrag -c -v /dev/sdxX` as root.
    *   Even though the filesystem is now converted to ext4, all files that have been written before the conversion do not yet take advantage of the extent option of ext4, which will improve large file performance and reduce fragmentation and filesystem check time. In order to fully take advantage of ext4, all files would have to be rewritten on disk. Use _e4defrag_ to take care of this problem.
9.  Reboot Arch Linux!

## Using ext4 per directory encryption

Linux 4.1 comes with a new Ext4 feature to encrypt directories of a filesystem.[[5]](http://lwn.net/Articles/639427/) [[6]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=6162e4b0bedeb3dac2ba0a5e1b1f56db107d97ec) [[7]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=8663da2c0919896788321cd8a0016af08588c656) See also [Quarkslab's blog](http://blog.quarkslab.com/a-glimpse-of-ext4-filesystem-level-encryption.html) entry with a write-up of the features, an overview of the implementation state and practical test results with kernel 4.1\.

Encryption keys are stored in the keyring. To get started, make sure you have enabled `CONFIG_KEYS` and `CONFIG_EXT4_ENCRYPTION` kernel options and you have kernel 4.1 or higher. Note the Arch default [linux](https://www.archlinux.org/packages/?name=linux) does not have `CONFIG_EXT4_ENCRYPTION` set yet.

First of all, you need to update [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) to at least version 1.43, which is a work in progress as of July 2015\. Package [e2fsprogs-git](https://aur.archlinux.org/packages/e2fsprogs-git/)<sup><small>AUR</small></sup> is available to install the latest git version.

e4crypt source has disabled a relevant section in its source code, enable it:

```
diff --git a/misc/e4crypt.c b/misc/e4crypt.c
index c5b384a..828e7cf 100644
--- a/misc/e4crypt.c
+++ b/misc/e4crypt.c
@@ -714,9 +714,6 @@ void do_set_policy(int argc, char **argv, const struct cmd_desc *cmd)
               exit(1);
       }

-      printf("arg %s\n", argv[optind]);
-      exit(0);
-
       strcpy(saltbuf.key_ref_str, argv[optind]);
       if ((strlen(argv[optind]) != (EXT4_KEY_DESCRIPTOR_SIZE * 2)) ||
           hex2byte(argv[optind], (EXT4_KEY_DESCRIPTOR_SIZE * 2),

```

Make sure you have installed updated versions of e2fsck and e4crypt:

```
# e2fsck -V
e2fsck 1.43-WIP (18-May-2015)
        Using EXT2FS Library version 1.43-WIP, 18-May-2015

```

Let us make a directory that we will encrypt. Encryption policy can be set only on empty directories:

```
# mkdir -p /encrypted/dir

```

First generate a random salt value and store it in a safe place:

```
# head -c 16 /dev/random | xxd -p
877282f53bd0adbbef92142fc4cac459

```

Now generate and add a new key into your keyring: this step should be repeated every time you flush your keychain (reboot)

```
# e4crypt -S 0x877282f53bd0adbbef92142fc4cac459
Enter passphrase (echo disabled): 
Added key with descriptor [f88747555a6115f5]

```

Now you know a descriptor for your key. Make sure you have added a key into your keychain:

```
# keyctl show
Session Keyring
1021618178 --alswrv   1000  1000  keyring: _ses
 176349519 --alsw-v   1000  1000   \_ logon: ext4:f88747555a6115f5

```

Almost done. Now set an encryption policy for a directory:

```
# e4crypt set_policy f88747555a6115f5 /encrypted/dir

```

That is all. If you try accessing the disk without adding a key into keychain, filenames and their contents will be seen as encrypted gibberish. Be careful running old versions of e2fsck on your filesystem - it will treat encrypted filenames as invalid.

## Tips and tricks

### E4rat

[E4rat](/index.php/E4rat "E4rat") is a preload application designed for the ext4 filesystem. It monitors files opened during boot, optimizes their placement on the partition to improve access time, and preloads them at the very beginning of the boot process. [E4rat](/index.php/E4rat "E4rat") does not offer improvements with [SSDs](/index.php/SSD "SSD"), whose access time is negligible compared to hard disks.

## Troubleshooting

### Barriers and Performance

Since kernel 2.6.30, ext4 performance has decreased due to changes that serve to improve data integrity [[8]](http://www.phoronix.com/scan.php?page=article&item=ext4_then_now&num=1).

_Most file systems (XFS, ext3, ext4, reiserfs) send write barriers to disk after fsync or during transaction commits. Write barriers enforce proper ordering of writes, making volatile disk write caches safe to use (at some performance penalty). If your disks are battery-backed in one way or another, disabling barriers may safely improve performance._

_Sending write barriers can be disabled using the `barrier=0` mount option (for ext3, ext4, and reiserfs), or using the `nobarrier` mount option (for XFS)_ [[9]](http://doc.opensuse.org/products/draft/SLES/SLES-tuning_sd_draft/cha.tuning.io.html).

**Warning:** Disabling barriers when disks cannot guarantee caches are properly written in case of power failure can lead to severe file system corruption and data loss.

To turn barriers off add the option `barrier=0` to the desired filesystem. For example:

 `/etc/fstab`  `/dev/sda5    /    ext4    noatime,barrier=0    0    1` 

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ext4&oldid=393347](https://wiki.archlinux.org/index.php?title=Ext4&oldid=393347)"