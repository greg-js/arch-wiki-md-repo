# Laptop/Toshiba

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - **Toshiba** - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

</tr>

</tbody>

</table>

### Portege, Qosmio, Satellite, Satellite Pro, T-Series, TE-Series, Tecra, libretto

<table class="wikitable">

<tbody>

<tr>

<th rowspan="2" style="padding: 0.5em;">Model Version</th>

<th rowspan="2" style="padding: 0.5em;">Arch Linux  
Install CD Version  
</th>

<th colspan="8" style="padding: 0.5em;">Hardware Support</th>

<th rowspan="2" style="padding: 0.5em;">Remark</th>

</tr>

<tr>

<th style="padding: 0.5em;">Video</th>

<th style="padding: 0.5em;">Sound</th>

<th style="padding: 0.5em;">Ethernet</th>

<th style="padding: 0.5em;">Wireless</th>

<th style="padding: 0.5em;">Bluetooth</th>

<th style="padding: 0.5em;">Power Management</th>

<th style="padding: 0.5em;">Modem</th>

<th style="padding: 0.5em;">Other</th>

</tr>

<tr>

<td>Satellite U405-S2856</td>

<td>current</td>

<td>Intel GMA X3100 3D support with xf86-video-intel driver</td>

<td>sound works with snd_hda_intel and [ALSA](/index.php/ALSA "ALSA"). Volume dial requires xorg configuration</td>

<td>Marvell 88E8040 works with sky2 kernel module</td>

<td>Atheros AR928X works with ma80211 and ath9k</td>

<td>not tested</td>

<td>Suspend to  
RAM: works  
Disk: NA  
Battery: 3hr  
Dimming of display: works  
Frequency scaling of CPU: not tested</td>

<td>NA</td>

<td>Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).  
Card reader: works</td>

<td>Kernel 2.6.27 fixes bugs in card reader, includes wireless modules</td>

</tr>

<tr>

<td>Satellite A135-S2276</td>

<td>2007.05-Linuxtag2007</td>

<td>3D supported with ATI fglrx Driver</td>

<td>No Sound</td>

<td>Yes</td>

<td>Atheros AR5006EG works with madwifi v0.9.2 or higher</td>

<td>NA</td>

<td>Suspend to  
RAM: NA  
Disk: NA  
Battery: NA  
Dimming of display: NA  
Frequency scaling of CPU: NA</td>

<td>Yes</td>

<td>NA</td>

<td>need BIOS Update V.1.20 or higher</td>

</tr>

<tr>

<td>Satellite A135-SP4108</td>

<td>current</td>

<td>Intel Mobile 945GM/GMS with xf86-video-intel driver</td>

<td>Sound works, Volume control wheel works</td>

<td>Yes</td>

<td>Intel Pro wireless 3945ABG (wicd)</td>

<td>NA</td>

<td>not tested</td>

<td>not tested</td>

<td>Card Reader works</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite A200-1TO</td>

<td>Current</td>

<td>ATI HD2400 (128-892MB Shared) Fully supported by latest ATI Catalyst Drivers</td>

<td>Sound works perfectly under current (2.6.25) kernel, using snd_hda_intel and ALSA.</td>

<td>Yes</td>

<td>Intel 3945 wireless. Works with stock Arch kernel</td>

<td>NA</td>

<td>Power Management working flawlessly. Setup as per Wiki instructions</td>

<td>Not tested.</td>

<td>NA</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite C50-B032</td>

<td>2015.09</td>

<td>xf86-video-intel</td>

<td>Yes (works out of the box)</td>

<td>Yes (works out of the box)</td>

<td>Yes (works out of the box)</td>

<td>[qca9565-bluetooth-firmware](https://aur.archlinux.org/packages/qca9565-bluetooth-firmware/)<sup><small>AUR</small></sup></td>

<td>works out of the box</td>

<td>NA</td>

<td>NA</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite P100-PSPA3C-MA502C</td>

<td>Current</td>

<td>3D supported with latest NVIDIA Driver</td>

<td>Sound works with snd_hda_intel and DSDT modification. See [Gentoo Wiki](http://www.gentoo-wiki.com/HARDWARE_Toshiba_Satellite_P100) for info.</td>

<td>Yes</td>

<td>Works with ipw3945</td>

<td>NA</td>

<td>Suspend to  
RAM: NA  
Disk: NA  
Battery: 2h  
Dimming of display: OK  
Frequency scaling of CPU: OK</td>

<td>Works with linuxant non-free driver</td>

<td>NA</td>

<td>need BIOS Update V.2.40\. Don't use BIOS v. 3.30; GPU may overheat.</td>

</tr>

<tr>

<td>Satellite 2435-S255</td>

<td>2007.05</td>

<td>3D supported with Nvidia legacy driver</td>

<td>Sound works by default with AC97 driver. All that was needed was running alsaconf.</td>

<td>Yes</td>

<td>Works with ipw2200</td>

<td>NA</td>

<td>Suspend to  
RAM: NA  
Disk: NA  
Battery: 2.5h  
Dimming of display: OK  
Frequency scaling of CPU: OK</td>

<td>Yes</td>

<td>NA</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite U305-S7446</td>

<td>current</td>

<td>Intel GMA X3100 3D support with xf86-video-intel driver</td>

<td>Sound works. Volume Control Dial is buggy. Keep getting events even when not turning the wheel. Most likely a bug in Xorg</td>

<td>Yes</td>

<td>Intel PRO/Wireless 3945ABG works</td>

<td>NA</td>

<td>Suspend to  
RAM: NA  
Disk: NA  
Battery: 2.5h  
Dimming of display: OK  
Frequency scaling of CPU: OK</td>

<td>Didn't test</td>

<td>Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).  
5 in 1 Bridge Media Adapter: Not tested</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite Pro L300-EZ1501</td>

<td>current</td>

<td>Intel Corporation Mobile 4 Series Chipset with xf86-video-intel driver</td>

<td>Sound works by default as do onboard speakers</td>

<td>Yes</td>

<td>Qualcomm Atheros AR242x/AR542x (wicd)</td>

<td>N\A</td>

<td>Not tested</td>

<td>Not tested</td>

<td>N\A</td>

<td>N\A</td>

</tr>

<tr>

<td>Satellite Pro L300D-13S</td>

<td>current</td>

<td>tested with open-source ati, works fine</td>

<td>Sound works by default as do onboard speakers</td>

<td>Yes</td>

<td>Works with rtl8187 module</td>

<td>N\A</td>

<td>Not tested</td>

<td>Not tested</td>

<td>Chicony webcam works with linux-uvc driver</td>

<td>N\A</td>

</tr>

<tr>

<td>Tecra A8-143</td>

<td>Don't panic</td>

<td>Intel i810 driver</td>

<td>Sound works by default without on-board speakers; after the changes suggested in [Gentoo Wiki](http://gentoo-wiki.com/HARDWARE_Toshiba_Tecra_A8) onboard speakers work as well</td>

<td>Yes</td>

<td>Works with iwlwifi</td>

<td>N/A</td>

<td>Suspend to  
RAM: NA  
Suspend-to-Disk: N\A  
Battery: 2h  
Dimming of display: OK  
Frequency scaling of CPU: OK  
Cooler stepping: OK</td>

<td>Not tested</td>

<td>N\A</td>

<td>Mandatory BIOS update to v.3.4 or higher</td>

</tr>

<tr>

<td>Satellite Pro U300</td>

<td>current</td>

<td>Intel GMA X3100  
xf86-video-intel driver</td>

<td>Works with snd_hda_intel driver and Alsa</td>

<td>Yes</td>

<td>Works perfectly with iwl4965 driver</td>

<td>Works well with [Omnibook module](https://aur.archlinux.org/packages.php?ID=6919) and ectype=14</td>

<td>Suspend to  
RAM: yes  
Disk: yes  
Battery: 2.5h  
Dimming of display: OK  
Frequency scaling of CPU: OK</td>

<td>Didn't test</td>

<td>Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de)</td>

<td>N\A</td>

</tr>

<tr>

<td>Satellite U405-S2856</td>

<td>current</td>

<td>Intel GMA X3100 3D support with xf86-video-intel driver</td>

<td>Sound works snd_hda_intel and alsa</td>

<td>Marvell 88E8040 works with sky2 module</td>

<td>needs modules: mac80211 and ath9k (kernel>= 2.6.27 or compat-wireless)</td>

<td>not tested</td>

<td>Suspend to  
RAM: works  
Disk: not tested  
Battery: 3h  
Dimming of display: OK  
Frequency scaling of CPU: not tested</td>

<td>NA</td>

<td>Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).  
5 in 1 Bridge Media Adapter: Not tested</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite A200-1M5</td>

<td>Current 2008.6</td>

<td>Intel 945GM support with xf86-video-intel driver</td>

<td>Sound works snd-hda-intel model=lenovo and alsa</td>

<td>works</td>

<td>works Intel PRO Wireless 4965</td>

<td>works with omnibook driver</td>

<td>NA</td>

<td>Winmodem, doesn't work</td>

<td>Chicony USB 2.0 Camera works out of the box. Card reader works.</td>

<td>NA</td>

</tr>

<tr>

<td>Satellite A300D</td>

<td>Current</td>

<td>ATI Mobility Radeon HD 3650 3D support with catalyst drivers</td>

<td>Sound works. Volume control wheel works.</td>

<td>Marvell 88E8040T works</td>

<td>Atheros AR5008 works with ar9k, support for passive monitoring.</td>

<td>NA</td>

<td>Suspend to  
RAM: NA  
Disk: NA  
Battery: NA  
Dimming of display: OK  
Frequency scaling of CPU: OK</td>

<td>Didn't test</td>

<td>Chicony USB 2.0 Camera works with [Linux UVC driver](http://linux-uvc.berlios.de).  
Microphone works out-of-box with ALSA.</td>

<td>NA</td>

</tr>

<tr>

<td>Portege z835-P330</td>

<td>Current</td>

<td>Intel HD Graphics (Sandy Bridge: make sure to enable i915_enable_rc6 and i915_enable_fbc for maximum battery life)</td>

<td>Sound (hda) works. Volume control works.</td>

<td>Intel 82579LM works</td>

<td>Centrino Wireless-N 1000 (iwlagn) works.</td>

<td>NA</td>

<td>Suspend to  
RAM: works  
Disk: not tested  
Battery: 3h/5h with power saving  
Dimming of display: brightness control only works with intel_backlight from intel-gpu-tools-git  
Frequency scaling of CPU: OK (need to load cpufreq)  
Fan control: no (noisy fan fixed with 1.6 bios update; instructions [here](http://benobs.blogspot.fr/2012/04/toshiba-z835-p330-bios-update-from.html))</td>

<td>NA</td>

<td>Camera works  
Microphone works (need to change options in skype)</td>

<td>NA</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Toshiba&oldid=405432](https://wiki.archlinux.org/index.php?title=Laptop/Toshiba&oldid=405432)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Toshiba](/index.php/Category:Toshiba "Category:Toshiba")