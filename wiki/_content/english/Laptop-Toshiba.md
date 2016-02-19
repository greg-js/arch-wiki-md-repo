| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - **Toshiba** - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model list

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| Satellite U405-S2856 | current | Intel GMA X3100 3D support with xf86-video-intel driver | sound works with snd_hda_intel and [ALSA](/index.php/ALSA "ALSA"). Volume dial requires xorg configuration | Marvell 88E8040 works with sky2 kernel module | Atheros AR928X works with ma80211 and ath9k | not tested | Suspend to
RAM: works
Disk: NA
Battery: 3hr
Dimming of display: works
Frequency scaling of CPU: not tested | NA | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
Card reader: works | Kernel 2.6.27 fixes bugs in card reader, includes wireless modules |
| Satellite A135-S2276 | 2007.05-Linuxtag2007 | 3D supported with ATI fglrx Driver | No Sound | Yes | Atheros AR5006EG works with madwifi v0.9.2 or higher | NA | Suspend to
RAM: NA
Disk: NA
Battery: NA
Dimming of display: NA
Frequency scaling of CPU: NA | Yes | NA | need BIOS Update V.1.20 or higher |
| Satellite A135-SP4108 | current | Intel Mobile 945GM/GMS with xf86-video-intel driver | Sound works, Volume control wheel works | Yes | Intel Pro wireless 3945ABG (wicd) | NA | not tested | not tested | Card Reader works | NA |
| Satellite A200-1TO | Current | ATI HD2400 (128-892MB Shared) Fully supported by latest ATI Catalyst Drivers | Sound works perfectly under current (2.6.25) kernel, using snd_hda_intel and ALSA. | Yes | Intel 3945 wireless. Works with stock Arch kernel | NA | Power Management working flawlessly. Setup as per Wiki instructions | Not tested. | NA | NA |
| Satellite C50-B032 | 2015.09 | xf86-video-intel | Yes (works out of the box) | Yes (works out of the box) | Yes (works out of the box) | [qca9565-bluetooth-firmware](https://aur.archlinux.org/packages/qca9565-bluetooth-firmware/) | works out of the box | NA | NA | NA |
| Satellite P100-PSPA3C-MA502C | Current | 3D supported with latest NVIDIA Driver | Sound works with snd_hda_intel and DSDT modification. See [Gentoo Wiki](http://www.gentoo-wiki.com/HARDWARE_Toshiba_Satellite_P100) for info. | Yes | Works with ipw3945 | NA | Suspend to
RAM: NA
Disk: NA
Battery: 2h
Dimming of display: OK
Frequency scaling of CPU: OK | Works with linuxant non-free driver | NA | need BIOS Update V.2.40\. Don't use BIOS v. 3.30; GPU may overheat. |
| Satellite 2435-S255 | 2007.05 | 3D supported with Nvidia legacy driver | Sound works by default with AC97 driver. All that was needed was running alsaconf. | Yes | Works with ipw2200 | NA | Suspend to
RAM: NA
Disk: NA
Battery: 2.5h
Dimming of display: OK
Frequency scaling of CPU: OK | Yes | NA | NA |
| Satellite U305-S7446 | current | Intel GMA X3100 3D support with xf86-video-intel driver | Sound works. Volume Control Dial is buggy. Keep getting events even when not turning the wheel. Most likely a bug in Xorg | Yes | Intel PRO/Wireless 3945ABG works | NA | Suspend to
RAM: NA
Disk: NA
Battery: 2.5h
Dimming of display: OK
Frequency scaling of CPU: OK | Didn't test | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
5 in 1 Bridge Media Adapter: Not tested | NA |
| Satellite Pro L300-EZ1501 | current | Intel Corporation Mobile 4 Series Chipset with xf86-video-intel driver | Sound works by default as do onboard speakers | Yes | Qualcomm Atheros AR242x/AR542x (wicd) | N\A | Not tested | Not tested | N\A | N\A |
| Satellite Pro L300D-13S | current | tested with open-source ati, works fine | Sound works by default as do onboard speakers | Yes | Works with rtl8187 module | N\A | Not tested | Not tested | Chicony webcam works with linux-uvc driver | N\A |
| Tecra A8-143 | Don't panic | Intel i810 driver | Sound works by default without on-board speakers; after the changes suggested in [Gentoo Wiki](http://gentoo-wiki.com/HARDWARE_Toshiba_Tecra_A8) onboard speakers work as well | Yes | Works with iwlwifi | N/A | Suspend to
RAM: NA
Suspend-to-Disk: N\A
Battery: 2h
Dimming of display: OK
Frequency scaling of CPU: OK
Cooler stepping: OK | Not tested | N\A | Mandatory BIOS update to v.3.4 or higher |
| Satellite Pro U300 | current | Intel GMA X3100
xf86-video-intel driver | Works with snd_hda_intel driver and Alsa | Yes | Works perfectly with iwl4965 driver | Works well with [Omnibook module](https://aur.archlinux.org/packages.php?ID=6919) and ectype=14 | Suspend to
RAM: yes
Disk: yes
Battery: 2.5h
Dimming of display: OK
Frequency scaling of CPU: OK | Didn't test | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de) | N\A |
| Satellite U405-S2856 | current | Intel GMA X3100 3D support with xf86-video-intel driver | Sound works snd_hda_intel and alsa | Marvell 88E8040 works with sky2 module | needs modules: mac80211 and ath9k (kernel>= 2.6.27 or compat-wireless) | not tested | Suspend to
RAM: works
Disk: not tested
Battery: 3h
Dimming of display: OK
Frequency scaling of CPU: not tested | NA | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
5 in 1 Bridge Media Adapter: Not tested | NA |
| Satellite A200-1M5 | Current 2008.6 | Intel 945GM support with xf86-video-intel driver | Sound works snd-hda-intel model=lenovo and alsa | works | works Intel PRO Wireless 4965 | works with omnibook driver | NA | Winmodem, doesn't work | Chicony USB 2.0 Camera works out of the box. Card reader works. | NA |
| Satellite A300D | Current | ATI Mobility Radeon HD 3650 3D support with catalyst drivers | Sound works. Volume control wheel works. | Marvell 88E8040T works | Atheros AR5008 works with ar9k, support for passive monitoring. | NA | Suspend to
RAM: NA
Disk: NA
Battery: NA
Dimming of display: OK
Frequency scaling of CPU: OK | Didn't test | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
Microphone works out-of-box with ALSA. | NA |
| Portege z835-P330 | Current | Intel HD Graphics (Sandy Bridge: make sure to enable i915_enable_rc6 and i915_enable_fbc for maximum battery life) | Sound (hda) works. Volume control works. | Intel 82579LM works | Centrino Wireless-N 1000 (iwlagn) works. | NA | Suspend to
RAM: works
Disk: not tested
Battery: 3h/5h with power saving
Dimming of display: brightness control only works with intel_backlight from intel-gpu-tools-git
Frequency scaling of CPU: OK (need to load cpufreq)
Fan control: no (noisy fan fixed with 1.6 bios update; instructions [here](http://benobs.blogspot.fr/2012/04/toshiba-z835-p330-bios-update-from.html)) | NA | Camera works
Microphone works (need to change options in skype) | NA |
| Portege z930-S9311 | Current | Intel® Ivybridge Mobile | Sound works. Also the keyboard shortcuts | works | works. | Not tested | Suspend to
RAM: works
Disk: not tested
Battery: 2h/3:50h with power saving
Dimming of display: brightness control works even after suspend with gnome-settings-daemon-backlight-toshiba 3.18.2-1 from AUR | NA | Camera works
Microphone works | NA |
| [Portege Z20t](/index.php/Toshiba_Portege_Z20t "Toshiba Portege Z20t")-B2112 | Current | Intel® HD Graphics 5300 (Broadwell GT2)
Touschscreen also works fine (Gnome)
Side note: To use dual monitor setup one cable has to be connected to the screen and the other one to the base (keyboard), both cables to the base doesn't work. | Sound works. Also the keyboard shortcuts to mute/unmute
Vol Buttons on the screen works too | works | works. | Not tested | Suspend to
RAM: works
Disk: not tested
Battery: 2h/3:50h with power saving
Dimming of display: works | NA | Camera works
Microphone works | NA |