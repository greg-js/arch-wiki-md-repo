**翻译状态：** 本文是英文页面 [PCI passthrough via OVMF](/index.php/PCI_passthrough_via_OVMF "PCI passthrough via OVMF") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-08-03，点击[这里](https://wiki.archlinux.org/index.php?title=PCI+passthrough+via+OVMF&diff=0&oldid=532316)可以查看翻译后英文页面的改动。

开放虚拟机固件（Open Virtual Machine Firmware, [OVMF](https://github.com/tianocore/tianocore.github.io/wiki/OVMF))是一个为虚拟机启用 UEFI 支持的项目。Linux 内核 3.9 之后的版本 和近期版本的 [QEMU](/index.php/QEMU "QEMU") ，支持将显卡直通给虚拟机，让虚拟机在执行图形密集型任务的时候有接近实体机的图形性能。

如果你可以为宿主机准备一张备用的显卡（无论是集成显卡还是独立显卡，还是旧的 OEM 卡都可以，品牌不需要一致），并且你的硬件支持 PCI 直通（参见 [#硬件要求](#.E7.A1.AC.E4.BB.B6.E8.A6.81.E6.B1.82)），那么任何操作系统的虚拟机都可以使用一张专用显卡并得到接近于原生的图形性能。请参阅[这篇演讲(PDF)](https://www.linux-kvm.org/images/b/b3/01x09b-VFIOandYou-small.pdf)了解有关技术的更多信息。

## Contents

*   [1 硬件要求](#.E7.A1.AC.E4.BB.B6.E8.A6.81.E6.B1.82)
*   [2 设置IOMMU](#.E8.AE.BE.E7.BD.AEIOMMU)
    *   [2.1 启用IOMMU](#.E5.90.AF.E7.94.A8IOMMU)
    *   [2.2 确保组有效](#.E7.A1.AE.E4.BF.9D.E7.BB.84.E6.9C.89.E6.95.88)
    *   [2.3 注意](#.E6.B3.A8.E6.84.8F)
        *   [2.3.1 如果客户机所用显卡插在 CPU 提供的 PCI-E 插槽中](#.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E6.9C.BA.E6.89.80.E7.94.A8.E6.98.BE.E5.8D.A1.E6.8F.92.E5.9C.A8_CPU_.E6.8F.90.E4.BE.9B.E7.9A.84_PCI-E_.E6.8F.92.E6.A7.BD.E4.B8.AD)
*   [3 隔离GPU](#.E9.9A.94.E7.A6.BBGPU)
*   [4 设置 OVMF 虚拟机](#.E8.AE.BE.E7.BD.AE_OVMF_.E8.99.9A.E6.8B.9F.E6.9C.BA)
    *   [4.1 配置libvirt](#.E9.85.8D.E7.BD.AElibvirt)
    *   [4.2 安装客户机系统](#.E5.AE.89.E8.A3.85.E5.AE.A2.E6.88.B7.E6.9C.BA.E7.B3.BB.E7.BB.9F)
    *   [4.3 附加PCI设备](#.E9.99.84.E5.8A.A0PCI.E8.AE.BE.E5.A4.87)
    *   [4.4 注意](#.E6.B3.A8.E6.84.8F_2)
        *   [4.4.1 OVMF虚拟机不能引导非EFI镜像](#OVMF.E8.99.9A.E6.8B.9F.E6.9C.BA.E4.B8.8D.E8.83.BD.E5.BC.95.E5.AF.BC.E9.9D.9EEFI.E9.95.9C.E5.83.8F)
*   [5 性能调整](#.E6.80.A7.E8.83.BD.E8.B0.83.E6.95.B4)
    *   [5.1 CPU核心固定](#CPU.E6.A0.B8.E5.BF.83.E5.9B.BA.E5.AE.9A)
        *   [5.1.1 CPU 拓扑](#CPU_.E6.8B.93.E6.89.91)
        *   [5.1.2 XML 示例](#XML_.E7.A4.BA.E4.BE.8B)
            *   [5.1.2.1 4c/1t 无超线程的例子](#4c.2F1t_.E6.97.A0.E8.B6.85.E7.BA.BF.E7.A8.8B.E7.9A.84.E4.BE.8B.E5.AD.90)
            *   [5.1.2.2 6c/2t Intel CPU 固定的例子](#6c.2F2t_Intel_CPU_.E5.9B.BA.E5.AE.9A.E7.9A.84.E4.BE.8B.E5.AD.90)
            *   [5.1.2.3 4c/2t AMD CPU 的例子](#4c.2F2t_AMD_CPU_.E7.9A.84.E4.BE.8B.E5.AD.90)
    *   [5.2 内存大分页](#.E5.86.85.E5.AD.98.E5.A4.A7.E5.88.86.E9.A1.B5)
        *   [5.2.1 透明大分页](#.E9.80.8F.E6.98.8E.E5.A4.A7.E5.88.86.E9.A1.B5)
        *   [5.2.2 Static huge pages](#Static_huge_pages)
        *   [5.2.3 Dynamic huge pages](#Dynamic_huge_pages)
    *   [5.3 CPU调速器](#CPU.E8.B0.83.E9.80.9F.E5.99.A8)
    *   [5.4 高DPC延迟](#.E9.AB.98DPC.E5.BB.B6.E8.BF.9F)
        *   [5.4.1 使用isolcpus固定CPU核心](#.E4.BD.BF.E7.94.A8isolcpus.E5.9B.BA.E5.AE.9ACPU.E6.A0.B8.E5.BF.83)
    *   [5.5 提高AMD CPU的性能](#.E6.8F.90.E9.AB.98AMD_CPU.E7.9A.84.E6.80.A7.E8.83.BD)
    *   [5.6 进一步调整](#.E8.BF.9B.E4.B8.80.E6.AD.A5.E8.B0.83.E6.95.B4)
*   [6 特殊步骤](#.E7.89.B9.E6.AE.8A.E6.AD.A5.E9.AA.A4)
    *   [6.1 宿主机和客户机使用相同的GPU](#.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.92.8C.E5.AE.A2.E6.88.B7.E6.9C.BA.E4.BD.BF.E7.94.A8.E7.9B.B8.E5.90.8C.E7.9A.84GPU)
        *   [6.1.1 脚本示例](#.E8.84.9A.E6.9C.AC.E7.A4.BA.E4.BE.8B)
            *   [6.1.1.1 直通除了启动时所用GPU之外的所有GPU](#.E7.9B.B4.E9.80.9A.E9.99.A4.E4.BA.86.E5.90.AF.E5.8A.A8.E6.97.B6.E6.89.80.E7.94.A8GPU.E4.B9.8B.E5.A4.96.E7.9A.84.E6.89.80.E6.9C.89GPU)
            *   [6.1.1.2 直通选定的GPU](#.E7.9B.B4.E9.80.9A.E9.80.89.E5.AE.9A.E7.9A.84GPU)
        *   [6.1.2 脚本安装](#.E8.84.9A.E6.9C.AC.E5.AE.89.E8.A3.85)
    *   [6.2 直通启动时所用的GPU](#.E7.9B.B4.E9.80.9A.E5.90.AF.E5.8A.A8.E6.97.B6.E6.89.80.E7.94.A8.E7.9A.84GPU)
    *   [6.3 使用Looking Glass将客户机画面流式传输到宿主机](#.E4.BD.BF.E7.94.A8Looking_Glass.E5.B0.86.E5.AE.A2.E6.88.B7.E6.9C.BA.E7.94.BB.E9.9D.A2.E6.B5.81.E5.BC.8F.E4.BC.A0.E8.BE.93.E5.88.B0.E5.AE.BF.E4.B8.BB.E6.9C.BA)
        *   [6.3.1 将IVSHMEM设备添加到虚拟机](#.E5.B0.86IVSHMEM.E8.AE.BE.E5.A4.87.E6.B7.BB.E5.8A.A0.E5.88.B0.E8.99.9A.E6.8B.9F.E6.9C.BA)
        *   [6.3.2 将IVSHMEM主机安装到Windows客户机](#.E5.B0.86IVSHMEM.E4.B8.BB.E6.9C.BA.E5.AE.89.E8.A3.85.E5.88.B0Windows.E5.AE.A2.E6.88.B7.E6.9C.BA)
        *   [6.3.3 安装客户端](#.E5.AE.89.E8.A3.85.E5.AE.A2.E6.88.B7.E7.AB.AF)
    *   [6.4 热切换外围设备](#.E7.83.AD.E5.88.87.E6.8D.A2.E5.A4.96.E5.9B.B4.E8.AE.BE.E5.A4.87)
    *   [6.5 分离IOMMU组(ACS补丁)](#.E5.88.86.E7.A6.BBIOMMU.E7.BB.84.28ACS.E8.A1.A5.E4.B8.81.29)
*   [7 仅使用QEMU不使用libvirt](#.E4.BB.85.E4.BD.BF.E7.94.A8QEMU.E4.B8.8D.E4.BD.BF.E7.94.A8libvirt)
*   [8 直通其它设备](#.E7.9B.B4.E9.80.9A.E5.85.B6.E5.AE.83.E8.AE.BE.E5.A4.87)
    *   [8.1 USB控制器](#USB.E6.8E.A7.E5.88.B6.E5.99.A8)
    *   [8.2 使用PulseAudio将虚拟机音频传递给宿主机](#.E4.BD.BF.E7.94.A8PulseAudio.E5.B0.86.E8.99.9A.E6.8B.9F.E6.9C.BA.E9.9F.B3.E9.A2.91.E4.BC.A0.E9.80.92.E7.BB.99.E5.AE.BF.E4.B8.BB.E6.9C.BA)
    *   [8.3 物理磁盘/分区](#.E7.89.A9.E7.90.86.E7.A3.81.E7.9B.98.2F.E5.88.86.E5.8C.BA)
    *   [8.4 注意](#.E6.B3.A8.E6.84.8F_3)
        *   [8.4.1 直通不支持Reset的设备](#.E7.9B.B4.E9.80.9A.E4.B8.8D.E6.94.AF.E6.8C.81Reset.E7.9A.84.E8.AE.BE.E5.A4.87)
*   [9 完整的例子](#.E5.AE.8C.E6.95.B4.E7.9A.84.E4.BE.8B.E5.AD.90)
*   [10 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [10.1 Nvidia GPU直通到Windows 虚拟机时发生"错误43:驱动程序加载失败”](#Nvidia_GPU.E7.9B.B4.E9.80.9A.E5.88.B0Windows_.E8.99.9A.E6.8B.9F.E6.9C.BA.E6.97.B6.E5.8F.91.E7.94.9F.22.E9.94.99.E8.AF.AF43:.E9.A9.B1.E5.8A.A8.E7.A8.8B.E5.BA.8F.E5.8A.A0.E8.BD.BD.E5.A4.B1.E8.B4.A5.E2.80.9D)
    *   [10.2 在启动虚拟机后在dmesg中看到"BAR 3: cannot reserve [mem]"错误](#.E5.9C.A8.E5.90.AF.E5.8A.A8.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.90.8E.E5.9C.A8dmesg.E4.B8.AD.E7.9C.8B.E5.88.B0.22BAR_3:_cannot_reserve_.5Bmem.5D.22.E9.94.99.E8.AF.AF)
    *   [10.3 VBIOS的UEFI (OVMF) 兼容](#VBIOS.E7.9A.84UEFI_.28OVMF.29_.E5.85.BC.E5.AE.B9)
    *   [10.4 HDMI音频不同步或是有噼啪声](#HDMI.E9.9F.B3.E9.A2.91.E4.B8.8D.E5.90.8C.E6.AD.A5.E6.88.96.E6.98.AF.E6.9C.89.E5.99.BC.E5.95.AA.E5.A3.B0)
    *   [10.5 intel_iommu启用之后主机没有HDMI音频输出](#intel_iommu.E5.90.AF.E7.94.A8.E4.B9.8B.E5.90.8E.E4.B8.BB.E6.9C.BA.E6.B2.A1.E6.9C.89HDMI.E9.9F.B3.E9.A2.91.E8.BE.93.E5.87.BA)
    *   [10.6 启用vfio_pci后X无法启动](#.E5.90.AF.E7.94.A8vfio_pci.E5.90.8EX.E6.97.A0.E6.B3.95.E5.90.AF.E5.8A.A8)
    *   [10.7 Chromium忽略集成图形加速](#Chromium.E5.BF.BD.E7.95.A5.E9.9B.86.E6.88.90.E5.9B.BE.E5.BD.A2.E5.8A.A0.E9.80.9F)
    *   [10.8 虚拟机只使用一个核心](#.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.8F.AA.E4.BD.BF.E7.94.A8.E4.B8.80.E4.B8.AA.E6.A0.B8.E5.BF.83)
    *   [10.9 直通貌似工作但没有输出](#.E7.9B.B4.E9.80.9A.E8.B2.8C.E4.BC.BC.E5.B7.A5.E4.BD.9C.E4.BD.86.E6.B2.A1.E6.9C.89.E8.BE.93.E5.87.BA)
    *   [10.10 virt-manager 遇到权限问题](#virt-manager_.E9.81.87.E5.88.B0.E6.9D.83.E9.99.90.E9.97.AE.E9.A2.98)
    *   [10.11 虚拟机关闭之后宿主机核心无响应](#.E8.99.9A.E6.8B.9F.E6.9C.BA.E5.85.B3.E9.97.AD.E4.B9.8B.E5.90.8E.E5.AE.BF.E4.B8.BB.E6.9C.BA.E6.A0.B8.E5.BF.83.E6.97.A0.E5.93.8D.E5.BA.94)
    *   [10.12 客户机在宿主机休眠眠情况下运行导致死机](#.E5.AE.A2.E6.88.B7.E6.9C.BA.E5.9C.A8.E5.AE.BF.E4.B8.BB.E6.9C.BA.E4.BC.91.E7.9C.A0.E7.9C.A0.E6.83.85.E5.86.B5.E4.B8.8B.E8.BF.90.E8.A1.8C.E5.AF.BC.E8.87.B4.E6.AD.BB.E6.9C.BA)
    *   [10.13 AMD显卡直通后无法重启虚拟机](#AMD.E6.98.BE.E5.8D.A1.E7.9B.B4.E9.80.9A.E5.90.8E.E6.97.A0.E6.B3.95.E9.87.8D.E5.90.AF.E8.99.9A.E6.8B.9F.E6.9C.BA)
*   [11 另请参阅](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E9.98.85)

## 硬件要求

VGA直通依赖许多功能。这些功能尚未成为所有硬件的标配，所以您的硬件可能并不支持。如果要使用VGA直通，您的硬件必须满足如下条件：

*   您的CPU必须支持硬件虚拟化（为了使用 kvm）和 IOMMU（为了使用 VGA 直通）。
    *   [Intel CPU 支持列表（VT-x 和 VT-d）](https://ark.intel.com/Search/FeatureFilter?productType=processors&VTD=true)
    *   推土机架构及以后的所有的AMD CPU（包括 Zen）都应支持。
        *   K10架构（2007）的 CPU 不具备 IOMMU，你需要一张[890FX](https://support.amd.com/TechDocs/43403.pdf#page=18)或者[990FX](https://support.amd.com/TechDocs/48691.pdf#page=21)芯片组的主板来使用 IOMMU（这些主板有自己的IOMMU支持）。
*   您的主板必须支持 IOMMU
    *   芯片组和BIOS必须都支持IOMMU。确定是否支持可能不是十分容易（比如，主板说明书一般不会提到这些），但是在 [Xen wiki](https://wiki.xen.org/wiki/VTd_HowTo) 和 [Wikipedia:List of IOMMU-supporting hardware](https://en.wikipedia.org/wiki/List_of_IOMMU-supporting_hardware "wikipedia:List of IOMMU-supporting hardware") 上有一个相当全面的支持列表。
*   分配给客户机的 GPU 的 ROM 必须支持 UEFI
    *   如果你可以在这个[列表](https://www.techpowerup.com/vgabios/)中找到适用您显卡的 ROM，就代表您的显卡可以支持 UEFI。所有2012年之后的显卡都应该支持 UEFI，因为微软将 UEFI 支持作为 Windows 8 兼容认证的必须条件。

您可能需要一台备用或者支持多个输入的显示器连接到显卡。如果没有连接显示器，那么直通的显卡不会有任何输出，并且使用 Spcie 或是 VNC 连接到虚拟机并不会让直通的显卡工作，换言之，没有任何使用 VGA 直通所带来的性能提升。您可能还需要准备一套备用的键鼠或是能通过 SSH 连接到宿主机的设备，如果虚拟机的配置出现了什么问题，您至少还可以控制宿主机。

## 设置IOMMU

**注意:**

*   IOMMU 是 Intel VT-d 和 AMD-Vi 的通用名称。
*   VT-d 指的是直接输入/输出虚拟化(Intel Virtualization Technology for Directed I/O)，不应与VT-x(x86平台下的Intel虚拟化技术，Intel Virtualization Technology)混淆。VT-x 可以让一个硬件平台作为多个“虚拟”平台，而 VT-d 提高了虚拟化的安全性、可靠性和 I/O 性能。

打开IOMMU之后可以使用 PCI Passthrough 和对于故障和恶意行为的内存保护。参见：[wikipedia:Input-output memory management unit#Advantages](https://en.wikipedia.org/wiki/Input-output_memory_management_unit#Advantages "wikipedia:Input-output memory management unit") 以及 [Memory Management (computer programming): Could you explain IOMMU in plain English?](https://www.quora.com/Memory-Management-computer-programming/Could-you-explain-IOMMU-in-plain-English)。

### 启用IOMMU

确保您的 CPU 支持 AMD-Vi/Intel Vt-d 并且已经在 BIOS 中打开。通常这个选项会在类似“其他 CPU 特性”的菜单里，也有可能隐藏在超频选项之中。选项可能就叫做 “VT-d” 或者 “AMD-Vi” ，也有可能是更通用的名称，比如“虚拟化技术”之类。有可能您主板的手册并不会解释这些。

设置[内核参数](/index.php/Kernel_parameters "Kernel parameters")以启用 IOMMU，注意不同品牌的 CPU 所需的内核参数并不同。

*   对于 Intel CPU(VT-d)，使用 `intel_iommu=on`。
*   对于 AMD CPU(AMD-Vi)，使用 `amd_iommu=on`。

您同时需要设置`iommu=pt`，这将防止Linux试图接触(touching)无法直通的设备。

在重启之后，检查 dmesg 以确认 IOMMU 已经被正确启用：

 `dmesg | grep -e DMAR -e IOMMU` 
```
[    0.000000] ACPI: DMAR 0x00000000BDCB1CB0 0000B8 (v01 INTEL  BDW      00000001 INTL 00000001)
[    0.000000] Intel-IOMMU: enabled
[    0.028879] dmar: IOMMU 0: reg_base_addr fed90000 ver 1:0 cap c0000020660462 ecap f0101a
[    0.028883] dmar: IOMMU 1: reg_base_addr fed91000 ver 1:0 cap d2008c20660462 ecap f010da
[    0.028950] IOAPIC id 8 under DRHD base  0xfed91000 IOMMU 1
[    0.536212] DMAR: No ATSR found
[    0.536229] IOMMU 0 0xfed90000: using Queued invalidation
[    0.536230] IOMMU 1 0xfed91000: using Queued invalidation
[    0.536231] IOMMU: Setting RMRR:
[    0.536241] IOMMU: Setting identity map for device 0000:00:02.0 [0xbf000000 - 0xcf1fffff]
[    0.537490] IOMMU: Setting identity map for device 0000:00:14.0 [0xbdea8000 - 0xbdeb6fff]
[    0.537512] IOMMU: Setting identity map for device 0000:00:1a.0 [0xbdea8000 - 0xbdeb6fff]
[    0.537530] IOMMU: Setting identity map for device 0000:00:1d.0 [0xbdea8000 - 0xbdeb6fff]
[    0.537543] IOMMU: Prepare 0-16MiB unity mapping for LPC
[    0.537549] IOMMU: Setting identity map for device 0000:00:1f.0 [0x0 - 0xffffff]
[    2.182790] [drm] DMAR active, disabling use of stolen memory

```

### 确保组有效

这个脚本将输出您的 PCI 设备是如何被分配到 IOMMU 组之中的。如果这个脚本没有输出任何东西，这代表您并没有启用 IOMMU 支持或者是您的硬件不支持 IOMMU。

```
#!/bin/bash
shopt -s nullglob
for d in /sys/kernel/iommu_groups/*/devices/*; do 
    n=${d#*/iommu_groups/*}; n=${n%%/*}
    printf 'IOMMU Group %s ' "$n"
    lspci -nns "${d##*/}"
done;

```

例子：

```
IOMMU Group 0 00:00.0 Host bridge [0600]: Intel Corporation 2nd Generation Core Processor Family DRAM Controller [8086:0104] (rev 09)
IOMMU Group 1 00:16.0 Communication controller [0780]: Intel Corporation 6 Series/C200 Series Chipset Family MEI Controller #1 [8086:1c3a] (rev 04)
IOMMU Group 2 00:19.0 Ethernet controller [0200]: Intel Corporation 82579LM Gigabit Network Connection [8086:1502] (rev 04)
IOMMU Group 3 00:1a.0 USB controller [0c03]: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #2 [8086:1c2d] (rev  
...

```

一个 IOMMU 组是将物理设备直通给虚拟机的最小单位（这不意味着您必须直通整个 USB 控制器，单独的 USB 设备，如键盘鼠标，可以单独设置直通）。例如，在上面的例子中，在 06:00.0 上的显卡和在6:00.1上的音频控制器被分配到13组，它们必须一起直通给虚拟机。前置 USB 控制器被分在了单独的一组（第2组），并不和 USB 扩展控制器（第10组）和后置USB控制器（第4组）分在一组，这意味着它们都可以在[不影响其它设备的情况下直通给虚拟机](#USB.E6.8E.A7.E5.88.B6.E5.99.A8)。

### 注意

#### 如果客户机所用显卡插在 CPU 提供的 PCI-E 插槽中

并非所有的PCI-E插槽均相同。许多主板同时具有 CPU 提供和 PCH 提供的 PCI-E 插槽。根据 CPU 不同，可能您 CPU 提供的 PCI-E 插槽并不能正确隔离。在这种情况下，PCI-E 插槽本身和所连接设备将分在同一组。

```
IOMMU Group 1 00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port (rev 09)
IOMMU Group 1 01:00.0 VGA compatible controller: NVIDIA Corporation GM107 [GeForce GTX 750] (rev a2)
IOMMU Group 1 01:00.1 Audio device: NVIDIA Corporation Device 0fbc (rev a1)

```

如果上一节的脚本输出类似这样，那么您的 PCI-E 插槽就属于上面所述的情况。根据您在 PCI-E 插槽上连接的设备和PCI-E插槽是由PCH还是CPU提供的，您可能发现在需要被直通的组中还有其它的设备，您必须将整个组中的设备全部直通给虚拟机。如果您愿意这样做的话，那么就可以继续。否则，您需要尝试将显卡插入其他的 PCI-E 插槽（如果有的话）并查看这些插槽是否能正确隔离。您也可以安装 ACS 补丁来绕过这个限制，不过这也有相应的缺点。要获得关于 ACS 补丁的更多信息，请参阅[#分离IOMMU组(ACS补丁)](#.E5.88.86.E7.A6.BBIOMMU.E7.BB.84.28ACS.E8.A1.A5.E4.B8.81.29)

**注意:** 如果您需要直通的设备像这样和其他的设备分在一组，那么PCI根设备 （pci root ports） 和 PCI Bridge **不**应在启动时绑定到vfio，也**不**应添加到虚拟机。

## 隔离GPU

为了将设备分配给虚拟机，此设备和同在一个IOMMU组的所有设备必须将驱动程序更换为 stub 或是 vfio ，以防止宿主机尝试与其交互。对于大多数设备，在虚拟机启动时就可以完成这项工作。

但是，由于它们的大小和复杂性，GPU 驱动程序并不倾向于支持动态的重新绑定。所以一般您不能将宿主机所使用的显卡直通给虚拟机，这会导致驱动程序之间的冲突。因此，通常情况下建议在启动虚拟机之前手动绑定这些占位 (placeholder) 驱动，防止其他驱动程序尝试认领 (claim) 设备。

以下部分详细地介绍了如何配置GPU，以便在启动过程中尽早绑定这些占位 (placeholder) 驱动程序，这会使设备处于非活动状态，直到虚拟机认领 (claim) 设备或是切换到其他驱动程序。这是首选方法，因为相比于系统完全启动之后再切换驱动程序，这种方法要简单许多。

**警告:** 在配置完成并重新启动之后，无论您配置的 GPU 是什么，它都将无法在宿主机上使用，直到您取消配置。在执行操作之前，确保您要在宿主机上使用的GPU 已经被正确配置，并且您也应该在BIOS中将宿主机所使用的GPU设为主要GPU。

从 Linux 4.1 开始，内核包括了 `vfio-pci` 。这是一个 VFIO 驱动程序，与 `pci-stub` 的作用相同。但它可以在一定程度上控制设备，例如在不使用设备的时候将它们切换到 D3 状态。

 `$ modinfo vfio-pci` 
```
filename:       /lib/modules/4.4.5-1-ARCH/kernel/drivers/vfio/pci/vfio-pci.ko.gz
description:    VFIO PCI - User Level meta-driver
author:         Alex Williamson <alex.williamson@redhat.com>
...

```

`vfio-pci`通常通过 ID 来定位 PCI 设备，这意味着您只需要指定设备的ID就可以完成绑定。对于下面的 IOMMU 组，您可能希望将`vfio-pci`与 `10de:13c2` 和 `10de:0fbb` 绑定，这将作为本章节其余部分的示例值。

```
IOMMU Group 13 06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
IOMMU Group 13 06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)}}

```

**注意:** 如果宿主机和客户机所使用的GPU设备ID相同（例如是同一型号）那么就不能使用供应商-设备ID来指定需要隔离的设备。如果是这种情况，参见 [#宿主机和客户机使用相同的GPU](#.E5.AE.BF.E4.B8.BB.E6.9C.BA.E5.92.8C.E5.AE.A2.E6.88.B7.E6.9C.BA.E4.BD.BF.E7.94.A8.E7.9B.B8.E5.90.8C.E7.9A.84GPU)。

您需要加载`vfio-pci`，并将设备-供应商ID参数传递给内核。

 `/etc/modprobe.d/vfio.conf`  `options vfio-pci ids=10de:13c2,10de:0fbb` 
**注意:** 像上面提到过的一样，[#如果客户机所用显卡插在 CPU 提供的 PCI-E 插槽中](#.E5.A6.82.E6.9E.9C.E5.AE.A2.E6.88.B7.E6.9C.BA.E6.89.80.E7.94.A8.E6.98.BE.E5.8D.A1.E6.8F.92.E5.9C.A8_CPU_.E6.8F.90.E4.BE.9B.E7.9A.84_PCI-E_.E6.8F.92.E6.A7.BD.E4.B8.AD)，并且 PCI 根设备是 IOMMU 组的一部分，**不**要将根设备的 ID 传递给`vfio-pci`，因为他需要连接到宿主机以保持正常运行。但是，该组中的任何其它设备都应该绑定到`vfio-pci`。

但是，这并不能保证`vfio-pci`会在其它图形驱动之前加载。为了确保这一点，我们需要在initramfs中静态绑定它和它的依赖项。按照`vfio_pci`，`vfio`，`vfio_iommu_type1`，`vfio_virqfd` 的顺序添加到[mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")：

 `/etc/mkinitcpio.conf`  `MODULES=(... vfio_pci vfio vfio_iommu_type1 vfio_virqfd ...)` 
**注意:** 如果您还有另一个驱动程序以这种方式进行[Early modesetting](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting")，例如`nouveau`，`radeon`，`amdgpu`，`i915`等等，则上述的所有 vfio 模块都必须在它们之前。

另外，确保 modconf hook 在`mkinitcpio.conf`的 HOOKS 列表中：

 `/etc/mkinitcpio.conf`  `HOOKS=(... modconf ...)` 

由于新模块已添加到 initramfs 配置中，因此必须[重新生成initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")。如果您在`/etc/modprobe.d/vfio.conf`修改了设备ID，您同样需要重新生成它。以便在早期启动过程得知需要隔离的设备。

重启并验证`vfio-pci`是否已经正确加载并绑定到正确的设备：

 `$ dmesg | grep -i vfio` 
```
[    0.329224] VFIO - User Level meta-driver version: 0.3
[    0.341372] vfio_pci: add [10de:13c2[ffff:ffff]] class 0x000000/00000000
[    0.354704] vfio_pci: add [10de:0fbb[ffff:ffff]] class 0x000000/00000000
[    2.061326] vfio-pci 0000:06:00.0: enabling device (0100 -> 0103)

```

`vfio.conf`中所绑定的设备（甚至是需要直通的设备）并不一定会出现在 dmesg 的输出之中。有时尽管设备没有出现在 dmesg 的输出中，但实际上在虚拟机中可以被使用。

 `$ lspci -nnk -d 10de:13c2` 
```
06:00.0 VGA compatible controller: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	Kernel driver in use: vfio-pci
	Kernel modules: nouveau nvidia

```
 `$ lspci -nnk -d 10de:0fbb` 
```
06:00.1 Audio device: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)
	Kernel driver in use: vfio-pci
	Kernel modules: snd_hda_intel

```

## 设置 OVMF 虚拟机

OVMF是一个为QEMU虚拟机开发的开源UEFI固件，虽然您可以使用 SeaBIOS 来获得和 PCI 直通类似的结果，但设置过程并不相同。如果您的硬件支持，则最好使用EFI方法。

### 配置libvirt

[Libvirt](/index.php/Libvirt "Libvirt") 是许多虚拟化实用程序的包装，可以极大的简化虚拟机的配置和部署过程。对于 KVM 和 QEMU ，它提供的前端让我们避免处理 QEMU 的权限，并使得在现有的虚拟机上添加和删除设备更加容易。但是，作为一个包装，它可能并不总是支持最新的 QEMU 功能，最终可能需要一些提供的脚本为 QEMU 传递一些额外的参数。

安装[qemu](https://www.archlinux.org/packages/?name=qemu)、[libvirt](https://www.archlinux.org/packages/?name=libvirt)、[ovmf](https://www.archlinux.org/packages/?name=ovmf)和[virt-manager](https://www.archlinux.org/packages/?name=virt-manager)之后，将您的 OVMF 固件映像和运行时变量模板添加到 libvirt 配置中，以便让 `virt-install`或是`virt-manager` 可以找到它们。

 `/etc/libvirt/qemu.conf` 
```
nvram = [
	"/usr/share/ovmf/x64/OVMF_CODE.fd:/usr/share/ovmf/x64/OVMF_VARS.fd"
]
```

您现在可以[启用](/index.php/Enable "Enable")并[启动](/index.php/Start "Start")`libvirtd.service`和它的日志记录组件`virtlogd.socket`。

### 安装客户机系统

使用 `virt-manager` 配置虚拟机的大部分过程都无需指导，只要按照屏幕上的提示即可。

如果使用`virt-manager`，则必须将用户添加到 `libvirt` [组](/index.php/User_group "User group")。

但是，您仍应该特别注意如下步骤：

*   在虚拟机创建向导要求您命名虚拟机时（点击“完成”前的最后一步），勾选“在安装前自定义配置”。
*   在“概况”屏幕，将“固件”选为["UEFI"](https://i.imgur.com/73r2ctM.png)，如果您不能选择它，检查是否在`/etc/libvirt/qemu.conf`正确配置了固件的路径并且[重新启动](/index.php/Restart "Restart")了`libvirtd.service`。

*   在“CPUs”屏幕，将CPU型号改为"`host-passthrough`"。如果它不在列表中，则您必须手动输入。这确保您的CPU会被正确检测，从而能使 libvirt 完全暴露您 CPU 的功能，而不是仅仅是它所识别到的那些（这会让 CPU 按默认行为运作）。如果不进行这项设置，某些程序可能会抱怨说您的 CPU 型号是未知的。
*   如果要最小化IO开销，请点击“添加硬件”，并在“控制器：中选择“SCSI”类型，型号为 "VirtIO SCSI"。你可以将默认的 IDE 磁盘改为 SCSI 磁盘，并绑定到上述的控制器。
    *   Windows 不包含VirtIO驱动程序，所以你需要从[这里](https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/latest-virtio/)下载包含驱动程序的 ISO 并且添加一个IDE CDROM（Windows 8.1之后可以使用SATA）并且连接到刚才的 ISO 。否则在安装过程中 Windows 无法识别 VirtIO 控制器。当 Windows 安装程序要求您选择要安装的磁盘时，加载 CD-ROM 下 visscsi 目录下的驱动程序。

其余的安装过程将使用在窗口中运行的标准QXL图形适配器进行。此时，无需为其余虚拟设备安装驱动程序，因为一些虚拟设备将被删除。客户机操作系统安装完成之后，只需要关闭虚拟机即可。您还可能会直接进入UEFI菜单，而不是自动从安装程序引导。客户机在启动的时候可能并未检测到正确的ISO文件，您需要手动指定引导顺序。点击“exit”并选择“boot manager”，您将会进入一个选择引导设备的菜单。

### 附加PCI设备

当安装完成之后，就可以编辑libvirt中的硬件详情并且删除一些虚拟设备。例如spcie通道和虚拟显示器，QXL图形适配器，虚拟鼠标键盘以及数位板设备。由于您没有可用的输入设备，您可能还想将几个主机上的USB设备附加到虚拟机。但请记住，**至少为宿主机留下一个鼠标和/或键盘**，防止客户机出现问题的时候无法操作宿主机。此时，可以添加先前隔离的PCI设备。只需单击“添加硬件”然后选择需要使用的PCI主机设备。如果一切顺利，连接到GPU的显示器上应该会显示OVMF启动画面，并可以正常启动。您可以在这时安装其他的驱动程序。

### 注意

#### OVMF虚拟机不能引导非EFI镜像

OVMF固件不支持启动非EFI介质。如果启动虚拟机之后您直接看到了UEFI Shell，可能是您的引导介质无效。尝试使用其他的引导映像来确定问题。

## 性能调整

使用PCI直通多数涉及性能密集型领域，例如游戏或是GPU加速任务。虽然PCI直通本身就是实现原生性能的一步，但宿主机和客户机仍可以通过一些调整来提升性能。

### CPU核心固定

默认情况下，KVM将虚拟机的操作作为虚拟处理器的多个线程运行（The default behavior for KVM guests is to run operations coming from the guest as a number of threads representing virtual processors）。这些线程由Linux调度程序管理，如同其他线程一样。并根据 niceness 和 priority 分配给任何可用的CPU核心。因此，当线程切换到另一个核心时，核心的高速缓存将无法发挥作用，这可能会显著影响虚拟机的性能。CPU核心固定旨在解决这些问题，因为它会忽略Linux的线程调度并确保虚拟机的线程始终在特定的内核上运行。例如客户机的核心 0,1,2,3 分别映射到宿主机的 4,5,6,7 核心。

**注意:** 某些启用CPU核心固定的用户可能会遇到卡顿和短暂挂起的问题。尤其是在使用MuQSS调度程序的情况下（存在与linux-ck内核和linux-zen内核）。如果遇到类似的问题，您可能需要首先禁用固定，保证始终具有最大的即时响应性能。

#### CPU 拓扑

大多数现代CPU都支持硬件多任务处理，即 Intel CPU 上的超线程或 AMD CPU 上的 SMT。 超线程/SMT 让一个物理核心具有两个虚拟线程。您需要根据虚拟机和宿主机的用途来设置 CPU 核心固定。

要查看您的 CPU 拓扑，运行 `lscpu -e`：

**注意:** 需要特别注意 **"CORE"** 栏，它表明了虚拟核心和物理核心的对应关系。

6c/12t Ryzen 5 1600 上的 `lscpu -e` 输出：

```
CPU NODE SOCKET CORE L1d:L1i:L2:L3 ONLINE MAXMHZ    MINMHZ
0   0    0      0    0:0:0:0       yes    3800.0000 1550.0000
1   0    0      0    0:0:0:0       yes    3800.0000 1550.0000
2   0    0      1    1:1:1:0       yes    3800.0000 1550.0000
3   0    0      1    1:1:1:0       yes    3800.0000 1550.0000
4   0    0      2    2:2:2:0       yes    3800.0000 1550.0000
5   0    0      2    2:2:2:0       yes    3800.0000 1550.0000
6   0    0      3    3:3:3:1       yes    3800.0000 1550.0000
7   0    0      3    3:3:3:1       yes    3800.0000 1550.0000
8   0    0      4    4:4:4:1       yes    3800.0000 1550.0000
9   0    0      4    4:4:4:1       yes    3800.0000 1550.0000
10  0    0      5    5:5:5:1       yes    3800.0000 1550.0000
11  0    0      5    5:5:5:1       yes    3800.0000 1550.0000

```

6c/12t Intel 8700k 上的 `lscpu -e` 输出：

```
CPU NODE SOCKET CORE L1d:L1i:L2:L3 ONLINE MAXMHZ    MINMHZ
0   0    0      0    0:0:0:0       yes    4600.0000 800.0000
1   0    0      1    1:1:1:0       yes    4600.0000 800.0000
2   0    0      2    2:2:2:0       yes    4600.0000 800.0000
3   0    0      3    3:3:3:0       yes    4600.0000 800.0000
4   0    0      4    4:4:4:0       yes    4600.0000 800.0000
5   0    0      5    5:5:5:0       yes    4600.0000 800.0000
6   0    0      0    0:0:0:0       yes    4600.0000 800.0000
7   0    0      1    1:1:1:0       yes    4600.0000 800.0000
8   0    0      2    2:2:2:0       yes    4600.0000 800.0000
9   0    0      3    3:3:3:0       yes    4600.0000 800.0000
10  0    0      4    4:4:4:0       yes    4600.0000 800.0000
11  0    0      5    5:5:5:0       yes    4600.0000 800.0000

```

如上所示，对于上面的 AMD CPU，CPU 0 和 CPU 1 对应 CORE 0，对于上面的英特尔 CPU，CPU 0 和 CPU 6 对应 CORE 0。

如果您不需要虚拟机使用所有核心，那么最好给宿主机留下一个核心。选择要用于宿主机或虚拟机的核心应该基于CPU的特定硬件特性，但在大多数情况下，“CORE0”是宿主机的不错选择。如果为宿主机保留了任何核心，建议将模拟器和 iothreads（如果使用）固定到宿主机核心而不是虚拟 CPU 上。这可以提高性能并减少虚拟机的延迟，因为这些线程不会污染缓存或争抢虚拟 CPU 线程调度。如果虚拟机需要使用所有核心，那么固定模拟器或 iothreads 是没有必要的。

#### XML 示例

**注意:** 如果你的磁盘控制器没有启用 **iothread**，那就不要使用下面例子中的 **iothread**。**iothread**只在**virtio-scsi** 或是 **virtio-blk** 设备上工作。

##### 4c/1t 无超线程的例子

 `$ virsh edit [vmname]` 
```
...
<vcpu placement='static'>4</vcpu>
<cputune>
    <vcpupin vcpu='0' cpuset='0'/>
    <vcpupin vcpu='1' cpuset='1'/>
    <vcpupin vcpu='2' cpuset='2'/>
    <vcpupin vcpu='3' cpuset='3'/>
</cputune>
...

```

##### 6c/2t Intel CPU 固定的例子

 `$ virsh edit [vmname]` 
```
...
<vcpu placement='static'>8</vcpu>
<iothreads>1</iothreads>
<cputune>
    <vcpupin vcpu='0' cpuset='2'/>
    <vcpupin vcpu='1' cpuset='8'/>
    <vcpupin vcpu='2' cpuset='3'/>
    <vcpupin vcpu='3' cpuset='9'/>
    <vcpupin vcpu='4' cpuset='4'/>
    <vcpupin vcpu='5' cpuset='10'/>
    <vcpupin vcpu='6' cpuset='5'/>
    <vcpupin vcpu='7' cpuset='11'/>
    <emulatorpin cpuset='0,6'/>
    <iothreadpin iothread='1' cpuset='0,6'/>
</cputune>
    ...
    <topology sockets='1' cores='4' threads='2'/>
    ...

```

##### 4c/2t AMD CPU 的例子

 `$ virsh edit [vmname]` 
```
...
<vcpu placement='static'>8</vcpu>
<iothreads>1</iothreads>
<cputune>
  <vcpupin vcpu='0' cpuset='2'/>
  <vcpupin vcpu='1' cpuset='3'/>
  <vcpupin vcpu='2' cpuset='4'/>
  <vcpupin vcpu='3' cpuset='5'/>
  <vcpupin vcpu='4' cpuset='6'/>
  <vcpupin vcpu='5' cpuset='7'/>
  <vcpupin vcpu='6' cpuset='8'/>
  <vcpupin vcpu='7' cpuset='9'/>
  <emulatorpin cpuset='0-1'/>
  <iothreadpin iothread='1' cpuset='0-1'/>
</cputune>
    ...
    <topology sockets='1' cores='4' threads='2'/>
    ...

```

**注意:** 如果你需要进一步的 CPU 隔离，考虑在未使用的物理/虚拟核心上使用 **isolcpus** 内核选项。

如果您不打算在使用虚拟机时在宿主机上进行计算繁重的工作（或是根本不打算在宿主机上做任何事情），您可以将虚拟线程固定在所有核心上以便充分使用 CPU 时间。不过，固定所有物理和虚拟核心可能会导致虚拟机出现延迟。

但是，在具有PCI直通的虚拟机上，从透明大分页中受益是**不可能**的。因为 IOMMU 要求在虚拟机启动之后立即分配所有内存。因此，必须使用静态大分页才能从中受益。

**警告:** 静态大分页会锁定分配的内存。未配置使用它们的应用程序不能使用这些内存、在具有8GB内存的计算机上分配4GB的大分页，**无论虚拟机是否运行**，宿主机都只有4GB的可用内存。

要在引导时分配大分页，必须使用`hugepages=*x*`在内核命令行中指定。例如，使用`hugepages=1024`保留1024个大分页，每个大分页的默认大小为2048kB，分配2GB的大分页。

如果CPU支持，则可以手动设置分页大小。`grep pdpe1gb /proc/cpuinfo`可以验证1GB的大页面支持。通过内核参数设置1GB的大分页`default_hugepagesz=1G hugepagesz=1G hugepages=X transparent_hugepage=never`。

此外，由于静态大分页只能由专门请求它的应用程序使用，因此必须在libvirt配置中添加此部分让kvm从中受益。

 `$ virsh edit [vmname]` 
```
...
<memoryBacking>
	<hugepages/>
</memoryBacking>
...

```

### 内存大分页

在处理需要大量内存的应用程序时，内存延迟可能会是一个问题，因为使用的内存分页越多，程序尝试跨分页访问信息的可能性就越高（页是基本的内存分配单位）。将分页解析为实际的内存地址需要多个步骤，因此CPU通常将信息缓存在最近使用的分页上，以加快后续的内存使用。使用大量内存的应用程序可能会遇到内存性能问题：例如，虚拟机使用 4GB 内存，分页大小为 4KB（这是普通分页的默认大小），总共104万页，这意味着缓存命中率可能会大幅降低并大幅增加内存延迟。大分页通过向应用程序提供更大的单个分页来缓解这个问题，从而增加了多个操作中连续位于同一分页的几率。

#### 透明大分页

QEMU 将在 QEMU 或 Libvirt 中自动使用 2 MiB 大小的透明大分页，但这可能并不那么顺利，在使用 VFIO 时，页面会在启动时锁定，并且在虚拟机首次启动时会预先分配透明的大分页。如果内存高度碎片化，或者虚拟机正在使用大部分剩余内存，则内核可能没有足够的2 MiB 页面来完全满足分配。在这种情况下，将会混合使用使用 2 MiB 和 4 KiB 分页，从而无法得到足够的性能提升。由于分页在 VFIO 模式下被锁定，因此内核无法在虚拟机启动后将这些 4 KiB 分页转换为大分页。THP（透明大分页）可用的 2 MiB 大页面数量与通过以下各节中描述的[#动态大分页](#.E5.8A.A8.E6.80.81.E5.A4.A7.E5.88.86.E9.A1.B5)机制相同。

要查看全局使用的 THP 内存量：

```
$ grep AnonHugePages /proc/meminfo
AnonHugePages:   8091648 kB

```

要查看特定 QEMU 实例所使用的 THP ，需要指定 QEMU 的 PID：

```
$ grep -P 'AnonHugePages:\s+(?!0)\d+' /proc/[PID]/smaps
AnonHugePages:   8087552 kB

```

在这个例子中，虚拟机分配了 8388608 KiB 的内存，但只有 8087552 KiB 可通过 THP 获得。 剩下的301056KiB被分配为 4 KiB 分页。没有任何警告提示使用了 4 KiB 分页。因此，THP 的有效性在很大程度上取决于虚拟机启动时宿主机系统的内存碎片。如果这是不可接受的，建议使用[#固定大分页](#.E5.9B.BA.E5.AE.9A.E5.A4.A7.E5.88.86.E9.A1.B5)。

Arch 内核已经编译并默认启用了 THP，默认为 `madvise` 模式。可在 `/sys/kernel/mm/transparent_hugepage/enabled` 查看。

#### Static huge pages

While transparent huge pages should work in the vast majority of cases, they can also be allocated statically during boot. This should only be needed to make use 1 GiB hugepages on machines that support it, since transparent huge pages normally only go up to 2 MiB.

**Warning:** Static huge pages lock down the allocated amount of memory, making it unavailable for applications that are not configured to use them. Allocating 4 GiBs worth of huge pages on a machine with 8 GiB of memory will only leave you with 4 GiB of available memory on the host **even when the VM is not running**.

To allocate huge pages at boot, one must simply specify the desired amount on their kernel command line with `hugepages=*x*`. For instance, reserving 1024 pages with `hugepages=1024` and the default size of 2048 KiB per huge page creates 2 GiB worth of memory for the virtual machine to use.

If supported by CPU page size could be set manually. 1 GiB huge page support could be verified by `grep pdpe1gb /proc/cpuinfo`. Setting 1 GiB huge page size via kernel parameters : `default_hugepagesz=1G hugepagesz=1G hugepages=X`.

Also, since static huge pages can only be used by applications that specifically request it, you must add this section in your libvirt domain configuration to allow kvm to benefit from them :

 `$ virsh edit [vmname]` 
```
...
<memoryBacking>
	<hugepages/>
</memoryBacking>
...

```

#### Dynamic huge pages

Hugepages could be allocated manually via `vm.nr_overcommit_hugepages` [sysctl](/index.php/Sysctl "Sysctl") parameter.

 `/etc/sysctl.d/10-kvm.conf` 
```
vm.nr_hugepages = 0
vm.nr_overcommit_hugepages = *num*
```

Where `*num*` - is the number of huge pages, which default size if 2 MiB. Pages will be automatically allocated, and freed after VM stops.

More manual way:

```
# echo *num* > /sys/kernel/mm/hugepages/hugepages-2048kB/nr_hugepages
# echo *num* > /sys/kernel/mm/hugepages/hugepages-1048576kB/nr_hugepages

```

For 2 MiB and 1 GiB page size respectively. And they should be manually freed in the same way.

It is hardly recommended to drop caches, compact memory and wait couple of seconds before starting VM, as there could be not enough free contiguous memory for required huge pages blocks. Especially after some uptime of the host system.

```
# echo 3 > /proc/sys/vm/drop_caches
# echo 1 > /proc/sys/vm/compact_memory

```

Theoretically, 1 GiB pages works as 2 MiB. But practically - no guaranteed way was found to get contiguous 1 GiB memory blocks. Each consequent request of 1 GiB blocks lead to lesser and lesser dynamically allocated count.

### CPU调速器

根据您[CPU 调速器](/index.php/CPU_frequency_scaling "CPU frequency scaling")的配置方式，虚拟机的线程可能无法达到负载阈值以提升频率。实际上，KVM 自身无法更改 CPU 频率，如果 CPU 频率并不能随着虚拟 CPU 的负载使用而提升，这可能是一个严重的性能问题。检查此问题最简单的方法是在虚拟机上运行 CPU 密集型任务的同时在宿主机上运行`watch lscpu`检查CPU频率是否上升。如果您的 CPU 频率无法正常上升且无法达到所报告的最大值，可能是由于[主机操作系统限制了 CPU 升频](https://lime-technology.com/forum/index.php?topic=46664.msg447678#msg447678)。这种情况下，尝试手动将所有CPU内核设为最大频率查看是否能够提升性能。请注意，如果您使用带有默认pstate驱动程序的现代Intel芯片，则cpupower命令[无效](/index.php/CPU_frequency_scaling#CPU_frequency_driver "CPU frequency scaling")，因此请监视`/proc/cpuinfo`确保您的CPU处于最大频率。

### 高DPC延迟

如果您在虚拟中遇到了高DPC和/或中断延迟，请确保已在主机内核上[加载](/index.php/Kernel_modules#Manual_module_handling "Kernel modules")了所需的VirtIO内核模块，可加载的VirtIO内核模块包括：`virtio-pci`，`virtio-net`，`virtio-blk`，`virtio-balloon`，`virtio-ring`和`virtio`。

加载一个或多个这些模块后，在宿主机上执行`lsmod | grep virtio`不应返回空。

#### 使用isolcpus固定CPU核心

此外，确保您已正确隔离CPU。 在本例中，我们假设您使用的是CPU 4-7。 使用内核参数`isolcpus nohz_full rcu_nocbs`将CPU与内核完全隔离。

 `sudo vim /etc/defaults/grub` 
```
...
GRUB_CMDLINE_LINUX="..your other params.. isolcpus=4-7 nohz_full=4-7 rcu_nocbs=4-7"
...

```

然后，用taskset和chrt运行`qemu-system-x86_64`：

```
# chrt -r 1 taskset -c 4-7 qemu-system-x86_64 ...

```

`chrt`命令将确保任务调度程序将循环分配工作（否则它将全部停留在第一个cpu上）。 对于`taskset`，CPU编号可以用“，”和“/”或"-"分隔，如“0,1,2,3”或“0-4”或“1,7-8,10”等。

参考reddit上的这篇[帖子](https://www.reddit.com/r/VFIO/comments/6vgtpx/high_dpc_latency_and_audio_stuttering_on_windows/dm0sfto/)了解详情。

### 提高AMD CPU的性能

以前，由于一个非常老的[bug](https://sourceforge.net/p/kvm/bugs/230/)，必须在运行 KVM 的 AMD 系统上禁用嵌套页表（NPT）以提高 GPU 性能，但这将降低 CPU 性能，导致卡顿。

有一个[内核补丁](https://patchwork.kernel.org/patch/10027525/)可以解决这个问题，它已经在4.14-stable和4.9-stable 版本被接受了。 如果你正在运行官方的[linux](https://www.archlinux.org/packages/?name=linux)或[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)内核，那么该补丁被已经应用了（请确保你使用的是最新内核）。如果您正在运行另一个内核，您可能需要手动应用补丁。

**注意:** 几个Ryzen用户（请参阅这个Reddit[帖子](https://www.reddit.com/r/VFIO/comments/78i3jx/possible_fix_for_the_npt_issue_discussed_on_iommu/)）已经测试了该补丁，并且可以确认它有效，使GPU直通性能接近原生性能。

### 进一步调整

[Red Hat的虚拟化调试和优化指南（中文）](https://access.redhat.com/documentation/zh-cn/red_hat_enterprise_linux/7/html/virtualization_tuning_and_optimization_guide/)中提供了更专业的VM调优技巧。 如果您遇到以下情况，本指南可能特别有用：

*   在从虚拟中下载/上传期间，主机CPU负载较高，请参阅“桥接零复制传输”了解可能的修复。
*   尽管使用了virtio-net，但是在下载/上传期间，访客网络速度有限制。请参阅“多队列virtio-net”以获得可能的修复。
*   在没有达到负载极限的情况下，虚拟机在高I/O下卡顿。请参阅“多队列virtio-scsi”以获得获得可能的修复。

## 特殊步骤

某些机器需要特定的配置调整才能正常工作。 如果您在的宿主机或虚拟机不能正常工作，请查看您的系统是否符合以下情况之一，并尝试相应地调整配置。

### 宿主机和客户机使用相同的GPU

由于`vfio-pci`如何使用您的供应商和设备ID对来识别需要在启动时绑定哪个设备，如果您的两个GPU 具有相同的ID，您将无法让您的直通驱动程序只与一个绑定。这种情况下必须使用脚本完成配置，无论您使用哪个驱动程序，都需要使用`driver_override`机制由pci总线地址完成分配。

#### 脚本示例

##### 直通除了启动时所用GPU之外的所有GPU

在`/usr/bin/vfio-pci-override.sh`，创建一个脚本让`vfio-pci`绑定除了启动时所用GPU之外的所有GPU。

```
#!/bin/sh

for i in /sys/devices/pci*/*/boot_vga; do
	if [ $(cat "$i") -eq 0 ]; then
		GPU="${i%/boot_vga}"
		AUDIO="$(echo "$GPU" | sed -e "s/0$/1/")"
		echo "vfio-pci" > "$GPU/driver_override"
		if [ -d "$AUDIO" ]; then
			echo "vfio-pci" > "$AUDIO/driver_override"
		fi
	fi
done

modprobe -i vfio-pci

```

##### 直通选定的GPU

手动指定需要绑定的GPU。

```
#!/bin/sh

GROUP="0000:00:03.0"
DEVS="0000:03:00.0 0000:03:00.1 ."

if [ ! -z "$(ls -A /sys/class/iommu)" ]; then
	for DEV in $DEVS; do
		echo "vfio-pci" > /sys/bus/pci/devices/$GROUP/$DEV/driver_override
	done
fi

modprobe -i vfio-pci

```

#### 脚本安装

创建`/etc/modprobe.d/vfio.conf`，内容如下:

```
install vfio-pci /usr/bin/vfio-pci-override.sh

```

编辑`/etc/mkinitcpio.conf`:

从`MODULES`中移除所有图形驱动程序，并添加`vfio-pci`和`vfio_iommu_type1`

```
MODULES=(ext4 vfat vfio-pci vfio_iommu_type1)

```

将`/etc/modprobe.d/vfio.conf`和`/usr/bin/vfio-pci-override.sh`添加到`FILES`

```
FILES=(/etc/modprobe.d/vfio.conf /usr/bin/vfio-pci-override.sh)

```

[重新生成initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")并重新启动。

### 直通启动时所用的GPU

标记为`boot_vga`的GPU在进行PCI直通时比较特殊，BIOS需要使用它才能显示启动消息或BIOS配置菜单等内容。为了完成达到这个目的，需要[创建一个可以被自由修改的VGA boot ROM 副本](https://www.redhat.com/archives/vfio-users/2016-May/msg00224.html)。这个副本可以让系统得知，但直通驱动程序可能会认为这是一个非法的版本。如果可能的话，从BIOS设置中调整启动GPU。如果没有相关选项，调换宿主机和客户机GPU的位置。

### 使用Looking Glass将客户机画面流式传输到宿主机

通过使用[Looking Glass](https://looking-glass.hostfission.com/)，可以让宿主机和客户机共享显示器，同时将键盘鼠标动作传递给虚拟机。

#### 将IVSHMEM设备添加到虚拟机

Looking glass通过在主机和来宾之间创建共享内存缓冲区来完成传输。这比通过localhost流式传输帧快得多，但需要额外的设置。

关闭你的虚拟机，修改配置：

 `$ virsh edit [vmname]` 
```
...
<devices>
    ...
  <shmem name='looking-glass'>
    <model type='ivshmem-plain'/>
    <size unit='M'>32</size>
  </shmem>
</devices>
...

```

您应该根据您要传输的分辨率将32替换为您自己所需要的值。计算方法如下：

```
宽 x 高 x 4 x 2 = 总比特数
总比特数 / 1024 / 1024 = 兆比特数 + 2

```

例如，分辨率为1920x1080

```
1920 x 1080 x 4 x 2 = 16,588,800 比特
16,588,800 / 1024 / 1024 = 15.82 MB + 2 = 17.82

```

实际上的数字应该是**大于**计算的得数的一个**2的幂**，因为17.82大于16，所以应该选择32。

接下来使用一个脚本创建共享内存文件。

 `/usr/local/bin/looking-glass-init.sh` 
```
#!/bin/sh

touch /dev/shm/looking-glass
chown **user**:kvm /dev/shm/looking-glass
chmod 660 /dev/shm/looking-glass
```

将`user`改为你的用户名。

记得为脚本授予[可执行](/index.php/Executable "Executable")权限。

创建一个[systemd](/index.php/Systemd "Systemd")单元文件，以便在开机时创建这个文件。

 `/etc/systemd/system/looking-glass-init.service` 
```
[Unit]
Description=Create shared memory for looking glass

[Service]
Type=oneshot
ExecStart=/usr/local/bin/looking-glass-init.sh

[Install]
WantedBy=multi-user.target
```

[启动](/index.php/Start "Start")并[启用](/index.php/Enable "Enable") `looking-glass-init.service`。

#### 将IVSHMEM主机安装到Windows客户机

目前Windows不会通知用户发现新的IVSHMEM设备，它会默默安装虚拟驱动程序。要实际启用该设备，您必须进入设备管理器并在“系统设备”下为“PCI标准RAM控制器”更新设备的驱动程序。因为它在其他地方尚未提供，所以必须从[issue 217](https://github.com/virtio-win/kvm-guest-drivers-windows/issues/217)下载签名的驱动程序。

安装驱动程序后，您必须下载最新的[looking-glass-host](https://looking-glass.hostfission.com/downloads)，然后在您的客户机上启动它。为了运行它，您还需要安装[Microsoft Visual C ++ Redistributable](https://www.visualstudio.com/downloads/)。可以通过编辑`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run`注册表并添加路径来自动启动它。

#### 安装客户端

Looking glass 客户端可以通过 [looking-glass](https://aur.archlinux.org/packages/looking-glass/)或[looking-glass-git](https://aur.archlinux.org/packages/looking-glass-git/) 安装。

**警告:** 如果你在使用[looking-glass-git](https://aur.archlinux.org/packages/looking-glass-git/)时出现问题，请选择[looking-glass](https://aur.archlinux.org/packages/looking-glass/)。git版本并不受上游支持，可能在任何时候破损。只有带有版本号的发布受到支持，并且保证能与Windows客户机上的主机程序一起使用。

当客户机配置完成之后，您可以通过如下方式运行运行客户端：

```
$ looking-glass-client

```

如果您不想通过spcie传递键盘和鼠标的话，你可以禁用它：

```
$ looking-glass-client -s

```

您也可能希望全屏运行客户端，因为图像缩放会导致质量下降：

```
$ looking-glass-client -F

```

使用`--help`选项查看更多信息。

### 热切换外围设备

Looking Glass 包含一个spcie客户端，以便控制Windows客户机。然而，对于某些应用程序，例如游戏，可能延迟太高了。另一种方法是直通特定的USB设备以尽可能地降低延迟。可以在主机和客户机之间热切换设备。

首先为您想要直通的设备创建一个`.xml`文件，libvirt使用该文件来识别设备。

 `/home/$USER/.VFIOinput/input_1.xml` 
```
<hostdev mode='subsystem' type='usb' managed='no'>
<source>
<vendor id='0x[Before Colon]'/>
<product id='0x[After Colon]'/>
</source>
</hostdev>
```

将`[before / After Colon]`替换为`lsusb`命令的内容，取决于于您要传递的设备。

例如，我的鼠标是`Bus 005 Device 002: ID 1532:0037 Razer USA, Ltd`，所以我的`vendor id` 是 1532，`product id` 是 1037。

重复以上步骤以添加所有想要直通的USB设备。如果您的键盘/鼠标在`lsusb`中有多个条目，那么请为每个条目创建.xml文件。

**注意:** 不要忘记更改上方和下方脚本的路径和名称，以匹配您的环境。

接下来需要创建一个bash脚本来告诉libvirt附加/分离设备。

 `/home/$USER/.VFIOinput/input_attach.sh` 
```
#!/bin/bash

virsh attach-device [VM-Name] [USBdevice]
```

将`[VM-Name]`替换为您的虚拟机名称，名称可以在virt-manager下看到。另外，将`[USBdevice]`替换为您希望传递的设备的.xml文件的**完整**路径。为多个设备添加额外的行。例如，这是我的脚本：

 `/home/ajmar/.VFIOinput/input_attach.sh` 
```
#!/bin/bash

virsh attach-device win10 /home/ajmar/.VFIOinput/input_mouse.xml
virsh attach-device win10 /home/ajmar/.VFIOinput/input_keyboard.xml
```

接下来复制脚本文件并用`detach-device`替换`attach-device`。并为每个脚本设置可执行权限。

现在可以执行这2个脚本，以将USB设备附加/分离到客户机。注意它们可能需要以root身份执行。要从Windows客户机运行脚本，您可以使用[PuTTY](/index.php/PuTTY "PuTTY") [SSH](/index.php/SSH "SSH")连接到主机，然后执行脚本。在Windows上，PuTTY附带了plink.exe，它可以通过SSH执行单一命令，然后自动关闭，而不是打开SSH终端。

 `detach_devices.bat`  `"C:\Program Files\PuTTY\plink.exe" root@$HOST_IP -pw $ROOTPASSWORD /home/$USER/.VFIOinput/input_detach.sh` 

用宿主机[IP 地址](/index.php/Network_configuration#IP_addresses "Network configuration")替换`$HOST_IP`，用root密码替换`$ROOTPASSWORD`。

**警告:** 如果有人可以访问您的虚拟机，则此方法并不安全，因为他们可以打开文件并读取您的ROOT密码。建议使用[SSH keys](/index.php/SSH_keys "SSH keys")！

您可能还希望使用快捷键来执行脚本文件。在Windows上，您可以使用[Autohotkey](https://autohotkey.com/)，在宿主机上可以使用[Xbindkeys](/index.php/Xbindkeys "Xbindkeys")，您的桌面环境也可能提供快捷键设置。 由于需要以root身份运行脚本，您可能还需要使用[Polkit](/index.php/Polkit "Polkit")，从而无需输入密码。

**提示：**

*   （译注）如果您配置了Polkit无密码授权，那么这个脚本也可以使用您自己的用户来执行。参见[Libvirt (简体中文)#设置授权](/index.php/Libvirt_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.AE.BE.E7.BD.AE.E6.8E.88.E6.9D.83 "Libvirt (简体中文)")和[Polkit (简体中文)#跳过口令提示](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.B7.B3.E8.BF.87.E5.8F.A3.E4.BB.A4.E6.8F.90.E7.A4.BA "Polkit (简体中文)").
*   （译注）您也可以使用Windows 10 自带的 OpenSSH，使用方法和Linux下相同，参见[Secure Shell#OpenSSH](/index.php/Secure_Shell#OpenSSH "Secure Shell")。

### 分离IOMMU组(ACS补丁)

如果您发现您的PCI设备与其他不希望直通的设备分在一组，您可以使用Alex Williamson的ACS补丁将它们分离。使用前请确保了解其中的[潜在风险](https://vfio.blogspot.com/2014/08/iommu-groups-inside-and-out.html)。

您需要一个应用了这个补丁的内核，最简单的办法就是安装[linux-vfio](https://aur.archlinux.org/packages/linux-vfio/)包。

此外，需要使用内核命令行选项启用ACS补丁。补丁文件添加以下文档：

```
pcie_acs_override =
        [PCIE] Override missing PCIe ACS support for:
    downstream
        All downstream ports - full ACS capabilties
    multifunction
        All multifunction devices - multifunction ACS subset
    id:nnnn:nnnn
        Specfic device - full ACS capabilities
        Specified as vid:did (vendor/device ID) in hex

```

使用选项`pcie_acs_override=downstream`通常就足够了。

安装和配置后，设置[内核参数](/index.php/Kernel_parameters "Kernel parameters")以在启用`pcie_acs_override=`选项的情况下加载新内核。

## 仅使用QEMU不使用libvirt

如果不想在libvirt的帮助下设置虚拟机，可以使用具有自定义参数的普通QEMU命令来运行要使用PCI直通的虚拟机，这对于脚本等一些用例来说是十分理想的，可以灵活地搭配其他脚本。

先完成[#设置IOMMU](#.E8.AE.BE.E7.BD.AEIOMMU)和[#隔离GPU](#.E9.9A.94.E7.A6.BBGPU)，接着配置好[QEMU](/index.php/QEMU "QEMU")虚拟化环境,[启用KVM](/index.php/QEMU#Enabling_KVM "QEMU")并使用`-device vfio-pci,host=07:00.0`选项，将`07:00.0`替换为您先前隔离的设备ID。

要使用OVMF固件，确保已安装[ovmf](https://www.archlinux.org/packages/?name=ovmf)，将UEFI固件从`/usr/share/ovmf/x64/OVMF_VARS.fd`复制到临时位置，如`/tmp/MY_VARS.fd`。最后指定OVMF路径。使用如下的参数（注意顺序）：

*   `-drive if=pflash,format=raw,readonly,file=/usr/share/ovmf/x64/OVMF_CODE.fd` 指向实际的位置，注意这是只读的
*   `-drive if=pflash,format=raw,file=/tmp/MY_VARS.fd` 指向临时位置

**注意:** 可以使用QEMU的默认SeaBIOS而不是OVMF，但不推荐使用它，因为它可能会导致直通设置出现问题。

建议通过使用[virtio驱动程序](/index.php/QEMU#Installing_virtio_drivers "QEMU")并进一步配置，以增强性能,参阅[QEMU](/index.php/QEMU "QEMU")。

您还可能必须使用`-cpu host,kvm=off`参数将主机的CPU型号信息转发给虚拟机，并欺骗Nvidia和其他制造商的设备驱动程序使用的虚拟化检测，防止驱动程序拒绝在虚拟机中运行。

## 直通其它设备

### USB控制器

如果你的主板具有多个USB控制器并映射到不同的组，则可以直通这些控制器而不是单个USB设备。直通整个控制器有如下的优势：

*   如果设备在某些操作（例如正在进行更新的手机）的过程中断开或更改ID，虚拟机不会突然丢失设备。
*   由该控制器管理的任何USB端口都由虚拟机直接处理，并且可以将其设备拔出，重新插入和更改，而无需通知管理程序。
*   如果启动VM时通常直通给虚拟机的其中一个USB设备丢失，Libvirt将不会抱怨。

与GPU不同，大多数USB控制器的驱动程序不需要任何特定配置即可在VM上运行，并且通常可以在主机和客户机系统之间来回传递控制而不会产生任何副作用。

**警告:** 确保您的USB控制器支持Reset。[#直通不支持Reset的设备](#.E7.9B.B4.E9.80.9A.E4.B8.8D.E6.94.AF.E6.8C.81Reset.E7.9A.84.E8.AE.BE.E5.A4.87)

您可以使用以下命令找出哪个PCI设备对应于哪个控制器以及每个端口和设备对应哪个控制器：

 `$ for usb_ctrl in $(find /sys/bus/usb/devices/usb* -maxdepth 0 -type l); do pci_path="$(dirname "$(realpath "${usb_ctrl}")")"; echo "Bus $(cat "${usb_ctrl}/busnum") --> $(basename $pci_path) (IOMMU group $(basename $(realpath $pci_path/iommu_group)))"; lsusb -s "$(cat "${usb_ctrl}/busnum"):"; echo; done` 
```
Bus 1 --> 0000:00:1a.0 (IOMMU group 4)
Bus 001 Device 004: ID 04f2:b217 Chicony Electronics Co., Ltd Lenovo Integrated Camera (0.3MP)
Bus 001 Device 007: ID 0a5c:21e6 Broadcom Corp. BCM20702 Bluetooth 4.0 [ThinkPad]
Bus 001 Device 008: ID 0781:5530 SanDisk Corp. Cruzer
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

Bus 2 --> 0000:00:1d.0 (IOMMU group 9)
Bus 002 Device 006: ID 0451:e012 Texas Instruments, Inc. TI-Nspire Calculator
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

款笔记本电脑有3个USB端口，由2个USB控制器管理，每个控制器都有自己的IOMMU组。 在此示例中，总线001管理单个USB端口（其中插入了SanDisk USB记忆棒，因此它显示在列表中），还有许多内部设备，例如内部网络摄像头和蓝牙卡。 另一方面，除了插入的计算器之外，总线002不会管理其他东西。第三个端口是空的，这就是它没有出现在列表中的原因，但实际上是由总线002管理的。

确定需要直通的控制器之后，只需将其添加到虚拟机控制的PCI主机设备列表中即可。不需要其他配置。

**注意:** 如果您的USB控制器不支持Reset，不在单独的组中，或者无法直通，您仍然可以通过[udev](/index.php/Udev "Udev")规则达到类似的目的。参见[[1]](https://github.com/olavmrk/usb-libvirt-hotplug)，它允许连接到指定USB端口的任何设备自动连接到虚拟机。

### 使用PulseAudio将虚拟机音频传递给宿主机

可以使用libvirt将虚拟机的音频作为应用程序传输到宿主机。 这具有以下优点：多个音频流可传输到一个主机输出，并且与无需考虑音频设备是否支持直通。[PulseAudio](/index.php/PulseAudio "PulseAudio") 是必需的。

PulseAudio守护进程通常在你的普通用户下运行，并且只接受来自相同用户的连接。然而libvirt默认使用root运行QEMU。为了让QEMU在普通用户下运行，编辑`/etc/libvirt/qemu.conf`并将`user`设置为你的用户名。

```
user = "dave"

```

你同样需要告诉QEMU使用PulseAudio后端并识别要连接的服务器，首先将QEMU命名空间添加到你的域。 编辑域的`.xml`文件（使用`virsh edit domain`），将`domain type`行改为：

```
<domain type='kvm' xmlns:qemu='[http://libvirt.org/schemas/domain/qemu/1.0'](http://libvirt.org/schemas/domain/qemu/1.0')>

```

并且加入如下的配置（在最后一个`</devices>`之后，`</domain>`之前）：

```
 <qemu:commandline>
   <qemu:env name='QEMU_AUDIO_DRV' value='pa'/>
   <qemu:env name='QEMU_PA_SERVER' value='/run/user/1000/pulse/native'/>
 </qemu:commandline>

```

`1000`是你的用户ID，如果必要的话改为你的用户ID，用户ID可以通过`id`命令查看。

请记住在继续之前保存文件并退出编辑器，否则更改将不会保存。如果您看到：“已更改域 [名称] XML配置”或是类似的消息，这表示您的更改已保存。

[重启](/index.php/Restart "Restart") `libvirtd.service` 和 [用户服务](/index.php/Systemd/User "Systemd/User") `pulseaudio.service`。

现在，虚拟机音频将作为应用程序传递给宿主机。[pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol)可用于控制输出设备。请注意，在Windows客户机上，[不使用消息信号中断可能会导致出现噼啪声](#HDMI.E9.9F.B3.E9.A2.91.E4.B8.8D.E5.90.8C.E6.AD.A5.E6.88.96.E6.98.AF.E6.9C.89.E5.99.BC.E5.95.AA.E5.A3.B0)。

### 物理磁盘/分区

可以通过向XML添加条目来使用整个磁盘或分区来提高I/O性能。

 `$ virsh edit [vmname]` 
```

<devices>
...
  <disk type='block' device='disk'>
    <driver name='qemu' type='raw' cache='none' io='native'/>
    <source dev='/dev/sdXX'/>
    <target dev='vda' bus='virtio'/>
    <address type='pci' domain='0x0000' bus='0x02' slot='0x0a' function='0x0'/>
  </disk>
...
</devices>

```

在Windows客户机上需要安装驱动程序才能工作，请参阅[#安装客户机系统](#.E5.AE.89.E8.A3.85.E5.AE.A2.E6.88.B7.E6.9C.BA.E7.B3.BB.E7.BB.9F)。

### 注意

#### 直通不支持Reset的设备

当虚拟机关闭时，虚拟机使用的所有设备都会被其操作系统取消初始化，以准备关闭。在这种状态下，这些设备不再能使用，必须先重新上电才能恢复正常运行。Linux可以自己处理这种电源循环，但是当设备没有已知的Reset方法时，它将于禁用状态并不再可用。Libvirt和Qemu都希望所有宿主机的PCI设备在完全停止虚拟机之前准备好重新连接到宿主机，当遇到不会重置的设备时，虚拟机将挂起“关闭”状态，并将无法重新启动，除非宿主机系统重新启动。 因此，推荐仅直通支持重置的PCI设备，这可以通过PCI设备sysfs节点中存在`reset`文件来确定，例如`/sys/bus/pci/devices/0000:00:1a.0/reset`。

以下bash命令显示设备是否可以被Reset。

 `for iommu_group in $(find /sys/kernel/iommu_groups/ -maxdepth 1 -mindepth 1 -type d);do echo "IOMMU group $(basename "$iommu_group")"; for device in $(\ls -1 "$iommu_group"/devices/); do if [[ -e "$iommu_group"/devices/"$device"/reset ]]; then echo -n "[RESET]"; fi; echo -n $'\t';lspci -nns "$device"; done; done` 
```
IOMMU group 0
	00:00.0 Host bridge [0600]: Intel Corporation Xeon E3-1200 v2/Ivy Bridge DRAM Controller [8086:0158] (rev 09)
IOMMU group 1
	00:01.0 PCI bridge [0604]: Intel Corporation Xeon E3-1200 v2/3rd Gen Core processor PCI Express Root Port [8086:0151] (rev 09)
	01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GK208 [GeForce GT 720] [10de:1288] (rev a1)
	01:00.1 Audio device [0403]: NVIDIA Corporation GK208 HDMI/DP Audio Controller [10de:0e0f] (rev a1)
IOMMU group 2
	00:14.0 USB controller [0c03]: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller [8086:1e31] (rev 04)
IOMMU group 4
[RESET]	00:1a.0 USB controller [0c03]: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 [8086:1e2d] (rev 04)
IOMMU group 5
[RESET]	00:1b.0 Audio device [0403]: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller [8086:1e20] (rev 04)
IOMMU group 10
[RESET]	00:1d.0 USB controller [0c03]: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 [8086:1e26] (rev 04)
IOMMU group 13
	06:00.0 VGA compatible controller [0300]: NVIDIA Corporation GM204 [GeForce GTX 970] [10de:13c2] (rev a1)
	06:00.1 Audio device [0403]: NVIDIA Corporation GM204 High Definition Audio Controller [10de:0fbb] (rev a1)

```

这表示`00：14.0`中的xHCI USB控制器无法Reset，将导致虚拟机无法正常关闭，而在`00：1b.0`中的集成声卡和在`00：1a.0`和`00:1d.0`中的其他两个控制器没有这个问题，可以毫无问题地直通。

**注意:** 如果你的AMD显卡无法正常Reset，参阅[#AMD显卡直通后无法重启虚拟机](#AMD.E6.98.BE.E5.8D.A1.E7.9B.B4.E9.80.9A.E5.90.8E.E6.97.A0.E6.B3.95.E9.87.8D.E5.90.AF.E8.99.9A.E6.8B.9F.E6.9C.BA)。

## 完整的例子

如果您在配置的时候遇到了麻烦，您可以参考[完整的配置示例](/index.php/PCI_passthrough_via_OVMF/Examples "PCI passthrough via OVMF/Examples")。一些用户在那里描述了它们的配置步骤，或许您可以从中发现一些技巧。

## 疑难解答

如果您遇到的问题并没有在下面列出，您也可以参考[QEMU#Troubleshooting](/index.php/QEMU#Troubleshooting "QEMU")。

### Nvidia GPU直通到Windows 虚拟机时发生"错误43:驱动程序加载失败”

> *"Accidental"* breakage, won't fix, unsupported (**"意外"**损坏，不修复，不支持)
> — [NVIDIA](https://www.linux-kvm.org/images/b/b3/01x09b-VFIOandYou-small.pdf)

**注意:**

*   这也可能修复与Nvidia驱动程序相关的SYSTEM_THREAD_EXCEPTION_NOT_HANDLED引导失败。
*   这可能也会修复Linux虚拟机的问题，

从337.88开始，Windows上的Nvidia驱动程序将会检查虚拟机管理程序是否正在运行，如果检测到虚拟机管理程序，则会拒绝加载，这会导致Windows设备管理器出现错误43。从QEMU 2.5.0和libvirt 1.3.3开始，可以设置虚假的vendor_id，这足以欺骗Nvidia驱动程序。所需的步骤是将`hv_vendor_id=随便什么的`添加到QEMU命令行中的cpu参数，或者将以下行添加到libvirt的域配置中。 ID必须设置为12个字符的字母数字（例如'1234567890ab'）。

 `$ virsh edit [vmname]` 
```
...
<features>
	<hyperv>
		...
		<vendor_id state='on' value='whatever'/>
		...
	</hyperv>
	...
	<kvm>
	<hidden state='on'/>
	</kvm>
</features>
...

```

使用旧版QEMU和/或libvirt的用户将必须禁用一些虚拟机管理程序扩展，这会大大降低性能。如果必须这样做的话，请在libvirt域配置文件中执行以下替换。

 `$ virsh edit [vmname]` 
```
...
<features>
	<hyperv>
		<relaxed state='on'/>
		<vapic state='on'/>
		<spinlocks state='on' retries='8191'/>
	</hyperv>
	...
</features>
...
<clock offset='localtime'>
	<timer name='hypervclock' present='yes'/>
</clock>
...

```

```
...
<clock offset='localtime'>
	<timer name='hypervclock' present='no'/>
</clock>
...
<features>
	<kvm>
	<hidden state='on'/>
	</kvm>
	...
	<hyperv>
		<relaxed state='off'/>
		<vapic state='off'/>
		<spinlocks state='off'/>
	</hyperv>
	...
</features>
...

```

### 在启动虚拟机后在dmesg中看到"BAR 3: cannot reserve [mem]"错误

查看[这篇文章](https://www.linuxquestions.org/questions/linux-kernel-70/kernel-fails-to-assign-memory-to-pcie-device-4175487043/):

如果你仍然遇到错误43，请在启动虚拟机后检查dmesg是否存在内存保留错误，如果您有类似消息，则可能是这种情况：

```
vfio-pci 0000:09:00.0: BAR 3: cannot reserve [mem 0xf0000000-0xf1ffffff 64bit pref]

```

找出您的GPU所连接的PCI Bridge。这条命令将给出设备的实际层次结构：

```
$ lspci -t

```

在启动VM之前运行以下命令，将ID替换为来自先前输出的实际ID。

```
# echo 1 > /sys/bus/pci/devices/0000\:00\:03.1/remove
# echo 1 > /sys/bus/pci/rescan

```

**注意:** 可能需要同时设置[内核参数](/index.php/Kernel_parameter "Kernel parameter") `video=efifb:off`。 [[2]](https://pve.proxmox.com/wiki/Pci_passthrough#BAR_3:_can.27t_reserve_.5Bmem.5D_error)

### VBIOS的UEFI (OVMF) 兼容

With respect to [this article](https://pve.proxmox.com/wiki/Pci_passthrough#How_to_known_if_card_is_UEFI_.28ovmf.29_compatible):

Error 43 can be caused by the GPU's VBIOS without UEFI support. To check whenever your VBIOS supports it, you will have to use `rom-parser`:

```
$ git clone [https://github.com/awilliam/rom-parser](https://github.com/awilliam/rom-parser)
$ cd rom-parser && make

```

Dump the GPU VBIOS:

```
# echo 1 > /sys/bus/pci/devices/0000:01:00.0/rom
# cat /sys/bus/pci/devices/0000:01:00.0/rom > /tmp/image.rom
# echo 0 > /sys/bus/pci/devices/0000:01:00.0/rom

```

And test it for compatibility:

 `$ ./rom-parser /tmp/image.rom` 
```
Valid ROM signature found @600h, PCIR offset 190h
	PCIR: type 0 (x86 PC-AT), vendor: 10de, device: 1184, class: 030000
	PCIR: revision 0, vendor revision: 1
Valid ROM signature found @fa00h, PCIR offset 1ch
	PCIR: type 3 (EFI), vendor: 10de, device: 1184, class: 030000
	PCIR: revision 3, vendor revision: 0
		EFI: Signature Valid, Subsystem: Boot, Machine: X64
	Last image

```

To be UEFI compatible, you need a "type 3 (EFI)" in the result. If it's not there, try updating your GPU VBIOS. GPU manufacturers often share VBIOS upgrades on their support pages. A large database of known compatible and working VBIOSes (along with their UEFI compatibility status!) is available on [TechPowerUp](https://www.techpowerup.com/vgabios/).

Updated VBIOS can be used in the VM without flashing. To load it in QEMU:

```
-device vfio-pci,host=07:00.0,......,romfile=/path/to/your/gpu/bios.bin \

```

And in libvirt:

```
<hostdev>
     ...
     <rom file='/path/to/your/gpu/bios.bin'/>
     ...
   </hostdev>
```

One should compare VBIOS versions between host and guest systems using [nvflash](https://www.techpowerup.com/download/nvidia-nvflash/) (Linux versions under *Show more versions*) or [GPU-Z](https://www.techpowerup.com/download/techpowerup-gpu-z/) (in Windows guest). To check the currently loaded VBIOS:

 `$ ./nvflash --version` 
```
...
Version               : 80.04.XX.00.97
...
UEFI Support          : No
UEFI Version          : N/A
UEFI Variant Id       : N/A ( Unknown )
UEFI Signer(s)        : Unsigned
...

```

And to check a given VBIOS file:

 `$ ./nvflash --version NV299MH.rom` 
```
...
Version               : 80.04.XX.00.95
...
UEFI Support          : Yes
UEFI Version          : 0x10022 (Jul  2 2013 @ 16377903 )
UEFI Variant Id       : 0x0000000000000004 ( GK1xx )
UEFI Signer(s)        : Microsoft Corporation UEFI CA 2011
...

```

If the external ROM did not work as it should in the guest, you will have to flash the newer VBIOS image to the GPU. In some cases it is possible to create your own VBIOS image with UEFI support using [GOPUpd](https://www.win-raid.com/t892f16-AMD-and-Nvidia-GOP-update-No-requests-DIY.html) tool, however this is risky and may result in GPU brick.

**Warning:** Failure during flashing may "brick" your GPU - recovery may be possible, but rarely easy and often requires additional hardware. **DO NOT** flash VBIOS images for other GPU models (different boards may use different VBIOSes, clocks, fan configuration). If it breaks, you get to keep all the pieces.

In order to avoid the irreparable damage to your graphics adapter it is necessary to unload the NVIDIA kernel driver first:

```
# modprobe -r nvidia_modeset nvidia 

```

Flashing the VBIOS can be done with:

```
# ./nvflash romfile.bin

```

**Warning:** **DO NOT** interrupt the flashing process, even if it looks like it's stuck. Flashing should take about a minute on most GPUs, but may take longer.

### HDMI音频不同步或是有噼啪声

对于一些用户来说，虚拟机的音频会在显卡上通过HDMI输出一段时间后减慢/卡顿。这通常也会降低图形处理速度。可能的解决方案包括启用MSI（基于消息信号的中断）而不是默认（基于线路的中断）。

要检查是否支持MSI以及是否被启用，请以root身份运行以下命令：

```
# lspci -vs $device | grep 'MSI:'

```

`$device`是设备位置 (例如 `01:00.0`)。

输出应该类似于：

```
Capabilities: [60] MSI: Enable**-** Count=1/1 Maskable- 64bit+

```

`Enable`后的`-`代表支持MSI，但虚拟机并没有启用。`+`代表虚拟机正在使用MSI。

启用它的过程有些复杂，可以在[此处](https://forums.guru3d.com/showthread.php?t=378044)找到说明。

其他的提示可以从[lime-technology's wiki](https://lime-technology.com/wiki/index.php/UnRAID_6/VM_Guest_Support#Enable_MSI_for_Interrupts_to_Fix_HDMI_Audio_Support)上找到， 或参考这篇帖子[VFIO tips and tricks](https://vfio.blogspot.it/2014/09/vfio-interrupts-and-how-to-coax-windows.html)。

网上有一些一些工具，例如 `MSI_util`，不过它们在 Windows 10 64bit下无效。

要解决这个问题，仅仅在function 0(`01:00.0 VGA compatible controller: NVIDIA Corporation GM206 [GeForce GTX 960] (rev a1) (prog-if 00 [VGA controller])`)上启用MSI是不够的，另一个function(`01:00.1 Audio device: NVIDIA Corporation Device 0fba (rev a1)`)同样需要启用。

### intel_iommu启用之后主机没有HDMI音频输出

如果启用 `intel_iommu`后，Intel GPU的HDMI输出设备在宿主机上无法使用，那么设置选项`igfx_off`（即`intel_iommu=on,igfx_off`）可能会恢复音频，有关设置`igfx_off`的详细信息，请阅读[Intel-IOMMU.txt](https://www.kernel.org/doc/Documentation/Intel-IOMMU.txt)中的*Graphics Problems?*。

### 启用vfio_pci后X无法启动

这与主机GPU被检测为额外GPU有关，当它尝试加载虚拟机所用的GPU的驱动程序时，会导致X崩溃。为了避免这种情况，需要一个指定主机GPU的BusID的Xorg配置文件。 可以从lspci或Xorg日志获取正确的BusID。[来源 →](https://www.redhat.com/archives/vfio-users/2016-August/msg00025.html)

 `/etc/X11/xorg.conf.d/10-intel.conf` 
```
Section "Device"
        Identifier "Intel GPU"
        Driver "modesetting"
        BusID  "PCI:0:2:0"
EndSection

```

### Chromium忽略集成图形加速

Chromium和它的朋友们将尝试在系统中检测尽可能多的GPU，并选择哪一个作为首选（通常是独立的的NVIDIA/AMD显卡）。它试图通过查看PCI设备来选择GPU，而不是系统中可用的OpenGL渲染器 - 结果是Chromium可能会忽略可用于渲染的集成GPU并尝试使用绑定到无法在宿主机上使用的虚拟机专用GPU。这导致使用软件渲染（导致更高的CPU负载，也可能导致视频播放不稳定，滚动不平滑）。

这可以通过[告诉Chromium使用哪个GPU](/index.php/Chromium/Tips_and_tricks#Forcing_specific_GPU "Chromium/Tips and tricks")来解决。

### 虚拟机只使用一个核心

对于某些用户，即使启用了IOMMU并且核心计数设置为大于1，VM仍然只使用一个CPU核心和线程。 要解决此问题，请在`virt-manager`中启用“手动设置CPU拓扑”，并将其设置为所需的CPU，内核和线程数量。 请记住，“线程”是指每个CPU的线程数，而不是总数。

### 直通貌似工作但没有输出

确保您为您的虚拟机选择了UEFI固件。此外，请确保已将正确的设备直通给虚拟机。

### virt-manager 遇到权限问题

如果你在virt-manager中遇到权限问题，将以下内容添加到`/etc/libvirt/qemu.conf`:

```
group="kvm"
user="*user*"

```

如果仍然不能工作，确保你的用户已经加入了kvm和libvirt[组](/index.php/User_group "User group")。

### 虚拟机关闭之后宿主机核心无响应

此问题似乎主要影响运行Windows 10 guest虚拟机的用户，并且通常在虚拟机运行很长一段时间后发生：主机的多个CPU核心被锁定（请参阅[[3]](https://bbs.archlinux.org/viewtopic.php?id=206050&p=2)）。要解决此问题，请尝试在直通的GPU上启用消息信号中断。有关如何执行此操作的指南，请参见[[4]](https://forums.guru3d.com/threads/windows-line-based-vs-message-signaled-based-interrupts.378044/)。

### 客户机在宿主机休眠眠情况下运行导致死机

启用VFIO的虚拟机如果在睡眠/唤醒周期中运行时会变得不稳定，并且在尝试关闭它们时会导致主机死机。为了避免这种情况，可以使用以下libvirt hook脚本和systemd单元在虚拟机运行时阻止主机进入休眠状态。hook文件需要可执行权限才能工作。

 `/etc/libvirt/hooks/qemu` 
```
#!/bin/bash

OBJECT="$1"
OPERATION="$2"
SUBOPERATION="$3"
EXTRA_ARG="$4"

case "$OPERATION" in
        "prepare")
                systemctl start libvirt-nosleep@"$OBJECT"
                ;;
        "release")
                systemctl stop libvirt-nosleep@"$OBJECT"
                ;;
esac

```
 `/etc/systemd/system/libvirt-nosleep@.service` 
```
[Unit]
Description=Preventing sleep while libvirt domain "%i" is running

[Service]
Type=simple
ExecStart=/usr/bin/systemd-inhibit --what=sleep --why="Libvirt domain \"%i\" is running" --who=%U --mode=block sleep infinity

```

### AMD显卡直通后无法重启虚拟机

某些AMD显卡在Windows虚拟机中可能无法正常Reset，导致虚拟机无法重新启动。

您可以通过在关闭虚拟机之前手动安全移除显卡（就像移除U盘那样）来避免这个问题。当您安装VirtIO驱动程序映像中的`guest-agent`之后，您就可以在安全移除菜单中看到相关的设备。

如果您希望自动完成这项任务，请参阅[[5]](https://forum.level1techs.com/t/linux-host-windows-guest-gpu-passthrough-reinitialization-fix/121097)。

## 另请参阅

*   [Discussion on Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=162768) | [Archived link](https://archive.is/kZYMt)
*   [User contributed hardware compatibility list](https://docs.google.com/spreadsheet/ccc?key=0Aryg5nO-kBebdFozaW9tUWdVd2VHM0lvck95TUlpMlE)
*   [Example script from https://www.youtube.com/watch?v=37D2bRsthfI](https://pastebin.com/rcnUZCv7)
*   [Complete tutorial for PCI passthrough](https://vfio.blogspot.com/)
*   [VFIO users mailing list](https://www.redhat.com/archives/vfio-users/)
*   [#vfio-users on freenode](https://webchat.freenode.net/?channels=vfio-users)
*   [YouTube: Level1Linux - GPU Passthrough for Virtualization with Ryzen](https://www.youtube.com/watch?v=aLeWg11ZBn0)