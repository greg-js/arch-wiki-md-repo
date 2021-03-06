相关文章

*   [ATI](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)")
*   [Intel](/index.php/Intel_Graphics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel Graphics (简体中文)")
*   [Nouveau](/index.php/Nouveau_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Nouveau (简体中文)")

**翻译状态：** 本文是英文页面 [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-10-29，点击[这里](https://wiki.archlinux.org/index.php?title=Kernel+mode+setting&diff=0&oldid=586589)可以查看翻译后英文页面的改动。

内核级[显示模式设置](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting") (KMS) ，作用是可以在内核级别而不是最终用户级别切换显示分辨率和颜色深度。

Linux 内核的 KMS 实现支持在 framebuffer 中使用原生分辨率和即时终端(tty)切换。KMS 使用了更新的技术(例如 DRI2)，可以减少失真、增强3D性能，甚至使用内核空间节能功能。

**注意:** [NVIDIA](/index.php/NVIDIA "NVIDIA") 闭源驱动从 364.12 开始也实现了 KMS，但是没有利用 linux 内核的实现，缺少高分辨率终端的 fbdev 驱动。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 背景](#背景)
*   [2 安装](#安装)
    *   [2.1 KMS 晚启动](#KMS_晚启动)
    *   [2.2 KMS 早启动](#KMS_早启动)
*   [3 问题解决](#问题解决)
    *   [3.1 字体太小](#字体太小)
    *   [3.2 启动错误信息](#启动错误信息)
*   [4 Forcing modes and EDID](#Forcing_modes_and_EDID)
    *   [4.1 Forcing modes](#Forcing_modes)
    *   [4.2 Forcing modes](#Forcing_modes_2)
*   [5 禁用 KMS](#禁用_KMS)

## 背景

以前，设定显卡是 X 服务器的工作。所以虚拟终端不可能提供漂亮的图像效果。同时，每次使用`Ctrl+Alt+F1~7`从X切换到虚拟终端时，x服务器必须将显卡的控制权交给内核，这个流程显得低效并且会导致闪烁。将控制权切回到X服务器同样是一个“痛苦”的过程。

使用内核模式设置后，内核可以设定显卡的模式。这样开机启动即可看到漂亮的显示画面，在 X 图形界面 和 终端 之间也可以快速切换，还有其他的一些优点。

## 安装

不管使用什么方法，都需要先“禁用”下列项：

*   所有启动加载器中的 "vga=" 选项，这个选项与 KMS 的原生分辨率设置冲突。
*   所有 "video=" 选项，这个选项会启动帧缓冲，导致驱动冲突。
*   所有帧缓冲驱动(例如 [uvesafb](/index.php/Uvesafb "Uvesafb")).

### KMS 晚启动

[Intel](/index.php/Intel_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Intel (简体中文)"), [Nouveau](/index.php/Nouveau "Nouveau"), [ATI](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)") 和 [AMDGPU](/index.php/AMDGPU "AMDGPU") 驱动已经为所有芯片组提供了 KMS 支持。这些驱动也会自动启用 KMS。

闭源的 [NVIDIA](/index.php/NVIDIA_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "NVIDIA (简体中文)") 驱动从 364.12 开始支持 KMS，但是需要 [手动启用](/index.php/NVIDIA#DRM_kernel_mode_setting "NVIDIA")。

闭源的 [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") 启动不支持 KMS. 要使用 KMS，需要替换为开源的 [AMDGPU](/index.php/AMDGPU "AMDGPU") 或 [ATI](/index.php/ATI "ATI") 驱动。

### KMS 早启动

**提示：** 如果你有分辨率方面的问题，可以参考一下 [强设模式](#强设模式和_EDID) ，也许会有帮助。

KMS通常是在[initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process")之后开始初始化，但是你也可以在initramfs的阶段启用KMS:

将[视频驱动](/index.php/Xorg#Driver_installation "Xorg")模块加入`/etc/mkinitcpio.conf`的 MODULES 行。

*   [AMDGPU](/index.php/AMDGPU "AMDGPU") 驱动加入 `amdgpu`; 老的 [ATI](/index.php/ATI "ATI") 驱动加入 `radeon`
*   Intel 卡加入：[i915](/index.php/Intel "Intel")
*   开源的 [Nouveau](/index.php/Nouveau "Nouveau") 驱动加入：[nouveau](/index.php/Nouveau "Nouveau")
*   [QEMU](/index.php/QEMU "QEMU") 显卡： VirtIO 加入 `virtio-gpu`， QXL 加入 `qxl` for QXL，Cirrus 加入 `cirrus`

例如对 Intel 显卡,将 `i915` 模块加入到 `/etc/mkinitcpio.conf` 的 `MODULES`行：

```
MODULES=(**i915**)

```

**注意:** 有些用户也许需要在 `i915` 之前添加`intel_agp` 用来阻止 ACPI 错误。顺序很重要，因为模块是按顺序加载的.

如果您使用的是自定义的 [EDID](https://en.wikipedia.org/wiki/Extended_display_identification_data "wikipedia:Extended display identification data") 文件,你应该也把它添加到initramfs中：

 `/etc/mkinitcpio.conf`  `FILES=(/lib/firmware/edid/your_edid.bin)` 

最后，重新生成内核镜像(详情参阅 [mkinitcpio (简体中文)](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)"))。

## 问题解决

### 字体太小

[Fonts (简体中文)#终端字体](/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#终端字体 "Fonts (简体中文)")介绍了如何在终端中使用大字体。软件仓库中的 ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font)) 字体提供了很多字号，比如更大一些的 `ter-132n`。 或者，可以[#禁用 KMS](#禁用_KMS) 以切换为更低的分辨率，使得字体外观显得更大一些。

### 启动错误信息

在比较老的系统上轮询已连接的显示设备的开销很大。在不同的硬件上甚至可能每几百毫秒就轮询一次。这会导致在视频播放等场景中可见的显示延迟，即使视频具有HDP输出，若硬件设置为其他非HDP输出仍会出现延迟。如果每10秒延迟一次，则应禁用轮询。

如果启动时看到 0x00000010 (2) 错误码，(应该有 10 行文字，最后一行是错误码)，请使用

 `/etc/modprobe.d/modprobe.conf`  `options drm_kms_helper poll=0` 

## Forcing modes and EDID

If your native resolution is not automatically configured or no display at all is detected, then your monitor might send none or just a skewed [EDID](https://en.wikipedia.org/wiki/EDID "wikipedia:EDID") file. The kernel will try to catch this case and will set one of the most typical resolutions.

In case you have the EDID file for your monitor you merely need to explicitly enforce it (see below). However most often one does not have direct access to a sane file and it is necessary to either extract an existing one and fix it or to generate a new one.

Generating new EDID binaries for various resolutions and configurations is possible during kernel compilation by following the [upstream documentation](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/Documentation/EDID/HOWTO.txt) (also see [here](https://www.osadl.org/Single-View.111+M5315d29dd12.0.html) for a short guide). Other solutions are outlined in details in this [article](https://kodi.wiki/view/Creating_and_using_edid.bin_via_xorg.conf). Extracting an existing one is in most cases easier, e.g. if your monitor works fine under Windows you might have luck extracting the EDID from the corresponding driver, or if a similar monitor works which has the same settings you may use `get-edid` from the [read-edid](https://www.archlinux.org/packages/?name=read-edid) package.

After having prepared your EDID place it in a folder, e.g. called `edid` under `/usr/lib/firmware` and copy your binary into it.

To load it at boot, specify the following in the [kernel command line](/index.php/Kernel_command_line "Kernel command line"):

```
drm_kms_helper.edid_firmware=edid/your_edid.bin

```

or alternatively (since kernel 4.15), one may also enforce the EDID information on a lower level, using:

```
drm.edid_firmware=edid/your_edid.bin

```

In order to apply it only to a specific connector use:

```
drm_kms_helper.edid_firmware=VGA-1:edid/your_edid.bin

```

For the built-in resolutions, refer to the table below. The **Name** column specifies the name which one is supposed to use in order to enforce its usage.

| **Resolution** | **Name** |
| 800x600 | edid/800x600.bin |
| 1024x768 | edid/1024x768.bin |
| 1280x1024 | edid/1280x1024.bin |
| 1600x1200 (kernel 3.10 or higher) | edid/1600x1200.bin |
| 1680x1050 | edid/1680x1050.bin |
| 1920x1080 | edid/1920x1080.bin |

If you are doing [early KMS](#Early_KMS_start), you must include the custom EDID file in the initramfs, otherwise you will run into problems.

### Forcing modes

**Warning:** The method described below is somehow incomplete because e.g. [Xorg](/index.php/Xorg "Xorg") does not take into account the resolution specified, so users are encouraged to use the method described above. However, specifying resolution with `video=` command line may be useful in some scenarios.

From [the nouveau wiki](http://nouveau.freedesktop.org/wiki/KernelModeSetting):

	A mode can be forced on the kernel command line. Unfortunately, the command line option video is poorly documented in the DRM case. Bits and pieces on how to use it can be found in

*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt)
*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c)

The format is:

```
video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

```

*   `<conn>`: Connector, e.g. DVI-I-1, see `/sys/class/drm/` for available connectors
*   `<xres> x <yres>`: resolution
*   `M`: compute a CVT mode?
*   `R`: reduced blanking?
*   `-<bpp>`: color depth
*   `@<refresh>`: refresh rate
*   `i`: interlaced (non-CVT mode)
*   `m`: margins?
*   `e`: output forced to on
*   `d`: output forced to off
*   `D`: digital output forced to on (e.g. DVI-I connector)

You can override the modes of several outputs using `video=` several times, for instance, to force `DVI` to *1024x768* at *85 Hz* and `TV-out` off:

```
video=DVI-I-1:1024x768@85 video=TV-1:d

```

To get the name and current status of connectors, you can use the following shell oneliner:

 `$ for p in /sys/class/drm/*/status; do con=${p%/status}; echo -n "${con#*/card?-}: "; cat $p; done` 
```
DVI-I-1: connected
HDMI-A-1: disconnected
VGA-1: disconnected

```

### Forcing modes

**警告:** 下面描述的方法并不完整，e.g. Xorg does not take into account the resolution specified, so users are encouraged to use the method described above; however, specifying resolution with `video=` command line may be useful in some scenarios

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

**注意:** 有些 [Xorg](/index.php/Xorg "Xorg") 驱动必须启用 KMS 才能工作，参阅所用驱动的页面。