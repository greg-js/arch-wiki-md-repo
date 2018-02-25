## Contents

*   [1 General instructions for Chromebooks](#General_instructions_for_Chromebooks)
*   [2 Platform Information](#Platform_Information)
*   [3 SeaBIOS support](#SeaBIOS_support)
*   [4 Hardware Support](#Hardware_Support)

## General instructions for Chromebooks

For basic information on how to enable developer mode, see [Chrome OS devices](/index.php/Chrome_OS_devices "Chrome OS devices").

## Platform Information

This chromebook is based on Intel's Baytrail platform and Google's product name is GNAWTY.

## SeaBIOS support

Booting from external USB or SD cards is **not supported**, so firmware has to be flashed. If dual-boot between Chrome OS and Arch Linux installed on external media is preferred, then there is no need to open up the laptop to remove write protection.

For installing firmware to enable USB/SD boot, follow the instructions in [https://mrchromebox.tech/](https://mrchromebox.tech/) to update the RW_LEGACY firmware with a fixed SeaBIOS payload that will allow booting an Arch Linux iso. Once that is done, press CTRL-L when booting and install Arch as usual.

## Hardware Support

Everything works with the stock Linux v4.15.x kernel except audio.

To fix sound:

```
git clone [https://github.com/plbossart/UCM.git](https://github.com/plbossart/UCM.git)
cd UCM
sudo cp -r chtmax98090/ /usr/share/alsa/ucm/
alsaucm -c chtmax98090 set _verb HiFi set _enadev Speakers (or)
alsaucm -c chtmax98090 set _verb HiFi set _enadev Headphone
sudo alsactl store

```