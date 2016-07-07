[GParted](http://gparted.sourceforge.net/index.php) is a GTK+ frontend to [GNU Parted](/index.php/GNU_Parted "GNU Parted") and the official GNOME Partition Editor application. Use it to make/delete/resize/check partitions of nearly [any file format](http://gparted.sourceforge.net/features.php). You can also manage drive labels and flags as well as copy/paste entire partitions. GParted is available in the extra repo and also as a [Live CD](http://gparted.sourceforge.net/download.php) if you'd prefer. One reason to actually download the Live CD would be that you need to make modifications to your root filesystem's partition which you cannot do without unmounting it.

**Warning:** Since GParted can read/write to your drive partitions misuse can result in data loss. It is recommended that you back-up affected partitions prior to using GParted.

## Contents

*   [1 Installation on Arch](#Installation_on_Arch)
    *   [1.1 Optional dependencies](#Optional_dependencies)
        *   [1.1.1 Filesystems](#Filesystems)
        *   [1.1.2 Additional functionality](#Additional_functionality)
*   [2 GParted support](#GParted_support)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Dual booting with Windows XP](#Dual_booting_with_Windows_XP)
    *   [3.2 Fixing messed-up partition order](#Fixing_messed-up_partition_order)
    *   [3.3 Starting GParted from a menu](#Starting_GParted_from_a_menu)
    *   [3.4 Enabling GParted online resize and dmraid](#Enabling_GParted_online_resize_and_dmraid)

## Installation on Arch

[Install](/index.php/Install "Install") the [gparted](https://www.archlinux.org/packages/?name=gparted) package.

### Optional dependencies

#### Filesystems

The base GParted package doesn't come with support for all filesystems. Here is a brief list of additional packages you can install to add support for different filesystems:

| **Package** | **Filesystem** |
| [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) | [Btrfs](/index.php/Btrfs "Btrfs") |
| [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) | fat16/32 |
| [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) | ext2/[ext3](/index.php/Ext3 "Ext3")/[ext4](/index.php/Ext4 "Ext4") (v1.41+) |
| [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils) | exfat |
| [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) | [F2FS](/index.php/F2FS "F2FS") |
| [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) | [JFS](/index.php/JFS "JFS") |
| [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | [NTFS](/index.php/NTFS "NTFS") |
| [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) | [Reiser4](/index.php/Reiser4 "Reiser4") |
| [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) | Reiser3 |
| [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) | [XFS](/index.php/XFS "XFS") |

#### Additional functionality

| **Package** | **Functionality** |
| [mtools](https://www.archlinux.org/packages/?name=mtools) | Utilities for MS-DOS disks. Needed if you want to change the label of FAT volumes. |

Note that when you install GParted via pacman, it will list these for you also.

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

Your partition order can get messed up if you have logical volumes and you erase one of them. Consider the following example:

```
/dev/sda1 (Primary partition)
/dev/sda2 (Primary partition)
/dev/sda3 (Primary partition)
/dev/sda4 (EXTENDED partition)
/dev/sda5 (Logical partition)
/dev/sda6 (Logical partition)
/dev/sda7 (Logical partition)

```

So 1-3 are primary partitions. 5-6 are logical partitions within the extended partition. Let's say you want to nuke `/dev/sda5` and copy/paste `/dev/sda2` into the resulting freespace. Now your drive looks like this:

```
/dev/sda1 (Primary partition)
/dev/sda2 (Primary partition)
/dev/sda3 (Primary partition)
/dev/sda4 (EXTENDED partition)
/dev/sda7 (Logical partition)
/dev/sda5 (Logical partition)
/dev/sda6 (Logical partition)

```

Notice that the order is messed up after your delete, copy/paste operation. This can cause all sorts of problems from not being able to mount an expected partition, to GRUB error 17/no bootable system. The solution to this little problem is simple:

1.  Boot with your Arch Live CD or GParted Live CD (or any other live Linux CD)
2.  Run fdisk on the drive, enter expert mode, fix the partition order, and write the changes to disk

Example using `/dev/sda`:

```
# fdisk /dev/sda

```

1.  Once you are in fdisk, choose option `x` (extra functionality (experts only)) and enter
2.  Then select `f` (fix partition order) and enter
3.  Then select option `w` (write table to disk and exit), and enter

**Note:** You must run **partprobe** as root or reboot the system in order for the kernel to read the new partition table!

### Starting GParted from a menu

If you are having issues loading GParted from a menu, for instance the xfce applications menu, you will have to install the [polkit](https://www.archlinux.org/packages/?name=polkit) package and autostart it with your session.

### Enabling GParted online resize and dmraid

You need rebuild package using following configuration:

```
./configure --enable-online-resize --enable-libparted-dmraid

```