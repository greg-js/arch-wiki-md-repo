相关文章

*   [udev](/index.php/Udev_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Udev (简体中文)")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")
*   [NTFS Write Support](/index.php/NTFS_Write_Support "NTFS Write Support")
*   [Firefox Ramdisk](/index.php/Firefox_Ramdisk "Firefox Ramdisk")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")

**翻译状态：** 本文是英文页面 [fstab](/index.php/Fstab "Fstab") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-05-07，点击[这里](https://wiki.archlinux.org/index.php?title=fstab&diff=0&oldid=223041)可以查看翻译后英文页面的改动。

[fstab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5)文件可用于定义磁盘分区，各种其他块设备或远程文件系统应如何装入文件系统。

每个文件系统在一个单独的行中描述。这些定义将在引导时动态地转换为系统挂载单元，并在系统管理器的配置重新加载时转换。在启动需要挂载的服务之前，默认设置会自动[fsck](/index.php/Fsck "Fsck")和挂载文件系统。例如，[systemd](/index.php/Systemd "Systemd")会自动确保远程文件系统挂载（如[NFS](/index.php/NFS "NFS")或[Samba](/index.php/Samba "Samba")）仅在网络设置完成后启动。因此，在`/etc/fstab`中指定的本地和远程文件系统挂载应该是开箱即用的。有关详细信息，请参阅 [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5) 。

`mount`命令将使用fstab，如果仅给出其中一个目录或设备，则填充其他参数的值。 这样做时，也将使用fstab中列出的挂载选项。

## Contents

*   [1 文件示例](#.E6.96.87.E4.BB.B6.E7.A4.BA.E4.BE.8B)
*   [2 字段定义](#.E5.AD.97.E6.AE.B5.E5.AE.9A.E4.B9.89)
*   [3 文件系统标识](#.E6.96.87.E4.BB.B6.E7.B3.BB.E7.BB.9F.E6.A0.87.E8.AF.86)
    *   [3.1 内核名称](#.E5.86.85.E6.A0.B8.E5.90.8D.E7.A7.B0)
    *   [3.2 标签](#.E6.A0.87.E7.AD.BE)
    *   [3.3 UUID](#UUID)
*   [4 提示和技巧](#.E6.8F.90.E7.A4.BA.E5.92.8C.E6.8A.80.E5.B7.A7)
    *   [4.1 自动挂载](#.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
    *   [4.2 交换分区 UUID](#.E4.BA.A4.E6.8D.A2.E5.88.86.E5.8C.BA_UUID)
    *   [4.3 路径名有空格](#.E8.B7.AF.E5.BE.84.E5.90.8D.E6.9C.89.E7.A9.BA.E6.A0.BC)
    *   [4.4 外部设备](#.E5.A4.96.E9.83.A8.E8.AE.BE.E5.A4.87)
    *   [4.5 atime 参数](#atime_.E5.8F.82.E6.95.B0)
    *   [4.6 tmpfs](#tmpfs)
        *   [4.6.1 使用](#.E4.BD.BF.E7.94.A8)
    *   [4.7 普通用户读写 FAT32](#.E6.99.AE.E9.80.9A.E7.94.A8.E6.88.B7.E8.AF.BB.E5.86.99_FAT32)
*   [5 参见](#.E5.8F.82.E8.A7.81)

## 文件示例

一个简单的 `/etc/fstab`，使用内核名称标识磁盘:

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
tmpfs                  /tmp          tmpfs     nodev,nosuid          0      0
/dev/sda1              /             ext4      defaults,noatime      0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      defaults,noatime      0      2

```

## 字段定义

`/etc/fstab` 文件包含了如下字段，通过空格或 Tab 分隔：

```
<file system>	<dir>	<type>	<options>	<dump>	<pass>

```

*   **<file systems>** - 要挂载的分区或存储设备.
*   **<dir>** - <file systems>的挂载位置。
*   **<type>** - 要挂载设备或是分区的文件系统类型，支持许多种不同的文件系统：`ext2`, `ext3`, `ext4`, `reiserfs`, `xfs`, `jfs`, `smbfs`, `iso9660`, `vfat`, `ntfs`, `swap` 及 `auto`。 设置成`auto`类型，mount 命令会猜测使用的文件系统类型，对 CDROM 和 DVD 等移动设备是非常有用的。
*   **<options>** - 挂载时使用的参数，注意有些 参数是特定文件系统才有的。一些比较常用的参数有 ([mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8))：

*   `auto` - 在启动时或键入了 `mount -a` 命令时自动挂载。
*   `noauto` - 只在你的命令下被挂载。
*   `exec` - 允许执行此分区的二进制文件。
*   `noexec` - 不允许执行此文件系统上的二进制文件。
*   `ro` - 以只读模式挂载文件系统。
*   `rw` - 以读写模式挂载文件系统。
*   `user` - 允许任意用户挂载此文件系统，若无显示定义，隐含启用 `noexec`, `nosuid`, `nodev` 参数。
*   `users` - 允许所有 users 组中的用户挂载文件系统.
*   `nouser` - 只能被 root 挂载。
*   `owner` - 允许设备所有者挂载.
*   `sync` - I/O 同步进行。
*   `async` - I/O 异步进行。
*   `dev` - 解析文件系统上的块特殊设备。
*   `nodev` - 不解析文件系统上的块特殊设备。
*   `suid` - 允许 suid 操作和设定 sgid 位。这一参数通常用于一些特殊任务，使一般用户运行程序时临时提升权限。
*   `nosuid` - 禁止 suid 操作和设定 sgid 位。
*   `noatime` - 不更新文件系统上 inode 访问记录，可以提升性能(参见 [atime 参数](#atime_.E5.8F.82.E6.95.B0))。
*   `nodiratime` - 不更新文件系统上的目录 inode 访问记录，可以提升性能(参见 [atime 参数](#atime_.E5.8F.82.E6.95.B0))。
*   `relatime` - 实时更新 inode access 记录。只有在记录中的访问时间早于当前访问才会被更新。（与 noatime 相似，但不会打断如 mutt 或其它程序探测文件在上次访问后是否被修改的进程。），可以提升性能(参见 [atime 参数](#atime_.E5.8F.82.E6.95.B0))。
*   `flush` - `vfat` 的选项，更频繁的刷新数据，复制对话框或进度条在全部数据都写入后才消失。
*   `defaults` - 使用文件系统的默认挂载参数，例如 `ext4` 的默认参数为:`rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, `async`.

*   **<dump>** dump 工具通过它决定何时作备份. dump 会检查其内容，并用数字来决定是否对这个文件系统进行备份。 允许的数字是 0 和 1 。0 表示忽略， 1 则进行备份。大部分的用户是没有安装 dump 的 ，对他们而言 <dump> 应设为 0。

*   **<pass>** fsck 读取 <pass> 的数值来决定需要检查的文件系统的检查顺序。允许的数字是0, 1, 和2。 根目录应当获得最高的优先权 1, 其它所有需要被检查的设备设置为 2\. 0 表示设备不会被 fsck 所检查。

## 文件系统标识

在 `/etc/fstab`配置文件中你可以以三种不同的方法表示文件系统：内核名称、UUID 或者 label。使用 UUID 或是 label 的好处在于它们与磁盘顺序无关。如果你在 BIOS 中改变了你的存储设备顺序，或是重新拔插了存储设备，或是因为一些 BIOS 可能会随机地改变存储设备的顺序，那么用 UUID 或是 label 来表示将更有效。参见 [持久化块设备名称](/index.php/Persistent_block_device_naming "Persistent block device naming") 。

要显示分区的基本信息请运行：

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL      UUID                                 MOUNTPOINT
sda                                                         
├─sda1 ext4   Arch_Linux 978e3e81-8048-4ae1-8a06-aa727458e8ff /
├─sda2 ntfs   Windows    6C1093E61093B594                     
└─sda3 ext4   Storage    f838b24e-3a66-4d02-86f4-a2e73e454336 /media/Storage
sdb                                                           
├─sdb1 ntfs   Games      9E68F00568EFD9D3                     
└─sdb2 ext4   Backup     14d50a6c-e083-42f2-b9c4-bc8bae38d274 /media/Backup
sdc                                                           
└─sdc1 vfat   Camera     47FA-4071                            /media/Camera
```

### 内核名称

你可以使用 `fdisk -l` 来获得内核名称，前缀是 `dev`.

### 标签

**注意:** 使用这一方法，每一个标签必须是唯一的.

添加标签的工具和方法位于 [这里](/index.php/Persistent_block_device_naming "Persistent block device naming")。要显示所有设备的标签，可以使用 `lsblk -f` 命令。在 `/etc/fstab` 中使用 `LABEL=` 作为设备名的开头 :

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass>

tmpfs                  /tmp          tmpfs     nodev,nosuid   0      0

LABEL=Arch_Linux       /             ext4      defaults,noatime      0      1
LABEL=Arch_Swap        none          swap      defaults              0      0
```

### UUID

所有分区和设备都有唯一的 UUID。它们由文件系统生成工具 (`mkfs.*`) 在创建文件系统时生成。

`lsblk -f` 命令将显示所有设备的 UUID 值。`/etc/fstab` 中使用 `UUID=` 前缀:

 `/etc/fstab` 
```
# <file system>                           <dir>         <type>    <options>             <dump> <pass>

tmpfs                                     /tmp          tmpfs     nodev,nosuid          0      0

UUID=24f28fc6-717e-4bcd-a5f7-32b959024e26 /     ext4              defaults,noatime      0      1
UUID=03ec5dd3-45c0-4f95-a363-61ff321a09ff /home ext4              defaults,noatime      0      2
UUID=4209c845-f495-4c43-8a03-5363dd433153 none  swap              defaults              0      0
```

## 提示和技巧

### 自动挂载

*   如果 `/home` 分区较大，可以让不依赖 `/home` 分区的服务先启动。把下面的参数添加到 `/etc/fstab` 文件中 `/home` 项目的参数部分即可：

```
noauto,x-systemd.automount

```

这样 `/home` 分区只有需要访问时才会被挂载。内核会缓存所有的文件操作，直到 `/home` 分区准备完成。

**注意:** 这样做会使 `/home` 的文件系统类型被识别为 `autofs`，造成 [mlocate](/index.php/Mlocate "Mlocate") 查询时忽略该目录。实际加速效果因配置而异，所以请自己权衡是否需要。

*   挂载远程文件系统也是同理。如果你仅想在需要的时候才挂载，也可以添加 `noauto,x-systemd.automount` 参数。另外，可以设置 `x-systemd.device-timeout=#` 参数，设置超时时间，以防止网络资源不能访问的时候浪费时间。

*   如果你的加密文件系统需要密钥，则需要添加 `noauto` 参数到 `/etc/crypttab` 文件中的对应位置。systemd 开机的时候就不会打开这个加密设备，会一直等待到设备被访问时再使用密钥文件挂载。比如在使用加密RAID设备的时候可以节省一定的时间，因为 systemd 不必等到设备可用后才能访问。例如：

 `/etc/crypttab`  `data /dev/md0 /root/key noauto` 

### 交换分区 UUID

如果交换分区没有 UUID，可以手动加入。如果使用 `lsblk -f` 命令没有列出交换分区的 UUID 就说明发生了这种情况。下面是为交换分区指定 UUID 的步骤：

确定交换分区：

```
# swapon -s

```

禁用交换分区：

```
# swapoff /dev/sda7

```

用新 UUID 重新创建交换分区：

```
# mkswap -U random /dev/sda7

```

激活交换分区:

```
# swapon /dev/sda7

```

### 路径名有空格

如果挂载的路径中有空格，可以使用 "\040" 转义字符来表示空格（以三位八进制数来进行表示）

 `/etc/fstab` 
```
UUID=47FA-4071     /home/username/Camera<font color="grey">\040</font>Pictures   vfat  defaults,noatime      0  2
/dev/sda7          /media/100<font color="grey">\040</font>GB<font color="grey">\040</font>(Storage)       ext4  defaults,noatime,user  0  0
```

### 外部设备

外部设备在插入时挂载，在未插入时忽略。这需要 `nofail` 选项，可以在启动时若设备不存在直接忽略它而不报错.

 `/etc/fstab` 
```
 /dev/sdg1    /media/backup    jfs    defaults,nofail    0  2

```

### atime 参数

使用 `noatime`, `nodiratime` 或 `relatime` 可以提升 ext2， ext3 及 ext4 格式磁盘的性能。 Linux 在默认情况下使用`atime`选项，每次在磁盘上读取（或写入）数据时都会产生一个记录。这是为服务器设计的，在桌面使用中意义不大。默认的 `atime` 选项最大的问题在于即使从页面缓存读取文件(从内存而不是磁盘读取)，也会产生磁盘写操作！

使用 `noatime` 选项阻止了读文件时的写操作。大部分应用程序都能很好工作。只有少数程序如 [Mutt](/index.php/Mutt "Mutt") 需要这些信息。Mutt 的用户应该使用 `relatime` 选项。使用 `relatime` 选项后，只有文件被修改时才会产生文件访问时间写操作。`nodiratime` 选项仅对目录禁用了文件访问时间。`relatime` 是比较好的折衷，[Mutt](/index.php/Mutt "Mutt") 等程序还能工作，但是仍然能够通过减少访问时间更新提升系统性能。

**注意:** `noatime` 已经包含了 `nodiratime`。不需要同时指定。

### tmpfs

[tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") 是一个临时文件系统，驻留于你的交换分区或是内存中（取决于你的使用情况）。使用它可以提高文件访问速度，并能保证重启时会自动清除这些文件。

经常使用 tmpfs 的目录有 [/tmp](http://www.pathname.com/fhs/2.2/fhs-3.15.html), [/var/lock](http://www.pathname.com/fhs/2.2/fhs-5.9.html) and [/var/run](http://www.pathname.com/fhs/2.2/fhs-5.13.html). 不要将之使用于 [/var/tmp](http://www.pathname.com/fhs/2.2/fhs-5.15.html), 因为这一目录中的临时文件在重启过程中需要被保留。使用 tmpfs `/run` 目录，`/var/run` 和 `/var/lock` 是为了兼容老版本建立的链接。默认 `/etc/fstab`中的的`/tmp`也是 tmpfs.

默认情况下， tmpfs 分区被设置为你总的内存的一半，当然你可以自由设定这一值。注意实际中内存和交换分区的使用情况取决于你的使用情况，而 tmpfs 分区在其真正使用前是不会占用存储空间的。

要将 `/tmp` 放到 tmpfs，将下行加入 `/etc/fstab`：

 `/etc/fstab` 
```
.....
tmpfs /tmp      tmpfs nodev,nosuid                 0 0
.....
```

可以指定大小，但不要修改 `mode` 选项，以保证文件具有正确的访问权限(1777)。在上例中 `/tmp` 将最多使用一半内存，要指定最大空间，使用 `size` 挂载选项：

 `/etc/fstab` 
```
.....
tmpfs /tmp      tmpfs nodev,nosuid,size=2G          0 0
.....
```

这里有一个更高级的例子，展示如何为用户添加 tmpfs 挂载。这对于网站、mysql 临时文件, `~/.vim/`, 和其他情况很有用。尝试并获得理想的挂载选项来完成目标是很重要的。目标是尽量采用安全的策略来防止滥用。限制大小，同时指定 uid 和 gid 加上 mode 是非常安全的。[更多信息](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99).

 `/etc/fstab`  `tmpfs /www/cache tmpfs rw,size=1G,nr_inodes=5k,noexec,nodev,nosuid,uid=648,gid=648,mode=1700 0 0` 

参阅 **mount** 命令 man 手册以获得更多的内容。

重启后方能生效。注意不要直接执行 `mount -a` 命令，因为可能造成无法访问当前目录中的文件（比如你应该保证 lockfiles 的正常存在）。然而，如果它们都是空的，那么就可以直接执行 `mount -a` 而不必重启电脑。

应用更改后，可以通过 `findmnt` 检查是否生效：

 `$ findmnt --target /tmp` 
```
TARGET SOURCE FSTYPE OPTIONS
/tmp   tmpfs  tmpfs  rw,nosuid,nodev,relatime
```

#### 使用

一般需要大量读写操作的程序在使用 tmpfs 时都会提升性能。有些程序把共享内存放到 tmpfs 上时性能会大幅提升，例如[将 Firefox Profile 文件夹放到内存](/index.php/Firefox_Ramdisk "Firefox Ramdisk")后，Firefox 性能大幅提升。

**Note:** tmpfs 目录(`/tmp`) 挂载时需要去掉 `noexec` 参数，否则有些编译程序无法执行，此外，tmpfs 的默认大小是内存的一半，可能会产生空间不够的问题。

下面命令可以让[makepkg](/index.php/Makepkg "Makepkg")在tmpfs目录进行编辑，也可以在在`/etc/makepkg.conf`中进行设置:

```
$ BUILDDIR=/tmp/makepkg makepkg

```

### 普通用户读写 FAT32

为了取得对 FAT32 分区的写权限，你必须修改`/etc/fstab`文件。

 `/etc/fstab`  `/dev/sdxY    /mnt/some_folder  vfat   user,rw,umask=000              0  0` 

“users”标签的意思是任何用户（甚至非 root 用户）都可以挂载或卸载分区 '/dev/sdX'。“rw”标签则分配读写的使用权。但我不知道“umask”标签的意义（umask 是权限掩码命令 umask=000 指任何人没有特权，且权限为777，即所有人都可以读、写、执行）。我曾试图在“man mount”中查询，但是没有什么结果。

比如你的 FAT32 分区在 '/dev/sda9'，你想将其挂载到 '/mnt/fat32'，那么你需要输入并运行

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   user,rw,umask=111,dmask=000    0  0` 

## 参见

*   [Full device listing including block device](http://www.kernel.org/pub/linux/docs/device-list/devices.txt)
*   [Filesystem Hierarchy Standard](http://www.pathname.com/fhs/2.2/index.html)
*   [30x Faster Web-Site Speed](http://www.askapache.com/web-hosting/super-speed-secrets.html) (详细介绍 tmpfs)