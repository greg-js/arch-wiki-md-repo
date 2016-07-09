See [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") for the main article.

## Contents

*   [1 TRIM](#TRIM)
    *   [1.1 Verify TRIM support](#Verify_TRIM_support)
    *   [1.2 Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim)
    *   [1.3 Enable continuous TRIM by mount flag](#Enable_continuous_TRIM_by_mount_flag)
    *   [1.4 Enable TRIM for LVM](#Enable_TRIM_for_LVM)
    *   [1.5 Enable TRIM for dm-crypt](#Enable_TRIM_for_dm-crypt)
    *   [1.6 I/O scheduler](#I.2FO_scheduler)
    *   [1.7 Swap space on SSDs](#Swap_space_on_SSDs)
*   [2 SSD security](#SSD_security)
    *   [2.1 Hdparm shows "frozen" state](#Hdparm_shows_.22frozen.22_state)
    *   [2.2 SSD memory cell clearing](#SSD_memory_cell_clearing)
    *   [2.3 Hardware encryption](#Hardware_encryption)
*   [3 Reduce disk reads/writes](#Reduce_disk_reads.2Fwrites)
    *   [3.1 Show disk writes](#Show_disk_writes)
    *   [3.2 Relocate partitions](#Relocate_partitions)
    *   [3.3 noatime mount option](#noatime_mount_option)
    *   [3.4 Move frequently used files to RAM](#Move_frequently_used_files_to_RAM)
        *   [3.4.1 Browser profiles](#Browser_profiles)
        *   [3.4.2 Others](#Others)
    *   [3.5 Compiling in tmpfs](#Compiling_in_tmpfs)
    *   [3.6 Disabling journaling on the filesystem](#Disabling_journaling_on_the_filesystem)

## TRIM

Most SSDs support the [ATA_TRIM command](https://en.wikipedia.org/wiki/TRIM "wikipedia:TRIM") for sustained long-term performance and wear-leveling. For a performance benchmark before and after filling an SSD with data, see [[1]](http://www.techspot.com/review/737-ocz-vector-150-ssd/page9.html).

As of Linux kernel version 3.8 onwards, the following filesystems support TRIM: [Ext4](/index.php/Ext4 "Ext4"), [Btrfs](/index.php/Btrfs "Btrfs"), [JFS](/index.php/JFS "JFS"), [XFS](/index.php/XFS "XFS"), [F2FS](/index.php/F2FS "F2FS"), VFAT.

As of [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) version 2015.3.14, TRIM is supported for [NTFS](/index.php/NTFS "NTFS") filesystem too [[2]](http://permalink.gmane.org/gmane.comp.file-systems.ntfs-3g.devel/1101).

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

### Verify TRIM support

```
# hdparm -I /dev/sda | grep TRIM
        *    Data Set Management TRIM supported (limit 1 block)

```

Note that there are different types of TRIM support defined by the specification. Hence, the output may differ depending what the drive supports. See [wikipedia:TRIM#ATA](https://en.wikipedia.org/wiki/TRIM#ATA "wikipedia:TRIM") for more information.

### Apply periodic TRIM via fstrim

The [util-linux](https://www.archlinux.org/packages/?name=util-linux) package (part of [base](https://www.archlinux.org/groups/x86_64/base/) and [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/)) provides `fstrim.service` and `fstrim.timer` [systemd](/index.php/Systemd "Systemd") unit files. [Enabling](/index.php/Enabling "Enabling") the timer will activate the service weekly, which will then trim all mounted filesystems on devices that support the discard operation.

The timer relies on the timestamp of `/var/lib/systemd/timers/stamp-fstrim.timer` (which it will create upon first invocation) to know whether a week has elapsed since it last ran. Therefore there is no need to worry about too frequent invocations, in an *anacron*-like fashion.

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

### Enable continuous TRIM by mount flag

**Warning:** Users need to be certain that their SSD supports TRIM before attempting to mount a partition with the `discard` flag. Data loss can occur otherwise! Unfortunately, there are wide quality gaps of SSD's bios' to perform continuous TRIM, which is also why using the `discard` mount flag is [recommended against](http://thread.gmane.org/gmane.comp.file-systems.ext4/41974) generally by filesystem developer Theodore Ts'o. If in doubt about your hardware, [#Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim) instead. Also be aware of other [shortcomings](https://en.wikipedia.org/wiki/Trim_(computing)#Shortcomings "wikipedia:Trim (computing)"), most importantly that "TRIM commands [have been linked](https://blog.algolia.com/when-solid-state-drives-are-not-that-solid/) to serious data corruption in several devices, most notably Samsung 8* series." After the data corruption [had been confirmed](https://github.com/torvalds/linux/blob/e64f638483a21105c7ce330d543fa1f1c35b5bc7/drivers/ata/libata-core.c#L4109-L4286), the Linux kernel blacklisted queued TRIM command execution for a number of [popular devices](https://github.com/torvalds/linux/blob/v4.5/drivers/ata/libata-core.c#L4223) as of March 28, 2016\. Read [Samsung Finds, Fixes Bug In Linux Trim Code](http://linux.slashdot.org/story/15/07/30/1814200/samsung-finds-fixes-bug-in-linux-trim-code) on Slashdot for more recent updates.

Using the `discard` option for a mount in `/etc/fstab` enables continuous TRIM in device operations:

```
/dev/sda2  /boot       ext4  defaults,noatime,**discard**   0  2
/dev/sda1  /boot/efi   vfat  defaults,noatime,**discard**   0  2
/dev/sda3  /           ext4  defaults,noatime,**discard**   0  2

```

The main benefit of continuous TRIM is speed; an SSD can perform more efficient [garbage collection](http://arstechnica.com/gadgets/2015/04/ask-ars-my-ssd-does-garbage-collection-so-i-dont-need-trim-right/). However, results vary and particularly earlier SSD generations may also show just the opposite effect. Also for this reason, some distributions decided against using it (e.g. Ubuntu: see [this article](http://www.phoronix.com/scan.php?page=news_item&px=MTUxOTY) and the [related blueprint](https://blueprints.launchpad.net/ubuntu/+spec/core-1311-ssd-trimming)).

**Note:**

*   There is no need for the `discard` flag if you run `fstrim` periodically.
*   Before SATA 3.1, TRIM commands are synchronous and will block all I/O while running. This may cause short freezes while this happens, for example during a filesystem sync. You may not want to use `discard` in that case but [#Apply periodic TRIM via fstrim](#Apply_periodic_TRIM_via_fstrim) instead. One way to check your SATA version is with `smartctl --info /dev/sd*X*`.

On the ext4 filesystem, the `discard` flag can also be set as a [default mount option](/index.php/Access_Control_Lists#Enabling_ACL "Access Control Lists") using *tune2fs*:

```
# tune2fs -o discard /dev/sd**XY**

```

Using the default mount options instead of an entry in `/etc/fstab` is useful for external drives, because such partition will be mounted with the default options also on other machines. There is no need to edit `/etc/fstab` on every machine.

**Note:** The default mount options are not listed in `/proc/mounts`.

### Enable TRIM for LVM

Change the value of `issue_discards` option from 0 to 1 in `/etc/lvm/lvm.conf`.

**Note:** Enabling this option will "issue discards to a logical volumes's underlying physical volume(s) when the logical volume is no longer using the physical volumes' space (e.g. lvremove, lvreduce, etc)" (see `man lvm.conf` and/or inline comments in `/etc/lvm/lvm.conf`). As such it does not seem to be required for "regular" TRIM requests (file deletions inside a filesystem) to be functional.

### Enable TRIM for dm-crypt

**Warning:** The discard option allows discard requests to be passed through the encrypted block device. This improves performance on SSD storage but has security implications. See [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") for more information.

For non-root filesystems, configure `/etc/crypttab` to include `discard` in the list of options for encrypted block devices located on a SSD (see [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration")).

For the root filesystem, follow the instructions from [Dm-crypt/TRIM support for SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") to add the right kernel parameter to the bootloader configuration.

### I/O scheduler

See [Maximizing performance#Tuning IO schedulers](/index.php/Maximizing_performance#Tuning_IO_schedulers "Maximizing performance").

### Swap space on SSDs

One can place a swap partition on an SSD. A recommended tweak for SSDs using a swap partition is to reduce the [swappiness](/index.php/Swappiness "Swappiness") of the system to some very low value (for example `1`), and thus avoiding writes to swap.

## SSD security

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

If you intend to set a password to a "frozen" device yourself, a motherboard BIOS with support for it is required. A lot of notebooks have support, because it is required for [hardware encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption"), but support may not be trivial for a desktop/server board. For the Intel DH67CL/BL motherboard, for example, the motherboard has to be set to "maintenance mode" by a physical jumper to access the settings (see [[3]](http://sstahlman.blogspot.in/2014/07/hardware-fde-with-intel-ssd-330-on.html?showComment=1411193181867#c4579383928221016762), [[4]](https://communities.intel.com/message/251978#251978)).

**Warning:** Do not try to change the above **lock** security settings with `hdparm` unless you know exactly what you are doing.

If you intend to erase the SSD, see [Securely wipe disk#hdparm](/index.php/Securely_wipe_disk#hdparm "Securely wipe disk") and [#SSD memory cell clearing](#SSD_memory_cell_clearing) below.

### SSD memory cell clearing

On occasion, users may wish to completely reset an SSD's cells to the same virgin state they were at the time the device was installed thus restoring it to its [factory default write performance](http://www.anandtech.com/storage/showdoc.aspx?i=3531&p=8). Write performance is known to degrade over time even on SSDs with native TRIM support. TRIM only safeguards against file deletes, not replacements such as an incremental save.

The reset is easily accomplished in a three step procedure denoted on the [SSD memory cell clearing](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") wiki article. If the reason for the reset is to wipe data, you may not want to rely on the SSD bios to perform it securely. See [Securely wipe disk#Flash memory](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk") for further information and examples to perform a wipe.

### Hardware encryption

As noted in [#Hdparm shows frozen state](#Hdparm_shows_.22frozen.22_state) setting a password for a storage device (SSD/HDD) in the BIOS may also initialize the hardware encryption of devices supporting it. If the device also conforms to the OPAL standard, this may also be achieved without a respective BIOS feature to set the passphrase, see [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives").

## Reduce disk reads/writes

**Note:** A 32GB SSD with a mediocre 10x write amplification factor, a standard 10000 write/erase cycle, and **10GB of data written per day**, would get an **8 years life expectancy**. It gets better with bigger SSDs and modern controllers with less write amplification. Also compare [[5]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update) when considering whether any particular strategy to limit disk writes is actually needed.

### Show disk writes

The [iotop](https://www.archlinux.org/packages/?name=iotop) package can sort by disk writes, and show how much and how frequently programs are writing to the disk. It can be run in batch mode, instead of the default interactive mode using the `-b` option. `-o` is used to show only processes actually doing I/O, and `-qqq` is to suppress column names and I/O summary. See `man iotop` for more options.

```
# iotop -boqqq

```

### Relocate partitions

The `/var` partition contains files which are frequently read or written to. On systems with both an SSD and an HDD, this partition could be relocated to a magnetic disc on the system, rather than on the SSD itself.

### noatime mount option

[fstab atime option](/index.php/Fstab#atime_options "Fstab") `noatime` or `relatime` removes the need to write to the file system for files which are simplfy being read. See [Fstab](/index.php/Fstab "Fstab") for details.

### Move frequently used files to RAM

#### Browser profiles

One can mount browser profile(s) such as chromium, firefox, opera, etc. into RAM via tmpfs, and use rsync to keep them synced with HDD-based backups.

The AUR contains several packages to automate this process, for example [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/).

#### Others

For the same reasons a browser's profile can be relocated to RAM, so can highly used directories such as `/srv/http` (if running a web server). A sister project to [profile-sync-daemon](https://aur.archlinux.org/packages/profile-sync-daemon/) is [anything-sync-daemon](https://aur.archlinux.org/packages/anything-sync-daemon/), which allows users to define **any** directory to sync to RAM using the same underlying logic and safe guards.

### Compiling in tmpfs

See [Makepkg#Improving compile times](/index.php/Makepkg#Improving_compile_times "Makepkg").

### Disabling journaling on the filesystem

**Warning:** Using a filesystem with journaling disabled is data loss as a result of an ungraceful dismount (i.e. post power failure, kernel lockup, etc.). With modern SSDs, [Ted Tso](http://tytso.livejournal.com/61830.html) advocates that journaling can be enabled with minimal added read/write cycles under most circumstances.

Using a journaling filesystem such as ext4 on an SSD **without** a journal is an option to decrease read/writes. With *ext4*, this is done by enabling the `nointegrity` option. See [Fstab](/index.php/Fstab "Fstab").