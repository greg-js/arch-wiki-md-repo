This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the ASUS Zenbook Pro UX501\.

For general instructions see [Laptop](/index.php/Laptop "Laptop") and comparable models from the summary page [Laptop/Asus](/index.php/Laptop/Asus "Laptop/Asus") and [Category:ASUS](/index.php/Category:ASUS "Category:ASUS").

## Contents

*   [1 Kernel Options](#Kernel_Options)
*   [2 Module Configuration](#Module_Configuration)
*   [3 Touch Pad](#Touch_Pad)
*   [4 Fan Control](#Fan_Control)
*   [5 Virtual Terminal Fonts](#Virtual_Terminal_Fonts)
*   [6 See also](#See_also)

## Kernel Options

To prevent random lock ups just before or as X loads, add the following option to your boot loader config:

```
i915.enable_execlists=0

```

To get brightness media keys and brightness adjustment working, add the following:

```
acpi_osi= acpi_backlight=native

```

## Module Configuration

Warning: Before trying out below fixes run pacman -Syu

To fix noise headphone noise create `/etc/modprobe.d/alsa-base.conf` containing:

```
options snd-hda-intel model=dell-headset-multi

```

To enable power saving functionality for the audio card create `/etc/modprobe.d/audio_powersave.conf` containing:

```
options snd_hda_intel power_save=1

```

To enable power-saving functionality for the Intel graphics card create `/etc/modprobe.d/i915.conf` containing:

```
options i915 enable_rc6=1 enable_fbc=1 lvds_downclock=1 semaphores=1

```

## Touch Pad

The touch pad will work with the [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) package.

## Fan Control

To setup variable fan control, install the [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) package and load the `coretemp` module at boot by creating `/etc/modules-load.d/lm_sensors.conf` containing:

```
coretemp

```

## Virtual Terminal Fonts

The 4k resolution causes the default virtual terminal font to be extremely small, one way to resolve this is to install the [terminus-font](https://www.archlinux.org/packages/?name=terminus-font) package and then creating `/etc/vconsole.conf` containing:

```
FONT=ter-v28b

```

## See also

*   **[Bumblebee](/index.php/Bumblebee "Bumblebee")** - To configure intel/nvidia hybrid graphics