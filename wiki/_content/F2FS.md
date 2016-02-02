# F2FS

[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) is a file system intended for NAND-based flash memory. It is supported from kernel 3.8 onwards.

## Creating a F2FS partition

In order to create a F2FS partition, [install](/index.php/Install "Install") [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) from the [official repositories](/index.php/Official_repositories "Official repositories").

Create the partition:

```
# mkfs.f2fs -l mylabel _/dev/sdxY_

```

where `_/dev/sdxY_` is the target volume to format in F2FS.

## Mounting a F2FS partition

Users will likely need to manually load the F2FS kernel module before mounting. Issue as root:

```
# modprobe f2fs

```

The partition can then be mounted:

```
# mount -t f2fs /dev/sdxY /mnt

```

## Install Arch Linux on F2FS partition

With the latest [installation media](https://www.archlinux.org/download/) it is possible to install Arch linux with root located on a F2FS filesystem:

1.  Create the root partition as F2FS as described in section [#Creating a F2FS partition](#Creating_a_F2FS_partition).
2.  Create a separate `/boot` partition as ext2, or any other filesystem supported by the bootloader.
3.  Continue with the installation procedure as per [Beginners' guide#Mount the partitions](/index.php/Beginners%27_guide#Mount_the_partitions "Beginners' guide") until [chrooted](/index.php/Change_root "Change root").
4.  Install [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) on the newly installed system as well.
5.  Regenerate the initramfs while chrooted.

It is no longer necessary to modify `/etc/mkinitpcio.conf`, as the `filesystems` hook adds the f2fs module to the initramfs image.

Retrieved from "[https://wiki.archlinux.org/index.php?title=F2FS&oldid=412074](https://wiki.archlinux.org/index.php?title=F2FS&oldid=412074)"