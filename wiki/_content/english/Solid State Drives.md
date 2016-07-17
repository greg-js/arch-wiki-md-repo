[w:Solid State Drives](https://en.wikipedia.org/wiki/Solid_State_Drive "w:Solid State Drive") (SSDs) are not PnP devices. Special considerations such as partition alignment, choice of file system, TRIM support, etc. are needed to set up SSDs for optimal performance. This article attempts to capture referenced, key learnings to enable users to get the most out of SSDs under Linux. Users are encouraged to read this article in its entirety before acting on recommendations.

## Contents

*   [1 Choice of filesystem](#Choice_of_filesystem)
    *   [1.1 Btrfs](#Btrfs)
    *   [1.2 Ext4](#Ext4)
    *   [1.3 XFS](#XFS)
    *   [1.4 JFS](#JFS)
    *   [1.5 Other filesystems](#Other_filesystems)
*   [2 Partition alignment](#Partition_alignment)
*   [3 Firmware updates](#Firmware_updates)
    *   [3.1 ADATA](#ADATA)
    *   [3.2 Crucial](#Crucial)
    *   [3.3 Intel](#Intel)
    *   [3.4 Kingston](#Kingston)
    *   [3.5 Mushkin](#Mushkin)
    *   [3.6 OCZ](#OCZ)
    *   [3.7 Samsung](#Samsung)
        *   [3.7.1 Native upgrade](#Native_upgrade)
    *   [3.8 SanDisk](#SanDisk)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Resolving NCQ errors](#Resolving_NCQ_errors)
    *   [4.2 Resolving SATA power management related errors](#Resolving_SATA_power_management_related_errors)
*   [5 See also](#See_also)

## Choice of filesystem

This section describes optimized [filesystems](/index.php/Filesystems "Filesystems") to use on a SSD.

It's still possible/required to use other filesystems, e.g. FAT32 for the [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI").

For TRIM support, see [Solid State Drives/Tips and tricks#TRIM](/index.php/Solid_State_Drives/Tips_and_tricks#TRIM "Solid State Drives/Tips and tricks").

### Btrfs

[Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") support has been included with the mainline 2.6.29 release of the Linux kernel, and since August 2014 it has been marked as stable. However, some features are experimental, and users are encouraged to read the [Btrfs](/index.php/Btrfs "Btrfs") article for more info.

### Ext4

[Ext4](https://en.wikipedia.org/wiki/Ext4 "wikipedia:Ext4") is another filesystem that has support for SSD. It is considered as stable since 2.6.28 and is mature enough for daily use. See the [official in kernel tree documentation](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/filesystems/ext4.txt) for further information on ext4.

### XFS

[XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") has TRIM support as well. More information can be found on the [XFS wiki](http://xfs.org/index.php/FITRIM/discard).

### JFS

As of Linux kernel version 3.7, proper TRIM support has been added.[[1]](http://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY)

### Other filesystems

There are other filesystems specifically [designed for SSD](https://en.wikipedia.org/wiki/List_of_flash_file_systems#File_systems_optimized_for_flash_memory.2C_solid_state_media "wikipedia:List of flash file systems"), for example [F2FS](/index.php/F2FS "F2FS").

## Partition alignment

See [Partitioning#Partition alignment](/index.php/Partitioning#Partition_alignment "Partitioning").

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

Samsung notes that update methods other than using their Magician Software are "not supported," but it is possible. The Magician Software can be used to make a USB drive bootable with the firmware update. Samsung provides pre-made [bootable ISO images](http://www.samsung.com/global/business/semiconductor/samsungssd/downloads.html) that can be used to update the firmware. Another option is to use Samsung's [samsung_magician](https://aur.archlinux.org/packages/samsung_magician/), which is available in the AUR. Magician only supports Samsung-branded SSDs; those manufactured by Samsung for OEMs (e.g., Lenovo) are not supported.

**Note:** Samsung does not make it obvious at all that they actually provide these. They seem to have 4 different firmware update pages, and each references different ways of doing things.

Users preferring to run the firmware update from a live USB created under Linux (without using Samsung's "Magician" software under Microsoft Windows) can refer to [this post](http://fomori.org/blog/?p=933) for reference.

#### Native upgrade

Alternatively, the firmware can be upgraded natively, without making a bootable USB stick, as shown below.

First visit the [Samsung downloads page](http://www.samsung.com/global/business/semiconductor/minisite/SSD/global/html/support/downloads.html) and download the latest firmware for Windows, which is available as a disk image. In the following, `Samsung_SSD_840_EVO_EXT0DB6Q.iso` is used as an example file name, adjust it accordingly.

Setup the disk image:

```
$ udisksctl loop-setup -r -f Samsung_SSD_840_EVO_EXT0DB6Q.iso

```

This will make the ISO available as a loop device, and display the device path. Assuming it was `/dev/loop0`:

```
$ udisksctl mount -b /dev/loop0

```

Get the contents of the disk:

```
$ mkdir Samsung_SSD_840_EVO_EXT0DB6Q
$ cp -r /run/media/$USER/CDROM/isolinux/ Samsung_SSD_840_EVO_EXT0DB6Q

```

Unmount the iso:

```
$ udisksctl unmount -b /dev/loop0
$ cd Samsung_SSD_840_EVO_EXT0DB6Q/isolinux

```

There is a FreeDOS image here that contains the firmware. Mount the image as before:

```
$ udisksctl loop-setup -r -f btdsk.img
$ udisksctl mount -b /dev/loop1
$ cp -r /run/media/$USER/C04D-1342/ Samsung_SSD_840_EVO_EXT0DB6Q
$ cd Samsung_SSD_840_EVO_EXT0DB6Q/C04D-1342/samsung

```

Get the disk number from magician:

```
# magician -L

```

Assuming it was 0:

```
# magician --disk 0 -F -p DSRD

```

Verify that the latest firmware has been installed:

```
# magician -L

```

Finally reboot.

### SanDisk

SanDisk makes **ISO firmware images** to allow SSD firmware update on operating systems that are unsupported by their SanDisk SSD Toolkit. One must choose the firmware for the right *SSD model*, as well as for the *capacity* that it has (e.g. 60GB, **or** 256GB). After burning the adequate ISO firmware image, simply restart the PC to boot with the newly created CD/DVD boot disk (may work from a USB stick).

The iso images just contain a linux kernel and an initrd. Extract them to `/boot` partition and boot them with [GRUB](/index.php/GRUB "GRUB") or [Syslinux](/index.php/Syslinux "Syslinux") to update the firmware.

See also:

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