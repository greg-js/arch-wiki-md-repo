**Note:** This page refers to the 9550 variant of the XPS 15\. This is identical to the Dell Precision 5510 but without a Nvidia Quadro 1000m card

| **Device** | **Status** | **Modules** |
| Video | Modify | i915, nvidia |
| Wireless | Working | brcmfmac |
| Bluetooth | Modify | bluez bluez-utils |
| Audio | Working | snd_hda_intel |
| Touchpad | Modify | libinput libinput-gestures |
| Webcam | Working |  ? |
| Card Reader | Working | rtsx_pci |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Modify |  ? |
| Power Management | Buggy | ... |

This page covers the current status of hardware support on Arch, pre-installation system configuration tweaks, as well as post-installation recommendations to improve the usability of the system.

The installation process for Arch on the XPS 15 9550 does not differ from any other PC. For installation help please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). To set up a dual boot configuration with Windows, refer to [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

As of kernel 4.3, the Intel Skylake architecture is supported.

## Contents

*   [1 Pre-Installation System Settings](#Pre-Installation_System_Settings)
*   [2 Boot Parameters](#Boot_Parameters)
*   [3 Graphics Configuration](#Graphics_Configuration)
    *   [3.1 Intel Only](#Intel_Only)
    *   [3.2 Optimus Configuration (Hybrid Intel and Nvidia)](#Optimus_Configuration_.28Hybrid_Intel_and_Nvidia.29)
*   [4 Touchpad](#Touchpad)
    *   [4.1 Gestures](#Gestures)
*   [5 Keyboard](#Keyboard)
*   [6 Power Management](#Power_Management)
    *   [6.1 Suspend & Hibernate](#Suspend_.26_Hibernate)
    *   [6.2 Battery](#Battery)
*   [7 Bluetooth](#Bluetooth)
*   [8 Thunderbolt 3 Docks](#Thunderbolt_3_Docks)
*   [9 USB-C / Thunderbolt 3 Compatibility Chart](#USB-C_.2F_Thunderbolt_3_Compatibility_Chart)

## Pre-Installation System Settings

Prior to installation, access the system UEFI firmware by pressing F2 during boot.

*   Turn off legacy ROM
*   System -> SATA: change to AHCI
*   Secure Boot: disable
*   POST Behavior: Fastboot: Thorough

[Source](https://ahxxm.com/151.moew/#prepare)

Installation of Arch can proceed normally. Refer to the [Installation guide](/index.php/Installation_guide "Installation guide") for more info.

## Boot Parameters

Use the following for your [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") to fix a number of issues:

`i915.edp_vswing=2 i915.preliminary_hw_support=1 intel_idle.max_cstate=1 acpi_backlight=vendor acpi_osi=Linux`

| **Parameter** | **Function** |
| `i915.edp_vswing=2` | Fix screen flickering |
| `i915.preliminary_hw_support=1` | Resolve issues with Intel Graphics |
| `intel_idle.max_cstate=1` | Prevent CPU from entering [c-states](https://gist.github.com/wmealing/2dd2b543c4d3cff6cab7) > 1 |
| `acpi_backlight=vendor acpi_osi=Linux` | make [Backlight](/index.php/Backlight "Backlight") control work |

[Source 1](https://blog.spirotot.com/2016/08/11/xps-9550-arch-linux-fix-screen-flickering), [Source 2](https://bbs.archlinux.org/viewtopic.php?pid=1576380#p1576380)

## Graphics Configuration

The Dell XPS 15 9550 has Intel HD Graphics 530 integrated graphics, and some models have a Nvidia GeForce GTX 960 dedicated card as well in a hybrid configuration.

For computers with only integrated graphics, just install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver.

If your XPS has a hybrid graphics configuration (GTX960M + HD Graphics 530) and you want to maximize battery life you can just use the Intel Graphics.

### Intel Only

If your model comes with an nVidia card which you don't use then you can try to disable it with an ACPI command. Depending on the model, this can have a small to profound effect on the laptop's temperature and battery life (it can more than double battery life!)

*   Install the Intel video driver using the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package.
*   Blacklist the `nvidia` & `nouveau` modules [Kernel modules#Blacklisting](/index.php/Kernel_modules#Blacklisting "Kernel modules")
*   Power down the GPU [with an ACPI command](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics")

### Optimus Configuration (Hybrid Intel and Nvidia)

The [Optimus](/index.php/Optimus "Optimus") setup consists of the integrated Intel chip connected to the laptop screen and the Nvidia card runs through this. As such, the Nvidia chip cannot be used without the Intel chip (some other laptops have the option in BIOS to turn Intel off and use just Nvidia, but not this laptop). See the [Bumblebee](/index.php/Bumblebee "Bumblebee") page set of instructions, particularly the [Bumblebee#Installation](/index.php/Bumblebee#Installation "Bumblebee") Intel/Nvidia section. The main thing to note is that installing both the Intel and Nvidia packages at once tends to avoid dependency issues. The correct driver for the Nvidia card is [nvidia](https://www.archlinux.org/packages/?name=nvidia).

## Touchpad

By default the touchpad does not respond to tap input or two finger scrolling. You can change the behavior by installing [Libinput](/index.php/Libinput "Libinput") and adding `30-touchpad.conf` to `/etc/X11/xorg.conf.d`:

```
 Section "InputClass"
     Identifier "MyTouchPad"
     MatchIsTouchpad "on"
     Driver "libinput"
     Option "Tapping" "on"
     Option "Natural Scrolling" "on"
 EndSection

```

[Source](https://ahxxm.com/151.moew#touchpad-tap-as-click-and-natural-scroll)

### Gestures

You can configure custom gestures using the [libinput-gestures](https://aur.archlinux.org/packages/libinput-gestures/) package. You can follow the instructions from the [documentation](https://github.com/bulletmark/libinput-gestures#readme). Below is a sample configuration file that one might use with this tool:

```
 # ~/.config/libinput-gestures.conf

 # Go back/forward in chrome
 gesture: swipe right 3 xdotool key Alt+Left
 gesture: swipe left 3 xdotool key Alt+Right

 # Zoom in / Zoom out
 gesture: pinch out xdotool key Ctrl+plus
 gesture: pinch in xdotool key Ctrl+minus

 # Switch between desktops
 gesture: swipe left 4 xdotool set_desktop --relative 1
 gesture: swipe right 4 xdotool set_desktop --relative -- -1

```

## Keyboard

The special touch keys are strangely mapped by default. One changes brightness, one does next track. They seem to be linked to the same key sequences as the Fn+F# keys that do the same job. To fix this, make this new file:

 `/opt/dell_touchkeys_keymap` 
```
0x90 previoussong # Previous song
0xA2 playpause # Play/Pause
0x99 nextsong # Next song
0xDB computer # First touch key, Dell apparently uses a key sequence here where 0xDB is a modifer, 0x2D stands for the touch key and 0x19 for the monitor toggle
0x85 prog1 # Second touch key
0x84 media # Third touch key

```

and add this to /etc/rc.local:

 `/etc/rc.local` 
```
…
# Fix touch keys
/usr/lib/udev/keymap input/event0 /opt/dell_touchkeys_keymap

```

[Source](https://bbs.archlinux.org/viewtopic.php?id=131886)

## Power Management

### Suspend & Hibernate

Suspend works without issues, however Hibernation is not completely stable. Write the following to `/etc/systemd/sleep.conf`:

```
 [Sleep]
 HibernateState=disk
 HibernateMode=shutdown

```

### Battery

Battery life can be improved by installing [powertop](https://www.archlinux.org/packages/?name=powertop) and calibrating it. See [Powertop](/index.php/Powertop "Powertop") for more info. To further improve the battery life, you can disable the touchscreen in the BIOS.

## Bluetooth

Bluetooth is disabled by default. If you wish to use Bluetooth you'll need to install some firmware. See [Bluetooth](/index.php/Bluetooth "Bluetooth") for details.

## Thunderbolt 3 Docks

It is possible to get video, audio, Ethernet and USB devices working by updating your BIOS to version >=1.2.19 and disabling Thunderbolt security in your bios settings. If you don't disable Thunderbolt security, then only video and power will work (at lest on the Dell TB16 dock).

You can update your bios either [manually](http://www.dell.com/support/article/hr/en/hrdhs1/SLN171755/en) or by using fwupdmgr although if you installed arch by just bundling everything into /boot as some guides suggest then your only option is to update manually util this [issue](https://github.com/rhinstaller/fwupdate/issues/58) is resolved.

## USB-C / Thunderbolt 3 Compatibility Chart

| **Device** | **Ports** | **Status** |
| [StarTech TBT3TBTADAP Thunderbolt 3 to Thunderbolt Adapter](https://www.amazon.com/StarTech-com-Thunderbolt-Adapter-Compatible-DisplayPort/dp/B019FPJDQ2) | Thunderbolt 2, Thunderbolt | Working |
| [Apple Thunderbolt 3 (USB-C) to Thunderbolt 2 Adapter](https://www.apple.com/shop/product/MMEL2AM/A/thunderbolt-3-usb-c-to-thunderbolt-2-adapter) | Thunderbolt 2, Thunderbolt | Not Working |
| [https://www.amazon.co.uk/DisplayPort-CHOETECH-Thunderbolt-Compatible-ChromeBook/dp/B01N5RFAI4](https://www.amazon.co.uk/DisplayPort-CHOETECH-Thunderbolt-Compatible-ChromeBook/dp/B01N5RFAI4) CHOETECH USB-C to DisplayPort Cable (4K@60Hz)] | DisplayPort | Working |

[This chart](https://wiki.archlinux.org/index.php/Dell_XPS_13_(9360)#USB-C_Compatibility_Chart) may also be helpful.