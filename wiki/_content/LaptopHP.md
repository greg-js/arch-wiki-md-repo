# Laptop/HP

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - **HP** - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

</tr>

</tbody>

</table>

## Model List

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

<td>HP EliteBook 2570p</td>

<td>2011.12</td>

<td>Intel HD 4000 driver: _i915_</td>

<td>Intel HDA driver: _snd_hda_intel_</td>

<td>Intel 82579LM driver: _e1000e_</td>

<td>Intel 6250 driver: _iwlwifi_</td>

<td>Yes</td>

<td>Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Yes</td>

<td>not tested</td>

<td>smart card reader</td>

<td>has xHCI IRQ issues</td>

</tr>

<tr>

<td>HP Compaq Mini 730</td>

<td>2009.02</td>

<td>Intel GMA 950 driver: _intel_</td>

<td>Intel HDA driver: _snd_hda_intel_</td>

<td>Broadcom driver: _tg3_</td>

<td>Broadcom 4312 driver: _wl_</td>

<td>Yes</td>

<td>Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Yes</td>

<td>--</td>

<td>--</td>

<td>--</td>

</tr>

<tr>

<td>HP Compaq 6715S</td>

<td>2010.05</td>

<td>ATI Radeon X1250 driver: _catalyst_</td>

<td>AD1981 driver: _snd_hda_intel_</td>

<td>Broadcom driver: _tg3_</td>

<td>Broadcom 4312 driver: _ndiswrapper_  
(Problematic with 64-bit CPU)</td>

<td>Yes</td>

<td>Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Yes</td>

<td>not tested</td>

<td>Hot keys: Yes  
LightScribe: untested</td>

<td>--</td>

</tr>

<tr>

<td>HP Compaq 6720S</td>

<td>2009.2</td>

<td>Intel X3100 driver: _xf86-video-intel_</td>

<td>Intel HDA driver: _snd_hda_intel_</td>

<td>Intel 10/100 driver: _e1000e_</td>

<td>Intel 3945 driver: _iwl3945_  
Broadcom 4312 driver: _wl_ [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup></td>

<td>Yes, _bluez-utils_</td>

<td>ACPI: Yes  
Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Yes, cpudyn</td>

<td>not tested</td>

<td>Hot keys: Configurable  
LightScribe: Yes [lightscribe](https://aur.archlinux.org/packages/lightscribe/)<sup><small>AUR</small></sup></td>

<td>--</td>

</tr>

<tr>

<td>Pavilion DV2172EA</td>

<td>Duke 2007.05</td>

<td>Nvidia Go7200 driver _nvidia_</td>

<td>Intel 82801G with internal microphones driver: _snd_hda_intel_</td>

<td>Yes  
driver: _e100_</td>

<td>Intel 3945 driver: _ipw3945_</td>

<td>Yes</td>

<td>Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Yes</td>

<td>Yes</td>

<td>Hot keys: Yes  
Remote: Yes  
Webcam: Yes (_uvcvideo_)  
IRDA: Yes  
LightScribe: untested</td>

<td>--</td>

</tr>

<tr>

<td>Pavilion DM1-1150SL</td>

<td>2009.02</td>

<td>Intel X4500MHD driver: _xf86-video-intel_</td>

<td>Intel 82801G with internal microphones driver: _snd_hda_intel_</td>

<td>Yes (RTL8101E) driver: _r8169_</td>

<td>Atheros AR9285 driver: _ath9k_</td>

<td>Yes</td>

<td>Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: N/A</td>

<td>Yes</td>

<td>Hot keys: Yes  
Webcam: Yes (_uvcvideo_)</td>

<td>--</td>

</tr>

<tr>

<td>HP Pavilion dv5055ea</td>

<td>2009.06</td>

<td>ATI Radeon XPRESS 200M</td>

<td>ATI IXP SB400 AC'97 Audio Controller (rev 02)</td>

<td>Realtek RTL-8139/8139C/8139C+ (rev 10)</td>

<td>Broadcom BCM4318 (AirForce One 54g) 802.11g Wireless LAN Controller (rev 02)</td>

<td>N/A</td>

<td>Suspend to RAM: not tested  
Suspend to Disk: not tested  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Odd on battery, Yes on A/C</td>

<td>not tested</td>

<td>Hot keys: Yes, for sound and WLAN. No, for DVD and Multimedia button</td>

<td>--</td>

</tr>

<tr>

<td>HP Pavilion dv6605ed</td>

<td>2007.08-2</td>

<td>Intel X3100 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel))</td>

<td>Intel 82801H (_snd-hda-intel_)</td>

<td>RTL8101e (_r8139_)</td>

<td>Broadcom BCM94311MCG driver _b43_: No (may need different firmware)  
_ndiswrapper_: Yes</td>

<td>N/A</td>

<td>ACPI: Yes  
Suspend to RAM: Yes  
Suspend to Disk: No  
Battery: Yes  
Display dimming: Yes  
CPU frequency scaling: Yes (_p4-clockmod_)</td>

<td>not tested</td>

<td>Hot keys: Yes _(HP keymap)_  
Remote: Yes, _except for DVD, Quickplay, and Windows MCE buttons_  
LightScribe: not tested</td>

<td>--</td>

</tr>

<tr>

<td>HP Pavilion dv9530em</td>

<td>2009.06</td>

<td>nVidia GeForce 8400M GS</td>

<td>Realtek ALC268</td>

<td>RTL8168b/8111b</td>

<td>Intel 3945 _(iwl3945)_</td>

<td>yes</td>

<td>Suspend to RAM: Yes  
Suspend to Disk: Yes  
Battery: Yes  
Dimming of display: Yes  
Frequency scaling of CPU: Yes</td>

<td>not tested</td>

<td>Hot keys: Yes  
LightScribe: not tested</td>

<td>--</td>

</tr>

<tr>

<td>HP Pavilion TX1220US (GA647UA)</td>

<td>Overlord</td>

<td>nVidia GeForce Go 6150 (works with _nvidia_)</td>

<td>nVidia MCP51 HD Audio (works with _snd-hda-intel_)</td>

<td>nVidia MCP51 Ethernet Controller (works with _forcedeth_)</td>

<td>Broadcom 4321 card (works with _ndiswrapper_ and Broadcom-released Linux driver: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup>)</td>

<td>not tested</td>

<td>not tested</td>

<td>not tested</td>

<td>Touch screen: (appears to work; have not calibrated)  
Remote: not working  
Hot keys: not tested  
LightScribe: not tested</td>

<td>People with this same laptop have gotten the hot keys and touch screen to work on other distributions.</td>

</tr>

<tr>

<td>HP Elitebook 8560w</td>

<td>2012</td>

<td>NVIDIA quadro 1000M (_nvidia/nouveau driver_)</td>

<td>Intel sound card: _snd-hda-intel_</td>

<td>_e1000e_</td>

<td>Intel wireless: _iwlwifi_</td>

<td>--</td>

<td>ACPI: Yes  
Suspend to RAM: No  
Suspend to Disk: Yes  
Battery: Yes  
Display dimming: Yes (using _nvidiabl for nvidia driver_)  
CPU frequency scaling: Yes (_acpi-cpufreq_)</td>

<td>not tested</td>

<td>Hot keys: Yes  
DVD/CD: Not tested  
SD slot: Not tested  
Touchkeys: N/A  
FireWire: Not tested</td>

<td>If using nvidia driver, nvidiabl should be used to allow backlight adjustments.</td>

</tr>

<tr>

<td>HP Compaq 8510w*</td>

<td>2008</td>

<td>NVIDIA FX570M (_nvidia driver_)</td>

<td>Intel sound card: _snd-hda-intel)_</td>

<td>_e1000_</td>

<td>Intel wireless: _iwl4965_</td>

<td>--</td>

<td>ACPI: Yes  
Suspend to RAM: Yes  
Suspend to Disk: Yes  
Battery: Yes  
Display dimming: Yes (using _nvclock_)  
CPU frequency scaling: Yes (_acpi-cpufreq_)</td>

<td>not tested</td>

<td>Hot keys: Yes  
DVD/CD: Yes  
SD slot: Yes  
Touchkeys: Yes  
FireWire: untested</td>

<td>--</td>

</tr>

<tr>

<td>[HP tx2z](/index.php/HP_tx2z "HP tx2z")</td>

<td>2009.08</td>

<td>Radeon HD 3200 driver: _radeon_</td>

<td>Intel HDA driver: _snd-hda-intel_</td>

<td>RTL8111/8168B driver: _r8169_</td>

<td>Broadcom 4322 driver: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup></td>

<td>not tested</td>

<td>not tested</td>

<td>not tested</td>

<td>Hot keys: yes  
LightScribe: not tested  
webcam: yes  
touchscreen: works  
stylus: still working on  
Media reader: works</td>

<td>some known successes with touchscreen and stylus in Ubuntu</td>

</tr>

<tr>

<td>[HP Pavilion DV3-2155MX](/index.php/HP_Pavilion_DV3-2155MX "HP Pavilion DV3-2155MX")</td>

<td>2010.05</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

</tr>

<tr>

<td>HP Pavilion dv6-2115sa</td>

<td>2010.05</td>

<td>Radeon HD 4200 series  
Works well with open-source Radeon driver</td>

<td>Intel HDA driver: _snd-hda-intel_</td>

<td>unknown</td>

<td>Broadcom wireless works out-of-the-box</td>

<td>not tested</td>

<td>ACPI: Yes  
Suspend to RAM: No  
Suspend to Disk: Yes, with TuxOnIce  
Battery: Yes  
Remote: Some buttons do not work  
Display dimming: Yes  
CPU frequency scaling: Yes, with K8 Driver</td>

<td>not tested</td>

<td>Hot keys: yes  
LightScribe: not tested  
Webcam: yes</td>

<td>To prevent output to both headphones and speakers simultaneously, add `options snd-hda-intel model=hp-dv5` to `/etc/modprobe.d/modprobe.conf`</td>

</tr>

<tr>

<td>HP 625</td>

<td>2010.05</td>

<td>Radeon HD 4200 series drivers: _radeon_ or _catalyst_</td>

<td>ATI RS880 Audio Device driver: _snd-hda-intel_</td>

<td>RTL8101E/8102E driver: _r8169_</td>

<td>Broadcom BCM4313 driver: _brcmsmac_ (in kernel)</td>

<td>not tested</td>

<td>ACPI: Yes  
Suspend to RAM: Yes  
Suspend to Disk: Yes  
Battery: Yes  
Display dimming: Yes  
CPU frequency scaling: Yes</td>

<td>not tested</td>

<td>Hot keys: yes  
LightScribe: untested  
Webcam: yes  
Card reader: yes</td>

<td>--</td>

</tr>

<tr>

<td>HP Pavilion g4</td>

<td>2013</td>

<td>AMD Radeon HD 7660G+HD 7670M Dual Graphics (A10 APU). APU graphics work with _radeon_ driver, but _catalyst_ is required for switchable graphics.</td>

<td>Intel sound card: _snd-hda-intel_</td>

<td>RTL8105\. Driver: _r8169_</td>

<td>Ralink RT3290\. Works (poorly) with _rt2800pci_, for best results use _rt3290sta_, from [rt3290sta-dkms in the AUR](https://aur.archlinux.org/packages/rt3290sta-dkms/)</td>

<td>Not working as of Oct 2014</td>

<td>ACPI: Yes  
Suspend to RAM: Yes  
Suspend to Disk: Yes  
Battery: Yes  
Display dimming: Yes  
CPU frequency scaling: Yes</td>

<td>not tested</td>

<td>Hot keys: yes  
LightScribe: untested  
Webcam: yes  
Card reader: yes</td>

<td>--</td>

</tr>

<tr>

<td>[HP ENVY TouchSmart 17-j113tx](/index.php/HP_ENVY_TouchSmart_17-j113tx "HP ENVY TouchSmart 17-j113tx")</td>

<td>2014.11</td>

<td>Intel HD 4600 (_i915_) + NVIDIA GeForce GT 740M (_nouveau_ or proprietary _NVIDIA_) as an Optimus setup.</td>

<td>Intel HD Audio (_snd_hda_intel_)</td>

<td>Realtek, exact model is unclear (_r8169_)</td>

<td>Intel 7260 (_iwlwifi_)</td>

<td>Intel Bluetooth, works</td>

<td>ACPI: Yes, Suspend to RAM: Yes, Suspend to Disk: Yes, Battery: Yes, Display Dimming: Yes, CPU Frequency Scaling: Yes</td>

<td>Not included.</td>

<td>Optical Disk Drive, TouchScreen, Webcam, SD Card Reader</td>

<td>See article.</td>

</tr>

<tr>

<td>HP Pavilion Ultrabook 15-b030st</td>

<td>2015.05</td>

<td>Intel Core i5-3317U + NVIDIA GeForce GT 630M (_nouveau_ or proprietary _NVIDIA_) as an Optimus setup.</td>

<td>Intel HD Audio (_snd_hda_intel_)</td>

<td> ???</td>

<td>Ralink RT3290</td>

<td>Not working</td>

<td>--</td>

<td>Works</td>

<td>--</td>

<td>--</td>

</tr>

</tbody>

</table>

## Configuration

### HP Compaq 8510w

Follow the steps outlined in [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate"). The suspend to disk process works correctly but the laptop does not power itself off. To fix this create the following file:

 `/etc/systemd/system/sleep.conf` 

```
[Sleep]
HibernateMode=shutdown
```

This file tells [Systemd](/index.php/Systemd "Systemd") to write `shutdown` instead of `platform` to `/sys/power/disk` before writing `disk` to `/sys/power/state`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/HP&oldid=406887](https://wiki.archlinux.org/index.php?title=Laptop/HP&oldid=406887)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")