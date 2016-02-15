The X201 Tablet is a quad core convertable laptop produced by Lenovo. See [Thinkwiki](http://www.thinkwiki.org/wiki/Category:X201_Tablet) for more information.

Follow the [Installation guide](/index.php/Installation_guide "Installation guide") or [Beginner's Guide](/index.php/Beginner%27s_Guide "Beginner's Guide") to get a base install working.

## Contents

*   [1 LCD](#LCD)
    *   [1.1 Driver](#Driver)
    *   [1.2 Wacom serial panel](#Wacom_serial_panel)
    *   [1.3 Rotation](#Rotation)
*   [2 Hibernation](#Hibernation)
*   [3 Fbsplash](#Fbsplash)
*   [4 Power Saving](#Power_Saving)
    *   [4.1 Battery](#Battery)
    *   [4.2 Fan control](#Fan_control)
    *   [4.3 TLP](#TLP)
    *   [4.4 Frequency Scaling](#Frequency_Scaling)
    *   [4.5 Undervolting](#Undervolting)
    *   [4.6 Bootloader kernel options](#Bootloader_kernel_options)
        *   [4.6.1 grub2](#grub2)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Using non-Lenovo Network cards](#Using_non-Lenovo_Network_cards)

## LCD

This has a few steps to get everything on the panel working.

### Driver

The driver it uses is the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver. See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### Wacom serial panel

To get basic support, install [linuxconsole](https://www.archlinux.org/packages/?name=linuxconsole) and [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) and run

 `inputattach -w8001 /dev/ttyS0` 

To handle it at boot, install [wacom-udev](https://aur.archlinux.org/packages/wacom-udev/).

### Rotation

I use this script, named rotate-script.sh, and keep it in ~/.local/bin. One could also keep it in /usr/local/bin to use with [acpid](https://www.archlinux.org/packages/?name=acpid).

It's usage is

```
$ rotate-script.sh normal

```

to rotate the screen either between right or normal, or

```
$ rotate-script.sh invert

```

to invert the screen.

 `~/.local/bin/rotate-script.sh` 

```
#!/bin/bash
# This is a script that toggles rotation of the screen through xrandr,
# and also toggles rotation of the stylus, eraser and cursor through xsetwacom

# Check orientation
orientation=`/usr/bin/xrandr --verbose -q | grep LVDS | awk '{print $6}'`
# Rotate the screen and stylus, eraser and cursor, according to your preferences.
if [ "$1" = "normal" ]; then
    if [ "$orientation" = "normal" ]; then
	/usr/bin/xrandr --output LVDS1 --rotate right
	/usr/bin/xsetwacom set 14 Rotate cw
	/usr/bin/xsetwacom set 15 Rotate cw
	/usr/bin/xsetwacom set 16 Rotate cw
    else
	/usr/bin/xrandr --output LVDS1 --rotate normal
	/usr/bin/xsetwacom set 14 Rotate none
	/usr/bin/xsetwacom set 15 Rotate none
	/usr/bin/xsetwacom set 16 Rotate none
    fi
elif [ "$1" = "invert" ]; then
    if [ "$orientation" = "normal" ]; then
	/usr/bin/xrandr --output LVDS1 --rotate inverted
	/usr/bin/xsetwacom set 14 Rotate half
	/usr/bin/xsetwacom set 15 Rotate half
	/usr/bin/xsetwacom set 16 Rotate half
    elif [ "$orientation" = "inverted" ]; then
	/usr/bin/xrandr --output LVDS1 --rotate normal
	/usr/bin/xsetwacom set 14 Rotate none
	/usr/bin/xsetwacom set 15 Rotate none
	/usr/bin/xsetwacom set 16 Rotate none
    elif [ "$orientation" = "right" ]; then
	/usr/bin/xrandr --output LVDS1 --rotate left
	/usr/bin/xsetwacom set 14 Rotate ccw
	/usr/bin/xsetwacom set 15 Rotate ccw
	/usr/bin/xsetwacom set 16 Rotate ccw
    elif [ "$orientation" = "left" ]; then
	/usr/bin/xrandr --output LVDS1 --rotate right
	/usr/bin/xsetwacom set 14 Rotate cw
	/usr/bin/xsetwacom set 15 Rotate cw
	/usr/bin/xsetwacom set 16 Rotate cw
    fi
fi

```

You can then bind them to a key to rotate/invert your screen using the hardware buttons or ACPI lid events. You also may have to tweak it a bit for models without the touchscreen (id 16)

## Hibernation

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Fbsplash

To make [fbsplash](/index.php/Fbsplash "Fbsplash") work, i915 has to be added to the modules array in mkinitcpio.conf:

 `/etc/mkinitcpio.conf`  `MODULES="i915"` 

## Power Saving

### Battery

Install [tp_smapi](https://www.archlinux.org/packages/?name=tp_smapi) and set your battery settings. They are located at: `/sys/devices/platform/smapi/BATx` 

BAT0 is the main battery attached to your laptop. BAT1 is the battery attached to the X200 Ultrabase.

### Fan control

There are some discussions concerning overheating-related shutdowns when running under full load (video encoding, etc) ([[1]](http://forums.lenovo.com/t5/X-Series-ThinkPad-Laptops/x201-random-shutdown/td-p/227471) [[2]](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/751689)).

[Thinkpad Fan Control](/index.php/Thinkpad_Fan_Control "Thinkpad Fan Control") contains instructions to install tpfand as a custom replacement for hardware (bios-) fan control.

**Warning:** Wrong settings may damage your machine! Use with caution!

Start `tpfan-admin` and adjust the settings (by clicking on the sensor's graph). You should split the graph (via context menu) and set the fan to **full-speed** when the sensor reaches, say, 65 °C. You may also edit the config file directly.

### TLP

You may install [TLP](/index.php/TLP "TLP") instead of [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") to automate power saving operations.

### Frequency Scaling

One can use [cpupower](https://www.archlinux.org/packages/?name=cpupower) to control frequency scaling; see [Cpufrequtils](/index.php/Cpufrequtils "Cpufrequtils") for more information.

### Undervolting

Undervolting is not possible with the intel core iX cpu.

### Bootloader kernel options

Add these kernel options to your bootloader's config file to make use of power saving mechanisms which are turned off by default because of reported instabilities. For me, they do a great job on my X201.

**Warning:** These options can cause instability on your system! Try them and remove them if you are experiencing problems.

#### grub2

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="[...] i915_enable_rc6=1 i915_enable_fbc=1"` 

Update grub.cfg afterwards: `grub-mkconfig -o /boot/grub/grub.cfg`

## Troubleshooting

### Using non-Lenovo Network cards

If you get

```
 1802: Unauthorized network card is plugged in - Power off and remove the miniPCI network card.

```

on boot, that means your BIOS does not include that specific card in it's whitelist. The only option is either coreboot or a custom BIOS with the whitelist "disabled".

Such a bios can be found at [this forum post at mydigitallife.info.](http://forums.mydigitallife.info/threads/20223-Remove-whitelist-check-add-ID-s-to-break-hardware-restrictions-mod-requests?p=770633&viewfull=1#post770633)

You can either use Windows to flash, or a DOS boot disk with [phlash16.exe](https://www.wimsbios.com/files/flashers/phoenix/phlash16-1.7.0.21.zip) and the 02C2100.ROM from the forum post's rar like I did. To do it this way, first upgrade the BIOS to the [latest version from Lenovo.](http://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/6quj19us.iso) Then, rename "02C2100.ROM" to "BIOS.WPH", save it to your DOS boot disk and run phlash16.exe.