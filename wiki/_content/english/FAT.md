Related articles

*   [File systems](/index.php/File_systems "File systems")

From [Wikipedia:File Allocation Table](https://en.wikipedia.org/wiki/File_Allocation_Table "wikipedia:File Allocation Table"):

	File Allocation Table (FAT) is a computer file system architecture and a family of industry-standard file systems utilizing it. The FAT file system is a legacy file system which is simple and robust. It offers good performance even in light-weight implementations, but cannot deliver the same performance, reliability and scalability as some modern file systems. It is, however, supported for compatibility reasons by nearly all currently developed operating systems for personal computers and many mobile devices and embedded systems, and thus is a well-suited format for data exchange between computers and devices of almost any type and age from 1981 up to the present.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 File system creation](#File_system_creation)
*   [2 Kernel configuration](#Kernel_configuration)
*   [3 Writing to FAT32 as normal user](#Writing_to_FAT32_as_normal_user)
*   [4 Detecting FAT type](#Detecting_FAT_type)
*   [5 See also](#See_also)

## File system creation

To create a FAT filesystem, [install](/index.php/Install "Install") [dosfstools](https://www.archlinux.org/packages/?name=dosfstools).

`mkfs.fat` supports creating FAT12, FAT16 and FAT32, see [Wikipedia:File Allocation Table#Types](https://en.wikipedia.org/wiki/File_Allocation_Table#Types "wikipedia:File Allocation Table") for an explanation on their differences. `mkfs.fat` will select the FAT type based on the partition size, to explicitly create a certain type of FAT filesystem use the `-F` option. See [mkfs.fat(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkfs.fat.8) for more information.

**Tip:** For most situations you will want to use FAT32.

Format a partition to FAT32:

```
# mkfs.fat -F 32 /dev/*partition*

```

**Note:** `mkfs.vfat` is a symlink to `mkfs.fat`, they are the same utility.

## Kernel configuration

Here is an example of the default *mount* configuration in the kernel:

 `$ zgrep -e FAT -e DOS /proc/config.gz | sort -r` 
```
# DOS/FAT/NT Filesystems
CONFIG_FAT_FS=m
CONFIG_MSDOS_PARTITION=y
CONFIG_FAT_FS=m
CONFIG_MSDOS_FS=m
CONFIG_VFAT_FS=m
CONFIG_FAT_DEFAULT_CODEPAGE=437
CONFIG_FAT_DEFAULT_IOCHARSET="iso8859-1"
CONFIG_NCPFS_SMALLDOS=y
```

A short description of the options:

*   Language settings: `CONFIG_FAT_DEFAULT_CODEPAGE`, `CONFIG_FAT_DEFAULT_IOCHARSET`
*   All filenames to lower letters on a FAT partitions if enabled: `CONFIG_NCPFS_SMALLDOS`
*   Enables support of the FAT file systems: `CONFIG_FAT_FS`, `CONFIG_MSDOS_FS`, `CONFIG_VFAT_FS`
*   Enables support of a FAT partitioned harddisks on 86x PCs: `CONFIG_MSDOS_PARTITION`

If the partition type detected by mount is VFAT then it will run the `/usr/bin/mount.vfat` script.

 `/usr/bin/mount.vfat` 
```
#!/bin/bash
#mount VFAT with full rw (read-write) permissions for all users
#/usr/bin/mount -i -t vfat -oumask=0000,iocharset=utf8 "$@"
#The above is the same as
mount -i -t vfat -oiocharset=utf8,fmask=0000,dmask=0000 "$@"
```

## Writing to FAT32 as normal user

To write on a FAT32 partition, you must make a few changes to the [fstab](/index.php/Fstab "Fstab") file.

 `/etc/fstab`  `/dev/sd*xY*    /mnt/some_folder  vfat   **user**,rw` 

The `user` option means that any user (even non-root) can mount and unmount the partition `/dev/sd*X*`. `rw` gives read-write access.

For example, if your FAT32 partition is on `/dev/sda9`, and you wish to mount it to `/mnt/fat32`, then you would use:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   **user**,rw` 

Now, any user can mount it with:

```
$ mount /mnt/fat32

```

And unmount it with:

```
$ umount /mnt/fat32

```

Note that FAT does not support Linux file permissions. Each file will also appear to be executable. You may want to use the `showexec` option to only mark Windows executables (com, exe, bat) as executable. See [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) for more options.

## Detecting FAT type

If you need to know which [type of FAT file system](https://en.wikipedia.org/wiki/File_Allocation_Table#Types "wikipedia:File Allocation Table") a partition uses, use the *file* command:

 `# file -s /dev/*partition*`  `/dev/*partition*: DOS/MBR boot sector, code offset 0x3c+2, OEM-ID "mkfs.fat", sectors/cluster 4, root entries 512, sectors 4096 (volumes <=32 MB), Media descriptor 0xf8, sectors/FAT 3, sectors/track 32, heads 64, serial number 0x5bc09c21, unlabeled, **FAT (12 bit)**` 

Alternatively you can use *minfo* from the [mtools](https://www.archlinux.org/packages/?name=mtools) package:

 `# minfo -i /dev/*partition* ::` 
```
device information:
===================
filename="/dev/*partition*"
sectors per track: 32
heads: 64
cylinders: 2

media byte: f8

mformat command line: mformat -t 2 -h 64 -s 32 -i "/dev/*partition*" ::

bootsector information
======================
banner:"mkfs.fat"
sector size: 512 bytes
cluster size: 4 sectors
reserved (boot) sectors: 1
fats: 2
max available root directory slots: 512
small size: 4096 sectors
media descriptor byte: 0xf8
sectors per fat: 3
sectors per track: 32
heads: 64
hidden sectors: 0
big size: 0 sectors
physical drive id: 0x80
reserved=0x0
dos4=0x29
serial number: 5BC09C21
disk label="NO NAME    "
disk type="**FAT12**   "

```

## See also

*   [MountFATFileSystems](http://www.nslu2-linux.org/wiki/HowTo/MountFATFileSystems)