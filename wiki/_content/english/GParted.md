[GParted](http://gparted.sourceforge.net/index.php) is a GTK+ frontend to [GNU Parted](/index.php/GNU_Parted "GNU Parted") and the official GNOME Partition Editor application. Use it to make/delete/resize/check partitions of nearly [any file format](http://gparted.sourceforge.net/features.php). You can also manage drive labels and flags as well as copy/paste entire partitions. GParted is available in the extra repo and also as a [Live CD](http://gparted.sourceforge.net/download.php) if you'd prefer. One reason to actually download the Live CD would be that you need to make modifications to your root filesystem's partition which you cannot do without unmounting it.

**Warning:** Since GParted can read/write to your drive partitions misuse can result in data loss. It is recommended that you back-up affected partitions prior to using GParted.

## Contents

*   [1 Installation on Arch](#Installation_on_Arch)
*   [2 GParted support](#GParted_support)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Dual booting with Windows XP](#Dual_booting_with_Windows_XP)
    *   [3.2 Fixing messed-up partition order](#Fixing_messed-up_partition_order)

## Installation on Arch

[Install](/index.php/Install "Install") the [gparted](https://www.archlinux.org/packages/?name=gparted) package.

The base GParted package does not come with support for all filesystems. See [File_systems#Types_of_file_systems](/index.php/File_systems#Types_of_file_systems "File systems") for a list of additional packages you can install to add support for different filesystems.

To change the label of FAT volumes, install [mtools](https://www.archlinux.org/packages/?name=mtools).

## GParted support

Have a look at the [official GParted forums](http://gparted-forum.surf4.info/) prior to executing a command if you are unsure about what you're doing.

## Tips and tricks

### Dual booting with Windows XP

If you have a Windows XP partition that you would like to move from drive-to-drive that also happens to be your boot partition, you can do so easily with GParted and keep Windows happy simply by deleting the following registry key PRIOR to the partition move:

```
HKEY_LOCAL_MACHINE\SYSTEM\MountedDevices

```

Reference to this little gem [here](http://gparted-forum.surf4.info/viewtopic.php?pid=8347#p8347).

### Fixing messed-up partition order

See [Fdisk#Sort_partitions](/index.php/Fdisk#Sort_partitions "Fdisk").

**Note:** You must run **partprobe** as root or reboot the system in order for the kernel to read the new partition table!