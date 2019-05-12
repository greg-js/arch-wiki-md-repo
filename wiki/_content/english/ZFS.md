Related articles

*   [File systems](/index.php/File_systems "File systems")
*   [ZFS/Virtual disks](/index.php/ZFS/Virtual_disks "ZFS/Virtual disks")
*   [Installing Arch Linux on ZFS](/index.php/Installing_Arch_Linux_on_ZFS "Installing Arch Linux on ZFS")

[ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS") is an advanced filesystem created by [Sun Microsystems](https://en.wikipedia.org/wiki/Sun_Microsystems "wikipedia:Sun Microsystems") (now owned by Oracle) and released for OpenSolaris in November 2005\.

Features of ZFS include: pooled storage (integrated volume management – zpool), [Copy-on-write](https://en.wikipedia.org/wiki/Copy-on-write "wikipedia:Copy-on-write"), [snapshots](https://en.wikipedia.org/wiki/Snapshot_(computer_storage) "wikipedia:Snapshot (computer storage)"), data integrity verification and automatic repair (scrubbing), [RAID-Z](https://en.wikipedia.org/wiki/RAID-Z "wikipedia:RAID-Z"), a maximum [16 Exabyte](https://en.wikipedia.org/wiki/Exabyte "wikipedia:Exabyte") file size, and a maximum 256 Quadrillion [Zettabytes](https://en.wikipedia.org/wiki/Zettabyte "wikipedia:Zettabyte") storage with no limit on number of filesystems (datasets) or files[[1]](http://docs.oracle.com/cd/E19253-01/819-5461/zfsover-2/index.html). ZFS is licensed under the [Common Development and Distribution License](https://en.wikipedia.org/wiki/CDDL "wikipedia:CDDL") (CDDL).

Described as ["The last word in filesystems"](http://web.archive.org/web/20060428092023/http://www.sun.com/2004-0914/feature/) ZFS is stable, fast, secure, and future-proof. Being licensed under the CDDL, and thus incompatible with GPL, it is not possible for ZFS to be distributed along with the Linux Kernel. This requirement, however, does not prevent a native Linux kernel module from being developed and distributed by a third party, as is the case with [zfsonlinux.org](http://zfsonlinux.org/) (ZOL).

ZOL is a project funded by the [Lawrence Livermore National Laboratory](https://www.llnl.gov/) to develop a native Linux kernel module for its massive storage requirements and super computers.

**Note:**

Due to potential legal incompatibilities between CDDL license of ZFS code and GPL of the Linux kernel ([[2]](https://sfconservancy.org/blog/2016/feb/25/zfs-and-linux/),[CDDL-GPL](https://en.wikipedia.org/wiki/Common_Development_and_Distribution_License#GPL_compatibility "wikipedia:Common Development and Distribution License"),[ZFS in Linux](https://en.wikipedia.org/wiki/ZFS#Linux "wikipedia:ZFS")) - ZFS development is not supported by the kernel.

As a result:

*   ZFSonLinux project must keep up with Linux kernel versions. After making stable ZFSonLinux release - Arch ZFS maintainers release them.
*   This situation sometimes locks down the normal rolling update process by unsatisfied dependencies because the new kernel version, proposed by update, is unsupported by ZFSonLinux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 General](#General)
    *   [1.2 Root on ZFS](#Root_on_ZFS)
    *   [1.3 DKMS](#DKMS)
*   [2 Experimenting with ZFS](#Experimenting_with_ZFS)
*   [3 Configuration](#Configuration)
    *   [3.1 Automatic Start](#Automatic_Start)
*   [4 Creating a storage pool](#Creating_a_storage_pool)
    *   [4.1 Identify disks](#Identify_disks)
        *   [4.1.1 Using GPT labels](#Using_GPT_labels)
    *   [4.2 Creating ZFS pools](#Creating_ZFS_pools)
        *   [4.2.1 Advanced Format disks](#Advanced_Format_disks)
        *   [4.2.2 GRUB-compatible pool creation](#GRUB-compatible_pool_creation)
    *   [4.3 Verifying pool status](#Verifying_pool_status)
    *   [4.4 Importing a pool created by id](#Importing_a_pool_created_by_id)
*   [5 Tuning](#Tuning)
    *   [5.1 General](#General_2)
    *   [5.2 Scrubbing](#Scrubbing)
        *   [5.2.1 How often should I do this?](#How_often_should_I_do_this?)
        *   [5.2.2 Start with a service or timer](#Start_with_a_service_or_timer)
    *   [5.3 Destroy a storage pool](#Destroy_a_storage_pool)
    *   [5.4 Exporting a storage pool](#Exporting_a_storage_pool)
    *   [5.5 Renaming a zpool](#Renaming_a_zpool)
    *   [5.6 Setting a different mount point](#Setting_a_different_mount_point)
    *   [5.7 SSD Caching](#SSD_Caching)
        *   [5.7.1 SLOG](#SLOG)
        *   [5.7.2 L2ARC](#L2ARC)
    *   [5.8 ZVOLs](#ZVOLs)
        *   [5.8.1 RAIDZ and Advanced Format physical disks](#RAIDZ_and_Advanced_Format_physical_disks)
    *   [5.9 I/O Scheduler](#I/O_Scheduler)
*   [6 Creating datasets](#Creating_datasets)
    *   [6.1 Native encryption](#Native_encryption)
        *   [6.1.1 Unlock at boot time](#Unlock_at_boot_time)
    *   [6.2 Swap volume](#Swap_volume)
    *   [6.3 Access Control Lists](#Access_Control_Lists)
    *   [6.4 Databases](#Databases)
    *   [6.5 /tmp](#/tmp)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Creating a zpool fails](#Creating_a_zpool_fails)
    *   [7.2 ZFS is using too much RAM](#ZFS_is_using_too_much_RAM)
    *   [7.3 Does not contain an EFI label](#Does_not_contain_an_EFI_label)
    *   [7.4 No hostid found](#No_hostid_found)
    *   [7.5 Pool cannot be found while booting from SAS/SCSI devices](#Pool_cannot_be_found_while_booting_from_SAS/SCSI_devices)
    *   [7.6 On boot the zfs pool does not mount stating: "pool may be in use from other system"](#On_boot_the_zfs_pool_does_not_mount_stating:_"pool_may_be_in_use_from_other_system")
        *   [7.6.1 Unexported pool](#Unexported_pool)
        *   [7.6.2 Incorrect hostid](#Incorrect_hostid)
    *   [7.7 Devices have different sector alignment](#Devices_have_different_sector_alignment)
    *   [7.8 Pool resilvering stuck/restarting/slow?](#Pool_resilvering_stuck/restarting/slow?)
    *   [7.9 Fix slow boot caused by failed import of unavailable pools in the initramfs zpool.cache](#Fix_slow_boot_caused_by_failed_import_of_unavailable_pools_in_the_initramfs_zpool.cache)
*   [8 Tips and tricks](#Tips_and_tricks)
    *   [8.1 Embed the archzfs packages into an archiso](#Embed_the_archzfs_packages_into_an_archiso)
    *   [8.2 Automatic snapshots](#Automatic_snapshots)
        *   [8.2.1 ZFS Automatic Snapshot Service for Linux](#ZFS_Automatic_Snapshot_Service_for_Linux)
        *   [8.2.2 ZFS Snapshot Manager](#ZFS_Snapshot_Manager)
    *   [8.3 Creating a share](#Creating_a_share)
        *   [8.3.1 NFS](#NFS)
        *   [8.3.2 SMB](#SMB)
    *   [8.4 Encryption in ZFS using dm-crypt](#Encryption_in_ZFS_using_dm-crypt)
    *   [8.5 Emergency chroot repair with archzfs](#Emergency_chroot_repair_with_archzfs)
    *   [8.6 Bind mount](#Bind_mount)
        *   [8.6.1 fstab](#fstab)
    *   [8.7 Monitoring / Mailing on Events](#Monitoring_/_Mailing_on_Events)
    *   [8.8 Wrap shell commands in pre & post snapshots](#Wrap_shell_commands_in_pre_&_post_snapshots)
    *   [8.9 Remote unlocking of ZFS encrypted root](#Remote_unlocking_of_ZFS_encrypted_root)
        *   [8.9.1 Changing the SSH server port](#Changing_the_SSH_server_port)
        *   [8.9.2 Unlocking from a Windows machine using PuTTY/Plink](#Unlocking_from_a_Windows_machine_using_PuTTY/Plink)
*   [9 See also](#See_also)

## Installation

### General

**Warning:** Unless you use the [dkms](/index.php/Dkms "Dkms") versions of these packages, the ZFS and SPL kernel modules are tied to a specific kernel version. It would not be possible to apply any kernel updates until updated packages are uploaded to AUR or the [archzfs](/index.php/Unofficial_user_repositories#archzfs "Unofficial user repositories") repository.

**Tip:** You can [downgrade](/index.php/Downgrade "Downgrade") your linux version to the one from [archzfs](/index.php/Unofficial_user_repositories#archzfs "Unofficial user repositories") repo if your current kernel is newer.

Install from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") or the [archzfs](/index.php/Unofficial_user_repositories#archzfs "Unofficial user repositories") repository:

*   [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) for [stable](http://zfsonlinux.org/) releases.
*   [zfs-linux-git](https://aur.archlinux.org/packages/zfs-linux-git/) for [development](https://github.com/zfsonlinux/zfs/releases) releases (with support of newer kernel versions).
*   [zfs-linux-lts](https://aur.archlinux.org/packages/zfs-linux-lts/) for stable releases for LTS kernels.
*   [zfs-linux-lts-git](https://aur.archlinux.org/packages/zfs-linux-lts-git/) for [development](https://github.com/zfsonlinux/zfs/releases) releases for LTS kernels.
*   [zfs-linux-hardened](https://aur.archlinux.org/packages/zfs-linux-hardened/) for stable releases for hardened kernels.
*   [zfs-linux-hardened-git](https://aur.archlinux.org/packages/zfs-linux-hardened-git/) for [development](https://github.com/zfsonlinux/zfs/releases) releases for hardened kernels.
*   [zfs-linux-zen](https://aur.archlinux.org/packages/zfs-linux-zen/) for stable releases for zen kernels.
*   [zfs-linux-zen-git](https://aur.archlinux.org/packages/zfs-linux-zen-git/) for [development](https://github.com/zfsonlinux/zfs/releases) releases for zen kernels.
*   [zfs-dkms](https://aur.archlinux.org/packages/zfs-dkms/) for versions with dynamic kernel module support.
*   [zfs-dkms-git](https://aur.archlinux.org/packages/zfs-dkms-git/) for [development](https://github.com/zfsonlinux/zfs/releases) releases for versions with dynamic kernel module support.

These branches have (according to them) dependencies on the `zfs-utils`, `spl`, `spl-utils` packages. SPL (Solaris Porting Layer) is a Linux Kernel module implementing Solaris APIs for ZFS compatibility.

Test the installation by issuing `zpool status` on the command line. If an "insmod" error is produced, try `depmod -a`.

### Root on ZFS

When performing an Arch install on ZFS, [zfs-linux](https://aur.archlinux.org/packages/zfs-linux/) or [zfs-dkms](https://aur.archlinux.org/packages/zfs-dkms/) and its dependencies can be installed in the archiso environment as outlined in the previous section.

It may be useful to prepare a [customized archiso](#Embed_the_archzfs_packages_into_an_archiso) with ZFS support builtin. For a much more detailed guide on installing Arch with ZFS as its root file system, see [Installing Arch Linux on ZFS](/index.php/Installing_Arch_Linux_on_ZFS "Installing Arch Linux on ZFS").

### DKMS

Users can make use of DKMS [Dynamic Kernel Module Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support") to rebuild the ZFS modules automatically with every kernel upgrade.

Install [zfs-dkms](https://aur.archlinux.org/packages/zfs-dkms/) or [zfs-dkms-git](https://aur.archlinux.org/packages/zfs-dkms-git/) and apply the post-install instructions given by these packages.

**Tip:** Add an `IgnorePkg` entry to [pacman.conf](/index.php/Pacman.conf "Pacman.conf") to prevent these packages from upgrading when doing a regular update.

## Experimenting with ZFS

Users wishing to experiment with ZFS on *virtual block devices* (known in ZFS terms as VDEVs) which can be simple files like `~/zfs0.img` `~/zfs1.img` `~/zfs2.img` etc. with no possibility of real data loss are encouraged to see the [Experimenting with ZFS](/index.php/Experimenting_with_ZFS "Experimenting with ZFS") article. Common tasks like building a RAIDZ array, purposefully corrupting data and recovering it, snapshotting datasets, etc. are covered.

## Configuration

ZFS is considered a "zero administration" filesystem by its creators; therefore, configuring ZFS is very straight forward. Configuration is done primarily with two commands: `zfs` and `zpool`.

### Automatic Start

For ZFS to live by its "zero administration" namesake, the zfs daemon must be loaded at startup. A benefit to this is that it is not necessary to mount the zpool in `/etc/fstab`; the zfs daemon can import and mount zfs pools automatically. The daemon mounts the zfs pools reading the file `/etc/zfs/zpool.cache`.

For each [imported pool](#Importing_a_pool_created_by_id) you want automatically mounted by the zfs daemon execute:

```
# zpool set cachefile=/etc/zfs/zpool.cache <pool>

```

Enable the service so it is automatically started at boot time:

```
# systemctl enable zfs.target

```

To manually start the daemon:

```
# systemctl start zfs.target

```

**Note:** Beginning with ZOL version 0.6.5.8 the ZFS service unit files have been changed so that you need to explicitly enable any ZFS services you want to run. See [https://github.com/archzfs/archzfs/issues/72](https://github.com/archzfs/archzfs/issues/72) for more information.

In order to mount zfs pools automatically on boot you need to enable the following services and targets:

```
# systemctl enable zfs-import-cache
# systemctl enable zfs-mount
# systemctl enable zfs-import.target

```

or, as explained on [the GitHub issue](https://github.com/archzfs/archzfs/issues/72), use the [systemd preset file](https://www.freedesktop.org/software/systemd/man/systemd.preset.html):

```
# systemctl preset $(tail -n +2 /usr/lib/systemd/system-preset/50-zfs.preset | cut -d ' ' -f 2)

```

## Creating a storage pool

Make sure the wanted disks contain an empty [GPT](/index.php/GPT "GPT")/[MBR](/index.php/MBR "MBR") [partition table](/index.php/Partition_table "Partition table"). It is not necessary nor recommended to partition the drives before creating the ZFS filesystem.

**Note:** If some or all device have been used in a software RAID set it is paramount to [erase any old RAID configuration information](/index.php/Mdadm#Prepare_the_devices "Mdadm").

**Warning:** For [Advanced Format](/index.php/Advanced_Format "Advanced Format") Disks with 4KB sector size, an ashift of 12 is recommended for best performance. Advanced Format disks emulate a sector size of 512 bytes for compatibility with legacy systems, this causes ZFS to sometimes use an ashift option number that is not ideal. Once the pool has been created, the only way to change the ashift option is to recreate the pool. Using an ashift of 12 would also decrease available capacity. See [1.10 What’s going on with performance?](https://github.com/zfsonlinux/zfs/wiki/faq#performance-considerations), [1.15 How does ZFS on Linux handle Advanced Format disks?](https://github.com/zfsonlinux/zfs/wiki/faq#advanced-format-disks), and [ZFS and Advanced Format disks](http://wiki.illumos.org/display/illumos/ZFS+and+Advanced+Format+disks).

### Identify disks

[ZFS on Linux](https://github.com/zfsonlinux/zfs/wiki/faq#selecting-dev-names-when-creating-a-pool) recommends using device IDs when creating ZFS storage pools of less than 10 devices. Use [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming") to identify the list of drives to be used for ZFS pool.

The disk IDs should look similar to the following:

 `# ls -lh /dev/disk/by-id/` 
```
lrwxrwxrwx 1 root root  9 Aug 12 16:26 ata-ST3000DM001-9YN166_S1F0JKRR -> ../../sdc
lrwxrwxrwx 1 root root  9 Aug 12 16:26 ata-ST3000DM001-9YN166_S1F0JTM1 -> ../../sde
lrwxrwxrwx 1 root root  9 Aug 12 16:26 ata-ST3000DM001-9YN166_S1F0KBP8 -> ../../sdd
lrwxrwxrwx 1 root root  9 Aug 12 16:26 ata-ST3000DM001-9YN166_S1F0KDGY -> ../../sdb
```

**Warning:** If you create zpools using device names (e.g. `/dev/sda`,`/dev/sdb`,...) ZFS might not be able to detect zpools intermittently on boot.

#### Using GPT labels

Disk labels and UUID can also be used for ZFS mounts by using [GPT](/index.php/GUID_Partition_Table "GUID Partition Table") partitions. ZFS drives have labels but Linux is unable to read them at boot. Unlike [MBR](/index.php/Master_Boot_Record "Master Boot Record") partitions, GPT partitions directly support both UUID and labels independent of the format inside the partition. Partitioning rather than using the whole disk for ZFS offers two additional advantages. The OS does not generate bogus partition numbers from whatever unpredictable data ZFS has written to the partition sector, and if desired, you can easily over provision SSD drives, and slightly over provision spindle drives to ensure that different models with slightly different sector counts can zpool replace into your mirrors. This is a lot of organization and control over ZFS using readily available tools and techniques at almost zero cost.

Use [gdisk](/index.php/GUID_Partition_Table "GUID Partition Table") to partition the all or part of the drive as a single partition. gdisk does not automatically name partitions so if partition labels are desired use gdisk command "c" to label the partitions. Some reasons you might prefer labels over UUID are: labels are easy to control, labels can be titled to make the purpose of each disk in your arrangement readily apparent, and labels are shorter and easier to type. These are all advantages when the server is down and the heat is on. GPT partition labels have plenty of space and can store most international characters [wikipedia:GUID_Partition_Table#Partition_entries](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries "wikipedia:GUID Partition Table") allowing large data pools to be labeled in an organized fashion.

Drives partitioned with GPT have labels and UUID that look like this.

```
# ls -l /dev/disk/by-partlabel
# lrwxrwxrwx 1 root root 10 Apr 30 01:44 zfsdata1 -> ../../sdd1
# lrwxrwxrwx 1 root root 10 Apr 30 01:44 zfsdata2 -> ../../sdc1
# lrwxrwxrwx 1 root root 10 Apr 30 01:59 zfsl2arc -> ../../sda1

```

```
# ls -l /dev/disk/by-partuuid
# lrwxrwxrwx 1 root root 10 Apr 30 01:44 148c462c-7819-431a-9aba-5bf42bb5a34e -> ../../sdd1
# lrwxrwxrwx 1 root root 10 Apr 30 01:59 4f95da30-b2fb-412b-9090-fc349993df56 -> ../../sda1
# lrwxrwxrwx 1 root root 10 Apr 30 01:44 e5ccef58-5adf-4094-81a7-3bac846a885f -> ../../sdc1

```

**Tip:** To minimize typing and copy/paste errors, set a local variable with the target PARTUUID: `$ UUID=$( lsblk --noheadings --output PARTUUID /dev/sd*XY* )`

### Creating ZFS pools

To create a ZFS pool:

```
# zpool create -f -m <mount> <pool> [raidz(2|3)|mirror] <ids>

```

**Tip:** One may want to read [#Advanced Format disks](#Advanced_Format_disks) first as it may be recommend to set `ashift` on pool creation.

*   **create**: subcommand to create the pool.

*   **-f**: Force creating the pool. This is to overcome the "EFI label error". See [#Does not contain an EFI label](#Does_not_contain_an_EFI_label).

*   **-m**: The mount point of the pool. If this is not specified, then the pool will be mounted to `/<pool>`.

*   **pool**: This is the name of the pool.

*   **raidz(2|3)|mirror**: This is the type of virtual device that will be created from the pool of devices, raidz is a single disk of parity, raidz2 for 2 disks of parity and raidz3 for 3 disks of parity, similar to raid5 and raid6\. Also available is **mirror**, which is similar to raid1 or raid10, but is not constrained to just 2 device. If not specified, each device will be added as a vdev which is similar to raid0\. After creation, a device can be added to each single drive vdev to turn it into a mirror, which can be useful for migrating data.

*   **ids**: The [ID's](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming") of the drives or partitions that to include into the pool.

Create pool with single raidz vdev:

```
# zpool create -f -m /mnt/data bigdata \
               raidz \
                  ata-ST3000DM001-9YN166_S1F0KDGY \
                  ata-ST3000DM001-9YN166_S1F0JKRR \
                  ata-ST3000DM001-9YN166_S1F0KBP8 \
                  ata-ST3000DM001-9YN166_S1F0JTM1

```

Create pool with two mirror vdevs:

```
# zpool create -f -m /mnt/data bigdata \
               mirror \
                  ata-ST3000DM001-9YN166_S1F0KDGY \
                  ata-ST3000DM001-9YN166_S1F0JKRR \
               mirror \
                  ata-ST3000DM001-9YN166_S1F0KBP8 \
                  ata-ST3000DM001-9YN166_S1F0JTM1

```

#### Advanced Format disks

At pool creation, **ashift=12** should always be used, except with SSDs that have 8k sectors where **ashift=13** is correct. A vdev of 512 byte disks using 4k sectors will not experience performance issues, but a 4k disk using 512 byte sectors will. Since **ashift** cannot be changed after pool creation, even a pool with only 512 byte disks should use 4k because those disks may need to be replaced with 4k disks or the pool may be expanded by adding a vdev composed of 4k disks. Because correct detection of 4k disks is not reliable, `-o ashift=12` should always be specified during pool creation. See the [ZFS on Linux FAQ](https://github.com/zfsonlinux/zfs/wiki/faq#advanced-format-disks) for more details.

**Tip:** Use [blockdev(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/blockdev.8) (part of [util-linux](https://www.archlinux.org/packages/?name=util-linux)) to print the sector size reported by the device's ioctls: `# blockdev --getpbsz /dev/sd*XY*`.

Create pool with ashift=12 and single raidz vdev:

```
# zpool create -f -o ashift=12 -m /mnt/data bigdata \
               raidz \
                  ata-ST3000DM001-9YN166_S1F0KDGY \
                  ata-ST3000DM001-9YN166_S1F0JKRR \
                  ata-ST3000DM001-9YN166_S1F0KBP8 \
                  ata-ST3000DM001-9YN166_S1F0JTM1

```

#### GRUB-compatible pool creation

**Note:** This section frequently goes out of date with updates to GRUB and ZFS. Consult the manual pages for the most up-to-date information.

By default, *zpool create* enables all features on a pool. If `/boot` resides on ZFS when using [GRUB](/index.php/GRUB "GRUB") you must only enable features supported by GRUB otherwise GRUB will not be able to read the pool. GRUB 2.02 supports the read-write features `lz4_compress`, `hole_birth`, `embedded_data`, `extensible_dataset`, and `large_blocks`; this is not suitable for all the features of ZFSonLinux 0.7.1, and must have unsupported features disabled.

You can create a pool with the incompatible features disabled:

```
# zpool create -o feature@multi_vdev_crash_dump=disabled \
               -o feature@large_dnode=disabled           \
               -o feature@sha512=disabled                \
               -o feature@skein=disabled                 \
               -o feature@edonr=disabled                 \
               $POOL_NAME $VDEVS

```

When running the git version of ZFS on Linux, make sure to also add `-o feature@encryption=disabled`.

### Verifying pool status

If the command is successful, there will be no output. Using the [mount](/index.php/Mount "Mount") command will show that the pool is mounted. Using `zpool status` will show that the pool has been created:

 `# zpool status -v` 
```
  pool: bigdata
 state: ONLINE
 scan: none requested
config:

        NAME                                       STATE     READ WRITE CKSUM
        bigdata                                    ONLINE       0     0     0
          -0                                       ONLINE       0     0     0
            ata-ST3000DM001-9YN166_S1F0KDGY-part1  ONLINE       0     0     0
            ata-ST3000DM001-9YN166_S1F0JKRR-part1  ONLINE       0     0     0
            ata-ST3000DM001-9YN166_S1F0KBP8-part1  ONLINE       0     0     0
            ata-ST3000DM001-9YN166_S1F0JTM1-part1  ONLINE       0     0     0

errors: No known data errors

```

At this point it would be good to reboot the machine to ensure that the ZFS pool is mounted at boot. It is best to deal with all errors before transferring data.

### Importing a pool created by id

Eventually a pool may fail to auto mount and you need to import to bring your pool back. Take care to avoid the most obvious solution.

**Warning:** Do not run `zpool import *pool*`! This will import your pools using `/dev/sd?` which will lead to problems the next time you rearrange your drives. This may be as simple as rebooting with a USB drive left in the machine, which harkens back to a time when PCs would not boot when a floppy disk was left in a machine.

Adapt one of the following commands to import your pool so that pool imports retain the persistence they were created with:

```
# zpool import -d /dev/disk/by-id bigdata
# zpool import -d /dev/disk/by-partlabel bigdata
# zpool import -d /dev/disk/by-partuuid bigdata

```

**Note:** Use the `-l` flag when importing a pool that contains [encrypted datasets keys](#Native_encryption):
```
# zpool import -l -d /dev/disk/by-id bigdata

```

Finally check the state of the pool:

```
# zpool status -v bigdata

```

## Tuning

### General

ZFS pools can be further adjusted using parameters, most commonly `atime` and `compression`.

To retrieve the current pool parameter status:

```
# zfs get all <pool>

```

To disable access time (atime), which is enabled by default:

```
# zfs set atime=off <pool>

```

As an alternative to turning off atime completely, `relatime` is available. This brings the default ext4/XFS atime semantics to ZFS, where access time is only updated if the modified time or changed time changes, or if the existing access time has not been updated within the past 24 hours. It is a compromise between `atime=off` and `atime=on`. This property *only* takes effect if `atime` is `on`:

```
# zfs set atime=on <pool>
# zfs set relatime=on <pool>

```

Compression is just that, transparent compression of data. ZFS supports a few different algorithms, presently lz4 is the default, *gzip* is also available for seldom-written yet highly-compressible data; consult the [OpenZFS Wiki](http://open-zfs.org/wiki/Performance_tuning#Compression) for more details.

To enable compression:

```
# zfs set compression=on <pool>

```

**Note:** To reset a property of a pool and/or dataset to it's default state, use `zfs inherit`:
```
# zfs inherit -rS atime <pool>
# zfs inherit -rS atime <pool>/<dataset>

```

### Scrubbing

Whenever data is read and ZFS encounters an error, it is silently repaired when possible, rewritten back to disk and logged so you can obtain an overview of errors on your pools. There is no fsck or equivalent tool for ZFS. Instead, ZFS supports a feature known as scrubbing. This traverses through all the data in a pool and verifies that all blocks can be read.

To scrub a pool:

```
# zpool scrub <pool>

```

To cancel a running scrub:

```
# zpool scrub -s <pool>

```

#### How often should I do this?

From the Oracle blog post [Disk Scrub - Why and When?](https://blogs.oracle.com/wonders-of-zfs-storage/disk-scrub-why-and-when-v2):

	This question is challenging for Support to answer, because as always the true answer is "It Depends". So before I offer a general guideline, here are a few tips to help you create an answer more tailored to your use pattern.

*   What is the expiration of your oldest backup? You should probably scrub your data at least as often as your oldest tapes expire so that you have a known-good restore point.
*   How often are you experiencing disk failures? While the recruitment of a hot-spare disk invokes a "resilver" -- a targeted scrub of just the VDEV which lost a disk -- you should probably scrub at least as often as you experience disk failures on average in your specific environment.
*   How often is the oldest piece of data on your disk read? You should scrub occasionally to prevent very old, very stale data from experiencing bit-rot and dying without you knowing it.

	If any of your answers to the above are "I do not know", the general guideline is: you should probably be scrubbing your zpool at least once per month. It is a schedule that works well for most use cases, provides enough time for scrubs to complete before starting up again on all but the busiest & most heavily-loaded systems, and even on very large zpools (192+ disks) should complete fairly often between disk failures.

In the [ZFS Administration Guide](https://pthree.org/2012/12/11/zfs-administration-part-vi-scrub-and-resilver/) by Aaron Toponce, he advises to scrub consumer disks once a week.

#### Start with a service or timer

Using a [systemd](/index.php/Systemd "Systemd") timer/service it is possible to automatically scrub pools monthly:

 `/etc/systemd/system/zfs-scrub@.timer` 
```
[Unit]
Description=Monthly zpool scrub on %i

[Timer]
OnCalendar=monthly
AccuracySec=1h
Persistent=true

[Install]
WantedBy=multi-user.target
```
 `/etc/systemd/system/zfs-scrub@.service` 
```
[Unit]
Description=zpool scrub on %i

[Service]
Nice=19
IOSchedulingClass=idle
KillSignal=SIGINT
ExecStart=/usr/bin/zpool scrub %i
```

[Enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") `zfs-scrub@*pool-to-scrub*.timer` unit for monthly scrubbing the specified zpool.

### Destroy a storage pool

ZFS makes it easy to destroy a mounted storage pool, removing all metadata about the ZFS device.

**Warning:** This command destroys **any data** containing in the pool and/or dataset.

To destroy the pool:

```
# zpool destroy <pool>

```

To destroy a dataset:

```
# zpool destroy <pool>/<dataset>

```

And now when checking the status:

 `# zpool status` 
```
no pools available

```

### Exporting a storage pool

If a storage pool is to be used on another system, it will first need to be exported. It is also necessary to export a pool if it has been imported from the archiso as the hostid is different in the archiso as it is in the booted system. The zpool command will refuse to import any storage pools that have not been exported. It is possible to force the import with the `-f` argument, but this is considered bad form.

Any attempts made to import an un-exported storage pool will result in an error stating the storage pool is in use by another system. This error can be produced at boot time abruptly abandoning the system in the busybox console and requiring an archiso to do an emergency repair by either exporting the pool, or adding the `zfs_force=1` to the kernel boot parameters (which is not ideal). See [#On boot the zfs pool does not mount stating: "pool may be in use from other system"](#On_boot_the_zfs_pool_does_not_mount_stating:_"pool_may_be_in_use_from_other_system")

To export a pool:

```
# zpool export <pool>

```

### Renaming a zpool

Renaming a zpool that is already created is accomplished in 2 steps:

```
# zpool export oldname
# zpool import oldname newname

```

### Setting a different mount point

The mount point for a given zpool can be moved at will with one command:

```
# zfs set mountpoint=/foo/bar poolname

```

### SSD Caching

You can add SSD devices as a write intent log (external ZIL or SLOG) and also as a layer 2 adaptive replacement cache (L2ARC). The process to add them is very similar to adding a new VDEV.

All of the below references to device-id are the IDs from `/dev/disk/by-id/*`.

#### SLOG

To add a mirrored SLOG:

```
 # zpool add <pool> log mirror <device-id-1> <device-id-2>

```

Or to add a single device SLOG (unsafe):

```
 # zpool add <pool> log <device-id>

```

Because the SLOG device stores data that has not been written to the pool, it is important to use devices that can finish writes when power is lost. It is also important to use redundancy, since a device failure can cause data loss. In addition, the SLOG is only used for sync writes, so may not provide any performance improvement.

#### L2ARC

To add L2ARC:

```
 # zpool add <pool> cache <device-id>

```

Because every block cached in L2ARC uses a small amount of memory, it is generally only useful in workloads where the amount of hot data is *bigger* than the maximum amount of memory that can fit in the computer, but small enough to fit into L2ARC. It is also cleared at reboot and is only a read cache, so redundancy is unnecessary. Un-intuitively, L2ARC can actually harm performance since it takes memory away from ARC.

### ZVOLs

ZFS volumes (ZVOLs) can suffer from the same block size-related issues as RDBMSes, but it is worth noting that the default recordsize for ZVOLs is 8 KiB already. If possible, it is best to align any partitions contained in a ZVOL to your recordsize (current versions of fdisk and gdisk by default automatically align at 1MiB segments, which works), and file system block sizes to the same size. Other than this, you might tweak the **recordsize** to accommodate the data inside the ZVOL as necessary (though 8 KiB tends to be a good value for most file systems, even when using 4 KiB blocks on that level).

#### RAIDZ and Advanced Format physical disks

Each block of a ZVOL gets its own parity disks, and if you have physical media with logical block sizes of 4096B, 8192B, or so on, the parity needs to be stored in whole physical blocks, and this can drastically increase the space requirements of a ZVOL, requiring 2× or more physical storage capacity than the ZVOL's logical capacity. Setting the **recordsize** to 16k or 32k can help reduce this footprint drastically.

See [ZFS on Linux issue #1807 for details](https://github.com/zfsonlinux/zfs/issues/1807)

### I/O Scheduler

When the pool is imported, for whole disk vdevs, the block device I/O scheduler is set to `zfs_vdev_scheduler` [[3]](https://github.com/zfsonlinux/zfs/wiki/ZFS-on-Linux-Module-Parameters#zfs_vdev_scheduler). The most common schedulers are: *noop*, *cfq*, *bfq*, and *deadline*.

In some cases, the scheduler is not changeable using this method. Known schedulers that cannot be changed are: *scsi_mq* and *none*. In these cases, the scheduler is unchanged and an error message can be reported to logs. [Manually setting](/index.php/Improving_performance#Changing_I/O_scheduler "Improving performance") one of the common schedulers used by `zfs_vdev_scheduler` can result in more consistent performance.

## Creating datasets

Users can optionally create a dataset under the zpool as opposed to manually creating directories under the zpool. Datasets allow for an increased level of control (quotas for example) in addition to snapshots. To be able to create and mount a dataset, a directory of the same name must not pre-exist in the zpool. To create a dataset, use:

```
# zfs create <nameofzpool>/<nameofdataset>

```

It is then possible to apply ZFS specific attributes to the dataset. For example, one could assign a quota limit to a specific directory within a dataset:

```
# zfs set quota=20G <nameofzpool>/<nameofdataset>/<directory>

```

To see all the commands available in ZFS, see zfs(8) or zpool(8).

### Native encryption

ZFS offers the following supported encryption options: `aes-128-ccm`, `aes-192-ccm`, `aes-256-ccm`, `aes-128-gcm`, `aes-192-gcm` and `aes-256-gcm`. When encryption is set to `on`, `aes-256-ccm` will be used.

The following keyformats are supported: `passphrase`, `raw`, `hex`.

One can also specify/increase the default iterations of PBKDF2 when using `passphrase` with `-o pbkdf2iters <n>`, although it may increase the decryption time.

**Note:**

*   Native ZFS encryption has been made available in 0.7.0.r26 or newer provided by packages like [zfs-linux-git](https://aur.archlinux.org/packages/zfs-linux-git/), [zfs-dkms-git](https://aur.archlinux.org/packages/zfs-dkms-git/) or other development builds. Despite the fact that version 0.7 has been released, this feature is still not enabled in the stable version as of 0.7.3, so a development build still needs to be used.
*   To import a pool with keys, one needs to specify the `-l` flag, without this flag encrypted datasets will be left unavailable until the keys are loaded. See [#Importing a pool created by id](#Importing_a_pool_created_by_id).

To create a dataset including native encryption with a passphrase, use:

```
# zfs create -o encryption=on -o keyformat=passphrase <nameofzpool>/<nameofdataset>

```

To use a key instead of using a passphrase:

```
# dd if=/dev/random of=/path/to/key bs=1 count=32
# zfs create -o encryption=on -o keyformat=raw -o keylocation=file:///path/to/key <nameofzpool>/<nameofdataset>

```

To verify the key location:

```
# zfs get keylocation <nameofzpool>/<nameofdataset>

```

To change the key location:

```
# zfs set keylocation=file:///path/to/key <nameofzpool>/<nameofdataset>

```

You can also manually load the keys by using one of the following commands:

```
# zfs load-key <nameofzpool>/<nameofdataset> # load key for a specific dataset
# zfs load-key -a # load all keys
# zfs load-key -r zpool/dataset # load all keys in a dataset

```

To mount the created encrypted dataset:

```
# zfs mount <nameofzpool>/<nameofdataset>

```

#### Unlock at boot time

It is possible to automatically unlock a pool dataset on boot time by using a [systemd](/index.php/Systemd "Systemd") unit. For example create the following service to unlock any dataset of the pool named *tank*:

 `/etc/systemd/system/zfskey-tank@.service` 
```
[Unit]
Description=Load pool encryption keys
#Before=systemd-user-sessions.service
Before=zfs-mount.service
After=zfs-import.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/bash -c '/usr/bin/zfs load-key %j/%i

[Install]
WantedBy=zfs-mount.service
```

[Enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") the service for each encrypted dataset, e.g. `# systemctl enable zfskey-tank@dataset`.

**Note:** The `Before=systemd-user-sessions.service` ensures that systemd-ask-password is invoked before the local IO devices are handed over to the [desktop environment](/index.php/Desktop_environment "Desktop environment").

An alternative is to load all possible keys:

 `etc/systemd/system/zfs-load-key.service` 
```
[Unit]
Description=Load encryption keys
Before=zfs-mount.service
After=zfs-import.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/bin/bash -c '/usr/bin/zfs load-key -a'

[Install]
WantedBy=zfs-mount.service
```

[Enable](/index.php/Enable "Enable")/[start](/index.php/Start "Start") `zfs-load-key.service`.

### Swap volume

**Warning:** On systems with extremely high memory pressure, using a zvol for swap can result in lockup, regardless of how much swap is still available. This issue is currently being investigated in [https://github.com/zfsonlinux/zfs/issues/7734](https://github.com/zfsonlinux/zfs/issues/7734)

ZFS does not allow to use swapfiles, but users can use a ZFS volume (ZVOL) as swap. It is important to set the ZVOL block size to match the system page size, which can be obtained by the `getconf PAGESIZE` command (default on x86_64 is 4KiB). Another option useful for keeping the system running well in low-memory situations is not caching the ZVOL data.

Create a 8 GiB zfs volume:

```
# zfs create -V 8G -b $(getconf PAGESIZE) \
              -o logbias=throughput -o sync=always\
              -o primarycache=metadata \
              -o com.sun:auto-snapshot=false <pool>/swap

```

Prepare it as swap partition:

```
# mkswap -f /dev/zvol/<pool>/swap
# swapon /dev/zvol/<pool>/swap

```

To make it permanent, edit `/etc/fstab`. ZVOLs support discard, which can potentially help ZFS's block allocator and reduce fragmentation for all other datasets when/if swap is not full.

Add a line to `/etc/fstab`:

```
/dev/zvol/<pool>/swap none swap discard 0 0

```

### Access Control Lists

To use [ACL](/index.php/ACL "ACL") on a ZFS pool:

```
# zfs set acltype=posixacl <nameofzpool>/<nameofdataset>
# zfs set xattr=sa <nameofzpool>/<nameofdataset>

```

Setting `xattr` is recommended for performance reasons [[4]](https://github.com/zfsonlinux/zfs/issues/170#issuecomment-27348094).

It may be preferable to enable ACL on the zpool instead. Setting `aclinherit=passthrough` may be wanted as the default mode is `restricted` [[5]](https://docs.oracle.com/cd/E19120-01/open.solaris/817-2271/gbaaz/index.html):

```
# zfs set aclinherit=passthrough <nameofzpool>
# zfs set acltype=posixacl <nameofzpool>
# zfs set xattr=sa <nameofzpool>

```

### Databases

ZFS, unlike most other file systems, has a variable record size, or what is commonly referred to as a block size. By default, the recordsize on ZFS is 128KiB, which means it will dynamically allocate blocks of any size from 512B to 128KiB depending on the size of file being written. This can often help fragmentation and file access, at the cost that ZFS would have to allocate new 128KiB blocks each time only a few bytes are written to.

Most RDBMSes work in 8KiB-sized blocks by default. Although the block size is tunable for [MySQL/MariaDB](/index.php/MySQL "MySQL"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), and [Oracle](/index.php/Oracle "Oracle"), all three of them use an 8KiB block size *by default*. For both performance concerns and keeping snapshot differences to a minimum (for backup purposes, this is helpful), it is usually desirable to tune ZFS instead to accommodate the databases, using a command such as:

```
# zfs set recordsize=8K <pool>/postgres

```

These RDBMSes also tend to implement their own caching algorithm, often similar to ZFS's own ARC. In the interest of saving memory, it is best to simply disable ZFS's caching of the database's file data and let the database do its own job:

```
# zfs set primarycache=metadata <pool>/postgres

```

If your pool has no configured log devices, ZFS reserves space on the pool's data disks for its intent log (the ZIL). ZFS uses this for crash recovery, but databases are often syncing their data files to the file system on their own transaction commits anyway. The end result of this is that ZFS will be committing data **twice** to the data disks, and it can severely impact performance. You can tell ZFS to prefer to not use the ZIL, and in which case, data is only committed to the file system once. Setting this for non-database file systems, or for pools with configured log devices, can actually *negatively* impact the performance, so beware:

```
# zfs set logbias=throughput <pool>/postgres

```

These can also be done at file system creation time, for example:

```
# zfs create -o recordsize=8K \
             -o primarycache=metadata \
             -o mountpoint=/var/lib/postgres \
             -o logbias=throughput \
              <pool>/postgres

```

Please note: these kinds of tuning parameters are ideal for specialized applications like RDBMSes. You can easily *hurt* ZFS's performance by setting these on a general-purpose file system such as your /home directory.

### /tmp

If you would like to use ZFS to store your /tmp directory, which may be useful for storing arbitrarily-large sets of files or simply keeping your RAM free of idle data, you can generally improve performance of certain applications writing to /tmp by disabling file system sync. This causes ZFS to ignore an application's sync requests (eg, with `fsync` or `O_SYNC`) and return immediately. While this has severe application-side data consistency consequences (never disable sync for a database!), files in /tmp are less likely to be important and affected. Please note this does *not* affect the integrity of ZFS itself, only the possibility that data an application expects on-disk may not have actually been written out following a crash.

```
# zfs set sync=disabled <pool>/tmp

```

Additionally, for security purposes, you may want to disable **setuid** and **devices** on the /tmp file system, which prevents some kinds of privilege-escalation attacks or the use of device nodes:

```
# zfs set setuid=off <pool>/tmp
# zfs set devices=off <pool>/tmp

```

Combining all of these for a create command would be as follows:

```
# zfs create -o setuid=off -o devices=off -o sync=disabled -o mountpoint=/tmp <pool>/tmp

```

Please note, also, that if you want /tmp on ZFS, you will need to mask (disable) [systemd](/index.php/Systemd "Systemd")'s automatic tmpfs-backed /tmp, else ZFS will be unable to mount your dataset at boot-time or import-time:

```
# systemctl mask tmp.mount

```

## Troubleshooting

### Creating a zpool fails

If the following error occurs then it can be fixed.

```
# the kernel failed to rescan the partition table: 16
# cannot label 'sdc': try using parted(8) and then provide a specific slice: -1

```

One reason this can occur is because [ZFS expects pool creation to take less than 1 second](https://github.com/zfsonlinux/zfs/issues/2582). This is a reasonable assumption under ordinary conditions, but in many situations it may take longer. Each drive will need to be cleared again before another attempt can be made.

```
# parted /dev/sda rm 1
# parted /dev/sda rm 1
# dd if=/dev/zero of=/dev/sdb bs=512 count=1
# zpool labelclear /dev/sda

```

A brute force creation can be attempted over and over again, and with some luck the ZPool creation will take less than 1 second. Once cause for creation slowdown can be slow burst read writes on a drive. By reading from the disk in parallell to ZPool creation, it may be possible to increase burst speeds.

```
# dd if=/dev/sda of=/dev/null

```

This can be done with multiple drives by saving the above command for each drive to a file on separate lines and running

```
# cat $FILE | parallel

```

Then run ZPool creation at the same time.

### ZFS is using too much RAM

By default, ZFS caches file operations ([ARC](https://en.wikipedia.org/wiki/Adaptive_replacement_cache "wikipedia:Adaptive replacement cache")) using up to two-thirds of available system memory on the host. To adjust the ARC size, add the following to the [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") list:

```
zfs.zfs_arc_max=536870912 # (for 512MB)

```

For a more detailed description, as well as other configuration options, see [gentoo-wiki:zfs#arc](http://wiki.gentoo.org/wiki/ZFS#ARC).

### Does not contain an EFI label

The following error will occur when attempting to create a zfs filesystem,

```
/dev/disk/by-id/<id> does not contain an EFI label but it may contain partition

```

The way to overcome this is to use `-f` with the zfs create command.

### No hostid found

An error that occurs at boot with the following lines appearing before initscript output:

```
ZFS: No hostid found on kernel command line or /etc/hostid.

```

This warning occurs because the ZFS module does not have access to the spl hosted. There are two solutions, for this. Either place the spl hostid in the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") in the boot loader. For example, adding `spl.spl_hostid=0x00bab10c`.

The other solution is to make sure that there is a hostid in `/etc/hostid`, and then [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") image. Which will copy the hostid into the initramfs image.

### Pool cannot be found while booting from SAS/SCSI devices

In case you are booting a SAS/SCSI based, you might occassionally get boot problems where the pool you are trying to boot from cannot be found. A likely reason for this is that your devices are initialized too late into the process. That means that zfs cannot find any devices at the time when it tries to assemble your pool.

In this case you should force the scsi driver to wait for devices to come online before continuing. You can do this by putting this into `/etc/modprobe.d/zfs.conf`:

 `/etc/modprobe.d/zfs.conf`  `options scsi_mod scan=sync` 

Afterwards, [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

This works because the zfs hook will copy the file at `/etc/modprobe.d/zfs.conf` into the initcpio which will then be used at build time.

### On boot the zfs pool does not mount stating: "pool may be in use from other system"

#### Unexported pool

If the new installation does not boot because the zpool cannot be imported, chroot into the installation and properly export the zpool. See [#Emergency chroot repair with archzfs](#Emergency_chroot_repair_with_archzfs).

Once inside the chroot environment, load the ZFS module and force import the zpool,

```
# zpool import -a -f

```

now export the pool:

```
# zpool export <pool>

```

To see the available pools, use,

```
# zpool status

```

It is necessary to export a pool because of the way ZFS uses the hostid to track the system the zpool was created on. The hostid is generated partly based on the network setup. During the installation in the archiso the network configuration could be different generating a different hostid than the one contained in the new installation. Once the zfs filesystem is exported and then re-imported in the new installation, the hostid is reset. See [Re: Howto zpool import/export automatically? - msg#00227](http://osdir.com/ml/zfs-discuss/2011-06/msg00227.html).

If ZFS complains about "pool may be in use" after every reboot, properly export pool as described above, and then [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") in normally booted system.

#### Incorrect hostid

Double check that the pool is properly exported. Exporting the zpool clears the hostid marking the ownership. So during the first boot the zpool should mount correctly. If it does not there is some other problem.

Reboot again, if the zfs pool refuses to mount it means the hostid is not yet correctly set in the early boot phase and it confuses zfs. Manually tell zfs the correct number, once the hostid is coherent across the reboots the zpool will mount correctly.

Boot using zfs_force and write down the hostid. This one is just an example.

 `$ hostid` 
```
0a0af0f8

```

This number have to be added to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") as `spl.spl_hostid=0x0a0af0f8`. Another solution is writing the hostid inside the initram image, see the [installation guide](/index.php/Installing_Arch_Linux_on_ZFS#After_the_first_boot "Installing Arch Linux on ZFS") explanation about this.

Users can always ignore the check adding `zfs_force=1` in the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), but it is not advisable as a permanent solution.

### Devices have different sector alignment

Once a drive has become faulted it should be replaced A.S.A.P. with an identical drive.

```
# zpool replace bigdata ata-ST3000DM001-9YN166_S1F0KDGY ata-ST3000DM001-1CH166_W1F478BD -f

```

but in this instance, the following error is produced:

```
cannot replace ata-ST3000DM001-9YN166_S1F0KDGY with ata-ST3000DM001-1CH166_W1F478BD: devices have different sector alignment

```

ZFS uses the ashift option to adjust for physical block size. When replacing the faulted disk, ZFS is attempting to use `ashift=12`, but the faulted disk is using a different ashift (probably `ashift=9`) and this causes the resulting error.

For Advanced Format Disks with 4KB blocksize, an ashift of 12 is recommended for best performance. See [1.10 What’s going on with performance?](https://github.com/zfsonlinux/zfs/wiki/faq#performance-considerations) and [ZFS and Advanced Format disks](http://wiki.illumos.org/display/illumos/ZFS+and+Advanced+Format+disks).

Use zdb to find the ashift of the zpool: `zdb` , then use the `-o` argument to set the ashift of the replacement drive:

```
# zpool replace bigdata ata-ST3000DM001-9YN166_S1F0KDGY ata-ST3000DM001-1CH166_W1F478BD -o ashift=9 -f

```

Check the zpool status for confirmation:

 `# zpool status -v` 
```
pool: bigdata
state: DEGRADED
status: One or more devices is currently being resilvered.  The pool will
        continue to function, possibly in a degraded state.
action: Wait for the resilver to complete.
scan: resilver in progress since Mon Jun 16 11:16:28 2014
    10.3G scanned out of 5.90T at 81.7M/s, 20h59m to go
    2.57G resilvered, 0.17% done
config:

        NAME                                   STATE     READ WRITE CKSUM
        bigdata                                DEGRADED     0     0     0
        raidz1-0                               DEGRADED     0     0     0
            replacing-0                        OFFLINE      0     0     0
            ata-ST3000DM001-9YN166_S1F0KDGY    OFFLINE      0     0     0
            ata-ST3000DM001-1CH166_W1F478BD    ONLINE       0     0     0  (resilvering)
            ata-ST3000DM001-9YN166_S1F0JKRR    ONLINE       0     0     0
            ata-ST3000DM001-9YN166_S1F0KBP8    ONLINE       0     0     0
            ata-ST3000DM001-9YN166_S1F0JTM1    ONLINE       0     0     0

errors: No known data errors

```

### Pool resilvering stuck/restarting/slow?

According to the ZFSonLinux github it is a known issue since 2012 with ZFS-ZED which causes the resilvering process to constantly restart, sometimes get stuck and be generally slow for some hardware. The simplest mitigation is to stop zfs-zed.service until the resilver completes

### Fix slow boot caused by failed import of unavailable pools in the initramfs zpool.cache

Your boot time can be significantly impacted if you update your intitramfs (eg when doing a kernel update) when you have additional but non-permanently attached pools imported because these pools will get added to your initramfs zpool.cache and ZFS will attempt to import these extra pools on every boot, regardless of whether you have exported it and removed it from your regular zpool.cache.

If you notice ZFS trying to import unavailable pools at boot, first run:

```
$ zdb -C

```

To check you zpool.cache for pools you do not want imported at boot. If this command is showing (a) additional, currently unavailable pool(s), run:

```
# zpool set cachefile=/etc/zfs/zpool.cache zroot

```

To clear the zpool.cache of any pools other than the pool named zroot. Sometimes there is no need to refresh your zpool.cache, but instead all you need to do is [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

## Tips and tricks

### Embed the archzfs packages into an archiso

Follow the [Archiso](/index.php/Archiso "Archiso") steps for creating a fully functional Arch Linux live CD/DVD/USB image.

Enable the [archzfs](/index.php/Unofficial_user_repositories#archzfs "Unofficial user repositories") repository:

 `~/archlive/pacman.conf` 
```
...
[archzfs]
Server = http://archzfs.com/$repo/x86_64

```

Add the `archzfs-linux` group to the list of packages to be installed (the `archzfs` repository provides packages for the x86_64 architecture only).

 `~/archlive/packages.x86_64` 
```
...
archzfs-linux

```

Complete [Build the ISO](/index.php/Archiso#Build_the_ISO "Archiso") to finally build the iso.

**Note:** If you later have problems running modprobe zfs, you should include the linux-headers in the packages.x86_64\.

### Automatic snapshots

#### ZFS Automatic Snapshot Service for Linux

The [zfs-auto-snapshot-git](https://aur.archlinux.org/packages/zfs-auto-snapshot-git/) package from [AUR](/index.php/AUR "AUR") provides a shell script to automate the management of snapshots, with each named by date and label (hourly, daily, etc), giving quick and convenient snapshotting of all ZFS datasets. The package also installs cron tasks for quarter-hourly, hourly, daily, weekly, and monthly snapshots. Optionally adjust the `--keep parameter` from the defaults depending on how far back the snapshots are to go (the monthly script by default keeps data for up to a year).

To prevent a dataset from being snapshotted at all, set `com.sun:auto-snapshot=false` on it. Likewise, set more fine-grained control as well by label, if, for example, no monthlies are to be kept on a snapshot, for example, set `com.sun:auto-snapshot:monthly=false`.

**Note:** zfs-auto-snapshot-git will not create snapshots during scrubbing ([scrub](#Scrub)). It is possible to override this by editing provided systemd unit ([Systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd")) and removing `--skip-scrub` from `ExecStart` line. Consequences not known, someone please edit.

#### ZFS Snapshot Manager

The [zfs-snap-manager](https://aur.archlinux.org/packages/zfs-snap-manager/) package from [AUR](/index.php/AUR "AUR") provides a python service that takes daily snapshots from a configurable set of ZFS datasets and cleans them out in a ["Grandfather-father-son"](https://en.wikipedia.org/wiki/Backup_rotation_scheme#Grandfather-father-son "wikipedia:Backup rotation scheme") scheme. It can be configured to e.g. keep 7 daily, 5 weekly, 3 monthly and 2 yearly snapshots.

The package also supports configurable replication to other machines running ZFS by means of `zfs send` and `zfs receive`. If the destination machine runs this package as well, it could be configured to keep these replicated snapshots for a longer time. This allows a setup where a source machine has only a few daily snapshots locally stored, while on a remote storage server a much longer retention is available.

### Creating a share

ZFS has support for creating shares by SMB or [NFS](/index.php/NFS "NFS").

#### NFS

Make sure [NFS](/index.php/NFS "NFS") has been installed/configured, note there is no need to edit the `/etc/exports` file. For sharing over NFS the services `nfs-server.service` and `zfs-share.service` should be [started](/index.php/Start "Start").

To make a pool available on the network:

```
# zfs set sharenfs=on <nameofzpool>

```

To make a dataset available on the network:

```
# zfs set sharenfs=on <nameofzpool>/<nameofdataset>

```

To enable read/write access for a specific ip-range(s):

```
# zfs set sharenfs="rw=@192.168.1.100/24,rw=@10.0.0.0/24" <nameofzpool>/<nameofdataset>

```

To check if the dataset is exported successful:

 `# showmount -e `hostname`` 
```
Export list for hostname:
/path/of/dataset 192.168.1.100/24

```

To view the current loaded exports state in more detail, use:

 `# exportfs -v` 
```
/path/of/dataset
    192.168.1.100/24(sync,wdelay,hide,no_subtree_check,mountpoint,sec=sys,rw,secure,no_root_squash,no_all_squash)
```

#### SMB

When sharing smb shares configuring usershares in your smb.conf will allow ZFS to setup and create the shares.

```
# [global]
#    usershare path = /var/lib/samba/usershares
#    usershare max shares = 100
#    usershare allow guests = yes
#    usershare owner only = no
```

Create and set permissions on the user directory as root

```
# mkdir /var/lib/samba/usershares
# chmod +t /var/lib/samba/usershares

```

### Encryption in ZFS using dm-crypt

The stable release version of ZFS on Linux does not support encryption directly, but zpools can be created in dm-crypt block devices. Since the zpool is created on the plain-text abstraction, it is possible to have the data encrypted while having all the advantages of ZFS like deduplication, compression, and data robustness.

dm-crypt, possibly via LUKS, creates devices in `/dev/mapper` and their name is fixed. So you just need to change `zpool create` commands to point to that names. The idea is configuring the system to create the `/dev/mapper` block devices and import the zpools from there. Since zpools can be created in multiple devices (raid, mirroring, striping, ...), it is important all the devices are encrypted otherwise the protection might be partially lost.

For example, an encrypted zpool can be created using plain dm-crypt (without LUKS) with:

```
# cryptsetup --hash=sha512 --cipher=twofish-xts-plain64 --offset=0 \
             --key-file=/dev/sdZ --key-size=512 open --type=plain /dev/sdX enc
# zpool create zroot /dev/mapper/enc

```

In the case of a root filesystem pool, the `mkinitcpio.conf` HOOKS line will enable the keyboard for the password, create the devices, and load the pools. It will contain something like:

```
HOOKS="... keyboard encrypt zfs ..."

```

Since the `/dev/mapper/enc` name is fixed no import errors will occur.

Creating encrypted zpools works fine. But if you need encrypted directories, for example to protect your users' homes, ZFS loses some functionality.

ZFS will see the encrypted data, not the plain-text abstraction, so compression and deduplication will not work. The reason is that encrypted data has always high entropy making compression ineffective and even from the same input you get different output (thanks to salting) making deduplication impossible. To reduce the unnecessary overhead it is possible to create a sub-filesystem for each encrypted directory and use [eCryptfs](/index.php/ECryptfs "ECryptfs") on it.

For example to have an encrypted home: (the two passwords, encryption and login, must be the same)

```
# zfs create -o compression=off -o dedup=off -o mountpoint=/home/<username> <zpool>/<username>
# useradd -m <username>
# passwd <username>
# ecryptfs-migrate-home -u <username>
<log in user and complete the procedure with ecryptfs-unwrap-passphrase>

```

### Emergency chroot repair with archzfs

To get into the ZFS filesystem from live system for maintenance, there are two options:

1.  Build custom archiso with ZFS as described in [#Embed the archzfs packages into an archiso](#Embed_the_archzfs_packages_into_an_archiso).
2.  Boot the latest official archiso and bring up the network. Then enable [archzfs](/index.php/Unofficial_user_repositories#archzfs "Unofficial user repositories") repository inside the live system as usual, sync the pacman package database and install the *archzfs-archiso-linux* package.

To start the recovery, load the ZFS kernel modules:

```
# modprobe zfs

```

Import the pool:

```
# zpool import -a -R /mnt

```

Mount the boot partitions (if any):

```
# mount /dev/sda2 /mnt/boot
# mount /dev/sda1 /mnt/boot/efi

```

Chroot into the ZFS filesystem:

```
# arch-chroot /mnt /bin/bash

```

Check the kernel version:

```
# pacman -Qi linux
# uname -r

```

uname will show the kernel version of the archiso. If they are different, run depmod (in the chroot) with the correct kernel version of the chroot installation:

```
# depmod -a 3.6.9-1-ARCH (version gathered from pacman -Qi linux but using the matching kernel modules directory name under the chroot's /lib/modules)

```

This will load the correct kernel modules for the kernel version installed in the chroot installation.

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs"). There should be no errors.

### Bind mount

Here a bind mount from /mnt/zfspool to /srv/nfs4/music is created. The configuration ensures that the zfs pool is ready before the bind mount is created.

#### fstab

See [systemd.mount](http://www.freedesktop.org/software/systemd/man/systemd.mount.html) for more information on how systemd converts fstab into mount unit files with [systemd-fstab-generator](http://www.freedesktop.org/software/systemd/man/systemd-fstab-generator.html).

 `/etc/fstab` 
```
/mnt/zfspool		/srv/nfs4/music		none	bind,defaults,nofail,x-systemd.requires=zfs-mount.service	0 0

```

### Monitoring / Mailing on Events

See [ZED: The ZFS Event Daemon](https://ramsdenj.com/2016/08/29/arch-linux-on-zfs-part-3-followup.html) for more information.

An email forwarder, such as [S-nail](/index.php/S-nail "S-nail") (installed as part of [base](https://www.archlinux.org/groups/x86_64/base/)), is required to accomplish this. Test it to be sure it is working correctly.

Uncomment the following in the configuration file:

 `/etc/zfs/zed.d/zed.rc` 
```
 ZED_EMAIL_ADDR="root"
 ZED_EMAIL_PROG="mailx"
 ZED_NOTIFY_VERBOSE=0
 ZED_EMAIL_OPTS="-s '@SUBJECT@' @ADDRESS@"

```

Update 'root' in `ZED_EMAIL_ADDR="root"` to the email address you want to receive notifications at.

If you are keeping your mailrc in your home directory, you can tell mail to get it from there by setting `MAILRC`:

 `/etc/zfs/zed.d/zed.rc`  `export MAILRC=/home/<user>/.mailrc` 

This works because ZED sources this file, so `mailx` sees this environment variable.

If you want to receive an email no matter the state of your pool, you will want to set `ZED_NOTIFY_VERBOSE=1`. You will need to do this temporary to test.

[Start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `zfs-zed.service`.

With `ZED_NOTIFY_VERBOSE=1`, you can test by running a scrub as root: `zpool scrub <pool-name>`.

### Wrap shell commands in pre & post snapshots

Since it is so cheap to make a snapshot, we can use this as a measure of security for sensitive commands such as system and package upgrades. If we make a snapshot before, and one after, we can later diff these snapshots to find out what changed on the filesystem after the command executed. Furthermore we can also rollback in case the outcome was not desired.

E.g.:

```
# zfs snapshot -r zroot@pre
# pacman -Syu
# zfs snapshot -r zroot@post
# zfs diff zroot@pre zroot@post 
# zfs rollback zroot@pre

```

A utility that automates the creation of pre and post snapshots around a shell command is [znp](https://gist.github.com/erikw/eeec35be33e847c211acd886ffb145d5).

E.g.:

```
# znp pacman -Syu
# znp find / -name "something*" -delete

```

and you would get snapshots created before and after the supplied command, and also output of the commands logged to file for future reference so we know what command created the diff seen in a pair of pre/post snapshots.

### Remote unlocking of ZFS encrypted root

As of [PR #261](https://github.com/archzfs/archzfs/pull/261), `archzfs` supports SSH unlocking of natively-encrypted ZFS datasets. This section describes how to use this feature, and is largely based on [dm-crypt/Specialties#Remote unlocking (hooks: netconf, dropbear, tinyssh, ppp)](/index.php/Dm-crypt/Specialties#Remote_unlocking_(hooks:_netconf,_dropbear,_tinyssh,_ppp) "Dm-crypt/Specialties").

1.  Install [mkinitcpio-netconf](https://www.archlinux.org/packages/?name=mkinitcpio-netconf) to provide hooks for setting up early user space networking.
2.  Choose an SSH server to use in early user space. The options are [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh) or [mkinitcpio-dropbear](https://www.archlinux.org/packages/?name=mkinitcpio-dropbear), and are mutually exclusive.
    1.  If using [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh), it is also recommended to install [tinyssh-convert](https://www.archlinux.org/packages/?name=tinyssh-convert) or [tinyssh-convert-git](https://aur.archlinux.org/packages/tinyssh-convert-git/). This tool converts an existing OpenSSH hostkey to the TinySSH key format, preserving the key fingerprint and avoiding connection warnings. The TinySSH and Dropbear mkinitcpio install scripts will automatically convert existing hostkeys when generating a new initcpio image.
3.  Decide whether to use an existing OpenSSH key or generate a new one (recommended) for the host that will be connecting to and unlocking the encrypted ZFS machine. Copy the public key into `/etc/tinyssh/root_key` or `/etc/dropbear/root_key`. When generating the initcpio image, this file will be added to `authorized_keys` for the root user and is only valid in the initrd environment.
4.  Add the `ip=` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to your boot loader configuration. The `ip` string is [highly configurable](https://www.kernel.org/doc/Documentation/filesystems/nfs/nfsroot.txt). A simple DHCP example is shown below. `ip=:::::eth0:dhcp` 
5.  Edit `/etc/mkinitcpio.conf` to include the `netconf`, `dropbear` or `tinyssh`, and `zfsencryptssh` hooks before the `zfs` hook: `HOOKS=(... netconf <tinyssh>|<dropbear> zfsencryptssh zfs ...)` 
6.  [Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").
7.  Reboot and try it out!

#### Changing the SSH server port

By default, [mkinitcpio-tinyssh](https://www.archlinux.org/packages/?name=mkinitcpio-tinyssh) and [mkinitcpio-dropbear](https://www.archlinux.org/packages/?name=mkinitcpio-dropbear) listen on port `22`. You may wish to change this.

For **TinySSH**, copy `/usr/lib/initcpio/hooks/tinyssh` to `/etc/initcpio/hooks/tinyssh`, and find/modify the following line in the `run_hook()` function:

 `/etc/initcpio/hooks/tinyssh` 
```
/usr/bin/tcpserver -HRDl0 0.0.0.0 <new_port> /usr/sbin/tinysshd -v /etc/tinyssh/sshkeydir &

```

For **Dropbear**, copy `/usr/lib/initcpio/hooks/dropbear` to `/etc/initcpio/hooks/dropbear`, and find/modify the following line in the `run_hook()` function:

 `/etc/initcpio/hooks/tinyssh` 
```
 /usr/sbin/dropbear -E -s -j -k -p <new_port>

```

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

#### Unlocking from a Windows machine using PuTTY/Plink

First, we need to use `puttygen.exe` to import and convert the OpenSSH key generated earlier into PuTTY's *.ppk* private key format. Let us call it `zfs_unlock.ppk` for this example.

The mkinitcpio-netconf process above does not setup a shell (nor do we need need one). However, because there is no shell, PuTTY will immediately close after a successful connection. This can be disabled in the PuTTY SSH configuration (*Connection -> SSH -> [X] Do not start a shell or command at all*), but it still does not allow us to see stdout or enter the encryption passphrase. Instead, we use `plink.exe` with the following parameters:

```
plink.exe -ssh -l root -i c:\path\to\zfs_unlock.ppk <hostname>

```

The plink command can be put into a batch script for ease of use.

## See also

*   [Aaron Toponce's 17-part blog on ZFS](https://pthree.org/2012/12/04/zfs-administration-part-i-vdevs/)
*   [ZFS on Linux](http://zfsonlinux.org/)
*   [ZFS on Linux FAQ](https://github.com/zfsonlinux/zfs/wiki/faq)
*   [FreeBSD Handbook -- The Z File System](https://www.freebsd.org/doc/en_US.ISO8859-1/books/handbook/zfs.html)
*   [Oracle Solaris ZFS Administration Guide](https://docs.oracle.com/cd/E19253-01/819-5461/index.html)
*   [Solaris Internals -- ZFS Troubleshooting Guide](http://www.solarisinternals.com/wiki/index.php/ZFS_Troubleshooting_Guide)
*   [How Pingdom uses ZFS to back up 5TB of MySQL data every day](http://royal.pingdom.com/2013/06/04/zfs-backup/)
*   [Tutorial on adding the modules to a custom kernel](https://www.linuxquestions.org/questions/linux-from-scratch-13/%5Bhow-to%5D-add-zfs-to-the-linux-kernel-4175514510/)
*   [How to create cross platform ZFS disks under Linux](https://github.com/danboid/creating-ZFS-disks-under-Linux)
*   [How-To: Using ZFS Encryption at Rest in OpenZFS (ZFS on Linux, ZFS on FreeBSD, …)](https://blog.heckel.xyz/2017/01/08/zfs-encryption-openzfs-zfs-on-linux/)