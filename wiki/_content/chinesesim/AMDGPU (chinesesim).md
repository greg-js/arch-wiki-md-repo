Related articles

*   [AMD Catalyst (简体中文)](/index.php/AMD_Catalyst_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "AMD Catalyst (简体中文)")
*   [ATI (简体中文)](/index.php/ATI_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ATI (简体中文)")
*   [Xorg (简体中文)](/index.php/Xorg_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Xorg (简体中文)")
*   [Vulkan](/index.php/Vulkan "Vulkan")

**翻译状态：** 本文是英文页面 [AMDGPU](/index.php/AMDGPU "AMDGPU") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-09-02，点击[这里](https://wiki.archlinux.org/index.php?title=AMDGPU&diff=0&oldid=581347)可以查看翻译后英文页面的改动。

**amdgpu** 是 AMD Radeon 显卡的开源图形驱动。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 选择正确的驱动](#选择正确的驱动)
*   [2 安装](#安装)
    *   [2.1 开启 Southern Islands (SI) and Sea Islands (CIK) 支持](#开启_Southern_Islands_(SI)_and_Sea_Islands_(CIK)_支持)
        *   [2.1.1 指定正确的模块加载顺序](#指定正确的模块加载顺序)
        *   [2.1.2 设置所需的模块参数](#设置所需的模块参数)
            *   [2.1.2.1 在内核命令行中设置模块参数](#在内核命令行中设置模块参数)
            *   [2.1.2.2 设置内核参数在 modprobe.d 中](#设置内核参数在_modprobe.d_中)
    *   [2.2 AMDGPU PRO](#AMDGPU_PRO)
*   [3 加载](#加载)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Xorg configuration](#Xorg_configuration)
    *   [4.1 Tear Free Rendering](#Tear_Free_Rendering)
    *   [4.2 DRI level](#DRI_level)
    *   [4.3 Variable refresh rate](#Variable_refresh_rate)
*   [5 Features](#Features)
    *   [5.1 Video acceleration](#Video_acceleration)
    *   [5.2 Overclocking](#Overclocking)
    *   [5.3 Enable GPU display scaling](#Enable_GPU_display_scaling)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Xorg or applications won't start](#Xorg_or_applications_won't_start)
    *   [6.2 Screen artifacts and frequency problem](#Screen_artifacts_and_frequency_problem)
    *   [6.3 R9 390 series Poor Performance and/or Instability](#R9_390_series_Poor_Performance_and/or_Instability)
    *   [6.4 Freezes with "[drm] IP block:gmc_v8_0 is hung!" kernel error](#Freezes_with_"[drm]_IP_block:gmc_v8_0_is_hung!"_kernel_error)
    *   [6.5 Cursor corruption](#Cursor_corruption)

## 选择正确的驱动

请参考[Xorg#AMD](/index.php/Xorg#AMD "Xorg")选择合适的显卡驱动，这个页面包含 **AMDGPU** 和 **AMDGPU PRO**的说明。

目前驱动支持[Volcanic Islands (VI)](https://www.x.org/wiki/RadeonFeature/) (和更新的显卡) 并且实验性支持 [Sea Islands (CI)](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) 和 [Southern Islands (SI)](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-SI-Experimental-Code) 显卡，AMD 没有计划支持更老的 GCN GPUs。

驱动不支持的显卡用户可以使用开源[radeon](/index.php/Radeon "Radeon")或则[AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")驱动代替。

## 安装

**Note:** 如果已安装专有的 Catalyst 驱动，请先卸载[AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst")。

安装这个[mesa](https://www.archlinux.org/packages/?name=mesa) 软件包，它提供 DRI 和 3D 加速。

*   为支持32位程序，也可以从[multilib](/index.php/Multilib "Multilib")仓库中安装[lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa)软件包。
*   为提供 DDX 驱动 (可提供 2D 加速 在[Xorg](/index.php/Xorg "Xorg")中)，可以安装这个 [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) 软件包。
*   为支持 [Vulkan](/index.php/Vulkan "Vulkan") , 可以安装 [vulkan-radeon](https://www.archlinux.org/packages/?name=vulkan-radeon) 软件包， 也可以选择安装[lib32-vulkan-radeon](https://www.archlinux.org/packages/?name=lib32-vulkan-radeon)软件包为 32 位程序提供支持。

想要开启[accelerated video decoding](#Video_acceleration)，可以安装[libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver)和[lib32-libva-mesa-driver](https://www.archlinux.org/packages/?name=lib32-libva-mesa-driver)软件包来支持 VA-API，安装[mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau)和[lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau)软件包支持VDPAU。

### 开启 Southern Islands (SI) and Sea Islands (CIK) 支持

[linux](https://www.archlinux.org/packages/?name=linux) 软件包 可以开启 AMDGPU 支持对于 the Southern Islands (SI) 和 Sea Islands (CIK)的显卡。 当编译和构建一个 [kernels (简体中文)](/index.php/Kernels_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernels (简体中文)"), 需要设置`CONFIG_DRM_AMDGPU_SI=Y` 和 `CONFIG_DRM_AMDGPU_CIK=Y` 参数。

#### 指定正确的模块加载顺序

当内核启用 AMDGPU 对 SI/CIK 显卡的支持时，[radeon](/index.php/Radeon "Radeon")驱动可能会在`amdgpu`驱动之前加载。

确保`amdgpu`在[Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio")数组中被设置为第一个模块，例如`MODULES=(amdgpu radeon)`。

#### 设置所需的模块参数

`amdgpu` 和 `radeon`模块都需要设置的[module parameters](/index.php/Module_parameters "Module parameters")是`cik_support=` and `si_support=`。

它们必需设置为内核参数或者在一个*modprobe*配置文件中，并且取决于显卡的 GCN 版本。

**Tip:** [dmesg](/index.php/Dmesg "Dmesg")可能会指示应该使用的正确内核参数: `[..] amdgpu 0000:01:00.0: Use radeon.cik_support=0 amdgpu.cik_support=1 to override`.

##### 在内核命令行中设置模块参数

设置以下 [kernel parameters](/index.php/Kernel_parameters "Kernel parameters")之一:

*   Southern Islands (SI): `radeon.si_support=0 amdgpu.si_support=1`
*   Sea Islands (CIK): `radeon.cik_support=0 amdgpu.cik_support=1`

##### 设置内核参数在 modprobe.d 中

在 `/etc/modprobe.d/`中创建配置 [modprobe](/index.php/Modprobe "Modprobe") 文件， 查看 [modprobe.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modprobe.d.5) 可以了解语法细节。

对于 Southern Islands (SI) 使用 `si_support=1` 选项，对于 Sea Islands (CIK) 使用 `cik_support=1` 选项，就像下面的例子一样:

 `/etc/modprobe.d/amdgpu.conf` 
```
options amdgpu si_support=1
options amdgpu cik_support=0
```
 `/etc/modprobe.d/radeon.conf` 
```
options radeon si_support=0
options radeon cik_support=0
```

确保 `modconf` 添加到 `HOOKS` 数组中在 `/etc/mkinitcpio.conf` 和 [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")。

### AMDGPU PRO

AMD 提供一个叫 *AMDGPU PRO* 的专有二进制用户驱动，它工作于开源驱动 AMDGPU 之上。

From [Radeon Software 18.50 vs Mesa 19 benchmarks](http://www.phoronix.com/vr.php?view=27266) article: When it comes to OpenGL games, the RadeonSI Gallium3D driver simply dominates the proprietary AMD OpenGL driver. About the only advantage to the closed-source AMD OpenGL driver is its support for GL 4.6 while RadeonSI is still limited to GL 4.5 until its SPIR-V ingestion support is completed.

安装 [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/)软件包， 也可以安装 [lib32-amdgpu-pro-libgl](https://aur.archlinux.org/packages/lib32-amdgpu-pro-libgl/) 软件包提供32位程序支持。

## 加载

应该会在系统启动时自动加载。

如果没有自动加载:

*   如果需要的话，确保 [#开启 Southern Islands (SI) and Sea Islands (CIK) 支持](#开启_Southern_Islands_(SI)_and_Sea_Islands_(CIK)_支持)。
*   确保你已经安装最新的 [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) 软件包。
*   确保你没有将 `nomodeset` 或 `vga=` 作为内核参数，因为`amdgpu` 需要 [KMS](/index.php/KMS "KMS")。
*   确保你没有禁用 `amdgpu` 通过使用 [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")。

### Enable early KMS

See [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting").

## Xorg configuration

[Xorg](/index.php/Xorg "Xorg") will automatically load the driver and it will use your monitor's EDID to set the native resolution. Configuration is only required for tuning the driver.

If you want manual configuration, create `/etc/X11/xorg.conf.d/20-amdgpu.conf`, and add the following:

 `/etc/X11/xorg.conf.d/20-amdgpu.conf` 
```
Section "Device"
     Identifier "AMD"
     Driver "amdgpu"
 EndSection
```

Using this section, you can enable features and tweak the driver settings, see [amdgpu(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/amdgpu.4) first before setting driver options.

### Tear Free Rendering

*TearFree* controls tearing prevention using the hardware page flipping mechanism. If this option is set, the default value of the property is 'on' or 'off' accordingly. If this option isn't set, the default value of the property is auto, which means that TearFree is on for rotated outputs, outputs with RandR transforms applied and for RandR 1.4 slave outputs, otherwise off:

```
Option "TearFree" "true"

```

### DRI level

*DRI* sets the maximum level of DRI to enable. Valid values are *2* for DRI2 or *3* for DRI3\. The default is *3* for DRI3 if the [Xorg](/index.php/Xorg "Xorg") version is >= 1.18.3, otherwise DRI2 is used:

```
Option "DRI" "3"

```

### Variable refresh rate

See [Variable refresh rate](/index.php/Variable_refresh_rate "Variable refresh rate").

## Features

### Video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

### Overclocking

Since Linux 4.17, it is possible to adjust clocks and voltages of the graphics card via `/sys/class/drm/card0/device/pp_od_clk_voltage`. It is however required to unlock access to it in sysfs by appending the boot parameter `amdgpu.ppfeaturemask=0xffffffff`.

**Note:** In sysfs, paths like `/sys/class/drm/...` are just symlinks and may change between reboots. Persistent locations can be found in `/sys/devices/`, e.g. `/sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0/`. Adjust the commands accordingly for a reliable result.

To set the GPU clock for the maximum pstate 7 on e.g. a Polaris GPU to 1209MHz and 900mV voltage, run:

```
# echo "s 7 1209 900" > /sys/class/drm/card0/device/pp_od_clk_voltage

```

The same procedure can be applied to the VRAM, e.g. maximum pstate 2 on Polaris 5xx series cards:

```
# echo "m 2 1850 850" > /sys/class/drm/card0/device/pp_od_clk_voltage

```

**Warning:** Double check the entered values, as mistakes might instantly cause fatal hardware damage!

To apply, run

```
# echo "c" > /sys/class/drm/card0/device/pp_od_clk_voltage

```

To check if it worked out, read out clocks and voltage under 3D load:

```
# watch -n 0.5  cat /sys/kernel/debug/dri/0/amdgpu_pm_info

```

You can reset to the default values using this:

```
# echo "r" > /sys/class/drm/card0/device/pp_od_clk_voltage

```

It is also possible to forbid the driver so switch to certain pstates, e.g. to workaround problems with deep powersaving pstates like flickering artifacts or stutter. To force the highest VRAM pstate on a Polaris RX 5xx card, while still allowing the GPU itself to run with lower clocks, run:

```
# echo "manual" > /sys/class/drm/card0/device/power_dpm_force_performance_level
# echo "2" >  /sys/class/drm/card0/device/pp_dpm_mclk

```

Allow only the three highest GPU pstates:

```
# echo "5 6 7" >  /sys/class/drm/card0/device/pp_dpm_sclk

```

To set the allowed maximum power consumption of the GPU to e.g. 50 Watts, run

```
# echo 50000000 > /sys/class/drm/card0/device/hwmon/hwmon0/power1_cap

```

Until Linux kernel 4.20, it will only be possible to decrease the value, not increase.

**Note:** The above procedure was tested with a Polaris RX 560 card. There may be different behavior or bugs with different GPUs.

### Enable GPU display scaling

To avoid the usage of the scaler which is built in the display, and use the GPU own scaler instead, when not using the native resolution of the monitor, execute:

```
$ xrandr --output "<output>" --set "scaling mode" "<scaling mode>"

```

Possible values for `"scaling mode"` are: `None, Full, Center, Full aspect`

*   To show the available outputs and settings, execute:

```
$ xrandr --prop

```

*   To set `scaling mode = Full aspect` for just every available output, execute:

```
$ for output in $(xrandr --prop | grep -E -o -i "^[A-Z\-]+-[0-9]+"); do xrandr --output "$output" --set "scaling mode" "Full aspect"; done

```

## Troubleshooting

### Xorg or applications won't start

*   "(EE) AMDGPU(0): [DRI2] DRI2SwapBuffers: drawable has no back or front?" error after opening glxgears, can open Xorg server but OpenGL apps crash.
*   "(EE) AMDGPU(0): Given depth (32) is not supported by amdgpu driver" error, Xorg won't start.

Setting the screen's depth under Xorg to 16 or 32 will cause problems/crash. To avoid that, you should use a standard screen depth of 24 by adding this to your "screen" section:

 `/etc/X11/xorg.conf.d/10-screen.conf` 
```
Section "Screen"
       Identifier     "Screen"
       DefaultDepth    24
       SubSection      "Display"
               Depth   24
       EndSubSection
EndSection

```

### Screen artifacts and frequency problem

[Dynamic power management](/index.php/ATI#Dynamic_power_management "ATI") may cause screen artifacts to appear when displaying to monitors at higher frequencies (120+Hz) due to issues in the way GPU clock speeds are managed[[1]](https://bugs.freedesktop.org/show_bug.cgi?id=96868)[[2]](https://bugs.freedesktop.org/show_bug.cgi?id=102646).

A workaround [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=96868#c13) is saving `high` or `low` in `/sys/class/drm/card0/device/power_dpm_force_performance_level`.

There is also a GUI solution [[4]](https://github.com/marazmista/radeon-profile) where you can manage the "power_dpm" with [radeon-profile-git](https://aur.archlinux.org/packages/radeon-profile-git/) and [radeon-profile-daemon-git](https://aur.archlinux.org/packages/radeon-profile-daemon-git/).

### R9 390 series Poor Performance and/or Instability

If you experience issues [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=91880) with a AMD R9 390 series graphics card, set `radeon.cik_support=0 radeon.si_support=0 amdgpu.cik_support=1 amdgpu.si_support=1 amdgpu.dpm=1 amdgpu.dc=1` as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to force the use of amdgpu driver instead of radeon.

If it still does not work, try disabling DPM, by setting the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to: `radeon.cik_support=0 radeon.si_support=0 amdgpu.cik_support=1 amdgpu.si_support=1`

### Freezes with "[drm] IP block:gmc_v8_0 is hung!" kernel error

If you experience freezes and kernel crashes during a GPU intensive task with the kernel error " [drm] IP block:gmc_v8_0 is hung!" [[6]](https://bugs.freedesktop.org/show_bug.cgi?id=102322), a workaround is to set `amdgpu.vm_update_mode=3` as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to force the GPUVM page tables update to be done using the CPU. Downsides are listed here [[7]](https://bugs.freedesktop.org/show_bug.cgi?id=102322#c15).

### Cursor corruption

If you experience issues with the mouse cursor sometimes not rendering properly, set `Option "SWCursor" "True"` in the `"Device"` section of the `/etc/X11/xorg.conf.d/20-amdgpu.conf` configuration file.

If you are using `xrandr` for scaling and the cursor is flickering or disappearing, you may be able to fix it by setting the `TearFree` property: `xrandr --output HDMI-A-0 --set TearFree on`.