The Mi Notebook Air 13.3 is an aluminuim Ultrabook. It is a product by the Chinese Company Xiaomi and is currently only available in China or through import online-shops. Using the Intel Core i5 6200U @ 2.3 Ghz and the NVIDIA GeForce 940MX, it provides good power for a decent price.

The installation should be going without any problems, if you follow the following steps.

## Contents

*   [1 Pre-Installation System Settings](#Pre-Installation_System_Settings)
*   [2 Grpahic Card Configuration](#Grpahic_Card_Configuration)
    *   [2.1 Intel Only](#Intel_Only)
    *   [2.2 Intel/Nvidia Hybrid Configuration](#Intel.2FNvidia_Hybrid_Configuration)
*   [3 Input](#Input)
    *   [3.1 Touchpad](#Touchpad)
    *   [3.2 Fn-Keys](#Fn-Keys)
*   [4 Troubleshoothing](#Troubleshoothing)
    *   [4.1 Backlight](#Backlight)

## Pre-Installation System Settings

It is actually very easy getting the Arch Installation Medium to boot properly. Prior to booting the Arch installation ISO enter the UEFI menu by pressing F2 during Boot.

*   Security -> set password
*   Security -> Disable Secure Boot
*   reset the password by setting the password again but letting the "New Password" fields blank

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

**Note:** Remember, that your SSD is called `nvme0n1`, not `sda`.

## Grpahic Card Configuration

The Mi Book has an Intel, as well as an Nvidia GPU.

### Intel Only

If you want to completely disable the Nvidia GPU and save batterylife, do the following:

*   Installing the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package
*   Blacklisting the [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) kernel modules [Kernel Modules#Blacklisting](/index.php/Kernel_Modules#Blacklisting "Kernel Modules")

 `/etc/modprobe.d/nouveau.conf` 
```
blacklist nouveau
blacklist nvidia
```

### Intel/Nvidia Hybrid Configuration

You can enable hybrid GPUs by either using [Bumblebee](/index.php/Bumblebee "Bumblebee") or [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"). Bumblebee is generally better for batterylife and compatibility but not oficially supported by NVIDIA.

Refer to the respective articles.

## Input

### Touchpad

To use the touchpad like a normal one, you have to use [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). If you use [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev), your touchpad acts like a touchscreen (e.g it maps your movements directly to your screen). But if you are using [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (What you really shouldn't, because it is deprecated( see [Synaptics](/index.php/Synaptics "Synaptics"))) things are only working sporadicly. This configuration of [libinput](https://www.archlinux.org/packages/?name=libinput) using XOrg configuration files enables two finger gestures, tap-to-click and 2-and 3-finger clicks (for right- and middleclick respectively).

 `/etc/X11/xorg.conf.d/20-touchpad.conf` 
```
Section "InputClass"
        Identifier "libinput touchpad"
        Driver "libinput"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Option "Tapping" "on"
        Option "ClickMethod" "clickfinger"
        Option "NaturalScrolling" "true"
EndSection
```

### Fn-Keys

On this notebook the Fn-keys are enabled as default (e.g. pressing F1 mutes the sound). If pressing the keys does nothing you are most likely using a [Window Manager](/index.php/Window_Manager "Window Manager") and not a [Desktop Environment](/index.php/Desktop_Environment "Desktop Environment"). Use the respective configuration files to bind the keys to their use. For example [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") or [i3](/index.php/I3 "I3")'s `bindsym`.

Most Fn-keys return the correct keycodes. Here is a table containing that information:

| Fn-F-Key | Keycode |
| `F1` | `XF86AudioMute` |
| `F2` | `XF86AudioLowerVolume` |
| `F3` | `XF86AudioRaiseVolume` |
| `F4` | `XF86MonBrightnessDown` |
| `F5` | `XF86MonBrightnessUp` |
| `F6` | `Super_L + P` |
| `F7` | `Nothing` |
| `F8` | `Super_L + Tab` |
| `F9` | `Nothing` |
| `F10` | `Turns Keyboard backlight on/off` |
| `F11` | `Print` |
| `F12` | `Insert` |

## Troubleshoothing

### Backlight

If you use a tool like [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) in its default configuration, nothing happens. To fix this issue, you have to use a X-Org configuration file:

 `/etc/X11/xorg.conf.d/10-backlight.conf` 
```
Section "Device" 
        Identifier "Card0" 
        Driver     "intel" 
        Option     "Backlight"  "intel_backlight" 
        BusID      "PCI:0:2:0" 
EndSection
```