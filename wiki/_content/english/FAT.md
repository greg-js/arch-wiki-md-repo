From [Wikipedia:File Allocation Table](https://en.wikipedia.org/wiki/File_Allocation_Table "wikipedia:File Allocation Table"):

	File Allocation Table (FAT) is a computer file system architecture and a family of industry-standard file systems utilizing it. The FAT file system is a legacy file system which is simple and robust.[3] It offers good performance even in light-weight implementations, but cannot deliver the same performance, reliability and scalability as some modern file systems. It is, however, supported for compatibility reasons by nearly all currently developed operating systems for personal computers and many mobile devices and embedded systems, and thus is a well-suited format for data exchange between computers and devices of almost any type and age from 1981 up to the present.

## Kernel configurations

Here is an example of the default *mount* configuration in the kernel:

 `$ zgrep -e FAT -e DOS /proc/config.gz | sort -r ` 
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

*   Language settings: CONFIG_FAT_DEFAULT_CODEPAGE, CONFIG_FAT_DEFAULT_IOCHARSET
*   All filenames to lower letters on a FAT partitions if enabled: CONFIG_NCPFS_SMALLDOS
*   Enables support of the FAT file systems: CONFIG_FAT_FS, CONFIG_MSDOS_FS, CONFIG_VFAT_FS
*   Enables support of a FAT partitioned harddisks on 86x PCs: CONFIG_MSDOS_PARTITION

If the partition type detected by mount is VFAT then it will run the `/usr/bin/mount.vfat` script.

 `/usr/bin/mount.vfat` 
```
#!/bin/bash
#mount VFAT with full rw (read-write) permissions for all users
#/usr/bin/mount -i -t vfat -oumask=0000,iocharset=utf8 "$@"
#The above is the same as
mount -i -t vfat -oiocharset=utf8,fmask=0000,dmask=0000 "$@"
```

## See also

*   [MountFATFileSystems](http://www.nslu2-linux.org/wiki/HowTo/MountFATFileSystems)