相关文章

*   [Improving performance/Boot process](/index.php/Improving_performance/Boot_process "Improving performance/Boot process")
*   [Pacman/Tips and tricks#Performance](/index.php/Pacman/Tips_and_tricks#Performance "Pacman/Tips and tricks")
*   [OpenSSH#Speeding up SSH](/index.php/OpenSSH#Speeding_up_SSH "OpenSSH")
*   [Openoffice#Speed up OpenOffice](/index.php/Openoffice#Speed_up_OpenOffice "Openoffice")
*   [Laptop](/index.php/Laptop "Laptop")
*   [Preload](/index.php/Preload "Preload")
*   [Cpulimit](/index.php/Cpulimit "Cpulimit")

**翻译状态：** 本文是英文页面 [Improving performance](/index.php/Improving_performance "Improving performance") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-12-25，点击[这里](https://wiki.archlinux.org/index.php?title=Improving+performance&diff=0&oldid=559927)可以查看翻译后英文页面的改动。

本文将介绍关于系统性能诊断的基本知识，以及优化系统性能的具体步骤。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 基础工作](#基础工作)
    *   [1.1 了解系统](#了解系统)
    *   [1.2 跑分](#跑分)
*   [2 存储设备](#存储设备)
    *   [2.1 分散存储](#分散存储)
    *   [2.2 交换分区/文件](#交换分区/文件)
    *   [2.3 组RAID (简体中文)](#组RAID_(简体中文))
    *   [2.4 硬盘的连接方式](#硬盘的连接方式)
    *   [2.5 分区方案](#分区方案)
    *   [2.6 文件系统](#文件系统)
        *   [2.6.1 挂载选项](#挂载选项)
        *   [2.6.2 Reiserfs](#Reiserfs)
    *   [2.7 调整内核参数](#调整内核参数)
    *   [2.8 Input/output schedulers](#Input/output_schedulers)
        *   [2.8.1 Background information](#Background_information)
        *   [2.8.2 The scheduling algorithms](#The_scheduling_algorithms)
        *   [2.8.3 Kernel's I/O schedulers](#Kernel's_I/O_schedulers)
        *   [2.8.4 Changing I/O scheduler](#Changing_I/O_scheduler)
        *   [2.8.5 Tuning I/O scheduler](#Tuning_I/O_scheduler)
    *   [2.9 优化SSD](#优化SSD)
    *   [2.10 使用RAM disks](#使用RAM_disks)
*   [3 CPU](#CPU)
    *   [3.1 超频](#超频)
    *   [3.2 频率自动调整](#频率自动调整)
    *   [3.3 Real-time kernel](#Real-time_kernel)
    *   [3.4 Adjusting priorities of processes](#Adjusting_priorities_of_processes)
        *   [3.4.1 Ananicy](#Ananicy)
        *   [3.4.2 cgroups](#cgroups)
        *   [3.4.3 Cpulimit](#Cpulimit)
    *   [3.5 irqbalance](#irqbalance)
*   [4 显卡](#显卡)
    *   [4.1 Xorg.conf配置](#Xorg.conf配置)
    *   [4.2 Driconf](#Driconf)
    *   [4.3 GPU超频](#GPU超频)
*   [5 内存及虚拟内存](#内存及虚拟内存)
    *   [5.1 将临时文件转移到tmpfs](#将临时文件转移到tmpfs)
    *   [5.2 Swappiness](#Swappiness)
    *   [5.3 Compcache/Zram](#Compcache/Zram)
    *   [5.4 使用显存](#使用显存)
    *   [5.5 预读](#预读)
        *   [5.5.1 Go-preload](#Go-preload)
        *   [5.5.2 Preload](#Preload)
*   [6 系统启动](#系统启动)
    *   [6.1 待机](#待机)
    *   [6.2 自己编译内核](#自己编译内核)
*   [7 Network](#Network)

## 基础工作

### 了解系统

性能优化的最佳方法是找到瓶颈，因为这个子系统是导致系统速度低下的主要原因。查看系统配置表可以发现瓶颈，也可以通过以下方式寻找线索：

*   运行多个大型程序（如 LibreOffice、Firefox等）时变卡，可能是内存问题。为进一步明确内存使用情况，可敲入以下命令，并检查“available” 列的数值：

```
$ free -m

```

*   如果开机时间非常长，并且第一次加载应用程序也很长（但是启动以后运行却很流畅），可能是硬盘问题。可以用 [hdparm](https://www.archlinux.org/packages/?name=hdparm) 命令测量硬盘速度，在硬盘空闲时执行：

```
$ hdparm -t /dev/sdx

```

虽然这个命令只测定读取速度，但只要这个速度超过40MB/s就足以应付一般的系统需要。

*   如果内存充裕，但是CPU使用率一直很高，那么系统的瓶颈可能是 CPU。有多种方法可以监测 CPU 负荷，比如`htop`命令：

```
$ htop

```

*   如果仅仅是游戏或视频播放时出现卡顿，那应该是显卡相关的问题。首先，请使用软件包 [mesa-demos](https://www.archlinux.org/packages/?name=mesa-demos) 中的 `glxinfo`检查显卡是否开启了直接渲染功能：

 `$ glxinfo | grep direct` 
```
direct rendering: Yes

```

*   使用 [桌面环境](/index.php/Desktop_environment "Desktop environment")时，禁用未使用的桌面效果可以减少 GPU 使用。如果硬件性能比较差，可以考虑使用 [自定义环境](/index.php/Desktop_environment#Custom_environments "Desktop environment")。

### 跑分

为定量评估优化成果，可使用[benchmarking (简体中文)](/index.php/Benchmarking_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Benchmarking (简体中文)")。

## 存储设备

### 分散存储

如果你有多个存储设备，那么把操作系统的工作负荷均匀分摊到这些设备上，将极大提升系统性能。

### 交换分区/文件

把交换分区/文件放在系统盘以外，对提升速度也有所帮助，尤其是系统频繁使用交换分区/文件时。

### 组[RAID (简体中文)](/index.php/RAID_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "RAID (简体中文)")

如果你有多个硬盘，组一个软RAID或许有不小惊喜。RAID 0可使存储系统的速度翻翻，而且加入的硬盘越多，速度越快，不过，RAID 0没有数据冗余，一旦某个硬盘故障，数据将有损失。RAID 5则是兼顾速度和数据安全的明智选择，但它至少需要3块硬盘。

### 硬盘的连接方式

由于接口速度有差异，所以硬盘连接到主板的方式也将影响系统性能。例如，将固态硬盘接到USB接口，远不如将其接到SATA接口。如果你有很多个硬盘，而主板上的接口有限，那你要充分利用可用的接口，并注意合理安排：

*   PCI/PCIe/SATA
*   将硬盘改装为网络存储设备，通过网卡连接
*   USB/Firewire

使用USB接口时还要注意USB接口是否为“衍生”。如果某两个USB接口正好出自同一个USB根Hub，那么它俩同时使用时将彼此竞争速度。以下命令将帮助你了解个接口的衍生情况：

 `USB设备树`  `$ lsusb -tv`  `PCI设备树`  `$ lspci -tv` 

### 分区方案

对于机械硬盘，分区有可能影响系统性能，因为开头的分区靠近硬盘中心，转速较快。类似的，小的分区可以减少磁盘头的移动，可以提升磁盘性能。因此，建议将系统分区放在开始的部分，并且容量不必太大（10GB左右，取决于具体的需要）。

### 文件系统

#### 挂载选项

[noatime](/index.php/Fstab#atime_options "Fstab") 选项可以提高文件系统的性能。其它选项和文件系统相关，请参考：

*   [Ext3](/index.php/Ext3 "Ext3")
*   [Ext4#Improving performance](/index.php/Ext4#Improving_performance "Ext4")
*   [JFS Filesystem#Optimizations](/index.php/JFS_Filesystem#Optimizations "JFS Filesystem")
*   [XFS](/index.php/XFS "XFS")
*   [Btrfs#Defragmentation](/index.php/Btrfs#Defragmentation "Btrfs"), [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs") 和 [btrfs(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/btrfs.5)
*   [ZFS#Tuning](/index.php/ZFS#Tuning "ZFS")

#### Reiserfs

挂载选项`data=writeback`可以提高速度，但是，死机或突然断电时将丢失数据。挂载选项`notail`可以增加大约5%的磁盘空间，并提升速度。你还可以将日志文件和数据文件分散在不同的磁盘，从而减少硬盘负荷。不过，要达到这个目的需要重新格式化：

```
# mkreiserfs –j /dev/sd**a1** /dev/sd**b1**

```

其中，`/dev/sd**a1**`将保存日志，而`/dev/sd**b1**`将保存数据文件。请参考 [Using ReiserFS and Linux](http://www.funtoo.org/Funtoo_Filesystem_Guide,_Part_2)。

### 调整内核参数

参见[Low write performance on SLES 11 servers with large RAM](http://www.novell.com/support/kb/doc.php?id=7010287)和[Better Linux Disk Caching & Performance with vm.dirty_ratio & vm.dirty_background_ratio](http://lonesysadmin.net/2013/12/22/better-linux-disk-caching-performance-vm-dirty_ratio/)。 对于大内存来说，需要考虑调整磁盘写缓存。在`[/etc/sysctl.conf](/index.php/Sysctl "Sysctl")`中加入

```
#磁盘写缓存上限（占总内存的百分比）
vm.dirty_ratio = 3
#内核flusher线程开始清理磁盘写缓存的上限
vm.dirty_background_ratio = 2

```

*   vm.dirty_ratio默认是10。按目前的标准配置，内存通常都有4GB，这就意味着磁盘的写缓存有400MB（4GB*10%）。对于磁盘的读取操作而言，大缓存并没有问题，但是对于写操作而言，过大的写缓存将造成两个重要风险，一是意外停机时丢失数据，二是累积太多的数据在内存，一旦开始集中写入操作很容易造成长时间卡机。所以，系统内存较大时，应该将这个参数降下来。
*   调整vm.dirty_background_ratio的原理同上。这个参数一般设置为vm.dirty_ratio的1/4～1/2。

### Input/output schedulers

#### Background information

The input/output *(I/O)* scheduler is the kernel component that decides in which order the block I/O operations are submitted to storage devices. It is useful to remind here some specifications of two main drive types because the goal of the I/O scheduler is to optimize the way these are able to deal with read requests:

*   An HDD has spinning disks and a head that moves physically to the required location. Therefore, random latency is quite high ranging between 3 and 12ms (whether it is a high end server drive or a laptop drive and bypassing the disk controller write buffer) while sequential access provides much higher throughput. The typical HDD throughput is about 200 I/O operations per second *(IOPS)*.

*   An SSD does not have moving parts, random access is as fast as sequential one, typically under 0.1ms, and it can handle multiple concurrent requests. The typical SSD throughput is greater than 10,000 IOPS, which is more than needed in common workload situations.

If there are many processes making I/O requests to different storage parts, thousands of IOPS can be generated while a typical HDD can handle only about 200 IOPS. There is a queue of requests that have to wait for access to the storage. This is where the I/O schedulers plays an optimization role.

#### The scheduling algorithms

One way to improve throughput is to linearize access: by ordering waiting requests by their logical address and grouping the closest ones. Historically this was the first Linux I/O scheduler called [elevator](https://en.wikipedia.org/wiki/Elevator_algorithm "w:Elevator algorithm").

One issue with the elevator algorithm is that it is not optimal for a process doing sequential access: reading a block of data, processing it for several microseconds then reading next block and so on. The elevator scheduler does not know that the process is about to read another block nearby and, thus, moves to another request at some other location. The [anticipatory](https://en.wikipedia.org/wiki/Anticipatory_scheduling "w:Anticipatory scheduling") I/O scheduler overcomes the problem: it pauses for a few milliseconds in anticipation of another close-by read operation before dealing with another request.

While these schedulers try to improve total throughput, they might leave some unlucky requests waiting for a very long time. As an example, imagine the majority of processes make requests at the beginning of the storage space while an unlucky process makes a request at the other end of storage. This potentially infinite postponement of the process is called starvation. To improve fairness, the [deadline](https://en.wikipedia.org/wiki/Deadline_scheduler "w:Deadline scheduler") algorithm was developed. It has a queue ordered by address, similar to the elevator, but if some request sits in this queue for too long then it moves to an "expired" queue ordered by expire time. The scheduler checks the expire queue first and processes requests from there and only then moves to the elevator queue. Note that this fairness has a negative impact on overall throughput.

The [Completely Fair Queuing *(CFQ)*](https://en.wikipedia.org/wiki/CFQ "w:CFQ") approaches the problem differently by allocating a timeslice and a number of allowed requests by queue depending on the priority of the process submitting them. It supports [cgroup](/index.php/Cgroup "Cgroup") that allows to reserve some amount of I/O to a specific collection of processes. It is in particular useful for shared and cloud hosting: users who paid for some IOPS want to get their share whenever needed. Also, it idles at the end of synchronous I/O waiting for other nearby operations, taking over this feature from the *anticipatory* scheduler and bringing some enhancements. Both the *anticipatory* and the *elevator* schedulers were decommissioned from the Linux kernel replaced by the more advanced alternatives presented above.

The [Budget Fair Queuing *(BFQ)*](https://algo.ing.unimo.it/people/paolo/disk_sched/) is based on CFQ code and brings some enhancements. It does not grant the disk to each process for a fixed time-slice but assigns a "budget" measured in number of sectors to the process and uses heuristics. It is a relatively complex scheduler, it may be more adapted to rotational drives and slow SSDs because its high per-operation overhead, especially if associated with a slow CPU, can slow down fast devices. The objective of BFQ on personal systems is that for interactive tasks, the storage device is virtually as responsive as if it was idle. In its default configuration it focuses on delivering the lowest latency rather than achieving the maximum throughput.

[Kyber](https://lwn.net/Articles/720675/) is a recent scheduler inspired by active queue management techniques used for network routing. The implementation is based on "tokens" that serve as a mechanism for limiting requests. A queuing token is required to allocate a request, this is used to prevent starvation of requests. A dispatch token is also needed and limits the operations of a certain priority on a given device. Finally, a target read latency is defined and the scheduler tunes itself to reach this latency goal. The implementation of the algorithm is relatively simple and it is deemed efficient for fast devices.

#### Kernel's I/O schedulers

While some of the early algorithms have now been decommissioned, the official Linux kernel supports a number of I/O schedulers which can be split into two categories:

*   The **multi-queue schedulers** are available by default with the kernel. The [Multi-Queue Block I/O Queuing Mechanism *(blk-mq)*](https://www.thomas-krenn.com/en/wiki/Linux_Multi-Queue_Block_IO_Queueing_Mechanism_(blk-mq)) maps I/O queries to multiple queues, the tasks are distributed across threads and therefore CPU cores. Within this framework the following schedulers are available:
    *   *None*, no queuing algorithm is applied.
    *   *mq-deadline* is the adaptation of the deadline scheduler to multi-threading.
    *   *Kyber*
    *   *BFQ*

**Note:** The multi-queue scheduler framework and its related algorithms are still under development, the state of some issues can be seen in the [bfq forum](https://groups.google.com/forum/#!forum/bfq-iosched) and [FS#57496](https://bugs.archlinux.org/task/57496). In particular, users reported USB drives to stop working - [[1]](https://bbs.archlinux.org/viewtopic.php?id=234070)[[2]](https://bbs.archlinux.org/viewtopic.php?id=234363) and [[3]](https://bbs.archlinux.org/viewtopic.php?id=236291).

*   The **single-queue schedulers** are legacy schedulers, they can be activated at boot time as described in [#Changing I/O scheduler](#Changing_I/O_scheduler):
    *   [NOOP](https://en.wikipedia.org/wiki/NOOP_scheduler "w:NOOP scheduler") is the simplest scheduler, it inserts all incoming I/O requests into a simple FIFO queue and implements request merging. In this algorithm, there is no re-ordering of the request based on the sector number. Therefore it can be used if the ordering is dealt with at another layer, at the device level for example, or if it does not matter, for SSDs for instance.
    *   *Deadline*
    *   *CFQ*

**Note:** The best choice of scheduler depends on both the device and the exact nature of the workload. Also, the throughput in MB/s is not the only measure of performance: deadline or fairness deteriorate the overall throughput but improve system responsiveness.

#### Changing I/O scheduler

**Note:** The block multi-queue *(blk-mq)* mode must be disabled at boot time to be able to access the legacy *CFQ* and *Deadline* schedulers. This is done by adding `scsi_mod.use_blk_mq=0` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). The multi-queue schedulers are no longer available once in this mode.

To see the available schedulers for a device and the active one, in brackets:

 `$ cat /sys/block/***sda***/queue/scheduler`  `mq-deadline kyber [bfq] none` 

or for all devices:

 `$ cat /sys/block/**sd***/queue/scheduler` 
```
mq-deadline kyber [bfq] none
[mq-deadline] kyber bfq none
mq-deadline kyber [bfq] none
```

To change the active I/O scheduler to *bfq* for device *sda*, use:

```
# echo ***bfq*** > /sys/block/***sda***/queue/scheduler

```

SSDs can handle many IOPS and tend to perform best with simple algorithm like *noop* or *mq-deadline* while *BFQ* is well adapted to HDDs. The process to change I/O scheduler, depending on whether the disk is rotating or not can be automated and persist across reboots. For example the [udev](/index.php/Udev "Udev") rule below sets the scheduler to *mq-deadline* for non-rotational drives, it covers the naming schemes for SATA SSD, eMMC and NVMe SSD and to *bfq* for SATA HDD.

 `/etc/udev/rules.d/60-ioschedulers.rules` 
```
# set scheduler for non-rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]|mmcblk[0-9]*|nvme[0-9]*", ATTR{queue/rotational}=="0", ATTR{queue/scheduler}="mq-deadline"
# set scheduler for rotating disks
ACTION=="add|change", KERNEL=="sd[a-z]", ATTR{queue/rotational}=="1", ATTR{queue/scheduler}="bfq"
```

Then reboot or force [udev#Loading new rules](/index.php/Udev#Loading_new_rules "Udev").

#### Tuning I/O scheduler

Each of the kernel's I/O scheduler has its own tunables, such as the latency time, the expiry time or the FIFO parameters. They are helpful in adjusting the algorithm to a particular combination of device and workload. This is typically to achieve a higher throughput or a lower latency for a given utilization. The tunables and their description can be found within the [kernel documentation files](https://www.kernel.org/doc/Documentation/block/).

To list the available tunables for a device, in the example below *sdb* which is using *deadline*, use:

 `$ ls /sys/block/***sdb***/queue/iosched`  `fifo_batch  front_merges  read_expire  write_expire  writes_starved` 

To improve *deadline'*s throughput at the cost of latency, one can increase `fifo_batch` with the command:

 `# echo *32* > /sys/block/***sdb***/queue/iosched/**fifo_batch**` 

### 优化SSD

参见[SSD#Tips for maximizing SSD performance](/index.php/SSD#Tips_for_maximizing_SSD_performance "SSD")。

### 使用RAM disks

参见[USB stick RAID](http://cs.joensuu.fi/~mmeri/usbraid/)和[Combine RAM disk with disk in RAID](https://bbs.archlinux.org/viewtopic.php?pid=493773#p493773)。

## CPU

### 超频

超频就是增加 CPU 的实际运行频率。可是一项复杂而又有风险的操作，不建议盲目使用。超频的最佳手段是通过BIOS。acpi_cpufreq等工具常用工具无法读取I5或I7处理器超频后的频率。用户需要改用[AUR](/index.php/AUR "AUR")中的[i7z](https://www.archlinux.org/packages/?name=i7z)工具。

### 频率自动调整

请参考 [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### Real-time kernel

Some applications such as running a TV tuner card at full HD resolution (1080p) may benefit from using a [realtime kernel](/index.php/Realtime_kernel "Realtime kernel").

### Adjusting priorities of processes

See also [nice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nice.1) and [renice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/renice.1).

#### Ananicy

[Ananicy](https://github.com/Nefelim4ag/Ananicy) is a daemon, available in the [ananicy-git](https://aur.archlinux.org/packages/ananicy-git/) package, for auto adjusting the nice levels of executables. The nice level represents the priority of the executable when allocating CPU resources.

#### cgroups

See [cgroups](/index.php/Cgroups "Cgroups").

#### Cpulimit

[Cpulimit](https://github.com/opsengine/cpulimit) is a program to limit the CPU usage percentage of a specific process. After installing [cpulimit](https://www.archlinux.org/packages/?name=cpulimit), you may limit the CPU usage of a processes' PID using a scale of 0 to 100 times the number of CPU cores that the computer has. For example, with eight CPU cores the precentage range will be 0 to 800\. Usage:

```
$ cpulimit -l 50 -p 5081

```

### irqbalance

The purpose of [irqbalance](https://www.archlinux.org/packages/?name=irqbalance) is distribute hardware interrupts across processors on a multiprocessor system in order to increase performance. It can be [controlled](/index.php/Systemd#Using_units "Systemd") by the provided `irqbalance.service`.

## 显卡

### Xorg.conf配置

显卡性能严重依赖于`/etc/X11/xorg.conf`，请参阅[NVIDIA](/index.php/NVIDIA "NVIDIA")、[ATI](/index.php/ATI "ATI")以及[Intel](/index.php/Intel "Intel")显卡的相关教程修改配置。注意，不当的配置可能导致Xorg停止工作，所以，请审慎操作。

### Driconf

[driconf](https://aur.archlinux.org/packages/driconf/)是[官方库](/index.php/Official_repositories "Official repositories")中收录的小工具，它可以修改开源驱动的直接渲染设置。启用HyperZ功能将显著改善性能。

### GPU超频

GPU超频要比CPU超频简单得多，通过软件可以实时调整GPU时钟频率。

*   ATI显卡可使用[rovclock](https://aur.archlinux.org/packages/rovclock/)或者[amdoverdrivectrl](https://aur.archlinux.org/packages/amdoverdrivectrl/)
*   NVIDIA显卡可使用[nvclock](https://aur.archlinux.org/packages/nvclock/)。
*   Intel显卡可使用[GMABooster.com](http://www.gmabooster.com/)出品的[gmabooster](https://aur.archlinux.org/packages/gmabooster/)。

超频设置可以保存到`~/.xinitrc`，每次X启动之后就能自动超频。当然，更安全的做法应该是按需设置。

## 内存及虚拟内存

### 将临时文件转移到tmpfs

如果内存充足，可将`/tmp`、`/dev/shm`或者浏览器缓存文件等转移至[tmpfs](https://en.wikipedia.org/wiki/tmpfs "wikipedia:tmpfs")，这些文件将保存在内存中，从而加快软件的响应速度。借助脚本的帮助，可以轻松实现：

*   同步浏览器缓存：[Profile-sync-daemon](/index.php/Profile-sync-daemon "Profile-sync-daemon")。
*   同步任意目录：[Anything-sync-daemon](/index.php/Anything-sync-daemon "Anything-sync-daemon")。

### Swappiness

参阅[Swap#Swappiness](/index.php/Swap#Swappiness "Swap")。

### Compcache/Zram

目前，[Compcache](https://code.google.com/p/compcache/)已被内核模块**zram**取代，它们在内存中开辟一个区域存储压缩过的交换文件。如果系统频繁陷入交换状态，此法可以改善系统响应。不过，Zram目前仍在开发状态，尚未完全稳定，使用需谨慎。 AUR中收录的[zramswap](https://aur.archlinux.org/packages/zramswap/)包含了一个脚本进行自动设置，每个CPU核心对应一个zram设备，总容量等于可用的内存。通过[systemctl](/index.php/Systemd#Basic_systemctl_usage "Systemd")启动`zramswap.service`，可使得每次开机时自动应用这些配置。

**Tip:** 该方法有利于减少由于交换空间造成的固态硬盘读写，延长固态硬盘寿命。

### 使用显存

如果你的系统内存很小，而显存又过剩（这种奇葩系统还真少见），请参阅[Swap on video RAM](/index.php/Swap_on_video_RAM "Swap on video RAM")的方法，将交换文件设置在显存上。

### 预读

通过预读程序、库到内存中，能有效加快程序加载速度。预读通常用于常用的程序，如浏览器。

#### Go-preload

[gopreload-git](https://aur.archlinux.org/packages/gopreload-git/)是来自gentoo的一个预读服务。安装后，通过下列命令采集预读信息：

```
# gopreload-prepare program

```

运行需要预读的程序，收集结束后按回车键。

然后会生成一个预读列表：`/usr/share/gopreload/enabled`。在`/etc/rc.conf`设置开机启动gopreload，Go-preload就会在每次开机时预读列表中的程序。要禁止预读某个程序，只需从`/usr/share/gopreload/enabled`删除项目，或者移入`/usr/share/gopreload/disabled`。

#### Preload

比起Go-preload，[Preload](/index.php/Preload "Preload")更自动化（尽管有违KISS）：只需要在`/etc/rc.conf`添加服务就完事了。

## 系统启动

参见：[加速系统启动](/index.php/Improve_boot_performance_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Improve boot performance (简体中文)")。

### 待机

想要加快系统启动，最好的方法就是不要关电脑，而选择[待机](/index.php/Suspend_to_RAM "Suspend to RAM")。当然，为了可持续发展（至少是电费），不用电脑时还是关了吧。

### 自己编译内核

自己编译内核，删除不需要的模块，可以减少引导时间和内存占用。但通常这是个耗时、枯燥甚至令人厌烦的事情，你可能面临各种错误——甚至最终节约的开机时间还不如你浪费的时间多。但通过自己编译内核，可以学习到不少知识。参见：[here](/index.php/Kernel_Compilation "Kernel Compilation")。

## Network

*   Kernel networking: see [Sysctl#Improving performance](/index.php/Sysctl#Improving_performance "Sysctl")
*   NIC: see [Network configuration#Set device MTU and queue length](/index.php/Network_configuration#Set_device_MTU_and_queue_length "Network configuration")
*   DNS: consider using a caching DNS resolver, see [Domain name resolution#Resolvers](/index.php/Domain_name_resolution#Resolvers "Domain name resolution")
*   Samba: see [Samba#Improve throughput](/index.php/Samba#Improve_throughput "Samba")