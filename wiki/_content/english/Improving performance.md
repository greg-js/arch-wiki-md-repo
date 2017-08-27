This article provides information on basic system diagnostics relating to performance as well as steps that may be taken to reduce resource consumption or to otherwise optimize the system with the end-goal being either perceived or documented improvements to a system's performance.

## Contents

*   [1 The basics](#The_basics)
    *   [1.1 Know your system](#Know_your_system)
    *   [1.2 Benchmarking](#Benchmarking)
*   [2 Storage devices](#Storage_devices)
    *   [2.1 Multiple hardware paths](#Multiple_hardware_paths)
    *   [2.2 Partitioning](#Partitioning)
        *   [2.2.1 Multiple drives](#Multiple_drives)
        *   [2.2.2 Layout on HDDs](#Layout_on_HDDs)
    *   [2.3 Choosing and tuning your filesystem](#Choosing_and_tuning_your_filesystem)
        *   [2.3.1 Mount options](#Mount_options)
            *   [2.3.1.1 Reiserfs](#Reiserfs)
    *   [2.4 Tuning kernel parameters](#Tuning_kernel_parameters)
        *   [2.4.1 USB storage devices](#USB_storage_devices)
    *   [2.5 Tuning IO schedulers](#Tuning_IO_schedulers)
        *   [2.5.1 Background](#Background)
        *   [2.5.2 Change at runtime](#Change_at_runtime)
        *   [2.5.3 Persisting the change](#Persisting_the_change)
            *   [2.5.3.1 Kernel parameter (for a single device)](#Kernel_parameter_.28for_a_single_device.29)
            *   [2.5.3.2 systemd-tmpfiles](#systemd-tmpfiles)
            *   [2.5.3.3 Using udev for one device or HDD/SSD mixed environment](#Using_udev_for_one_device_or_HDD.2FSSD_mixed_environment)
    *   [2.6 Power management configuration](#Power_management_configuration)
    *   [2.7 Reduce disk reads/writes](#Reduce_disk_reads.2Fwrites)
        *   [2.7.1 Show disk writes](#Show_disk_writes)
        *   [2.7.2 Relocate files to tmpfs](#Relocate_files_to_tmpfs)
        *   [2.7.3 Compiling in tmpfs](#Compiling_in_tmpfs)
        *   [2.7.4 Disabling journaling on the filesystem](#Disabling_journaling_on_the_filesystem)
        *   [2.7.5 Swap space](#Swap_space)
    *   [2.8 Storage I/O scheduling with ionice](#Storage_I.2FO_scheduling_with_ionice)
*   [3 CPU](#CPU)
    *   [3.1 Overclocking](#Overclocking)
    *   [3.2 Frequency scaling](#Frequency_scaling)
    *   [3.3 Alternative CPU scheduler](#Alternative_CPU_scheduler)
    *   [3.4 Adjusting priorities of processes](#Adjusting_priorities_of_processes)
        *   [3.4.1 Ananicy](#Ananicy)
        *   [3.4.2 cgroups](#cgroups)
    *   [3.5 irqbalance](#irqbalance)
*   [4 Graphics](#Graphics)
    *   [4.1 Xorg.conf configuration](#Xorg.conf_configuration)
    *   [4.2 Driconf](#Driconf)
*   [5 RAM and swap](#RAM_and_swap)
    *   [5.1 Clock frequency and timings](#Clock_frequency_and_timings)
    *   [5.2 Root on RAM overlay](#Root_on_RAM_overlay)
    *   [5.3 Zram or zswap](#Zram_or_zswap)
        *   [5.3.1 Swap on zRAM using a udev rule](#Swap_on_zRAM_using_a_udev_rule)
    *   [5.4 Using the graphic card's RAM](#Using_the_graphic_card.27s_RAM)
*   [6 Network](#Network)
*   [7 Watchdogs](#Watchdogs)

## The basics

### Know your system

The best way to tune a system is to target bottlenecks, or subsystems which limit overall speed. The system specifications can help identify them.

*   If the computer becomes slow when large applications (such as OpenOffice.org and Firefox) run at the same time, check if the amount of RAM is sufficient. Use the following command, and check the "available" column:

```
$ free -h

```

*   If boot time is slow, and applications take a long time to load at first launch (only), then the hard drive is likely to blame. The speed of a hard drive can be measured with the `hdparm` command:

**Note:** [hdparm](https://www.archlinux.org/packages/?name=hdparm) indicates only the pure read speed of a hard drive, and is not a valid benchmark. A value higher than 40MB/s (while idle) is however acceptable on an average system.

```
# hdparm -t /dev/sdx

```

*   If CPU load is consistently high even with enough RAM available, then try to lower CPU usage by disabling running [daemons](/index.php/Daemons "Daemons") and/or processes. This can be monitored in several ways, for example with [htop](https://www.archlinux.org/packages/?name=htop), `pstree` or any other [system monitoring](/index.php/List_of_applications#System_monitoring "List of applications") tool:

```
$ htop

```

*   If applications using direct rendering are slow (i.e those which use the GPU, such as video players, games, or even a [window manager](/index.php/Window_manager "Window manager")), then improving GPU performance should help. The first step is to verify if direct rendering is actually enabled. This is indicated by the `glxinfo` command, part of the [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) package:

 `$ glxinfo | grep direct` 
```
direct rendering: Yes

```

*   When running a [desktop environment](/index.php/Desktop_environment "Desktop environment"), disabling (unused) visual desktop effects may reduce GPU usage. Use a more lightweight environment or create a [custom environment](/index.php/Desktop_environment#Custom_environments "Desktop environment") if the current does not meet the hardware and/or personal requirements.

### Benchmarking

The effects of optimization are often difficult to judge. They can however be measured by [benchmarking](/index.php/Benchmarking "Benchmarking") tools.

## Storage devices

### Multiple hardware paths

An internal hardware path is how the storage device is connected to your motherboard. There are different ways to connect to the motherboard such as TCP/IP through a NIC, plugged in directly using PCIe/PCI, Firewire, Raid Card, USB, etc. By spreading your storage devices across these multiple connection points you maximize the capabilities of your motherboard, for example 6 hard-drives connected via USB would be much much slower than 3 over USB and 3 over Firewire. The reason is that each entry path into the motherboard is like a pipe, and there is a set limit to how much can go through that pipe at any one time. The good news is that the motherboard usually has several pipes.

More Examples

1.  Directly to the motherboard using pci/PCIe/ata
2.  Using an external enclosure to house the disk over USB/Firewire
3.  Turn the device into a network storage device by connecting over tcp/ip

Note also that if you have a 2 USB ports on the front of your machine, and 4 USB ports on the back, and you have 4 disks, it would probably be fastest to put 2 on front/2 on back or 3 on back/1 on front. This is because internally the front ports are likely a separate Root Hub than the back, meaning you can send twice as much data by using both than just 1\. Use the following commands to determine the various paths on your machine.

 `USB Device Tree`  `$ lsusb -tv`  `PCI Device Tree`  `$ lspci -tv` 

### Partitioning

Make sure that your partitions are [properly aligned](/index.php/Partitioning#Partition_alignment "Partitioning").

#### Multiple drives

If you have multiple disks available, you can set them up as a software [RAID](/index.php/RAID "RAID") for serious speed improvements.

Creating [swap](/index.php/Swap "Swap") on a separate disk can also help quite a bit, especially if your machine swaps frequently.

#### Layout on HDDs

If using a traditional spinning HDD, your partition layout can influence the system's performance. Sectors at the beginning of the drive (closer to the outside of the disk) are faster than those at the end. Also, a smaller partition requires less movements from the drive's head, and so speed up disk operations. Therefore, it is advised to create a small partition (10GB, more or less depending on your needs) only for your system, as near to the beginning of the drive as possible. Other data (pictures, videos) should be kept on a separate partition, and this is usually achieved by separating the home directory (`/home/*user*`) from the system (`/`).

### Choosing and tuning your filesystem

Choosing the best filesystem for a specific system is very important because each has its own strengths. The [File systems](/index.php/File_systems "File systems") article provides a short summary of the most popular ones. You can also find relevant articles [here](/index.php/Category:File_systems "Category:File systems").

#### Mount options

The [noatime](/index.php/Fstab#atime_options "Fstab") option is known to improve performance of the filesystem.

Other mount options are filesystem specific, therefore see the relevant articles for the filesystems:

*   [Ext3](/index.php/Ext3 "Ext3")
*   [Ext4#Tips and tricks](/index.php/Ext4#Tips_and_tricks "Ext4")
*   [JFS Filesystem#Optimizations](/index.php/JFS_Filesystem#Optimizations "JFS Filesystem")
*   [XFS](/index.php/XFS "XFS")
*   [Btrfs#Defragmentation](/index.php/Btrfs#Defragmentation "Btrfs") and [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs")
*   [ZFS#Tuning](/index.php/ZFS#Tuning "ZFS")

##### Reiserfs

The `data=writeback` mount option improves speed, but may corrupt data during power loss. The `notail` mount option increases the space used by the filesystem by about 5%, but also improves overall speed. You can also reduce disk load by putting the journal and data on separate drives. This is done when creating the filesystem:

```
# mkreiserfs –j /dev/sd**a1** /dev/sd**b1**

```

Replace `/dev/sd**a1**` with the partition reserved for the journal, and `/dev/sd**b1**` with the partition for data. You can learn more about reiserfs with this [article](http://www.funtoo.org/Funtoo_Filesystem_Guide,_Part_2).

### Tuning kernel parameters

There are several key tunables affecting the performance of block devices, see [sysctl#Virtual memory](/index.php/Sysctl#Virtual_memory "Sysctl") for more information.

#### USB storage devices

If USB drives like pendrives are slow to copy files, append these three lines in a [systemd](/index.php/Systemd "Systemd") tmpfile:

(this should not be needed anymore: [[1]](https://lwn.net/Articles/475405/))

 `/etc/tmpfiles.d/local.conf` 
```
w /sys/kernel/mm/transparent_hugepage/enabled - - - - madvise
w /sys/kernel/mm/transparent_hugepage/defrag - - - - madvise
w /sys/kernel/mm/transparent_hugepage/khugepaged/defrag - - - - 0

```

See also [[2]](http://unix.stackexchange.com/questions/107703/why-is-my-pc-freezing-while-im-copying-a-file-to-a-pendrive), [[3]](http://lwn.net/Articles/572911/) and [[4]](http://lwn.net/Articles/467328/).

### Tuning IO schedulers

**Warning:** Only the CFQ scheduler supports setting IO priorities with ionice. Some background processes rely on this capability to perform background IO unobtrusively by reducing their IO priority, for example KDE's file indexer baloo. Using a different scheduler than the default CFQ scheduler can worsen the user experience on desktops. [[5]](https://blogs.kde.org/2014/10/15/ubuntus-linux-scheduler-or-why-baloo-might-be-slowing-your-system-1404)

The kernel officially supports the following schedulers for storage disk in-/output (IO):

*   [CFQ](https://en.wikipedia.org/wiki/CFQ "wikipedia:CFQ") scheduler (Completely Fair Queuing)
*   [NOOP](https://en.wikipedia.org/wiki/NOOP_scheduler "wikipedia:NOOP scheduler")
*   [Deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "wikipedia:Deadline scheduler").

Unofficial support is available through the [BFQ](/index.php/Linux-ck#How_to_enable_the_BFQ_I.2FO_Scheduler "Linux-ck") (Budget Fair Queueing) which is compiled into the [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) kernel as well as many kernels in the [AUR](/index.php/AUR "AUR").

A more contemporary option (since kernel version 3.16) is the [Multi-Queue Block IO Queuing Mechanism](https://www.thomas-krenn.com/en/wiki/Linux_Multi-Queue_Block_IO_Queueing_Mechanism_(blk-mq)) or blk-mq for short. Blk-mq leverages a CPU with multiple cores to map I/O queries to multiple queues. The tasks are distributed across multiple threads and therefore to multiple CPU cores (per-core software queues) and can speed up read/write operations vs. traditional I/O schedulers.

One can enable blk-mq by adding the following to the kernel's boot line:

```
scsi_mod.use_blk_mq=y dm_mod.use_blk_mq=y

```

**Note:** Using blk_mq is an all-or-nothing proposition. When enabled all IO schedulers are disabled which is fine for SSDs but doing this may [negatively impact performance of rotational discs](https://mahmoudhatem.wordpress.com/2016/02/08/oracle-uek-4-where-is-my-io-scheduler-none-multi-queue-model-blk-mq/).

#### Background

A HDD has spinning disks and head that move physically to the required location. Such structure leads to following characteristics:

*   random latency is quite high, for modern HDDs it is ~10ms (ignoring a disk controller write buffer).
*   sequential access provides much higher throughput. In this case the head needs to move less distance.

If we have a lot of running processes that make IO requests to different parts of storage (i.e. random access) then we can expect that a disk handles ~100 IO requests per second. Because modern systems can easily generate load much higher than 100 requests per second we have a queue of requests that have to wait for access to the storage. One way to improve throughput is to linearize access, i.e. order waiting requests by its logical address and always choose the closest request. Historically this was the first Linux IO scheduler called **elevator** scheduler.

One of the problems with the elevator algorithm is that it makes suffer processes with sequential access. Such processes read a block of data then process it for several microseconds then read next block and so on. The elevator scheduler does not know that the process is going to read another block nearby and, thus, moves to another request at some other location. To overcome the problem **anticipatory IO** scheduler was added. For synchronous requests this algorithm waits for a short amount of time before moving to another request.

While these schedulers try to improve total throughput they also might leave some unlucky requests waiting for a very long time. As an example, imagine the majority of processes make requests at the beginning of storage space while an unlucky process makes a request at the other end of storage. So developers tried to make the algorithm more fair and the **deadline** scheduler was added. It has a queue ordered by address (the same as elevator). If some request sits in this queue for a long time then it moves to an "expired" queue ordered by expire time. The scheduler checks the expire queue first and processes requests from there and only then moves to elevator queue. It is important to understand that this algorithm sacrifices total throughput for fairness.

CFQ (the default scheduler nowadays) aggregates all ideas from above and adds `cgroup` support that allows to reserve some amount of IO to a specific `cgroup`. It is useful on shared (and cloud) hosting - users who paid for 20 IO/s want to get their share if needed.

The characteristics of a SSD are different. It does not have moving parts. Random access is as fast as sequential one. An SSD can handle multiple requests at the same time. Modern devices' throughput ~10K IO/s, which is higher than workload on most systems. Essentially a user cannot generate enough requests to saturate a SDD, the requests queue is effectively always empty. In this case IO scheduler does not provide any improvements. Thus, it is recommended to use the **noop** scheduler for an SSD.

#### Change at runtime

It is possible to change the scheduler at runtime and even to use different schedulers for separate storage devices at the same time. Available schedulers can be queried by viewing the contents of `/sys/block/sd**X**/queue/scheduler` (the active scheduler is denoted by brackets):

 `$ cat /sys/block/sd**X**/queue/scheduler` 
```
noop deadline [cfq]

```

Users can change the active scheduler at runtime without the need to reboot, for example:

```
# echo noop > /sys/block/sd**X**/queue/scheduler

```

This method is non-persistent and will be lost upon rebooting.

#### Persisting the change

##### Kernel parameter (for a single device)

If the sole storage device in the system is an SSD, consider setting the I/O scheduler for the entire system via the `elevator=noop` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

##### systemd-tmpfiles

If you have more than one storage device, or wish to avoid clutter on the kernel cmdline, you can set the I/O scheduler via `systemd-tmpfiles`:

 `/etc/tmpfiles.d/10_ioscheduler.conf`  `w /sys/block/sdX/queue/scheduler - - - - noop` 

For more detail on `systemd-tmpfiles` see [Systemd#Temporary files](/index.php/Systemd#Temporary_files "Systemd").

##### Using udev for one device or HDD/SSD mixed environment

Though the above will undoubtedly work, it is probably considered a reliable workaround. Ergo, it would be preferred to use the system that is responsible for the devices in the first place to implement the scheduler. In this case it is udev, and to do this, all one needs is a simple [udev](/index.php/Udev "Udev") rule.

To do this, create the following:

 `/etc/udev/rules.d/60-schedulers.rules` 
```
# set deadline scheduler for non-rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="deadline"

```

Of course, set Deadline/CFQ to the desired schedulers. Changes should occur upon next boot. To check success of the new rule:

```
$ cat /sys/block/sd**X**/queue/scheduler  # where **X** is the device in question

```

**Note:** In the example sixty is chosen because that is the number udev uses for its own persistent naming rules. Thus, it would seem that block devices are at this point able to be modified and this is a safe position for this particular rule. But the rule can be named anything so long as it ends in `.rules`.)

### Power management configuration

When dealing with traditional rotational disks (HDD's) you may want to [lower or disable power saving features](/index.php/Hdparm#Power_management_configuration "Hdparm") completely.

### Reduce disk reads/writes

Avoiding unnecessary access to slow storage drives is good for performance and also increasing lifetime of the devices, although on modern hardware the difference in life expectancy is usually negligible.

**Note:** A 32GB SSD with a mediocre 10x write amplification factor, a standard 10000 write/erase cycle, and **10GB of data written per day**, would get an **8 years life expectancy**. It gets better with bigger SSDs and modern controllers with less write amplification. Also compare [[7]](http://techreport.com/review/25889/the-ssd-endurance-experiment-500tb-update) when considering whether any particular strategy to limit disk writes is actually needed.

#### Show disk writes

The [iotop](https://www.archlinux.org/packages/?name=iotop) package can sort by disk writes, and show how much and how frequently programs are writing to the disk. See [iotop(8)](http://man7.org/linux/man-pages/man8/iotop.8.html) for details.

#### Relocate files to tmpfs

Relocate files, such as your browser profile, to a [tmpfs](/index.php/Tmpfs "Tmpfs") file system, for improvements in application response as all the files are now stored in RAM:

*   Refer to [Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon") for syncing browser profiles. Certain browsers might need special attention, see e.g. [Firefox on RAM](/index.php/Firefox_on_RAM "Firefox on RAM").
*   Refer to [Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon") for syncing any specified folder.
*   Refer to [Makepkg#tmpfs](/index.php/Makepkg#tmpfs "Makepkg") for improving compile times when building packages.

#### Compiling in tmpfs

See [Makepkg#Improving compile times](/index.php/Makepkg#Improving_compile_times "Makepkg").

#### Disabling journaling on the filesystem

**Warning:** Using a filesystem with journaling disabled is data loss as a result of an ungraceful dismount (i.e. post power failure, kernel lockup, etc.). With modern SSDs, [Ted Tso](http://tytso.livejournal.com/61830.html) advocates that journaling can be enabled with minimal added read/write cycles under most circumstances.

Using a journaling filesystem such as ext4 on an SSD **without** a journal is an option to decrease read/writes. With *ext4*, this is done by enabling the `nointegrity` option. See [Fstab](/index.php/Fstab "Fstab").

#### Swap space

See [Swap#Swappiness](/index.php/Swap#Swappiness "Swap").

### Storage I/O scheduling with ionice

Many tasks such as backups do not rely on a short storage I/O delay or high storage I/O bandwidth to fulfil their task, they can be classified as background tasks. On the other hand quick I/O is necessary for good UI responsiveness on the desktop. Therefore it is beneficial to reduce the amount of storage bandwidth available to background tasks, whilst other tasks are in need of storage I/O. This can be achieved by making use of the linux I/O scheduler CFQ, which allows setting different priorities for processes.

The I/O priority of a background process can be reduced to the "Idle" level by starting it with

```
# ionice -c 3 command

```

See man ionice(1) and [[8]](https://www.cyberciti.biz/tips/linux-set-io-scheduling-class-priority.html) for more information.

## CPU

### Overclocking

[Overclocking](https://en.wikipedia.org/wiki/Overclocking "w:Overclocking") improves the computational performance of the CPU by increasing its peak clock frequency. The ability to overclock depends on the combination of CPU model and motherboard model. It is most frequently done through the BIOS. Overclocking also has disadvantages and risks. It is neither recommended nor discouraged here.

Many Intel chips will not correctly report their clock frequency to acpi_cpufreq and most other utilities. This will result in excessive messages in dmesg, which can be avoided by unloading and blacklisting the kernel module `acpi_cpufreq`. To read their clock speed use `i7z`, available through the `i7z` and [i7z-git](https://aur.archlinux.org/packages/i7z-git/) packages.

### Frequency scaling

See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### Alternative CPU scheduler

The default CPU scheduler in the mainline Linux kernel is [CFS](https://en.wikipedia.org/wiki/Completely_Fair_Scheduler "w:Completely Fair Scheduler").

An alternative scheduler designed to be used on desktop computers is MuQSS, developed by [Con Kolivas](http://users.tpg.com.au/ckolivas/kernel/), which is focused on desktop interactivity and responsiveness. MuQSS is available either as a stand-alone patch or as part of a wider patchset, the **-ck** patchset. See [Linux-ck](/index.php/Linux-ck "Linux-ck") and [Linux-pf](/index.php/Linux-pf "Linux-pf") for more information on the patchset.

### Adjusting priorities of processes

#### Ananicy

[Ananicy](https://github.com/Nefelim4ag/Ananicy) is a daemon, available in the [ananicy-git](https://aur.archlinux.org/packages/ananicy-git/) package, for auto adjusting the nice levels of executables. The nice level represents the priority of the executable when allocating CPU resources.

#### cgroups

See [cgroups](/index.php/Cgroups "Cgroups").

### irqbalance

The purpose of [irqbalance](https://www.archlinux.org/packages/?name=irqbalance) is distribute hardware interrupts across processors on a multiprocessor system in order to increase performance. It can be [controlled](/index.php/Systemd#Using_units "Systemd") by the provided `irqbalance.service`.

## Graphics

As with CPUs, overclocking can directly improve performance, but is generally recommended against. There are several packages in the [AUR](/index.php/AUR "AUR"), such as [amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/) (ATI) and [nvclock](https://aur.archlinux.org/packages/nvclock/) (NVIDIA).

### Xorg.conf configuration

Graphics performance may depend on the settings in `/etc/X11/xorg.conf`; see the [NVIDIA](/index.php/NVIDIA "NVIDIA"), [ATI](/index.php/ATI "ATI") and [Intel](/index.php/Intel "Intel") articles. Improper settings may stop Xorg from working, so caution is advised.

### Driconf

[driconf](https://www.archlinux.org/packages/?name=driconf) is a small utility which allows to change direct rendering settings for open source drivers. Enabling *HyperZ* may improve performance.

## RAM and swap

### Clock frequency and timings

RAM can run at different clock frequencies and timings, which can be configured in the BIOS. Memory performance depends on both values. Selecting the highest preset presented by the BIOS usually improves the performance over the default setting. Note that increasing the frequency to values not supported by both motherboard and RAM vendor is overclocking, and similar risks and disdvantages apply, see [#Overclocking](#Overclocking).

### Root on RAM overlay

If running off a slow writing medium (USB, spinning HDDs) and storage requirements are low, the root may be run on a RAM overlay ontop of read only root (on disk). This can vastly improve performance at the cost of a limited writable space to root. See [liveroot](https://aur.archlinux.org/packages/liveroot/).

### Zram or zswap

The [zram](https://www.kernel.org/doc/Documentation/blockdev/zram.txt) kernel module (previously called **compcache**) provides a compressed block device in RAM. If you use it as swap device, the RAM can hold much more information but uses more CPU. Still, it is much quicker than swapping to a hard drive. If a system often falls back to swap, this could improve responsiveness. Using zram is also a good way to reduce disk read/write cycles due to swap on SSDs.

Similar benefits (at similar costs) can be achieved using [zswap](/index.php/Zswap "Zswap") rather than zram. The two are generally similar in intent although not operation: zswap operates as a compressed RAM cache and neither requires (nor permits) extensive userspace configuration.

Example: To set up one lz4 compressed zram device with 32GiB capacity and a higher-than-normal priority (only for the current session):

```
# modprobe zram
# echo lz4 > /sys/block/zram0/comp_algorithm
# echo 32G > /sys/block/zram0/disksize
# mkswap --label zram0 /dev/zram0
# swapon --priority 100 /dev/zram0

```

To disable it again, either reboot or run

```
# swapoff /dev/zram0
# rmmod zram

```

A detailed explanation of all steps, options and potential problems is provided in the official documentation of the module [here](https://www.kernel.org/doc/Documentation/blockdev/zram.txt).

The [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) package provides a `systemd-swap.service` unit to automatically initialize zram devices. Configuration is possible in `/etc/systemd/swap.conf`.

The package [zramswap](https://aur.archlinux.org/packages/zramswap/) provides an automated script for setting up such swap devices with optimal settings for your system (such as RAM size and CPU core number). The script creates one zram device per CPU core with a total space equivalent to the RAM available, so you will have a compressed swap with higher priority than regular swap, which will utilize multiple CPU cores for compessing data. To do this automatically on every boot, [enable](/index.php/Enable "Enable") `zramswap.service`.

#### Swap on zRAM using a udev rule

The example below describes how to set up swap on zRAM automatically at boot with a single udev rule. No extra package should be needed to make this work.

First, enable the module:

 `/etc/modules-load.d/zram.conf` 
```
zram

```

Configure the number of /dev/zram nodes you need.

 `/etc/modprobe.d/zram.conf` 
```
options zram num_devices=2

```

Create the udev rule as shown in the example.

 `/etc/udev/rules.d/99-zram.rules` 
```
KERNEL=="zram0", ATTR{disksize}="512M" RUN="/usr/bin/mkswap /dev/zram0", TAG+="systemd"
KERNEL=="zram1", ATTR{disksize}="512M" RUN="/usr/bin/mkswap /dev/zram1", TAG+="systemd"

```

Add /dev/zram to your fstab.

 `/etc/fstab` 
```
/dev/zram0 none swap defaults 0 0
/dev/zram1 none swap defaults 0 0

```

### Using the graphic card's RAM

In the unlikely case that you have very little RAM and a surplus of video RAM, you can use the latter as swap. See [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram").

## Network

Every time a connection is made, the system must first resolve a fully qualified domain name to an IP address before the actual connection can be established. Response times of network requests can be improved by caching DNS queries locally. Common tools for this purpose include [pdnsd](/index.php/Pdnsd "Pdnsd"), [dnsmasq](/index.php/Dnsmasq "Dnsmasq"), [unbound](/index.php/Unbound "Unbound") and [rescached](/index.php/Rescached "Rescached").

## Watchdogs

According to [wikipedia:Watchdog_timer](https://en.wikipedia.org/wiki/Watchdog_timer "wikipedia:Watchdog timer"):

	A watchdog timer [...] is an electronic timer that is used to detect and recover from computer malfunctions. During normal operation, the computer regularly resets the watchdog timer [...]. If, [...], the computer fails to reset the watchdog, the timer will elapse and generate a timeout signal [...] used to initiate corrective [...] actions [...] typically include placing the computer system in a safe state and restoring normal system operation.

Many users need this feature due to their system's mission-critical role (i.e. servers), or because of the lack of power reset (i.e. embedded devices). Thus, this feature is required for a good operation in some situations. On the other hand, normal users (i.e. desktop and laptop) do not need this feature and can disable it.

To disable watchdog timers (both software and hardware), append `nowatchdog` to your boot parameters.

To check the new configuration do:

```
# cat /proc/sys/kernel/watchdog

```

or use:

```
# wdctl

```

After you disabled watchdogs, you can *optionally* avoid the loading of the module responsible of the hardware watchdog, too. Do it by [blacklisting](/index.php/Blacklisting "Blacklisting") the related module, e.g. `iTCO_wdt`.

**Note:** Some users [reported](https://bbs.archlinux.org/viewtopic.php?id=221239) the `nowatchdog` parameter doesn't work as expected but they have successfully disabled the watchdog (at least the hardware one) by blacklisting the above-mentioned module.

Either action will speed up your boot and shutdown, because one less module is loaded. Additionally disabling watchdog timers increases performance and [lowers power consumption](/index.php/Power_management#Disabling_NMI_watchdog "Power management").

See [[9]](https://bbs.archlinux.org/viewtopic.php?id=163768), [[10]](https://bbs.archlinux.org/viewtopic.php?id=165834), [[11]](http://0pointer.de/blog/projects/watchdog.html), and [[12]](https://www.kernel.org/doc/Documentation/watchdog/watchdog-parameters.txt) for more information.