## Contents

*   [1 Installation](#Installation)
*   [2 GPU](#GPU)
    *   [2.1 Detecting Mini Display Port](#Detecting_Mini_Display_Port)
    *   [2.2 Intel HD 4000](#Intel_HD_4000)
    *   [2.3 NVIDIA NVS 5400M](#NVIDIA_NVS_5400M)
*   [3 Input](#Input)
    *   [3.1 Hotkeys (Media Keys)](#Hotkeys_.28Media_Keys.29)
*   [4 Networking](#Networking)
*   [5 Backlight Brightness with the Nvidia driver](#Backlight_Brightness_with_the_Nvidia_driver)
    *   [5.1 Ericsson H5321 GW Mobile Broadband modem](#Ericsson_H5321_GW_Mobile_Broadband_modem)
*   [6 See also](#See_also)

## Installation

See [Installation guide](/index.php/Installation_guide "Installation guide").

## GPU

### Detecting Mini Display Port

When using Nvidia optimus the Display port will not be accessible. To have access to this port go into Bios and change the your GPU to discrete, also change the auto detect OS to false. Restart and you can now access the mini-display port.

See [Bumblebee](/index.php/Bumblebee "Bumblebee"), or disable the dedicated GPU in the BIOS for power-saving.

### Intel HD 4000

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### NVIDIA NVS 5400M

See [Nouveau](/index.php/Nouveau "Nouveau") for open-source driver or [NVIDIA](/index.php/NVIDIA "NVIDIA") for the proprietary driver.

When in discrete graphics mode, The backlight does not work while in UEFI Mode. This limitation does not exist in Legacy Mode.

## Input

### Hotkeys (Media Keys)

Media keys that work out of the box:

*   Wireless On/Off
*   Backlight Brightness (If you use the nVidia driver, configuration will be needed - see below)
*   Thinklight / Keyboard Backlighting
*   Sleep

Keys that do not work out of the box, depending on your DE (you can bind them):

*   Mute
*   Vol+/-
*   Prev/PlayPause/Next
*   Lock
*   Mic Mute (may not register with [xorg-xev](https://www.archlinux.org/packages/?name=xorg-xev))
*   Fn+F7 - Display Toggle (Projector?)
*   Fn+F6 - WebCam Toggle
*   Launcher (right of Mic Mute)

See [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys") for necessary configuration.

## Networking

Both the Ethernet and wireless are supported by Arch out of the box. All the available Intel wireless cards are very well supported, including good powersaving. The Lenovo branded (Realtek) card does not work as well and does not support powersaving on Linux.

## Backlight Brightness with the Nvidia driver

When using the proprietary nvidia driver, it needs to be instructed to take care of brightness control.

 `/etc/X11/xorg.conf.d/10-nvidia-brightness.conf` 
```
Section "Device"
    Identifier     "Device0"
    Driver         "nvidia"
    VendorName     "NVIDIA Corporation"
    BoardName      "GF108M [NVS 5400M]"
    Option         "RegistryDwords" "EnableBrightnessControl=1"
EndSection
```

### Ericsson H5321 GW Mobile Broadband modem

The Mobile Broadband modem may need the following change to be made into module settings so that mobile data starts to work.

 `/etc/modprobe.d/cdc_ncm.conf`  `options cdc_ncm prefer_mbim=N` 

## See also

*   [Technical specifications](https://www.lenovo.com/products/us/tech-specs/laptop/thinkpad/t-series/t530/)