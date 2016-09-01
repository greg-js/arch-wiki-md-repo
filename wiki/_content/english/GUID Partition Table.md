GUID Partition Table (GPT) is a partitioning scheme that is part of the [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") specification; it uses a [globally unique identifier](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") for qualifying devices. It is the next generation partitioning scheme designed to succeed the [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") partitioning scheme method. It evolved to deal with [several shortcomings](/index.php/Master_Boot_Record#Problems_with_MBR "Master Boot Record") of the MBR partitioning scheme method and offers additional advantages.

## Contents

*   [1 About the GUID Partition Table](#About_the_GUID_Partition_Table)
    *   [1.1 Advantages of GPT](#Advantages_of_GPT)
    *   [1.2 Kernel Support](#Kernel_Support)
*   [2 See also](#See_also)

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
4.  Uses 64-bit LBA for storing Sector numbers - maximum addressable disk size is 2 [ZiB](https://en.wikipedia.org/wiki/ZiB "wikipedia:ZiB"). MBR is limited to addressing 2 TiB of space per drive.
5.  Stores a backup header and partition table at the end of the disk that aids in recovery in case the primary ones are damaged.
6.  CRC32 checksums to detect errors and corruption of the header and partition table.

### Kernel Support

`CONFIG_EFI_PARTITION` option in the kernel config enables GPT support in the kernel (despite the name EFI PARTITION). This options must be built-in the kernel and not compiled as a loadable module. This option is required even if GPT disks are used only for data storage and not for booting. This option is enabled by default in Arch's [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) kernels in [core] repo. In case of a custom kernel enable this option by doing `CONFIG_EFI_PARTITION=y`.

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