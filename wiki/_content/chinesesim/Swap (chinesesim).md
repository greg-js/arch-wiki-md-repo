相关文章

*   [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram")
*   [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")

	*Linux 将物理内存分为内存段，叫做页面。交换是指内存页面被复制到预先设定好的硬盘空间(叫做交换空间)的过程，目的是释放对于页面的内存。物理内存和交换空间的总大小是可用的虚拟内存的总量。*

	- Linux.com, [关于 Linux Swap 空间](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space)。

## Contents

*   [1 交换空间](#.E4.BA.A4.E6.8D.A2.E7.A9.BA.E9.97.B4)
*   [2 交换分区](#.E4.BA.A4.E6.8D.A2.E5.88.86.E5.8C.BA)
*   [3 交换文件](#.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
    *   [3.1 手动方式](#.E6.89.8B.E5.8A.A8.E6.96.B9.E5.BC.8F)
        *   [3.1.1 建立交换文件](#.E5.BB.BA.E7.AB.8B.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
        *   [3.1.2 删除交换文件](#.E5.88.A0.E9.99.A4.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
        *   [3.1.3 恢复交换文件](#.E6.81.A2.E5.A4.8D.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
    *   [3.2 systemd-swap](#systemd-swap)
*   [4 使用 USB 设备交换](#.E4.BD.BF.E7.94.A8_USB_.E8.AE.BE.E5.A4.87.E4.BA.A4.E6.8D.A2)
*   [5 交换测试](#.E4.BA.A4.E6.8D.A2.E6.B5.8B.E8.AF.95)
*   [6 性能优化](#.E6.80.A7.E8.83.BD.E4.BC.98.E5.8C.96)
    *   [6.1 Swappiness](#Swappiness)
    *   [6.2 优先级](#.E4.BC.98.E5.85.88.E7.BA.A7)

## 交换空间

交换空间通常是一个磁盘分区，但是也可以是一个文件。必要的话，用户可以在安装 Arch Linux 或之后的任何时间建立交换空间。对于 RAM 小于 1GB 的用户，交换空间通常是推荐的，但是对于拥有大量的物理内存的用户来说是否使用主要看个人口味了(尽管它对于休眠到硬盘支持是必须的)。

要检查交换空间的状态，使用

```
$ swapon -s

```

或者：

```
$ free -m

```

## 交换分区

交换分区可以用大多数 GNU/Linux 分区工具(例如 `fdisk`, `cfdisk`)创建。交换分区被分配为类型 **82**.

想安装一个 Linux 交换区域，使用 `mkswap` 命令。例如：

```
# mkswap /dev/sda2

```

**警告:** 指定分区上的所有数据会丢失。

想要启用一个设备作为交换分区：

```
# swapon /dev/sda2

```

想要启动时自动启用交换分区，添加一个条目到 [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)"):

```
/dev/sda2 none swap defaults 0 0

```

## 交换文件

相比于使用一个磁盘分区作为交换空间，使用交换文件可以更方便地随时调整大小或者移除。当磁盘空间有限（例如常规大小的SSD）时，使用交换文件更加理想。

**注意:** BTRFS 文件系统暂时不支持交换文件。

### 手动方式

#### 建立交换文件

作为root，利用`fallocate`来创建一个所需大小的交换文件（也可以使用`dd`来创建，但这会花费更多时间）。例如，创建一个512 MB的交换文件：

```
# fallocate -l 512M /swapfile
或
# dd if=/dev/zero of=/swapfile bs=1M count=512

```

为交换文件设置权限：（出于安全考虑，交换文件不应被用户可读）

```
# chmod 600 /swapfile

```

创建好交换文件后，将其格式化：

```
# mkswap /swapfile

```

启用交换文件：

```
# swapon /swapfile

```

为了开机自动挂载，还需要在`/etc/fstab`中添加如下的一行：

```
/swapfile none swap defaults 0 0

```

#### 删除交换文件

如果要删除一个交换文件，必须先停用它。

作为root运行：

```
# swapoff -a

```

然后即可删除它：

```
# rm -rf /swapfile

```

#### 恢复交换文件

Resuming the system from a swap file after hibernation requires an addition parameter to the kernel compared to resuming from a swap partition. The additional parameter is `resume_offset=<Swap File Offset>`.

The value of `<Swap File Offset>` can be obtained from the output of `filefrag -v`; The output is in a table format; the required value is located in the `physical` column from the first row. Eg:

```
# filefrag -v /swapfile
Filesystem type is: ef53
File size of /swapfile is 4290772992 (1047552 blocks, blocksize 4096)
ext logical  physical  expected  length flags
  0       0     7546880                6144 
  1    6144  7557120  7553023   2048 
  2    8192  7567360  7559167   2048 
...

```

From the example `<Swap FIle Offset>` is `7546880`.

**Note:** Please note that in kernel `resume` parameter you still have to type path to partition (e.g. `resume=/dev/sda1`) not to swapfile explicitly! Parameter `resume_offset` is for informing system where swapfile starts on hard disk.

### systemd-swap

[Install](/index.php/Install "Install") the [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap) package. Set `swapfu_enabled=1` in the *Swap File Universal* section of `/etc/systemd/swap.conf`. [Start/enable](/index.php/Start/enable "Start/enable") the `systemd-swap` service. Visit the [authors GitHub](https://github.com/Nefelim4ag/systemd-swap) page for more information and setting up the [recommend configuration](https://github.com/Nefelim4ag/systemd-swap/blob/master/README.md#about-configuration).

## 使用 USB 设备交换

Thanks to modularity offered by Linux, we can have multiple swap partitions spread over different devices. If you have a very full hard disk, USB device can be used as partition temporally. But this method has some severe disadvantage：

*   USB device is slower than hard disk.
*   flash memories have limited write cycles. Using it as swap partition will kill it quickly.
*   when another device is attached to the computer, no swap can be used.

To add a a USB device to SWAP, first take a USB flash and partition it with a swap partition.You can use graphical tools such as Gparted or console tools like fdisk. Make sure to label the partition as SWAP before writing the partition table.

**Warning:** Make sure you are writing the partition to the correct disk!

Next edit the `fstab`

```
# nano /etc/fstab

```

Now add a new entry, just under the current swap entry, which take the current swap partition over the new USB one

```
UUID=... none swap defaults,pri=10 0 0

```

where UUID is taken from the output of the command

```
ls -l /dev/disk/by-uuid/ | grep /dev/sdc1

```

Just replace sdc1 with your new USB swap partition. `sdb1`

**Tip:** We use UUID because when you attach other devices to the computer it could modify the device order

Last, add

```
pri=0

```

in the *original* swap entry for teaching fstab to use HD swap only when USB is full

This guide will work for other memory such as SD cards, etc.

## 交换测试

Ensure that swap is activated with `swapon` of `free`:

```
$ swapon -s
$ free -m

```

## 性能优化

Swap 参数之可以调整来优化性能。

### Swappiness

*swappiness* [sysctl](/index.php/Sysctl "Sysctl") 参数代表了内核对于交换空间的喜好(或厌恶)程度。Swappiness 可以有 0 到 100 的值。设置这个参数为较低的值会减少内存的交换，从而提升一些系统上的响应度。

```
/etc/sysctl.d/90-swappiness.conf

```

```
vm.swappiness=1
vm.vfs_cache_pressure=50

```

### 优先级

如果你有多于一个交换文件或交换分区，你可以给它们各自分配一个优先级值(0 到 32767)。系统会在使用较低优先级的交换区域前优先使用较高优先级的交换区域。例如，如果你有一个较快的磁盘 (`/dev/sda`) 和一个较慢的磁盘 (`/dev/sdb`)，给较快的设备分配一个更高的优先级。优先级可以在 fstab 中通过 `pri` 参数指定：

```
/dev/sda1 none swap defaults,pri=100 0 0
/dev/sdb2 none swap defaults,pri=10  0 0

```

或者通过 swapon 的 `−p` (或者 `−−priority`) 参数：

```
# swapon -p 100 /dev/sda1

```

如果两个或更多的区域有同样的优先级，并且它们都是可用的最高优先级，页面会按照循环的方式在它们之间分配。