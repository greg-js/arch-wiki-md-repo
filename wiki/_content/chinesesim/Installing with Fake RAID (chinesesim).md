相关文章

*   [Installing with Software RAID or LVM](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM")
*   [Convert a single drive system to RAID](/index.php/Convert_a_single_drive_system_to_RAID "Convert a single drive system to RAID")

本指南的目的是使用由板上BIOS的RAID控制器所生成的RAID，从而使得GRUB可以从RAID**内**的Linux和Windows的分区启动。当使用所谓的"fake RAID"或"host RAID"时,硬盘是`/dev/mapper/chipsetName_randomName`而不是`/dev/sdX`.

## Contents

*   [1 什么是"fake RAID"](#.E4.BB.80.E4.B9.88.E6.98.AF.22fake_RAID.22)
*   [2 历史](#.E5.8E.86.E5.8F.B2)
*   [3 备份](#.E5.A4.87.E4.BB.BD)
*   [4 提纲](#.E6.8F.90.E7.BA.B2)
*   [5 准备](#.E5.87.86.E5.A4.87)
    *   [5.1 配置RAID](#.E9.85.8D.E7.BD.AERAID)
*   [6 从安装盘启动](#.E4.BB.8E.E5.AE.89.E8.A3.85.E7.9B.98.E5.90.AF.E5.8A.A8)
*   [7 加载dmraid](#.E5.8A.A0.E8.BD.BDdmraid)
*   [8 执行传统安装](#.E6.89.A7.E8.A1.8C.E4.BC.A0.E7.BB.9F.E5.AE.89.E8.A3.85)
    *   [8.1 RAID分区](#RAID.E5.88.86.E5.8C.BA)
    *   [8.2 加载文件系统](#.E5.8A.A0.E8.BD.BD.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F)
    *   [8.3 安装和配置Archlinux](#.E5.AE.89.E8.A3.85.E5.92.8C.E9.85.8D.E7.BD.AEArchlinux)
*   [9 安装 GRUB](#.E5.AE.89.E8.A3.85_GRUB)
*   [10 Troubleshooting](#Troubleshooting)
    *   [10.1 Booting with degraded array](#Booting_with_degraded_array)

## 什么是"fake RAID"

维基:

	*基于操作系统的RAID并不总是保护引导过程,对Windows桌面版本一般的不实用。硬件RAID昂贵且是专有的。为了填补这一缺口，引入了价格便宜的“RAID控制器“，它不包含RAID控制器芯片，但只是一个带特殊的固件和控制器芯片的标准磁盘驱动器。在启动初期，RAID通过固件实现。当加载了保护模式操作系统内核如Linux或现代微软Windows系统，驱动程序接管RAID。*

	*这些控制器被制造商描述为RAID控制器，但很少清楚地告诉购买者，RAID处理的开销是由主机的CPU承担,而不是RAID控制器本身,硬件RAID不存在这样的开销。固件控制器往往只能使用特定的几种硬盘（例如：Intel的Matrix RAID使用SATA硬盘，现代Intel ICH南桥不支持PATA和SCSI；但主板厂商在一些主板的南桥之外实现了RAID控制器）。因为在此之前，“RAID控制器“已经实现了--控制器做了处理，所以这种新技术被技术知识界称为“fake RAID“，即使RAID本身是正确实施。 Adaptec的称他们为“host RAID“。*[wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID")

参考 [Wikipedia:RAID](https://en.wikipedia.org/wiki/RAID "wikipedia:RAID") or [FakeRaidHowto @ Community Ubuntu Documentation](https://help.ubuntu.com/community/FakeRaidHowto)以获得更多的信息。

不考虑术语，通过[dmraid](https://www.archlinux.org/packages/?name=dmraid)建立的"fake RAID"软RAID是健壮的，提供了一个通过多个磁盘实现的坚实的镜像或条带的数据系统，并只有可以忽略不计开销。 dmraid的对比于mdraid（纯粹的Linux软RAID）提供了如下好处：当出错时，能够在重启之前完全重建一个硬盘。

## 历史

在Linux 2.4中,　ATARAID kernel framework提供了对fake RAID (由BIOS协助的软RAID)的支持. Linux 2.6中，device-mapper framework ，包括其它的如[LVM](/index.php/LVM "LVM")和EVMS, 可以做ATARAID在2.4中做的事.虽然新的代码中处理RAID的I/O仍然在内核中运行时，device-mapper通常是由一个用户空间应用程序配置。很明显，当使用RAID的device-mapper，检测会在用户空间。

Heinz Maulshagen开发了dmraid工具来检测RAID和创建它们的映射.支持的硬件是带BIOS功能的fake RAID IDE/SATA. 常见的如: Promise FastTrak controllers; HighPoint HPT37x; Intel Matrix RAID; Silicon Image Medley; 和 NVIDIA nForce.

## 备份

**警告:** 使用RAID前请备份您的数据。条带式RAID对硬盘错误是很第敏感的。可以考虑常规的备份或镜像式RAID。**警告!**

## 提纲

*   准备
*   从安装盘启动
*   加载dmraid
*   执行传统安装
*   安装GRUB

## 准备

*   在其它机器上打开需要的指南(如 [Installation guide](/index.php/Installation_guide "Installation guide"))。如果没有其它的机器，打印出来。
*   下载最新的Arch Linux安装镜像.
*   备份所有重要的文件，因为目标分区中的所有文件将被破坏。

### 配置RAID

**警告:** 如果您的硬盘没有配置RAID并安装了Windows, 切换到"RAID"可能造成Windows启动时的BSOD错误。[[1]](http://support.microsoft.com/kb/316401/)

*   进入BIOS设置，激活RAID控制器。
    *   BIOS可能包含配置SATA硬盘的选项如"IDE","AHCI"或者"RAID"; 确认选择了"RAID"。
*   保存并退出BIOS设置。启动时进入RAID设置工具。
    *   RAID设置工具通常可以通过启动菜单(通常是F8, F10或CTRL+I)或RAID控制器启动时进入。
*   使用RAID设置工具来建立所选的条带或镜像的集。

**提示：** 详情查看主板文档。具体型号可能不同。

## 从安装盘启动

详情参见[Installation guide#Pre-installation](/index.php/Installation_guide#Pre-installation "Installation guide")。

**提示：** 如果您的显示器支持，考虑在启动时加`vga=795`选项以获得更高的framebuffer分辨率。

## 加载dmraid

加载device-mapper并寻找RAID:

```
# modprobe dm_mod
# dmraid -ay
# ls -la /dev/mapper/

```

输出例子:

```
/dev/mapper/control            <- 由device-mapper生成;如果存在，device-mapper是工作的。
/dev/mapper/sil_aiageicechah   <- Silicon镜像SATA RAID控制器下的一个RAID集
/dev/mapper/sil_aiageicechah1  <- 该RAID的第一个分区

```

如果只有(`/dev/mapper/control`)，用`lsmod`检查您是否加载了控制芯片的模块。如果加载了,那么dmraid不支持该控制芯片或系统没有RAID集(再检查一下BIOS中的RAID设置)。如果还是正确的，那您只能用[software RAID](/index.php/Installing_with_Software_RAID_or_LVM "Installing with Software RAID or LVM") (也就是说您不能用双启动的RAID系统)。

如果你的芯片模块没有加载，加载它，如:

```
# modprobe sata_sil

```

可用的驱动参见`/lib/modules/`uname -r`/kernel/drivers/ata/`。

测试RAID:

```
# dmraid -tay

```

## 执行传统安装

切换到**tty2**开始安装:

```
# /arch/setup

```

### RAID分区

*   在**Prepare Hard Drive**选择**Manually partition hard drives**因为**Auto-prepare**选项找不到您的RAID。
*   选择OTHER，输入您的RAID路径(如`/dev/mapper/sil_aiageicechah`)。切换到**tty1**检查您的输入。
*   按常规方法分区。

**提示：** 如果计划双启动，这时可以安装其它系统。如安装Windows XP到"C:"，则所有Windows分区前的分区应该改为类型[1B](隐藏的FAT32)来在安装windows时隐藏分区.当安装完后再将它们改回为类型[83] (Linux)。当然上述过程需重启。

### 加载文件系统

如果在**Manually configure block devices, filesystems and mountpoints**没有找到新的分区--很可能是这种情况:

*   切换到**tty1**.

*   去除所有device-mapper节点:

```
# dmsetup remove_all

```

*   重新激活新建立的RAID节点:

```
# dmraid -ay
# ls -la /dev/mapper

```

*   切换到**tty2**,重新进入**Manually configure block devices, filesystems and mountpoints**菜单，分区应该就可用了。

### 安装和配置Archlinux

**提示：** 使用3个终端:一个使用GUI来配置系统,一个使用chroot来安装GRUB,一全使用cfdisk来参考因为RAID盘的名字很奇怪。

*   **tty1:** chroot和安装grub
*   **tty2:** /arch/setup
*   **tty3:** 用cfdisk做输入参考，分区

让程序一直运行，使用时切换。

切换到安装程序(**tty2**)继续:

*   选择包
    *   确认标记了安装**dmraid**

*   配置系统
    *   在`mkinitcpio.conf`中的MODULES行加入**dm_mod**。如果使用镜像阵列还要加入**dm_mirror**
    *   如果需要还要在MODULES行加入芯片驱动模块**chipset_module_driver**
    *   在`mkinitcpio.conf`中HOOKS行加入**dmraid**;可加在**sata** but before **filesystems**之后

## 安装 GRUB

**Warning:** You can normally specify **default saved** instead of a number in `menu.lst` so that the default entry is the entry saved with the command **savedefault**. If you are using dmraid do not use **savedefault** or your array will de-sync and will not let you boot your system.

Please read [GRUB](/index.php/GRUB "GRUB") for more information about configuring GRUB. Installation is begun by selecting **Install Bootloader** from the Arch installer.

**Note:** For an unknown reason, the default `menu.lst` will likely be incorrectly populated when installing via fake RAID. Double-check the **root** lines (e.g. `root (hd0,0)`). Additionally, if you did **not** create a separate `/boot` partition, ensure the kernel/initrd paths are correct (e.g. `/boot/vmlinuz-linux` and `/boot/initramfs-linux.img` instead of `/vmlinuz-linux` and `/initramfs-linux.img`.

For example, if you created logical partitions (creating the equivalent of sda5, sda6, sda7, etc.) that were mapped as:

```
  /dev/mapper     |    Linux    GRUB Partition
                  |  Partition      Number
nvidia_fffadgic   |
nvidia_fffadgic5  |    /              4
nvidia_fffadgic6  |    /boot          5
nvidia_fffadgic7  |    /home          6

```

The correct root designation would be **(hd0,5)** in this example.

**Note:** If you use more than one set of dmraid arrays or multiple Linux distributions installed on different dmraid arrays (for example 2 disks in nvidia_fdaacfde and 2 disks in nvidia_fffadgic and you are installing to the second dmraid array (nvidia_fffadgic)), you will need designate the second array's `/boot` partition as the GRUB root. In the example above, if nvidia_fffadgic was the second dmraid array you were installing to, your root designation would be root **(hd1,5)**.

After saving the configuration file, the GRUB installer will **FAIL**. However it will still copy files to `/boot`. **DO NOT GIVE UP AND REBOOT** -- just follow the directions below:

*   Switch to **tty1** and [chroot](/index.php/Chroot "Chroot") into our installed system:

```
# mount -o bind /dev /mnt/dev
# mount -t proc none /mnt/proc
# mount -t sysfs none /mnt/sys
# chroot /mnt /bin/bash

```

*   Switch to **tty3** and look up the geometry of the RAID set. In order for cfdisk to find the array and provide the proper C H S information, you may need to start cfdisk providing your raid set as the first argument. (i.e. cfdisk /dev/mapper/nvidia_fffadgic):
    *   The number of **C**ylinders, **H**eads and **S**ectors on the RAID set should be written at the top of the screen inside cfdisk. **Note:** cfdisk shows the information in **H S C** order, but grub requires you to enter the geometry information in **C H S** order.

	Example: `18079 255 63` for a RAID stripe of two 74GB Raptor discs.

	Example: `38914 255 63` for a RAID stripe of two 160GB laptop discs.

*   GRUB will fail to properly read the drives; the **geometry** command must be used to manually direct GRUB:
    *   Switch to **tty1**, the chrooted environment.
    *   Install GRUB on `/dev/mapper/raidSet`:

```
# dmsetup mknodes
# grub --device-map=/dev/null

grub> device (hd0) /dev/mapper/raidSet
grub> geometry (hd0) C H S

```

Exchange **C H S** above with the proper numbers (be aware: they are **not** entered in the same order as they are read from cfdisk).

If geometry is entered properly, GRUB will list partitions found on this RAID set. You can confirm that grub is using the correct geometry and verify the proper grub root device to boot from by using the grub find command. If you have created a separate boot partition, then search for /grub/stage1 with find. If you have no separate boot partition, then search /boot/grub/stage1 with find. Examples:

```
grub> find /grub/stage1       # use when you have a separate boot partition
grub> find /boot/grub/stage1  # use when you have no separate boot partition

```

Grub will report the proper device to designate as the grub root below (i.e. (hd0,0), (hd0,4), etc...) Then, continue to install the bootloader into the Master Boot Record, changing "hd0" to "hd1" if required.

```
grub> root (hd0,0)
grub> setup (hd0)
grub> quit

```

**Note:** With dmraid >= 1.0.0.rc15-8, partitions are labeled "raidSet**p1**, raidSet**p2**, etc. instead of raidSet**1**, raidSet**2**, etc. If the setup command fails with "error 22: No such partition", temporary symlinks must be created.[[2]](http://bugs.gentoo.org/275566)

The problem is that GRUB still uses an older detection algorithm, and is looking for `/dev/mapper/raidSet1` instead of `/dev/mapper/raidSetp1`.

The solution is to create a symlink from `/dev/mapper/raidSetp1` to `/dev/mapper/raidSet1` (changing the partition number as needed). The simplest way to accomplish this is to:

```
# cd /dev/mapper
# for i in raidSetp*; do ln -s $i ${i/p/}; done

```

Lastly, if you have multiple dmraid devices with multiple sets of arrays set up (say: nvidia_fdaacfde and nvidia_fffadgic), then create the `/boot/grub/device.map` file to help GRUB retain its sanity when working with the arrays. All the file does is map the dmraid device to a traditional hd#. Using these dmraid devices, your device.map file will look like this:

```
(hd0) /dev/mapper/nvidia_fdaacfde
(hd1) /dev/mapper/nvidia_fffadgic

```

And now you are finished with the installation!

```
# reboot

```

## Troubleshooting

### Booting with degraded array

One drawback of the fake RAID approach on GNU/Linux is that dmraid is currently unable to handle degraded arrays, and will refuse to activate. In this scenario, one must resolve the problem from within another OS (e.g. Windows) or via the BIOS/chipset RAID utility.

Alternatively, if using a mirrored (RAID 1) array, users may temporarily bypass dmraid during the boot process and boot from a single drive:

1.  Edit the **kernel** line from the [GRUB](/index.php/GRUB "GRUB") menu
    1.  Remove references to dmraid devices (e.g. change `/dev/mapper/raidSet1` to `/dev/sda1`)
    2.  Append `disablehooks=dmraid` to prevent a kernel panic when dmraid discovers the degraded array
2.  Boot the system