[Solid State Drives](https://en.wikipedia.org/wiki/Solid_State_Drive "w:Solid State Drive") (SSDs) are not PnP devices. Special considerations such as partition alignment, choice of file system, TRIM support, etc. are needed to set up SSDs for optimal performance. This article attempts to capture referenced, key learnings to enable users to get the most out of SSDs under Linux. Users are encouraged to read this article in its entirety before acting on recommendations.

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
*   [3 See also](#See_also)

## Usage

### TRIM

Most SSDs support the [ATA_TRIM command](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") for sustained long-term performance and wear-leveling. For a performance benchmark before and after filling an SSD with data, see [[1]](http://www.techspot.com/review/737-ocz-vector-150-ssd/page9.html).

As of Linux kernel version 3.8 onwards, the following filesystems support TRIM: [Ext4](/index.php/Ext4 "Ext4"), [Btrfs](/index.php/Btrfs "Btrfs"), [JFS](/index.php/JFS "JFS") [[2]](http://www.phoronix.com/scan.php?page=news_item&px=MTE5ODY), [XFS](/index.php/XFS "XFS") [[3]](http://xfs.org/index.php/FITRIM/discard), [F2FS](/index.php/F2FS "F2FS"), VFAT.

As of [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) version 2015.3.14, TRIM is supported for [NTFS](/index.php/NTFS "NTFS") filesystem too [[4]](http://permalink.gmane.org/gmane.comp.file-systems.ntfs-3g.devel/1101).

| File system | Continuous TRIM
(`discard` option) | Periodic TRIM
(*fstrim*) |
| [Ext3](/index.php/Ext3 "Ext3") | No | ? |
| [Ext4](/index.php/Ext4 "Ext4") | Yes | Yes |
| [Btrfs](/index.php/Btrfs "Btrfs") | Yes | Yes |
| [JFS](/index.php/JFS "JFS") | Yes | Yes |
| [XFS](/index.php/XFS "XFS") | Yes | Yes |
| [F2FS](/index.php/F2FS "F2FS") | Yes | Yes |
| VFAT | Yes | No |
| [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) | No | Yes |

To verify TRIM support, run:

```
# hdparm -I /dev/sda | grep TRIM
        *    Data Set Management TRIM supported (limit 1 block)

```

**Note:** There are different types of TRIM support defined by the specification. Hence, the output may differ depending what the drive supports. See [w:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "w:TRIM") for more information.

See also [File systems](/index.php/File_systems "File systems") and [w:List_of_file_systems#File_systems_optimized_for_flash_memory.2C_solid_state_media](https://en.wikipedia.org/wiki/List_of_file_systems#File_systems_optimized_for_flash_memory.2C_solid_state_media "w:List of file systems").

#### Periodic TRIM

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package provides `fstrim.service` and `fstrim.timer` [systemd](/index.php/Systemd "Systemd") unit files. [Enabling](/index.php/Enabling "Enabling") the timer will activate the service weekly, which will then trim all mounted filesystems on devices that support the *discard* operation.

The timer relies on the timestamp of `/var/lib/systemd/timers/stamp-fstrim.timer` (which it will create upon first invocation) to know whether a week has elapsed since it last ran. Therefore there is no need to worry about too frequent invocations, in an *anacron*-like fashion.

To query the units activity and status, see [journalctl](/index.php/Journalctl "Journalctl"). To change the periodicity of the timer or the command run, [edit](/index.php/Edit "Edit") the provided unit files.

#### Continuous TRIM

**Warning:** Users need to be certain that their SSD supports TRIM before attempting to mount a partition with the `discard` flag. Data loss can occur otherwise! Unfortunately, there are wide quality gaps of SSD's bios' to perform continuous TRIM, which is also why using the `discard` mount flag is [recommended against](http://thread.gmane.org/gmane.comp.file-systems.ext4/41974) generally by filesystem developer Theodore Ts'o. If in doubt about your hardware, [#Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim) instead. Also be aware of other [shortcomings](https://en.wikipedia.org/wiki/Trim_(computing)#Shortcomings "wikipedia:Trim (computing)"), most importantly that "TRIM commands [have been linked](https://blog.algolia.com/when-solid-state-drives-are-not-that-solid/) to serious data corruption in several devices, most notably Samsung 8* series." After the data corruption [had been confirmed](https://github.com/torvalds/linux/blob/e64f638483a21105c7ce330d543fa1f1c35b5bc7/drivers/ata/libata-core.c#L4109-L4286), the Linux kernel blacklisted queued TRIM command execution for a number of [popular devices](https://github.com/torvalds/linux/blob/v4.5/drivers/ata/libata-core.c#L4223) as of March 28, 2016\. For affected Samsung 8 series drives, the drive incorrectly identifies it supports queued TRIM even though it does not. Firmware updated EVO 850's and newer EVO 840's or 840's with updated firmware and newer drives in the 8* series are all affected. Read [trim does not work with Samsung 840 EVO after firmware update](https://bugs.launchpad.net/ubuntu/+source/fstrim/+bug/1449005) on the Ubuntu bug tracker for more information.

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

**Note:** Enabling this option will "issue discards to a logical volumes's underlying physical volume(s) when the logical volume is no longer using the physical volumes' space (e.g. *lvremove*, *lvreduce*, etc)" (see `man lvm.conf` and/or inline comments in `/etc/lvm/lvm.conf`). As such it does not seem to be required for "regular" TRIM requests (file deletions inside a filesystem) to be functional.

#### dm-crypt

**Warning:** The discard option allows discard requests to be passed through the encrypted block device. This improves performance on SSD storage but has security implications. See [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") for more information.

For non-root filesystems, configure `/etc/crypttab` to include `discard` in the list of options for encrypted block devices located on a SSD (see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")).

For the root filesystem, follow the instructions from [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") to add the right kernel parameter to the bootloader configuration.

### Maximizing performance

Follow the tips in [Maximizing performance#Storage devices](/index.php/Maximizing_performance#Storage_devices "Maximizing performance") to maximize the performance of your drives.

### Security

#### Hdparm shows "frozen" state

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