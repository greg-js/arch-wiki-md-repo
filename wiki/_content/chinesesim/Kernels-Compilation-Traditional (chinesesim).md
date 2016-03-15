以下的一些步骤有助于你从 **kernel.org 源代码** 编译自己的内核。这种方法是一种对所有发行版均适用的传统方法；但同时，本文也包含了用 makepkg 和 pacman 干净安装自己的内核的优秀方法。

另外你可以选择用 [ABS 工具](/index.php/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch Build System (简体中文)") 建立并安装你的内核；参见 [用ABS工具编译内核](/index.php/Kernels/Arch_Build_System_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels/Arch Build System (简体中文)")。使用已有的 [linux](https://www.archlinux.org/packages/?name=linux) PKGBUILD 文件可以自动化大多数过程并生成一个软件包，然而，一些 Arch 使用者更喜欢用**传统**方法。

## Contents

*   [1 获取源码](#.E8.8E.B7.E5.8F.96.E6.BA.90.E7.A0.81)
    *   [1.1 /usr/src/怎么样?](#.2Fusr.2Fsrc.2F.E6.80.8E.E4.B9.88.E6.A0.B7.3F)
*   [2 构建配置](#.E6.9E.84.E5.BB.BA.E9.85.8D.E7.BD.AE)
    *   [2.1 编译前设置](#.E7.BC.96.E8.AF.91.E5.89.8D.E8.AE.BE.E7.BD.AE)
    *   [2.2 设置内核](#.E8.AE.BE.E7.BD.AE.E5.86.85.E6.A0.B8)
        *   [2.2.1 传统菜单配置（menuconfig）](#.E4.BC.A0.E7.BB.9F.E8.8F.9C.E5.8D.95.E9.85.8D.E7.BD.AE.EF.BC.88menuconfig.EF.BC.89)
        *   [2.2.2 localmodconfig](#localmodconfig)
        *   [2.2.3 本地版本](#.E6.9C.AC.E5.9C.B0.E7.89.88.E6.9C.AC)
*   [3 编译和安装](#.E7.BC.96.E8.AF.91.E5.92.8C.E5.AE.89.E8.A3.85)
    *   [3.1 编译](#.E7.BC.96.E8.AF.91)
    *   [3.2 安装模块](#.E5.AE.89.E8.A3.85.E6.A8.A1.E5.9D.97)
    *   [3.3 拷贝内核到 /boot 目录](#.E6.8B.B7.E8.B4.9D.E5.86.85.E6.A0.B8.E5.88.B0_.2Fboot_.E7.9B.AE.E5.BD.95)
    *   [3.4 制作初始化内存盘](#.E5.88.B6.E4.BD.9C.E5.88.9D.E5.A7.8B.E5.8C.96.E5.86.85.E5.AD.98.E7.9B.98)
    *   [3.5 拷贝System.map](#.E6.8B.B7.E8.B4.9DSystem.map)
*   [4 Bootloader 设置](#Bootloader_.E8.AE.BE.E7.BD.AE)
*   [5 在自定义内核下使用nVIDIA视频驱动](#.E5.9C.A8.E8.87.AA.E5.AE.9A.E4.B9.89.E5.86.85.E6.A0.B8.E4.B8.8B.E4.BD.BF.E7.94.A8nVIDIA.E8.A7.86.E9.A2.91.E9.A9.B1.E5.8A.A8)

## 获取源码

*   先从 `[ftp://ftp.xx.kernel.org/pub/linux/kernel/](ftp://ftp.xx.kernel.org/pub/linux/kernel/)` 或者 `[http://www.kernel.org/pub/linux/kernel/](http://www.kernel.org/pub/linux/kernel/)`获得源码, xx 是你的国家代号 (f.e. 'us', 'uk', 'de', ... - 查看 [完整的镜像列表](http://www.kernel.org))。 如果你没有图形界面的ftp程序，你可以用`wget`。例如，我们可以获取3.2.9的源码并编译；你可以将版本号改成你所需要的版本号。

例:

```
$ wget -c [http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.2.9.tar.bz2](http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.2.9.tar.bz2)

```

*   验证下载到的任何tar压缩包的签名总是好的做法。参见[kernel.org/signature](http://kernel.org/signature.html#using-gnupg-to-verify-kernel-signatures)以了解此如何运作及其他细节。

*   将源码拷贝到你的构建目录:

```
$ cp linux-3.2.9.tar.bz2 ~/kernelbuild/

```

*   将其解压后进入源码目录:

```
$ cd ~/kernelbuild
$ tar -xvjf linux-3.2.9.tar.bz2
$ cd linux-3.2.9

```

运行如下命令以进行编译准备工作：

```
make mrproper

```

该命令确保内核树绝对干净。内核组推荐每次编译内核前都执行该命令。而不要依靠解压后的内核树是干净的。

### /usr/src/怎么样?

作为root用户，使用/usr/src目录编译内核，并创建相关链接，被某些黑客认为是糟糕的习惯。他们认为最干净的方法是仅使用家目录。如果你认同该观点，请作为普通用户构建和配置你的内核，然后作为root用户安装，或者[用makepkg和pacman](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System").

然而，该观点受到争议，其他那些经验丰富的黑客认为作为root在/usr/src/目录下编译的习惯完全安全，可接受，甚至要更好。

所以，你只要选择你认为更舒服的方式就好。

## 构建配置

这是定制精确适配你的电脑的规格的内核的最关键步骤。通过在'menuconfig'中设置合适的配置，你的内核和电脑将会以最有效的方式运行。

### 编译前设置

可选，但是对于初学者强烈推荐：

*   如果你想更改默认的Arch设置，拷贝正在运行的内核的配置文件（.config文件）。

```
 $ zcat /proc/config.gz > .config

```

*   注意`lsmod`输出的当前载入的模块。该输出结果在每个系统上都不一样。

### 设置内核

**警告:** 如果为了早期的KMS，将较新的显卡的*radeon*驱动编译进内核（>3.3.3），你**必须**包括你的显卡的固件文件。否者加速将失效。参见[这里](http://wiki.x.org/wiki/radeonBuildHowTo#Missing_Extra_Firmware)

**Tip:** 通过***简单的配置***是有可能配置出一个无initramfs的内核的。确保显卡/输入/磁盘/文件系统所需的所有模块都被编译进内核。同时至少支持DEVTMPFS_MOUNT，TMPFS，AUTOFS4_FS。如果有疑问，*在尝试编译之前*，请了解这些选项和其含义。

有两个主流选择:

#### 传统菜单配置（menuconfig）

`$ make menuconfig`

该命令将启动一个全新的`.config`配置文件，除非已经存在一个（例如拷贝过来的）配置文件。选项依赖会自动被选中。而新选项（例如用一个旧版本的内核`.config`配置文件）不一定会自动被选中。

改变配置文件并保存。在源代码目录外备份.config文件是明智之举，因为你可能需要编译多次，直到所有的选项都配置正确。如果不确定每个选项的含义，每次编译只改变少量选项。如果无法启动新构建的内核，参见[这里](https://www.archlinux.org/news/users-of-unofficial-kernels-must-enable-devtmpfs-support/)查看必须的配置项列表。从liveCD运行`$ lspci -k #`以列出使用中的内核模块的名字。最重要的是，你必须保持CGROUPS支持。对[systemd](/index.php/Systemd "Systemd")来说，它是必须的。

#### localmodconfig

自2.6.32版本内核以来，该构建选项被用于最简化配置步骤。这是新手的超级捷径，应当只选择那些当前被使用的选项。

为获得最大效用：

1.  启动进入备用`-ARCH`内核，然后插上所有你希望在系统上使用的设备。
2.  在源码目录中运行：`$ make localmodconfig`
3.  配置结果会被写入到`.config`文件。然后你可以进行普通构建安装过程。

#### 本地版本

如果你用当前配置文件编译内核，不要忘记重命名你的内核版本，否者你可能错误地使用一个已存在的内核版本。

```
$ make menuconfig
General setup  --->
 (-ARCH) Local version - append to kernel release '3.n.n-RCn'

```

## 编译和安装

如果你手动编译和安装的话，见下面的步骤：

### 编译

**警告:** 如果你用的是 GRUB，并且同时装有 LILO，不要运行 `make all` ； 因它最后会设置 LILO，这样你可能再也不能启动你的机器了。如果你使用的是 GRUB， 先卸载 LILO(pacman -R lilo)，然后执行`make all`。

*   开始编译。

```
$ make      (等效于make vmlinux && make modules && make bzImage——关于这方面，参见‘make help’以获取详细信息。)

```

or

```
$ make -jN   (N = 处理器数目 + 1) (该选项使得编译时100%使用所有的CPUs。)

```

编译时间将从15分钟到超过一小时不等。这很大程度依赖于选择了多少选项/模块和处理器性能。

### 安装模块

```
# make modules_install

```

该命令将编译好的模块拷贝至`/lib/modules/`[内核版本号 + CONFIG_LOCALVERSION]。这样，这些模块和那些被你电脑上其他内核使用的模块就独立开来。

### 拷贝内核到 /boot 目录

```
# cp -v arch/x86/boot/bzImage /boot/vmlinuz-YourKernelName

```

### 制作初始化内存盘

初始化内存盘（GRUB菜单中的initrd选项，或，“initramfs-YourKernelName.img”文件）是一个在真正的根文件系统可访问之前被挂载的初始化根目录文件系统。初始化内存盘（initrd）被绑定到对应的内核，且作为内核启动过程的一部分被载入。内核将该初始化内存盘（initrd）作为两阶段启动过程的一部分挂载起来，以载入模块使得真正的文件系统可用，然后得到真正的根文件系统。初始化内存盘包含实现以上过程的目录和可执行文件的最小集合，例如用来将内核模块安装到内核的insmod工具。对桌面或服务器Linux系统来说，初始化内存盘(initrd)就是一个临时的文件系统。其生命周期短暂，仅作为到真正的根文件系统的桥梁。在没有可变存储的嵌入式系统中，初始化内存盘就是永久的根文件系统。

如果挂载根文件系统需要你载入任何模块，创建一个内存盘（大部分用户需要这样做）。-k参数接收内核版本，然后追加到你在menuconfig中设置的字符串之后，该字符串被用于定位'/usr/lib/modules'中的相应模块目录。

```
# mkinitcpio -k FullKernelName -c /etc/mkinitcpio.conf -g /boot/initramfs-YourKernelName.img

```

You are free to name the /boot files anything you want. However, using the [kernel-major-minor-revision] naming scheme helps to keep order if you: Keep multiple kernels/ Use mkinitcpio often/ Build third-party modules. 你可以为以上命令中/boot中的文件取任何名字。然而，如果你：使用多个内核/经常使用mkinitcpio/构建第三方模块，使用[内核名-主版本号-次版本号-修订版本号]的命名方案可以保持命名的一致性。

**Tip:** 如果经常重构镜像，用类似`# mkinitcpio -p custom`的命令创建一个独立的预先设置文件可能会有帮助。参见[这里](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")

If you are using LILO and it cannot communicate with the kernel device-mapper driver, you have to run `modprobe dm-mod` first. 如果你使用LILO且其无法与内核设备映射器驱动连通，你可能需要先运行`modprobe dm-mod`命令。

### 拷贝System.map

System.map文件非Linux启动必须的。它是一种“电话本”，列出内核的某够特定构建的功能。System.map包含一张内核标识符的列表（例如函数名，变量名等等）和他们相应的地址。该“标识符到地址的映射”是用于：

*   某些进程，像klogd, ksymoops等
*   OOPS处理程序，当内核崩溃出错信息释放到屏幕时（例如类似于内核在某个函数中崩溃了的信息）。

将System.map拷贝到/boot目录然后创建链接：

```
# cp System.map /boot/System.map-YourKernelName

```

完成以上所有步骤之后，你的/boot目录中应该多出以下三个文件和一个软链接：

```
vmlinuz-YourKernelName          (Kernel)
initramfs-YourKernelName.img    (Ramdisk)
System.map-YourKernelName       (System Map)

```

## Bootloader 设置

在你的启动器（bootloader）配置文件中为你神奇的新内核添加一个入口——范例见[GRUB](/index.php/GRUB "GRUB"), [LILO](/index.php/LILO "LILO"), [GRUB2](/index.php/GRUB2 "GRUB2") or [Syslinux](/index.php/Syslinux "Syslinux")。

**Tip:** 内核源码中有一个为LILO准备的脚本，以自动化实现该步骤：`$ arch/x86/boot/install.sh`。记得以root权限执行`lilo`来更新它。

## 在自定义内核下使用nVIDIA视频驱动

想在你自己编译的内核下用nVIDIA 视频驱动，参见: [如何为定制内核安装 nVIDIA 驱动](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.A4.87.E7.94.A8.E5.AE.89.E8.A3.85.EF.BC.9A.E5.AE.9A.E5.88.B6.E5.86.85.E6.A0.B8 "NVIDIA (简体中文)").