相关文章

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [VirtualBox/Tips and tricks](/index.php/VirtualBox/Tips_and_tricks "VirtualBox/Tips and tricks")
*   [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

**翻译状态：** 本文是英文页面 [VirtualBox](/index.php/VirtualBox "VirtualBox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-6-12，点击[这里](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=434334)可以查看翻译后英文页面的改动。

**VirtualBox** 是运行于现有操作系统之上的虚拟机监视器，用途是在特制环境（即虚拟机）里运行操作系统。VirtualBox 处于活跃开发状态，时常会引入新功能。VirtualBox 支持 [Qt](/index.php/Qt "Qt")，[SDL](https://en.wikipedia.org/wiki/SDL "wikipedia:SDL") 与无界面模式运行虚拟机。也支持用 Qt 图形界面和命令行工具管理虚拟机。

为了实现某些主体-客体系统间的整合功能，例如共享目录与剪贴板、显卡加速渲染、无缝窗口整合，VirtualBox 需要在某些系统中安装客体机插件（Guest Addition）。

## Contents

*   [1 在 Arch 里安装 VirtualBox](#.E5.9C.A8_Arch_.E9.87.8C.E5.AE.89.E8.A3.85_VirtualBox)
    *   [1.1 安装基本软件包](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [1.2 模块签名](#.E6.A8.A1.E5.9D.97.E7.AD.BE.E5.90.8D)
    *   [1.3 加载 VirtualBox 内核模块](#.E5.8A.A0.E8.BD.BD_VirtualBox_.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [1.4 从客体系统访问主机 USB 设备](#.E4.BB.8E.E5.AE.A2.E4.BD.93.E7.B3.BB.E7.BB.9F.E8.AE.BF.E9.97.AE.E4.B8.BB.E6.9C.BA_USB_.E8.AE.BE.E5.A4.87)
    *   [1.5 客体机插件光盘](#.E5.AE.A2.E4.BD.93.E6.9C.BA.E6.8F.92.E4.BB.B6.E5.85.89.E7.9B.98)
    *   [1.6 扩展包](#.E6.89.A9.E5.B1.95.E5.8C.85)
    *   [1.7 使用正确的前端](#.E4.BD.BF.E7.94.A8.E6.AD.A3.E7.A1.AE.E7.9A.84.E5.89.8D.E7.AB.AF)
*   [2 在 VirtualBox 中安装 Archlinux](#.E5.9C.A8_VirtualBox_.E4.B8.AD.E5.AE.89.E8.A3.85_Archlinux)
    *   [2.1 以 EFI 模式安装](#.E4.BB.A5_EFI_.E6.A8.A1.E5.BC.8F.E5.AE.89.E8.A3.85)
    *   [2.2 安装客体机插件](#.E5.AE.89.E8.A3.85.E5.AE.A2.E4.BD.93.E6.9C.BA.E6.8F.92.E4.BB.B6)
    *   [2.3 加载 VirtualBox 内核模块](#.E5.8A.A0.E8.BD.BD_VirtualBox_.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97_2)
    *   [2.4 启动 VirtualBox 客体机服务](#.E5.90.AF.E5.8A.A8_VirtualBox_.E5.AE.A2.E4.BD.93.E6.9C.BA.E6.9C.8D.E5.8A.A1)
    *   [2.5 显卡加速](#.E6.98.BE.E5.8D.A1.E5.8A.A0.E9.80.9F)
    *   [2.6 启用共享目录](#.E5.90.AF.E7.94.A8.E5.85.B1.E4.BA.AB.E7.9B.AE.E5.BD.95)
        *   [2.6.1 手动挂载](#.E6.89.8B.E5.8A.A8.E6.8C.82.E8.BD.BD)
        *   [2.6.2 自动挂载](#.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
        *   [2.6.3 按配置于启动时挂载](#.E6.8C.89.E9.85.8D.E7.BD.AE.E4.BA.8E.E5.90.AF.E5.8A.A8.E6.97.B6.E6.8C.82.E8.BD.BD)
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

## 在 Arch 里安装 VirtualBox

以下步骤可以帮你在 Arch 主体系统里安装 VirtualBox

### 安装基本软件包

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") 软件包 [virtualbox](https://www.archlinux.org/packages/?name=virtualbox)。内核模块的安装方式要从下面二选一：

*   如果在用默认的 [linux](https://www.archlinux.org/packages/?name=linux) 内核，建议安装[virtualbox-host-modules-arch](https://www.archlinux.org/packages/?name=virtualbox-host-modules-arch)
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

将需要运行 VirtualBox 的用户名添加到 `vboxusers` [用户组](/index.php/Group "Group")，USB 设备才能被访问。

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

**Warning:** 如果你想把在虚拟机的硬盘镜像放到 [Btrfs](/index.php/Btrfs "Btrfs") 文件系统上，在创建镜像之前，你应该考虑为镜像所处的文件夹关闭[写时复制](/index.php/Btrfs#Copy-on-Write_.28CoW.29 "Btrfs")。

## 在 VirtualBox 中安装 Archlinux

简单来说，在虚拟机的虚拟光驱里加载 Arch Linux 的[安装镜像](https://www.archlinux.org/download/)，然后按照[安装指南](/index.php/Installation_guide_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installation guide (简体中文)")里的步骤继续即可。

### 以 EFI 模式安装

如果你想在 VirtualBox 里以 EFI 模式安装 Arch Linux，这需要在虚拟机的设置窗口里，先从左侧选择 *System*，再从右侧选择 *Motherboard* 标签页，最后勾选 *Enable EFI (special OSes only)* 选项。从安装镜像的启动菜单里选好 Arch Linux 的内核之后，这时启动过程要卡顿一两分钟，之后就能正常进入系统。稍安勿躁。

等系统和 [启动引导程序](/index.php/Boot_loaders_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot loaders (简体中文)")安装成功之后，VirtualBox 会首先尝试从 [ESP](/index.php/ESP "ESP") 加载 `/EFI/BOOT/BOOTX64.EFI`。如果这个首选的文件加载失败，VirtualBox 会从 ESP 根目录尝试加载 EFI shell 脚本 `startup.nsh`。这样来说，为了能顺利进入系统，你需要从下面几种方案选一个：

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

[virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) 包提供了 XDG 自启动项目 `/etc/xdg/autostart/vboxclient.desktop`，这会在登录 X 时自动运行 `VBoxClient-all`。然而，如果你在用的[桌面环境](/index.php/%E6%A1%8C%E9%9D%A2%E7%8E%AF%E5%A2%83 "桌面环境")或[窗口管理器](/index.php/%E7%AA%97%E5%8F%A3%E7%AE%A1%E7%90%86%E5%99%A8 "窗口管理器")不支持 XDG 自启动，那么你就需要手动配置。详见 [Autostarting_(简体中文)#图形程序](/index.php/Autostarting_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.9B.BE.E5.BD.A2.E7.A8.8B.E5.BA.8F "Autostarting (简体中文)")。

至此，你的 Arch Linux 应该能在虚拟机里正常运行了。需要指出的是，某些功能（如剪贴板互通）在 VirtualBox 里是默认禁用的。这需要在各个虚拟机的设置选项里手动开启（*Settings > General > Advanced > Shared Clipboard*）。

### 显卡加速

从 VirtualBox 选项里可以开启显卡加速。已知 [GDM](/index.php/GDM "GDM") 显示管理器从 3.16 版本起会导致显卡加速失效。[[3]](https://bugzilla.gnome.org/show_bug.cgi?id=749390) 如果你遇到类似问题，可以换另一种显示管理器（比如 [LightDM](/index.php/LightDM "LightDM")）试试看。[[4]](https://bbs.archlinux.org/viewtopic.php?id=200025) [[5]](https://bbs.archlinux.org/viewtopic.php?pid=1607593#p1607593)

### 启用共享目录

共享目录的设置在宿主机这边操作。启动 VirtualBox 的图形管理界面，在虚拟机的设置界面的 *Shared Folders* 标签页可以找到相关设置。可以设置的项目包括：目录在宿主机的位置 *Folder Path*，客户机挂载点的名字 *Folder name*，还有 *Read-only*，*Auto-mount*, *Make permanent* 等杂项。还有一种管理方法是使用 `VBoxManage`。详情可以参阅 [VirtualBox 手册](https://www.virtualbox.org/manual/ch04.html#sharedfolders)。

无论用哪一种方法来挂载共享目录，首先都要做些准备工作。

为了避免出现 `/sbin/mount.vboxsf: mounting failed with the error: No such device` 这种错误，首先要确保 `vboxsf` 内核模块已经加载。只要按照前面的步骤在加载客体机里加载内核模块，这一步应该没问题。

为了让挂载之后的目录能让 root 之外的用户也直接读写，还要：

*   安装 [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) 软件包时会创建用户组 `vboxsf`（在前面的步骤就装过了）
*   你的用户需要加入到 `vboxsf` [用户组](/index.php?title=Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87&action=edit&redlink=1 "Users and groups (简体中文 (page does not exist)")

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
*   `dmode`/`fmode` 分别用来指定挂载共享目录之后，下面的子目录与文件的属性。}}

`mount.vboxsf` 尚不支持 `nofail` 挂载参数：

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

Alternately you can use [qemu](https://www.archlinux.org/packages/?name=qemu)'s kernel module that can do this [attrib](http://bethesignal.org/blog/2011/01/05/how-to-mount-virtualbox-vdi-image/):

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

In this case, you will either have to use [CDemu](/index.php/CDemu "CDemu") for Linux inside VirtualBox or any other utility used to mount disk images.

### VirtualBox的GUI没有应用我的GTK主题

See [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for information about theming Qt based applications like Virtualbox.

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

Make sure all required kernel modules are loaded. See [#Load the Virtualbox kernel modules](#Load_the_Virtualbox_kernel_modules).

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

Faulty or missing drivers may cause the guest to freeze after starting Xorg, see for example [[6]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) and [[7]](https://bbs.archlinux.org/viewtopic.php?id=156079). Try disabling 3D acceleration in *Settings > Display*, and check if all [Xorg](/index.php/Xorg "Xorg") drivers are installed.

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
    *   Fuse mounted partitions (like ntfs) [[8]](https://bbs.archlinux.org/viewtopic.php?id=185841), [[9]](https://bugzilla.kernel.org/show_bug.cgi?id=82951#c12)

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