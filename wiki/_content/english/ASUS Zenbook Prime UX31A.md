This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the ASUS Zenbook UX31A and UX21A Ultrabooks. Most of it should also hold for UX32VD.

See previous generation [ASUS Zenbook UX31E](/index.php/ASUS_Zenbook_UX31E "ASUS Zenbook UX31E") page that has mostly orthogonal information to those here (may be only partially applicable to UX31A)

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Boot from USB medium](#Boot_from_USB_medium)
*   [2 Function keys](#Function_keys)
    *   [2.1 Screen backlight](#Screen_backlight)
    *   [2.2 Keyboard backlight](#Keyboard_backlight)
        *   [2.2.1 Manually setting the brightness](#Manually_setting_the_brightness)
        *   [2.2.2 Using asus-kbd-backlight from AUR](#Using_asus-kbd-backlight_from_AUR)
        *   [2.2.3 Ambient Light Sensor (ALS)](#Ambient_Light_Sensor_.28ALS.29)
            *   [2.2.3.1 ALS Driver](#ALS_Driver)
            *   [2.2.3.2 ALS Controller](#ALS_Controller)
            *   [2.2.3.3 Sample Script](#Sample_Script)
*   [3 Solid State Drive](#Solid_State_Drive)
*   [4 Graphics](#Graphics)
*   [5 Touchpad](#Touchpad)
    *   [5.1 Multitouch gestures](#Multitouch_gestures)
    *   [5.2 Multi-tap, two-finger scrolling doesn't work](#Multi-tap.2C_two-finger_scrolling_doesn.27t_work)
    *   [5.3 Multitouch gestures in Gnome 3](#Multitouch_gestures_in_Gnome_3)
    *   [5.4 Disable Touchpad While Typing](#Disable_Touchpad_While_Typing)
*   [6 HDMI plugged at boot](#HDMI_plugged_at_boot)
*   [7 Powersave management](#Powersave_management)
*   [8 Hardware and Modules](#Hardware_and_Modules)
    *   [8.1 Devices](#Devices)
    *   [8.2 Other Devices and Drivers](#Other_Devices_and_Drivers)
        *   [8.2.1 MEI](#MEI)
        *   [8.2.2 watchdog](#watchdog)
    *   [8.3 Problem with ACPI and gpio_ich](#Problem_with_ACPI_and_gpio_ich)
*   [9 Additional resources](#Additional_resources)

## Installation

To install Arch Linux on UX31A, you can follow the official [Installation guide](/index.php/Installation_guide "Installation guide"). Since the UX31A uses UEFI and GPT, make sure to also read the [UEFI](/index.php/UEFI "UEFI"), [GPT](/index.php/GPT "GPT") and [UEFI Bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") pages. To prepare a UEFI USB device, read [UEFI#Create UEFI bootable USB from ISO](/index.php/UEFI#Create_UEFI_bootable_USB_from_ISO "UEFI").

### Boot from USB medium

Press `Escape` to get into the boot menu. If the USB bootable device is not listed, enter the configuration menu and directly press `F10` to save. Press `Escape` again on reboot: This time the USB bootable device should appear in the menu.

Make sure to boot the USB in EFI-Mode, to easily install the bootloader later.

## Function keys

**Note:** A working keymap means that there is some output in `xev` when the key combination is pressed OR that the functionality is built in and "just works". It does not means that the keymap is linked to the functionality. For that it is often necessary to add a keyboard shortcut [by the method of your choice](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg") or to use a desktop shell with built-in shortcut support for the keycode in question. For some of the keys the function operates on a BIOS level and no shortcut is needed.

This table shows the function keys, their intended function, what keycode (if any) X recognizes and whether the function key operates at the BIOS level or if it needs a shortcut.

| Keys | Function | X sees | shortcut needed |
| `Fn+F1` | Sleep | XF86Sleep | no |
| `Fn+F2` | Turn off WLAN and Bluetooth | XF86WLAN & XF86Bluetooth | no |
| `Fn+F3` | Dim keyboard backlight | XF86KbdBrightnessDown | yes |
| `Fn+F4` | Brighten keyboard backlight | XF86KbdBrightnessUp | yes |
| `Fn+F5` | Dim LCD backlight | XF86MonBrightnessDown | no |
| `Fn+F6` | Brighten LCD backlight | XF86MonBrightnessUp | no |
| `Fn+F7` | Turn off LCD | No named key | no |
| `Fn+F8` | Toggle display | XF86Display | yes |
| `Fn+F9` | Toggle touchpad | XF86TouchpadToggle | yes |
| `Fn+F10` | Audio mute/unmute | XF86AudioMute | yes |
| `Fn+F11` | Audio volume down | XF86AudioLowerVolume | yes |
| `Fn+F12` | Audio volume up | XF86AudioRaiseVolume | yes |
| `Fn+a` | Ambient light sensor | m:0x0 + c:248 | yes |
| `Fn+c` | Switch display profiles | XF86Launch1 | yes |
| `Fn+v` | Webcam | XF86WebCam | yes |
| `Fn+space` | Switch power profiles | XF86Launch6 | yes |

### Screen backlight

Screen backlight should work with any recent kernel (after 3.7). The brightness is managed via hardware, so it should work across all DE's.

### Keyboard backlight

Keyboard backlight should work automatically with any recent kernel. Desktop environments that use UPower, like GNOME or KDE, work out the box and don't need any tool or script to register the keys and change the keyboard brightness.

#### Manually setting the brightness

The easiest way to change the keyboard brightness is to use the UPower D-Bus interface. This even works without root.

```
 # Get current brightness
 dbus-send --type=method_call --print-reply=literal --system --dest="org.freedesktop.UPower" /org/freedesktop/UPower/KbdBacklight org.freedesktop.UPower.KbdBacklight.GetBrightness
 # Set brightness to 2
 dbus-send --type=method_call --print-reply=literal --system --dest="org.freedesktop.UPower" /org/freedesktop/UPower/KbdBacklight org.freedesktop.UPower.KbdBacklight.SetBrightness int32:2

```

You can also control the brightness of the keyboard backlight through the `brightness` file in `/sys/class/leds/asus::kbd_backlight/` or `/sys/devices/platform/asus-nb-wmi/leds/asus::kbd_backlight/` by writing a value to it. This needs root. You can retrieve the maximum from `max_brightness`:

```
# get maximum brightness value
cat /sys/class/leds/asus::kbd_backlight/max_brightness
```
 `3` 
```
# set to a particular value:
echo 2 > /sys/class/leds/asus::kbd_backlight/brightness
```

#### Using asus-kbd-backlight from AUR

[asus-kbd-backlight](https://aur.archlinux.org/packages/asus-kbd-backlight/) from the AUR is a convenient way to manage the backlight brightness, if one doesn't want to use UPower. To allow users to change the brightness, write:

```
# asus-kbd-backlight allowusers

```

Users of [systemd](/index.php/Systemd "Systemd") can use the unit file included in the package.

```
# systemctl daemon-reload
# systemctl start asus-kbd-backlight.service
# systemctl enable asus-kbd-backlight.service

```

Now you can easily change keyboard backlight in terminal:

```
$ asus-kbd-backlight up
$ asus-kbd-backlight down
$ asus-kbd-backlight max
$ asus-kbd-backlight off
$ asus-kbd-backlight night
$ asus-kbd-backlight 2
$ asus-kbd-backlight show

```

You can then set the XF86KbdBrightnessDown and XF86KbdBrightnessUp keys to the above functions. See [Extra keyboard keys in Xorg](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

#### Ambient Light Sensor (ALS)

The Zenbook has an ambient light sensor which enables adjustment of the keyboard and LCD backlights based on the light environment in which the Zenbook finds itself. The AUR contains packages to build the necessary kernel module and userspace programs to change keyboard and backlights and to turn the sensor on and off. The kernel module package is [als-driver-git](https://aur.archlinux.org/packages/als-driver-git/) and the userspace programs in [als-controller-git](https://aur.archlinux.org/packages/als-controller-git/).

##### ALS Driver

The ALS driver is a module named `als`. The resulting device is represented in sysfs in the directory `/sys/bus/acpi/devices/ACPI0008:00`. The ambient light sensor is enabled by writing a "1" to the file `enable`:

```
# echo "1" > /sys/bus/acpi/devices/ACPI0008:00/enable

```

However, it is better to use the userspace controller described below. Note that the module will need to be rebuilt with every kernel update.

If the sensor is not visible at `/sys/bus/acpi/devices/ACPI0008:00`, you should set `acpi_osi='!Windows 2012'` at the end of `GRUB_CMDLINE_LINUX_DEFAULT` in `/etc/default/grub` and then rebuild `sudo grub-mkconfig -o /boot/grub/grub.cfg` and reboot.

##### ALS Controller

The `als-controller` package will build the als-controller program and an example userspace script. The als-controller program is installed as `/usr/share/als-controller/service/als-controller`. If the programs is run as root and without parameters it will start the als-controller daemon and create a pidfile and socket for it in `/var/run`:

```
# /usr/share/als-controller/service/als-controller

```

The als can then be enabled and disabled by running als-controller as an unprivileged user with the appropriate parameter ( `-e` or `-d`. To enable:

```
$ /usr/share/als-controller/service/als-controller -e

```

and to disable

```
$ /usr/share/als-controller/service/als-controller -d

```

The project, which seems to be Ubuntu-centric, doesn't yet include a systemd service file. I use the following (overly verbose) one:

```
[Unit]
Description=Ambient Light Sensor Daemon

[Service]
User=root
Group=root
PIDFile=/var/run/als-controller.pid
ExecStart=/usr/share/als-controller/service/als-controller
Restart=on-failure

[Install]
WantedBy=multi-user.target

```

##### Sample Script

The sample userspace script is installed as `/usr/share/als-controller/example/switch.sh`. The script is designed to be run by being bound to a key combination. It requires that `libnotify` be installed to have OSD confirmation of state change appear. If you wish to bind enabling/disabling to the same [Fn]+[a] combination as in Windows, the relevant keycode under X is 248\. If you are using `xbindkeys`, add the following to your `.xbindkeysrc` file:

```
# Ambient Light Sensor (ALS) Toggle [Fn a]
"/usr/share/als-controller/example/switch.sh"
m:0x0 + c:248

```

More information can be found in the project's [README](https://github.com/danieleds/Asus-Zenbook-Ambient-Light-Sensor-Controller/blob/e0f0f07a99aca7483d3f7f8056cae9a61f47dac3/README.md) file.

## Solid State Drive

If you're using a SSD, make sure to read [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives").

## Graphics

To use the Intel graphics card, install the xf86-video-intel package and read [Intel graphics](/index.php/Intel_graphics "Intel graphics"). For hardware accelerated video read [Hardware video acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

## Touchpad

[Instructions to activate the right button](/index.php/Touchpad_Synaptics#Buttonless_touchpads_.28aka_ClickPads.29 "Touchpad Synaptics"). (As an alternative you cant try [This](http://ubuntuforums.org/showpost.php?p=12110689&postcount=73)).

Multifinger taps work out of the box.

**Tip:** Multifinger taps: Two finger for middle click; three fingers for right click.

### Multitouch gestures

To enable multitouch gestures like those under Windows, one can install [touchegg](https://aur.archlinux.org/packages/touchegg/) from the AUR. Using `touchegg` will require disabling some input-handling that is done by the synaptics input driver. Edit your `/etc/X11/xorg.conf.d/10-synaptics.conf`

```
Section "InputClass"
        Identifier "touchpad catchall"
        Driver "synaptics"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Option "TapButton1" "1"
        Option "TapButton2" "0"
        Option "TapButton3" "0"
        Option "ClickFinger2" "0"
        Option "ClickFinger3" "0"
        Option "HorizTwoFingerScroll" "0"
        Option "VertTwoFingerScroll" "0"
        Option "ClickPad" "true"
        Option "EmulateMidButtonTime" "0"
        Option "SoftButtonAreas" "50% 0 82% 0 0 0 0 0"
EndSection

```

An alternative to X.org configuration files is to use the `synclient` command within the `.xinitrc` script. This method will limit changes to your desktop environment.

```
 synclient TapButton2=0 TapButton3=0 ClickFinger2=0 ClickFinger3=0 HorizTwoFingerScroll=0 VertTwoFingerScroll=0

```

`touchegg` will need to be autostarted for multitouch gestures to be activated. This can be done with `touchegg &` in your `.xinitrc`, or using the autostart/startup applications functionality of your desktop environment. `~/.config/touchegg/touchegg.conf` can then be configured as necessary.

### Multi-tap, two-finger scrolling doesn't work

Check "xinput list" and see whether the Elantech touchpad was recognized as an Elantech Click-pad. If so, brenix's comment in [psmouse-elantech AUR](https://aur.archlinux.org/packages/psmouse-elantech/) fixed it for me.

### Multitouch gestures in Gnome 3

GNOME 3's gnome-shell does its own mouse-handling, which can interfere with synaptics and touchegg settings unless the appropriate plugin is disabled.

```
 gsettings set org.gnome.settings-daemon.plugins.mouse active false

```

Note that disabling this plugin will cause the the current settings within the Mouse & Touchpad section of System Settings to be ignored.

### Disable Touchpad While Typing

One of the criticisms this laptop gets (see reviews at Amazon) is that the placement of the touchpad results in frequent touchpad brushing during typing. You should use whatever touchpad disabling method you prefer. See [Touchpad Synaptics#Disable touchpad while typing](/index.php/Touchpad_Synaptics#Disable_touchpad_while_typing "Touchpad Synaptics").

## HDMI plugged at boot

There seems to be a problem whereby having an HDMI device plugged in at boot results in the screens being switched and also the laptop screen not coming on. To make this more bearable you can automate switching HDMI on with the following udev rule and script:

Add the following script as root:

 `/usr/local/share/hdmi-plugged-startup` 
```
#!/bin/bash

export XAUTHORITY=/home/$USER/.Xauthority
export DISPLAY=:0

/usr/bin/xrandr -display :0 --output eDP1 --auto --output HDMI1 --auto --above eDP1
```

then make it executable

```
# chmod +x /usr/local/share/hdmi-plugged-startup

```

And add the following udev rule:

```
# echo 'ACTION=="change", SUBSYSTEM=="drm", RUN+="/usr/local/share/hdmi-plugged-startup"' >> /etc/udev/rules.d/10-local.rules

```

Suspending, unplugging the HDMI cable, and resuming is a way to enable the Zenbook's screen without rebooting if it was booted with the cable plugged in.

## Powersave management

To configure some power saving options and tools, see [Power saving](/index.php/Power_saving "Power saving").

## Hardware and Modules

#### Devices

| Description | Device Id | Driver/Module |
| Intel Corporation 3rd Gen Core processor DRAM Controller | 8086:0154 | ivb_uncore |
| Intel Corporation 3rd Gen Core processor Graphics Controller | 8086:0166 | i915 |
| Intel Corporation Device | 8086:0153 | none |
| Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller | 8086:1e31 | xhci_hcd |
| Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 | 8086:1e3a | mei_me |
| Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 | 8086:1e2d | ehci_hcd |
| Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller | 8086:1e20 | snd_hda_intel |
| Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 | 8086:1e10 | pcieport |
| Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 | 8086:1e12 | pcieport |
| Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 | 8086:1e26 | ehci_hcd |
| Intel Corporation HM76 Express Chipset LPC Controller | 8086:1e59 | lpc_ich |
| Intel Corporation 7 Series Chipset Family 6-port SATA Controller | 8086:1e03 | ahci |
| Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller | 8086:1e22] | i2c_i801 |
| Intel Corporation 7 Series/C210 Series Chipset Family Thermal Management Controller | 8086:1e24 | none |
| Intel Corporation Centrino Advanced-N 6235 | 8086:088e | iwlwifi |
| Chicony Electronics Co., Ltd Asus 720p CMOS webcam | 04f2:b330 | uvcvideo |
| Intel Corporation [Bluetooth Device] | 8087:07da | btusb |
| Realtek Semiconductor Corp. RTS5139 Card Reader Controller | 0bda:0139 | rtsx_usb |

#### Other Devices and Drivers

##### MEI

If you know what you are doing and want to use the i7 MEI, you need the Intel Local Manageability Service. You can find it as [intel-lms](/index.php/AUR "AUR") in the AUR.

##### watchdog

The chipset also has an hardware watchdog:

```
root@asarum chris]# wdctl
Device:        /dev/watchdog
Identity:      iTCO_wdt [version 0]
Timeout:       30 seconds
Timeleft:       2 seconds
FLAG           DESCRIPTION               STATUS BOOT-STATUS
KEEPALIVEPING  Keep alive ping reply          0           0
MAGICCLOSE     Supports magic close char      0           0
SETTIMEOUT     Set timeout (in seconds)       0           0

```

Activating the watchdog under systemd is trivial, as systemd author Lennart Poettering explains in [this blog post](http://0pointer.de/blog/projects/watchdog.html).

All you do is go into /etc/systemd/system.conf, uncomment the RuntimeWatchdogSec=0 line and change zero to how long the watchdog should go without receiving a ping before it reboots the system. I used 30s, which is the default setting for iTCO_wdt and seemed sane.

```
#RuntimeWatchdogSec=0
RuntimeWatchdogSec=30

```

Check after next boot:

```
[root@asarum chris]# journalctl | grep -i watchdog
Oct 06 06:36:27 asarum kernel: iTCO_wdt: Intel TCO WatchDog Timer Driver v1.10
Oct 06 06:36:27 asarum systemd[1]: Hardware watchdog 'iTCO_wdt', version 0
Oct 06 06:36:27 asarum systemd[1]: Set hardware watchdog to 30s.

```

#### Problem with ACPI and gpio_ich

The gpio_ich module causes the following error:

```
ACPI Warning: 0x0000000000000428-0x000000000000042f SystemIO conflicts with Region \PMIO 2 (20120711/utaddress-251)
ACPI Warning: 0x0000000000000500-0x000000000000053f SystemIO conflicts with Region \GPIO 1 (20120711/utaddress-251)
ACPI Warning: 0x0000000000000500-0x000000000000053f SystemIO conflicts with Region \GP01 2 (20120711/utaddress-251)
lpc_ich: Resource conflict(s) found affecting gpio_ich
ACPI Warning: 0x000000000000f040-0x000000000000f05f SystemIO conflicts with Region \SMB0 1 (20120711/utaddress-251)
ACPI Warning: 0x000000000000f040-0x000000000000f05f SystemIO conflicts with Region \_SB_.PCI0.SBUS.SMBI 2 (20120711/utaddress-251)

```

This is just a warning that the ACPI has reserved some memory regions for other use. Nothing to worry about!

## Additional resources

*   [https://help.ubuntu.com/community/AsusZenbookPrime](https://help.ubuntu.com/community/AsusZenbookPrime)
*   [http://ubuntuforums.org/showthread.php?t=2005999](http://ubuntuforums.org/showthread.php?t=2005999)
*   [Wikipedia:Zenbook#UX32.2C UX42 and UX52](https://en.wikipedia.org/wiki/Zenbook#UX32.2C_UX42_and_UX52 "wikipedia:Zenbook")