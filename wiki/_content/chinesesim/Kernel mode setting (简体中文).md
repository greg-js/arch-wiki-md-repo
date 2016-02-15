**翻译状态：** 本文是英文页面 [Kernel_Mode_Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2012-09-08，点击[这里](https://wiki.archlinux.org/index.php?title=Kernel_Mode_Setting&diff=0&oldid=221955)可以查看翻译后英文页面的改动。

内核级[显示模式设置](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting") (KMS) ，作用是可以在内核级别而不是最终用户级别切换显示分辨率和颜色深度。

KMS 支持在 framebuffer 中使用原生分辨率和即时终端(tty)切换。KMS 使用了更新的技术(例如 DRI2)，可以减少失真、增强3D性能，甚至使用内核空间节能功能。

## Contents

*   [1 背景](#.E8.83.8C.E6.99.AF)
*   [2 安装](#.E5.AE.89.E8.A3.85)
    *   [2.1 KMS 晚启动](#KMS_.E6.99.9A.E5.90.AF.E5.8A.A8)
    *   [2.2 KMS 早启动](#KMS_.E6.97.A9.E5.90.AF.E5.8A.A8)
*   [3 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
    *   [3.1 字体太小](#.E5.AD.97.E4.BD.93.E5.A4.AA.E5.B0.8F)
    *   [3.2 启动错误信息](#.E5.90.AF.E5.8A.A8.E9.94.99.E8.AF.AF.E4.BF.A1.E6.81.AF)
*   [4 强设模式](#.E5.BC.BA.E8.AE.BE.E6.A8.A1.E5.BC.8F)
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

[Intel](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)"), [Nouveau](/index.php/Nouveau "Nouveau") 和 [ATI](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)") 驱动已经为所有芯片组提供了 KMS 支持。这些驱动也会自动启用 KMS。

闭源的 [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") 和 [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") 驱动并不使用开放的驱动堆栈，要使用 KMS 请使用开源驱动。

### KMS 早启动

要在启动时尽早启用 KMS，将启动模块加入`/etc/mkinitcpio.conf`的 MODULES 行。

*   Radeon 卡加入：[radeon](/index.php/Radeon "Radeon")
*   Intel 卡加入：[i915](/index.php/Intel "Intel")
*   Nvidia 卡加入：[nouveau](/index.php/Nouveau "Nouveau")

 `/etc/mkinitcpio.conf` 

```
MODULES="i915"
**或**
MODULES="radeon"
**或**
MODULES="nouveau"
```

重新生成内核镜像(详情参阅 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")):

 `# mkinitcpio -p [name of your kernel preset]` 

## 问题解决

### 字体太小

[更换默认字体](/index.php/Fonts#Changing_the_default_font "Fonts")介绍了如何在终端中使用大字体。[extra] 中的 Terminus 字体提供了很多字号，包括大字体。

### 启动错误信息

如果启动时看到 0x00000010 (2) 错误码，(应该有 10 行文字，最后一行是错误码)，请在 `/etc/modprobe.d/modprobe.conf` 中加入:

```
options drm_kms_helper poll=0

```

## 强设模式

来自 [nouveau wiki](http://nouveau.freedesktop.org/wiki/KernelModeSetting):

用内核命令行可以强制设置使用的模式。但是 DRM 内核选项的文档很少，使用的方法位于：

*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt)
*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c)

格式:

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

*   <conn>: Connector, e.g. DVI-I-1, see your kernel log.
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

## 禁用 KMS

有时需要禁用 KMS，例如使用 catalyst 驱动时. 只需在内核参数中加入 **nomodeset** 即可，设置方法请阅读[内核参数](/index.php/Kernel_parameters "Kernel parameters")页面。

使用 `nomodeset` 内核参数的同时，Intel 卡需要添加 `i915.modeset=0`， Nvidia 卡需要添加 `nouveau.modeset=0`. Nvidia Optimus 双显卡系统，需要添加三个内核参数：

```
"nomodeset i915.modeset=0 nouveau.modeset=0"

```

**Note:** 有些[Xorg](/index.php/Xorg "Xorg") 驱动必须启用 KMS 才能工作，参阅所用驱动的页面。