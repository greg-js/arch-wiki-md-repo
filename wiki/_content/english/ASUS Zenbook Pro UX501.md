This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the ASUS Zenbook Pro UX501\.

For general instructions see [Laptop](/index.php/Laptop "Laptop") and comparable models from the summary page [Laptop/ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") and [Category:ASUS](/index.php/Category:ASUS "Category:ASUS").

## Contents

*   [1 Kernel Options](#Kernel_Options)
*   [2 Microcode](#Microcode)
*   [3 Module Configuration](#Module_Configuration)
*   [4 Touch Pad](#Touch_Pad)
*   [5 Fan Control](#Fan_Control)
*   [6 Virtual Terminal Fonts](#Virtual_Terminal_Fonts)
*   [7 Headphones not detected](#Headphones_not_detected)
*   [8 See also](#See_also)

## Kernel Options

To prevent random lock ups just before or as X loads, add the following option to your boot loader config:

```
i915.enable_execlists=0

```

To get brightness media keys and brightness adjustment working, add the following:

```
acpi_osi= acpi_backlight=native

```

To allow X to start without locking up when the GPU is powered down via bbswitch, replace the acpi_osi= above with:

```
acpi_osi=! acpi_osi="Windows 2009"

```

## Microcode

Be sure to load the latest [microcode](/index.php/Microcode "Microcode") alongside your kernel to prevent random lock ups while using the modesetting driver.

## Module Configuration

Before trying out the fixed below make sure you system is completely up to date by [updating your system](/index.php/Pacman#Upgrading_packages "Pacman").

To fix noise headphone noise create `/etc/modprobe.d/alsa-base.conf` containing:

```
options snd-hda-intel model=dell-headset-multi

```

Restoring the laptop from suspend will bring the noise back. In order to fix this use [https://github.com/dakatapetrov/zenbook-pro-ux501vw-sound-fix](https://github.com/dakatapetrov/zenbook-pro-ux501vw-sound-fix).

To enable power-saving functionality for the Intel graphics card create `/etc/modprobe.d/i915.conf` containing:

```
options i915 enable_rc6=1 enable_fbc=1 lvds_downclock=1 semaphores=1

```

But be careful with `/etc/modprobe.d/i915.conf`. It may cause screen freezing.

## Touch Pad

The touch pad will work with the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package.

**The below is only necessary with kernels older than 4.10, as it has been included in the base version of the kernel.**

Multi-gesture can be activated downloading this git project [Asus HID DKMS](https://github.com/vlasenko/hid-asus-dkms) and executing the following script:

```
./dkms-add.sh

```

It will build and load immediately the touch pad driver kernel module and will add it persistently to load it during boot.

Notice: You must have installed before the packages `dkms` and `linux-headers`

## Fan Control

To setup variable fan control, install the [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) package and load the `coretemp` module at boot by creating `/etc/modules-load.d/lm_sensors.conf` containing:

```
coretemp

```

## Virtual Terminal Fonts

The 4K resolution causes the default virtual terminal font to be extremely small, and the loss of detail caused by the fact that the UX501 uses a false-4K Pentile display instead of a true-4K display can make it even more difficult to read. One way to resolve this is to install the [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) package and then create `/etc/vconsole.conf` containing:

```
FONT=ter-v28b

```

## Headphones not detected

To attempt to scan for your headphones again run:

```
alsactl restore

```

## See also

*   **[Bumblebee](/index.php/Bumblebee "Bumblebee")** - To configure intel/nvidia hybrid graphics
*   **[iwlwifi issue](https://bbs.archlinux.org/viewtopic.php?id=213363)** - if you have [*** ] A start job is running for wlp3s0 (14 s / 1min 30s).
*   **[cheat sheet](https://github.com/nicholasglazer/arch-cheat-sheet)** - Arch guide did with this laptop model