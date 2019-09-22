| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | iwlwifi |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | ? |
| Webcam | Working | uvcvideo |
| USB-C / Thunderbolt 3 | Working | ? |
| Function/Multimedia Keys | Working | ? |

The Mi Notebook Air 15.6 is an aluminium notebook. It is a product by the Chinese Company Xiaomi.

The installation should be going without any problems if you follow the following steps.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pre-Installation System Settings](#Pre-Installation_System_Settings)
*   [2 Graphics Card Configuration](#Graphics_Card_Configuration)
    *   [2.1 Intel Only](#Intel_Only)
    *   [2.2 Intel/NVIDIA Hybrid Configuration](#Intel/NVIDIA_Hybrid_Configuration)
*   [3 Input](#Input)
    *   [3.1 Touchpad](#Touchpad)
    *   [3.2 Fn-Keys](#Fn-Keys)
*   [4 Display Calibration](#Display_Calibration)
*   [5 Hardware information](#Hardware_information)
*   [6 Troubleshoothing](#Troubleshoothing)
    *   [6.1 Backlight](#Backlight)

## Pre-Installation System Settings

It is actually very easy getting the Arch Installation Medium to boot properly. Prior to booting the Arch installation ISO enter the UEFI menu by pressing F2 during Boot.

*   Security -> set password
*   Security -> Disable Secure Boot
*   reset the password by setting the password again but letting the "New Password" fields blank

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

**Note:** Remember that your SSD is called `nvme0n1`, not `sda`.

## Graphics Card Configuration

The Mi Book has an Intel, as well as an NVIDIA GPU.

### Intel Only

If you want to completely disable the NVIDIA GPU (which might save batterlife), do the following:

*   Install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package
*   Blacklist the [nvidia](https://www.archlinux.org/packages/?name=nvidia) and [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) kernel modules [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")

 `/etc/modprobe.d/nouveau.conf` 
```
blacklist nouveau
blacklist nvidia
```

*   Install [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) to [turn off the card](/index.php/Bumblebee#Power_management "Bumblebee")

 `/etc/modprobe.d/bbswitch.conf`  `options bbswitch load_state=0 unload_state=0` 

### Intel/NVIDIA Hybrid Configuration

You can enable hybrid GPUs by either using [Bumblebee](/index.php/Bumblebee "Bumblebee") or [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"). Bumblebee is generally better for battery-life and compatibility but not officially supported by NVIDIA.

Refer to the respective articles.

Note that included MX150 GPU does not properly work with VDPAU. It also does not work with NVDECODE and NVENCODE. Thus, video playback works faster and better with Intel's chip with VAAPI on this particular notebook. Even though it supports specifications, this particular GPUs hardware acceleration APIs do not work with the proprietary NVIDIA driver (nouveau needs to be tested). The only benefit of NVIDIA GPU is better performance on high-resolution screens and CUDA/gaming.

While video playback performance is best with Intel VAAPI, battery life is best when relying on CPU for video decoding (as VDPAU/NCDECODE/NVENCODE does not work).

## Input

### Touchpad

To use the touchpad like a normal one, you have to use [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput). If you use [xf86-input-evdev](https://www.archlinux.org/packages/?name=xf86-input-evdev), your touchpad acts like a touchscreen (e.g it maps your movements directly to your screen). But if you are using [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (although you really should not, because it is deprecated (see [Synaptics](/index.php/Synaptics "Synaptics"))) things are only working sporadically. This configuration of [libinput](https://www.archlinux.org/packages/?name=libinput) using XOrg configuration files enables two-finger gestures, tap-to-click and 2-and 3-finger clicks (for right- and middle-click respectively).

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

On this notebook, the Fn-keys are enabled as default (e.g. pressing F1 mutes the sound). If pressing the keys does nothing you are most likely using a [Window manager](/index.php/Window_manager "Window manager") and not a [Desktop environment](/index.php/Desktop_environment "Desktop environment"). Use the respective configuration files to bind the keys to their use. For example [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") or [i3](/index.php/I3 "I3")'s `bindsym`.

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

## Display Calibration

Factory display calibration is poor. Check the panel model:

```
$ edid-decode < /sys/class/drm/card1-eDP-1/edid | grep ASCII

```

If it's NV156FHM-N61, try the [ICC profiles](/index.php/ICC_profiles "ICC profiles") at [[1]](https://www.notebookcheck.net/uploads/tx_nbc2/NV156FHM_N61.icm).

## Hardware information

The output of *lspci* is

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v6/7th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 620 (rev 07)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #0 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller #1 (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #5 (rev f1)
00:1c.7 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #8 (rev f1)
00:1d.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #9 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point LPC Controller/eSPI Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 3D controller: NVIDIA Corporation GP108M [GeForce MX150] (rev a1)
03:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
04:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM961/PM961

```

The output of *lsusb* is

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 04f3:0c1a Elan Microelectronics Corp. ELAN:Fingerprint
Bus 001 Device 004: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 003: ID 05c8:03b7 Cheng Uei Precision Industry Co., Ltd (Foxlink) XiaoMi USB 2.0 Webcam
Bus 001 Device 002: ID 8087:0a2b Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Troubleshoothing

### Backlight

You can adjust brightness directly (works even with `modesetting` driver):

```
# echo 7500 > /sys/class/backlight/intel_backlight/brightness

```

However, if you use a tool like [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) in its default configuration, nothing happens, because the path to the backlighting variable is not standard. To fix this issue, you have to setup Intel driver and add Backlight option to respective X-Org configuration file:

 `/etc/X11/xorg.conf.d/10-backlight.conf` 
```
Section "Device" 
        Identifier "Card0" 
        Driver     "intel" 
        Option     "Backlight"  "intel_backlight" 
        BusID      "PCI:0:2:0" 
EndSection
```