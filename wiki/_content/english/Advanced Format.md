## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 More Detailed Explanation](#More_Detailed_Explanation)
    *   [1.2 External Links](#External_Links)
*   [2 Current HDD Models that Employ a 4k Sectors](#Current_HDD_Models_that_Employ_a_4k_Sectors)
*   [3 How to determine if HDD employ a 4k sector](#How_to_determine_if_HDD_employ_a_4k_sector)
*   [4 Aligning Partitions](#Aligning_Partitions)
    *   [4.1 Check your partitions alignment](#Check_your_partitions_alignment)
    *   [4.2 GPT (Recommended)](#GPT_.28Recommended.29)
*   [5 Special Consideration for WD Green HDDs](#Special_Consideration_for_WD_Green_HDDs)
    *   [5.1 Disable via hdparm](#Disable_via_hdparm)
        *   [5.1.1 Is this safe?](#Is_this_safe.3F)
    *   [5.2 Disable via changing firmware value (persistent)](#Disable_via_changing_firmware_value_.28persistent.29)

## Introduction

The [Advanced Format](https://en.wikipedia.org/wiki/Advanced_Format "wikipedia:Advanced Format") feature reduces overhead by using 4 kilobyte sectors instead of the traditional 512 byte sectors. The old format gave a format efficiency of 87%. Advanced Format results in a format efficiency of 96% which increases space by up to 11%. The 4k sector is slated to become the next standard for HDDs by 2014.

### More Detailed Explanation

The main idea behind using 4096-byte sectors is to increase the bit density on each track by reducing the number of gaps which hold Sync/DAM and ECC (Error Correction Code) information between data sectors. For eight 512-byte sectors, the track also holds eight sector gaps.

By having one single sector of size 4096-byte (8 x 512-byte), the track holds only 1 sector gap for each data sector thus reducing an overhead for a need to support multiple Sync/DAM and ECC blocks and at the same time increasing bit density.

Linux partitioning tools by default start each partition on sector 63 which leads to a bad performance in HDDs that use this 4K sector size due to misalignment to 4K sector from the beginning of the track.

### External Links

*   [Western Digital’s Advanced Format: The 4K Sector Transition Begins](http://www.anandtech.com/Show/Index/2888?cPage=2&all=False&sort=0&page=1)
*   [White paper entitled "Advanced Format Technology."](http://www.wdc.com/wdproducts/library/WhitePapers/ENG/2579-771430.pdf)
*   Failure to align one's HDD results in poor read/write performance. See [this article](http://www.linuxconfig.org/linux-wd-ears-advanced-format) for specific examples.

## Current HDD Models that Employ a 4k Sectors

As of June 2011, there are a limited number of HDDs that support "Advanced Format" or 4k sectors as shown below.

All drives in this list have a physical sector size of 4096 bytes, but not all drives correctly report this to the OS. The actual value reported (via new fields in the ATA-8 spec) is shown in the table as the physical reported sector size. As this is the value partitioning tools use for alignment, it is important that it should be 4096 to avoid misalignment issues.

The logical sector size is the sector size used for data transfer. This value multiplied by the number of LBA sectors on the disk gives the disk capacity. Thus a disk with 4096 byte logical sectors will have a lower maximum LBA for the same capacity compared to a drive with 512 byte sectors. Drives with 512 byte logical sectors offer better compatibility with legacy operating systems (roughly those released before 2009) however drives with 4096 byte logical sectors may offer marginally better performance (e.g. more read/write requests may fit into the NCQ buffer.)

| Manufacturer | Model | Capacity | Reported sector size (bytes) |
| Logical | Physical |
| **3.5"** |
| Samsung | HD204UI | 2.0 TB | 512 | 512 |
| Seagate | ST3500413AS | 500.0 GB | 512 | 512 |
| Seagate | ST500DM002 | 500.0 GB | 512 | 4096 |
| Seagate | ST1000DL002 | 1.0 TB | 512 | 4096 |
| Seagate | ST1000DM003 | 1.0 TB | 512 | 4096 |
| Seagate | ST2000DL003 | 2.0 TB | 512 | 512 |
| Seagate | ST2000DM001 | 2.0 TB | 512 | 4096 |
| Seagate | ST3000DM001 | 3.0 TB | 512 | 4096 |
| Seagate | ST4000VN000 | 4.0 TB | 512 | 4096 |
| Western Digital | WD3000F9YZ | 2.0 TB | 512 | 4096 |
| Western Digital | WD30EZRX | 3.0 TB | 512 | 4096 |
| Western Digital | WD20EZRX | 2.0 TB | 512 | 4096 |
| Western Digital | WD30EZRSDTL | 3.0 TB |
| Western Digital | WD25EZRSDTL | 2.5 TB |
| Western Digital | WD20EARX | 2.0 TB | 512 | 4096 |
| Western Digital | WD20EFRX | 2.0 TB | 512 | 4096 |
| Western Digital | WD30EFRX | 3.0 TB | 512 | 4096 |
| Western Digital | WD40EFRX | 4.0 TB | 512 | 4096 |
| Western Digital | WD60EFRX | 6.0 TB | 512 | 4096 |
| Western Digital | WD10EARS | 1.0 TB |
| Western Digital | WD15EARS | 1.5 TB | 512 | [4096](http://excess.org/article/2010/11/wd-hdd-lying-about-4k-sectors/) |
| Western Digital | WD20EARS | 2.0 TB | 512 | [4096](http://community.wd.com/t5/Desktop-Mobile-Drives/Physical-Sector-Size-different-between-WD20EARS-00MVWB0-and/td-p/218226) or [512](http://community.wdc.com/t5/Desktop/4k-sector-drive-reporting-512-byte-sectors-to-OS-why/td-p/205060) |
| Western Digital | WD10EURS | 1.0 TB |
| Western Digital | WD8000AARS | 800.0 GB |
| Western Digital | WD6400AARS | 640.0 GB |
| **2.5"** |
| Samsung | ST1000LM024 | 1.0 TB | 512 | 4096 |
| Samsung | ST2000LM003 | 2.0 TB | 512 | 4096 |
| Seagate | ST320LT007 | 320 GB | 512 | 4096 |
| Seagate | ST9750420AS | 750 GB | 512 | 4096 |
| Seagate | ST1000LM014 | 1.0 TB | 512 | 4096 |
| Western Digital | WD10JPVT | 1.0 TB | 512 | 4096 |
| Western Digital | WD10TPVT | 1.0 TB |
| Western Digital | WD7500BPVT | 750.0 GB |
| Western Digital | WD7500KPVT | 750.0 GB |
| Western Digital | WD6400BPVT | 640.0 GB |
| Western Digital | WD5000BPVT | 500.0 GB |
| Western Digital | WD3200BPVT | 320.0 GB |
| Western Digital | WD2500BPVT | 250.0 GB | 512 | 4096 |
| Western Digital | WD1600BPVT | 160.0 GB |
| Western Digital | WD7500BPKX | 750.0 GB | 512 | 4096 |
| TOSHIBA | MQ01ABD100 | 1.0 TB | 512 | 4096 |
| TOSHIBA | MQ01ABC150 | 1.5 TB | 512 | 4096 |

**Note:** Readers are encouraged to add to this table.

## How to determine if HDD employ a 4k sector

The physical and logical sector size of hard disk /dev/sd*X* can be determined by reading the following sysfs entries:

```
$ cat /sys/class/block/sd*X*/queue/physical_block_size
$ cat /sys/class/block/sd*X*/queue/logical_block_size

```

Tools which will report the physical sector of a drive (provided the drive will report it correctly) includes

*   smartmontools (since 5.41 ; <tt>smartmontools -a</tt>, in information section)
*   hdparm (since 9.12 ; <tt>hdparm -I</tt>, in configuration section)

Note that both works even for USB-attached discs (if the USB bridge supports SAT aka SCSI/ATA Translation, ANSI INCITS 431-2007).

## Aligning Partitions

**Note:** This should no longer require manual intervention. Any tools using recent libblkid versions are capable of handling Advanced Format automatically.

Versions with this support include:

*   fdisk, since util-linux >= 2.15\. You should start with ‘-c -u’ to disable DOS compatibility and use sectors instead of cylinders.
*   parted, since parted >= 2.1.
*   mdadm, since util-linux >= 2.15
*   lvm2, since util-linux >= 2.15
*   mkfs.{ext,xfs,gfs2,ocfs2} all support libblkid directly.

Refer to [this page](https://www.tolaris.com/2011/07/21/libblkid-or-why-you-dont-need-to-worry-about-4k-disk-format/) for further information.

### Check your partitions alignment

**Note:** This only works with [MBR](/index.php/MBR "MBR"), not [GPT](/index.php/GPT "GPT").

```
# fdisk -lu /dev/sda
...
# Device     Boot      Start   End         Blocks      Id System
# /dev/sda1            2048    46876671    23437312    7  HPFS/NTFS

```

2048 (default since fdisk 2.17.2) means that your HDD is aligned correctly. Any other value divisible by 8 is good as well.

### GPT (Recommended)

When using [GPT](/index.php/GPT "GPT") partition tables, one need only use gdisk to create partitions which are aligned by default. For an example, see [SSD#Detailed Usage Example](/index.php/SSD#Detailed_Usage_Example "SSD").

## Special Consideration for WD Green HDDs

FYI - this section has nothing to do with Advanced Format technology, but this is an appropriate location to share it with users. The WD20EARS (and other sizes include 1.0 and 1.5 TB driver in the series) will attempt to park the read heads once every 8 seconds FOR THE LIFE OF THE HDD which is just horrible! To see if you are affected use the smartctl command (part of smartmontools). If the last column changes rapidly, this section applies to your drive.

```
# smartctl /dev/sdb -a | grep Load_Cycle
193 Load_Cycle_Count        0x0032   001   001   000    Old_age   Always       -       597115

```

### Disable via hdparm

Use hdparm in `/etc/systemd/system/lcc_fix.service` to disable this 'feature' and likely add life to your hdd:

 `/etc/systemd/system/lcc_fix.service ` 
```
[Unit]
Description=WDIDLE3

[Service]
Type=oneshot
ExecStart=/usr/bin/hdparm -J 300 --please-destroy-my-drive /dev/sdX
TimeoutSec=0
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Start the service

```
# systemctl start lcc_fix.service

```

Enable the service to autorun at boot.

```
# systemctl enable lcc_fix.service

```

#### Is this safe?

Why do we need to pass the "--please-destroy-my-drive" flag? Here is an email from hdparm author, Mark Lord:

```
> I have a Western DIgital \"Green\" drive (wd20ears).  I noticed you added a -J switch and that 
> it is said to adjust the idle3 timeout.  What frightens me is the output you gave it:
> 
> How safe or not is this to use?

I use it on my own drives.  It works for me.

If you can run the WDIDLE3.EXE MS-Dos program,
then use it instead -- it was written by WD,
and only they know how things really work there.

If you cannot use the WDIDLE3.EXE, then you
could consider "hdparm -J".  It works for me,
but it may or may not void some kind of warranty.

Cheers
-- 
Mark Lord
Real-Time Remedies Inc.
mlord@pobox.com

```

### Disable via changing firmware value (persistent)

**Warning:** The tool used in this process is experimental, use at your own risk!

**Note:** This method is persistent, you only need to do this once for every drive.

This method will use a utility called idle3ctl to alter the firmware value for the idle3 timer on WD hard drives (similar to wdidle3.exe from WD). The advantage compared to the official utility is you do not need to create a DOS bootdisk first to change the idle3 timer value. Additionally idle3ctl might also work over USB-to-S-ATA bridges (in some cases). The utility is provided by the [idle3-tools](https://www.archlinux.org/packages/?name=idle3-tools) package.

```
# idle3ctl -g /dev/your_wd_hdd

```

to get the raw idle3 timer value. You can disable the IntelliPark feature completely, with:

```
# idle3ctl -d /dev/your_wd_hdd

```

or set it to a different value (*0*-*255*) with (e.g. 10 seconds):

```
# idle3ctl -s 100 /dev/your_wd_hd

```

The range *0*-*128* is in 0.1s and *129-255* in 30s. For the changes to take effect, the drive needs to go through one powercycle, meaning powering it off and on again (on internal drives, a reboot is not sufficient).

If your WD hard drive is not recognized, you can use the *--force* option. For more options see:

```
$ idle3ctl -h

```