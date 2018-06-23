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
    *   [5.2 setpci](#setpci)
    *   [5.3 Using DBus with Gnome](#Using_DBus_with_Gnome)
*   [6 Color correction](#Color_correction)
    *   [6.1 xcalib](#xcalib)
    *   [6.2 NVIDIA settings](#NVIDIA_settings)
    *   [6.3 Increase brightness above maximum level](#Increase_brightness_above_maximum_level)
*   [7 External monitors](#External_monitors)
*   [8 Troubleshooting](#Troubleshooting)
    *   [8.1 Backlight PWM modulation frequency (Intel i915 only)](#Backlight_PWM_modulation_frequency_.28Intel_i915_only.29)
    *   [8.2 Inverted Brightness (Intel i915 only)](#Inverted_Brightness_.28Intel_i915_only.29)
    *   [8.3 sysfs modified but no brightness change](#sysfs_modified_but_no_brightness_change)

## Overview

There are many ways to control brightness. According to this [discussion](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/397617) and this [wiki page](https://wiki.ubuntu.com/Kernel/Debugging/Backlight) the control method can be divided into these categories:

*   brightness is controlled by vendor-specified hotkey and there is no interface for the OS to adjust the brightness.
*   brightness is controlled by either the ACPI or the graphic driver.
*   brightness is controlled by HW register through setpci.

All methods are exposed to the user through `/sys/class/backlight` and xrandr/xbacklight can choose one method to control brightness. It is still not very clear which one xbacklight prefers by default.

## ACPI

The brightness of the screen backlight is adjusted by setting the power level of the backlight LEDs or cathodes. The power level can often be controlled using the ACPI kernel module for video. An interface to this module is provided via a sysfs directory at `/sys/class/backlight/`.

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

By default, only `root` can change the brightness by this method. To allow users in the `video` group to change the brightness, a [udev](/index.php/Udev "Udev") rule such as the following can be used:

 `/etc/udev/rules.d/backlight.rules` 
```
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="acpi_video0", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="acpi_video0", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"

```

### Kernel command-line options

Sometimes, ACPI does not work well due to different motherboard implementations and ACPI quirks, resulting in, for instance, inaccurate brightness notifications. This includes some laptops with dual graphics (e.g. Nvidia/Radeon dedicated GPU with Intel/AMD integrated GPU). Additionally, ACPI sometimes needs to register its own `acpi_video0` backlight even if one already exists (such as `intel_backlight`), which can be done by adding one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

```
acpi_backlight=video
acpi_backlight=vendor
acpi_backlight=native

```

If you find that changing the `acpi_video0` backlight does not actually change the brightness, you may need to use `acpi_backlight=none`.

**Tip:**

*   On Nvidia Optimus laptops, the kernel parameter `nomodeset` can interfere with the ability to adjust the backlight.
*   On an Asus notebooks you might also need to load the `asus-nb-wmi` [kernel module](/index.php/Kernel_module "Kernel module").
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
$ sleep 1 && xset dpms force off

```

The backlight should switch on again on mouse movement or keyboard input. If the previous command does not work, there is a chance that `vbetool` works. Note, however, that in this case the backlight must be manually activated again. The command is as follows:

```
$ vbetool dpms off

```

To activate the backlight again:

```
$ vbetool dpms on

```

For example, this can be put to use when closing the notebook lid using [Acpid](/index.php/Acpid "Acpid").

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

*   **acpilight** — "xbacklight" compatible utility that uses the sys filesystem to set the display brightness. Since it doesn't use X at all, it can also be used on the console and Wayland and has no problems with KMS drivers. Furthermore, on ThinkPad laptops, the keyboard backlight can also be controlled.

	[https://gitlab.com/wavexx/acpilight/](https://gitlab.com/wavexx/acpilight/) || [acpilight](https://aur.archlinux.org/packages/acpilight/)

*   **brightd** — Macbook-inspired brightd automatically dims (but does not put to standby) the screen when there is no user input for some time. A good companion of [Display Power Management Signaling](/index.php/Display_Power_Management_Signaling "Display Power Management Signaling") so that the screen does not blank out in a sudden.

	[http://www.pberndt.com/Programme/Linux/brightd/](http://www.pberndt.com/Programme/Linux/brightd/) || [brightd](https://aur.archlinux.org/packages/brightd/)

*   **brightnessctl** — Lightweight brightness control tool (Wayland compatible). Note that brightnessctl is a setuid binary, which might be considered a security risk by some.

	[https://github.com/Hummer12007/brightnessctl](https://github.com/Hummer12007/brightnessctl) || [brightnessctl](https://aur.archlinux.org/packages/brightnessctl/)

*   **Calise** — Calculates ambient brightness and sets screen’s correct backlight using a camera.

	[http://calise.sourceforge.net/](http://calise.sourceforge.net/) || [calise](https://aur.archlinux.org/packages/calise/)

*   **Clight** — User daemon utility that aims to fully manage your display. It will automagically change screen backlight level to match ambient brightness, as computed by capturing frames from webcam. Moreover, it can manage your screen temperature, just like redshift does. Finally, it can dim your screen after a timeout.

	[https://github.com/FedeDP/Clight](https://github.com/FedeDP/Clight) || [clight-git](https://aur.archlinux.org/packages/clight-git/)

*   **enlighten** — Very small C utility to control the backlight brightness in Linux.

	[https://github.com/HalosGhost/enlighten](https://github.com/HalosGhost/enlighten) || [enlighten-git](https://aur.archlinux.org/packages/enlighten-git/)

*   **illum** — Backlight manager, which changes the screen backlight level based on keypresses (brightness up and brightness down). Written for newer BIOS/UEFI that does not automatically handle those buttons. This is an alternate to handling those buttons via acpi handlers or via x11/wm hotkeys.

	[https://github.com/jmesmon/illum](https://github.com/jmesmon/illum) || [illum-git](https://aur.archlinux.org/packages/illum-git/)

*   **Light** — Program to control backlight controllers. It is the successor of *LightScript*.

	[https://haikarainen.github.io/light/](https://haikarainen.github.io/light/) || [light](https://aur.archlinux.org/packages/light/)

*   **Lux** — Shell script to easily control brightness on backlight-controllers.

	[https://github.com/Ventto/lux](https://github.com/Ventto/lux) || [lux](https://aur.archlinux.org/packages/lux/)

*   **relight** — The package provides `relight.service`, a [systemd](/index.php/Systemd "Systemd") service to automatically restore previous backlight settings during reboot along using the ACPI method explained above, and *relight-menu*, a dialog-based menu for selecting and configuring backlights for different screens.

	[http://xyne.archlinux.ca/projects/relight](http://xyne.archlinux.ca/projects/relight) || [relight](https://aur.archlinux.org/packages/relight/)

*   **xbacklight** — RandR-based backlight control application.

	[https://xorg.freedesktop.org/](https://xorg.freedesktop.org/) || [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight)

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

**Tip:** These commands can be bound to keyboard keys as described in [Xorg keybinding](/index.php/Xorg_keybinding "Xorg keybinding").

If you get the "No outputs have backlight property" error, it is because xrandr/xbacklight does not choose the right directory in `/sys/class/backlight`. You can specify the directory by setting the `Backlight` option of the device section in xorg.conf. For instance, if the name of the directory is `intel_backlight`, the device section can be configured as follows:

 `/etc/X11/xorg.conf` 
```
Section "Device"
    Identifier  "Card0"
    Driver      "intel"
    Option      "Backlight"  "intel_backlight"
EndSection
```

Note: You'd need to install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) to reference the intel driver.

See [FS#27677](https://bugs.archlinux.org/task/27677) and [[2]](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741) for details.

### setpci

It is possible to set the register of the graphic card to adjust the backlight. It means you adjust the backlight by manipulating the hardware directly, which can be risky and generally is not a good idea. Not all of the graphic cards support this method.

When using this method, you need to use `lspci` first to find out where your graphic card is.

```
# setpci -s 00:02.0 F4.B=0

```

### Using DBus with Gnome

Brightness can also be adjusted as the gnome controls do. Changes are reflected in the gnome UI using this method.

```
gdbus call --session --dest org.gnome.SettingsDaemon.Power --object-path /org/gnome/SettingsDaemon/Power --method org.freedesktop.DBus.Properties.Set org.gnome.SettingsDaemon.Power.Screen Brightness "<int32 50>"

```

Steps in brightness for keyboard contol can be implemented with this method as well.

```
gdbus call --session --dest org.gnome.SettingsDaemon.Power --object-path /org/gnome/SettingsDaemon/Power --method org.gnome.SettingsDaemon.Power.Screen.StepUp
gdbus call --session --dest org.gnome.SettingsDaemon.Power --object-path /org/gnome/SettingsDaemon/Power --method org.gnome.SettingsDaemon.Power.Screen.StepDown

```

## Color correction

*   **Clight** — User daemon utility that aims to fully manage your display. It can manage the screen temperature depending on the current time of the day, just like redshift does. It tries to use [geoclue2](https://www.archlinux.org/packages/?name=geoclue2) to retrieve the user position if neither latitude or longitude are set in the configuration file. It also supports fixed times for sunrise and sunset.

	[https://github.com/FedeDP/Clight](https://github.com/FedeDP/Clight) || [clight-git](https://aur.archlinux.org/packages/clight-git/)

*   **Monica** — Monitor calibration tool. It works as frontend to xgamma to alter the gamma correction.

	[https://web.archive.org/web/20090815224839/http://www.pcbypaul.com/software/monica.html](https://web.archive.org/web/20090815224839/http://www.pcbypaul.com/software/monica.html) || [monica](https://www.archlinux.org/packages/?name=monica)

*   **[Redshift](/index.php/Redshift "Redshift")** — Color temperature adjustment tool. It adjusts the color temperature of your screen according to your surroundings. This may help your eyes hurt less if you are working in front of the screen at night. This program is inspired by [f.lux](https://en.wikipedia.org/wiki/f.lux "wikipedia:f.lux").

	[http://jonls.dk/redshift/](http://jonls.dk/redshift/) || [redshift](https://www.archlinux.org/packages/?name=redshift)

*   **xcalib** — Lightweight monitor calibration loader which can load an ICC monitor profile to be shared across desktop applications.

	[https://github.com/OpenICC/xcalib](https://github.com/OpenICC/xcalib) || [xcalib](https://aur.archlinux.org/packages/xcalib/)

*   **xgamma** — Alter a monitor's gamma correction.

	[https://xorg.freedesktop.org/](https://xorg.freedesktop.org/) || [xorg-xgamma](https://www.archlinux.org/packages/?name=xorg-xgamma)

### xcalib

**Note:** *xcalib* does *not* change the backlight power, it just modifies the video LUT table: this means that your battery life will be unaffected by the change. Nevertheless, it could be useful when no backlight control is available (Desktop PCs). Use `xcalib -clear` to reset the LUT.

The package [xcalib](https://aur.archlinux.org/packages/xcalib/) ([upstream URL](http://xcalib.sourceforge.net/)) is available in the [AUR](/index.php/AUR "AUR") and can be used to dim the screen. A demonstration video is available on [YouTube](https://www.youtube.com/watch?v=A9xsvntT6i4). This program can correct gamma, invert colors, and reduce contrast, the latter of which we use in this case. For example, to dim down:

```
$ xcalib -co 40 -a

```

This program uses ICC technology to interact with X11 and while the screen is dimmed, you may find that the mouse cursor is just as bright as before.

### NVIDIA settings

Users of [NVIDIA's proprietary drivers](/index.php/NVIDIA "NVIDIA") users can change display brightness via the nvidia-settings utility under "X Server Color Correction." However, note that this has absolutely nothing to do with backlight (intensity), it merely adjusts the color output. (Reducing brightness this way is a power-inefficient last resort when all other options fail; increasing brightness spoils your color output completely, in a way similar to overexposed photos.)

### Increase brightness above maximum level

You can use [xrandr](/index.php/Xrandr "Xrandr") to increase brightness above its maximum level:

```
$ xrandr --output *output_name* --brightness 2

```

This will set the brightness level to 200%. It will cause higher power usage and sacrifice color quality for brightness, nevertheless it is particularly suited for situations where the ambient light is very bright (e.g. sunlight).

## External monitors

DDC/CI (Display Data Channel Command Interface) can be used to communicate with external monitors implementing MCCS (Monitor Control Command Set) over I2C. DDC can control brightness, contrast, inputs, etc on supported monitors. Settings available via the OSD (On-Screen Display) panel can usually also be managed via DDC.

[ddcutil](http://www.ddcutil.com/) can be used to query and set brightness settings:

 `# ddcutil capabilities | grep Brightness` 
```
  Feature: 10 (Brightness)

```
 `# ddcutil getvcp 10`  `VCP code 0x10 (Brightness                    ): current value =    60, max value =   100` 
```
# ddcutil setvcp 10 70

```

## Troubleshooting

### Backlight PWM modulation frequency (Intel i915 only)

Laptops with LED backlight are known to have screen flicker sometimes. This is because the most efficient way of controlling LED backlight brightness is by turning the LED's on and off very quickly varying the amount of time they are on.

However, the frequency of the switching, so-called PWM (pulse-width modulation) frequency, may not be high enough for the eye to perceive it as a single brightness and instead see flickering. This causes some people to have symptoms such as headaches and eyestrain.

If you have an Intel i915 GPU, then it may be possible to adjust PWM frequency to eliminate flicker.

Period of PWM (inverse to frequency) is stored in 4 higher bytes of `0xC8254` register (if you are using the Intel GM45 chipset use address `0x61254` instead). To manipulate registers values install [intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools) from the official repositories.

To increase the frequency, period must be reduced. For example:

 `# intel_reg read 0xC8254`  `0xC8254 : 0x12281228` 

Then to double PWM frequency divide 4 higher bytes by 2 and write back resulting value, keeping lower bytes unchanged:

```
# intel_reg write 0xC8254 0x09141228

```

You can use online calculator to calculate desired value [http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html](http://devbraindom.blogspot.com/2013/03/eliminate-led-screen-flicker-with-intel.html)

To set new frequency automatically, consider writing an udev rule or install [intelpwm-udev](https://aur.archlinux.org/packages/intelpwm-udev/).

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
    factor=$((100 / max))
    printf '%d
' "$((level * factor))"
}

read -r max < "$path"/max_brightness

xbacklight -set "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    xbacklight -set "$(luminance)"
done

```