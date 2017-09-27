Related articles

*   [File systems](/index.php/File_systems "File systems")

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory equipped with Flash Transition Layer. Unlike JFFS or UBIFS it relies on FTL to handle write distribution. It is supported from kernel 3.8 onwards.

## Contents

*   [1 Creating a F2FS partition](#Creating_a_F2FS_partition)
*   [2 Mounting a F2FS partition](#Mounting_a_F2FS_partition)
*   [3 Grow an F2FS partition](#Grow_an_F2FS_partition)
*   [4 Install Arch Linux on F2FS partition](#Install_Arch_Linux_on_F2FS_partition)
*   [5 Checking and repair](#Checking_and_repair)

## Creating a F2FS partition

In order to create a F2FS partition, [install](/index.php/Install "Install") [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) from the [official repositories](/index.php/Official_repositories "Official repositories").

Create the partition:

```
# mkfs.f2fs -l mylabel */dev/sdxY*

```

where `*/dev/sdxY*` is the target volume to format in F2FS.

## Mounting a F2FS partition

The partition can then be mounted manually or via other mechanisms:

```
# mount /dev/sdxY /mnt/foo

```

## Grow an F2FS partition

When the filesystem is unmounted, it can be grown if the partition is expanded. [Shrinking is not currently supported](https://www.mail-archive.com/linux-f2fs-devel@lists.sourceforge.net/msg04247.html).

First use a [partition tool](/index.php/Partitioning#Partitioning_tools "Partitioning") to resize the partition. This can be done, for example, by deleting the old partition and creating a new one with with the same type, the same start sector, and a new end position.

Then expand the filesystem to fill the new partition using:

```
# resize.f2fs /dev/sdxY

```

where `*/dev/sdxY*` is the target F2FS volume to grow.

**Note:** If you're using GPT, the partition's GUID (seen in /dev/disk/by-partuuid/*) might change, but the filesystem UUID (seen in /dev/disk/by-uuid) should stay the same.

## Install Arch Linux on F2FS partition

**Warning:** If using GRUB your freshly installed system might not boot after reboot. As GRUB doesn't support F2FS it isn't able to extract the UUID (which is persistent across reboots) of your drive so it uses classic `/dev/sdXx` names instead (which are not guaranteed to be persistent across reboots). In this case you might have to manually edit `/boot/grub/grub.cfg` and replace `root=/dev/sdXx` with `root=UUID=xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`; you can use the `blkid` command to get the UUID of your device.

With the latest [installation media](https://www.archlinux.org/download/) it is possible to install Arch linux with root located on a F2FS filesystem:

1.  Create the root partition as F2FS as described in section [#Creating a F2FS partition](#Creating_a_F2FS_partition).
2.  If your [bootloader](/index.php/Bootloader "Bootloader") does not support F2FS, create a separate `/boot` partition using a filesystem that it does.
3.  Continue with the installation procedure in the Installation Guide as per [#Mount the file systems](/index.php/Installation_guide#Mount_the_file_systems "Installation guide") until [chrooted](/index.php/Change_root "Change root").
4.  Install [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) on the newly installed system as well.
5.  Regenerate the [initramfs](/index.php/Initramfs "Initramfs") while chrooted.

Be sure to also check out the [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") page if you're installing Arch on a USB flash drive. (In particular the part about editing `/etc/mkinitcpio.conf` is important, otherwise your system won't boot.)

## Checking and repair

Checking and repairs to f2fs partitions are accomplished with `fsck.f2fs` provided by [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools). See the manpage for available switches.