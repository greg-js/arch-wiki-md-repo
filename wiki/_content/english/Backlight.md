Screen brightness might be tricky to control. On some machines physical hardware switches are missing and software solutions may not work well. However, it is generally possible to find a functional method for a given hardware. This article aims to summarize all possible ways to adjust the backlight.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Overview](#Overview)
*   [2 ACPI](#ACPI)
    *   [2.1 Kernel command-line options](#Kernel_command-line_options)
    *   [2.2 Udev rule](#Udev_rule)
*   [3 OLED screen brightness](#OLED_screen_brightness)
    *   [3.1 Backlight with OLED screen in Wayland](#Backlight_with_OLED_screen_in_Wayland)
*   [4 Switch off the backlight](#Switch_off_the_backlight)
*   [5 Save/Restore functionality](#Save/Restore_functionality)
*   [6 Backlight utilities](#Backlight_utilities)
    *   [6.1 xbacklight](#xbacklight)
    *   [6.2 setpci](#setpci)
    *   [6.3 Using DBus with Gnome](#Using_DBus_with_Gnome)
*   [7 Color correction](#Color_correction)
    *   [7.1 xcalib](#xcalib)
    *   [7.2 NVIDIA settings](#NVIDIA_settings)
    *   [7.3 Increase brightness above maximum level](#Increase_brightness_above_maximum_level)
*   [8 External monitors](#External_monitors)
*   [9 Troubleshooting](#Troubleshooting)
    *   [9.1 Backlight PWM modulation frequency (Intel i915 only)](#Backlight_PWM_modulation_frequency_(Intel_i915_only))
    *   [9.2 Inverted Brightness (Intel i915 only)](#Inverted_Brightness_(Intel_i915_only))
    *   [9.3 Unable to control eDP Panel brightness (Intel i915 only)](#Unable_to_control_eDP_Panel_brightness_(Intel_i915_only))
    *   [9.4 sysfs modified but no brightness change](#sysfs_modified_but_no_brightness_change)

## Overview

There are many ways to control brightness of a monitor, laptop or integrated panel (such as the iMac). According to [these](https://bugs.launchpad.net/ubuntu/+source/xserver-xorg-video-intel/+bug/397617) [discussions](https://lore.kernel.org/patchwork/patch/528936/#708706) and this [wiki page](https://wiki.ubuntu.com/Kernel/Debugging/Backlight) the control method can be divided into these categories:

*   brightness is controlled by vendor-specified hotkey and there is no interface for the OS to adjust the brightness.
*   brightness is controlled by either the ACPI, graphic or platform driver.
*   brightness is controlled by HW register through setpci.

All methods are exposed to the user through `/sys/class/backlight` and [xrandr](/index.php/Xrandr "Xrandr")/xbacklight can choose one method to control brightness. It is still not very clear which one xbacklight prefers by default.

**Note:** On some new laptops with an OLED screen you can't use xbacklight since OLED screens have no backlight so while you will be able to change the brightness values this will not have any affect on the actual screen brightness. In this case see, [#OLED screen brightness](#OLED_screen_brightness)

## ACPI

The brightness of the screen backlight is adjusted by setting the power level of the backlight LEDs or cathodes. The power level can often be controlled using the ACPI kernel module for video. An interface to this module is provided via a sysfs directory at `/sys/class/backlight/`.

The name of the directory depends on the graphics card model.

 `$ ls /sys/class/backlight/` 
```
acpi_video0

```

In this case, the backlight is managed by an ATI graphics card. In the case of an Intel card, the directory is called `intel_backlight`. In the following examples, `acpi_video0` is used. If you use an Intel card, simply replace `acpi_video0` with `intel_backlight` in the examples.

The directory contains the following files and subdirectories:

 `$ ls /sys/class/backlight/acpi_video0/` 
```
actual_brightness  brightness         max_brightness     subsystem/    uevent             
bl_power           device/            power/             type

```

The maximum brightness can be displayed by reading from `max_brightness`, which is often 15.

 `$ cat /sys/class/backlight/acpi_video0/max_brightness` 
```
15

```

The brightness can be set by writing a number to `brightness`. Attempting to set a brightness greater than the maximum results in an error.

```
# echo 5 > /sys/class/backlight/acpi_video0/brightness

```

By default, only `root` can change the brightness by this method. To allow users in the `video` group to change the brightness, a [udev](/index.php/Udev "Udev") rule such as the following can be used:

 `/etc/udev/rules.d/backlight.rules` 
```
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="acpi_video0", RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness"
ACTION=="add", SUBSYSTEM=="backlight", KERNEL=="acpi_video0", RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"

```

### Kernel command-line options

Sometimes ACPI does not work well due to different motherboard implementations and ACPI quirks. This results in, for instance, inaccurate brightness notifications. This includes some laptops with dual graphics (e.g., Nvidia/Radeon dedicated GPU with Intel/AMD integrated GPU). Additionally, ACPI sometimes needs to register its own `acpi_video0` backlight even if one already exists (such as `intel_backlight`), which can be done by adding one of the following [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"):

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

**Note:** The systemd-backlight service restores the previous backlight brightness level at boot. To prevent conflicts for the above rules, see [#Save/Restore_functionality](#Save/Restore_functionality).

**Tip:** To set the backlight depending on power state, see [Power management#Using a script and an udev rule](/index.php/Power_management#Using_a_script_and_an_udev_rule "Power management") and use your favourite [backlight utility](#Backlight_utilities) in the script.

## OLED screen brightness

If using a desktop environment or a laptop with an OLED screen, you may notice the backlight does not function (the brightness control keys toggles the on-screen display and the brightness values can be manually adjusted in `/sys/class/backlight/intel_backlight`, but it doesn't change the actual brightness level of the screen). Since the screen is OLED (which do not have physical backlights) and until brightness control for OLED screens is supported by the kernel, you may need to shim the ACPI backlight functions to update Xrandr's "--backlight" option. This is done by monitoring the acpi_video0 (or intel_backlight) levels, and updating the xrandr brightness levels accordingly.

For this to work, you must first install [inotify-tools](https://www.archlinux.org/packages/?name=inotify-tools) and [bc](https://www.archlinux.org/packages/?name=bc). Then, create the following file:

```
$ cat /usr/local/bin/xbacklightmon

```

```
#!/bin/sh
#use LC_NUMERIC if you are using an European LC, else printf will not work because it expects an comma instead of a decimal point
LC_NUMERIC="en_US.UTF-8"

# modify this path to the location of your backlight class
path=/sys/class/backlight/intel_backlight
# get name of primary screen to adjust brightness
primaryOutput=$(xrandr | grep -E " connected primary ?[1-9]+" | sed -e "s/\([A-Z0-9]\+\) connected.*/\1/")

luminance() {
    read -r level < "$path"/actual_brightness
    factor=$((max))
    new_brightness="$(bc -l <<< "scale = 2; $level / $factor")"
    printf '%f
' $new_brightness
}

read -r max < "$path"/max_brightness

xrandr --output $primaryOutput --brightness "$(luminance)"

inotifywait -me modify --format '' "$path"/actual_brightness | while read; do
    xrandr --output $primaryOutput --brightness "$(luminance)"
done

```

Then make this file executable and owned by root:

```
$ chown root:root /usr/local/bin/xbacklightmon
$ chmod 755 /usr/local/bin/xbacklightmon

```

You may test this by running the file, and using the backlight keys to test if the brightness updates. Finally, configure the script to run when you display manager starts.

**Note:** The above script takes into account that your laptop screen is the primary screen if this is not the case you will need to set the name of the screen manually.

While all this fixes brightness issues on laptops with OLED screens, there might still be some issues showing up, e.g.:

*   Chromium and some other programs reset brightness to 100% upon their first start since reboot.
*   Hotkeys aren't working prior to login.

### Backlight with OLED screen in Wayland

The above xrandr based script and commands do not work on Wayland. Instead you can use the `icc-brightness` tool to control the OLED display brightness by applying ICC color profiles (this approach works both in xorg and wayland). The tool can be found and downloaded here: [https://github.com/udifuchs/icc-brightness](https://github.com/udifuchs/icc-brightness)

## Switch off the backlight

Switching off the backlight (for example when one locks a notebook) can be useful to conserve battery energy. Ideally the following command should work for any [Xorg](/index.php/Xorg "Xorg") graphical session:

```
xset dpms force off

```

The backlight should switch on again on mouse movement or keyboard input. Alternately `xset s` could be used.

The following example will toggle the screen saver timeout for a similar result (should be bound to a key):

 `~/.local/bin/xlcd.sh` 
```
#!/usr/bin/dash
read lcd < /tmp/lcd
    if [ "$lcd" -eq "0" ]; then
        xset s
        echo 1 > /tmp/lcd
        sleep 1
        notify-send -t 2000 LCD\ ON
    else
        xset s 3
        echo 0 > /tmp/lcd
        notify-send -t 2000 LCD\ OFF
    fi

```

If the previous commands do not work, there is a chance that *vbetool* may work. Note, however, that in this case the backlight must be manually activated again. The command is as follows:

```
$ vbetool dpms off

```

To activate the backlight again:

```
$ vbetool dpms on

```

For example, this can be put to use when closing the notebook lid using [Acpid](/index.php/Acpid "Acpid").

## Save/Restore functionality

The [systemd](/index.php/Systemd "Systemd") package includes the service `systemd-backlight@.service`, which is enabled by default and "static". It saves the backlight brightness level at shutdown and restores it at boot. The service uses the ACPI method described in [#ACPI](#ACPI), generating services for each folder found in `/sys/class/backlight/`. For example, if there is a folder named `acpi_video0`, it generates a service called `systemd-backlight@backlight:acpi_video0.service`. When using other methods of setting the backlight at boot, it is recommended to stop systemd-backlight from restoring the backlight by setting the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") parameter `systemd.restore_state=0`. See [systemd-backlight@.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-backlight%40.service.8) for details.

**Note:** Some laptops have multiple video cards (e.g. Optimus) and the backlight restoration fails. Try [masking](/index.php/Systemd#Using_units "Systemd") an instance of the service (e.g. `systemd-backlight@backlight:acpi_video1` for `acpi_video1`).

The [relight](https://aur.archlinux.org/packages/relight/) package provides an alternative systemd-based method of saving and restoring screen brightness.

Additionally, the [brillo](https://aur.archlinux.org/packages/brillo/) and [light](https://www.archlinux.org/packages/?name=light) utilities support save/restore functionality. These two may be more useful if one wishes to restore the screen brightness on a per-user basis, however no systemd units are provided to accomplish this.

## Backlight utilities

The utilities in the following table can be used to control screen brightness. All of them are compatible with Wayland and do not require X.

| Name | Controls keyboard backlights | Reacts to ambient brightness | Language | License | Notes | Package | Homepage |
| acpilight | Yes | No | Python3 | GPL-3.0-or-later | "xbacklight" compatible | [acpilight](https://www.archlinux.org/packages/?name=acpilight) | [https://gitlab.com/wavexx/acpilight](https://gitlab.com/wavexx/acpilight) |
| brightd | No | No | C | GPL-2.0 | Dims the screen when there is no user input for some time. | [brightd](https://aur.archlinux.org/packages/brightd/) | [http://www.pberndt.com/Programme/Linux/brightd](http://www.pberndt.com/Programme/Linux/brightd) |
| brillo | Yes | No | C | GPL-3.0-only | Supports smooth and relative adjustments. | [brillo](https://aur.archlinux.org/packages/brillo/) | [https://gitlab.com/cameronnemo/brillo](https://gitlab.com/cameronnemo/brillo) |
| brightnessctl | Yes | No | C | MIT | Binary is setuid unless otherwise configured. | [brightnessctl](https://www.archlinux.org/packages/?name=brightnessctl) | [https://github.com/Hummer12007/brightnessctl](https://github.com/Hummer12007/brightnessctl) |
| Calise | No | Yes | Python2 | GPL-3.0 | - | [calise](https://aur.archlinux.org/packages/calise/) | [http://calise.sourceforge.net](http://calise.sourceforge.net) |
| Clight | Yes | Yes | C | GPL-3.0-or-later | Manages screen temperature and smoothly dims brightness after a timeout. Turns webcam into an ambient light sensor. | [clight](https://aur.archlinux.org/packages/clight/) | [https://github.com/FedeDP/Clight](https://github.com/FedeDP/Clight) |
| macbook-lighter | Yes | Yes | Bash,Perl | GPL | Macbook screen/keyboard backlight CLI and auto-adjust on ambient light. | [macbook-lighter](https://aur.archlinux.org/packages/macbook-lighter/) | [https://github.com/harttle/macbook-lighter](https://github.com/harttle/macbook-lighter) |
| enlighten | No | No | C | GPL-3.0-or-later | - | [enlighten-git](https://aur.archlinux.org/packages/enlighten-git/) | [https://github.com/HalosGhost/enlighten](https://github.com/HalosGhost/enlighten) |
| illum | No | No | C | AGPL-3.0 | Reacts to key presses. | [illum-git](https://aur.archlinux.org/packages/illum-git/) | [https://github.com/jmesmon/illum](https://github.com/jmesmon/illum) |
| Light | Yes | No | C | GPL-3.0-only | Binary is setuid unless otherwise configured. | [light](https://www.archlinux.org/packages/?name=light) | [https://haikarainen.github.io/light](https://haikarainen.github.io/light) |
| Lux | No | No | Shell | MIT | - | [lux](https://aur.archlinux.org/packages/lux/) | [https://github.com/Ventto/lux](https://github.com/Ventto/lux) |

### xbacklight

Brightness can be set using the [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) package.

**Note:**

*   xbacklight only works with [Intel](/index.php/Intel "Intel"). Other drivers (e.g. [Radeon](/index.php/Radeon "Radeon")) did not add support for the RandR backlight property.
*   xbacklight currently does not work with the modesetting driver [[1]](https://gitlab.freedesktop.org/xorg/xserver/issues/47).

To set brightness to 50% of maximum:

```
$ xbacklight -set 50

```

Increments can be used instead of absolute values, for example to increase or decrease brightness by 10%:

```
$ xbacklight -inc 10
$ xbacklight -dec 10

```

Gamma can be set using either the [xorg-xrandr](https://www.archlinux.org/packages/?name=xorg-xrandr) or [xorg-xgamma](https://www.archlinux.org/packages/?name=xorg-xgamma) package. The following commands create the same effect:

```
$ xrandr --output LVDS1 --gamma 1.0:1.0:1.0
$ xgamma -rgamma 1 -ggamma 1 -bgamma 1

```

**Tip:** These commands can be bound to keyboard keys as described in [Keyboard shortcuts#Xorg](/index.php/Keyboard_shortcuts#Xorg "Keyboard shortcuts").

If you get the "No outputs have backlight property" error, it is because xrandr/xbacklight does not choose the right directory in `/sys/class/backlight`. You can specify the directory by setting the `Backlight` option of the device section in `/etc/X11/xorg.conf.d/20-*video*.conf`. For instance, if the name of the directory is `intel_backlight` and using the [Intel](/index.php/Intel "Intel") driver, the device section may be configured as follows:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
    Identifier  "Intel Graphics" 
    Driver      "intel"
    Option      "Backlight"  "intel_backlight"
EndSection
```

See [FS#27677](https://bugs.archlinux.org/task/27677) and [https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=651741) for details.

If you have enabled [Intel Fastboot](/index.php/Intel_graphics#Fastboot "Intel graphics") you might also get the `No outputs have backlight property` error. In this case, trying the above method may cause Xorg to crash on start up. You should disable it to fix the issue. It is [known](https://bugs.freedesktop.org/show_bug.cgi?id=108225) to cause issues with brightness control.

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

*   **Clight** — User daemon utility that aims to fully manage your display. It can manage the screen temperature depending on the current time of the day, just like redshift does. It tries to use [geoclue](https://www.archlinux.org/packages/?name=geoclue) to retrieve the user position if neither latitude or longitude are set in the configuration file. It also supports fixed times for sunrise and sunset.

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

You can use [xrandr](/index.php/Xrandr "Xrandr") to increase perceived brightness above its maximum level (the same caveats mentioned above for Nvidia apply):

```
$ xrandr --output *output_name* --brightness 2

```

This should roughly double luma in the image. It will sacrifice color quality for brightness, nevertheless it is particularly suited for situations where the ambient light is very bright (e.g. sunlight).

## External monitors

[DDC/CI](https://en.wikipedia.org/wiki/https://en.wikipedia.org/wiki/Display_Data_Channel#DDC.2FCI "wikipedia:https://en.wikipedia.org/wiki/Display Data Channel") (Display Data Channel Command Interface) can be used to communicate with external monitors implementing MCCS (Monitor Control Command Set) over I2C. DDC can control brightness, contrast, inputs, etc on supported monitors. Settings available via the OSD (On-Screen Display) panel can usually also be managed via DDC. The [kernel module](/index.php/Kernel_module "Kernel module") `i2c-dev` may need to be loaded if the `/dev/i2c-*` devices do not exist.

[ddcutil](http://www.ddcutil.com/) can be used to query and set brightness settings:

 `# ddcutil capabilities | grep "Feature: 10"` 
```
  Feature: 10 (Brightness)

```
 `# ddcutil getvcp 10`  `VCP code 0x10 (Brightness                    ): current value =    60, max value =   100` 
```
# ddcutil setvcp 10 70

```

Alternatively, one may use [ddcci-driver-linux-dkms](https://aur.archlinux.org/packages/ddcci-driver-linux-dkms/) to expose external monitors in sysfs. Then, after loading the `ddcci` [kernel module](/index.php/Kernel_module "Kernel module"), one can use any [backlight utility](#Backlight_utilities).

## Troubleshooting

### Backlight PWM modulation frequency (Intel i915 only)

Laptops with LED backlight are known to have screen flicker sometimes. This is because the most efficient way of controlling LED backlight brightness is by turning the LED's on and off very quickly varying the amount of time they are on.

However, the frequency of the switching, so-called PWM (pulse-width modulation) frequency, may not be high enough for the eye to perceive it as a single brightness and instead see flickering. This causes some people to have symptoms such as headaches and eyestrain.

If you have an Intel i915 GPU, then it may be possible to adjust PWM frequency to eliminate flicker.

Period of PWM (inverse to frequency) is stored in 2 higher bytes of `0xC8254` register (if you are using the Intel GM45 chipset use address `0x61254` instead). To manipulate registers values install [intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools) from the official repositories.

To increase the frequency, period must be reduced. For example:

 `# intel_reg read 0xC8254`  `0xC8254 : 0x12281228` 

Then to double PWM frequency divide 2 higher bytes (4 higher hex digits) by 2 and write back resulting value, keeping lower bytes unchanged:

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

### Unable to control eDP Panel brightness (Intel i915 only)

Embedded Display Port (eDP) v1.2 introduced a new display panel control protocol for backlight and other controls that works through the AUX channel.[[2]](https://www.vesa.org/wp-content/uploads/2010/12/DisplayPort-DevCon-Presentation-eDP-Dec-2010-v3.pdf)

By default the i915 driver tries to use PWM to control backlight brightness, which might not work.

To set the backlight through writes to DPCD registers using the AUX channel set `i915.enable_dpcd_backlight` as [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") or set in `/etc/modprobe.d/i915.conf`:

 `/etc/modprobe.d/i915.conf` 
```
options i915 enable_dpcd_backlight

```

### sysfs modified but no brightness change

**Note:** This behavior and their workarounds have been confirmed on the Dell M6700 with Nvidia K5000m (BIOS version prior to A10) and Clevo P750ZM (Eurocom P5 Pro Extreme) with Nvidia 980m.

On some systems, the brightness hotkeys on your keyboard correctly modify the values of the acpi interface in `/sys/class/backlight/acpi_video0/actual_brightness` but the brightness of the screen is not changed. Brightness applets from [desktop environments](/index.php/Desktop_environments "Desktop environments") may also show changes to no effect.

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