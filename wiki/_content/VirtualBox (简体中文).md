# VirtualBox (简体中文)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

相关文章

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [VirtualBox Extras](/index.php/VirtualBox_Extras "VirtualBox Extras")
*   [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**本页面或部分需要翻译，部分内容可能已经与英文文章脱节。如果您希望贡献翻译，请访问[简体中文翻译组](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")。**

**附注:** please use the first argument of the template to provide more detailed indications.

**翻译状态：** 本文是英文页面 [VirtualBox](/index.php/VirtualBox "VirtualBox") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-7-29，点击[这里](https://wiki.archlinux.org/index.php?title=VirtualBox&diff=0&oldid=389392)可以查看翻译后英文页面的改动。

**VirtualBox** 是类似 [VMware](/index.php/VMware "VMware") 的虚拟 PC 模拟器，处于不断的开发中。使用 [Qt](/index.php/Qt "Qt") 图形界面，提供了无界面运行和 [SDL](https://en.wikipedia.org/wiki/SDL "wikipedia:SDL") 命令行工具进行运行管理。它包含**guest additions**为一些虚拟系统提供附加功能，包括文件共享、剪贴板和图形加速，支持 “无缝” 窗口整合模式。

[Wikipedia:Virtualbox](https://en.wikipedia.org/wiki/Virtualbox "wikipedia:Virtualbox")

## Contents

*   [1 在arch linux的安装步骤](#.E5.9C.A8arch_linux.E7.9A.84.E5.AE.89.E8.A3.85.E6.AD.A5.E9.AA.A4)
    *   [1.1 安装基本软件包](#.E5.AE.89.E8.A3.85.E5.9F.BA.E6.9C.AC.E8.BD.AF.E4.BB.B6.E5.8C.85)
    *   [1.2 安装VirtualBox内核模块](#.E5.AE.89.E8.A3.85VirtualBox.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
        *   [1.2.1 运行官方内核的主机](#.E8.BF.90.E8.A1.8C.E5.AE.98.E6.96.B9.E5.86.85.E6.A0.B8.E7.9A.84.E4.B8.BB.E6.9C.BA)
        *   [1.2.2 定制内核的主机](#.E5.AE.9A.E5.88.B6.E5.86.85.E6.A0.B8.E7.9A.84.E4.B8.BB.E6.9C.BA)
    *   [1.3 加载VirtualBox的内核模块](#.E5.8A.A0.E8.BD.BDVirtualBox.E7.9A.84.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [1.4 添加用户到 vboxusers组](#.E6.B7.BB.E5.8A.A0.E7.94.A8.E6.88.B7.E5.88.B0_vboxusers.E7.BB.84)
    *   [1.5 Guest 附加光盘](#Guest_.E9.99.84.E5.8A.A0.E5.85.89.E7.9B.98)
    *   [1.6 扩展包](#.E6.89.A9.E5.B1.95.E5.8C.85)
    *   [1.7 使用正确的前端](#.E4.BD.BF.E7.94.A8.E6.AD.A3.E7.A1.AE.E7.9A.84.E5.89.8D.E7.AB.AF)
*   [2 安装 Arch Linux的客户端](#.E5.AE.89.E8.A3.85_Arch_Linux.E7.9A.84.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.1 安装Arch Linux在虚拟机内部](#.E5.AE.89.E8.A3.85Arch_Linux.E5.9C.A8.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.86.85.E9.83.A8)
        *   [2.1.1 安装模式为EFI](#.E5.AE.89.E8.A3.85.E6.A8.A1.E5.BC.8F.E4.B8.BAEFI)
    *   [2.2 在 VirtualBox EFI 模式下使用 Arch](#.E5.9C.A8_VirtualBox_EFI_.E6.A8.A1.E5.BC.8F.E4.B8.8B.E4.BD.BF.E7.94.A8_Arch)
    *   [2.3 安装客户端增强包](#.E5.AE.89.E8.A3.85.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.A2.9E.E5.BC.BA.E5.8C.85)
    *   [2.4 Arch Linux 客户端](#Arch_Linux_.E5.AE.A2.E6.88.B7.E7.AB.AF)
        *   [2.4.1 Windows 客户端](#Windows_.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [2.5 安装VirtualBox guest内核模块](#.E5.AE.89.E8.A3.85VirtualBox_guest.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
        *   [2.5.1 运行官方内核Guests](#.E8.BF.90.E8.A1.8C.E5.AE.98.E6.96.B9.E5.86.85.E6.A0.B8Guests)
        *   [2.5.2 运行定制内核Guests](#.E8.BF.90.E8.A1.8C.E5.AE.9A.E5.88.B6.E5.86.85.E6.A0.B8Guests)
    *   [2.6 加载Virtualbox 内核模块](#.E5.8A.A0.E8.BD.BDVirtualbox_.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [2.7 加载VirtualBox guest 服务](#.E5.8A.A0.E8.BD.BDVirtualBox_guest_.E6.9C.8D.E5.8A.A1)
    *   [2.8 启用文件共享](#.E5.90.AF.E7.94.A8.E6.96.87.E4.BB.B6.E5.85.B1.E4.BA.AB)
*   [3 Arch Linux 客户机共享文件夹](#Arch_Linux_.E5.AE.A2.E6.88.B7.E6.9C.BA.E5.85.B1.E4.BA.AB.E6.96.87.E4.BB.B6.E5.A4.B9)
    *   [3.1 和主机系统同步日期](#.E5.92.8C.E4.B8.BB.E6.9C.BA.E7.B3.BB.E7.BB.9F.E5.90.8C.E6.AD.A5.E6.97.A5.E6.9C.9F)
        *   [3.1.1 Systemd](#Systemd)
        *   [3.1.2 手动挂载](#.E6.89.8B.E5.8A.A8.E6.8C.82.E8.BD.BD)
        *   [3.1.3 自动挂载](#.E8.87.AA.E5.8A.A8.E6.8C.82.E8.BD.BD)
        *   [3.1.4 引导时挂载](#.E5.BC.95.E5.AF.BC.E6.97.B6.E6.8C.82.E8.BD.BD)
*   [4 VirtualBox虚拟机从其他虚拟机导入/导出的管理](#VirtualBox.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.BB.8E.E5.85.B6.E4.BB.96.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.AF.BC.E5.85.A5.2F.E5.AF.BC.E5.87.BA.E7.9A.84.E7.AE.A1.E7.90.86)
    *   [4.1 添加删除](#.E6.B7.BB.E5.8A.A0.E5.88.A0.E9.99.A4)
    *   [4.2 使用正确的虚拟磁盘格式](#.E4.BD.BF.E7.94.A8.E6.AD.A3.E7.A1.AE.E7.9A.84.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98.E6.A0.BC.E5.BC.8F)
        *   [4.2.1 自动工具](#.E8.87.AA.E5.8A.A8.E5.B7.A5.E5.85.B7)
        *   [4.2.2 手动转换](#.E6.89.8B.E5.8A.A8.E8.BD.AC.E6.8D.A2)
    *   [4.3 创建虚拟机的配置为你的虚拟机管理程序](#.E5.88.9B.E5.BB.BA.E8.99.9A.E6.8B.9F.E6.9C.BA.E7.9A.84.E9.85.8D.E7.BD.AE.E4.B8.BA.E4.BD.A0.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA.E7.AE.A1.E7.90.86.E7.A8.8B.E5.BA.8F)
*   [5 虚拟磁盘管理](#.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98.E7.AE.A1.E7.90.86)
    *   [5.1 支持VirtualBox的格式](#.E6.94.AF.E6.8C.81VirtualBox.E7.9A.84.E6.A0.BC.E5.BC.8F)
    *   [5.2 磁盘映像格式转换](#.E7.A3.81.E7.9B.98.E6.98.A0.E5.83.8F.E6.A0.BC.E5.BC.8F.E8.BD.AC.E6.8D.A2)
        *   [5.2.1 VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK)
        *   [5.2.2 VHD to VDI and VDI to VDH](#VHD_to_VDI_and_VDI_to_VDH)
        *   [5.2.3 QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2)
*   [6 从其他虚拟机中迁移](#.E4.BB.8E.E5.85.B6.E4.BB.96.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.B8.AD.E8.BF.81.E7.A7.BB)
    *   [6.1 从QEMU映像转换](#.E4.BB.8EQEMU.E6.98.A0.E5.83.8F.E8.BD.AC.E6.8D.A2)
    *   [6.2 从VMware映像转换](#.E4.BB.8EVMware.E6.98.A0.E5.83.8F.E8.BD.AC.E6.8D.A2)
    *   [6.3 挂载虚拟磁盘](#.E6.8C.82.E8.BD.BD.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98)
        *   [6.3.1 VDI](#VDI)
    *   [6.4 压缩磁盘映像](#.E5.8E.8B.E7.BC.A9.E7.A3.81.E7.9B.98.E6.98.A0.E5.83.8F)
    *   [6.5 增加虚拟磁盘](#.E5.A2.9E.E5.8A.A0.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98)
    *   [6.6 从.vbox文件中手动更换虚拟磁盘](#.E4.BB.8E.vbox.E6.96.87.E4.BB.B6.E4.B8.AD.E6.89.8B.E5.8A.A8.E6.9B.B4.E6.8D.A2.E8.99.9A.E6.8B.9F.E7.A3.81.E7.9B.98)
        *   [6.6.1 Linux主机和其他操作系统之间的转移](#Linux.E4.B8.BB.E6.9C.BA.E5.92.8C.E5.85.B6.E4.BB.96.E6.93.8D.E4.BD.9C.E7.B3.BB.E7.BB.9F.E4.B9.8B.E9.97.B4.E7.9A.84.E8.BD.AC.E7.A7.BB)
*   [7 配置](#.E9.85.8D.E7.BD.AE)
    *   [7.1 网络](#.E7.BD.91.E7.BB.9C)
        *   [7.1.1 NAT](#NAT)
        *   [7.1.2 桥接](#.E6.A1.A5.E6.8E.A5)
    *   [7.2 主机端和客户端之间的键盘和鼠标](#.E4.B8.BB.E6.9C.BA.E7.AB.AF.E5.92.8C.E5.AE.A2.E6.88.B7.E7.AB.AF.E4.B9.8B.E9.97.B4.E7.9A.84.E9.94.AE.E7.9B.98.E5.92.8C.E9.BC.A0.E6.A0.87)
    *   [7.3 主机端和客户端间的共享文件夹](#.E4.B8.BB.E6.9C.BA.E7.AB.AF.E5.92.8C.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.97.B4.E7.9A.84.E5.85.B1.E4.BA.AB.E6.96.87.E4.BB.B6.E5.A4.B9)
    *   [7.4 Clone a virtual disk and assigning a new UUID to it](#Clone_a_virtual_disk_and_assigning_a_new_UUID_to_it)
*   [8 高级配置](#.E9.AB.98.E7.BA.A7.E9.85.8D.E7.BD.AE)
    *   [8.1 虚拟机管理启动](#.E8.99.9A.E6.8B.9F.E6.9C.BA.E7.AE.A1.E7.90.86.E5.90.AF.E5.8A.A8)
        *   [8.1.1 启动虚拟机服务](#.E5.90.AF.E5.8A.A8.E8.99.9A.E6.8B.9F.E6.9C.BA.E6.9C.8D.E5.8A.A1)
        *   [8.1.2 启动虚拟机键盘快捷键](#.E5.90.AF.E5.8A.A8.E8.99.9A.E6.8B.9F.E6.9C.BA.E9.94.AE.E7.9B.98.E5.BF.AB.E6.8D.B7.E9.94.AE)
    *   [8.2 在虚拟机中使用特定的设备](#.E5.9C.A8.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.B8.AD.E4.BD.BF.E7.94.A8.E7.89.B9.E5.AE.9A.E7.9A.84.E8.AE.BE.E5.A4.87)
    *   [8.3 使用 USB 摄像头 / 麦克风](#.E4.BD.BF.E7.94.A8_USB_.E6.91.84.E5.83.8F.E5.A4.B4_.2F_.E9.BA.A6.E5.85.8B.E9.A3.8E)
        *   [8.3.1 获得可探测的Web-cam和其他USB设备](#.E8.8E.B7.E5.BE.97.E5.8F.AF.E6.8E.A2.E6.B5.8B.E7.9A.84Web-cam.E5.92.8C.E5.85.B6.E4.BB.96USB.E8.AE.BE.E5.A4.87)
    *   [8.4 访问guest 服务](#.E8.AE.BF.E9.97.AEguest_.E6.9C.8D.E5.8A.A1)
    *   [8.5 在Windows客户端中激活D3D加速](#.E5.9C.A8Windows.E5.AE.A2.E6.88.B7.E7.AB.AF.E4.B8.AD.E6.BF.80.E6.B4.BBD3D.E5.8A.A0.E9.80.9F)
    *   [8.6 在USB key上使用VirtualBox](#.E5.9C.A8USB_key.E4.B8.8A.E4.BD.BF.E7.94.A8VirtualBox)
    *   [8.7 Run a native Arch Linux installation inside VirtualBox](#Run_a_native_Arch_Linux_installation_inside_VirtualBox)
        *   [8.7.1 Make sure you have a persistent naming scheme](#Make_sure_you_have_a_persistent_naming_scheme)
        *   [8.7.2 Make sure your mkinitcpio image is correct](#Make_sure_your_mkinitcpio_image_is_correct)
        *   [8.7.3 Create a VM configuration to boot from the physical drive](#Create_a_VM_configuration_to_boot_from_the_physical_drive)
            *   [8.7.3.1 创建一个原始只读磁盘的.vmdk映像](#.E5.88.9B.E5.BB.BA.E4.B8.80.E4.B8.AA.E5.8E.9F.E5.A7.8B.E5.8F.AA.E8.AF.BB.E7.A3.81.E7.9B.98.E7.9A.84.vmdk.E6.98.A0.E5.83.8F)
            *   [8.7.3.2 创建虚拟机配置文件](#.E5.88.9B.E5.BB.BA.E8.99.9A.E6.8B.9F.E6.9C.BA.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
        *   [8.7.4 Install the Guest Additions](#Install_the_Guest_Additions)
    *   [8.8 安装VirtualBox的本地Arch Linux系统](#.E5.AE.89.E8.A3.85VirtualBox.E7.9A.84.E6.9C.AC.E5.9C.B0Arch_Linux.E7.B3.BB.E7.BB.9F)
    *   [8.9 将本机Windows安装到虚拟机](#.E5.B0.86.E6.9C.AC.E6.9C.BAWindows.E5.AE.89.E8.A3.85.E5.88.B0.E8.99.9A.E6.8B.9F.E6.9C.BA)
        *   [8.9.1 Tasks on Windows](#Tasks_on_Windows)
        *   [8.9.2 Tasks on GNU/Linux](#Tasks_on_GNU.2FLinux)
        *   [8.9.3 修复MBR和Microsoft引导](#.E4.BF.AE.E5.A4.8DMBR.E5.92.8CMicrosoft.E5.BC.95.E5.AF.BC)
        *   [8.9.4 已知的限制](#.E5.B7.B2.E7.9F.A5.E7.9A.84.E9.99.90.E5.88.B6)
*   [9 故障排除](#.E6.95.85.E9.9A.9C.E6.8E.92.E9.99.A4)
    *   [9.1 modprobe Exec 格式错误](#modprobe_Exec_.E6.A0.BC.E5.BC.8F.E9.94.99.E8.AF.AF)
    *   [9.2 VERR_ACCESS_DENIED](#VERR_ACCESS_DENIED)
    *   [9.3 键盘和鼠标都在我的虚拟机](#.E9.94.AE.E7.9B.98.E5.92.8C.E9.BC.A0.E6.A0.87.E9.83.BD.E5.9C.A8.E6.88.91.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [9.4 无法发送CTRL + ALT+ Fn键到我的虚拟机](#.E6.97.A0.E6.B3.95.E5.8F.91.E9.80.81CTRL_.2B_ALT.2B_Fn.E9.94.AE.E5.88.B0.E6.88.91.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [9.5 解决ISO映像问题](#.E8.A7.A3.E5.86.B3ISO.E6.98.A0.E5.83.8F.E9.97.AE.E9.A2.98)
    *   [9.6 VirtualBox的GUI没有应用我的GTK主题](#VirtualBox.E7.9A.84GUI.E6.B2.A1.E6.9C.89.E5.BA.94.E7.94.A8.E6.88.91.E7.9A.84GTK.E4.B8.BB.E9.A2.98)
    *   [9.7 OpenBSD系统无法使用时，虚拟化指令不可用](#OpenBSD.E7.B3.BB.E7.BB.9F.E6.97.A0.E6.B3.95.E4.BD.BF.E7.94.A8.E6.97.B6.EF.BC.8C.E8.99.9A.E6.8B.9F.E5.8C.96.E6.8C.87.E4.BB.A4.E4.B8.8D.E5.8F.AF.E7.94.A8)
    *   [9.8 VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)](#VBOX_E_INVALID_OBJECT_STATE_.280x80BB0007.29)
    *   [9.9 USB 子系统在宿主机和虚拟机没有作用](#USB_.E5.AD.90.E7.B3.BB.E7.BB.9F.E5.9C.A8.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.92.8C.E8.99.9A.E6.8B.9F.E6.9C.BA.E6.B2.A1.E6.9C.89.E4.BD.9C.E7.94.A8)
    *   [9.10 主机模式网络接口创建失败](#.E4.B8.BB.E6.9C.BA.E6.A8.A1.E5.BC.8F.E7.BD.91.E7.BB.9C.E6.8E.A5.E5.8F.A3.E5.88.9B.E5.BB.BA.E5.A4.B1.E8.B4.A5)
    *   [9.11 WinXP: 位深不能大于 16](#WinXP:_.E4.BD.8D.E6.B7.B1.E4.B8.8D.E8.83.BD.E5.A4.A7.E4.BA.8E_16)
    *   [9.12 虚拟系统使用串行端口](#.E8.99.9A.E6.8B.9F.E7.B3.BB.E7.BB.9F.E4.BD.BF.E7.94.A8.E4.B8.B2.E8.A1.8C.E7.AB.AF.E5.8F.A3)
    *   [9.13 Windows 8.x Error Code 0x000000C4](#Windows_8.x_Error_Code_0x000000C4)
    *   [9.14 Windows 8 VM fails to boot with error "ERR_DISK_FULL"](#Windows_8_VM_fails_to_boot_with_error_.22ERR_DISK_FULL.22)
    *   [9.15 Linux guests have slow/distorted audio](#Linux_guests_have_slow.2Fdistorted_audio)
    *   [9.16 客户端启动后的Xorg死机](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.90.AF.E5.8A.A8.E5.90.8E.E7.9A.84Xorg.E6.AD.BB.E6.9C.BA)
    *   [9.17 "NS_ERROR_FAILURE" and missing menu items](#.22NS_ERROR_FAILURE.22_and_missing_menu_items)
    *   [9.18 USB modem](#USB_modem)
    *   [9.19 "The specified path does not exist. Check the path and then try again." error in Windows guests](#.22The_specified_path_does_not_exist._Check_the_path_and_then_try_again..22_error_in_Windows_guests)
    *   [9.20 挂载失败导致的啟动问题](#.E6.8C.82.E8.BD.BD.E5.A4.B1.E8.B4.A5.E5.AF.BC.E8.87.B4.E7.9A.84.E5.95.9F.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [9.21 复制和粘贴在 Arch Linux 客户机没有作用](#.E5.A4.8D.E5.88.B6.E5.92.8C.E7.B2.98.E8.B4.B4.E5.9C.A8_Arch_Linux_.E5.AE.A2.E6.88.B7.E6.9C.BA.E6.B2.A1.E6.9C.89.E4.BD.9C.E7.94.A8)
    *   [9.22 唤醒后异常](#.E5.94.A4.E9.86.92.E5.90.8E.E5.BC.82.E5.B8.B8)
    *   [9.23 Btrfs 系统镜像](#Btrfs_.E7.B3.BB.E7.BB.9F.E9.95.9C.E5.83.8F)
    *   [9.24 vagrant 啟动问题](#vagrant_.E5.95.9F.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [9.25 没有64位客户端选项](#.E6.B2.A1.E6.9C.8964.E4.BD.8D.E5.AE.A2.E6.88.B7.E7.AB.AF.E9.80.89.E9.A1.B9)
    *   [9.26 主机上的虚拟机启动操作系统死机](#.E4.B8.BB.E6.9C.BA.E4.B8.8A.E7.9A.84.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.90.AF.E5.8A.A8.E6.93.8D.E4.BD.9C.E7.B3.BB.E7.BB.9F.E6.AD.BB.E6.9C.BA)
    *   [9.27 向客户端发送CTRL+ALT+F1](#.E5.90.91.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.8F.91.E9.80.81CTRL.2BALT.2BF1)
    *   [9.28 在运行于无显示器的服务器上的系统上启动虚拟机](#.E5.9C.A8.E8.BF.90.E8.A1.8C.E4.BA.8E.E6.97.A0.E6.98.BE.E7.A4.BA.E5.99.A8.E7.9A.84.E6.9C.8D.E5.8A.A1.E5.99.A8.E4.B8.8A.E7.9A.84.E7.B3.BB.E7.BB.9F.E4.B8.8A.E5.90.AF.E5.8A.A8.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [9.29 从主机端访问虚拟机上的服务器](#.E4.BB.8E.E4.B8.BB.E6.9C.BA.E7.AB.AF.E8.AE.BF.E9.97.AE.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.B8.8A.E7.9A.84.E6.9C.8D.E5.8A.A1.E5.99.A8)
    *   [9.30 守护进程工具](#.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B.E5.B7.A5.E5.85.B7)
*   [10 参阅](#.E5.8F.82.E9.98.85)

## 在arch linux的安装步骤

为了启动的VirtualBox虚拟机在您的Arch Linux中，按照下列安装步骤。

### 安装基本软件包

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)") GPL 版本的 [virtualbox](https://www.archlinux.org/packages/?name=virtualbox) 软件包。作为依赖安装的 [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) 包含了archlinux 默认内核使用的模块。

如果使用[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)内核，需要安装[virtualbox-host-modules-lts](https://www.archlinux.org/packages/?name=virtualbox-host-modules-lts).

要使用基于 [Qt](/index.php/Qt "Qt") 的 `VirtualBox` 命令，需要安装 [qt4](https://www.archlinux.org/packages/?name=qt4) 软件包。如果使用简单的基于 SDL 的 `VBoxSDL` 命令或者 `VBoxHeadless` 命令，则不需要安装 [qt4](https://www.archlinux.org/packages/?name=qt4)。

### 安装VirtualBox内核模块

Next, to fully virtualize your guest installation, VirtualBox provides the following [kernel modules](/index.php/Kernel_modules "Kernel modules"): `vboxdrv`, `vboxnetadp`, `vboxnetflt`, and `vboxpci`. These must be added to your host kernel.

The binary compatibility of kernel modules depends on the API of the kernel against which they have been compiled. The problem with the Linux kernel is that these interfaces might not be the same from one kernel version to another. In order to avoid compatibility problems and subtle bugs, each time the Linux kernel is upgraded, it is advised to recompile the kernel modules against the Linux kernel version that has just been installed. This is what Arch Linux packagers actually do with the VirtualBox kernel modules packages: each time a new Arch Linux kernel is released, the Virtualbox modules are upgraded accordingly.

Therefore, if you are using a kernel from the [official repositories](/index.php/Official_repositories "Official repositories") or a custom one (self-compiled or installed from the [AUR](/index.php/AUR "AUR")), the kernel module package you will need to install will thus vary.

#### 运行官方内核的主机

*   如果你使用的是 [linux](https://www.archlinux.org/packages/?name=linux) 内核, 当你安装 [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) 软件包的时候，需要安装[virtualbox](https://www.archlinux.org/packages/?name=virtualbox) package.
*   如果你使用的是 LTS 稳定内核 ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), 你需要安装 [virtualbox-host-modules-lts](https://www.archlinux.org/packages/?name=virtualbox-host-modules-lts) 软件包。 [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules) 现在可以移除。
*   如果你使用的是 [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup> kernel, 需要构建 [virtualbox-ck-host-modules](https://aur.archlinux.org/packages/virtualbox-ck-host-modules/)<sup><small>AUR</small></sup> 软件包。

#### 定制内核的主机

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Dynamic Kernel Module Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support").**

**Notes:** The general tips on DKMS usage do not belong on this page. (Discuss in [Talk:VirtualBox (简体中文)#](https://wiki.archlinux.org/index.php/Talk:VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

If you use or intend to use a self-compiled kernel from sources, you have to know that VirtualBox does not require any virtualization modules (e.g. virtuo, kvm,...). The VirtualBox kernel modules provide all the necessary for VirtualBox to work properly. You can thus disable in your kernel _.config_ file these virtualization modules if you do not use other hypervisors like Xen, KVM or QEMU.

The `virtualbox-host-modules` package works fine with custom kernels of the same version of the Arch Linux stock kernel such as [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup>. Since the `virtualbox-host-modules` comes with the official Arch Linux kernel ([linux](https://www.archlinux.org/packages/?name=linux)) as a dependency and if you do not use that kernel, install [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) instead.

If you are using a custom kernel which is not of the same version of the Arch Linux stock one, you will have to install the [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) too. The latter comes bundled with the source of the VirtualBox kernel modules that will be compiled to generate these modules for your kernel.

As the [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) package requires compilation, make sure you have the kernel headers corresponding to your custom kernel version to prevent this error from happening `Your kernel headers for kernel _your custom kernel version_ cannot be found at /usr/lib/modules/_your custom kernel version_/build or /usr/lib/modules/_your custom kernel version_/source`.

*   If you use a self-compiled kernel and have used `make modules_install` to install its modules, folders `/usr/lib/modules/_your custom kernel version_/build` and `(...)/source` will be symlinked to your kernel sources. These will act as the kernel headers you need. If you have not removed these kernel sources yet, you have nothing to do.
*   If you use a custom kernel from [AUR](/index.php/AUR "AUR"), make sure the package [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) is installed.

一旦[virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) 安装完成后，只要用下面命令生成内核模块：

```
# dkms install vboxhost/<virtualbox-host-source 版本> -k <你的自制内核模块版本>/<你的架构>

```

**Tip:** 懒人做法是键入以下命令: `# dkms install vboxhost/$(pacman -Q virtualbox|awk '{print $2}'|sed 's/\-.\+//') -k $(uname -rm|sed 's/\ /\//')` 

To automatically recompile the VirtualBox kernel modules when their sources get upgraded (i.e. when the [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) package gets upgraded) and avoid to type again the above `dkms install` command manually afterwards, enable the `dkms` service with:

```
# systemctl enable dkms.service

```

If this service is not enabled while the [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) package is being updated, the VirtualBox modules will not be updated and you will have to type in manually the `dkms install` command described above to compile the latest version of the Virtualbox kernel modules. If you do not want to type in manually this command, if the `dkms` service is automatically loaded at startup, you just need to reboot and your VirtualBox modules will be recompiled silently.

However, if you want to keep this daemon disabled, you can use an [initramfs hook](/index.php/Mkinitcpio "Mkinitcpio") that will automatically trigger the `dkms install` command described above at boot time. This will require a reboot to recompile the VirtualBox modules. To enable this hook, install the [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/)<sup><small>AUR</small></sup> package and add `vboxhost` to your HOOKS array in `/etc/mkinitcpio.conf`. Again, make sure the right linux headers are available for the new kernel otherwise the compilation will fail.

**Tip:** Like the `dkms` command, the `vboxhost` hook will tell you if anything goes wrong during the recompilation of the VirtualBox modules.

### 加载VirtualBox的内核模块

```
VirtualBox 在 Linux 上运行需要使用自己的[内核模块](/index.php/Kernel_modules "Kernel modules")，包括一个必须的 **vboxdrv**。这个模块必须在虚拟机运行前启动。如果需要，可以在 Arch Linux 启动时自动加载。

```

手动加载模块:

```
# modprobe vboxdrv

```

若要启动时加载 VirtualBox 驱动，在 `/etc/[modules-load.d](/index.php/Kernel_modules#Loading "Kernel modules")` 创建 `*.conf` 文件 (例如：`virtualbox.conf`)，包括所有应加载的模块:

 `/etc/modules-load.d/virtualbox.conf`  `vboxdrv` 

**Note:** You may need to update the kernel modules db in order to avoid 'no such file or directory' error when loading vboxdrv. Run: `depmod -a`.

启动 VirtualBox 图形管理员:

```
$VirtualBox

```

以下模块是可选的，但建议选上如果您不想在进行一些高级配置时被打扰(如下): `vboxnetadp`, `vboxnetflt` 和`vboxpci`.

*   `vboxnetadp` 和`vboxnetflt` 都是需要的当你使用网桥时 [bridged](https://www.virtualbox.org/manual/ch06.html#network_bridged) or [host-only networking](https://www.virtualbox.org/manual/ch06.html#network_hostonly) feature. More precisely, `vboxnetadp` is needed to create the host interface in the VirtualBox global preferences, and `vboxnetflt` is needed to launch a virtual machine using that network interface.

*   `vboxpci`是需要的， 当你的虚拟机需要使用一个你的主机上的pci设备时

**Note:** If the VirtualBox kernel modules were loaded in the kernel while you updated the modules, you need to reload them manually to use the new updated version. To do it, run `vboxreload` as root.

Finally, if you use the aforementioned "Host-only" or "bridge networking" feature, make sure [net-tools](https://www.archlinux.org/packages/?name=net-tools) is installed. VirtualBox actually uses `ifconfig` and `route` to assign the IP and route to the host interface configured with `VBoxManage hostonlyif` or via the GUI in _Settings > Network > Host-only Networks > Edit host-only network (space) > Adapter_.

### 添加用户到 vboxusers组

将需要运行 Virtualbox 的用户名添加到 **vboxusers** [用户组](/index.php/Group "Group")，文件夹共享和其它功能需要正确的组才能工作。新组设置不会应用到当前会话，请重新登录或者通过命令 `newgrp` 或 `sudo -u _username_ -s` 启动一个新环境。

```
# gpasswd -a $USER vboxusers

```

### Guest 附加光盘

建议在运行VirtualBox 的主机系统上安装[virtualbox-guest-iso](https://www.archlinux.org/packages/?name=virtualbox-guest-iso) 软件包 。 这个包是一个磁盘镜像，用来安装虚拟系统的附加功能。 The _.iso_ file will be located at `/usr/lib/virtualbox/additions/VBoxGuestAdditions.iso`, and may have to be mounted manually inside the virtual machine. Once mounted, you can run the guest additions installer inside the guest.

### 扩展包

Since VirtualBox 4.0, non-GPL components have been split from the rest of the application. Despite being released under a non-free license and **being only available for personal use**, you might be interested in installing the Oracle Extension Pack which provides [additional features](https://www.virtualbox.org/manual/ch01.html#intro-installing). To avoid manual manipulation, the [virtualbox-ext-oracle](https://aur.archlinux.org/packages/virtualbox-ext-oracle/)<sup><small>AUR</small></sup> package is available, and a prebuilt version can be found in the [seblu](/index.php/Unofficial_user_repositories#seblu "Unofficial user repositories") repository.

If you prefer to use the traditional and manual way: download the extension manually and install it via the GUI (_File > Preferences > Extensions_) or via `VBoxManage extpack install <.vbox-extpack>`, make sure you have a toolkit (like [Polkit](/index.php/Polkit "Polkit"), gksu, etc.) to grant privileged access to VirtualBox. The installation of this extension [requires root access](https://www.virtualbox.org/ticket/8473).

### 使用正确的前端

现在，你已经准备好使用VirtualBox的。祝贺!

多个前端提供给您，其中两个是默认提供:

*   If you want to use VirtualBox in command-line only (only launch and change settings of existing virtual machines), you can use the `VBoxSDL` command. VBoxSDL does only provide a simple window that contains only the _pure_ virtual machine, without menus or other controls.
*   If you want to use VirtualBox in command-line without any GUI running (e.g. on a server) to create, launch and configure virtual machines, use the `VBoxHeadless` which produces no visible output on the host at all, but instead only delivers VRDP data.

If you installed the [qt4](https://www.archlinux.org/packages/?name=qt4) optional dependency, you can run `VirtualBox` and have a nice-looking GUI interface with menus usable via the mouse.

Finally, you can use [PhpVirtualBox](/index.php/PhpVirtualBox "PhpVirtualBox") to administrate your virtual machines via a web interface.

Refer to the [VirtualBox manual](https://www.virtualbox.org/manual) to learn how to create virtual machines.

**Warning:** If you intend to store virtual disk images on a [Btrfs](/index.php/Btrfs "Btrfs") file system, before creating any images, you should consider disabling [Copy-on-Write](/index.php/Btrfs#Copy-On-Write_.28CoW.29 "Btrfs") for the destination directory of these images.

## 安装 Arch Linux的客户端

### 安装Arch Linux在虚拟机内部

在 VirtualBox 中安装 Arch 非常简单直接，而且最好通过 pacman 安装 Guest Addition，不要使用 VirtualBox 中的 "Install Guest Additions" 或挂载的 ISO 安装。

**Note:** Windows 8+ or Server 2008+ hosts may have to disable Hyper-V in order to use hardware virtualization features and create 64 bit virtual machines in VirtualBox. To learn how to disable or re-enable Hyper-V [see this Super User post](https://superuser.com/questions/684966/switch-off-hyper-v-without-disable-functionality-in-windows-8-1).

Boot the Arch installation media through one of the virtual machine's virtual drives. Then, complete the installation of a basic Arch system as explained in the [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide") or the [Installation guide](/index.php/Installation_guide "Installation guide") without installing any graphic driver: we will install one provided by VirtualBox just at the next step.

#### 安装模式为EFI

If you want to install Arch Linux in EFI mode inside VirtualBox, in the settings of the virtual machine, go in the _Settings_ tab, and check the checkbox _Enable EFI (special OSes only)_. After selecting the kernel from the Arch Linux installation media's menu, the media will hang for a minute or two and will continue to boot the kernel normally afterwards. Be patient.

When booting in EFI mode, VirtualBox will first attempt to run `/EFI/BOOT/BOOTX64.EFI` from the ESP. If that first option fails, VirtualBox will then try the EFI shell script `startup.nsh` from the root of the ESP. Unless you want to manually launch your bootloader from the EFI shell every time, you will need to move your bootloader to that default path. Do not bother with the VirtualBox Boot Manager (accessible with `F2` at boot): EFI entries added to it manually at boot or with [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr) will persist after a reboot [but are lost when the VM is shut down](https://www.virtualbox.org/ticket/11177).

### 在 VirtualBox EFI 模式下使用 Arch

我对这方面的设置有非常不好的经历，但是依然可以办到。

_UPD. Using efibootmgr has the same effect as using VirtualBox boot menu (see the note below): settings [disappear](https://www.virtualbox.org/ticket/11177) after VM shutdown._首先要说的是 `efibootmgr` *完全无效*。虽然看起来是正常的，但是所有更动似乎在重啟后就失效。在进行正常 UEFI/GPT 安装后重啟，你会被丢到 EFI shell。送出 exit 后会看到菜单，选中 Boot Management Manager -> Boot Options -> Add Boot Option。使用文件浏览器找到 grub efi 文件并选中，添加你要的标签。之后，菜单选中 Change Boot Order，使用方向键选中你的 Arch 选项，按下 `+` 移到最上方。现在 GRUB 应该默认啟动了。

其它选项: 1) 将引导程序移到 `\EFI\boot\bootx64.efi`, 2) 创建 `\startup.nsh` 脚本，运行选定的引导程序，就像这样:

 `\startup.nsh`  `HD16a0a1:\EFI\refind\refindx64.efi` 

Here I'm using consistent mapping name (HD16a0a1). It is probably a good idea, because they do survive configuration changes.

**Note:** Another useful way to get back to the EFI menu after autobooting is working is to press the `C` key inside GRUB and type `exit`. Obviously, this will only work with `grub-efi`, not `grub-bios`.  

Regenerating the `grub.cfg` file may also be required to fix broken UUIDs. Check with the `lsblk -f` command that they match.  

Yet another useful way to get to VirtualBox boot menu is pressing `F12` right after starting virtual machine. It comes in handy when using rEFInd + EFISTUB, for example.

### 安装客户端增强包

客户端增强包（The Guest Additions）能够激活共享文件夹功能，改善显卡加速支持和在主机端及客户端之间启用双向剪贴板。鼠标集成是另一项功能，用于减少在客户端中使用鼠标后将其释放的需要。

After completing the installation of the guest system, install the VirtualBox [Guest Additions](https://www.virtualbox.org/manual/ch04.html) which include drivers and applications that optimize the guest operating system. These can be installed via [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils), which provides [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) as a required dependency.

**Note:** The method described in the [VirtualBox manual](https://www.virtualbox.org/manual/ch04.html#idp54932560) does not work on Arch Linux guests, resulting in an `Unable to determine your Linux distribution` repeated several times as error message. If you tried this method first and you use the right solution described above afterwards, this will fail. You will get a [file conflict](/index.php/Pacman#.22Failed_to_commit_transaction_.28conflicting_files.29.22_error "Pacman"): `/usr/bin/VBox*` and `/usr/lib/VBox* exists in filesystem`. The solution is to remove the offending files first with `rm /usr/bin/VBox* /usr/lib/VBox*` as root. These files are actually symbolic links to the location where the additions tools were installed; by default, this is `/opt/VBoxGuestAdditions-_version number_`. Remove these files too with `rm -r /opt/VBoxGuestAdditions-_version number_` as they are not needed. Now you can restart the installation from the right method above.

### Arch Linux 客户端

参阅Arch Linux VirtualBox客户端

#### Windows 客户端

在你的虚拟机中安装Windows（XP 等等）后，只需选择_设备 → 安装增强功能_

这将会挂载ISO镜像，接着Windows应该自动运行客户端增强包安装向导（The guest additions installer）。按照说明进行到底。

### 安装VirtualBox guest内核模块

#### 运行官方内核Guests

*   If you are using the [linux](https://www.archlinux.org/packages/?name=linux) kernel, make sure the [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) package is still installed. The latter has been installed when you installed the [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) package.
*   If you are using the LTS version of the kernel ([linux-lts](https://www.archlinux.org/packages/?name=linux-lts)), you need to install the [virtualbox-guest-modules-lts](https://www.archlinux.org/packages/?name=virtualbox-guest-modules-lts) package. [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) can now be removed if you want.
*   If you are using the [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup>, kernel, build the [virtualbox-ck-guest-modules](https://aur.archlinux.org/packages/virtualbox-ck-guest-modules/)<sup><small>AUR</small></sup> package. [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules) can now be removed in this case too, if you want.

#### 运行定制内核Guests

As this installation step is quite similar to the Vitualbox kernel modules section for the host described above, please refer to [that section](#Install_the_VirtualBox_kernel_modules) for more information and replace all [virtualbox-host-modules](https://www.archlinux.org/packages/?name=virtualbox-host-modules), [virtualbox-host-dkms](https://www.archlinux.org/packages/?name=virtualbox-host-dkms) and [vboxhost-hook](https://aur.archlinux.org/packages/vboxhost-hook/)<sup><small>AUR</small></sup> statements by [virtualbox-guest-modules](https://www.archlinux.org/packages/?name=virtualbox-guest-modules), [virtualbox-guest-dkms](https://www.archlinux.org/packages/?name=virtualbox-guest-dkms) and [vboxguest-hook](https://aur.archlinux.org/packages/vboxguest-hook/)<sup><small>AUR</small></sup> respectively.

### 加载Virtualbox 内核模块

手动加载内核模块：

```
# modprobe -a vboxguest vboxsf vboxvideo

```

开机时自动加载VirtualBox模块[Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules") 创建`*.conf` 文件 (e.g. `virtualbox.conf`) 在`/etc/modules-load.d/` 加入如下几行:

 `/etc/modules-load.d/virtualbox.conf` 

```
vboxguest
vboxsf
vboxvideo
```

Alternatively, [enable](/index.php/Enable "Enable") the `vboxservice` service which loads the modules and synchronizes the guest's system time with the host.

### 加载VirtualBox guest 服务

After the rather big installation step dealing with VirtualBox kernel modules, now you need to start the guest services. The guest services are actually just a binary executable called `VBoxClient` which will interact with your X Window System. `VBoxClient` manages the following features:

*   shared clipboard and drag and drop between the host and the guest;
*   seamless window mode;
*   the guest display is automatically resized according to the size of the guest window;
*   checking the VirtualBox host version

All of these features can be enabled independently with their dedicated flags:

```
$ VBoxClient --clipboard --draganddrop --seamless --display --checkhostversion

```

As a shortcut, the `VBoxClient-all` bash script enables all of these features. You should set `VBoxClient` to be automatically loaded as your [desktop environment](/index.php/Desktop_environment "Desktop environment") or [window manager](/index.php/Window_manager "Window manager") starts. In practice,

*   if you are using a [desktop environment](/index.php/Desktop_environment "Desktop environment"), you just need to check a box or add the `/usr/sbin/VBoxClient-all` to the autostart section in your [desktop environment](/index.php/Desktop_environment "Desktop environment") settings (the DE will typically set a flag to a _.desktop_ file in `~/.config/autostart`, see [the Autostart section](/index.php/Autostart#Desktop_entries "Autostart") for more details);
*   if you do not have any [desktop environment](/index.php/Desktop_environment "Desktop environment"), add the following line to the top of `~/.xinitrc` above any `exec` options. See [Xinitrc](/index.php/Xinitrc "Xinitrc") for detail.

 `~/.xinitrc`  `/usr/bin/VBoxClient-all` 

VirtualBox can also synchronize the time between the host and the guest. To do this, run `VBoxService` as root. To set this to run automatically on boot, simply [enable](/index.php/Enable "Enable") the `vboxservice` service.

Now, you should have a working Arch Linux guest. Note that features like clipboard sharing are disabled by default in VirtualBox, and you will need to turn them on in the per-VM settings if you actually want to use them (e.g. _Settings > General > Advanced > Shared Clipboard_).

If you want to share folders between your host and your Arch Linux guest, read on.

### 启用文件共享

在安装 [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) 之后，你应该运行 `VBoxClient-all` 啟动共享剪贴板、调整屏幕大小等服务。

*   若你运行会啟动 `/etc/xdg/autostart/vboxclient.desktop` 的服务，例如 GNOME 或 KDE，便不需再进行额外动作。
*   If you use `.xinitrc` to launch things instead, you must add the following to your `.xinitrc` before launching your WM.

```
# VBoxClient-all &

```

Shared folders are managed on the host, in the settings of the Virtual Machine accessible via the GUI of VirtualBox, in the _Shared Folders_ tab. There, _Folder Path_, the name of the mount point identified by _Folder name_, and options like _Read-only_, _Auto-mount_ and _Make permanent_ can be specified. These parameters can be defined with the `VBoxManage` command line utility. See [there for more details](https://www.virtualbox.org/manual/ch04.html#sharedfolders).

No matter which method you will use to mount your folder, all methods require some steps first.

To avoid this issue `/sbin/mount.vboxsf: mounting failed with the error: No such device`, make sure the `vboxsf` kernel module is properly loaded. It should be, since we enabled all guest kernel modules previously.

Two additional steps are needed in order for the mount point to be accessible from users other than root:

*   the [virtualbox-guest-utils](https://www.archlinux.org/packages/?name=virtualbox-guest-utils) package created a group `vboxsf` (done in a previous step);
*   your username must be in this group, use this command `gpasswd -a $USER vboxsf` to add your username and use `newgrp` to apply the changes immediately;

## Arch Linux 客户机共享文件夹

共享文件夹是主机上的 VirtualBox 程序控制。可以添加、自动挂载并设置成只读。主机系统创建的共享文件夹位于 /media/sf_SHAREDFOLDERNAME。要使用共享文件，需要在安装完 Guest Additions 软件包之后执行:

```
$sudo groupadd vboxsf
$sudo gpasswd -a $USER vboxsf

```

### 和主机系统同步日期

要同步系统间的日期，

#### Systemd

下次开机开始同步:

```
# systemctl enable vboxservice.service

```

立即启动同步：

```
# systemctl start vboxservice.service

```

#### 手动挂载

Use the following command to mount your folder in your Arch Linux guest:

```
# mount -t vboxsf _shared_folder_name_ _mount_point_on_guest_system_

```

The vboxsf filesystem offers other options which can be displayed with this command:

```
# mount.vboxsf

```

For example if the user was not in the _vboxsf_ group, we could have used this command to give access our mountpoint to him:

```
# mount -t vboxsf -o uid=1000,gid=1000 home /mnt/

```

Where _uid_ and _gid_ are values corresponding to the users we want to give access to. These values are obtained from the `id` command run against this user.

#### 自动挂载

In order for the automounting feature to work you must have checked the auto-mount checkbox in the GUI or used the optional `--automount` argument with the command `VBoxManage sharedfolder`.

The shared folder should now appear in `/media/sf__shared_folder_name_`. If users in `media` cannot access the shared folders, check that `media` has permissions 755 or has group ownership `vboxsf` if using permission 750\. This is currently not the default if media is created by installing the `virtualbox-guest-utils`.

You can use symlinks if you want to have a more convenient access and avoid to browse in that directory, e.g.:

```
$ ln -s /media/sf__shared_folder_name_ ~/_my_documents_

```

#### 引导时挂载

You can mount your directory with [fstab](/index.php/Fstab "Fstab"). However, to prevent startup problems with systemd, `comment=systemd.automount` should be added to `/etc/fstab`. This way, the shared folders are mounted only when those mount points are accessed and not during startup. This can avoid some problems, especially if the guest additions are not loaded yet when systemd read fstab and mount the partitions.

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,comment=systemd.automount 0 0

```

As of 2012-08-02, mount.vboxsf does not support the _nofail_ option:

```
desktop   /media/desktop    vboxsf  uid=user,gid=group,rw,dmode=700,fmode=600,nofail 0 0

```

## VirtualBox虚拟机从其他虚拟机导入/导出的管理

If you plan to use your virtual machine on another hypervisor or want to import in VirtualBox a virtual machine created with another hypervisor, you might be interested in reading the following steps.

### 添加删除

Guest additions are available in most hypervisor solutions: VirtualBox comes with the Guest Additions, VMware with the VMware Tools, Parallels with the Parallels Tools, etc. These additional components are designed to be installed inside a virtual machine after the guest operating system has been installed. They consist of device drivers and system applications that optimize the guest operating system for better performance and usability [by providing these features](https://www.virtualbox.org/manual/ch04.html).

If you have installed the additions to your virtual machine, please uninstall them first. Your guest, especially if it is using an OS from the Windows family, might behave weirdly, crash or even might not boot at all if you are still using the specific drivers in another hypervisor.

### 使用正确的虚拟磁盘格式

这一步将取决于虚拟磁盘映像直接或不能转换的能力。

#### 自动工具

Some companies provide tools which offer the ability to create virtual machines from a Windows or GNU/Linux operating system located either in a virtual machine or even in a native installation. With such a product, you do not need to apply this and the following steps and can stop reading here.

*   _[Parallels Transporter](http://www.parallels.com/products/transporter)_ which is non free, is a product from Parallels Inc. This solution basically consists in an piece of software called _agent_ that will be installed in the guest you want to import/convert. Then, Parallels Transporter, <u>which only works on OS X</u>, will create a virtual machine from that _agent_ which is contacted either by USB or Ethernet network.
*   _[VMware vCenter Converter](https://www.vmware.com/products/converter/)_ which is free upon registration on the VMware webiste, works nearly the same way as Parallels Transporter, but the piece of software that will gather the data to create the virtual machine only works on a Windows platform.

#### 手动转换

First, familiarize yourself with the [#Formats supported by VirtualBox](#Formats_supported_by_VirtualBox) and [those supported by third-party hypervisors](https://en.wikipedia.org/wiki/Comparison_of_platform_virtual_machines#Image_type_compatibility "wikipedia:Comparison of platform virtual machines").

*   Importing or exporting a virtual machine from/to a VMware solution is not a problem at all if you use the VMDK or OVF disk format, otherwise converting [#VMDK to VDI and VDI to VMDK](#VMDK_to_VDI_and_VDI_to_VMDK) is possible and the aforementioned VMware vCenter Converter tool is available.

*   Importing or exporting from/to QEMU is not a problem neither: some QEMU formats are supported directly by VirtualBox and conversion between [#QCOW2 to VDI and VDI to QCOW2](#QCOW2_to_VDI_and_VDI_to_QCOW2) is still available if needed.

*   Importing or exporting from/to Parallels hypervisor is the hardest way: Parallels does only support its own HDD format (even the standard and portable OVF format is not supported!).

*   To export your virtual machine to Parallels, you will need to use the Parallels Transporter tool described above.
*   To import your virtual machine to VirtualBox, you will need to use the VMware vCenter Converter described above to convert the VM to the VMware format first. Then, apply the solution to migrate from VMware.

### 创建虚拟机的配置为你的虚拟机管理程序

Each hypervisor have their own virtual machine configuration file: `.vbox` for VirtualBox, `.vmx` for VMware, a `config.pvs` file located in the virtual machine bundle (`.pvm` file), etc. You will have thus to recreate a new virtual machine in your new destination hypervisor and specify its hardware configuration as close as possible as your initial virtual machine.

Pay a close attention to the firmware interface (BIOS or UEFI) used to install the guest operating system. While an option is available to choose between these 2 interfaces on VirtualBox and on Parallels solutions, on VMware, you will have to add manually the following line to your _.vmx_ file.

 `ArchLinux_vm.vmx`  `firmware = "efi"` 

Finally, ask your hypervisor to use the existing virtual disk you have converted and launch the virtual machine.

**Tip:**

*   On VirtualBox, if you do not want to browse the whole GUI to find the right location to add your new virtual drive device, you can [#Replace a virtual disk manually from the .vbox file](#Replace_a_virtual_disk_manually_from_the_.vbox_file), or use the `VBoxManage storageattach` described in [#Increase virtual disks](#Increase_virtual_disks) or in the [VirtualBox manual page](https://www.virtualbox.org/manual/ch08.html#vboxmanage-storageattach).
*   Similarly, in VMware products, you can replace the location of the current virtual disk location by adapting the _.vmdk_ file location in your _.vmx_ configuration file.

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
$ VBoxManage clonehd _source.vmdk_ _destination.vdi_ --format VDI

```

VDI to VMDK:

```
$ VBoxManage clonehd _source.vdi_ _destination.vmdk_ --format VMDK

```

#### VHD to VDI and VDI to VDH

VirtualBox can handle conversion back and forth this format with [`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) too.

VHD to VDI:

```
$ VBoxManage clonehd _source.vhd_ _destination.vdi_ --format VDI

```

VDI to VHD:

```
$ VBoxManage clonehd _source.vdi_ _destination.vhd_ --format VHD

```

#### QCOW2 to VDI and VDI to QCOW2

[`VBoxManage clonehd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi) cannot handle the QEMU format conversion; we will thus rely on another tool. The `qemu-img` command from [qemu](https://www.archlinux.org/packages/?name=qemu) can be used to convert images back and forth from VDI to QCOW2\.

**Note:** `qemu-img` can handle a bunch of other formats too. According to the `qemu-img --help`, here are the supported formats this tool supports: "_vvfat vpc vmdk vhdx vdi ssh sheepdog sheepdog sheepdog raw host_cdrom host_floppy host_device file qed qcow2 qcow parallels nbd nbd nbd iscsi dmg tftp ftps ftp https http cow cloop bochs blkverify blkdebug'"._

QCOW2 to VDI:

```
$ qemu-img convert -pO vdi _source.qcow2_ _destination.vdi_

```

VDI to QCOW2:

```
$ qemu-img convert -pO qcow2 _source.vdi_ _destination.qcow2_

```

As QCOW2 comes in two revisions (see [#Formats supported by VirtualBox](#Formats_supported_by_VirtualBox), use the flag `-o compat=` to specify the revision.

```
$ qemu-img convert -pO qcow2 _source.vdi_ _destination.qcow2_ -o compat=0.10

```

or

```
$ qemu-img convert -pO qcow2 _source.vdi_ _destination.qcow2_ -o compat=1.1

```

**Tip:** The `-p` parameter is used to get the progression of the conversion task.

## 从其他虚拟机中迁移

`qemu-img` 程序可以用来将映像从一种格式转换到另一种格式，或为一个映像添加压缩或加密。

```
  # pacman -S qemu

```

### 从QEMU映像转换

To convert a QEMU image for use with VirtualBox, first convert it to _raw_ format, then use VirtualBox's conversion utility to convert and compact it in its native format.

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
# mount -t vdi -o fstype=ext4,rw,noatime,noexec _vdi_file_location_ _/mnt/_

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

*   If you were previously using Bleachbit, check the checkbox _System > Free disk space_ in the GUI, or use `bleachbit -c system.free_disk_space` in CLI;
*   在 UNIX基本系统,使用 `dd` or preferably [dcfldd](https://www.archlinux.org/packages/?name=dcfldd) (see [here](http://superuser.com/a/355322) to learn the differences) :

 `# dcfldd if=/dev/zero of=_/fillfile_ bs=4M` 

When `fillfile` reaches the limit of the partition, you will get a message like `1280 blocks (5120Mb) written.dcfldd:: No space left on device`. This means that all of the user-space and non-reserved blocks of the partition will be filled with zeros. Using this command as root is important to make sure all free blocks have been overwritten. Indeed, by default, when using partitions with ext filesystem, a specified percentage of filesystem blocks is reserved for the super-user (see the `-m` argument in the `mkfs.ext4` man pages or use `tune2fs -l` to see how much space is reserved for root applications).

When the aforementioned process has completed, you can remove the file `_fillfile_` you created.

*   On Windows, there are two tools available:

*   `sdelete` from the [Sysinternals Suite](http://technet.microsoft.com/en-us/sysinternals/bb842062.aspx), type `sdelete -s -z _c:_`, where you need to reexecute the command for each drive you have in your virtual machine;
*   or, if you love scripts, there is a [PowerShell solution](http://blog.whatsupduck.net/2012/03/powershell-alternative-to-sdelete.html), but which still needs to be repeated for all drives.

 `PS> ./Write-ZeroesToFreeSpace.ps1 -Root _c:\_ -PercentFree 0` 

**Note:** This script must be run in a PowerShell environment with administrator privileges. By default, scripts cannot be run, ensure the execution policy is at least on `RemoteSigned` and not on `Restricted`. This can be checked with `Get-ExecutionPolicy` and the required policy can be set with `Set-ExecutionPolicy RemoteSigned`.

Once the free disk space have been wiped, shut down your virtual machine.

The next time you boot your virtual machine, it is recommended to do a filesystem check.

*   On UNIX-based systems, you can use `fsck` manually;

*   On GNU/Linux systems, and thus on Arch Linux, you can force a disk check at boot [thanks to a kernel boot parameter](/index.php/Fsck#Forcing_the_check "Fsck");

*   On Windows systems, you can use:

*   either `chkdsk _c:_ /F` where `_c:_` needs to be replaced by each disk you need to scan and fix errors;
*   or `FsckDskAll` [from here](http://therightstuff.de/2009/02/14/ChkDskAll-ChkDsk-For-All-Drives.aspx) which is basically the same software as `chkdsk`, but without the need to repeat the command for all drives;

Now, remove the zeros from the `vdi` file with `[VBoxManage modifyhd](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi)`:

```
$ VBoxManage modifyhd _your_disk.vdi_ --compact

```

**Note:** If your virtual machine has snapshots, you need to apply the above command on each `.vdi` files you have.

### 增加虚拟磁盘

If you are running out of space due to the small hard drive size you selected when you created your virtual machine, the solution adviced by the VirtualBox manual is to use [`VBoxManage modifyhd`](https://www.virtualbox.org/manual/ch08.html#vboxmanage-modifyvdi). However this command only works for VDI and VHD disks and only for the dynamically allocated variants. If you want to resize a fixed size virtual disk disk too, read on this trick which works either for a Windows or UNIX-like virtual machine.

First, create a new virtual disk next to the one you want to increase:

```
$ VBoxManage createhd -filename _new.vdi_ --size _10000_

```

where size is in MiB, in this example 10000MiB ~= 10GiB, and _new.vdi_ is name of new hard drive to be created.

Next, the old virtual disk needs to be cloned to the new one which this may take some time:

```
$ VBoxManage clonehd _old.vdi_ _new.vdi_ --existing

```

**Note:** By default, this command uses the _Standard_ (corresponding to dynamic allocated) file format variant and thus will not use the same file format variant as your source virtual disk. If your _old.vdi_ has a fixed size and you want to keep this variant, add the parameter `--variant Fixed`.

Detach the old hard drive and attach new one, replace all mandatory italic arguments by your own:

```
$ VBoxManage storageattach _VM_name_ --storagectl _SATA_ --port _0_ --medium none
$ VBoxManage storageattach _VM_name_ --storagectl _SATA_ --port _0_ --medium _new.vdi_ --type hdd

```

To get the storage controller name and the port number, you can use the command `VBoxManage showvminfo _VM_name_`. Among the output you will get such a result (what you are looking for is in italic):

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
_SATA_ (_0_, 0): /home/wget/IT/Virtual_machines/GNU_Linux_distributions/ArchLinux_x64_EFI/Snapshots/{6bb17af7-e8a2-4bbf-baac-fbba05ebd704}.vdi (UUID: 6bb17af7-e8a2-4bbf-baac-fbba05ebd704)
[...]
```

Download [GParted live image](http://gparted.org/download.php) and mount it as a virtual CD/DVD disk file, boot your virtual machine, increase/move your partitions, umount GParted live and reboot.

**Note:** On GPT disks, increasing the size of the disk will result in the backup GPT header not being at the end of the device. GParted will ask to fix this, click on _Fix_ both times. On MBR disks, you do not have such a problem as this partition table as no trailer at the end of the disk.

Finally, unregister the virtual disk from VirtualBox and remove the file:

```
$ VBoxManage closemedium disk _old.vdi_
$ rm _old.vdi_

```

### 从.vbox文件中手动更换虚拟磁盘

If you think that editing a simple _XML_ file is more convenient than playing with the GUI or with `VBoxManage` and you want to replace (or add) a virtual disk to your virtual machine, in the _.vbox_ configuration file corresponding to your virtual machine, simply replace the GUID, the file location and the format to your needs:

 `ArchLinux_vm.vbox`  `<HardDisk uuid="_{670157e5-8bd4-4f7b-8b96-9ee412a712b5}_" location="_ArchLinux_vm.vdi_" format="_VDI_" type="Normal"/>` 

then in the `<AttachedDevice>` sub-tag of `<StorageController>`, replace the GUID by the new one.

 `ArchLinux_vm.vbox` 

```
<AttachedDevice type="HardDisk" port="0" device="0">
  <Image uuid="_{670157e5-8bd4-4f7b-8b96-9ee412a712b5}_"/>
</AttachedDevice>
```

**Note:** If you do not know the GUID of the drive you want to add, you can use the `VBoxManage showhdinfo _file_`. If you previously used `VBoxManage clonehd` to copy/convert your virtual disk, this command should have outputted the GUID just after the copy/conversion completed. Using a random GUID does not work, as each [UUID is stored inside each disk image](http://www.virtualbox.org/manual/ch05.html#cloningvdis).

#### Linux主机和其他操作系统之间的转移

The information about path to harddisks and the snapshots is stored between `<HardDisks> .... </HardDisks>` tags in the file with the _.vbox_ extension. You can edit them manually or use this script where you will need change only the path or use defaults, assumed that _.vbox_ is in the same directory with a virtual harddisk and the snapshots folder. It will print out new configuration to stdout.

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
*   To make it run on a new host you will need to add it first to the register by clicking on **Machine -> Add...** or use hotkeys Ctrl+A and then browse to _.vbox_ file that contains configuration or use command line `VBoxManage registervm _filename_.vbox`

## 配置

### 网络

VirtualBox 客户端可以通过不同的方式连接网络；其中，有[#NAT](#NAT)和[#桥接](#.E6.A1.A5.E6.8E.A5)链接。[#NAT](#NAT)是最简单的且作为一个新虚拟机的默认方式。

[VirtualBox手册](http://www.virtualbox.org/manual/UserManual.html)涵盖了主机模式和内网选项。这些都被忽略了，因为在大多数情况下与操作系统无关。

#### NAT

在VirtualBox中：

*   访问虚拟机的_设置_菜单；
*   点击左边的_网络‘’；最后，_
*   在“连接方式”的下拉列表中选择_NAT_。

与VirtualBox捆绑的DHCP服务使得客户端系统能够与DHCP一起配置，第一张卡的NAT IP地址是 10.0.2.0，第二张是10.0.3.0，往后以此类推。

#### 桥接

桥接网络可能被以多种方式启动；其中，有要求以较少控制为代价进行最小启动的原生方式。对于较新版本，VirtualBox可以在没有第三方工具的帮助下，在客户端和无线主机接口间进行桥接。

在继续之前，加载必要模块：

```
# modprobe vboxnetflt

```

在VirtualBox中：

*   访问虚拟机的_设置_菜单；
*   点击左边列表中的_网络_
*   在_链接方式_的下拉列表中选择_Bridged Adapter(桥接适配器)_；最后，
*   在_界面名称_下拉列表中，选择客户端操作系统被包含在内，主机用于连接网络的接口。

Start the virtual machine and configure its network as usual; e.g., DHCP or static. 打开虚拟机，像往常一样配置其网络；例如 DHCP 或 static（静态网络）。

### 主机端和客户端之间的键盘和鼠标

*   为了捕获键盘和鼠标，点击虚拟机内部。
*   想要释放，按下右 `Ctrl`.

想要获得在主机端和客户端之间的无缝鼠标集成功能，在客户端内安装[#客户端增强包](#.E5.AE.A2.E6.88.B7.E7.AB.AF.E5.A2.9E.E5.BC.BA.E5.8C.85)。

### 主机端和客户端间的共享文件夹

在虚拟机的设置中，找到数据空间标签，然后加入你想要共享的文件夹。

*   注意：为了使用这个功能你需要安装客户端增强包。

```
在Linux主机中，_设备 → 安装增强功能_
确定（被要求下载CD镜像时）
挂载（被要求注册和挂载时）

```

In a Linux host, create one or more folders for sharing files, then set the shared folders via the virtualbox menu (guest window). 在Linux主机端中，为共享的文件创建一个或更多的文件夹，然后通过Virtualbox菜单中设置（Windows客户端）

在Windows客户端中，从VirtualBox 1.5.0开始，共享文件夹是可浏览的，所以在Windows资源管理器中是可视的。打开Windows资源管理器，在_我的网络位置（My Networking Places） → 整个网络（Entire Network） → VirtualBox Shared Folders（VirtualBox共享文件夹）_。

启动Windows资源管理器（运行资源管理器命令），游览 网络位置（network places） -> （+）号展开： 整个网络（entire network）&rarr； VirtualBox Shared Folders（VirtualBox共享文件夹） &rarr；**\\Vboxsvr** → 然后你就可以在此展开所有已配置的文件夹了，并且在客户端文件系统中为Linux文件夹创建快捷方式。你也可以使用“添加网络位置向导（Add network place wizard）”找到“VBoxsvr”。

此外，在Windows命令行提示符中，你也可以使用以下命令：

```
net use x: \\VBOXSVR\sharename

```

虽然`VBOXSVR`是一个固定名称，但请用你所想要用于共享的盘符替代`x:`，用VBoxManage指定的共享名替换sharename。

在Windows客户端中，为了以VirtualBox共享文件夹改善文件的读取与保存（如MS Office），编辑_c:\windows\system32\drivers\etc\hosts_如下：

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
$ VBoxManage internalcommands sethduuid _/path/to/disk.vdi_

```

**Tip:** In the future, to avoid copying the virtual disk and assigning a new UUID to your file manually, use `[VBoxManage clonehd](http://www.virtualbox.org/manual/ch08.html#vboxmanage-clonevdi)` instead.

**Note:** The commands above supports [all virtual disk formats supported by VirtualBox](#Formats_supported_by_VirtualBox).

## 高级配置

### 虚拟机管理启动

#### 启动虚拟机服务

此后查找将用于考虑虚拟机作为服务systemd服务的实现。

 `/etc/systemd/system/vboxvmservice@.service` 

```
[Unit]
Description=VBox Virtual Machine %i Service
Requires=systemd-modules-load.service
After=systemd-modules-load.service

[Service]
User=_username_
Group=vboxusers
ExecStart=/usr/bin/VBoxHeadless -s %i
ExecStop=/usr/bin/VBoxManage controlvm %i savestate

[Install]
WantedBy=multi-user.target
```

**Note:** Replace `_username_` with a user that is a member of the `vboxusers` group. Make sure the user chosen is the same user that will create/import virtual machines, otherwise the user will not see the VM appliances.

**Note:** If you have multiple virtual machines managed by Systemd and they are not stopping properly, try to add `RemainAfterExit=true` and `KillMode=none` at the end of `[Service]` section.

To enable the service that will launch the virtual machine at next boot, use:

```
# systemctl enable vboxvmservice@_your_virtual_machine_name_

```

To start the service that will launch directly the virtual machine, use:

```
# systemctl start vboxvmservice@_your_virtual_machine_name_

```

VirtualBox 4.2 introduces [a new way](http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/) for UNIX-like systems to have virtual machines started automatically, other than using a systemd service.

#### 启动虚拟机键盘快捷键

It can be useful to start virtual machines directly with a keyboard shortcut instead of using the VirtualBox interface (GUI or CLI). For that, you can simply define key bindings in `.xbindkeysrc`. Please refer to [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") for more details.

Example, using the `Fn` key of a laptop with an unused battery key (`F3` on the computer used in this example):

```
"VBoxManage startvm 'Windows 7'"
m:0x0 + c:244
XF86Battery

```

**Note:** If you have a space in the name of your virtual machine, then enclose it with single apostrophes like made in the example just above.

### 在虚拟机中使用特定的设备

### 使用 USB 摄像头 / 麦克风

**Note:** 在遵照下列步骤前，你需要安装 VirtualBox 扩展包。详见 [VirtualBox_Extras#Extension_pack](/index.php/VirtualBox_Extras#Extension_pack "VirtualBox Extras")。

1.  要确保没有在运行虚拟机，以及没有使用摄像头 / 麦克风。
2.  进入VirtualBox主界面并打开Arch系统的设置界面，到USB设备页。
3.  要确保勾选上“启用USB控制器”选项。 还要确保选择“启用USB 2.0(EHCI)控制器”选项。
4.  点击“从设备列表中添加筛选器”按钮 (就是那个有“+”图标的连接线).
5.  从列表中选择你的USB摄像头 / 麦克风设备。
6.  然后再点击OK，启动你的VM

#### 获得可探测的Web-cam和其他USB设备

Make sure you filter any devices that are not a keyboard or a mouse so they do not start up at boot and this insures that Windows will detect the device at start-up.

### 访问guest 服务

To access [Apache server](https://en.wikipedia.org/wiki/Apache_HTTP_Server "wikipedia:Apache HTTP Server") on a Virtual Machine from the host machine **only**, simply execute the following lines on the host:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/_pcnet_/0/LUN#0/Config/Apache/HostPort" _8888_
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/_pcnet_/0/LUN#0/Config/Apache/GuestPort" _80_
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/_pcnet_/0/LUN#0/Config/Apache/Protocol" TCP

```

Where 8888 is the port the host should listen on and 80 is the port the VM will send Apache's signal on.

To use a port lower than 1024 on the host machine, changes need to be made to the firewall on that host machine. This can also be set up to work with SSH or any other services by changing "Apache" to the corresponding service and ports.

**Note:** `pcnet` refers to the network card of the VM. If you use an Intel card in your VM settings, change `pcnet` to `e1000`.

To communicate between the VirtualBox guest and host using ssh, the server port must be forwarded under Settings > Network. When connecting from the client/host, connect to the IP address of the client/host machine, as opposed to the connection of the other machine. This is because the connection will be made over a virtual adapter.

### 在Windows客户端中激活D3D加速

Recent versions of Virtualbox have support for accelerating OpenGL inside guests. This can be enabled with a simple checkbox in the machine's settings, right below where video ram is set, and installing the Virtualbox guest additions. However, most Windows games use Direct3D (part of DirectX), not OpenGL, and are thus not helped by this method. However, it is possible to gain accelerated Direct3D in your Windows guests by borrowing the d3d libraries from Wine, which translate d3d calls into OpenGL, which is then accelerated. These libraries are now part of Virtualbox guest additions software.

After enabling OpenGL acceleration as described above, reboot the guest into safe mode (press F8 before the Windows screen appears but after the Virtualbox screen disappears), and install Virtualbox guest additions, during install enable checkbox "Direct3D support". Reboot back to normal mode and you should have accelerated Direct3D.

**Note:** This hack may or may not work for some games depending on what hardware checks they make and what parts of D3D they use.

**Note:** This was tested on Windows XP, 7 and 8.1\. If method does not work on your Windows version please add data here.

### 在USB key上使用VirtualBox

When using VirtualBox on a USB key, for example to start an installed machine with an ISO image, you will manually have to create VDMKs from the existing drives. However, once the new VMDKs are saved and you move on to another machine, you may experience problems launching an appropriate machine again. To get rid of this issue, you can use the following script to launch VirtualBox. This script will clean up and unregister old VMDK files and it will create new, proper VMDKs for you:

```
#!/bin/bash

# Erase old VMDK entries
rm ~/.VirtualBox/*.vmdk

# Clean up VBox-Registry
sed -i '/sd/d' ~/.VirtualBox/VirtualBox.xml

# Remove old harddisks from existing machines
find ~/.VirtualBox/Machines -name \*.xml | while read file; do
  line=`grep -e "type\=\"HardDisk\"" -n $file | cut -d ':' -f 1`
  if [ -n "$line" ]; then
    sed -i ${line}d $file
    sed -i ${line}d $file
    sed -i ${line}d $file
  fi
  sed -i "/rg/d" $file
done

# Delete prev-files created by VirtualBox
find  ~/.VirtualBox/Machines -name \*-prev -exec rm '{}' \;

# Recreate VMDKs
ls -l /dev/disk/by-uuid | cut -d ' ' -f 9,11 | while read ln; do
  if [ -n "$ln" ]; then
    uuid=`echo "$ln" | cut -d ' ' -f 1`
    device=`echo "$ln" | cut -d ' ' -f 2 | cut -d '/' -f 3 | cut -b 1-3`

    # determine whether drive is mounted already
    checkstr1=`mount | grep $uuid`
    checkstr2=`mount | grep $device`
    checkstr3=`ls ~/.VirtualBox/*.vmdk | grep $device`
    if [[ -z "$checkstr1" && -z "$checkstr2" && -z "$checkstr3" ]]; then
      VBoxManage internalcommands createrawvmdk -filename ~/.VirtualBox/$device.vmdk -rawdisk /dev/$device -register
    fi
  fi
done

# Start VirtualBox
VirtualBox

```

Note that your user has to be added to the "disk" group to create VMDKs out of existing drives.

### Run a native Arch Linux installation inside VirtualBox

If you have a dual boot system between Arch Linux and another operating system, it can become rapidly tedious to switch back and forth if you need to work in both. Also, by using virtual machines, you just have a tiny fragment of your computer power, which can cause issues when working on projects requiring performance.

This guide will let you reuse, in a virtual machine, your native Arch Linux installation when you are running your second operating system. This way, you keep the ability to run each operating system natively, but have the option to run your Arch Linux installation inside a virtual machine.

#### Make sure you have a persistent naming scheme

Depending on your hard drive setup, device files representing your hard drives may appear differently when you will run your Arch Linux installation natively or in virtual machine. This problem occurs when using [FakeRAID](/index.php/RAID#Implementation "RAID") for example. The fake RAID device will be mapped in `/dev/mapper/` when you run your GNU/Linux distribution natively, while the devices are still accessible separately. However, in your virtual machine, it can appear without any mapping in `/dev/sdaX` for example, because the drivers controlling the fake RAID in your host operating system (e.g. Windows) are abstracting the fake RAID device.

To circumvent this problem, we will need to use an addressing scheme that is persistent to both systems. This can be achieved using [UUIDs](/index.php/Fstab#UUIDs "Fstab") in your `/etc/fstab` file. Make sure your [fstab](/index.php/Fstab "Fstab") file is using UUIDs, otherwise fix this issue. Read [fstab](/index.php/Fstab "Fstab") and [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

`/etc/fstab` is not the only location where UUIDs are used. Bootloaders and boot managers make use of them too. Now, make sure these are really using UUIDs.

[GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy")

If you are still using the old [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), maybe is it [time to upgrade](/index.php/GRUB_Legacy#Upgrading_to_GRUB2 "GRUB Legacy"), since this package is now dropped from the official Arch Linux repositories. If you want to keep it, edit `/boot/grub/menu.lst` and replace the `root=/dev/sdXX` statement in your Arch Linux boot entry by the Linux UUID mapping in `/dev/disk/by-uuid/` corresponding to your root partition.

```
title  Arch Linux
root
kernel /vmlinuz-linux root=_/dev/disk/by-uuid/0a3407de-014b-458b-b5c1-848e92a327a3_ ro vga=773
initrd /initramfs-linux-vbox.img

```

Repeat the process here, for the fallback entry.

[GRUB](/index.php/GRUB "GRUB")

If you are running the most recent version of [GRUB](/index.php/GRUB "GRUB"); you have nothing to do. Yet another reason to upgrade to GRUB 2.

**Warning:**

*   Make sure your host partition is only accessible in read only from your Arch Linux virtual machine, this will avoid risk of corruptions if you were to corrupt that host partition by writing on it due to lack of attention.
*   You should NEVER allow VirtualBox to boot from the entry of your second operating system, which, as a reminder, is used as the host for this virtual machine! Take thus a special care especially if your default boot loader/boot manager entry is your other operating system. Give a more important timeout or put it below in the order of preferences.

#### Make sure your mkinitcpio image is correct

Make sure your [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") configuration uses the [HOOK](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") `block`:

 `/etc/mkinitcpio.conf` 

```
[...]
HOOKS="base udev autodetect modconf _block_ filesystems keyboard fsck"
[...]
```

If it is not present, add it and [regenerate your initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio"):

```
# mkinitcpio -p linux

```

#### Create a VM configuration to boot from the physical drive

##### 创建一个原始只读磁盘的.vmdk映像

Now, we need to create a new virtual machine which will use a [RAW disk](https://www.virtualbox.org/manual/ch09.html#rawdisk) as virtual drive, for that we will use a ~ 1Kio VMDK file which will be mapped to a physical disk. Unfortunately, VirtualBox does not have this option in the GUI, so we will have to use the console and use an internal command of `VBoxManage`.

Boot the host which will use the Arch Linux virtual machine. The command will need to be adapted according to the host you have.

On a GNU/Linux host

There is 3 ways to achieve this: login as root, changing the access right of the device with `chmod`, adding your user to the `disk` group. The latter way is the more elegant, let us proceed that way:

```
# gpasswd -a _your_user_ disk

```

Apply the new group settings with:

```
$ newgrp

```

Now, you can use the command:

```
$ VBoxManage internalcommands createrawvmdk -filename _/path/to/file.vmdk_ -rawdisk _/dev/sdb_ -register 

```

Adapt the above command to your need, especially the path and filename of the VMDK location and the raw disk location to map which contain your Arch Linux installation.

On a Windows host

Open a command prompt must be run as administrator.

**Tip:** On Windows, open your start menu/start screen, type `cmd`, and type `Ctrl+Shift+Enter`, this is a shortcut to execute the selected program with admin rights.

On Windows, as the disk filename convention is different from UNIX, use this command to determine what drives you have in your Windows system and their location: `# wmic diskdrive get name,size,model` 

```
Model                               Name                Size
WDC WD40EZRX-00SPEB0 ATA Device     \\.\PHYSICALDRIVE1  4000783933440
KINGSTON SVP100S296G ATA Device     \\.\PHYSICALDRIVE0  96024821760
Hitachi HDT721010SLA360 ATA Device  \\.\PHYSICALDRIVE2  1000202273280
Innostor Ext. HDD USB Device        \\.\PHYSICALDRIVE3  1000202273280
```

In this example, as the Windows convention is `\\.\PhysicalDriveX` where X is a number from 0, `\\.\PHYSICALDRIVE1` could be analogous to `/dev/sdb` from the Linux disk terminology.

To use the `VBoxManage` command on Windows, you can either, change the current directory to your VirtualBox installation folder first with `cd C:\Program Files\Oracle\VirtualBox\`

```
# .\VBoxManage.exe internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

or use the absolute path name:

```
# "C:\Program Files\Oracle\VirtualBox\VBoxManage.exe" internalcommands createrawvmdk -filename C:\file.vmdk -rawdisk \\.\PHYSICALDRIVE1

```

On another OS host

There are other limitations regarding the aforementioned command when used in other operating systems like OS X, please thus [read carefully the manual page](https://www.virtualbox.org/manual/ch09.html#rawdisk), if you are concerned.

##### 创建虚拟机配置文件

**Note:**

*   To make use of the VBoxManage command on Windows, you need to change the current directory to your VirtualBox installation folder first: cd C:\Program Files\Oracle\VirtualBox\.
*   Windows makes use of backslashes instead of slashes, please replace all slashes / occurrences by backslashes \ in the commands that follow when you will use them.

After, we need to create a new machine (replace the _VM_name_ to your convenience) and register it with VirtualBox.

```
$ VBoxManage createvm -name _VM_name_ -register

```

Then, the newly raw disk needs to be attached to the machine. This will depend if your computer or actually the root of your native Arch Linux installation is on an IDE or a SATA controller.

If you need an IDE controller:

```
$ VBoxManage storagectl _VM_name_ --name "IDE Controller" --add ide
$ VBoxManage storageattach _VM_name_ --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

otherwise:

```
$ VBoxManage storagectl _VM_name_ --name "SATA Controller" --add sata
$ VBoxManage storageattach _VM_name_ --storagectl "SATA Controller" --port 0 --device 0 --type hdd --medium /path/to/file.vmdk

```

While you continue using the CLI, it is recommended to use the VirtualBox GUI, to personalise the virtual machine configuration. Indeed, you must specify its hardware configuration as close as possible as your native machine: turning on the 3D acceleration, increasing video memory, setting the network interface, etc.

#### Install the Guest Additions

Finally, you may want to seamlessly integrate your Arch Linux with your host operating system and allow copy pasting between both OSes. Please refer to [#Install the Guest Additions](#Install_the_Guest_Additions) for that, since this Arch Linux virtual machine is basically an Arch Linux guest.

**Warning:** For [Xorg](/index.php/Xorg "Xorg") to work in natively and in the virtual machine, since obviously it will be using different drivers, it is best if there is no `/etc/X11/xorg.conf`, so Xorg will pick up everything it needs on the fly. However, if you really do need your own Xorg configuration, maybe is it worth to set your default systemd target to `multi-user.target` with `systemctl isolate graphical.target` as root (more details at [Systemd#Targets table](/index.php/Systemd#Targets_table "Systemd") and [Systemd#Change current target](/index.php/Systemd#Change_current_target "Systemd")). In that way, the graphical interface is disabled (i.e. Xorg is not launched) and after you logged in, you can `startx`} manually with a custom `xorg.conf`.

### 安装VirtualBox的本地Arch Linux系统

In some cases it may be useful to install a native Arch Linux system while running another operating system: one way to accomplish this is to perform the installation through VirtualBox on a [raw disk](http://www.virtualbox.org/manual/ch09.html#rawdisk). If the existing operating system is Linux based, you may want to consider following [Install from Existing Linux](/index.php/Install_from_Existing_Linux "Install from Existing Linux") instead.

This scenario is very similar to [#Run a native Arch Linux installation inside VirtualBox](#Run_a_native_Arch_Linux_installation_inside_VirtualBox), but will follow those steps in a different order: start by [#Create a raw disk .vmdk image](#Create_a_raw_disk_.vmdk_image), then [#Create the VM configuration file](#Create_the_VM_configuration_file).

Now, you should have a working VM configuration whose virtual VMDK disk is tied to a real disk. The installation process is exactly the same as the steps described in [#Installation steps for Arch Linux guests](#Installation_steps_for_Arch_Linux_guests), but [#Make sure you have a persistent naming scheme](#Make_sure_you_have_a_persistent_naming_scheme) and [#Make sure your mkinitcpio image is correct](#Make_sure_your_mkinitcpio_image_is_correct).

**Warning:**

*   For BIOS systems and MBR disks, do not install a bootloader inside your virtual machine, this will not work since the MBR is not linked to the MBR of your real machine and your virtual disk is only mapped to a real partition without the MBR.
*   For UEFI systems without [CSM](https://en.wikipedia.org/wiki/Compatibility_Support_Module#CSM "wikipedia:Compatibility Support Module") and GPT disks, the installation will not work at all since:

*   the [ESP](https://en.wikipedia.org/wiki/EFI_System_partition "wikipedia:EFI System partition") partition is not mapped to your virtual disk and Arch Linux requires to have the Linux kernel on it to boot as an EFI application (see [EFISTUB](/index.php/EFISTUB "EFISTUB") for details);
*   and the efivars, if you are installing Arch Linux using the EFI mode brought by VirtualBox, are not the one of your real system: the bootmanager entries will hence not be registered.

*   This is why, it is recommended to create your partitions in a native installation first, otherwize the partitions will not be taken into consideration in your MBR/GPT partition table.

After completing the installation, boot your computer natively with an GNU/Linux installation media (whether it be Arch Linux or not), [chroot](/index.php/Beginner%27s_Guide#Chroot_and_configure_the_base_system "Beginner's Guide") into your installed Arch Linux installation and [#Install and configure a bootloader](/index.php/Beginner%27s_Guide#Install_and_configure_a_bootloader "Beginner's Guide").

### 将本机Windows安装到虚拟机

If you want to migrate an existing native Windows installation to a virtual machine which will be used with VirtualBox on GNU/Linux, this use case is for you. This section only covers native Windows installation using the MSDOS/Intel partition scheme. Your Windows installation must reside on the first MBR partition for this operation to success. Operation for other partitions are available but have been untested (see [#Known limitations](#Known_limitations) for details).

**Warning:** If you are using an OEM version of Windows, this process is unauthorized by the end user license license. Indeed, the OEM license typically states the Windows install is tied with the hardware together. Transferring a Windows install to a virtual machine removes this link. Make thus sure you have a full Windows install or a volume license model before continuing. If you have a full Windows license but the latter is not coming in volume, nor as a special license for several PCs, this means you will have to remove the native installation after the transfer operation has been achieved.

A couple of tasks are required to be done inside your native Windows installation first, then on your GNU/Linux host.

#### Tasks on Windows

The first three following points comes from [this outdated VirtualBox wiki page](https://www.virtualbox.org/wiki/Migrate_Windows#HAL), but are updated here.

*   Remove IDE/ATA controllers checks (Windows XP only): Windows memorize the IDE/ATA drive controllers it has been installed on and will not boot if it detects these have changed. The solution proposed by Microsoft is to reuse the same controller or use one of the same serial, which is impossible to achieve since we are using a Virtual Machine. [MergeIDE](https://www.virtualbox.org/wiki/Migrate_Windows#HardDiskSupport), a German tool, developped upon another other solution proposed by Microsoft can be used. That solution basically consists in taking all IDE/ATA controller drivers supported by Windows XP from the initial driver archive (the location is hard coded, or specify it as the first argument to the `.bat` script), installing them and registering them with the regedit database.

*   Use the right type of Hardware Abstraction Layer (old 32 bits Windows versions): Microsoft ships 3 default versions: `Hal.dll` (Standard PC), `Halacpi.dll` (ACPI HAL) and `Halaacpi.dll` (ACPI HAL with IO APIC). Your Windows install could come installed with the first or the second version. In that way, please [disable the _Enable IO/APIC_ VirtualBox extended feature](https://www.virtualbox.org/manual/ch08.html#idp56927888).

*   Disable any AGP device driver (only outdated Windows versions): If you have the files `agp440.sys` or `intelppm.sys` inside the `C:\Windows\SYSTEM32\drivers\` directory, remove it. As VirtualBox uses a PCI virtual graphic card, this can cause problems when this AGP driver is used.

*   Create a Windows recovery disk: In the following steps, if things turn bad, you will need to repair your Windows installation. Make sure you have an install media at hand, or create one with _Create a recovery disk_ from Vista SP1, _Create a system repair disc_ on Windows 7 or _Create a recovery drive_ on Windows 8.x).

#### Tasks on GNU/Linux

*   Reduce the native Windows partition size to the size Windows actually needs with `ntfsresize` available from [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g). The size you will specify will be the same size of the VDI that will be created in the next step. If this size is too low, you may break your Windows install and the latter might not boot at all.

Use the `--no-action` option first to run a test:

 `# ntfsresize --no-action --size _52Gi_ _/dev/sda1_` 

If only the previous test succeeded, execute this command again, but this time without the aforementioned test flag.

*   Install VirtualBox on your GNU/Linux host (see [#Installation steps for Arch Linux hosts](#Installation_steps_for_Arch_Linux_hosts) if your host is Arch Linux).

*   Create the Windows disk image from the beginning of the drive to the end of the first partition where is located your Windows installation. Copying from the beginning of the disk is necessary because the MBR space at the beginning of the drive needs to be on the virtual drive along with the Windows partition. In this example two following partitions `sda2` and `sda3`will be later removed from the partition table and the MBR bootloader will be updated.

 `# sectnum=$(( $(cat /sys/block/''sda/sda1''/start) + $(cat /sys/block/''sda/sda1''/size) ))` 

Using `cat /sys/block/_sda/sda1_/size` will output the number of total sectors of the first partition of the disk `sda`. Adapt where necessary.

 `# dd if=''/dev/sda'' bs=512 count=$sectnum | VBoxManage convertfromraw stdin ''windows.vdi'' $(( $sectnum * 512 ))` 

We need to display the size in byte, `$(( $sectnum * 512 ))` will convert the sector numbers to bytes.

*   Since you created your disk image as root, set the right ownership to the virtual disk image: `# chown _your_user_:_your_group_ windows.vdi` 

*   Create your virtual machine configuration file and use the virtual disk created previously as the main virtual hard disk.

*   Try to boot your Windows VM, it may just work. First though remove and repair disks from the boot process as it may interfere (and likely will) booting into safe-mode.

*   Attempt to boot your Windows virtual machine in safe mode (press the F8 key before the Windows logo shows up)... if running into boot issues, read [#Fix MBR and Microsoft bootloader](#Fix_MBR_and_Microsoft_bootloader). In safe-mode, drivers will be installed likely by the Windows plug-and-play detection mechanism [view](http://i.imgur.com/hh1RrSp.png). Additionally, install the VirtualBox Guest Additions via the menu _Devices_ > _Insert Guest Additions CD image..._. If a new disk dialog does not appear, navigate to the CD drive and start the installer manually.

*   You should finally have a working Windows virtual machine. Do not forget to read the [#Known limitations](#Known_limitations).

#### 修复MBR和Microsoft引导

如果您的Windows虚拟机拒绝引导, 你可能需要修复你的虚拟机.

*   Boot a GNU/Live live distribution inside your virtual machine before Windows starts up.

*   Remove other partitions entries from the virtual disk MBR. Indeed, since we copied the MBR and only the Windows partition, the entries of the other partitions are still present in the MBR, but the partitions are not available anymore. Use `fdisk` to achieve this for example.

```
fdisk ''/dev/sda''
Command (m for help): a
Partition number (''1-3'', default ''3''): ''1''
```

*   Write the updated partition table to the disk (this will recreate the MBR) using the `m` command inside `fdisk`.

*   Use [testdisk](https://www.archlinux.org/packages/?name=testdisk) (see [here](http://www.cgsecurity.org/index.html?testdisk.html) for details) to add a generic MBR:

 `# testdisk > _Disk /dev/sda...'_ > [Proceed] >  [Intel] Intel/PC partition > [MBR Code] Write TestDisk MBR to first sector > Write a new copy of MBR code to first sector? (Y/n) > Y > Write a new copy of MBR code, confirm? (Y/N) > A new copy of MBR code has been written. You have to reboot for the change to take effect. > [OK]` 

*   With the new MBR and updated partition table, your Windows virtual machine should be able to boot. If you are still encountering issues, boot your Windows recovery disk from on of the previous step, and inside your Windows RE environment, execute the commands [described here](http://support.microsoft.com/kb/927392).

#### 已知的限制

*   Your virtual machine can sometimes hang and overrun your RAM, this can be caused by conflicting drivers still installed inside your Windows virtual machine. Good luck to find them!
*   Additional software expecting a given driver beneath may either not be disabled/uninstalled or needs to be uninstalled first as the drivers that are no longer available.
*   Your Windows installation must reside on the first partition for the above process to work. If this requirement is not met, the process might be achieved too, but this had not been tested. This will require either copying the MBR and editing in hexadecimal see [VirtualBox: booting cloned disk](http://superuser.com/questions/237782/virtualbox-booting-cloned-disk/253417#253417) or will require to fix the partition table [manually](http://gparted.org/h2-fix-msdos-pt.php) or by repairing Windows with the recovery disk you created in a previous step. Let us consider our Windows installation on the second partition; we will copy the MBR, then the second partition where to the disk image. `VBoxManage convertfromraw` needs the total number of bytes that will be written: calculated thanks to the size of the MBR (the start of the first partition) plus the size of the second (Windows) partition. `{ dd if=/dev/sda bs=512 count=$(cat /sys/block/sda/sda1/start) ; dd if=/dev/sda2 bs=512 count=$(cat /sys/block/sda/sda2/size) ; } | VBoxManage convertfromraw stdin windows.vdi $(( ($(cat /sys/block/sda/sda1/start) + $(cat /sys/block/sda/sda2/size)) * 512 ))`.

## 故障排除

### modprobe Exec 格式错误

确认你使用的是最新系统:

```
pacman -Syu

```

### VERR_ACCESS_DENIED

To access the raw vmdk image on a windows host, run the VirtualBox GUI as administrator.

### 键盘和鼠标都在我的虚拟机

This means your virtual machine has captured the input of your keyboard and your mouse. Simply press the right `Ctrl` key and your input should control your host again.

To control transparently your virtual machine with your mouse going back and forth your host, without having to press any key, and thus have a seamless integration, install the guest additions inside the guest. Read from the [#Install the Guest Additions](#Install_the_Guest_Additions) step if you guest is Arch Linux, otherwise read the official VirtualBox help.

### 无法发送CTRL + ALT+ Fn键到我的虚拟机

Your guest operating system is a GNU/Linux distribution and you want to open a new TTY shell by hitting `Ctrl+Alt+F2` or exit your current X session with `Ctrl+Alt+Backspace`. If you type these keyboard shortcuts without any adaptation, the guest will not receive any input and the host (if it is a GNU/Linux distribution too) will intercept these shortcut keys. To send `Ctrl+Alt+F2` to the guest for example, simply hit your _Host Key_ (usually the right `Ctrl` key) and press `F2` simultaneously.

### 解决ISO映像问题

While VirtualBox can mount ISO images without problem, there are some image formats which cannot reliably be converted to ISO. For instance, ccd2iso ignores .ccd and .sub files, which can give disk images with broken files.

In this case, you will either have to use [CDEmu](/index.php/CDEmu "CDEmu") for Linux inside VirtualBox or any other utility used to mount disk images.

### VirtualBox的GUI没有应用我的GTK主题

See [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications") for information about theming Qt based applications like Virtualbox.

### OpenBSD系统无法使用时，虚拟化指令不可用

While OpenBSD is reported to work fine on other hypervisors without virtualisation instructions (VT-x AMD-V) enabled, an OpenBSD virtual machine running on VirtualBox without these instructions will be unusable, manifesting with a bunch of segmentation faults. Starting VirtualBox with the _-norawr0_ argument [may solve the problem](https://www.virtualbox.org/ticket/3947). You can do it like this:

```
$ VBoxSDL -norawr0 -vm _name_of_OpenBSD_VM_

```

### VBOX_E_INVALID_OBJECT_STATE (0x80BB0007)

这种情形可能会在虚拟机没有正常退出时发生，解除锁定虚拟机并不难:

```
$ VBoxManage controlvm _virtual_machine_name_ poweroff

```

### USB 子系统在宿主机和虚拟机没有作用

Your user must be in the `vboxusers` group, and you need to install the [extension pack](#Extension_pack) if you want USB 2 support. Then you will be able to enable USB 2 in the VM settings and add one or several filters for the devices you want to access from the guest OS.

Sometimes, on old Linux hosts, the USB subsystem is not auto-detected resulting in an error `Could not load the Host USB Proxy service: VERR_NOT_FOUND` or in a not visible USB drive on the host, [even when the user is in the **vboxusers** group](https://bbs.archlinux.org/viewtopic.php?id=121377). This problem is due to the fact that VirtualBox switched from _usbfs_ to _sysfs_ in version 3.0.8\. If the host does not understand this change, you can revert to the old behaviour by defining the following environment variable in any file that is sourced by your shell (e.g. your `~/.bashrc` if you are using _bash_):

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
$ vboxmanage setextradata _virtual_machine_name_ VBoxInternal/CPUM/CMPXCHG16B 1

```

### Windows 8 VM fails to boot with error "ERR_DISK_FULL"

Situation: Your Windows 8 VM refuses to start. VirtualBox throws an error stating the virtual disk is full. However, you are certain that the disk is not full. Bring up your VM's settings at _Settings > Storage > Controller:SATA_ and select "Use Host I/O Cache".

### Linux guests have slow/distorted audio

The AC97 audio driver within the Linux kernel occasionally guesses the wrong clock settings when running inside Virtual Box, leading to audio that is either too slow or too fast. To fix this, create a file in `/etc/modprobe.d` with the following line:

```
options snd-intel8x0 ac97_clock=48000

```

### 客户端启动后的Xorg死机

Faulty or missing drivers may cause the guest to freeze after starting Xorg, see for example [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1167838) and [[2]](https://bbs.archlinux.org/viewtopic.php?id=156079). Try disabling 3D acceleration in _Settings > Display_, and check if all [Xorg](/index.php/Xorg "Xorg") drivers are installed.

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
  <strike><MachineEntry uuid="{00000000-0000-0000-0000-000000000000}" src="/home/void/VirtualBox VMs/lastvmcausingproblems/lastvmcausingproblems.qcow"/></strike>
</MachineRegistry>
...
```

This happens sometimes when selecting _QCOW_/_QCOW2_/_QED_ disk format when creating a new virutal disk.

### USB modem

If you have a USB modem which is being used by the guest OS, killing the guest OS can cause the modem to become unusable by the host system. Killing and restarting `VBoxSVC` should fix this problem.

### "The specified path does not exist. Check the path and then try again." error in Windows guests

This error message often appears when running an .exe file which requires administrator priviliges from a shared folder in windows guests. See [the bug report](https://www.virtualbox.org/ticket/5732) for details.

There are several workarounds:

1.  Disable UAC from Control Panel -> Action Center -> "Change User Account Control settings" from left side pane -> set slider to "Never notify" -> OK and reboot
2.  Copy the file from the shared folder to the guest and run from there
3.  Control Panel -> Network and Internet -> Internet Options -> Security -> Trusted Sites -> Sites -> Add "VBOXSVR" as a website
4.  Start -> type "gpedit.msc" and press Enter -> Computer Configuration -> Administrative Templates -> Windows Components -> Internet Explorer -> Internet Control Panel -> Security Page -> Size to Zone Assignment List -> Add "VBOXSVR" to "2" and reboot

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Haven't tested#3 and #4 workarounds myself. If someone can confirm that they are working as well, please delete this note/template. (Discuss in [Talk:VirtualBox (简体中文)#](https://wiki.archlinux.org/index.php/Talk:VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

### 挂载失败导致的啟动问题

若你在内核升级后 [systemd](/index.php/Systemd "Systemd") 设定遇到问题，你应该透过 `init=/bin/bash` 开啟系统 (如果应急 shell 对你没有作用)。

```
root=/dev/mapper/vg_main-lv_root ro vga=792 resume=/dev/mapper/vg_main-lv_swap init=/bin/bash

```

接著附加写入权限挂载 _root_-文件系统:

```
# mount / -o remount,rw

```

根据 [#Arch Linux 客户机共享文件夹](#Arch_Linux_.E5.AE.A2.E6.88.B7.E6.9C.BA.E5.85.B1.E4.BA.AB.E6.96.87.E4.BB.B6.E5.A4.B9) 更改 `/etc/fstab`]]，然后在 Bash shell 运行 systemd:

```
# exec /bin/systemd

```

### 复制和粘贴在 Arch Linux 客户机没有作用

Since updating `virtualbox-guest-additions` to version `4.2.0-2` copy&paste from Host OS to Arch Linux Guest stopped working. It seems to be due to `VBoxClient-all` requiring _root_ access. In previous versions adding _VBoxClient-all &_ to _~/.xinitrc_ was sufficient to make copy&paste work. Update _~/.xinitrc_ to match `sudo VBoxClient-all &` and add the line `, NOPASSWD: /usr/bin/VBoxClient-all` to your username in the sudoers file and restart X. It should all work again. The line in the sudoers file should look similar to this:

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

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Needs a link to a bug report; vague expressions like "currently" and "at the moment of writing" are of no help. (Discuss in [Talk:VirtualBox (简体中文)#](https://wiki.archlinux.org/index.php/Talk:VirtualBox_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)))

This is a known incompatiblity with SMAP enabled kernels affecting (mostly) Intel Broadwell chipsets.

The matter is currently being investigated, with a wide variety of WIP vboxhost module patches out in the wild that are meant to solve the issue.

At the moment of writing though, the only 100% guaranteed solution to this problem is disabling SMAP support in your kernel by appending the "nosmap" option to your kernel boot command line.

### 向客户端发送CTRL+ALT+F1

如果你的客户端操作系统是Linux发行版，且你又想打开一个新的tty文本shell或者通过键入`Ctrl`+`Alt`+`F1`来退出 X ，你可以简单地敲击你的'Host Key'向客户端操作系统发送这个命令（通常为键盘右边的`Ctrl`） + `F1` 或 `F2`，以此类推。

### 在运行于无显示器的服务器上的系统上启动虚拟机

Add this line to /etc/rc.local

```
exec /bin/su -c 'VBoxManage startvm --type headless <_UUID|NAME_>' _PREFERED_USER_ >/dev/null 2>&1

```

Where <UUID|NAME> is the guest identifier, and PREFERRED_USER is the user profile that contains the VM definitions and .vdi files.

Since exec replaces the currently running process, you will not be able to start a second VM, or execute any other commands, after the exec. Try the following if this is a problem:

```
su -c 'VBoxHeadless -s <_UUID|NAME_> &' -s /bin/sh _PREFERED_USER_ >/dev/null 2>&1

```

Using fully qualified path to su and VBoxHeadless is recommend. Add additional lines like above to start additional VMs. Commands following these in rc.local will be executed. Based on some rooting around in the VBox documentation, I get the impression this will be a little more robust than 'VBoxManage ... --type headless' in future VBox releases.

To determine the available VMs for a user:

```
su -c 'VBoxManage list vms' PREFERED_USER

```

To save the state of a running VM:

```
su -c 'VBoxManage controlvm <UUID|NAME> savestate' PREFERED_USER

```

rc.local.shutdown would be a good spot for this.

### 从主机端访问虚拟机上的服务器

To access apache on a VM from the Host machine ONLY, simply execute the following lines on the Host:

```
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/HostPort" 8888
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/GuestPort" 80
$ VBoxManage setextradata GuestName "VBoxInternal/Devices/pcnet/0/LUN#0/Config/Apache/Protocol" TCP

```

Where 8888 is the port the host should listen on and 80 is the port the VM will send Apache's signal on. To use a port lower than 1024 on the host machine changes need to be made to the firewall on the host machine. This can also be set up to work with SSH, etc.. by changing "Apache" to whatever service and using different ports.

Note: "pcnet" refers to the network card of the VM. If you use an Intel card in your VM settings change "pcnet" to "e1000"

*   from [[3]](http://mydebian.blogdns.org/?p=111)

It might also be necessary to allow connections from the outside to the server in your VM. E.g. if the guest OS is Arch, you may want to add the line

```
httpd: ALL

```

to your /etc/hosts.allow file.

### 守护进程工具

While VirtualBox can mount ISO images without a problem, there are some image formats which cannot reliably be converted to ISO. For instance, ccd2iso ignores .ccd and .sub files, which can give disk images with broken files. cdemu, fuseiso, and MagicISO will do the same. In this case there is no choice but to use Daemon Tools inside VirtualBox.

Recent Daemon Tools versions won't install, so use this old one: [[4]](http://www.disc-tools.com/download/daemon347+hashcalc)

## 参阅

*   [VirtualBox User Manual](https://www.virtualbox.org/manual/UserManual.html)
*   [Wikipedia:VirtualBox](https://en.wikipedia.org/wiki/VirtualBox "wikipedia:VirtualBox")

Retrieved from "[https://wiki.archlinux.org/index.php?title=VirtualBox_(简体中文)&oldid=416302](https://wiki.archlinux.org/index.php?title=VirtualBox_(简体中文)&oldid=416302)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Emulators (简体中文)](/index.php/Category:Emulators_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Emulators (简体中文)")
*   [Virtualization (简体中文)](/index.php/Category:Virtualization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Category:Virtualization (简体中文)")

Hidden categories:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")