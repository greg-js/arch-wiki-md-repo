Related articles

*   [File systems](/index.php/File_systems "File systems")

[Reiser4](https://en.wikipedia.org/wiki/Reiser4 "wikipedia:Reiser4") is the successor filesystem for [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS"), initially designed and developed entirely from scratch by [Namesys](https://en.wikipedia.org/wiki/Namesys "wikipedia:Namesys") and [Hans Reiser](https://en.wikipedia.org/wiki/Hans_Reiser "wikipedia:Hans Reiser"). It is very efficient in handling many files (often used in `/var` for this purpose) and includes a plugin-based design with plugins with features such as intelligent transparent compression, both inline data and meta-data checksums through the [crc32c](https://en.wikipedia.org/wiki/Cyclic_redundancy_check#CRC-32_algorithm "wikipedia:Cyclic redundancy check") algorithm with added optional [mirrors and failover](https://reiser4.wiki.kernel.org/index.php/Reiser4_Mirrors_and_Failover) support through its own implementation of subvolumes.

Reiser4 supports different [transaction models](https://reiser4.wiki.kernel.org/index.php/Reiser4_transaction_models) optimized for different types of storage devices. These include **Write-Anywhere** (or **CoW**), **journal** and a unique combination of the two called **hybrid**. Reiser4's main goals is performance as well as the modular nature which can expand features of the file system more easily, as well as the implementations that make it less prone to both data loss and corruption because of it's atomic approach in regards to every transaction that it performs. In the hybrid transaction model, Reiser4 heuristically alternates between journaling and Write-Anywhere/Copy-on-Write and is also the default if no mount option is specificed and this transaction model is optimized primarily for performance for rotating disks (while Write-Anywhere is aimed towards SSDs). However, in **hybrid** mode, it will result in more fragmentation compared to the **journal** transaction model over time.

However, Reiser4's journaling model (in both hybrid or journal modes) is more efficient than regular journaling file systems in that instead of traditional journaling, Reiser4 uses a more advanced technique known as [**wandering logs**](https://reiser4.wiki.kernel.org/index.php/V4#Wandering_Logs) which provides journaling without having to write data to the disk twice thus reducing writes. In many cases, Reiser4 can write journal data to a disk block, then atomically swap the journal block into the file itself which avoids having to write the data twice by changing one's definition of where the log area and the committed area are instead of moving the data from the log to the committed area.

Another unique feature is the implementation of a special technique for SSD users called [**Precise Asynchronous Discard**](https://reiser4.wiki.kernel.org/index.php/PreciseDiscard). This implementation means that in Reiser4, issuing discard requests is a delayed action, which is performed on a per-atom basis at transaction commit time. It allows to reduce number of discard requests issued (because the merging of extents, which needs to be discarded) and eliminates the need for issuing discards periodically as well, thus removing the need to set up an external tool like **fstrim** through a cron daemon which issues discard requests on a schedule.

Additionally, it also features block suballocation and is built on the [dancing tree](https://en.wikipedia.org/wiki/Dancing_tree "wikipedia:Dancing tree") design, which was exclusively invented for the use with Reiser4 and is also one of the several unique but also fundamental differences when compared to every other file system in general. The idea behind the **dancing tree** approach is to speed up file system operations by delaying optimization/balancing of the tree and only writing to disk when necessary, as writing to disk is much slower than writing to memory. Because this optimization is done less often than with other tree data structures like [B+ tree's](https://en.wikipedia.org/wiki/B%2B_tree "wikipedia:B+ tree") or [B- tree's](https://en.wikipedia.org/wiki/B-tree "wikipedia:B-tree"), the optimizations and performance gains can be more extensive.

Because it is designed as an atomic file system, "your file system operations either entirely occur, or they entirely don't, and they do not corrupt due to half occurring." What this means in practice is that all operations in Reiser4 are atomic. In the case of very long writes, Reiser4 is forced to close transactions to free dirty pages in a response to memory pressure and thus, long writes in Reiser4 are split into a number of atomic writes to maintain is atomicity. However, current lead developer, mathematician and programmer **PhD Edward Shishkin** has [suggested](https://reiser4.wiki.kernel.org/index.php/Why_Reiser4) a change to full atomicity (atomic writes of any length) in the **Write-Anywhere** transaction model, where atoms can be flushed without closing a transaction.

It's core design is very modular and allows for easy integration of new modules (called "plugins"). According to the developers, because of the modular design, Reiser4 can quite easily be ported to other operating systems like [FreeBSD](https://en.wikipedia.org/wiki/FreeBSD "wikipedia:FreeBSD"). As of 2019, Linux is still the only operating system Reiser4 is known to be compatible with.

Synthetic benchmarks and speed comparisons between **Reiser4**, [Btrfs](/index.php/Btrfs "Btrfs") and [Ext4](/index.php/Ext4 "Ext4") are [available](https://www.phoronix.com/scan.php?page=article&item=reiser4_benchmarks&num=1), as well as [benchmarks](https://openbenchmarking.org/result/1510278-BE-REISER4VS69) that include comparisons between the different **transaction models** and with/without the **cryptcompress** plugin.

More information about the features, plugins, design and mkfs or mount options is described in detail [here](https://reiser4.wiki.kernel.org/index.php/Main_Page).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Important Notes](#Important_Notes)
*   [2 Packages](#Packages)
*   [3 Moving to Reiser4](#Moving_to_Reiser4)
    *   [3.1 Sample system](#Sample_system)
    *   [3.2 Formatting](#Formatting)
    *   [3.3 Copy system](#Copy_system)
    *   [3.4 /etc/fstab:](#/etc/fstab:)
*   [4 Bootloader Examples](#Bootloader_Examples)
    *   [4.1 /boot/grub/grub.cfg:](#/boot/grub/grub.cfg:)
    *   [4.2 /etc/lilo.conf:](#/etc/lilo.conf:)
*   [5 Troubleshooting](#Troubleshooting)

## Important Notes

*   Reiser4 requires a patched kernel. A custom [Linux-ck](/index.php/Linux-ck "Linux-ck") based kernel with Reiser4 patches is available as [linux-ck-reiser4](https://aur.archlinux.org/packages/linux-ck-reiser4/)
*   It consumes a little more CPU than other filesystems (just like [Btrfs](/index.php/Btrfs "Btrfs")). To avoid having issues on laptops using [TLP](/index.php/TLP "TLP") for power saving, it is recommended to disable the options for **SATA Link** power saving in **/etc/default/tlp** (again, as with [Btrfs](/index.php/Btrfs "Btrfs")).
*   Even [LILO](/index.php/LILO "LILO") as the only bootloader officially supporting Reiser4 seems to have issues with it when `/boot` is formatted as Reiser4
*   It is still not included in the official Linux kernel, but patches for **Linux-5.x** is already available.
*   [Access Control Lists](/index.php/Access_Control_Lists "Access Control Lists") is not implemented and as of linux-5.x.x requires that [Systemd/Journal](/index.php/Systemd/Journal "Systemd/Journal") either logs to a seperate logging [daemon](/index.php/Daemon "Daemon") or to [Tmpfs](/index.php/Tmpfs "Tmpfs"). Another workaround is to compile systemD by source without ACL support, but is not recommended.

**Tip:** [Gparted LiveCD](http://gparted.sourceforge.net/livecd.php) is a small Linux distribution booting straight into Gparted. It also supports Reiser4 and can be used to migrate from an existing filesystem to Reiser4

## Packages

1\. [Install](/index.php/Install "Install") the [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/) package which provides utilities for creating, fsck'ing and debugging Reiser4 volumes.

2\. You will need a Reiser4 patched kernel. Patches can be found [here](https://sourceforge.net/projects/reiser4/files/) or at the more recently created Git [repository](https://github.com/edward6/reiser4) which is maintained by it's current lead developer, the mathematician and programmer **Edward Shishkin**.

3\. Bootloader *(Optional, only needed if you want to format your `/` (root, including **/boot**) as **Reiser4**)*

**Note:** Backing up your bootloader configuration file should be considered if one is going to have /boot residing on a Reiser4 volume.

a) **Recommended:** make a small (as mentioned above, 20-200mb) partition for `/boot` with a filesystem other than Reiser4 with [GParted](/index.php/GParted "GParted"), and then copy your `/boot` folder to the partition. Update your bootloader config accordingly, eg. with [Grub2](/index.php/Grub2 "Grub2") do:

```
# grub-mkconfig -o /boot/grub/grub.cfg. 

```

**Note:** [EFI](/index.php/EFI "EFI") systems in general require a [FAT32](/index.php/FAT32 "FAT32") partition for booting the kernel and thus it may be advantageous or unproblematic to have the /boot directory residing on that partition instead of only the EFI directory. Many EFI-users have their whole /boot directory on their [ESP](/index.php/ESP "ESP")

b) If you do not use [EFI](/index.php/EFI "EFI") and wish to put everything including `/boot` on a Reiser4 partition (not recommended) you will need to use [LILO](/index.php/LILO "LILO"). This is not advised, as you will probably get an error when trying to update `lilo.conf`:

```
# lilo

```

4\. Reboot

**Note:** The following steps are for using Reiser4 as your / (root, including /boot). If you just want to use Reiser4 as root with /boot mounted on the [ESP](/index.php/ESP "ESP") you should modify the following instructions according to your needs.

## Moving to Reiser4

In the next steps we will copy the data from your current root partition to the new Reiser4 partitions. Make sure you have enough disk space on the Reiser4 partition with:

```
# df -h

```

### Sample system

```
# fdisk -l
* /dev/sda1: (10 Gb, 5 Gb free); Reiserfs /mnt/reiser4
* /dev/sda2: (10 Gb, 10 Gb free); Reiser4 /
* /dev/sda3: (200 Mb, 180 Mb free); ext2 /boot

```

### Formatting

Since Reiser4 supports different transaction models optimized for different types of storage media (SSDs, HDDs), the options used while formatting and mounting will differ.

**Note:** For users with traditional HDDs, the defaults listed below will be enough.

Keep in mind that the defaults for mkfs.reiser4 includes enabled compression with the default algorithm being Zstd.

If one wishes to use either lzo or gzip instead of Zstd, it is needed to append `-o compress=lzo1` or `-o compress=gzip1` 

If one wishes to disable compression altogether, one must append:

 `-o create=reg40` to the `mkfs.reiser4` command. Additionally, the inline checksum plugin can be enabled with `-o node=node41` More information about the features, plugins and options is available [here.](https://reiser4.wiki.kernel.org/index.php/Reiser4_Howto)

**Note:** With **X** being your partition number!

```
mkfs.reiser4 /dev/sdaX
mkdir /mnt/reiser4
mount -t reiser4 -o txmod=journal,noatime,onerror=remount-ro /dev/sdaX /mnt/reiser4

```

It is recommended and also the default to use the **Cryptcompress** plugin by formatting with the following options:

mkfs.reiser4 -o create=ccreg40 /dev/sda**X**

Since Reiser4 also has options specifically for SSD users as well, it is recommended to discard the partition upon creation of the filesystem, the **-d** switch can be applied as shown below:

```
mkfs.reiser4 -d -o create=ccreg40,compress=Zstd1 /dev/nvme0n1X

```

For drives with controllers already having hardware compression (like SandForce ones), it may be better to to disable the compression plugin.

For HDDs:

 `mkfs.reiser4 -o create=reg40,node=node41 /dev/sdX` 

For SSDs:

 `mkfs.reiser4 -d -o create=reg40,node=node41 /dev/nvme0n1pX` 

### Copy system

Once the partition is formatted, copy you current system to the new partition and create the system directories. You may either do this from Arch Linux, or **to make it easier** (so that you do not have to use makedev later), just **boot up with the [Gparted LiveCD](http://gparted.sourceforge.net/livecd.php) and mount both your new Reiser4 partition and your current root partition. Then, just copy everything over (as root) like so:**

```
cd /mnt
mkdir oldroot
mkdir reiser4
mount /dev/sdaX oldroot

```

Depending on what transaction model one wish to use which are optimized for different types of storage media, the mount option **txmod=wa** (for SSDs), **txmod=journal** (for HDDs) must be defined when mounting the partitions through the **-o** switch. The default is **txmod=hybrid** which heuristically alternates between the "wa" (write-anywhere) and "journal" models for optimized performance on rotating disks while trying to avoid excess fragmentation at the same time.

```
mount -t reiser4 -o txmod=hybrid,noatime,onerror=remount-ro /dev/sdaY reiser4 (the Reiser4 partition)
cp -R -a /mnt/oldroot/* /mnt/reiser4/

```

Then, you need to mount your `/boot` partition, and if you have not already, copy `/boot` from your original root partition over to it.

**Note:** It is suggested to empty your /boot from the Reiser4 partition to use it as a mountpoint, which is reflected later in your fstab

```
mkdir bootpart
mount /dev/sdaZ bootpart
cp -R -a /mnt/oldroot/boot/* /mnt/bootpart/

```

Do not forget to edit your bootloader's config appropriately (see examples at the bottom of the article).

**Note:** In case you upgraded grub before rebooting you may need to manually install grub to your /boot partition, otherwise, things may break and prevent you from booting. In this case using a LiveCD to Chroot and would be your last hope.

### /etc/fstab:

Note: If you can confirm that Reiser4 works for you, you should format the old root partition.

```
#
# /etc/fstab: static file system information
#
# <file system>	<dir>	      <type>  <options>	         <dump>	<pass>

/dev/nvme0n1p1  /             reiser4 noatime,txmod=wa,onerror=remount-ro,discard 0   1
/dev/sda2       /mnt/oldroot  ext4    defaults                                    0   0
/dev/sda3       /boot         ext2    defaults                                    0   1
```

## Bootloader Examples

#### /boot/grub/grub.cfg:

```
# (0) Arch Linux
title  Arch Linux
set root=(hd0,msdos3)
kernel /vmlinuz-linux root=/dev/sda3 ro rootfstype=reiser4 rootflags=noatime,txmod=journal,onerror=remount-ro init=/usr/bin/bootchartd
initrd /initramfs-linux.img

# (1) Arch Linux
title  Arch Linux Fallback
set root=(hd0,msdos3)
kernel /vlinuz-linux root=/dev/sda3 ro rootfstype=reiser4 rootflags=noatime,txmod=journal,onerror=remount-ro
initrd /initramfs-linux-fallback.img
```

Run `grub-mkconfig` to update your config:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### /etc/lilo.conf:

```
#
# /etc/lilo.conf
#

boot=/dev/hda
# This line often fixes L40 errors on bootup
# disk=/dev/hda bios=0x80

default=Arch4
timeout=20
lba32
prompt
compact

image=/boot/vmlinuz-linux
        label=Arch4
        root=/dev/hda5
        append="video=vesafb:1024x768-24@56,ywrap,mtrr splash=verbose,theme:darch console=tty1 resume2=swap:/dev/hdb1"
initrd=/boot/initramfs-linux.img
read-only

image=/boot/vmlinuz-linux
        label=Arch
        root=/dev/hda3
        append="video=vesafb:1024x768-24@56,ywrap,mtrr splash=verbose,theme:darch console=tty1 resume2=swap:/dev/hdb1"
initrd=/boot/initramfs-linux.img
read-only

```

Run **lilo** to update your config:

```
# lilo

```

## Troubleshooting

*   Permissions: chown -R username.group <userdir>
*   If you have problem with **su** command after the change of fs, you should reinstall **coreutils** package.