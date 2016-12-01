[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory. It is supported from kernel 3.8 onwards.

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

## Install Arch Linux on F2FS partition

**Warning:** If using F2FS as your root partition, you will need to add the following module to the `MODULES` line in your `/etc/mkinitcpio.conf` file ([FS#49380](https://bugs.archlinux.org/task/49380)): `MODULES="... **crypto-crc32**"` 

With the latest [installation media](https://www.archlinux.org/download/) it is possible to install Arch linux with root located on a F2FS filesystem:

1.  Create the root partition as F2FS as described in section [#Creating a F2FS partition](#Creating_a_F2FS_partition).
2.  If your [bootloader](/index.php/Bootloader "Bootloader") does not support F2FS, create a separate `/boot` partition using a filesystem that it does.
3.  Continue with the installation procedure as per [Installation guide#Mount the partitions](/index.php/Installation_guide#Mount_the_partitions "Installation guide") until [chrooted](/index.php/Change_root "Change root").
4.  Install [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) on the newly installed system as well.
5.  Regenerate the [initramfs](/index.php/Initramfs "Initramfs") while chrooted.