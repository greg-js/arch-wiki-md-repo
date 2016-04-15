*mount* is an application used to access file systems, partition tables, and shared folders. It can mount file systems supported by the Linux kernel, but can be extended with other drivers or applications, such as [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) for mounting [NTFS](/index.php/NTFS "NTFS") filesystems.

## Contents

*   [1 Supported file systems](#Supported_file_systems)
*   [2 Mounting a file system](#Mounting_a_file_system)
*   [3 Seeing what's been mounted](#Seeing_what.27s_been_mounted)
    *   [3.1 mtab](#mtab)
    *   [3.2 mtab File Definition](#mtab_File_Definition)
*   [4 Alternatives that can be used to change the default options for mounting](#Alternatives_that_can_be_used_to_change_the_default_options_for_mounting)
*   [5 Some other file systems](#Some_other_file_systems)
    *   [5.1 VFAT, FAT, DOS](#VFAT.2C_FAT.2C_DOS)
    *   [5.2 NTFS](#NTFS)
*   [6 See also](#See_also)

## Supported file systems

To view the supported file systems by your kernel and their configurations:

```
$ zgrep -e 'FS_' -e _FS -e 'CONFIG_ISO' -e  '_NLS=' -e CONFIG_NLS_ISO /proc/config.gz

```

You can read about supported file systems by the mount command in the manual: `man mount`.

## Mounting a file system

The file [/etc/fstab](/index.php//etc/fstab "/etc/fstab") (see fstab(5)), may contain lines describing what devices are usually mounted where, using which options. A filesystem specified in `/etc/fstab` will be mounted at boot time, with some exceptions. For example, any device whose line contains the `noauto` option will not be mounted. This is useful for things like partitions for other OSes. External devices that are to be mounted when present, but ignored if absent, may require the `nofail` option. See [external devices](/index.php/Fstab#External_devices "Fstab") for more information.

When mounting a filesystem mentioned in fstab or mtab, it is sufficient to give only the device, or only the mount point.

```
# mount /dev/sdXY 

```

The mount program does not read the /etc/fstab file if device (or LABEL/UUID) and dir (mount point) are specified. For example:

```
# mount /dev/foo /dir

```

If the mount point does not exist, it may be necessary to create it first. To mount to MYDIR1:

```
# mkdir /mnt/mydir1
# mount /dev/sdXY /mnt/mydir1

```

See [/etc/fstab](/index.php//etc/fstab "/etc/fstab"), `man fstab` and `man mount` for more information.

## Seeing what's been mounted

You can see what's been mounted by looking at the `/etc/mtab` and `/proc/mounts` files.

### mtab

The [/etc/mtab](https://en.wikipedia.org/wiki/Mtab "wikipedia:Mtab") is a system-generated file created and updated by the **mount** application whenever any [file system](/index.php/File_system "File system") is mounted or unmounted.

It lists each device node, mount point and mount options used. Whenever the `mount` program is executed without any arguments, this file is printed.

**Note:** The `/etc/mtab` file is meant to be used to display the status of currently mounted file systems only. It should not be manually modified.

### mtab File Definition

Each line in the file represents a file system that is currently mounted and displays the following information:

*   The file system.
*   The mount point.
*   The file system type.
*   Mount options used while mounting the file system.

## Alternatives that can be used to change the default options for mounting

Here are a few examples about how to extend mount functionality and modify default options. To change the default settings in the [kernel](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation") you will need to compile the kernel yourself. If the script does not exist then the default options will be used.

*   [By compiling the kernel yourself](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation")
*   By using scripts
*   [By editing fstab](/index.php/Fstab "Fstab")
*   [By creating udev / udisks rules](/index.php/Udev "Udev") - device manager for the Linux kernel.
*   Manually mounting as shown above

The *mount.X* scripts or symbolic links, where *X* is the name of a file system, can be used to alter the default *mount* options for almost any of its supported file systems. Use the `-i` option to ignore *mount.X* scripts and also for avoiding of the loops(starting *mount.X* non-stop) when *mount* is inside the script, e.g. `mount -i -t reiserfs /dev/sd*XY* /mnt/sd*XY*`.

There are two ways to list available altered mount settings:

*   Write *mount* and press a `Tab` key.
*   Execute `ls /usr/bin/mount.*`.

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
*   Manual for the *mount* command: [linux.die.net](http://linux.die.net/man/8/mount)
*   [Wikipedia:Mount (Unix)](https://en.wikipedia.org/wiki/Mount_(Unix) "wikipedia:Mount (Unix)")
*   Creating and using disk images mini-howto: [darkdust.net](http://darkdust.net/writings/diskimagesminihowto)