[Bcache](https://bcache.evilpiepirate.org/) (block cache) allows one to use an SSD as a read/write cache (in writeback mode) or read cache (writethrough or writearound) for another blockdevice (generally a rotating HDD or array). This article will show how to install arch using Bcache as the root partition. For an intro to bcache itself, see [the bcache homepage](http://bcache.evilpiepirate.org/). Be sure to read and reference [the bcache manual](https://evilpiepirate.org/git/linux-bcache.git/tree/Documentation/bcache.txt). Bcache is in the mainline kernel since 3.10\. The kernel on the arch install disk includes the bcache module since 2013.08.01.

An alternative to Bcache is Facebook's [Flashcache](/index.php/Flashcache "Flashcache") and its offspring [EnhanceIO](/index.php/EnhanceIO "EnhanceIO").

Bcache needs the backing device to be formatted as a bcache block device. In most cases, [blocks to-bcache](https://github.com/g2p/blocks) can do an in-place conversion.

**Warning:**

*   Be sure you back up any important data first.
*   The bcache-dev branch is under heavy development. The on-disk format has undergone changes in 3.18 which are not backwards compatible with previous formats[[1]](http://www.spinics.net/lists/linux-bcache/msg02721.html). Note: This only applies to users who compile-in bcache-dev. The version built-in to the upstream Linux kernel is unaffected[[2]](http://www.spinics.net/lists/linux-bcache/msg02724.html).
*   Bcache and [btrfs](/index.php/Btrfs "Btrfs") could leave you with a corrupted filesystem. Please visit [this post](https://www.hdevalence.ca/blog/2013-09-21-notes-on-my-archlinux-install) for more information. Btrfs wiki reports that it was fixed in kernels 3.19+ [[3]](https://btrfs.wiki.kernel.org/index.php/Gotchas#Historical_references).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 在现存的系统上配置bcache设备](#在现存的系统上配置bcache设备)
    *   [1.1 管理 Bcache](#管理_Bcache)
*   [2 将系统安装到一个 bcache 设备](#将系统安装到一个_bcache_设备)
*   [3 从安装盘访问bcache分区](#从安装盘访问bcache分区)
*   [4 配置](#配置)
*   [5 高级操作](#高级操作)
    *   [5.1 调整后端设备的容量](#调整后端设备的容量)
        *   [5.1.1 扩容举例](#扩容举例)
        *   [5.1.2 缩容举例](#缩容举例)
            *   [5.1.2.1 强制把缓存写入后端设备](#强制把缓存写入后端设备)
*   [6 疑难解答](#疑难解答)
    *   [6.1 启动时 /dev/bcache 不存在](#启动时_/dev/bcache_不存在)
    *   [6.2 /sys/fs/bcache/ 不存在](#/sys/fs/bcache/_不存在)
*   [7 参考资料](#参考资料)

## 在现存的系统上配置bcache设备

**警告:** make-bcache **不会** 导入(import)一个现存的设备或分区——它会格式化它。请务必做好数据备份。

1\. 从 [AUR](/index.php/AUR "AUR") [安装](/index.php/%E5%AE%89%E8%A3%85 "安装") [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/)。

2\. 创建一个后端设备（通常来说这是你的机械硬盘）。后端设备可以是整个设备、一个分区或者其他任何的block设备。这将会创建/dev/bcache0：

```
# make-bcache -B /dev/sdx1

```

3\. 创建一个缓存设备（这通常是你的固态硬盘）。缓存设备可以是整个设备、一个分区或者其他任何的block设备：

```
# make-bcache -C /dev/sdy2

```

在这个例子里，默认的block大小是512B、bucket大小是128kB。block的大小应该与后端设备的sector大小匹配（通常是512或者4k）。bucket的大小应该与缓存设备的擦除block大小匹配（以减少写入放大）。例如，如果是一个4k sector的HDD和一个擦除block大小是2MB的SSD搭配，命令就应该是这样的：

```
# make-bcache --block 4k --bucket 2M -C /dev/sdy2

```

4\. 把缓存设备注册到后端设备。为了找到它的*cache set UUID*，运行`# bcache-super-show /dev/sdy2 | grep cset.uuid`然后把它添加到bcache设备。Udev规则会在以后的重启阶段自动搞定这个，因此你只需要执行一次这个命令：

```
# echo **cset.uuid** > /sys/block/bcache0/bcache/attach

```

5\. 更改你的缓存模式（如果你想要同时缓存读和写）：

```
# echo writeback > /sys/block/bcache0/bcache/cache_mode

```

6\. 如果你需要让这个分区在initcpio的时候就已经可以使用（即，在系统启动过程中需要用到它），你需要把'bcache'添加到`/etc/mkinitcpio.conf`文件里：

 `/etc/mkinitcpio.conf` 
```
...
MODULES=(... **bcache**)
...
HOOKS=(... block ... **bcache** ... filesystems ...)
...
```

然后请重新生成initramfs镜像：

```
# mkinitcpio -p linux

```

### 管理 Bcache

1\. 确认所有的东西都已经正确地配置了：

```
# cat /sys/block/bcache0/bcache/state

```

输出的内容有以下可能：

*   **no cache**: 这代表你还没有绑定缓存设备到你的后端设备上
*   **clean**: 这代表一切正常，缓存是clean的
*   **dirty**: 这代表一切正常，缓存模式被设置成了*writeback*，缓存是dirty的
*   **inconsistent**: 这代表问题很大，后端设备与缓存设备没有同步

使用一个没有缓存设备的 `/dev/bcache0` 的话所有的IO都会直接在后端设备上执行，等于pass-through模式。

2\. 查看正在使用的缓存模式：

```
# cat /sys/block/bcache0/bcache/cache_mode
[writethrough] writeback writearound none

```

在这个示例中，输出显示当前使用的是*writethrough*模式。

3\. 显示bcached设备的信息：

```
# bcache-super-show /dev/sdXY

```

4\. 停止后端设备：

```
# echo 1 > /sys/block/sdX/sdX[Y]/bcache/stop

```

5\. 让缓存设备脱机：

```
# echo 1 > /sys/block/sdX/sdX[Y]/bcache/detach

```

6\. 安全移除缓存设备：

```
# echo <cache-set-uuid> > /sys/block/bcache0/bcache/detach

```

7\. 释放已连接的设备：

```
# echo 1 > /sys/fs/bcache/<cache-set-uuid>/stop

```

## 将系统安装到一个 bcache 设备

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

8\. Install the system as per the [Installation Guide](/index.php/Installation_guide#Connect_to_the_internet "Installation guide") as normal except this:

Before you edit `/etc/mkinitcpio.conf` and run `mkinitcpio -p linux`:

*   install [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/) package from the [AUR](/index.php/AUR "AUR") on the new system.
*   Edit `/etc/mkinitcpio.conf`:
    *   add the "bcache" module
    *   add the "bcache" hook between block and filesystem hooks

**Note:** Should you want to open the backing device from the installation media for any reason after a reboot you must register it manually. Make sure the bcache module is loaded and then echo the relevant devices to /sys/bcache/register. You should see whether this worked or not by using dmesg.

## 从安装盘访问bcache分区

This is how to access a bcache partition from the install disk that was present before the install disk was booted. Boot the install disk and install [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/) from the AUR, just as in the previous section. Then, add the module to the kernel:

```
# modprobe bcache

```

Your device will not appear immediately at `/dev/bcache*`. To force the kernel to find it, tell it to reread the partition table:

```
# partprobe

```

Now, `/dev/bcache*` should be present, and you can carry on mounting, reformatting, etc. from here.

## 配置

可以配置的选项有很多，比如缓存模式、缓存写入时间间隔、启发式顺序写入等。通过写入 `/sys/block/bcache[0-9]/bcache` 目录中的对应文件可以进行相应的配置，详情查看 [bcache user documentation](https://evilpiepirate.org/git/linux-bcache.git/tree/Documentation/bcache.txt)。

例如，改变缓存模式通过以下命令实现：

```
echo 'writethrough' > /sys/block/bcache[0-9]/bcache/cache

```

可以把 'writethrough' 换成 'writeback', 'writearound' 或者 'none' 中的任意一个。

**Note:** 写入 /sys 的设置有些是临时的，重启之后就会失效（缓存模式的更改不会失效）。如果要“模拟”永久更改，在 `/etc/tmpfile.d` 目录中创建包含类似下面的内容的 *.conf* 文件： `/etc/tmpfile.d/my-bcache.conf` 
```
w /sys/block/bcache0/bcache/sequential_cutoff - - - - 1M
w /sys/block/bcache0/bcache/cache_mode        - - - - writeback
```

在这个例子中该文件会在系统启动时把 sequential cutoff 设置为1M、cache mode 设置为 writeback。

## 高级操作

### 调整后端设备的容量

It is possible to resize the backing device so long as you do not move the partition start. This process is described on [the mailing list](http://comments.gmane.org/gmane.linux.kernel.bcache.devel/249). Here is an example using btrfs volume directly on bcache0\. For LVM containers or for other filesystems, procedure will differ.

#### 扩容举例

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

#### 缩容举例

In this example, I shrink the filesystem by 4GB.

1\. Disable writeback cache (switch to writethrough cache) and wait for the disk to flush.

```
# echo writethrough > /sys/block/bcache0/bcache/cache_mode
$ watch cat /sys/block/bcache0/bcache/state

```

wait until state reports "clean". This might take a while.

###### 强制把缓存写入后端设备

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

## 疑难解答

### 启动时 /dev/bcache 不存在

如果你在启动时见到下面的提示信息并进入了busybox shell:

```
ERROR: Unable to find root device 'UUID=b6b2d82b-f87e-44d5-bbc5-c51dd7aace15'.
You are being dropped to a recovery shell
    Type 'exit' to try and continue booting
```

可能是因为后端设备设置成了"writeback"模式 (默认是 writearound)。在"writeback"模式下 /dev/bcache0 在缓存设备注册并连接之前是不存在的。注册(register)是每次启动时需要进行的操作，但是连接(attach)只需要进行一次。

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

### /sys/fs/bcache/ 不存在

当前尝试启动的内核不支持bcache或者bcache[内核模块未加载](/index.php/Kernel_module#Manual_module_handling "Kernel module")。

## 参考资料

*   [Bcache Homepage](http://bcache.evilpiepirate.org)
*   [Bcache Manual](https://www.kernel.org/doc/Documentation/bcache.txt)