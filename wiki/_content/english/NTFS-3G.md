Related articles

*   [File systems](/index.php/File_systems "File systems")

[NTFS-3G](http://www.tuxera.com/community/ntfs-3g-download/) is an open source implementation of [Microsoft NTFS](https://en.wikipedia.org/wiki/NTFS "w:NTFS") that includes read *and* write support (the Linux kernel only supports reading NTFS). NTFS-3G developers use the FUSE file system to facilitate development and to help with portability.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Manual mounting](#Manual_mounting)
*   [3 Formatting](#Formatting)
*   [4 Configuring](#Configuring)
    *   [4.1 Default settings](#Default_settings)
    *   [4.2 Linux compatible permissions](#Linux_compatible_permissions)
    *   [4.3 Allowing group/user](#Allowing_group/user)
    *   [4.4 Basic NTFS-3G options](#Basic_NTFS-3G_options)
    *   [4.5 Allowing user to mount](#Allowing_user_to_mount)
*   [5 Resizing NTFS partition](#Resizing_NTFS_partition)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Compressed files](#Compressed_files)
    *   [6.2 Damaged NTFS filesystems](#Damaged_NTFS_filesystems)
    *   [6.3 Metadata kept in Windows cache, refused to mount](#Metadata_kept_in_Windows_cache,_refused_to_mount)
    *   [6.4 Deleting Windows hibernate metadata](#Deleting_Windows_hibernate_metadata)
    *   [6.5 Mount failure](#Mount_failure)
    *   [6.6 Windows mount failure](#Windows_mount_failure)
*   [7 Beta features & releases](#Beta_features_&_releases)
*   [8 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) package.

## Manual mounting

Two options exist when manually mounting NTFS partitions. The traditional:

```
# mount /dev/*your_NTFS_partition* */mount/point*

```

The mount type `ntfs-3g` does not need to be explicitly specified in Arch. The *mount* command by default will use `/usr/bin/mount.ntfs` which is symlinked to `/usr/bin/ntfs-3g` after the ntfs-3g package is installed.

The second option is to call `ntfs-3g` directly:

```
# ntfs-3g /dev/*your_NTFS_partition* */mount/point*

```

See [ntfs-3g(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntfs-3g.8) for the available options.

## Formatting

**Warning:** As always, double check the device path.

```
# mkfs.ntfs -Q -L diskLabel /dev/sd*XY*

```

**Note:** `-Q` speeds up the formatting by not zeroing the drive and not checking for bad sectors.

## Configuring

Your NTFS partition(s) can be setup to mount automatically, or pre-configured to be able to mount in a certain way when you would like them to be mounted. This configuration can be done in the static filesystem configuration ([fstab](/index.php/Fstab "Fstab")) or by the use of udev rules.

### Default settings

Using the default settings will mount the NTFS partition(s) at boot. With this method, **if** the parent folder that it is mounted upon has the proper user or group [permissions](/index.php/Users_and_groups "Users and groups") (e.g. /run/media/<username>/), **then** that user or group will be able to read and write on that partition(s).

 `/etc/fstab` 
```
# <file system>   <dir> <type>    <options>             <dump>  <pass>
/dev/*NTFS-part*  /mnt/windows  ntfs-3g   defaults          0       0

```

### Linux compatible permissions

Permissions on a Linux system are normally set to 755 for folders and 644 for files. It is recommended to keep these permissions in use for the NTFS partition as well if you use the partition on a regular basis. The following example assigns the above permissions to a normal user:

```
# Mount internal Windows partition with linux compatible permissions, i.e. 755 for directories (dmask=022) and 644 for files (fmask=133)
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g uid=*userid*,gid=*groupid*,dmask=022,fmask=133 0 0

```

Alternatively, if the Windows permissions do matter to you, you can use the [ntfsusermap(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntfsusermap.8) command to map Windows users to Linux ones. ntfs-3g will handle the translation of these permissions.

### Allowing group/user

In `/etc/fstab` you can also specify other options like those who are allowed to access (read) the partition. For example, for you to allow people in the `groupid` group to have access:

```
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g   gid=*groupid*,umask=0022    0       0

```

By default, the above line will enable write support for root only. To enable user writing, you have to specify the user who should be granted write permissions. Use the `uid` parameter together with your user id to enable user writing:

```
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g   uid=*userid*,gid=*groupid*,umask=0022    0       0

```

If you are running on a single user machine, you may like to own the file system yourself and grant all possible permissions:

```
/dev/*NTFS-partition*  /mnt/windows  ntfs-3g   uid=*userid*,gid=*groupid*    0       0

```

### Basic NTFS-3G options

For most, the above settings should suffice. Here are a few other options that are general common options for various Linux filesystems. For a complete list, see [ntfs-3g(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntfs-3g.8#OPTIONS).

	[umask](/index.php/Umask "Umask")

	umask is a built-in shell command which automatically sets file permissions on newly created files. For Arch Linux, the default umask for root and user is 0022\. With 0022 new folders have the directory permissions of 755 and new files have permissions of 644\. You can read more about umask permissions [here](http://www.cyberciti.biz/tips/understanding-linux-unix-umask-value-usage.html).

	fmask and dmask

	Like `umask` but defining file and directory respectively individually.

	noauto

	If `noauto` is set, NTFS entries in `/etc/fstab` do not get mounted automatically at boot.

	uid

	The user id. This allows a specific user to have full access to the partition. Your uid can be found with the `id` command.

	big_writes

	This FUSE option enables the use of a 128 KiB write buffer as opposed to the libfuse2 default of 4 KiB. It will reduce the CPU utilization of the ntfs-3g process and generally increase write performance. One should always include it because [it is safe.](https://unix.stackexchange.com/a/544864/73443)

The following option is specific to ntfs-3g only:

	windows_names

	prevents files, directories and extended attributes to be created with a name not allowed by windows.

### Allowing user to mount

By default, *ntfs-3g* requires root rights to mount the filesystem if it is a [block device](/index.php/Block_device "Block device"), even with the `user` option in `/etc/fstab`. See [ntfs-3g-faq](http://www.tuxera.com/community/ntfs-3g-faq/#useroption) for details. The `user` option in the fstab is still required.

**Note:**

*   The [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) package does not have internal FUSE support. Rebuild the package using [ABS](/index.php/ABS "ABS"), or install [ntfs-3g-fuse](https://aur.archlinux.org/packages/ntfs-3g-fuse/).
    *   The longer story is that "user" and "users" work via a setuid `mount` not dropping its setuid privillage so that the block device can be used without root. However, ntfs-3g has a hard-coded restriction in ntfs-3g that bails on setuid if an external libfuse is used.
    *   There is no good technical reason for not allowing setuid for external FUSE besides a mistrust of the library. [This patch](https://github.com/AOSC-Dev/ntfs-3g/commit/c918fb79f9f340bce1a19dacf4b720d19922450d) removes the said restriction.
*   There seems to be an issue with unmounting rights, so you will still need root rights if you need to unmount the filesystem. You can also use `fusermount -u /mnt/*mountpoint*` to unmount the filesystem without root rights. Also, if you use the `*users*` option (plural) in `/etc/fstab` instead of the `user` option, you will be able to both mount and unmount the filesystem using the `mount` and `umount` commands.

For non-blockfiles like normal images, *ntfs-3g* on the command-line should work out-of-the-box with normal user privillages as the underlying FUSE calls are redirected to the setuid-root *fusermount* when direct kernel interaction is unavailable. If it does not work for you, run `ls -l /usr/bin/fusermount`; if the first field is not `-rwsr-xr-x`, it means the setuid bit is gone and has to be reset by `chmod u+s /usr/bin/fusermount`.

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

If you already have Arch Linux installed on your system and simply want to resize an existing NTFS partition, you can use the parted and ntfs-3g packages to do it. Optionally, you can use the GParted GUI after installing the [GParted](/index.php/GParted "GParted") package. At the core of the resizing is the [ntfsresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntfsresize.8) command.

## Troubleshooting

### Compressed files

If you have a Windows 10 partition and when accessing files/directories,

1.  you see broken symbolic links to 'unsupported reparse point', *or*
2.  you see the error message "cannot access <*filename*>: Input/output error" (in this case you see in /var/log/messages "Could not load plugin /usr/lib64/ntfs-3g/ntfs-plugin-80000017.so: Success")

then install [ntfs-3g-system-compression](https://aur.archlinux.org/packages/ntfs-3g-system-compression/). This plugin handles system-compressed files.

There exists some other types of [reparse points](https://en.wikipedia.org/wiki/NTFS_reparse_points "wikipedia:NTFS reparse points") that ntfs-3g does not support by default. See [this page](https://jp-andre.pagesperso-orange.fr/junctions.html#other) for a list of available plugins.

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

To enable writing to the partitions on other operating systems, be sure fast startup is disabled. This can be achieved by issuing as an administrator the command:

```
powercfg /h off

```

You can check the current settings on *Control Panel > Hardware and Sound > Power Options > System Setting > Choose what the power buttons do*. The box *Turn on fast startup* should either be disabled or missing.

### Deleting Windows hibernate metadata

As an alternative to above clean shutdown method, there is a way to completely destroy NTFS metadata that was saved after hibernating. This method is only feasible if you are not able or unwilling to boot into Windows and shut it down completely. This is by placing **remove_hiberfile** option when you are mounting your NTFS file system using ntfs-3g.

```
# mount -t ntfs-3g -o remove_hiberfile /dev/*your_NTFS_partition* */mount/point*

```

**Warning:** Please note that this method means that the saved Windows session will be completely lost. Use this option under your own responsibility.

### Mount failure

If you cannot mount your NTFS partition even when following this guide, try using the [UUID](/index.php/UUID "UUID") instead of device name in `/etc/fstab` for all NTFS partitions. See [fstab#File system UUIDs](/index.php/Fstab#File_system_UUIDs "Fstab") for an example.

### Windows mount failure

Windows will not recognize a NTFS partition that does not have a corresponding partition type. A common pitfall when creating an NTFS partition to work with Windows is forgetting to set the partition type as NTFS. See [fdisk](/index.php/Fdisk "Fdisk") or one of the [partitioning tools](/index.php/Partitioning_tools "Partitioning tools").

## Beta features & releases

There is a [web page](http://jp-andre.pagesperso-orange.fr/advanced-ntfs-3g.html) on "advanced features" (add-ons) [1], maintained by Jean-Pierre André, one of the ntfs-3g authors. That page also provides new versions, not yet incorporated to the official releases.

Currently these add-ons support:

*   System compression
*   OneDrive
*   Duplicated files

In the page [1] there is a pointer to the "updated version" of the system compression plugin [mentioned above](#Compressed_files). In fact, the update is small; all updates are in:

*   README.md
*   configure.ac, with slight modification. See the attachment

The web page [1] is surely written by J.-P. André. The page [NTFS-3G Advanced](https://www.tuxera.com/community/ntfs-3g-advanced/) in the official site in tuxera.com has a link to the [OpenIndiana page](http://jp-andre.pagesperso-orange.fr/openindiana-ntfs-3g.html), which in turn links to [1].

## See also

*   [ntfs-3g(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntfs-3g.8)