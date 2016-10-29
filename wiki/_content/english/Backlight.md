Screen brightness might be tricky to control. On some machines physical hardware switches are missing and software solutions may not work well. However, it is generally possible; be sure to use a method that works for your hardware.

There are many ways to adjust the screen backlight of a monitor, laptop or integrated panel (such as the iMac) using software, but depending on hardware and model, sometimes only some options are available. This article aims to summarize all possible ways to adjust the backlight.

## Contents

*   [1 Overview](#Overview)
*   [2 ACPI](#ACPI)
    *   [2.1 Kernel command-line options](#Kernel_command-line_options)
    *   [2.2 Udev rule](#Udev_rule)
*   [3 Switching off the backlight](#Switching_off_the_backlight)
*   [4 systemd-backlight service](#systemd-backlight_service)
*   [5 Backlight utilities](#Backlight_utilities)
    *   [5.1 xbacklight](#xbacklight)
    *   [5.2 light](#light)
    *   [5.3 acpilight](#acpilight)
    *   [5.4 illum](#illum)
    *   [5.5 relight](#relight)
    *   [5.6 setpci (use with great care)](#setpci_.28use_with_great_care.29)
    *   [5.7 Calise](#Calise)
    *   [5.8 brightd](#brightd)
    *   [5.9 lux](#lux)
*   [6 Color correction](#Color_correction)
    *   [6.1 xcalib](#xcalib)
    *   [6.2 Xflux](#Xflux)
    *   [6.3 redshift](#redshift)
    *   [6.4 NVIDIA settings](#NVIDIA_settings)
    *   [6.5 Increase brightness above maximum level](#Increase_brightness_above_maximum_level)
*   [7 Troubleshooting](#Troubleshooting)
    *   [7.1 Backlight PWM modulation frequency (Intel i915 only)](#Backlight_PWM_modulation_frequency_.28Intel_i915_only.29)
    *   [7.2 Inverted Brightness (Intel i915 only)](#Inverted_Brightness_.28Intel_i915_only.29)
    *   [7.3 sysfs modified but no brightness change](#sysfs_modified_but_no_brightness_change)

## Overview

There are many ways to control brightness. According to this [discussion](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/397617) and this [wiki page](https://wiki.ubuntu.com/Kernel/Debugging/Backlight) the control method can be divided into these categories:

*   brightness is controlled by vendor-specified hotkey and there is no interface for the OS to adjust the brightness.
*   brightness is controlled by either the ACPI or the graphic driver.
*   brightness is controlled by HW register through setpci.

All methods are exposed to the user through `/sys/class/backlight` and xrandr/xbacklight can choose one method to control brightness. It is still not very clear which one xbacklight prefers by default.

## ACPI

The brightness of the screen backlight is adjusted by setting the power level of the backlight LEDs or cathodes. The power level can often be controlled using the ACPI kernel module for video. An interface to this module is provided via a folder in the sysfs at `/sys/class/backlight`.

The name of the folder depends on the graphics card model.

 `# ls /sys/class/backlight/` 
```
acpi_video0

```

In this case, the backlight is managed by an ATI graphics card. In the case of an Intel card it is called `intel_backlight`. In the following example, `acpi_video0` is used.

The directory contains the following files and folders:

 `# ls /sys/class/backlight/acpi_video0/` 
```
actual_brightness  brightness         max_brightness     subsystem/    uevent             
bl_power           device/            power/             type

```

The maximum brightness can be found by reading from `max_brightness`, which is often 15.

 `# cat /sys/class/backlight/acpi_video0/max_brightness` 
```
15

```

The brightness can be set by writing a number to `brightness`. Attempting to set a brightness greater than the maximum results in an error.

```
# tee /sys/class/backlight/acpi_video0/brightness <<< 5

```

### Kernel command-line options

Sometimes, ACPI does not work well due to different motherboard implementations and ACPI quirks. This includes some laptops with dual graphics (e.g. Nvidia/Radeon dedicated GPU with Intel/AMD integrated GPU). On Nvidia Optimus laptops, the kernel parameter nomodeset can interfere with the ability to adjust the backlight. Additionally, ACPI sometimes needs to register its own `acpi_video0` backlight even if one already exists (such as `intel_backlight`), which can be done by adding one of the following kernel parameters in your [bootloader](/index.php/Bootloader "Bootloader"):

```
acpi_backlight=video
acpi_backlight=vendor
acpi_backlight=native

```

If you find that changing the `acpi_video0` backlight does not actually change the brightness, you may need to use `acpi_backlight=none`.

**Tip:**

*   On an Asus notebooks you might also need to `modprobe asus-nb-wmi` as root.
*   Disabling legacy boot on Dell XPS13 breaks backlight support.

### Udev rule

If the ACPI interface is available, the backlight level can be set at boot using a [udev](/index.php/Udev "Udev") rule:

 `/etc/udev/rules.d/81-backlight.rules` 
```
# Set backlight level to 8
SUBSYSTEM=="backlight", ACTION=="add", KERNEL=="acpi_video0", ATTR{brightness}="8"
```

**Note:** The systemd-backlight service restores the previous backlight brightness level at boot. To prevent conflicts for the above rules, see [#systemd-backlight service](#systemd-backlight_service).

**Tip:** To set the backlight depending on power state, see [Power management#Using a script and an udev rule](/index.php/Power_management#Using_a_script_and_an_udev_rule "Power management") and use your favourite [backlight utility](#Backlight_utilities) in the script.

## Switching off the backlight

Switching off the backlight (for example when one locks the notebook) can be useful to conserve battery energy. Ideally the following command inside of a graphical session should work:

```
sleep 1 && xset dpms force off

```

The backlight should switch on again on mouse movement or keyboard input. If the previous command does not work, there is a chance that `vbetool` works. Note, however, that in this case the backlight must be manually activated again. The command is as follows:

```
vbetool dpms off

```

To activate the backlight again:

```
vbetool dpms on

```

For example, this can be put to use when closing the notebook lid as outlined in the entry for [Acipd](/index.php/Acpid#Laptop_Monitor_Power_Off "Acpid").

## systemd-backlight service

The [systemd](/index.php/Systemd "Systemd") package includes the service `systemd-backlight@.service`, which is enabled by default and "static". It saves the backlight brightness level at shutdown and restores it at boot. The service uses the ACPI method described in [#ACPI](#ACPI), generating services for each folder found in `/sys/class/backlight/`. For example, if there is a folder named `acpi_video0`, it generates a service called `systemd-backlight@backlight:acpi_video0.service`. When using other methods of setting the backlight at boot, it is recommended to [mask](/index.php/Mask "Mask") the service `systemd-backlight@.service`.

Some laptops have multiple video cards (e.g. Optimus) and the backlight restoration fails. Try [masking](/index.php/Systemd#Using_units "Systemd") an *instance* of the service, e.g. `systemd-backlight@backlight\:acpi_video1` for `acpi_video1`.

From the systemd-backlight@.service man page:

systemd-backlight understands the following kernel command line parameter:

```
systemd.restore_state=

```

Takes a boolean argument. Defaults to "1".

If "0", does not restore the backlight settings on boot. However, settings will still be stored on shutdown.

## Backlight utilities

### xbacklight

Brightness can be set using the [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) package.

**Note:**

*   xbacklight only works with intel. Radeon does not support the RandR backlight property.
*   xbacklight currently does not work with the modesetting driver [[1]](https://bugs.freedesktop.org/show_bug.cgi?id=96572).

To set brightness to 50% of maximum:

```
$ xbacklight -set 50

```

Increments can be used instead of absolute values, for example to increase or decrease brightness by 10%:

```
$ xbacklight -inc 10
$ xbacklight -dec 10

```

Gamma can be set using either the [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) or [xorg-xgamma](https://www.archlinux.org/packages/?name=xorg-xgamma) package. The following commands create the same effect.

```
$ xrandr --output LVDS1 --gamma 1.0:1.0:1.0
$ xgamma -rgamma 1 -ggamma 1 -bgamma 1

```

**Tip:** These commands can be bound to keyboard keys as described in [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

If you get the "No outputs have backlight property" error, it is because xrandr/xbacklight does not choose the right directory in `/sys/class/backlight`. You can specify the directory by setting the `Backlight` option of the device section in xorg.conf. For instance, if the name of the directory is `intel_backlight`, the device section can be configured as follows:

 `/etc/X11/xorg.conf` 
```
Section "Device"
    Identifier  "Card0"
    Driver      "intel"
    Option      "Backlight"  "intel_backlight"
EndSection
```

See [FS#27677](https://bugs.archlinux.org/task/27677) and [[2]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741) for details.

### light

Light is the successor and C-port of *LightScript*.

[Install](/index.php/Install "Install") [light](https://aur.archlinux.org/packages/light/) for the latest tagged version, or [light-git](https://aur.archlinux.org/packages/light-git/) for the latest development version. Patches are frequently committed to the git repository so it is recommended to use the [light-git](https://aur.archlinux.org/packages/light-git/) package.

See the [GitHub page](http://haikarainen.github.io/light/) for more information.

### acpilight

[acpilight](https://aur.archlinux.org/packages/acpilight/) contains an "xbacklight" compatibile utility that uses the sys filesystem to set the display brightness. Since it doesn't use X at all, it can also be used on the console.

See the [acpilight repository](https://github.com/wavexx/acpilight/) for more information.

### illum

[illum-git](https://aur.archlinux.org/packages/illum-git/) monitors the brightness up and brightness down keys on all input devices (via libevdev) and adjusts the backlight when they are pressed (via sysfs).

Written for newer BIOS/UEFI that doesn't automatically handle those buttons for you. This is an alternate to handling those buttons via acpi handlers or via x11/wm hotkeys.

### relight

[relight](http://xyne.archlinux.ca/projects/relight) is available in [Xyne's repos](http://xyne.archlinux.ca/repos) and as package [relight](https://aur.archlinux.org/packages/relight/) in the [AUR](/index.php/AUR "AUR"). The package provides `relight.service`, a [systemd](/index.php/Systemd "Systemd") service to automatically restore previous backlight settings during reboot along using the ACPI method explained above, and *relight-menu*, a dialog-based menu for selecting and configuring backlights for different screens.

### setpci (use with great care)

It is possible to set the register of the graphic card to adjust the backlight. It means you adjust the backlight by manipulating the hardware directly, which can be risky and generally is not a good idea. Not all of the graphic cards support this method.

When using this method, you need to use `lspci` first to find out where your graphic card is.

```
# setpci -s 00:02.0 F4.B=0

```

### Calise

The software [calise](http://calise.sourceforge.net/wordpress/) can be found in AUR.

*   Stable version: [calise](https://aur.archlinux.org/packages/calise/)
*   Development version: [calise-git](https://aur.archlinux.org/packages/calise-git/)

It basically computes ambient brightness, and set screen's correct backlight, simply making captures from the webcam, for laptop without light sensor. For more information, calise has its own wiki: [Calise wiki](http://calise.sourceforge.net/mediawiki/index.php/Main_Page).

The main features of this program are that it is very precise, very light on resource usage, and with the daemon version (.service file for systemd users available too), it has practically no impact on battery life.

### brightd

Macbook-inspired [brightd](https://aur.archlinux.org/packages/brightd/) automatically dims (but does not put to standby) the screen when there is no user input for some time. A good companion of [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") so that the screen does not blank out in a sudden.

### lux

[lux](https://aur.archlinux.org/packages/lux/) is a Bash script to easily control brightness on backlight-controllers.

See the [GitHub page](https://github.com/Ventto/lux) for more information.

## Color correction

### xcalib

**Note:** *xcalib* does *not* change the backlight power, it just modifies the video LUT table: this means that your battery life will be unaffected by the change. Nevertheless, it could be useful when no backlight control is available (Desktop PCs). Use `xcalib -clear` to reset the LUT.

The package [xcalib](https://aur.archlinux.org/packages/xcalib/) ([upstream URL](http://xcalib.sourceforge.net/)) is available in the [AUR](/index.php/AUR "AUR") and can be used to dim the screen. A demonstration video is available on [YouTube](https://www.youtube.com/watch?v=A9xsvntT6i4). This program can correct gamma, invert colors, and reduce contrast, the latter of which we use in this case. For example, to dim down:

```
$ xcalib -co 40 -a

```

This program uses ICC technology to interact with X11 and while the screen is dimmed, you may find that the mouse cursor is just as bright as before.

### Xflux

Xflux is the [f.lux](http://justgetflux.com) port for the X-Windows system. It fluctuates your screen between blue during the day and yellow or orange at night. This helps you adapt to the time of day and stop staying up late because of your bright computer screen.

Various packages exist in the AUR that use *f.lux*.[[3]](https://aur.archlinux.org/packages/?O=0&K=xflux) The "main" package is [xflux](https://aur.archlinux.org/packages/xflux/) which handles the command line functionality of *f.lux*. Various daemons exist to handle the automatic startup of the xflux package.

### redshift

The program [redshift](/index.php/Redshift "Redshift") in the official repositories uses `randr` to adjust the screen brightness depending on the time of day and your geographic position. It can also do RGB gamma corrections and set color temperatures. As with `xcalib`, this is very much a software solution and the look of the mouse cursor is unaffected. To execute a single quick adjustment of the brightness, try something like this:

```
redshift -o -l 0:0 -b 0.8 -t 6500:6500

```

**Tip:** If your longitude is west or your latitude is south, you should input it as negative.

Example for Berkeley, CA:

```
redshift-gtk -l 37.8717:-122.2728 

```

### NVIDIA settings

Users of [NVIDIA's proprietary drivers](/index.php/NVIDIA "NVIDIA") users can change display brightness via the nvidia-settings utility under "X Server Color Correction." However, note that this has absolutely nothing to do with backlight (intensity), it merely adjusts the color output. (Reducing brightness this way is a power-inefficient last resort when all other options fail; increasing brightness spoils your color output completely, in a way similar to overexposed photos.)

### Increase brightness above maximum level

You can use [xrandr](/index.php/Xrandr "Xrandr") to increase brightness above its maximum level:

```
$ xrandr --output *output_name* --brightness 2

```

This will set the brightness level to 200%. It will cause higher power usage and sacrifice color quality for brightness, nevertheless it is particularly suited for situations where the ambient light is very bright (e.g. sunlight).

## Troubleshooting

### Backlight PWM modulation frequency (Intel i915 only)

Laptops with LED backlight are known to have screen flicker sometimes. This is because the most efficient way of controlling LED backlight brightness is by turning the LED's on and off very quickly varying the amount of time they are on.

However, the frequency of the switching (so-called PWM modulation frequency) may not be high enough for the eye to perceive it as a single brightness and instead see flickering. This causes some people to have symptoms such as headaches and eyestrain.

If you have an Intel i915 GPU, then it may be possible to adjust PWM modulation frequency to eliminate flicker.

Install [intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools) from the official repositories. Get value of the register, that determines PWM modulation frequency

 `# intel_reg read 0xC8254` 
```
0xC8254 : 0x12281228

```

The value returned represents period of PWM modulation. So to increase PWM modulation frequency, value of the register has to be reduced. For example, to double frequency from the previous listing, execute:

```
# intel_reg write 0xC8254 0x09140914

```

You can use online calculator to calculate desired value [http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html](http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html)

Refer to dedicated topic for details [https://bbs.archlinux.org/viewtopic.php?pid=1245913](https://bbs.archlinux.org/viewtopic.php?pid=1245913)

If you are using the Intel GM45 chipset use address 0x61254 instead of 0xC8254.

### Inverted Brightness (Intel i915 only)

Symptoms:

*   after installing `xf86-video-intel` systemd-backlight.service turns off the backlight during boot
    *   possible solution: mask systemd-backlight.service
*   switching from X to another VT turns the backlight off
*   the brightness keys are inverted (i.e. turning up the brightness makes the screen darker)

This problem may be solved by adding `i915.invert_brightness=1` to the list of [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

### sysfs modified but no brightness change

**Note:** This behavior and their workarounds have been confirmed on the Dell M6700 with Nvidia K5000m (BIOS version prior to A10) and Clevo P750ZM (Eurocom P5 Pro Extreme) with Nvidia 980m.

On some systems, the brighness hotkeys on your keyboard correctly modify the values of the acpi interface in `/sys/class/backlight/acpi_video0/actual_brightness` but the brightness of the screen is not changed. Brigthness applets from [desktop environments](/index.php/Desktop_environments "Desktop environments") may also show changes to no effect.

If you have tested the recommended kernel parameters and only `xbacklight` works, then you may be facing an incompatibility between your BIOS and kernel driver.

In this case the only solution is to wait for a fix either from the BIOS or GPU driver manufacturer.

A workaround is to use the inotify kernel api to trigger `xbacklight` each time the value of `/sys/class/backlight/acpi_video0/actual_brightness` changes.

First [install](/index.php/Install "Install") [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools). Then create a script around inotify that will be launched upon each boot or through [autostart](/index.php/Autostart "Autostart").

 `/usr/local/bin/xbacklightmon` 
```
#!/bin/sh

path=/sys/class/backlight/acpi_video0

luminance() {
    read -r level < "$path"/actual_brightness
    factor=$((max / 100))
    printf '%d
' "$((level / factor))"
}

read -r max < "$path"/max_brightness

xbacklight -set "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    xbacklight -set "$(luminance)"
done

```