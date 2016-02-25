From [Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs")

	*Btrfs (B-tree file system, variously pronounced: "Butter F S", "Better F S", "B-tree F S", or simply "Bee Tee Arr Eff Ess") is a GPL-licensed experimental copy-on-write file system for Linux. Development began at Oracle Corporation in 2007.*

From [Btrfs Wiki](https://btrfs.wiki.kernel.org/index.php/Main_Page)

	*Btrfs is a new copy on write (CoW) filesystem for Linux aimed at implementing advanced features while focusing on fault tolerance, repair and easy administration. Jointly developed at Oracle, Red Hat, Fujitsu, Intel, SUSE, STRATO and many others, Btrfs is licensed under the GPL and open for contribution from anyone.*

**Warning:**

*   Btrfs has some features that are considered experimental. See the Btrfs Wiki's [Stability status,](https://btrfs.wiki.kernel.org/index.php/Main_Page#Stability_status) [Is Btrfs stable,](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_btrfs_stable.3F) and [Getting started](https://btrfs.wiki.kernel.org/index.php/Getting_started) for more detailed information.
*   Beware of the [limitations](#Limitations).

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Additional packages](#Additional_packages)
*   [2 General administration of Btrfs](#General_administration_of_Btrfs)
    *   [2.1 Creating a new file system](#Creating_a_new_file_system)
    *   [2.2 Convert from Ext3/4](#Convert_from_Ext3.2F4)
    *   [2.3 Mount options](#Mount_options)
        *   [2.3.1 Examples](#Examples)
    *   [2.4 Displaying used/free space](#Displaying_used.2Ffree_space)
*   [3 Limitations](#Limitations)
    *   [3.1 Encryption](#Encryption)
    *   [3.2 Swap file](#Swap_file)
    *   [3.3 Linux-rt kernel](#Linux-rt_kernel)
*   [4 Features](#Features)
    *   [4.1 Commit interval settings](#Commit_interval_settings)
    *   [4.2 Copy-On-Write (CoW)](#Copy-On-Write_.28CoW.29)
    *   [4.3 Multi-device filesystem and RAID feature](#Multi-device_filesystem_and_RAID_feature)
        *   [4.3.1 Multi-device filesystem](#Multi-device_filesystem)
        *   [4.3.2 RAID features](#RAID_features)
    *   [4.4 Sub-volumes](#Sub-volumes)
        *   [4.4.1 Creating sub-volumes](#Creating_sub-volumes)
        *   [4.4.2 Listing sub-volumes](#Listing_sub-volumes)
        *   [4.4.3 Setting a default sub-volume](#Setting_a_default_sub-volume)
        *   [4.4.4 Snapshots](#Snapshots)
    *   [4.5 Defragmentation](#Defragmentation)
    *   [4.6 Compression](#Compression)
    *   [4.7 Checkpoint interval](#Checkpoint_interval)
    *   [4.8 Partitioning](#Partitioning)
    *   [4.9 Scrub](#Scrub)
        *   [4.9.1 Services](#Services)
    *   [4.10 Balance](#Balance)
    *   [4.11 SSD TRIM](#SSD_TRIM)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 GRUB](#GRUB)
        *   [5.1.1 Partition offset](#Partition_offset)
        *   [5.1.2 Missing root](#Missing_root)
    *   [5.2 BTRFS: open_ctree failed](#BTRFS:_open_ctree_failed)
    *   [5.3 btrfs check](#btrfs_check)
*   [6 See also](#See_also)

## Installation

The official kernels [linux](https://www.archlinux.org/packages/?name=linux) and [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) include support for Btrfs, user space utilities are available in [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs).

[GRUB](/index.php/GRUB "GRUB"), [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), and [Syslinux](/index.php/Syslinux "Syslinux") have support for Btrfs and require no additional configuration.

### Additional packages

*   [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) includes *btrfsck*, a tool that can fix errors on Btrfs filesystems.
*   [btrfs-progs-git](https://aur.archlinux.org/packages/btrfs-progs-git/) for nightly

**Tip:** See [Btrfs Wiki Getting Started](https://btrfs.wiki.kernel.org/index.php/Getting_started) for suggestions regarding running Btrfs effectively.

## General administration of Btrfs

### Creating a new file system

A Btrfs file system can either be newly created or have one converted.

To format a partition do:

```
# mkfs.btrfs -L *mylabel* /dev/*partition*

```

**Note:** As of [this](https://git.kernel.org/cgit/linux/kernel/git/mason/btrfs-progs.git/commit/?id=c652e4efb8e2dd76ef1627d8cd649c6af5905902) commit (November 2013), Btrfs default blocksize is 16KB.

To use a larger blocksize for data/metadata, specify a value for the `nodesize` via the `-n` switch as shown in this example using 16KB blocks:

```
# mkfs.btrfs -L *mylabel* -n 16k /dev/*partition*

```

Multiple devices can be entered to create a RAID. Supported RAID levels include RAID 0, RAID 1, RAID 10, RAID 5 and RAID 6\. The RAID levels can be configured separately for data and metadata using the `-d` and `-m` options respectively. By default the metadata is mirrored and data is striped. See [Using Btrfs with Multiple Devices](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) for more information about how to create a Btrfs RAID volume.

```
# mkfs.btrfs [*options*] /dev/*part1* /dev/*part2* ...

```

### Convert from Ext3/4

**Warning:** As of mid-to-late 2015, there are many reports on the btrfs mailing list about incomplete/corrupt/broken conversions. The situation is improving as patches are being submitted, but proceed very carefully. Make sure you have *working* backups of any data you cannot afford to lose. See [Conversion from Ext3](https://btrfs.wiki.kernel.org/index.php/Conversion_from_Ext3) on the btrfs wiki.

Boot from an install CD, then convert by doing:

```
# btrfs-convert /dev/*partition*

```

Mount the partion and test the conversion by checking the files. Be sure to change the `/etc/fstab` to reflect the change (**type** to `btrfs` and **fs_passno** [the last field] to `0` as Btrfs does not do a file system check on boot). Also note that the UUID of the partition will have changed, so update fstab accordingly when using UUIDs. `chroot` into the system and rebuild the GRUB menu list (see [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux") and [GRUB](/index.php/GRUB "GRUB") articles). If converting a root filesystem, while still chrooted run `mkinitcpio -p linux` to regenerate the initramfs or the system will not successfully boot. If you get stuck in grub with 'unknown filesystem' try reinstalling grub with `grub-install /dev/*partition*` and regenerate the config as well `grub-mkconfig -o /boot/grub/grub.cfg`.

After confirming that there are no problems, complete the conversion by deleting the backup `ext2_saved` sub-volume. Note that you cannot revert back to ext3/4 without it.

```
# btrfs subvolume delete /ext2_saved

```

Finally [balance](#Balance) the file system to reclaim the space.

### Mount options

**Warning:** Specific mount options can disable safety features and increase the risk of complete file system corruption.

See [Btrfs Wiki Mount options](https://btrfs.wiki.kernel.org/index.php/Mount_options) and [Btrfs Wiki Gotchas](https://btrfs.wiki.kernel.org/index.php/Gotchas) for more information.

In addition to configurations that can be made during or after file system creation, the various mount options for Btrfs can drastically change its performance characteristics.

As this is a file system that is still in active development, changes and regressions should be expected. See links in the [#See also](#See_also) section for some benchmarks.

#### Examples

*   **Linux 3.15**
    *   Btrfs on a SSD for system installation and an emphasis on maximizing performance (also read [#SSD TRIM](#SSD_TRIM))

    	 `noatime,discard,ssd,compress=lzo,space_cache` 

    *   Btrfs on a HDD for archival purposes with an emphasis on maximizing space.

    	 `noatime,autodefrag,compress-force=lzo,space_cache` 

### Displaying used/free space

General linux userspace tools such as `/usr/bin/df` will inaccurately report free space on a Btrfs partition since it does not take into account space allocated for and used by the metadata. It is recommended to use `/usr/bin/btrfs` to query a Btrfs partition. Below is an illustration of this effect, first querying using `df -h`, and then using `btrfs filesystem df`:

 `$ df -h /` 
```
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda3       119G  3.0G  116G   3% /

```
 `$ btrfs filesystem df /` 
```
Data: total=3.01GB, used=2.73GB
System: total=4.00MB, used=16.00KB
Metadata: total=1.01GB, used=181.83MB
```

Notice that `df -h` reports 3.0GB used but `btrfs filesystem df` reports 2.73GB for the data. This is due to the way Btrfs allocates space into the pool. The true disk usage is the sum of all three 'used' values which is inferior to 3.0GB as reported by `df -h`.

**Note:** If you see an entry of type `unknown` in the output of `btrfs filesystem df` at kernel >= 3.15, this is a display bug. As of [this patch](http://thread.gmane.org/gmane.comp.file-systems.btrfs/34419), the entry means GlobalReserve, which is kind of a buffer for changes not yet flushed. This entry is displayed as `unknown, single` in RAID setups and is not possible to re-balance.

Another useful command to show a less verbose readout of used space is `btrfs filesystem show`:

```
# btrfs filesystem show /dev/sda3

```

The newest command to get information on free/used space of a is `btrfs filesystem usage`:

```
# btrfs filesystem usage

```

**Note:** The `btrfs filesystem usage` command does not currently work correctly with `RAID5/RAID6` RAID levels.

## Limitations

A few limitations should be known before trying.

### Encryption

Btrfs has no built-in encryption support (this may come in future); users can encrypt the partition before running `mkfs.btrfs`. See [dm-crypt](/index.php/Dm-crypt "Dm-crypt").

Existing Btrfs file system, can use something like [EncFS](/index.php/EncFS "EncFS") or [TrueCrypt](/index.php/TrueCrypt "TrueCrypt"), though perhaps without some of Btrfs' features.

### Swap file

Btrfs does not yet support [swap files](/index.php/Swap#Swap_file "Swap"). This is due to swap files requiring a function that Btrfs doesn't have for possibility of file system corruption [[1]](https://btrfs.wiki.kernel.org/index.php/FAQ#Does_btrfs_support_swap_files.3F). Patches for swapfile support are already available [[2]](https://lkml.org/lkml/2014/12/9/718) and may be included in an upcoming kernel release. As an alternative a swap file can be mounted on a loop device with poorer performance but will not be able to hibernate. Install the package [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) from the [official repositories](/index.php/Official_repositories "Official repositories") to automate this.

### Linux-rt kernel

As of version 3.14.12_rt9, the [linux-rt](/index.php/Kernel#-rt "Kernel") kernel does not boot with the Btrfs file system. This is due to the slow development of the *rt* patchset.

## Features

Various features are available and can be adjusted.

### Commit interval settings

The resolution at which data are written to the filesystem is dictated by Btrfs itself and by system-wide settings. Btrfs defaults to a 30 seconds checkpoint interval in which new data are committed to the filesystem. This is tuneable using mount options (see below)

System-wide settings also affect commit intervals. They include the files under `/proc/sys/vm/*` and are out-of-scope of this wiki article. The kernel documentation for them resides in `Documentation/sysctl/vm.txt`.

### Copy-On-Write (CoW)

By default, Btrfs performs copy-on-write for all files, at all times: If you write a file that did not exist before, then the data is written to empty space, and some of the metadata blocks that make up the filesystem are copied-on-write. In a traditional filesystem, if you then go back and overwrite a piece of that file, then the piece you are writing is put directly over the data it is replacing. In a CoW filesystem, the new data is written to a piece of free space on the disk, and only then is the file's metadata changed to refer to the new data. The old data that was replaced can then be freed up if nothing points to it any more.

Copy-on-write comes with some advantages, but can negatively affect performance with large files that have small random writes because it will fragment them (even if no "copy" is ever performed!). It is recommended to disable copy-on-write for database files and virtual machine images.

One can disable copy-on-write for the entire block device by mounting it with `nodatacow` option. However, this will disable copy-on-write for the entire file system.

**Note:** `nodatacow` will only affect newly created files. Copy-on-write may still happen for existing files.

To disable copy-on-write for single files/directories do:

```
$ chattr +C */dir/file*

```

This will disable copy-on-write for those operation in which there is only one reference to the file. If there is more than one reference (e.g. through `cp --reflink=always` or because of a filesystem snapshot), copy-on-write still occurs.

**Note:** From chattr man page: For Btrfs, the 'C' flag should be set on new or empty files. If it is set on a file which already has data blocks, it is undefined when the blocks assigned to the file will be fully stable. If the 'C' flag is set on a directory, it will have no effect on the directory, but new files created in that directory will have the `No_COW` attribute.

**Tip:** In accordance with the note above, you can use the following trick to disable copy-on-write on existing files in a directory:
```
$ mv */path/to/dir* */path/to/dir*_old
$ mkdir */path/to/dir*
$ chattr +C */path/to/dir*
$ cp -a */path/to/dir*_old/* */path/to/dir*
$ rm -rf */path/to/dir*_old

```

Make sure that the data are not used during this process. Also note that `mv` or `cp --reflink` as described below will not work.

Likewise, to save space by forcing copy-on-write when copying files use:

```
$ cp --reflink *source* *dest* 

```

As `*dest*` file is changed, only those blocks that are changed from source will be written to the disk. One might consider aliasing *cp* to `cp --reflink=auto`.

### Multi-device filesystem and RAID feature

See [Using Btrfs with Multiple Devices](https://btrfs.wiki.kernel.org/index.php/Using_Btrfs_with_Multiple_Devices) for suggestions.

#### Multi-device filesystem

**Note:** Mounting such a filesystem may result in all but one of the according *.device*-jobs getting stuck and systemd never finishing startup due to a [bug](https://github.com/systemd/systemd/issues/1921) in handling this type of filesystem.

When creating a Btrfs filesystem, one can pass many partitions or disk devices to *mkfs.btrfs*. The filesystem will be created across these devices. One can **"**pool**"** this way, multiple partitions or devices to get a single Btrfs filesystem.

One can also add or remove device from an existing Btrfs filesystem (caution is mandatory).

#### RAID features

**Note:** As of kernel 3.19, the recovery and rebuild code has been integrated. This brings the implementation to the point where it should be usable for most purposes. Since this is new code, you should expect it to stabilize over the next couple of kernel releases.

When creating a multi-device filesystem, one can also specify to use RAID0, RAID1, RAID10, RAID5 or RAID6 across the devices comprising the filesystem. RAID levels can be applied independently to data and metadata. By default, metadata is duplicated on single volumes or RAID1 on multi-disk sets.

Btrfs works in block-pairs for raid0, raid1, and raid10\. This means:

raid0 - block-pair striped across 2 devices

raid1 - block-pair written to 2 devices

The raid level can be changed while the disks are online using the `btrfs balance` command:

```
# btrfs balance start -mconvert=RAIDLEVEL -dconvert=RAIDLEVEL /path/to/mount

```

For 2 disk sets, this matches raid levels as defined in md-raid (mdadm). For 3+ disk-sets, the result is entirely different than md-raid.

For example:

*   Three 1TB disks in an md based raid1 yields a `/dev/md0` with 1TB free space and the ability to safely lose 2 disks without losing data.
*   Three 1TB disks in a Btrfs volume with data=raid1 will allow the storage of approximately 1.5TB of data before reporting full. Only 1 disk can safely be lost without losing data.

Btrfs uses a round-robin scheme to decide how block-pairs are spread among disks. As of Linux 3.0, a quasi-round-robin scheme is used which prefers larger disks when distributing block pairs. This allows raid0 and raid1 to take advantage of most (and sometimes all) space in a disk set made of multiple disks. For example, a set consisting of a 1TB disk and 2 500GB disks with data=raid1 will place a copy of every block on the 1TB disk and alternate (round-robin) placing blocks on each of the 500GB disks. Full space utilization will be made. A set made from a 1TB disk, a 750GB disk, and a 500GB disk will work the same, but the filesystem will report full with 250GB unusable on the 750GB disk. To always take advantage of the full space (even in the last example), use data=single. (data=single is akin to JBOD defined by some raid controllers) See [the Btrfs FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ#How_much_space_do_I_get_with_unequal_devices_in_RAID-1_mode.3F) for more info.

### Sub-volumes

See the following links for more details:

*   [Btrfs Wiki SysadminGuide#Subvolumes](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Subvolumes)
*   [Btrfs Wiki Getting started#Basic Filesystem Commands](https://btrfs.wiki.kernel.org/index.php/Getting_started#Basic_Filesystem_Commands)
*   [Btrfs Wiki Trees](https://btrfs.wiki.kernel.org/index.php/Trees)

#### Creating sub-volumes

To create a sub-volume:

```
# btrfs subvolume create */path/to/subvolume*

```

#### Listing sub-volumes

To see a list of current sub-volumes:

```
# btrfs subvolume list -p .

```

#### Setting a default sub-volume

**Warning:** Changing the default subvolume with `btrfs subvolume set-default` will make the top level of the filesystem inaccessible, except by use of the `subvolid=0` mount option. Reference: [Btrfs Wiki Sysadmin Guide](https://btrfs.wiki.kernel.org/index.php/SysadminGuide).

The default sub-volume is mounted if no `subvol=` mount option is provided.

```
# btrfs subvolume set-default *subvolume-id* /.

```

**Example:**

 `# btrfs subvolume list .` 
```
ID 258 gen 9512 top level 5 path root_subvolume
ID 259 gen 9512 top level 258 path home
ID 260 gen 9512 top level 258 path var
ID 261 gen 9512 top level 258 path usr

```

```
# btrfs subvolume set-default 258 .

```

**Reset:**

```
# btrfs subvolume set-default 0 .

```

#### Snapshots

See [Btrfs Wiki SysadminGuide#Snapshots](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Snapshots) for details.

To create a snapshot:

```
# btrfs subvolume snapshot *source* [*dest*/]*name*

```

Snapshots are not recursive. Every sub-volume inside sub-volume will be an empty directory inside the snapshot.

### Defragmentation

Btrfs supports online defragmentation. To defragment the metadata of the root folder:

```
# btrfs filesystem defragment /

```

This *will not* defragment the entire file system. For more information read [this page](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ#Defragmenting_a_directory_doesn.27t_work) on the Btrfs wiki.

To defragment the entire file system verbosely:

```
# btrfs filesystem defragment -r -v /

```

### Compression

Btrfs supports transparent compression, meaning every file on the partition is automatically compressed. This not only reduces the size of files, but also [improves performance](http://www.phoronix.com/scan.php?page=article&item=btrfs_compress_2635&num=1), in particular if using the [lzo algorithm](http://www.phoronix.com/scan.php?page=article&item=btrfs_lzo_2638&num=1), in some specific use cases (e.g. single thread with heavy file IO), while obviously harming performance on other cases (e.g. multithreaded and/or cpu intensive tasks with large file IO).

Compression is enabled using the `compress=zlib` or `compress=lzo` mount options. Only files created or modified after the mount option is added will be compressed. However, it can be applied quite easily to existing files (e.g. after a conversion from ext3/4) using the `btrfs filesystem defragment -c*alg*` command, where `*alg*` is either `zlib` or `lzo`. In order to re-compress the whole file system with `lzo`, run the following command:

```
# btrfs filesystem defragment -r -v -clzo /

```

**Tip:** Compression can also be enabled per-file without using the `compress` mount option; simply apply `chattr +c` to the file. When applied to directories, it will cause new files to be automatically compressed as they come.

When installing Arch to an empty Btrfs partition, use the `compress` option when [mounting the filesystem](/index.php/Beginners%27_guide#Format_file_systems_and_enable_swap "Beginners' guide"): `mount -o compress=lzo /dev/sd*xY* /mnt/`. During [configuration](/index.php/Beginners%27_guide#Configuration "Beginners' guide"), add `compress=lzo` to the mount options of the root file system in [fstab](/index.php/Fstab "Fstab").

### Checkpoint interval

Starting with Linux 3.12, users are able to change the checkpoint interval from the default 30 s to any value by appending the `commit` mount option in `/etc/fstab` for the btrfs partition.

```
LABEL=arch64 / btrfs defaults,noatime,ssd,compress=lzo,commit=120 0 0

```

### Partitioning

Btrfs can occupy an entire data storage device, replacing the [MBR](/index.php/MBR "MBR") or [GPT](/index.php/GPT "GPT") partitioning schemes. One can use [subvolumes](#Sub-volumes) to simulate partitions. There are some limitations to this approach in single disk setups:

*   Cannot use different [file systems](/index.php/File_systems "File systems") for different [mount points](/index.php/Fstab "Fstab").
*   Cannot use [swap area](/index.php/Swap "Swap") as Btrfs does not support [swap files](/index.php/Swap#Swap_file "Swap") and there is no place to create [swap partition](/index.php/Swap#Swap_partition "Swap"). This also limits the use of hibernation/resume, which needs a swap area to store the hibernation image.
*   Cannot use [UEFI](/index.php/UEFI "UEFI") to boot.

To overwrite the existing partition table with Btrfs, run the following command:

```
# mkfs.btrfs /dev/sd*X*

```

Do not specify `/dev/sda*X*` or it will format an existing partition instead of replacing the entire partitioning scheme.

Install the [boot loader](/index.php/Boot_loader "Boot loader") in a like fashion to installing it for a data storage device with a [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record"). For example:

```
# grub-install --recheck /dev/sd*X*

```

for [GRUB](/index.php/GRUB#Install_to_440-byte_MBR_boot_code_region "GRUB").

**Warning:** Using the `btrfs subvolume set-default` command to change the default sub-volume from anything other than the top level (ID 0) may break Grub. See [#Setting a default sub-volume](#Setting_a_default_sub-volume) to reset.

### Scrub

See [Btrfs Wiki Glossary](https://btrfs.wiki.kernel.org/index.php/Glossary).

```
# btrfs scrub start /
# btrfs scrub status /

```

**Warning:** The running scrub process will prevent the system from suspending, see [this thread](http://comments.gmane.org/gmane.comp.file-systems.btrfs/33106) for details.

#### Services

The [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) package brings the `btrfs-scrub@.timer` unit for monthly scrubbing the specified mountpoint. [Enable](/index.php/Enable "Enable") the timer with an encoded path, e.g. `btrfs-scrub@-.timer` for `/` and `btrfs-scrub@home.timer` for `/home`.

You can also run the scrub manually by [starting](/index.php/Starting "Starting") `btrfs-scrub@.service` (with the same encoded path). The advantage of this over `# btrfs scrub` is that the results of the scrub will be logged in the [systemd journal](/index.php/Systemd_journal "Systemd journal").

### Balance

See [Upstream FAQ page](https://btrfs.wiki.kernel.org/index.php/FAQ#What_does_.22balance.22_do.3F).

Since [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)-3.12 *balancing* is a background process - see `man 8 btrfs-balance` for full description.

```
# btrfs balance start /
# btrfs balance status /

```

### SSD TRIM

A Btrfs filesystem will automatically free unused blocks from an SSD drive supporting the TRIM command.

More information about enabling and using TRIM can be found in [Solid State Drives#TRIM](/index.php/Solid_State_Drives#TRIM "Solid State Drives").

## Troubleshooting

See the [Btrfs Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ) for general troubleshooting.

### GRUB

#### Partition offset

**Note:** The offset problem may happen when you try to embed `core.img` into a partitioned disk. It means that [it is OK](https://wiki.archlinux.org/index.php?title=Talk:Btrfs&diff=319474&oldid=292530) to embed grub's `corg.img` into a Btrfs pool on a partitionless disk (e.g. `/dev/sd*X*`) directly.

[GRUB](/index.php/GRUB "GRUB") can boot Btrfs partitions however the module may be larger than other [file systems](/index.php/File_systems "File systems"). And the `core.img` file made by `grub-install` may not fit in the first 63 sectors (31.5KiB) of the drive between the MBR and the first partition. Up-to-date partitioning tools such as `fdisk` and `gdisk` avoid this issue by offsetting the first partition by roughly 1MiB or 2MiB.

#### Missing root

Users experiencing the following: `error no such device: root` when booting from a RAID style setup then edit /usr/share/grub/grub-mkconfig_lib and remove both quotes from the line `echo " search --no-floppy --fs-uuid --set=root ${hints} ${fs_uuid}"`. Regenerate the config for grub and the system should boot without an error.

### BTRFS: open_ctree failed

As of November 2014 there seems to be a bug in [systemd](/index.php/Systemd "Systemd") or [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") causing the following error on systems with multi-device Btrfs filesystem using the `btrfs` hook in `mkinitcpio.conf`:

```
BTRFS: open_ctree failed
mount: wrong fs type, bad option, bad superblock on /dev/sdb2, missing codepage or helper program, or other error

In some cases useful info is found in syslog - try dmesg|tail or so.

You are now being dropped into an emergency shell.

```

A workaround is to remove `btrfs` from the `HOOKS` array in `/etc/mkinitcpio.conf` and instead add `btrfs` to the `MODULES` array. Then regenerate the initramfs with `mkinitcpio -p linux` (adjust the preset if needed) and reboot.

See the [original forums thread](https://bbs.archlinux.org/viewtopic.php?id=189845) and [FS#42884](https://bugs.archlinux.org/task/42884) for further information and discussion.

You will get the same error if you try to mount a raid array without one of the devices. In that case you must add the `degraded` mount option to `/etc/fstab`. If your root resides on the array, you must also add `rootflags=degraded` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### btrfs check

**Warning:** Since Btrfs is under heavy development, especially the `btrfs check` command, it is highly recommended to create a **backup** and consult the following Btfrs documentation before executing `btrfs check` with the `--repair` switch.

The *[btrfs check](https://btrfs.wiki.kernel.org/index.php/Manpage/btrfs-check)* command can be used to check or repair an unmounted Btrfs filesystem. However, this repair tool is still immature and not able to repair certain filesystem errors even those that do not render the filesystem unmountable.

See [Btrfsck](https://btrfs.wiki.kernel.org/index.php/Btrfsck) for more information.

## See also

*   **Official site**
    *   [Btrfs Wiki](https://btrfs.wiki.kernel.org/)
    *   [Btrfs Wiki Glossary](https://btrfs.wiki.kernel.org/index.php/Glossary)
*   **Official FAQs**
    *   [Btrfs Wiki FAQ](https://btrfs.wiki.kernel.org/index.php/FAQ)
    *   [Btrfs Wiki Problem FAQ](https://btrfs.wiki.kernel.org/index.php/Problem_FAQ)
*   **Btrfs pull requests**
    *   [3.14](http://lkml.indiana.edu/hypermail/linux/kernel/1401.3/03045.html)
    *   [3.13](http://lkml.indiana.edu/hypermail/linux/kernel/1311.1/03526.html)
    *   [3.12](http://lkml.indiana.edu/hypermail/linux/kernel/1309.1/02981.html)
    *   [3.11](http://lkml.indiana.edu/hypermail/linux/kernel/1305.1/01064.html)
*   **Performance related**
    *   [Btrfs on raw disks?](http://superuser.com/questions/432188/should-i-put-my-multi-device-btrfs-filesystem-on-disk-partitions-or-raw-devices)
    *   [Varying leafsize and nodesize in Btrfs](http://comments.gmane.org/gmane.comp.file-systems.btrfs/19440)
    *   [Btrfs support for efficient SSD operation (data blocks alignment)](http://comments.gmane.org/gmane.comp.file-systems.btrfs/15646)
    *   [Is Btrfs optimized for SSDs?](https://btrfs.wiki.kernel.org/index.php/FAQ#Is_Btrfs_optimized_for_SSD.3F)
    *   **Phoronix mount option benchmarking**
        *   [Linux 3.14](http://www.phoronix.com/scan.php?page=article&item=linux_314_btrfs)
        *   [Linux 3.11](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_311&num=1)
        *   [Linux 3.9](http://www.phoronix.com/scan.php?page=news_item&px=MTM0OTU)
        *   [Linux 3.7](http://www.phoronix.com/scan.php?page=article&item=btrfs_linux37_mounts&num=1)
        *   [Linux 3.2](http://www.phoronix.com/scan.php?page=article&item=linux_btrfs_options&num=1)
    *   [Lzo vs. zLib](http://blog.erdemagaoglu.com/post/4605524309/lzo-vs-snappy-vs-lzf-vs-zlib-a-comparison-of)
*   **Miscellaneous**
    *   [Funtoo Wiki Btrfs Fun](http://www.funtoo.org/wiki/BTRFS_Fun)
    *   [Avi Miller presenting Btrfs](http://www.phoronix.com/scan.php?page=news_item&px=MTA0ODU) at SCALE 10x, January 2012.
    *   [Summary of Chris Mason's talk](http://www.phoronix.com/scan.php?page=news_item&px=MTA4Mzc) from LFCS 2012
    *   [Btrfs: stop providing a bmap operation to avoid swapfile corruptions](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=commit;h=35054394c4b3cecd52577c2662c84da1f3e73525) 2009-01-21
    *   [Doing Fast Incremental Backups With Btrfs Send and Receive](http://marc.merlins.org/perso/btrfs/post_2014-03-22_Btrfs-Tips_-Doing-Fast-Incremental-Backups-With-Btrfs-Send-and-Receive.html)