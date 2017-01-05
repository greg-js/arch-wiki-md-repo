[HP ENVY TouchSmart 17-j113tx](http://support.hp.com/us-en/product/HP-ENVY-TouchSmart-17-j100-Notebook-PC-series/5425742/model/6663758) is a laptop computer model capable of running ArchLinux.

## Contents

*   [1 System Components](#System_Components)
    *   [1.1 Processor](#Processor)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Audio](#Audio)
    *   [1.4 Mass Storage](#Mass_Storage)
    *   [1.5 Power](#Power)
*   [2 I/O Components](#I.2FO_Components)
    *   [2.1 Display](#Display)
    *   [2.2 Camera](#Camera)
    *   [2.3 Sound Playback](#Sound_Playback)
    *   [2.4 Sound Capture](#Sound_Capture)
    *   [2.5 Networking](#Networking)
    *   [2.6 Keyboard](#Keyboard)
    *   [2.7 Pointer](#Pointer)
    *   [2.8 Serial Bus](#Serial_Bus)
    *   [2.9 Security](#Security)
*   [3 Software Components](#Software_Components)
    *   [3.1 Booting](#Booting)
    *   [3.2 Installation](#Installation)

## System Components

### Processor

 `% lscpu` 
```
CPU op-mode(s): 32-bit, 64-bit
    Model name: Intel(R) Core(TM) i7-4700MQ CPU @ 2.40GHz
   CPU max MHz: 3400.0000
      L3 cache: 6144K
```

Works without intervention. Recommend to use x86_64 architecture and enable [Intel microcode updates](/index.php/Microcode "Microcode").

### Graphics

 `% lspci`  `VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller` 

Works successfully with [Intel graphics](/index.php/Intel_graphics "Intel graphics"), using either **xf86-video-intel** or modesetting.

 `            3D controller: NVIDIA Corporation GK208M [GeForce GT 740M]` 

This is a [hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics") setup using [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"), and works successfully with [Bumblebee](/index.php/Bumblebee "Bumblebee") and [PRIME](/index.php/PRIME "PRIME").

Either [Nouveau](/index.php/Nouveau "Nouveau") or the proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") packages can be used, noting that the proprietary package currently offers better performance and results.

### Audio

 `% aplay -l`  `HDMI [HDA Intel HDMI], HDMI 0 [HDMI 0]` 

Not (yet) tested.

 `PCH [HDA Intel PCH], 92HD91BXX Analog [92HD91BXX Analog]` 

Basic functionality works with the **snd_hda_intel** kernel module.

### Mass Storage

 `% lsblk` 
```
NAME          RM   SIZE TYPE TRAN
sda            0 931.5G disk sata
sdb            0 931.5G disk sata
```

HDDs. [Hpfall](/index.php/Hpfall "Hpfall") or [freefall](https://aur.archlinux.org/packages/freefall/) are theoretically compatible, however as at early 2015:

*   The unit had not been 'dropped' to confirm actual functionality.
*   Either package only allowed one device to be specified for protection.
*   Asynchronous loading through [Udev](/index.php/Udev "Udev") means that the device being protected may change between reboots.

There is an HDD activity LED, which shows activity for both HDDs.

 `sr0            1        rom  sata` 

[Optical disc drive](/index.php/Optical_disc_drive "Optical disc drive") capable of both reading and writing CDs, DVDs and [BDs](/index.php/BluRay "BluRay"). Reading of data CDs and data DVDs is confirmed to work; reading of other disc types and disc writing has not (yet) been tested.

* * *

**Note:** A memory card slot is also present, however it has not (yet) been tested.

### Power

[Power management](/index.php/Power_management "Power management") -- including AC and Battery Status, Sleep and Hibernate -- works successfully without special intervention under [systemd](/index.php/Systemd "Systemd")+UPower.

Battery status and power status LEDs both work, but are on opposite sides of the laptop.

## I/O Components

### Display

 `% xrandr`  `eDP1 1920x1080+0+0 381mm x 214mm` 

Integrated display works successfully, at preferred resolution and without intervention, under [Xorg](/index.php/Xorg "Xorg") ([Wayland](/index.php/Wayland "Wayland") has not yet been tested). Automatically set console resolution is acceptable.

A switch is present for lid-closed/lid-open events, and lid-closed operation is possible.

**HDMI port:** An external display can be driven successfully up to the same resolution under the same conditions, with both mirroring and extended desktop modes.

 `% xinput` 
```
⎡ Virtual core pointer
⎜   ↳ eGalax Inc. eGalaxTouch
```

The integrated display includes a [Touchscreen](/index.php/Touchscreen "Touchscreen"). Basic (single-touch) gestures work successfully without intervention. Some complex (multi-touch) gestures could be made to work as at early 2015 with a combination of [Touchegg](/index.php/Touchegg "Touchegg") and the proprietary [xf86-input-egalax](https://aur.archlinux.org/packages/xf86-input-egalax/) package.

**Note:** When working with the laptop lid closed, the touchscreen sends spurious touch events. It is recommended to disable touchscreen input when the lid is closed and re-enable it when the lid is opened (using e.g. `xinput --disable` and `xinput --enable` respectively). Touchscreen calibration has not (yet) been tested.

### Camera

 `% lsusb`  `Realtek Semiconductor Corp. HP "Truevision HD" laptop camera` 

Integrated [webcam](/index.php/Webcam "Webcam"). Works successfully with Video4Linux2\. Activity LED shows when camera is active.

### Sound Playback

The laptop has integrated 4.1 speakers. Stereo sound works successfully from the front two speakers without intervention under [ALSA](/index.php/ALSA "ALSA").

The other speakers are not recognised or used by default; they can be mapped using the `hdajackretask` utility from the [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) package, and it appears the correct combination is the same as for other contemporary HP ENVY models listed in ArchWiki:

| **Pin ID** | **Override Mapping** |
| 0x0d | Internal speaker |
| 0x0f | Internal speaker (Back) |
| 0x10 | Internal speaker (LFE) |

**Audio Jack port:** This is a combined analog audio-out/audio-in port. Audio out to speakers works, with the integrated speakers deactivated upon plug-in.

* * *

**Note:** The laptop also emits [PC Speaker Beep](/index.php/Disable_PC_speaker_beep "Disable PC speaker beep") and automatically loads the **pcspkr** module, although whether a separate speaker is actually present for this is unknown.

### Sound Capture

The laptop has integrated dual microphones. Basic capture from these microphones works successfully under [ALSA](/index.php/ALSA "ALSA"); more advanced capture features have not (yet) been tested.

**Audio Jack port:** This is a combined analog audio-out/audio-in port. Audio in has not (yet) been tested.

### Networking

 `% lspci`  `Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller` 

Working successfully with [wired network configuration](/index.php/Wired_network_configuration "Wired network configuration") using the **r8169** kernel module.

**RJ-45 Ethernet port:** Link and activity LEDs operate when connected and are adjacent to the port itself.

 ` Network controller: Intel Corporation Wireless 7260` 

Working successfully with [wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") using the **iwlwifi** kernel module. The antennae are in the integrated display and give acceptable reception.

 `% lsusb`  `Intel Corp.` 

[Bluetooth](/index.php/Bluetooth "Bluetooth") transceiver. As at early 2015, works successfully with the standard bluetooth software stack; pairing to one device, with limited testing of multimedia and file transfer modes, showed no difficulties.

### Keyboard

Integrated keyboard is standard 'US' layout, and works successfully in this configuration. The 'Windows' key is correctly mapped as a [Meta] key.

The integrated numeric keypad is dual-function, and defaults to scrolling actions unless [Num Lock] is enabled. There is no [Scroll Lock] key and there is no indicator light for [Num Lock].

The integrated Function keys are also dual-function, and default to either system control actions or assigned Functions depending on what is configured in the Firmware Setup Utility (reversible at runtime by using the [Fn] key in combination). The system control actions are:

| **Key(s)** | **Cotrol Action** | **Status (assuming appropriate software)** |
| F1 | [Meta]+[F1] | No hardware action by default, but may trigger a software action (meant to be a 'Help' key under Windows). |
| F2, F3 | Monitor Brightness Down/Up | Works for integrated display. |
| F4 | [Meta]+[P] | No hardware action by default, but may trigger a software action (meant to switch video output under Windows). |
| F5 | Not captured (activates and deactivates the keyboard backlight, which appears to be hardware controlled). |
| F6, F7, F8 | Volume Mute/Down/Up | Works, including the LED that shows when volume is muted. |
| F9, F10, F11 | Media Previous/Play/Next | Works. |
| F12 | Not captured (activates and deactivates Wireless LAN and Bluetooth transceivers, with a LED that changes depending on this state). |

### Pointer

 `% xinput` 
```
⎡ Virtual core pointer
⎜   ↳ SynPS/2 Synaptics TouchPad
```

Works with either [Libinput](/index.php/Libinput "Libinput") or the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") package.

### Serial Bus

The only serial bus present is USB 3.0, with four ports (one of which is a 'charging port'). These work successfully.

### Security

 `% lsusb`  `Validity Sensors, Inc. Swipe Fingerprint Sensor` 

Currently not supported by [Fprint](/index.php/Fprint "Fprint"), according to the project website. The [libfprint-git](https://aur.archlinux.org/packages/libfprint-git/) package may offer some hope, but this has not (yet) been tested on this model.

## Software Components

### Booting

As at November 2014, this model shipped with Windows 8.1, booting in [UEFI](/index.php/UEFI "UEFI")/[GPT](/index.php/GPT "GPT") mode. Secure Boot is enabled by default, but can be disabled through the Firmware Setup Utility.

The firmware on this model respects the EFI Boot Order (use e.g. [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)), so no workarounds are required to boot something else by default.

If dual-booting is wanted, the standard [Windows and Arch dual boot](/index.php/Windows_and_Arch_dual_boot "Windows and Arch dual boot") advice applies. Note that booting Windows 8.1 causes the EFI Boot Order to be reset.

### Installation

Installation was undertaken from optical media using the 2014.11 Arch ISO. No special steps were required for the installation beyond overriding the default EFI Boot Order (which always attempts to boot Windows from HDD first).

All of the volumes important to booting/recovering Windows are located on the first HDD, with the second HDD being extra space for data (it is formatted to NTFS, but otherwise empty). If dual-booting is wanted, the easiest approach is to erase the second HDD and install there.

Alternatively, it is possible to reclaim almost half the capacity of the first HDD by performing a [resize of the volume](/index.php/NTFS-3G#Resizing_NTFS_partition "NTFS-3G") that is the Windows 'C:\' mount, assuming no significant activity has occurred on that volume under Windows.

**Warning:** As always, make sure you take a backup of any important data before erasing or resizing any volumes.