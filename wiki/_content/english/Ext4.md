From [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4):

	Ext4 is the evolution of the most used Linux filesystem, Ext3\. In many ways, Ext4 is a deeper improvement over Ext3 than Ext3 was over Ext2\. Ext3 was mostly about adding journaling to Ext2, but Ext4 modifies important data structures of the filesystem such as the ones destined to store the file data. The result is a filesystem with an improved design, better performance, reliability, and features.

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
*   [3 Using file-based encryption](#Using_file-based_encryption)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 E4rat](#E4rat)
    *   [4.2 Barriers and performance](#Barriers_and_performance)
*   [5 Enabling metadata checksums](#Enabling_metadata_checksums)
    *   [5.1 New filesystem](#New_filesystem)
    *   [5.2 Existing filesystem](#Existing_filesystem)
    *   [5.3 Impact on performance](#Impact_on_performance)
*   [6 See also](#See_also)

## Create a new ext4 filesystem

To format a partition do:

```
# mkfs.ext4 /dev/*partition*

```

**Tip:** See the mkfs.ext4 [man page](/index.php/Man_page "Man page") for more options; edit `/etc/mke2fs.conf` to view/configure default options.

### Bytes-per-inode ratio

From `man mkfs.ext4`:

	***mke2fs** creates an inode for every* bytes-per-inode *bytes of space on the disk. The larger the* bytes-per-inode *ratio, the fewer inodes will be created.*

Creating a new file, directory, symlink etc. requires at least one free [inode](https://en.wikipedia.org/wiki/Inode "wikipedia:Inode"). If the inode count is too low, no file can be created on the filesystem even though there is still space left on it.

Because it is not possible to change either the bytes-per-inode ratio or the inode count after the filesystem is created, `mkfs.ext4` uses by default a rather low ratio of one inode every 16384 bytes (16 Kb) to avoid this situation.

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

By default, 5% of the filesystem blocks will be reserved for the super-user, to avoid fragmentation and "*allow root-owned daemons to continue to function correctly after non-privileged processes are prevented from writing to the filesystem*" (from `man mkfs.ext4`).

For modern high-capacity disks, this is higher than necessary if the partition is used as a long-term archive or not crucial to system operations (like `/home`). See [this email](http://www.redhat.com/archives/ext3-users/2009-January/msg00026.html) for the opinion of ext4 developer Ted Ts'o on reserved blocks.

It is generally safe to reduce the percentage of reserved blocks to free up disk space when the partition is either:

*   Very large (for example > 50G)
*   Used as long-term archive, i.e., where files will not be deleted and created very often

The `-m` option of ext4-related utilities allows to specify the percentage of reserved blocks.

To totally prevent reserving blocks upon filesystem creation, use:

```
# mkfs.ext4 -m 0 /dev/*device*

```

To reduce it to 1% afterwards, use:

```
# tune2fs -m 1 /dev/*device*

```

You can use `findmnt(8)` to find the device name:

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
    *   The user **must *fsck*** the filesystem, or it **will be unreadable**! This *fsck* run is needed to return the filesystem to a consistent state. It **will** find checksum errors in the group descriptors - this **is** expected. The `-f` option asks *fsck* to force checking even if the file system seems clean. The `-p` option may be used on top to 'automatically repair' (otherwise, the user will be asked for input for each error).
8.  Recommended: mount the partition and run `e4defrag -c -v /dev/sdxX` as root.
    *   Even though the filesystem is now converted to ext4, all files that have been written before the conversion do not yet take advantage of the extent option of ext4, which will improve large file performance and reduce fragmentation and filesystem check time. In order to fully take advantage of ext4, all files would have to be rewritten on disk. Use *e4defrag* to take care of this problem.
9.  Reboot Arch Linux!

## Using file-based encryption

Since Linux 4.1, ext4 supports file-based encryption. In a directory tree marked for encryption, file contents, filenames, and symbolic link targets are all encrypted. Encryption keys are stored in the kernel keyring. See also [Quarkslab's blog](http://blog.quarkslab.com/a-glimpse-of-ext4-filesystem-level-encryption.html) entry with a write-up of the feature, an overview of the implementation state, and practical test results with kernel 4.1.

Make sure you are using a kernel with the option `CONFIG_EXT4_ENCRYPTION` enabled and have the [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) package updated to at least version 1.43.

Then verify that your filesystem is using a supported block size for encryption:

```
# tune2fs -l /dev/*device* | grep 'Block size'
Block size:               4096
# getconf PAGE_SIZE
4096

```

If these values are not the same, then your filesystem will not support encryption, so **do not proceed further**.

Next, enable the encryption feature flag on your filesystem:

```
# tune2fs -O encrypt /dev/*device*

```

**Warning:** Once the encryption feature flag is enabled, kernels older than 4.1 will be unable to mount the filesystem.

Next, make a directory to encrypt:

```
# mkdir /encrypted

```

Note that encryption can only be applied to an empty directory. The encryption setting (or "encryption policy") is inherited by new files and subdirectories. Encrypting existing files is not yet supported.

Now generate and add a new key to your keyring. This step must be repeated every time you flush your keyring (reboot):

```
# e4crypt add_key
Enter passphrase (echo disabled): 
Added key with descriptor [f88747555a6115f5]

```

**Warning:** If you forget your passphrase, there will be no way to decrypt your files! It also isn't yet possible to change a passphrase after you've set it.

**Note:** To help prevent [dictionary attacks](https://en.wikipedia.org/wiki/Dictionary_attack is automatically generated and stored in the ext4 filesystem superblock. Both the passphrase *and* the salt are used to derive the actual encryption key. As a consequence of this, if you have multiple ext4 filesystems with encryption enabled mounted, then `e4crypt add_key` will actually add multiple keys, one per filesystem. Although any key can be used on any filesystem, it would be wise to only use, on a given filesystem, keys using that filesystem's salt. Otherwise, you risk being unable to decrypt files on filesystem A if filesystem B is unmounted. Alternatively, you can use the `-S` option to `e4crypt add_key` to specify a salt yourself.

Now you know the descriptor for your key. Make sure the key is in your session keyring:

```
# keyctl show
Session Keyring
1021618178 --alswrv   1000  1000  keyring: _ses
 176349519 --alsw-v   1000  1000   \_ logon: ext4:f88747555a6115f5

```

Almost done. Now set an encryption policy on the directory (assign the key to it):

```
# e4crypt set_policy f88747555a6115f5 /encrypted

```

That is all. If you try accessing the directory without adding the key into your keyring, filenames and their contents will be seen as encrypted gibberish.

## Tips and tricks

### E4rat

[E4rat](/index.php/E4rat "E4rat") is a preload application designed for the ext4 filesystem. It monitors files opened during boot, optimizes their placement on the partition to improve access time, and preloads them at the very beginning of the boot process. [E4rat](/index.php/E4rat "E4rat") does not offer improvements with [SSDs](/index.php/SSD "SSD"), whose access time is negligible compared to hard disks.

### Barriers and performance

Since kernel 2.6.30, ext4 performance has decreased due to changes that serve to improve data integrity.[[5]](http://www.phoronix.com/scan.php?page=article&item=ext4_then_now&num=1)

	Most file systems (XFS, ext3, ext4, reiserfs) send write barriers to disk after fsync or during transaction commits. Write barriers enforce proper ordering of writes, making volatile disk write caches safe to use (at some performance penalty). If your disks are battery-backed in one way or another, disabling barriers may safely improve performance.

	Sending write barriers can be disabled using the `barrier=0` mount option (for ext3, ext4, and reiserfs), or using the `nobarrier` mount option (for XFS).

**Warning:** Disabling barriers when disks cannot guarantee caches are properly written in case of power failure can lead to severe file system corruption and data loss.

To turn barriers off add the option `barrier=0` to the desired filesystem. For example:

 `/etc/fstab`  `/dev/sda5    /    ext4    noatime,barrier=0    0    1` 

## Enabling metadata checksums

In both cases of enabling metadata checksums for new and existing filesystems, you will need to load some kernel modules.

If your CPU supports SSE 4.2, make sure the `crc32c_intel` kernel module is loaded in order to enable the hardware accelerated CRC32C algorithm. If not you will need to load the `crc32c_generic` module.

If this is the root file-system your `crc32c_` module might need to be added to `/etc/mkinitcpio.conf`:

```
   MODULES="... crc32c_intel crc32c_generic"

```

And then regenerate the initramfs. See [Mkinitcpio#Image creation and activation](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

After this, you are ready to enable support for metadata checksums as described in the following two sections. In both cases the file system must not be mounted.

More about metadata checksums can be read on the [ext4 wiki](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums).

### New filesystem

To enable support for ext4 metadata checksums on a new file system make sure that you have `e2fsprogs 1.43` or newer and simply do a:

```
# mkfs.ext4 */dev/path/to/disk*

```

The `metadata_csum` and `64bit` options will be enabled by default.

The file-system can then be mounted as usual.

### Existing filesystem

To enable support on an existing ext4 file system do the following.

This needs to be done with the partition unmounted, so if you want to convert the root, you'll need to run off an USB live distro.

First the partition needs to be checked and optimized using:

```
# e2fsck -Df */dev/path/to/disk*  

```

Then the file-system needs to be converted to 64bit:

```
# resize2fs -b */dev/path/to/disk* 

```

Finally checksums can be added

```
# tune2fs -O metadata_csum */dev/path/to/disk*

```

The file-system can then be mounted as usual.

You can check whether the features were successfully enabled by running:

```
# dumpe2fs */dev/path/to/disk*

```

### Impact on performance

Keep in mind that the intel module consistently performs 10x faster than the generic one, peaking at 20x faster as can be seen in [this benchmark](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums#Benchmarking).

## See also

*   [Official Ext4 wiki](https://ext4.wiki.kernel.org/)
*   [Ext4 Disk Layout](https://ext4.wiki.kernel.org/index.php/Ext4_Disk_Layout) described in its wiki
*   [Ext4 Encryption](http://lwn.net/Articles/639427/) LWN article
*   Kernel commits for ext4 encryption [[6]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=6162e4b0bedeb3dac2ba0a5e1b1f56db107d97ec) [[7]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=8663da2c0919896788321cd8a0016af08588c656)
*   [e2fsprogs Changelog](http://e2fsprogs.sourceforge.net/e2fsprogs-release.html)
*   [Ext4 Metadata Checksums](https://ext4.wiki.kernel.org/index.php/Ext4_Metadata_Checksums)