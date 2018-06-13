| **Device** | **Status** |
| Intel | Working |
| HDMI | Not Tested |
| Wireless | Working |
| Audio | Working |
| Touchpad | Working |
| Camera | Working |
| Card Reader | Working |
| Bluetooth | Working |
| Function keys | Working |
| Fingerprint Sensor | Not Tested |

This page contains instructions, tips, pointers, and links for installing and configuring Arch Linux on the [Asus ZenBook UX331UA](https://www.asus.com/Laptops/ASUS-ZenBook-13-UX331UA/).

Hardware reference from UX331UA-EG013T with kernel 4.16.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Secure Boot (option)](#Secure_Boot_.28option.29)
    *   [1.2 Video](#Video)
    *   [1.3 Touchpad](#Touchpad)
    *   [1.4 Function Keys](#Function_Keys)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Power saving and performance](#Power_saving_and_performance)

# Configuration

## Secure Boot (option)

In order to boot any Linux operating system, navigate to BIOS, then hit F7 or click on "Advanced Menu", then the "Security" tab and set "Secure Boot" to `Off`.

If the aforementioned "Secure Boot" option is a menu rather than an on-or-off option, click on "Secure Boot", "Key Management", then "Reset to Setup Mode" and confirm in the dialog.

## Video

See [Intel Graphics](/index.php/Intel_graphics#Installation "Intel graphics") and [Hardware Acceleration](/index.php/Hardware_video_acceleration "Hardware video acceleration").

## Touchpad

See [Libinput](/index.php/Libinput "Libinput").

## Function Keys

Working fine with Arch and Gnome without tweaking anything. FN+f5 lowers brightness, fn+f6 increases brightness, fn+f11 lowers sound, fn+f12 increases sound.

# Tips and tricks

## Power saving and performance

As advertised by ASUS, the laptop is capable to last up to 14 hours on battery. In order to achieve this, see:

*   BIOS update - It is generally recommended to update BIOS, as it usually brings performance, power-saving and security features.
*   [Power Saving](/index.php/Power_Saving "Power Saving") - List of general recommendations to increase battery life.
*   [Improving performance](/index.php/Improving_performance "Improving performance") - List of general recommendations to increase performance.
*   [SSD](/index.php/SSD "SSD") - Tips and tricks for Solid State Drives.