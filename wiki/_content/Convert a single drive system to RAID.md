# Convert a single drive system to RAID

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This guide shows how to convert a functional single-drive system to a [RAID](/index.php/RAID "RAID") 1 setup after adding a second drive, without the need to temporarily store the data on a third drive. The procedure can also be adapted, simplifying it, to the conversion of simple non-root partitions, and to other RAID levels.

**Tip:** You may consider using [Raider](https://aur.archlinux.org/packages/Raider/)<sup><small>AUR</small></sup>, which can convert a single disk into a RAID system with a two-pass command.

## Contents

*   [1 Scenario](#Scenario)
*   [2 Prepare the new disk](#Prepare_the_new_disk)
    *   [2.1 Partition the disk](#Partition_the_disk)
    *   [2.2 Create the RAID device](#Create_the_RAID_device)
    *   [2.3 Make file system](#Make_file_system)
*   [3 Copy the data on the array](#Copy_the_data_on_the_array)
*   [4 Boot on the new disk](#Boot_on_the_new_disk)
    *   [4.1 Update the boot loader](#Update_the_boot_loader)
        *   [4.1.1 GRUB legacy](#GRUB_legacy)
        *   [4.1.2 GRUB](#GRUB)
    *   [4.2 Alter fstab](#Alter_fstab)
    *   [4.3 Rebuild the initramfs](#Rebuild_the_initramfs)
        *   [4.3.1 Chroot into the RAID system](#Chroot_into_the_RAID_system)
        *   [4.3.2 Record mdadm's config](#Record_mdadm.27s_config)
        *   [4.3.3 Rebuild initcpio](#Rebuild_initcpio)
    *   [4.4 Install the boot loader on the RAID array](#Install_the_boot_loader_on_the_RAID_array)
        *   [4.4.1 GRUB Legacy](#GRUB_Legacy_2)
    *   [4.5 Verify success](#Verify_success)
*   [5 Add original disk to array](#Add_original_disk_to_array)
    *   [5.1 Partition original disk](#Partition_original_disk)
    *   [5.2 Add disk partition to array](#Add_disk_partition_to_array)
*   [6 See also](#See_also)

## Scenario

This example assumes that the pre-existing disk is `/dev/sda`, which contains only one partition, `/dev/sda1`, used for the whole system. The newly-added disk is `/dev/sdb`.

**Warning:** Backup important data before proceeding.

## Prepare the new disk

### Partition the disk

The first step is creating the [partition](/index.php/Partition "Partition") on the new disk, `/dev/sdb1`, that will be used as the mirror for the RAID array. In general, in this step it is not needed to recreate the exact partitioning scheme of the pre-existing drive; RAID can even be configured on whole disks, and [partitions](https://raid.wiki.kernel.org/index.php/Partitioning_RAID_/_LVM_on_RAID#Partitions%20on%20a%20RAID%20device) or [logical volumes](/index.php/LVM "LVM") created later.

Make sure that the partition type is set as `FD`. See [RAID#Prepare the Devices](/index.php/RAID#Prepare_the_Devices "RAID") and [RAID#Create the Partition Table (GPT)](/index.php/RAID#Create_the_Partition_Table_.28GPT.29 "RAID") for more information.

### Create the RAID device

Next, create the RAID array in a degraded state, using only the new disk. Note how the `missing` keyword is specified for the first device: this will be added later.

```
# mdadm --create /dev/md0 --level=1 --raid-devices=2 missing /dev/sdb1

```

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Why would mdadm not see /dev/sdbX? And is rebooting the only way to fix it? (Discuss in [Talk:Convert a single drive system to RAID#](https://wiki.archlinux.org/index.php/Talk:Convert_a_single_drive_system_to_RAID))

Note: If the above command causes mdadm to say "no such device /dev/sdb2", then reboot, and run the command again.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Check if Syslinux doesn't support version 1.2 yet. (Discuss in [Talk:Convert a single drive system to RAID#](https://wiki.archlinux.org/index.php/Talk:Convert_a_single_drive_system_to_RAID))

If you want to use Syslinux, you need to specify --metadata=1.0 (for the boot partition) [as of Sept. 2011](http://www.zytor.com/pipermail/syslinux/2011-September/016911.html)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-09-27]</sup>

Make sure the array has been created correctly by checking `/proc/mdstat`:

```
# Personalities : [raid1]                                                                                                                                                                       
md0 : active raid1 sdb1[1]                                                                                                                                                                    
      2930034432 blocks super 1.2 [2/1] [_U]                                                                                                                                                  
      bitmap: 22/22 pages [88KB], 65536KB chunk                                                                                                                                               

unused devices: <none>

```

### Make file system

Create the needed [file system](/index.php/File_system "File system") on the `/dev/md0` device.

## Copy the data on the array

**Warning:** It is recommended to copy the data from another system, such as a live image, to minimize the risk of the data changing in the middle of the copy. Alternatively, switch to single-user mode with `systemctl isolate rescue.target`.

Mount the array:

```
# mkdir /mnt/new-raid
# mount /dev/md0 /mnt/new-raid

```

Now copy the data from `/dev/sda1` to `/mnt/new-raid`, for example using [rsync](/index.php/Full_system_backup_with_rsync "Full system backup with rsync").

## Boot on the new disk

### Update the boot loader

Create a new entry in the boot loader to load the system from the RAID array in the new disk.

#### GRUB legacy

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The following configuration has not been verified after the article has been reorganized on September 2015\. (Discuss in [Talk:Convert a single drive system to RAID#](https://wiki.archlinux.org/index.php/Talk:Convert_a_single_drive_system_to_RAID))

Use your preferred text editor to open `/mnt/new-raid/boot/grub/menu.lst`.

```
--- SNIP ---
default   0
color light-blue/black light-cyan/blue

## fallback
fallback 1

# (0) Arch Linux
title  Arch Linux - Original Disc
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/sda1

# (1) Arch Linux
title  Arch Linux - New RAID
root   (hd1,0)
#kernel /vmlinuz-linux root=/dev/sda1 ro
kernel /vmlinuz-linux root=/dev/md0 md=0,/dev/sda1,/dev/sdb1
--- SNIP ---

```

Notice we added the `fallback` line and duplicated the Arch Linux entry with a different `root` directive on the kernel line.

Also update the "kopt" and "groot" sections, as shown below, if they are in your `/mnt/new-raid/boot/grub/menu.lst` file, because it will make applying distribution kernel updates easier:

```
- # kopt=root=UUID=fbafab1a-18f5-4bb9-9e66-a71c1b00977e ro
+ # kopt=root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1

## default GRUB root device
## e.g. groot=(hd0,0)
- # groot=(hd0,0)
+ # groot=(hd0,1)

```

See [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") for more information.

#### GRUB

Please refer to [GRUB](/index.php/GRUB#Other_Options "GRUB") article.

### Alter fstab

You need to tell fstab on the **new** disk where to find the new device. It is recommended to use [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

 `/mnt/new-raid/etc/fstab` 

```
/dev/md0    /    ext4     defaults   0 1

```

### Rebuild the initramfs

#### Chroot into the RAID system

```
# mount --bind /sys /mnt/new-raid/sys
# mount --bind /proc /mnt/new-raid/proc
# mount --bind /dev /mnt/new-raid/dev
# chroot /mnt/new-raid/

```

If the chroot command gives you an error like `chroot: failed to run command `/bin/zsh': No such file or directory`, then use `chroot /mnt/new-raid/ /bin/bash` instead.

#### Record mdadm's config

[Edit](/index.php/Edit "Edit") `/etc/mdadm.conf` and change the `MAILADDR` line to be your email address, if you want emailed alerts of problems with the RAID 1.

Then save the array configuration with UUIDs to make it easier for the system to find `/dev/md0` at boot. If you do not do this, you can get an `ALERT! /dev/md0 does not exist` error when booting:

```
# mdadm --detail --scan >> /etc/mdadm.conf

```

#### Rebuild initcpio

Follow [RAID#Add mdadm hook to mkinitcpio.conf](/index.php/RAID#Add_mdadm_hook_to_mkinitcpio.conf "RAID").

### Install the boot loader on the RAID array

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Support more boot loaders, simplify. (Discuss in [Talk:Convert a single drive system to RAID#](https://wiki.archlinux.org/index.php/Talk:Convert_a_single_drive_system_to_RAID))

#### GRUB Legacy

Start GRUB:

```
# grub --no-floppy

```

Then we find our two partitions - the current one (hd0,0) (I.e. first disk, first partition), and (hd1,1) (i.e. the partition we just added above, on the second partition of the second drive). Check you get two results here:

```
grub> find /boot/grub/stage1
(hd0,0)
(hd1,1)

```

Then we tell GRUB to assume the new second drive is (hd0), i.e. the first disk in the system (when it is not currently the case). If your first disk fails, however, and you remove it, or you change the order disks are detected in the BIOS so that you can boot from your second disk, then your second disk will become the first disk in the system. The MBR will then be correct, your new second drive will have become your first drive, and you will be able to boot from this disk.

```
grub> device (hd0) /dev/sdb

```

Then we install GRUB onto the MBR of our new second drive. Check that the "partition type" is detected as "0xfd", as shown below, to make sure you have the right partition:

```
grub> root (hd0,1)
 Filesystem type is ext2fs, partition type 0xfd
grub> setup (hd0)
 Checking if "/boot/grub/stage1" exists... yes
 Checking if "/boot/grub/stage2" exists... yes
 Checking if "/boot/grub/e2fs_stage1_5" exists... yes
 Running "embed /boot/grub/e2fs_stage1_5 (hd0)"...  16 sectors are embedded. succeeded
 Running "install /boot/grub/stage1 (hd0) (hd0)1+16 p (hd0,1)/boot/grub/stage2 /boot/grub/grub.conf"... succeeded
 Done
grub> quit

```

### Verify success

Reboot the computer, making sure it boots from the new RAID disk (`/dev/sdb`) and not the original disk (`/dev/sda`). You may need to change the boot device priorities in your BIOS to do this.

Once the boot loader on the **new** disk loads, make sure you select to boot the new system entry you created earlier.

Verify you have booted from the RAID array by looking at the output of mount. Also check mdstat again only to confirm which disk is in the array.

 `# mount` 

```
 /dev/md0 on / type ext4 (rw)

```

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The output of the following command has not been verified after the article has been reorganized on September 2015\. (Discuss in [Talk:Convert a single drive system to RAID#](https://wiki.archlinux.org/index.php/Talk:Convert_a_single_drive_system_to_RAID))

 `# cat /proc/mdstat` 

```
 Personalities : [linear] [raid0] [raid1] [raid5] [multipath] [raid6] [raid10]
 md0 : active raid1 sdb1[1]
      40064 blocks [2/1] [_U]

 unused devices: <none>

```

If the system boots fine, and the output of the above commands is correct, then you are running off the degraded RAID array, as expected.

## Add original disk to array

### Partition original disk

Copy the partition table from `/dev/sdb` (newly implemented RAID disk) to `/dev/sda` (second disk we are adding to the array) so that both disks have exactly the same layout:

```
# sfdisk -d /dev/sdb | sfdisk /dev/sda

```

Alternative method: this will output the `/dev/sdb` partition layout to a file, then it is used as input for partitioning `/dev/sda`.

```
# sfdisk -d /dev/sdb > raidinfo-partitions.sdb
# sfdisk /dev/sda < raidinfo-partitions.sdb

```

Verify that the partitioning is identical:

```
# fdisk -l

```

**Note:** If you get an error when attempting to add the partition to the array:

```
mdadm: /dev/sda1 not large enough to join array

```

You might have seen an earlier warning message when partitioning this disk that the kernel still sees the old disk size: a reboot ought to fix this, then try adding again to the array.

### Add disk partition to array

 `# mdadm /dev/md0 -a /dev/sda1` 

```
 mdadm: hot added /dev/sda1

```

Verify that the RAID array is being rebuilt:

 `# cat /proc/mdstat` 

```
 Personalities : [raid1] 
md0 : active raid1 sda1[2] sdb1[1]
      2930034432 blocks super 1.2 [2/1] [_U]
      [>....................]  recovery =  0.2% (5973824/2930034432) finish=332.5min speed=146528K/sec
      bitmap: 22/22 pages [88KB], 65536KB chunk

unused devices: <none>

```

## See also

*   [Convert running system to RAID 5](http://askubuntu.com/questions/252795/convert-running-system-to-raid-5) — Example using RAID 5

Retrieved from "[https://wiki.archlinux.org/index.php?title=Convert_a_single_drive_system_to_RAID&oldid=416026](https://wiki.archlinux.org/index.php?title=Convert_a_single_drive_system_to_RAID&oldid=416026)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")

Hidden categories:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages with dead links](/index.php/Category:Pages_with_dead_links "Category:Pages with dead links")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")