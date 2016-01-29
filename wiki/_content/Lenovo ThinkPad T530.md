# Lenovo ThinkPad T530

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo").**

**Notes:** Little of note here, merge support and bluetooth note to the table. (Discuss in [Talk:Lenovo ThinkPad T530#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T530))

## Contents

*   [1 Installation](#Installation)
*   [2 GPU](#GPU)
    *   [2.1 Intel HD 4000](#Intel_HD_4000)
    *   [2.2 NVIDIA NVS 5400M](#NVIDIA_NVS_5400M)
*   [3 Input](#Input)
    *   [3.1 Hotkeys (Media Keys)](#Hotkeys_.28Media_Keys.29)
*   [4 Networking](#Networking)
    *   [4.1 Ericsson H5321 GW Mobile Broadband modem](#Ericsson_H5321_GW_Mobile_Broadband_modem)
*   [5 See also](#See_also)

## Installation

See [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch").

## GPU

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
*   Backlight Brightness (If you use the nVidia driver, configuration will be needed - see [NVIDIA](/index.php/NVIDIA "NVIDIA"))
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

### Ericsson H5321 GW Mobile Broadband modem

The Mobile Broadband modem may need the following change to be made into module settings so that mobile data starts to work.

 `/etc/modprobe.d/cdc_ncm.conf`  `options cdc_ncm prefer_mbim=N` 

## See also

*   [Technical specifications](https://www.lenovo.com/products/us/tech-specs/laptop/thinkpad/t-series/t530/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T530&oldid=402103](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T530&oldid=402103)"