[mount](https://en.wikipedia.org/wiki/Mount_(Unix) "w:Mount (Unix)") is an application used to access file systems, partition tables, and shared folders. It can mount file systems supported by the Linux kernel, but can be extended with other drivers or applications, such as [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) for mounting [NTFS](/index.php/NTFS "NTFS") filesystems. See [mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html).

## Contents

*   [1 Usage](#Usage)
*   [2 Some other file systems](#Some_other_file_systems)
    *   [2.1 VFAT, FAT, DOS](#VFAT.2C_FAT.2C_DOS)
    *   [2.2 NTFS](#NTFS)
*   [3 See also](#See_also)

## Usage

See [File systems#Mount a file system](/index.php/File_systems#Mount_a_file_system "File systems").

## Some other file systems

### VFAT, FAT, DOS

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

See also: [more details about mounting of the FAT file systems](http://www.nslu2-linux.org/wiki/HowTo/MountFATFileSystems).

### NTFS

The default configuration:

 `$ zgrep ^CONFIG_NTFS  /proc/config.gz` 
```
CONFIG_NTFS_FS=m
CONFIG_NTFS_RW=y
```

The kernel config option `CONFIG_NTFS_RW=y` enables read-write support for [NTFS](https://en.wikipedia.org/wiki/NTFS "wikipedia:NTFS") file systems. It also means the kernel is predefined to use the [ntfs-3g](/index.php/Ntfs "Ntfs") driver in read-write mode. The build in support of the NTFS file systems by the kernel is *read-only* even if read-write is activated by an option.

**Note:**

*   When [ntfs-3g](/index.php/Ntfs "Ntfs") is being installed it might create a symlink `/usr/bin/mount.ntfs` to the `/usr/bin/ntfs-3g`.
*   The [ntfs-3g](/index.php/Ntfs "Ntfs") mount tool supports many of the same command line options as the linux standard *mount* utility, but is specialized on mounting of the [NTFS](https://en.wikipedia.org/wiki/NTFS "wikipedia:NTFS") formated partitions.
*   By default on mounting the [ntfs-3g](/index.php/Ntfs "Ntfs") driver gives the full read-write permissions to the all users. In some situations access with a full permission rights can cause the damage, see [NTFS troubleshooting](/index.php/Ntfs#Troubleshooting "Ntfs").

The default mount options can be altered when running `mount.ntfs` by renaming the `/usr/bin/mount.ntfs` symlink if exists and creating a script in its place with a preferred options or use the *-i* option (`mount -i -t ntfs`) to ignore all the *mount.X* files and use the natively supported functionality by the kernel. This example will mount NTFS as a read-only:

 `/usr/bin/mount.ntfs` 
```
#!/bin/bash
#mount -i -oro "$@"
#mount with a read-only rights
ntfs-3g -oro  "$@" & disown
```

See `man 8 ntfs-3g` for more information about the ntfs-3g driver.

You can add more actions for when an external storage device, such as a USB drive or image file (ISO, img, dd), is mounted by using scripts.

## See also

*   Documentation of file systems supported by kernel: [kernel.org](https://www.kernel.org/doc/Documentation/filesystems/)
*   [Wikipedia:Mount (Unix)](https://en.wikipedia.org/wiki/Mount_(Unix) "wikipedia:Mount (Unix)")
*   Creating and using disk images mini-howto: [darkdust.net](http://darkdust.net/writings/diskimagesminihowto)