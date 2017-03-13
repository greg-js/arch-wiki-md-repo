**Tip:** A great resource for thinkpads is [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Support](#Support)
    *   [1.2 Fingerprint Reader](#Fingerprint_Reader)
*   [2 Configuration](#Configuration)
    *   [2.1 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)
    *   [2.2 Display](#Display)
    *   [2.3 TrackPoint Scrolling](#TrackPoint_Scrolling)

## Model description

Lenovo ThinkPad X1 Carbon, Gen 5.

To ensure you have this version, run *dmidecode*:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 5th

```

### Support

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes |
| Native Ethernet with [Dongle](http://shop.lenovo.com/us/en/itemdetails/4X90F84315/460/D60A78A4A48A422E9761BD184AD3750A) | Yes |
| Mobile broadband |  ?? |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| Camera | Yes |
| Fingerprint Reader | No |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| microSD card reader | Yes |

### Fingerprint Reader

The fingerprint reader included with this model `138a:0097 Validity Sensors, Inc` currently lacks a linux driver. [Community discussion](https://bugs.freedesktop.org/show_bug.cgi?id=94536) of this issue indicates that preliminary efforts to reverse engineer a driver have failed. Synaptics (which has acquired 'Validity Sensors') has unofficially said that they cannot disclose the protocol, but may possibly release a binary driver.

## Configuration

### Keyboard Fn Shortcuts

*   Fn+4 sends XF86Sleep (puts computer to sleep by default)
*   Fn+S sends Alt_L+Sys_Req
*   Fn+P sends Pause
*   Fn+B sends Control_L+Break
*   Fn+K sends Scroll_Lock
*   Fn by itself sends XF86WakeUp (wakes computer from sleep by default)

### Display

There are two options for displays:

*   14" FHD IPS (1920 x 1080): Works
*   14" WQHD (2560 x 1440): ??

### TrackPoint Scrolling

To enable TrackPoint middle-button scrolling, [install](/index.php/Install "Install") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package from the [official repositories](/index.php/Official_repositories "Official repositories") add the following line to your [.xinitrc](https://wiki.archlinux.org/index.php/Xinit).

 `xinput set-prop "ImPS/2 Generic Wheel Mouse" 288 0 0 1`