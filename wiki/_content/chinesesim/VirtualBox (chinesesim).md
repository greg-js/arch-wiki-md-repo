**翻译状态：** 本文是英文页面 [VirtualBox](/index.php/VirtualBox "VirtualBox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-6-12，点击[这里](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=434334)可以查看翻译后英文页面的改动。

**VirtualBox** 是一个类似 [VMware](/index.php/VMware "VMware") 的虚拟 PC 模拟器，处于不断的开发中。使用 [Qt](/index.php/Qt "Qt") 图形界面，提供了无界面运行和 [SDL](https://en.wikipedia.org/wiki/SDL "wikipedia:SDL") 命令行工具进行运行管理。它包含**guest additions**为一些虚拟系统提供附加功能，包括文件共享、剪贴板和图形加速，支持 “无缝” 窗口整合模式。

[Wikipedia:Virtualbox](https://en.wikipedia.org/wiki/Virtualbox "wikipedia:Virtualbox")

## Contents

*   [1 在Archlinux中安装VirtualBox的安装步骤](#.E5.9C.A8Archlinux.E4.B8.AD.E5.AE.89.E8.A3.85VirtualBox.E7.9A.84.E5.AE.89.E8.A3.85.E6.AD.A5.E9.AA.A4)
    *   [1.1 安装基本软件包](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [1.2 加载VirtualBox的内核模块](#.E5.8A.A0.E8.BD.BDVirtualBox.E7.9A.84.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [1.3 在客户端系统访问主机 USB](#.E5.9C.A8.E5.AE.A2.E6.88.B7.E7.AB.AF.E7.B3.BB.E7.BB.9F.E8.AE.BF.E9.97.AE.E4.B8.BB.E6.9C.BA_USB)
    *   [1.4 Guest 附加光盘](#Guest_.E9.99.84.E5.8A.A0.E5.85.89.E7.9B.98)
    *   [1.5 扩展组件](#.E6.89.A9.E5.B1.95.E7.BB.84.E4.BB.B6)
    *   [1.6 使用正确的前端](#.E4.BD.BF.E7.94.A8.E6.AD.A3.E7.A1.AE.E7.9A.84.E5.89.8D.E7.AB.AF)
*   [2 在 VirtualBox 中安装 Archlinux](#.E5.9C.A8_VirtualBox_.E4.B8.AD.E5.AE.89.E8.A3.85_Archlinux)
    *   [2.1 在EFI模式下安装](#.E5.9C.A8EFI.E6.A8.A1.E5.BC.8F.E4.B8.8B.E5.AE.89.E8.A3.85)
    *   [2.2 Install the Guest Additions](#Install_the_Guest_Additions)
    *   [2.3 Load the Virtualbox kernel modules](#Load_the_Virtualbox_kernel_modules)
    *   [2.4 Launch the VirtualBox guest services](#Launch_the_VirtualBox_guest_services)
    *   [2.5 Hardware acceleration](#Hardware_acceleration)
    *   [2.6 Enable shared folders](#Enable_shared_folders)
        *   [2.6.1 Manual mounting](#Manual_mounting)
        *   [2.6.2 Automounting](#Automounting)
        *   [2.6.3 Mount at boot](#Mount_at_boot)
*   [3 虚拟磁盘管理](#.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98.E7.AE.A1.E7.90.86)
    *   [3.1 支持VirtualBox的格式](#.E6.94.AF.E6.8C.81VirtualBox.E7.9A.84.E6.A0.BC.E5.BC.8F)
    *   [3.2 磁盘映像格式转换](#.E7.A3.81.E7.9B.98.E6.98.A0.E5.83.8F.E6.A0.BC.E5.BC.8F.E8.BD.AC.E6.8D.A2)
        *   [3.2.1 VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK)
        *   [3.2.2 VHD to VDI and VDI to VDH](#VHD_to_VDI_and_VDI_to_VDH)
        *   [3.2.3 QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2)
*   [4 从其他虚拟机中迁移](#.E4.BB.8E.E5.85.B6.E4.BB.96.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.B8.AD.E8.BF.81.E7.A7.BB)
    *   [4.1 从QEMU映像转换](#.E4.BB.8EQEMU.E6.98.A0.E5.83.8F.E8.BD.AC.E6.8D.A2)
    *   [4.2 从VMware映像转换](#.E4.BB.8EVMware.E6.98.A0.E5.83.8F.E8.BD.AC.E6.8D.A2)
    *   [4.3 挂载虚拟磁盘](#.E6.8C.82.E8.BD.BD.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98)
        *   [4.3.1 VDI](#VDI)
    *   [4.4 压缩磁盘映像](#.E5.8E.8B.E7.BC.A9.E7.A3.81.E7.9B.98.E6.98.A0.E5.83.8F)
    *   [4.5 增加虚拟磁盘](#.E5.A2.9E.E5.8A.A0.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98)
        *   [4.5.1 Increase size for VDI disks](#Increase_size_for_VDI_disks)
    *   [4.6 从.vbox文件中手动更换虚拟磁盘](#.E4.BB.8E.vbox.E6.96.87.E4.BB.B6.E4.B8.AD.E6.89.8B.E5.8A.A8.E6.9B.B4.E6.8D.A2.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98)
        *   [4.6.1 Linux主机和其他操作系统之间的转移](#Linux.E4.B8.BB.E6.9C.BA.E5.92.8C.E5.85.B6.E4.BB.96.E6.93.8D.E4.BD.9C.E7.B3.BB.E7.BB.9F.E4.B9.8B.E9.97.B4.E7.9A.84.E8.BD.AC.E7.A7.BB)
*   [5 配置](#.E9.85.8D.E7.BD.AE)
    *   [5.1 网络](#.E7.BD.91.E7.BB.9C)
        *   [5.1.1 NAT](#NAT)
        *   [5.1.2 桥接](#.E6.A1.A5.E6.8E.A5)
    *   [5.2 主机端和客户端之间的键盘和鼠标](#.E4.B8.BB.E6.9C.BA.E7.AB.AF.E5.92.8C.E5.AE.A2.E6.88.B7.E7.AB.AF.E4.B9.8B.E9.97.B4.E7.9A.84.E9.94.AE.E7.9B.98.E5.92.8C.E9.BC.A0.E6.A0.87)
    *   [5.3 主机端和客户端间的共享文件夹](#.E4.B8.BB.E6.9C.BA.E7.AB.AF.E5.92.8C.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.97.B4.E7.9A.84.E5.85.B1.E4.BA.AB.E6.96.87.E4.BB.B6.E5.A4.B9)
    *   [5.4 Clone a virtual disk and assigning a new UUID to it](#Clone_a_virtual_disk_and_assigning_a_new_UUID_to_it)
*   [6 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [6.1 modprobe Exec 格式错误](#modprobe_Exec_.E6.A0.BC.E5.BC.8F.E9.94.99.E8.AF.AF)
    *   [6.2 VERR_ACCESS_DENIED](#VERR_ACCESS_DENIED)
    *   [6.3 pacstrap script fails](#pacstrap_script_fails)
    *   [6.4 键盘和鼠标都在我的虚拟机](#.E9.94.AE.E7.9B.98.E5.92.8C.E9.BC.A0.E6.A0.87.E9.83.BD.E5.9C.A8.E6.88.91.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [6.5 无法发送CTRL + ALT+ Fn键到我的虚拟机](#.E6.97.A0.E6.B3.95.E5.8F.91.E9.80.81CTRL_.2B_ALT.2B_Fn.E9.94.AE.E5.88.B0.E6.88.91.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [6.6 解决ISO映像问题](#.E8.A7.A3.E5.86.B3ISO.E6.98.A0.E5.83.8F.E9.97.AE.E9.A2.98)
    *   [6.7 VirtualBox的GUI没有应用我的GTK主题](#VirtualBox.E7.9A.84GUI.E6.B2.A1.E6.9C.89.E5.BA.94.E7.94.A8.E6.88.91.E7.9A.84GTK.E4.B8.BB.E9.A2.98)
    *   [6.8 OpenBSD系统无法使用时，虚拟化指令不可用](#OpenBSD.E7.B3.BB.E7.BB.9F.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8.E6.97.B6.EF.BC.8C.E8.99.9A.E6.8B.9F.E5.8C.96.E6.8C.87.E4.BB.A4.E4.B8.8D.E5.8F.AF.E7.94.A8)
    *   [6.9 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [6.10 USB 子系统在宿主机和虚拟机没有作用](#USB_.E5.AD.90.E7.B3.BB.E7.BB.9F.E5.9C.A8.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.92.8C.E8.99.9A.E6.8B.9F.E6.9C.BA.E6.B2.A1.E6.9C.89.E4.BD.9C.E7.94.A8)
    *   [6.11 主机模式网络接口创建失败](#.E4.B8.BB.E6.9C.BA.E6.A8.A1.E5.BC.8F.E7.BD.91.E7.BB.9C.E6.8E.A5.E5.8F.A3.E5.88.9B.E5.BB.BA.E5.A4.B1.E8.B4.A5)
    *   [6.12 WinXP: 位深不能大于 16](#WinXP:_.E4.BD.8D.E6.B7.B1.E4.B8.8D.E8.83.BD.E5.A4.A7.E4.BA.8E_16)
    *   [6.13 虚拟系统使用串行端口](#.E8.99.9A.E6.8B.9F.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8.E4.B8.B2.E8.A1.8C.E7.AB.AF.E5.8F.A3)
    *   [6.14 Windows 8.x Error Code 0x000000C4](#Windows_8.x_Error_Code_0x000000C4)
    *   [6.15 Windows 8, 8.1 or 10 fails to install, boot or has error "ERR_DISK_FULL"](#Windows_8.2C_8.1_or_10_fails_to_install.2C_boot_or_has_error_.22ERR_DISK_FULL.22)
    *   [6.16 Linux guests have slow/distorted audio](#Linux_guests_have_slow.2Fdistorted_audio)
    *   [6.17 客户端启动后的Xorg死机](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.90.AF.E5.8A.A8.E5.90.8E.E7.9A.84Xorg.E6.AD.BB.E6.9C.BA)
    *   [6.18 "NS_ERROR_FAILURE" and missing menu items](#.22NS_ERROR_FAILURE.22_and_missing_menu_items)
    *   [6.19 USB modem](#USB_modem)
    *   [6.20 "The specified path does not exist. Check the path and then try again." error in Windows guests](#.22The_specified_path_does_not_exist._Check_the_path_and_then_try_again..22_error_in_Windows_guests)
    *   [6.21 挂载失败导致的啟动问题](#.E6.8C.82.E8.BD.BD.E5.A4.B1.E8.B4.A5.E5.AF.BC.E8.87.B4.E7.9A.84.E5.95.9F.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [6.22 复制和粘贴在 Arch Linux 客户机没有作用](#.E5.A4.8D.E5.88.B6.E5.92.8C.E7.B2.98.E8.B4.B4.E5.9C.A8_Arch_Linux_.E5.AE.A2.E6.88.B7.E6.9C.BA.E6.B2.A1.E6.9C.89.E4.BD.9C.E7.94.A8)
    *   [6.23 唤醒后异常](#.E5.94.A4.E9.86.92.E5.90.8E.E5.BC.82.E5.B8.B8)
    *   [6.24 Btrfs 系统镜像](#Btrfs_.E7.B3.BB.E7.BB.9F.E9.95.9C.E5.83.8F)
    *   [6.25 vagrant 啟动问题](#vagrant_.E5.95.9F.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [6.26 没有64位客户端选项](#.E6.B2.A1.E6.9C.8964.E4.BD.8D.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.80.89.E9.A1.B9)
    *   [6.27 主机上的虚拟机启动操作系统死机](#.E4.B8.BB.E6.9C.BA.E4.B8.8A.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.90.AF.E5.8A.A8.E6.93.8D.E4.BD.9C.E7.B3.BB.E7.BB.9F.E6.AD.BB.E6.9C.BA)
    *   [6.28 The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)](#The_virtual_machine_has_terminated_unexpectedly_during_startup_with_exit_code_1_.280x1.29)
    *   [6.29 Analog microphone not working in guest](#Analog_microphone_not_working_in_guest)
    *   [6.30 Fullscreen mode shows blank guest screen](#Fullscreen_mode_shows_blank_guest_screen)
    *   [6.31 Failed to insert module](#Failed_to_insert_module)
*   [7 参阅](#.E5.8F.82.E9.98.85)

## 在Archlinux中安装VirtualBox的安装步骤

为了在您的Archlinux中安装VirtualBox，请遵循以下步骤。

### 安装基本软件包

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [virtualbox](https://www.archlinux.org/packages/?name=virtualbox)。从下面选择一个内核模块获取方式

*   如果使用[linux](https://www.archlinux.org/packages/?name=linux)内核，请安装[virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch)
*   其它内核安装 [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms)

要编译 [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) 提供的内核文件，需要同时安装对应的内核头文件(例如安装 [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) 的头文件 [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers)). [[1]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) VirtualBox 或内核更新的时候，DKMS Pacman 钩子会自动编译内核模块。

要使用基于 [Qt](/index.php/Qt "Qt") 的图形界面，需要安装 [qt5-x11extras](https://www.archlinux.org/packages/?name=qt5-x11extras) 软件包。如果使用命令行命令，则不需要安装。

### 加载VirtualBox的内核模块

从版本 5.0.16 开始，[virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch) 和 [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) 使用 `systemd-modules-load.service` 在启动时自动加载内核模块。

**Note:** 如果不希望启动时就加载 VirtualBox 模块，需要屏蔽默认的 `/usr/lib/modules-load.d/virtualbox-host-modules-arch.conf` (或 `-dkms.conf`)。创建一个同名空文件或链接到 `/dev/null`.

VirtualBox 在 Linux 上运行需要使用自己的[内核模块](/index.php/Kernel_modules "Kernel modules")，**vboxdrv**模块必须在虚拟机运行前加载。

手动加载模块:

```
# modprobe vboxdrv

```

**Note:** 使用命令前可能需要更新内核模块数据库以避免 'no such file or directory' 错误，执行: `depmod -a`.

启动 VirtualBox 图形界面:

```
$VirtualBox

```

以下模块是可选的，但建议选上如果您不想在进行一些高级配置时被打扰(如下): `vboxnetadp`, `vboxnetflt` 和`vboxpci`.

*   `vboxnetadp` 和`vboxnetflt` 都是需要的当你使用网桥时 [bridged](https://www.virtualbox.org/manual/ch06.html#network_bridged) or [host-only networking](https://www.virtualbox.org/manual/ch06.html#network_hostonly) feature. More precisely, `vboxnetadp` is needed to create the host interface in the VirtualBox global preferences, and `vboxnetflt` is needed to launch a virtual machine using that network interface.

*   `vboxpci`是需要的， 当你的虚拟机需要使用一个你的主机上的pci设备时

**Note:** 如果在virtualbox内核模块运行时你更新了模块，你需要手动重新加载这些模块以使用新版本。为了这么做，请在 root 权限下运行 `vboxreload`

最后，如果你使用前面提到的 "Host-only" 或是 "bridge networking" 功能，请确保 [net-tools](https://www.archlinux.org/packages/?name=net-tools) 已经安装。VirtualBoxt 为主机接口配置命令 `VBoxManage hostonlyif` 使用 `ifconfig` 和 `route` 来定位 IP 和 route，或通过 GUI 的*Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter*选项。

### 在客户端系统访问主机 USB

将需要运行 Virtualbox 的用户名添加到 **vboxusers** [用户组](/index.php/Group "Group")，USB 设备才能被访问。

### Guest 附加光盘

建议在运行VirtualBox 的主机系统上安装[virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) 软件包 。 这个包是一个磁盘镜像，用来安装虚拟系统的附加功能。 这个 *.iso* 文件会被定位在 `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`，也许需要手动在虚拟机中加载，当挂载之后你可以安装增强工具。

### 扩展组件

Oracle 的扩展组件以仅供个人使用的协议发布，在这里提供 [additional features](https://www.virtualbox.org/manual/ch01.html#intro-installing)。安装 [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/) 可获得这些组件, 已编译的版本可以在 [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories")仓库找到。

如果你喜欢使用传统的手动方法：手动下载扩展组件并通过 GUI 安装 (*File > Preferences > Extensions*) 或通过 `VBoxManage extpack install <.vbox-extpack>`命令来安装, 请确保你拥有 toolkit (like [Polkit](/index.php/Polkit "Polkit"), gksu, etc.) 来获准进入 VirtualBox。安装过程 [需要 root 权限](https://www.virtualbox.org/ticket/8473).

### 使用正确的前端

恭喜你！现在，你已经准备好使用VirtualBox了。

这里有多个前端提供给您，其中两个是默认提供:

*   如果你只想在命令行下使用 VirtualBox (只想启动现有的虚拟机或是更改一些配置)，你可以使用 `VBoxSDL` 命令。VBoxSDL 仅仅提供一个简单的窗口包含所有虚拟机，没有菜单或是其他控制项。
*   如果你想使用命令行并且不使用任何 GUI (例如在服务器上) 来创建、运行和配置虚拟机，使用 `VBoxHeadless` 命令，不会有任何图形输出，但是仅仅使用 VRDP 数据(安装扩展模块之后才能使用)

如果你安装了 [qt5-x11extras](https://www.archlinux.org/packages/?name=qt5-x11extras)这一可选依赖，你可以运行 `VirtualBox` 来获得一个美观易用的图形界面并能够使用鼠标。

最后你可以使用 [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") 来通过网页界面来管理你的虚拟机。

查阅 [VirtualBox manual](https://www.virtualbox.org/manual) 来了解如何创建虚拟机。

**Warning:** 如果你打算在 [Btrfs](/index.php/Btrfs "Btrfs") 文件系统上存储虚拟硬盘镜像在创建任何镜像之前，你应该考虑在镜像的目标文件夹中关闭[Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs")

## 在 VirtualBox 中安装 Archlinux

在 VirtualBox 中新建一个虚拟机，并在加载 Archlinux 镜像，按照一般步骤完整安装 Archlinux系统，参考[Beginners' guide (简体中文)](/index.php/Beginners%27_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Beginners' guide (简体中文)") 或是 [Installation guide (简体中文)](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")

### 在EFI模式下安装

If you want to install Arch Linux in EFI mode inside VirtualBox, in the settings of the virtual machine, choose *System* item from the panel on the left and *Motherboard* tab from the right panel, and check the checkbox *Enable EFI (special OSes only)*. After selecting the kernel from the Arch Linux installation media's menu, the media will hang for a minute or two and will continue to boot the kernel normally afterwards. Be patient.

Once the system and the boot loader are installed, VirtualBox will first attempt to run `/EFI/BOOT/BOOTX64.EFI` from the [ESP](/index.php/ESP "ESP"). If that first option fails, VirtualBox will then try the EFI shell script `startup.nsh` from the root of the ESP. This means that in order to boot the system you have the following options:

*   [Launch the bootloader manually](/index.php/Unified_Extensible_Firmware_Interface#UEFI_Shell "Unified Extensible Firmware Interface") from the EFI shell every time;
*   Move the bootloader to the default `/EFI/BOOT/BOOTX64.EFI` path;
*   Create the `startup.nsh` script at the ESP root containing the path to the boot loader application, e.g. `\EFI\grub\grubx64.efi`.

Do not bother with the VirtualBox Boot Manager (accessible with `F2` at boot): EFI entries added to it manually at boot or with [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) will persist after a reboot [but are lost when the VM is shut down](https://www.virtualbox.org/ticket/11177).

See also [UEFI Virtualbox installation boot problems](https://bbs.archlinux.org/viewtopic.php?id=158003).

### Install the Guest Additions

VirtualBox [Guest Additions](https://www.virtualbox.org/manual/ch04.html) provides drivers and applications that optimize the guest operating system including improved image resolution and better control of the mouse. Within the installed guest system, install:

*   [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) for VirtualBox Guest utilities with X support
*   [virtualbox-guest-utils-nox](https://www.archlinux.org/packages/?name=virtualbox-guest-utils-nox) for VirtualBox Guest utilities without X support

Both packages will make you choose a package to provide guest modules:

*   for [linux](https://www.archlinux.org/packages/?name=linux) kernel choose [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch)
*   for other kernels choose [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms)

To compile the virtualbox modules provided by [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms), it will also be necessary to install the appropriate headers package(s) for your installed kernel(s) (e.g. [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers) for [linux-lts](https://www.archlinux.org/packages/?name=linux-lts)). [[2]](https://lists.archlinux.org/pipermail/arch-dev-public/2016-March/027808.html) When either VirtualBox or the kernel is updated, the kernel modules will be automatically recompiled thanks to the DKMS Pacman hook.

**Note:**

*   You can alternatively install the Guest Additions with the ISO from the [virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) package, provided you installed this on the host system. To do this, go to the device menu click Insert Guest Additions CD Image.
*   To recompile the vbox kernel modules, run `rcvboxdrv` as root.

### Load the Virtualbox kernel modules

To load the modules automatically, [enable](/index.php/Enable "Enable") the `vboxservice` service which loads the modules and synchronizes the guest's system time with the host.

To load the modules manually, type:

```
# modprobe -a vboxguest vboxsf vboxvideo

```

Since version 5.0.16, [virtualbox-guest-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-arch) and [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) use **systemd-modules-load** service to load their modules at boot time.

**Note:** If you don't want the VirtualBox modules to be loaded at boot time, you have to mask the default `/usr/lib/modules-load.d/virtualbox-guest-modules-arch.conf` (or `-dkms.conf`) by creating an empty file (or symlink to `/dev/null`) with the same name in `/etc/modules-load.d`.

### Launch the VirtualBox guest services

After the rather big installation step dealing with VirtualBox kernel modules, now you need to start the guest services. The guest services are actually just a binary executable called `VBoxClient` which will interact with your X Window System. `VBoxClient` manages the following features:

*   shared clipboard and drag and drop between the host and the guest;
*   seamless window mode;
*   the guest display is automatically resized according to the size of the guest window;
*   checking the VirtualBox host version

All of these features can be enabled independently with their dedicated flags:

```
$ VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

```

As a shortcut, the `VBoxClient-all` bash script enables all of these features.

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) installs `/etc/xdg/autostart/vboxclient.desktop` that launches `VBoxClient-all` on logon. If your [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager") does not support this scheme, you will need to set up autostarting yourself, see [Autostarting#Graphical](/index.php/Autostarting#Graphical "Autostarting") for more details.

VirtualBox can also synchronize the time between the host and the guest, to do this, [start/enable](/index.php/Start/enable "Start/enable") the `vboxservice.service`.

Now, you should have a working Arch Linux guest. Note that features like clipboard sharing are disabled by default in VirtualBox, and you will need to turn them on in the per-VM settings if you actually want to use them (e.g. *Settings > General > Advanced > Shared Clipboard*).

### Hardware acceleration

Hardware acceleration can be activated from the VirtualBox options on the host computer. Note the [GDM](/index.php/GDM "GDM") display manager 3.16+ is known to [break](https://bugzilla.gnome.org/show_bug.cgi?id=749390) hardware acceleration support. So if you get issues with hardware acceleration, try out another display manager (lightdm seems to work fine).[[3]](https://bbs.archlinux.org/viewtopic.php?id=200025) [[4]](https://bbs.archlinux.org/viewtopic.php?pid=1607593#p1607593)

If you want to share folders between your host and your Arch Linux guest, read on.

### Enable shared folders

Shared folders are managed on the host, in the settings of the Virtual Machine accessible via the GUI of VirtualBox, in the *Shared Folders* tab. There, *Folder Path*, the name of the mount point identified by *Folder name*, and options like *Read-only*, *Auto-mount* and *Make permanent* can be specified. These parameters can be defined with the `VBoxManage` command line utility. See [there for more details](https://www.virtualbox.org/manual/ch04.html#sharedfolders).

No matter which method you will use to mount your folder, all methods require some steps first.

To avoid this issue `/sbin/mount.vboxsf: mounting failed with the error: No such device`, make sure the `vboxsf` kernel module is properly loaded. It should be, since we enabled all guest kernel modules previously.

Two additional steps are needed in order for the mount point to be accessible from users other than root:

*   the [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) package created a group `vboxsf` (done in a previous step);
*   your username must be in `vboxsf` [group](/index.php/Group "Group").

#### Manual mounting

Use the following command to mount your folder in your Arch Linux guest:

```
# mount -t vboxsf *shared_folder_name* *mount_point_on_guest_system*

```

The vboxsf filesystem offers other options which can be displayed with this command:

```
# mount.vboxsf

```

For example if the user was not in the *vboxsf* group, we could have used this command to give access our mountpoint to him:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt/

```

Where *uid* and *gid* are values corresponding to the users we want to give access to. These values are obtained from the `id` command run against this user.

#### Automounting

In order for the automounting feature to work you must have checked the auto-mount checkbox in the GUI or used the optional `--automount` argument with the command `VBoxManage sharedfolder`.

The shared folder should now appear in `/media/sf_*shared_folder_name*`. If users in `media` cannot access the shared folders, check that `media` has permissions 755 or has group ownership `vboxsf` if using permission 750\. This is currently not the default if media is created by installing the `virtualbox-guest-utils`.

You can use symlinks if you want to have a more convenient access and avoid to browse in that directory, e.g.:

```
$ ln -s /media/sf_*shared_folder_name* ~/*my_documents*

```

#### Mount at boot

You can mount your directory with [fstab](/index.php/Fstab "Fstab"). However, to prevent startup problems with systemd, `comment=systemd.automount` should be added to `/etc/fstab`. This way, the shared folders are mounted only when those mount points are accessed and not during startup. This can avoid some problems, especially if the guest additions are not loaded yet when systemd read fstab and mount the partitions.

```
*sharedFolderName*  */path/to/mntPtOnGuestMachine*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,comment=systemd.automount  0  0

```

*   `*sharedFolderName*`: the value from the VirtualMachine's *Settings > SharedFolders > Edit > FolderName* menu. This value can be different from the name of the real folder name on the host machine. To see the VirtualMachine's *Settings* go to the host OS VirtualBox application, select the corresponding virtual machine and click on *Settings*.
*   `*/path/to/mntPtOnGuestMachine*`: if not existing, this directory should be created manually (for example by using [mkdir](/index.php/Core_utilities#mkdir "Core utilities"))
*   `dmode`/`fmode` are directory/file permissions for directories/files inside `*/path/to/mntPtOnGuestMachine*`.}}

As of 2012-08-02, mount.vboxsf does not support the *nofail* option:

```
*desktop*  */media/desktop*  vboxsf  uid=*user*,gid=*group*,rw,dmode=700,fmode=600,nofail  0  0

```

## 虚拟磁盘管理

### 支持VirtualBox的格式

VirtualBox supports the following virtual disk formats:

*   VDI: The Virtual Disk Image is the VirtualBox own open container used by default when you create a virtual machine with VirtualBox.

*   VMDK: The Virtual Machine Disk has been initially developed by VMware for their products. The specification was initially closed source, but it became now an open format which is fully supported by VirtualBox. This format offers the ability to be split into several 2GB files. This feature is specially useful if you want to store the virtual machine on machines which do not support very large files. Other formats, excluding the HDD format from Parallels, do not provide such an equivalent feature.

*   VHD: The Virtual Hard Disk is the format used by Microsoft in Windows Virtual PC and Hyper-V. If you intend to use any of these Microsoft products, you will have to choose this format.

**Tip:** Since Windows 7, this format can be mounted directly without any additional application.

*   VHDX (read only): This is the eXtended version of the Virtual Hard Disk format developed by Microsoft, which has been released on 2012-09-04 with Hyper-V 3.0 coming with Windows Server 2012\. This new version of the disk format does offer enhanced performance (better block alignment), larger blocks size, and journal support which brings power failure resiliency. VirtualBox [should support this format in read only](https://www.virtualbox.org/manual/ch15.html#idp63002176).

*   Version 2 of the HDD: The HDD format is developed by Parallels Inc and used in their hypervisor solutions like Parallels Desktop for Mac. Newer versions of this format (i.e. 3 and 4) are not supported due to the lack of documentation for this proprietary format.
    **Note:** There is currently a controversy regarding the support of the version 2 of the format. While the official VirtualBox manual [only reports the second version of the HDD file format as supported](https://www.virtualbox.org/manual/ch05.html#vdidetails), Wikipedia's contributors are [reporting the first version may work too](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines"). Help is welcome if you can perform some tests with the first version of the HDD format.

*   QED: The QEMU Enhanced Disk format is an old file format for QEMU, another free and open source hypervisor. This format was designed from 2010 in a way to provide a superior alternative to QCOW2 and others. This format features a fully asynchronous I/O path, strong data integrity, backing files, and sparse files. QED format is supported only for compatibility with virtual machines created with old versions of QEMU.

*   QCOW: The QEMU Copy On Write format is the current format for QEMU. The QCOW format does support zlib-based transparent compression and encryption (the latter has flaw and is not recommended). QCOW is available in two versions: QCOW and QCOW2\. The latter tends to supersede the first one. QCOW is [currently fully supported by VirtualBox](https://www.virtualbox.org/manual/ch15.html#idp63002176). QCOW2 comes in two revisions: QCOW2 0.10 and QCOW2 1.1 (which is the default when you create a virtual disk with QEMU). VirtualBox does not support this QCOW2 format (both revisions have been tried).

*   OVF: The Open Virtualization Format is an open format which has been designed for interoperability and distributions of virtual machines between different hypervisors. VirtualBox supports all revisions of this format via the [`VBoxManage` import/export feature](https://www.virtualbox.org/manual/ch08.html#idp55423424) but with [known limitations](https://www.virtualbox.org/manual/ch14.html#KnownProblems).

*   RAW: This is the mode when the virtual disk is exposed directly to the disk without being contained in a specific file format container. VirtualBox supports this feature in several ways: converting RAW disk [to a specific format](https://www.virtualbox.org/manual/ch08.html#idp59139136), or by [cloning a disk to RAW](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi), or by using directly a VMDK file [which points to a physical disk or a simple file](https://www.virtualbox.org/manual/ch09.html#idp57804112).

### 磁盘映像格式转换

#### VMDK to VDI and VDI to VMDK

VirtualBox can handle back and forth conversion between VDI and VMDK by itself with [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi).

VMDK to VDI:

```
$ VBoxManage clonehd *source.vmdk* *destination.vdi* --format VDI

```

VDI to VMDK:

```
$ VBoxManage clonehd *source.vdi* *destination.vmdk* --format VMDK

```

#### VHD to VDI and VDI to VDH

VirtualBox can handle conversion back and forth this format with [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) too.

VHD to VDI:

```
$ VBoxManage clonehd *source.vhd* *destination.vdi* --format VDI

```

VDI to VHD:

```
$ VBoxManage clonehd *source.vdi* *destination.vhd* --format VHD

```

#### QCOW2 to VDI and VDI to QCOW2

[`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) cannot handle the QEMU format conversion; we will thus rely on another tool. The `qemu-img` command from [qemu](https://www.archlinux.org/packages/?name=qemu) can be used to convert images back and forth from VDI to QCOW2\.
**Note:** `qemu-img` can handle a bunch of other formats too. According to the `qemu-img --help`, here are the supported formats this tool supports: "*vvfat vpc vmdk vhdx vdi ssh sheepdog sheepdog sheepdog raw host_cdrom host_floppy host_device file qed qcow2 qcow parallels nbd nbd nbd iscsi dmg tftp ftps ftp https http cow cloop bochs blkverify blkdebug'".*

QCOW2 to VDI:

```
$ qemu-img convert -pO vdi *source.qcow2* *destination.vdi*

```

VDI to QCOW2:

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2*

```

As QCOW2 comes in two revisions (see [#Formats supported by VirtualBox](#Formats_supported_by_VirtualBox), use the flag `-o compat=` to specify the revision.

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=0.10

```

or

```
$ qemu-img convert -pO qcow2 *source.vdi* *destination.qcow2* -o compat=1.1

```

**Tip:** The `-p` parameter is used to get the progression of the conversion task.

## 从其他虚拟机中迁移

`qemu-img` 程序可以用来将映像从一种格式转换到另一种格式，或为一个映像添加压缩或加密。

```
  # pacman -S qemu

```

### 从QEMU映像转换

To convert a QEMU image for use with VirtualBox, first convert it to *raw* format, then use VirtualBox's conversion utility to convert and compact it in its native format.

```
  $ qemu-img convert -O raw test.qcow2 test.raw
  $ VBoxManage modifyvdi /full/path/to/test.vdi compact
or 
  $ qemu-img convert -O raw test.qcow2 test.raw
    (of course you must have installed qemu package for that)
  $ VBoxManage convertfromraw /full/path/to/test.raw /full/path/to/test.vdi
  $ VBoxManage modifyvdi      /full/path/to/test.vdi compact

```

### 从VMware映像转换

运行

```
  $ VBoxManage clonehd source.vmdk target.vdi --format VDI

```

对于当前VirtualBox版本来说也许是不必要的（有待证实）

### 挂载虚拟磁盘

#### VDI

Mounting vdi images only works with fixed size images (a.k.a. static images); dynamic (dynamically size allocating) images are not easily mountable.

The offset of the partition (within the vdi) is needed, then add the value of `offData` to `32256` (e.g. 69632 + 32256 = 101888):

```
$ VBoxManage internalcommands dumphdinfo <storage.vdi> | grep "offData"

```

The can now be mounted with:

```
# mount -t ext4 -o rw,noatime,noexec,loop,offset=101888 <storage.vdi> /mntpoint/

```

You can also use [mount.vdi](https://github.com/pld-linux/VirtualBox/blob/master/mount.vdi) script that, which you can use as (install script itself to `/usr/bin/`):

```
# mount -t vdi -o fstype=ext4,rw,noatime,noexec *vdi_file_location* */mnt/*

```

Alternately you can use [qemu](https://www.archlinux.org/packages/?name=qemu)'s kernel module that can do this [[attrib](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/)]:

```
# modprobe nbd max_part=16
# qemu-nbd -c /dev/nbd0 <storage.vdi>
# mount /dev/nbd0p1 /mnt/dir/
# # to unmount:
# umount /mnt/dir/
# qemu-nbd -d /dev/nbd0

```

If the partition nodes are not propagated try using `partprobe /dev/nbd0`; otherwise, a vdi partition can be mapped directly to a node by: `qemu-nbd -P 1 -c /dev/nbd0 <storage.vdi>`.

### 压缩磁盘映像

Compacting virtual disks only works with `.vdi` files and basically consists in the following steps.

Boot your virtual machine and remove all bloat manually or by using cleaning tools like [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) which is [available for Windows systems too](http://bleachbit.sourceforge.net/download/windows).

Wiping free space with zeroes can be achieved with several tools:

*   If you were previously using Bleachbit, check the checkbox *System > Free disk space* in the GUI, or use `bleachbit -c system.free_disk_space` in CLI;
*   在 UNIX基本系统,使用 `dd` or preferably [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (see [here](http://superuser.com/a/355322) to learn the differences) :

	 `# dcfldd if=/dev/zero of=*/fillfile* bs=4M` 

	When `fillfile` reaches the limit of the partition, you will get a message like `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. This means that all of the user-space and non-reserved blocks of the partition will be filled with zeros. Using this command as root is important to make sure all free blocks have been overwritten. Indeed, by default, when using partitions with ext filesystem, a specified percentage of filesystem blocks is reserved for the super-user (see the `-m` argument in the `mkfs.ext4` man pages or use `tune2fs -l` to see how much space is reserved for root applications).

	When the aforementioned process has completed, you can remove the file `*fillfile*` you created.

*   On Windows, there are two tools available:

*   `sdelete` from the [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), type `sdelete -s -z *c:*`, where you need to reexecute the command for each drive you have in your virtual machine;
*   or, if you love scripts, there is a [PowerShell solution](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html), but which still needs to be repeated for all drives.

	 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root *c:\* -PercentFree 0` 

**Note:** This script must be run in a PowerShell environment with administrator privileges. By default, scripts cannot be run, ensure the execution policy is at least on `RemoteSigned` and not on `Restricted`. This can be checked with `Get-ExecutionPolicy` and the required policy can be set with `Set-ExecutionPolicy RemoteSigned`.

Once the free disk space have been wiped, shut down your virtual machine.

The next time you boot your virtual machine, it is recommended to do a filesystem check.

*   On UNIX-based systems, you can use `fsck` manually;

*   On GNU/Linux systems, and thus on Arch Linux, you can force a disk check at boot [thanks to a kernel boot parameter](/index.php/Fsck#Forcing_the_check "Fsck");

*   On Windows systems, you can use:

*   either `chkdsk *c:* /F` where `*c:*` needs to be replaced by each disk you need to scan and fix errors;
*   or `FsckDskAll` [from here](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx) which is basically the same software as `chkdsk`, but without the need to repeat the command for all drives;

Now, remove the zeros from the `vdi` file with `[VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi)`:

```
$ VBoxManage modifyhd *your_disk.vdi* --compact

```

**Note:** If your virtual machine has snapshots, you need to apply the above command on each `.vdi` files you have.

### 增加虚拟磁盘

If you are running out of space due to the small hard drive size you selected when you created your virtual machine, the solution adviced by the VirtualBox manual is to use [`VBoxManage modifyhd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). However this command only works for VDI and VHD disks and only for the dynamically allocated variants. If you want to resize a fixed size virtual disk disk too, read on this trick which works either for a Windows or UNIX-like virtual machine.

First, create a new virtual disk next to the one you want to increase:

```
$ VBoxManage createhd -filename *new.vdi* --size *10000*

```

where size is in MiB, in this example 10000MiB ~= 10GiB, and *new.vdi* is name of new hard drive to be created.

Next, the old virtual disk needs to be cloned to the new one which this may take some time:

```
$ VBoxManage clonehd *old.vdi* *new.vdi* --existing

```

**Note:** By default, this command uses the *Standard* (corresponding to dynamic allocated) file format variant and thus will not use the same file format variant as your source virtual disk. If your *old.vdi* has a fixed size and you want to keep this variant, add the parameter `--variant Fixed`.

Detach the old hard drive and attach new one, replace all mandatory italic arguments by your own:

```
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium none
$ VBoxManage storageattach *VM_name* --storagectl *SATA* --port *0* --medium *new.vdi* --type hdd

```

To get the storage controller name and the port number, you can use the command `VBoxManage showvminfo *VM_name*`. Among the output you will get such a result (what you are looking for is in italic):

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

Download [GParted live image](http://gparted.org/download.php) and mount it as a virtual CD/DVD disk file, boot your virtual machine, increase/move your partitions, umount GParted live and reboot.

**Note:** On GPT disks, increasing the size of the disk will result in the backup GPT header not being at the end of the device. GParted will ask to fix this, click on *Fix* both times. On MBR disks, you do not have such a problem as this partition table as no trailer at the end of the disk.

Finally, unregister the virtual disk from VirtualBox and remove the file:

```
$ VBoxManage closemedium disk *old.vdi*
$ rm *old.vdi*

```

#### Increase size for VDI disks

If your disk is a vdi one, simply run:

```
$ VBoxManage modifyhd *your_virtual_disk.vdi* --resize *the_new_size*

```

Then jump back to the Gparted step, to increase the size of the partition on the virtual disk.

### 从.vbox文件中手动更换虚拟磁盘

If you think that editing a simple *XML* file is more convenient than playing with the GUI or with `VBoxManage` and you want to replace (or add) a virtual disk to your virtual machine, in the *.vbox* configuration file corresponding to your virtual machine, simply replace the GUID, the file location and the format to your needs:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*" location="*ArchLinux_vm.vdi*" format="*VDI*" type="Normal"/>` 

then in the `<AttachedDevice>` sub-tag of `<StorageController>`, replace the GUID by the new one.

 `ArchLinux_vm.vbox` 
```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="*{670157e5-8bd4-4f7b-8b96-9ee412a712b5}*"/>
</AttachedDevice>
```

**Note:** If you do not know the GUID of the drive you want to add, you can use the `VBoxManage showhdinfo *file*`. If you previously used `VBoxManage clonehd` to copy/convert your virtual disk, this command should have outputted the GUID just after the copy/conversion completed. Using a random GUID does not work, as each [UUID is stored inside each disk image](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

#### Linux主机和其他操作系统之间的转移

The information about path to harddisks and the snapshots is stored between `<HardDisks> .... </HardDisks>` tags in the file with the *.vbox* extension. You can edit them manually or use this script where you will need change only the path or use defaults, assumed that *.vbox* is in the same directory with a virtual harddisk and the snapshots folder. It will print out new configuration to stdout.

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

**Note:**

*   If you will prepare virtual machine for use in Windows host then in the path name end you should use backslash \ instead of / .
*   The script detects snapshots by looking for `{` in the file name.
*   To make it run on a new host you will need to add it first to the register by clicking on **Machine -> Add...** or use hotkeys Ctrl+A and then browse to *.vbox* file that contains configuration or use command line `VBoxManage registervm *filename*.vbox`

## 配置

### 网络

VirtualBox 客户端可以通过不同的方式连接网络；其中，有[#NAT](#NAT)和[#桥接](#.E6.A1.A5.E6.8E.A5)链接。[#NAT](#NAT)是最简单的且作为一个新虚拟机的默认方式。

[VirtualBox手册](http://www.virtualbox.org/manual/UserManual.html)涵盖了主机模式和内网选项。这些都被忽略了，因为在大多数情况下与操作系统无关。

#### NAT

在VirtualBox中：

*   访问虚拟机的*设置*菜单；
*   点击左边的*网络‘’；最后，*
*   在“连接方式”的下拉列表中选择*NAT*。

与VirtualBox捆绑的DHCP服务使得客户端系统能够与DHCP一起配置，第一张卡的NAT IP地址是 10.0.2.0，第二张是10.0.3.0，往后以此类推。

#### 桥接

桥接网络可能被以多种方式启动；其中，有要求以较少控制为代价进行最小启动的原生方式。对于较新版本，VirtualBox可以在没有第三方工具的帮助下，在客户端和无线主机接口间进行桥接。

在继续之前，加载必要模块：

```
# modprobe vboxnetflt

```

在VirtualBox中：

*   访问虚拟机的*设置*菜单；
*   点击左边列表中的*网络*
*   在*链接方式*的下拉列表中选择*Bridged Adapter(桥接适配器)*；最后，
*   在*界面名称*下拉列表中，选择客户端操作系统被包含在内，主机用于连接网络的接口。

Start the virtual machine and configure its network as usual; e.g., DHCP or static. 打开虚拟机，像往常一样配置其网络；例如 DHCP 或 static（静态网络）。

### 主机端和客户端之间的键盘和鼠标

*   为了捕获键盘和鼠标，点击虚拟机内部。
*   想要释放，按下右 `Ctrl`.

想要获得在主机端和客户端之间的无缝鼠标集成功能，在客户端内安装[#客户端增强包](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.A2.9E.E5.BC.BA.E5.8C.85)。

### 主机端和客户端间的共享文件夹

在虚拟机的设置中，找到数据空间标签，然后加入你想要共享的文件夹。

*   注意：为了使用这个功能你需要安装客户端增强包。

```
在Linux主机中，*设备 → 安装增强功能*
确定（被要求下载CD镜像时）
挂载（被要求注册和挂载时）

```

In a Linux host, create one or more folders for sharing files, then set the shared folders via the virtualbox menu (guest window). 在Linux主机端中，为共享的文件创建一个或更多的文件夹，然后通过Virtualbox菜单中设置（Windows客户端）

在Windows客户端中，从VirtualBox 1.5.0开始，共享文件夹是可浏览的，所以在Windows资源管理器中是可视的。打开Windows资源管理器，在*我的网络位置（My Networking Places） → 整个网络（Entire Network） → VirtualBox Shared Folders（VirtualBox共享文件夹）*。

启动Windows资源管理器（运行资源管理器命令），游览 网络位置（network places） -> （+）号展开： 整个网络（entire network）&rarr； VirtualBox Shared Folders（VirtualBox共享文件夹） &rarr；**\\Vboxsvr** → 然后你就可以在此展开所有已配置的文件夹了，并且在客户端文件系统中为Linux文件夹创建快捷方式。你也可以使用“添加网络位置向导（Add network place wizard）”找到“VBoxsvr”。

此外，在Windows命令行提示符中，你也可以使用以下命令：

```
net use x: \\VBOXSVR\sharename

```

虽然`VBOXSVR`是一个固定名称，但请用你所想要用于共享的盘符替代`x:`，用VBoxManage指定的共享名替换sharename。

在Windows客户端中，为了以VirtualBox共享文件夹改善文件的读取与保存（如MS Office），编辑*c:\windows\system32\drivers\etc\hosts*如下：

```
127.0.0.1 localhost vboxsvr

```

在Linux客户端中，实用以下命令：

```
# mount -t vboxsf [-o OPTIONS] sharename mountpoint
  (注意：共享名是任意的，或者和VirtualBox对话框中选定的一样（在主机端文件系统中共享目录的挂载点）。

```

	自动挂载共享文件夹可以通过Linux客户端 /etc/fstab 文件来实现。你可以指定uid=#,gid=#（# 用实际的数字uid和gid替换），以便以普通用户权限（而不是root权限）来挂载共享文件夹。（这个对于为了在Linux客户端中使用而挂载主机上～/home的一部分是很有用的。为了做到这点，依照以下格式添加一个条目到Linux客户端中的/etc/fstab：

```
sharename mountpoint vboxsf uid=#,gid=# 0 0

```

用在VBoxManage中指定的共享名替换`sharename`，并用你想要共享的路径替换mountpoint（如 /mnt/share）。通常的挂载申请，就是说，如果还没有的话，先创建这个文件夹。注意，如果你已经让VirtualBox“自动挂载”这个共享文件夹，这一步可能就不必了，而且你的文件夹可以在/media 下找到。

除了mount命令提供的标准选项外，以下是可选的：

```
iocharset=CHARSET

```

设置用于I/O操作的字符集（默认utf8），并且：

```
convertcp=CHARSET

```

用于指定用于共享文件夹名称的字符集（默认utf8）

### Clone a virtual disk and assigning a new UUID to it

UUIDs are widely used by VirtualBox. Each virtual machines and each virtual disk of a virtual machine must have a different UUID. When you launch a virtual machine in VirtualBox, the latter will keep track of all UUID of your virtual machine instance. See the [`VBoxManage list`](http://www.virtualbox.org/manual/ch08.html#vboxmanage-list) to list the items registered with VirtualBox.

If you cloned a virtual disk manually by copying the virtual disk file, you will need to assign a new UUID to the cloned virtual drive if you want to use the disk in the same virtual machine or even in another (if that one has already been opened, and thus registered, with VirtualBox).

You can use this command to assign a new UUID to your virtual disk:

```
$ VBoxManage internalcommands sethduuid */path/to/disk.vdi*

```

**Tip:** In the future, to avoid copying the virtual disk and assigning a new UUID to your file manually, use `[VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi)` instead.

**Note:** The commands above supports [all virtual disk formats supported by VirtualBox](#Formats_supported_by_VirtualBox).

## 故障排除

### modprobe Exec 格式错误

确认你使用的是最新系统:

```
pacman -Syu

```

### VERR_ACCESS_DENIED

To access the raw vmdk image on a windows host, run the VirtualBox GUI as administrator.

### pacstrap script fails

If you used *pacstrap* in the [#Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests) to also [#Install the Guest Additions](#Install_the_Guest_Additions) **before** performing a first boot into the new guest, you will need to `umount -l /mnt/dev` as root before using *pacstrap* again; a failure to do this will render it unusable.

### 键盘和鼠标都在我的虚拟机

This means your virtual machine has captured the input of your keyboard and your mouse. Simply press the right `Ctrl` key and your input should control your host again.

To control transparently your virtual machine with your mouse going back and forth your host, without having to press any key, and thus have a seamless integration, install the guest additions inside the guest. Read from the [#Install the Guest Additions](#Install_the_Guest_Additions) step if you guest is Arch Linux, otherwise read the official VirtualBox help.

### 无法发送CTRL + ALT+ Fn键到我的虚拟机

Your guest operating system is a GNU/Linux distribution and you want to open a new TTY shell by hitting `Ctrl+Alt+F2` or exit your current X session with `Ctrl+Alt+Backspace`. If you type these keyboard shortcuts without any adaptation, the guest will not receive any input and the host (if it is a GNU/Linux distribution too) will intercept these shortcut keys. To send `Ctrl+Alt+F2` to the guest for example, simply hit your *Host Key* (usually the right `Ctrl` key) and press `F2` simultaneously.

### 解决ISO映像问题

While VirtualBox can mount ISO images without problem, there are some image formats which cannot reliably be converted to ISO. For instance, ccd2iso ignores .ccd and .sub files, which can give disk images with broken files.

In this case, you will either have to use [CDEmu](/index.php/CDEmu "CDEmu") for Linux inside VirtualBox or any other utility used to mount disk images.

### VirtualBox的GUI没有应用我的GTK主题

See [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications") for information about theming Qt based applications like Virtualbox.

### OpenBSD系统无法使用时，虚拟化指令不可用

While OpenBSD is reported to work fine on other hypervisors without virtualisation instructions (VT-x AMD-V) enabled, an OpenBSD virtual machine running on VirtualBox without these instructions will be unusable, manifesting with a bunch of segmentation faults. Starting VirtualBox with the *-norawr0* argument [may solve the problem](https://www.virtualbox.org/ticket/3947). You can do it like this:

```
$ VBoxSDL -norawr0 -vm *name_of_OpenBSD_VM*

```

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

这种情形可能会在虚拟机没有正常退出时发生，解除锁定虚拟机并不难:

```
$ VBoxManage controlvm *virtual_machine_name* poweroff

```

### USB 子系统在宿主机和虚拟机没有作用

Your user must be in the `vboxusers` group, and you need to install the [extension pack](#Extension_pack) if you want USB 2 support. Then you will be able to enable USB 2 in the VM settings and add one or several filters for the devices you want to access from the guest OS.

Sometimes, on old Linux hosts, the USB subsystem is not auto-detected resulting in an error `Could not load the Host USB Proxy service: VERR_NOT_FOUND` or in a not visible USB drive on the host, [even when the user is in the **vboxusers** group](https://bbs.archlinux.org/viewtopic.php?id=121377). This problem is due to the fact that VirtualBox switched from *usbfs* to *sysfs* in version 3.0.8\. If the host does not understand this change, you can revert to the old behaviour by defining the following environment variable in any file that is sourced by your shell (e.g. your `~/.bashrc` if you are using *bash*):

 `~/.bashrc`  `VBOX_USB=usbfs` 

Then make sure, the environment has been made aware of this change (reconnect, source the file manually, launch a new shell instance or reboot).

Also make sure that your user is a member of the `storage` group.

### 主机模式网络接口创建失败

Make sure all required kernel modules are loaded. See [#Load the VirtualBox kernel modules](#Load_the_VirtualBox_kernel_modules).

To be able to create a Host-Only Network Adapter or a Bridged Network Adapter the kernel modules `vboxnetadp` and `vboxnetflt` need to be loaded, you also need to make sure the [net-tools](https://www.archlinux.org/packages/?name=net-tools) package is installed. It's possible to load these kernel modules manually with

```
# modprobe -a vboxnetadp vboxnetflt

```

若要开机自动加载，每个模块添加一行到 `/etc/modules-load.d/virtualbox.conf`:

```
vboxdrv
vboxnetadp
vboxnetflt

```

**Note:** 以前这些都要添加到 `/etc/rc.conf` 的 `MODULES` 数组，现此方法已过时。

更多信息请看[这个](https://bbs.archlinux.org/viewtopic.php?id=130581)主题。

### WinXP: 位深不能大于 16

若你运行于 16 位色深，图标可能看起来糊糊的。但是当你试图调到更高色深，系统可能会受限于较低的分辨率，甚至根本不允许更改色深。若要修正此问题，运行 `regedit` 并添加下列键值到虚拟 XP 注册表:

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services]
"ColorDepth"=dword:00000004

```

接著在桌面属性窗口改变色深。若没有反应，可透过一些方法强制屏幕重绘 (按下 `Host+F` 重绘/进入全屏)。

### 虚拟系统使用串行端口

确认你的串行端口权限

```
$ /bin/ls -l /dev/ttyS*
crw-rw---- 1 root uucp 4, 64 Feb  3 09:12 /dev/ttyS0
crw-rw---- 1 root uucp 4, 65 Feb  3 09:12 /dev/ttyS1
crw-rw---- 1 root uucp 4, 66 Feb  3 09:12 /dev/ttyS2
crw-rw---- 1 root uucp 4, 67 Feb  3 09:12 /dev/ttyS3

```

添加你的用户到 `uucp` 组。

```
# gpasswd -a $USER uucp 

```

然后重新登陆。

### Windows 8.x Error Code 0x000000C4

If you get this error code while booting, even if you choose OS Type Win 8, try to enable the `CMPXCHG16B` CPU instruction:

```
$ vboxmanage setextradata *virtual_machine_name* VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8, 8.1 or 10 fails to install, boot or has error "ERR_DISK_FULL"

Update the VM's settings by going to *Settings > Storage > Controller:SATA* and check "Use Host I/O Cache".

### Linux guests have slow/distorted audio

The AC97 audio driver within the Linux kernel occasionally guesses the wrong clock settings when running inside Virtual Box, leading to audio that is either too slow or too fast. To fix this, create a file in `/etc/modprobe.d` with the following line:

```
options snd-intel8x0 ac97_clock=48000

```

### 客户端启动后的Xorg死机

Faulty or missing drivers may cause the guest to freeze after starting Xorg, see for example [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) and [[6]](https://bbs.archlinux.org/viewtopic.php?id=156079). Try disabling 3D acceleration in *Settings > Display*, and check if all [Xorg](/index.php/Xorg "Xorg") drivers are installed.

### "NS_ERROR_FAILURE" and missing menu items

If you encounter this message when first time starting the virtual machine:

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

Exit VirtualBox, delete all files of the new machine and from virtualbox config file remove the last line in `MachineRegistry` menu (or the offending machine you are creating):

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

This happens sometimes when selecting *QCOW*/*QCOW2*/*QED* disk format when creating a new virutal disk.

### USB modem

If you have a USB modem which is being used by the guest OS, killing the guest OS can cause the modem to become unusable by the host system. Killing and restarting `VBoxSVC` should fix this problem.

### "The specified path does not exist. Check the path and then try again." error in Windows guests

This error message often appears when running an .exe file which requires administrator priviliges from a shared folder in windows guests. See [the bug report](https://www.virtualbox.org/ticket/5732) for details.

There are several workarounds:

1.  Disable UAC from Control Panel -> Action Center -> "Change User Account Control settings" from left side pane -> set slider to "Never notify" -> OK and reboot
2.  Copy the file from the shared folder to the guest and run from there

Other threads on the internet suggest to add VBOXSVR to the list of trusted sites, but this doesn't work with Windows 7 or newer.

### 挂载失败导致的啟动问题

若你在内核升级后 [systemd](/index.php/Systemd "Systemd") 设定遇到问题，你应该透过 `init=/bin/bash` 开啟系统 (如果应急 shell 对你没有作用)。

```
root=/dev/mapper/vg_main-lv_root ro vga=792 resume=/dev/mapper/vg_main-lv_swap init=/bin/bash

```

接著附加写入权限挂载 *root*-文件系统:

```
# mount / -o remount,rw

```

根据 [#Arch Linux 客户机共享文件夹](#Arch_Linux_.E5.AE.A2.E6.88.B7.E6.9C.BA.E5.85.B1.E4.BA.AB.E6.96.87.E4.BB.B6.E5.A4.B9) 更改 `/etc/fstab`]]，然后在 Bash shell 运行 systemd:

```
# exec /bin/systemd

```

### 复制和粘贴在 Arch Linux 客户机没有作用

Since updating `virtualbox-guest-additions` to version `4.2.0-2` copy&paste from Host OS to Arch Linux Guest stopped working. It seems to be due to `VBoxClient-all` requiring *root* access. In previous versions adding *VBoxClient-all &* to *~/.xinitrc* was sufficient to make copy&paste work. Update *~/.xinitrc* to match `sudo VBoxClient-all &` and add the line `, NOPASSWD: /usr/bin/VBoxClient-all` to your username in the sudoers file and restart X. It should all work again. The line in the sudoers file should look similar to this:

```
 # Allow sudo for user 'you' and let him run VBoxClient-all without requiring a password
 you ALL = PASSWD: ALL, NOPASSWD: /usr/bin/VBoxClient-all

```

**Note:** 使用 `visudo` 编辑 sudoer 文件，这会在存储时检查语法错误。

### 唤醒后异常

有个已知臭虫导致唤醒后异常: [https://www.virtualbox.org/ticket/11289。避开的方法很简单](https://www.virtualbox.org/ticket/11289。避开的方法很简单): 每次都按 Host+q 或菜单关闭虚拟机。

### Btrfs 系统镜像

In 2010 there were reports that OS disk images would not start if they were attached via a virtual SATA device. It was reportedly fixed, and seemed to be. But as of around March 2013, that particular bug report has been [repoened](https://www.virtualbox.org/ticket/6905). This can be fixed by enabling the use of the host I/O cache, which is disabled by default with virtual SATA interfaces.

### vagrant 啟动问题

在最新版的 VirtualBox(4.2.14-1)，运行 `vagrant up` 命令伴随以下错误:

```
Command: ["import",
"/Users/username/.vagrant.d/boxes/precise32/virtualbox/box.ovf"]
Stderr: 0%...10%...20%...30%...40%...50%...60%...70%...80%...90%...100%
Interpreting
/Users/username/.vagrant.d/boxes/precise32/virtualbox/box.ovf...
OK.
0%...
Progress object failure: NS_ERROR_CALL_FAILED

```

在[这个修正](https://www.virtualbox.org/ticket/11895)释出前，你需要使用其它方法解决，或是将 VirtualBox 降级。

有个临时的解决方法是在 `~/.vagrant.d/boxes/BoxName/virtualbox` 為每个 box 创建 manifest:

```
openssl sha1 *.vmdk *.ovf > box.mf

```

你可以降级 VirtualBox。若你的缓存有旧的软件包，可以透过下列命令降级:

```
sudo pacman -U /var/cache/pacman/pkg/virtualbox-4.2.12-3-x86_64.pkg.tar.xz

```

这个错误似乎同时出现在所有平台: [http://www.marshut.com/pzisi/progress-object-failure-ns-error-call-failed-when-running-vagrant-up-in-getting-started-guide.html#qhihz](http://www.marshut.com/pzisi/progress-object-failure-ns-error-call-failed-when-running-vagrant-up-in-getting-started-guide.html#qhihz)

It's unclean for the moment. It could be regression inside Virtualbox or a issue inside Vagrant. When you delete the cache you can downgrade via ArchLinux [downgrader](https://aur.archlinux.org/packages/downgrader/) (I did not test it correctly, but I assume this works, else check the wiki page for downgrading: [Downgrading packages](/index.php/Downgrading_packages "Downgrading packages")

更多信息请到 GitHub issue 页面查看 [Clean install on OS X 10.8.4 w/ latest VirtualBox not working](https://github.com/mitchellh/vagrant/issues/1847)

根据 [Vagrant creator on Twitter](https://twitter.com/mitchellh/status/348886504728305664)，这是 VirtualBox 的臭虫。在 2013 年 06 月 25 日，他说他们在 SVN 修正此臭虫，并且正在等待释出。同时，我可以确认这是跨平台的问题，4.2.14 在我的 Win7 上面是坏的。

这个问题在 virtualbox-4.2.16-1 这份 VirtualBox 版本释出时已解决

### 没有64位客户端选项

When launching a VM client, and no 64-bit options are available, make sure your CPU virtualization capabilities (usually named `VT-x`) are enabled in the BIOS.

### 主机上的虚拟机启动操作系统死机

Possible causes/solutions :

*   SMAP

This is a known incompatiblity with SMAP enabled kernels affecting (mostly) Intel Broadwell chipsets. The matter is currently being investigated, with a wide variety of WIP vboxhost module patches out in the wild that are meant to solve the issue. At the moment of writing though, the only 100% guaranteed solution to this problem is disabling SMAP support in your kernel by appending the "nosmap" option to your kernel boot command line.

*   Hardware Virtualisation

Disabling hardware virtualisation (VT-x/AMD-V) may solve the problem.

*   Various Kernel bugs
    *   Fuse mounted partitions (like ntfs) [[7]](https://bbs.archlinux.org/viewtopic.php?id=185841), [[8]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

Generally, such issues are observed after upgrading VirtualBox or linux kernel. Downgrading them to the previous versions of theirs might solve the problem.

### The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)

When trying to launch a virtual machine, an error message like the following appears:

```
The virtual machine has terminated unexpectedly during startup with exit code 1 (0x1)
NS_ERROR_FAILURE 0x80004005
Component: MachineWrap
Interface: IMachine
```

This may occur after upgrading the [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) or [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) package. Try reloading the `vboxdrv` module:

```
# modprobe -r vboxdrv
# modprobe vboxdrv

```

### Analog microphone not working in guest

If the audio input from an analog microphone is working correctly on the host, but no sound seems to get through to the guest, despite the microphone device apparently being detected normally, installing a [sound server](/index.php/Sound_system#Sound_servers "Sound system") such as [PulseAudio](/index.php/PulseAudio "PulseAudio") on the host might fix the problem.

### Fullscreen mode shows blank guest screen

On some window managers ([i3](/index.php/I3 "I3")), VirtualBox has issues with fullscreen mode properly due to the overlay bar. To workaround this issue, disable "Show in Full-screen/Seamless" option in "Guest Settings --> User Interface --> Mini ToolBar". See [the upstream bug report](https://www.virtualbox.org/ticket/14323) for more information.

### Failed to insert module

If you encounter problem when loading modules as follow:

```
Failed to insert 'vboxdrv': Required key not available

```

Make sure you signed your modules or disable `CONFIG_MODULE_SIG_FORCE` in your kernel config.

## 参阅

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")