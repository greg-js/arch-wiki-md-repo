[Bcache](https://bcache.evilpiepirate.org/) (block cache) allows one to use an SSD as a read/write cache (in writeback mode) or read cache (writethrough or writearound) for another blockdevice (generally a rotating HDD or array). This article will show how to install arch using Bcache as the root partition. For an intro to bcache itself, see [the bcache homepage](http://bcache.evilpiepirate.org/). Be sure to read and reference [the bcache manual](https://evilpiepirate.org/git/linux-bcache.git/tree/Documentation/bcache.txt). Bcache is in the mainline kernel since 3.10\. The kernel on the arch install disk includes the bcache module since 2013.08.01.

An alternative to Bcache is Facebook's [Flashcache](/index.php/Flashcache "Flashcache") and its offspring [EnhanceIO](/index.php/EnhanceIO "EnhanceIO"). Another alternative - [btier-dkms](https://aur.archlinux.org/packages/btier-dkms/).

Bcache needs the backing device to be formatted as a bcache block device. In most cases, [blocks to-bcache](https://github.com/g2p/blocks) can do an in-place conversion.

**Warning:**

*   Be sure you back up any important data first.
*   The bcache-dev branch is under heavy development. The on-disk format has undergone changes in 3.18 which are not backwards compatible with previous formats[[1]](http://www.spinics.net/lists/linux-bcache/msg02721.html). Note: This only applies to users who compile-in bcache-dev. The version built-in to the upstream Linux kernel is unaffected[[2]](http://www.spinics.net/lists/linux-bcache/msg02724.html).
*   Bcache and [btrfs](/index.php/Btrfs "Btrfs") could leave you with a corrupted filesystem. Please visit [this post](https://www.hdevalence.ca/blog/2013-09-21-notes-on-my-archlinux-install) for more information. Btrfs wiki reports that it was fixed in kernels 3.19+ [[3]](https://btrfs.wiki.kernel.org/index.php/Gotchas#Historical_references).

## Contents

*   [1 Setting up a bcache device on an existing system](#Setting_up_a_bcache_device_on_an_existing_system)
    *   [1.1 Bcache management](#Bcache_management)
    *   [1.2 Converting existing disks](#Converting_existing_disks)
        *   [1.2.1 Troubleshooting](#Troubleshooting)
*   [2 Installation to a bcache device](#Installation_to_a_bcache_device)
*   [3 Accessing from the install disk](#Accessing_from_the_install_disk)
*   [4 Configuring](#Configuring)
*   [5 Advanced operations](#Advanced_operations)
    *   [5.1 Resize backing device](#Resize_backing_device)
        *   [5.1.1 Example of growing](#Example_of_growing)
        *   [5.1.2 Example of shrinking](#Example_of_shrinking)
            *   [5.1.2.1 Force flush of cache to backing device](#Force_flush_of_cache_to_backing_device)
*   [6 Troubleshooting](#Troubleshooting_2)
    *   [6.1 /dev/bcache device does not exist on bootup](#/dev/bcache_device_does_not_exist_on_bootup)
    *   [6.2 /sys/fs/bcache/ does not exist](#/sys/fs/bcache/_does_not_exist)
*   [7 See also](#See_also)

## Setting up a bcache device on an existing system

**Warning:** make-bcache **will not** import an existing drive or partition – it will reformat it. If you want to use an existing data partition as backing device, see [#Converting existing disks](#Converting_existing_disks).

1\. [Install](/index.php/Install "Install") the [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/) package from [AUR](/index.php/AUR "AUR").

2\. Create a backing device (This will typically be your mechanical drive). The backing device can be a whole device, a partition or any other standard block device. This will create /dev/bcache0

```
   # make-bcache -B /dev/sdx1

```

3\. Create a cache device (This will typically be your SSD). The cache device can be a whole device, a partition or any other standard block device

```
   # make-bcache -C /dev/sdy2

```

In this example the default block and bucket sizes of 512B and 128kB are used. The block size should match the backing devices sector size which will usually be either 512 or 4k. The bucket size should match the erase block size of the caching device with the intent of reducing write amplification. For example, using a HDD with 4k sectors and an SSD with an erase block size of 2MB this command would look like

```
   # make-bcache --block 4k --bucket 2M -C /dev/sdy2

```

4\. Register the cache device against your backing device. To find its *cache set UUID*, run `# bcache-super-show /dev/sdy2 | grep cset.uuid` and then add it to the bcache device initially. Udev rules will take care of this on reboot and will only need to be done once.

```
   # echo **cset.uuid** > /sys/block/bcache0/bcache/attach

```

5\. Change your cache mode (if you want to cache writes as well as reads):

```
   # echo writeback > /sys/block/bcache0/bcache/cache_mode

```

6\. If you want to have this partition available during the initcpio (i.e. you require it at some point in the boot process) you need to add 'bcache' to your modules array in /etc/mkinitcpio.conf as well as adding the 'bcache' hook in your list between block and filesystems. You must then rebuild the initramfs image. This is typically done with

```
   # mkinitcpio -p linux

```

### Bcache management

1\. Check that everything has been correctly setup

```
   # cat /sys/block/bcache0/bcache/state

```

The output can be:

*   **no cache**: this means you have not attached a caching device to your backing bcache device
*   **clean**: this means everything is ok. The cache is clean.
*   **dirty**: this means everything is setup fine and that you have enabled *writeback* and that the cache is dirty.
*   **inconsistent**: you are in trouble because the backing device is not in sync with the caching device

You can have a `/dev/bcache0` device associated with a backing device with no caching device attached. This means that all I/O (read/write) are passed directly to the backing device (pass-through mode)

2\. See what caching mode is in use

```
# cat /sys/block/bcache0/bcache/cache_mode 
[writethrough] writeback writearound none

```

In the above example, the *writethrough* mode is enabled.

3\. Show info about a bcached device:

```
   # bcache-super-show /dev/sdXY

```

4\. Stop the backing device:

```
   # echo 1 > /sys/block/sdX/sdX[Y]/bcache/stop

```

5\. Detach a caching device:

```
   # echo 1 > /sys/block/sdX/sdX[Y]/bcache/detach

```

6\. Safely remove the cache device

```
   # echo <cache-set-uuid> > /sys/block/bcache0/bcache/detach

```

7\. Release attached devices

```
   # echo 1 > /sys/fs/bcache/<cache-set-uuid>/stop

```

### Converting existing disks

**Warning:**

*   it is widely recommended to use Bcache underneath any other block layer.
*   the **blocks** package is broken with Python3\. Please visit [this thread](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=769737) for a workaround, or use [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv").
*   when on top of a **LVM2** layer, the *discard* mount option may not be handled well.

With `blocks`, you can add a Bcache layer on a device with an existing filesystem or layer (normal partition, LUKS partition, logical volume).

First, install the [blocks-git](https://aur.archlinux.org/packages/blocks-git/) package from [AUR](/index.php/AUR "AUR").

*blocks* needs to add the **bcache** metadata at the start of the targeted partition, here `/dev/sdz4`; to be able to do so, it will resize the partition just before the targeted one (`/dev/sdz3`) to make necessary room, typically 2048 bits (2k). It will ask for your passphrase if the partition(`/dev/sdz3`) is an LUKS partition. Then it will recreate another partition with the start just lower of 2048 bits and run *make-bcache*, so you do not need to run it yourself.

```
   # blocks to-bcache /dev/sdz4

```

You can check that everything is ok by running:

```
   # bcache-super-show /dev/sdz4

```

which should output metadata about the new backing **bcache** device

You can proceed to create the caching device and attach it to the backing device.

#### Troubleshooting

If `blocks` complains about *overlapping metadata* when running `blocks to-bcache`, you will need to shrink by 100Mb the partition you want to cache and create a new 100Mb free partition.

## Installation to a bcache device

1\. Boot on the install disk (2013.08.01 minimum).

2\. Install the [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/) package from [AUR](/index.php/AUR "AUR").

3\. Partition your hdd

**Note:** While it may be true that Grub2 does not offer support for bcache as noted below, it does, however, fully support UEFI. It follows then, that so long as the necessary modules for the linux kernel to properly handle your boot device are either compiled into the kernel or are included in an initramfs, and you can include these files on it, the separate boot partition described below may be omitted in favor of the FAT EFI system partition. See [GRUB](/index.php/GRUB "GRUB") and/or [UEFI](/index.php/UEFI "UEFI") for more.

grub cannot handle bcache, so you will need at least 2 partitions (boot and one for the bcache backing device). If you are doing UEFI, you will need an [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) as well. E.g.:

```
     1            2048           22527   10.0 MiB    EF00  EFI System
     2           22528          432127   200.0 MiB   8300  arch_boot
     3          432128       625142414   297.9 GiB   8300  bcache_backing

```

**Note:** This example has no swapfile/partition. For a swap partition on the cache, use LVM in step 7\. For a swap partition outside the cache, be sure to make a swap partition now.

4\. Configure your HDD as a bcache backing device.

```
# make-bcache -B /dev/sda3

```

**Note:**

*   When preparing any boot disk it is important to know the ramifications of any decision you may make. Please review and review again the documentation for your chosen boot-loader/-manager and consider seriously how it might relate to bcache.
*   If all associated disks are partitioned at once as below bcache will automatically attach "-B backing stores" to the "-C ssd cache" and step 5 is unnecessary.

```
# make-bcache -B /dev/sd? /dev/sd? -C /dev/sd?

```

You now have a `/dev/bcache0` device.

5\. Configure your SSD

Format the SSD as a caching device and link it to the backing device

```
# make-bcache -C /dev/sdb
# echo /dev/sdb > /sys/fs/bcache/register 
# echo *UUID__from_previous_command* > /sys/block/bcache0/bcache/attach

```

**Note:** If the UUID is forgotten, it can be found with `ls /sys/fs/bcache/` after the cache device has been registered.

6\. Format the bcache device. Use LVM or btrfs subvolumes if you want to divide up the `/dev/bcache0` device how you like (ex for separate `/`, `/home`, `/var`, etc):

```
# mkfs.btrfs /dev/bcache0
# mount /dev/bcache0 /mnt/
# btrfs subvolume create /mnt/root
# btrfs subvolume create /mnt/home
# umount /mnt

```

You can even setup LUKS on it if you want using e.g. cryptsetup. Referencing the bcache device in the 'cryptdevice' kernel option will work fine, for instance.

7\. Prepare the installation mount point:

```
# mkfs.ext4 /dev/sda2
# mkfs.msdos /dev/sda1 (if your ESP is at least 500MB, use mkfs.vfat to make a FAT32 partition instead)
# pacman -S arch-install-scripts
# mount /dev/bcache0 -o subvol=root,compress=lzo /mnt/
# mkdir /mnt/boot /mnt/home
# mount /dev/bcache0 -o subvol=home,compress=lzo /mnt/home
# mount /dev/sda2 /mnt/boot
# mkdir /boot/efi
# mount /dev/sda1 /mnt/boot/efi/

```

8\. Install the system as per the [Installation Guide](/index.php/Installation_guide#Connect_to_the_Internet "Installation guide") as normal except this:

Before you edit `/etc/mkinitcpio.conf` and run `mkinitcpio -p linux`:

*   install [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/) package from the [AUR](/index.php/AUR "AUR") on the new system.
*   Edit `/etc/mkinitcpio.conf`:
    *   add the "bcache" module
    *   add the "bcache" hook between block and filesystem hooks

**Note:** Should you want to open the backing device from the installation media for any reason after a reboot you must register it manually. Make sure the bcache module is loaded and then echo the relevant devices to /sys/bcache/register. You should see whether this worked or not by using dmesg.

## Accessing from the install disk

This is how to access a bcache partition from the install disk that was present before the install disk was booted. Boot the install disk and install [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/) from the AUR, just as in the previous section. Then, add the module to the kernel:

```
# modprobe bcache

```

Your device will not appear immediately at `/dev/bcache*`. To force the kernel to find it, tell it to reread the partition table:

```
# partprobe

```

Now, `/dev/bcache*` should be present, and you can carry on mounting, reformatting, etc. from here.

## Configuring

There are many options that can be configured (such as cache mode, cache flush interval, sequential write heuristic, etc.) This is currently done by writing to files in `/sys`. See the [bcache user documentation](https://evilpiepirate.org/git/linux-bcache.git/tree/Documentation/bcache.txt).

Changing the cache mode is done by echoing one of 'writethrough', 'writeback', 'writearound' or 'none' to /sys/block/bcache[0-9]/bcache/cache_mode.

Note that some changes to /sys are temporary, and will revert back after a reboot (It seems that at least cache_mode does not need this workaround). To set custom configurations at boot create a .conf file in `/etc/tmpfile.d`. To set, in a persistent fashion, the sequential cutoff for bcache0 to 1 MB and write back you could create a file `/etc/tmpfile.d/my-bcache.conf` with the contents

```
  w /sys/block/bcache0/bcache/sequential_cutoff - - - - 1M
  w /sys/block/bcache0/bcache/cache_mode        - - - - writeback

```

## Advanced operations

### Resize backing device

It is possible to resize the backing device so long as you do not move the partition start. This process is described on [the mailing list](http://comments.gmane.org/gmane.linux.kernel.bcache.devel/249). Here is an example using btrfs volume directly on bcache0\. For LVM containers or for other filesystems, procedure will differ.

#### Example of growing

In this example, I grow the filesystem by 4GB.

1\. Reboot to a live CD/USB Drive (need not be bcache enabled) and use fdisk, gdisk, parted, or your other favorite tool to delete the backing partition and recreate it with the same start and a total size 4G larger.

**Warning:** Do not use a tool like GParted that might perform filesystem operations! It will not recognize the bcache partition and might overwrite part of it!!

2\. Reboot to your normal install. Your filesystem will be currently mounted. That is fine. Issue the command to resize the partition to its maximum. For btrfs, that is

```
# btrfs filesystem resize max /

```

For ext3/4, that is:

```
# resize2fs /dev/bcache0

```

#### Example of shrinking

In this example, I shrink the filesystem by 4GB.

1\. Disable writeback cache (switch to writethrough cache) and wait for the disk to flush.

```
# echo writethrough > /sys/block/bcache0/bcache/cache_mode
$ watch cat /sys/block/bcache0/bcache/state

```

wait until state reports "clean". This might take a while.

###### Force flush of cache to backing device

I suggest to use

```
 # echo 0 > /sys/block/bcache0/bcache/writeback_percent

```

This will flush the dirty data of the cache to the backing device in less a minute.

Revert back the value after with

```
 # echo 10 > /sys/block/bcache0/bcache/writeback_percent

```

2\. Shrink the mounted filesystem by something more than the desired amount, to ensure we do not accidentally clip it later. For btrfs, that is:

```
# btrfs filesystem resize -5G /

```

For ext3/4 you can use *resize2fs*, but only if the partition is unmounted

```
$ df -h /home
/dev/bcache0    290G   20G   270G   1% /home
# umount /home
# resize2fs /dev/bcache0 283G

```

3\. Reboot to a LiveCD/USB drive (does not need to support bcache) and use fdisk, gdisk, parted, or your other favorite tool to delete the backing partition and recreate it with the same start and a total size 4G smaller.

**Warning:** Do not use a tool like GParted that might perform filesystem operations! It will not recognize the bcache partition and might overwrite part of it!!

4\. Reboot to your normal install. Your filesystem will be currently mounted. That is fine. Issue the command to resize the partition to its maximum (that is, the size we shrunk the actual partition to in step 3). For btrfs, that is:

```
# btrfs filesystem resize max /

```

For ext3/4, that is:

```
# resize2fs /dev/bcache0

```

5\. Re-enable writeback cache if you want that enabled:

```
# echo writeback > /sys/block/bcache0/bcache/cache_mode

```

**Note:** If you are very careful you can shrink the filesystem to the exact size in step 2 and avoid step 4\. Be careful, though, many partition tools do not do exactly what you want, but instead adjust the requested partition start/end points to end on sector boundaries. This may be difficult to calculate ahead of time

## Troubleshooting

### /dev/bcache device does not exist on bootup

If you are sent to a busy box shell with an error:

```
ERROR: Unable to find root device 'UUID=b6b2d82b-f87e-44d5-bbc5-c51dd7aace15'.
You are being dropped to a recovery shell
    Type 'exit' to try and continue booting
```

This might happen if the backing device is configured for "writeback" mode (default is writearound). When in "writeback" mode, the /dev/bcache0 device is not started until the cache device is both registered and attached. Registering is something that needs to happen every bootup, but attaching should only have to be done once.

To continue booting, try one of the following:

*   Register both the backing device and the caching device

```
# echo /dev/sda3 > /sys/fs/bcache/register
# echo /dev/sdb > /sys/fs/bcache/register

```

If the /dev/bcache0 device now exists, type exit and continue booting. You will need to fix your initcpio to ensure devices are registered before mounting the root device.

**Note:**

*   An error of "sh: echo: write error: Invalid argument" means the device was already registered or is not recognized as either a bcache backing device or cache. If using the udev rule on boot it should only attempt to register a device if it finds a bcache superblock
*   This can also happen if using udev's 69-bcache.rules in Installation's step 7 and blkid and bcache-probe "disagree" due to rogue superblocks. See [bcache's wiki](http://bcache.evilpiepirate.org/#index6h1) for a possible explanation/resolution.

*   Re-attach the cache to the backing device:

If the cache device was registered, a folder with the UUID of the cache should exist in `/sys/fs/bcache`. Use that UUID when following the example below:

```
# ls /sys/fs/bcache/
b6b2d82b-f87e-44d5-bbc5-c51dd7aace15     register     register_quiet
# echo b6b2d82b-f87e-44d5-bbc5-c51dd7aace15 > /sys/block/sda/sda3/bcache/attach

```

If the `/dev/bcache0` device now exists, type exit and continue booting. You should not have to do this again. If it persists, ask on the bcache mailing list.

**Note:** An error of `sh: echo: write error: Invalid argument` means the device was already attached. An error of `sh: echo: write error: No such file or directory` means the UUID is not a valid cache (make sure you typed it correctly).

*   Invalidate the cache and force the backing device to run without it. You might want to check some stats, such as "dirty_data" so you have some idea of how much data will be lost.

```
# cat /sys/block/sda/sda3/bcache/dirty_data
-3.9M

```

dirty data is data in the cache that has not been written to the backing device. If you force the backing device to run, this data will be lost, even if you later re-attach the cache.

```
# cat /sys/block/sda/sda3/bcache/running
0
# echo 1 > /sys/block/sda/sda3/bcache/running

```

The `/dev/bcache0` device will now exist. Type exit and continue booting. You might want to unregister the cache device and run make-bcache again. An fsck on `/dev/bcache0` would also be wise. See the [bcache user documentation](http://atlas.evilpiepirate.org/git/linux-bcache.git/tree/Documentation/bcache.txt?h=bcache).

**Warning:** Only invalidate the cache if one of the two options above did not work.

### /sys/fs/bcache/ does not exist

The kernel you booted is not bcache enabled, or you the bcache [module is not loaded](/index.php/Kernel_module#Manual_module_handling "Kernel module")

## See also

*   [Bcache Homepage](http://bcache.evilpiepirate.org)
*   [Bcache Manual](https://www.kernel.org/doc/Documentation/bcache.txt)