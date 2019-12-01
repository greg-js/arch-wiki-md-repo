Related articles

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")
*   [ATI](/index.php/ATI "ATI")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Vulkan](/index.php/Vulkan "Vulkan")

[AMDGPU](https://en.wikipedia.org/wiki/AMDGPU "wikipedia:AMDGPU") is the open source graphics driver for the latest AMD Radeon graphics cards.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Selecting the right driver](#Selecting_the_right_driver)
*   [2 Installation](#Installation)
    *   [2.1 Enable Southern Islands (SI) and Sea Islands (CIK) support](#Enable_Southern_Islands_(SI)_and_Sea_Islands_(CIK)_support)
        *   [2.1.1 Specify the correct module order](#Specify_the_correct_module_order)
        *   [2.1.2 Set required module parameters](#Set_required_module_parameters)
            *   [2.1.2.1 Set module parameters in kernel command line](#Set_module_parameters_in_kernel_command_line)
            *   [2.1.2.2 Set module parameters in modprobe.d](#Set_module_parameters_in_modprobe.d)
    *   [2.2 AMDGPU PRO](#AMDGPU_PRO)
    *   [2.3 ACO compiler](#ACO_compiler)
*   [3 Loading](#Loading)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Xorg configuration](#Xorg_configuration)
    *   [4.1 Tear free rendering](#Tear_free_rendering)
    *   [4.2 DRI level](#DRI_level)
    *   [4.3 Variable refresh rate](#Variable_refresh_rate)
*   [5 Features](#Features)
    *   [5.1 Video acceleration](#Video_acceleration)
    *   [5.2 Monitoring](#Monitoring)
        *   [5.2.1 CLI (default)](#CLI_(default))
        *   [5.2.2 GUI](#GUI)
    *   [5.3 Overclocking](#Overclocking)
        *   [5.3.1 Boot parameter](#Boot_parameter)
        *   [5.3.2 Manual (default)](#Manual_(default))
        *   [5.3.3 Assisted](#Assisted)
            *   [5.3.3.1 CLI tools](#CLI_tools)
            *   [5.3.3.2 GUI tools](#GUI_tools)
        *   [5.3.4 Startup on boot](#Startup_on_boot)
    *   [5.4 Enable GPU display scaling](#Enable_GPU_display_scaling)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Xorg or applications will not start](#Xorg_or_applications_will_not_start)
    *   [6.2 Screen artifacts and frequency problem](#Screen_artifacts_and_frequency_problem)
    *   [6.3 R9 390 series poor performance and/or instability](#R9_390_series_poor_performance_and/or_instability)
    *   [6.4 Freezes with "[drm] IP block:gmc_v8_0 is hung!" kernel error](#Freezes_with_"[drm]_IP_block:gmc_v8_0_is_hung!"_kernel_error)
    *   [6.5 Cursor corruption](#Cursor_corruption)
    *   [6.6 System freeze or crash when gaming on Vega cards](#System_freeze_or_crash_when_gaming_on_Vega_cards)

## Selecting the right driver

Depending on the card you have, find the right driver in [Xorg#AMD](/index.php/Xorg#AMD "Xorg"). This page has instructions for **AMDGPU** and **AMDGPU PRO**.

At the moment there is support for [Volcanic Islands (VI)](https://www.x.org/wiki/RadeonFeature/) (and newer) and experimental support for [Sea Islands (CI)](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) and [Southern Islands (SI)](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-SI-Experimental-Code) cards. AMD has no plans to support pre-GCN GPUs.

Owners of unsupported GPUs may use the open source [radeon](/index.php/Radeon "Radeon") or the [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") driver instead.

## Installation

**Note:** If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.

[Install](/index.php/Install "Install") the [mesa](https://www.archlinux.org/packages/?name=mesa) package, which provides the DRI driver for 3D acceleration.

*   For 32-bit application support, also install the [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) package from the [multilib](/index.php/Multilib "Multilib") repostory.
*   For the DDX driver (which provides 2D acceleration in [Xorg](/index.php/Xorg "Xorg")), install the [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package.
*   For [Vulkan](/index.php/Vulkan "Vulkan") support, install the [vulkan-radeon](https://www.archlinux.org/packages/?name=vulkan-radeon) package. Optionally install the [lib32-vulkan-radeon](https://www.archlinux.org/packages/?name=lib32-vulkan-radeon) package for 32-bit application support.

Support for [accelerated video decoding](#Video_acceleration) is provided by [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) and [lib32-libva-mesa-driver](https://www.archlinux.org/packages/?name=lib32-libva-mesa-driver) for VA-API and [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages for VDPAU.

### Enable Southern Islands (SI) and Sea Islands (CIK) support

The [linux](https://www.archlinux.org/packages/?name=linux) package enables AMDGPU support for cards of the Southern Islands (SI) and Sea Islands (CIK). When building or compiling a [kernel](/index.php/Kernel "Kernel"), `CONFIG_DRM_AMDGPU_SI=Y` and/or `CONFIG_DRM_AMDGPU_CIK=Y` should be be set in the config.

#### Specify the correct module order

Even when AMDGPU support for SI/CIK has been enabled by the kernel, the [radeon](/index.php/Radeon "Radeon") driver may be loaded before the `amdgpu` driver.

Make sure `amdgpu` has been set as first module in the [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array, e.g. `MODULES=(amdgpu radeon)`.

#### Set required module parameters

The [module parameters](/index.php/Module_parameters "Module parameters") of both `amdgpu` and `radeon` modules are `cik_support=` and `si_support=`.

They need to be set as kernel parameters or in a *modprobe* configuration file, and depend on the cards GCN version.

**Tip:** [dmesg](/index.php/Dmesg "Dmesg") may indicate the correct kernel parameter to use: `[..] amdgpu 0000:01:00.0: Use radeon.cik_support=0 amdgpu.cik_support=1 to override`.

##### Set module parameters in kernel command line

Set one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

*   Southern Islands (SI): `radeon.si_support=0 amdgpu.si_support=1`
*   Sea Islands (CIK): `radeon.cik_support=0 amdgpu.cik_support=1`

##### Set module parameters in modprobe.d

Create the configuration [modprobe](/index.php/Modprobe "Modprobe") files in `/etc/modprobe.d/`, see [modprobe.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/modprobe.d.5) for syntax details.

For Southern Islands (SI) use option `si_support=1`, for Sea Islands (CIK) use option `cik_support=1`, e.g.:

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

Make sure `modconf` is in the the `HOOKS` array in `/etc/mkinitcpio.conf` and [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

### AMDGPU PRO

AMD provides a proprietary, binary userland driver called *AMDGPU PRO*, which works on top of the open-source AMDGPU kernel driver.

From [Radeon Software 18.50 vs Mesa 19 benchmarks](http://www.phoronix.com/vr.php?view=27266) article: When it comes to OpenGL games, the RadeonSI Gallium3D driver simply dominates the proprietary AMD OpenGL driver. About the only advantage to the closed-source AMD OpenGL driver is its support for GL 4.6 while RadeonSI is still limited to GL 4.5 until its SPIR-V ingestion support is completed.

Install the [amdgpu-pro-libgl](https://aur.archlinux.org/packages/amdgpu-pro-libgl/). Optionally install the [lib32-amdgpu-pro-libgl](https://aur.archlinux.org/packages/lib32-amdgpu-pro-libgl/) package for 32-bit application support.

### ACO compiler

[ACO](https://steamcommunity.com/games/221410/announcements/detail/1602634609636894200) is an open-source shader compiler developed by [Valve](https://en.wikipedia.org/wiki/Valve_Corporation "wikipedia:Valve Corporation") to directly compete with [LLVM](http://llvm.org/) and [Windows 10](https://en.wikipedia.org/wiki/Windows_10 "wikipedia:Windows 10"). It offers lesser compilation time and also provides more FPS (sources from [It's FOSS](https://itsfoss.com/linux-games-performance-boost-amd-gpu/), [Forbes](https://www.forbes.com/sites/jasonevangelho/2019/07/17/these-windows-10-vs-pop-os-benchmarks-reveal-a-surprising-truth-about-linux-gaming-performance/#d5e808c5e747) and [Phoronix](https://www.phoronix.com/scan.php?page=article&item=radv-aco-llvm&num=1)).

**Warning:** ACO is a very early development and still is marked as **testing**, you may experience issues.

[Follow the instructions here](https://steamcommunity.com/app/221410/discussions/0/1640915206474070669/) to take advantage of the ACO compiler.

## Loading

The `amdgpu` kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure to [#Enable Southern Islands (SI) and Sea Islands (CIK) support](#Enable_Southern_Islands_(SI)_and_Sea_Islands_(CIK)_support) when needed.
*   Make sure you have the latest [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package installed. This driver requires the latest firmware for each model to successfully boot.
*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since `amdgpu` requires [KMS](/index.php/KMS "KMS").
*   Check that you have not disabled `amdgpu` by using any [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

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

### Tear free rendering

*TearFree* controls tearing prevention using the hardware page flipping mechanism. If this option is set, the default value of the property is 'on' or 'off' accordingly. If this option is not set, the default value of the property is auto, which means that TearFree is on for rotated outputs, outputs with RandR transforms applied and for RandR 1.4 slave outputs, otherwise off:

```
Option "TearFree" "true"

```

You can also enable TearFree temporarily with [xrandr](/index.php/Xrandr "Xrandr"):

```
# xrandr --output *output* --set TearFree on

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

### Monitoring

Monitoring your GPU is often used to check the temperature and also the P-states of your GPU.

#### CLI (default)

To check your GPU's P-states, execute:

```
# cat /sys/class/drm/card0/device/pp_od_clk_voltage

```

To monitor your GPU, execute:

```
# watch -n 0.5  cat /sys/kernel/debug/dri/0/amdgpu_pm_info

```

#### GUI

*   **WattmanGTK** — A GTK GUI tool to monitor your GPU's temperatures P-states

	[https://github.com/BoukeHaarsma23/WattmanGTK](https://github.com/BoukeHaarsma23/WattmanGTK) || [wattman-gtk-git](https://aur.archlinux.org/packages/wattman-gtk-git/).

*   **TuxClocker** — A Qt5 monitoring and overclocking tool.

	[https://github.com/Lurkki14/tuxclocker](https://github.com/Lurkki14/tuxclocker) || [tuxclocker](https://aur.archlinux.org/packages/tuxclocker/) [tuxclocker-git](https://aur.archlinux.org/packages/tuxclocker-git/)

### Overclocking

Since Linux 4.17, it is possible to adjust clocks and voltages of the graphics card via `/sys/class/drm/card0/device/pp_od_clk_voltage`.

#### Boot parameter

It is required to unlock access to adjust clocks and voltages in sysfs by appending the [Kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `amdgpu.ppfeaturemask=0xfffd7fff`.

#### Manual (default)

**Note:** In sysfs, paths like `/sys/class/drm/...` are just symlinks and may change between reboots. Persistent locations can be found in `/sys/devices/`, e.g. `/sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0/`. Adjust the commands accordingly for a reliable result.

To set the GPU clock for the maximum P-state 7 on e.g. a Polaris GPU to 1209MHz and 900mV voltage, run:

```
# echo "s 7 1209 900" > /sys/class/drm/card0/device/pp_od_clk_voltage

```

The same procedure can be applied to the VRAM, e.g. maximum P-state 2 on Polaris 5xx series cards:

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

It is also possible to forbid the driver so switch to certain P-states, e.g. to workaround problems with deep powersaving P-states like flickering artifacts or stutter. To force the highest VRAM P-state on a Polaris RX 5xx card, while still allowing the GPU itself to run with lower clocks, run:

```
# echo "manual" > /sys/class/drm/card0/device/power_dpm_force_performance_level
# echo "2" >  /sys/class/drm/card0/device/pp_dpm_mclk

```

Allow only the three highest GPU P-states:

```
# echo "5 6 7" >  /sys/class/drm/card0/device/pp_dpm_sclk

```

To set the allowed maximum power consumption of the GPU to e.g. 50 Watts, run

```
# echo 50000000 > /sys/class/drm/card0/device/hwmon/hwmon0/power1_cap

```

Until Linux kernel 4.20, it will only be possible to decrease the value, not increase.

**Note:** The above procedure was tested with a Polaris RX 560 card. There may be different behavior or bugs with different GPUs.

#### Assisted

If you are not inclined to fully manually overclock your GPU, there are some overclocking tools that are offered by the community to assist you to overclock and monitor your AMD GPU.

##### CLI tools

*   **amdgpu-clocks** — A script that can be used to monitor and set custom power states for AMD GPUs. It also offers a Systemd service to apply the settings automatically upon boot.

	[https://github.com/sibradzic/amdgpu-clocks](https://github.com/sibradzic/amdgpu-clocks) || [amdgpu-clocks-git](https://aur.archlinux.org/packages/amdgpu-clocks-git/)

##### GUI tools

*   **TuxClocker** — A Qt5 monitoring and overclocking tool.

	[https://github.com/Lurkki14/tuxclocker](https://github.com/Lurkki14/tuxclocker) || [tuxclocker](https://aur.archlinux.org/packages/tuxclocker/) [tuxclocker-git](https://aur.archlinux.org/packages/tuxclocker-git/)

*   **CoreCtrl** — A GUI overclocking tool with a WattMan-like UI that supports per-application profiles.

	[https://gitlab.com/corectrl/corectrl](https://gitlab.com/corectrl/corectrl) || [corectrl](https://aur.archlinux.org/packages/corectrl/) [corectrl-git](https://aur.archlinux.org/packages/corectrl-git/)

#### Startup on boot

If you want your settings to apply automatically upon boot, consider looking at this [Reddit thread](https://www.reddit.com/r/Amd/comments/agwroj/how_to_overclock_your_amd_gpu_on_linux/) to configure and apply your settings on boot.

### Enable GPU display scaling

To avoid the usage of the scaler which is built in the display, and use the GPU own scaler instead, when not using the native resolution of the monitor, execute:

```
$ xrandr --output *output* --set "scaling mode" *scaling_mode*

```

Possible values for `"scaling mode"` are: `None`, `Full`, `Center`, `Full aspect`.

*   To show the available outputs and settings, execute:

```
$ xrandr --prop

```

*   To set `scaling mode = Full aspect` for just every available output, execute:

```
$ for output in $(xrandr --prop | grep -E -o -i "^[A-Z\-]+-[0-9]+"); do xrandr --output "$output" --set "scaling mode" "Full aspect"; done

```

## Troubleshooting

### Xorg or applications will not start

*   "(EE) AMDGPU(0): [DRI2] DRI2SwapBuffers: drawable has no back or front?" error after opening glxgears, can open Xorg server but OpenGL apps crash.
*   "(EE) AMDGPU(0): Given depth (32) is not supported by amdgpu driver" error, Xorg will not start.

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

### R9 390 series poor performance and/or instability

If you experience issues [[5]](https://bugs.freedesktop.org/show_bug.cgi?id=91880) with a AMD R9 390 series graphics card, set `radeon.cik_support=0 radeon.si_support=0 amdgpu.cik_support=1 amdgpu.si_support=1 amdgpu.dpm=1 amdgpu.dc=1` as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to force the use of amdgpu driver instead of radeon.

If it still does not work, try disabling DPM, by setting the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to: `radeon.cik_support=0 radeon.si_support=0 amdgpu.cik_support=1 amdgpu.si_support=1`

### Freezes with "[drm] IP block:gmc_v8_0 is hung!" kernel error

If you experience freezes and kernel crashes during a GPU intensive task with the kernel error " [drm] IP block:gmc_v8_0 is hung!" [[6]](https://bugs.freedesktop.org/show_bug.cgi?id=102322), a workaround is to set `amdgpu.vm_update_mode=3` as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to force the GPUVM page tables update to be done using the CPU. Downsides are listed here [[7]](https://bugs.freedesktop.org/show_bug.cgi?id=102322#c15).

### Cursor corruption

If you experience issues with the mouse cursor sometimes not rendering properly, set `Option "SWCursor" "True"` in the `"Device"` section of the `/etc/X11/xorg.conf.d/20-amdgpu.conf` configuration file.

If you are using `xrandr` for scaling and the cursor is flickering or disappearing, you may be able to fix it by setting the `TearFree` property: `xrandr --output HDMI-A-0 --set TearFree on`.

### System freeze or crash when gaming on Vega cards

[Dynamic power management](/index.php/ATI#Dynamic_power_management "ATI") may cause a complete system freeze whilst gaming due to issues in the way GPU clock speeds are managed. [[8]](https://bugs.freedesktop.org/show_bug.cgi?id=109955) A workaround is to disable dynamic power management, see [ATI#Dynamic power management](/index.php/ATI#Dynamic_power_management "ATI") for details.