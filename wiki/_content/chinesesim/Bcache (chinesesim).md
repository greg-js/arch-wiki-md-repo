**翻译状态：** 本文是英文页面 [Bcache](/index.php/Bcache "Bcache") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-05-05，点击[这里](https://wiki.archlinux.org/index.php?title=Bcache&diff=0&oldid=572594)可以查看翻译后英文页面的改动。

[Bcache](https://bcache.evilpiepirate.org/) (block 缓存) 允许使用固态硬盘作为读写缓存（writeback模式）或者读缓存（writethrough 或者 writearound模式）来为另一个 block 设备（通常是机械硬盘或硬盘阵列）加速。这篇文章会展示如何把 Bcache 作为根分区安装 Archlinux。如果要看对于 bcache 本身的介绍，请浏览 [the bcache homepage](http://bcache.evilpiepirate.org/)。请一定要阅读并参考 [the bcache manual](https://evilpiepirate.org/git/linux-bcache.git/tree/Documentation/bcache.txt)。Bcache 从 Linux 内核 3.10 版本开始就已经并入 mainline，而 Archlinux 的安装盘自从 2013.08.01 版本开始就支持 bcache。

类似 Bcache 的还有 Facebook 的 [Flashcache](/index.php/Flashcache "Flashcache") 和它衍生的 [EnhanceIO](/index.php/EnhanceIO "EnhanceIO")。

Bcache 需要把后端设备格式化成 bcache block 设备。多数情况下，[blocks to-bcache](https://github.com/g2p/blocks) 可以用来做转换。

**Warning:**

*   一定要先备份数据！
*   bcache-dev 分支正处于非常不成熟的开发阶段。The on-disk format has undergone changes in 3.18 which are not backwards compatible with previous formats[[1]](http://www.spinics.net/lists/linux-bcache/msg02721.html). Note: This only applies to users who compile-in bcache-dev. The version built-in to the upstream Linux kernel is unaffected[[2]](http://www.spinics.net/lists/linux-bcache/msg02724.html).
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

1\. 从 Archlinux 的USB安装盘启动 (至少是 2013.08.01 版本的)。

2\. 从 [AUR](/index.php/AUR "AUR") 安装 [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/)。

3\. 对硬盘进行分区

**Note:** 虽然 Grub2 理论上不提供对 bcache 的支持，但是因为它完整支持 UEFI ，所以是有办法启动系统的。只要用来处理 boot 设备的模块被正确编译进内核或者包含在 initramfs 里面，那么就没必要按照下面的例子单独分区一个 boot 分区（第二行，名字是 arch_boot 的）。详情参考 [GRUB](/index.php/GRUB "GRUB") 和 [UEFI](/index.php/UEFI "UEFI")。

grub 无法处理 bcache, 所以你需要至少两个分区 (一个 boot 和一个作为 bcache 后端设备的分区). 如果你用的是 UEFI, 则额外需要 [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP)。比如:

```
     1            2048           22527   10.0 MiB    EF00  EFI System
     2           22528          432127   200.0 MiB   8300  arch_boot
     3          432128       625142414   297.9 GiB   8300  bcache_backing

```

**Note:** 例子里是没有 swap 文件或分区的，如果要让 swap 也受到 cache 设备缓存，使用步骤7里面的 LVM 来实现。如果不需要 swap 被缓存，请在这一步就创建 swap 分区。

4\. 配置你的机械硬盘作为 bcache 后端设备。

```
# make-bcache -B /dev/sda3

```

**Note:**

*   在配置启动盘的时候，一定要明白自己在做什么——多看几次你选择的 boot-loader/boot-manager 的文档，想想它和 bcache 一起用会不会有兼容性问题。
*   如果所有相关的设备都通过下面这样的命令连接起来的话，bcache 会自动把缓存设备连接到后端设备，步骤5就可以跳过。`# make-bcache -B /dev/sd? /dev/sd? -C /dev/sd?`

现在你有了一个 `/dev/bcache0`。

5\. 配置固态硬盘。

下面这个例子是把整个固态硬盘（`/dev/sdb`）作为缓存设备格式化，并链接到后端设备：

```
# make-bcache -C /dev/sdb
# echo /dev/sdb > /sys/fs/bcache/register 
# echo *前面的命令输出的UUID* > /sys/block/bcache0/bcache/attach

```

**Note:** 如果忘了 UUID 是什么，可以用 `ls /sys/fs/bcache/` 命令找到（如果缓存设备成功链接），最长的那一串东西就是 UUID。

6\. 格式化 bcache 设备。如果你要在 `/dev/bcache0` 里面分区的话，用 LVM 或者 btrfs 的 子卷来实现，比如下面的例子用 btrfs 的子卷功能分了 `/` 和 `/home` 两个区：

```
# mkfs.btrfs /dev/bcache0
# mount /dev/bcache0 /mnt/
# btrfs subvolume create /mnt/root
# btrfs subvolume create /mnt/home
# umount /mnt

```

你甚至可以配置 LUKS 如果你想要用类似 cryptsetup 的东西。把内核 option 'cryptdevice' 指向 bcache 设备是没有问题的。

7\. 配置安装挂载点（这里用的是步骤3的分区方案和步骤6的btrfs子卷分区方案）：

```
# mkfs.ext4 /dev/sda2 （arch_boot 分区）
# mkfs.msdos /dev/sda1 (如果你的 ESP 分区有至少 500MB，请用 mkfs.vfat 命令来创建一个 FAT32 分区)
# pacman -S arch-install-scripts
# mount /dev/bcache0 -o subvol=root,compress=lzo /mnt/ （挂载btrfs的root子卷作为根目录）
# mkdir /mnt/boot /mnt/home
# mount /dev/bcache0 -o subvol=home,compress=lzo /mnt/home （挂载btrfs的home子卷作为home目录）
# mount /dev/sda2 /mnt/boot
# mkdir /boot/efi
# mount /dev/sda1 /mnt/boot/efi/

```

8\. 按照 [Installation Guide](/index.php/Installation_guide#Connect_to_the_internet "Installation guide") 的步骤安装系统，除了下面这个：

在修改 `/etc/mkinitcpio.conf` 并运行 `mkinitcpio -p linux` 之前：

*   在新系统上，从 [AUR](/index.php/AUR "AUR") 安装 [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/)。
*   修改 `/etc/mkinitcpio.conf`:
    *   添加 bcache 到 MODULES=() 里面
    *   添加 bcache 到 HOOKS=() 的 block 和 filesystems 之间

**Note:** 因为安装介质不会储存任何更改，所以如果你想在重启之后再在安装介质里打开bcache的后端设备，你需要手动注册它。首先确认 bcache 模块已经加载，然后把相关的设备都 echo 到 `/sys/bcache/register`。可以通过 `dmesg` 来检查是否已经成功注册。

## 从安装盘访问bcache分区

要访问一个在安装盘启动之前就已经存在的 bcache 分区，首先从 AUR 安装 [bcache-tools](https://aur.archlinux.org/packages/bcache-tools/)，然后加载 bcache 模块：

```
# modprobe bcache

```

然后强制内核重新加载分区表：

```
# partprobe

```

现在 `/dev/bcache*` 应该会存在了，挂载、格式化之类的操作也可以进行了。

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

这里举例的是缩小4G容量。

1\. 切换缓存模式，从 writeback 改成 writethrough，并等待缓存写入后端设备。

```
# echo writethrough > /sys/block/bcache0/bcache/cache_mode
$ watch cat /sys/block/bcache0/bcache/state

```

请等到第二个命令输出 "clean"。

###### 强制把缓存写入后端设备

```
 # echo 0 > /sys/block/bcache0/bcache/writeback_percent

```

这会把缓存比例改成0，从而强制把缓存的内容写入到后端设备。

然后把缓存比例改回来：

```
 # echo 10 > /sys/block/bcache0/bcache/writeback_percent

```

2\. 为了避免之后缩小分区的时候不会破坏文件系统，请把文件系统缩小比想要缩小的大小更多的量。比如例子里要把分区缩小4G，那就要把文件系统缩小5G以避免破坏了文件系统。如果用的是 btrfs，用下面的命令来缩小文件系统：

```
# btrfs filesystem resize -5G /

```

对于 ext3/4，用的命令是 *resize2fs*，但是需要目标文件系统没有处于挂载：

```
$ df -h /home
/dev/bcache0    290G   20G   270G   1% /home
# umount /home
# resize2fs /dev/bcache0 283G

```

3\. 重启到 LiveCD/USB盘 (并不需要支持 bcache) 并使用 fdisk、gdisk、parted或者其他你用得顺手的工具去把后端分区删掉并重新创建一个 start 位置一样的、但是总大小少4G的分区。

**Warning:** 不要使用类似 Gparted 的工具，因为它们会进行文件系统操作！它们可能识别不出来 bcache 分区并破坏它！

4\. 重启到原来的系统，现在你的文件系统会挂载好，并且分区已经缩小了4G。现在要做的是把文件系统扩展到分区的大小。对于 btrfs，命令是：

```
# btrfs filesystem resize max /

```

对于 ext3/4：

```
# resize2fs /dev/bcache0

```

5\. 把缓存模式重新改成 writeback （如果你想用 writeback 的话）：

```
# echo writeback > /sys/block/bcache0/bcache/cache_mode

```

**Note:** 如果你够小心，第二步里面文件系统可以刚好缩小4G而不预留更多的空间，但是很多分区工具并不是按照字面意思来工作的，它们会把分区的起始和终止位置对齐到底层硬盘的 sector 边界，所以就会出现意料之外的文件系统破坏事故。小心为妙。

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