**翻译状态：** 本文是英文页面 [Microcode](/index.php/Microcode "Microcode") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-06-21，点击[这里](https://wiki.archlinux.org/index.php?title=Microcode&diff=0&oldid=438585)可以查看翻译后英文页面的改动。

处理器制造商发布对处理器[微码](https://en.wikipedia.org/wiki/Microcode "wikipedia:Microcode")的稳定性和安全性更新。虽然微码可以通过BIOS进行更新，但Linux内核也可以在引导期间应用这些更新。这些更新提供了对系统稳定性至关重要的错误修复。如果没有这些更新，您可能会遇到虚假崩溃或难以跟踪的意外系统暂停。

属于Intel Haswell和Broadwell处理器系列的CP US用户必须安装这些微代码更新，以确保系统稳定性。当然，所有用户都应该安装这些更新。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 启用早期微码更新](#启用早期微码更新)
    *   [2.1 Grub](#Grub)
        *   [2.1.1 自动模式](#自动模式)
        *   [2.1.2 手动模式](#手动模式)
    *   [2.2 systemd-boot](#systemd-boot)
    *   [2.3 EFI boot stub / EFI handover](#EFI_boot_stub_/_EFI_handover)
    *   [2.4 rEFInd](#rEFInd)
    *   [2.5 Syslinux](#Syslinux)
    *   [2.6 LILO](#LILO)
*   [3 验证微指令已在启动时更新](#验证微指令已在启动时更新)
*   [4 哪些 CPU 可以接受微指令更新](#哪些_CPU_可以接受微指令更新)
    *   [4.1 检查可用微指令更新](#检查可用微指令更新)
*   [5 在自定义内核中启用微代码加载](#在自定义内核中启用微代码加载)
*   [6 参阅](#参阅)

## 安装

对于 AMD 处理器，安装 [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode)。

对于 Intel 处理器，安装 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode)。

如果你在一个移动介质上安装Arch Linux（[Installing Arch Linux on a USB key (简体中文)](/index.php/Installing_Arch_Linux_on_a_USB_key_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Installing Arch Linux on a USB key (简体中文)")），需要应该安装以上两个厂商处理器的微码软件包。

## 启用早期微码更新

微码必须被[boot loader](/index.php/Boot_loader "Boot loader")加载，由于用户的早期引导配置具有很大的可变性，因此Arch的默认配置可能不会自动触发微码更新。在这方面，许多aur内核都遵循了Arch官方的[kernels](/index.php/Kernels "Kernels")路径。

These updates must be enabled by adding `/boot/amd-ucode.img` or `/boot/intel-ucode.img` as the **first initrd in the bootloader config file**. This is in addition to the normal initrd file. See below for instructions for common bootloaders.

**Note:** In the following sections replace `*cpu_manufacturer*` with your CPU manufacturer, i.e. `amd` or `intel`.

**Tip:** For [Arch Linux on a removable drive](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key") add both microcode files as `initrd` to the boot loader configuration. Their order does not matter as long as they both are specified before the real initramfs image.

### Grub

#### 自动模式

*grub-mkconfig* 会自动发现微码更新并更新 [GRUB](/index.php/GRUB "GRUB") 配置信息。安装微码软件包后，重新生成GRUB 配置以激活更新：

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

#### 手动模式

或者，手动管理GRUB配置文件，用户可以添加`/boot/*cpu_manufacturer*-ucode.img` (或者 `/*cpu_manufacturer*-ucode.img` ，当 `/boot` 是一个独立分区的情况) 如下:

 `/boot/grub/grub.cfg` 
```
...
echo 'Loading initial ramdisk'
initrd	**/boot/*cpu_manufacturer*-ucode.img** /boot/initramfs-linux.img
...

```

为每个入口菜单执行以上操作。

### systemd-boot

在 `/boot/loader/entries/*entry*.conf` 中使用 `initrd` 两次：

```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options ...

```

如果 ESP 没有挂载到 `/boot`, 请将 `/boot/intel-ucode.img` 复制到 [EFI system partition](/index.php/EFI_system_partition "EFI system partition").

### EFI boot stub / EFI handover

添加两个 `initrd=` 选项:

 `initrd=/intel-ucode.img initrd=/initramfs-linux.img` 

对于要创建包含全部initrd和命令行的内核，首先集成两个镜像：

```
cat /boot/intel-ucode.img /boot/initramfs-linux.img > my_new_initrd
objcopy ... --add-section .initrd=my_new_initrd
```

### rEFInd

如上述每个 EFI boot stub 一样编辑 `/boot/refind_linux.conf` 中的引导选项，例如：

```
"Boot with standard options" "ro root=UUID=(...) quiet initrd=/intel-ucode.img initrd=/initramfs-linux.img"

```

如果你在 `/boot/refind.conf` 中使用 [手动配置](/index.php/REFInd#Manual_boot_stanzas "REFInd") 定义所要引导的内核，那么简单地依需求添加 initrd=/intel-ucode.img 或 /boot/intel-ucode.img 到选项行，并不需要修改节的主干部分。

### Syslinux

**Note:** 在 `intel-ucode` 和 `initramfs-linux` initrd 文件间不要用空格，下面的点不是省略号，`INITRD` 行必须和下面示例中一样。

在配置文件`/boot/syslinux/syslinux.cfg`中，多个 initrd 可以通过逗号来分隔。

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD ../intel-ucode.img,../initramfs-linux.img
    APPEND ...
```

### LILO

LILO和其他的老版本启动引导器可能不支持多个initrd镜像，所以`intel-ucode` 和 `initramfs-linux` 需要被合并成一个镜像。

**警告:** 每次更新内核后都要重新合并！

**注意:** 多出的镜像，`intel-ucode`，不能被压缩，否则内核会提示有多余的无用数据并不能启动。

`intel-ucode.img` 应是一个cpio存档。建议每次微码更新后检查存档是否被压缩，因为不能保证以后它会不会被压缩。检查是否被压缩：

```
$ file /boot/intel-ucode.img 
/boot/intel-ucode.img: ASCII cpio archive (SVR4 with no CRC)

```

**注意:** 顺序很重要。原来的 `initramfs-linux` 必须在 `intel-ucode`**之后**。

合并两个镜像并生成 `initramfs-merged.img`：

```
# cat /boot/intel-ucode.img /boot/initramfs-linux.img > /boot/initramfs-merged.img

```

现在编辑 `/etc/lilo.conf` 装载新的镜像：

```
...
initrd=/boot/initramfs-merged.img
...

```

以root运行`lilo`：

```
# lilo

```

## 验证微指令已在启动时更新

使用 `/usr/bin/dmesg` 可以查看微代码有没有更新：

```
$ dmesg | grep microcode

```

在 Intel 系统上，你应当会看到和下面类似的一些东西，表明微指令已在早先更新：

```
[    0.000000] CPU0 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.221951] CPU1 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.242064] CPU2 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.262349] CPU3 microcode updated early to revision 0x1b, date = 2014-05-29
[    0.507267] microcode: CPU0 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507272] microcode: CPU1 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507276] microcode: CPU2 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507281] microcode: CPU3 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507286] microcode: CPU4 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507292] microcode: CPU5 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507296] microcode: CPU6 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507300] microcode: CPU7 sig=0x306a9, pf=0x2, revision=0x1b
[    0.507335] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

```

如果硬件比较新，也可能没有任何微代码更新，结果应该是下面这样：

```
[    0.292893] microcode: CPU0 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292899] microcode: CPU1 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292906] microcode: CPU2 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292912] microcode: CPU3 sig=0x306c3, pf=0x2, revision=0x1c
[    0.292956] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba

```

在 AMD 系统上，微指令会在启动的更晚阶段被更新，所以输出会看起来像这样：

```
[    0.807879] microcode: CPU0: patch_level=0x01000098
[    0.807888] microcode: CPU1: patch_level=0x01000098
[    0.807983] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
[   16.150642] microcode: CPU0: new patch_level=0x010000c7
[   16.150682] microcode: CPU1: new patch_level=0x010000c7

```

**注意:** 微代码的日期和 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) 软件包版本不一定一样，而是代表英特尔最后一次更新微代码的时间。

## 哪些 CPU 可以接受微指令更新

可以从 Intel 和 AMD 的网站查看支持的型号：

*   [AMD 操作系统研发中心](http://www.amd64.org/microcode.html).
*   [Intel 下载中心](https://downloadcenter.intel.com/Detail_Desc.aspx?DwnldID=24290&lang=eng).

### 检查可用微指令更新

可以通过 [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool) 来检查 intel-ucode.img 是否包含适用于你 CPU 的微指令映像。

1.  安装 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) （检测并不需要修改 initrd）
2.  从 AUR 安装 [iucode-tool](https://www.archlinux.org/packages/?name=iucode-tool)
3.  `# modprobe cpuid` 
4.  解包微指令映像，并根据你的 cpuid 搜索是否适用：
     `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS - ` 
5.  如果有更新可用，它应该会在 *selected microcodes* 之下显示
6.  微码可能已经在你的BIOS里，所以不会在dmesg里出现。和正在运行的微码对比：`grep microcode /proc/cpuinfo`

## 在自定义内核中启用微代码加载

启用 “CPU microcode loading support” 才能在启动早期加载微代码，必须编译到内核中，而不是编译为模块。然后将 “Early load microcode” 设置为 “Y”。

```
CONFIG_MICROCODE=y
CONFIG_MICROCODE_INTEL=y
CONFIG_MICROCODE_INTEL_EARLY=y
CONFIG_MICROCODE_EARLY=y

```

## 参阅

*   [Updating microcodes](https://flossexperiences.wordpress.com/2013/11/17/updating-microcodes/)
*   [Notes on Intel Microcode updates](http://inertiawar.com/microcode/)
*   [Kernel early microcode](https://www.kernel.org/doc/Documentation/x86/early-microcode.txt)
*   [Erratum found in Haswell/Broadwell](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly)
*   [Technical details](https://gitlab.com/iucode-tool/iucode-tool)