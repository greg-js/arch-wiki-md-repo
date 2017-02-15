This article covers the open-source [Nouveau](https://nouveau.freedesktop.org/) driver for NVIDIA graphics cards. For information about the proprietary driver, see [NVIDIA](/index.php/NVIDIA "NVIDIA").

Find your card's [code name](https://nouveau.freedesktop.org/wiki/CodeNames) (a more detailed list is available on [Wikipedia](https://en.wikipedia.org/wiki/Comparison_of_Nvidia_Graphics_Processing_Units "wikipedia:Comparison of Nvidia Graphics Processing Units")), and compare it with the [feature matrix](https://nouveau.freedesktop.org/wiki/FeatureMatrix/) for supported features.

## Contents

*   [1 Installation](#Installation)
*   [2 Loading](#Loading)
    *   [2.1 Enable early KMS](#Enable_early_KMS)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Keep NVIDIA driver installed](#Keep_NVIDIA_driver_installed)
    *   [3.2 Installing the latest development packages](#Installing_the_latest_development_packages)
    *   [3.3 Dual Head](#Dual_Head)
    *   [3.4 Setting console resolution](#Setting_console_resolution)
    *   [3.5 Power Management](#Power_Management)
        *   [3.5.1 Fan Control](#Fan_Control)
    *   [3.6 Optimus](#Optimus)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Disable MSI](#Disable_MSI)
    *   [4.2 Phantom Output Issue](#Phantom_Output_Issue)
    *   [4.3 Random lockups with kernel error messages](#Random_lockups_with_kernel_error_messages)

## Installation

[Install](/index.php/Install "Install") the [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) package. It provides the DDX driver for 2D acceleration in [Xorg](/index.php/Xorg "Xorg"), and pulls in [mesa](https://www.archlinux.org/packages/?name=mesa) as a dependency which provides the DRI driver for 3D acceleration.

For 32-bit application support on x86_64, also install [lib32-mesa](https://www.archlinux.org/packages/?name=lib32-mesa) from [multilib](/index.php/Multilib "Multilib").

For OpenGL support, also install [mesa-libgl](https://www.archlinux.org/packages/?name=mesa-libgl), and [lib32-mesa-libgl](https://www.archlinux.org/packages/?name=lib32-mesa-libgl).

## Loading

The Nouveau kernel module should load automatically on system boot. If it does not happen, then:

*   Make sure you do **not** have `nomodeset` or `vga=` as a [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"), since Nouveau requires kernel mode-setting.
*   Also, check that you do not have Nouveau disabled using any modprobe blacklisting technique within `/etc/modprobe.d/` or `/usr/lib/modprobe.d/`.
*   If all above still fails to load nouveau check dmesg for an opcode error. Add `nouveau.config=NvBios=PRAMIN` to your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to prevent module unloading.[[1]](https://nouveau.freedesktop.org/wiki/TroubleShooting/#index10h3)

### Enable early KMS

**Tip:** If you have problems with the resolution, check [Kernel mode setting#Forcing modes and EDID](/index.php/Kernel_mode_setting#Forcing_modes_and_EDID "Kernel mode setting").

[Kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS) is required by the Nouveau driver. By default, the KMS is done after the other kernel modules are loaded. You will see the text "Loading modules" and the size of the text may change, possibly with an undesirable flicker. See the [Nouveau KernelModeSetting page](https://nouveau.freedesktop.org/wiki/KernelModeSetting) for more details.

It is also possible to start the KMS as early as possible in the boot process, when the [initramfs](/index.php/Initramfs "Initramfs") is loaded.

To do this, add `nouveau` to the `MODULES` array in `/etc/mkinitcpio.conf`:

```
MODULES="... nouveau ..."

```

If you are using a custom EDID file, you should embed it into initramfs as well:

 `/etc/mkinitcpio.conf`  `FILES="/lib/firmware/edid/your_edid.bin"` 

Re-generate the initial ramdisk image:

```
# mkinitcpio -p <kernel preset; e.g. *linux*>

```

If you're experiencing troubles with Nouveau leading to rebuild nouveau-drm several times for testing purposes, do not add `nouveau` to the initramfs. It is too easy to forget to rebuild the initramfs and it will just make any testing harder. Just use "Late start" until you are confident the system is stable. There might be additional problems with initramfs if you need a custom firmware (generally not advised).

## Tips and tricks

### Keep NVIDIA driver installed

If you want to keep the proprietary NVIDIA driver installed (and are not using OpenGL), but want to use the Nouveau driver, comment out nouveau blacklisting in `/etc/modprobe.d/nouveau_blacklist.conf` or `/usr/lib/modprobe.d/nvidia.conf` modifying it as follows:

```
#blacklist nouveau

```

And tell Xorg to load nouveau instead of nvidia by creating the file `/etc/X11/xorg.conf.d/20-nouveau.conf` with the following content:

```
Section "Device"
    Identifier "Nvidia card"
    Driver "nouveau"
EndSection

```

If you already used the NVIDIA driver, and want to test Nouveau without reboot, make sure the 'nvidia' module is no longer loaded:

```
# rmmod nvidia

```

Then load the 'nouveau' module:

```
# modprobe nouveau

```

And check that it loaded fine by looking at kernel messages:

```
$ dmesg

```

### Installing the latest development packages

You may install the latest -git packages, through AUR:

*   You can use [mesa-git](https://aur.archlinux.org/packages/mesa-git/) which will allow the installation of the latest Mesa (including the latest DRI driver).
*   You can also try installing a newer kernel version, through packages like [linux-mainline](https://aur.archlinux.org/packages/linux-mainline/) in which the Nouveau DRM code would allow better performance.
*   To get the latest Nouveau improvements, you should use the [linux-git](https://aur.archlinux.org/packages/linux-git/) package from the AUR, edit the PKGBUILD and use Nouveau's own kernel repository, which is currently located at [git://anongit.freedesktop.org/git/nouveau/xf86-video-nouveau](git://anongit.freedesktop.org/git/nouveau/xf86-video-nouveau).

Upstream driver sources can be found at the [Nouveau Source page](https://nouveau.freedesktop.org/wiki/Source).

### Dual Head

Nouveau supports the xrandr extension for modesetting and multiple monitors. See the [xrandr](/index.php/Xrandr "Xrandr") page for tutorials.

Here is a full sample `/etc/X11/xorg.conf.d/20-nouveau.conf` above for running 2 monitors in dual head mode. You may prefer to use a graphical tool to configure monitors like GNOME Control Center's Display panel (`gnome-control-center display`).

```
# the right one
Section "Monitor"
          Identifier   "NEC"
          Option "PreferredMode" "1280x1024_60.00"
EndSection

# the left one
Section "Monitor"
          Identifier   "FUS"
          Option "PreferredMode" "1280x1024_60.00"
          Option "LeftOf" "NEC"
EndSection

Section "Device"
    Identifier "nvidia card"
    Driver "nouveau"
    Option  "Monitor-DVI-I-1" "NEC"
    Option  "Monitor-DVI-I-2" "FUS"
EndSection

Section "Screen"
    Identifier "screen1"
   Monitor "NEC"
    DefaultDepth 24
      SubSection "Display"
       Depth      24
       Virtual 2560 2048
      EndSubSection
    Device "nvidia card"
EndSection

Section "ServerLayout"
    Identifier "layout1"
    Screen "screen1"
EndSection
```

### Setting console resolution

Use the [fbset](https://www.archlinux.org/packages/?name=fbset) tool to adjust console resolution.

You can also pass the resolution to nouveau with the `video=` kernel line option (see [KMS](/index.php/KMS "KMS")).

### Power Management

The lack of proper power management in the nouveau driver is one of the most important causes of performance issue, since most card will remain in their lower power state with lower clocks during their use. Experimental support for GPU reclocking is available for some cards (See the [Nouveau PowerManagement page](https://nouveau.freedesktop.org/wiki/PowerManagement)) and since kernel 4.5 can be controlled through a debugfs interface located at `/sys/kernel/debug/dri/*/pstate`.

For example, to check the available power states and the current setting for the first card in your system, run:

```
# cat /sys/kernel/debug/dri/0/pstate

```

It's also possible to manually set/force a certain power state by writing to said interface:

```
# echo *pstate* > /sys/kernel/debug/dri/0/pstate

```

**Warning:** The support for reclocking is highly experimental. Manually setting the power state may hang your system, cause corruption or overheat your card.

#### Fan Control

If it is implemented for you card you can configure fan control via `/sys`.

```
$ find /sys -name pwm1_enable
/sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0/hwmon/hwmon1/pwm1_enable
$ readlink /sys/devices/pci0000:00/0000:00:01.0/0000:01:00.0/driver
../../../../bus/pci/drivers/nouveau

```

`pwm1_enable` can be set to 0, 1 or 2 meaning NONE, MANUAL and AUTO fan control. If set to manual fan control, you can set `pwm1` manually, for example to 40 for 40%.

**Warning:** Use at your own risk! Don't overheat your card!

You can also set it by udev rule:

```
$ cat /etc/udev/rules.d/50-nouveau-hwmon.rules
ACTION=="add", SUBSYSTEM=="hwmon", DRIVERS=="nouveau", ATTR{pwm1_enable}="2"

```

Sources:

*   [http://floppym.blogspot.de/2013/07/fan-control-with-nouveau.html](http://floppym.blogspot.de/2013/07/fan-control-with-nouveau.html)
*   [https://kalgan.cc/blog/posts/Controlling_nVidia_cards_fans_with_nouveau_in_Debian/](https://kalgan.cc/blog/posts/Controlling_nVidia_cards_fans_with_nouveau_in_Debian/)

### Optimus

You have two solutions to use [Optimus](/index.php/Optimus "Optimus") on a laptop (aka hybrid graphics, when you have two GPUs on your laptop): [bumblebee](/index.php/Bumblebee "Bumblebee") and [PRIME](/index.php/PRIME "PRIME")

## Troubleshooting

Add `drm.debug=14` and `log_buf_len=16M` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to turn on video debugging:

Create verbose Xorg log:

```
$ startx -- -logverbose 9 -verbose 9

```

View loaded video module parameters and values:

```
$ modinfo -p video

```

### Disable MSI

If you are still having problems loading the module or starting X server append `nouveau.config=NvMSI=0` to your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

Source: [https://bugs.freedesktop.org/show_bug.cgi?id=78441](https://bugs.freedesktop.org/show_bug.cgi?id=78441)

### Phantom Output Issue

It is possible for the nouveau driver to detect "phantom" outputs. For example, both VGA-1 and LVDS-1 are shown as connected but only LVDS-1 is present.

This causes display problems and a corrupted screen.

The problem can be overcome by disabling the phantom output (VGA-1 in the examples given) on the kernel command line of your boot loader. This can be achieved by appending the following:

```
video=VGA-1:d

```

Where **d** = disable.

The phantom output can also be disabled in X by adding the following to `/etc/X11/xorg.conf.d/20-nouveau.conf`:

```
Section "Monitor"
Identifier "VGA-1"
Option "Ignore" "1"
EndSection

```

Source: [http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues](http://gentoo-en.vfose.ru/wiki/Nouveau#Phantom_and_unpopulated_output_connector_issues)

### Random lockups with kernel error messages

Specific Nvidia chips with Nouveau may give random system lockups and more commonly throw many kernel messages, seen with *dmesg*. Try adding the `nouveau.noaccel=1` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter"). See [[2]](https://fedoraproject.org/wiki/Common_kernel_problems#Systems_with_nVidia_adapters_using_the_nouveau_driver_lock_up_randomly) for more information.