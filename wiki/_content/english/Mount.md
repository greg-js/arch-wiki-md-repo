[mount](https://en.wikipedia.org/wiki/Mount_(Unix) "w:Mount (Unix)") is an application used to access file systems, partition tables, and shared folders. It can mount file systems supported by the Linux kernel, but can be extended with other drivers or applications, such as [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) for mounting [NTFS](/index.php/NTFS "NTFS") filesystems. See [mount(8)](http://man7.org/linux/man-pages/man8/mount.8.html).

## Contents

*   [1 Usage](#Usage)
    *   [1.1 Listing mounted file systems](#Listing_mounted_file_systems)
    *   [1.2 Alternatives to change the default mount options](#Alternatives_to_change_the_default_mount_options)
*   [2 Some other file systems](#Some_other_file_systems)
    *   [2.1 VFAT, FAT, DOS](#VFAT.2C_FAT.2C_DOS)
    *   [2.2 NTFS](#NTFS)
*   [3 See also](#See_also)

## Usage

The [fstab](/index.php/Fstab "Fstab") file may contain lines describing what devices are usually mounted where, using which options. A [file system](/index.php/File_system "File system") specified in `/etc/fstab` will be mounted at boot time, with some exceptions. For example, any device whose line contains the `noauto` option will not be mounted. This is useful for things like partitions for other OSes.

External devices that are to be mounted when present, but ignored if absent, may require the `nofail` option. See [external devices](/index.php/Fstab#External_devices "Fstab") for more information.

**Note:** Supported file systems are listed in `/proc/filesystems`.

When mounting a file system mentioned in fstab or mtab, it is sufficient to give only the device, or only the mount point. For example, to mount `/dev/sdb1`:

```
# mount /dev/*sdb1*

```

The mount program does not read the `/etc/fstab` file if device (or [LABEL/UUID](/index.php/Persistent_block_device_naming "Persistent block device naming")) and directory (mount point) are specified. For example:

```
# mount /dev/*sdb1* */mnt/mydir*

```

If the mount point does not exist, it may be necessary to create it first. For example:

```
# mkdir */mnt/mydir*
# mount /dev/*sdb1* */mnt/mydir*

```

### Listing mounted file systems

Mounted file systems are visible from [/etc/mtab](https://en.wikipedia.org/wiki/Mtab "wikipedia:Mtab"), which is a symbolic link to `/proc/self/mounts`. See also [findmnt(8)](http://man7.org/linux/man-pages/man8/findmnt.8.html).

The [/etc/mtab](https://en.wikipedia.org/wiki/Mtab "wikipedia:Mtab") is a system-generated file created and updated by the **mount** application whenever any [file system](/index.php/File_system "File system") is mounted or unmounted.

Whenever the `mount` program is executed without any arguments, this file is printed. Each line in the file represents a file system that is currently mounted and displays the following information:

*   device node
*   mount point
*   file system type
*   Mount options used while mounting the file system.

**Note:** The `/etc/mtab` file is meant to be used to display the status of currently mounted file systems only. It should not be modified manually.

### Alternatives to change the default mount options

A few examples about how to extend mount functionality and modify default options:

*   [By editing fstab](/index.php/Fstab "Fstab") to include the desired mount options
*   [By creating udev / udisks rules](/index.php/Udev "Udev") - mostly useful for removable devices
*   Mounting manually / by using scripts

	The *mount.X* scripts or symbolic links, where *X* is the name of a file system, can be used to alter the default *mount* options for almost any of its supported file systems. Option `-i` is used to let the *mount* command ignore *mount.X* scripts and must also be used inside *mount.X* scripts for any *mount* command.

	There are two ways to list the available scripts:

*   Write *mount* and press a `Tab` key.
*   Execute `ls /usr/bin/mount.*`.

*   [By compiling the kernel yourself](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System")

	To change the default settings in the kernel, you will need to compile it yourself.

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