Related articles

*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")
*   [File systems](/index.php/File_systems "File systems")
*   [tmpfs](/index.php/Tmpfs "Tmpfs")
*   [swap](/index.php/Swap "Swap")

The [fstab(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5) file can be used to define how disk partitions, various other block devices, or remote filesystems should be mounted into the filesystem.

Each filesystem is described in a separate line. These definitions will be converted into [systemd](/index.php/Systemd "Systemd") mount units dynamically at boot, and when the configuration of the system manager is reloaded. The default setup will automatically [fsck](/index.php/Fsck "Fsck") and mount filesystems before starting services that need them to be mounted. For example, systemd automatically makes sure that remote filesystem mounts like [NFS](/index.php/NFS "NFS") or [Samba](/index.php/Samba "Samba") are only started after the network has been set up. Therefore, local and remote filesystem mounts specified in `/etc/fstab` should work out of the box. See [systemd.mount(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5) for details.

The `mount` command will use fstab, if just one of either directory or device is given, to fill in the value for the other parameter. When doing so, mount options which are listed in fstab will also be used.

## Contents

*   [1 Usage](#Usage)
*   [2 Identifying filesystems](#Identifying_filesystems)
    *   [2.1 Kernel name descriptors](#Kernel_name_descriptors)
    *   [2.2 Labels](#Labels)
    *   [2.3 UUIDs](#UUIDs)
    *   [2.4 GPT labels](#GPT_labels)
    *   [2.5 GPT UUIDs](#GPT_UUIDs)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Automount with systemd](#Automount_with_systemd)
    *   [3.2 External devices](#External_devices)
    *   [3.3 Filepath spaces](#Filepath_spaces)
    *   [3.4 atime options](#atime_options)
    *   [3.5 Remounting the root partition](#Remounting_the_root_partition)
*   [4 See also](#See_also)

## Usage

A simple `/etc/fstab`, using kernel name descriptors:

 `/etc/fstab` 
```
# <device>             <dir>         <type>    <options>             <dump> <fsck>
/dev/sda1              /             ext4      defaults,noatime      0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      defaults,noatime      0      2
```

*   `<device>` describes the block special device or remote filesystem to be mounted; see [#Identifying filesystems](#Identifying_filesystems).
*   `<dir>` describes the [mount](/index.php/Mount "Mount") directory, `<type>` the [file system](/index.php/File_system "File system") type, and `<options>` the associated mount options; see [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8#FILESYSTEM-INDEPENDENT_MOUNT_OPTIONS).
*   `<dump>` is checked by the [dump(8)](http://linux.die.net/man/8/dump) utility. This field is usually set to `0`, which disables the check.
*   `<fsck>` sets the order for filesystem checks at boot time; see [fsck(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fsck.8). For the root device it should be `1`. For other partitions it should be `2`, or `0` to disable checking.

**Tip:** The `auto` type lets the mount command guess what type of file system is used. This is useful for optical media (CD/DVD).

**Note:** If the root file system is [btrfs](/index.php/Btrfs "Btrfs"), the fsck order should be set to `0` instead of `1`.

All specified devices within `/etc/fstab` will be automatically mounted on startup and when the `-a` flag is used with [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) unless the `noauto` option is specified. Devices that are listed and not present will result in an error unless the `nofail` option is used.

See [fstab(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5#DESCRIPTION) for details.

## Identifying filesystems

There are different ways to identify filesystems that will be mounted in `/etc/fstab`: kernel name descriptor, label or UUID, and GPT labels and UUID for GPT disks. UUID must be privileged over kernel name descriptors and labels. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for more explanations. It is recommended to read that article first before continuing with this article.

In this section, we will describe how to mount filesystems using all the mount methods available via examples. The output of the commands `lsblk -f` and `blkid` used in the following examples are available in the article [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

To use kernel name descriptors, use /dev/sd*xy* in the first column.

### Kernel name descriptors

Run `lsblk -f` to list the partitions and prefix the values in the *NAME* column with `/dev/`.

 `/etc/fstab` 
```
# <device>      <dir> <type> <options>                                                                                            <dump> <fsck>
/dev/sda1       /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
/dev/sda2       /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
/dev/sda3       /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
/dev/sda4       none  swap   defaults                                                                                             0      0

```

### Labels

Run `lsblk -f` to list the partitions, and prefix the values in the *LABEL* column with `LABEL=`:

 `/etc/fstab` 
```
# <device>      <dir> <type> <options>                                                                                            <dump> <fsck>
LABEL=EFI       /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
LABEL=SYSTEM    /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
LABEL=DATA      /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
LABEL=SWAP      none  swap   defaults                                                                                             0      0

```

**Note:** If any of your fields contains spaces, see [#Filepath spaces](#Filepath_spaces).

### UUIDs

Run `lsblk -f` to list the partitions, and prefix the values in the *UUID* column with `UUID=`:

 `/etc/fstab` 
```
# <device>                                <dir> <type> <options>                                                                                            <dump> <fsck>
UUID=CBB6-24F2                            /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
UUID=0a3407de-014b-458b-b5c1-848e92a327a3 /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
UUID=b411dc99-f0a0-4c87-9e05-184977be8539 /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
UUID=f9fe0b69-a280-415d-a03a-a32752370dee none  swap   defaults                                                                                             0      0

```

**Tip:** If you would like to return just the UUID of a specific partition: `lsblk -no UUID /dev/sda2`.

### GPT labels

Run `blkid` to list the partitions, and use the *PARTLABEL* values without the quotes:

 `/etc/fstab` 
```
# <device>                           <dir> <type> <options>                                                                                            <dump> <fsck>
PARTLABEL=EFI\040SYSTEM\040PARTITION /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
PARTLABEL=GNU/LINUX                  /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
PARTLABEL=HOME                       /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
PARTLABEL=SWAP                       none  swap   defaults                                                                                             0      0

```

**Note:** If any of your fields contains spaces, see [#Filepath spaces](#Filepath_spaces).

### GPT UUIDs

Run `blkid` to list the partitions, and use the *PARTUUID* values without the quotes:

 `/etc/fstab` 
```
# <device>                                    <dir> <type> <options>                                                                                            <dump> <fsck>
PARTUUID=d0d0d110-0a71-4ed6-936a-304969ea36af /boot vfat   rw,relatime,fmask=0022,dmask=0022,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro 0      2
PARTUUID=98a81274-10f7-40db-872a-03df048df366 /     ext4   rw,relatime,discard,data=ordered                                                                     0      1
PARTUUID=7280201c-fc5d-40f2-a9b2-466611d3d49e /home ext4   rw,relatime,discard,data=ordered                                                                     0      2
PARTUUID=039b6c1c-7553-4455-9537-1befbc9fbc5b none  swap   defaults                                                                                             0      0

```

## Tips and tricks

### Automount with systemd

If you have a large `/home` partition, it might be better to allow services that do not depend on `/home` to start while `/home` is checked by *fsck*. This can be achieved by adding the following options to the `/etc/fstab` entry of your `/home` partition:

```
noauto,x-systemd.automount

```

This will fsck and mount `/home` when it is first accessed, and the kernel will buffer all file access to `/home` until it is ready.

**Note:** This will make your `/home` filesystem type `autofs`, which is ignored by [mlocate](/index.php/Mlocate "Mlocate") by default. The speedup of automounting `/home` may not be more than a second or two, depending on your system, so this trick may not be worth it.

The same applies to remote filesystem mounts. If you want them to be mounted only upon access, you will need to use the `noauto,x-systemd.automount` parameters. In addition, you can use the `x-systemd.device-timeout=#` option to specify a timeout in case the network resource is not available.

**Note:** If you intend to use the `exec` flag with automount, you should remove the `user` flag for it to work properly as found in the course of a [Fedora Bug Report](https://bugzilla.redhat.com/show_bug.cgi?id=769636)

If you have encrypted filesystems with keyfiles, you can also add the `noauto` parameter to the corresponding entries in `/etc/crypttab`. *systemd* will then not open the encrypted device on boot, but instead wait until it is actually accessed and then automatically open it with the specified keyfile before mounting it. This might save a few seconds on boot if you are using an encrypted RAID device for example, because systemd does not have to wait for the device to become available. For example:

 `/etc/crypttab`  `data /dev/md0 /root/key noauto` 

You may also specify an idle timeout for a mount with the `x-systemd.idle-timeout` flag. For example:

```
noauto,x-systemd.automount,x-systemd.idle-timeout=1min

```

This will make systemd unmount the mount after it has been idle for 1 minute.

### External devices

External devices that are to be mounted when present but ignored if absent may require the `nofail` option. This prevents errors being reported at boot. For example:

 `/etc/fstab`  `/dev/sdg1        /media/backup    jfs    defaults,nofail,x-systemd.device-timeout=1    0  2` 

The `nofail` option is best combined with the `x-systemd.device-timeout` option. This is because the default device timeout is 90 seconds, so a disconnected external device with only `nofail` will make your boot take 90 seconds longer, unless you reconfigure the timeout as shown. Make sure not to set the timeout to 0, as this translates to infinite timeout.

If your external device requires another systemd unit to be loaded (for example the network for a network share) you can use `x-systemd.requires=x` combined with `x-systemd.automount`to postpone automounting until after the unit is available. For example:

 `/etc/fstab`  `//host/share        /net/share        cifs        noauto,nofail,x-systemd.automount,x-systemd.requires=network-online.target,x-systemd.device-timeout=10,workgroup=workgroup,credentials=/foo/credentials        0 0` 

### Filepath spaces

Since spaces are used in `fstab` to delimit fields, if any field (*PARTLABEL*, *LABEL* or the mount point) contains spaces, these spaces must be replaced by escape characters `\` followed by the 3 digit octal code `040`:

 `/etc/fstab` 
```
UUID=47FA-4071     /home/username/Camera<font color="grey">\040</font>Pictures   vfat  defaults,noatime       0  0
/dev/sda7          /media/100<font color="grey">\040</font>GB<font color="grey">\040</font>(Storage)       ext4  defaults,noatime,user  0  2
```

### atime options

Below atime options can impact drive performance.

*   The `strictatime` option updates the access time of the files every time they are accessed. This is more purposeful when Linux is used for servers; it does not have much value for desktop use. The drawback about the `strictatime` option is that even reading a file from the page cache (reading from memory instead of the drive) will still result in a write!

*   The `noatime` option fully disables writing file access times to the drive every time you read a file. This works well for almost all applications, except for those that need to know if a file has been read since the last time it was modified. The write time information to a file will continue to be updated anytime the file is written to with this option enabled.

*   The `nodiratime` option disables the writing of file access times only for directories while other files still get access times written.

**Note:** `noatime` implies `nodiratime`. [You do not need to specify both](http://lwn.net/Articles/244941/).

*   `relatime` updates the access time only if the previous access time was earlier than the current modify or change time. In addition, since Linux 2.6.30, the access time is always updated if the previous access time was more than 24 hours old. This option is used when the `defaults` option, `atime` option (which means to use the kernel default, which is `relatime`; see [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8) and [wikipedia:Stat (system call)#Criticism of atime](https://en.wikipedia.org/wiki/Stat_(system_call)#Criticism_of_atime "wikipedia:Stat (system call)")) or no options at all are specified.

When using [Mutt](/index.php/Mutt "Mutt") or other applications that need to know if a file has been read since the last time it was modified, the `noatime` option should not be used; using the `relatime` option is acceptable and still provides a performance improvement.

Since kernel 4.0 there is another related option:

*   `lazytime` reduces writes to disk by maintaining changes to inode timestamps (access, modification and creation times) only in memory. The on-disk timestamps are updated only when either (1) the file inode needs to be updated for some change unrelated to file timestamps, (2) a sync to disk occurs, (3) an undeleted inode is evicted from memory or (4) if more than 24 hours passed since the the last time the in-memory copy was written to disk.

**Warning:** In the event of a system crash, the access and modification times on disk might be out of date by up to 24 hours.

Note that the `lazytime` option works **in combination** with the aforementioned `*atime` options, not as an alternative. That is `relatime` by default, but can be even `strictatime` with the same or less cost of disk writes as the plain `relatime` option.

### Remounting the root partition

If for some reason the root partition has been improperly mounted read only, remount the root partition with read-write access with the following command:

```
# mount -o remount,rw /

```

## See also

*   [Full device listing including block device](http://www.kernel.org/pub/linux/docs/lanana/device-list/devices-2.6.txt)
*   [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/2.2/index.html)
*   [30x Faster Cache and Site Speed with TMPFS](http://www.askapache.com/optimize/super-speed-secrets/)
*   [Adding Samba shares to /etc/fstab](/index.php/Samba#As_mount_entry "Samba")