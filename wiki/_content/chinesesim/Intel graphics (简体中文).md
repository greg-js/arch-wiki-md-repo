**翻译状态：** 本文是英文页面 [Intel_Graphics](/index.php/Intel_Graphics "Intel Graphics") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-10-27，点击[这里](https://wiki.archlinux.org/index.php?title=Intel_Graphics&diff=0&oldid=407162)可以查看翻译后英文页面的改动。

由于Intel对X.Org开源驱动的支持，现在所需做的基本上是即插即用。

Intel显卡和相应芯片组、cpu的完整型号参考[this comparison on wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Intel_graphics_processing_units "wikipedia:Comparison of Intel graphics processing units")。

**注意:** 开源驱动不支持基于PowerVR的显卡([GMA 500](/index.php/Poulsbo "Poulsbo") and [GMA 3600](/index.php/Intel_GMA3600 "Intel GMA3600") series)。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
*   [3 加载](#.E5.8A.A0.E8.BD.BD)
    *   [3.1 启用 early KMS](#.E5.90.AF.E7.94.A8_early_KMS)
*   [4 Module-based Powersaving Options](#Module-based_Powersaving_Options)
*   [5 技巧](#.E6.8A.80.E5.B7.A7)
    *   [5.1 选择加速方式](#.E9.80.89.E6.8B.A9.E5.8A.A0.E9.80.9F.E6.96.B9.E5.BC.8F)
    *   [5.2 设置自动缩放模式](#.E8.AE.BE.E7.BD.AE.E8.87.AA.E5.8A.A8.E7.BC.A9.E6.94.BE.E6.A8.A1.E5.BC.8F)
    *   [5.3 KMS 问题: 终端面积很小](#KMS_.E9.97.AE.E9.A2.98:_.E7.BB.88.E7.AB.AF.E9.9D.A2.E7.A7.AF.E5.BE.88.E5.B0.8F)
    *   [5.4 在 GMA 4500 硬解 H.264](#.E5.9C.A8_GMA_4500_.E7.A1.AC.E8.A7.A3_H.264)
    *   [5.5 设置伽马和亮度](#.E8.AE.BE.E7.BD.AE.E4.BC.BD.E9.A9.AC.E5.92.8C.E4.BA.AE.E5.BA.A6)
*   [6 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [6.1 Glxgears 显示性能低下](#Glxgears_.E6.98.BE.E7.A4.BA.E6.80.A7.E8.83.BD.E4.BD.8E.E4.B8.8B)
        *   [6.1.1 禁用 VSYNC](#.E7.A6.81.E7.94.A8_VSYNC)
    *   [6.2 在启动阶段，当 "Loading modules" 时黑屏](#.E5.9C.A8.E5.90.AF.E5.8A.A8.E9.98.B6.E6.AE.B5.EF.BC.8C.E5.BD.93_.22Loading_modules.22_.E6.97.B6.E9.BB.91.E5.B1.8F)
    *   [6.3 播放视频时屏幕撕裂](#.E6.92.AD.E6.94.BE.E8.A7.86.E9.A2.91.E6.97.B6.E5.B1.8F.E5.B9.95.E6.92.95.E8.A3.82)
    *   [6.4 X 冻结/崩溃](#X_.E5.86.BB.E7.BB.93.2F.E5.B4.A9.E6.BA.83)
    *   [6.5 添加未识别分辨率](#.E6.B7.BB.E5.8A.A0.E6.9C.AA.E8.AF.86.E5.88.AB.E5.88.86.E8.BE.A8.E7.8E.87)
    *   [6.6 更新到 libGL 9 和 Intel-DRI 9 后，系统变慢](#.E6.9B.B4.E6.96.B0.E5.88.B0_libGL_9_.E5.92.8C_Intel-DRI_9_.E5.90.8E.EF.BC.8C.E7.B3.BB.E7.BB.9F.E5.8F.98.E6.85.A2)
    *   [6.7 视频游戏时出现黑色纹理](#.E8.A7.86.E9.A2.91.E6.B8.B8.E6.88.8F.E6.97.B6.E5.87.BA.E7.8E.B0.E9.BB.91.E8.89.B2.E7.BA.B9.E7.90.86)
*   [7 更多信息](#.E6.9B.B4.E5.A4.9A.E4.BF.A1.E6.81.AF)

## 安装

先安装 [Xorg](/index.php/Xorg "Xorg")，然后[安装](/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Pacman (简体中文)")位于[官方软件仓库](/index.php/Official_repositories_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Official repositories (简体中文)")的 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 软件包。它提供了用于2D加速的DDX驱动和旧显卡的[XvMC](/index.php/XvMC "XvMC")视频解码驱动。它依赖于3D加速的DRI驱动 [mesa](https://www.archlinux.org/packages/?name=mesa)。

启用OpenGL支持, 安装 [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl).64位系统需要安装[lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) 才能在 32 位程序中使用加速功能。

要使用新 GPU 的硬件编解码功能，请按装官方软件仓库中的[libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver)和[libva](https://www.archlinux.org/packages/?name=libva)软件包，它提供了[VA-API](/index.php/VA-API "VA-API")驱动。

## 配置

没必要做任何形式的配置来运行X.ORG（不需要`xorg.conf`，但若有则要正确配置）。

However, to take advantage of some driver options, you will need to create a Xorg configuration file similar to the one below:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
EndSection
```

Additional options are added by the user on new lines below `Driver`.

**Note:**

*   You may need to indicate `AccelMethod` when creating a configuration file, even just to set it to the default method (currently `"sna"`); otherwise, X may crash.
*   You might need to add more device sections than the one listed above. This will be indicated where necessary.

查看完整选项，输入`man intel`。

## 加载

英特尔内核模块在系统启动时自动加载. 如果它不启动，则:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since Intel requires kernel mode-setting.
*   Also, check that you have not disabled Intel by using any modprobe blacklisting within `/etc/modprobe.d/` or `/usr/lib/modprobe.d/`.

### 启用 early KMS

**Tip:** If you have problems with the resolution, you can check whether [enforcing the mode](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") helps.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS)的支持,使用的的i915 DRM驱动程序英特尔芯片组和是强制性的，默认情况下启用。

KMS之后，通常初始化[initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process")，这是可能的，但是，要在initramfs的阶段启用KMS。添加`i915`模块到`/etc/mkinitcpio.conf`的`MODULES`行：

```
MODULES="**i915**"

```

**Tip:** Users might need to add `intel_agp` before `i915` to suppress the ACPI errors. The order matters because the modules are activated in sequence.

如果您使用的是自定义的 [EDID](https://en.wikipedia.org/wiki/Extended_display_identification_data "wikipedia:Extended display identification data") 文件, you should embed it into initramfs as well:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

然后，重新生成initramfs

```
mkinitcpio -p linux

```

重启系统，一切搞定！

## Module-based Powersaving Options

The `i915` kernel module allows for configuration via [module options](/index.php/Kernel_modules#Setting_module_options "Kernel modules"). Some of the module options impact power saving.

A list of all options along with short descriptions and default values can be generated with the following command:

```
$ modinfo -p i915

```

To check which options are currently enabled, run

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

You can experiment with higher values for `enable_rc6`, but your GPU may not support them or the activation of the other options [[1]](https://wiki.archlinux.org/index.php?title=Talk:Intel_Graphics&oldid=327547#Kernel_Module_options).

Framebuffer compression, for example, may be unreliable or unavailable on Intel GPU generations before Sandy Bridge (generation 6). This results in messages logged to the system journal similar to this one:

```
kernel: drm: not enough stolen space for compressed buffer, disabling.

```

## 技巧

### 选择加速方式

*   UXA - (Unified Acceleration Architecture) 是支持GEM驱动模型(GEM driver model)的成熟后端(backend)
*   SNA - (Sandybridge's New Acceleration) 在有硬件支持下比UXA更快

现在默认的加速方式为SNA(截至 2013-08-05[[2]](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/xf86-video-intel&id=d03f5fb77df413017821f492aa81e5d68def7e48))，比UXA更快，但是稳定性比UXA稍差

DDX驱动可重设你需要的加速方式。Phoronix的基准测试在 [[3]](http://www.phoronix.com/scan.php?page=news_item&px=MTEzOTE).Sandy Bridge为[[4]](http://www.phoronix.com/scan.php?page=article&item=intel_glamor_first&num=1)，Ivy Bridge为[[5]](http://www.phoronix.com/scan.php?page=article&item=intel_ivy_glamor&num=1). 若使用SNA有问题，UXA仍为稳妥的选择.

要使用旧的UXA加速方式, 创建包含下列内容的`/etc/X11/xorg.conf.d/20-intel.conf` 就可使用UXA:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
   Identifier  "Intel Graphics"
   Driver      "intel"
   Option      "AccelMethod"  "uxa"
EndSection
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

GMA 4500 平台上，[libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver) 只能硬解 MPEG-2。 H.264 的硬解为另一分支——g45-h264， 在 [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") 中安装 [libva-driver-intel-g45-h264](https://aur.archlinux.org/packages/libva-driver-intel-g45-h264/) 就OK。 但注意 g45-h264 目前仍处于试验阶段，且开发不活跃。通过 VA-API 会减轻cpu的负载但不如使用非加速方式流畅。 mplayer的测试表明 使用vaapi 播放H.264 编码的 1080p 视频会让cpu的负载减半 (与XV相比) ，但播放很不稳定, 而 720p 则很到位 [[6]](https://bbs.archlinux.org/viewtopic.php?id=150550)。其他一些用户也提到这点[[7]](http://www.emmolution.org/?p=192&cpage=1#comment-12292)。

### 设置伽马和亮度

Intel没有提供在驱动层面设置这些值的途径，幸运的是，可通过 `xgamma` 和 `xrandr` 来设置。

设置伽马:

```
$ xgamma -gamma 1.0

```

或:

```
$ xrandr --output VGA1 --gamma 1.0:1.0:1.0

```

设置亮度:

```
$ xrandr --output VGA1 --brightness 1.0

```

## 疑难解答

### Glxgears 显示性能低下

**注意:** `glxgears` 不是在不同系统上进行比较的基准测试工具。

若运行 `glxgears` 来获取显卡性能参数, 你会发现结果都在 60 FPS 左右， 如:

```
[...]
311 frames in 5.0 seconds = 61.973 FPS
311 frames in 5.0 seconds = 62.064 FPS
311 frames in 5.0 seconds = 62.026 FPS
[...]

```

这不是性能低下的表现, 这是因为显卡使用了 [vertical synchronization](https://en.wikipedia.org/wiki/Analog_television#Vertical_synchronization "wikipedia:Analog television"), 也就是显示器的原生帧频.

#### 禁用 VSYNC

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

### 在启动阶段，当 "Loading modules" 时黑屏

若使用 "late start" KMS ，当 "Loading modules" 时黑屏, 在 initramfs 中添加 `i915` 和 `intel_agp` 可能有帮助. 查看 [the above](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel") 的 KMS 节.

在尾部添加下面 [kernel parameter](/index.php/Kernel_parameters "Kernel parameters") 可能也会有效果:

```
video=SVIDEO-1:d

```

### 播放视频时屏幕撕裂

若使用 SNA，将下列内容添加到 `/etc/X11/xorg.conf.d/20-intel.conf` 的 `Device` 段可杜绝屏幕撕裂问题。

```
Option "TearFree" "true"

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

### 添加未识别分辨率

[Xrandr page](/index.php/Xrandr#Adding_undetected_resolutions "Xrandr") 讲到了此问题。

### 更新到 libGL 9 和 Intel-DRI 9 后，系统变慢

[降级软件包](/index.php/Downgrading_packages#ARM "Downgrading packages") 到 Intel-DRI 8 和 libGL 8.

### 视频游戏时出现黑色纹理

启用 S3TC 纹理压缩支持可能会解决此问题。 通过 [driconf](https://www.archlinux.org/packages/?name=driconf) 或安装 [libtxc_dxtn](https://www.archlinux.org/packages/?name=libtxc_dxtn) 都可启用。

此问题很快会得到解决，参考 [newer drivers](http://www.phoronix.com/scan.php?page=news_item&px=MTIwOTg)

更多 S3TC 信息参考: [http://dri.freedesktop.org/wiki/S3TC](http://dri.freedesktop.org/wiki/S3TC) [wikipedia:S3_Texture_Compression](https://en.wikipedia.org/wiki/S3_Texture_Compression "wikipedia:S3 Texture Compression")

受此影响的其中一个游戏是 [Oil Rush](http://www.phoronix.com/scan.php?page=article&item=unigine_oilrush_gold&num=2)

## 更多信息

*   [http://intellinuxgraphics.org/documentation.html](http://intellinuxgraphics.org/documentation.html) (includes a list of supported hardware)
*   [KMS](/index.php/KMS "KMS") — Arch wiki article on kernel mode setting
*   [Xrandr](/index.php/Xrandr "Xrandr") — If you have problems setting the resolution
*   Arch Linux forums: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)