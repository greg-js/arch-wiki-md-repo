*Partitioning* a hard drive allows one to logically divide the available space into sections that can be accessed independently of one another.

An entire hard drive may be allocated to a single partition, or one may divide the available storage space across multiple partitions. A number of scenarios require creating multiple partitions: dual- or multi-booting, for example, or maintaining a [swap](/index.php/Swap "Swap") partition. In other cases, partitioning is used as a means of logically separating data, such as creating separate partitions for audio and video files. Common partitioning schemes are discussed in detail below.

Each partition should be formatted to a [file system type](/index.php/File_systems "File systems") before being used.

## Contents

*   [1 Partition table](#Partition_table)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
    *   [1.2 GUID Partition Table](#GUID_Partition_Table)
    *   [1.3 Btrfs Partitioning](#Btrfs_Partitioning)
    *   [1.4 Choosing between GPT and MBR](#Choosing_between_GPT_and_MBR)
*   [2 Partition scheme](#Partition_scheme)
    *   [2.1 Single root partition](#Single_root_partition)
    *   [2.2 Discrete partitions](#Discrete_partitions)
    *   [2.3 Mount points](#Mount_points)
        *   [2.3.1 Root partition](#Root_partition)
        *   [2.3.2 /boot](#.2Fboot)
        *   [2.3.3 /home](#.2Fhome)
        *   [2.3.4 /var](#.2Fvar)
        *   [2.3.5 /tmp](#.2Ftmp)
        *   [2.3.6 Swap](#Swap)
        *   [2.3.7 How big should my partitions be?](#How_big_should_my_partitions_be.3F)
*   [3 Partitioning tools](#Partitioning_tools)
*   [4 Partition alignment](#Partition_alignment)
    *   [4.1 Hard disk drives](#Hard_disk_drives)
    *   [4.2 Solid state drives](#Solid_state_drives)
    *   [4.3 Partitioning tools](#Partitioning_tools_2)
*   [5 See also](#See_also)

## Partition table

Partition information is stored in the partition table; today, there are 2 main formats in use: the classic [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"), and the modern [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). The latter is an improved version that does away with several limitations of MBR style.

### Master Boot Record

MBR originally only supported up to 4 partitions. Later on, extended and logical partitions were introduced to get around this limitation.

There are 3 types of partitions:

*   Primary
*   Extended
    *   Logical

**Primary** partitions can be bootable and are limited to four partitions per disk or RAID volume. If a partitioning scheme requires more than four partitions, an **extended** partition containing **logical** partitions is used. Extended partitions can be thought of as containers for logical partitions. A hard disk can contain no more than one extended partition. The extended partition is also counted as a primary partition so if the disk has an extended partition, only three additional primary partitions are possible (i.e. three primary partitions and one extended partition). The number of logical partitions residing in an extended partition is unlimited. A system that dual boots with Windows will require that Windows reside in a primary partition.

The customary numbering scheme is to create primary partitions *sda1* through *sda3* followed by an extended partition *sda4*. The logical partitions on *sda4* are numbered *sda5*, *sda6*, etc.

See also [Wikipedia:Master boot record](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record").

### GUID Partition Table

There is only one type of partition, **primary**. The amount of partitions per disk or RAID volume is unlimited.

See also [Wikipedia:GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table").

### Btrfs Partitioning

Btrfs can occupy an entire data storage device and replace the [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT") partitioning schemes. See the [Btrfs#Partitioning](/index.php/Btrfs#Partitioning "Btrfs") instructions for details.

See also [Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs").

### Choosing between GPT and MBR

[GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) is an alternative, contemporary, partitioning style; it is intended to replace the old [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (MBR) system. GPT has several advantages over MBR which has quirks dating back to MS-DOS times. With the recent developments to the formatting tools *fdisk* (MBR) and *gdisk* (GPT), it is equally easy to get good dependability and performance for GPT or MBR.

One should consider these to choose between GPT and MBR:

*   If using GRUB legacy as the bootloader, one must use MBR.
*   To dual-boot with Windows (both 32-bit and 64-bit) using Legacy BIOS, one must use MBR.
*   To dual-boot Windows 64-bit using [UEFI](/index.php/UEFI "UEFI") instead of BIOS, one must use GPT.
*   If you are installing on the older hardware, especially laptop, consider choosing MBR because its BIOS might not support GPT.
*   If none of the above apply, choose freely between GPT and MBR; since GPT is more modern, it is recommended in this case.
*   It is recommended to use always GPT for [UEFI](/index.php/UEFI "UEFI") boot as some UEFI firmwares do not allow UEFI-MBR boot.

**Note:** For GRUB to boot from a GPT partitioned disk on a BIOS based system, one has to create a [BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Please note this partition is unrelated to the `/boot` mountpoint, and will be used by GRUB directly. Do not create a filesystem on it, and do not mount it.

## Partition scheme

There are no strict rules for partitioning a hard drive, although one may follow the general guidance given below. A disk partitioning scheme is determined by various issues such as desired flexibility, speed, security, as well as the limitations imposed by available disk space. It is essentially personal preference. If you would like to dual boot Arch Linux and a Windows operating system please see [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

### Single root partition

This scheme is the simplest and should be enough for most use cases. A [swapfile](/index.php/Swapfile "Swapfile") can be created and easily resized as needed. It usually makes sense to start by considering a single `/` partition and then separate out others based on specific use cases like RAID, encryption, a shared media partition, etc. Note that installing GRUB on a BIOS system partitioned with GPT requires an additional BIOS boot partition.

### Discrete partitions

Separating out a path as a partition allows for the choice of a different filesystem and mount options. In some cases like a media partition, they can also be shared between operating systems.

### Mount points

The following mount points are possible choices for separate partitions, you can make your decision based on actual needs.

#### Root partition

**Note:** Upon installation, the `/` (root) partition must be mounted **first**: this is because any directories such as `/boot` or `/home` that have separate partitions will have to be created in the root file system. The `/mnt` directory of the live system will be used to mount the root partition, and consequently all the other partitions will stem from there. Once the `/` partition has been mounted, any remaining partitions may be mounted in any order. The general procedure is to first create the mount point, and then mount the partition to it.

The root directory is the top of the hierarchy, the point where the primary filesystem is mounted and from which all other filesystems stem. All files and directories appear under the root directory `/`, even if they are stored on different physical devices. The contents of the root filesystem must be adequate to boot, restore, recover, and/or repair the system. Therefore, certain directories under `/` are not candidates for separate partitions.

The `/` partition or root partition is necessary and it is the most important. The other partitions can be replaced by it.

**Warning:** Directories essential for booting (except for `/boot`) **must** be on the same partition as `/` or mounted in early userspace by the [initramfs](/index.php/Initramfs "Initramfs"). These essential directories are: `/etc` and `/usr` [[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

#### /boot

The `/boot` directory contains the kernel and ramdisk images as well as the bootloader configuration file and bootloader stages. It also stores data that is used before the kernel begins executing user-space programs. `/boot` is not required for normal system operation, but only during boot and kernel upgrades (when regenerating the initial ramdisk).

A separate `/boot` partition is needed if installing a software RAID0 (stripe) system.

**Note:** It is recommended to mount [ESP](/index.php/UEFI#EFI_System_Partition "UEFI") to `/boot` if booting using UEFI boot loaders that do not contain drivers for other filesystems. Such loaders are for example [EFISTUB](/index.php/EFISTUB "EFISTUB") and [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

#### /home

The `/home` directory contains user-specific configuration files, caches, application data and media files.

Separating out `/home` allows `/` to be re-partitioned separately, but note that you can still reinstall Arch with `/home` untouched even if it is not separate - the other top-level directories just need to be removed, and then pacstrap can be run.

You should not share home directories between users on different distributions, because they use incompatible software versions and patches. Instead, consider sharing a media partition or at least using different home directories on the same `/home` partition.

#### /var

The `/var` directory stores variable data such as spool directories and files, administrative and logging data, [pacman](/index.php/Pacman "Pacman")'s cache, the [ABS](/index.php/ABS "ABS") tree, etc. It is used, for example, for caching and logging, and hence frequently read or written. Keeping it in a separate partition avoids running out of disk space due to flunky logs, etc.

It exists to make it possible to mount `/usr` as read-only. Everything that historically went into `/usr` that is written to during system operation (as opposed to installation and software maintenance) must reside under `/var`.

**Note:** `/var` contains many small files. The choice of file system type should consider this fact if a separate partition is used.

#### /tmp

This is already a separate partition by default, by virtue of being mounted as *tmpfs* by systemd.

#### Swap

A [swap](/index.php/Swap "Swap") partition provides memory that can be used as virtual RAM. A [swap file](/index.php/Swap#Swap_file "Swap") should be considered too, as they have almost no performance overhead compared to a partition but are much easier to resize as needed. A swap partition can *potentially* be shared between operating systems, but not if hibernation is used.

#### How big should my partitions be?

**Note:**

*   The below are simply recommendations; there is no hard rule dictating partition size.
*   If available, an extra 25% of space added to each filesystem will provide a cushion for future expansion and help protect against fragmentation.

The size of the partitions depends on personal preference, but the following information may be helpful:

	/boot - 200 MB 

	It requires only about 100 MB, but if multiple kernels/boot images are likely to be in use, 200 or 300 MB is a better choice.

	/ - 15-20 GB 

	It traditionally contains the `/usr` directory, which can grow significantly depending upon how much software is installed. 15-20 GB should be sufficient for most users with modern hard disks. If you plan to store a swap file here, you might need a larger partition size.

	/var - 8-12 GB 

	It will contain, among other data, the [ABS](/index.php/ABS "ABS") tree and the [pacman](/index.php/Pacman "Pacman") cache. Retaining these packages is helpful in case a package upgrade causes instability, requiring a [downgrade](/index.php/Downgrade "Downgrade") to an older, archived package. The pacman cache in particular will grow as the system is expanded and updated, but it can be safely cleared if space becomes an issue. 8-12 GB on a desktop system should be sufficient for `/var`, depending on how much software will be installed.

	/home - [varies] 

	It is typically where user data, downloads, and multimedia reside. On a desktop system, `/home` is typically the largest filesystem on the drive by a large margin.

	swap - [varies] 

	Historically, the general rule for swap partition size was to allocate twice the amount of physical RAM. As computers have gained ever larger memory capacities, this rule is outdated. For example, on average desktop machines with up to 512MB RAM, the 2x rule is usually adequate; if a sufficient amount of RAM (more than 1024MB) is available, it may be possible to have a smaller swap partition.

	/data - [varies] 

	One can consider mounting a "data" partition to cover various files to be shared by all users. Using the `/home` partition for this purpose is fine as well.

**Note:**

*   See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate") to hibernate into a swap partition or file.
*   A swap partition is highly recommended when using [virtual machine](/index.php/Virtual_machine "Virtual machine") guests.

## Partitioning tools

*   **[fdisk](/index.php/Fdisk "Fdisk")** — Terminal partitioning tools included in Linux.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[cfdisk](/index.php/Cfdisk "Cfdisk")** — Terminal partitioning tool written with ncurses libraries.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[gdisk](/index.php/Gdisk "Gdisk")** — [GPT](/index.php/GPT "GPT") version of fdisk.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[cgdisk](/index.php/Cgdisk "Cgdisk")** — GPT version of cfdisk.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[sgdisk](/index.php/Sgdisk "Sgdisk")** — Scriptable version of gdisk.

	[http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html](http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[GNU Parted](/index.php/GNU_Parted "GNU Parted")** — Terminal partitioning tool.

	[https://www.gnu.org/software/parted/parted.html](https://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **[GParted](/index.php/GParted "GParted")** — Graphical tool written in GTK.

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **Partitionmanager** — Graphical tool written in Qt.

	[http://sourceforge.net/projects/partitionman/](http://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

*   **QtParted** — Similar to Partitionmanager, available in [AUR](/index.php/AUR "AUR").

	[http://qtparted.sourceforge.net/](http://qtparted.sourceforge.net/) || [qtparted](https://aur.archlinux.org/packages/qtparted/)

## Partition alignment

Proper partition alignment is essential for optimal performance and longevity. This is due to the [block](https://en.wikipedia.org/wiki/Block_(data_storage) nature of every I/O operation on the hardware level as well as file system level. The key to alignment is partitioning to (at least) the given *block size*, which depends on the used hardware. If the partitions are not aligned to begin at multiples of the *block size*, aligning the file system is a pointless exercise because everything is skewed by the start offset of the partition.

### Hard disk drives

Historically, hard drives were addressed by indicating the *cylinder*, the *head*, and the *sector* at which data was to be read or written (also known as [CHS addressing](https://en.wikipedia.org/wiki/Cylinder-head-sector "wikipedia:Cylinder-head-sector")). These represented the radial position (cylinder), the axial position (drive head: platter and side), and the azimuth (sector) of the data respectively. Nowadays, with [logical block addressing](https://en.wikipedia.org/wiki/Logical_block_addressing "wikipedia:Logical block addressing"), the entire hard drive is addressed as one continuous stream of data and the term [sector](https://en.wikipedia.org/wiki/Disk_sector "wikipedia:Disk sector") designates the smallest addressable unit.

The standard *sector size* is 512B, but modern high-capacity hard drives use greater value, commonly 4KiB. Using values greater than 512B is referred to as the [Advanced Format](/index.php/Advanced_Format "Advanced Format").

### Solid state drives

Solid state drives are based on [flash memory](https://en.wikipedia.org/wiki/Flash_memory "wikipedia:Flash memory"), and thus differ significantly from hard drives. While reading remains possible in a random access fashion, erasure (hence rewriting and random writing) is possible only by [whole blocks](https://en.wikipedia.org/wiki/Flash_memory#Block_erasure "wikipedia:Flash memory"). Additionally, the *erase block size* (EBS) are significantly greater than regular *block size*, for example 128KiB vs. 4KiB, so it is necessary to align to multiples of EBS. [NVMe](/index.php/NVMe "NVMe") drives should be aligned to 4KiB.

### Partitioning tools

In the past, proper alignment required manual calculation and intervention when partitioning. Many of the common partition tools now handle partition alignment automatically:

*   *fdisk*
*   *gdisk*
*   *gparted*
*   *parted*

On an already partitioned disk, you can use [parted](/index.php/Parted "Parted") to verify the alignment of a partition on a device. For instance, to verify alignment of partition 1 on `/dev/sda`:

```
# parted /dev/sda
(parted) align-check optimal 1
1 aligned

```

**Warning:** Using `/usr/bin/blockdev` with option `--getalignoff` to check if a the partition is aligned has been reported to be [unreliable](https://bbs.archlinux.org/viewtopic.php?id=174141).

## See also

*   [Wikipedia:Disk partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "wikipedia:Disk partitioning")
*   [Manually Partitioning Your Hard Drive with fdisk](http://www.novell.com/coolsolutions/feature/19350.html)
*   [Partition Alignment](http://www.thomas-krenn.com/en/wiki/Partition_Alignment) (with examples)