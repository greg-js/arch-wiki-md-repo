Related articles

*   [File systems](/index.php/File_systems "File systems")

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory equipped with Flash Translation Layer. Unlike JFFS or UBIFS it relies on FTL to handle write distribution. It is supported from kernel 3.8 onwards.

An FTL is found in all flash memory with a SCSI/SATA/PCIe/NVMe interface [[1]](http://accelazh.github.io/ssd/A-Summary-On-SSD-And-FTL), opposed to bare NAND Flash and SmartMediaCards [[2]](http://www.linux-mtd.infradead.org/archive/tech/nand.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Creating a F2FS file system](#Creating_a_F2FS_file_system)
*   [2 Mounting a F2FS file system](#Mounting_a_F2FS_file_system)
*   [3 Grow an F2FS file system](#Grow_an_F2FS_file_system)
*   [4 Checking and repair](#Checking_and_repair)
*   [5 File-based encryption support](#File-based_encryption_support)
*   [6 Known issues](#Known_issues)
    *   [6.1 Long running fsck delays boot](#Long_running_fsck_delays_boot)

## Creating a F2FS file system

In order to create a F2FS file system, [install](/index.php/Install "Install") [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools).

Create the file system:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

where `*/dev/sdxY*` is the target volume to format in F2FS. See [mkfs.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.f2fs.8) for all available options.

## Mounting a F2FS file system

The file system can then be mounted manually or via other mechanisms:

```
# mount /dev/sdxY /mnt/foo

```

## Grow an F2FS file system

When the filesystem is unmounted, it can be grown if the partition is expanded. [Shrinking is not currently supported](https://www.mail-archive.com/linux-f2fs-devel@lists.sourceforge.net/msg04247.html).

First use a [partition tool](/index.php/Partitioning#Partitioning_tools "Partitioning") to resize the partition: for example, suppose the output of the `print` command in the `parted` console for your disk is the following:

```
   Number  Start   End     Size        File system     Name                  Flag
    1      1049kB  106MB   105MB       fat32           EFI system partition  boot, esp
    2      106MB   11,0GB  10,9GB      ext4
    3      11,0GB  12,3GB  1322MB      f2fs
    4      31,0GB  31,3GB  261MB       ext4

```

To resize the `f2fs` partition to occupy all the space up to the fourth one, just give `resizepart 3 31GB` and `exit`. You can now expand the filesystem to fill the new partition using:

```
# resize.f2fs /dev/sdxY

```

where `*/dev/sdxY*` is the target F2FS volume to grow. See [resize.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resize.f2fs.8) for supported options.

**Note:** If you're using GPT, the partition's GUID (seen in `/dev/disk/by-partuuid/`) might change, but the filesystem UUID (seen in `/dev/disk/by-uuid/`) should stay the same.

## Checking and repair

Checking and repairs to f2fs file systems are accomplished with `fsck.f2fs` provided by [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools). See [fsck.f2fs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.f2fs.8) for available switches.

## File-based encryption support

Since Linux 4.2, F2FS natively supports file encryption. Encryption is applied at the directory level, and different directories can use different encryption keys. This is different from both [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), which is block-device level encryption, and from [eCryptfs](/index.php/ECryptfs "ECryptfs"), which is a stacked cryptographic filesystem. To use F2FS's native encryption support, see the [fscrypt](/index.php/Fscrypt "Fscrypt") article.

## Known issues

### Long running fsck delays boot

If the kernel version has changed between boots, the *fsck.f2fs* utility will perform a full file system check which will take longer to finish.[[3]](https://bbs.archlinux.org/viewtopic.php?id=245702)