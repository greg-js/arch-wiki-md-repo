This article covers special topics for operating [w:Solid State Drives](https://en.wikipedia.org/wiki/Solid_State_Drive "w:Solid State Drive") (SSDs) and other flash-memory based storage devices. If you want to partition a SSD for a specific purpose, it may be useful to consider the [List of file systems optimized for flash memory](https://en.wikipedia.org/wiki/List_of_file_systems#File_systems_optimized_for_flash_memory.2C_solid_state_media "w:List of file systems"). For general usage, you should simply choose your preferred [filesystem](/index.php/Filesystem "Filesystem").

## Contents

*   [1 Usage](#Usage)
    *   [1.1 TRIM](#TRIM)
        *   [1.1.1 Periodic TRIM](#Periodic_TRIM)
        *   [1.1.2 Continuous TRIM](#Continuous_TRIM)
        *   [1.1.3 LVM](#LVM)
        *   [1.1.4 dm-crypt](#dm-crypt)
    *   [1.2 Maximizing performance](#Maximizing_performance)
    *   [1.3 Security](#Security)
        *   [1.3.1 Hdparm shows "frozen" state](#Hdparm_shows_.22frozen.22_state)
        *   [1.3.2 SSD memory cell clearing](#SSD_memory_cell_clearing)
        *   [1.3.3 Hardware encryption](#Hardware_encryption)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Resolving NCQ errors](#Resolving_NCQ_errors)
    *   [2.2 Resolving SATA power management related errors](#Resolving_SATA_power_management_related_errors)
*   [3 Firmware](#Firmware)
    *   [3.1 ADATA](#ADATA)
    *   [3.2 Crucial](#Crucial)
    *   [3.3 Intel](#Intel)
    *   [3.4 Kingston](#Kingston)
    *   [3.5 Mushkin](#Mushkin)
    *   [3.6 OCZ](#OCZ)
    *   [3.7 Samsung](#Samsung)
        *   [3.7.1 Native upgrade](#Native_upgrade)
    *   [3.8 SanDisk](#SanDisk)
*   [4 See also](#See_also)

## Usage

### TRIM

Most SSDs support the [ATA_TRIM command](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") for sustained long-term performance and wear-leveling. A [techspot](http://www.techspot.com/review/737-ocz-vector-150-ssd/page9.html) article shows performance benchmark examples of before and after filling an SSD with data.

As of Linux kernel version 3.8 onwards, support for TRIM was continually added for the different [filesystems](/index.php/Filesystems "Filesystems"). See the following table for an indicative overview and the respective filesystems' articles for further details:

| File system | Continuous TRIM
(`discard` option) | Periodic TRIM
(*fstrim*) | References
and notes |
| [Ext3](/index.php/Ext3 "Ext3") | No | ? |
| [Ext4](/index.php/Ext4 "Ext4") | Yes | Yes | [[1]](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/ext4.txt#n344) |
| [Btrfs](/index.php/Btrfs "Btrfs") | Yes | Yes |
| [JFS](/index.php/JFS "JFS") | Yes | Yes | [[2]](http://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY) |
| [XFS](/index.php/XFS "XFS") | Yes | Yes | [[3]](http://xfs.org/index.php/FITRIM/discard) |
| [F2FS](/index.php/F2FS "F2FS") | Yes | Yes |
| [VFAT](/index.php/VFAT "VFAT") | Yes | No |
| [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | No | Yes | since version 2015.3.14, [[4]](http://permalink.gmane.org/gmane.comp.file-systems.ntfs-3g.devel/1101) |

**Warning:** Users need to be certain that their SSD supports TRIM before attempting to use it. Data loss can occur otherwise!

To verify TRIM support, run:

```
# lsblk -D

```

And check the values of DISC-GRAN and DISC-MAX columns. Non-zero values indicate TRIM support.

Or [install](/index.php/Help:Reading#Installation_of_packages "Help:Reading") [hdparm](https://www.archlinux.org/packages/?name=hdparm) package and run:

```
# hdparm -I /dev/sda | grep TRIM
        *    Data Set Management TRIM supported (limit 1 block)

```

**Note:** There are different types of TRIM support defined by the specification. Hence, the output may differ depending what the drive supports. See [w:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "w:TRIM") for more information.

#### Periodic TRIM

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package provides `fstrim.service` and `fstrim.timer` [systemd](/index.php/Systemd "Systemd") unit files. [Enabling](/index.php/Enabling "Enabling") the timer will activate the service weekly. The service executes [fstrim(8)](http://man7.org/linux/man-pages/man8/fstrim.8.html) on all mounted filesystems on devices that support the *discard* operation.

The timer relies on the timestamp of `/var/lib/systemd/timers/stamp-fstrim.timer` (which it will create upon first invocation) to know whether a week has elapsed since it last ran. Therefore there is no need to worry about too frequent invocations, in an *anacron*-like fashion.

To query the units activity and status, see [journalctl](/index.php/Journalctl "Journalctl"). To change the periodicity of the timer or the command run, [edit](/index.php/Edit "Edit") the provided unit files.

#### Continuous TRIM

**Warning:** Unfortunately, there are wide quality gaps of SSD's bios' to perform continuous TRIM, which is also why using the `discard` mount flag is [recommended against](http://thread.gmane.org/gmane.comp.file-systems.ext4/41974) generally by filesystem developer Theodore Ts'o. If in doubt about your hardware, apply [#Periodic TRIM](#Periodic_TRIM) instead.

**Note:** Before [SATA 3.1](https://en.wikipedia.org/wiki/Serial_ATA#SATA_revision_3.1 "w:Serial ATA") all TRIM commands were synchronous, so continuous trimming would produce frequent system freezes. In this case, applying [#Periodic TRIM](#Periodic_TRIM) less often is better alternative. Similar issue holds also for a [number of devices](https://github.com/torvalds/linux/blob/master/drivers/ata/libata-core.c#L4403-L4417), for which queued TRIM command execution was blacklisted due to [serious data corruption](https://blog.algolia.com/when-solid-state-drives-are-not-that-solid/). See [Wikipedia:Trim (computing)#Shortcomings](https://en.wikipedia.org/wiki/Trim_(computing)#Shortcomings for details.

Using the `discard` option for a mount in `/etc/fstab` enables continuous TRIM in device operations:

```
/dev/sda2  /boot       ext4  defaults,noatime,**discard**   0  2
/dev/sda1  /boot/efi   vfat  defaults,noatime,**discard**   0  2
/dev/sda3  /           ext4  defaults,noatime,**discard**   0  2

```

The main benefit of continuous TRIM is speed; an SSD can perform more efficient [garbage collection](http://arstechnica.com/gadgets/2015/04/ask-ars-my-ssd-does-garbage-collection-so-i-dont-need-trim-right/). However, results vary and particularly earlier SSD generations may also show just the opposite effect. Also for this reason, some distributions decided against using it (e.g. Ubuntu: see [this article](http://www.phoronix.com/scan.php?page=news_item&px=MTUxOTY) and the [related blueprint](https://blueprints.launchpad.net/ubuntu/+spec/core-1311-ssd-trimming)).

**Note:** There is no need for the `discard` flag if you run `fstrim` periodically.

On the ext4 filesystem, the `discard` flag can also be set as a [default mount option](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") using *tune2fs*:

```
# tune2fs -o discard /dev/sd**XY**

```

Using the default mount options instead of an entry in `/etc/fstab` is useful for external drives, because such partition will be mounted with the default options also on other machines. There is no need to edit `/etc/fstab` on every machine.

**Note:** The default mount options are not listed in `/proc/mounts`.

#### LVM

Change the value of `issue_discards` option from 0 to 1 in `/etc/lvm/lvm.conf`.

**Note:** Enabling this option will "issue discards to a logical volumes's underlying physical volume(s) when the logical volume is no longer using the physical volumes' space (e.g. *lvremove*, *lvreduce*, etc)" (see [lvm.conf(5)](http://man7.org/linux/man-pages/man5/lvm.conf.5.html) and/or inline comments in `/etc/lvm/lvm.conf`). As such it does not seem to be required for "regular" TRIM requests (file deletions inside a filesystem) to be functional.

#### dm-crypt

**Warning:** The discard option allows discard requests to be passed through the encrypted block device. This improves performance on SSD storage but has security implications. See [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") for more information.

For non-root filesystems, configure `/etc/crypttab` to include `discard` in the list of options for encrypted block devices located on a SSD (see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")).

For the root filesystem, follow the instructions from [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") to add the right kernel parameter to the bootloader configuration.

### Maximizing performance

Follow the tips in [Improving performance#Storage devices](/index.php/Improving_performance#Storage_devices "Improving performance") to maximize the performance of your drives.

### Security

#### Hdparm shows "frozen" state

Some motherboard BIOS' issue a "security freeze" command to attached storage devices on initialization. Likewise some SSD (and HDD) BIOS' are set to "security freeze" in the factory already. Both result in the device's password security settings to be set to **frozen**, as shown in below output:

 `# hdparm -I /dev/sda` 
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

If you intend to set a password to a "frozen" device yourself, a motherboard BIOS with support for it is required. A lot of notebooks have support, because it is required for [hardware encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption"), but support may not be trivial for a desktop/server board. For the Intel DH67CL/BL motherboard, for example, the motherboard has to be set to "maintenance mode" by a physical jumper to access the settings (see [[5]](http://sstahlman.blogspot.in/2014/07/hardware-fde-with-intel-ssd-330-on.html?showComment=1411193181867#c4579383928221016762), [[6]](https://communities.intel.com/message/251978#251978)).

**Warning:** Do not try to change the above **lock** security settings with `hdparm` unless you know exactly what you are doing.

If you intend to erase the SSD, see [Securely wipe disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk") and [#SSD memory cell clearing](#SSD_memory_cell_clearing) below.

#### SSD memory cell clearing

On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were at the time the device was installed thus restoring it to its [factory default write performance](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

The reset is easily accomplished in a three step procedure denoted on the [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") wiki article. If the reason for the reset is to wipe data, you may not want to rely on the SSD bios to perform it securely. See [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk") for further information and examples to perform a wipe.

#### Hardware encryption

As noted in [#Hdparm shows frozen state](#Hdparm_shows_.22frozen.22_state) setting a password for a storage device (SSD/HDD) in the BIOS may also initialize the hardware encryption of devices supporting it. If the device also conforms to the OPAL standard, this may also be achieved without a respective BIOS feature to set the passphrase, see [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives").

## Troubleshooting

It is possible that the issue you are encountering is a firmware bug which is not Linux specific, so before trying to troubleshoot an issue affecting the SSD device, you should first check if updates are available for:

*   The [SSD's firmware](/index.php/Solid_State_Drives/Firmware "Solid State Drives/Firmware")
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

## Firmware

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

Users seeing this warning are advised to backup all sensible data and **consider upgrading immediately**. Check [this instructions](http://www.rojtberg.net/1008/updating-crucial-mx100-firmware-with-ubuntu/) to update Crucial MX100 firmware by using the ISO image and Grub.

### Intel

Intel has a Linux live system based [Firmware Update Tool](https://downloadcenter.intel.com/download/18363) for operating systems that are not compatible with its [Intel® Solid-State Drive Toolbox](https://downloadcenter.intel.com/download/18455) software.

### Kingston

Kingston has a Linux utility to update the firmware of Sandforce controller based drives: [SSD support page](http://www.kingston.com/en/support/technical/category/ssd). Click the images on the page to go to a support page for your SSD model. Support specifically for, e.g. the SH100S3 SSD, can be found here: [support page](http://www.hyperxgaming.com/us/support/technical/products?model=sh100s3).

### Mushkin

The lesser known Mushkin brand Solid State drives also use Sandforce controllers, and have a Linux utility (nearly identical to Kingston's) to update the firmware.

### OCZ

OCZ has a command line utility available for Linux (i686 and x86_64) on their forum [here](http://www.ocztechnology.com/ssd_tools/). The AUR provides [ocz-ssd-utility](https://aur.archlinux.org/packages/ocz-ssd-utility/), [ocztoolbox](https://aur.archlinux.org/packages/ocztoolbox/) and [oczclout](https://aur.archlinux.org/packages/oczclout/).

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

## See also

*   [Discussion on Reddit about installing Arch on an SSD](http://www.reddit.com/r/archlinux/comments/rkwjm/what_should_i_keep_in_mind_when_installing_on_ssd/)
*   See the [Flashcache](/index.php/Flashcache "Flashcache") article for advanced information on using solid-state with rotational drives for top performance.
*   [Re: Varying Leafsize and Nodesize in Btrfs](http://permalink.gmane.org/gmane.comp.file-systems.btrfs/19446)
*   [Re: SSD alignment and Btrfs sector size](http://thread.gmane.org/gmane.comp.file-systems.btrfs/19650/focus=19667)
*   [Erase Block (Alignment) Misinformation?](http://forums.anandtech.com/showthread.php?t=2266113)
*   [Is alignment to erase block size needed for modern SSD's?](http://superuser.com/questions/492084/is-alignment-to-erase-block-size-needed-for-modern-ssds)
*   [Btrfs support for efficient SSD operation (data blocks alignment)](http://thread.gmane.org/gmane.comp.file-systems.btrfs/15646)
*   [SSD, Erase Block Size & LVM: PV on raw device, Alignment](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)