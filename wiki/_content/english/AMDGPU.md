Related articles

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst")
*   [ATI](/index.php/ATI "ATI")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Vulkan](/index.php/Vulkan "Vulkan")

**amdgpu** is the open source graphics driver for the latest AMD Radeon graphics cards.

At the moment there is support for [Volcanic Islands (VI)](https://www.x.org/wiki/RadeonFeature/) and experimental support for [Sea Islands (CI)](https://www.phoronix.com/scan.php?page=news_item&px=AMD-AMDGPU-Released) and [Southern Islands (SI)](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-SI-Experimental-Code) cards. AMD has absolutely no plans for supporting the pre-GCN GPUs.

Owners of unsupported AMD/ATI video cards may use the [Radeon open source](/index.php/ATI "ATI") or [AMD's proprietary](/index.php/AMD_Catalyst "AMD Catalyst") driver instead.

## Contents

*   [1 Selecting the right driver](#Selecting_the_right_driver)
*   [2 Installation](#Installation)
    *   [2.1 Enable Southern Islands (SI) and Sea Islands (CIK) support](#Enable_Southern_Islands_.28SI.29_and_Sea_Islands_.28CIK.29_support)
    *   [2.2 AMDGPU PRO](#AMDGPU_PRO)
*   [3 Loading](#Loading)
    *   [3.1 Enable early KMS](#Enable_early_KMS)
*   [4 Xorg configuration](#Xorg_configuration)
*   [5 Performance tuning](#Performance_tuning)
    *   [5.1 Enabling video acceleration](#Enabling_video_acceleration)
    *   [5.2 Driver options](#Driver_options)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 No HDMI/DP Audio](#No_HDMI.2FDP_Audio)
    *   [6.2 Incorrect screen position on HDMI](#Incorrect_screen_position_on_HDMI)
    *   [6.3 Xorg or applications won't start](#Xorg_or_applications_won.27t_start)
    *   [6.4 Screen artifacts and frequency problem](#Screen_artifacts_and_frequency_problem)

## Selecting the right driver

Depending on the card you have, find the right driver in [Xorg#AMD](/index.php/Xorg#AMD "Xorg"). This page has instructions for **AMDGPU** and **AMDGPU PRO**.

## Installation

**Note:**

*   If coming from the proprietary Catalyst driver, see [AMD Catalyst#Uninstallation](/index.php/AMD_Catalyst#Uninstallation "AMD Catalyst") first.
*   The [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package is only used for [Xorg](/index.php/Xorg "Xorg") acceleration and not strictly required.

[Install](/index.php/Install "Install") the [xf86-video-amdgpu](https://www.archlinux.org/packages/?name=xf86-video-amdgpu) package. It provides the DDX driver for 2D acceleration and it pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency, providing the DRI driver for 3D acceleration.

For 32-bit application support on x86_64, also install [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) from [multilib](/index.php/Multilib "Multilib").

Support for [accelerated video decoding](#Enabling_video_acceleration) is provided by [mesa-vdpau](https://www.archlinux.org/packages/?name=mesa-vdpau) and [lib32-mesa-vdpau](https://www.archlinux.org/packages/?name=lib32-mesa-vdpau) packages.

### Enable Southern Islands (SI) and Sea Islands (CIK) support

The [linux](https://www.archlinux.org/packages/?name=linux) package enables AMDGPU support for cards of the Southern Islands (SI) and Sea Islands (CIK). When building or compiling a [kernel](/index.php/Kernel "Kernel"), `CONFIG_DRM_AMDGPU_SI=Y` and/or `CONFIG_DRM_AMDGPU_CIK=Y` should be be set in the config.

Even when AMDGPU support for SI/CIK has been enabled by the kernel, the [radeon](/index.php/Radeon "Radeon") driver may be used instead of the AMDGPU driver.

The following workarounds are available:

*   Set `amdgpu` as first to load in the [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") array, e.g. `MODULES="amdgpu radeon"`.
*   [Blacklist](/index.php/Blacklist "Blacklist") the `radeon` module.

Also, since kernel 4.13, adding the `amdgpu.si_support=1` or `amdgpu.cik_support=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") is [required](http://www.phoronix.com/scan.php?page=article&item=linux-413-gcn101&num=1). Otherwise, AMDGPU will not start and you will end up with either radeon being used instead or the display being frozen during the boot.

### AMDGPU PRO

**Warning:** Arch Linux is officially not supported.

**Note:**

*   To use the proprietary OpenCL component without AMDGPU PRO, [install](/index.php/Install "Install") [opencl-amd](https://aur.archlinux.org/packages/opencl-amd/) instead.
*   A [downgrade](/index.php/Downgrade "Downgrade") of the [linux](https://www.archlinux.org/packages/?name=linux) (4.8 or 4.9) and [Xorg](/index.php/Xorg "Xorg") (1.18) packages may be required to use AMDGPU PRO.

AMD provides a proprietary, binary userland driver called *AMDGPU PRO*, which works on top of the open-source AMDGPU kernel driver. The driver provides OpenGL, [OpenCL](/index.php/OpenCL "OpenCL"), [Vulkan](/index.php/Vulkan "Vulkan") and [VDPAU](/index.php/VDPAU "VDPAU") support (although this is also supported by the open-source driver). For some workloads it provides better performance than the open-source driver ([example benchmark](https://www.phoronix.com/scan.php?page=news_item&px=AMDGPU-PRO-16.40-Deus-MD)), while for others it is true the contrary ([example benchmark](https://openbenchmarking.org/prospect/1610315-TA-AMDGPUPRO08/998ba9b677230564e0fbca342a8e1b9a7e85b6ab)).

See the [release notes](https://support.amd.com/en-us/kb-articles/Pages/AMDGPU-PRO-Driver-for-Linux-Release-Notes.aspx) and the [announcement at the Phoronix forum](https://www.phoronix.com/forums/forum/linux-graphics-x-org-drivers/amd-linux/855699-amd-representative-says-their-vulkan-linux-driver-will-be-here-soon/page6) for more information.

A patched version of the official AMDGPU PRO driver is available as [amdgpu-pro](https://aur.archlinux.org/packages/amdgpu-pro/) in [AUR](/index.php/AUR "AUR").

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

## Xorg configuration

Xorg will automatically load the driver and it will use your monitor's EDID to set the native resolution. Configuration is only required for tuning the driver.

If you want manual configuration, create `/etc/X11/xorg.conf.d/20-amdgpu.conf`, and add the following:

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

Please read [amdgpu(4)](http://jlk.fjfi.cvut.cz/arch/manpages/man/amdgpu.4) first before setting driver options.

**DRI** sets the maximum level of DRI to enable. Valid values are *2* for DRI2 or *3* for DRI3\. The default is *3* for DRI3 if the Xorg version is >= 1.18.3, otherwise DRI2 is used:

```
Option "DRI" "3" 

```

**TearFree** controls tearing prevention using the hardware page flipping mechanism. If this option is set, the default value of the property is set to *auto*, which means that TearFree is on for outputs with rotation or other RandR transforms:

```
Option "TearFree" "true"

```

## Troubleshooting

### No HDMI/DP Audio

The open source AMDGPU driver relies on the DAL code that [currently being worked on](https://cgit.freedesktop.org/~agd5f/linux/log/?h=drm-next-4.7-wip-dal). Until DAL is mainlined, audio suppport for HDMI and DisplayPort will not be available. The only current way to get HDMI and DisplayPort audio is to install the [#AMDGPU PRO](#AMDGPU_PRO) driver.

### Incorrect screen position on HDMI

Use `amdgpu.audio=0` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to prevent the (incomplete) HDMI audio-support from being enabled [[1]](https://bugzilla.kernel.org/show_bug.cgi?id=195737).

### Xorg or applications won't start

*   "(EE) AMDGPU(0): [DRI2] DRI2SwapBuffers: drawable has no back or front?" error after opening glxgears, can open Xorg server but OpenGL apps crash.
*   "(EE) AMDGPU(0): Given depth (32) is not supported by amdgpu driver" error, Xorg won't start.

Setting the screen's depth under Xorg to 16 or 32 will cause problems/crash. To avoid that, you should use a standard screen depth of 24 by adding this to your "screen" section (assuming you have one, assuming you don't add this to `/etc/X11/xorg.conf.d/10-screen.conf`).

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

If you have screen artifacts when setting your screen frequency up to 120+Hz your "Memory Clock" and "GPU Clock" are certainly too low to handle the screen request.

A workaround [[2]](https://bugs.freedesktop.org/show_bug.cgi?id=96868#c13) is saving `high` or `low` in `/sys/class/drm/card0/device/power_dpm_force_performance_level`.

There is a GUI solution [[3]](https://github.com/marazmista/radeon-profile) where you can manage the "power_dpm" with [radeon-profile-git](https://aur.archlinux.org/packages/radeon-profile-git/) and [radeon-profile-daemon-git](https://aur.archlinux.org/packages/radeon-profile-daemon-git/).