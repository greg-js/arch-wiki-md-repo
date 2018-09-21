Related articles

*   [Solid state drive/NVMe](/index.php/Solid_state_drive/NVMe "Solid state drive/NVMe")
*   [Solid state drive/Memory cell clearing](/index.php/Solid_state_drive/Memory_cell_clearing "Solid state drive/Memory cell clearing")
*   [Benchmarking/Data storage devices](/index.php/Benchmarking/Data_storage_devices "Benchmarking/Data storage devices")
*   [Improving performance#Storage devices](/index.php/Improving_performance#Storage_devices "Improving performance")
*   [Flashcache](/index.php/Flashcache "Flashcache")

This article covers special topics for operating [solid state drives](https://en.wikipedia.org/wiki/Solid-state_drive "wikipedia:Solid-state drive") (SSDs) and other flash-memory based storage devices. If you want to partition an SSD for a specific purpose, it may be useful to consider the [List of file systems optimized for flash memory](https://en.wikipedia.org/wiki/List_of_file_systems#File_systems_optimized_for_flash_memory.2C_solid_state_media "wikipedia:List of file systems"). For general usage, you should simply choose your preferred [filesystem](/index.php/Filesystem "Filesystem").

## Contents

*   [1 Usage](#Usage)
    *   [1.1 TRIM](#TRIM)
        *   [1.1.1 Periodic TRIM](#Periodic_TRIM)
        *   [1.1.2 Continuous TRIM](#Continuous_TRIM)
        *   [1.1.3 Trim an entire device](#Trim_an_entire_device)
        *   [1.1.4 LVM](#LVM)
        *   [1.1.5 dm-crypt](#dm-crypt)
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

Most SSDs support the [ATA_TRIM command](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") for sustained long-term performance and wear-leveling. A [techspot article](https://www.techspot.com/review/737-ocz-vector-150-ssd/page9.html) shows performance benchmark examples of before and after filling an SSD with data.

As of Linux kernel version 3.8 onwards, support for TRIM was continually added for the different [filesystems](/index.php/Filesystems "Filesystems"). See the following table for an indicative overview:

| File system | Continuous TRIM
(`discard` option) | Periodic TRIM
(*fstrim*) | References
and notes |
| [Ext3](/index.php/Ext3 "Ext3") | No | ? |
| [Ext4](/index.php/Ext4 "Ext4") | Yes | Yes | [[1]](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/tree/Documentation/filesystems/ext4.txt#n344) |
| [Btrfs](/index.php/Btrfs "Btrfs") | Yes | Yes |
| [JFS](/index.php/JFS "JFS") | Yes | Yes | [[2]](https://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY) |
| [XFS](/index.php/XFS "XFS") | Yes | Yes | [[3]](http://xfs.org/index.php/FITRIM/discard) |
| [F2FS](/index.php/F2FS "F2FS") | Yes | Yes |
| [VFAT](/index.php/VFAT "VFAT") | Yes | No |
| [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | No | Yes | since version 2015.3.14, [[4]](http://permalink.gmane.org/gmane.comp.file-systems.ntfs-3g.devel/1101) |

**Warning:** Users need to be certain that their SSD supports TRIM before attempting to use it. Data loss can occur otherwise!

To verify TRIM support, run:

```
# lsblk --discard

```

And check the values of DISC-GRAN (discard granularity) and DISC-MAX (discard max bytes) columns. Non-zero values indicate TRIM support.

Alternatively, [install](/index.php/Install "Install") [hdparm](https://www.archlinux.org/packages/?name=hdparm) package and run:

 `# hdparm -I /dev/sda | grep TRIM` 
```
        *    Data Set Management TRIM supported (limit 1 block)

```

**Note:** There are different types of TRIM support defined by the specification. Hence, the output may differ depending what the drive supports. See [Wikipedia:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "wikipedia:TRIM") for more information.

#### Periodic TRIM

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package provides `fstrim.service` and `fstrim.timer` [systemd](/index.php/Systemd "Systemd") unit files. [Enabling](/index.php/Enabling "Enabling") the timer will activate the service weekly. The service executes [fstrim(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fstrim.8) on all mounted filesystems on devices that support the *discard* operation.

The timer relies on the timestamp of `/var/lib/systemd/timers/stamp-fstrim.timer` (which it will create upon first invocation) to know whether a week has elapsed since it last ran. Therefore there is no need to worry about too frequent invocations, in an *anacron*-like fashion.

To query the units activity and status, see [journalctl](/index.php/Journalctl "Journalctl"). To change the periodicity of the timer or the command run, [edit](/index.php/Edit "Edit") the provided unit files.

#### Continuous TRIM

**Note:** There is no need to enable continuous TRIM if you run `fstrim` periodically. If you want to use TRIM, use either periodic TRIM or continuous TRIM.

Instead of issuing TRIM commands once in a while (by default once a week if using `fstrim.timer`), it is also possible to issue TRIM commands each time files are deleted instead. The latter is the continuous TRIM.

**Warning:** Before [SATA 3.1](https://en.wikipedia.org/wiki/Serial_ATA#SATA_revision_3.1 for details.

**Note:** Continuous TRIM is not the most preferred way to issue TRIM commands among the Linux community. For example, Ubuntu enables periodic TRIM by default [[5]](https://askubuntu.com/questions/1034169/is-trim-enabled-on-my-ubuntu-18-04-installation), Debian does not recommend using continuous TRIM [[6]](https://wiki.debian.org/SSDOptimization#Mounting_SSD_filesystems) and Red Hat recommends using periodic TRIM over using continuous TRIM if feasible. [[7]](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/ch02s04.html)

Using the `discard` option for a mount in `/etc/fstab` enables continuous TRIM in device operations:

```
/dev/sda1  /           ext4  defaults,**discard**   0  1

```

**Note:** Specifying the discard mount option in `/etc/fstab` does not work on XFS on `/` because it gets remounted on boot. According to [this thread](https://bbs.archlinux.org/viewtopic.php?id=143254) it has to be set using the `rootflags=discard` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

On the ext4 filesystem, the `discard` flag can also be set as a [default mount option](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") using *tune2fs*:

```
# tune2fs -o discard /dev/sd**XY**

```

Using the default mount options instead of an entry in `/etc/fstab` is useful for external drives, because such partition will be mounted with the default options also on other machines. There is no need to edit `/etc/fstab` on every machine.

**Note:** The default mount options are not listed in `/proc/mounts`.

#### Trim an entire device

If you want to trim your entire SSD at once, e.g. for a new install, or you want to sell your SSD, you can use the blkdiscard command, which will instantly discard all blocks on a device.

**Warning:** all data on the device will be lost!

```
# blkdiscard /dev/sd*X*

```

#### LVM

Change the value of `issue_discards` option from 0 to 1 in `/etc/lvm/lvm.conf`.

**Note:** Enabling this option will "issue discards to a logical volumes's underlying physical volume(s) when the logical volume is no longer using the physical volumes' space (e.g. *lvremove*, *lvreduce*, etc)" (see [lvm.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.conf.5) and/or inline comments in `/etc/lvm/lvm.conf`). As such it does not seem to be required for "regular" TRIM requests (file deletions inside a filesystem) to be functional.

#### dm-crypt

**Warning:** The discard option allows discard requests to be passed through the encrypted block device. This improves performance on SSD storage but has security implications. See [dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") for more information.

For non-root filesystems, configure `/etc/crypttab` to include `discard` in the list of options for encrypted block devices located on an SSD (see [dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")).

For the root filesystem, follow the instructions from [dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") to add the right kernel parameter to the bootloader configuration.

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

If you intend to set a password to a "frozen" device yourself, a motherboard BIOS with support for it is required. A lot of notebooks have support, because it is required for [hardware encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption"), but support may not be trivial for a desktop/server board. For the Intel DH67CL/BL motherboard, for example, the motherboard has to be set to "maintenance mode" by a physical jumper to access the settings (see [[8]](https://sstahlman.blogspot.in/2014/07/hardware-fde-with-intel-ssd-330-on.html?showComment=1411193181867#c4579383928221016762), [[9]](https://communities.intel.com/message/251978#251978)).

**Warning:** Do not try to change the above **lock** security settings with `hdparm` unless you know exactly what you are doing.

If you intend to erase the SSD, see [Securely wipe disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk") and [#SSD memory cell clearing](#SSD_memory_cell_clearing) below.

#### SSD memory cell clearing

On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were at the time the device was installed thus restoring it to its [factory default write performance](https://www.anandtech.com/show/2738/8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

The reset is easily accomplished in a three step procedure denoted on the [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") wiki article. If the reason for the reset is to wipe data, you may not want to rely on the SSD bios to perform it securely. See [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk") for further information and examples to perform a wipe.

#### Hardware encryption

As noted in [#Hdparm shows "frozen" state](#Hdparm_shows_.22frozen.22_state) setting a password for a storage device (SSD/HDD) in the BIOS may also initialize the hardware encryption of devices supporting it. If the device also conforms to the OPAL standard, this may also be achieved without a respective BIOS feature to set the passphrase, see [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives").

## Troubleshooting

It is possible that the issue you are encountering is a firmware bug which is not Linux specific, so before trying to troubleshoot an issue affecting the SSD device, you should first check if updates are available for:

*   The [SSD's firmware](#Firmware)
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

To disable NCQ on boot, add `libata.force=noncq` to the kernel command line in the [bootloader](/index.php/Bootloader "Bootloader") configuration. To disable NCQ only for disk 0 on port 9 use: `libata.force=9.00:noncq`

Alternatively, you may disable NCQ for a specific drive without rebooting via sysfs:

```
# echo 1 > /sys/block/sdX/device/queue_depth

```

If this (and also updating the firmware) does not resolves the problem or cause other issues, then [file a bug report](/index.php/Reporting_bug_guidelines "Reporting bug guidelines").

### Resolving SATA power management related errors

Some SSDs (e.g. Transcend MTS400) are failing when SATA Active Link Power Management, [ALPM](https://en.wikipedia.org/wiki/Aggressive_Link_Power_Management "wikipedia:Aggressive Link Power Management"), is enabled. ALPM is disabled by default and enabled by a power saving daemon (e.g. [TLP](/index.php/TLP "TLP"), [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools")).

If you are starting to encounter SATA related errors when using such a daemon, you should try to disable ALPM by setting its state to `max_performance` for both battery and AC powered profiles.

## Firmware

### ADATA

ADATA has a utility available for Linux (i686) on their [support page](http://www.adata.com.tw/index.php?action=ss_main&page=ss_content_driver&lan=en). The link to latest firmware will appear after selecting the model. The latest Linux update utility is packed with firmware and needs to be run as root. One may need to set correct permissions for binary file first.

### Crucial

Crucial provides an option for updating the firmware with an ISO image. These images can be found after selecting the product on their [SSD support page](http://www.crucial.com/usa/en/support-ssd) and downloading the "Manual Boot File."

**Note:** ISO images provided by Crucial does not seem to be hybrid. If you will use just the `dd` command to copy the image to some device, the [MBR](/index.php/MBR "MBR") won't be present, making such device unbootable.

Owners of an M4 Crucial model, may check if a firmware upgrade is needed with `smartctl`.

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

KFU tool is available on the AUR for the Sandforce based drives, [kingston_fw_updater](https://aur.archlinux.org/packages/kingston_fw_updater/).

### Mushkin

The lesser known Mushkin brand solid state drives also use Sandforce controllers, and have a Linux utility (nearly identical to Kingston's) to update the firmware.

### OCZ

OCZ has a [Command Line Online Update Tool (CLOUT)](https://www.ocz.com/us/download/clout) available for Linux. The AUR provides [ocz-ssd-utility](https://aur.archlinux.org/packages/ocz-ssd-utility/), [ocztoolbox](https://aur.archlinux.org/packages/ocztoolbox/) and [oczclout](https://aur.archlinux.org/packages/oczclout/).

### Samsung

Samsung notes that update methods other than using their Magician Software are "not supported," but it is possible. The Magician Software can be used to make a USB drive bootable with the firmware update. Samsung provides pre-made [bootable ISO images](https://www.samsung.com/semiconductor/minisite/ssd/download/tools.html) that can be used to update the firmware. Another option is to use Samsung's [samsung_magician](https://aur.archlinux.org/packages/samsung_magician/), which is available in the AUR. Magician only supports Samsung-branded SSDs; those manufactured by Samsung for OEMs (e.g., Lenovo) are not supported.

**Note:** Samsung does not make it obvious at all that they actually provide these. They seem to have 4 different firmware update pages, and each references different ways of doing things.

Users preferring to run the firmware update from a live USB created under Linux (without using Samsung's "Magician" software under Microsoft Windows) can refer to [this post](http://fomori.org/blog/?p=933) for reference.

#### Native upgrade

Alternatively, the firmware can be upgraded natively, without making a bootable USB stick, as shown below.

First visit the [Samsung downloads page](https://www.samsung.com/semiconductor/minisite/ssd/download/tools.html) and download the latest firmware for Windows, which is available as a disk image. In the following, `Samsung_SSD_840_EVO_EXT0DB6Q.iso` is used as an example file name, adjust it accordingly.

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

SanDisk Extreme SSD [Firmware Release notes](https://kb.sandisk.com/app/answers/detail/a_id/10127) and [Manual Firmware update version R211](https://kb.sandisk.com/app/answers/detail/a_id/10476)

SanDisk Ultra SSD [Firmware release notes](https://kb.sandisk.com/app/answers/detail/a_id/10192) and [Manual Firmware update version 365A13F0](https://kb.sandisk.com/app/answers/detail/a_id/10477)

## See also

*   [Discussion on Reddit about installing Arch on an SSD](https://www.reddit.com/r/archlinux/comments/rkwjm/what_should_i_keep_in_mind_when_installing_on_ssd/)
*   [Re: Varying Leafsize and Nodesize in Btrfs](http://permalink.gmane.org/gmane.comp.file-systems.btrfs/19446)
*   [Re: SSD alignment and Btrfs sector size](http://thread.gmane.org/gmane.comp.file-systems.btrfs/19650/focus=19667)
*   [Erase Block (Alignment) Misinformation?](https://forums.anandtech.com/threads/erase-block-alignment-misinformation.2266113/)
*   [Is alignment to erase block size needed for modern SSD's?](https://superuser.com/questions/492084/is-alignment-to-erase-block-size-needed-for-modern-ssds)
*   [Btrfs support for efficient SSD operation (data blocks alignment)](http://thread.gmane.org/gmane.comp.file-systems.btrfs/15646)
*   [SSD, Erase Block Size & LVM: PV on raw device, Alignment](https://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)