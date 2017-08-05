**Tip:** A great resource for thinkpads is [http://www.thinkwiki.org/wiki/ThinkWiki](http://www.thinkwiki.org/wiki/ThinkWiki)

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Support](#Support)
    *   [1.2 Fingerprint Reader](#Fingerprint_Reader)
    *   [1.3 Bug: Fans blowing at max speed after resuming](#Bug:_Fans_blowing_at_max_speed_after_resuming)
*   [2 Configuration](#Configuration)
    *   [2.1 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)
    *   [2.2 Display](#Display)
    *   [2.3 TrackPoint Scrolling](#TrackPoint_Scrolling)
    *   [2.4 Lenovo ThinkPad Thunderbolt 3 Dockingstation](#Lenovo_ThinkPad_Thunderbolt_3_Dockingstation)
        *   [2.4.1 Ethernet](#Ethernet)
        *   [2.4.2 USB](#USB)
    *   [2.5 HP Thunderbolt 3 Dock](#HP_Thunderbolt_3_Dock)

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
| Mobile broadband | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes |
| Camera | Yes |
| Fingerprint Reader | No |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| microSD card reader | Yes |

### Fingerprint Reader

The fingerprint reader included with this model `138a:0097 Validity Sensors, Inc` currently lacks a linux driver. [libfprint bugreport](https://bugs.freedesktop.org/show_bug.cgi?id=94536). Synaptics (which has acquired 'Validity Sensors') has unofficially said that they cannot disclose the protocol, but may possibly release a binary driver.

Open source Linux driver is being developed by reverse engineering the Windows driver. [[1]](https://github.com/nmikhailov/Validity90)

### Bug: Fans blowing at max speed after resuming

There is a bug in the current kernel, causing the fans to often go on full throttle non-stop after resuming from suspend-to-ram.

**This bug is fixed since the kernel 4.12.4-1.**

Set of patches available for older version: [https://bugzilla.kernel.org/show_bug.cgi?id=196129#c26](https://bugzilla.kernel.org/show_bug.cgi?id=196129#c26)

If you have an older version of the kernel, you need to manually patch the kernel or work around the issue by repeatedly suspend (<kbd>Fn+4</kbd>) and resume (<kbd>Fn</kbd>) until it resumes without the fans starting with a short burst of activity. For me, the issue arises in about 2/3 resumes without the patches and never with kernel 4.12.0-2 with patches.

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
*   14" WQHD (2560 x 1440): Works

### TrackPoint Scrolling

TrackPoint Scrolling is working out of the box in GNOME and MATE. In some WindowManagers, the TrackPoint middle-button scrolling can be enabled by [installing](/index.php/Installing "Installing") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package from the [official repositories](/index.php/Official_repositories "Official repositories") and appending the following line to your [.xinitrc](/index.php/.xinitrc ".xinitrc"):

 `xinput set-prop "ImPS/2 Generic Wheel Mouse" "libinput Scroll Method Enabled" 0 0 1` 

### Lenovo ThinkPad Thunderbolt 3 Dockingstation

The USB-C Dock is a Thunderbolt 3 device. Plugging it in results in a whole lot of PCI entries:

```
06:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:01.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:02.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:04.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
3c:00.0 USB controller: Intel Corporation Device 15d4 (rev 02)

```

The dock works nearly perfect out of the box with Kernel 4.10.13\. Even hot plugging works: unplugging the dock while a display is connected just lets all the devices disappear. Replugging it later works, all the USB devices come back up automagically, thought you might need to issue a xrandr to get the display showing again (tested with Xorg based i3 setup).

#### Ethernet

The r8152 based USB Ethernet Port does not work out of the box. It gives the message:

```
[    7.574773] r8152 4-1.1:1.0 (unnamed net_device) (uninitialized): Unknown version 0x6010

```

Installing [r8152-dkms](https://aur.archlinux.org/packages/r8152-dkms/) fixes this (the DKMS module adds the version 0x6010 to the module).

#### USB

In order for the internal USB hub in the dock to work without having to boot with the dock connected to your computer, you need to set "Security Level" to "No Security" under Thuderbolt settings in BIOS. Also remember to enable the "Support in pre boot environment" for USB peripherals connected to the dock to work at all.

### HP Thunderbolt 3 Dock

The HP Thunderbolt 3 Dock is working out of the box.