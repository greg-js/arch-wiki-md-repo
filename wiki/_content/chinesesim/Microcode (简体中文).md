**翻译状态：** 本文是英文页面 [Microcode](/index.php/Microcode "Microcode") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2014-12-06，点击[这里](https://wiki.archlinux.org/index.php?title=Microcode&diff=0&oldid=348268)可以查看翻译后英文页面的改动。

[处理器微指令](https://en.wikipedia.org/wiki/Microcode "wikipedia:Microcode") 和处理器固件是同一概念。内核有能力不通过 BIOS 来更新处理器固件。

	*微指令数据文件包含所有 Intel 处理器的最新微指令定义。Intel 发布微指令更新来修正处理器行为，修正内容登在处理器相关更新文档中。常规的更新方法时通过 BIOS 升级，而 Intel 意识到这会是一个管理争端（administrative hassle）。Linux 操作系统和 VMware ESX 产品拥有一个机制，可以在引导完毕后更新微指令。比如，将这个文件放在 Linux 系统的 /etc/firmware 目录下之后，这个文件就会被该操作系统机制使用。* ——[Intel](https://downloadcenter.intel.com/Detail_Desc.aspx?DwnldID=23082)

## Contents

*   [1 更新微指令](#.E6.9B.B4.E6.96.B0.E5.BE.AE.E6.8C.87.E4.BB.A4)
    *   [1.1 启用 Intel 微指令更新](#.E5.90.AF.E7.94.A8_Intel_.E5.BE.AE.E6.8C.87.E4.BB.A4.E6.9B.B4.E6.96.B0)
        *   [1.1.1 EFI boot stub / EFI handover](#EFI_boot_stub_.2F_EFI_handover)
        *   [1.1.2 Gummiboot](#Gummiboot)
        *   [1.1.3 rEFInd](#rEFInd)
        *   [1.1.4 Grub](#Grub)
        *   [1.1.5 Syslinux](#Syslinux)
    *   [1.2 启用 AMD 微指令更新](#.E5.90.AF.E7.94.A8_AMD_.E5.BE.AE.E6.8C.87.E4.BB.A4.E6.9B.B4.E6.96.B0)
*   [2 验证微指令已在启动时更新](#.E9.AA.8C.E8.AF.81.E5.BE.AE.E6.8C.87.E4.BB.A4.E5.B7.B2.E5.9C.A8.E5.90.AF.E5.8A.A8.E6.97.B6.E6.9B.B4.E6.96.B0)
*   [3 哪些 CPU 可以接受微指令更新](#.E5.93.AA.E4.BA.9B_CPU_.E5.8F.AF.E4.BB.A5.E6.8E.A5.E5.8F.97.E5.BE.AE.E6.8C.87.E4.BB.A4.E6.9B.B4.E6.96.B0)
    *   [3.1 检查可用微指令更新](#.E6.A3.80.E6.9F.A5.E5.8F.AF.E7.94.A8.E5.BE.AE.E6.8C.87.E4.BB.A4.E6.9B.B4.E6.96.B0)

## 更新微指令

对于 Intel 处理器，安装 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode)。

对于 AMD 处理器，微指令更新放置在 [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) ，而它作为基本系统的一部分安装。

### 启用 Intel 微指令更新

**警告:** 在 linux 3.17-2 和 linux-lts 3.14.21-2 以及更新版本中，Intel 微指令更新不再被自动触发。需要在启动加载器的 initrd 设置中添加 `/boot/intel-ucode.img` 才能启用更新。

#### EFI boot stub / EFI handover

只需要附加两个 `initrd=` 选项即可：

 `initrd=/intel-ucode.img initrd=/initramfs-linux.img` 

#### Gummiboot

在 `/boot/loader/entries/*.conf` 中使用 `initrd` 两次：

```
title   Arch Linux
linux   /vmlinuz-linux
initrd  /intel-ucode.img
initrd  /initramfs-linux.img
options ...
```

#### rEFInd

如上述每个 EFI boot stub 一样编辑 `/boot/refind_linux.conf` 中的引导选项，例如：

 `"Boot with standard options" "ro root=UUID=(...) quiet initrd=/intel-ucode.img initrd=/initramfs-linux.img"` 

如果你在 `/boot/refind.conf` 中使用手动的节（manual stanzas）来定义所要引导的内核，那么简单地依需求添加 initrd=/intel-ucode.img 或 /boot/intel-ucode.img 到选项行，并不需要修改节的主干部分。

#### Grub

grub-1:2.02-beta2-5发布之后， `/usr/bin/grub-mkconfig` 可以自动处理微指令更新.用戶在安装完[intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode)后，运行`grub-mkconfigke`就可以重新生成grub配置文件启用微指令更新。

用户也可以在 `grub.cfg` 中添加`/intel-ucode.img` 或 `/boot/intel-ucode.img` (记住 `/intel-ucode.img` 文件的路径和你的引导分区有关，就像 initramfs 一样。

```
	[...]
	echo	'Loading initial ramdisk ...'
	initrd	/intel-ucode.img /initramfs-linux.img
	[...]
```

**注意:** 相关的菜单项都要修改

**警告:** 这个文件会被 `grub-mkconfig` 自动覆盖，并且这些更新会消除你的修改。

#### Syslinux

在配置文件`/boot/syslinux/syslinux.cfg`中，多个 initrd 可以通过逗号来分隔。

```
LABEL arch
    MENU LABEL Arch Linux
    LINUX ../vmlinuz-linux
    INITRD ../intel-ucode.img,../initramfs-linux.img
    APPEND ...
```

### 启用 AMD 微指令更新

在 AMD 系统上，微指令会在启动时自动更新，所以不必做更多动作。

## 验证微指令已在启动时更新

你可以通过 `dmesg | grep microcode` 命令来检查微指令是否已经在启动时成功更新。

在 Intel 系统上，你应当会看到和下面类似的一些东西，表明微指令已在早先更新：

```
[    0.000000] CPU0 microcode updated early to revision 0x218, date = 2009-04-10
[    0.588776] microcode: CPU0 sig=0x106c2, pf=0x4, revision=0x218
[    0.588799] microcode: CPU1 sig=0x106c2, pf=0x4, revision=0x218
[    0.588977] microcode: Microcode Update Driver: v2.00 <tigran@aivazian.fsnet.co.uk>, Peter Oruba
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

#### 检查可用微指令更新

可以通过 [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/) 来检查 intel-ucode.img 是否包含适用于你 CPU 的微指令映像。

*   安装 [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) （检测并不需要修改 initrd）
*   从 AUR 安装 [iucode-tool](https://aur.archlinux.org/packages/iucode-tool/)
*   `# modprobe cpuid`
*   `# bsdtar -Oxf /boot/intel-ucode.img | iucode_tool -tb -lS -`
    （解开微指令映像，并根据你的 cpuid 搜索是否适用）
*   如果有更新可用，它应该会在 *selected microcodes* 之下显示