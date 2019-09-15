Related articles

*   [Improving performance](/index.php/Improving_performance "Improving performance")
*   [Improving performance/Boot process](/index.php/Improving_performance/Boot_process "Improving performance/Boot process")
*   [Kernel](/index.php/Kernel "Kernel")
*   [Microcode](/index.php/Microcode "Microcode")

Ryzen is a multithreaded, high performance processor released by AMD in Q1, 2017\. It is the first CPU released based on the [Zen microarchitecture](https://en.wikipedia.org/wiki/Zen_(microarchitecture) "wikipedia:Zen (microarchitecture)"). Its goal is to directly compete with Intel's Broadwell-E processor line, primarily the Core i7-6900K.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Kernels](#Kernels)
    *   [1.2 Graphics Drivers](#Graphics_Drivers)
    *   [1.3 Enable Microcode Support](#Enable_Microcode_Support)
*   [2 Tweaking Ryzen](#Tweaking_Ryzen)
    *   [2.1 Power Managing](#Power_Managing)
    *   [2.2 Overclocking](#Overclocking)
*   [3 Improving Ryzen](#Improving_Ryzen)
    *   [3.1 Enabling The Ananicy Daemon](#Enabling_The_Ananicy_Daemon)
    *   [3.2 Irqbalance](#Irqbalance)
    *   [3.3 CPU Mitigations](#CPU_Mitigations)
    *   [3.4 Gaming Performance](#Gaming_Performance)
*   [4 Compiling A Kernel](#Compiling_A_Kernel)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Screen-Tearing (APU)](#Screen-Tearing_(APU))
*   [6 See also](#See_also)

## Installation

### Kernels

*   [Install](/index.php/Install "Install") the [linux-zen](https://www.archlinux.org/packages/?name=linux-zen) kernel for more optimisation. Linux ZEN provides better stability for any processors and also provides more speed in general (including gaming). It is **only** recommended for **desktop** users because the ZEN kernel uses as much power as the default kernel.
*   [Install](/index.php/Install "Install") the [linux-ck](https://aur.archlinux.org/packages/linux-ck/) kernel which contains patches that is designed to improve system responsiveness with specific emphasis on the desktop, but suitable to any workload. The CK kernel is recommended for **laptop** users as it's intended to be very power efficient.

**Warning:** [linux-ck](https://aur.archlinux.org/packages/linux-ck/) is not officially supported for Arch Linux and its derivatives. You may experience some issues.

Reconfigure GRUB to use the kernel(s) you have installed so you can boot into it/them next time. If you do not use GRUB, you will have to create a configuration file to use the kernel(s) for your bootloader.

**Note:** For more information about kernels, head on over the [Kernel](/index.php/Kernel "Kernel") page.

**Tip:** Have the [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) package as a backup kernel in case a kernel upgrade breaks your system.

### Graphics Drivers

[Install](/index.php/Install "Install") the [mesa](https://www.archlinux.org/packages/?name=mesa) package which provides the [DRI](https://en.wikipedia.org/wiki/Direct_Rendering_Infrastructure "wikipedia:Direct Rendering Infrastructure") driver for 3D acceleration (only for Ryzen APUs and/or AMD GPUs).

### Enable Microcode Support

[Install](/index.php/Install "Install") the [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) package to enable microcode updates and enable it with the help of the [Microcode](/index.php/Microcode "Microcode") page. These updates provide bug fixes that can be critical to the stability of your system. It is **highly recommended** to use it despite it being proprietary.

## Tweaking Ryzen

### Power Managing

[RyzenAdj](https://github.com/FlyGoat/RyzenAdj) (CLI) is a tool created by [FlyGoat](https://github.com/FlyGoat) to adjust power management settings for Ryzen processors using a terminal emulator.

**Tip:** You can use [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) to monitor the temperature of your processor.

### Overclocking

[ZenStates-Linux](https://github.com/r4m0n/ZenStates-Linux/) (CLI) is a tool made by [r4m0n](https://github.com/r4m0n) to adjust the clock speed and voltage. A detailed example was given in [Level1Techs](https://forum.level1techs.com/t/overclock-your-ryzen-cpu-from-linux/126025)' forums by *catsay* for you to understand it.

## Improving Ryzen

### Enabling The Ananicy Daemon

See [Improving performance#Ananicy](/index.php/Improving_performance#Ananicy "Improving performance").

### Irqbalance

See [Improving performance#irqbalance](/index.php/Improving_performance#irqbalance "Improving performance").

### CPU Mitigations

See [Improving performance#Turn off CPU exploit mitigations](/index.php/Improving_performance#Turn_off_CPU_exploit_mitigations "Improving performance").

### Gaming Performance

See [Gaming#Improving performance](/index.php/Gaming#Improving_performance "Gaming").

## Compiling A Kernel

See [Gentoo:Ryzen#Kernel](https://wiki.gentoo.org/wiki/Ryzen#Kernel "gentoo:Ryzen") on enabling Ryzen support.

## Troubleshooting

### Screen-Tearing (APU)

If you are using [Xorg](/index.php/Xorg "Xorg") and are experiencing screen-tearing, enabling the `"TearFree"` option will fix the problem.

 `/etc/X11/xorg.conf.d/20-amdgpu.conf` 
```
Section "Device"
     Identifier  "AMD"
     Driver "amdgpu"
     Option "TearFree" "true"
  EndSection

```

**Note:** `"TearFree"` is **not** Vsync.

## See also

*   [Gentoo:Ryzen](https://wiki.gentoo.org/wiki/Ryzen "gentoo:Ryzen")