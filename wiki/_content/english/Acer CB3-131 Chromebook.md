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

Like all other Baytrail Chromebooks, the CB3-131 does not have functional Legacy Boot/SeaBIOS firmware in the stock firmware image, so custom firmware has to be flashed. If dual-boot between Chrome OS and Arch Linux installed on external media is preferred, then there is no need to open up the laptop to remove write protection.

For installing firmware to enable USB/SD boot, follow the instructions in [https://mrchromebox.tech/](https://mrchromebox.tech/) to update the RW_LEGACY firmware with a fixed SeaBIOS payload that will allow booting an Arch Linux iso. Once that is done, press CTRL-L when booting and install Arch as usual.

## Hardware Support

Everything works with the stock Linux v4.16.x kernel except audio.

To fix sound:

```
# git clone [https://github.com/plbossart/UCM.git](https://github.com/plbossart/UCM.git)
# cd UCM
# cp -r chtmax98090/ /usr/share/alsa/ucm/
# alsaucm -c chtmax98090 set _verb HiFi set _enadev Speakers (or)
# alsaucm -c chtmax98090 set _verb HiFi set _enadev Headphone
# alsactl store

```

The above method enables basic audio to work, but video playback is too fast. The problem appears to be with the new unified ALSA sound driver for Baytrail and Cherrytrail machines. Reverting to the old Baytrail driver fixes this problem and both audio/video works fine. A custom kernel needs to be compiled for this purpose with a modified config containing the following options to enable the old driver:

```
# CONFIG_SND_SST_ATOM_HIFI2_PLATFORM is not set
CONFIG_SND_SOC_INTEL_BYT_MAX98090_MACH=m
CONFIG_SND_SOC_MAX98090=m

```

For more information, see [FS#48936](https://bugs.archlinux.org/task/48936)

Note that with the older Baytrail driver, the 'byt-max98090' UCM files have to be used from the repository mentioned above.