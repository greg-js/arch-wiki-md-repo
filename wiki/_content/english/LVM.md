Related articles

*   [Install Arch Linux on LVM](/index.php/Install_Arch_Linux_on_LVM "Install Arch Linux on LVM")
*   [Software RAID and LVM](/index.php/Software_RAID_and_LVM "Software RAID and LVM")
*   [dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system")
*   [dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system")
*   [Resizing LVM-on-LUKS](/index.php/Resizing_LVM-on-LUKS "Resizing LVM-on-LUKS")
*   [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM")

From [Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)"):

	LVM is a [logical volume manager](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management") for the [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel"); it manages disk drives and similar mass-storage devices.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Background](#Background)
    *   [1.1 LVM building blocks](#LVM_building_blocks)
    *   [1.2 Advantages](#Advantages)
    *   [1.3 Disadvantages](#Disadvantages)
    *   [1.4 Getting started](#Getting_started)
        *   [1.4.1 Graphical configuration](#Graphical_configuration)
*   [2 Volume operations](#Volume_operations)
    *   [2.1 Physical volumes](#Physical_volumes)
        *   [2.1.1 Growing](#Growing)
        *   [2.1.2 Shrinking](#Shrinking)
            *   [2.1.2.1 Move physical extents](#Move_physical_extents)
            *   [2.1.2.2 Resize physical volume](#Resize_physical_volume)
            *   [2.1.2.3 Resize partition](#Resize_partition)
    *   [2.2 Volume groups](#Volume_groups)
        *   [2.2.1 Activating a volume group](#Activating_a_volume_group)
        *   [2.2.2 Repairing a volume group](#Repairing_a_volume_group)
        *   [2.2.3 Deactivating a volume group](#Deactivating_a_volume_group)
        *   [2.2.4 Renaming a volume group](#Renaming_a_volume_group)
        *   [2.2.5 Add physical volume to a volume group](#Add_physical_volume_to_a_volume_group)
        *   [2.2.6 Remove partition from a volume group](#Remove_partition_from_a_volume_group)
    *   [2.3 Logical volumes](#Logical_volumes)
        *   [2.3.1 Renaming a logical volume](#Renaming_a_logical_volume)
        *   [2.3.2 Resizing the logical volume and file system in one go](#Resizing_the_logical_volume_and_file_system_in_one_go)
        *   [2.3.3 Resizing the logical volume and file system separately](#Resizing_the_logical_volume_and_file_system_separately)
        *   [2.3.4 Removing a logical volume](#Removing_a_logical_volume)
*   [3 Logical volume types](#Logical_volume_types)
    *   [3.1 Snapshots](#Snapshots)
        *   [3.1.1 Configuration](#Configuration)
    *   [3.2 LVM cache](#LVM_cache)
        *   [3.2.1 Create cache](#Create_cache)
        *   [3.2.2 Remove cache](#Remove_cache)
    *   [3.3 RAID](#RAID)
        *   [3.3.1 Setup RAID](#Setup_RAID)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Boot/Shutdown-problems because of disabled lvmetad](#Boot/Shutdown-problems_because_of_disabled_lvmetad)
    *   [4.2 LVM commands do not work](#LVM_commands_do_not_work)
    *   [4.3 Logical Volumes do not show up](#Logical_Volumes_do_not_show_up)
    *   [4.4 LVM on removable media](#LVM_on_removable_media)
        *   [4.4.1 Suspend/resume with LVM and removable media](#Suspend/resume_with_LVM_and_removable_media)
    *   [4.5 Resizing a contiguous logical volume fails](#Resizing_a_contiguous_logical_volume_fails)
    *   [4.6 Command "grub-mkconfig" reports "unknown filesystem" errors](#Command_"grub-mkconfig"_reports_"unknown_filesystem"_errors)
    *   [4.7 Thinly-provisioned root volume device times out](#Thinly-provisioned_root_volume_device_times_out)
    *   [4.8 Delay on shutdown](#Delay_on_shutdown)
*   [5 See also](#See_also)

## Background

### LVM building blocks

Logical Volume Management utilizes the kernel's [device-mapper](http://sources.redhat.com/dm/) feature to provide a system of partitions independent of underlying disk layout. With LVM you abstract your storage and have "virtual partitions", making [extending/shrinking](#Resizing_the_logical_volume_and_file_system_separately) easier (subject to potential filesystem limitations).

Virtual partitions allow addition and removal without worry of whether you have enough contiguous space on a particular disk, getting caught up fdisking a disk in use (and wondering whether the kernel is using the old or new partition table), or, having to move other partitions out of the way.

Basic building blocks of LVM:

	Physical volume (PV)

	Unix block device node, usable for storage by LVM. Examples: a hard disk, an MBR or GPT [partition](/index.php/Partition "Partition"), a loopback file, a device mapper device (e.g. [dm-crypt](/index.php/Dm-crypt "Dm-crypt")). It hosts an LVM header.

	Volume group (VG)

	Group of PVs that serves as a container for LVs. PEs are allocated from a VG for a LV.

	Logical volume (LV)

	"Virtual/logical partition" that resides in a VG and is composed of PEs. LVs are Unix block devices analogous to physical partitions, e.g. they can be directly formatted with a [file system](/index.php/File_system "File system").

	Physical extent (PE)

	The smallest contiguous extent (default 4 MiB) in the PV that can be assigned to a LV. Think of PEs as parts of PVs that can be allocated to any LV.

Example:

```
Physical disks

  Disk1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partition1 50 GiB (Physical volume) |Partition2 80 GiB (Physical volume)     |
    |/dev/sda1                           |/dev/sda2                               |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

  Disk2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partition1 120 GiB (Physical volume)                 |
    |/dev/sdb1                                            |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

```
LVM logical volumes

  Volume Group1 (/dev/MyVolGroup/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Logical volume1 15 GiB  |Logical volume2 35 GiB      |Logical volume3 200 GiB              |
    |/dev/MyVolGroup/rootvol |/dev/MyVolGroup/homevol     |/dev/MyVolGroup/mediavol             |
    |_ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

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
*   Support for various device-mapper targets, including transparent filesystem encryption and caching of frequently used data. This allows creating a system with (one or more) physical disks (encrypted with LUKS) and [LVM on top](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") to allow for easy resizing and management of separate volumes (e.g. for `/`, `/home`, `/backup`, etc.) without the hassle of entering a key multiple times on boot.

### Disadvantages

*   Additional steps in setting up the system, more complicated.
*   If dual-booting, note that Windows does not support LVM; you will be unable to access any LVM partitions from Windows.

### Getting started

Make sure the [lvm2](https://www.archlinux.org/packages/?name=lvm2) package is [installed](/index.php/Install "Install").

#### Graphical configuration

There is no "official" GUI tool for managing LVM volumes, but [system-config-lvm](https://aur.archlinux.org/packages/system-config-lvm/) covers most of the common operations, and provides simple visualizations of volume state. It can automatically resize many file systems when resizing logical volumes.

## Volume operations

### Physical volumes

After extending or prior to reducing the size of a device that has a physical volume on it, you need to grow or shrink the PV using `pvresize`.

#### Growing

To expand the PV on `/dev/sda1` after enlarging the [partition](/index.php/Partition "Partition"), run:

```
# pvresize /dev/sda1

```

This will automatically detect the new size of the device and extend the PV to its maximum.

**Note:** This command can be done while the volume is online.

#### Shrinking

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

##### Move physical extents

Before moving free extents to the end of the volume, one must run `pvdisplay -v -m` to see physical segments. In the below example, there is one physical volume on `/dev/sdd1`, one volume group `vg1` and one logical volume `backup`.

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

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92467` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100.0 %

```

**Note:**

*   this command moves 399668 - 307201 + 1 = 92468 PEs **from** the last segment **to** the first segment. This is possible as the first segment encloses 153600 free PEs, which can contain the 92467 - 0 + 1 = 92468 moved PEs.
*   the `--alloc anywhere` option is used as we move PEs inside the same partition. In case of different partitions, the command would look something like this: `# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999` 
*   this command may take a long time (one to two hours) in case of large volumes. It might be a good idea to run this command in a [Tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen") session. Any unwanted stop of the process could be fatal.
*   once the operation is complete, run [fsck](/index.php/Fsck "Fsck") to make sure your file system is valid.

##### Resize physical volume

Once all your free physical segments are on the last physical extents, run `vgdisplay` and see your free PE.

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

##### Resize partition

Last, you need to shrink the partition with your favorite [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning").

### Volume groups

#### Activating a volume group

**Note:** You can restrict the volumes that are activated automatically by setting the `auto_activation_volume_list` in `/etc/lvm/lvm.conf`. If in doubt, leave this option commented out.

```
# vgchange -a y vg0

```

This will reactivate the volume group if for example you had a drive failure in a mirror and you swapped the drive, ran `pvcreate`, `vgextend` and `vgreduce --removemissing --force`.

#### Repairing a volume group

To start the rebuilding process of the degraded mirror array in this example, you would run:

```
# lvconvert --repair /dev/vg0/mirror

```

You can monitor the rebuilding process (Cpy%Sync Column output) with:

```
# lvs -a -o +devices

```

#### Deactivating a volume group

Just invoke

```
# vgchange -a n my_volume_group

```

This will deactivate the volume group and allow you to unmount the container it is stored in.

#### Renaming a volume group

Use the [vgrename(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vgrename.8) command to rename an existing volume group.

Either of the following commands renames the existing volume group `vg02` to `my_volume_group`

```
# vgrename /dev/vg02 /dev/my_volume_group

```

```
# vgrename vg02 my_volume_group

```

#### Add physical volume to a volume group

You first create a new physical volume on the block device you wish to use, then extend your volume group

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1

```

This of course will increase the total number of physical extents on your volume group, which can be allocated by logical volumes as you see fit.

**Note:** It is considered good form to have a [partition table](/index.php/Partitioning "Partitioning") on your storage medium below LVM. Use the appropriate type code: `8e` for MBR, and `8e00` for GPT partitions.

#### Remove partition from a volume group

If you created a logical volume on the partition, [remove](#Removing_a_logical_volume) it first.

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

For example: if you have a bad disk in a group that cannot be found because it has been removed or failed:

```
# vgreduce --removemissing --force vg0

```

And lastly, if you want to use the partition for something else, and want to avoid LVM thinking that the partition is a physical volume:

```
# pvremove /dev/sdb1

```

### Logical volumes

**Note:** [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) provides more or less the same options as the specialized [lvextend(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvextend.8) and [lvreduce(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvreduce.8) commands, while allowing to do both types of operation. Notwithstanding this, all those utilities offer a `-r`/`--resizefs` option which allows to resize the file system together with the LV using [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) (*ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") supported). Therefore it may be easier to simply use `lvresize` for both operations and use `--resizefs` to simplify things a bit, except if you have specific needs or want full control over the process.

**Warning:** While enlarging a file system can often be done on-line (*i.e.* while it is mounted), even for the root partition, shrinking will nearly always require to first unmount the file system so as to prevent data loss. Make sure your FS supports what you are trying to do.

#### Renaming a logical volume

To rename an existing logical volume, use the [lvrename(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvrename.8) command.

Either of the following commands renames logical volume `lvold` in volume group `vg02` to `lvnew`.

```
# lvrename /dev/vg02/lvold /dev/vg02/lvnew

```

```
# lvrename vg02 lvold lvnew

```

#### Resizing the logical volume and file system in one go

**Note:** Only *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") [file systems](/index.php/File_systems "File systems") are supported. For a different type of file system see [#Resizing the logical volume and file system separately](#Resizing_the_logical_volume_and_file_system_separately).

Extend the logical volume `mediavol` in `MyVolGroup` by 10 GiB and resize its file system *all at once*:

```
# lvresize -L +10G --resizefs MyVolGroup/mediavol

```

Set the size of logical volume `mediavol` in `MyVolGroup` to 15 GiB and resize its file system *all at once*:

```
# lvresize -L 15G --resizefs MyVolGroup/mediavol

```

If you want to fill all the free space on a volume group, use the following command:

```
# lvresize -l +100%FREE --resizefs MyVolGroup/mediavol

```

See [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) for more detailed options.

#### Resizing the logical volume and file system separately

For file systems not supported by [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) will need to use the [appropriate utility](/index.php/File_systems#Types_of_file_systems "File systems") to resize the file system before shrinking the logical volume or after expanding it.

To extend logical volume `mediavol` within volume group `MyVolGroup` by 2 GiB *without* touching its file system:

```
# lvresize -L +2G MyVolGroup/mediavol

```

Now expand the file system ([ext4](/index.php/Ext4 "Ext4") in this example) to the maximum size of the underlying logical volume:

```
# resize2fs /dev/MyVolGroup/mediavol

```

To reduce the size of logical volume `mediavol` in `MyVolGroup` by 500 MiB, first calculate the resulting file system size and shrink the file system ([ext4](/index.php/Ext4 "Ext4") in this example) to the new size:

```
# resize2fs /dev/MyVolGroup/mediavol *NewSize*

```

When the file system is shrunk, reduce the size of logical volume:

```
# lvresize -L -500M MyVolGroup/mediavol

```

To calculate the exact logical volume size for *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4") file systems, use a simple formula: `LVM_EXTENTS = FS_BLOCKS × FS_BLOCKSIZE ÷ LVM_EXTENTSIZE`.

 `# tune2fs -l /dev/MyVolGroup/mediavol | grep Block` 
```
Block count:              102400000
Block size:               4096
Blocks per group:         32768

```
 `# vgdisplay MyVolGroup | grep "PE Size"` 
```
PE Size               4.00 MiB

```

**Note:** The file system block size is in bytes. Make sure to use the same units for both block and extent size.

```
102400000 blocks × 4096 bytes/block ÷ 4 MiB/extent = 100000 extents

```

Passing `--resizefs` will confirm that the correctness.

 `# lvreduce -l 100000 --resizefs /dev/MyVolGroup/mediavol` 
```
...
The filesystem is already 102400000 (4k) blocks long.  Nothing to do!
...
Logical volume sysvg/root successfully resized.

```

See [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) for more detailed options.

#### Removing a logical volume

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

## Logical volume types

Besides simple logical volumes, LVM supports snapshots, logical volume caching, thin provisioned logical volumes and RAID.

### Snapshots

LVM allows you to take a snapshot of your system in a much more efficient way than a traditional backup. It does this efficiently by using a COW (copy-on-write) policy. The initial snapshot you take simply contains hard-links to the inodes of your actual data. So long as your data remains unchanged, the snapshot merely contains its inode pointers and not the data itself. Whenever you modify a file or directory that the snapshot points to, LVM automatically clones the data, the old copy referenced by the snapshot, and the new copy referenced by your active system. Thus, you can snapshot a system with 35 GiB of data using just 2 GiB of free space so long as you modify less than 2 GiB (on both the original and snapshot). In order to be able to create snapshots you need to have unallocated space in your volume group. Snapshot like any other volume will take up space in the volume group. So, if you plan to use snapshots for backing up your root partition do not allocate 100% of your volume group for root logical volume.

#### Configuration

You create snapshot logical volumes just like normal ones.

```
# lvcreate --size 100M --snapshot --name snap01 /dev/vg0/lv

```

With that volume, you may modify less than 100 MiB of data, before the snapshot volume fills up.

Reverting the modified 'lv' logical volume to the state when the 'snap01' snapshot was taken can be done with

```
# lvconvert --merge /dev/vg0/snap01

```

In case the origin logical volume is active, merging will occur on the next reboot (merging can be done even from a LiveCD).

**Note:** The snapshot will no longer exist after merging.

Also multiple snapshots can be taken and each one can be merged with the origin logical volume at will.

The snapshot can be mounted and backed up with **dd** or **tar**. The size of the backup file done with **dd** will be the size of the files residing on the snapshot volume. To restore just create a snapshot, mount it, and write or extract the backup to it. And then merge it with the origin.

Snapshots are primarily used to provide a frozen copy of a file system to make backups; a backup taking two hours provides a more consistent image of the file system than directly backing up the partition.

See [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") for automating the creation of clean root file system snapshots during system startup for backup and rollback.

[dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") and [dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system").

If you have LVM volumes not activated via the [initramfs](/index.php/Initramfs "Initramfs"), [enable](/index.php/Enable "Enable") `lvm-monitoring.service`, which is provided by the [lvm2](https://www.archlinux.org/packages/?name=lvm2) package.

### LVM cache

From [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7):

	The cache logical volume type uses a small and fast LV to improve the performance of a large and slow LV. It does this by storing the frequently used blocks on the faster LV. LVM refers to the small fast LV as a cache pool LV. The large slow LV is called the origin LV. Due to requirements from dm-cache (the kernel driver), LVM further splits the cache pool LV into two devices - the cache data LV and cache metadata LV. The cache data LV is where copies of data blocks are kept from the origin LV to increase speed. The cache metadata LV holds the accounting information that specifies where data blocks are stored (e.g. on the origin LV or on the cache data LV). Users should be familiar with these LVs if they wish to create the best and most robust cached logical volumes. All of these associated LVs must be in the same VG.

#### Create cache

The fast method is creating a PV (if necessary) on the fast disk (replace X with your drive letter) and add it to the existing volume group:

```
# vgextend dataVG /dev/sdX

```

Create a cache pool with automatic meta data on sdX, and convert the existing logical volume (dataLV) to a cached volume, all in one step:

```
# lvcreate --type cache --cachemode writethrough -L 20G -n dataLV_cachepool dataVG/dataLV /dev/sdX

```

Obviously, if you want your cache to be bigger, you can change the `-L` parameter to a different size.

**Note:** Cachemode has two possible options:

*   `writethrough` ensures that any data written will be stored both in the cache pool LV and on the origin LV. The loss of a device associated with the cache pool LV in this case would not mean the loss of any data;
*   `writeback` ensures better performance, but at the cost of a higher risk of data loss in case the drive used for cache fails.

If a specific `--cachemode` is not indicated, the system will assume `writethrough` as default.

#### Remove cache

If you ever need to undo the one step creation operation above:

```
# lvconvert --uncache dataVG/dataLV

```

This commits any pending writes still in the cache back to the origin LV, then deletes the cache. Other options are available and described in [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7).

### RAID

From [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7):

	[lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8) RAID is a way to create a Logical Volume (LV) that uses multiple physical devices to improve performance or tolerate device failures. In LVM, the physical devices are Physical Volumes (PVs) in a single Volume Group (VG).

LVM RAID supports RAID 0, RAID 1, RAID 4, RAID 5, RAID 6 and RAID 10\. See [Wikipedia:Standard RAID levels](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels") for details on each level.

#### Setup RAID

Create physical volumes:

```
# pvcreate /dev/sda2 /dev/sdb2

```

Create volume group on the physical volumes:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb2

```

Create logical volumes useing `lvcreate --type *raidlevel*`, see [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7) and [lvcreate(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvcreate.8) for more options.

```
# lvcreate --type RaidLevel [OPTIONS] -n Name -L Size VG [PVs]

```

For example:

```
# lvcreate --type raid1 --mirrors 1 -L 20G -n myraid1vol VolGroup00 /dev/sda2 /dev/sdb2

```

will create a 20 GiB mirrored logical volume named "myraid1vol" in VolGroup00 on `/dev/sda2` and `/dev/sdb2`.

## Troubleshooting

### Boot/Shutdown-problems because of disabled lvmetad

The `use_lvmetad = 1` **must** be set in `/etc/lvm/lvm.conf`. This is the default now - if you have a `lvm.conf.pacnew` file, you must merge this change.

### LVM commands do not work

*   Load proper module:

```
# modprobe dm_mod

```

The `dm_mod` module should be automatically loaded. In case it does not, you can try:

 `/etc/mkinitcpio.conf`  `MODULES=(dm_mod ...)` 

You will need to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") to commit any changes you made.

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

 `# vgscan` 
```
  Reading all physical volumes.  This may take a while...
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
  Found volume group "backupdrive1" using metadata type lvm2
  Found volume group "networkdrive" using metadata type lvm2

```

Cause: removing an external LVM drive without deactivating the volume group(s) first. Before you disconnect, make sure to:

```
# vgchange -an *volume group name*

```

Fix: assuming you already tried to activate the volume group with `vgchange -ay *vg*`, and are receiving the Input/output errors:

```
# vgchange -an *volume group name*

```

Unplug the external drive and wait a few minutes:

```
# vgscan
# vgchange -ay *volume group name*

```

#### Suspend/resume with LVM and removable media

In order for LVM to work properly with removable media – like an external USB drive – the volume group of the external drive needs to be deactivated before suspend. If this is not done, you may get 'buffer I/O errors on the dm device (after resume). For this reason, it is not recommended to mix external and internal drives in the same volume group.

To automatically deactivate the volume groups with external USB drives, tag each volume group with the `sleep_umount` tag in this way:

```
# vgchange --addtag sleep_umount *vg_external*

```

Once the tag is set, use the following unit file for systemd to properly deactivate the volumes before suspend. On resume, they will be automatically activated by LVM.

 `/etc/systemd/system/ext_usb_vg_deactivate.service` 
```
[Unit]
Description=Deactivate external USB volume groups on suspend
Before=sleep.target

[Service]
Type=oneshot
ExecStart=-/etc/systemd/system/deactivate_sleep_vgs.sh

[Install]
WantedBy=sleep.target
```

and this script:

 `/etc/systemd/system/deactivate_sleep_vgs.sh` 
```
#!/bin/sh

TAG=@sleep_umount
vgs=$(vgs --noheadings -o vg_name $TAG)

echo "Deactivating volume groups with $TAG tag: $vgs"

# Unmount logical volumes belonging to all the volume groups with tag $TAG
for vg in $vgs; do
    for lv_dev_path in $(lvs --noheadings  -o lv_path -S lv_active=active,vg_name=$vg); do
        echo "Unmounting logical volume $lv_dev_path"
        umount $lv_dev_path
    done
done

# Deactivate volume groups tagged with sleep_umount
for vg in $vgs; do
    echo "Deactivating volume group $vg"
    vgchange -an $vg
done
```

Finally, [enable](/index.php/Enable "Enable") the unit.

### Resizing a contiguous logical volume fails

If trying to extend a logical volume errors with:

```
" Insufficient suitable contiguous allocatable extents for logical volume "

```

The reason is that the logical volume was created with an explicit contiguous allocation policy (options `-C y` or `--alloc contiguous`) and no further adjacent contiguous extents are available (see also [reference](http://www.hostatic.ro/2010/02/15/lvm-inherit-and-contiguous-policies/)).

To fix this, prior to extending the logical volume, change its allocation policy with `lvchange --alloc inherit <logical_volume>`. If you need to keep the contiguous allocation policy, an alternative approach is to move the volume to a disk area with sufficient free extents (see [[1]](http://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents)).

### Command "grub-mkconfig" reports "unknown filesystem" errors

Make sure to remove snapshot volumes before [generating grub.cfg](/index.php/GRUB#Generate_the_main_configuration_file "GRUB").

### Thinly-provisioned root volume device times out

With a large number of snapshots, `thin_check` runs for a long enough time so that waiting for the root device times out. To compensate, add the `rootdelay=60` kernel boot parameter to your boot loader configuration. Or, make `thin_check` skip checking block mappings (see [[2]](https://www.redhat.com/archives/linux-lvm/2016-January/msg00010.html)) and [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs"):

 `/etc/lvm/lvm.conf`  `thin_check_options = [ "-q", "--clear-needs-check-flag", "--skip-mappings" ]` 

### Delay on shutdown

If you use RAID, snapshots or thin provisioning and experience a delay on shutdown, make sure `lvm2-monitor.service` is [started](/index.php/Started "Started"). See [FS#50420](https://bugs.archlinux.org/task/50420).

## See also

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) on SourceWare.org
*   [LVM](http://wiki.gentoo.org/wiki/LVM) article at Gentoo wiki
*   [Ubuntu LVM Guide Part 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Part 2 detals snapshots](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)
*   [Red Hat: Logical Volume Manager Administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Logical_Volume_Manager_Administration/index.html)