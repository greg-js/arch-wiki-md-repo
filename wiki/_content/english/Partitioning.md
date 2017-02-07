[Partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "w:Disk partitioning") a hard drive divides the available space into sections that can be accessed independently. An entire drive may be allocated to a single partition, or multiple ones for cases such as dual-booting, maintaining a [swap](/index.php/Swap "Swap") partition, or to logically separate data such as audio and video files.

The required information is stored in a [#Partition table](#Partition_table) scheme such as MBR or GPT.

Partition tables are created and modified using one of many [#Partitioning tools](#Partitioning_tools) which must be compatible to the chosen scheme of partitioning table. Available tools include [fdisk](/index.php/Fdisk "Fdisk") and [parted](/index.php/Parted "Parted").

Once created, a partition must be formatted with an appropriate [file system](/index.php/File_system "File system") (*swap* excepted) before data can be written to it.

## Contents

*   [1 Partition table](#Partition_table)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
        *   [1.1.1 Master Boot Record (partition table)](#Master_Boot_Record_.28partition_table.29)
        *   [1.1.2 Master Boot Record (bootstrap code)](#Master_Boot_Record_.28bootstrap_code.29)
    *   [1.2 GUID Partition Table](#GUID_Partition_Table)
    *   [1.3 Choosing between GPT and MBR](#Choosing_between_GPT_and_MBR)
    *   [1.4 Partitionless disk](#Partitionless_disk)
        *   [1.4.1 Btrfs partitioning](#Btrfs_partitioning)
    *   [1.5 Backup](#Backup)
*   [2 Partition scheme](#Partition_scheme)
    *   [2.1 Single root partition](#Single_root_partition)
    *   [2.2 Discrete partitions](#Discrete_partitions)
        *   [2.2.1 /](#.2F)
        *   [2.2.2 /boot](#.2Fboot)
        *   [2.2.3 /home](#.2Fhome)
        *   [2.2.4 /var](#.2Fvar)
        *   [2.2.5 /data](#.2Fdata)
        *   [2.2.6 /tmp](#.2Ftmp)
        *   [2.2.7 Swap](#Swap)
    *   [2.3 Example layouts](#Example_layouts)
        *   [2.3.1 UEFI/GPT example layout](#UEFI.2FGPT_example_layout)
        *   [2.3.2 MBR/BIOS example layout](#MBR.2FBIOS_example_layout)
        *   [2.3.3 UEFI separate /home example layout](#UEFI_separate_.2Fhome_example_layout)
*   [3 Partitioning tools](#Partitioning_tools)
    *   [3.1 fdisk/gdisk](#fdisk.2Fgdisk)
    *   [3.2 GNU Parted](#GNU_Parted)
    *   [3.3 partitionmanager](#partitionmanager)
*   [4 Partition alignment](#Partition_alignment)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Converting MBR to GPT](#Converting_MBR_to_GPT)
    *   [5.2 GPT Kernel Support](#GPT_Kernel_Support)
*   [6 See also](#See_also)

## Partition table

**Note:** To print/list existing tables (of a specific device), run `parted */dev/sda* print` or `fdisk -l */dev/sda*`, where `*/dev/sda*` is a device name.

There are two main types of partition table available: Master Boot Record (MBR), and GUID Partition Table (GPT). These are described below along with a discussion on how to choose between the two. A third, less common alternative is using a partitionless disk, which is also discussed.

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

### Choosing between GPT and MBR

GUID Partition Table (GPT) is an alternative, contemporary, partitioning style; it is intended to replace the old Master Boot Record (MBR) system. GPT has several advantages over MBR which has quirks dating back to MS-DOS times. With the recent developments to the formatting tools *fdisk* (MBR) and *gdisk* (GPT), it is equally easy to get good dependability and performance for GPT or MBR.

Some points to consider when choosing:

*   To dual-boot with Windows (both 32-bit and 64-bit) using Legacy BIOS, the MBR scheme is required.
*   To dual-boot Windows 64-bit using [UEFI](/index.php/UEFI "UEFI") mode instead of BIOS, the GPT scheme is required.
*   If you are installing on older hardware, especially on old laptops, consider choosing MBR because its BIOS might not support GPT.
*   If you are partitioning a disk of 2 TiB or larger, you need to use GPT.
*   It is recommended to always use GPT for [UEFI](/index.php/UEFI "UEFI") boot, as some UEFI implementations do not support booting to the MBR while in UEFI mode.
*   If none of the above apply, choose freely between GPT and MBR. Since GPT is more modern, it is recommended in this case.

Some advantages of GPT over MBR are:

*   Provides a unique disk GUID and unique [partition GUID](/index.php/Persistent_block_device_naming#by-partuuid "Persistent block device naming") (`PARTUUID`) for each partition - A good filesystem-independent way of referencing partitions and disks.
*   Provides a filesystem-independent [partition name](/index.php/Persistent_block_device_naming#by-partlabel "Persistent block device naming") (`PARTLABEL`).
*   Arbitrary number of partitions - depends on space allocated for the partition table - No need for extended and logical partitions. By default the GPT table contains space for defining 128 partitions. However if you want to define more partitions, you can allocate more space to the partition table (currently only *gdisk* is known to support this feature).
*   Uses 64-bit LBA for storing Sector numbers - maximum addressable disk size is 2 ZiB. MBR is limited to addressing 2 TiB of space per drive.
*   Stores a backup header and partition table at the end of the disk that aids in [recovery](/index.php/Fdisk#Recover_GPT_header "Fdisk") in case the primary ones are damaged.
*   CRC32 checksums to detect errors and corruption of the header and partition table.

**Note:** For GRUB to boot from a GPT-partitioned disk on a BIOS-based system, a [BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") is required. Please note that this partition is unrelated to the `/boot` mountpoint, and will be used by GRUB directly. Do not create a filesystem on it, and do not mount it.

The section on [#Partitioning tools](#Partitioning_tools) contains a table indicating which tools are available for creating and modifying GPT and MBR tables.

### Partitionless disk

Partitionless disk (a.k.a. superfloppy) refers to using a storage device without using a partition table, having one file system occupying the whole storage device.

#### Btrfs partitioning

[Btrfs](/index.php/Btrfs "Btrfs") can occupy an entire data storage device and replace the [MBR](#Master_Boot_Record) or [GPT](#GUID_Partition_Table) partitioning schemes. See the [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") instructions for details.

### Backup

See [fdisk#Backup and restore partition table](/index.php/Fdisk#Backup_and_restore_partition_table "Fdisk").

## Partition scheme

There are no strict rules for partitioning a hard drive, although one may follow the general guidance given below. A disk partitioning scheme is determined by various issues such as desired flexibility, speed, security, as well as the limitations imposed by available disk space. It is essentially personal preference. If you would like to dual boot Arch Linux and a Windows operating system please see [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

**Note:**

*   [UEFI](/index.php/UEFI "UEFI") systems require an [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition").
*   BIOS systems that are partitioned with [GPT](#GUID_Partition_Table) require a [BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB") if [GRUB](/index.php/GRUB "GRUB") is used as the bootloader.
*   If using [Btrfs](/index.php/Btrfs "Btrfs"), subvolumes can be treated as partitions. See the [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs") section.

### Single root partition

This scheme is the simplest and should be enough for most use cases. A [swapfile](/index.php/Swapfile "Swapfile") can be created and easily resized as needed. It usually makes sense to start by considering a single `/` partition and then separate out others based on specific use cases like RAID, encryption, a shared media partition, etc.

### Discrete partitions

Separating out a path as a partition allows for the choice of a different filesystem and mount options. In some cases like a media partition, they can also be shared between operating systems.

Below are some example layouts that can be used when partitioning, and the following subsections detail a few of the directories which can be placed on their own separate partition and then [mounted](/index.php/Mount "Mount") at mount points under `/`. See [file-hierarchy(7)](http://man7.org/linux/man-pages/man7/file-hierarchy.7.html) for a full description of the contents of these directories.

#### /

The root directory is the top of the hierarchy, the point where the primary filesystem is mounted and from which all other filesystems stem. All files and directories appear under the root directory `/`, even if they are stored on different physical devices. The contents of the root filesystem must be adequate to boot, restore, recover, and/or repair the system. Therefore, certain directories under `/` are not candidates for separate partitions.

The `/` partition or root partition is necessary and it is the most important. The other partitions can be replaced by it.

**Warning:** Directories essential for booting (except for `/boot`) **must** be on the same partition as `/` or mounted in early userspace by the [initramfs](/index.php/Initramfs "Initramfs"). These essential directories are: `/etc` and `/usr` [[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

`/` traditionally contains the `/usr` directory, which can grow significantly depending upon how much software is installed. 15–20 GB should be sufficient for most users with modern hard disks. If you plan to store a swap file here, you might need a larger partition size.

#### /boot

The `/boot` directory contains the kernel and ramdisk images as well as the bootloader configuration file and bootloader stages. It also stores data that is used before the kernel begins executing user-space programs. `/boot` is not required for normal system operation, but only during boot and kernel upgrades (when regenerating the initial ramdisk).

A separate `/boot` partition is needed if installing a software RAID0 (stripe) system.

**Note:** It is recommended to mount [ESP](/index.php/ESP "ESP") to `/boot` if booting using UEFI boot loaders that do not contain drivers for other filesystems. Such loaders are for example [EFISTUB](/index.php/EFISTUB "EFISTUB") and [systemd-boot](/index.php/Systemd-boot "Systemd-boot").

A suggested size for `/boot` is 200 MiB unless using [UEFI](/index.php/UEFI "UEFI"), in which case greater than 512 MiB is needed.

#### /home

The `/home` directory contains user-specific configuration files, caches, application data and media files.

Separating out `/home` allows `/` to be re-partitioned separately, but note that you can still reinstall Arch with `/home` untouched even if it is not separate—the other top-level directories just need to be removed, and then pacstrap can be run.

You should not share home directories between users on different distributions, because they use incompatible software versions and patches. Instead, consider sharing a media partition or at least using different home directories on the same `/home` partition. The size of this partition varies.

#### /var

The `/var` directory stores variable data such as spool directories and files, administrative and logging data, [pacman](/index.php/Pacman "Pacman")'s cache, the [ABS](/index.php/ABS "ABS") tree, etc. It is used, for example, for caching and logging, and hence frequently read or written. Keeping it in a separate partition avoids running out of disk space due to flunky logs, etc.

It exists to make it possible to mount `/usr` as read-only. Everything that historically went into `/usr` that is written to during system operation (as opposed to installation and software maintenance) must reside under `/var`.

**Note:** `/var` contains many small files. The choice of file system type should consider this fact if a separate partition is used.

`/var` will contain, among other data, the [ABS](/index.php/ABS "ABS") tree and the [pacman](/index.php/Pacman "Pacman") cache. Retaining these packages is helpful in case a package upgrade causes instability, requiring a [downgrade](/index.php/Downgrade "Downgrade") to an older, archived package. The pacman cache in particular will grow as the system is expanded and updated, but it can be safely cleared if space becomes an issue. 8–12 GB on a desktop system should be sufficient for `/var`, depending on how much software will be installed.

#### /data

One can consider mounting a "data" partition to cover various files to be shared by all users. Using the `/home` partition for this purpose is fine as well. The size of this partition varies.

#### /tmp

This is already a separate partition by default, by virtue of being mounted as *tmpfs* by systemd; therefore, there is no need to create a partition for it.

#### Swap

A [swap](/index.php/Swap "Swap") partition provides memory that can be used as virtual RAM. A [swap file](/index.php/Swap_file "Swap file") should be considered too, as they don't have any performance overhead compared to a partition but are much easier to resize as needed. A swap partition can *potentially* be shared between operating systems, but not if hibernation is used.

Historically, the general rule for swap partition size was to allocate twice the amount of physical RAM. As computers have gained ever larger memory capacities, this rule is outdated. For example, on average desktop machines with up to 512MB RAM, the 2x rule is usually adequate; if a sufficient amount of RAM (more than 1024MB) is available, it may be possible to have a smaller swap partition. See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate") to hibernate into a swap partition or file.

### Example layouts

#### UEFI/GPT example layout

| Mount point | Partition | [Partition type (GUID)](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | Bootable flag | Suggested size |
| /boot | /dev/sd**x**1 | [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") | Yes | 260–512 MiB |
| [SWAP] | /dev/sd**x**2 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| / | /dev/sd**x**3 | Linux | No | Remainder of the device |

#### MBR/BIOS example layout

| Mount point | Partition | [Partition type](https://en.wikipedia.org/wiki/Partition_type "w:Partition type") | Bootable flag | Suggested size |
| [SWAP] | /dev/sd**x**1 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| / | /dev/sd**x**2 | Linux | Yes | Remainder of the device |

#### UEFI separate /home example layout

| Mount point | Partition | [Partition type (GUID)](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | Bootable flag | Suggested size |
| /boot | /dev/sd**x**1 | [EFI System Partition](/index.php/EFI_System_Partition "EFI System Partition") | Yes | More than 512 MiB |
| / | /dev/sd**x**2 | Linux | No | 15 - 20 GiB |
| [SWAP] | /dev/sd**x**3 | Linux [swap](/index.php/Swap "Swap") | No | More than 512 MiB |
| /home | /dev/sd**x**4 | Linux | No | Remainder of the device |

## Partitioning tools

The following programs are used to create and/or manipulate device partition tables and partitions. See the linked articles for the exact commands to be used.

This table will help you to choose utility for your needs:

 MBR | GPT |
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

**Warning:** To partition devices, use a partitioning tool compatible to the chosen type of partition table. Incompatible tools may result in the destruction of that table, along with existing partitions or data.

### fdisk/gdisk

These group of tools fall under *fdisk* or *gdisk* and are described in the [fdisk](/index.php/Fdisk "Fdisk") article.

*   **[fdisk](/index.php/Fdisk "Fdisk")** — Dialog-driven program for creation and manipulation of partition tables.

	[https://www.kernel.org/pub/linux/utils/util-linux/](https://www.kernel.org/pub/linux/utils/util-linux/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[cfdisk](/index.php/Cfdisk "Cfdisk")** — Curses-based variant of fdisk.

	[https://www.kernel.org/pub/linux/utils/util-linux/](https://www.kernel.org/pub/linux/utils/util-linux/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[sfdisk](/index.php/Sfdisk "Sfdisk")** — Scriptable variant of fdisk.

	[https://www.kernel.org/pub/linux/utils/util-linux/](https://www.kernel.org/pub/linux/utils/util-linux/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **[gdisk](/index.php/Gdisk "Gdisk")** — [GPT](#GUID_Partition_Table) alternative to fdisk.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[cgdisk](/index.php/Cgdisk "Cgdisk")** — Curses-based variant of gdisk.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **[sgdisk](/index.php/Sgdisk "Sgdisk")** — Scriptable variant of gdisk.

	[http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html](http://www.rodsbooks.com/gdisk/sgdisk-walkthrough.html) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

### GNU Parted

These group of tools are described in the [GNU Parted](/index.php/GNU_Parted "GNU Parted") article.

*   **[GNU Parted](/index.php/GNU_Parted "GNU Parted")** — Terminal partitioning tool.

	[https://www.gnu.org/software/parted/parted.html](https://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **[GParted](/index.php/GParted "GParted")** — Graphical tool written in GTK.

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

### partitionmanager

*   **Partitionmanager** — Graphical tool written in Qt.

	[http://sourceforge.net/projects/partitionman/](http://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

## Partition alignment

[fdisk/gdisk](/index.php/Fdisk "Fdisk") and [parted](/index.php/Parted#Alignment "Parted") handle alignment automatically. See [GNU Parted#Check alignment](/index.php/GNU_Parted#Check_alignment "GNU Parted") if you want to verify your alignment after partitioning.

For certain drives [Advanced Format](/index.php/Advanced_Format "Advanced Format") might be able to provide a better-performing alignment.

## Tips and tricks

#### Converting MBR to GPT

See [fdisk#Convert between MBR and GPT](/index.php/Fdisk#Convert_between_MBR_and_GPT "Fdisk").

#### GPT Kernel Support

The `CONFIG_EFI_PARTITION` option in the kernel config enables GPT support in the kernel (despite the name, EFI PARTITION). This option must be built in the kernel and not compiled as a loadable module. This option is required even if GPT disks are used only for data storage and not for booting. This option is enabled by default in Arch's [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernels in the [core] repo. In case of a custom kernel, enable this option by doing `CONFIG_EFI_PARTITION=y`.

## See also

*   [Wikipedia:Disk partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "wikipedia:Disk partitioning")
*   [Wikipedia:Binary prefix](https://en.wikipedia.org/wiki/Binary_prefix "wikipedia:Binary prefix")
*   [Understanding Disk Drive Terminology](http://thestarman.pcministry.com/asm/mbr/DiskTerms.htm)
*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)
*   Rod Smith's page on [What's a GPT?](http://www.rodsbooks.com/gdisk/whatsgpt.html) and [Booting OSes from GPT](http://rodsbooks.com/gdisk/booting.html)
*   [Make the most of large drives with GPT and Linux - IBM Developer Works](http://www.ibm.com/developerworks/linux/library/l-gpt/index.html?ca=dgr-lnxw07GPT-Storagedth-lx&S_TACT=105AGY83&S_CMP=grlnxw07)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   [Partition Alignment](http://www.thomas-krenn.com/en/wiki/Partition_Alignment) (with examples)