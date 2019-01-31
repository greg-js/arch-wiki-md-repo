相关文章

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")
*   [System maintenance#Backup](/index.php/System_maintenance#Backup "System maintenance")
*   [Disk cloning](/index.php/Disk_cloning "Disk cloning")
*   [Migrate installation to new hardware](/index.php/Migrate_installation_to_new_hardware "Migrate installation to new hardware")
*   [File recovery](/index.php/File_recovery "File recovery")

**翻译状态：** 本文是英文页面 [System backup](/index.php/System_backup "System backup") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-01-31，点击[这里](https://wiki.archlinux.org/index.php?title=System+backup&diff=0&oldid=565294)可以查看翻译后英文页面的改动。

常规性的备份系统和用户数据是非常重要的，比如说 `/etc`, `/home`, `/var` 这些目录。如果是服务器还有 `/srv`.

## Contents

*   [1 使用 Btrfs snapshots](#使用_Btrfs_snapshots)
*   [2 使用 LVM snapshots](#使用_LVM_snapshots)
*   [3 使用 rsync](#使用_rsync)
*   [4 使用 tar](#使用_tar)
*   [5 使用 SquashFS](#使用_SquashFS)
*   [6 能够启动（boot）的备份](#能够启动（boot）的备份)
    *   [6.1 更新 fstab](#更新_fstab)
    *   [6.2 更新引导程序的配置文件](#更新引导程序的配置文件)
    *   [6.3 第一次启动](#第一次启动)

## 使用 Btrfs snapshots

详情请看 [Btrfs#Snapshots](/index.php/Btrfs#Snapshots "Btrfs") 和 [Snapper](/index.php/Snapper "Snapper").

## 使用 LVM snapshots

详情请看 [LVM#Snapshots](/index.php/LVM#Snapshots "LVM") 和 [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM").

## 使用 rsync

详情请看 [rsync#As a backup utility](/index.php/Rsync#As_a_backup_utility "Rsync").

## 使用 tar

See [Full system backup with tar](/index.php/Full_system_backup_with_tar "Full system backup with tar").

## 使用 SquashFS

详情请看 [Full system backup with SquashFS](/index.php/Full_system_backup_with_SquashFS "Full system backup with SquashFS").

## 能够启动（boot）的备份

Having a bootable backup can be useful in case the filesystem becomes corrupt or if an update breaks the system. The backup can also be used as a test bed for updates, with the *testing* repo enabled, etc. If you transferred the system to a different partition or drive and you want to boot it, the process is as simple as updating the backup's `/etc/fstab` and your bootloader's configuration file.

This section assumes that you backed up the system to another drive or partition, that your current bootloader is working fine, and that you want to boot from the backup as well.

### 更新 fstab

Without rebooting, edit the backup's [fstab](/index.php/Fstab "Fstab") by commenting out or removing any existing entries. Add one entry for the partition containing the backup like the example here:

```
/dev/sda*X*    /             *ext4*      defaults                 0   1

```

Remember to use the proper device name and filesystem type.

### 更新引导程序的配置文件

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

### 第一次启动

Reboot the computer and select the right entry in the bootloader. This will load the system for the first time. All peripherals should be detected and the empty folders in `/` will be populated.

Now you can re-edit `/etc/fstab` to add the previously removed partitions and mount points.