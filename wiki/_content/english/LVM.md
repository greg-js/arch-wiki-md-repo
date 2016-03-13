From [Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)"):

	LVM is a [logical volume manager](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management") for the [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel"); it manages disk drives and similar mass-storage devices.

## Contents

*   [1 LVM Building Blocks](#LVM_Building_Blocks)
*   [2 Advantages](#Advantages)
*   [3 Disadvantages](#Disadvantages)
*   [4 Installing Arch Linux on LVM](#Installing_Arch_Linux_on_LVM)
    *   [4.1 Create partitions](#Create_partitions)
    *   [4.2 Create physical volumes](#Create_physical_volumes)
    *   [4.3 Create volume group](#Create_volume_group)
    *   [4.4 Create in one step](#Create_in_one_step)
    *   [4.5 Create logical volumes](#Create_logical_volumes)
    *   [4.6 Create file systems and mount logical volumes](#Create_file_systems_and_mount_logical_volumes)
    *   [4.7 Add lvm2 hook to mkinitcpio.conf for root on LVM](#Add_lvm2_hook_to_mkinitcpio.conf_for_root_on_LVM)
    *   [4.8 Special preparations for root on thinly-provisioned volume](#Special_preparations_for_root_on_thinly-provisioned_volume)
    *   [4.9 Kernel options](#Kernel_options)
*   [5 Volume operations](#Volume_operations)
    *   [5.1 Advanced options](#Advanced_options)
    *   [5.2 Resizing volumes](#Resizing_volumes)
        *   [5.2.1 Physical volumes](#Physical_volumes)
            *   [5.2.1.1 Growing](#Growing)
            *   [5.2.1.2 Shrinking](#Shrinking)
                *   [5.2.1.2.1 Move physical extents](#Move_physical_extents)
                *   [5.2.1.2.2 Resize physical volume](#Resize_physical_volume)
                *   [5.2.1.2.3 Resize partition](#Resize_partition)
        *   [5.2.2 Logical volumes](#Logical_volumes)
            *   [5.2.2.1 Growing or shrinking with lvresize](#Growing_or_shrinking_with_lvresize)
            *   [5.2.2.2 Resizing the file system separately](#Resizing_the_file_system_separately)
    *   [5.3 Remove logical volume](#Remove_logical_volume)
    *   [5.4 Add physical volume to a volume group](#Add_physical_volume_to_a_volume_group)
    *   [5.5 Remove partition from a volume group](#Remove_partition_from_a_volume_group)
    *   [5.6 Deactivate volume group](#Deactivate_volume_group)
    *   [5.7 Snapshots](#Snapshots)
        *   [5.7.1 Introduction](#Introduction)
        *   [5.7.2 Configuration](#Configuration)
    *   [5.8 LVM Cache (lvmcache)](#LVM_Cache_.28lvmcache.29)
        *   [5.8.1 Create](#Create)
        *   [5.8.2 Remove](#Remove)
        *   [5.8.3 Root device on a cached LV](#Root_device_on_a_cached_LV)
*   [6 Graphical Configuration](#Graphical_Configuration)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Changes that could be required due to changes in the Arch-Linux defaults](#Changes_that_could_be_required_due_to_changes_in_the_Arch-Linux_defaults)
    *   [7.2 LVM commands do not work](#LVM_commands_do_not_work)
    *   [7.3 Logical Volumes do not show up](#Logical_Volumes_do_not_show_up)
    *   [7.4 LVM on removable media](#LVM_on_removable_media)
    *   [7.5 Resizing a contiguous logical volume fails](#Resizing_a_contiguous_logical_volume_fails)
    *   [7.6 Command "grub-mkconfig" reports "unknown filesystem" errors](#Command_.22grub-mkconfig.22_reports_.22unknown_filesystem.22_errors)
*   [8 See also](#See_also)

### LVM Building Blocks

Logical Volume Management utilizes the kernel's [device-mapper](http://sources.redhat.com/dm/) feature to provide a system of partitions independent of underlying disk layout. With LVM you abstract your storage and have "virtual partitions", making [extending/shrinking](#Resizing_volumes) easier (subject to potential filesystem limitations).

Virtual partitions allow addition and removal without worry of whether you have enough contiguous space on a particular disk, getting caught up fdisking a disk in use (and wondering whether the kernel is using the old or new partition table), or, having to move other partitions out of the way. This is strictly an ease-of-management solution: LVM adds no security.

Basic building blocks of LVM:

*   **Physical volume (PV)**: Partition on hard disk (or even the disk itself or loopback file) on which you can have volume groups. It has a special header and is divided into physical extents. Think of physical volumes as big building blocks used to build your hard drive.
*   **Volume group (VG)**: Group of physical volumes used as a storage volume (as one disk). They contain logical volumes. Think of volume groups as hard drives.
*   **Logical volume (LV)**: A "virtual/logical partition" that resides in a volume group and is composed of physical extents. Think of logical volumes as normal partitions.
*   **Physical extent (PE)**: The smallest size in the physical volume that can be assigned to a logical volume (default 4MiB). Think of physical extents as parts of disks that can be allocated to any partition.

Example:

```
**Physical disks**

  Disk1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partition1 50GB (Physical volume) |Partition2 80GB (Physical volume)     |
    |/dev/sda1                         |/dev/sda2                             |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

  Disk2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partition1 120GB (Physical volume)                 |
    |/dev/sdb1                                          |
    | _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ __ _ _|

```

```
**LVM logical volumes**

  Volume Group1 (/dev/MyStorage/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ 
    |Logical volume1 15GB  |Logical volume2 35GB      |Logical volume3 200GB               |
    |/dev/MyStorage/rootvol|/dev/MyStorage/homevol    |/dev/MyStorage/mediavol             |
    |_ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

```

### Advantages

LVM gives you more flexibility than just using normal hard drive partitions:

*   Use any number of disks as one big disk.
*   Have logical volumes stretched over several disks.
*   Create small logical volumes and resize them "dynamically" as they get filled up.
*   Resize logical volumes regardless of their order on disk. It does not depend on the position of the LV within VG, there is no need to ensure surrounding available space.
*   Resize/create/delete logical and physical volumes online. File systems on them still need to be resized, but some (such as ext4) support online resizing.
*   Online/live migration of LV being used by services to different disks without having to restart services.
*   Snapshots allow you to backup a frozen copy of the file system, while keeping service downtime to a minimum.
*   Support for various device-mapper targets, including transparent filesystem encryption and caching of frequently used data.

### Disadvantages

*   Additional steps in setting up the system, more complicated.

## Installing Arch Linux on LVM

You should create your LVM Volumes between the [partitioning](/index.php/Partitioning "Partitioning") and [formatting](/index.php/File_systems#Create_a_filesystem "File systems") steps of the [installation procedure](/index.php/Installation_guide "Installation guide"). Instead of directly formatting a partition to be your root file system, the file system will be created inside a logical volume (LV).

Make sure the [lvm2](https://www.archlinux.org/packages/?name=lvm2) package is [installed](/index.php/Pacman "Pacman").

Quick overview:

*   Create partition(s) where your PV(s) will reside. Set the partition type to 'Linux LVM', which is 8e if you use MBR, 8e00 for GPT.
*   Create your physical volumes (PVs). If you have one disk it is best to just create one PV in one large partition. If you have multiple disks you can create partitions on each of them and create a PV on each partition.
*   Create your volume group (VG) and add all PVs to it.
*   Create logical volumes (LVs) inside that VG.
*   Continue with “Format the partitions” step of [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").
*   When you reach the “Create initial ramdisk environment” step in the Beginners Guide, add the `lvm` hook to `/etc/mkinitcpio.conf` (see below for details).

**Warning:** `/boot` cannot reside in LVM when using [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), which does not support LVM. [GRUB](/index.php/GRUB "GRUB") users do not have this limitation. If you need to use GRUB Legacy, you must create a separate `/boot` partition and format it directly.

### Create partitions

If LVM has to be set on the entire disk, there is no need to create any partitions.

Otherwise, [partition](/index.php/Partition "Partition") the device as required before configuring LVM.

### Create physical volumes

To list all your devices capable of being used as a physical volume:

```
# lvmdiskscan

```

**Warning:** Make sure you target the correct device, or below commands will result in data loss!

Create a physical volume on them:

```
# pvcreate *DEVICE*

```

This command creates a header on each device so it can be used for LVM. As defined in [#LVM Building Blocks](#LVM_Building_Blocks), *DEVICE* can be a disk (e.g. `/dev/sda`), a partition (e.g. `/dev/sda2`) or a loop back device. For example:

```
# pvcreate /dev/sda2

```

You can track created physical volumes with:

```
# pvdisplay

```

**Note:** If using a SSD without partitioning it first, use `pvcreate --dataalignment 1m /dev/sda` (for erase block size < 1MiB), see e.g. [here](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

### Create volume group

The next step is to create a volume group on this physical volume.

First you need to create a volume group on one of the physical volumes:

```
# vgcreate <*volume_group*> <*physical_volume*>

```

For example:

```
# vgcreate VolGroup00 /dev/sda2

```

Then add to it all other physical volumes you want to have in it:

```
# vgextend <*volume_group*> <*physical_volume*>
# vgextend <*volume_group*> <*another_physical_volume*>
# ...

```

For example:

```
# vgextend VolGroup00 /dev/sdb1
# vgextend VolGroup00 /dev/sdc

```

You can track how your volume group grows with:

```
# vgdisplay

```

**Note:** You can create more than one volume group if you need to, but then you will not have all your storage presented as one disk.

### Create in one step

LVM allows you to combine the creation of a volume group and the physical volumes in one easy step. For example, to create the group VolGroup00 with the three devices mentioned above, you can run:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb1 /dev/sdc

```

This command will first set up the three partitions as physical volumes (if necessary) and then create the volume group with the three volumes. The command will warn you it detects an existing filesystem on any of the devices.

### Create logical volumes

Now we need to create logical volumes on this volume group. You create a logical volume with the next command by giving the name of a new logical volume, its size, and the volume group it will live on:

```
# lvcreate -L <*size*> <*volume_group*> -n <*logical_volume*>

```

For example:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

This will create a logical volume that you can access later with `/dev/mapper/Volgroup00-lvolhome` or `/dev/VolGroup00/lvolhome`. Same as with the volume groups, you can use any name you want for your logical volume when creating it.

You can also specify one or more physical volumes to restrict where LVM allocates the data. For example, you may wish to create a logical volume for the root filesystem on your small SSD, and your home volume on a slower mechanical drive. Simply add the physical volume devices to the command line, for example:

```
# lvcreate -L 10G VolGroup00 -n lvolhome /dev/sdc1

```

If you want to fill all the free space left on a volume group, use the next command:

```
# lvcreate -l 100%FREE  <*volume_group*> -n <*logical_volume*>

```

You can track created logical volumes with:

```
# lvdisplay

```

**Note:** You may need to load the *device-mapper* kernel module (**modprobe dm_mod**) for the above commands to succeed.

**Tip:** You can start out with relatively small logical volumes and expand them later if needed. For simplicity, leave some free space in the volume group so there is room for expansion.

### Create file systems and mount logical volumes

Your logical volumes should now be located in `/dev/mapper/` and `/dev/*YourVolumeGroupName*`. If you cannot find them, use the next commands to bring up the module for creating device nodes and to make volume groups available:

```
# modprobe dm_mod
# vgscan
# vgchange -ay

```

Now you can create file systems on logical volumes and mount them as normal partitions (if you are installing Arch linux, refer to [mounting the partitions](/index.php/Beginners%27_guide#Mount_the_partitions "Beginners' guide") for additional details):

```
# mkfs.<*fstype*> /dev/mapper/<*volume_group*>-<*logical_volume*>
# mount /dev/mapper/<*volume_group*>-<*logical_volume*> /<*mountpoint*>

```

For example:

```
# mkfs.ext4 /dev/mapper/VolGroup00-lvolhome
# mount /dev/mapper/VolGroup00-lvolhome /home

```

**Warning:** When choosing mountpoints, just select your newly created logical volumes (use: `/dev/mapper/Volgroup00-lvolhome`). Do **not** select the actual partitions on which logical volumes were created (do not use: `/dev/sda2`).

### Add lvm2 hook to mkinitcpio.conf for root on LVM

In case your root filesystem is on LVM, you will need to make sure the `udev` and `lvm2` [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hooks are enabled.

`udev` is there by default. Edit the file and insert `lvm2` between `block` and `filesystems` like so:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev ... block **lvm2** filesystems"` 

Afterwards, you can continue in normal installation instructions with the [create an initial ramdisk](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") step.

**Tip:** The `lvm2` hook is installed by [lvm2](https://www.archlinux.org/packages/?name=lvm2), not [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio). If you are running *mkinitcpio* in an *arch-chroot* for a new installation, [lvm2](https://www.archlinux.org/packages/?name=lvm2) must be installed inside the *arch-chroot* for *mkinitcpio* to find the `lvm2` hook. If [lvm2](https://www.archlinux.org/packages/?name=lvm2) only exists outside the *arch-chroot*, *mkinitcpio* will output `Error: Hook 'lvm2' cannot be found`.

**Warning:** When using the `systemd` mkinitcpio hook you should use the `sd-lvm2` hook instead of the `lvm2` hook. Otherwise your system might not boot. See [Mkinitcpio#Common_hooks](/index.php/Mkinitcpio#Common_hooks "Mkinitcpio")

### Special preparations for root on thinly-provisioned volume

If your root device is on a thinly-provisioned LVM volume (as may be needed by [snapper](/index.php/Snapper "Snapper") if you don't trust [btrfs](/index.php/Btrfs "Btrfs")), then some more preparations are needed.

First, `mkinitcpio` by default does not include modules and binaries needed for thin provisioning. Adjust the configuration file to compensate:

 `/etc/mkinitcpio.conf` 
```
MODULES="... **dm-thin-pool** ..."
BINARIES="**/usr/bin/thin_check /usr/bin/pdata_tools** ..."
```

LVM only calls `thin_check` while booting, but if the check fails, you will need other commands provided by `pdata_tools` for recovery.

Second, with a large number of snapshots, `thin_check` runs for a long enough time so that waiting for the root device times out. To compensate, add the `rootdelay=60` kernel boot parameter to your boot loader configuration.

### Kernel options

If the root file system resides in a logical volume, the `root=` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") must be pointed to the mapped device, e.g `/dev/mapper/*vg-name*-*lv-name*`.

You may also need `dolvm`.

## Volume operations

### Advanced options

If you need monitoring (needed for snapshots) you can enable lvmetad. For this set `use_lvmetad = 1` in `/etc/lvm/lvm.conf`. This is the default by now.

You can restrict the volumes that are activated automatically by setting the `auto_activation_volume_list` in `/etc/lvm/lvm.conf`. If in doubt, leave this option commented out.

### Resizing volumes

#### Physical volumes

After extending or prior to reducing the size of a device that has a physical volume on it, you need to grow or shrink the PV using `pvresize`.

##### Growing

To expand the PV on `/dev/sda1` after enlarging the [partition](/index.php/Partition "Partition"), run:

```
# pvresize /dev/sda1

```

This will automatically detect the new size of the device and extend the PV to its maximum.

**Note:** This command can be done while the volume is online.

##### Shrinking

To shrink a physical volume prior to reducing its underlying device, add the `--setphysicalvolumesize *size*` parameters to the command, *e.g.*:

```
# pvresize --setphysicalvolumesize 40G /dev/sda1

```

The above command may leave you with this error:

```
 /dev/sda1: cannot resize to 25599 extents as later ones are allocated.
 0 physical volume(s) resized / 1 physical volume(s) not resized

```

Indeed `pvresize` will refuse to shrink a PV if it has allocated extents after where its new end would be. One needs to run [pvmove](#Move_physical_extents) beforehand to relocate these elsewhere in the volume group if there is sufficient free space.

###### Move physical extents

Before moving free extents to the end of the volume, one must run `# pvdisplay -v -m` to see physical segments. In the below example, there is one physical volume on `/dev/sdd1`, one volume group `vg1` and one logical volume `backup`.

 `# pvdisplay -v -m` 
```
    Finding all volume groups.
    Using physical volume(s) on command line.
  --- Physical volume ---
  PV Name               /dev/sdd1
  VG Name               vg1
  PV Size               1.52 TiB / not usable 1.97 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              399669
  Free PE               153600
  Allocated PE          246069
  PV UUID               MR9J0X-zQB4-wi3k-EnaV-5ksf-hN1P-Jkm5mW

  --- Physical Segments ---
  Physical extent 0 to 153600:
    FREE
  Physical extent 153601 to 307199:
    Logical volume	/dev/vg1/backup
    Logical extents	1 to 153599
  Physical extent 307200 to 307200:
    FREE
  Physical extent 307201 to 399668:
    Logical volume	/dev/vg1/backup
    Logical extents	153601 to 246068
```

One can observe FREE space are split across the volume. To shrink the physical volume, we must first move all used segments to the beginning.

Here, the first free segment is from 0 to 153600 and leaves us with 153601 free extents. We can now move this segment number from the last physical extent to the first extent. The command will thus be:

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92466` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100,0%
```

**Note:**

*   this command tells to move 92468 (399668-307200) PE **from** the last segment **to** the first segment. This is possible as first segment enclosed FREE 153600 PE, which can contains the 92467 moved PE.
*   the `--alloc anywhere` option is used as we move PE inside the same partition. In case of different partitions, the command would look something like this: `# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999`
*   the move can takes long (one/two hours) in case of large size. It can be a good idea to run this command in a [Tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen") session. Any unwanted stop of the process can be fatal.
*   once the operation is complete, run [Fsck](/index.php/Fsck "Fsck") to make sure your file system is valid.

###### Resize physical volume

Once all your free physical segments are on the last physical extent, run `# vgdisplay` and see your free PE.

Then you can now run again the command:

```
# pvresize --setphysicalvolumesize *size* *PhysicalVolume*

```

See the result:

 `# pvs` 
```
  PV         VG   Fmt  Attr PSize    PFree 
  /dev/sdd1  vg1  lvm2 a--     1t     500g

```

###### Resize partition

Last, you need to shrink the partition with your favorite [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning").

#### Logical volumes

**Note:** *lvresize* provides more or less the same options as the specialized `lvextend` and `lvreduce` commands, while allowing to do both types of operation. Notwithstanding this, all those utilities offer a `-r, --resizefs` option which allows to resize the file system together with the LV using `fsadm(8)` (*ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") supported). Therefore it may be easier to simply use `lvresize` for both operations and use `--resizefs` to simplify things a bit, except if you have specific needs or want full control over the process.

##### Growing or shrinking with lvresize

**Warning:** While enlarging a file system can often be done on-line (*i.e.* while it is mounted), even for the root partition, shrinking will nearly always require to first unmount the file system so as to prevent data loss. Make sure your FS supports what you are trying to do.

Extend logical volume *lv1* within volume group *vg1* by 2GB *without* touching its file system:

```
# lvresize -L +2G vg1/lv1

```

Reduce `vg1/lv1` of 500MB *without* resizing its file system (make sure it is [already shrunk](#Resizing_the_file_system_separately) in that case):

```
# lvresize -L -500M vg1/lv1

```

Set `vg1/lv1` to 15GB and resize its file sytem *all at once*:

```
# lvresize -L 15G -r vg1/lv1

```

**Note:** Only *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") [file systems](/index.php/File_systems "File systems") are supported. If different look for the [appropriate utility](/index.php/File_systems#Arch_Linux_support "File systems").

If you want to fill all the free space on a volume group, use the following command:

```
# lvresize -l +100%FREE *vg*/*lv*

```

See `man lvresize` for more detailed options.

##### Resizing the file system separately

If not using the `-r, --resizefs` option to `lv{resize,extend,reduce}` or using a file system unspported by `fsadm(8)` ([Btrfs](/index.php/Btrfs "Btrfs"), [ZFS](/index.php/ZFS "ZFS")...), you need to manually resize the FS before shrinking the LV or after expanding it.

**Warning:** Not all file systems support resizing without loss of data and/or resizing online.

For example with and ext2/ext3/ext4 file system:

```
# resize2fs *vg*/*lv*

```

will expand the FS to the maximum size of the underlying LV, while

```
# resize2fs -M *vg*/*lv*

```

will shrink it to its minimum size. To resize it to a specified size, use:

```
# resize2fs *vg*/*lv* *NewSize*

```

### Remove logical volume

**Warning:** Before you remove a logical volume, make sure to move all data that you want to keep somewhere else; otherwise, it will be lost!

First, find out the name of the logical volume you want to remove. You can get a list of all logical volumes with:

```
# lvs

```

Next, look up the mountpoint of the chosen logical volume:

```
$ lsblk

```

Then unmount the filesystem on the logical volume:

```
# umount /<*mountpoint*>

```

Finally, remove the logical volume:

```
# lvremove <*volume_group*>/<*logical_volume*>

```

For example:

```
# lvremove VolGroup00/lvolhome

```

Confirm by typing in `y`.

Update `/etc/fstab` as necessary.

You can verify the removal of the logical volume by typing `lvs` as root again (see first step of this section).

### Add physical volume to a volume group

You first create a new physical volume on the block device you wish to use, then extend your volume group

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1
```

This of course will increase the total number of physical extents on your volume group, which can be allocated by logical volumes as you see fit.

**Note:** It is considered good form to have a [partition table](/index.php/Partitioning "Partitioning") on your storage medium below LVM. Use the appropriate type code: `8e` for MBR, and `8e00` for GPT partitions.

### Remove partition from a volume group

If you created a logical volume on the partition, [remove](#Remove_logical_volume) it first.

All of the data on that partition needs to be moved to another partition. Fortunately, LVM makes this easy:

```
# pvmove /dev/sdb1

```

If you want to have the data on a specific physical volume, specify that as the second argument to `pvmove`:

```
# pvmove /dev/sdb1 /dev/sdf1

```

Then the physical volume needs to be removed from the volume group:

```
# vgreduce myVg /dev/sdb1

```

Or remove all empty physical volumes:

```
# vgreduce --all vg0

```

And lastly, if you want to use the partition for something else, and want to avoid LVM thinking that the partition is a physical volume:

```
# pvremove /dev/sdb1

```

### Deactivate volume group

Just invoke

```
# vgchange -a n my_volume_group

```

This will deactivate the volume group and allow you to unmount the container it is stored in.

### Snapshots

#### Introduction

LVM allows you to take a snapshot of your system in a much more efficient way than a traditional backup. It does this efficiently by using a COW (copy-on-write) policy. The initial snapshot you take simply contains hard-links to the inodes of your actual data. So long as your data remains unchanged, the snapshot merely contains its inode pointers and not the data itself. Whenever you modify a file or directory that the snapshot points to, LVM automatically clones the data, the old copy referenced by the snapshot, and the new copy referenced by your active system. Thus, you can snapshot a system with 35GB of data using just 2GB of free space so long as you modify less than 2GB (on both the original and snapshot).

#### Configuration

You create snapshot logical volumes just like normal ones.

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

With that volume, you may modify less than 100M of data, before the snapshot volume fills up.

Reverting the modified 'pv' logical volume to the state when the 'snap01' snapshot was taken can be done with

`# lvconvert --merge /dev/vg0/snap01`

In case the origin logical volume is active, merging will occur on the next reboot.(Merging can be done even from a LiveCD)

The snapshot will no longer exist after merging.

Also multiple snapshots can be taken and each one can be merged with the origin logical volume at will.

The snapshot can be mounted and backed up with **dd** or **tar**. The size of the backup file done with **dd** will be the size of the files residing on the snapshot volume. To restore just create a snapshot, mount it, and write or extract the backup to it. And then merge it with the origin.

It is important to have the *dm_snapshot* module listed in the MODULES variable of `/etc/mkinitcpio.conf`, otherwise the system will not boot. If you do this on an already installed system, make sure to rebuild the image with

```
# mkinitcpio -g /boot/initramfs-linux.img

```

Todo: scripts to automate snapshots of root before updates, to rollback... updating `menu.lst` to boot snapshots (separate article?)

snapshots are primarily used to provide a frozen copy of a file system to make backups; a backup taking two hours provides a more consistent image of the file system than directly backing up the partition.

See [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") for automating the creation of clean root file system snapshots during system startup for backup and rollback.

[Dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") and [Dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system").

If you have LVM volumes not activated via the [initramfs](/index.php/Initramfs "Initramfs"), [enable](#Using_units) the **lvm-monitoring** service, which is provided by the [lvm2](https://www.archlinux.org/packages/?name=lvm2) package.

### LVM Cache (lvmcache)

From [man](http://man7.org/linux/man-pages/man7/lvmcache.7.html):

	*The cache logical volume type uses a small and fast LV to improve the performance of a large and slow LV. It does this by storing the frequently used blocks on the faster LV. LVM refers to the small fast LV as a cache pool LV. The large slow LV is called the origin LV. Due to requirements from dm-cache (the kernel driver), LVM further splits the cache pool LV into two devices - the cache data LV and cache metadata LV. The cache data LV is where copies of data blocks are kept from the origin LV to increase speed. The cache metadata LV holds the accounting information that specifies where data blocks are stored (e.g. on the origin LV or on the cache data LV). Users should be familiar with these LVs if they wish to create the best and most robust cached logical volumes. All of these associated LVs must be in the same VG.*

#### Create

The fast method is creating a PV (if necessary) on the fast disk and add it to the existing volume group:

```
# vgextend dataVG /dev/sdx

```

Create a cache pool with automatic meta data on sdb, and convert the existing logical volume (dataLV) to a cached volume, all in one step:

```
# lvcreate –type cache -L 19.9G -n dataLV_cachepool dataVG/dataLV /dev/sdx

```

#### Remove

If you ever need to undo the one step creation operation above:

```
# lvconvert --uncache dataVG/dataLV

```

This commits any pending writes still in the cache back to the origin LV, then deletes the cache. Other options are available and described in [man](http://man7.org/linux/man-pages/man7/lvmcache.7.html).

#### Root device on a cached LV

If your root device is on a cached LV, you must prepare `mkinitcpio` to include required modules:

 `/etc/mkinitcpio.conf`  `MODULES="... **dm-cache dm_cache_mq dm_cache_smq** ..."` 

**dm_cache_smq** is only if you run a linux kernel superior or equal to 4.2

If you fail to do so, you'll end up in a rescue shell early in the boot process. A way to boot again is to remove the cache as described above (`lvconvert` may not be available from the rescue shell, but is accessible from the `lvm` tool). Before leaving the rescue shell, activate the LV.

## Graphical Configuration

There is no "official" GUI tool for managing LVM volumes, but [system-config-lvm](https://aur.archlinux.org/packages/system-config-lvm/) covers most of the common operations, and provides simple visualizations of volume state. It can automatically resize many file systems when resizing logical volumes.

system-config-lvm requires root access, so the .desktop launcher will not work, and you must launch it with sudo. It does not support thin provisioning pools, and will crash on start-up if you have any.

## Troubleshooting

### Changes that could be required due to changes in the Arch-Linux defaults

The `use_lvmetad = 1` must be set in `/etc/lvm/lvm.conf`. This is the default now - if you have a `lvm.conf.pacnew` file, you must merge this change.

### LVM commands do not work

*   Load proper module:

```
# modprobe dm_mod

```

The `dm_mod` module should be automatically loaded. In case it does not, you can try:

 `/etc/mkinitcpio.conf:`  `MODULES="dm_mod ..."` 

You will need to [rebuild](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") the initramfs to commit any changes you made.

*   Try preceding commands with *lvm* like this:

```
# lvm pvdisplay

```

### Logical Volumes do not show up

If you are trying to mount existing logical volumes, but they do not show up in `lvscan`, you can use the following commands to activate them:

```
# vgscan
# vgchange -ay

```

### LVM on removable media

Symptoms:

```
# vgscan
 Reading all physical volumes.  This may take a while...
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
 /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
 Found volume group "backupdrive1" using metadata type lvm2
 Found volume group "networkdrive" using metadata type lvm2

```

Cause:

	Removing an external LVM drive without deactivating the volume group(s) first. Before you disconnect, make sure to:

```
# vgchange -an *volume group name*

```

Fix: assuming you already tried to activate the volume group with `# vgchange -ay *vg*`, and are receiving the Input/output errors:

```
# vgchange -an *volume group name*

```

Unplug the external drive and wait a few minutes:

```
# vgscan
# vgchange -ay *volume group name*

```

### Resizing a contiguous logical volume fails

If trying to extend a logical volume errors with:

```
" Insufficient suitable contiguous allocatable extents for logical volume "

```

The reason is that the logical volume was created with an explicit contiguous allocation policy (options `-C y` or `--alloc contiguous`) and no further adjacent contiguous extents are available (see also [reference](http://www.hostatic.ro/2010/02/15/lvm-inherit-and-contiguous-policies/)).

To fix this, prior to extending the logical volume, change its allocation policy with `lvchange --alloc inherit <logical_volume>`. If you need to keep the contiguous allocation policy, an alternative approach is to move the volume to a disk area with sufficient free extents (see [[1]](http://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents)).

### Command "grub-mkconfig" reports "unknown filesystem" errors

Make sure to remove snapshot volumes before generating grub.cfg.

## See also

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) on SourceWare.org
*   [LVM HOWTO](http://tldp.org/HOWTO/LVM-HOWTO/) article at The Linux Documentation project
*   [LVM](http://wiki.gentoo.org/wiki/LVM) article at Gentoo wiki
*   [LVM2 Mirrors vs. MD Raid 1](http://www.joshbryan.com/blog/2008/01/02/lvm2-mirrors-vs-md-raid-1/) post by Josh Bryan
*   [Ubuntu LVM Guide Part 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Part 2 detals snapshots](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)