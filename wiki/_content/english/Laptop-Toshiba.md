[Acer](/index.php/Laptop/Acer "Laptop/Acer") – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – <a class="mw-selflink selflink">Toshiba</a> – [Other](/index.php/Laptop/Other "Laptop/Other")

## Satellite

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Satellite C650-160 | 2017.2 | Intel Corporation Mobile 4 Series Chipset Integrated Graphics Controller support with xf86-video-intel driver | sound works with PulseAudio - volume buttons work | Qualcomm Atheros AR8152 v1.1 works | Qualcomm Atheros AR9285 Wireless Network Adapter (PCI-Express) works with linux-libre | not tested | Suspend to
RAM: works
Disk: NA
Battery: 3hr
Dimming of display: works
Frequency scaling of CPU: not tested | NA | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
Card reader: not tested | Kernel 4.9.11-gnu-1 linux-libre |
| Satellite U405-S2856 | current | Intel GMA X3100 3D support with xf86-video-intel driver | sound works with snd_hda_intel and [ALSA](/index.php/ALSA "ALSA"). Volume dial requires xorg configuration | Marvell 88E8040 works with sky2 kernel module | Atheros AR928X works with ma80211 and ath9k | not tested | Suspend to
RAM: works
Disk: NA
Battery: 3hr
Dimming of display: works
Frequency scaling of CPU: not tested | NA | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
Card reader: works | Kernel 2.6.27 fixes bugs in card reader, includes wireless modules |
| Satellite A200-1TO | Current | ATI HD2400 (128-892MB Shared) Fully supported by latest ATI Catalyst Drivers | Sound works perfectly under current (2.6.25) kernel, using snd_hda_intel and ALSA. | Yes | Intel 3945 wireless. Works with stock Arch kernel | NA | Power Management working flawlessly. Setup as per Wiki instructions | Not tested. | NA | NA |
| Satellite C50-B032 | 2016.07.01 | xf86-video-intel | Yes (works out of the box) | Yes (works out of the box) | Yes (works out of the box) | works out of the box | works out of the box | NA | NA | NA |
| Satellite P100-PSPA3C-MA502C | Current | 3D supported with latest NVIDIA Driver | Sound works with snd_hda_intel and DSDT modification. See [Gentoo Wiki](http://www.gentoo-wiki.com/HARDWARE_Toshiba_Satellite_P100) for info. | Yes | Works with ipw3945 | NA | Suspend to
RAM: NA
Disk: NA
Battery: 2h
Dimming of display: OK
Frequency scaling of CPU: OK | Works with linuxant non-free driver | NA | need BIOS Update V.2.40\. Don't use BIOS v. 3.30; GPU may overheat. |
| Satellite U305-S7446 | current | Intel GMA X3100 3D support with xf86-video-intel driver | Sound works. Volume Control Dial is buggy. Keep getting events even when not turning the wheel. Most likely a bug in Xorg | Yes | Intel PRO/Wireless 3945ABG works | NA | Suspend to
RAM: NA
Disk: NA
Battery: 2.5h
Dimming of display: OK
Frequency scaling of CPU: OK | Didn't test | Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).
5 in 1 Bridge Media Adapter: Not tested | NA |
| Satellite Pro L300-EZ1501 | current | Intel Corporation Mobile 4 Series Chipset with xf86-video-intel driver | Sound works by default as do onboard speakers | Yes | Qualcomm Atheros AR242x/AR542x (wicd) | N\A | Not tested | Not tested | N\A | N\A |
| Satellite Pro L300D-13S | current | tested with open-source ati, works fine | Sound works by default as do onboard speakers | Yes | Works with rtl8187 module | N\A | Not tested | Not tested | Chicony webcam works with linux-uvc driver | N\A |
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

## Portege

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Portege z835-P330 | Current | Intel HD Graphics (Sandy Bridge: make sure to enable i915_enable_rc6 and i915_enable_fbc for maximum battery life) | Sound (hda) works. Volume control works. | Intel 82579LM works | Centrino Wireless-N 1000 (iwlagn) works. | NA | Suspend to
RAM: works
Disk: not tested
Battery: 3h/5h with power saving
Dimming of display: brightness control only works with intel_backlight from intel-gpu-tools-git
Frequency scaling of CPU: OK
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
Side note: To use dual monitor setup one cable has to be connected to the screen and the other one to the base (keyboard), both cables to the base doesn't work. | Sound works [except no sound from speaker after resuming from suspend to RAM](https://bbs.archlinux.org/viewtopic.php?id=213720). Also the keyboard shortcuts to mute/unmute
Vol Buttons on the screen works too | works | works. | Not tested | Suspend to
RAM: works
Disk: not tested
Battery: 2h/3:50h with power saving
Dimming of display: works | NA | Camera works
Microphone works | NA |