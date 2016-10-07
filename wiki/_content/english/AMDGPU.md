**amdgpu** is the open source graphics driver for the latest AMD Radeon graphics cards.

At the moment there is support for the [Volcanic Islands](http://xorg.freedesktop.org/wiki/RadeonFeature/), some cards of the [Sea Islands](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) family and the [Southern Islands](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-SI-Experimental-Code) family (more experimental than Sea Islands and coming only in Linux 4.9). AMD has absolutely no plans for supporting the pre-GCN GPUs.

Owners of unsupported AMD/ATI video cards can use the [Radeon open source](/index.php/ATI "ATI") or [AMD's proprietary](/index.php/AMD_Catalyst "AMD Catalyst") driver instead.

## Contents

*   [1 Selecting the right driver](#Selecting_the_right_driver)
*   [2 Installation](#Installation)
    *   [2.1 AMDGPU PRO](#AMDGPU_PRO)
*   [3 Configuration](#Configuration)
*   [4 Loading](#Loading)
    *   [4.1 Enable early KMS](#Enable_early_KMS)
*   [5 Performance tuning](#Performance_tuning)
    *   [5.1 Enabling video acceleration](#Enabling_video_acceleration)
*   [6 Enable amdgpu for Sea Islands or Southern Islands cards](#Enable_amdgpu_for_Sea_Islands_or_Southern_Islands_cards)
*   [7 Disable radeon driver](#Disable_radeon_driver)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Xorg or applications won't start](#Xorg_or_applications_won.27t_start)

## Selecting the right driver

Depending on the card you have, find the right driver in [Xorg#ATI](/index.php/Xorg#ATI "Xorg"). This page has instructions for **AMDGPU** and **AMDGPU PRO**.

## Installation

**Note:** If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.

[Install](/index.php/Install "Install") the [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package. It provides the DDX driver for 2D acceleration and it pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency, providing the DRI driver for 3D acceleration.

To enable OpenGL support, also install [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl). If you are on x86_64 and need 32-bit support, also install [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) from the [multilib](/index.php/Multilib "Multilib") repository.

Support for [accelerated video decoding](#Enabling_video_acceleration) is provided by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages.

**Note:** The [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package is only used for Xorg acceleration and not strictly required.

### AMDGPU PRO

**Warning:** AMDGPU PRO is still in beta. Arch Linux is not officially supported.

AMD provides a proprietary, binary userland driver called *AMDGPU PRO*, which works on top of the open-source AMDGPU kernel driver. This hybrid approach allows the in-kernel component to be recompiled by the Arch Linux maintainers when required (e.g. on a kernel or Xorg update), while keeping the same binary userspace part. This should remedy the problem where the driver provided by AMD is out of date and incompatible with newer kernels or Xorg versions (a problem that was very common with the old [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") driver). For an detailed overview of the hybrid system, see [this article](http://www.phoronix.com/scan.php?page=news_item&px=MTgwODA).

The AMDGPU PRO driver provides OpenGL, OpenCL, Vulkan and VDPAU support. It aims to provide better performance than the open-source driver.

See the [release notes](http://support.amd.com/en-us/kb-articles/Pages/AMD-Radeon-GPU-PRO-Linux-Beta-Driver%E2%80%93Release-Notes.aspx) and the [announcement at the Phoronix forum](https://www.phoronix.com/forums/forum/linux-graphics-x-org-drivers/amd-linux/855699-amd-representative-says-their-vulkan-linux-driver-will-be-here-soon/page6) for more information.

There are packages for the amdgpu-pro components in the [AUR](/index.php/AUR "AUR") ([amdgpu-pro](https://aur.archlinux.org/packages/amdgpu-pro/)), visit [https://github.com/Corngood/archlinux-amdgpu](https://github.com/Corngood/archlinux-amdgpu) for issues or pull requests.

## Configuration

Xorg will automatically load the driver and it will use your monitor's EDID to set the native resolution. Configuration is only required for tuning the driver.

If you want manual configuration, create `/etc/X11/xorg.conf.d/20-amdgpu.conf`, and add the following:

```
Section "Device"
    Identifier "AMD"
    Driver "amdgpu"
EndSection

```

Using this section, you can enable features and tweak the driver settings.

## Loading

The `amdgpu` kernel module should load fine automatically on system boot.

If it does not happen, then:

*   Make sure you have the latest [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package installed. This driver requires the latest firmware for each model to successfully boot.
*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since `amdgpu` requires [KMS](/index.php/KMS "KMS").
*   Also, check that you have not disabled `amdgpu` by using any [kernel module blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules").

### Enable early KMS

**Tip:** If you have problems with the resolution, [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting") may help.

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by the amdgpu driver and is mandatory and enabled by default.

KMS is typically initialized after the [initramfs stage](/index.php/Arch_boot_process#initramfs "Arch boot process"). It is possible, however, to enable KMS during the initramfs stage. To do this, add the `amdgpu` module to the `MODULES` line in `/etc/mkinitcpio.conf`:

```
MODULES="... amdgpu ..."

```

Now, regenerate the initramfs:

```
# mkinitcpio -p linux

```

The change takes effect at the next reboot.

## Performance tuning

### Enabling video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

## Enable amdgpu for Sea Islands or Southern Islands cards

`amdgpu` has experimental support for Sea Islands (CIK) and Southern Islands (SI; since Linux 4.9) cards, which is disabled by default. One possible reason why you might want to enable it and switch from radeon to `amdgpu` is that AMD announced their user space [Vulkan](https://www.khronos.org/vulkan/) driver will only be supporting the new `amdgpu` stack [[1]](https://phoronix.com/scan.php?page=news_item&px=AMDGPU-Vulkan-Driver-Only). Same might be the case for the new OpenCL driver, which was also mentioned in the [XDC presentation](http://www.x.org/wiki/Events/XDC2015/Program/deucher_zhou_amdgpu.pdf).

If you want to enable `amdgpu` and use it with your Sea Islands or Southern Islands product, you have to recompile your kernel. Probably the easiest way to setup a custom kernel is using the ABS, described in [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). You can also uncomment `make menuconfig` or `make nconfig` in the PKGBUILD, which will allow you to verify that the CIK option is selected by following the instructions from [Gentoo wiki](https://wiki.gentoo.org/wiki/Amdgpu#Feature_support).

For Sea Islands (CIK), set "Enable amdgpu support for CIK parts" to "yes", then compile and install your kernel.

```
CONFIG_DRM_AMDGPU_CIK=Y

```

For Southern Islands (SI; since Linux 4.9), set "Enable amdgpu support for SI parts" to "yes", then compile and install your kernel.

```
CONFIG_DRM_AMDGPU_SI=Y

```

It may also be needed to use the `amdgpu.exp_hw_support=1` [[2]](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-Iceland-Experimental) as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or by setting the [kernel module](/index.php/Kernel_modules#Using_files_in_.2Fetc.2Fmodprobe.d.2F "Kernel modules") options.

## Disable radeon driver

To prevent `radeon` from loading, you can disable it in the Kconfig or [blacklist](/index.php/Blacklist "Blacklist") the `radeon` module.

 `/etc/modprobe.d/radeon.conf`  `blacklist radeon` 

## Troubleshooting

### Xorg or applications won't start

*   "(EE) AMDGPU(0): [DRI2] DRI2SwapBuffers: drawable has no back or front?" error after opening glxgears, can open Xorg server but OpenGL apps crash.
*   "(EE) AMDGPU(0): Given depth (32) is not supported by amdgpu driver" error, Xorg won't start.

Setting the screen's depth under Xorg to 16 or 32 will cause problems/crash. To avoid that, you should use a standard screen depth of 24 by adding this to your "screen" section (assuming you have one, assuming you don't add this to `/etc/X11/xorg.conf.d/10-screen.conf`).

```
Section "Screen"
       DefaultDepth    24
       SubSection      "Display"
               Depth   24
       EndSubSection
EndSection

```