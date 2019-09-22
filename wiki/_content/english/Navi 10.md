Related articles

*   [AMDGPU](/index.php/AMDGPU "AMDGPU")
*   [Xorg](/index.php/Xorg "Xorg")
*   [Vulkan](/index.php/Vulkan "Vulkan")
*   [Wayland](/index.php/Wayland "Wayland")

**Navi 10** is the GPU architecture featured in AMD's [Radeon RX 5000 series](https://en.wikipedia.org/wiki/AMD_Radeon_5000_series). Since it's very new hardware, software support for it is not yet completely ready. This page will lay out the procedure to make Navi 10 based GPUs work under Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Firmware](#Firmware)
    *   [1.3 Mesa](#Mesa)
    *   [1.4 LLVM](#LLVM)
    *   [1.5 AMDGPU PRO](#AMDGPU_PRO)
*   [2 Loading and Early KMS](#Loading_and_Early_KMS)
*   [3 Xorg configuration, Tear Free Rendering, DRI Level and Variable refresh rate](#Xorg_configuration,_Tear_Free_Rendering,_DRI_Level_and_Variable_refresh_rate)
*   [4 Video acceleration](#Video_acceleration)
*   [5 GPGPU](#GPGPU)
*   [6 Overclocking](#Overclocking)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 General](#General)

## Installation

### Kernel

Navi 10 GPUs require version 5.3 or newer of the Linux kernel. The Linux kernel 5.3 is already available in the **core** repository of Arch Linux. Make sure to use the [linux](https://www.archlinux.org/packages/?name=linux) and [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) packages to get the latest version.

You can check your current kernel version by running the following command:

```
uname -r

```

Another way to get Navi 10 support in older kernel versions is to install [amdgpu-dkms](https://aur.archlinux.org/packages/amdgpu-dkms/). Be warned that this is not officially supported.

### Firmware

> Linux firmware is a package distributed alongside the Linux kernel that containes firmware binary blobs necessary for partial or full functionality of certain hardware devices. These binary blobs are usually proprietary because some hardware manufacturers do not release source code necessary to build the firmware itself.
> 
> [Gentoo Wiki](https://wiki.gentoo.org/wiki/Linux_firmware)

While most of the blobs required by standard hardware are available in the [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) package, the blobs needed for Navi 10 GPUs aren't. You can get these blobs by installing the [linux-firmware-agd5f-radeon-navi10](https://aur.archlinux.org/packages/linux-firmware-agd5f-radeon-navi10/) package.

If you have a new enough kernel, but do not have sufficient firmware files, then you may need to boot with the `nomodeset` kernel option in order to have a working virtual console.

### Mesa

Support for Navi 10 GPUs isn't yet available in the standard repositories. You will need the development version of mesa and its related packages. To get them, you can add the `mesa-git` repository to your system. To do that, add the following lines to `/etc/pacman.conf` just above the `[core]` section:

 `/etc/pacman.conf` 
```
[mesa-git]
Server = https://pkgbuild.com/~lcarlier/$repo/$arch
SigLevel = Optional

```

Then update your system and install the following packages, replacing anything it prompts to:

```
amdvlk clang-git libclc-git libdrm-git llvm-git llvm-libs-git mesa-git opencl-mesa-git vulkan-mesa-layer-git vulkan-radeon-git xf86-video-amdgpu-git lib32-mesa-git lib32-mesa-git lib32-vulkan-radeon-git lib32-vulkan-mesa-layer-git

```

These packages will provide support for the latest mesa stack, as well as support for [Vulkan](/index.php/Vulkan "Vulkan"), for both 64 bit and 32 bit applications.

### LLVM

You need LLVM 9.0 or newer: [[1]](https://releases.llvm.org/9.0.0/docs/ReleaseNotes.html#changes-to-the-amdgpu-target)

This should be selected as a dependency for [mesa](https://www.archlinux.org/packages/?name=mesa) / [mesa-git](https://aur.archlinux.org/packages/mesa-git/) above, either provided by the [llvm-git](https://aur.archlinux.org/packages/llvm-git/) family of packages, or via [llvm](https://www.archlinux.org/packages/?name=llvm) when 9.0 is considered stable by its archlinux maintainer

### AMDGPU PRO

Using AMDGPU PRO is not recommended. If you're still interested, see [AMDGPU#AMDGPU PRO](/index.php/AMDGPU#AMDGPU_PRO "AMDGPU").

## Loading and Early KMS

See [AMDGPU#Loading](/index.php/AMDGPU#Loading "AMDGPU").

## Xorg configuration, Tear Free Rendering, DRI Level and Variable refresh rate

See [AMDGPU#Xorg configuration](/index.php/AMDGPU#Xorg_configuration "AMDGPU")

## Video acceleration

See [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

## GPGPU

As of writing this, I wasn't able to make OpenCL work with either Clover, nor AMDGPU-PRO. For more info on GPGPU, see [GPGPU](/index.php/GPGPU "GPGPU").

## Overclocking

See [AMDGPU#Overclocking](/index.php/AMDGPU#Overclocking "AMDGPU")

## Troubleshooting

### General

See [AMDGPU#Troubleshooting](/index.php/AMDGPU#Troubleshooting "AMDGPU").