| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | ? |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working | ? |
| Function/Multimedia Keys | Working | ? |
| Fingerprint | Working | (none) |

The Mi Notebook Air 13.3 is an aluminium Ultrabook. It is a product by the Chinese Company Xiaomi and is available in China or Europe through online-shops. Using the [Intel Core i5 8250U](https://ark.intel.com/products/124967/Intel-Core-i5-8250U-Processor-6M-Cache-up-to-3_40-GHz) @ 3.4 GHz and the NVIDIA GeForce MX150, it provides good power for a decent price.

This 2018 global version is hardware updated: new CPU and GPU, as well as a fingerprint reader.

The installation should be going without any problems, if you follow the following steps.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pre-Installation System Settings](#Pre-Installation_System_Settings)
*   [2 Graphics Card Configuration](#Graphics_Card_Configuration)
    *   [2.1 Intel Only](#Intel_Only)
    *   [2.2 Intel/Nvidia Hybrid Configuration](#Intel/Nvidia_Hybrid_Configuration)
*   [3 Input](#Input)
    *   [3.1 Touchpad](#Touchpad)
    *   [3.2 Fn-Keys](#Fn-Keys)
*   [4 Display Calibration](#Display_Calibration)
*   [5 Hardware information](#Hardware_information)
*   [6 Troubleshoothing](#Troubleshoothing)
    *   [6.1 Backlight](#Backlight)
    *   [6.2 WiFi](#WiFi)

## Pre-Installation System Settings

It is actually very easy getting the Arch Installation Medium to boot properly. Prior to booting the Arch installation ISO enter the UEFI menu by pressing F2 during Boot.

*   Security -> set password
*   Security -> Disable Secure Boot
*   reset the password by setting the password again but letting the "New Password" fields blank

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

**Note:** Remember that your SSD is called `nvme0n1`, not `sda`.

## Graphics Card Configuration

The Mi Book has an Intel, as well as a Nvidia GPU.

**Note:** The HDMI port is linked to the Intel chipset, so disabling the nVidia GPU will not need any configuration to use this graphic output.

### Intel Only

If you want to completely disable the Nvidia GPU and save batterylife, do the following:

*   Install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package
*   Blacklist the [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) kernel modules [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")

 `/etc/modprobe.d/nouveau.conf` 
```
blacklist nouveau
blacklist nvidia
```

*   Install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) to [turn off the card](/index.php/Bumblebee#Power_management "Bumblebee")

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=0` 

### Intel/Nvidia Hybrid Configuration

You can enable hybrid GPUs by either using [Bumblebee](/index.php/Bumblebee "Bumblebee") or [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"). Bumblebee is generally better for battery-life and compatibility but not officially supported by NVIDIA.

Refer to the respective articles.

## Input

### Touchpad

To use the touchpad like a normal one, you have to use [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). If you use [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev), your touchpad acts like a touchscreen (e.g it maps your movements directly to your screen). But if you are using [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (although you really should not, because it is deprecated (see [Synaptics](/index.php/Synaptics "Synaptics"))) things are only working sporadically. This configuration of [libinput](https://www.archlinux.org/packages/?name=libinput) using XOrg configuration files enables two finger gestures, tap-to-click and 2-and 3-finger clicks (for right- and middle-click respectively).

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

On this notebook the Fn-keys are enabled as default (e.g. pressing F1 mutes the sound). If pressing the keys does nothing you are most likely using a [Window manager](/index.php/Window_manager "Window manager") and not a [Desktop environment](/index.php/Desktop_environment "Desktop environment"). Use the respective configuration files to bind the keys to their use. For example [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") or [i3](/index.php/I3 "I3")'s `bindsym`.

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

**Note:** The Fn lock (Fn+Esc) is an hardware functionality and cannot be detected with showkey or another key detection tool.

## Display Calibration

Factory display calibration is poor. In lieu of a colorimeter, try the [ICC profiles](/index.php/ICC_profiles "ICC profiles") at [tlvince/xiaomi-mi-notebook-air-13](https://github.com/tlvince/xiaomi-mi-notebook-air-13/tree/master/display-calibration).

## Hardware information

The output of *lspci* is

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Intel(R) 100 Series Chipset Family LPC Controller/eSPI Controller - 9D4E (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 3D controller: NVIDIA Corporation GP108M [GeForce MX150] (rev a1)
02:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
03:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM961/PM961
```

The output of *lsusb* is

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 8087:0a2b Intel Corp. 
Bus 001 Device 004: ID 04f3:0c1a Elan Microelectronics Corp. 
Bus 001 Device 003: ID 04f2:b5a3 Chicony Electronics Co., Ltd 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

## Troubleshoothing

### Backlight

If you use a tool like [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) in its default configuration, nothing happens, because the path to the backlighting variable is not standard. To fix this issue, you have to use a X-Org configuration file:

 `/etc/X11/xorg.conf.d/10-backlight.conf` 
```
Section "Device" 
        Identifier "Card0" 
        Driver     "intel" 
        Option     "Backlight"  "intel_backlight" 
        BusID      "PCI:0:2:0" 
EndSection
```

### WiFi

If you are having issues with the auto-detected WiFi drivers, that is because there is a conflict between two of them, as you can see using `rfkill list` To solve it, block the wrong driver:

 `/etc/modprobe.d/blacklist.conf`  `blacklist acer-wmi` 

Note, this issue is fixed in kernel version 4.9 and above.