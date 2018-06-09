Related articles

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [LVM#RAID](/index.php/LVM#RAID "LVM")
*   [Installing with Fake RAID](/index.php/Installing_with_Fake_RAID "Installing with Fake RAID")
*   [Convert a single drive system to RAID](/index.php/Convert_a_single_drive_system_to_RAID "Convert a single drive system to RAID")
*   [ZFS](/index.php/ZFS "ZFS")
*   [ZFS/Virtual disks](/index.php/ZFS/Virtual_disks "ZFS/Virtual disks")
*   [Swap#Striping](/index.php/Swap#Striping "Swap")
*   [Btrfs#RAID](/index.php/Btrfs#RAID "Btrfs")

Redundant Array of Independent Disks ([RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID")) is a storage technology that combines multiple disk drive components (typically disk drives or partitions thereof) into a logical unit. Depending on the RAID implementation, this logical unit can be a file system or an additional transparent layer that can hold several partitions. Data is distributed across the drives in one of several ways called [#RAID levels](#RAID_levels), depending on the level of redundancy and performance required. The RAID level chosen can thus prevent data loss in the event of a hard disk failure, increase performance or be a combination of both.

This article explains how to create/manage a software RAID array using mdadm.

**Warning:** Be sure [to back up](/index.php/Backup_programs "Backup programs") all data before proceeding.

## Contents

*   [1 RAID levels](#RAID_levels)
    *   [1.1 Standard RAID levels](#Standard_RAID_levels)
    *   [1.2 Nested RAID levels](#Nested_RAID_levels)
    *   [1.3 RAID level comparison](#RAID_level_comparison)
*   [2 Implementation](#Implementation)
    *   [2.1 Which type of RAID do I have?](#Which_type_of_RAID_do_I_have.3F)
*   [3 Installation](#Installation)
    *   [3.1 Prepare the devices](#Prepare_the_devices)
    *   [3.2 Partition the devices](#Partition_the_devices)
        *   [3.2.1 GUID Partition Table](#GUID_Partition_Table)
        *   [3.2.2 Master Boot Record](#Master_Boot_Record)
    *   [3.3 Build the array](#Build_the_array)
    *   [3.4 Update configuration file](#Update_configuration_file)
    *   [3.5 Assemble the array](#Assemble_the_array)
    *   [3.6 Format the RAID filesystem](#Format_the_RAID_filesystem)
        *   [3.6.1 Calculating the stride and stripe width](#Calculating_the_stride_and_stripe_width)
            *   [3.6.1.1 Example 1\. RAID0](#Example_1._RAID0)
            *   [3.6.1.2 Example 2\. RAID5](#Example_2._RAID5)
            *   [3.6.1.3 Example 3\. RAID10,far2](#Example_3._RAID10.2Cfar2)
*   [4 Mounting from a Live CD](#Mounting_from_a_Live_CD)
*   [5 Installing Arch Linux on RAID](#Installing_Arch_Linux_on_RAID)
    *   [5.1 Update configuration file](#Update_configuration_file_2)
    *   [5.2 Configure mkinitcpio](#Configure_mkinitcpio)
    *   [5.3 Configure the boot loader](#Configure_the_boot_loader)
*   [6 RAID Maintenance](#RAID_Maintenance)
    *   [6.1 Scrubbing](#Scrubbing)
        *   [6.1.1 General notes on scrubbing](#General_notes_on_scrubbing)
        *   [6.1.2 RAID1 and RAID10 notes on scrubbing](#RAID1_and_RAID10_notes_on_scrubbing)
    *   [6.2 Removing devices from an array](#Removing_devices_from_an_array)
    *   [6.3 Adding a new device to an array](#Adding_a_new_device_to_an_array)
    *   [6.4 Increasing size of a RAID volume](#Increasing_size_of_a_RAID_volume)
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

## RAID levels

Despite redundancy implied by most RAID levels, RAID does not guarantee that data is safe. A RAID will not protect data if there is a fire, the computer is stolen or multiple hard drives fail at once. Furthermore, installing a system with RAID is a complex process that may destroy data.

### Standard RAID levels

There are many different [levels of RAID](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels"), please find hereafter the most commonly used ones.

	[RAID 0](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_0 "wikipedia:Standard RAID levels")

	Uses striping to combine disks. Even though it *does not provide redundancy*, it is still considered RAID. It does, however, *provide a big speed benefit*. If the speed increase is worth the possibility of data loss (for [swap](/index.php/Swap "Swap") partition for example), choose this RAID level. On a server, RAID 1 and RAID 5 arrays are more appropriate. The size of a RAID 0 array block device is the size of the smallest component partition times the number of component partitions.

	[RAID 1](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_1 "wikipedia:Standard RAID levels")

	The most straightforward RAID level: straight mirroring. As with other RAID levels, it only makes sense if the partitions are on different physical disk drives. If one of those drives fails, the block device provided by the RAID array will continue to function as normal. The example will be using RAID 1 for everything except [swap](/index.php/Swap "Swap") and temporary data. Please note that with a software implementation, the RAID 1 level is the only option for the boot partition, because bootloaders reading the boot partition do not understand RAID, but a RAID 1 component partition can be read as a normal partition. The size of a RAID 1 array block device is the size of the smallest component partition.

	[RAID 5](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_5 "wikipedia:Standard RAID levels")

	Requires 3 or more physical drives, and provides the redundancy of RAID 1 combined with the speed and size benefits of RAID 0\. RAID 5 uses striping, like RAID 0, but also stores parity blocks *distributed across each member disk*. In the event of a failed disk, these parity blocks are used to reconstruct the data on a replacement disk. RAID 5 can withstand the loss of one member disk.

**Note:** RAID 5 is a common choice due to its combination of speed and data redundancy. The caveat is that if one drive were to fail and another drive failed before that drive was replaced, all data will be lost. Furthermore, with modern disk sizes and expected unrecoverable read error (URE) rates on consumer disks, the rebuild of a 4TiB array is **expected** (i.e. higher than 50% chance) to have at least one URE. Because of this, RAID 5 is no longer advised by the storage industry.

	[RAID 6](https://en.wikipedia.org/wiki/Standard_RAID_levels#RAID_6 "wikipedia:Standard RAID levels")

	Requires 4 or more physical drives, and provides the benefits of RAID 5 but with security against two drive failures. RAID 6 also uses striping, like RAID 5, but stores two distinct parity blocks *distributed across each member disk*. In the event of a failed disk, these parity blocks are used to reconstruct the data on a replacement disk. RAID 6 can withstand the loss of two member disks. The robustness against unrecoverable read errors is somewhat better, because the array still has parity blocks when rebuilding from a single failed drive. However, given the overhead, RAID 6 is costly and in most settings RAID 10 in far2 layout (see below) provides better speed benefits and robustness, and is therefore preferred.

### Nested RAID levels

	[RAID 1+0](https://en.wikipedia.org/wiki/Nested_RAID_levels#RAID_10_.28RAID_1.2B0.29 "wikipedia:Nested RAID levels")

	RAID1+0 is a nested RAID that combines two of the standard levels of RAID to gain performance and additional redundancy. It is commonly referred to as *RAID10*, however, Linux MD RAID10 is slightly different from simple RAID layering, see below.

	[RAID 10](https://en.wikipedia.org/wiki/Non-standard_RAID_levels#Linux_MD_RAID_10 "wikipedia:Non-standard RAID levels")

	RAID10 under Linux is built on the concepts of RAID1+0, however, it implements this as a single layer, with multiple possible layouts.

	The *near X* layout on Y disks repeats each chunk X times on Y/2 stripes, but does not need X to divide Y evenly. The chunks are placed on almost the same location on each disk they are mirrored on, hence the name. It can work with any number of disks, starting at 2\. Near 2 on 2 disks is equivalent to RAID1, near 2 on 4 disks to RAID1+0.

	The *far X* layout on Y disks is designed to offer striped read performance on a mirrored array. It accomplishes this by dividing each disk in two sections, say front and back, and what is written to disk 1 front is mirrored in disk 2 back, and vice versa. This has the effect of being able to stripe sequential reads, which is where RAID0 and RAID5 get their performance from. The drawback is that sequential writing has a very slight performance penalty because of the distance the disk needs to seek to the other section of the disk to store the mirror. RAID10 in far 2 layout is, however, preferable to layered RAID1+0 **and** RAID5 whenever read speeds are of concern and availability / redundancy is crucial. However, it is still not a substitute for backups. See the wikipedia page for more information.

### RAID level comparison

| RAID level | Data redundancy | Physical drive utilization | Read performance | Write performance | Min drives |
| **0** | No | 100% | nX

**Best**

 | nX

**Best**

 | 2 |
| **1** | Yes | 50% | Up to nX if multiple processes are reading, otherwise 1X | 1X | 2 |
| **5** | Yes | 67% - 94% | (n−1)X

**Superior**

 | (n−1)X

**Superior**

 | 3 |
| **6** | Yes | 50% - 88% | (n−2)X | (n−2)X | 4 |
| **10,far2** | Yes | 50% | nX

**Best;** on par with RAID0 but redundant

 | (n/2)X | 2 |
| **10,near2** | Yes | 50% | Up to nX if multiple processes are reading, otherwise 1X | (n/2)X | 2 |

* Where *n* is standing for the number of dedicated disks.

## Implementation

The RAID devices can be managed in different ways:

	Software RAID

	This is the easiest implementation as it does not rely on obscure proprietary firmware and software to be used. The array is managed by the operating system either by:

*   by an abstraction layer (e.g. [mdadm](#Installation));
    **Note:** This is the method we will use later in this guide.

*   by a logical volume manager (e.g. [LVM](/index.php/LVM#RAID "LVM"));
*   by a component of a file system (e.g. [ZFS](/index.php/ZFS "ZFS"), [Btrfs](/index.php/Btrfs#RAID "Btrfs")).

	Hardware RAID

	The array is directly managed by a dedicated hardware card installed in the PC to which the disks are directly connected. The RAID logic runs on an on-board processor independently of [the host processor (CPU)](https://en.wikipedia.org/wiki/Central_processing_unit "wikipedia:Central processing unit"). Although this solution is independent of any operating system, the latter requires a driver in order to function properly with the hardware RAID controller. The RAID array can either be configured via an option rom interface or, depending on the manufacturer, with a dedicated application when the OS has been installed. The configuration is transparent for the Linux kernel: it does not see the disks separately.

	[FakeRAID](/index.php/Fakeraid "Fakeraid")

	This type of RAID is properly called BIOS or Onboard RAID, but is falsely advertised as hardware RAID. The array is managed by pseudo-RAID controllers where the RAID logic is implemented in an option rom or in the firmware itself [with a EFI SataDriver](http://www.win-raid.com/t19f13-Intel-EFI-RAID-quot-SataDriver-quot-BIOS-Modules.html) (in case of [UEFI](/index.php/UEFI "UEFI")), but are not full hardware RAID controllers with *all* RAID features implemented. Therefore, this type of RAID is sometimes called FakeRAID. [dmraid](https://www.archlinux.org/packages/?name=dmraid) from the [official repositories](/index.php/Official_repositories "Official repositories"), will be used to deal with these controllers. Here are some examples of FakeRAID controllers: [Intel Rapid Storage](https://en.wikipedia.org/wiki/Intel_Rapid_Storage_Technology "wikipedia:Intel Rapid Storage Technology"), JMicron JMB36x RAID ROM, AMD RAID, ASMedia 106x, and NVIDIA MediaShield.

### Which type of RAID do I have?

Since software RAID is implemented by the user, the type of RAID is easily known to the user.

However, discerning between FakeRAID and true hardware RAID can be more difficult. As stated, manufacturers often incorrectly distinguish these two types of RAID and false advertising is always possible. The best solution in this instance is to run the `lspci` command and looking through the output to find the RAID controller. Then do a search to see what information can be located about the RAID controller. Hardware RAID controllers appear in this list, but FakeRAID implementations do not. Also, true hardware RAID controller are often rather expensive, so if someone customized the system, then it is very likely that choosing a hardware RAID setup made a very noticeable change in the computer's price.

## Installation

[Install](/index.php/Install "Install") [mdadm](https://www.archlinux.org/packages/?name=mdadm). *mdadm* is used for administering pure software RAID using plain block devices: the underlying hardware does not provide any RAID logic, just a supply of disks. *mdadm* will work with any collection of block devices. Even if unusual. For example, one can thus make a RAID array from a collection of thumb drives.

### Prepare the devices

**Warning:** These steps erase everything on a device, so type carefully!

If the device is being reused or re-purposed from an existing array, erase any old RAID configuration information:

```
# mdadm --misc --zero-superblock /dev/<drive>

```

or if a particular partition on a drive is to be deleted:

```
# mdadm --misc --zero-superblock /dev/<partition>

```

**Note:**

*   Zapping a partition's superblock should not affect the other partitions on the disk.
*   Due to the nature of RAID functionality it is very difficult to [securely wipe disks](/index.php/Securely_wipe_disk "Securely wipe disk") fully on a running array. Consider whether it is useful to do so before creating it.

### Partition the devices

It is highly recommended to partition the disks to be used in the array. Since most RAID users are selecting disk drives larger than 2 TiB, GPT is required and recommended. See [Partitioning](/index.php/Partitioning "Partitioning") for the more information on partitioning and the available [partitioning tools](/index.php/Partitioning_tools "Partitioning tools").

**Note:** It is also possible to create a RAID directly on the raw disks (without partitions), but not recommended because it can cause problems when swapping a failed disk.

**Tip:** When replacing a failed disk of a RAID, the new disk has to be exactly the same size as the failed disk or bigger — otherwise the array recreation process will not work. Even hard drives of the same manufacturer and model can have small size differences. By leaving a little space at the end of the disk unallocated one can compensate for the size differences between drives, which makes choosing a replacement drive model easier. Therefore, it is good practice to leave about 100 MiB of unallocated space at the end of the disk.

#### GUID Partition Table

*   After creating the partitions, their [partition type GUIDs](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") should be `A19D880F-05FC-4D3B-A006-743F0F84911E` (it can be assigned by selecting partition type `Linux RAID` in *fdisk* or `FD00` in *gdisk*).
*   If a larger disk array is employed, consider assigning [filesystem labels](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming") or [partition labels](/index.php/Persistent_block_device_naming#by-partlabel "Persistent block device naming") to make it easier to identify an individual disk later.
*   Creating partitions that are of the same size on each of the devices is recommended.

#### Master Boot Record

For those creating partitions on HDDs with a MBR partition table, the [partition types IDs](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") available for use are:

*   `0xFD` for raid autodetect arrays (`Linux raid autodetect` in *fdisk*)
*   `0xDA` for non-fs data (`Non-FS data` in *fdisk*)

See [Linux Raid Wiki:Partition Types](https://raid.wiki.kernel.org/index.php/Partition_Types) for more information.

### Build the array

Use `mdadm` to build the array. See [mdadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mdadm.8) for supported options. Several examples are given below.

**Warning:** Do not simply copy/paste the examples below; make sure you use substitute the correct options and drive letters.

**Note:**

*   If this is a RAID1 array which is intended to boot from [Syslinux](/index.php/Syslinux "Syslinux") a limitation in syslinux v4.07 requires the metadata value to be 1.0 rather than the default of 1.2.
*   When creating an array from [Arch installation medium](/index.php/Archiso "Archiso") use the option `--homehost=*myhostname*` (or `--homehost=any` to always have the same name regardless of the host) to set the [hostname](/index.php/Hostname "Hostname"), otherwise the hostname `archiso` will be written in the array metadata.

**Tip:** You can specify a custom raid device name using the option `--name=*MyRAIDName*` or by setting the raid device path to `/dev/md/*MyRAIDName*`. Udev will create symlinks to the raid arrays in `/dev/md/` using that name. If `homehost` matches the current [hostname](/index.php/Hostname "Hostname") (or if homehost is set to `any`) the link will be `/dev/md/*name*`, if the hostname does not match the link be `/dev/md/*homehost*:*name*`.

The following example shows building a 2-device RAID1 array:

```
# mdadm --create --verbose --level=1 --metadata=1.2 --raid-devices=2 /dev/md/MyRAID1Array /dev/sdb1 /dev/sdc1

```

The following example shows building a RAID5 array with 4 active devices and 1 spare device:

```
# mdadm --create --verbose --level=5 --metadata=1.2 --chunk=256 --raid-devices=4 /dev/md/MyRAID5Array /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 --spare-devices=1 /dev/sdf1

```

**Tip:** `--chunk` is used to change the chunk size from the default value. See [Chunks: the hidden key to RAID performance](http://www.zdnet.com/article/chunks-the-hidden-key-to-raid-performance/) for more on chunk size optimisation.

The following example shows building a RAID10,far2 array with 2 devices:

```
# mdadm --create --verbose --level=10 --metadata=1.2 --chunk=512 --raid-devices=2 --layout=f2 /dev/md/MyRAID10Array /dev/sdb1 /dev/sdc1

```

The array is created under the virtual device `/dev/mdX`, assembled and ready to use (in degraded mode). One can directly start using it while mdadm resyncs the array in the background. It can take a long time to restore parity. Check the progress with:

```
$ cat /proc/mdstat

```

### Update configuration file

By default, most of `mdadm.conf` is commented out, and it contains just the following:

 `/etc/mdadm.conf` 
```
...
DEVICE partitions
...

```

This directive tells mdadm to examine the devices referenced by `/proc/partitions` and assemble as many arrays as possible. This is fine if you really do want to start all available arrays and are confident that no unexpected superblocks will be found (such as after installing a new storage device). A more precise approach is to explicitly add the arrays to `/etc/mdadm.conf`:

```
# mdadm --detail --scan >> /etc/mdadm.conf

```

This results in something like the following:

 `/etc/mdadm.conf` 
```
...
DEVICE partitions
...
ARRAY /dev/md/MyRAID1Array metadata=1.2 name=pine:MyRAID1Array UUID=27664f0d:111e493d:4d810213:9f291abe
```

This also causes mdadm to examine the devices referenced by `/proc/partitions`. However, only devices that have superblocks with a UUID of `27664…` are assembled in to active arrays.

See [mdadm.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mdadm.conf.5) for more information.

### Assemble the array

Once the configuration file has been updated the array can be assembled using mdadm:

```
# mdadm --assemble --scan

```

### Format the RAID filesystem

The array can now be formatted with a [file system](/index.php/File_system "File system") like any other partition, just keep in mind that:

*   Due to the large volume size not all filesystems are suited (see: [Wikipedia:Comparison of file systems#Limits](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Limits "wikipedia:Comparison of file systems")).
*   The filesystem should support growing and shrinking while online (see: [Wikipedia:Comparison of file systems#Features](https://en.wikipedia.org/wiki/Comparison_of_file_systems#Features "wikipedia:Comparison of file systems")).
*   One should calculate the correct stride and stripe-width for optimal performance.

#### Calculating the stride and stripe width

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

 `# mdadm --detail /dev/md0 | grep 'Chunk Size'` 
```
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

If your RAID 1 that is missing a disk array was wrongly auto-detected as RAID 1 (as per `mdadm --detail /dev/md<number>`) and reported as inactive (as per `cat /proc/mdstat`), stop the array first:

```
# mdadm --stop /dev/md<number>

```

## Installing Arch Linux on RAID

**Note:** The following section is applicable only if the root filesystem resides on the array. Users may skip this section if the array holds a data partition(s).

You should create the RAID array between the [Partitioning](/index.php/Partitioning "Partitioning") and [formatting](/index.php/File_systems#Create_a_file_system "File systems") steps of the Installation Procedure. Instead of directly formatting a partition to be your root file system, it will be created on a RAID array. Follow the section [#Installation](#Installation) to create the RAID array. Then continue with the installation procedure until the pacstrap step is completed. When using [UEFI boot](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), also read [EFI System Partition#ESP on RAID](/index.php/EFI_System_Partition#ESP_on_RAID "EFI System Partition").

### Update configuration file

**Note:** This should be done outside of the chroot, hence the prefix `/mnt` to the filepath.

After the base system is installed the default configuration file, `mdadm.conf`, must be updated like so:

```
# mdadm --detail --scan >> /mnt/etc/mdadm.conf

```

Always check the `mdadm.conf` configuration file using a text editor after running this command to ensure that its contents look reasonable.

**Note:** To prevent failure of `mdmonitor.service` at boot (enabled by default), you will need to uncomment `MAILADDR` and provide an e-mail address and/or application to handle notification of problems with your array at the bottom of `mdadm.conf`. See [#Mailing on events](#Mailing_on_events).

Continue with the installation procedure until you reach the step [Installation guide#Initramfs](/index.php/Installation_guide#Initramfs "Installation guide"), then follow the next section.

### Configure mkinitcpio

**Note:** This should be done whilst chrooted.

Add `mdadm_udev` to the [HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") section of the `mkinitcpio.conf` to add support for mdadm into the initramfs image:

 `/etc/mkinitcpio.conf` 
```
...
 HOOKS=(base udev autodetect keyboard modconf block **mdadm_udev** filesystems fsck)
...
```

If you use the `mdadm_udev` hook with a FakeRAID array, it is recommended to include *mdmon* in the [BINARIES](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") array:

 `/etc/mkinitcpio.conf` 
```
...
BINARIES=(**mdmon**)
...
```

Then [Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

See also [mkinitcpio#Using RAID](/index.php/Mkinitcpio#Using_RAID "Mkinitcpio").

### Configure the boot loader

Point the `root` parameter to the mapped device. E.g.:

```
root=/dev/md/*MyRAIDArray*

```

If booting from a software raid partition fails using the kernel device node method above, an alternative way is to use one of the methods from [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), for example:

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

#### General notes on scrubbing

**Note:** Users may alternatively echo **repair** to `/sys/block/md0/md/sync_action` but this is ill-advised since if a mismatch in the data is encountered, it would be automatically updated to be consistent. The danger is that we really do not know whether it is the parity or the data block that is correct (or which data block in case of RAID1). It is luck-of-the-draw whether or not the operation gets the right data instead of the bad data.

It is a good idea to set up a cron job as root to schedule a periodic scrub. See [raid-check](https://aur.archlinux.org/packages/raid-check/) which can assist with this. To perform a periodic scrub using systemd timers instead of cron, See [raid-check-systemd](https://aur.archlinux.org/packages/raid-check-systemd/) which contains the same script along with associated systemd timer unit files.

**Note:** For typical platter drives, scrubbing can take approximately **six seconds per gigabyte** (that is one hour forty-five minutes per terabyte) so plan the start of your cron job or timer appropriately.

#### RAID1 and RAID10 notes on scrubbing

Due to the fact that RAID1 and RAID10 writes in the kernel are unbuffered, an array can have non-0 mismatch counts even when the array is healthy. These non-0 counts will only exist in transient data areas where they do not pose a problem. However, we cannot tell the difference between a non-0 count that is just in transient data or a non-0 count that signifies a real problem. This fact is a source of false positives for RAID1 and RAID10 arrays. It is however still recommended to scrub regularly in order to catch and correct any bad sectors that might be present in the devices.

### Removing devices from an array

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

**Warning:**

*   Do not issue this command on linear or RAID0 arrays or data loss will occur!
*   Reusing the removed disk without zeroing the superblock will cause loss of all data on the next boot. (After mdadm will try to use it as the part of the raid array).

Stop using an array:

1.  Umount target array
2.  Stop the array with: `mdadm --stop /dev/md0`
3.  Repeat the three command described in the beginning of this section on each device.
4.  Remove the corresponding line from `/etc/mdadm.conf`.

### Adding a new device to an array

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

This is because the above commands will add the new disk as a "spare" but RAID0 does not have spares. If you want to add a device to a RAID0 array, you need to "grow" and "add" in the same command. This is demonstrated below:

```
# mdadm --grow /dev/md0 --raid-devices=3 --add /dev/sdc1

```

### Increasing size of a RAID volume

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
# awk '/^md/ {printf "%s: ", $1}; /blocks/ {print $NF}' </proc/mdstat

```

```
md1: [UU]
md0: [UU]

```

### Watch mdstat

```
# watch -t 'cat /proc/mdstat'

```

Or preferably using [tmux](https://www.archlinux.org/packages/?name=tmux)

```
# tmux split-window -l 12 "watch -t 'cat /proc/mdstat'"

```

### Track IO with iotop

The [iotop](https://www.archlinux.org/packages/?name=iotop) package displays the input/output stats for processes. Use this command to view the IO for raid threads.

```
# iotop -a -p $(sed 's, , -p ,g' <<<`pgrep "_raid|_resync|jbd2"`)

```

### Track IO with iostat

The *iostat* utility from [sysstat](https://www.archlinux.org/packages/?name=sysstat) package displays the input/output statistics for devices and partitions.

```
# iostat -dmy 1 /dev/md0
# iostat -dmy 1 # all

```

### Mailing on events

A smtp mail server (sendmail) or at least an email forwarder (ssmtp/msmtp) is required to accomplish this. Perhaps the most simplistic solution is to use [dma](https://aur.archlinux.org/packages/dma/) which is very tiny (installs to 0.08 MiB) and requires no setup.

Edit `/etc/mdadm.conf` defining the email address to which notifications will be received.

**Note:** If using dma as mentioned above, users may simply mail directly to the username on the localhost rather than to an external email address.

To test the configuration:

```
# mdadm --monitor --scan --oneshot --test

```

mdadm includes `mdmonitor.service` to perform the monitoring task, so at this point, you have nothing left to do. If you do not set a mail address in `/etc/mdadm.conf`, that service will fail. If you do not want to receive mail on mdadm events, the failure can be ignored; if you do not want notifications and are sensitive about failure messages, you can [mask](/index.php/Mask "Mask") the unit.

#### Alternative method

To avoid the installation of a smtp mail server or an email forwarder you can use the [S-nail](/index.php/S-nail "S-nail") tool (do not forget to setup) already on your system.

Create a file named `/etc/mdadm_warning.sh`:

 `/etc/mdadm_warning.sh` 
```
 /usr/bin/mailx -s "$event on $device" **destination@email.com**

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

Is does not necessarily mean that a drive is broken. You often find panic links on the web which go for the worst. In a word, No Panic. Maybe you just changed APIC or ACPI settings within your BIOS or Kernel parameters somehow. Change them back and you should be fine. Ordinarily, turning ACPI and/orACPI off should help.

### Start arrays read-only

When an md array is started, the superblock will be written, and resync may begin. To start read-only set the kernel module `md_mod` parameter `start_ro`. When this is set, new arrays get an 'auto-ro' mode, which disables all internal io (superblock updates, resync, recovery) and is automatically switched to 'rw' when the first write request arrives.

**Note:** The array can be set to true 'ro' mode using `mdadm --readonly` before the first write request, or resync can be started without a write using `mdadm --readwrite`.

To set the parameter at boot, add `md_mod.start_ro=1` to your kernel line.

Or set it at module load time from `/etc/modprobe.d/` file or from directly from `/sys/`:

```
# echo 1 > /sys/module/md_mod/parameters/start_ro

```

### Recovering from a broken or missing drive in the raid

You might get the above mentioned error also when one of the drives breaks for whatever reason. In that case you will have to force the raid to still turn on even with one disk short. Type this (change where needed):

```
# mdadm --manage /dev/md0 --run

```

Now you should be able to mount it again with something like this (if you had it in fstab):

```
# mount /dev/md0

```

Now the raid should be working again and available to use, however with one disk short! So, to add that one disc partition it the way like described above in [#Prepare the devices](#Prepare_the_devices). Once that is done you can add the new disk to the raid by doing:

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
*   [Wikipedia:Non-RAID drive architectures](https://en.wikipedia.org/wiki/Non-RAID_drive_architectures "wikipedia:Non-RAID drive architectures")

**mdadm**

*   [Debian mdadm FAQ](http://anonscm.debian.org/gitweb/?p=pkg-mdadm/mdadm.git;a=blob_plain;f=debian/FAQ;hb=HEAD)
*   [mdadm source code](http://www.kernel.org/pub/linux/utils/raid/mdadm/)
*   [Software RAID on Linux with mdadm](http://www.linux-mag.com/id/7939/) in Linux Magazine
*   [Wikipedia - mdadm](https://en.wikipedia.org/wiki/mdadm "wikipedia:mdadm")

**Forum threads**

*   [Raid Performance Improvements with bitmaps](http://forums.overclockers.com.au/showthread.php?t=865333)
*   [GRUB and GRUB2](https://bbs.archlinux.org/viewtopic.php?id=125445)
*   [Can't install grub2 on software RAID](https://bbs.archlinux.org/viewtopic.php?id=123698)
*   [Use RAID metadata 1.2 in boot and root partition](http://forums.gentoo.org/viewtopic-t-888624-start-0.html)

**RAID with encryption**

*   [Linux/Fedora: Encrypt /home and swap over RAID with dm-crypt](http://www.shimari.com/dm-crypt-on-raid/) by Justin Wells