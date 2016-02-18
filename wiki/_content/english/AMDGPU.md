**amdgpu** is the open source graphics driver for the latest AMD Radeon graphics cards.

At the moment there is only support for the [Volcanic Islands](http://xorg.freedesktop.org/wiki/RadeonFeature/) and some cards of the [Sea Islands](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) family. AMD has yet to decide to add support for older cards in the near future.

Owners of unsupported AMD/ATI video cards can use the [Radeon open source](/index.php/ATI "ATI") or [AMD's proprietary](/index.php/AMD_Catalyst "AMD Catalyst") driver instead.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Loading](#Loading)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Performance tuning](#Performance_tuning)
    *   [4.1 Enabling video acceleration](#Enabling_video_acceleration)
*   [5 Enable amdgpu for Sea Islands Cards](#Enable_amdgpu_for_Sea_Islands_Cards)

## Installation

**Note:** If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.

[Install](/index.php/Install "Install") the [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package. It provides the DDX driver for 2D acceleration and it pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency, providing the DRI driver for 3D acceleration.

To enable OpenGL support, also install [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl). If you are on x86_64 and need 32-bit support, also install [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl) from the [multilib](/index.php/Multilib "Multilib") repository.

Support for [accelerated video decoding](#Enabling_video_acceleration) is provided by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages.

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

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is supported by the radeon driver and is mandatory and enabled by default.

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

[VA-API](/index.php/VA-API "VA-API") and [VDPAU](/index.php/VDPAU "VDPAU") can be installed to provide hardware accelerated video encoding and decoding.

## Enable amdgpu for Sea Islands Cards

`amdgpu` has experimental support for Sea Islands (CI) cards, which is disabled by default. One possible reason why you might want to enable it and switch from radeon to `amdgpu` is that AMD announced their user space [Vulkan](https://www.khronos.org/vulkan/) driver will only be supporting the new `amdgpu` stack [[1]](https://phoronix.com/scan.php?page=news_item&px=AMDGPU-Vulkan-Driver-Only). Same might be the case for the new OpenCL driver, which was also mentioned in the [XDC presentation](http://www.x.org/wiki/Events/XDC2015/Program/deucher_zhou_amdgpu.pdf). If you want to enable `amdgpu` and use it with your Sea Islands product, you have to recompile your kernel. Probably the easiest way to setup a custom kernel is using the ABS, described in the article [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System"). Set "Enable amdgpu support for CIK parts" to "yes", then compile and install your kernel.

```
CONFIG_DRM_AMDGPU_CIK=Y

```

To prevent `radeon` from loading, you can disable it in the Kconfig or [blacklist](https://wiki.archlinux.org/index.php/Kernel_modules#Blacklisting) the `radeon` module.

 `/etc/modprobe.d/radeon.conf`  `blacklist radeon` 

It may also be needed to use the `amdgpu.exp_hw_support=1` [[2]](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-Iceland-Experimental) as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or by setting the [kernel module](/index.php/Kernel_modules#Using_files_in_.2Fetc.2Fmodprobe.d.2F "Kernel modules") options.