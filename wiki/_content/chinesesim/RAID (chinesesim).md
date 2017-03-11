**翻译状态：** 本文是英文页面 [RAID](/index.php/RAID "RAID") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2017-02-07，点击[这里](https://wiki.archlinux.org/index.php?title=RAID&diff=0&oldid=466889)可以查看翻译后英文页面的改动。

本文主要叙述了RAID的意义与基本形式，以及如何配置软/硬RAID。

## Contents

*   [1 简介](#.E7.AE.80.E4.BB.8B)
    *   [1.1 基本RAID级别](#.E5.9F.BA.E6.9C.ACRAID.E7.BA.A7.E5.88.AB)
    *   [1.2 嵌套 RAID 级别](#.E5.B5.8C.E5.A5.97_RAID_.E7.BA.A7.E5.88.AB)
    *   [1.3 RAID 级别对比](#RAID_.E7.BA.A7.E5.88.AB.E5.AF.B9.E6.AF.94)
*   [2 实施方法](#.E5.AE.9E.E6.96.BD.E6.96.B9.E6.B3.95)
    *   [2.1 Which type of RAID do I have?](#Which_type_of_RAID_do_I_have.3F)
*   [3 Installation](#Installation)
    *   [3.1 Prepare the Devices](#Prepare_the_Devices)
    *   [3.2 Create the Partition Table (GPT)](#Create_the_Partition_Table_.28GPT.29)
        *   [3.2.1 Partitions Types for MBR](#Partitions_Types_for_MBR)
    *   [3.3 Build the Array](#Build_the_Array)
    *   [3.4 Update configuration file](#Update_configuration_file)
    *   [3.5 Assemble the Array](#Assemble_the_Array)
    *   [3.6 Format the RAID Filesystem](#Format_the_RAID_Filesystem)
        *   [3.6.1 Calculating the Stride and Stripe Width](#Calculating_the_Stride_and_Stripe_Width)
            *   [3.6.1.1 Example 1\. RAID0](#Example_1._RAID0)
            *   [3.6.1.2 Example 2\. RAID5](#Example_2._RAID5)
            *   [3.6.1.3 Example 3\. RAID10,far2](#Example_3._RAID10.2Cfar2)
*   [4 Mounting from a Live CD](#Mounting_from_a_Live_CD)
*   [5 Installing Arch Linux on RAID](#Installing_Arch_Linux_on_RAID)
    *   [5.1 Update configuration file](#Update_configuration_file_2)
    *   [5.2 Add mdadm hook to mkinitcpio.conf](#Add_mdadm_hook_to_mkinitcpio.conf)
    *   [5.3 Configure the boot loader](#Configure_the_boot_loader)
*   [6 RAID Maintenance](#RAID_Maintenance)
    *   [6.1 Scrubbing](#Scrubbing)
        *   [6.1.1 General Notes on Scrubbing](#General_Notes_on_Scrubbing)
        *   [6.1.2 RAID1 and RAID10 Notes on Scrubbing](#RAID1_and_RAID10_Notes_on_Scrubbing)
    *   [6.2 Removing Devices from an Array](#Removing_Devices_from_an_Array)
    *   [6.3 Adding a New Device to an Array](#Adding_a_New_Device_to_an_Array)
    *   [6.4 Increasing Size of a RAID Volume](#Increasing_Size_of_a_RAID_Volume)
    *   [6.5 Change sync speed limits](#Change_sync_speed_limits)
*   [7 Monitoring](#Monitoring)
    *   [7.1 Watch mdstat](#Watch_mdstat)
    *   [7.2 Track IO with iotop](#Track_IO_with_iotop)
    *   [7.3 Track IO with iostat](#Track_IO_with_iostat)
    *   [7.4 Mailing on events](#Mailing_on_events)
        *   [7.4.1 Alternative method](#Alternative_method)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Error: "kernel: ataX.00: revalidation failed"](#Error:_.22kernel:_ataX.00:_revalidation_failed.22)
    *   [8.2 Start arrays read-only](#Start_arrays_read-only)
    *   [8.3 Recovering from a broken or missing drive in the raid](#Recovering_from_a_broken_or_missing_drive_in_the_raid)
*   [9 Benchmarking](#Benchmarking)
*   [10 See also](#See_also)

## 简介

参见 [Wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID").

磁盘阵列（Redundant Arrays of Independent Disks，RAID），有“独立磁盘构成的具有冗余能力的阵列”之意。 磁盘阵列是由很多价格较便宜的磁盘，以硬件（RAID卡）或软件（例如[ZFS (简体中文)](/index.php/ZFS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ZFS (简体中文)") ）形式组合成一个容量巨大的磁盘组，利用个别磁盘提供数据所产生加成效果提升整个磁盘系统效能。利用这项技术，将数据切割成许多区段，分别存放在各个硬盘上。 磁盘阵列还能利用同位检查（Parity Check）的观念，在数组中任意一个硬盘故障时，仍可读出数据，在数据重构时，将数据经计算后重新置入新硬盘中。

**Warning:** 尽管RAID可以预防数据丢失，但并不完全保证数据不会丢失，请在使用RAID的同时注意备份重要数据
}

### 基本RAID级别

这里有许多不同的 [RAID级别](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels")，请你选择最合适于您的。

	[RAID 0](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_0 "wikipedia:Standard RAID levels")

	RAID 0 并不是真正的RAID结构，没有数据冗余，没有数据校验的磁盘陈列。实现RAID 0至少需要两块以上的硬盘，它将两块以上的硬盘合并成一块，数据连续地分割在每块盘上。 因为带宽加倍，所以读/写速度加倍， 但RAID 0在提高性能的同时，并没有提供数据保护功能，只要任何一块硬盘损坏就会丢失所有数据。因此RAID 0 不可应用于需要数据高可用性的关键领域。

	[RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1 "wikipedia:Standard RAID levels")

	RAID1是将一个两块硬盘所构成RAID磁盘阵列，其容量仅等于一块硬盘的容量，因为另一块只是当作数据“镜像”。RAID 1磁盘阵列显然是最可靠的一种阵列，因为它总是保持一份完整的数据备份。它的性能自然没有RAID 0磁盘阵列那样好，但其数据读取确实较单一硬盘来的快，因为数据会从两块硬盘中较快的一块中读出。RAID 1磁盘阵列的写入速度通常较慢，因为数据得分别写入两块硬盘中并做比较。RAID 1磁盘阵列一般支持“热交换”，就是说阵列中硬盘的移除或替换可以在系统运行时进行，无须中断退出系统。RAID 1磁盘阵列是十分安全的，不过也是较贵一种RAID磁盘阵列解决方案，因为两块硬盘仅能提供一块硬盘的容量。RAID 1磁盘阵列主要用在数据安全性很高，而且要求能够快速恢复被破坏的数据的场合。

	[RAID 5](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_5 "wikipedia:Standard RAID levels")

	RAID 5 是一种存储性能、数据安全和存储成本兼顾的存储解决方案。 RAID 5可以理解为是RAID 0和RAID 1的折中方案。RAID 5可以为系统提供数据安全保障，但保障程度要比Mirror低而磁盘空间利用率要比Mirror高。RAID 5具有和RAID 0相近似的数据读取速度，只是多了一个奇偶校验信息，写入数据的速度比对单个磁盘进行写入操作稍慢。同时由于多个数据对应一个奇偶校验信息，RAID 5的磁盘空间利用率要比RAID 1高，存储成本相对较低，是目前运用较多的一种解决方案。

**Note:** 尽管RAID 5是数据安全与I/O速度的权衡，但是由于其工作方式，在大于4Tb的场合下，磁盘故障发生后，数据重建的难度将大大增加。所以存储行业并不建议使用RAID5

	[RAID 6](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_6 "wikipedia:Standard RAID levels")

	RAID6技术是在RAID 5基础上，为了进一步加强数据保护而设计的一种RAID方式，实际上是一种扩展RAID 5等级。与RAID 5的不同之处于除了每个硬盘上都有同级数据XOR校验区外，还有一个针对每个数据块的XOR校验区。当然，当前盘数据块的校验数据不可能存在当前盘而是交错存储的，具体形式见图。这样一来，等于每个数据块有了两个校验保护屏障（一个分层校验，一个是总体校验），因此RAID 6的数据冗余性能相当好。但是，由于增加了一个校验，所以写入的效率较RAID 5还差，而且控制系统的设计也更为复杂，第二块的校验区也减少了有效存储空间。

**Note:** 组成RAID 6阵列需要至少四块磁盘。

### 嵌套 RAID 级别

	RAID 10/01

	RAID 10是先镜射再分区数据，再将所有硬盘分为两组，视为是RAID 0的最低组合，然后将这两组各自视为RAID 1运作。RAID 01则是跟RAID 10的程序相反，是先分区再将数据镜射到两组硬盘。它将所有的硬盘分为两组，变成RAID 1的最低组合，而将两组硬盘各自视为RAID 0运作。

当RAID 10有一个硬盘受损，其余硬盘会继续运作。RAID 01只要有一个硬盘受损，同组RAID 0的所有硬盘都会停止运作，只剩下其他组的硬盘运作，可靠性较低。如果以六个硬盘建RAID 01，镜射再用三个建RAID 0，那么坏一个硬盘便会有三个硬盘离线。因此，RAID 10远较RAID 01常用，零售主板绝大部分支持RAID 0/1/5/10，但不支持RAID 01。

### RAID 级别对比

| RAID等級 | 最少磁盘 | 最大容错 | 可用容量 | 读取效能 | 写入效能 | 安全性 | 目的 | 应用场合 |
| 单一硬盘 | (參考) | 0 | 1 | 1 | 1 | 无 |
| JBOD | 1 | 0 | n | 1 | 1 | 无（同RAID 0） | 增加容量 | 个人（暂时）存储备份 |
| 0 | 2 | 0 | n | n | n | 一块硬盘故障，整个阵列损坏 | 追求最大容量、速度 | 影片剪接快取用途 |
| 1 | 2 | n-1 | 1 | n | 1 | 最高，一个正常即可 | 追求最大安全性 | 个人，企业备份 |
| 5 | 3 | 1 | n-1 | n-1 | n-1 | 高 | 追求最大容量、最小预算 | 个人，企业备份 |
| 6 | 4 | 2 | n-2 | n-2 | n-2 | 安全性較RAID 5高 | 同RAID 5，但较安全 | 個人、企業備份 |
| 10 | 4 | n/2 | n/2 | n | n/2 | 安全性高 | 綜合RAID 0/1优点，理论速度較快 | 大型服务器 |

## 实施方法

RAID可由以下方法实施:

	软RAID

	对于软RAID阵列，有以下途径可以实施阵列：

*   抽象层实现 (例如 [mdadm](#Installation));
    **Note:** 我们会在接下来引导你安装

*   逻辑卷实现 (例如 [LVM (简体中文)](/index.php/LVM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "LVM (简体中文)"));
*   文件系统实现 (例如 [ZFS (简体中文)](/index.php/ZFS_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ZFS (简体中文)"), [Btrfs (简体中文)](/index.php/Btrfs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Btrfs (简体中文)")).

	硬RAID

	硬RAID由硬件（可以使芯片组內建也可以是单独设备）直接连接磁盘实现。RAID 逻辑一般由一块板载I/O芯片实现。RAID 的配置可以由直接更改RAID卡的设置实现，也可以由其他厂商指定的方法。操作系统不直接与硬盘联系。在一些情况下可能需要安装厂商专有驱动。

	[FakeRAID](/index.php/Fakeraid "Fakeraid")

	This type of RAID is properly called BIOS or Onboard RAID, but is falsely advertised as hardware RAID. The array is managed by pseudo-RAID controllers where the RAID logic is implemented in an option rom or in the firmware itself [with a EFI SataDriver](http://www.win-raid.com/t19f13-Intel-EFI-RAID-quot-SataDriver-quot-BIOS-Modules.html) (in case of [UEFI](/index.php/UEFI "UEFI")), but are not full hardware RAID controllers with *all* RAID features implemented. Therefore, this type of RAID is sometimes called FakeRAID. [dmraid](https://www.archlinux.org/packages/?name=dmraid) from the [official repositories](/index.php/Official_repositories "Official repositories"), will be used to deal with these controllers. Here are some examples of FakeRAID controllers: [Intel Rapid Storage](https://en.wikipedia.org/wiki/Intel_Rapid_Storage_Technology "wikipedia:Intel Rapid Storage Technology"), JMicron JMB36x RAID ROM, AMD RAID, ASMedia 106x, and NVIDIA MediaShield.

### Which type of RAID do I have?

Since software RAID is implemented by the user, the type of RAID is easily known to the user.

However, discerning between FakeRAID and true hardware RAID can be more difficult. As stated, manufacturers often incorrectly distinguish these two types of RAID and false advertising is always possible. The best solution in this instance is to run the `lspci` command and looking through the output to find the RAID controller. Then do a search to see what information can be located about the RAID controller. Hardware RAID controllers appear in this list, but FakeRAID implementations do not. Also, true hardware RAID controller are often rather expensive (~$400+), so if someone customized the system, then it is very likely that choosing a hardware RAID setup made a very noticeable change in the computer's price.

## Installation

Install [mdadm](https://www.archlinux.org/packages/?name=mdadm) from the [official repositories](/index.php/Official_repositories "Official repositories"). *mdadm* is used for administering pure software RAID using plain block devices: the underlying hardware does not provide any RAID logic, just a supply of disks. *mdadm* will work with any collection of block devices. Even if unusual. For example, one can thus make a RAID array from a collection of thumb drives.

### Prepare the Devices

**Warning:** These steps erase everything on a device, so type carefully!

If the device is being reused or re-purposed from an existing array, erase any old RAID configuration information:

```
# mdadm --zero-superblock /dev/<drive>

```

or if a particular partition on a drive is to be deleted:

```
# mdadm --zero-superblock /dev/<partition>

```

**Note:**

*   Zapping a partition's superblock should not affect the other partitions on the disk.
*   Due to the nature of RAID functionality it is very difficult to [Securely wipe disks](/index.php/Securely_wipe_disk "Securely wipe disk") fully on a running array. Consider whether it is useful to do so before creating it.

### Create the Partition Table (GPT)

It is highly recommended to pre-partition the disks to be used in the array. Since most RAID users are selecting HDDs >2 TB, GPT partition tables are required and recommended. Disks are easily partitioned using [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

*   After created, the partition type should be assigned hex code FD00.
*   If a larger disk array is employed, consider assigning [disk labels](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming") or [partition labels](/index.php/Persistent_block_device_naming#by-partlabel "Persistent block device naming") to make it easier to identify an individual disk later.
*   Creating partitions that are of the same size on each of the devices is preferred.
*   A good tip is to leave approx 100 MB at the end of the device when partitioning. See below for rationale.

#### Partitions Types for MBR

For those creating partitions on HDDs with a MBR partition table, the partition types available for use are:

*   0xDA (for non-fs data -- current recommendation by [kernel.org](https://raid.wiki.kernel.org/index.php/Partition_Types))
*   0xFD (for raid autodetect arrays -- was useful before booting an initrd to load kernel modules)

**Note:** It is also possible to create a RAID directly on the raw disks (without partitions), but not recommended because it can cause problems when swapping a failed disk.

When replacing a failed disk of a RAID, the new disk has to be exactly the same size as the failed disk or bigger — otherwise the array recreation process will not work. Even hard drives of the same manufacturer and model can have small size differences. By leaving a little space at the end of the disk unallocated one can compensate for the size differences between drives, which makes choosing a replacement drive model easier. Therefore, **it is good practice to leave about 100 MB of unallocated space at the end of the disk.**

### Build the Array

**Warning:** Kernel versions 4.2.x and 4.3.x currently have an active bug that prevents them from assembling a RAID10 array; users needing this layout are encouraged to use kernel version 4.1.x series provided by [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) until this bug is fixed. References are provided in the [#See also](#See_also) section.

Use `mdadm` to build the array. Several examples are given below.

**Warning:** Do not simply copy/paste the examples below; use your brain and substitute the correct options/drive letters!

**Note:** If this is a RAID1 array which is intended to boot from [Syslinux](/index.php/Syslinux "Syslinux") a limitation in syslinux v4.07 requires the metadata value to be 1.0 rather than the default of 1.2.

The following example shows building a 2-device RAID1 array:

```
# mdadm --create --verbose --level=1 --metadata=1.2 --raid-devices=2 /dev/md0 /dev/sdb1 /dev/sdc1

```

The following example shows building a RAID5 array with 4 active devices and 1 spare device:

```
# mdadm --create --verbose --level=5 --metadata=1.2 --chunk=256 --raid-devices=4 /dev/md0 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 --spare-devices=1 /dev/sdf1

```

**Tip:** `--chunk` was used in the previous example to change the chunk size from the default value. See [Chunks: the hidden key to RAID performance](http://www.zdnet.com/article/chunks-the-hidden-key-to-raid-performance/) for more on chunk size optimisation.

The following example shows building a RAID10,far2 array with 2 devices:

```
# mdadm --create --verbose --level=10 --metadata=1.2 --chunk=512 --raid-devices=2 --layout=f2 /dev/md0 /dev/sdb1 /dev/sdc1

```

**Tip:** The `--homehost` and `--name` options can be used for a custom raid device name. They are delimited by a colon in the resulting name.

The array is created under the virtual device `/dev/mdX`, assembled and ready to use (in degraded mode). One can directly start using it while mdadm resyncs the array in the background. It can take a long time to restore parity. Check the progress with:

```
$ cat /proc/mdstat

```

### Update configuration file

By default, most of `mdadm.conf` is commented out, and it contains just the following:

 `/etc/mdadm.conf`  `DEVICE partitions` 

This directive tells mdadm to examine the devices referenced by `/proc/partitions` and assemble as many arrays as possible. This is fine if you really do want to start all available arrays and are confident that no unexpected superblocks will be found (such as after installing a new storage device). A more precise approach is as follows:

```
# echo 'DEVICE partitions' > /etc/mdadm.conf
# mdadm --detail --scan >> /etc/mdadm.conf

```

This results in something like the following:

 `/etc/mdadm.conf` 
```
DEVICE partitions
ARRAY /dev/md/0 metadata=1.2 name=pine:0 UUID=27664f0d:111e493d:4d810213:9f291abe
```

This also causes mdadm to examine the devices referenced by `/proc/partitions`. However, only devices that have superblocks with a UUID of `27664…` are assembled in to active arrays.

See `mdadm.conf(5)` for more information.

### Assemble the Array

Once the configuration file has been updated the array can be assembled using mdadm:

```
# mdadm --assemble --scan

```

### Format the RAID Filesystem

The array can now be formatted like any other disk, just keep in mind that:

*   Due to the large volume size not all filesystems are suited (see: [File system limits](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Limits "wikipedia:Comparison of file systems")).
*   The filesystem should support growing and shrinking while online (see: [File system features](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "wikipedia:Comparison of file systems")).
*   One should calculate the correct stride and stripe-width for optimal performance.

#### Calculating the Stride and Stripe Width

Two parameters are required to optimise the filesystem structure to fit optimally within the underlying RAID structure: the *stride* and *stripe width*. These are derived from the RAID *chunk size*, the filesystem *block size*, and the *number of "data disks"*.

The chunk size is a property of the RAID array, decided at the time of its creation. `mdadm`'s current default is 512 KiB. It can be found with `mdadm`:

```
# mdadm --detail /dev/mdX | grep 'Chunk Size'

```

The block size is a property of the filesystem, decided at *its* creation. The default for many filesystems, including ext4, is 4 KiB. See `/etc/mke2fs.conf` for details on ext4.

The number of "data disks" is the minimum number of devices in the array required to completely rebuild it without data loss. For example, this is N for a raid0 array of N devices and N-1 for raid5.

Once you have these three quantities, the stride and the stripe width can be calculated using the following formulas:

```
stride = chunk size / block size
stripe width = number of data disks * stride

```

##### Example 1\. RAID0

Example formatting to ext4 with the correct stripe width and stride:

*   Hypothetical RAID0 array is composed of 2 physical disks.
*   Chunk size is 64 KiB.
*   Block size is 4 KiB.

stride = chunk size / block size. In this example, the math is 64/4 so the stride = 16.

stripe width = # of physical **data** disks * stride. In this example, the math is 2*16 so the stripe width = 32.

```
# mkfs.ext4 -v -L myarray -m 0.5 -b 4096 -E stride=16,stripe-width=32 /dev/md0

```

##### Example 2\. RAID5

Example formatting to ext4 with the correct stripe width and stride:

*   Hypothetical RAID5 array is composed of 4 physical disks; 3 data discs and 1 parity disc.
*   Chunk size is 512 KiB.
*   Block size is 4 KiB.

stride = chunk size / block size. In this example, the math is 512/4 so the stride = 128.

stripe width = # of physical **data** disks * stride. In this example, the math is 3*128 so the stripe width = 384.

```
# mkfs.ext4 -v -L myarray -m 0.01 -b 4096 -E stride=128,stripe-width=384 /dev/md0

```

For more on stride and stripe width, see: [RAID Math](http://wiki.centos.org/HowTos/Disk_Optimization).

##### Example 3\. RAID10,far2

Example formatting to ext4 with the correct stripe width and stride:

*   Hypothetical RAID10 array is composed of 2 physical disks. Because of the properties of RAID10 in far2 layout, both count as data disks.
*   Chunk size is 512 KiB.

```
# mdadm --detail /dev/md0 | grep 'Chunk Size'
    Chunk Size : 512K

```

*   Block size is 4 KiB.

stride = chunk size / block size. In this example, the math is 512/4 so the stride = 128.

stripe width = # of physical **data** disks * stride. In this example, the math is 2*128 so the stripe width = 256.

```
# mkfs.ext4 -v -L myarray -m 0.01 -b 4096 -E stride=128,stripe-width=256 /dev/md0

```

## Mounting from a Live CD

Users wanting to mount the RAID partition from a Live CD, use:

```
# mdadm --assemble /dev/<disk1> /dev/<disk2> /dev/<disk3> /dev/<disk4>

```

If your RAID 1 that's missing a disk array was wrongly auto-detected as RAID 1 (as per `mdadm --detail /dev/md<number>`) and reported as inactive (as per `cat /proc/mdstat`), stop the array first:

```
# mdadm --stop /dev/md<number>

```

## Installing Arch Linux on RAID

**Note:** The following section is applicable only if the root filesystem resides on the array. Users may skip this section if the array holds a data partition(s).

You should create the RAID array between the [Partitioning](/index.php/Partitioning "Partitioning") and [formatting](/index.php/File_systems#Format_a_device "File systems") steps of the Installation Procedure. Instead of directly formatting a partition to be your root file system, it will be created on a RAID array. Follow the section [#Setup](#Setup) to create the RAID array. Then continue with the installation procedure until the pacstrap step is completed. When using [UEFI boot](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), also read [ESP on RAID](/index.php/EFI_System_Partition#ESP_on_RAID "EFI System Partition").

### Update configuration file

**Note:** This should be done outside of the chroot, hence the prefix /mnt to the filepath.

After the base system is installed the default configuration file, `mdadm.conf`, must be updated like so:

```
# mdadm --detail --scan >> /mnt/etc/mdadm.conf

```

Always check the mdadm.conf configuration file using a text editor after running this command to ensure that its contents look reasonable.

**Note:** To prevent failure of **mdmonitor** at boot (enabled by default), you will need to uncomment **MAILADDR** and provide an e-mail address and/or application to handle notification of problems with your array at the bottom of mdadm.conf.

Continue with the installation procedure until you reach the step “Create initial ramdisk environment”, then follow the next section.

### Add mdadm hook to mkinitcpio.conf

**Note:** This should be done whilst chrooted.

Add `mdadm_udev` to the [HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") section of the `mkinitcpio.conf` to add support for mdadm directly into the init image:

```
HOOKS="base udev autodetect block **mdadm_udev** filesystems usbinput fsck"

```

Then [Regenerate the initramfs image](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

### Configure the boot loader

Add an `md` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") for each RAID array; also point the `root` parameter to the correct mapped device. The following example accommodates three RAID 1 arrays and sets the second one as root:

```
root=/dev/md1 md=0,/dev/sda2,/dev/sdb2 md=1,/dev/sda3,/dev/sdb3 md=2,/dev/sda4,/dev/sdb4

```

If booting from a software raid partition fails using the kernel device node method above, an alternative and more reliable way is to use [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), for example:

```
root=LABEL=Root_Label

```

See also [GRUB#RAID](/index.php/GRUB#RAID "GRUB").

## RAID Maintenance

### Scrubbing

It is good practice to regularly run data [scrubbing](https://en.wikipedia.org/wiki/Data_scrubbing "wikipedia:Data scrubbing") to check for and fix errors. Depending on the size/configuration of the array, a scrub may take multiple hours to complete.

To initiate a data scrub:

```
# echo check > /sys/block/md0/md/sync_action

```

The check operation scans the drives for bad sectors and automatically repairs them. If it finds good sectors that contain bad data (the data in a sector does not agree with what the data from another disk indicates that it should be, for example the parity block + the other data blocks would cause us to think that this data block is incorrect), then no action is taken, but the event is logged (see below). This "do nothing" allows admins to inspect the data in the sector and the data that would be produced by rebuilding the sectors from redundant information and pick the correct data to keep.

As with many tasks/items relating to mdadm, the status of the scrub can be queried by reading `/proc/mdstat`.

Example:

 `$ cat /proc/mdstat` 
```
Personalities : [raid6] [raid5] [raid4] [raid1] 
md0 : active raid1 sdb1[0] sdc1[1]
      3906778112 blocks super 1.2 [2/2] [UU]
      [>....................]  check =  4.0% (158288320/3906778112) finish=386.5min speed=161604K/sec
      bitmap: 0/30 pages [0KB], 65536KB chunk

```

To stop a currently running data scrub safely:

```
# echo idle > /sys/block/md0/md/sync_action

```

**Note:** If the system is rebooted after a partial scrub has been suspended, the scrub will start over.

When the scrub is complete, admins may check how many blocks (if any) have been flagged as bad:

```
# cat /sys/block/md0/md/mismatch_cnt

```

#### General Notes on Scrubbing

**Note:** Users may alternatively echo **repair** to /sys/block/md0/md/sync_action but this is ill-advised since if a mismatch in the data is encountered, it would be automatically updated to be consistent. The danger is that we really don't know whether it's the parity or the data block that's correct (or which data block in case of RAID1). It's luck-of-the-draw whether or not the operation gets the right data instead of the bad data.

It is a good idea to set up a cron job as root to schedule a periodic scrub. See [raid-check](https://aur.archlinux.org/packages/raid-check/) which can assist with this. To perform a periodic scrub using systemd timers instead of cron, See [raid-check-systemd](https://aur.archlinux.org/packages/raid-check-systemd/) which contains the same script along with associated systemd timer unit files. (note: for typical platter drives, scrubbing can take approximately **six seconds per gigabyte** [that's one hour forty-five minutes per terabyte] so plan the start of your cron job or timer appropriately)

#### RAID1 and RAID10 Notes on Scrubbing

Due to the fact that RAID1 and RAID10 writes in the kernel are unbuffered, an array can have non-0 mismatch counts even when the array is healthy. These non-0 counts will only exist in transient data areas where they don't pose a problem. However, we can't tell the difference between a non-0 count that is just in transient data or a non-0 count that signifies a real problem. This fact is a source of false positives for RAID1 and RAID10 arrays. It is however still recommended to scrub regularly in order to catch and correct any bad sectors that might be present in the devices.

### Removing Devices from an Array

One can remove a device from the array after marking it as faulty:

```
# mdadm --fail /dev/md0 /dev/sdxx

```

Now remove it from the array:

```
# mdadm --remove /dev/md0 /dev/sdxx

```

Remove device permanently (for example, to use it individually from now on): Issue the two commands described above then:

```
# mdadm --zero-superblock /dev/sdxx

```

**Warning:** **DO NOT** issue this command on linear or RAID0 arrays or data **LOSS** will occur!

**Warning:** Reusing the removed disk without zeroing the superblock **WILL CAUSE LOSS OF ALL DATA** on the next boot. (After mdadm will try to use it as the part of the raid array).

Stop using an array:

1.  Umount target array
2.  Stop the array with: `mdadm --stop /dev/md0`
3.  Repeat the three command described in the beginning of this section on each device.
4.  Remove the corresponding line from /etc/mdadm.conf

### Adding a New Device to an Array

Adding new devices with mdadm can be done on a running system with the devices mounted. Partition the new device using the same layout as one of those already in the arrays as discussed above.

Assemble the RAID array if it is not already assembled:

```
# mdadm --assemble /dev/md0 /dev/sda1 /dev/sdb1

```

Add the new device the array:

```
# mdadm --add /dev/md0 /dev/sdc1

```

This should not take long for mdadm to do. Again, check the progress with:

```
# cat /proc/mdstat

```

Check that the device has been added with the command:

```
# mdadm --misc --detail /dev/md0

```

**Note:** For RAID0 arrays you may get the following error message:
```
mdadm: add new device failed for /dev/sdc1 as 2: Invalid argument

```

This is because the above commands will add the new disk as a "spare" but RAID0 doesn't have spares. If you want to add a device to a RAID0 array, you need to "grow" and "add" in the same command. This is demonstrated below:

```
# mdadm --grow /dev/md0 --raid-devices=3 --add /dev/sdc1

```

### Increasing Size of a RAID Volume

If larger disks are installed in a RAID array or partition size has been increased, it may be desirable to increase the size of the RAID volume to fill the larger available space. This process may be begun by first following the above sections pertaining to replacing disks. Once the RAID volume has been rebuilt onto the larger disks it must be "grown" to fill the space.

```
# mdadm --grow /dev/md0 --size=max

```

Next, partitions present on the RAID volume `/dev/md0` may need to be resized. See [Partitioning](/index.php/Partitioning "Partitioning") for details. Finally, the filesystem on the above mentioned partition will need to be resized. If partitioning was performed with `gparted` this will be done automatically. If other tools were used, unmount and then resize the filesystem manually.

```
# umount /storage
# fsck.ext4 -f /dev/md0p1
# resize2fs /dev/md0p1

```

### Change sync speed limits

Syncing can take a while. If the machine is not needed for other tasks the speed limit can be increased.

 `# cat /proc/mdstat` 
```
 Personalities : [raid1] 
 md0 : active raid1 sda3[2] sdb3[1]
       155042219 blocks super 1.2 [2/1] [_U]
       [>....................]  recovery =  0.0% (77696/155042219) finish=265.8min speed=9712K/sec

 unused devices: <none>

```

Check the current speed limit.

 `# cat /proc/sys/dev/raid/speed_limit_min` 
```
1000

```
 `# cat /proc/sys/dev/raid/speed_limit_max` 
```
200000

```

Increase the limits.

```
# echo 400000 >/proc/sys/dev/raid/speed_limit_min
# echo 400000 >/proc/sys/dev/raid/speed_limit_max

```

Then check out the syncing speed and estimated finish time.

 `# cat /proc/mdstat` 
```
 Personalities : [raid1] 
 md0 : active raid1 sda3[2] sdb3[1]
       155042219 blocks super 1.2 [2/1] [_U]
       [>....................]  recovery =  1.3% (2136640/155042219) finish=158.2min speed=16102K/sec

 unused devices: <none>

```

See also [sysctl#MDADM](/index.php/Sysctl#MDADM "Sysctl").

## Monitoring

A simple one-liner that prints out the status of the RAID devices:

```
awk '/^md/ {printf "%s: ", $1}; /blocks/ {print $NF}' </proc/mdstat

```

```
md1: [UU]
md0: [UU]

```

### Watch mdstat

 `watch -t 'cat /proc/mdstat'` 

Or preferably using [tmux](https://www.archlinux.org/packages/?name=tmux)

 `tmux split-window -l 12 "watch -t 'cat /proc/mdstat'"` 

### Track IO with iotop

The [iotop](https://www.archlinux.org/packages/?name=iotop) package displays the input/output stats for processes. Use this command to view the IO for raid threads.

 `iotop -a -p $(sed 's, , -p ,g' <<<`pgrep "_raid|_resync|jbd2"`)` 

### Track IO with iostat

The *iostat* utility from [sysstat](https://www.archlinux.org/packages/?name=sysstat) package displays the input/output statistics for devices and partitions.

```
 iostat -dmy 1 /dev/md0
 iostat -dmy 1 # all

```

### Mailing on events

A smtp mail server (sendmail) or at least an email forwarder (ssmtp/msmtp) is required to accomplish this. Perhaps the most simplistic solution is to use [dma](https://aur.archlinux.org/packages/dma/) which is very tiny (installs to 0.08 MiB) and requires no setup.

Edit `/etc/mdadm.conf` defining the email address to which notifications will be received.

**Note:** If using dma as mentioned above, users may simply mail directly to the username on the localhost rather than to an external email address.

To test the configuration:

```
# mdadm --monitor --scan --oneshot --test

```

[mdadm](/index.php/Mdadm "Mdadm") includes a systemd service (mdmonitor.service) to perform the monitoring task, so at this point, you have nothing left to do. If you do not set a mail address in `/etc/mdadm.conf`, that service will fail. If you do not want to receive mail on mdadm events, the failure can be ignored; if you don't want notifications and are sensitive about failure messages, you can mask the unit.

#### Alternative method

To avoid the installation of a smtp mail server or an email forwarder you can use the [S-nail](/index.php/S-nail "S-nail") tool (don't forget to setup) already on your system.

Create a file named `/etc/mdadm_warning.sh` with:

```
#!/bin/bash
event=$1
device=$2

echo " " | /usr/bin/mailx -s "$event on $device" **destination@email.com**

```

And give it execution permissions `chmod +x /etc/mdadm_warning.sh`

Then add this to the mdadm.conf

```
PROGRAM /etc/mdadm_warning.sh

```

To test and enable use the same as in the previous method.

## Troubleshooting

If you are getting error when you reboot about "invalid raid superblock magic" and you have additional hard drives other than the ones you installed to, check that your hard drive order is correct. During installation, your RAID devices may be hdd, hde and hdf, but during boot they may be hda, hdb and hdc. Adjust your kernel line accordingly. This is what happened to me anyway.

### Error: "kernel: ataX.00: revalidation failed"

If you suddenly (after reboot, changed BIOS settings) experience Error messages like:

```
Feb  9 08:15:46 hostserver kernel: ata8.00: revalidation failed (errno=-5)

```

Is doesn't necessarily mean that a drive is broken. You often find panic links on the web which go for the worst. In a word, No Panic. Maybe you just changed APIC or ACPI settings within your BIOS or Kernel parameters somehow. Change them back and you should be fine. Ordinarily, turning ACPI and/orACPI off should help.

### Start arrays read-only

When an md array is started, the superblock will be written, and resync may begin. To start read-only set the kernel module `md_mod` parameter `start_ro`. When this is set, new arrays get an 'auto-ro' mode, which disables all internal io (superblock updates, resync, recovery) and is automatically switched to 'rw' when the first write request arrives.

**Note:** The array can be set to true 'ro' mode using `mdadm --readonly` before the first write request, or resync can be started without a write using `mdadm --readwrite`.

To set the parameter at boot, add `md_mod.start_ro=1` to your kernel line.

Or set it at module load time from `/etc/modprobe.d/` file or from directly from `/sys/`.

 `echo 1 > /sys/module/md_mod/parameters/start_ro` 

### Recovering from a broken or missing drive in the raid

You might get the above mentioned error also when one of the drives breaks for whatever reason. In that case you will have to force the raid to still turn on even with one disk short. Type this (change where needed):

```
# mdadm --manage /dev/md0 --run

```

Now you should be able to mount it again with something like this (if you had it in fstab):

```
# mount /dev/md0

```

Now the raid should be working again and available to use, however with one disk short! So, to add that one disc partition it the way like described above in [Prepare the device](#Prepare_the_Devices). Once that is done you can add the new disk to the raid by doing:

```
# mdadm --manage --add /dev/md0 /dev/sdd1

```

If you type:

```
# cat /proc/mdstat

```

you probably see that the raid is now active and rebuilding.

You also might want to update your configuration (see: [#Update configuration file](#Update_configuration_file)).

## Benchmarking

There are several tools for benchmarking a RAID. The most notable improvement is the speed increase when multiple threads are reading from the same RAID volume.

[tiobench](https://aur.archlinux.org/packages/tiobench/) specifically benchmarks these performance improvements by measuring fully-threaded I/O on the disk.

[bonnie++](https://www.archlinux.org/packages/?name=bonnie%2B%2B) tests database type access to one or more files, and creation, reading, and deleting of small files which can simulate the usage of programs such as Squid, INN, or Maildir format e-mail. The enclosed [ZCAV](http://www.coker.com.au/bonnie++/zcav/) program tests the performance of different zones of a hard drive without writing any data to the disk.

`hdparm` should **NOT** be used to benchmark a RAID, because it provides very inconsistent results.

## See also

*   [Software RAID in the new Linux 2.4 kernel, Part 1](http://www.gentoo.org/doc/en/articles/software-raid-p1.xml) and [Part 2](http://www.gentoo.org/doc/en/articles/software-raid-p2.xml) in the Gentoo Linux Docs
*   [Linux RAID wiki entry](http://raid.wiki.kernel.org/index.php/Linux_Raid) on The Linux Kernel Archives
*   [How Bitmaps Work](https://raid.wiki.kernel.org/index.php/Write-intent_bitmap)
*   [Chapter 15: Redundant Array of Independent Disks (RAID)](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html) of Red Hat Enterprise Linux 6 Documentation
*   [Linux-RAID FAQ](http://tldp.org/FAQ/Linux-RAID-FAQ/x37.html) on the Linux Documentation Project
*   [Dell.com Raid Tutorial](http://support.dell.com/support/topics/global.aspx/support/entvideos/raid?c=us&l=en&s=gen) - Interactive Walkthrough of Raid
*   [BAARF](http://www.miracleas.com/BAARF/) including *[Why should I not use RAID 5?](http://www.miracleas.com/BAARF/RAID5_versus_RAID10.txt)* by Art S. Kagel
*   [Introduction to RAID](http://www.linux-mag.com/id/7924/), [Nested-RAID: RAID-5 and RAID-6 Based Configurations](http://www.linux-mag.com/id/7931/), [Intro to Nested-RAID: RAID-01 and RAID-10](http://www.linux-mag.com/id/7928/), and [Nested-RAID: The Triple Lindy](http://www.linux-mag.com/id/7932/) in Linux Magazine
*   [HowTo: Speed Up Linux Software Raid Building And Re-syncing](http://www.cyberciti.biz/tips/linux-raid-increase-resync-rebuild-speed.html)
*   [RAID5-Server to hold all your data](http://fomori.org/blog/?p=94)

**Active bugs**

*   [linux-raid ML #1](http://marc.info/?l=linux-raid&m=144960710718870&w=2)
*   [linux-raid ML #2](http://marc.info/?l=linux-raid&m=144830809503689&w=2)

**mdadm**

*   [Debian mdadm FAQ](http://anonscm.debian.org/gitweb/?p=pkg-mdadm/mdadm.git;a=blob_plain;f=debian/FAQ;hb=HEAD)
*   [mdadm source code](http://www.kernel.org/pub/linux/utils/raid/mdadm/)
*   [Software RAID on Linux with mdadm](http://www.linux-mag.com/id/7939/) in Linux Magazine

**Forum threads**

*   [Raid Performance Improvements with bitmaps](http://forums.overclockers.com.au/showthread.php?t=865333)
*   [GRUB and GRUB2](https://bbs.archlinux.org/viewtopic.php?id=125445)
*   [Can't install grub2 on software RAID](https://bbs.archlinux.org/viewtopic.php?id=123698)
*   [Use RAID metadata 1.2 in boot and root partition](http://forums.gentoo.org/viewtopic-t-888624-start-0.html)

**RAID with encryption**

*   [Linux/Fedora: Encrypt /home and swap over RAID with dm-crypt](http://www.shimari.com/dm-crypt-on-raid/) by Justin Wells