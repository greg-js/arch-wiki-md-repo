[Partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "w:Disk partitioning") a hard drive divides the available space into sections that can be accessed independently. An entire drive may be allocated to a single partition, or multiple ones for cases such as dual-booting, maintaining a [swap](/index.php/Swap "Swap") partition, or to logically separate data such as audio and video files.

The required information is stored in a [#Partition table](#Partition_table) scheme such as MBR or GPT.

Tables are modified using a [#Partitioning tool](#Partitioning_tool) which must be compatible to the chosen scheme of partitioning table. Available tools include [fdisk](/index.php/Fdisk "Fdisk") and [parted](/index.php/Parted "Parted").

Once created, a partition must be formatted with an appropriate [file system](/index.php/File_system "File system") (*swap* excepted) before data can be written to the newly-formatted file system volume.

## Contents

*   [1 Partition table](#Partition_table)
    *   [1.1 Choosing between GPT and MBR](#Choosing_between_GPT_and_MBR)
    *   [1.2 Master Boot Record](#Master_Boot_Record)
        *   [1.2.1 Master Boot Record (partition table)](#Master_Boot_Record_.28partition_table.29)
        *   [1.2.2 Master Boot Record (bootstrap code)](#Master_Boot_Record_.28bootstrap_code.29)
    *   [1.3 GUID Partition Table](#GUID_Partition_Table)
        *   [1.3.1 Advantages of GPT](#Advantages_of_GPT)
        *   [1.3.2 Kernel Support](#Kernel_Support)
    *   [1.4 Partitionless disk](#Partitionless_disk)
        *   [1.4.1 Btrfs partitioning](#Btrfs_partitioning)
    *   [1.5 Backup and restoration](#Backup_and_restoration)
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

**Note:** To print/list existing tables (of a specific device), run `parted */dev/sda* print` or `fdisk -l */dev/sda*`, where `*/dev/sda*` is a device name.

### Choosing between GPT and MBR

GUID Partition Table (GPT) is an alternative, contemporary, partitioning style; it is intended to replace the old Master Boot Record (MBR) system. GPT has several advantages over MBR which has quirks dating back to MS-DOS times. With the recent developments to the formatting tools *fdisk* (MBR) and *gdisk* (GPT), it is equally easy to get good dependability and performance for GPT or MBR.

Some points to consider when choosing:

*   To dual-boot with Windows (both 32-bit and 64-bit) using Legacy BIOS, the MBR scheme is required.
*   To dual-boot Windows 64-bit using [UEFI](/index.php/UEFI "UEFI") mode instead of BIOS, the GPT scheme is required.
*   If you are installing on older hardware, especially on old laptops, consider choosing MBR because its BIOS might not support GPT.
*   If you are partitioning a disk of 2 TiB or larger, you need to use GPT.
*   It is recommended to always use GPT for [UEFI](/index.php/UEFI "UEFI") boot, as some UEFI implementations do not support booting to the MBR while in UEFI mode.
*   If none of the above apply, choose freely between GPT and MBR. Since GPT is more modern, it is recommended in this case.

**Note:** For GRUB to boot from a GPT-partitioned disk on a BIOS-based system, a [BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") is required. Please note that this partition is unrelated to the `/boot` mountpoint, and will be used by GRUB directly. Do not create a filesystem on it, and do not mount it.

### Master Boot Record

The [Master Boot Record](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record") (MBR) is the first 512 bytes of a storage device. It contains an operating system bootloader and the storage device's partition table. It plays an important role in the [boot process](/index.php/Boot_process "Boot process") under [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") systems. See [Wikipedia:Master boot record#Disk partitioning](https://en.wikipedia.org/wiki/Master_boot_record#Disk_partitioning "wikipedia:Master boot record") for the MBR structure.

**Note:** The MBR is not located in a partition; it is located at the first sector of the device (physical offset 0), preceding the first partition. (The boot sector present on a partitionless device or within an individual partition is called a [Volume boot record](https://en.wikipedia.org/wiki/Volume_boot_record "w:Volume boot record") instead.)

#### Master Boot Record (partition table)

There are 3 types of partitions in the MBR scheme:

*   Primary
*   Extended
    *   Logical

**Primary** partitions can be bootable and are limited to four partitions per disk or RAID volume. If the MBR partition table requires more than four partitions, then one of the primary partitions needs to be replaced by an **extended** partition containing **logical** partitions within it.

Extended partitions can be thought of as containers for logical partitions. A hard disk can contain no more than one extended partition. The extended partition is also counted as a primary partition so if the disk has an extended partition, only three additional primary partitions are possible (i.e. three primary partitions and one extended partition). The number of logical partitions residing in an extended partition is unlimited. A system that dual boots with Windows will require for Windows to reside in a primary partition.

The customary numbering scheme is to create primary partitions *sda1* through *sda3* followed by an extended partition *sda4*. The logical partitions on *sda4* are numbered *sda5*, *sda6*, etc.

#### Master Boot Record (bootstrap code)

The first 446 bytes of MBR are **bootstrap code area**. On BIOS systems it usually contains the first stage of the boot loader.

### GUID Partition Table

[GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") (GPT) is a partitioning scheme that is part of the [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") specification; it uses [globally unique identifiers](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") (GUIDs), or UUIDs in linux world, to define partitions and [partition types](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table"). It is designed to succeed the [#Master Boot Record](#Master_Boot_Record) partitioning scheme method.

#### Advantages of GPT

*   Provides a unique disk GUID and unique [partition GUID](/index.php/Persistent_block_device_naming#by-partuuid "Persistent block device naming") (`PARTUUID`) for each partition - A good filesystem-independent way of referencing partitions and disks.
*   Provides a filesystem-independent [partition name](/index.php/Persistent_block_device_naming#by-partlabel "Persistent block device naming") (`PARTLABEL`).
*   Arbitrary number of partitions - depends on space allocated for the partition table - No need for extended and logical partitions. By default the GPT table contains space for defining 128 partitions. However if you want to define more partitions, you can allocate more space to the partition table (currently only *gdisk* is known to support this feature).
*   Uses 64-bit LBA for storing Sector numbers - maximum addressable disk size is 2 ZiB. MBR is limited to addressing 2 TiB of space per drive.
*   Stores a backup header and partition table at the end of the disk that aids in [recovery](/index.php/Fdisk#Recover_GPT_header "Fdisk") in case the primary ones are damaged.
*   CRC32 checksums to detect errors and corruption of the header and partition table.

#### Kernel Support

The `CONFIG_EFI_PARTITION` option in the kernel config enables GPT support in the kernel (despite the name, EFI PARTITION). This option must be built in the kernel and not compiled as a loadable module. This option is required even if GPT disks are used only for data storage and not for booting. This option is enabled by default in Arch's [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernels in the [core] repo. In case of a custom kernel, enable this option by doing `CONFIG_EFI_PARTITION=y`.

### Partitionless disk

Partitionless disk (a.k.a. superfloppy) refers to using a storage device without using a partition table, having one file system volume occupying the whole storage device.

#### Btrfs partitioning

Btrfs can occupy an entire data storage device and replace the [MBR](#Master_Boot_Record) or [GPT](#GUID_Partition_Table) partitioning schemes. See the [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") instructions for details.

See also [Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs").

### Backup and restoration

See [fdisk#Backup and restore](/index.php/Fdisk#Backup_and_restore "Fdisk") and [File recovery#Testdisk and PhotoRec](/index.php/File_recovery#Testdisk_and_PhotoRec "File recovery").

## Partition scheme

There are no strict rules for partitioning a hard drive, although one may follow the general guidance given below. A disk partitioning scheme is determined by various issues such as desired flexibility, speed, security, as well as the limitations imposed by available disk space. It is essentially personal preference. If you would like to dual boot Arch Linux and a Windows operating system please see [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

### Single root partition

This scheme is the simplest and should be enough for most use cases. A [swapfile](/index.php/Swapfile "Swapfile") can be created and easily resized as needed. It usually makes sense to start by considering a single `/` partition and then separate out others based on specific use cases like RAID, encryption, a shared media partition, etc.

**Note:**

*   [UEFI](/index.php/UEFI "UEFI") systems require an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").
*   Installing [GRUB](/index.php/GRUB "GRUB") on a BIOS system partitioned with [GPT](#GUID_Partition_Table) requires an additional [BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB").

### Discrete partitions

Separating out a path as a partition allows for the choice of a different filesystem and mount options. In some cases like a media partition, they can also be shared between operating systems.

### Mount points

The following mount points are possible choices for separate partitions, you can make your decision based on actual needs.

#### Root partition

The root directory is the top of the hierarchy, the point where the primary filesystem is mounted and from which all other filesystems stem. All files and directories appear under the root directory `/`, even if they are stored on different physical devices. The contents of the root filesystem must be adequate to boot, restore, recover, and/or repair the system. Therefore, certain directories under `/` are not candidates for separate partitions.

The `/` partition or root partition is necessary and it is the most important. The other partitions can be replaced by it.

**Warning:** Directories essential for booting (except for `/boot`) **must** be on the same partition as `/` or mounted in early userspace by the [initramfs](/index.php/Initramfs "Initramfs"). These essential directories are: `/etc` and `/usr` [[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

#### /boot

The `/boot` directory contains the kernel and ramdisk images as well as the bootloader configuration file and bootloader stages. It also stores data that is used before the kernel begins executing user-space programs. `/boot` is not required for normal system operation, but only during boot and kernel upgrades (when regenerating the initial ramdisk).

A separate `/boot` partition is needed if installing a software RAID0 (stripe) system.

**Note:** It is recommended to mount [ESP](/index.php/ESP "ESP") to `/boot` if booting using UEFI boot loaders that do not contain drivers for other filesystems. Such loaders are for example [EFISTUB](/index.php/EFISTUB "EFISTUB") and [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

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

A [swap](/index.php/Swap "Swap") partition provides memory that can be used as virtual RAM. A [swap file](/index.php/Swap_file "Swap file") should be considered too, as they don't have any performance overhead compared to a partition but are much easier to resize as needed. A swap partition can *potentially* be shared between operating systems, but not if hibernation is used.

#### How big should my partitions be?

**Note:**

*   The below are simply recommendations; there is no hard rule dictating partition size.
*   If available, an extra 25% of space added to each filesystem will provide a cushion for future expansion and help protect against fragmentation.

The size of the partitions depends on personal preference, but the following information may be helpful:

	/boot - 200 MB 

	It requires only about 100 MB, but if multiple kernels/boot images are likely to be in use, 200 or 300 MB is a better choice.

	/ - 15–20 GB 

	It traditionally contains the `/usr` directory, which can grow significantly depending upon how much software is installed. 15–20 GB should be sufficient for most users with modern hard disks. If you plan to store a swap file here, you might need a larger partition size.

	/var - 8–12 GB 

	It will contain, among other data, the [ABS](/index.php/ABS "ABS") tree and the [pacman](/index.php/Pacman "Pacman") cache. Retaining these packages is helpful in case a package upgrade causes instability, requiring a [downgrade](/index.php/Downgrade "Downgrade") to an older, archived package. The pacman cache in particular will grow as the system is expanded and updated, but it can be safely cleared if space becomes an issue. 8–12 GB on a desktop system should be sufficient for `/var`, depending on how much software will be installed.

	/home - [varies] 

	It is typically where user data, downloads, and multimedia reside. On a desktop system, `/home` is typically the largest filesystem on the drive by a large margin.

	swap - [varies] 

	Historically, the general rule for swap partition size was to allocate twice the amount of physical RAM. As computers have gained ever larger memory capacities, this rule is outdated. For example, on average desktop machines with up to 512MB RAM, the 2x rule is usually adequate; if a sufficient amount of RAM (more than 1024MB) is available, it may be possible to have a smaller swap partition. See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate") to hibernate into a swap partition or file.

	/data - [varies] 

	One can consider mounting a "data" partition to cover various files to be shared by all users. Using the `/home` partition for this purpose is fine as well.

## Partitioning tools

**Warning:** To partition devices, use a partitioning tool compatible to the chosen type of partition table. Incompatible tools may result in the destruction of that table, along with existing partitions or data.

*   **[fdisk](/index.php/Fdisk "Fdisk")** — Terminal partitioning tools included in Linux.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[cfdisk](/index.php/Cfdisk "Cfdisk")** — Terminal partitioning tool written with ncurses libraries.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[sfdisk](/index.php/Sfdisk "Sfdisk")** — Scriptable version of fdisk.

	|| [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[gdisk](/index.php/Gdisk "Gdisk")** — [GPT](#GUID_Partition_Table) version of fdisk.

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

This table will help you to choose utility for your needs:

| User interaction | MBR | GPT |
| Dialog | fdisk
parted | fdisk
gdisk
parted |
| Pseudo-graphics | cfdisk | cfdisk
cgdisk |
| Non-interactive | sfdisk
parted | sfdisk
sgdisk
parted |
| Graphical | GParted
partitionmanager | GParted
partitionmanager |

## Partition alignment

Proper partition alignment is essential for optimal performance and longevity. This is due to the [block](https://en.wikipedia.org/wiki/Block_(data_storage) nature of every I/O operation on the hardware level as well as file system level. The key to alignment is partitioning to (at least) the given *block size*, which depends on the used hardware. If the partitions are not aligned to begin at multiples of the *block size*, aligning the file system is a pointless exercise because everything is skewed by the start offset of the partition.

### Hard disk drives

Historically, hard drives were addressed by indicating the *cylinder*, the *head*, and the *sector* at which data was to be read or written (also known as [CHS addressing](https://en.wikipedia.org/wiki/Cylinder-head-sector "wikipedia:Cylinder-head-sector")). These represented the radial position (cylinder), the axial position (drive head: platter and side), and the azimuth (sector) of the data respectively. Nowadays, with [logical block addressing](https://en.wikipedia.org/wiki/Logical_block_addressing "wikipedia:Logical block addressing"), the entire hard drive is addressed as one continuous stream of data and the term [sector](https://en.wikipedia.org/wiki/Disk_sector "wikipedia:Disk sector") designates the smallest addressable unit.

The standard *sector size* is 512B, but modern high-capacity hard drives use greater value, commonly 4KiB. Using values greater than 512B is referred to as the [Advanced Format](/index.php/Advanced_Format "Advanced Format").

### Solid state drives

Solid state drives are based on [flash memory](https://en.wikipedia.org/wiki/Flash_memory "wikipedia:Flash memory"), and thus differ significantly from hard drives. While reading remains possible in a random access fashion, erasure (hence rewriting and random writing) is possible only by [whole blocks](https://en.wikipedia.org/wiki/Flash_memory#Block_erasure "wikipedia:Flash memory"). Additionally, the *erase block size* (EBS) are significantly greater than regular *block size*, for example 128KiB vs. 4KiB, so it is necessary to align to multiples of EBS. Some [NVMe](/index.php/NVMe "NVMe") drives should be aligned to 4KiB, but not all. To find the sector size of your SSD, see [Advanced Format#How to determine if HDD employ a 4k sector](/index.php/Advanced_Format#How_to_determine_if_HDD_employ_a_4k_sector "Advanced Format").

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
*   [Wikipedia:Binary prefix](https://en.wikipedia.org/wiki/Binary_prefix "wikipedia:Binary prefix")
*   [Understanding Disk Drive Terminology](http://thestarman.pcministry.com/asm/mbr/DiskTerms.htm)
*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)
*   Rod Smith's page on [What's a GPT?](http://www.rodsbooks.com/gdisk/whatsgpt.html) and [Booting OSes from GPT](http://rodsbooks.com/gdisk/booting.html)
*   [Make the most of large drives with GPT and Linux - IBM Developer Works](http://www.ibm.com/developerworks/linux/library/l-gpt/index.html?ca=dgr-lnxw07GPT-Storagedth-lx&S_TACT=105AGY83&S_CMP=grlnxw07)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Partition Alignment](http://www.thomas-krenn.com/en/wiki/Partition_Alignment) (with examples)