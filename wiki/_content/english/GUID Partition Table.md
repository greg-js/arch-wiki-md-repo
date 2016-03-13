GUID Partition Table (GPT) is a partitioning scheme that is part of the [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") specification; it uses a [globally unique identifier](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") for qualifying devices. It is the next generation partitioning scheme designed to succeed the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") partitioning scheme method. It evolved to deal with several shortcomings of the MBR partitioning scheme method and offers additional advantages.

## Contents

*   [1 About the Master Boot Record](#About_the_Master_Boot_Record)
    *   [1.1 Problems with MBR](#Problems_with_MBR)
*   [2 About the GUID Partition Table](#About_the_GUID_Partition_Table)
    *   [2.1 Advantages of GPT](#Advantages_of_GPT)
    *   [2.2 Kernel Support](#Kernel_Support)
*   [3 Bootloader Support](#Bootloader_Support)
    *   [3.1 UEFI systems](#UEFI_systems)
    *   [3.2 BIOS systems](#BIOS_systems)
        *   [3.2.1 Workarounds](#Workarounds)
*   [4 Partitioning Utilities](#Partitioning_Utilities)
    *   [4.1 GPT fdisk](#GPT_fdisk)
    *   [4.2 GNU Parted](#GNU_Parted)
    *   [4.3 Util-linux fdisk](#Util-linux_fdisk)
*   [5 Partitioning examples](#Partitioning_examples)
    *   [5.1 gdisk basic](#gdisk_basic)
    *   [5.2 gdisk basic (with hybrid MBR)](#gdisk_basic_.28with_hybrid_MBR.29)
    *   [5.3 parted basic (via command line options)](#parted_basic_.28via_command_line_options.29)
    *   [5.4 sgdisk basic (auto discover)](#sgdisk_basic_.28auto_discover.29)
    *   [5.5 Convert from MBR to GPT](#Convert_from_MBR_to_GPT)
    *   [5.6 Resize a partition](#Resize_a_partition)
    *   [5.7 Sort the partitions](#Sort_the_partitions)
*   [6 See also](#See_also)

## About the Master Boot Record

To understand GPT it is important to understand what MBR is and what its disadvantages are. The MBR partition table stores the partitions info in the first sector of a hard disk as follows:

| Location in the HDD | Purpose of the Code |
| `001-440 bytes` | MBR boot code that is launched by the BIOS. |
| `441-446 bytes` | MBR disk signature. |
| `447-510 bytes` | Partition table (of primary and extended partitions, not logical). |
| `511-512 bytes` | MBR boot signature 0xAA55. |

The entire information about the primary partitions is limited to the 64 bytes allotted. To extend this, extended partitions were used. An extended partition is simply a primary partition in the MBR which acts like a container for other partitions called logical partitions. So one is limited to either 4 primary partitions, or 3 primary and 1 extended partitions with many logical partitions inside it.

### Problems with MBR

1.  Only 4 primary partitions or 3 primary + 1 extended partitions (with arbitrary number of logical partitions within the extended partition) can be defined. If you have 3 primary + 1 extended partitions, and you have some free space outside the extended partition area, you cannot create a new partition over that free space.
2.  Within the extended partition, the logical partitions' meta-data is stored in a linked-list structure. If one link is lost, all the logical partitions following that metadata are lost.
3.  MBR supports only 1 byte partition type codes which leads to many collisions.
4.  MBR stores partition sector information using 32-bit LBA values. This LBA length along with 512 byte sector size (more commonly used) limits the maximum addressable size of the disk to be 2 [TiB](https://en.wikipedia.org/wiki/TiB "wikipedia:TiB"). Any space beyond 2 TiB cannot be defined as a partition if MBR partitioning is used.

## About the GUID Partition Table

GUID Partition Table (GPT) uses GUIDs (or UUIDs in linux world) to define partitions and its types, hence the name. The GPT consists of:

| Location in the HDD | Purpose |
| First logical sector of the disk or First 512 bytes | Protective MBR - Same as a normal MBR but the 64-byte area contains a single 0xEE type Primary partition entry defined over the entire size of the disk or in case of >2 [TiB](https://en.wikipedia.org/wiki/TiB "wikipedia:TiB"), upto a partition size of 2 TiB. |
| Second logical sector of the disk or Next 512 bytes | Primary GPT Header - Contains the Unique Disk GUID, Location of the Primary Partition Table, Number of possible entries in partition table, CRC32 checksums of itself and the Primary Partition Table, Location of the Secondary (or Backup) GPT Header |
| 16 KiB (by default) following the second logical sector of the disk | Primary GPT Table - 128 Partition entries (by default, can be higher), each with an entry of size 128 bytes (hence total of 16 KiB for 128 partition entries). Sector numbers are stored as 64-bit LBA and each partition has a Partition Type GUID and a Unique Partition GUID. |
| 16 KiB (by default) before the last logical sector of the disk | Secondary GPT table - It is byte-for-byte identical to the Primary table. Used mainly for recovery in case the primary partition table is damaged. |
| Last logical sector of the disk or Last 512 bytes | Secondary GPT Header - Contains the Unique Disk GUID, Location of the Secondary Partition Table, Number of possible entries in the partition table, CRC32 checksums of itself and the Secondary Partition Table, Location of the Primary GPT Header. This header can be used to recover GPT info in case the primary header is corrupted. |

### Advantages of GPT

1.  Uses GUIDs (UUIDs) to identify partition types - No collisions.
2.  Provides a unique disk GUID and unique partition GUID for each partition - A good filesystem-independent way of referencing partitions and disks.
3.  Arbitrary number of partitions - depends on space allocated for the partition table - No need for extended and logical partitions. By default the GPT table contains space for defining 128 partitions. However if the user wants to define more partitions, he/she can allocate more space to the partition table (currently only gdisk is known to support this feature).
4.  Uses 64-bit LBA for storing Sector numbers - maximum addressable disk size is 2 [ZiB](https://en.wikipedia.org/wiki/ZiB "wikipedia:ZiB").
5.  Stores a backup header and partition table at the end of the disk that aids in recovery in case the primary ones are damaged.
6.  CRC32 checksums to detect errors and corruption of the header and partition table.

### Kernel Support

`CONFIG_EFI_PARTITION` option in the kernel config enables GPT support in the kernel (despite the name EFI PARTITION). This options must be built-in the kernel and not compiled as a loadable module. This option is required even if GPT disks are used only for data storage and not for booting. This option is enabled by default in Arch's [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernels in [core] repo. In case of a custom kernel enable this option by doing `CONFIG_EFI_PARTITION=y`.

## Bootloader Support

### UEFI systems

All UEFI Bootloaders support GPT disks since GPT is a part of UEFI Specification and thus mandatory for UEFI boot. See [Boot loaders](/index.php/Boot_loaders "Boot loaders") for more information.

### BIOS systems

While GPT support on BIOS systems is theoretically possible it sometimes isn't practical and other times there are complete incompatibilities. Technically the BIOS is only supposed to execute the code on the MBR, therefore leaving the possibility of differing partitioning schemes... However a BIOS may do additional checks including: checking a MBR's integrity, and possibly even for a MBR partition table (though usually only the first partition). If this is a case, a number of workarounds exist that may be able to repair the problem (listed below).

**Warning:** For Windows, there is **no** support for booting from a BIOS/GPT partitioning scheme. If you have already installed Windows with a BIOS/MBR partitioning scheme **do not** convert the drive to GPT! Windows will fail to boot if this is done - irrespective of the bootloader used to chainload Windows. One can either install Windows in UEFI mode and use an [UEFI bootloader](/index.php/UEFI_Bootloaders "UEFI Bootloaders") (which uses GPT), or possibly restore/install Windows on a BIOS/GPT hybrid MBR (see partitioning examples).

Bootloaders that support GPT/BIOS partitioning scheme bootloading:

*   [GRUB](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")
*   [Syslinux](/index.php/Syslinux#GUID_partition_table "Syslinux")
*   Not suported: [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") and [LILO](/index.php/LILO "LILO")

#### Workarounds

A few workarounds may help boot a BIOS/GPT partitioning scheme; however, before trying these, try booting a BIOS/GPT partitioning scheme with the bootloaders standard procedure. If it doesn't work, these may help boot them ([read this](http://www.rodsbooks.com/gdisk/bios.html#bios) for full reference):

*   Set the boot flag on the protective MBR partition (type 0xEE) . This can be done with `parted /dev/sdX` and `disk_toggle pmbr_boot` or using `sgdisk /dev/sdX --attributes=1:set:2`.
*   Be sure there is no EFI system partition
*   Create a hybrid MBR. This will be needed for a BIOS that looks for a valid MBR partition (see example below).
*   Recompute CHS (Cylinder/Head/Sector) values in the protective MBR. GPT does not use these values but the protective MBR may need to be calibrated to them to work for those BIOS that test them.
*   A second disk that has a valid MBR table may signify to the BIOS that it is alright to execute the code on the protective MBR.
*   Many computers since 2011 may have support for an EFI booting if wanting from a BIOS option.

## Partitioning Utilities

Several partitioning utilities exists.

### GPT fdisk

GPT fdisk is a set of text-mode utilities for editing GPT disks. It consists of gdisk, sgdisk and cgdisk which are equivalent to respective tools from util-linux fdisk (used for MBR disks). It is available in the [extra] repository as [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

### GNU Parted

[GNU Parted](/index.php/GNU_Parted "GNU Parted") is a full-featured command line program for creating and manipulating partition tables. It can be used interactively and is the backend for the popular [GParted](/index.php/GParted "GParted") GUI partitioning tool.

It supports GPT as well as MBR.

### Util-linux fdisk

The [fdisk](/index.php/Fdisk "Fdisk") utility from [util-linux](https://www.archlinux.org/packages/?name=util-linux) (based on util-linux internal libfdisk) partially supports GPT, but it is still in beta stage (as on 07 October 2013). The related utilities cfdisk and sfdisk do not yet support GPT, and may damage the GPT header and partition table if used on a GPT disk.

## Partitioning examples

Examples of various partitioning setups.

### gdisk basic

```
# gdisk /dev/sdX
o  # create new empty GUID partition table
n  # partition 1 [enter], from beginning [enter], to 100GiB [+100GiB], linux fs type [enter]
n  # partition 2 [enter], from beginning [enter], to 108GiB [+8GiB],   linux swap    [8200]
w  # write table to disk and exit

```

### gdisk basic (with hybrid MBR)

Tip: use MiB, GiB to align to 2048 sectors:

```
# gdisk /dev/sdX
o  # create new empty GUID partition table
n  # partition 1 [enter], from beginning [enter], to 100GiB [+100GiB], linux fs type [enter]
n  # partition 2 [enter], from beginning [enter], to 108GiB [+8GiB],   linux swap    [8200]
n  # partition 3 [enter], from beginning [enter],           [+1MiB],   linux fs type [enter]
r  # recovery/transformation menu
h  # make hybrid mbr
3  # add partition 3 to hybrid mbr
Place EFI GPT (0xEE) partition first in MBR (good for GRUB)? (Y/N): **N**
Enter an MBR hex code (default 83): [enter]
Set the bootable flag? (Y/N): Y
Unused partition space(s) found. Use one to protect more partitions? (Y/N): N
w  # write table to disk and exit

```

### parted basic (via command line options)

```
parted --script /dev/sda mklabel gpt
parted --script --align optimal /dev/sda mkpart primary ext4 0% -8GiB mkpart primary linux-swap -8GiB 100%

```

### sgdisk basic (auto discover)

Get the values of: **disk space** and **swap space**, then set **root partition** space.

*   **Disk space** is rounded **down** to nearest mebibyte, and the header GPT metadata space is deducted (1 MiB).
*   **Swap space** is rounded **up** to nearest mebibyte based on memory.

```
diskspace=$(( $(grep sda$ /proc/partitions | awk '{print $3}') * 2 / 2048 - 1 ))
swapspace=$(( $(head -n1 /proc/meminfo | awk '{print $2}') / 1024 + 1 ))
rootspace=$(( $diskspace - $swapspace ))

```

Then run this (this is a **dry-run** used for testing, remove **--pretend** to alter partition table):

```
sgdisk --clear --new 1:0:+${rootspace}MiB --new 2:0:+${swapspace}MiB --typecode 2:8200 --pretend --print /dev/sda

```

### Convert from MBR to GPT

One of the best features of gdisk (and sgdisk and cgdisk too) is its ability to convert MBR and BSD disklabels to GPT without data loss. Upon conversion, all the MBR primary partitions and the logical partitions become GPT partitions with the correct partition type GUIDs and Unique partition GUIDs created for each partition.

Just open the MBR disk using gdisk and exit with "w" option to write the changes back to the disk (similar to fdisk) to convert the MBR disk to GPT. **Watch out for any error and fix them before writing any change to disk** because you may risk losing data. See [http://www.rodsbooks.com/gdisk/mbr2gpt.html](http://www.rodsbooks.com/gdisk/mbr2gpt.html) for more info. After conversion, the bootloaders will need to be reinstalled to configure them to boot from GPT.

**Note:**

*   Remember that GPT stores a secondary table at the end of disk. This data structure consumes 33 512-byte sectors by default. MBR doesn't have a similar data structure at its end, which means that the last partition on an MBR disk sometimes extends to the very end of the disk and prevents complete conversion. If this happens to you, you must abandon the conversion, resize the final partition, or convert everything but the final partition.
*   Keep in mind that if your Boot-Manager is GRUB, it needs a [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). If your MBR Partitioning Layout isn't too old, there is a good chance that the first partition starts at sector 2048 for alignment reasons. That means at the beginning will be 1007 [KiB](https://en.wikipedia.org/wiki/KiB "wikipedia:KiB") of empty space where this bios-boot partition can be created. To do this, first do the mbr->gpt conversion with gdisk as described above. Afterwards, create a new partition with gdisk and manually specify its position to be sectors 34 - 2047, and set the `EF02` partition type.
*   There are known corruption issues with the backup GPT table on laptops that are Intel chipset based, and run in RAID mode. The solution is to use AHCI instead of RAID, if possible.

See also [fdisk#Convert between MBR and GPT](/index.php/Fdisk#Convert_between_MBR_and_GPT "Fdisk").

### Resize a partition

This is generally applicable to reduce partition, so a new one can be created in that space. But it can be applied to growing a partition also. This example is for reducing a partition size.

**Warning:** Backup your data before attempting this. Resizing a partition can possibly compromise the filesystem on it. Try this on a [virtual machine environment](/index.php/Category:Virtualization "Category:Virtualization"), before trying this on a live system.

```
# parted /dev/sdX
p # take note of where the target partition ends
resizepart <PART NUMBER> <NEW END SIZE>
quit

```

After this, the filesystem on the reduced partition might need to be recreated. A new partition can be created in the new space at the end of the resized partition. The partition numbering will not be sequential. [Sorting](#Sort_the_partitions) can be used.

### Sort the partitions

This applies for when a new partition is created in the space between two partitions, after one of them is [resized](#Resize_a_partition).

```
# gdisk /dev/sdX
s # this will sort the partitions
w

```

After sorting the partitions, it might be required to adjust the `/etc/fstab` and/or the `/etc/crypttab` configuration files, the latter only in case of [encrypted](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") partitions.

## See also

*   Wikipedia's Page on [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") and [MBR](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record")
*   [Homepage of Rod Smith's GPT fdisk tool](http://rodsbooks.com/gdisk/) and its [Sourceforge.net Project page - gptfdisk](http://sourceforge.net/projects/gptfdisk/)
*   Rod Smith's page on [What's a GPT?](http://www.rodsbooks.com/gdisk/whatsgpt.html) [Converting MBR to GPT](http://rodsbooks.com/gdisk/mbr2gpt.html) and [Booting OSes from GPT](http://rodsbooks.com/gdisk/booting.html)
*   Rod Smith's page on the [New Partition Type GUID](http://www.rodsbooks.com/linux-fs-code/index.html) for Linux data partitions
*   [System Rescue CD's page on GPT](http://sysresccd.org/Sysresccd-Partitioning-The-new-GPT-disk-layout)
*   Wikipedia page on [BIOS Boot Partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [Make the most of large drives with GPT and Linux - IBM Developer Works](http://www.ibm.com/developerworks/linux/library/l-gpt/index.html?ca=dgr-lnxw07GPT-Storagedth-lx&S_TACT=105AGY83&S_CMP=grlnxw07)
*   [Microsoft's Windows and GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)
*   Fedora developer discussion on [BIOS/GPT configuration](http://mjg59.dreamwidth.org/8035.html)