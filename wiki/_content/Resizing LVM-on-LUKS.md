# Resizing LVM-on-LUKS

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [LVM#Shrink logical volume](/index.php/LVM#Shrink_logical_volume "LVM").**

**Notes:** This howto only aggregates information from other articles (thus duplicating it) for a too specific case: if some explanations are clearer here, they should be merged into [LVM#Shrink logical volume](/index.php/LVM#Shrink_logical_volume "LVM"), and then the little remaining wrapping part about dm-crypt should be merged into [Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") with a link to [LVM#Shrink logical volume](/index.php/LVM#Shrink_logical_volume "LVM") for the LVM resizing. (Discuss in [Talk:Resizing LVM-on-LUKS#](https://wiki.archlinux.org/index.php/Talk:Resizing_LVM-on-LUKS))

This article follows the process of resizing and shrinking an LVM-on-LUKS-on-GPT partition, such that an extra (plain) partition can be added in the unused space cleared up on the end of the hard drive.

## Contents

*   [1 Method](#Method)
*   [2 Process](#Process)
    *   [2.1 Boot and setup](#Boot_and_setup)
    *   [2.2 Resize filesystem](#Resize_filesystem)
    *   [2.3 Resize LVM logical volume](#Resize_LVM_logical_volume)
    *   [2.4 Resize LVM physical Volume](#Resize_LVM_physical_Volume)
    *   [2.5 Resize LUKS volume](#Resize_LUKS_volume)
    *   [2.6 Resize the partition](#Resize_the_partition)
    *   [2.7 Create a new partition](#Create_a_new_partition)
    *   [2.8 Recover the logical volume buffer](#Recover_the_logical_volume_buffer)

## Method

We do all the resizes from the innermost partition to the outermost on, keeping 1G buffers along the way on each step. It is possible to keep smaller buffers, but that should be done carefully, especially where there are manual calculations.

The filesystem we work on will have the following strucure:

```
# lsblk
NAME                MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                   8:0    0 111.8G  0 disk  
├─sda1                8:1    0    99M  0 part  /boot
└─sda2                8:2    0 111.7G  0 part  
  └─vgroup          254:0    0 111.7G  0 crypt 
    ├─vgroup-lvroot 254:1    0    30G  0 lvm   /
    └─vgroup-lvhome 254:2    0  81.7G  0 lvm   /home

```

The goal is to clear up unused space and create a new partition, `sda3`, without any data loss. All filesystems are assumed to be `ext4`.

The entire process should run from a live USB Arch system to avoid any filesystem corruption.

## Process

**Warning:** **Do not** run any of this code by copy-pasting, you need to adapt all these commands to your specific setup.

**Note:** It is highly recommended to write out the exact transition plan so that at each step you know exactly which partition size you're going to need.

### Boot and setup

Boot into your live [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media").

Decrypt the LUKS volume:

```
# cryptsetup luksOpen /dev/sda2 cryptdisk

```

### Resize filesystem

First we need to resize the innermost filesystem itself. In this case, we only resize the last and largest filesystem and shave off 11GB:

```
# resize2fs -p /dev/mapper/vgroup-lvhome 70g

```

**Note:** `resize2fs` works only on ext{2,3,4} filesystems.

You can run a `fsck` just to make sure nothing broke:

```
# e2fsck -f /dev/mapper/vgroup-lvhome

```

### Resize LVM logical volume

We now resize the logical volume, keeping a safety buffer from the filesystem (reduce only by 10GB, not 11GB):

```
# lvreduce -L -10G /dev/vgroup/lvhome

```

### Resize LVM physical Volume

Again we keep a large safety buffer:

```
# pvresize --setphysicalvolumesize 102G /dev/mapper/cryptdisk

```

### Resize LUKS volume

First, we need to calculate how many sectors we'll be shaving off by comparing to the existing number of sectors:

```
# cryptsetup status cryptdisk

```

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** What is the reason for the safety buffer? The cryptsetup resize itself does not require one. (Discuss in [Talk:Resizing LVM-on-LUKS#](https://wiki.archlinux.org/index.php/Talk:Resizing_LVM-on-LUKS))

**Note:** To calculate how many sectors we want to shrink to, use a simple formula: `NEW_SECTORS = EXISTING_SECTORS * NEW_SIZE_IN_GB / EXISTING_SIZE_IN_GB`. Remember to take a safety buffer here as well.

Resize the LUKS volume:

```
# cryptsetup -b $NEW_SECTOR_COUNT resize cryptdisk

```

### Resize the partition

Use parted to actually resize the partition:

```
# parted /dev/sda

```

Select `resizepart 2` and give the partition a new size based on your calculations.

### Create a new partition

This is a GPT disk so run:

```
# gdisk /dev/sda

```

and add the new partition on the remaining free space. If all went well there should be no data loss.

### Recover the logical volume buffer

At the end of this process, the filesystem of your `lvhome` volume will be 1GB smaller than the underlying logical volume.

In order to regain this 1GB, first verify that the filesystem is clean:

```
# e2fsck -f /dev/vgroup/lvhome

```

Then resize the filesystem to occupy the whole logical volume:

```
# resize2fs /dev/vgroup/lvhome

```

If all went fine, your `lvhome` filesystem is now as large as your logical volume itself.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Resizing_LVM-on-LUKS&oldid=390800](https://wiki.archlinux.org/index.php?title=Resizing_LVM-on-LUKS&oldid=390800)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [File systems](/index.php/Category:File_systems "Category:File systems")