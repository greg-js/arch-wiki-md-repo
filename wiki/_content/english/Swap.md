Related articles

*   [fstab](/index.php/Fstab "Fstab")
*   [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate")
*   [Zswap](/index.php/Zswap "Zswap")
*   [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram")
*   [ZFS#Swap_volume](/index.php/ZFS#Swap_volume "ZFS")
*   [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption")

This page provides an introduction to [swap space and paging](https://en.wikipedia.org/wiki/Paging "wikipedia:Paging") on GNU/Linux. It covers creation and activation of swap partitions and swap files.

From [All about Linux swap space](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space):

	Linux divides its physical RAM (random access memory) into chunks of memory called pages. Swapping is the process whereby a page of memory is copied to the preconfigured space on the hard disk, called swap space, to free up that page of memory. The combined sizes of the physical memory and the swap space is the amount of virtual memory available.

Support for swap is provided by the Linux kernel and user-space utilities from the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Swap space](#Swap_space)
*   [2 Swap partition](#Swap_partition)
    *   [2.1 Activation by systemd](#Activation_by_systemd)
    *   [2.2 Disabling swap](#Disabling_swap)
*   [3 Swap file](#Swap_file)
    *   [3.1 Manually](#Manually)
        *   [3.1.1 Swap file creation](#Swap_file_creation)
        *   [3.1.2 Remove swap file](#Remove_swap_file)
    *   [3.2 Automated](#Automated)
        *   [3.2.1 systemd-swap](#systemd-swap)
*   [4 Swap encryption](#Swap_encryption)
*   [5 Performance](#Performance)
    *   [5.1 Swappiness](#Swappiness)
    *   [5.2 VFS cache pressure](#VFS_cache_pressure)
    *   [5.3 Priority](#Priority)
    *   [5.4 Using zswap or zram](#Using_zswap_or_zram)
    *   [5.5 Striping](#Striping)

## Swap space

Swap space can take the form of a disk partition or a file. Users may create a swap space during installation or at any later time as desired. Swap space can be used for two purposes, to extend the virtual memory beyond the installed physical memory (RAM), a.k.a "enable swap", and also for suspend-to-disk support.

If it is beneficial to enable swap depends on the amount of installed physical memory, and the amount of memory required to run all the desired programs. If the amount of physical memory is less than the required amount, then it is beneficial to enable swap. This avoids [out of memory conditions](https://en.wikipedia.org/wiki/Out_of_memory "wikipedia:Out of memory"), where the Linux kernel OOM killer mechanism will automatically attempt to free up memory by killing processes. To increase the amount of virtual memory to the required amount, add the necessary difference as swap space. For example, if your programs require 7.5 GB of memory to run, and there are 4 GB of physical memory installed, add the difference of 3.5 GB in swap space. Add more swap space to account for future requirements. It is a matter of personal preference if you prefer programs to be killed over enabling swap. The biggest drawback to enabling swap is its lower performance, see section [#Performance](#Performance).

To check swap status, use:

```
$ swapon --show

```

Or

```
$ free -h

```

*free* also indicates if memory is running short, which can be remedied by enabling swap or increasing swap.

**Note:** There is no performance advantage to either a contiguous swap file or a partition, both are treated the same way.

## Swap partition

A swap partition can be created with most GNU/Linux [partitioning tools](/index.php/Partitioning_tools "Partitioning tools"). Swap partitions are typically designated as type `82`. Even though it is possible to use any partition type as swap, it is recommended to use type `82` in most cases since [systemd](/index.php/Systemd "Systemd") will automatically detect it and mount it (see below).

To set up a partition as Linux swap area, the `mkswap` command is used. For example:

```
# mkswap /dev/sd*xy*

```

**Warning:** All data on the specified partition will be lost.

To enable the device for paging:

```
# swapon /dev/sd*xy*

```

To enable this swap partition on boot, add an entry to `/etc/fstab`:

```
UUID=*device_UUID* none swap defaults 0 0

```

where the `*device_UUID*` is the [UUID](/index.php/UUID "UUID") of the swap space.

See [fstab](/index.php/Fstab "Fstab") for the file syntax.

**Note:**

*   The fstab-entry is optional if the swap partition is located on a device using GPT. See the next subsection.
*   If using an SSD with [TRIM](/index.php/TRIM "TRIM") support, consider using `defaults,discard` in the swap line in [fstab](/index.php/Fstab "Fstab"). If activating swap manually with *swapon*, using the `-d`/`--discard` parameter achieves the same. See [swapon(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/swapon.8) for details.

**Warning:** Enabling discard on RAID setups using mdadm will cause system lockup on boot and during runtime, if using swapon.

### Activation by systemd

[systemd](/index.php/Systemd "Systemd") activates swap partitions based on two different mechanisms. Both are executables in `/usr/lib/systemd/system-generators`. The generators are run on start-up and create native systemd units for mounts. The first, `systemd-fstab-generator`, reads the fstab to generate units, including a unit for swap. The second, `systemd-gpt-auto-generator` inspects the root disk to generate units. It operates on GPT disks only, and can identify swap partitions by their type GUID, see [systemd#GPT partition automounting](/index.php/Systemd#GPT_partition_automounting "Systemd") for more information.

### Disabling swap

To deactivate specific swap space:

```
# swapoff /dev/sd*xy*

```

Alternatively use the `-a` switch to deactivate all swap space.

Since swap is managed by systemd, it will be activated again on the next system startup. To disable the automatic activation of detected swap space permanently, run `systemctl --type swap` to find the responsible *.swap* unit and [mask](/index.php/Mask "Mask") it.

## Swap file

As an alternative to creating an entire partition, a swap file offers the ability to vary its size on-the-fly, and is more easily removed altogether. This may be especially desirable if disk space is at a premium (e.g. a modestly-sized SSD).

**Warning:** [Btrfs](/index.php/Btrfs "Btrfs") supports swap file with limitations since Linux kernel version 5.0\. See [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs") for more information.

### Manually

#### Swap file creation

For copy-on-write file systems like [Btrfs](/index.php/Btrfs "Btrfs"), first create a zero length file, set the `No_COW` attribute on it with [chattr](/index.php/Chattr "Chattr"), and make sure compression is disabled:

```
# truncate -s 0 /swapfile
# chattr +C /swapfile
# btrfs property set /swapfile compression none

```

See [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs") for more information.

Use `fallocate` to create a swap file the size of your choosing (M = [Mebibytes](https://en.wikipedia.org/wiki/Mebibyte "wikipedia:Mebibyte"), G = [Gibibytes](https://en.wikipedia.org/wiki/Gibibyte "wikipedia:Gibibyte")). For example, creating a 512 MiB swap file:

```
# fallocate -l 512M /swapfile

```

**Note:** *fallocate* may cause problems with some file systems such as [F2FS](/index.php/F2FS "F2FS").[[1]](https://github.com/karelzak/util-linux/issues/633) As an alternative, using *dd* is more reliable, but slower: `# dd if=/dev/zero of=/swapfile bs=1M count=512 status=progress` 

Set the right permissions (a world-readable swap file is a huge local vulnerability):

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

Finally, edit the fstab configuration to add an entry for the swap file:

 `/etc/fstab` 
```
/swapfile none swap defaults 0 0

```

For additional information, see [fstab#Usage](/index.php/Fstab#Usage "Fstab").

**Note:** The swap file must be specified by its location on the file system not by its UUID or LABEL.

#### Remove swap file

To remove a swap file, it must be turned off first and then can be removed:

```
# swapoff /swapfile
# rm -f /swapfile

```

Finally remove the relevant entry from `/etc/fstab`.

### Automated

#### systemd-swap

[Install](/index.php/Install "Install") the [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) package. Set `swapfc_enabled=1` in the *Swap File Chunked* section of `/etc/systemd/swap.conf`. [Start/enable](/index.php/Start/enable "Start/enable") the `systemd-swap` service. Visit the [authors GitHub](https://github.com/Nefelim4ag/systemd-swap) page for more information and setting up the [recommended configuration](https://github.com/Nefelim4ag/systemd-swap/blob/master/README.md#about-configuration).

**Note:** If the journal keeps showing the following warning `systemd-swap[..]: WARN: swapFC: ENOSPC` and no swap file is being created, you need to set `swapfc_force_preallocated=1` in `/etc/systemd/swap.conf`.

## Swap encryption

See [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

## Performance

Swap operations are usually significantly slower than directly accessing data in RAM. Disabling swap entirely to improve performance can sometimes lead to a degradation, since it decreases the memory available for VFS caches, causing more frequent and costly disk I/O.

Swap values can be adjusted to help performance:

### Swappiness

The *swappiness* [sysctl](/index.php/Sysctl "Sysctl") parameter represents the kernel's preference (or avoidance) of swap space. Swappiness can have a value between 0 and 100, the default value is 60\. A low value causes the kernel to avoid swapping, a higher value causes the kernel to try to use swap space. Using a low value on sufficient memory is known to improve responsiveness on many systems.

To check the current swappiness value:

```
$ cat /sys/fs/cgroup/memory/memory.swappiness

```

or

```
$ cat /proc/sys/vm/swappiness

```

**Note:** As `/proc` is a lot less organized and is kept only for compatibility purposes, you are encouraged to use `/sys` instead.

To temporarily set the swappiness value:

```
# sysctl -w vm.swappiness=10

```

To set the swappiness value permanently, create a [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5) configuration file. For example:

 `/etc/sysctl.d/99-swappiness.conf`  `vm.swappiness=10` 

To test and more on why this may work, take a look at [this article](http://rudd-o.com/en/linux-and-free-software/tales-from-responsivenessland-why-linux-feels-slow-and-how-to-fix-that).

### VFS cache pressure

Another *sysctl* parameter that affects swap performance is `vm.vfs_cache_pressure`, which controls the tendency of the kernel to reclaim the memory which is used for caching of VFS caches, versus pagecache and swap. Increasing this value increases the rate at which VFS caches are reclaimed[[2]](http://doc.opensuse.org/documentation/leap/tuning/html/book.sle.tuning/cha.tuning.memory.html#cha.tuning.memory.vm.reclaim). For more information, see the [Linux kernel documentation](https://www.kernel.org/doc/Documentation/sysctl/vm.txt).

### Priority

If you have more than one swap file or swap partition you should consider assigning a priority value (0 to 32767) for each swap area. The system will use swap areas of higher priority before using swap areas of lower priority. For example, if you have a faster disk (`/dev/sda`) and a slower disk (`/dev/sdb`), assign a higher priority to the swap area located on the fastest device. Priorities can be assigned in [fstab](/index.php/Fstab "Fstab") via the `pri` parameter:

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

Or via the `--priority` parameter of *swapon*:

```
# swapon --priority 100 /dev/sda1

```

If two or more areas have the same priority, and it is the highest priority available, pages are allocated on a round-robin basis between them.

### Using zswap or zram

[Zswap](/index.php/Zswap "Zswap") is a Linux kernel feature providing a compressed write-back cache for swapped pages. This increases the performance and decreases the IO-Operations. [ZRAM](/index.php/ZRAM "ZRAM") creates a virtual compressed Swap-file in memory as alternative to a swapfile on disc.

### Striping

There is no necessity to use [RAID](/index.php/RAID "RAID") for swap performance reasons. The kernel itself can stripe swapping on several devices, if you just give them the same priority in the `/etc/fstab` file. Refer to [The Software-RAID HOWTO](http://unthought.net/Software-RAID.HOWTO/Software-RAID.HOWTO-2.html#ss2.3) for details.