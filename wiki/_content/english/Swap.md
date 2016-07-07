This page provides an introduction to swap space and paging on GNU/Linux. It covers creation and activation of swap partitions and swap files.

From [All about Linux swap space](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	Linux divides its physical RAM (random access memory) into chunks of memory called pages. Swapping is the process whereby a page of memory is copied to the preconfigured space on the hard disk, called swap space, to free up that page of memory. The combined sizes of the physical memory and the swap space is the amount of virtual memory available.

Support for swap is provided by the Linux kernel and user-space utilities from the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.

## Contents

*   [1 Swap space](#Swap_space)
*   [2 Swap partition](#Swap_partition)
    *   [2.1 Activation by systemd](#Activation_by_systemd)
    *   [2.2 Disabling swap](#Disabling_swap)
*   [3 Swap file](#Swap_file)
    *   [3.1 Swap file creation](#Swap_file_creation)
    *   [3.2 Remove swap file](#Remove_swap_file)
*   [4 Swap with USB device](#Swap_with_USB_device)
*   [5 Swap encryption](#Swap_encryption)
*   [6 Performance Tuning](#Performance_Tuning)
    *   [6.1 Swappiness](#Swappiness)
    *   [6.2 Priority](#Priority)
*   [7 Striping](#Striping)

## Swap space

Swap space will usually be a disk partition but can also be a file. Users may create a swap space during installation of Arch Linux or at any later time should it become necessary. Swap space is generally recommended for users with less than 1 GB of RAM, but becomes more a matter of personal preference on systems with gratuitous amounts of physical RAM (though it is required for suspend-to-disk support).

To check swap status, use:

```
$ swapon --show

```

Or:

```
$ free -h

```

**Note:** There is no performance advantage to either a contiguous swap file or a partition, both are treated the same way.

## Swap partition

A swap partition can be created with most GNU/Linux partitioning tools (e.g. `fdisk`, `cfdisk`). Swap partitions are typically designated as type **82**, however it is possible to use any partition type as swap.

To set up a Linux swap area, the `mkswap` command is used. For example:

```
# mkswap /dev/sda2

```

**Warning:** All data on the specified partition will be lost.

The *mkswap* utility generates a UUID for the partition by default, use the `-U` flag in case you want to specify custom UUID:

```
# mkswap -U *custom_UUID* /dev/sda2

```

To enable the device for paging:

```
# swapon /dev/sda2

```

To enable this swap partition on boot, add an entry to [fstab](/index.php/Fstab "Fstab"):

 `/etc/fstab`  `/dev/sda2 none swap defaults 0 0` 
**Note:**

*   Adding an entry to fstab is optional in most cases with systemd. See the next subsection.
*   If using an SSD with TRIM support, consider using `defaults,discard` in the swap line in [fstab](/index.php/Fstab "Fstab"). If activating swap manually with *swapon*, using the `-d` or `--discard` parameter achieves the same. See `man 8 swapon` for details.

**Warning:** Enabling discard on RAID setups using mdadm will cause system lockup on boot and during runtime, if using swapon.

### Activation by systemd

systemd activates swap partitions based on two different mechanisms, both are executables in `/usr/lib/systemd/system-generators`. The generators are run on start-up and create native systemd units for mounts. The first, `systemd-fstab-generator`, reads the fstab to generate units, including a unit for swap. The second, `systemd-gpt-auto-generator` inspects the root disk to generate units. It operates on GPT disks only, and can identify swap partitions by their type code **82**.

This can be solved by one of the following options:

*   removing the swap entry from `/etc/fstab`
*   changing the swap partition's type code from **82** to an arbitrary type code
*   setting the attribute of the swap partition to "**63**: do not automount"

### Disabling swap

To deactivate specific swap space:

```
# swapoff /dev/sda2

```

Alternatively use the `-a` switch to deactivate all swap space.

Since swap is managed by systemd, it will be activated again on the next system startup. To disable the automatic activation of detected swap space permanently, run `systemctl --type swap` to find the responsible *.swap* unit and [mask](/index.php/Mask "Mask") it.

## Swap file

As an alternative to creating an entire partition, a swap file offers the ability to vary its size on-the-fly, and is more easily removed altogether. This may be especially desirable if disk space is at a premium (e.g. a modestly-sized SSD).

**Warning:** [Btrfs](/index.php/Btrfs "Btrfs") does not support swap files. Failure to heed this warning may result in file system corruption. While a swap file may be used on Btrfs when mounted through a loop device, this will result in severely degraded swap performance.

### Swap file creation

As root use `fallocate` to create a swap file the size of your choosing (M = Megabytes, G = Gigabytes). For example, creating a 512 MB swap file:

```
# fallocate -l 512M /swapfile

```

**Note:** *fallocate* may cause problems with some file systems such as [F2FS](/index.php/F2FS "F2FS") or [XFS](/index.php/XFS "XFS").[[1]](https://bugzilla.redhat.com/show_bug.cgi?id=1129205#c3) As an alternative, using *dd* is more reliable, but slower: `# dd if=/dev/zero of=/swapfile bs=1M count=512` 

Set the right permissions (a world-readable swap file is a huge local vulnerability)

```
# chmod 600 /swapfile

```

After creating the correctly sized file, format it to swap:

```
# mkswap /swapfile

```

Activate the swap file:

```
# swapon /swapfile

```

Finally, edit [fstab](/index.php/Fstab#File_example "Fstab") to add an entry for the swap file:

 `/etc/fstab`  `/swapfile none swap defaults 0 0` 

### Remove swap file

To remove a swap file, the current swap file must be turned off.

As root:

```
# swapoff -a

```

Remove swap file:

```
# rm -f /swapfile

```

Finally remove the relevant entry from `/etc/fstab`.

## Swap with USB device

Thanks to the modularity offered by Linux, we can have multiple swap partitions spread over different devices. If you have a very full hard disk, a USB device can be used as a swap partition temporarily. However, this method has some severe disadvantages:

*   A USB device is slower than a hard disk
*   Flash memory has a limited number of write cycles. Using it as a swap partition can kill it quickly

To add a USB device to swap, first take a USB flash drive and partition it for swap as described in [#Swap partition](#Swap_partition).

Next open `/etc/fstab`.

Now add the following entry, just under the current swap entry, which take the current swap partition over the new USB one

```
UUID=... none swap defaults,pri=10 0 0

```

where the UUID is taken from the command:

```
ls -l /dev/disk/by-uuid/ | grep /dev/sdc1

```

Just replace sdc1 with your new USB swap partition. `sdb1`

**Tip:** The UUID is used because when other devices are attached to the computer, the device order could be changed

Last, add

```
pri=0

```

in the *original* swap entry so that the USB swap partition will take priority over the old swap partition.

This guide will work for other memory such as SD cards, etc.

## Swap encryption

See [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

## Performance Tuning

Swap values can be adjusted to help performance.

### Swappiness

The *swappiness* [sysctl](/index.php/Sysctl "Sysctl") parameter represents the kernel's preference (or avoidance) of swap space. Swappiness can have a value between 0 and 100, the default value is 60\. Setting this parameter to a low value will reduce swapping from RAM, and is known to improve responsiveness on many systems.

To check the current swappiness value:

```
$ cat /proc/sys/vm/swappiness

```

To temporarily set the swappiness value:

```
# sysctl vm.swappiness=10

```

To set the swappiness value permanently, edit a *sysctl* configuration file

 `/etc/sysctl.d/99-sysctl.conf`  `vm.swappiness=10` 

To test and more on why this may work, take a look at [this article](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that).

Another *sysctl* parameter that affects swap performance is `vm.vfs_cache_pressure`, which controls the tendency of the kernel to reclaim the memory which is used for caching of VFS caches, versus pagecache and swap. Increasing this value increases the rate at which VFS caches are reclaimed.[[2]](http://doc.opensuse.org/products/draft/SLES/SLES-tuning_sd_draft/cha.tuning.memory.html#cha.tuning.memory.vm.reclaim) For more information, see the [Linux kernel documentation](https://www.kernel.org/doc/Documentation/sysctl/vm.txt).

### Priority

If you have more than one swap file or swap partition you should consider assigning a priority value (0 to 32767) for each swap area. The system will use swap areas of higher priority before using swap areas of lower priority. For example, if you have a faster disk (`/dev/sda`) and a slower disk (`/dev/sdb`), assign a higher priority to the swap area located on the faster device. Priorities can be assigned in fstab via the `pri` parameter:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

Or via the `-p` (or `--priority`) parameter of swapon:

```
# swapon -p 100 /dev/sda1

```

If two or more areas have the same priority, and it is the highest priority available, pages are allocated on a round-robin basis between them.

## Striping

There is no necessity to use [RAID](/index.php/RAID "RAID") for swap performance reasons. The kernel itself can stripe swapping on several devices, if you just give them the same priority in the `/etc/fstab` file. Refer to [The Software-RAID HOWTO](http://unthought.net/Software-RAID.HOWTO/Software-RAID.HOWTO-2.html#ss2.3) for details.