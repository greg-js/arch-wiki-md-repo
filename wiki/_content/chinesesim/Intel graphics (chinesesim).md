[[[Category:Graphics (简体中文)]]

相关文章

*   [Intel GMA3600](/index.php/Intel_GMA3600 "Intel GMA3600")
*   [Xorg](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")
*   [Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting")
*   [Xrandr](/index.php/Xrandr "Xrandr")
*   [Hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics")

**翻译状态：** 本文是英文页面 [Intel_Graphics](/index.php/Intel_Graphics "Intel Graphics") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2016-08-16，点击[这里](https://wiki.archlinux.org/index.php?title=Intel_Graphics&diff=0&oldid=446766)可以查看翻译后英文页面的改动。

由于 Intel 提供和支持 X.Org 开源驱动，Intel 的显卡基本上是即插即用的。

Intel显卡和相应芯片组、cpu的完整型号参考[维基百科上的 Intel 显卡处理单元对比](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units")。

**注意:**

*   有些人建议不要安装Intel驱动，而应该使用通用的 modesetting 驱动。 参见 [[1]](https://packages.debian.org/sid/x11/xserver-xorg-video-intel) 与 [[2]](https://www.reddit.com/r/archlinux/comments/4cojj9/it_is_probably_time_to_ditch_xf86videointel/).
*   开源驱动不支持基于PowerVR的显卡([GMA 3600](/index.php/Intel_GMA_3600 "Intel GMA 3600") 系列)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 加载](#.E5.8A.A0.E8.BD.BD)
    *   [3.1 启用 early KMS](#.E5.90.AF.E7.94.A8_early_KMS)
*   [4 基于模块的省电选项](#.E5.9F.BA.E4.BA.8E.E6.A8.A1.E5.9D.97.E7.9A.84.E7.9C.81.E7.94.B5.E9.80.89.E9.A1.B9)
    *   [4.1 RC6 sleep modes (enable_rc6)](#RC6_sleep_modes_.28enable_rc6.29)
    *   [4.2 帧缓冲压缩 (enable_fbc)](#.E5.B8.A7.E7.BC.93.E5.86.B2.E5.8E.8B.E7.BC.A9_.28enable_fbc.29)
*   [5 技巧](#.E6.8A.80.E5.B7.A7)
    *   [5.1 避免播放视频时屏幕撕裂](#.E9.81.BF.E5.85.8D.E6.92.AD.E6.94.BE.E8.A7.86.E9.A2.91.E6.97.B6.E5.B1.8F.E5.B9.95.E6.92.95.E8.A3.82)
    *   [5.2 禁用垂直同步 (VSYNC)](#.E7.A6.81.E7.94.A8.E5.9E.82.E7.9B.B4.E5.90.8C.E6.AD.A5_.28VSYNC.29)
    *   [5.3 设置自动缩放模式](#.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.8A.A8.E7.BC.A9.E6.94.BE.E6.A8.A1.E5.BC.8F)
    *   [5.4 KMS 问题: 终端面积很小](#KMS_.E9.97.AE.E9.A2.98:_.E7.BB.88.E7.AB.AF.E9.9D.A2.E7.A7.AF.E5.BE.88.E5.B0.8F)
    *   [5.5 在 GMA 4500 硬解 H.264](#.E5.9C.A8_GMA_4500_.E7.A1.AC.E8.A7.A3_H.264)
    *   [5.6 设置伽马和亮度](#.E8.AE.BE.E7.BD.AE.E4.BC.BD.E9.A9.AC.E5.92.8C.E4.BA.AE.E5.BA.A6)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 SNA 问题](#SNA_.E9.97.AE.E9.A2.98)
    *   [6.2 DRI3 问题](#DRI3_.E9.97.AE.E9.A2.98)
    *   [6.3 Font and screen corruption in GTK+ applications (missing glyphs after suspend/resume)](#Font_and_screen_corruption_in_GTK.2B_applications_.28missing_glyphs_after_suspend.2Fresume.29)
    *   [6.4 在启动阶段，当 "Loading modules" 时黑屏](#.E5.9C.A8.E5.90.AF.E5.8A.A8.E9.98.B6.E6.AE.B5.EF.BC.8C.E5.BD.93_.22Loading_modules.22_.E6.97.B6.E9.BB.91.E5.B1.8F)
    *   [6.5 X 冻结/崩溃](#X_.E5.86.BB.E7.BB.93.2F.E5.B4.A9.E6.BA.83)
    *   [6.6 添加未识别分辨率](#.E6.B7.BB.E5.8A.A0.E6.9C.AA.E8.AF.86.E5.88.AB.E5.88.86.E8.BE.A8.E7.8E.87)
    *   [6.7 Weathered colors (color range problem)](#Weathered_colors_.28color_range_problem.29)
    *   [6.8 Backlight is not adjustable](#Backlight_is_not_adjustable)
    *   [6.9 Disabling frame buffer compression](#Disabling_frame_buffer_compression)
    *   [6.10 Corruption/Unresponsiveness in Chromium and Firefox](#Corruption.2FUnresponsiveness_in_Chromium_and_Firefox)
    *   [6.11 Kernel crashing w/kernels 4.0+ on Broadwell/Core-M chips](#Kernel_crashing_w.2Fkernels_4.0.2B_on_Broadwell.2FCore-M_chips)
    *   [6.12 Skylake support](#Skylake_support)
    *   [6.13 Lag in Windows guests](#Lag_in_Windows_guests)
*   [7 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 软件包。它提供了用于2D加速的DDX驱动。并且它依赖于3D加速的DRI驱动 [mesa](https://www.archlinux.org/packages/?name=mesa)。

要启用OpenGL支持, 需要安装 [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl)。如果你使用的是64位系统并且需要 32 位程序中使用加速功能，还需要安装[multilib](/index.php/Multilib "Multilib") 仓库中的 [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl)。

参考 [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

Ivy-Bridge以及更新的GPU支持 [Vulkan](/index.php/Vulkan "Vulkan") ，要启用这项功能，请安装 [vulkan-intel](https://www.archlinux.org/packages/?name=vulkan-intel) 。

## 配置

要运行 [Xorg](/index.php/Xorg "Xorg")，没有必要做任何形式的配置（不需要`xorg.conf`，但若有则需要正确配置）。

**注意:** 一些最新型号的核心显卡（例如Skylake/HD 530）可能需要额外的设置，参见[#Skylake 支持](#Skylake_.E6.94.AF.E6.8C.81)

然而，为了设定驱动的选项，你可能需要创建一份形式如下的Xorg的配置文件。

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
EndSection
```

其他的一些选项由用户自行添加在`Driver`下方（每个选项一行）。

**注意:**

*   在创建配置文件时，你可能需要指定`Option "AccelMethod"`（加速方式），哪怕只是将他设定为默认的方式 （现在的默认加速方式为 `"sna"`）；否则 X 可能会崩溃。
*   你可能会需要在配置文件中添加更多的`Section "Device"`（驱动部分）。在相应的文章中会提示你在何处添加。

查看完整选项列表，在终端中输入[intel(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/intel.4)。

## 加载

英特尔内核模块在系统启动时自动加载. 如果它不启动，请检查:

*   首先，确认你 **没有** 在 [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") 中添加 `nomodeset` 或 `vga=`选项， 因为Intel显示驱动需要 [KMS](/index.php/KMS "KMS").
*   其次，检查你没有把Intel列入 `/etc/modprobe.d/` 或 `/usr/lib/modprobe.d/` 中的modprobe的黑名单文件中。

### 启用 early KMS

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS)被使用的i915 DRM驱动程序英特尔芯片组所支持，并且默认情况下被强制启用。

要在启动过程的早期启动 KMS，请参考 [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting")。

## 基于模块的省电选项

可以通过[内核模块选项](/index.php/Kernel_modules#Setting_module_options "Kernel modules") 配置 `i915` 内核模块，其中一些选项会对影响省电功能。

通过下面命令可以获得所有支持选项及其简介和默认值

```
$ modinfo -p i915

```

要检查目前启用了那些选项：

```
# systool -m i915 -av

```

You will note that the `i915.powersave` option which "enable[s] powersavings, fbc, downclocking, etc." is enabled by default, resulting in per-chip powersaving defaults. It is however possible to configure more aggressive powersaving by using [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules").

**Warning:** Diverting from the defaults will mark the kernel as [tainted](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=fc9740cebc3ab7c65f3c5f6ce0caf3e4969013ca) from Linux 3.18 onwards. This basically implies using other options than the per-chip defaults is considered experimental and not supported by the developers.

The following set of options should be generally safe to enable:

 `/etc/modprobe.d/i915.conf` 
```
options i915 enable_rc6=1 enable_fbc=1 lvds_downclock=1 semaphores=1

```

### RC6 sleep modes (enable_rc6)

You can experiment with higher values for `enable_rc6`, but your GPU may not support them or the activation of the other options [[3]](https://wiki.archlinux.org/index.php?title=Talk:Intel_Graphics&oldid=327547#Kernel_Module_options).

The available `enable_rc6` values are a bitmask with bit values RC6=1, RC6p=2, RC6pp=3[[4]](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/drivers/gpu/drm/i915/intel_pm.c#n34) - where "RC6p" and "RC6pp" are lower power states.

To confirm the current running RC6 level, you can look in sysfs:

```
# cat /sys/class/drm/card0/power/rc6_enable

```

... if the value read is a lower number than expected, the other RC6 level are probably not supported. Passing `drm.debug=0xe` will add DRM debugging information to the kernel log - possibly including a line like this:

```
[drm:sanitize_rc6_option] Adjusting RC6 mask to 1 (requested 7, valid 1)

```

### 帧缓冲压缩 (enable_fbc)

在 Sandy Bridge之前世代的 Intel GPU （第六代）上使用帧缓冲压缩可能会导致 GPU 的不稳定，甚至不可用。这时系统日志里可能会出现类似于下面的消息：

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## 技巧

### 避免播放视频时屏幕撕裂

若使用 SNA，将下列内容添加到 `/etc/X11/xorg.conf.d/20-intel.conf` 的 `Device` 部分可杜绝屏幕撕裂问题。

```
Option "TearFree" "true"

```

参见 [original bug report](https://bugs.freedesktop.org/show_bug.cgi?id=37686) 以获取更多信息.

**注意:**

*   如果 `SwapbuffersWait` 被设定为 `false`，这个选项可能不会生效。
*   这个选项对一些非常挑剔垂直同步时间的程序会产生很多问题，例如 [Super Meat Boy](https://en.wikipedia.org/wiki/Super_Meat_Boy "wikipedia:Super Meat Boy")。
*   这个选项对 UXA 的加速方式不起作用，它仅仅作用于 SNA 的加速方式。
*   当 DRI3 被启用时，这个选项应该是不需要的。

### 禁用垂直同步 (VSYNC)

在`/etc/X11/xorg.conf.d/20-intel.conf` 的 `Section "Device"` 段添加 `Option "SwapbuffersWait" "false"` 可禁用 VSYNC.

在 `~/.drirc` 中将 `vblank_mode` 设为 `0` 并且将 `driver` 设为 `dri2` 也可达到上述效果:

 `~/.drirc` 
```
<device screen="0" driver="dri2">
   <application name="Default">
   <option name="vblank_mode" value="0"/>
   </application>
</device>
```

### 设置自动缩放模式

在一些全屏应用中此方法适用:

```
$ xrandr --output LVDS1 --set PANEL_FITTING param

```

`param` 可以是:

*   `center`: 使用自定义分辨率，不缩放；
*   `full`: 使用全屏；
*   `full_aspect`: 在长宽比不变的情况下使用最大可用分辨率。

若无效，可尝试:

```
$ xrandr --output LVDS1 --set "scaling mode" param

```

`param`可以是`"Full"`、`"Center"` 或 `"Full aspect"`.

### KMS 问题: 终端面积很小

在启动阶段，启用了低分辨率的接口会导致终端面积很小。通过i915模块设置可解决此问题，具体在加载器的内核参数添加 `video=SVIDEO-1:d`。内核参数的更多信息参考 [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") .

若无效，可试着禁用 TV1 或 VGA1 接口。

### 在 GMA 4500 硬解 H.264

GMA 4500 平台上，[libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) 只能硬解 MPEG-2。 H.264 的硬解为另一分支——g45-h264， 在 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 中安装 [libva-driver-intel-g45-h264](https://aur.archlinux.org/packages/libva-driver-intel-g45-h264/) 就OK。 但注意 g45-h264 目前仍处于试验阶段，且开发不活跃。通过 VA-API 会减轻cpu的负载但不如使用非加速方式流畅。 mplayer的测试表明 使用vaapi 播放H.264 编码的 1080p 视频会让cpu的负载减半 (与XV相比) ，但播放很不稳定, 而 720p 则很到位 [[5]](https://bbs.archlinux.org/viewtopic.php?id=150550)。其他一些用户也提到这点[[6]](http://www.emmolution.org/?p=192&cpage=1#comment-12292)。

### 设置伽马和亮度

See [Backlight](/index.php/Backlight "Backlight").

## 疑难解答

### SNA 问题

xf86-video-intel 现在默认的加速方式为SNA，如果出现图形问题，可以尝试使用使用旧的 UXA 加速方式, 创建包含下列内容的`/etc/X11/xorg.conf.d/20-intel.conf` 就可使用UXA:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "uxa"
EndSection
```

### DRI3 问题

*DRI3* 是 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 默认的 DRI 版本，在有些系统上可能出现 [问题](https://bugs.chromium.org/p/chromium/issues/detail?id=370022)。要退回到 *DRI2*，在配置文件中加入:

```
Option "DRI" "2"

```

### Font and screen corruption in GTK+ applications (missing glyphs after suspend/resume)

Should you experience missing font glyphs in GTK+ applications, the following workaround might help. [Edit](/index.php/Textedit "Textedit") `/etc/environment` to add the following line:

 `/etc/environment`  `COGL_ATLAS_DEFAULT_BLIT_MODE=framebuffer` 

See also [FreeDesktop bug 88584](https://bugs.freedesktop.org/show_bug.cgi?id=88584).

### 在启动阶段，当 "Loading modules" 时黑屏

若使用 "late start" KMS ，当 "Loading modules" 时黑屏, 在 initramfs 中添加 `i915` 和 `intel_agp` 可能有帮助. 查看 [the above](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel") 的 KMS 节.

在尾部添加下面 [kernel parameter](/index.php/Kernel_parameters "Kernel parameters") 可能也会有效果:

```
video=SVIDEO-1:d

```

如果是输出到 VGA:

```
video=VGA-1:1280x800

```

### X 冻结/崩溃

使用 `NoAccel` 选项可能对 X 冻结／崩溃或显卡停止工作有效。

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "NoAccel" "True"
EndSection
```

此外， 也可尝试 `DRI` 选项来禁用 3D 加速:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier "Intel Graphics"
   Driver "intel"
   Option "DRI" "False"
EndSection
```

If you experience crashes and have

```
Option "TearFree" "true"
Option "AccelMethod" "sna"

```

in your configuration file, in most cases these can be fixed by adding

```
i915.semaphores=1

```

to your boot parameters.

If you are using kernel 4.0.X or above on Baytrail architecture and frequently encounter complete system freezes (especially when watching video or using GFX intensivelly), you should try adding the following kernel option as a workaround, until [this bug](https://bugzilla.kernel.org/show_bug.cgi?id=109051) will be fixed permanently.

```
 intel_idle.max_cstate=1

```

### 添加未识别分辨率

[Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr") 讲到了此问题。

### Weathered colors (color range problem)

**Note:** This problem is related to the [changes](http://lists.freedesktop.org/archives/dri-devel/2013-January/033576.html) in the kernel 3.9\. This problem still remains in kernel 4.1.

Kernel 3.9 contains a new default "Automatic" mode for the "Broadcast RGB" property in the Intel driver. It is almost equivalent to "Limited 16:235" (instead of the old default "Full") whenever an HDMI/DP output is in a [CEA mode](http://raspberrypi.stackexchange.com/questions/7332/what-is-the-difference-between-cea-and-dmt). If a monitor does not support signal in limited color range, it will cause weathered colors.

**Note:** Some monitors/TVs support both color range. In that case an option often known as *Black Level* may need to be adjusted to make them handle the signal correctly. Some TVs can handle signal in limited range only. Setting Broadcast RGB to "Full" will cause color clipping. You may need to set it to "Limited 16:235" manually to avoid the clipping.

One can force mode e.g. `xrandr --output <HDMI> --set "Broadcast RGB" "Full"` (replace `<HDMI>` with the appropriate output device, verify by running `xrandr`).

Unfortunately, the Intel driver does not support setting the color range through an `xorg.conf.d` configuration file.

A [bug report](https://bugzilla.kernel.org/show_bug.cgi?id=94921) is filed and a patch can be found in the attachment.

Also there are other related problems which can be fixed editing GPU registers. More information can be found [[7]](http://lists.freedesktop.org/archives/intel-gfx/2012-April/016217.html) and [[8]](http://github.com/OpenELEC/OpenELEC.tv/commit/09109e9259eb051f34f771929b6a02635806404c).

### Backlight is not adjustable

If after resuming from suspend, the hotkeys for changing the screen brightness do not take effect, check your configuration against the [Backlight](/index.php/Backlight "Backlight") article.

If the problem persists, try one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_osi=Linux
acpi_osi="!Windows 2012"
acpi_osi=

```

### Disabling frame buffer compression

Enabling frame buffer compression on pre-Sandy Bridge CPUs results in endless error messages:

```
$ dmesg |tail 
[ 2360.475430] [drm] not enough stolen space for compressed buffer (need 4325376 bytes), disabling
[ 2360.475437] [drm] hint: you may be able to increase stolen memory size in the BIOS to avoid this

```

The solution is to disable frame buffer compression which will slightly increase power consumption. In order to disable it add `i915.enable_fbc=0` to the kernel line parameters. More information on the results of disabled compression can be found [here](http://zinc.canonical.com/~cking/power-benchmarking/background-colour-and-framebuffer-compression/results.txt).

### Corruption/Unresponsiveness in Chromium and Firefox

If you experience corruption or unresponsiveness in Chromium and/or Firefox [set the AccelMethod to "uxa"](#SNA_issues).

### Kernel crashing w/kernels 4.0+ on Broadwell/Core-M chips

A few seconds after X/Wayland loads the machine will freeze and journalctl will log a kernel crash referencing the Intel graphics as below:

```
Jun 16 17:54:03 hostname kernel: BUG: unable to handle kernel NULL pointer dereference at           (null)
Jun 16 17:54:03 hostname kernel: IP: [<          (null)>]           (null)
...
Jun 16 17:54:03 hostname kernel: CPU: 0 PID: 733 Comm: gnome-shell Tainted: G     U     O    4.0.5-1-ARCH #1
...
Jun 16 17:54:03 hostname kernel: Call Trace:
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055cc27>] ? i915_gem_object_sync+0xe7/0x190 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0579634>] intel_execlists_submission+0x294/0x4c0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa05539fc>] i915_gem_do_execbuffer.isra.12+0xabc/0x1230 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa055d349>] ? i915_gem_object_set_to_cpu_domain+0xa9/0x1f0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ba2ae>] ? __kmalloc+0x2e/0x2a0
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555471>] i915_gem_execbuffer2+0x141/0x2b0 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa042fcab>] drm_ioctl+0x1db/0x640 [drm]
Jun 16 17:54:03 hostname kernel:  [<ffffffffa0555330>] ? i915_gem_execbuffer+0x450/0x450 [i915]
Jun 16 17:54:03 hostname kernel:  [<ffffffff8122339b>] ? eventfd_ctx_read+0x16b/0x200
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebc36>] do_vfs_ioctl+0x2c6/0x4d0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811f6452>] ? __fget+0x72/0xb0
Jun 16 17:54:03 hostname kernel:  [<ffffffff811ebec1>] SyS_ioctl+0x81/0xa0
Jun 16 17:54:03 hostname kernel:  [<ffffffff8157a589>] system_call_fastpath+0x12/0x17
Jun 16 17:54:03 hostname kernel: Code:  Bad RIP value.
Jun 16 17:54:03 hostname kernel: RIP  [<          (null)>]           (null)

```

This can be fixed by disabling execlist support which was changed to default on with kernel 4.0\. Add the following kernel parameter:

```
i915.enable_execlists=0

```

This is known to be broken to at least kernel 4.0.5.

### Skylake support

For linux kernels older than 4.3.x, `i915.preliminary_hw_support=1` must be added to your boot parameters for the driver to work on the new Intel Skylake (6th gen.) GPUs. On a fully updated system running kernel 4.3.x and up, this step is unneccesary.

**Note:** Fixes for the GPU/DRM bugs are pending in kernel 4.6\. The following steps are unneccesary if you have [testing](/index.php/Testing "Testing") repo enabled, or once 4.6 lands in [core](/index.php/Official_repositories#core "Official repositories").

The i915 DRM driver is known to cause various GPU hangs, crashes and even full system freezes. It might be neccesary to disable hardware acceleration to workaround these issues. One solution is to use the following Xorg configuration.

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
	Identifier  "Intel Graphics"
	Driver      "intel"
	Option	    "DRI"	"false"
EndSection

```

Otherwise, specific applications such as Chromium and Firefox browsers can be instructed to disable hardware rendering directly.

Another option that seems to work for some users is to add the `i915.enable_rc6=0` kernel boot parameter, which will cause the CPU/GPU to remain in high-power modes, but seems to resolve most cases of GPU hangs and system freezes.

**Note:** If the system appears to hang after "Loading Initial Ramdisk", make sure that the IGD aperture size in BIOS is less than 4GB.

### Lag in Windows guests

The video output of a Windows guests in VirtualBox sometimes hangs until the host forces a screen update (e.g. by moving the mouse cursor). Removing the `enable_fbc=1` option fixes this issue.

## 更多信息

*   [http://intellinuxgraphics.org/documentation.html](http://intellinuxgraphics.org/documentation.html) (包括一个被支持的硬件列表)
*   [KMS](/index.php/KMS "KMS") — Arch维基上关于 kernel mode setting 的文章
*   [Xrandr](/index.php/Xrandr "Xrandr") — 如果你有关于分辨率方面的问题，请参阅它。
*   Arch Linux 论坛中的讨论: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)