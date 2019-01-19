Related articles

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")
*   [File recovery](/index.php/File_recovery "File recovery")

It is important to regularly backup system and user data stored for example in `/etc`, `/home`, `/var` and for server installations, also `/srv`.

## Contents

*   [1 Using Btrfs snapshots](#Using_Btrfs_snapshots)
*   [2 Using LVM snapshots](#Using_LVM_snapshots)
*   [3 Using rsync](#Using_rsync)
*   [4 Using tar](#Using_tar)
*   [5 Using SquashFS](#Using_SquashFS)
*   [6 Bootable backup](#Bootable_backup)
    *   [6.1 Update the fstab](#Update_the_fstab)
    *   [6.2 Update the bootloader's configuration file](#Update_the_bootloader's_configuration_file)
    *   [6.3 First boot](#First_boot)

## Using Btrfs snapshots

See [Btrfs#Snapshots](/index.php/Btrfs#Snapshots "Btrfs") and [Snapper](/index.php/Snapper "Snapper").

## Using LVM snapshots

See [LVM#Snapshots](/index.php/LVM#Snapshots "LVM") and [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM").

## Using rsync

See [rsync#As a backup utility](/index.php/Rsync#As_a_backup_utility "Rsync").

## Using tar

See [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar").

## Using SquashFS

See [Full system backup with SquashFS](/index.php/Full_system_backup_with_SquashFS "Full system backup with SquashFS").

## Bootable backup

Having a bootable backup can be useful in case the filesystem becomes corrupt or if an update breaks the system. The backup can also be used as a test bed for updates, with the *testing* repo enabled, etc. If you transferred the system to a different partition or drive and you want to boot it, the process is as simple as updating the backup's `/etc/fstab` and your bootloader's configuration file.

This section assumes that you backed up the system to another drive or partition, that your current bootloader is working fine, and that you want to boot from the backup as well.

### Update the fstab

Without rebooting, edit the backup's [fstab](/index.php/Fstab "Fstab") by commenting out or removing any existing entries. Add one entry for the partition containing the backup like the example here:

```
/dev/sda*X*    /             *ext4*      defaults                 0   1

```

Remember to use the proper device name and filesystem type.

### Update the bootloader's configuration file

For [Syslinux](/index.php/Syslinux "Syslinux"), all you need to do is duplicate the current entry, except pointing to a different drive or partition.

**Tip:** Instead of editing `syslinux.cfg`, you can also temporarily edit the menu during boot. When the menu shows up, press the `Tab` key and change the relevant entries. Partitions are counted from one, drives are counted from zero.

For [GRUB](/index.php/GRUB "GRUB"), it is recommended that you automatically [re-generate the main configuration file](/index.php/GRUB#Generate_the_main_configuration_file "GRUB"). If you want to freshly install all grub files to somewhere other than `/boot`, such as `/mnt/newroot/boot`, use the `--boot-directory` flag.

Also verify the new menu entry in `/boot/grub/grub.cfg`. Make sure the UUID is matching the new partition, otherwise it could still boot the old system. Find the UUID of a partition with [lsblk](/index.php/Lsblk "Lsblk"):

```
$ lsblk -no NAME,UUID /dev/sdb3

```

where you substitute the desired partition for /dev/sdb3\. To list the UUIDs of partitions grub thinks it can boot, use grep:

```
# grep UUID= /boot/grub/grub.cfg

```

### First boot

Reboot the computer and select the right entry in the bootloader. This will load the system for the first time. All peripherals should be detected and the empty folders in `/` will be populated.

Now you can re-edit `/etc/fstab` to add the previously removed partitions and mount points.