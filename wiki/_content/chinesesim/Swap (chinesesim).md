相关文章

*   [Swap on video ram](/index.php/Swap_on_video_ram "Swap on video ram")
*   [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)")

	*Linux 将物理内存分为内存段，叫做页面。交换是指内存页面被复制到预先设定好的硬盘空间(叫做交换空间)的过程，目的是释放对于页面的内存。物理内存和交换空间的总大小是可用的虚拟内存的总量。*

	- Linux.com, [关于 Linux Swap 空间](http://www.linux.com/news/software/applications/8208-all-about-linux-swap-space)。

## Contents

*   [1 交换空间](#.E4.BA.A4.E6.8D.A2.E7.A9.BA.E9.97.B4)
*   [2 交换分区](#.E4.BA.A4.E6.8D.A2.E5.88.86.E5.8C.BA)
    *   [2.1 通过 Systemd 激活](#.E9.80.9A.E8.BF.87_Systemd_.E6.BF.80.E6.B4.BB)
    *   [2.2 关闭交换分区](#.E5.85.B3.E9.97.AD.E4.BA.A4.E6.8D.A2.E5.88.86.E5.8C.BA)
*   [3 交换文件](#.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
    *   [3.1 手动方式](#.E6.89.8B.E5.8A.A8.E6.96.B9.E5.BC.8F)
        *   [3.1.1 建立交换文件](#.E5.BB.BA.E7.AB.8B.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
        *   [3.1.2 删除交换文件](#.E5.88.A0.E9.99.A4.E4.BA.A4.E6.8D.A2.E6.96.87.E4.BB.B6)
    *   [3.2 自动化](#.E8.87.AA.E5.8A.A8.E5.8C.96)
        *   [3.2.1 systemd-swap](#systemd-swap)
*   [4 使用 USB 设备交换](#.E4.BD.BF.E7.94.A8_USB_.E8.AE.BE.E5.A4.87.E4.BA.A4.E6.8D.A2)
*   [5 交换测试](#.E4.BA.A4.E6.8D.A2.E6.B5.8B.E8.AF.95)
*   [6 性能优化](#.E6.80.A7.E8.83.BD.E4.BC.98.E5.8C.96)
    *   [6.1 Swappiness](#Swappiness)
    *   [6.2 优先级](#.E4.BC.98.E5.85.88.E7.BA.A7)

## 交换空间

交换空间通常是一个磁盘分区，但是也可以是一个文件。用户可以在安装 Arch Linux 的时候创建交换空间，或者在安装后的任何时间建立交换空间。对于 RAM 小于 1GB 的用户，交换空间通常是推荐的，但是对于拥有大量的物理内存的用户来说是否使用主要看个人口味了(尽管它对于休眠到硬盘支持是必须的)。

要检查交换空间的状态，使用

```
$ swapon -s

```

或者：

```
$ free -m

```

**注意:** 连续交换文件和交换分区之间没有性能之别，两者的处理方式是一样的。

## 交换分区

交换分区可以用大多数 GNU/Linux [分区工具](/index.php/Partitioning_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Partitioning (简体中文)")(例如 `fdisk`, `cfdisk`)创建。交换分区被分配为类型 `82`。尽管可以使用任何分区类型作为交换分区，但是在大多数情况下，建议使用 `82`，因为 [systemd](/index.php/Systemd "Systemd") 会自动检测并挂载它（见下文）。

想安装一个 Linux 交换区域，使用 `mkswap` 命令。例如：

```
# mkswap /dev/sd*xy*

```

**警告:** 指定分区上的所有数据会丢失。

想要启用一个设备作为交换分区：

```
# swapon /dev/sd*xy*

```

想要启动时自动启用交换分区，添加一个条目到 [fstab](/index.php/Fstab_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Fstab (简体中文)"):

```
UUID=<UUID> none swap defaults 0 0

```

UUID可以通过以下命令获得：

```
lsblk -no UUID /dev/sd*xy*

```

**提示：** UUID 和 LABEL 应该比使用由内核给出的设备名称更受青睐，因为设备顺序可能在将来发生变化。 请参阅：[fstab](/index.php/Fstab "Fstab")。

**注意:**

*   如果交换分区位于使用 GPT 的设备上，那么 [fstab](/index.php/Fstab "Fstab") 中的 swap 条目是可选的，参阅下一小节。
*   如果使用支持 [TRIM](/index.php/TRIM "TRIM") 的 SSD，请考虑在 [fstab](/index.php/Fstab "Fstab") 的 swap 条目中使用 `defaults,discard`。 如果使用 *swapon* 命令手动激活交换分区，则使用 `-d`/`--discard` 参数实现相同功能。详细信息，请参阅 [swapon(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/swapon.8)。

**警告:** 在使用 madam 进行 RAID 设置时，如果开启 swapon 命令的 discard 参数，将导致系统在启动和运行时锁定。

### 通过 Systemd 激活

[systemd](/index.php/Systemd "Systemd") 通过两种机制来激活 swap 分区。两种都是 `/usr/lib/systemd/system-generators` 内的可执行文件。 generators 在启动时运行并为 mounts 创建本地 systemd 单元。第一种机制是通过 `systemd-fstab-generator` 读取 fstab 来生成单元，包括 swap 单元。 第二种机制是通过 `systemd-gpt-auto-generator` 检查根磁盘来生成单位。这个机制仅在 GPT 磁盘上运行，并可通过类型代码 `82` 识别交换分区。

### 关闭交换分区

使用下面的命令关闭交换分区：

```
# swapoff /dev/sd*xy*

```

也可以使用 `-a` 参数来关闭所有的交换分区。

因为 swap 通过 systemd 管理，因此会在下一次系统启动时再次激活。要永久禁用该特性，运行 `systemctl --type swap` 来查找 *.swap* 单元，然后 [mask](/index.php/Mask "Mask") 它。

## 交换文件

相比于使用一个磁盘分区作为交换空间，使用交换文件可以更方便地随时调整大小或者移除。当磁盘空间有限（例如常规大小的SSD）时，使用交换文件更加理想。

**注意:** BTRFS 文件系统暂时不支持交换文件。不注意此警告可能会导致文件系统损坏。 虽然在通过循环设备挂载时 Btrfs 上可能会使用交换文件，但这会导致交换性能严重下降。

### 手动方式

#### 建立交换文件

用root账号，使用 `fallocate` 命令来创建一个所需大小的交换文件（M = [Mebibytes](https://en.wikipedia.org/wiki/Mebibyte "wikipedia:Mebibyte"), G = [Gibibytes](https://en.wikipedia.org/wiki/Gibibyte "wikipedia:Gibibyte")）。例如，创建一个512 MB的交换文件：

```
# fallocate -l 512M /swapfile

```

**注意:** *fallocate* 命令用在 [F2FS](/index.php/F2FS "F2FS") 或 [XFS](/index.php/XFS "XFS") 文件系统时可能会引起问题。[[1]](https://bugzilla.redhat.com/show_bug.cgi?id=1129205#c3) 代替方式是使用 *dd* 命令，但是要慢一点: `# dd if=/dev/zero of=/swapfile bs=1M count=512` 

为交换文件设置权限：（交换文件全局可读是一个巨大的本地漏洞）

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

最后，编辑 `/etc/fstab`， 在其中添加如下的一行：

 `/etc/fstab`  `/swapfile none swap defaults 0 0` 

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

最后从 `/etc/fstab` 中删除相关条目

### 自动化

#### systemd-swap

[安装](/index.php/Install "Install") 软件包 [systemd-swap](https://www.archlinux.org/packages/?name=systemd-swap)。设置 `/etc/systemd/swap.conf` 文件的 *Swap File Universal* 一节下的 `swapfu_enabled=1`。 [启动/启用](/index.php/Start/enable "Start/enable") `systemd-swap` 服务。 访问 [作者的 GitHub](https://github.com/Nefelim4ag/systemd-swap) 页面来获取更多的信息，或者设置 [推荐的配置](https://github.com/Nefelim4ag/systemd-swap/blob/master/README.md#about-configuration)。

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

用`swapon` 或 `free`确定Swap已激活：

```
$ swapon -s
$ free -m

```

## 性能优化

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