**翻译状态：** 本文是英文页面 [Kernel_Mode_Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-16，点击[这里](https://wiki.archlinux.org/index.php?title=Kernel_Mode_Setting&diff=0&oldid=441731)可以查看翻译后英文页面的改动。

内核级[显示模式设置](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting") (KMS) ，作用是可以在内核级别而不是最终用户级别切换显示分辨率和颜色深度。

Linux 内核的 KMS 实现支持在 framebuffer 中使用原生分辨率和即时终端(tty)切换。KMS 使用了更新的技术(例如 DRI2)，可以减少失真、增强3D性能，甚至使用内核空间节能功能。

**注意:** [NVIDIA](/index.php/NVIDIA "NVIDIA") 闭源驱动从 364.12 开始也实现了 KMS，但是没有利用 linux 内核的实现，缺少高分辨率终端的 fbdev 驱动。

## Contents

*   [1 背景](#.E8.83.8C.E6.99.AF)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 KMS 晚启动](#KMS_.E6.99.9A.E5.90.AF.E5.8A.A8)
    *   [2.2 KMS 早启动](#KMS_.E6.97.A9.E5.90.AF.E5.8A.A8)
*   [3 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [3.1 字体太小](#.E5.AD.97.E4.BD.93.E5.A4.AA.E5.B0.8F)
    *   [3.2 启动错误信息](#.E5.90.AF.E5.8A.A8.E9.94.99.E8.AF.AF.E4.BF.A1.E6.81.AF)
*   [4 强设模式和 EDID](#.E5.BC.BA.E8.AE.BE.E6.A8.A1.E5.BC.8F.E5.92.8C_EDID)
*   [5 禁用 KMS](#.E7.A6.81.E7.94.A8_KMS)

## 背景

以前，设定显卡是在 X服务器上工作。所以虚拟终端不可能提供漂亮的图像效果。同时，每次使用`Ctrl+Alt+F1~7`从X切换到虚拟终端时，x服务器必须将显卡的控制权交给内核，这个流程显得低效并且会导致闪烁。将控制权切回到X服务器同样是一个“痛苦”的过程。

使用内核模式设置后，内核可以设定显卡的模式。这样开机启动即可看到漂亮的显示画面，在 X 图形界面 和 终端 之间也可以快速切换，还有其他的一些优点。

## 安装

不管使用什么方法，都需要先“禁用”下列项：

*   所有启动加载器中的 "vga=" 选项，这个选项与 KMS 的原生分辨率设置冲突。
*   所有 "video=" 选项，这个选项会启动帧缓冲，导致驱动冲突。
*   所有帧缓冲驱动(例如 [uvesafb](/index.php/Uvesafb "Uvesafb")).

### KMS 晚启动

[Intel](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)"), [Nouveau](/index.php/Nouveau "Nouveau"), [ATI](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)") 和 [AMDGPU](/index.php/AMDGPU "AMDGPU") 驱动已经为所有芯片组提供了 KMS 支持。这些驱动也会自动启用 KMS。

闭源的 [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") 驱动从 364.12 开始支持 KMS，但是需要 [手动启用](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA")。

闭源的 [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") 启动不支持 KMS. 要使用 KMS，需要替换为开源的 [ATI](/index.php/ATI "ATI") 驱动。

### KMS 早启动

**提示:** 如果你有分辨率方面的问题，可以参考一下 [enforcing the mode](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") ，也许会有帮助。

KMS通常是在[initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process")之后开始初始化，但是你也可以在initramfs的阶段启用KMS:

将启动模块加入`/etc/mkinitcpio.conf`的 MODULES 行。

*   Radeon 卡加入：[radeon](/index.php/Radeon "Radeon")
*   Intel 卡加入：[i915](/index.php/Intel "Intel")
*   Nvidia 卡加入：[nouveau](/index.php/Nouveau "Nouveau")

例如对 Intel 显卡,将 `i915` 模块加入到 `/etc/mkinitcpio.conf` 的 `MODULES`行：

```
MODULES="**i915**"

```

**注意:** 有些用户也许需要在 `i915` 之前添加`intel_agp` 用来阻止 ACPI 错误。顺序很重要，因为模块是按顺序加载的.

如果您使用的是自定义的 [EDID](https://en.wikipedia.org/wiki/Extended_display_identification_data "wikipedia:Extended display identification data") 文件,你应该也把它添加到initramfs中：

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

最后，重新生成内核镜像(详情参阅 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"))。

## 问题解决

### 字体太小

[Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts")介绍了如何在终端中使用大字体。软件仓库中的 ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font)) 字体提供了很多字号，包括大字体。

### 启动错误信息

Polling for connected display devices on older systems can be quite expensive. Poll will happen periodically and can in worst cases take several hundred milliseconds, depending on the hardware. This will cause visible stalls, for example in video playback. These stalls might happen even when your video is on HDP output but you have other non HDP outputs in your hw configuration. If you experience stalls in display output occurring every 10 seconds, disabling polling might help.

如果启动时看到 0x00000010 (2) 错误码，(应该有 10 行文字，最后一行是错误码)，请使用

 `/etc/modprobe.d/modprobe.conf`  `options drm_kms_helper poll=0` 

## 强设模式和 EDID

In case that your monitor/TV is not sending the appropriate [EDID](https://en.wikipedia.org/wiki/EDID "wikipedia:EDID") or similar problems, you will notice that the native resolution is not automatically configured or no display at all. The kernel has a provision to load the binary EDID data, and provides as well data to set four of the most typical resolutions.

If you have the EDID file for your monitor the process is easy. If you do not have, you can either use one of the built-in resolution-EDID binaries (or generate one during kernel compilation, [more info here](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/plain/Documentation/EDID/HOWTO.txt)) or build your own EDID.

In case you have an EDID file (e.g. extracted from Windows drivers for your monitor or using `get-edid` command from [read-edid](https://www.archlinux.org/packages/?name=read-edid)), create a dir `edid` under `/usr/lib/firmware`:

```
# mkdir /usr/lib/firmware/edid

```

and then copy your binary into the `/usr/lib/firmware/edid` directory.

To load it at boot, specify the following in the [kernel command line](/index.php/Kernel_command_line "Kernel command line"):

```
 drm_kms_helper.edid_firmware=edid/your_edid.bin

```

You can also specify it only for a specified connection:

```
drm_kms_helper.edid_firmware=VGA-1:edid/your_edid.bin

```

For the four built-in resolutions, see table below for the name to specify:

| **Resolution** | **Name to specify** |
| 1024x768 | edid/1024x768.bin |
| 1280x1024 | edid/1280x1024.bin |
| 1600x1200 (kernel 3.10 or higher) | edid/1600x1200.bin |
| 1680x1050 | edid/1680x1050.bin |
| 1920x1080 | edid/1920x1080.bin |

If you are doing early KMS, you must include the custom EDID file in the [initramfs](#Early_KMS_start) or you will run into problems.

You can also construct your own EDID with the makefile included in the `Documentation/EDID` sources of the kernel. The full information can be read [here](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/EDID/HOWTO.txt) and [there](https://www.osadl.org/Single-View.111+M591850c02b5.0.html).

**Warning:** The method described below is somehow incomplete because e.g. Xorg does not take into account the resolution specified, so users are encouraged to use the method described above; however, specifying resolution with `video=` command line may be useful in some scenarios

来自 [nouveau wiki](http://nouveau.freedesktop.org/wiki/KernelModeSetting):

用内核命令行可以强制设置使用的模式。但是 DRM 内核选项的文档很少，使用的方法位于：

*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt)
*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c)

格式:

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

*   <conn>: Connector, e.g. DVI-I-1, 查看 `/sys/class/drm/` .
*   <xres> x <yres>: resolution
*   M: compute a CVT mode?
*   R: reduced blanking?
*   -<bpp>: color depth
*   @<refresh>: refresh rate
*   i: interlaced (non-CVT mode)
*   m: margins?
*   e: output forced to on
*   d: output forced to off
*   D: digital output forced to on (e.g. DVI-I connector)

可以使用多个 "video" 设置不同输出的分辨率，例如要强制 DVI 使用 1024x768 85 Hz ，同时禁用 TV-out :

```
video=DVI-I-1:1024x768@85 video=TV-1:d

```

要获取当前连接器的状态，使用下面命令：

 `$ for p in /sys/class/drm/*/status; do con=${p%/status}; echo -n "${con#*/card?-}: "; cat $p; done` 
```

DVI-I-1: connected
HDMI-A-1: disconnected
VGA-1: disconnected

```

## 禁用 KMS

有时需要禁用 KMS，例如使用 catalyst 驱动时. 只需在内核参数中加入 **nomodeset** 即可，设置方法请阅读[内核参数](/index.php/Kernel_parameters "Kernel parameters")页面。

使用 `nomodeset` 内核参数的同时，Intel 卡需要添加 `i915.modeset=0`， Nvidia 卡需要添加 `nouveau.modeset=0`. Nvidia Optimus 双显卡系统，需要添加三个内核参数：

```
"nomodeset i915.modeset=0 nouveau.modeset=0"

```

**Note:** 有些[Xorg](/index.php/Xorg "Xorg") 驱动必须启用 KMS 才能工作，参阅所用驱动的页面。