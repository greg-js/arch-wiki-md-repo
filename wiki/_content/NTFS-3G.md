# NTFS-3G

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [File systems](/index.php/File_systems "File systems")
*   [Mount](/index.php/Mount "Mount")

[NTFS-3G](http://www.tuxera.com/community/ntfs-3g-download/) is an open source implementation of Microsoft's NTFS file system that includes read and write support. NTFS-3G developers use the FUSE file system to facilitate development and to help with portability.

## Contents

*   [1 Installation](#Installation)
*   [2 Manual mounting](#Manual_mounting)
*   [3 Formatting](#Formatting)
*   [4 Configuring](#Configuring)
    *   [4.1 Default settings](#Default_settings)
    *   [4.2 Linux compatible permissions](#Linux_compatible_permissions)
    *   [4.3 Allowing group/user](#Allowing_group.2Fuser)
    *   [4.4 Basic NTFS-3G options](#Basic_NTFS-3G_options)
    *   [4.5 Allowing user to mount](#Allowing_user_to_mount)
    *   [4.6 ntfs-config](#ntfs-config)
*   [5 Resizing NTFS partition](#Resizing_NTFS_partition)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Damaged NTFS filesystems](#Damaged_NTFS_filesystems)
    *   [6.2 Metadata kept in Windows cache, refused to mount](#Metadata_kept_in_Windows_cache.2C_refused_to_mount)
    *   [6.3 Mount failure](#Mount_failure)
*   [7 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) package.

## Manual mounting

Two options exist for manually mounting NTFS partitions. The traditional:

```
# mount -t ntfs-3g /dev/_your_NTFS_partition_ _/mount/point_

```

Mount type `ntfs-3g` does not need to be explicitly specified in Arch. The _mount_ command by default will use `/usr/bin/mount.ntfs` which is symlinked to `/usr/bin/ntfs-3g` after the ntfs-3g package is installed.

The second option is to call `ntfs-3g` directly:

```
# ntfs-3g /dev/_your_NTFS_partition_ _/mount/point_

```

## Formatting

**Warning:** As always, double check the device path.

```
# mkfs.ntfs -Q -L diskLabel /dev/sd_XY_

```

**Note:** `-Q` speeds up the formatting by not zeroing the drive and not checking for bad sectors.

## Configuring

Your NTFS partition(s) can be setup to mount automatically, or pre-configured to be able to mount in a certain way when you would like them to be mounted. This configuration can be done in the static filesystem configuration ([fstab](/index.php/Fstab "Fstab")) or by the use of udev rules.

### Default settings

Using the default settings will mount the NTFS partition(s) at boot. With this method, **if** the parent folder that it is mounted upon has the proper user or group [permissions](/index.php/Users_and_groups "Users and groups"), then that user or group will be able to read and write on that partition(s).

Put this in `/etc/fstab`:

```
# <file system>   <dir>		<type>    <options>             <dump>  <pass>
/dev/_NTFS-part_  /mnt/windows  ntfs-3g   defaults		  0       0

```

### Linux compatible permissions

Permissions on a Linux system are normally set to 755 for folders and 644 for files. It is recommended to keep these permissions in use for the NTFS partition as well if you use the partition on a regular basis. The following example assigns the above permissions to a normal user:

```
# Mount internal Windows partition with linux compatible permissions, i.e. 755 for directories (dmask=022) and 644 for files (fmask=133)
UUID=01CD2ABB65E17DE0 /run/media/user1/Windows ntfs-3g uid=user1,gid=users,dmask=022,fmask=133 0 0

```

### Allowing group/user

In `/etc/fstab` you can also specify other options like those who are allowed to access (read) the partition. For example, for you to allow people in the `users` group to have access:

```
/dev/_NTFS-partition_  /mnt/windows  ntfs-3g   gid=users,umask=0022    0       0

```

By default, the above line will enable write support for root only. To enable user writing, you have to specify the user who should be granted write permissions. Use the `uid` parameter together with your username to enable user writing:

```
/dev/_NTFS-partition_  /mnt/windows  ntfs-3g   uid=_username_,gid=users,umask=0022    0       0

```

If you are running on a single user machine, you may like to own the file system yourself and grant all possible permissions:

```
/dev/_NTFS-partition_  /mnt/windows  ntfs-3g   uid=_username_,gid=users    0       0

```

### Basic NTFS-3G options

For most, the above settings should suffice. Here are a few other options that are general common options for various Linux filesystems. For a complete list, see [this](http://www.tuxera.com/community/ntfs-3g-manual/#6)

[umask](/index.php/Umask "Umask")

umask is a built-in shell command which automatically sets file permissions on newly created files. For Arch Linux, the default umask for root and user is 0022\. With 0022 new folders have the directory permissions of 755 and new files have permissions of 644\. You can read more about umask permissions [here](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html).

noauto

If `noauto` is set, NTFS entries in `/etc/fstab` do not get mounted automatically at boot.

uid

The user id number. This allows a specific user to have full access to the partition. Your uid can be found with the `id` command.

fmask and dmask

Like `umask` but defining file and directory respectively individually.

### Allowing user to mount

By default, _ntfs-3g_ requires root rights to mount the filesystem, even with the "user" option in `/etc/fstab`, the reason why can be found [here](http://www.tuxera.com/community/ntfs-3g-faq/#unprivileged). The user option in the fstab is still required. To be able to mount as user, a few tweaks need to be made:

First, check that you have access to the mount block you want to use, the easiest way to do that is to be in the disk groups with the following command:

```
# gpasswd -a username disk

```

**Note:** Groups rights sometimes requires rebooting to kick in.

You also need access to the mountpoint you want to use. Since we're going to mount something as user on this mountpoint, we might as well own it:

```
# chown _user_ /mnt/_mountpoint_

```

Second, you need a NTFS-3G driver compiled with integrated FUSE support. The ntfs-3g package from the official repositories does not have this support, but [ntfs-3g-fuse](https://aur.archlinux.org/packages/ntfs-3g-fuse/)<sup><small>AUR</small></sup> does.

You should now be able to mount your NTFS partition without root rights.

**Note:** There seems to be an issue with unmounting rights, so you will still need root rights if you need to unmount the filesystem. You can also use `fusermount -u /mnt/_mountpoint_` to unmount the filesystem without root rights. Also, if you use the `_users_` option (plural) in `/etc/fstab` instead of the `user` option, you will be able to both mount and unmount the filesystem using the `mount` and `umount` commands.

### ntfs-config

[ntfs-config](https://aur.archlinux.org/packages/ntfs-config/)<sup><small>AUR</small></sup> is a program that may be able to help configure your NTFS partition(s) if other methods do not work.

## Resizing NTFS partition

**Note:** Please ensure you have a backup before attempting this if your data is important!

Most systems that are purchased already have [Windows](https://en.wikipedia.org/wiki/Windows "wikipedia:Windows") installed on it, and some people would prefer not wipe it off completely when doing an Arch Linux installation. For this reason, among others, it is useful to resize the existing Windows partition to make room for a Linux partition or two. This is often accomplished with a [Live CD](https://en.wikipedia.org/wiki/Live_CD "wikipedia:Live CD") or bootable USB thumb drive.

For Live CDs the typical procedure is to download an ISO file, burn it to a CD, and then boot from it. [InfraRecorder](http://infrarecorder.org/) is a free (as in GPL3) CD/DVD burning application for Windows which fits the bill nicely. If you would rather use a bootable USB media instead, see [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media") for methods to create bootable USB stick.

There are a number of bootable CD/USB images avaliable. This list is not exhaustive, but is a good place to start:

*   **[GParted](https://en.wikipedia.org/wiki/GParted "wikipedia:GParted")** — Small bootable GNU/Linux distribution for x86 based computers. It enables you to use all the features of the latest versions of the GParted application. Does not include additional packages System Rescue CD may incorporate, and disk encryption schemes may not be supported.

[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) ||

*   **[Parted Magic](https://en.wikipedia.org/wiki/Parted_Magic "wikipedia:Parted Magic")** — Very good complete hard disk management solution. With the Partition Editor you can re-size, copy, and move partitions. You can grow or shrink your C: drive. Create space for new operating systems. Attempt data rescue from lost partitions.

[http://partedmagic.com/](http://partedmagic.com/) ||

*   **[SystemRescueCD](https://en.wikipedia.org/wiki/SystemRescueCD "wikipedia:SystemRescueCD")** — Good tool to have, and works seamlessly in most cases. Once booted, run GParted and the rest should be fairly obvious.

[http://www.sysresccd.org/](http://www.sysresccd.org/) ||

Note that the important programs for resizing NTFS partitions include ntfs-3g and a utility like (G)parted or fdisk, provided by the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package. Unless you are an "advanced" user it is advisable to use a tool like GParted to perform any resize operations to minimize the chance of data loss due to user error.

If you already have Arch Linux installed on your system and simply want to resize an existing NTFS partition, you can use the parted and ntfs-3g packages to do it. Optionally, you can use the GParted GUI after installing the [GParted](/index.php/GParted "GParted") package.

## Troubleshooting

### Damaged NTFS filesystems

If an NTFS filesystem has errors on it, NTFS-3G will mount it as read-only. To fix an NTFS filesystem, load Windows and run its disk checking program, chkdsk. Take in account that ntfsfix can only repair some errors. If it fails, chkdsk will probably succeed.

To fix the NTFS file system, the device must already be unmounted. For example, to fix an NTFS partition residing in `/dev/sda2`:

```
# umount /dev/sda2
# ntfsfix /dev/sda2
Mounting volume... OK
Processing of $MFT and $MFTMirr completed successfully.
NTFS volume version is 3.1.
NTFS partition /dev/sda2 was processed successfully.
# mount /dev/sda2

```

If all went well, the volume will now be writable.

### Metadata kept in Windows cache, refused to mount

When dual booting with Windows 8 or 10, trying to mount a partition that is visible to Windows may yield the following error:

```
The disk contains an unclean file system (0, 0).
Metadata kept in Windows cache, refused to mount.
Failed to mount '/dev/sdc1': Operation not permitted
The NTFS partition is in an unsafe state. Please resume and shutdown
Windows fully (no hibernation or fast restarting), or mount the volume
read-only with the 'ro' mount option.

```

The problem is due to a feature introduced in Windows 8 called "fast startup". When fast startup is enabled, part of the metadata of all mounted partitions are restored to the state they were at the previous closing down. As a consequence, changes made on Linux may be lost. This can happen to any NTFS partition when selecting "Shut down" or "Hibernate" under Windows 8 or 10\. Leaving Windows by selecting "Restart", however, is apparently safe.

To enable writing to the partitions on other operating systems, be sure fast restart is disabled. This can be achieved by issuing as an administrator the command:

```
powercfg /h off

```

You can check the current settings on _Control Panel > Hardware and Sound > Power Options > System Setting > Choose what the power buttons do_. The box _Turn on fast startup_ should either be disabled or missing.

### Mount failure

If you cannot mount your NTFS partition even when following this guide, try using the [UUID](/index.php/UUID "UUID") instead of device name in `/etc/fstab` for all NTFS partitions. Here's an fstab [example](/index.php/Fstab#UUIDs "Fstab").

## See also

*   [Official NTFS-3G manual](http://www.tuxera.com/community/ntfs-3g-manual/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=NTFS-3G&oldid=412749](https://wiki.archlinux.org/index.php?title=NTFS-3G&oldid=412749)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")