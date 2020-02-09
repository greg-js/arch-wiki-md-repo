相关文章

*   [VirtualBox/Tips and tricks](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks")
*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")
*   [RemoteBox](/index.php/RemoteBox "RemoteBox")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

**翻译状态：** 本文是英文页面 [VirtualBox](/index.php/VirtualBox "VirtualBox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2020-02-04，点击[这里](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=491411)可以查看翻译后英文页面的改动。

**VirtualBox** 是运行于现有操作系统之上的虚拟机监视器，用途是在特制环境（即虚拟机）里运行操作系统。VirtualBox 处于活跃开发状态，时常会引入新功能。VirtualBox 支持 [Qt](/index.php/Qt "Qt")，[SDL](https://en.wikipedia.org/wiki/SDL "wikipedia:SDL") 与无界面模式运行虚拟机。也支持用 Qt 图形界面和命令行工具管理虚拟机。

为了实现某些主体-客体系统间的整合功能，例如共享目录与剪贴板、显卡加速渲染、无缝窗口整合，VirtualBox 需要在某些系统中安装客体机插件（Guest Addition）。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 在 Arch 里安装 VirtualBox](#在_Arch_里安装_VirtualBox)
    *   [1.1 安装基本软件包](#安装基本软件包)
    *   [1.2 模块签名](#模块签名)
    *   [1.3 加载 VirtualBox 内核模块](#加载_VirtualBox_内核模块)
    *   [1.4 从客体系统访问主机 USB 设备](#从客体系统访问主机_USB_设备)
    *   [1.5 客体机插件光盘](#客体机插件光盘)
    *   [1.6 扩展包](#扩展包)
    *   [1.7 使用正确的前端](#使用正确的前端)
*   [2 在 VirtualBox 中安装 Archlinux](#在_VirtualBox_中安装_Archlinux)
    *   [2.1 以 EFI 模式安装](#以_EFI_模式安装)
    *   [2.2 安装客体机插件](#安装客体机插件)
    *   [2.3 加载 VirtualBox 内核模块](#加载_VirtualBox_内核模块_2)
    *   [2.4 启动 VirtualBox 客体机服务](#启动_VirtualBox_客体机服务)
    *   [2.5 显卡加速](#显卡加速)
    *   [2.6 启用共享目录](#启用共享目录)
        *   [2.6.1 手动挂载](#手动挂载)
        *   [2.6.2 自动挂载](#自动挂载)
        *   [2.6.3 按配置于启动时挂载](#按配置于启动时挂载)
    *   [2.7 从宿主机 SSH 登录客体机](#从宿主机_SSH_登录客体机)
        *   [2.7.1 用 SSHFS 来实现共享目录](#用_SSHFS_来实现共享目录)
*   [3 虚拟磁盘管理](#虚拟磁盘管理)
    *   [3.1 VirtualBox 支持的格式](#VirtualBox_支持的格式)
    *   [3.2 转换虚拟磁盘文件格式](#转换虚拟磁盘文件格式)
        *   [3.2.1 QCOW](#QCOW)
    *   [3.3 在宿主机直接挂载并读写虚拟磁盘镜像](#在宿主机直接挂载并读写虚拟磁盘镜像)
        *   [3.3.1 VDI](#VDI)
    *   [3.4 压紧虚拟磁盘](#压紧虚拟磁盘)
    *   [3.5 扩充虚拟硬盘容量](#扩充虚拟硬盘容量)
        *   [3.5.1 一般方法](#一般方法)
        *   [3.5.2 VDI 格式的方法](#VDI_格式的方法)
    *   [3.6 修改 .vbox 文件来替换磁盘镜像](#修改_.vbox_文件来替换磁盘镜像)
        *   [3.6.1 将虚拟机从 Linux 宿主系统迁移到其他系统（或迁回）](#将虚拟机从_Linux_宿主系统迁移到其他系统（或迁回）)
    *   [3.7 复制虚拟盘并为其分配新 UUID](#复制虚拟盘并为其分配新_UUID)
*   [4 使用技巧](#使用技巧)
*   [5 故障排除](#故障排除)
    *   [5.1 鼠标键盘都锁死在虚拟机里了](#鼠标键盘都锁死在虚拟机里了)
    *   [5.2 无法新建 64 位虚拟机](#无法新建_64_位虚拟机)
    *   [5.3 VirtualBox 图形管理界面和主机 GTK 主题样式不匹配](#VirtualBox_图形管理界面和主机_GTK_主题样式不匹配)
    *   [5.4 无法向虚拟机键入 Ctrl+Alt+Fn](#无法向虚拟机键入_Ctrl+Alt+Fn)
    *   [5.5 USB 功能不可用](#USB_功能不可用)
    *   [5.6 USB 调制解调器在宿主系统不可用](#USB_调制解调器在宿主系统不可用)
    *   [5.7 让虚拟机使用串口](#让虚拟机使用串口)
    *   [5.8 重启 Xorg 之后虚拟机卡死](#重启_Xorg_之后虚拟机卡死)
    *   [5.9 全屏模式只能看到黑屏](#全屏模式只能看到黑屏)
    *   [5.10 虚拟机启动时宿主系统卡死](#虚拟机启动时宿主系统卡死)
    *   [5.11 Linux 客体机的声音缓慢 / 扭曲](#Linux_客体机的声音缓慢_/_扭曲)
    *   [5.12 模拟信号麦克风不可用](#模拟信号麦克风不可用)
    *   [5.13 版本更新之后麦克风不能用](#版本更新之后麦克风不能用)
    *   [5.14 转换得来的 ISO 文件出现问题](#转换得来的_ISO_文件出现问题)
    *   [5.15 Host-only 网卡创建失败](#Host-only_网卡创建失败)
    *   [5.16 插入模块失败](#插入模块失败)
    *   [5.17 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_(0x80BB0007))
    *   [5.18 NS_ERROR_FAILURE 且菜单项缺失](#NS_ERROR_FAILURE_且菜单项缺失)
    *   [5.19 Arch: pacstrap 脚本出错](#Arch:_pacstrap_脚本出错)
    *   [5.20 缺少硬件虚拟化导致 OpenBSD 不稳定](#缺少硬件虚拟化导致_OpenBSD_不稳定)
    *   [5.21 Windows 宿主机: VERR_ACCESS_DENIED](#Windows_宿主机:_VERR_ACCESS_DENIED)
    *   [5.22 Windows: "The specified path does not exist. Check the path and then try again."](#Windows:_"The_specified_path_does_not_exist._Check_the_path_and_then_try_again.")
    *   [5.23 Windows 8.x 出现错误代码 0x000000C4](#Windows_8.x_出现错误代码_0x000000C4)
    *   [5.24 Windows 8, 8.1 或 10 无法安装、启动或报错 "ERR_DISK_FULL"](#Windows_8,_8.1_或_10_无法安装、启动或报错_"ERR_DISK_FULL")
    *   [5.25 WinXP: 颜色深度不得多于 16 位](#WinXP:_颜色深度不得多于_16_位)
    *   [5.26 Windows: 开启3D加速后屏幕闪烁](#Windows:_开启3D加速后屏幕闪烁)
    *   [5.27 Arch Linux guest虚拟机中没有硬件3D加速](#Arch_Linux_guest虚拟机中没有硬件3D加速)
    *   [5.28 无法在Wayland上启动VirtualBox：段错误](#无法在Wayland上启动VirtualBox：段错误)
*   [6 已知问题](#已知问题)
    *   [6.1 自动挂载不起作用](#自动挂载不起作用)
    *   [6.2 缺少 vboximg-mount](#缺少_vboximg-mount)
*   [7 参阅](#参阅)

## 在 Arch 里安装 VirtualBox

以下步骤可以帮你在 Arch 主体系统里安装 VirtualBox

### 安装基本软件包

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [virtualbox](https://www.archlinux.org/packages/?name=virtualbox)。内核模块的安装方式要从下面二选一：

*   如果在用默认的 [linux](https://www.archlinux.org/packages/?name=linux) 内核，建议安装 [virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch)
*   如果用了其它的内核，需要安装 [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)

为了能基于 [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) 编译内核模块，你还要安装与内核对应的内核头文件（例如[linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 内核的头文件是 [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers)）。[[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) 当 VirtualBox 或内核更新的时候，DKMS 的 Pacman 钩子会自动编译内核模块。

### 模块签名

如果你的 Linux 内核是自行编译的，并启用了 `CONFIG_MODULE_SIG_FORCE` 选项，那么你需要用编译内核时所使用的密钥为所有模块签名。

进入内核源码目录，执行下面的命令：

```
# for module in `ls /lib/modules/$(uname -r)/kernel/misc/{vboxdrv.ko,vboxnetadp.ko,vboxnetflt.ko,vboxpci.ko}` ; do ./scripts/sign-file sha1 certs/signing_key.pem certs/signing_key.x509 $module ; done

```

**注意:** 哈系算法不必与配置时选择的算法相匹配，但必须被编译进内核。

### 加载 VirtualBox 内核模块

从版本 5.0.16 开始，[virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch) 和 [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) 使用 `systemd-modules-load.service` 在启动时自动加载 VirtualBox 的四个内核模块。若要在安装之后就加载模块，可以手动加载一次，或者干脆重启。

**注意:** 如果希望启动时不自动加载 VirtualBox 模块，需要将默认的 `/usr/lib/modules-load.d/virtualbox-host-modules-arch.conf` (或 `-dkms.conf`) 配置文件屏蔽掉。具体做法是：在 `/etc/modules-load.d` 目录里创建同名的空文件。

在 VirtualBox 所使用的 [内核模块](/index.php/Kernel_modules "Kernel modules") 中，只有 `vboxdrv` 是必须的。该模块必须在虚拟机运行之前加载。

手动加载模块的命令是：

```
# modprobe vboxdrv

```

以下模块不是必需的，但如果你不想在使用高级功能（见下）时再操心，建议都加载上。

*   `vboxnetadp` 和 `vboxnetflt`：这两个模块在使用[桥接网络](https://www.virtualbox.org/manual/ch06.html#network_bridged)和[host-only 网络](https://www.virtualbox.org/manual/ch06.html#network_hostonly)功能时，都是需要的。具体来说，`vboxnetadp` 模块用于在 VirtualBox 全局配置里为主体机创建虚拟网卡；`vboxnetflt` 模块会在使用了该功能的客体机启动时起作用。

*   `vboxpci`：若要让虚拟机使用主体机的 PCI 设备，那么就需要这个模块。

**注意:** 如果在 VirtualBox 内核模块运行期间你更新了模块（所属的软件包），为了使用新版本，你需要手动重新加载这些模块。在 root 权限下运行 `vboxreload` 即可重新加载。

最后，如果你要使用前面提到的 "Host-only 网络" 或是桥接网络功能，请确保 [net-tools](https://www.archlinux.org/packages/?name=net-tools) 已经安装。当VirtualBox 通过 `VBoxManage hostonlyif` 命令或是 GUI 的 *Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter* 选项来配置网络功能时，背后都会调用 `ifconfig` 和 `route` 命令，来为宿主机的虚拟网卡完成 IP 与路由的配置。

### 从客体系统访问主机 USB 设备

将需要运行 VirtualBox 的用户名添加到 `vboxusers` [用户组](/index.php/User_group "User group")，USB 设备才能被访问。

### 客体机插件光盘

建议在运行 VirtualBox 的主机系统上安装 [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) 软件包。这个包里有个 `.iso` 镜像文件，用来为 Arch 之外的客体系统安装插件。镜像文件的位置在 `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`，手动在虚拟机的虚拟光驱里加载这个文件之后，即可在客体机里安装插件。

### 扩展包

Oracle Extension Pack 为虚拟机提供了[额外功能](https://www.virtualbox.org/manual/ch01.html#intro-installing)。但它并不是以自由软件协议发布的，*仅供个人使用*。这些扩展包可以从 [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) 安装，从 [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories") 仓库可以安装编译好的版本。

如果你喜欢使用传统的手动方法来安装扩展包：通过 GUI 下载并安装 (*File > Preferences > Extensions*) 或着手动下载后用 `VBoxManage extpack install <.vbox-extpack>` 命令来安装。你需要某种方式（例如 [Polkit](/index.php/Polkit "Polkit")，gksu 等等）在安装时为 VirtualBox 授予 [root 权限](https://www.virtualbox.org/ticket/8473)。

### 使用正确的前端

VirtualBox 自带三个前端：

*   如果你想通过常规 GUI 使用 VirtualBox，使用 `VirtualBox` 命令来启动 VirtualBox。
*   如果你想在命令行下启动与管理 VirtualBox，可以使用 `VBoxSDL` 命令。从 VBoxSDL 启动的虚拟机，其窗口仅包含虚拟机的画面，没有菜单或是其他控制项。
*   如果你想使用不想由任何 GUI（例如在服务器上）来使用 VirtualBox，使用 `VBoxHeadless` 命令。如果还想登录到这种虚拟机的图形界面，就需要安装 VRDP 扩展。

如果你想通过 web 界面来管理虚拟机，可以安装 [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")。

若要了解如何创建虚拟机，可以查阅 [VirtualBox 手册](https://www.virtualbox.org/manual)。

**Warning:** 如果你想把在虚拟机的硬盘镜像放到 [Btrfs](/index.php/Btrfs "Btrfs") 文件系统上，在创建镜像之前，你应该考虑为镜像所处的文件夹关闭[写时复制](/index.php/Btrfs#Copy-on-Write_(CoW) "Btrfs")。

## 在 VirtualBox 中安装 Archlinux

简单来说，在虚拟机的虚拟光驱里加载 Arch Linux 的[安装镜像](https://www.archlinux.org/download/)，然后按照[安装指南](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")里的步骤继续即可。

### 以 EFI 模式安装

如果你想在 VirtualBox 里以 EFI 模式安装 Arch Linux，这需要在虚拟机的设置窗口里，先从左侧选择 *System*，再从右侧选择 *Motherboard* 标签页，最后勾选 *Enable EFI (special OSes only)* 选项。从安装镜像的启动菜单里选好 Arch Linux 的内核之后，这时启动过程要卡顿一两分钟，之后就能正常进入系统。稍安勿躁。

等系统和[启动引导程序](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")安装成功之后，VirtualBox 会首先尝试从 [ESP](/index.php/ESP "ESP") 加载 `/EFI/BOOT/BOOTX64.EFI`。如果这个首选的文件加载失败，VirtualBox 会从 ESP 根目录尝试加载 EFI shell 脚本 `startup.nsh`。这样来说，为了能顺利进入系统，你需要从下面几种方案选一个：

*   每次都从 EFI shell [手动选择启动引导程序](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface")
*   把启动引导程序的 .EFI 文件移动到默认位置：`/EFI/BOOT/BOOTX64.EFI`
*   自己编写 ESP 分区的 `/startup.nsh` 脚本，用这个脚本加载想使用的引导程序（例如 `\EFI\grub\grubx64.efi`）
*   从 ESP 分区的 [startup.nsh 脚本](/index.php/EFISTUB#Using_a_startup.nsh_script "EFISTUB")直接启动到 Linux

虽然 VirtualBox 支持按 F2 进入自带的 VirtualBox Boot Manager 来管理 EFI 启动过程，但这部分功能还不完整而且有 bug。它还不能持久保存交互式设置的 EFI 变量。也就是说，开机时按下 F12 之后手动添加的、或者用 [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) 添加的 EFI 项目，重启后依然可以生效，但关机之后就会失效。

另见：[UEFI VirtualBox installation boot problems](https://bbs.archlinux.org/viewtopic.php?id=158003).

### 安装客体机插件

VirtualBox [客体机插件](https://www.virtualbox.org/manual/ch04.html) 为客体系统提供了必要的驱动与应用软件，其作用包括改善图像分辨率与鼠标支持等。在客体机的 Arch Linux 系统里：

*   若需要支持 X，安装 [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) 这个包
*   若不需支持 X，安装 [virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox)

安装这两个包都会询问你希望如何对应安装客体机插件所需的内核模块：

*   若使用了默认的 [linux](https://www.archlinux.org/packages/?name=linux) 内核，安装 [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch) 这个包
*   若使用其他内核，需要安装 [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms)

为了安装由 [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) 提供的内核模块，还需要给你所使用的内核安装相应的包来提供内核头文件。（例如 [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 内核需要配套安装 [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers)）。[[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) 这样，无论内核还是 VirtualBox 有更新， [DKMS](/index.php/DKMS "DKMS") 的Pacman 钩子程序都会自动编译好内核模块。

**注意:**

*   另一个安装方案是从宿主机（如果也是 Arch 系统）安装 [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso)，这个软件包里有供客体机安装插件的 ISO 文件。装好这个包之后，启动客体机，点击菜单项目 Devices -> Insert Guest Additions CD Image 即可加载安装镜像。
*   若要手动重新编译客体机的 VirtualBox 内核模块，以 root 权限运行 `rcvboxdrv` 即可。

客体机里运行的插件和主体机上的 VirtualBox 程序版本需要匹配。否则某些功能（比如剪贴板互通）可能会失效。如果你在客体机里升级系统（比如运行了 `pacman -Syu`），那么宿主机上的 VirtualBox 也要跟进更新到最新版。VirtualBox GUI 菜单里的 "Check for updates" 功能未必够用，可以去官网 virtualbox.org 再看看。

### 加载 VirtualBox 内核模块

若要开机自动加载模块，[启用](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") `vboxservice.service` 服务即可。该服务还能起到将客户机时间与宿主机同步的功能。

若要手动加载模块，使用这个命令：

```
# modprobe -a vboxguest vboxsf vboxvideo

```

自从 5.0.16 版本起，[virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch) 与 [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) 都能利用 `systemd-modules-load.service` 服务来在开机时自动加载各自提供的模块。

**注意:**

如果你希望开机时不要加载 VirtualBox 模块，办法是将配置文件 `/usr/lib/modules-load.d/virtualbox-guest-modules-arch.conf` (或是 `-dkms.conf`，如果安装了 [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms)) 屏蔽掉。具体的操作是：在 `/etc/modules-load.d` 目录里创建一个同文件名的空文件。例如：

```
# touch /etc/modules-load.d/virtualbox-guest-modules-arch.conf

```

### 启动 VirtualBox 客体机服务

安装并加载了 VirtualBox 内核模块之后，如果你在虚拟机系统里使用 [X](/index.php/Xorg "Xorg")，那么推荐启动这样一个客体机服务：服务的程序名字叫 `VBoxClient`，它与 X 窗口系统沟通来实现其功能。具体功能包括：

*   在宿主机与客体机之间互通剪贴板，实现鼠标拖拽文件
*   无缝窗口模式
*   宿主机的虚拟机窗口缩放之后，使客体机的显示分辨率与之自动匹配
*   检查宿主机的 VirtualBox 的版本

上述功能由专门的命令行参数来各自启用：

```
$ VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

```

为了方便，`VBoxClient-all` 这个 shell 脚本能取代上面这一整行命令。

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) 包提供了 XDG 自启动项目 `/etc/xdg/autostart/vboxclient.desktop`，这会在登录 X 时自动运行 `VBoxClient-all`。然而，如果你在用的[桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")或[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")不支持 XDG 自启动，那么你就需要手动配置。详见 [Autostarting (简体中文)#图形程序](/index.php/Autostarting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#图形程序 "Autostarting (简体中文)")。

至此，你的 Arch Linux 应该能在虚拟机里正常运行了。需要指出的是，某些功能（如剪贴板互通）在 VirtualBox 里是默认禁用的。这需要在各个虚拟机的设置选项里手动开启（*Settings > General > Advanced > Shared Clipboard*）。

### 显卡加速

从 VirtualBox 选项里可以开启显卡加速。已知 [GDM](/index.php/GDM "GDM") 显示管理器从 3.16 版本起会导致显卡加速失效。[[3]](https://bugzilla.gnome.org/show_bug.cgi?id=749390) 如果你遇到类似问题，可以换另一种显示管理器（比如 [LightDM](/index.php/LightDM "LightDM")）试试看。[[4]](https://bbs.archlinux.org/viewtopic.php?id=200025) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1607593#p1607593)

### 启用共享目录

共享目录的设置在宿主机这边操作。启动 VirtualBox 的图形管理界面，在虚拟机的设置界面的 *Shared Folders* 标签页可以找到相关设置。可以设置的项目包括：目录在宿主机的位置 *Folder Path*，客户机挂载点的名字 *Folder name*，还有 *Read-only*，*Auto-mount*, *Make permanent* 等杂项。还有一种管理方法是使用 `VBoxManage`。详情可以参阅 [VirtualBox 手册](https://www.virtualbox.org/manual/ch04.html#sharedfolders)。

无论用哪一种方法来挂载共享目录，首先都要做些准备工作。

为了避免出现 `/sbin/mount.vboxsf: mounting failed with the error: No such device` 这种错误，首先要确保 `vboxsf` 内核模块已经加载。只要按照前面的步骤在加载客体机里加载内核模块，这一步应该没问题。

为了让挂载之后的目录能让 root 之外的用户也直接读写，还要：

*   安装 [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) 软件包时会创建用户组 `vboxsf`（在前面的步骤就装过了）
*   你的用户需要加入到 `vboxsf` [用户组](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#用户组管理 "Users and groups (简体中文)")

#### 手动挂载

在 Arch Linux 客体系统里挂载共享目录的命令是：

```
# mount -t vboxsf *<共享目录的名字>* *<客户机系统的挂载点>*

```

这个命令可以查看 vboxsf 的挂载参数：

```
# mount.vboxsf

```

假如用户不在 `vboxsf` 组里，用这个命令可以把挂载点的读写权限授权给他：

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt/

```

其中 *uid* 和 *gid* 的值要与接受授权的用户的值相对应。用 `id` 命令可以为该用户找到这两个值。

#### 自动挂载

**注意:** 自动挂载需要启用 `vboxservice` 服务才能生效

为使用自动挂载功能，首先需要在 GUI 的管理界面里勾选自动挂载，或者为命令行工具 `VBoxManage sharedfolder` 加上参数 `--automount`。

此时，共享目录应该已经在 `/media/sf_*<共享目录的名字>*` 挂载上了。如果用户没有读写权限，确认一下该目录的权限是否是 755。如果是 750 的话，确保该目录属于 `vboxsf` 组。

可以用软链接把共享目录链接到方便的位置，这样就不必进入那么远的目录了：

```
$ ln -s /media/sf_*共享目录的名字* ~/*my_documents*

```

#### 按配置于启动时挂载

[fstab](/index.php/Fstab "Fstab") 可以用来挂载目录。然而，为了避免 Systemd 启动可能带来的问题，要在 `/etc/fstab` 配置里为共享目录加上挂载选项 `noauto,x-systemd.automount`。这样，共享目录会在开机后初次访问时挂载，而不是在系统启动过程里挂载。这可以避免 Systemd 在客体机插件加载之前就按 fstab 挂载目录而导致的出错。

```
*sharedFolderName*  */path/to/mntPtOnGuestMachine*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,noauto,x-systemd.automount 

```

*   `*sharedFolderName*`: 在虚拟机设置界面 *Settings > SharedFolders > Edit > FolderName* 里所设置的值。这个值和宿主机里实际的目录名可以不相同。要查看虚拟机的设置，在宿主机的 VirtualBox GUI 管理界面选中虚拟机，然后点击工具栏的 *Settings* 按钮，再从弹出的对话框里选择 *Shared Folders*。
*   `*/path/to/mntPtOnGuestMachine*`: 如果这个路径在虚拟机里还不存在，那么需要在挂载之前手动创建（用 [mkdir](/index.php/Core_utilities#mkdir "Core utilities") 就可以）。
*   `dmode`/`fmode` 分别用来指定挂载共享目录之后，下面的子目录与文件的属性。

`mount.vboxsf` 尚不支持 `nofail` 挂载参数：

```
*desktop*  */media/desktop*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,nofail  0  0

```

### 从宿主机 SSH 登录客体机

在虚拟机设置的 Network 标签页 -> 右侧打开 Advanced 折叠 -> 单击 Port Forwarding 按钮，可以设置端口。

假如我们设置了将宿主机的 3022 端口转发到客体机的 22 端口。然后在宿主机执行：

```
user@host$ ssh -p 3022 $USER@localhost

```

即可 SSH 登录客体机。

#### 用 SSHFS 来实现共享目录

配置好了端口转发，再装上 [SSHFS](/index.php/SSHFS "SSHFS")，只要在宿主机运行这个命令就可以把客体机的目录挂载到宿主机：

```
user@host$ sshfs -p 3022 $USER@localhost:$HOME ~/shared_folder

```

这样也能实现互传文件。

## 虚拟磁盘管理

### VirtualBox 支持的格式

VirtualBox 支持下列虚拟磁盘格式：

*   **VDI**: Virtual Disk Image 格式是 VirtualBox 新建虚拟机时默认选用的格式。也是 VirtualBox 的自有开放格式。

*   **VMDK**: Virtual Machine Disk 最初是由 VMware 为其产品研发的格式。该格式技术设计文档最初是闭源的，而现在已经开源，在 VirtualBox 里完全可用。这种格式有个功能是：把一个虚拟机的镜像分割成多个 2GB 大小的文件。如果你要把虚拟机镜像放在不支持大文件的文件系统（例如 FAT32）上，那么这个功能就非常有用。在其他的虚拟磁盘格式里，能做到同样功能的只有 Parallels 的 HDD。

*   **VHD**: Virtual Hard Disk 是 Microsoft 为 Windows Virtual PC 与 Hyper-V 研发的格式。如果你想把虚拟机部署到这些平台上，那么你只能用这种格式。

**Tip:** Windows 7 开始可以直接把 VHD 文件挂载成虚拟盘进行读写。而不需要额外安装软件。

*   **VHDX** (只读): 这是由 Microsoft 研发的 Virtual Hard Disk 格式的加强版。于 2012-09-04 与 Hyper-V 3.0 同步发布，二者都是 Windows Server 2012 的功能。该加强版的改进包括性能优化（源于区块对齐），支持大区块单位，还有应对断电的磁盘日志。VirtualBox [支持该格式的只读访问](https://www.virtualbox.org/manual/ch15.html#idp63002176)。

*   **HDD** (V2): HDD 格式是由 Parallels Inc 研发的，由他们的虚拟机方案（如 Parallels Desktop for Mac）所使用。该格式的新版（v3 和 v4）由于缺少文档，又是专有格式，未能被 VirtualBox 支持。

**注意:** 关于该格式“仅支持 V2 版”的说法目前有争议。VirtualBox 官方手册 [声称只支持 V2 版](https://www.virtualbox.org/manual/ch05.html#vdidetails)，但 Wikipedia 上的说法是 [V1 版也能正常工作](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines")。如果你能为 V1 的支持状况做测试验证，非常欢迎。

*   **QED**: QEMU Enhanced Disk 是旧版 QEMU 使用的格式。QEMU 也是一个开源免费的虚拟机方案。该格式于 2010 年设计出来，目的是要比 QCOW2 等格式更优秀。这种格式支持的功能包括全异步 I/O，数据高度完整性，文件备份，稀疏文件。VirtualBox 支持 QED 格式只是为了兼容由旧版 QEMU 创建的虚拟机。

*   **QCOW**: QEMU Copy On Write 是 QEMU 现有版本支持的格式。QCOW 支持基于 zlib 实现的透明压缩与加密（加密功能有缺陷，不推荐使用）。QCOW 包括两个版本：QCOW 与 QCOW2。QCOW2 取代了旧版。[VirtualBox 完全支持旧版 QCOW](https://www.virtualbox.org/manual/ch15.html#idp63002176)。QCOW2 包含两个修订版：QCOW2 0.10 和 QCOW2 1.1（QEMU 新建的虚拟机默认使用 1.1）。然而 VirtualBox 并不支持 QCOW2。

*   **OVF**: Open Virtualization Format 是为了在让虚拟机在不同监视器方案间得到通用而设计的开放方案。VirtualBox 支持该格式的所有修订版，具体的支持方式是 [VBoxManage import/export 命令](https://www.virtualbox.org/manual/ch08.html#idp55423424)，但也有[部分功能受限](https://www.virtualbox.org/manual/ch14.html#KnownProblems)。

*   **RAW**: 虚拟磁盘可以不以任何文件格式封装，而直接以这种 RAW 模式供虚拟机使用。VirtualBox 对此有多种支持方案：将 RAW 磁盘 [转换成上述某种格式](https://www.virtualbox.org/manual/ch08.html#idp59139136)；[将物理盘转换成 RAW 格式](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi)；直接挂载一个[指向物理盘或 RAW 格式文件](https://www.virtualbox.org/manual/ch09.html#idp57804112)的 VMDK 文件。

### 转换虚拟磁盘文件格式

[VBoxManage clonehd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) 这个命令可以实现 VDI, VMDK, VHD 与 RAW 格式间的互转

```
$ VBoxManage clonehd *inputfile* *outputfile* --format *outputformat*

```

以 VDI 转成 VMDK 为例：

```
$ VBoxManage clonehd *source.vdi* *destination.vmdk* --format VMDK

```

#### QCOW

VirtualBox 不支持 [QEMU](/index.php/QEMU "QEMU") 的 QCOW2 格式。若要让 VirtualBox 使用 QCOW2 格式的文件，你只能将其转换成已支持的格式。用 [qemu](https://www.archlinux.org/packages/?name=qemu) 包提供的 `qemu-img` 程序可以做到。`qemu-img` 可以实现 QCOW 格式与 VDI, VMDK, VHDX, RAW 等其他格式间的互转。具体支持的格式可以通过运行 `qemu-img --help` 命令查看。

该命令的一般形式是：

```
$ qemu-img convert -O *output_fmt* *inputfile* *outputfile*

```

以 QCOW2 转成 VDI 为例：

```
$ qemu-img convert -O vdi *source.qcow2* *destination.vdi*

```

**Tip:** 转换时加上 `-p` 参数可以实时查看转换进度

QCOW2 有两个修订版： 0.10 和 1.1，用 `-o compat=*revision*` 参数可以具体指定。

### 在宿主机直接挂载并读写虚拟磁盘镜像

#### VDI

固定大小的 VDI 镜像（又名静态镜像）可以直接在宿主机挂载。动态镜像则没法轻松挂载。

首先要拿到 VDI 里数据分区的偏移量 `offData`：

```
$ VBoxManage internalcommands dumphdinfo <storage.vdi> | grep "offData"

```

然后再加上 `32256` (例如 69632 + 32256 = 101888)，那么就用这个命令来挂载：

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <storage.vdi> /mntpoint/

```

另一个办法是用 [mount.vdi](https://github.com/pld-linux/VirtualBox/blob/master/mount.vdi) 脚本来完成挂载。首先要把脚本安装到 `/usr/bin/`，然后：

```
# mount -t vdi -o fstype=ext4,rw,noatime,noexec *vdi_file_location* */mnt/*

```

还有一个办法是用 [qemu](https://www.archlinux.org/packages/?name=qemu) 的内核模块来实现[[6]](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/)：

```
# modprobe nbd max_part=16
# qemu-nbd -c /dev/nbd0 <storage.vdi>
# mount /dev/nbd0p1 /mnt/dir/
# # to unmount:
# umount /mnt/dir/
# qemu-nbd -d /dev/nbd0

```

如果未能生成分区节点，试试运行命令：`partprobe /dev/nbd0`。另外，VDI 分区还可以直接用这个命令来映射到节点：`qemu-nbd -P 1 -c /dev/nbd0 <storage.vdi>`。

### 压紧虚拟磁盘

只有 `.vdi` 格式的虚拟磁盘文件可以压紧。具体操作步骤如下。

启动虚拟机，手动删除无用文件，或者用自动的清理工具（如 [bleachbit](https://www.archlinux.org/packages/?name=bleachbit)，同时也支持 [Windows](http://bleachbit.sourceforge.net/download/windows)）来清理磁盘。

下一步要用零字节来填充可用空间。这有如下的可行方案：

*   如果你已经在用 Bleachbit 了，在 GUI 菜单里选择 *System > Free disk space*，或者在命令行执行：`bleachbit -c system.free_disk_space`；
*   在类 UNIX 系统里，`dd` 或 [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) 都可以做到，后者更推荐。（参阅 [这里](http://superuser.com/a/355322)来了解两者的区别）；

	 `# dcfldd if=/dev/zero of=*/fillfile* bs=4M` 

	当 `fillfile` 文件的体积占满分区时，会出现这样的错误信息：`1280 blocks (5120Mb) written.dcfldd:: No space left on device`。这意味着所有的可用空间与未保留区块都已经被零字节填满了。因为 ext 类系统会为 root 用户默认保留一部分硬盘空间（见 `mkfs.ext4` 手册页对 `-m` 参数的解释，或者用 `tune2fs -l` 命令来查看具体为 root 保留了多少空间），所以运行这一命令时需要有 root 权限。

	前面一步操作完成后，手动把 `*fillfile*` 删掉。

*   在 Windows 系统里有两种办法：

*   由 [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx) 提供的 `sdelete` 命令，用法是 `sdelete -s -z *c:*`。在虚拟机里的每一个分区都要执行一遍（当然 *c:* 这个参数要对应地改成各个分区的盼覆）；
*   如果你喜欢脚本，可以用这个 [PowerShell 实现的方案](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html)，但依然要每个分区执行一次。

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**注意:** 该脚本需要在有管理员权限的 PowerShell 环境才能运行。默认的 PowerShell 默认配置下，这个脚本无法运行。需要把秩序策略至少调整到 `RemoteSigned`，而不能是 `Restricted`。用 `Get-ExecutionPolicy` 命令可以看到当前的执行策略，用 `Set-ExecutionPolicy RemoteSigned` 可以设置想要的执行策略。

完成这一步之后，将虚拟机停机。

下一次启动虚拟机时，推荐先进行文件系统检查：

*   在类 UNIX 系统上可以手动运行 `fsck` 来检查；

*   在 GNU/Linux 系统上（包括 Arch）可以在系统启动时强行执行硬盘检查。详见 [thanks to a kernel boot parameter](/index.php/Fsck#Forcing_the_check "Fsck")；

*   在 Windows 系统上：

*   可以用这个命令 `chkdsk *c:* /F`。其中 `*c:*` 可以替换成所有你希望检查的盘符；
*   或者从 [这里下载](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx) `FsckDskAll`。这和前面的 `chkdsk` 基本一样，只是不必手动为每个分区执行一遍了。

接下来用 [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi) 即可完成压紧过程：

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**注意:** 如果你的虚拟机有保存过快照，那么每个 `.vdi` 文件都要单独执行一遍压紧操作。

### 扩充虚拟硬盘容量

#### 一般方法

如果你在创建虚拟机时给虚拟硬盘分配的容量太小了，VirtualBox 推荐的扩容方案是用 [VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi) 这个命令。然而这个命令只支持 VDI 和 VHD 这两种格式，而且还需要设置成动态分配容量。如果你想为固定容量的虚拟磁盘扩容，下面的办法可以适用于 Windows 或类 UNIX 系统的虚拟机。

首先创建一个新的虚拟磁盘：

```
$ VBoxManage createhd -filename *new.vdi* --size *10000*

```

`--size` 参数的值的单位是 MiB，在例子里 10000 MiB ~= 10 GiB，`new.vdi` 是新创建的镜像文件。

**Note:** 由这个命令创建的镜像文件默认是动态分配空间的。如果想让新镜像和旧镜像一样固定空间，需要追加参数 `--variant Fixed`。

接下来要把旧镜像的内容复制到新镜像里去，这一步骤可能会花些时间：

```
$ VBoxManage clonehd *old.vdi* *new.vdi* --existing

```

取下旧硬盘镜像，挂载新镜像，下面命令中的斜体字部分需要按照你的使用环境来换成真实的值：

```
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium *new.vdi* --type hdd

```

在上面的命令中，若要获知储存控制器的名字与端口号，可以使用命令：`VBoxManage showvminfo *VM_name*`。这会打印出如下的输出（斜体标注的信息是有用的）：

```
[...]
Storage Controller Name (0):            IDE
Storage Controller Type (0):            PIIX4
Storage Controller Instance Number (0): 0
Storage Controller Max Port Count (0):  2
Storage Controller Port Count (0):      2
Storage Controller Bootable (0):        on
Storage Controller Name (1):            SATA
Storage Controller Type (1):            IntelAhci
Storage Controller Instance Number (1): 0
Storage Controller Max Port Count (1):  30
Storage Controller Port Count (1):      1
Storage Controller Bootable (1):        on
IDE (1, 0): Empty
*SATA* (*0*, 0): /home/wget/IT/Virtual_machines/GNU_Linux_distributions/ArchLinux_x64_EFI/Snapshots/{6bb17af7-e8a2-4bbf-baac-fbba05ebd704}.vdi (UUID: 6bb17af7-e8a2-4bbf-baac-fbba05ebd704)
[...]
```

下载 [GParted Live 可引导镜像](http://gparted.org/download.php)，在虚拟机里用虚拟光驱加载之，启动虚拟机，调整分区大小 / 位置，取下镜像并重启。这样扩容就完成了。

**注意:** 如果虚拟盘用了 GPT 分区表，扩容会导致 GPT 备份头不再位于磁盘末尾。GParted 会询问是否要将其修复，此时两次询问都要点 *Fix*。如果是 MBR 分区，就不存在这一问题。

最后，从 VirtualBox 里注销旧的镜像文件，并删除掉：

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

#### VDI 格式的方法

如果你的虚拟磁盘是 VDI 格式的：

```
$ VBoxManage modifyhd *your_virtual_disk.vdi* --resize *the_new_size*

```

然后回到上面的 Gparted 步骤，继续完成扩容操作。

### 修改 .vbox 文件来替换磁盘镜像

如果相比用 GUI 或 `VBoxManage` 来管理虚拟机，你觉得编辑 XML 文件更加简单直接。按下面的步骤修改虚拟机对应的 .vbox 文件，即可完成虚拟机的磁盘替换：

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

找到 `<StorageController>` 的子元素 `<AttachedDevice>`，把 GUID 属性改成新镜像文件的值：

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**注意:** 如果你还不知道新镜像文件的 GUID 值，可以用命令 `VBoxManage showhdinfo *file*` 来查看。如果你用 `VBoxManage clonehd` 命令来处理过虚拟盘，那么在复制 / 转换过程完成时，也会打印出 GUID 值。随便写一个 GUID 上去是不行的，必须与 [镜像文件里的 GUID 值](http://www.virtualbox.org/manual/ch05.html#cloningvdis)相对应才行。

#### 将虚拟机从 Linux 宿主系统迁移到其他系统（或迁回）

.vbox 配置文件把虚拟盘和快照文件的位置记录在 `<HardDisks> .... </HardDisks>` 标签里。如果新宿主系统存放虚拟机文件的路径与旧宿主系统不同，你可以手动修改 .vbox 文件来调整路径。如果 .vbox 文件与虚拟盘 / 快照文件位于相同的目录，也可以用下面的脚本自动修改。该脚本会将修改后的新配置打印到标准输出。

```
#!/bin/bash
NewPath="${PWD}/"
Snapshots="Snapshots/"
Filename="$1"

 awk -v SetPath="$NewPath" -v SnapPath="$Snapshots" '{if(index($0,"<HardDisk uuid=") != 0){A=$3;split(A,B,"=");
L=B[2];
 gsub(/\"/,"",L);
  sub(/^.*\//,"",L);
  sub(/^.*\\/,"",L);
 if(index($3,"{") != 0){SnapS=SnapPath}else{SnapS=""};
  print $1" "$2" location="\"SetPath SnapS L"\" "$4" "$5}
else print $0}' "$Filename"
```

**注意:**

*   如果你想把虚拟机迁移到 Windows 宿主系统上去，文件路径里应该使用 \ 而不是 /。
*   这个脚本判断快照的逻辑是：文件名是否包含 `{`。
*   为了在新宿主机上运行起来，首先得在管理界面注册：点选菜单项 **Machine -> Add...** 或者按快捷键 Ctrl+A ，然后找到 *.vbox* 配置文件。也可以用命令行：`VBoxManage registervm *filename*.vbox`

### 复制虚拟盘并为其分配新 UUID

VirtualBox 广泛应用了 UUID。每个虚拟机，虚拟机的每个虚拟盘，都有属于自己的 UUID。用 [VBoxManage list](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) 命令可以列出 VirtualBox 管理的所有资源。

如果你想复制一台虚拟机，仅复制虚拟盘镜像文件是不够的。你还得给复制出的新镜像文件分配一个新的 UUID。否则在同一个 VirtualBox 的环境里无法同时注册两个具有相同 UUID 的镜像文件。

下面这个命令可以用来为虚拟盘分配新 UUID：

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Tip:** 用 [VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) 可以一次性完成复制内容与分配新 UUID

**注意:** 上述命令可以用于任意 [VirtualBox 所支持的镜像格式](#VirtualBox_支持的格式)。

## 使用技巧

高端使用技巧可以参阅 [VirtualBox/Tips and tricks (简体中文)](/index.php/VirtualBox/Tips_and_tricks_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "VirtualBox/Tips and tricks (简体中文)")。

## 故障排除

### 鼠标键盘都锁死在虚拟机里了

这是因为你的虚拟机捕获了键盘与鼠标的输入。只要按下右 `Ctrl` 键即可让输入焦点回到宿主系统。

如果想要不按切换键就能让鼠标在宿主机与虚拟机之间无缝切换，这需要安装客户机插件。如果你的虚拟机系统是 Arch Linux，可以参阅前面的章节：[#安装客体机插件](#安装客体机插件)。其他系统请参阅 VirtualBox 的官方帮助文档。

### 无法新建 64 位虚拟机

如果新建虚拟机时看不到 64 位系统选项，这需要确认你的 CPU 是否支持虚拟化技术（通常称作 `VT-x`），并且还要在 BIOS 中启用。

如果你的宿主系统是 Windows，那么你得禁用 Hyper-V 功能。因为 Hyper-V 会妨碍 VirtualBox 使用 VT-x。[[7]](https://www.virtualbox.org/ticket/12350)

### VirtualBox 图形管理界面和主机 GTK 主题样式不匹配

VirtualBox 的 GUI 是基于 Qt 实现的。为了修改这类应用的外观，见 [Uniform look for Qt and GTK applications (简体中文)](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform look for Qt and GTK applications (简体中文)")。

### 无法向虚拟机键入 Ctrl+Alt+Fn

如果你在虚拟机安装了某个 Linux 发行版，有时会需要按 `Ctrl+Alt+F2` 进入它的 TTY 界面，或者按 `Ctrl+Alt+Backspace` 来退出 X 会话。如果你的宿主系统也是 Linux，这些组合键默认会首先被宿主系统捕获。正确的做法是按 *Host Key*（默认是右 `Ctrl`）加 `F2` 来向虚拟机键入 `Ctrl+Alt+F2`。

### USB 功能不可用

在宿主系统里使用虚拟机的用户需要加入到 `vboxusers` 用户组。如果想要支持 USB 2 设备，还要安装 [扩展包](#扩展包)。此后在虚拟机的设置里即可开启 USB 2 支持，并且通过过滤规则来允许客体系统访问指定的 USB 设备。

如果用 root 身份运行 `VBoxManage list usbhost` 命令也没有列出任何 USB 设备，需要确认一下 `/etc/udev/rules.d/` 目录里没有遗留的 VirtualBox 4.x 的 udev 规则。VirtualBox 5.0 起会把 udev 规则文件安装到 `/usr/lib/udev/rules.d/` 目录。用 `pacman -Qo /usr/lib/udev/rules.d/60-vboxdrv.rules` 命令可以查看这些 udev 文件是否已经过期。

有时某些旧 Linux 宿主系统无法自动检测到 USB 子系统，就会出现这个错误：`Could not load the Host USB Proxy service: VERR_NOT_FOUND`。或者可能让宿主机也识别不了 USB 磁盘，[哪怕用户已经加入了 `vboxusers` 用户组](https://bbs.archlinux.org/viewtopic.php?id=121377)。出现这类问题的原因是 VirtualBox 从 3.0.8 版本开始，从 *usbfs* 转向使用 *sysfs*。如果宿主系统不支持这一改动，你可以在 shell 的启动脚本（举例：如果在用 *bash* 的话，就修改 `~/.bashrc` 文件）里声明这一环境变量，让 VirtualBox 回退到旧的行为：

 `~/.bashrc`  `export VBOX_USB=usbfs` 

然后确保这行代码对环境变量的修改生效：重新登录，手动加载该文件，启动一个新 shell 会话，或者干脆重启。

另外，还应确保用户加入到了 `storage` 用户组。

### USB 调制解调器在宿主系统不可用

如果你的客体系统正在使用 USB 调制解调器，`kill` 掉虚拟机进程可能会造成它在宿主系统里不可用。杀掉并重启余下的 `VBoxSVC` 进程应该可以解决这一问题。

### 让虚拟机使用串口

确认你有权限使用串口：

```
$ /bin/ls -l /dev/ttyS*
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

将你的用户添加到 `uucp` [用户组](/index.php/%E7%94%A8%E6%88%B7%E7%BB%84 "用户组")即可。

### 重启 Xorg 之后虚拟机卡死

出现这一问题的原因是驱动程序缺失或有错。例如：[[8]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) 或 [[9]](https://bbs.archlinux.org/viewtopic.php?id=156079)。试试从菜单项 *Settings > Display* 里关闭 3D 加速，并确认要用的 [Xorg](/index.php/Xorg "Xorg") 驱动都已装好。

### 全屏模式只能看到黑屏

在某些窗口管理器（[i3](/index.php/I3 "I3"), [awesome](/index.php/Awesome "Awesome")）下运行 VirtualBox 时，由于顶层状态栏（overlay bar）的问题，VirtualBox 的全屏模式会出现问题。试试在菜单项 "Guest Settings > User Interface > Mini ToolBar" 里禁用 "Show in Full-screen/Seamless" 有可能绕过这一问题。详情可见[上游的问题汇报](https://www.virtualbox.org/ticket/14323)。

### 虚拟机启动时宿主系统卡死

潜在原因与解决方案：

*   SMAP

已知启用了 SMAP 的内核与某些芯片组（多为 Intel Broadwell）不兼容。解决办法是在[内核参数](/index.php/%E5%86%85%E6%A0%B8%E5%8F%82%E6%95%B0 "内核参数")里添加 `nosmap` 来禁用 SMAP 支持。

*   硬件虚拟化

禁用硬件虚拟化（VT-x/AMD-V）有可能解决这一问题。

*   各种内核的 bug
    *   通过 Fuse 挂载的分区（如 ntfs）[[10]](https://bbs.archlinux.org/viewtopic.php?id=185841)，[[11]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

一般来说，这类问题都是在 VirtualBox 或 Linux 内核版本更新之后初次出现。降级回到前一个版本就有可能解决问题。

### Linux 客体机的声音缓慢 / 扭曲

在 VirtualBox 里运行时，Linux 内核的 AC97 声卡驱动偶尔会猜错时钟频率设定。这就会造成声音播放速度太慢 / 太快。在 `/etc/modprobe.d` 目录里创建一个内容如下的文件即可解决：

```
options snd-intel8x0 ac97_clock=48000

```

### 模拟信号麦克风不可用

如果从模拟信号麦克风输入的音频信号在宿主系统可用，但在客体系统里不可用，可以试试在宿主系统上安装 [PulseAudio](/index.php/PulseAudio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "PulseAudio (简体中文)") 之类的[音频服务器](/index.php/Sound_system#Sound_servers "Sound system")试试看。

如果装了 PulseAudio 之后麦克风还是不能用，在菜单项 *VirtualBox > Machine > Settings > Audio* 里把 *Host Audio Driver* 的值改成 *ALSA Audio Driver* 也许有用。

### 版本更新之后麦克风不能用

5.1.x 版本以来一些用户遇到了音频输入问题：[[12]](https://forums.virtualbox.org/viewtopic.php?f=7&t=78797)

[降级](/index.php/%E9%99%8D%E7%BA%A7 "降级")也许能解决问题。[virtualbox-bin-5.0](https://aur.archlinux.org/packages/virtualbox-bin-5.0/) 可以帮你相对轻松地降级。

### 转换得来的 ISO 文件出现问题

有些镜像文件格式无法可靠地转换到 ISO 格式。例如：[ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso) 在转换时会忽略 .ccd 和 .sub 文件里的信息，最终产出的 ISO 镜像里的文件就可能受损。

为了避免这种情况，可以使用 [CDemu](/index.php/CDemu "CDemu") 或类似软件来在 Linux 客体系统里挂载光盘镜像。

### Host-only 网卡创建失败

确保所需的内核模块都已成功加载。详见 [#加载 VirtualBox 内核模块](#加载_VirtualBox_内核模块)。

### 插入模块失败

如果你在加载模块时遇到如下错误信息：

```
Failed to insert 'vboxdrv': Required key not available

```

将[模块签名](#模块签名)，或者在内核配置中禁用 `CONFIG_MODULE_SIG_FORCE`。

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

虚拟机不能平滑退出，就可能出现这个错误。试试下面这个命令：

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### NS_ERROR_FAILURE 且菜单项缺失

如果创建虚拟机时选择了 *QCOW*/*QCOW2*/*QED* 虚拟盘格式，有时就会出现这个错误。

如果初次启动虚拟机时遇到下面的错误消息：

```
Failed to open a session for the virtual machine debian.
Could not open the medium '/home/.../VirtualBox VMs/debian/debian.qcow'.
QCow: Reading the L1 table for image '/home/.../VirtualBox VMs/debian/debian.qcow' failed (VERR_EOF).
VD: error VERR_EOF opening image file '/home/.../VirtualBox VMs/debian/debian.qcow' (VERR_EOF).

Result Code: 
NS_ERROR_FAILURE (0x80004005)
Component: 
Medium

```

退出 VirtualBox，把新建虚拟机的相关文件都删除，并且在 VirtualBox 的配置文件中找到 `MachineRegistry` 元素，从这里删除你所创建的格式错误的虚拟机（一般是其最后一个子元素）：

 `~/.config/VirtualBox/VirtualBox.xml` 
```
...
<MachineRegistry>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/debian/debian.vbox"/>
  <MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/ubuntu/ubuntu.vbox"/>
  ~~<MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/lastvmcausingproblems/lastvmcausingproblems.qcow"/>~~
</MachineRegistry>
...
```

### Arch: pacstrap 脚本出错

如果你在[安装 Arch 系统](#在_VirtualBox_中安装_Archlinux)时，用 `pactrap` 脚本直接[#安装客体机插件](#安装客体机插件)，但此时 **还没有** 启动至新安装到虚拟盘的系统。那么你需要以 root 身份运行一次 `umount -l /mnt/dev` 然后再次运行 `pactrap`。否则新装的系统就不可用。

### 缺少硬件虚拟化导致 OpenBSD 不稳定

据称在其他的虚拟机平台上，OpenBSD 可以不依赖虚拟化指令集（VT-X，AMD-V）正常运行，VirtualBox 上的 OpenBSD 则不然。具体现象是出现大量的分段错误（segfault）。解决办法是在启动虚拟机时加上 `-norawr0` 参数。例如：

```
$ VBoxSDL -norawr0 -vm *name_of_OpenBSD_VM*

```

### Windows 宿主机: VERR_ACCESS_DENIED

为了能在 Windows 宿主机上读取 RAW 格式的 VMDK 镜像，VirtualBox GUI 需要以管理员权限启动。

### Windows: "The specified path does not exist. Check the path and then try again."

当在 Windows 客体系统里运行位于共享目录里 `.exe` 程序，而这一程序又需要管理员权限时，就可能出现这一错误信息。[[13]](https://www.virtualbox.org/ticket/5732#comment:39)

一个解决办法是把文件复制到虚拟硬盘上再运行。或者直接从[UNC 路径](https://en.wikipedia.org/wiki/Uniform_Naming_Convention "w:Uniform Naming Convention") (`\\vboxsvr`) 运行程序。详见 [[14]](https://support.microsoft.com/de-de/help/2019185/copying-files-from-a-mapped-drive-to-a-local-directory-fails-with-erro)。

### Windows 8.x 出现错误代码 0x000000C4

如果你在创建虚拟机时选择了 Win 8 系统，但在启动时还是遇到这一错误，可以尝试启用 `CMPXCHG16B` CPU 指令集。命令如下：

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8, 8.1 或 10 无法安装、启动或报错 "ERR_DISK_FULL"

修改虚拟机设置，在菜单项 *Settings > Storage > Controller:SATA* 里勾选 "Use Host I/O Cache"。

### WinXP: 颜色深度不得多于 16 位

如果只显示 16 位色，桌面图标看起来会模糊 / 结块。但是将色深调高时，系统可能会将桌面分辨率限制得较低，或者根本不允许改变色身。解决办法是在 Windows XP 虚拟机里运行 `regedit`，并写入这一项：

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

然后再去“桌面属性”窗口里修改色深。如果还是不见效，强制让屏幕重绘（比如按 `Host+f` 进入全屏模式）试试。

### Windows: 开启3D加速后屏幕闪烁

VirtualBox > 4.3.14 has a regression in which Windows guests with 3D acceleration flicker.

由于r120678补丁已经添加识别[environment variable](/index.php/Environment_variable "Environment variable")设置，可像如下启动VirtualBox：

```
$ CR_RENDER_FORCE_PRESENT_MAIN_THREAD=0 VirtualBox

```

请确保没有VirtualBox服务还在运行，并参考[VirtualBox bug 13653](https://www.virtualbox.org/ticket/13653)。

### Arch Linux guest虚拟机中没有硬件3D加速

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils)软件包从5.2.16-2版开始不再包含文件`VBoxEGL.so`。这导致Arch Linux guest虚拟机没有适当的3D加速。参见[49752 FS# 49752](https://bugs.archlinux.org/task/)。

要解决此问题，请应用位于[FS#49752#comment152254](https://bugs.archlinux.org/task/49752#comment152254)的补丁集。需要对补丁集进行一些修复，才能使其适用于5.2.16-2版。

### 无法在Wayland上启动VirtualBox：段错误

此问题通常是由Wayland上的Qt引起的，请参见[FS#58761](https://bugs.archlinux.org/task/58761)。

最好的办法是，在不影响其余的Qt应用程序（通常在Wayland中正常运行）的情况下，取消在VirtualBox的[desktop entry](/index.php/Desktop_entry "Desktop entry")中的`QT_QPA_PLATFORM` [environment variable](/index.php/Environment_variable "Environment variable")设置。

请按照[Desktop entries#Modify environment variables](/index.php/Desktop_entries#Modify_environment_variables "Desktop entries")中的说明进行操作，并修改Exec：

```
Exec=VirtualBox ...

```

为

```
Exec=env -u QT_QPA_PLATFORM VirtualBox ...

```

如果不起作用，则可能需要将`QT_QPA_PLATFORM`设置为`xcb`：

```
Exec=env QT_QPA_PLATFORM=xcb VirtualBox ...

```

## 已知问题

### 自动挂载不起作用

从6.0.0-1版本开始，自动挂载不适用于guest additions包[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils)和[virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox)。参见[FS#61307](https://bugs.archlinux.org/task/61307)。

### 缺少 vboximg-mount

`vboximg-mount`文件未打包在[virtualbox](https://www.archlinux.org/packages/?name=virtualbox)包中。参见[FS#64961](https://bugs.archlinux.org/task/64961)。

## 参阅

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")