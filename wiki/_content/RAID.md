# RAID

Related articles

*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [Installing with Fake RAID](/index.php/Installing_with_Fake_RAID "Installing with Fake RAID")
*   [Convert a single drive system to RAID](/index.php/Convert_a_single_drive_system_to_RAID "Convert a single drive system to RAID")
*   [ZFS](/index.php/ZFS "ZFS")
*   [Experimenting with ZFS](/index.php/Experimenting_with_ZFS "Experimenting with ZFS")
*   [Swap#Striping](/index.php/Swap#Striping "Swap")

This article explains what RAID is and how to create/manage a software RAID array using mdadm.

## Contents

*   [1 Introduction](#Introduction)
    *   [1.1 Standard RAID levels](#Standard_RAID_levels)
    *   [1.2 Nested RAID levels](#Nested_RAID_levels)
    *   [1.3 RAID level comparison](#RAID_level_comparison)
*   [2 Implementation](#Implementation)
    *   [2.1 Which type of RAID do I have?](#Which_type_of_RAID_do_I_have.3F)
*   [3 Setup](#Setup)
    *   [3.1 Prepare the Devices](#Prepare_the_Devices)
    *   [3.2 Create the Partition Table (GPT)](#Create_the_Partition_Table_.28GPT.29)
        *   [3.2.1 Partitions Types for MBR](#Partitions_Types_for_MBR)
    *   [3.3 Build the Array](#Build_the_Array)
    *   [3.4 Update configuration file](#Update_configuration_file)
    *   [3.5 Assemble the Array](#Assemble_the_Array)
    *   [3.6 Format the RAID Filesystem](#Format_the_RAID_Filesystem)
        *   [3.6.1 Calculating the Stride and Stripe-width](#Calculating_the_Stride_and_Stripe-width)
            *   [3.6.1.1 Example 1\. RAID0](#Example_1._RAID0)
            *   [3.6.1.2 Example 2\. RAID5](#Example_2._RAID5)
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
        *   [6.3.1 For RAID0 Arrays](#For_RAID0_Arrays)
    *   [6.4 Change sync speed limits](#Change_sync_speed_limits)
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

## Introduction

See also [Wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID").

Redundant Array of Independent Disks (RAID) is a storage technology that combines multiple disk drive components (typically disk drives or partitions thereof) into a logical unit. Depending on the RAID implementation, this logical unit can be a file system or an additional transparent layer that can hold several partitions. Data is distributed across the drives in one of several ways called "RAID levels", depending on the level of redundancy and performance required. The RAID level chosen can thus prevent data loss in the event of a hard disk failure, increase performance or be a combination of both.

Despite redundancy implied by most RAID levels, RAID does not guarantee that data is safe. A RAID will not protect data if there is a fire, the computer is stolen or multiple hard drives fail at once. Furthermore, installing a system with RAID is a complex process that may destroy data.

**Warning:** Therefore, be sure [to back up](/index.php/Backup_programs "Backup programs") all data before proceeding.

**Note:** Users considering a RAID array for data storage/redundancy should also consider RAIDZ which is implemented via [ZFS](/index.php/ZFS "ZFS"), a more modern and powerful alternative to software RAID.

### Standard RAID levels

There are many different [levels of RAID](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels"), please find hereafter the most commonly used ones.

NaN

### Nested RAID levels

NaN

### RAID level comparison

| RAID level | Data redundancy | Physical drive utilization | Read performance | Write performance | Min drives |
| **0** | **No** | 100% | nX

**Best**

 | nX

**Best**

 | 2 |
| **1** | Yes | 50% | nX (theoretically)

1X (in practice)

 | 1X | 2 |
| **5** | Yes | 67% - 94% | (n−1)X

**Superior**

 | (n−1)X

**Superior**

 | 3 |
| **6** | Yes | 50% - 88% | (n−2)X | (n−2)X | 4 |
| **10** | Yes | 50% | nX (theoretically) | (n/2)X | 4 |

* Where _n_ is standing for the number of dedicated disks.

## Implementation

The RAID devices can be managed in different ways:

NaN

NaN

NaN

### Which type of RAID do I have?

Since software RAID is implemented by the user, the type of RAID is easily known to the user.

However, discerning between FakeRAID and true hardware RAID can be more difficult. As stated, manufacturers often incorrectly distinguish these two types of RAID and false advertising is always possible. The best solution in this instance is to run the `lspci` command and looking through the output to find the RAID controller. Then do a search to see what information can be located about the RAID controller. Hardware RAID controllers appear in this list, but FakeRAID implementations do not. Also, true hardware RAID controller are often rather expensive (~$400+), so if someone customized the system, then it is very likely that choosing a hardware RAID setup made a very noticeable change in the computer's price.

## Setup

Install [mdadm](https://www.archlinux.org/packages/?name=mdadm) from the [official repositories](/index.php/Official_repositories "Official repositories"). _mdadm_ is used for administering pure software RAID using plain block devices: the underlying hardware does not provides any RAID logic, just a supply of disks. _mdadm_ will work with any collection of block devices. Even if unusual. For example, one can thus make a RAID array from a collection of thumb drives.

### Prepare the Devices

**Warning:** These steps erase everything on a device, so type carefully!

To prevent possible issues each device in the RAID should be [securely wiped](/index.php/Securely_wipe_disk "Securely wipe disk"). If the device is being reused or re-purposed from an existing array, erase any old RAID configuration information:

```
# mdadm --zero-superblock /dev/<drive>

```

or if a particular partition on a drive is to be deleted:

```
# mdadm --zero-superblock /dev/<partition>

```

**Note:** Zapping a partition's superblock should not affect the other partitions on the disk.

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

**Tip:** See [Chunks: the hidden key to RAID performance](http://www.zdnet.com/article/chunks-the-hidden-key-to-raid-performance/) for determining a good chunk size.

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

#### Calculating the Stride and Stripe-width

Stride = (chunk size/block size).

**Note:** Arch's default block size for many filesystems is 4096, see: `/etc/mke2fs.conf` for details.

Stripe-width = (# of physical **data** disks * stride).

##### Example 1\. RAID0

Example formatting to ext4 with the correct stripe-width and stride:

*   Hypothetical RAID0 array is composed of 2 physical disks.
*   Chunk size is 64k.
*   Block size is 4k.

Stride = (chunk size/block size). In this example, the math is (64/4) so the stride = 16.

Stripe-width = (# of physical **data** disks * stride). In this example, the math is (2*16) so the stripe-width = 32.

```
# mkfs.ext4 -v -L myarray -m 0.5 -b 4096 -E stride=16,stripe-width=32 /dev/md0

```

##### Example 2\. RAID5

Example formatting to ext4 with the correct stripe-width and stride:

*   Hypothetical RAID5 array is composed of 4 physical disks; 3 data discs and 1 parity disc.
*   Chunk size is 512k.
*   Block size is 4k.

Stride = (chunk size/block size). In this example, the math is 512/4) so the stride = 128.

Stripe-width = (# of physical **data** disks * stride). In this example, the math is (3*128) so the stripe-width = 384.

```
# mkfs.ext4 -v -L myarray -m 0.01 -b 4096 -E stride=128,stripe-width=384 /dev/md0

```

For more on stride and stripe-width, see: [RAID Math](http://wiki.centos.org/HowTos/Disk_Optimization).

## Mounting from a Live CD

Users wanting to mount the RAID partition from a Live CD, use

```
# mdadm --assemble /dev/<disk1> /dev/<disk2> /dev/<disk3> /dev/<disk4>

```

## Installing Arch Linux on RAID

**Note:** The following section is applicable only if the root filesystem resides on the array. Users may skip this section if the array holds a data partition(s).

You should create the RAID array between the [Partitioning](/index.php/Partitioning "Partitioning") and [formatting](/index.php/File_systems#Format_a_device "File systems") steps of the Installation Procedure. Instead of directly formatting a partition to be your root file system, it will be created on a RAID array. Follow the section [#Setup](#Setup) to create the RAID array. Then continue with the installation procedure until the pacstrap step is completed. When using [UEFI boot](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface"), also read [ESP on RAID](/index.php/Unified_Extensible_Firmware_Interface#ESP_on_RAID "Unified Extensible Firmware Interface").

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

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** [Mkinitcpio#Common hooks](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio") also suggests adding `mdmon` to the `BINARIES` section. See also [[1]](https://bbs.archlinux.org/viewtopic.php?id=148947) and [[2]](http://unix.stackexchange.com/questions/57440/cant-remount-local-file-systems-for-read-write-raid1). (Discuss in [Talk:RAID#](https://wiki.archlinux.org/index.php/Talk:RAID))

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

It is a good idea to set up a cron job as root to schedule a periodic scrub. See [raid-check](https://aur.archlinux.org/packages/raid-check/)<sup><small>AUR</small></sup> which can assist with this.

#### RAID1 and RAID10 Notes on Scrubbing

Due to the fact that RAID1 and RAID10 writes in the kernel are unbuffered, an array can have non-0 mismatch counts even when the array is healthy. These non-0 counts will only exist in transient data areas where they don't pose a problem. However, we can't tell the difference between a non-0 count that is just in transient data or a non-0 count that signifies a real problem. This fact is a source of false positives for RAID1 and RAID10 arrays. It is however still recommended to scrub regularly in order to catch and correct any bad sectors that might be present in the devices.

### Removing Devices from an Array

One can remove a device from the array after marking it as faulty:

```
# mdadm --fail /dev/md0 /dev/sdxx

```

Now remove it from the array:

```
# mdadm -r /dev/md0 /dev/sdxx

```

Remove device permanently (for example, to use it individually from now on): Issue the two commands described above then:

```
# mdadm --zero-superblock /dev/sdxx

```

**Warning:** Reusing the removed disk without zeroing the superblock **WILL CAUSE LOSS OF ALL DATA** on the next boot. (After mdadm will try to use it as the part of the raid array). **DO NOT** issue this command on linear or RAID0 arrays or data **LOSS** will occur!

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

#### For RAID0 Arrays

If you get an error like:

```
mdadm: add new device failed for /dev/sdc1 as 2: Invalid argument

```

It may be because you're using RAID0\. The command above will add the new disk as a "spare", but RAID0 doesn't have spares. If you want to add a device to a RAID0 array, you need to "grow" and "add" in the same command:

```
# mdadm --grow /dev/md0 --raid-devices=3 --add /dev/sdc1

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

The _iostat_ utility from [sysstat](https://www.archlinux.org/packages/?name=sysstat) package displays the input/output statistics for devices and partitions.

```
 iostat -dmy 1 /dev/md0
 iostat -dmy 1 # all

```

### Mailing on events

A smtp mail server (sendmail) or at least an email forwarder (ssmtp/msmtp) is required to accomplish this. Perhaps the most simplistic solution is to use [dma](https://aur.archlinux.org/packages/dma/)<sup><small>AUR</small></sup> which is very tiny (installs to 0.08 MiB) and requires no setup.

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

[tiobench](https://aur.archlinux.org/packages/tiobench/)<sup><small>AUR</small></sup> specifically benchmarks these performance improvements by measuring fully-threaded I/O on the disk.

[bonnie++](https://www.archlinux.org/packages/?name=bonnie%2B%2B) tests database type access to one or more files, and creation, reading, and deleting of small files which can simulate the usage of programs such as Squid, INN, or Maildir format e-mail. The enclosed [ZCAV](http://www.coker.com.au/bonnie++/zcav/) program tests the performance of different zones of a hard drive without writing any data to the disk.

`hdparm` should **NOT** be used to benchmark a RAID, because it provides very inconsistent results.

## See also

*   [Software RAID in the new Linux 2.4 kernel, Part 1](http://www.gentoo.org/doc/en/articles/software-raid-p1.xml) and [Part 2](http://www.gentoo.org/doc/en/articles/software-raid-p2.xml) in the Gentoo Linux Docs
*   [Linux RAID wiki entry](http://raid.wiki.kernel.org/index.php/Linux_Raid) on The Linux Kernel Archives
*   [How Bitmaps Work](https://raid.wiki.kernel.org/index.php/Write-intent_bitmap)
*   [Chapter 15: Redundant Array of Independent Disks (RAID)](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Storage_Administration_Guide/ch-raid.html) of Red Hat Enterprise Linux 6 Documentation
*   [Linux-RAID FAQ](http://tldp.org/FAQ/Linux-RAID-FAQ/x37.html) on the Linux Documentation Project
*   [Dell.com Raid Tutorial](http://support.dell.com/support/topics/global.aspx/support/entvideos/raid?c=us&l=en&s=gen) - Interactive Walkthrough of Raid
*   [BAARF](http://www.miracleas.com/BAARF/) including _[Why should I not use RAID 5?](http://www.miracleas.com/BAARF/RAID5_versus_RAID10.txt)_ by Art S. Kagel
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

Retrieved from "[https://wiki.archlinux.org/index.php?title=RAID&oldid=413408](https://wiki.archlinux.org/index.php?title=RAID&oldid=413408)"