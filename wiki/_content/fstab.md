# fstab

Related articles

*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")
*   [File systems](/index.php/File_systems "File systems")
*   [Mount](/index.php/Mount "Mount")
*   [tmpfs](/index.php/Tmpfs "Tmpfs")
*   [swap](/index.php/Swap "Swap")

The [/etc/fstab](https://en.wikipedia.org/wiki/Fstab "wikipedia:Fstab") file can be used to define how disk partitions, various other block devices, or remote filesystems should be mounted into the filesystem.

Each filesystem is described in a separate line. These definitions will be converted into [systemd](/index.php/Systemd "Systemd") mount units dynamically at boot, and when the configuration of the system manager is reloaded. The default setup will automatically [fsck](/index.php/Fsck "Fsck") and mount filesystems before starting services that need them to be mounted. For example, systemd automatically makes sure that remote filesystem mounts like [NFS](/index.php/NFS "NFS") or [Samba](/index.php/Samba "Samba") are only started after the network has been set up. Therefore, local and remote filesystem mounts specified in `/etc/fstab` should work out of the box. See `man 5 systemd.mount` for details.

The `mount` command will use fstab, if just one of either directory or device is given, to fill in the value for the other parameter. When doing so, mount options which are listed in fstab will also be used.

## Contents

*   [1 File example](#File_example)
*   [2 Field definitions](#Field_definitions)
*   [3 Identifying filesystems](#Identifying_filesystems)
    *   [3.1 Kernel name descriptors](#Kernel_name_descriptors)
    *   [3.2 Labels](#Labels)
    *   [3.3 UUIDs](#UUIDs)
    *   [3.4 GPT labels](#GPT_labels)
    *   [3.5 GPT UUIDs](#GPT_UUIDs)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Automount with systemd](#Automount_with_systemd)
    *   [4.2 External devices](#External_devices)
    *   [4.3 Filepath spaces](#Filepath_spaces)
    *   [4.4 atime options](#atime_options)
    *   [4.5 Writing to FAT32 as Normal User](#Writing_to_FAT32_as_Normal_User)
    *   [4.6 Remounting the root partition](#Remounting_the_root_partition)
    *   [4.7 bind mounts](#bind_mounts)
*   [5 See also](#See_also)

## File example

A simple `/etc/fstab`, using kernel name descriptors:

 `/etc/fstab` 

```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
/dev/sda1              /             ext4      defaults,noatime      0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      defaults,noatime      0      2
```

## Field definitions

Each line in the `/etc/fstab` file contains the following fields separated by spaces or tabs:

```
_file_system_    _dir_    _type_    _options_    _dump_    _pass_

```

	_file system_

	The partition or storage device to be mounted.

	_dir_

	The mountpoint where <file system> is mounted to.

	_type_

	The file system type of the partition or storage device to be mounted. Many different file systems are supported: `ext2`, `ext3`, `ext4`, `btrfs`, `reiserfs`, `xfs`, `jfs`, `smbfs`, `iso9660`, `vfat`, `ntfs`, `swap` and `auto`. The `auto` type lets the mount command guess what type of file system is used. This is useful for optical media (CD/DVD).

	_options_

	Mount options of the filesystem to be used. See the [mount man page](http://man7.org/linux/man-pages/man8/mount.8.html#FILESYSTEM-INDEPENDENT_MOUNT%20OPTIONS). Please note that some options are specific to filesystems; to discover them see below in the aforementioned mount man page.

	_dump_

	Used by the dump utility to decide when to make a backup. Dump checks the entry and uses the number to decide if a file system should be backed up. Possible entries are 0 and 1\. If 0, dump will ignore the file system; if 1, dump will make a backup. Most users will not have dump installed, so they should put 0 for the _dump_ entry.

	_pass_

	Used by [fsck](/index.php/Fsck "Fsck") to decide which order filesystems are to be checked. Possible entries are 0, 1 and 2\. The root file system should have the highest priority 1 (unless its type is [btrfs](/index.php/Btrfs "Btrfs"), in which case this field should be 0) - all other file systems you want to have checked should have a 2\. File systems with a value 0 will not be checked by the fsck utility.

## Identifying filesystems

There are different ways to identify filesystems that will be mounted. `/etc/fstab` does support several methods: kernel name descriptor, label or UUID, and GPT labels and UUID for GPT disks. UUID must be privileged over kernel name descriptors and labels. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for more explanations. It is recommended to read that article first before continuing with this article.

In this section, we will describe how to mount filesystems using all the mount methods available via examples. The output of the commands `lsblk -f` and `blkid` used in the following examples are available in the article [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"). If you have not read that article yet, please read it now.

### Kernel name descriptors

Run `lsblk -f` to list the partitions and prefix the values in the _NAME_ column with `/dev/`.

 `/etc/fstab` 

```
# <file system> <dir> <type> <options>                                                                                            <dump> <pass>
/dev/sda1       /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
/dev/sda2       /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
/dev/sda3       /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
/dev/sda4       none  swap   defaults                                                                                             0      0

```

### Labels

Run `lsblk -f` to list the partitions, and prefix the values in the _LABEL_ column with `LABEL=`:

 `/etc/fstab` 

```
# <file system> <dir> <type> <options>                                                                                            <dump> <pass>
LABEL=EFI       /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
LABEL=SYSTEM    /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
LABEL=DATA      /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
LABEL=SWAP      none  swap   defaults                                                                                             0      0

```

**Note:** If any of your fields contains spaces, see [#Filepath spaces](#Filepath_spaces).

### UUIDs

Run `lsblk -f` to list the partitions, and prefix the values in the _UUID_ column with `UUID=`:

 `/etc/fstab` 

```
# <file system>                           <dir> <type> <options>                                                                                            <dump> <pass>
UUID=CBB6-24F2                            /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
UUID=0a3407de-014b-458b-b5c1-848e92a327a3 /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
UUID=b411dc99-f0a0-4c87-9e05-184977be8539 /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
UUID=f9fe0b69-a280-415d-a03a-a32752370dee none  swap   defaults                                                                                             0      0

```

**Tip:** If you would like to return just the UUID of a specific partition: $ lsblk -no UUID /dev/sda2

### GPT labels

Run `blkid` to list the partitions, and use the _PARTLABEL_ values without the quotes:

 `/etc/fstab` 

```
# <file system>                      <dir> <type> <options>                                                                                            <dump> <pass>
PARTLABEL=EFI\040SYSTEM\040PARTITION /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
PARTLABEL=GNU/LINUX                  /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
PARTLABEL=HOME                       /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
PARTLABEL=SWAP                       none  swap   defaults                                                                                             0      0

```

**Note:** If any of your fields contains spaces, see [#Filepath spaces](#Filepath_spaces).

### GPT UUIDs

Run `blkid` to list the partitions, and use the _PARTUUID_ values without the quotes:

 `/etc/fstab` 

```
# <file system>                               <dir> <type> <options>                                                                                            <dump> <pass>
PARTUUID=d0d0d110-0a71-4ed6-936a-304969ea36af /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
PARTUUID=98a81274-10f7-40db-872a-03df048df366 /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
PARTUUID=7280201c-fc5d-40f2-a9b2-466611d3d49e /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
PARTUUID=039b6c1c-7553-4455-9537-1befbc9fbc5b none  swap   defaults                                                                                             0      0

```

## Tips and tricks

### Automount with systemd

If you have a large `/home` partition, it might be better to allow services that do not depend on `/home` to start while `/home` is checked by _fsck_. This can be achieved by adding the following options to the `/etc/fstab` entry of your `/home` partition:

```
noauto,x-systemd.automount

```

This will fsck and mount `/home` when it is first accessed, and the kernel will buffer all file access to `/home` until it is ready.

**Note:** This will make your `/home` filesystem type `autofs`, which is ignored by [mlocate](/index.php/Mlocate "Mlocate") by default. The speedup of automounting `/home` may not be more than a second or two, depending on your system, so this trick may not be worth it.

The same applies to remote filesystem mounts. If you want them to be mounted only upon access, you will need to use the `noauto,x-systemd.automount` parameters. In addition, you can use the `x-systemd.device-timeout=#` option to specify a timeout in case the network resource is not available.

**Note:** If you intend to use the `exec` flag with automount, you should remove the `user` flag for it to work properly as found in the course of a [Fedora Bug Report](https://bugzilla.redhat.com/show_bug.cgi?id=769636)

If you have encrypted filesystems with keyfiles, you can also add the `noauto` parameter to the corresponding entries in `/etc/crypttab`. _systemd_ will then not open the encrypted device on boot, but instead wait until it is actually accessed and then automatically open it with the specified keyfile before mounting it. This might save a few seconds on boot if you are using an encrypted RAID device for example, because systemd does not have to wait for the device to become available. For example:

 `/etc/crypttab`  `data /dev/md0 /root/key noauto` 

You may also specify an idle timeout for a mount with the `x-systemd.idle-timeout` flag. For example:

```
noauto,x-systemd.automount,x-systemd.idle-timeout=1min

```

This will make systemd unmount the mount after it has been idle for 1 minute.

### External devices

External devices that are to be mounted when present but ignored if absent may require the `nofail` option. This prevents errors being reported at boot. For example:

 `/etc/fstab`  `/dev/sdg1        /media/backup    jfs    defaults,nofail,x-systemd.device-timeout=1    0  2` 

As of systemd 219, the `nofail` option is best combined with the `x-systemd.device-timeout` option. This is because the default device timeout is 90 seconds, so a disconnected external device with only `nofail` will make your boot take 90 seconds longer, unless you reconfigure the timeout as shown. Make sure not to set the timeout to 0, as this translates to infinite timeout.

If your external device requires another systemd unit to be loaded (for example the network for a network share) you can use `x-systemd.requires=x` combined with `x-systemd.automount`to postpone automounting until after the unit is available. For example:

 `/etc/fstab`  `//host/share        /net/share        cifs        noauto,nofail,x-systemd.automount,x-systemd.requires=network-online.target,x-systemd.device-timeout=10,workgroup=workgroup,credentials=/foo/credentials        0 0` 

### Filepath spaces

Since spaces are used in `fstab` to delimit fields, if any field (_PARTLABEL_, _LABEL_ or the mount point) contains spaces, these spaces must be replaced by escape characters `\` followed by the 3 digit octal code `040`:

 `/etc/fstab` 

```
UUID=47FA-4071     /home/username/Camera<font color="grey">\040</font>Pictures   vfat  defaults,noatime       0  0
/dev/sda7          /media/100<font color="grey">\040</font>GB<font color="grey">\040</font>(Storage)       ext4  defaults,noatime,user  0  2
```

### atime options

The use of `noatime`, `nodiratime` or `relatime` can impact drive performance.

*   The `strictatime` option updates the _atime_ of the files every time they are accessed. This is more purposeful when Linux is used for servers; it does not have much value for desktop use. The drawback about the `strictatime` option is that even reading a file from the page cache (reading from memory instead of the drive) will still result in a write!

	Using the `noatime` option fully disables writing file access times to the drive every time you read a file. This works well for almost all applications, except for a rare few like [Mutt](/index.php/Mutt "Mutt") that needs such information. For mutt, you should only use the `relatime` option.

	The `nodiratime` option disables the writing of file access times only for directories while other files still get access times written.

**Note:** `noatime` already includes `nodiratime`. [You do not need to specify both](http://lwn.net/Articles/244941/).

*   `relatime` enables the writing of file access times only when the file is being modified (unlike `noatime` where the file access time will never be changed and will be older than the modification time). The best compromise might be the use this option since programs like [Mutt](/index.php/Mutt "Mutt") will continue to work, but you will still have a performance boost as the files will not get access times updated unless they are modified. This option is used when the `defaults` keyword option, `atime` option (which means to use the kernel default, which is relatime; see `man 8 mount` and [[1]](http://en.wikipedia.org/wiki/Stat_%28system_call%29#Solutions)) or no options at all are specified in _fstab_ for a given mount point.

### Writing to FAT32 as Normal User

To write on a FAT32 partition, you must make a few changes to your `/etc/fstab` file.

 `/etc/fstab`  `/dev/sdxY    /mnt/some_folder  vfat   user,rw,umask=000              0  0` 

The `user` flag means that any user (even non-root) can mount and unmount the partition `/dev/sdX`. `rw` gives read-write access; `umask` option removes selected rights - for example `umask=111` remove executable rights. The problem is that this entry removes executable rights from directories too, so we must correct it by `dmask=000`. See also [Umask](/index.php/Umask "Umask").

Without these options, all files will be executable. You can use the option `showexec` instead of the umask and dmask options, which shows all Windows executables (com, exe, bat) in executable colours.

For example, if your FAT32 partition is on `/dev/sda9`, and you wish to mount it to `/mnt/fat32`, then you would use:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   user,rw,umask=111,dmask=000    0  0` 

### Remounting the root partition

If for some reason the root partition has been improperly mounted read only, remount the root partition with read-write access with the following command:

```
# mount -o remount,rw /

```

### bind mounts

**Note:** Binding a directory to a different location is not recognised by almost any program, so for instance careless commands like `rm -r *` will also erase any content from the original location. So softlinks should be the preferable way in most cases. If you need permission to a directory on a Btrfs and softlinks are not sufficient its [subvolumes](/index.php/Btrfs#Sub-volumes "Btrfs") faciliate extended capabilities like mount options compared to bind mounting

Sometimes programs or users cannot access one specific directory due to insufficient permissions. One feasable possibility to give the program access to this directory is bind mounting it to a location the program can access. If a program has permission to access directory bar but not to directory foo, under some circumstances the access can be granted without any permission hassle by adding an entry to `/etc/fstab`:

 `/etc/fstab`  `/<path to foo>         /<path to bar>     none     bind     0 0` 

## See also

*   [Full device listing including block device](http://www.kernel.org/pub/linux/docs/lanana/device-list/devices-2.6.txt)
*   [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/2.2/index.html)
*   [30x Faster Web-Site Speed](http://www.askapache.com/web-hosting/super-speed-secrets.html) (Detailed tmpfs)
*   [Adding Samba shares to /etc/fstab](/index.php/Samba#Add_Share_to_.2Fetc.2Ffstab "Samba")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Fstab&oldid=413878](https://wiki.archlinux.org/index.php?title=Fstab&oldid=413878)"