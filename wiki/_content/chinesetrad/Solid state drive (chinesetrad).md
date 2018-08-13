相關文章

*   [SSD Benchmarking](/index.php/SSD_Benchmarking "SSD Benchmarking")
*   [SSD Memory Cell Clearing](/index.php/SSD_Memory_Cell_Clearing "SSD Memory Cell Clearing")
*   [profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")

## Contents

*   [1 概觀](#.E6.A6.82.E8.A7.80)
    *   [1.1 介紹](#.E4.BB.8B.E7.B4.B9)
    *   [1.2 和一般硬碟相比的優勢](#.E5.92.8C.E4.B8.80.E8.88.AC.E7.A1.AC.E7.A2.9F.E7.9B.B8.E6.AF.94.E7.9A.84.E5.84.AA.E5.8B.A2)
    *   [1.3 目前的限制](#.E7.9B.AE.E5.89.8D.E7.9A.84.E9.99.90.E5.88.B6)
    *   [1.4 購買前的注意事項](#.E8.B3.BC.E8.B2.B7.E5.89.8D.E7.9A.84.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A0.85)
        *   [1.4.1 參考連結](#.E5.8F.83.E8.80.83.E9.80.A3.E7.B5.90)
*   [2 Tips for Maximizing SSD Performance](#Tips_for_Maximizing_SSD_Performance)
    *   [2.1 Partition Alignment](#Partition_Alignment)
    *   [2.2 TRIM](#TRIM)
        *   [2.2.1 Verify TRIM Support](#Verify_TRIM_Support)
        *   [2.2.2 Enable TRIM by Mount Flags](#Enable_TRIM_by_Mount_Flags)
        *   [2.2.3 Apply TRIM via cron](#Apply_TRIM_via_cron)
        *   [2.2.4 Apply TRIM via a systemd service](#Apply_TRIM_via_a_systemd_service)
            *   [2.2.4.1 Enable TRIM for LVM](#Enable_TRIM_for_LVM)
        *   [2.2.5 Enable TRIM With mkfs.ext4 or tune2fs (Discouraged)](#Enable_TRIM_With_mkfs.ext4_or_tune2fs_.28Discouraged.29)
    *   [2.3 I/O Scheduler](#I.2FO_Scheduler)
        *   [2.3.1 Kernel parameter (for a single device)](#Kernel_parameter_.28for_a_single_device.29)
        *   [2.3.2 Using the sys virtual filesystem (for multiple devices)](#Using_the_sys_virtual_filesystem_.28for_multiple_devices.29)
        *   [2.3.3 Using udev for one device or HDD/SSD mixed environment](#Using_udev_for_one_device_or_HDD.2FSSD_mixed_environment)
    *   [2.4 Swap Space on SSDs](#Swap_Space_on_SSDs)
    *   [2.5 SSD Memory Cell Clearing](#SSD_Memory_Cell_Clearing)
*   [3 Tips for Minimizing SSD Read/Writes](#Tips_for_Minimizing_SSD_Read.2FWrites)
    *   [3.1 Intelligent Partition Scheme](#Intelligent_Partition_Scheme)
    *   [3.2 noatime Mount Flag](#noatime_Mount_Flag)
    *   [3.3 Locate High-Use Files to RAM](#Locate_High-Use_Files_to_RAM)
        *   [3.3.1 Browser Profiles](#Browser_Profiles)
        *   [3.3.2 Others](#Others)
    *   [3.4 Compiling in tmpfs](#Compiling_in_tmpfs)
    *   [3.5 Disabling Journaling on the filesystem](#Disabling_Journaling_on_the_filesystem)
*   [4 Choice of Filesystem](#Choice_of_Filesystem)
    *   [4.1 Btrfs](#Btrfs)
    *   [4.2 Ext4](#Ext4)
    *   [4.3 XFS](#XFS)
    *   [4.4 JFS](#JFS)
*   [5 Firmware Updates](#Firmware_Updates)
    *   [5.1 ADATA](#ADATA)
    *   [5.2 Crucial](#Crucial)
    *   [5.3 Kingston](#Kingston)
    *   [5.4 Mushkin](#Mushkin)
    *   [5.5 OCZ](#OCZ)
    *   [5.6 Samsung](#Samsung)
    *   [5.7 SanDisk](#SanDisk)
*   [6 See also](#See_also)

## 概觀

### 介紹

固態硬碟 (SSD) 並不是一個隨插即用的裝置。在使用 SSD 上我們要特別去考量 partition 的校準，選擇適合的檔案系統，以及是否支援 TRIM 等等。才能將效能最佳化。這篇文章儘量深入淺出來讓使用者學習，如何在 Linux 中設定 SSD。

**Note:** 雖然本篇文章主要的目標使用者是是使用 Linux 的族群，但是文中的內容一樣也是相容於使用其他作業系統的朋友們，像是 BSD, Mac OS X 或 Windows.

### 和一般硬碟相比的優勢

*   更快的讀取速度 - 比起現在最新的硬碟，還要快上 2-3 倍 (7,200 RPM 使用 SATA2 介面).
*   讀取速度連貫且持續 - 因為 SSD 沒有磁頭，所以不會因為要移動磁頭來讀取碟盤上的資料而導致速度慢在磁頭的移動上。
*   最小的 access time - 大約是硬碟的 100 倍快。舉例來說， 0.1 ms (100 us) vs. 12-20 ms (12,000-20,000 us) for desktop HDDs.
*   高度的可靠性。
*   沒有移動部件。
*   產出的熱能極小。
*   省電 - 在靜止的狀態時，不到 1 W，在讀寫狀態時則是 1-2 W，而硬碟則根據硬碟轉速需消耗 10-30 W。
*   輕巧 - 這對筆記型電腦來說很重要。

### 目前的限制

*   價格昂貴，大約是 1 GB 要 1 美金，而一般硬碟每 1 GB 大約是 0.1-0.2 美金。
*   一般市售得 SSD 的儲存容量，都小於一般硬碟。
*   Large cells require different filesystem optimizations than rotating media. The flash translation layer hides the raw flash access which a modern OS could use to optimize access.
*   Partitions and filesystems need some SSD-specific tuning. Page size and erase page size are not autodetected.
*   Cells wear out. Consumer MLC cells at mature 50nm processes can handle 10000 writes each; 35nm generally handles 5000 writes, and 25nm 3000 (smaller being higher density and cheaper). If writes are properly spread out, are not too small, and align well with cells, this translates into a lifetime write volume for the SSD that is a multiple of its capacity. Daily write volumes have to be balanced against life expectancy.
*   Firmwares and controllers are complex. They occasionally have bugs. Modern ones consume power comparable with HDDs. They [implement](https://lwn.net/Articles/353411/) the equivalent of a log-structured filesystem with garbage collection. They translate SATA commands traditionally intended for rotating media. Some of them do on the fly compression. They spread out repeated writes across the entire area of the flash, to prevent wearing out some cells prematurely. They also coalesce writes together so that small writes are not amplified into as many erase cycles of large cells. Finally they move cells containing data so that the cell does not lose its contents over time.
*   Performance can drop as the disk gets filled. Garbage collection is not universally well implemented, meaning freed space is not always collected into entirely free cells.

### 購買前的注意事項

There are several key features to look for prior to purchasing a contemporary SSD.

*   Native [TRIM](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") support is a vital feature that both prolongs SSD lifetime and reduces loss of performance for write operations over time.
*   Buying the right sized SSD is key. As with all filesystems, target <75 % occupancy for all SSD partitions to ensure efficient use by the kernel.

#### 參考連結

這些文章並不能包含所有的情況，但是你可以從中學習到一些重點。

*   [SSD Anthology (歷史課，有點時間了)](http://www.anandtech.com/show/2738)
*   [SSD Relapse (較新一點，比較跟的上時代了](http://www.anandtech.com/show/2829))
*   [一位使用者的建議](http://forums.anandtech.com/showthread.php?t=2069761)
*   [使用與測試 SSD TRIM 在 Linux 底下的支援性](http://techgage.com/article/enabling_and_testing_ssd_trim_support_under_linux/)

## Tips for Maximizing SSD Performance

### Partition Alignment

Using partitions that are aligned with the erase block size is highly recommended. In past, this required manual calculation and intervention when partitioning. Many of the common partition tools handle partition alignment automatically (assuming users are using an up-to-date version):

*   fdisk
*   gdisk
*   gparted
*   parted

To verify a partition is aligned, query it using `/usr/bin/blockdev` as shown below, if a '0' is returned, the partition is aligned:

```
# blockdev --getalignoff /dev/<partition>
0

```

### TRIM

Most SSDs support the [ATA_TRIM command](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") for sustained long-term performance and wear-leveling. For more including some before and after benchmark, see [this](https://sites.google.com/site/lightrush/random-1/howtoconfigureext4toenabletrimforssdsonubuntu) tutorial.

As of linux kernel version 3.7, the following filesystems support TRIM: [Ext4](/index.php/Ext4 "Ext4"), [Btrfs](/index.php/Btrfs "Btrfs"), [JFS](/index.php/JFS "JFS"), and [XFS](/index.php/XFS "XFS").

The [Choice of Filesystem](#Choice_of_Filesystem) section of this article offers more details.

#### Verify TRIM Support

```
# hdparm -I /dev/sda |grep TRIM
        *    Data Set Management TRIM supported (limit 1 block)
        *    Deterministic read data after TRIM

```

To have a better understanding of "limit 1 block" or "limit 8 block", see [wikipedia:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "wikipedia:TRIM")

#### Enable TRIM by Mount Flags

Using this flag in one's `/etc/fstab` enables the benefits of the TRIM command stated above.

```
/dev/sda1  /       ext4   defaults,noatime,**discard**   0  1
/dev/sda2  /home   ext4   defaults,noatime,**discard**   0  2

```

**Note:** Using the `discard` flag for an ext3 root partition will result in it being mounted read-only.

**Warning:** Users need to be certain that kernel version 2.6.33 or above is being used AND that their SSD supports TRIM before attempting to mount a partition with the `discard` flag. Data loss can occur otherwise!

#### Apply TRIM via cron

Enabling TRIM on supported SSDs is definitely recommended. But sometimes it may cause some SSDs to [perform slowly](https://patrick-nagel.net/blog/archives/337) during deletion of files. If this is the case, one may choose to use fstrim as an alternative.

```
# fstrim -v /

```

The partition for which fstrim is to be applied must be mounted, and must be indicated by the mount point.

If this method seems like a better alternative, it might be a good idea to have this run from time to time using cron. To have this run daily, the default cron package ([cronie](https://www.archlinux.org/packages/?name=cronie)) includes an anacron implementation which, by default, is set up for hourly, daily, weekly, and monthly jobs. To add to the list of daily cron tasks, simply create a script that takes care of the desired actions and put it in `/etc/cron.daily`, `/etc/cron.weekly`, etc. Appropriate nice and ionice values are recommended if this method is chosen. If implemented, remove the `discard` option from `/etc/fstab`.

**Note:** Use the `discard` mount option as a first choice. This method should be considered second to the normal implementation of TRIM.

#### Apply TRIM via a systemd service

See [this blog post](http://mjanja.co.ke/2013/04/systemd-service-to-trim-free-ssd-cells-at-boot/).

##### Enable TRIM for LVM

Enable `issue_discards` option in `/etc/lvm/lvm.conf`.

#### Enable TRIM With mkfs.ext4 or tune2fs (Discouraged)

One can set the trim flag statically with tune2fs or when the filesystem is created:

```
# tune2fs -o discard /dev/sd**XY**

```

or:

```
# mkfs.ext4 -E discard /dev/sd**XY**

```

**Warning:** This method will cause the `discard` option to [not show up](https://bbs.archlinux.org/viewtopic.php?id=137314) with `mount`.

### I/O Scheduler

Consider switching from the default [CFQ](https://en.wikipedia.org/wiki/CFQ "wikipedia:CFQ") scheduler (Completely Fair Queuing) to [NOOP](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler") or [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler"). The latter two offer performance boosts for SSDs. The NOOP scheduler, for example, implements a simple queue for all incoming I/O requests, without re-ordering and grouping the ones that are physically closer on the disk. On SSDs seek times are identical for all sectors, thus invalidating the need to re-order I/O queues based on them.

The CFQ scheduler is enabled by default on Arch. Verify this by viewing the contents `/sys/block/sd**X**/queue/scheduler`:

 `$ cat /sys/block/sd**X**/queue/scheduler` 
```
noop deadline [cfq]

```

The scheduler currently in use is denoted from the available schedulers by the brackets.

Users can change this on the fly without the need to reboot with:

```
# echo noop > /sys/block/sd**X**/queue/scheduler

```

or:

```
$ sudo tee /sys/block/sd**X**/queue/scheduler <<< noop

```

This method is non-persistent (eg. change will be lost upon rebooting). Confirm the change was made by viewing the contents of the file again and ensuring "noop" is between brackets.

#### Kernel parameter (for a single device)

If the sole storage device in the system is an SSD, consider setting the I/O scheduler for the entire system via the `elevator=noop` [kernel parameter](/index.php/Kernel_parameters "Kernel parameters").

#### Using the sys virtual filesystem (for multiple devices)

This method is preferred when the system has several physical storage devices (for example an SSD and an HDD).

Create the following tmpfile where **X** is the letter for the SSD device.

 `/etc/tmpfiles.d/set_IO_scheduler.conf ` 
```
w /sys/block/sd**X**/queue/scheduler - - - - noop

```

Because of the potential for udev to assign different `/dev/` nodes to drives before and after a kernel update, users must take care that the NOOP scheduler is applied to the correct device upon boot. One way to do this is by using the SSD's device ID to determine its `/dev/` node. To do this automatically, use the following snippet instead of the line above and add it to `/etc/rc.local`:

```
declare -ar SSDS=(
  'scsi-SATA_SAMSUNG_SSD_PM8_S0NUNEAB861972'
  'ata-SAMSUNG_SSD_PM810_2.5__7mm_256GB_S0NUNEAB861972'
)

for SSD in "${SSDS[@]}" ; do
  BY_ID=/dev/disk/by-id/$SSD

  if [[ -e $BY_ID ]] ; then
    DEV_NAME=`ls -l $BY_ID | awk '{ print $NF }' | sed -e 's/[/\.]//g'`
    SCHED=/sys/block/$DEV_NAME/queue/scheduler

    if [[ -w $SCHED ]] ; then
      echo noop > $SCHED
    fi
  fi
done

```

where `SSDS` is a Bash array containing the device IDs of all SSD devices. Device IDs are listed in `/dev/disk/by-id/` as symbolic links pointing to their corresponding `/dev/` nodes. To view the links listed with their targets, issue the following command:

```
$ ls -l /dev/disk/by-id/

```

#### Using udev for one device or HDD/SSD mixed environment

Though the above will undoubtedly work, it is probably considered a reliable workaround. Ergo, it would be preferred to use the system that is responsible for the devices in the first place to implement the scheduler. In this case it is udev, and to do this, all one needs is a simple [udev](/index.php/Udev "Udev") rule.

To do this, create the following:

 `/etc/udev/rules.d/60-schedulers.rules` 
```
# set deadline scheduler for non-rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", TEST!="queue/rotational", ATTR{queue/scheduler}="deadline"
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="deadline"

# set cfq scheduler for rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="cfq"

```

Of course, set Deadline/CFQ to the desired schedulers. Changes should occur upon next boot. To check success of the new rule:

```
$ cat /sys/block/sd**X**/queue/scheduler  # where **X** is the device in question

```

**Note:** Keep in mind CFQ is the default scheduler, so the second rule with the standard kernel is not actually necessary. Also, in the example sixty is chosen because that is the number udev uses for its own persistent naming rules. Thus, it would seem that block devices are at this point able to be modified and this is a safe position for this particular rule. But the rule can be named anything so long as it ends in `.rules`.)

### Swap Space on SSDs

One can place a swap partition on an SSD. Most modern desktops with an excess of 2 Gigs of memory rarely use swap at all. The notable exception is systems which make use of the hibernate feature. The following is a recommended tweak for SSDs using a swap partition that will reduce the "swappiness" of the system thus avoiding writes to swap:

```
# echo 1 > /proc/sys/vm/swappiness

```

Or one can simply do as recommended in the [Maximizing Performance](/index.php/Improving_performance#Swappiness "Improving performance") article:

 `/etc/sysctl.d/99-sysctl.conf` 
```
vm.swappiness=1
vm.vfs_cache_pressure=50
```

### SSD Memory Cell Clearing

On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were at the time the device was installed thus restoring it to its [factory default write performance](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

The reset is easily accomplished in a three step procedure denoted on the [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") wiki article.

## Tips for Minimizing SSD Read/Writes

An overarching theme for SSD usage should be 'simplicity' in terms of locating high-read/write operations either in RAM (Random Access Memory) or on a physical HDD rather than on an SSD. Doing so will add longevity to an SSD. This is primarily due to the large erase block size (512 KiB in some cases); a lot of small writes result in huge effective writes.

**Note:** A 32GB SSD with a mediocre 10x write amplification factor, a standard 10000 write/erase cycle, and **10GB of data written per day**, would get an **8 years life expectancy**. It gets better with bigger SSDs and modern controllers with less write amplification.

Use `$ iotop -oPa` and sort by disk writes to see how much programs are writing to disk.

### Intelligent Partition Scheme

*   For systems with both an SSD and an HDD, consider relocating the `/var` partition to a magnetic disc on the system rather than on the SSD itself to avoid read/write wear.

### noatime Mount Flag

Using this flag in one's `/etc/fstab` halts the logging of read accesses to the file system via an update to the atime information associated with the file. The importance of the `noatime` setting is that it eliminates the need by the system to make writes to the file system for files which are simply being read. Since writes can be somewhat expensive as mentioned in previous section, this can result in measurable performance gains.

**Note:** The write time information to a file will continue to be updated anytime the file is written to with this option enabled.

```
/dev/sda1  /       ext4   defaults,**noatime**   0  1
/dev/sda2  /home   ext4   defaults,**noatime**   0  2

```

**Note:** This setting will cause issues with some programs such as [Mutt](/index.php/Mutt "Mutt"), as the access time of the file will eventually be previous than the modification time, which would make no sense. Using the `relatime` option instead of `noatime` will ensure that the atime field will never be prior to the last modification time of a file. Alternatively, using the maildir storage format also solves this mutt issue.

### Locate High-Use Files to RAM

#### Browser Profiles

One can *easily* mount browser profile(s) such as chromium, firefox, opera, etc. into RAM via tmpfs and also use rsync to keep them synced with HDD-based backups. In addition to the obvious speed enhancements, users will also save read/write cycles on their SSD by doing so.

The AUR contains several packages to automate this process, for example [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/).

#### Others

For the same reasons a browser's profile can be relocated to RAM, so can highly used directories such as `/srv/http` (if running a web server). A sister project to [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/) is [anything-sync-daemon](https://aur.archlinux.org/packages/anything-sync-daemon/), which allows users to define **any** directory to sync to RAM using the same underlying logic and safe guards.

### Compiling in tmpfs

Intentionally compiling in `/tmp` is a great idea to minimize this problem. Arch Linux defaults `/tmp` to 50 % of the physical memory. For systems with >4 GB of memory, one can create a `/scratch` and mount it to tmpfs set to use more than 50 % of the physical memory.

Example of a machine with 8 GB of physical memory:

 `$ mount | grep tmpfs`  `tmpfs     /scratch     tmpfs     nodev,nosuid,size=7G     0     0` 

### Disabling Journaling on the filesystem

Using a journaling filesystem such as ext4 on an SSD WITHOUT a journal is an option to decrease read/writes. The obvious drawback of using a filesystem with journaling disabled is data loss as a result of an ungraceful dismount (i.e. post power failure, kernel lockup, etc.). With modern SSDs, [Ted Tso](http://tytso.livejournal.com/61830.html) advocates that journaling can be enabled with minimal extraneous read/write cycles under most circumstances:

**Amount of data written (in megabytes) on an ext4 file system mounted with `noatime`.**

| operation | journal | w/o journal | percent change |
| git clone | 367.0 | 353.0 | 3.81 % |
| make | 207.6 | 199.4 | 3.95 % |
| make clean | 6.45 | 3.73 | 42.17 % |

*"What the results show is that metadata-heavy workloads, such as make clean, do result in almost twice the amount data written to disk. This is to be expected, since all changes to metadata blocks are first written to the journal and the journal transaction committed before the metadata is written to their final location on disk. However, for more common workloads where we are writing data as well as modifying filesystem metadata blocks, the difference is much smaller."*

**Note:** The make clean example from the table above typifies the importance of intentionally doing compiling in tmpfs as recommended in the [preceding section](/index.php/Solid_State_Drives#Compiling_in_tmpfs "Solid State Drives") of this article!

## Choice of Filesystem

### Btrfs

[Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") support has been included with the mainline 2.6.29 release of the Linux kernel. Some feel that it is not mature enough for production use while there are also early adopters of this potential successor to ext4\. Users are encouraged to read the [Btrfs](/index.php/Btrfs "Btrfs") article for more info.

### Ext4

[Ext4](https://en.wikipedia.org/wiki/Ext4 "wikipedia:Ext4") is another filesystem that has support for SSD. It is considered as stable since 2.6.28 and is mature enough for daily use. ext4 users must explicitly enable the TRIM command support using the `discard` mount option in [fstab](/index.php/Fstab "Fstab") (or with `tune2fs -o discard /dev/sdaX`). See the [official in kernel tree documentation](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/filesystems/ext4.txt) for further information on ext4.

### XFS

Many users do not realize that in addition to ext4 and btrfs, [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") has TRIM support as well. This can be enabled in the usual ways. That is, the choice may be made of either using the discard option mentioned above, or by using the fstrim command. More information can be found on the [XFS wiki](http://xfs.org/index.php/FITRIM/discard).

### JFS

As of Linux kernel version 3.7, proper TRIM support has been added. So far, there is not a great wealth of information of the topic but it has certainly been picked up by [Linux news sites.](http://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY) It is apparent that it can be enabled via the `discard` mount option, or by using the method of batch TRIMs with fstrim.

## Firmware Updates

### ADATA

ADATA has a utility available for Linux (i686) on their support page [here](http://www.adata.com.tw/index.php?action=ss_main&page=ss_content_driver&lan=en). The link to the utility will appear after selecting the model.

### Crucial

Crucial provides an option for updating the firmware with an ISO image. These images can be found after selecting the product [here](http://www.crucial.com/support/firmware.aspx) and downloading the "Manual Boot File." Owners of an M4 Crucial model, may check if a firmware upgrade is needed with `smartctl`.

 `$ smartctl --all /dev/sd**X**` 
```
==> WARNING: This drive may hang after 5184 hours of power-on time:
[http://www.tomshardware.com/news/Crucial-m4-Firmware-BSOD,14544.html](http://www.tomshardware.com/news/Crucial-m4-Firmware-BSOD,14544.html)
See the following web pages for firmware updates:
[http://www.crucial.com/support/firmware.aspx](http://www.crucial.com/support/firmware.aspx)
[http://www.micron.com/products/solid-state-storage/client-ssd#software](http://www.micron.com/products/solid-state-storage/client-ssd#software)

```

Users seeing this warning are advised to backup all sensible data and **consider upgrading immediately**.

### Kingston

Kingston has a Linux utilty to update the firmware of their Sandforce based drives. It can be found on their [support page](http://www.kingston.com/us/support).

### Mushkin

The lesser known Mushkin brand Solid State drives also use Sandforce controllers, and have a Linux utility (nearly identical to Kingston's) to update the firmware.

### OCZ

OCZ has a command line utility available for Linux (i686 and x86_64) on their forum [here](http://www.ocztechnology.com/ssd_tools/).

### Samsung

Samsung notes that update methods other than by using their Magician Software is "not supported", but it is possible. Apparently the Magician Software can be used to make a USB drive bootable with the firmware update. The easiest method, though, is to use the bootable ISO images they provide for updating the firmware. They can be grabbed from [here](http://www.samsung.com/global/business/semiconductor/samsungssd/downloads.html).

**Note:** Samsung does not make it obvious at all that they actually provide these. They seem to have 4 different firmware update pages each referencing different ways of doing things.

### SanDisk

SanDisk makes **ISO firmware images** to allow SSD firmware update on operating systems that are unsupported by their SanDisk SSD Toolkit. One must choose the firmware for the right *SSD model*, as well as for the *capacity* that it has (e.g. 60GB, **or** 256GB). After burning the adequate ISO firmware image, simply restart the PC to boot with the newly created CD/DVD boot disk (may work from a USB stick.

The iso images just contain a linux kernel and an initrd. Extract them to `/boot` partition and boot them with [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux") to update the firmware.

I could not find a single page listing the firmware updates yet (site is a mess IMHO), but here are some relevant links:

SanDisk Extreme SSD [Firmware Release notes](http://kb.sandisk.com/app/answers/detail/a_id/10127) and [Manual Firmware update version R211](http://kb.sandisk.com/app/answers/detail/a_id/10476)

SanDisk Ultra SSD [Firmware release notes](http://kb.sandisk.com/app/answers/detail/a_id/10192) and [Manual Firmware update version 365A13F0](http://kb.sandisk.com/app/answers/detail/a_id/10477)

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