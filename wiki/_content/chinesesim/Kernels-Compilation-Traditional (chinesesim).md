**翻译状态：** 本文是英文页面 [Kernels/Traditional_compilation](/index.php/Kernels/Traditional_compilation "Kernels/Traditional compilation") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-07-20，点击[这里](https://wiki.archlinux.org/index.php?title=Kernels%2FTraditional_compilation&diff=0&oldid=442198)可以查看翻译后英文页面的改动。

以下的一些步骤有助于你从 **kernel.org 源代码** 编译自己的内核。这种方法是一种对所有发行版均适用的传统方法；但同时，本文也包含了用 makepkg 和 pacman 干净安装自己的内核的优秀方法。

另外你可以选择用 [ABS 工具](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 建立并安装你的内核；参见 [用ABS工具编译内核](/index.php/Kernels/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels/Arch Build System (简体中文)")。使用已有的 [linux](https://www.archlinux.org/packages/?name=linux) PKGBUILD 文件可以自动化大多数过程并生成一个软件包，然而，一些 Arch 使用者更喜欢用**传统**方法。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 准备](#准备)
    *   [1.1 安装核心软件包](#安装核心软件包)
    *   [1.2 创建内核编译目录](#创建内核编译目录)
    *   [1.3 获取源码](#获取源码)
    *   [1.4 解压内核代码](#解压内核代码)
*   [2 配置](#配置)
    *   [2.1 简单配置](#简单配置)
    *   [2.2 导出当前内核设置](#导出当前内核设置)
        *   [2.2.1 用 localmodconfig 生成配置](#用_localmodconfig_生成配置)
    *   [2.3 高级配置](#高级配置)
*   [3 编译和安装](#编译和安装)
    *   [3.1 编译内核](#编译内核)
    *   [3.2 编译内核模块](#编译内核模块)
    *   [3.3 拷贝内核到 /boot 目录](#拷贝内核到_/boot_目录)
    *   [3.4 制作初始化内存盘](#制作初始化内存盘)
        *   [3.4.1 自动生成](#自动生成)
        *   [3.4.2 手动方法](#手动方法)
    *   [3.5 拷贝System.map](#拷贝System.map)
*   [4 Bootloader 设置](#Bootloader_设置)

## 准备

准备编译时，不需要也不建议使用 root 账号或用 [Sudo](/index.php/Sudo "Sudo") 等工具获取 root 权限。

### 安装核心软件包

安装 [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) 软件组，这个组包含了 [make](https://www.archlinux.org/packages/?name=make) 和 [gcc](https://www.archlinux.org/packages/?name=gcc) 等需要的软件包。同时也建议参考 Arch kernel [PKGBUILD](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/linux) 安装下面的软件包：[xmlto](https://www.archlinux.org/packages/?name=xmlto), [docbook-xsl](https://www.archlinux.org/packages/?name=docbook-xsl), [kmod](https://www.archlinux.org/packages/?name=kmod), [inetutils](https://www.archlinux.org/packages/?name=inetutils), [bc](https://www.archlinux.org/packages/?name=bc)

### 创建内核编译目录

建议创建单独的内核编译目录，本文使用 `home` 下的 `kernelbuild` 目录。

```
$ mkdir ~/kernelbuild

```

### 获取源码

*   验证下载到的任何tar压缩包的签名总是好的做法。参见[kernel.org/signature](http://kernel.org/signature.html#using-gnupg-to-verify-kernel-signatures)以了解此如何运作及其他细节。
*   [systemd](/index.php/Systemd "Systemd") 需要 3.11 或更新版本，需要 [cgroups](/index.php/Cgroups "Cgroups") 架构支持的话，需要 4.2 或更新的版本，参考 `/usr/share/systemd/README`。

从 [http://www.kernel.org](http://www.kernel.org) 获得源码, 应该是 [tarball](https://en.wikipedia.org/wiki/Tar_(computing) (`tar.xz`) 文件。可以在浏览器右击 `tar.xz` 链接下载或通过 [FTP](/index.php/Ftp#FTP "Ftp"), [RSYNC](/index.php/Rsync "Rsync") 或 [Git](/index.php/Git "Git") 下载，下面例子中使用 [wget](https://www.archlinux.org/packages/?name=wget) 下载 3.18 内核到 `~/kernelbuild` 目录:

```
$ cd ~/kernelbuild
$ wget [https://kernel.org/pub/linux/kernel/v3.x/linux-3.18.28.tar.xz](https://kernel.org/pub/linux/kernel/v3.x/linux-3.18.28.tar.xz)

```

将源码拷贝到你的构建目录:

```
$ cp linux-3.2.9.tar.bz2 ~/kernelbuild/

```

### 解压内核代码

*   将其解压后进入源码目录:

```
$ tar -xvJf linux-3.18.28.tar.xz

```

为确保内核树绝对干净，进入内核目录并执行 `make mrproper` 命令:

```
$ cd linux-3.18.28
$ make clean && make mrproper

```

## 配置

这是定制精确适配你的电脑的规格的内核的最关键步骤。内核及[内核模块](/index.php/Kernel_modules "Kernel modules")的配置通过 `.config` 设置。不需要 root 权限就能进行内核配置。

### 简单配置

**Note:** 定制的内核可以配置使用和 Arch 内核不同的功能，`y` 是启用, `n` 是禁用, `m` 是需要时启用.

参考使用下面内容可以节省时间：

*   使用 Arch 官方内核的设置(推荐)
*   生成正在运行内核的配置文件和设置。

### 导出当前内核设置

导出正在运行的内核的 .config 配置文件:

```
$ zcat /proc/config.gz > .config

```

**警告:** 如果使用导出的 `.config` 文件，不要忘了在 `General Setup --->` 选项中修改内核版本，这样可以避免编译的内核覆盖当前内核文件。

#### 用 localmodconfig 生成配置

**Tip:** 使用此方法是，请插上所有需要使用的设备。

自 2.6.32 版本内核开始，可以使用 `localmodconfig` 命令创建 `.config` 文件。当前内核没有被使用的选项都会被禁用。也就是说，只会启用当前在使用的选项。

虽然这个方法可以生成一个非常精简高效的内核，也是有缺点的，例如无法支持新硬件、外围设备或其它功能。

```
$ make localmodconfig

```

### 高级配置

**Tip:** 如果不想在启动和关闭时看到很多内核输出，可以禁用相关的调试选项。

有多种方式可以协助配置内核：

*   `make menuconfig`: 老的 ncurses 界面，被 `nconfig` 取代
*   `make nconfig`: 新的命令行 ncurses 界面
*   `make xconfig`: 用户友好的图形界面，需要安装 [packagekit-qt4](https://www.archlinux.org/packages/?name=packagekit-qt4)。建议没有经验的用户使用此方法。
*   `make gconfig`: 和 xconfig 类似的图形界面，使用 gtk.

在内核源代码目录执行选择的方法，将生成一个全新的`.config`，可选参数默认是选中的，但是如果有老内核的 `.config` 文件，这些参数不一定会被选中。

改变配置文件并保存。建议在源代码目录外备份`.config`,因为你可能需要编译多次，直到所有的选项都配置正确。如果不确定每个选项的影响，每次编译只改变少量选项。如果无法启动新构建的内核，参见[这里](https://www.archlinux.org/news/users-of-unofficial-kernels-must-enable-devtmpfs-support/)查看必须的配置项列表。从liveCD运行`$ lspci -k #`以列出使用中的内核模块的名字。最重要的是，你必须保留 [systemd](/index.php/Systemd "Systemd") 需要的 CGROUPS 支持。

## 编译和安装

如果希望 [gcc](https://www.archlinux.org/packages/?name=gcc) 根据处理器指令集进行优化， 编辑内核目录下的 `arch/x86/Makefile` (i686) 或 `arch/x86_64/Makefile` (86_64)文件：

*   查找 `Processor type and features > Processor Family` 中设置的处理器系列 `CONFIG_MK8,CONFIG_MPSC,CONFIG_MCORE2,CONFIG_MATOM,CONFIG_GENERIC_CPU`
*   将 cc 调用选项设置为 `-march=native`，例如 `cflags-$(CONFIG_MK8) += $(call cc-option,-march=native)`.

对 32bit 内核，需要编辑 `arch/x86/Makefile_32.cpu` 并设置处理器的 `-march=native`。

### 编译内核

编译时间将从15分钟到超过一小时不等。这很大程度依赖于选择了多少选项/模块和处理器性能。详情参考 [Makeflags](/index.php/Makepkg#MAKEFLAGS "Makepkg")。`.config` 配置好之后，在内核目录运行：

```
$ make

```

### 编译内核模块

**Warning:** 从这里开始，需要 root 权限执行命令，否则会失败.

编译完内核后编译模块:

```
# make modules_install

```

该命令将编译好的模块拷贝至 `/lib/modules/<kernel version>-<config local version>`，例如 `/lib/modules/3.18.28-ARCH`。这样，这些模块和那些被你电脑上其他内核使用的模块就独立开来。

**Tip:** 如果系统需要正常 Linux 内核外的模块，需要在定制内核安装完成之后重新编译它们。Nvidia 显卡模块可以参考 [NVIDIA#Alternate install: custom kernel](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA")。

### 拷贝内核到 /boot 目录

内核编译完成后会生成内核的 `bzImage` (big zImage) 文件，根据系统架构，将此文件复制到 `/boot` 目录，以 3.18 内核为例：

*   32-bit (i686) kernel:

```
# cp -v arch/x86/boot/bzImage /boot/vmlinuz-linux318

```

*   64-bit (x86_64) kernel:

```
# cp -v arch/x86_64/boot/bzImage /boot/vmlinuz-linux318

```

### 制作初始化内存盘

初始化内存盘，是一个在真正的根文件系统可访问之前被挂载的初始化根目录文件系统。初始化内存盘（initrd）被绑定到对应的内核，且作为内核启动过程的一部分被载入。内核将该初始化内存盘（initrd）作为两阶段启动过程的一部分挂载起来，以载入模块使得真正的文件系统可用，然后得到真正的根文件系统。初始化内存盘包含实现以上过程的目录和可执行文件的最小集合，例如用来将内核模块安装到内核的insmod工具。对桌面或服务器Linux系统来说，初始化内存盘(initrd)就是一个临时的文件系统。其生命周期短暂，仅作为到真正的根文件系统的桥梁。在没有可变存储的嵌入式系统中，初始化内存盘就是永久的根文件系统。参考 [Initramfs on Wikipedia](https://en.wikipedia.org/wiki/Initrd "wikipedia:Initrd") 和 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")。

/boot 中的文件可以取任何名字。然而，为了方便区分，建议采取统一的命名规范，例如使用 `linux<major revision><minor revision>`。

如果你使用LILO且其无法与内核设备映射器驱动连通，你可能需要先运行`modprobe dm-mod`命令。

#### 自动生成

复制和修改 [mkinitcpio preset](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")，就能用官方内核一样的方式生成自定义内核的 initramfs 镜像。下面例子中将已有的 preset 复制到 `linux318` 要使用的版本:

```
# cp /etc/mkinitcpio.d/linux.preset /etc/mkinitcpio.d/linux318.preset

```

针对定制内核编辑和修改此文件，`ALL_kver=` 应该和定制内核匹配：

 `/etc/mkinitcpio.d/linux318.preset` 
```
...
ALL_kver="/boot/vmlinuz-linux318"
...
default_image="/boot/initramfs-linux318.img"
...
fallback_image="/boot/initramfs-linux318-fallback.img"
```

用官方内核一样的方式生成 initramfs 镜像：

```
# mkinitcpio -p linux318

```

#### 手动方法

不是呀 preset 文件，可以用 mkinitcpio 手动生成：

```
# mkinitcpio -k <kernelversion> -g /boot/initramfs-<file name>.img

```

*   `-k` (--kernel <kernelversion>): 生成 initramfs image 的内核版本. `<kernelversion>` 需要和内核源代码目录和`/usr/lib/modules/`下的模块目录一致.
*   `-g` (--generate <filename>): 要生成的 initramfs 文件。

示例：

```
# mkinitcpio -k linux-3.18.28 -g /boot/initramfs-linux318.img

```

### 拷贝System.map

`System.map`文件并非 Linux 启动必须的。它是一种“电话本”，列出内核的某够特定构建的功能。System.map 包含一张内核标识符的列表（例如函数名，变量名等等）和他们相应的地址。该“标识符到地址的映射”是用于：

*   某些进程，像klogd, ksymoops等
*   OOPS处理程序，当内核崩溃出错信息释放到屏幕时（例如类似于内核在某个函数中崩溃了的信息）。

**Tip:** UEFI partitions are formatted using FAT32, which does not support symlinks.

如果 `/boot` 支持软链接(i.e., not FAT32), 将 `System.map` 复制到 `/boot`, 然后创建 `/boot/System.map` 软链接到 `/boot/System.map-YourKernelName`:

```
# cp System.map /boot/System.map-YourKernelName
# ln -sf /boot/System.map-YourKernelName /boot/System.map

```

完成以上所有步骤之后，你的/boot目录中应该多出以下三个文件和一个软链接：

*   Kernel: `vmlinuz-YourKernelName`
*   Initramfs: `Initramfs-YourKernelName.img`
*   System Map: `System.map-YourKernelName`
*   System Map kernel symlink

## Bootloader 设置

在你的启动器（bootloader）配置文件中为你神奇的新内核添加一个入口。范例见[GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), [GRUB2](/index.php/GRUB2 "GRUB2") or [Syslinux](/index.php/Syslinux "Syslinux")。

**Tip:** 内核源码中有一个为LILO准备的脚本，以自动化实现该步骤：`$ arch/x86/boot/install.sh`。记得以root权限执行`lilo`来更新它。