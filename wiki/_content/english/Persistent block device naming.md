Related articles

*   [fstab](/index.php/Fstab "Fstab")
*   [udev](/index.php/Udev "Udev")
*   [LVM](/index.php/LVM "LVM")

This article describes how to use persistent names for your [block devices](/index.php/Block_device "Block device"). This has been made possible by the introduction of [udev](/index.php/Udev "Udev") and has some advantages over bus-based naming. If your machine has more than one SATA, SCSI or IDE disk controller, the order in which their corresponding device nodes are added is arbitrary. This may result in device names like `/dev/**sda**` and `/dev/**sdb**` switching around on each boot, culminating in an unbootable system, kernel panic, or a block device disappearing. Persistent naming solves these issues.

**Note:**

*   Persistent naming has limits that are out-of-scope in this article. For example, while [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") may support a method, systemd may impose its own limits (e.g. [FS#42884](https://bugs.archlinux.org/task/42884)) on naming it can process during boot.
*   If you are using [LVM](/index.php/LVM "LVM"), this article is not relevant as LVM takes care of this automatically.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Persistent naming methods](#Persistent_naming_methods)
    *   [1.1 by-label](#by-label)
    *   [1.2 by-uuid](#by-uuid)
    *   [1.3 by-id and by-path](#by-id_and_by-path)
    *   [1.4 by-partlabel](#by-partlabel)
    *   [1.5 by-partuuid](#by-partuuid)
    *   [1.6 Static device names with Udev](#Static_device_names_with_Udev)
*   [2 Using persistent naming](#Using_persistent_naming)
    *   [2.1 fstab](#fstab)
    *   [2.2 Boot managers](#Boot_managers)

## Persistent naming methods

There are four different schemes for persistent naming: [by-label](#by-label), [by-uuid](#by-uuid), [by-id and by-path](#by-id_and_by-path). For those using disks with [GUID Partition Table (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table"), two additional schemes can be used [by-partlabel](#by-partlabel) and [by-partuuid](#by-partuuid). You can also use [static device names by using Udev](#Static_device_names_with_Udev).

**Note:** Beware that [Disk cloning](/index.php/Disk_cloning "Disk cloning") creates two different disks with the same name.

The following sections describes what the different persistent naming methods are and how they are used.

The [lsblk](/index.php/Lsblk "Lsblk") command can be used for viewing graphically the first persistent schemes:

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL  UUID                                 MOUNTPOINT
sda                                                       
├─sda1 vfat          CBB6-24F2                            /boot
├─sda2 ext4   System 0a3407de-014b-458b-b5c1-848e92a327a3 /
├─sda3 ext4   Data   b411dc99-f0a0-4c87-9e05-184977be8539 /home
└─sda4 swap          f9fe0b69-a280-415d-a03a-a32752370dee [SWAP]

```

For those using [GPT](/index.php/GPT "GPT"), use the `blkid` command instead. The latter is more convenient for scripts, but more difficult to read.

 `$ blkid` 
```
/dev/sda1: UUID="CBB6-24F2" TYPE="vfat" PARTLABEL="EFI system partition" PARTUUID="d0d0d110-0a71-4ed6-936a-304969ea36af" 
/dev/sda2: LABEL="System" UUID="0a3407de-014b-458b-b5c1-848e92a327a3" TYPE="ext4" PARTLABEL="GNU/Linux" PARTUUID="98a81274-10f7-40db-872a-03df048df366" 
/dev/sda3: LABEL="Data" UUID="b411dc99-f0a0-4c87-9e05-184977be8539" TYPE="ext4" PARTLABEL="Home" PARTUUID="7280201c-fc5d-40f2-a9b2-466611d3d49e" 
/dev/sda4: UUID="f9fe0b69-a280-415d-a03a-a32752370dee" TYPE="swap" PARTLABEL="Swap" PARTUUID="039b6c1c-7553-4455-9537-1befbc9fbc5b"
```

### by-label

Almost every [filesystem](/index.php/Filesystem "Filesystem") type can have a label. All your partitions that have one are listed in the `/dev/disk/by-label` directory. This directory is created and destroyed dynamically, depending on whether you have partitions with labels attached.

 `$ ls -l /dev/disk/by-label` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 Data -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 System -> ../../sda2

```

The labels of your filesystems can be changed. Following are some methods for changing labels on common filesystems:

	swap 

	`swaplabel -L "*new label*" /dev/*XXX*` using [util-linux](https://www.archlinux.org/packages/?name=util-linux)

	ext2/3/4 

	`e2label /dev/*XXX* "*new label*"` using [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

	btrfs 

	`btrfs filesystem label /dev/*XXX* "*new label*"` using [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

	reiserfs 

	`reiserfstune -l "*new label*" /dev/*XXX*` using [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

	jfs 

	`jfs_tune -L "*new label*" /dev/*XXX*` using [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

	xfs 

	`xfs_admin -L "*new label*" /dev/*XXX*` using [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

	fat/vfat 

	`fatlabel /dev/*XXX* "*new label*"` using [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

	`mlabel -i /dev/*XXX* ::"*new label*"` using [mtools](https://www.archlinux.org/packages/?name=mtools)

	exfat 

	`exfatlabel /dev/*XXX* "*new label*"` using [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

	ntfs 

	`ntfslabel /dev/*XXX* "*new label*"` using [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

	zfs 

	this filesystem does not support `/dev/disk/by-label`, but [#by-partlabel](#by-partlabel) may be used

**Note:**

*   Changing the filesystem label of the root partition has to be done after booting from another partition because it needs to be unmounted first.
*   Labels have to be unambiguous to prevent any possible conflicts.
*   Labels can be up to 16 characters long.
*   Since the label is a property of the filesystem, it is not suitable for addressing a single RAID device persistently.
*   When using encrypted containers with [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), the labels of filesystems inside of containers are not available while the container is locked/encrypted.

### by-uuid

[UUID](https://en.wikipedia.org/wiki/UUID "wikipedia:UUID") is a mechanism to give each [filesystem](/index.php/Filesystem "Filesystem") a unique identifier. These identifiers are generated by filesystem utilities (e.g. `mkfs.*`) when the partition gets formatted and are designed so that collisions are unlikely. All GNU/Linux filesystems (including swap and LUKS headers of raw encrypted devices) support UUID. FAT, exFAT and NTFS filesystems do not support UUID, but are still listed in `/dev/disk/by-uuid/` with a shorter UID (unique identifier):

 `$ ls -l /dev/disk/by-uuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 0a3407de-014b-458b-b5c1-848e92a327a3 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 b411dc99-f0a0-4c87-9e05-184977be8539 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 CBB6-24F2 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 f9fe0b69-a280-415d-a03a-a32752370dee -> ../../sda4

```

The advantage of using the UUID method is that it is much less likely that name collisions occur than with labels. Further, it is generated automatically on creation of the filesystem. It will, for example, stay unique even if the device is plugged into another system (which may perhaps have a device with the same label).

The disadvantage is that UUIDs make long code lines hard to read and break formatting in many configuration files (e.g. [fstab](/index.php/Fstab "Fstab") or [crypttab](/index.php/Crypttab "Crypttab")). Also every time a partition is resized or reformatted a new UUID is generated and configs have to get adjusted (manually).

**Tip:** In case your swap partition does not have an UUID assigned, you will need to reset the swap partition using [mkswap](/index.php/Swap#Swap_partition "Swap") utility.

### by-id and by-path

`by-id` creates a unique name depending on the hardware serial number, `by-path` depending on the shortest physical path (according to sysfs). Both contain strings to indicate which subsystem they belong to (i.e. `pci-` for `by-path`, and `ata-` for `by-id`), so they are linked to the hardware controlling the device. This implies different levels of persistence: the `by-path` will already change when the device is plugged into a different port of the controller, the `by-id` will change when the device is plugged into a port of a hardware controller subject to another subsystem. [[1]](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/persistent_naming.html) Thus, both are not suitable to achieve persistent naming tolerant to hardware changes.

However, both provide important information to find a particular device in a large hardware infrastructure. For example, if you do not manually assign persistent labels (`by-label` or `by-partlabel`) and keep a directory with hardware port usage, `by-id` and `by-path` can be used to find a particular device.[[2]](http://linuxshellaccount.blogspot.in/2008/09/how-to-easily-find-wwns-of-qlogic-hba.html) [[3]](http://www.linuxquestions.org/questions/linux-server-73/how-to-find-wwn-for-dev-sdc-917269/)

`by-id` also creates [World Wide Name](https://en.wikipedia.org/wiki/World_Wide_Name "wikipedia:World Wide Name") links of storage devices that support it. Unlike other `by-id` links, WWNs are fully persistent and will not change depending on the used subsystem.

 `$ ls -l /dev/disk/by-id/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470 -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part4 -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 wwn-0x60015ee0000b237f-part4 -> ../../sda4

```
 `$ ls -l /dev/disk/by-path/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1 -> ../../sda
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part1 -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part2 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part3 -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 pci-0000:00:1f.2-ata-1-part4 -> ../../sda4

```

### by-partlabel

**Note:** This method only concerns disks with [GUID Partition Table (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table").

Partition labels can be defined in the header of the partition entry on GPT disks.

See also [Wikipedia:GUID Partition Table#Partition entries (LBA 2-33)](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries_.28LBA_2-33.29 "wikipedia:GUID Partition Table").

This method is very similar to the [filesystem labels](#by-label), excepted that the dynamic directory is `/dev/disk/by-partlabel`.

 `ls -l /dev/disk/by-partlabel/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 EFI\x20system\x20partition -> ../../sda1
lrwxrwxrwx 1 root root 10 May 27 23:31 GNU\x2fLinux -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 Home -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 Swap -> ../../sda4

```

**Note:**

*   GPT partition labels also have to be different to avoid conflicts. To change your partition label, you can use [gdisk](/index.php/Gdisk "Gdisk") or the ncurses-based version [cgdisk](/index.php/Cgdisk "Cgdisk"). Both are available from the [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) package. See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").
*   According to the specification, GPT partition labels can be up to 72 characters long.

### by-partuuid

**Note:** This method only concerns disks with [GUID Partition Table (GPT)](/index.php/GUID_Partition_Table "GUID Partition Table").

Like [GPT partition labels](#by-partlabel), GPT partition UUIDs are defined in the partition entry on GPT disks. See also [Wikipedia:GUID Partition Table#Partition entries](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries "wikipedia:GUID Partition Table").

The dynamic directory is similar to other methods and, like [filesystem UUIDs](#by-uuid), using UUIDs is preferred over labels.

 `ls -l /dev/disk/by-partuuid/` 
```
total 0
lrwxrwxrwx 1 root root 10 May 27 23:31 039b6c1c-7553-4455-9537-1befbc9fbc5b -> ../../sda4
lrwxrwxrwx 1 root root 10 May 27 23:31 7280201c-fc5d-40f2-a9b2-466611d3d49e -> ../../sda3
lrwxrwxrwx 1 root root 10 May 27 23:31 98a81274-10f7-40db-872a-03df048df366 -> ../../sda2
lrwxrwxrwx 1 root root 10 May 27 23:31 d0d0d110-0a71-4ed6-936a-304969ea36af -> ../../sda1

```

### Static device names with Udev

See [udev#Setting static device names](/index.php/Udev#Setting_static_device_names "Udev").

## Using persistent naming

There are various applications that can be configured using persistent naming. Following are some examples of how to configure them.

### fstab

See the main article: [fstab#Identifying filesystems](/index.php/Fstab#Identifying_filesystems "Fstab").

### Boot managers

To use persistent names in the [boot manager (boot loader)](/index.php/Boot_loader "Boot loader"), the following prerequisites must be met. On a standard installation following the installation guide both prerequisites are met.

*   You are using a [mkinitcpio](/index.php/Mkinitcpio#Configuration "Mkinitcpio") initial RAM disk image
*   You have udev enabled in `/etc/mkinitcpio.conf`

The location of the root filesystem is given by the parameter `root` on the kernel commandline. The kernel commandline is configured from the bootloader, see [Kernel parameters#Configuration](/index.php/Kernel_parameters#Configuration "Kernel parameters"). To change to persistent device naming, only change the parameters which specify block devices, e.g. `root` and `resume`, while leaving other parameters as is. Various naming schemes are supported:

Persistent device naming using label and the `LABEL=` format, in this example `System` is the LABEL of the root file system.

```
root=LABEL=System

```

Persistent device naming using UUID and the `UUID=` format, in this example `0a3407de-014b-458b-b5c1-848e92a327a3` is the UUID of the root file system.

```
root=UUID=0a3407de-014b-458b-b5c1-848e92a327a3

```

Persistent device naming using disk id and the `/dev` path format, in this example `wwn-0x60015ee0000b237f-part2` is the id of the root partition.

```
root=/dev/disk/by-id/wwn-0x60015ee0000b237f-part2

```

Persistent device naming using GPT partition UUID and the `PARTUUID=` format, in this example `98a81274-10f7-40db-872a-03df048df366` is the PARTUUID of the root partition.

```
root=PARTUUID=98a81274-10f7-40db-872a-03df048df366

```

Persistent device naming using GPT partition label and the `PARTLABEL=` format, in this example `GNU/Linux` is the PARTLABEL of the root partition.

```
root="PARTLABEL=GNU/Linux"

```