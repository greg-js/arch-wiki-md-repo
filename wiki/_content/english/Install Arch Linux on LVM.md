Related articles

*   [LVM](/index.php/LVM "LVM")
*   [Installation guide](/index.php/Installation_guide "Installation guide")

You should create your LVM Volumes between the [partitioning](/index.php/Partitioning "Partitioning") and [formatting](/index.php/File_systems#Create_a_file_system "File systems") steps of the [installation procedure](/index.php/Installation_guide "Installation guide"). Instead of directly formatting a partition to be your root file system, the file system will be created inside a logical volume (LV).

Quick overview:

*   Install the required packages. (refer to [LVM#Getting started](/index.php/LVM#Getting_started "LVM"))
*   Create [partition(s)](/index.php/Partitioning "Partitioning") where your PV(s) will reside.
*   Create your physical volumes (PVs). If you have one disk it is best to just create one PV in one large partition. If you have multiple disks you can create partitions on each of them and create a PV on each partition.
*   Create your volume group (VG) and add all PVs to it.
*   Create logical volumes (LVs) inside that VG.
*   Continue with [Installation guide#Format the partitions](/index.php/Installation_guide#Format_the_partitions "Installation guide").
*   When you reach the “Create initial ramdisk environment” step in the Installation guide, add the `lvm2` hook to `/etc/mkinitcpio.conf` (see below for details).

**Warning:** `/boot` cannot reside in LVM when using a boot loader which does not support LVM; you must create a separate `/boot` partition and format it directly. Only [GRUB](/index.php/GRUB "GRUB") is known to support LVM.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Create partitions](#Create_partitions)
    *   [1.2 Create physical volumes](#Create_physical_volumes)
    *   [1.3 Create and extend your volume group](#Create_and_extend_your_volume_group)
        *   [1.3.1 Combined creation of physical volumes and volume groups](#Combined_creation_of_physical_volumes_and_volume_groups)
    *   [1.4 Create logical volumes](#Create_logical_volumes)
    *   [1.5 Format and mount logical volumes](#Format_and_mount_logical_volumes)
*   [2 Configure the system](#Configure_the_system)
    *   [2.1 Adding mkinitcpio hooks](#Adding_mkinitcpio_hooks)
        *   [2.1.1 Configure mkinitcpio for RAID](#Configure_mkinitcpio_for_RAID)
    *   [2.2 Kernel boot options](#Kernel_boot_options)

## Installation

You will follow along with the installation guide until you come to [Installation guide#Partition the disks](/index.php/Installation_guide#Partition_the_disks "Installation guide"). At this point you will diverge and doing all your partitioning with LVM in mind.

### Create partitions

First, [partition](/index.php/Partition "Partition") your disks as required before configuring LVM.

Create the partitions:

*   If you use Master Boot Record partition table, set the [partition type ID](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") to `8e` (partition type `Linux LVM` in *fdisk*).
*   If you use GUID Partition Table, set the [partition type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") to `E6D6D379-F507-44C2-A23C-238F2A3DF928` (partition type `Linux LVM` in *fdisk* and `8e00` in *gdisk*).

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

This command creates a header on each device so it can be used for LVM. As defined in [LVM#LVM building blocks](/index.php/LVM#LVM_building_blocks "LVM"), *DEVICE* can be any [block device](/index.php/Block_device "Block device"), e.g. a disk `/dev/sda`, a partition `/dev/sda2` or a loop back device. For example:

```
# pvcreate /dev/sda2

```

You can track created physical volumes with:

```
# pvdisplay

```

You can also get summary information on physical volumes with:

```
# pvscan

```

**Tip:** If you run into trouble with a pre-existing disk signature, you can delete it using [wipefs](/index.php/Wipefs "Wipefs").

**Note:** If using a SSD without partitioning it first, use `pvcreate --dataalignment 1m /dev/sda` (for erase block size < 1 MiB), see e.g. [here](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

### Create and extend your volume group

First you need to create a volume group on any one of the physical volumes:

```
# vgcreate <*volume_group*> <*physical_volume*>

```

For example:

```
# vgcreate VolGroup00 /dev/sda2

```

See [lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8) for a list of valid characters for volume group names.

Extending the volume group is just as easy:

```
# vgextend <*volume_group*> <*physical_volume*>

```

For example, to add both `sdb1` and `sdc` to your volume group:

```
# vgextend VolGroup00 /dev/sdb1
# vgextend VolGroup00 /dev/sdc

```

You can track how your volume group grows with:

```
# vgdisplay

```

This is also what you would do if you wanted to add a disk to a RAID or mirror group with failed disks.

**Note:** You can create more than one volume group if you need to, but then you will not have all your storage presented as a single disk.

#### Combined creation of physical volumes and volume groups

LVM allows you to combine the creation of a volume group and the physical volumes in one easy step. For example, to create the group VolGroup00 with the three devices mentioned above, you can run:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb1 /dev/sdc

```

This command will first set up the three partitions as physical volumes (if necessary) and then create the volume group with the three volumes. The command will warn you if it detects an existing filesystem on any devices.

### Create logical volumes

**Tip:** If you wish to use snapshots, logical volume caching, thin provisioned logical volumes or RAID see [LVM#Logical volume types](/index.php/LVM#Logical_volume_types "LVM").

Now we need to create logical volumes on this volume group. You create a logical volume with the next command by specifying the new volume's name and size, and the volume group it will reside on:

```
# lvcreate -L <*size*> <*volume_group*> -n <*logical_volume*>

```

For example:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

This will create a logical volume that you can access later with `/dev/VolGroup00/lvolhome`. Just like volume groups, you can use any name you want for your logical volume when creating it besides a few exceptions listed in [lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8#VALID_NAMES).

You can also specify one or more physical volumes to restrict where LVM allocates the data. For example, you may wish to create a logical volume for the root filesystem on your small SSD, and your home volume on a slower mechanical drive. Simply add the physical volume devices to the command line, for example:

```
# lvcreate -L 10G VolGroup00 -n lvolhome /dev/sdc1

```

To use all the free space left in a volume group, use the next command:

```
# lvcreate -l 100%FREE  <*volume_group*> -n <*logical_volume*>

```

You can track created logical volumes with:

```
# lvdisplay

```

**Note:** You may need to load the *device-mapper* kernel module (`modprobe dm_mod`) for the above commands to succeed.

**Tip:** You can start out with relatively small logical volumes and expand them later if needed. For simplicity, leave some free space in the volume group so there is room for expansion.

### Format and mount logical volumes

Your logical volumes should now be located in `/dev/*YourVolumeGroupName*/`. If you cannot find them, use the next commands to bring up the module for creating device nodes and to make volume groups available:

```
# modprobe dm_mod
# vgscan
# vgchange -ay

```

Now you can format your logical volumes and mount them as normal partitions (see [mount a file system](/index.php/Mount "Mount") for additional details):

```
# mkfs.<*fstype*> /dev/<*volume_group*>/<*logical_volume*>
# mount /dev/<*volume_group*>/<*logical_volume*> /<*mountpoint*>

```

For example:

```
# mkfs.ext4 /dev/VolGroup00/lvolhome
# mount /dev/VolGroup00/lvolhome /home

```

**Warning:** When choosing mountpoints, just select your newly created logical volumes (use: `/dev/Volgroup00/lvolhome`). Do **not** select the actual partitions on which logical volumes were created (do not use: `/dev/sda2`).

## Configure the system

### Adding mkinitcpio hooks

In case your root filesystem is on LVM, you will need to enable the appropriate [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hooks, otherwise your system might not boot. Enable:

*   `udev` and `lvm2` for the default busybox based initramfs
*   `systemd` and `sd-lvm2` for systemd based initramfs

`udev` is there by default. Edit the file and insert `lvm2` between `block` and `filesystems` like so:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **udev** ... block **lvm2** filesystems)` 

For systemd based initramfs:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)` 

Afterwards, you can continue in normal installation instructions with the [create an initial ramdisk](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") step.

**Tip:**

*   The `lvm2` and `sd-lvm2` hooks are installed by [lvm2](https://www.archlinux.org/packages/?name=lvm2), not [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio). If you are running *mkinitcpio* in an *arch-chroot* for a new installation, [lvm2](https://www.archlinux.org/packages/?name=lvm2) must be installed inside the *arch-chroot* for *mkinitcpio* to find the `lvm2` or `sd-lvm2` hook. If [lvm2](https://www.archlinux.org/packages/?name=lvm2) only exists outside the *arch-chroot*, *mkinitcpio* will output `Error: Hook 'lvm2' cannot be found`.
*   If your root filesystem is on LVM RAID see [#Configure mkinitcpio for RAID](#Configure_mkinitcpio_for_RAID).

#### Configure mkinitcpio for RAID

If your root filesystem is on LVM RAID additionally to `lvm2` or `sd-lvm2` hooks, you need to add `dm-raid` and the appropriate RAID modules (e.g. `raid0`, `raid1`, `raid10` and/or `raid456`) to the MODULES array in `mkinitcpio.conf`.

For busybox based initramfs:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **udev** ... block **lvm2** filesystems)
```

For systemd based initramfs:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)
```

### Kernel boot options

If the root file system resides in a logical volume, the `root=` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") must be pointed to the mapped device, e.g `/dev/*vg-name*/*lv-name*`.