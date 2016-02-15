[HP ENVY TouchSmart 17-j113tx](http://h10025.www1.hp.com/ewfrf/wc/product?cc=us&lc=en&product=6663757) is a laptop computer model capable of running ArchLinux.

## Contents

*   [1 System Components](#System_Components)
    *   [1.1 Processor](#Processor)
    *   [1.2 Graphics](#Graphics)
    *   [1.3 Audio](#Audio)
    *   [1.4 Mass Storage](#Mass_Storage)
    *   [1.5 Power](#Power)
*   [2 Interactivity Components](#Interactivity_Components)
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

Working without intervention on 3.17/3.18 kernels.

Recommend to use x86_64 architecture and enable [Intel microcode updates](/index.php/Microcode "Microcode").

### Graphics

 `% lspci`  `VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller` 

Working successfully with [Intel graphics](/index.php/Intel_graphics "Intel graphics") package on 3.17/3.18 kernels.

 `            3D controller: NVIDIA Corporation GK208M [GeForce GT 740M]` 

This is a [hybrid graphics](/index.php/Hybrid_graphics "Hybrid graphics") setup using [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus"), and is working successfully with [Bumblebee](/index.php/Bumblebee "Bumblebee") on 3.17/3.18 kernels. Also since tested successfully with [PRIME](/index.php/PRIME "PRIME") and DRI3/Nouveau on 3.19 kernel.

The controller itself is working successfully with either [Nouveau](/index.php/Nouveau "Nouveau") or proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") packages on 3.17/3.18 kernels. The proprietary package currently provides better performance.

### Audio

 `% aplay -l`  `HDMI [HDA Intel HDMI], HDMI 0 [HDMI 0]` 

Not tested at this writing.

 `PCH [HDA Intel PCH], 92HD91BXX Analog [92HD91BXX Analog]` 

Basic functionality is working with the **snd_hda_intel** module provided in the 3.17/3.18 kernels.

### Mass Storage

 `% lsblk` 

```
NAME          RM   SIZE TYPE TRAN
sda            0 931.5G disk sata
sdb            0 931.5G disk sata
```

HDDs. [Hpfall](/index.php/Hpfall "Hpfall") or [freefall](https://aur.archlinux.org/packages/freefall/) are theoretically compatible (and seem to run on 3.18 kernels), however at this writing:

*   The unit has not been 'dropped' to confirm actual functionality.
*   Either package only currently allows one device to be specified for protection.
*   Asynchronous loading through [Udev](/index.php/Udev "Udev") can mean that the device being protected may change between reboots (and if that device is one that doesn't support **unload_heads**, the service will error).

There is an HDD activity LED, which appears to show activity for both HDDs.

 `sr0            1        rom  sata` 

[Optical disc drive](/index.php/Optical_disc_drive "Optical disc drive") capable of both reading and writing CDs, DVDs and [BDs](/index.php/BluRay "BluRay"). Reading of data CDs and data DVDs is working successfully with the relevant packages under 3.17/3.18 kernels; reading of other types of discs or writing discs has not been tested at this time.

* * *

**Note:** A memory card slot is also present, however it has not been tested at this writing.

### Power

[Power management](/index.php/Power_management "Power management") -- including AC and Battery Status, Sleep and Hibernate -- works successfully without special intervention under [systemd](/index.php/Systemd "Systemd")+UPower and 3.17/3.18 kernels.

Battery status and power status LEDs both work, but are on opposite sides of the laptop.

## Interactivity Components

### Display

 `% xrandr`  `eDP1 1920x1080+0+0 381mm x 214mm` 

Integrated display working successfully, at preferred resolution and without intervention, under 1.16 [Xorg](/index.php/Xorg "Xorg") package. Automatically set console resolution is also acceptable.

A switch is present for lid-closed/lid-open events, and lid-closed operation is possible.

**HDMI port:** An external display has been driven successfully up to the same resolution under the same conditions, with both mirroring and extended desktop modes used.

 `% xinput` 

```
⎡ Virtual core pointer
⎜   ↳ eGalax Inc. eGalaxTouch
```

The integrated display includes a [Touchscreen](/index.php/Touchscreen "Touchscreen"). Basic (single-touch) gestures work successfully without intervention. Some complex (multi-touch) gestures could be made to work at this writing with a combination of [Touchegg](/index.php/Touchegg "Touchegg") and the proprietary [xf86-input-egalax](https://aur.archlinux.org/packages/xf86-input-egalax/) package.

**Note:** When working with the laptop lid closed, the touchscreen sends spurious touch events. It is recommended to disable touchscreen input when the lid is closed and re-enable it when the lid is opened (using e.g. `xinput --disable` and `xinput --enable` respectively). Touchscreen calibration has not been tested at this writing.

### Camera

 `% lsusb`  `Realtek Semiconductor Corp. HP "Truevision HD" laptop camera` 

Integrated [webcam](/index.php/Webcam "Webcam"). Working successfully without intervention under Video4Linux2 in the 3.17/3.18 kernels. Activity LED shows when camera is active.

### Sound Playback

The laptop has integrated 4.1 speakers. Stereo sound works successfully from the front two speakers without intervention (under [ALSA](/index.php/ALSA "ALSA") in the 3.17/3.18 kernels).

The other speakers are not recognised or used by default; they can be manipulated using the `hdajackretask` utility from the [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools) package, however the correct combination has not been investigated at this writing.

**Audio Jack port:** This is a combined analog audio-out/audio-in port. Audio out to speakers works successfully, with the integrated speakers deactived upon plug-in.

* * *

**Note:** The laptop also emits [PC Speaker Beep](/index.php/Disable_PC_speaker_beep "Disable PC speaker beep") and audomatically loads the **pcspkr** module, although whether a separate speaker is actually present for this is unknown.

### Sound Capture

The laptop has integrated dual microphones. Basic capture from these microphones works successfully without intervention (under [ALSA](/index.php/ALSA "ALSA") in the 3.17/3.18 kernels) other than installing relevant capture software; more advanced capture features have not been tested at this writing.

**Audio Jack port:** This is a combined analog audio-out/audio-in port. Audio in has not been tested at this writing.

### Networking

 `% lspci`  `Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller` 

Working successfully with [wired network configuration](/index.php/Wired_network_configuration "Wired network configuration") using the **r8169** module in 3.17/3.18 kernels.

**RJ-45 Ethernet port:** Link and activity LEDs operate when connected and are adjacent to the port itself.

 ` Network controller: Intel Corporation Wireless 7260` 

Working successfully with [wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") using the **iwlwifi** module in 3.17/3.18 kernels. The antennae are in the integrated display and give acceptable reception.

 `% lsusb`  `Intel Corp.` 

[Bluetooth](/index.php/Bluetooth "Bluetooth") transceiver, working successfully with the standard blueooth software stack under 3.17/3.18 kernels. Pairing to one device, with limited testing of multimedia and file transfer modes, showed no difficulties.

### Keyboard

Standard 'US' layout keys work successfully without intervention on the integrated keyboard. The 'Windows' key is correctly mapped as a [Meta] key.

The integrated numeric keypad is dual-function, and defaults to scrolling actions unless [Num Lock] is enabled. There is no [Scroll Lock] key and there is no indicator light for [Num Lock].

The integrated Function keys are also dual-function, and default to system control actions rather than assigned Functions (reversed of course by using the [Fn] key in combination). The system control actions are:

| **Key(s)** | **Default Action** | **Status (with software to process the events)** |
| F1 | [Meta]+[F1] | Does nothing by default (meant to be a 'Help' key under Windows). |
| F2, F3 | Monitor Brightness Down/Up | Working for integrated display. |
| F4 | [Meta]+[P] | Does nothing by default (meant to switch video output under Windows). |
| F5 | Not captured (activates and deactives the keyboard backlight, which appears to be hardware controlled). |
| F6, F7, F8 | Volume Mute/Down/Up | Working, including the LED that shows when volume is muted. |
| F9, F10, F11 | Media Previous/Play/Next | Working. |
| F12 | Not captured (activates and deactivates Wireless LAN and Bluetooth transceivers, with a LED that changes depending on this state). |

### Pointer

 `% xinput` 

```
⎡ Virtual core pointer
⎜   ↳ SynPS/2 Synaptics TouchPad
```

Requires the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") package to be installed, then works successfully.

### Serial Bus

The only serial bus present is USB 3.0, with four ports (one of which is a 'charging port'). These work successfully without intervention under the 3.17/3.18 kernels.

### Security

 `% lsusb`  `Validity Sensors, Inc. Swipe Fingerprint Sensor` 

Currently not supported by [Fprint](/index.php/Fprint "Fprint"), according to the project website.

## Software Components

### Booting

As at November 2014, this model shipped with Windows 8.1, booting in [UEFI](/index.php/UEFI "UEFI") mode from a [GPT](/index.php/GPT "GPT") drive. Secure Boot is enabled by default, though it can be disabled through the Firmware Setup Utility.

The firmware on this model respects the EFI Boot Order (configured using e.g. [efibootmgr](https://www.archlinux.org/packages/?name=efibootmgr)), so no workarounds are required to boot something else by default. The only configuration tested so far is [GRUB](/index.php/GRUB "GRUB"), but there is nothing to suggest other [Boot loaders](/index.php/Boot_loaders "Boot loaders") couldn't be used.

If dual-booting is wanted, the standard [Windows and Arch dual boot](/index.php/Windows_and_Arch_dual_boot "Windows and Arch dual boot") advice applies. Booting Windows 8.1 causes the EFI Boot Order to be reset, so you will need to manually activate the desired boot loader on startup to boot back into ArchLinux.

### Installation

You will also need to manually activate the desired boot device on startup for [installation](/index.php/Installation "Installation"), as the default EFI Boot Order places the Windows boot loader first.

Installation was undertaken from optical media using the Arch ISO that was current in November 2014\. No special extra steps were required in order to ensure success, other than those related to booting above.

All of the volumes important to booting/recovering Windows are located on the first HDD, with the second HDD being extra space for data (it is formatted to NTFS, but otherwise empty). If dual-booting is wanted, the obvious approach is to erase the second HDD and install there.

Alternatively, it is possible - and has been tested successfully - to reclaim almost half the capacity of the first HDD by performing a [resize of the volume](/index.php/NTFS-3G#Resizing_NTFS_partition "NTFS-3G") that is the Windows 'C:\' mount, assuming no significant activity has occurred on that volume under Windows.

**Warning:** As always, make sure you take a backup of any important data before erasing or resizing any volumes or disks.