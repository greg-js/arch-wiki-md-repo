Related articles

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")
*   [ATI](/index.php/ATI "ATI")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Vulkan](/index.php/Vulkan "Vulkan")

**amdgpu** is the open source graphics driver for the latest AMD Radeon graphics cards.

At the moment there is support for [Volcanic Islands (VI) and newer](https://www.x.org/wiki/RadeonFeature/) and experimental support for [Sea Islands (CI)](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) and [Southern Islands (SI)](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-SI-Experimental-Code) cards. AMD has absolutely no plans for supporting the pre-GCN GPUs.

Owners of unsupported AMD/ATI video cards may use the [Radeon open source](/index.php/ATI "ATI") or [AMD's proprietary](/index.php/AMD_Catalyst "AMD Catalyst") driver instead.

## Contents

*   [1 Selecting the right driver](#Selecting_the_right_driver)
*   [2 Installation](#Installation)
    *   [2.1 Enable Southern Islands (SI) and Sea Islands (CIK) support](#Enable_Southern_Islands_.28SI.29_and_Sea_Islands_.28CIK.29_support)
        *   [2.1.1 Set required module parameters](#Set_required_module_parameters)
    *   [2.2 AMD DC](#AMD_DC)
    *   [2.3 AMDGPU PRO](#AMDGPU_PRO)
*   [3 Loading](#Loading)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Xorg configuration](#Xorg_configuration)
*   [5 Performance tuning](#Performance_tuning)
    *   [5.1 Enabling video acceleration](#Enabling_video_acceleration)
    *   [5.2 Driver options](#Driver_options)
*   [6 Enable GPU display scaling](#Enable_GPU_display_scaling)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Xorg or applications won't start](#Xorg_or_applications_won.27t_start)
    *   [7.2 Screen artifacts and frequency problem](#Screen_artifacts_and_frequency_problem)
    *   [7.3 Screen flickering](#Screen_flickering)
    *   [7.4 R9 390 series Poor Performance and/or Instability](#R9_390_series_Poor_Performance_and.2For_Instability)
    *   [7.5 Freezes with "[drm] IP block:gmc_v8_0 is hung!" kernel error](#Freezes_with_.22.5Bdrm.5D_IP_block:gmc_v8_0_is_hung.21.22_kernel_error)

## Selecting the right driver

Depending on the card you have, find the right driver in [Xorg#AMD](/index.php/Xorg#AMD "Xorg"). This page has instructions for **AMDGPU** and **AMDGPU PRO**.

## Installation

**Note:** If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.

[Install](/index.php/Install "Install") the [mesa](https://www.archlinux.org/packages/?name=mesa) package, which provides the DRI driver for 3D acceleration.

*   For 32-bit application support, also install the [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) package from the [multilib](/index.php/Multilib "Multilib") repostory.
*   For the DDX driver (which provides 2D acceleration in [Xorg](/index.php/Xorg "Xorg")), install the [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package.
*   For [Vulkan](/index.php/Vulkan "Vulkan") support, install the [vulkan-radeon](https://www.archlinux.org/packages/?name=vulkan-radeon) package. Optionally install the [lib32-vulkan-radeon](https://www.archlinux.org/packages/?name=lib32-vulkan-radeon) package for 32-bit application support.

Support for [accelerated video decoding](#Enabling_video_acceleration) is provided by [libva-mesa-driver](https://www.archlinux.org/packages/?name=libva-mesa-driver) and [lib32-libva-mesa-driver](https://www.archlinux.org/packages/?name=lib32-libva-mesa-driver) or [libva-vdpau-driver](https://www.archlinux.org/packages/?name=libva-vdpau-driver) for VA-API and [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages for VDPAU.

### Enable Southern Islands (SI) and Sea Islands (CIK) support

The [linux](https://www.archlinux.org/packages/?name=linux) package enables AMDGPU support for cards of the Southern Islands (SI) and Sea Islands (CIK). When building or compiling a [kernel](/index.php/Kernel "Kernel"), `CONFIG_DRM_AMDGPU_SI=Y` and/or `CONFIG_DRM_AMDGPU_CIK=Y` should be be set in the config.

Even when AMDGPU support for SI/CIK has been enabled by the kernel, the [radeon](/index.php/Radeon "Radeon") driver may be used instead of the AMDGPU driver.

To make sure the `amdgpu` is loaded first use the following [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array, e.g. `MODULES=(amdgpu radeon)`.

#### Set required module parameters

To enable full support for SI/CIK when using the `amdgpu`, set the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to prevent the `radeon` module from being used [[1]](http://www.phoronix.com/scan.php?page=article&item=linux-413-gcn101&num=1):

 `$ dmesg` 
```
[..] amdgpu 0000:01:00.0: CIK support provided by radeon.
[..] amdgpu 0000:01:00.0: Use radeon.cik_support=0 amdgpu.cik_support=1 to override.
```

The flags depend on the cards GCN version:

*   Southern Islands (SI): `radeon.si_support=0 amdgpu.si_support=1`
*   Sea Islands (CIK): `radeon.cik_support=0 amdgpu.cik_support=1`

### AMD DC

AMD DC (display code), introduced in [linux](https://www.archlinux.org/packages/?name=linux) 4.15-4.17, is a new display stack that brings support for atomic mode-setting and HDMI/DP audio. For more info about AMDGPU-DC, see [this article](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-DC-Accepted).

If you are on GCN 1.1 or newer with AMDGPU and want to use DC, set `amdgpu.dc=1` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter").

### AMDGPU PRO

**Warning:** Arch Linux is officially not supported.

**Note:**

*   To use the proprietary OpenCL component without AMDGPU PRO, [install](/index.php/Install "Install") [opencl-amd](https://aur.archlinux.org/packages/opencl-amd/) instead.
*   A [downgrade](/index.php/Downgrade "Downgrade") of the [linux](https://www.archlinux.org/packages/?name=linux) (4.9) and [Xorg](/index.php/Xorg "Xorg") (1.18) packages is required to use AMDGPU PRO 17.10.

AMD provides a proprietary, binary userland driver called *AMDGPU PRO*, which works on top of the open-source AMDGPU kernel driver. The driver provides OpenGL, [OpenCL](/index.php/OpenCL "OpenCL"), [Vulkan](/index.php/Vulkan "Vulkan") and [VDPAU](/index.php/VDPAU "VDPAU") support (although this is also supported by the open-source driver). For some workloads it provides better performance than the open-source driver ([example benchmark](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-PRO-16.40-Deus-MD)), while for others it is true the contrary ([example benchmark](https://openbenchmarking.org/prospect/1610315-TA-AMDGPUPRO08/998ba9b677230564e0fbca342a8e1b9a7e85b6ab)).

See the [release notes](https://support.amd.com/en-us/kb-articles/Pages/AMDGPU-PRO-Driver-for-Linux-Release-Notes.aspx) and the [announcement at the Phoronix forum](https://www.phoronix.com/forums/forum/linux-graphics-x-org-drivers/amd-linux/855699-amd-representative-says-their-vulkan-linux-driver-will-be-here-soon/page6) for more information.

A patched version of the official AMDGPU PRO driver is available as [amdgpu-pro](https://aur.archlinux.org/packages/amdgpu-pro/) in [AUR](/index.php/AUR "AUR").

## Loading

The `amdgpu` kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure to [#Enable Southern Islands (SI) and Sea Islands (CIK) support](#Enable_Southern_Islands_.28SI.29_and_Sea_Islands_.28CIK.29_support) when needed.
*   Make sure you have the latest [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package installed. This driver requires the latest firmware for each model to successfully boot.
*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since `amdgpu` requires [KMS](/index.php/KMS "KMS").
*   Check that you have not disabled `amdgpu` by using any [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

### Enable early KMS

**Tip:** If you have problems with the resolution, [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") may help.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by the amdgpu driver, is mandatory and enabled by default.

KMS is typically initialized after the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process"). It is possible, however, to enable KMS during the initramfs stage. To do this, add the `amdgpu` module to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES=(amdgpu radeon)

```

Now, regenerate the initramfs:

```
# mkinitcpio -p linux

```

The change takes effect at the next reboot.

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

Using this section, you can enable features and tweak the driver settings.

## Performance tuning

### Enabling video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

### Driver options

The following options apply to `/etc/X11/xorg.conf.d/**20-amdgpu.conf**`.

Please read [amdgpu(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/amdgpu.4) first before setting driver options.

**DRI** sets the maximum level of DRI to enable. Valid values are *2* for DRI2 or *3* for DRI3\. The default is *3* for DRI3 if the Xorg version is >= 1.18.3, otherwise DRI2 is used:

```
Option "DRI" "3" 

```

**TearFree** controls tearing prevention using the hardware page flipping mechanism. If this option is set, the default value of the property is set to *auto*, which means that TearFree is on for outputs with rotation or other RandR transforms:

```
Option "TearFree" "true"

```

## Enable GPU display scaling

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

[Dynamic power management](/index.php/ATI#dynamic_power_management "ATI") may cause screen artifacts to appear when displaying to monitors at higher frequencies (120+Hz) due to issues in the way GPU clock speeds are managed[[2]](https://bugs.freedesktop.org/show_bug.cgi?id=96868)[[3]](https://bugs.freedesktop.org/show_bug.cgi?id=102646).

A workaround is to force the GPU to a fixed performance level:

```
# echo high > /sys/class/drm/card0/device/power_dpm_force_performance_level

```

The available options for performance levels are:

*   `auto` automatic switching between performance levels (default)
*   `low` lowest performance level
*   `high` highest performance level

The workaround above is only temporary. It can be made persistent by creating a [udev](/index.php/Udev "Udev") rule:

 `/etc/udev/rules.d/30-amdgpu-pm.rules` 
```
KERNEL=="card0", SUBSYSTEM=="drm", DRIVERS=="amdgpu", ATTR{device/power_dpm_force_performance_level}="high"

```

There is also a GUI solution [[4]](https://github.com/marazmista/radeon-profile) where you can manage the "power_dpm" with [radeon-profile-git](https://aur.archlinux.org/packages/radeon-profile-git/) and [radeon-profile-daemon-git](https://aur.archlinux.org/packages/radeon-profile-daemon-git/).

### Screen flickering

If you experience flickering [[5]](https://bugzilla.kernel.org/show_bug.cgi?id=199101) add `amdgpu.dc=0` to your kernel parameters.

### R9 390 series Poor Performance and/or Instability

If you experience issues [[6]](https://bugs.freedesktop.org/show_bug.cgi?id=91880) with a AMD R9 390 series graphics card, set `radeon.cik_support=0 amdgpu.cik_support=1 amdgpu.dpm=1 amdgpu.dc=1` as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to force DPM support.

### Freezes with "[drm] IP block:gmc_v8_0 is hung!" kernel error

If you experience freezes and kernel crashes during a GPU intensive task with the kernel error " [drm] IP block:gmc_v8_0 is hung!" [[7]](https://bugs.freedesktop.org/show_bug.cgi?id=102322), a workaround is to set `amggpu.vm_update_mode=3` as [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to force the GPUVM page tables update to be done using the CPU. Downsides are listed here [[8]](https://bugs.freedesktop.org/show_bug.cgi?id=102322#c15).