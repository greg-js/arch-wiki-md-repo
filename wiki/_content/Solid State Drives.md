# Solid State Drives

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Benchmarking/Data storage devices](/index.php/Benchmarking/Data_storage_devices "Benchmarking/Data storage devices")
*   [Solid State Drives/NVMe](/index.php/Solid_State_Drives/NVMe "Solid State Drives/NVMe")
*   [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing")
*   [profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")

Solid State Drives (SSDs) are not PnP devices. Special considerations such as partition alignment, choice of file system, TRIM support, etc. are needed to set up SSDs for optimal performance. This article attempts to capture referenced, key learnings to enable users to get the most out of SSDs under Linux. Users are encouraged to read this article in its entirety before acting on recommendations.

**Note:** This article is targeted at users running Linux, but much of the content is also relevant to other operating systems like BSD, Mac OS X or Windows.

## Contents

*   [1 Overview](#Overview)
    *   [1.1 Advantages over HDDs](#Advantages_over_HDDs)
    *   [1.2 Limitations](#Limitations)
    *   [1.3 Pre-purchase considerations](#Pre-purchase_considerations)
*   [2 Choice of filesystem](#Choice_of_filesystem)
    *   [2.1 Btrfs](#Btrfs)
    *   [2.2 Ext4](#Ext4)
    *   [2.3 XFS](#XFS)
    *   [2.4 JFS](#JFS)
    *   [2.5 Other filesystems](#Other_filesystems)
*   [3 Tips for maximizing SSD performance](#Tips_for_maximizing_SSD_performance)
    *   [3.1 Partition alignment](#Partition_alignment)
    *   [3.2 TRIM](#TRIM)
        *   [3.2.1 Verify TRIM support](#Verify_TRIM_support)
        *   [3.2.2 Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim)
        *   [3.2.3 Enable continuous TRIM by mount flag](#Enable_continuous_TRIM_by_mount_flag)
        *   [3.2.4 Enable TRIM for LVM](#Enable_TRIM_for_LVM)
        *   [3.2.5 Enable TRIM for dm-crypt](#Enable_TRIM_for_dm-crypt)
    *   [3.3 I/O scheduler](#I.2FO_scheduler)
    *   [3.4 Swap space on SSDs](#Swap_space_on_SSDs)
*   [4 Tips for SSD security](#Tips_for_SSD_security)
    *   [4.1 Hdparm shows "frozen" state](#Hdparm_shows_.22frozen.22_state)
    *   [4.2 SSD memory cell clearing](#SSD_memory_cell_clearing)
*   [5 Tips for minimizing disk reads/writes](#Tips_for_minimizing_disk_reads.2Fwrites)
    *   [5.1 Intelligent partition scheme](#Intelligent_partition_scheme)
    *   [5.2 noatime mount option](#noatime_mount_option)
    *   [5.3 Locate frequently used files to RAM](#Locate_frequently_used_files_to_RAM)
        *   [5.3.1 Browser profiles](#Browser_profiles)
        *   [5.3.2 Others](#Others)
    *   [5.4 Compiling in tmpfs](#Compiling_in_tmpfs)
    *   [5.5 Disabling journaling on the filesystem](#Disabling_journaling_on_the_filesystem)
*   [6 Firmware updates](#Firmware_updates)
    *   [6.1 ADATA](#ADATA)
    *   [6.2 Crucial](#Crucial)
    *   [6.3 Intel](#Intel)
    *   [6.4 Kingston](#Kingston)
    *   [6.5 Mushkin](#Mushkin)
    *   [6.6 OCZ](#OCZ)
    *   [6.7 Samsung](#Samsung)
    *   [6.8 SanDisk](#SanDisk)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Resolving NCQ errors](#Resolving_NCQ_errors)
    *   [7.2 Resolving SATA power management related errors](#Resolving_SATA_power_management_related_errors)
*   [8 See also](#See_also)

## Overview

### Advantages over HDDs

*   Fast read speeds - 2-3x faster than modern desktop HDDs (7,200 RPM using SATA2 interface).
*   Sustained read speeds - no decrease in read speed across the entirety of the device. HDD performance tapers off as the drive heads move from the outer edges to the center of HDD platters.
*   Minimal access time - approximately 100x faster than an HDD. For example, 0.1 ms (100 us) vs. 12-20 ms (12,000-20,000 us) for desktop HDDs.
*   High degree of reliability.
*   No moving parts.
*   Minimal heat production.
*   Minimal power consumption - fractions of a W at idle and 1-2 W while reading/writing vs. 10-30 W for a HDD depending on RPMs.
*   Light-weight - ideal for laptops.

### Limitations

*   Per-storage cost (about a third of a dollar per GB, vs. around a dime or two per GB for rotating media).
*   Capacity of marketed models is lower than that of HDDs.
*   Large cells require different filesystem optimizations than rotating media. The flash translation layer hides the raw flash access which a modern OS could use to optimize access.
*   Partitions and filesystems need some SSD-specific tuning. Page size and erase page size are not autodetected.
*   Cells wear out. Consumer MLC cells at mature 50nm processes can handle 10000 writes each; 35nm generally handles 5000 writes, and 25nm 3000 (smaller being higher density and cheaper). If writes are properly spread out, are not too small, and align well with cells, this translates into a lifetime write volume for the SSD that is a multiple of its capacity. Daily write volumes have to be balanced against life expectancy. However, tests [[1]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update)[[2]](http://techreport.com/review/26523/the-ssd-endurance-experiment-casualties-on-the-way-to-a-petabyte)[[3]](http://techreport.com/review/27436/the-ssd-endurance-experiment-two-freaking-petabytes)[[4]](http://techreport.com/review/27909/the-ssd-endurance-experiment-theyre-all-dead) performed on recent hardware suggest that SSD wear is negligible, with the lifetime expectancy of SSDs comparable to those of HDDs even with artificially high write-volumes.
*   Firmwares and controllers are complex. They occasionally have bugs. Modern ones consume power comparable with HDDs. They [implement](https://lwn.net/Articles/353411/) the equivalent of a log-structured filesystem with garbage collection. They translate SATA commands traditionally intended for rotating media. Some of them do on the fly compression. They spread out repeated writes across the entire area of the flash, to prevent wearing out some cells prematurely. They also coalesce writes together so that small writes are not amplified into as many erase cycles of large cells. Finally they move cells containing data so that the cell does not lose its contents over time.
*   Performance can drop as the disk gets filled. Garbage collection is not universally well implemented, meaning freed space is not always collected into entirely free cells.

### Pre-purchase considerations

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Would be nice to get some sources here, particularly on the "75% occupancy" (Discuss in [Talk:Solid State Drives#](https://wiki.archlinux.org/index.php/Talk:Solid_State_Drives))

There are several key features to look for prior to purchasing a contemporary SSD.

*   Native [TRIM](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") support is a vital feature that both prolongs SSD lifetime and reduces loss of performance for write operations over time.
*   Buying the right sized SSD is key. As with all filesystems, target <75 % occupancy for all SSD partitions to ensure efficient use by the kernel.

## Choice of filesystem

This section describes optimized [filesystems](/index.php/Filesystems "Filesystems") to use on a SSD.

It's still possible/required to use other filesystems, e.g. FAT32 for the [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI").

### Btrfs

[Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") support has been included with the mainline 2.6.29 release of the Linux kernel. Some feel that it is not mature enough for production use while there are also early adopters of this potential successor to ext4\. Users are encouraged to read the [Btrfs](/index.php/Btrfs "Btrfs") article for more info.

### Ext4

[Ext4](https://en.wikipedia.org/wiki/Ext4 "wikipedia:Ext4") is another filesystem that has support for SSD. It is considered as stable since 2.6.28 and is mature enough for daily use. ext4 users can enable the TRIM command support using the `discard` mount option in [fstab](/index.php/Fstab "Fstab") (or with `tune2fs -o discard /dev/sdaX`). See the [official in kernel tree documentation](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/filesystems/ext4.txt) for further information on ext4.

### XFS

Many users do not realize that in addition to ext4 and btrfs, [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") has TRIM support as well. This can be enabled in the usual ways. That is, the choice may be made of either using the discard option mentioned above, or by using the fstrim command. More information can be found on the [XFS wiki](http://xfs.org/index.php/FITRIM/discard).

### JFS

As of Linux kernel version 3.7, proper TRIM support has been added. So far, there is not a great wealth of information of the topic but it has certainly been picked up by [Linux news sites.](http://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY) It is apparent that it can be enabled via the `discard` mount option, or by using the method of batch TRIMs with fstrim.

### Other filesystems

There are other filesystems specifically [designed for SSD](https://en.wikipedia.org/wiki/List_of_flash_file_systems#File_systems_optimized_for_flash_memory.2C_solid_state_media "wikipedia:List of flash file systems"), for example [F2FS](/index.php/F2FS "F2FS").

## Tips for maximizing SSD performance

### Partition alignment

See [Partitioning#Partition alignment](/index.php/Partitioning#Partition_alignment "Partitioning").

### TRIM

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Mention which options apply to which filesystems. (Discuss in [Talk:Solid State Drives#](https://wiki.archlinux.org/index.php/Talk:Solid_State_Drives))

Most SSDs support the [ATA_TRIM command](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") for sustained long-term performance and wear-leveling. For more including some before and after benchmark, see [this](https://sites.google.com/site/lightrush/random-1/howtoconfigureext4toenabletrimforssdsonubuntu) tutorial.

As of Linux kernel version 3.8 onwards, the following filesystems support TRIM: [Ext4](/index.php/Ext4 "Ext4"), [Btrfs](/index.php/Btrfs "Btrfs"), [JFS](/index.php/JFS "JFS"), VFAT, [XFS](/index.php/XFS "XFS"), [F2FS](/index.php/F2FS "F2FS").

As of [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) version 2015.3.14, TRIM is supported for [NTFS](/index.php/NTFS "NTFS") filesystem too [[5]](http://permalink.gmane.org/gmane.comp.file-systems.ntfs-3g.devel/1101).

VFAT only supports TRIM by the mount option `discard`, not manually with _fstrim_.

The [Choice of Filesystem](#Choice_of_filesystem) section of this article offers more details.

#### Verify TRIM support

```
# hdparm -I /dev/sda | grep TRIM
        *    Data Set Management TRIM supported (limit 1 block)

```

Note that there are different types of TRIM support defined by the specification. Hence, the output may differ depending what the drive supports. See [wikipedia:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "wikipedia:TRIM") for more information.

#### Apply periodic TRIM via fstrim

**Note:** This method does not work for VFAT filesystems.

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package (part of [base](https://www.archlinux.org/groups/x86_64/base/) and [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)) provides `fstrim.service` and `fstrim.timer` [systemd](/index.php/Systemd "Systemd") unit files. [Enabling](/index.php/Enabling "Enabling") the timer will activate the service weekly, which will then trim all mounted filesystems on devices that support the discard operation.

The timer relies on the timestamp of `/var/lib/systemd/timers/stamp-fstrim.timer` (which it will create upon first invocation) to know whether a week has elapsed since it last ran. Therefore there is no need to worry about too frequent invocations, in an _anacron_-like fashion.

It is also possible to query the units activity and status using standard `journalctl` and `systemctl status` commands:

```
# journalctl -u fstrim
...
<shows several log entries if enabled>
...
# systemctl status fstrim
● fstrim.service - Discard unused blocks
   Loaded: loaded (/usr/lib/systemd/system/fstrim.service; static; vendor preset: disabled)
   Active: inactive (dead) since lun. 2015-06-08 00:00:18 CEST; 2 days ago
  Process: 18152 ExecStart=/sbin/fstrim -a (code=exited, status=0/SUCCESS)
 Main PID: 18152 (code=exited, status=0/SUCCESS)

juin 08 00:00:16 arch-clevo systemd[1]: Starting Discard unused blocks...
juin 08 00:00:18 arch-clevo systemd[1]: Started Discard unused blocks.
```

**Note:** Specify the `.timer` suffix if you specifically want to inquire about it.

If you wish to change the periodicity of the timer or the command run, simply [edit the provided unit files](/index.php/Systemd#Editing_provided_units "Systemd").

#### Enable continuous TRIM by mount flag

**Warning:** Users need to be certain that their SSD supports TRIM before attempting to mount a partition with the `discard` flag. Data loss can occur otherwise! Unfortunately, there are wide quality gaps of SSD's bios' to perform continuous TRIM, which is also why using the `discard` mount flag is [recommended against](http://thread.gmane.org/gmane.comp.file-systems.ext4/41974) generally by filesystem developer Theodore Ts'o. If in doubt about your hardware, [#Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim) instead. Also be aware of other [shortcomings](https://en.wikipedia.org/wiki/Trim_(computing)#Shortcomings "wikipedia:Trim (computing)"), most importantly that "TRIM commands [have been linked](https://blog.algolia.com/when-solid-state-drives-are-not-that-solid/) to serious data corruption in several devices, most notably Samsung 8* series." After the data corruption [had been confirmed](https://github.com/torvalds/linux/blob/e64f638483a21105c7ce330d543fa1f1c35b5bc7/drivers/ata/libata-core.c#L4109-L4286), the Linux kernel blacklisted queued TRIM command execution for a number of [popular devices](https://github.com/torvalds/linux/blob/e64f638483a21105c7ce330d543fa1f1c35b5bc7/drivers/ata/libata-core.c#L4227) as of July 1, 2015\. Read [Samsung Finds, Fixes Bug In Linux Trim Code](http://linux.slashdot.org/story/15/07/30/1814200/samsung-finds-fixes-bug-in-linux-trim-code) on Slashdot for more recent updates.

Using the `discard` option for a mount in `/etc/fstab` enables continuous TRIM in device operations:

```
/dev/sda2  /boot       ext4  defaults,noatime,**discard**   0  2
/dev/sda1  /boot/efi   vfat  defaults,noatime,**discard**   0  2
/dev/sda3  /           ext4  defaults,noatime,**discard**   0  2

```

The main benefit of continuous TRIM is speed; an SSD can perform more efficient [garbage collection](http://arstechnica.com/gadgets/2015/04/ask-ars-my-ssd-does-garbage-collection-so-i-dont-need-trim-right/). However, results vary and particularly earlier SSD generations may also show just the opposite effect. Also for this reason, some distributions decided against using it (e.g. Ubuntu: see [this article](http://www.phoronix.com/scan.php?page=news_item&px=MTUxOTY) and the [related blueprint](https://blueprints.launchpad.net/ubuntu/+spec/core-1311-ssd-trimming)).

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** 1) `mount(8)` indicates that ext3 does not support the `discard` option, which would explain any errors trying to use it. 2) Synchronous TRIM commands before SATA 3.1 are hardware property, so how can software adjustments make a difference? (Discuss in [Talk:Solid State Drives#](https://wiki.archlinux.org/index.php/Talk:Solid_State_Drives))

**Note:**

*   There is no need for the `discard` flag if you run `fstrim` periodically.
*   Using the `discard` flag for an ext3 root partition will result in it being mounted read-only.
*   Before SATA 3.1, TRIM commands are synchronous and will block all I/O while running. This may cause short freezes while this happens, for example during a filesystem sync. You may not want to use `discard` in that case but [#Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim) instead. One way to check your SATA version is with `smartctl --info /dev/sd_X_`.

On the ext4 filesystem, the `discard` flag can also be set as a [default mount option](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") using _tune2fs_:

```
# tune2fs -o discard /dev/sd**XY**

```

Using the default mount options instead of an entry in `/etc/fstab` is useful for external drives, because such partition will be mounted with the default options also on other machines. There is no need to edit `/etc/fstab` on every machine.

**Note:** The default mount options are not listed in `/proc/mounts`.

#### Enable TRIM for LVM

Change the value of `issue_discards` option from 0 to 1 in `/etc/lvm/lvm.conf`.

**Note:** Enabling this option will "issue discards to a logical volumes's underlying physical volume(s) when the logical volume is no longer using the physical volumes' space (e.g. lvremove, lvreduce, etc)" (see `man lvm.conf` and/or inline comments in `/etc/lvm/lvm.conf`). As such it does not seem to be required for "regular" TRIM requests (file deletions inside a filesystem) to be functional.

#### Enable TRIM for dm-crypt

**Warning:** The discard option allows discard requests to be passed through the encrypted block device. This improves performance on SSD storage but has security implications. See [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") for more information.

For non-root filesystems, configure `/etc/crypttab` to include `discard` in the list of options for encrypted block devices located on a SSD (see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")).

For the root filesystem, follow the instructions from [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") to add the right kernel parameter to the bootloader configuration.

### I/O scheduler

See [Maximizing performance#Tuning IO schedulers](/index.php/Maximizing_performance#Tuning_IO_schedulers "Maximizing performance").

### Swap space on SSDs

One can place a swap partition on an SSD. A recommended tweak for SSDs using a swap partition is to reduce the [swappiness](/index.php/Swappiness "Swappiness") of the system to some very low value (for example `1`), and thus avoiding writes to swap.

## Tips for SSD security

### Hdparm shows "frozen" state

Some motherboard BIOS' issue a "security freeze" command to attached storage devices on initialization. Likewise some SSD (and HDD) BIOS' are set to "security freeze" in the factory already. Both result in the device's password security settings to be set to **frozen**, as shown in below output:

 `:~# hdparm -I /dev/sda` 

```
Security: 
 	Master password revision code = 65534
 		supported
 	not	enabled
 	**not	locked**
 		**frozen**
 	not	expired: security count
 		supported: enhanced erase
 	4min for SECURITY ERASE UNIT. 2min for ENHANCED SECURITY ERASE UNIT.
```

Operations like formatting the device or installing operating systems are not affected by the "security freeze".

The above output shows the device is **not locked** by a HDD-password on boot and the **frozen** state safeguards the device against malwares which may try to lock it by setting a password to it at runtime.

If you intend to set a password to a "frozen" device yourself, a motherboard BIOS with support for it is required. A lot of notebooks have support, because it is required for [hardware encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption"), but support may not be trivial for a desktop/server board. For the Intel DH67CL/BL motherboard, for example, the motherboard has to be set to "maintenance mode" by a physical jumper to access the settings (see [[6]](http://sstahlman.blogspot.in/2014/07/hardware-fde-with-intel-ssd-330-on.html?showComment=1411193181867#c4579383928221016762), [[7]](https://communities.intel.com/message/251978#251978)).

**Warning:** Do not try to change the above **lock** security settings with `hdparm` unless you know exactly what you are doing.

If you intend to erase the SSD, see [Securely wipe disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk") and [below](#SSD_memory_cell_clearing).

### SSD memory cell clearing

On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were at the time the device was installed thus restoring it to its [factory default write performance](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

The reset is easily accomplished in a three step procedure denoted on the [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") wiki article. If the reason for the reset is to wipe data, you may not want to rely on the SSD bios to perform it securely. See [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk") for further information and examples to perform a wipe.

## Tips for minimizing disk reads/writes

An overarching theme for SSD usage should be 'simplicity' in terms of locating high-read/write operations either in RAM (Random Access Memory) or on a physical HDD rather than on an SSD. Doing so will add longevity to an SSD. This is primarily due to the large erase block size (512 KiB in some cases); a lot of small writes result in huge effective writes.

**Note:** A 32GB SSD with a mediocre 10x write amplification factor, a standard 10000 write/erase cycle, and **10GB of data written per day**, would get an **8 years life expectancy**. It gets better with bigger SSDs and modern controllers with less write amplification. Also compare [[8]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update) when considering whether any particular strategy to limit disk writes is actually needed.

Use [iotop](https://www.archlinux.org/packages/?name=iotop) and sort by disk writes to see how much and how frequently are programs writing to the disk.

**Tip:** _iotop_ can be run in batch mode instead of the default interactive mode using the `-b` option. `-o` is used to show only processes actually doing I/O, and `-qqq` is to suppress column names and I/O summary. See `man iotop` for more options.

```
# iotop -boqqq

```

### Intelligent partition scheme

*   For systems with both an SSD and an HDD, consider relocating the `/var` partition to a magnetic disc on the system rather than on the SSD itself to avoid read/write wear.

### noatime mount option

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [fstab#atime options](/index.php/Fstab#atime_options "Fstab").**

**Notes:** This should be described only in one place, just link to [fstab](/index.php/Fstab "Fstab") afterwards. (Discuss in [Talk:Solid State Drives#](https://wiki.archlinux.org/index.php/Talk:Solid_State_Drives))

Using this flag in one's `/etc/fstab` halts the logging of read accesses to the file system via an update to the atime information associated with the file. The importance of the `noatime` setting is that it eliminates the need by the system to make writes to the file system for files which are simply being read. Since writes can be somewhat expensive as mentioned in previous section, this can result in measurable performance gains.

**Note:** The write time information to a file will continue to be updated anytime the file is written to with this option enabled.

```
/dev/sda1  /       ext4   defaults,**noatime**   0  1
/dev/sda2  /home   ext4   defaults,**noatime**   0  2

```

**Note:** This setting will cause issues with some programs such as [Mutt](/index.php/Mutt "Mutt"), as the access time of the file will eventually be previous than the modification time, which would make no sense. Using the `relatime` option instead of `noatime` will ensure that the atime field will never be prior to the last modification time of a file. Alternatively, using the maildir storage format also solves this mutt issue.

### Locate frequently used files to RAM

#### Browser profiles

One can _easily_ mount browser profile(s) such as chromium, firefox, opera, etc. into RAM via tmpfs and also use rsync to keep them synced with HDD-based backups. In addition to the obvious speed enhancements, users will also save read/write cycles on their SSD by doing so.

The AUR contains several packages to automate this process, for example [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/)<sup><small>AUR</small></sup>.

#### Others

For the same reasons a browser's profile can be relocated to RAM, so can highly used directories such as `/srv/http` (if running a web server). A sister project to [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/)<sup><small>AUR</small></sup> is [anything-sync-daemon](https://aur.archlinux.org/packages/anything-sync-daemon/)<sup><small>AUR</small></sup>, which allows users to define **any** directory to sync to RAM using the same underlying logic and safe guards.

### Compiling in tmpfs

Intentionally compiling in [tmpfs](/index.php/Tmpfs "Tmpfs") is great to minimize disk reads/writes. For more information, refer to [Makepkg#Improving compile times](/index.php/Makepkg#Improving_compile_times "Makepkg").

### Disabling journaling on the filesystem

Using a journaling filesystem such as ext4 on an SSD **without** a journal is an option to decrease read/writes. The obvious drawback of using a filesystem with journaling disabled is data loss as a result of an ungraceful dismount (i.e. post power failure, kernel lockup, etc.). With modern SSDs, [Ted Tso](http://tytso.livejournal.com/61830.html) advocates that journaling can be enabled with minimal extraneous read/write cycles under most circumstances:

**Amount of data written (in megabytes) on an ext4 file system mounted with `noatime`.**

<table class="wikitable">

<tbody>

<tr>

<th>operation</th>

<th>journal</th>

<th>w/o journal</th>

<th>percent change</th>

</tr>

<tr>

<th>git clone</th>

<td>367.0</td>

<td>353.0</td>

<td>3.81 %</td>

</tr>

<tr>

<th>make</th>

<td>207.6</td>

<td>199.4</td>

<td>3.95 %</td>

</tr>

<tr>

<th>make clean</th>

<td>6.45</td>

<td>3.73</td>

<td>42.17 %</td>

</tr>

</tbody>

</table>

_"What the results show is that metadata-heavy workloads, such as make clean, do result in almost twice the amount data written to disk. This is to be expected, since all changes to metadata blocks are first written to the journal and the journal transaction committed before the metadata is written to their final location on disk. However, for more common workloads where we are writing data as well as modifying filesystem metadata blocks, the difference is much smaller."_

**Note:** The make clean example from the table above typifies the importance of intentionally doing compiling in tmpfs as recommended in the [preceding section](#Compiling_in_tmpfs) of this article!

## Firmware updates

### ADATA

ADATA has a utility available for Linux (i686) on their support page [here](http://www.adata.com.tw/index.php?action=ss_main&page=ss_content_driver&lan=en). The link to latest firmware will appear after selecting the model. The latest Linux update utility is packed with firmware and needs to be run as root. One may need to set correct permissions for binary file first.

### Crucial

Crucial provides an option for updating the firmware with an ISO image. These images can be found after selecting the product [here](http://www.crucial.com/usa/en/support-ssd) and downloading the "Manual Boot File." Owners of an M4 Crucial model, may check if a firmware upgrade is needed with `smartctl`.

 `$ smartctl --all /dev/sd**X**` 

```
==> WARNING: This drive may hang after 5184 hours of power-on time:
[http://www.tomshardware.com/news/Crucial-m4-Firmware-BSOD,14544.html](http://www.tomshardware.com/news/Crucial-m4-Firmware-BSOD,14544.html)
See the following web pages for firmware updates:
[http://www.crucial.com/support/firmware.aspx](http://www.crucial.com/support/firmware.aspx)
[http://www.micron.com/products/solid-state-storage/client-ssd#software](http://www.micron.com/products/solid-state-storage/client-ssd#software)

```

Users seeing this warning are advised to backup all sensible data and **consider upgrading immediately**.

### Intel

Intel has a Linux live system based [Firmware Update Tool](https://downloadcenter.intel.com/download/18363) for operating systems that are not compatible with its [Intel® Solid-State Drive Toolbox](https://downloadcenter.intel.com/download/18455) software.

### Kingston

Kingston has a Linux utility to update the firmware of Sandforce controller based drives: [SSD support page](http://www.kingston.com/en/ssd). Click the images on the page to go to a support page for your SSD model. Support specifically for, e.g. the SH100S3 SSD, can be found here: [support page](http://www.kingston.com/en/support/technical/downloads?product=sh100s3&filename=sh100_503fw_win).

### Mushkin

The lesser known Mushkin brand Solid State drives also use Sandforce controllers, and have a Linux utility (nearly identical to Kingston's) to update the firmware.

### OCZ

OCZ has a command line utility available for Linux (i686 and x86_64) on their forum [here](http://www.ocztechnology.com/ssd_tools/).

### Samsung

Samsung notes that update methods other than using their Magician Software are "not supported," but it is possible. The Magician Software can be used to make a USB drive bootable with the firmware update. Samsung provides pre-made [bootable ISO images](http://www.samsung.com/global/business/semiconductor/samsungssd/downloads.html) that can be used to update the firmware. Another option is to use Samsung's [samsung_magician](https://aur.archlinux.org/packages/samsung_magician/)<sup><small>AUR</small></sup>, which is available in the AUR. Magician only supports Samsung-branded SSDs; those manufactured by Samsung for OEMs (e.g., Lenovo) are not supported.

**Note:** Samsung does not make it obvious at all that they actually provide these. They seem to have 4 different firmware update pages, and each references different ways of doing things.

Users preferring to run the firmware update from a live USB created under Linux (without using Samsung's "Magician" software under Microsoft Windows) can refer to [this post](http://fomori.org/blog/?p=933) for reference.

### SanDisk

SanDisk makes **ISO firmware images** to allow SSD firmware update on operating systems that are unsupported by their SanDisk SSD Toolkit. One must choose the firmware for the right _SSD model_, as well as for the _capacity_ that it has (e.g. 60GB, **or** 256GB). After burning the adequate ISO firmware image, simply restart the PC to boot with the newly created CD/DVD boot disk (may work from a USB stick).

The iso images just contain a linux kernel and an initrd. Extract them to `/boot` partition and boot them with [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux") to update the firmware.

I could not find a single page listing the firmware updates yet (site is a mess IMHO), but here are some relevant links:

SanDisk Extreme SSD [Firmware Release notes](http://kb.sandisk.com/app/answers/detail/a_id/10127) and [Manual Firmware update version R211](http://kb.sandisk.com/app/answers/detail/a_id/10476)

SanDisk Ultra SSD [Firmware release notes](http://kb.sandisk.com/app/answers/detail/a_id/10192) and [Manual Firmware update version 365A13F0](http://kb.sandisk.com/app/answers/detail/a_id/10477)

## Troubleshooting

It is possible that the issue you are encountering is a firmware bug which is not Linux specific, so before trying to troubleshoot an issue affecting the SSD device, you should first check if updates are available for:

*   The [SSD's firmware](#Firmware_updates)
*   The [motherboard's BIOS/UEFI firmware](/index.php/Flashing_BIOS_from_Linux "Flashing BIOS from Linux")

Even if it is a firmware bug it might be possible to avoid it, so if there are no updates to the firmware or you hesitant on updating firmware then the following might help.

### Resolving NCQ errors

Some SSDs and SATA chipsets do not work properly with Linux Native Command Queueing (NCQ). The tell-tale dmesg errors look like this:

```
[ 9.115544] ata9: exception Emask 0x0 SAct 0xf SErr 0x0 action 0x10 frozen
[ 9.115550] ata9.00: failed command: READ FPDMA QUEUED
[ 9.115556] ata9.00: cmd 60/04:00:d4:82:85/00:00:1f:00:00/40 tag 0 ncq 2048 in
[ 9.115557] res 40/00:18:d3:82:85/00:00:1f:00:00/40 Emask 0x4 (timeout)

```

To disable NCQ on boot, add `libata.force=noncq` to the kernel command line in the [bootloader](/index.php/Bootloader "Bootloader") configuration. To disable NCQ only for disk 0 on port 1 use: `libata.force=1.00:noncq`

Alternatively, you may disable NCQ for a specific drive without rebooting via sysfs:

```
# echo 1 > /sys/block/sdX/device/queue_depth

```

If this (and also updating the firmware) does not resolves the problem or cause other issues, then [file a bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

### Resolving SATA power management related errors

Some SSDs (e.g. Transcend MTS400) are failing when SATA Active Link Power Management, [ALPM](https://en.wikipedia.org/wiki/Aggressive_Link_Power_Management "wikipedia:Aggressive Link Power Management"), is enabled. ALPM is disabled by default and enabled by a power saving daemon (e.g. [TLP](/index.php/TLP "TLP"), [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")).

If you starting to encounter SATA related errors when using such daemon then you should try to disable ALPM by setting its state to `max_performance` for both battery and AC powered profiles.

## See also

*   [Discussion on Reddit about installing Arch on an SSD](http://www.reddit.com/r/archlinux/comments/rkwjm/what_should_i_keep_in_mind_when_installing_on_ssd/)
*   See the [Flashcache](/index.php/Flashcache "Flashcache") article for advanced information on using solid-state with rotational drives for top performance.
*   [Speed Up Your SSD By Correctly Aligning Your Partitions](http://lifehacker.com/5837769/make-sure-your-partitions-are-correctly-aligned-for-optimal-solid-state-drive-performance) (using GParted)
*   [Re: Varying Leafsize and Nodesize in Btrfs](http://permalink.gmane.org/gmane.comp.file-systems.btrfs/19446)
*   [Re: SSD alignment and Btrfs sector size](http://thread.gmane.org/gmane.comp.file-systems.btrfs/19650/focus=19667)
*   [Erase Block (Alignment) Misinformation?](http://forums.anandtech.com/showthread.php?t=2266113)
*   [Is alignment to erase block size needed for modern SSD's?](http://superuser.com/questions/492084/is-alignment-to-erase-block-size-needed-for-modern-ssds)
*   [Btrfs support for efficient SSD operation (data blocks alignment)](http://thread.gmane.org/gmane.comp.file-systems.btrfs/15646)
*   [SSD, Erase Block Size & LVM: PV on raw device, Alignment](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Solid_State_Drives&oldid=416181](https://wiki.archlinux.org/index.php?title=Solid_State_Drives&oldid=416181)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Storage](/index.php/Category:Storage "Category:Storage")

Hidden categories:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")
*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")