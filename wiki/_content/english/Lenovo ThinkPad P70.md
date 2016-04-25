This is a guide of steps aggregated from other sources to installation of Arch on the Lenovo ThinkPad P70\. This guide was written for ARCH_201604 ISO. The laptop features a 17.3" 4K IPS display and two SSD (one [NVMe](/index.php/NVMe "NVMe"), one SATA).

| **Device** | **Status** | **Modules** |
| Intel | Working | xf86-video-intel |
| NVIDIA (Quadro M3000M) | untested |
| Ethernet | Working |
| Wireless | Working | iwlwifi |
| Audio | untested |
| Trackpad | Working | xf86-input-libinput |
| Trackpoint | Working | xf86-input-libinput |
| Camera | untested |
| Card Reader | untested |
| Bluetooth | untested |

## Contents

*   [1 Preliminaries](#Preliminaries)
*   [2 Installation](#Installation)
*   [3 Configuration](#Configuration)
    *   [3.1 Keyboard](#Keyboard)
    *   [3.2 Sound](#Sound)
    *   [3.3 NVIDIA/Bumblebee](#NVIDIA.2FBumblebee)
    *   [3.4 HiDPI](#HiDPI)
    *   [3.5 Xfce](#Xfce)
    *   [3.6 Compiz/Emerald](#Compiz.2FEmerald)

## Preliminaries

1.  Create a recovery device in Windows 10\. It required a USB-only (no SD card, no optical media?) flash drive greater than 8 GB. Formatting FAT32 works.

1.  [Update the BIOS.](https://support.lenovo.com/us/en/documents/yast-3jwkjx) As of writing, the latest BIOS was 2.00 (2016-04-17). You may be able to do this in Linux/OS-independently.

1.  Getting **into** the BIOS is difficult, so [here are some instructions](https://support.lenovo.com/us/en/documents/sf13-t0025) that seemed to work. The easiest way was through Windows 10.

1.  In the BIOS, you will want to disable UEFI Secure Boot, change the boot order to look at USB devices first, allow `F12` to bypass the BIOS, and possibly enable the verbose mode because it is easier to press the appropriate buttons on time.

## Installation

This section assumes that you've successfully created bootable Arch install media (hint: unetbootin) to a USB drive. The label of the USB installer must be correct (ARCH_201604 in this case). Restart the computer boot from the USB drive. You may need to press `F12` at some point to trigger a boot order override.

You need an internet connection; this guide got both ethernet and wifi to work.

Ethernet: turn on DHCP with

```
# dhcpcd *interface* 

```

Wifi: wifi-menu worked here, the appropriate SSID was selected with the right password.

The font sizes will make you feel very far away. To deal with this, fonts are in `/usr/share/kbd/consolefonts`.

You can see the currently selected font with showconsolefont. The font was changed here to `sun12x22` with: `setfont sun12x22`. It is a little better.

Following the [Beginner's guide](/index.php/Beginner%27s_guide "Beginner's guide") to install Arch.

Shutdown, remove the USB drive, and then boot the computer, and make sure the installed drive is first in the BIOS.

## Configuration

### Keyboard

### Sound

### NVIDIA/Bumblebee

### HiDPI

### Xfce

### Compiz/Emerald