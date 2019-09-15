[Acer](/index.php/Laptop/Acer "Laptop/Acer") – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – <a class="mw-selflink selflink">HP</a> – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Model List](#Model_List)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Fan noise](#Fan_noise)
    *   [2.2 HP Compaq 8510w](#HP_Compaq_8510w)
    *   [2.3 HP Compaq nc8000](#HP_Compaq_nc8000)

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Compaq Presario F700 | 2009.02 | Nvidia 7000M driver: *nvidia* | Nvidia HD audio with ALSA | Nvidia: OK | Atheros: OK
driver: *ath5k* | none | ACPI
Suspend to RAM/disk: OK
Used pm-utils + uswsusp
CPU frequency scaling: OK | N/A | Hangs for 20-30s when loading ACPI modules when on battery power. Some hotkeys do not work. Need to turn `AutoAddDevices` to `false` in [Xorg](/index.php/Xorg "Xorg") configuration to fix keyboard layout problems. |
| Compaq Presario CQ60-420ED | 2009.08 | Nvidia GeForce 8200M driver: *nvidia* | nVidia MCP72XE/MCP72P/MCP78U/MCP78S HD Audio using ALSA | nVidia MCP77 Ethernet | Atheros AR5001 driver: *ath5k* | none | Using [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/) and [cpupower](https://www.archlinux.org/packages/?name=cpupower) (replaces *cpufrequtils*), haven't properly tested yet | Untested | The console framebuffer is a bit slow (using `vga=773` in [GRUB](/index.php/GRUB "GRUB")) and the wireless LED indicator flickers red and blue. Touchpad (scrolling) works with GNOME |
| HP EliteBook 2570p | 2011.12 | Intel HD 4000 driver: *i915* | Intel HDA driver: *snd_hda_intel* | Intel 82579LM driver: *e1000e* | Intel 6250 driver: *iwlwifi* | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | smart card reader | has xHCI IRQ issues |
| [HP EliteBook 840 G1](/index.php/HP_EliteBook_840_G1 "HP EliteBook 840 G1") | 2017.12 | Intel HD 4400 driver: *i915* | Intel HDA driver: *snd_hda_intel* | Intel I218-LM driver: *e1000e* | Intel 7260 driver: *iwlwifi* | Yes | Suspend to RAM: Yes
Disk: not tested
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | Smart card reader: Yes | -- |
| HP Compaq 6715S | 2010.05 | ATI Radeon X1250 driver: *catalyst* | AD1981 driver: *snd_hda_intel* | Broadcom driver: *tg3* | Broadcom 4312 driver: *ndiswrapper*
(Problematic with 64-bit CPU) | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | Hot keys: Yes
LightScribe: untested | -- |
| HP Compaq 6720S | 2009.2 | Intel X3100 driver: *xf86-video-intel* | Intel HDA driver: *snd_hda_intel* | Intel 10/100 driver: *e1000e* | Intel 3945 driver: *iwl3945*
Broadcom 4312 driver: *wl* [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) | Yes, *bluez-utils* | ACPI: Yes
Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes, cpudyn | not tested | Hot keys: Configurable
LightScribe: Yes [lightscribe](https://aur.archlinux.org/packages/lightscribe/) | -- |
| Pavilion DV2172EA | Duke 2007.05 | Nvidia Go7200 driver *nvidia* | Intel 82801G with internal microphones driver: *snd_hda_intel* | Yes
driver: *e100* | Intel 3945 driver: *ipw3945* | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | Yes | Hot keys: Yes
Remote: Yes
Webcam: Yes (*uvcvideo*)
IRDA: Yes
LightScribe: untested | -- |
| Pavilion DM1-1150SL | 2009.02 | Intel X4500MHD driver: *xf86-video-intel* | Intel 82801G with internal microphones driver: *snd_hda_intel* | Yes (RTL8101E) driver: *r8169* | Atheros AR9285 driver: *ath9k* | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: N/A | Yes | Hot keys: Yes
Webcam: Yes (*uvcvideo*) | -- |
| HP Pavilion dv5055ea | 2009.06 | ATI Radeon XPRESS 200M | ATI IXP SB400 AC'97 Audio Controller (rev 02) | Realtek RTL-8139/8139C/8139C+ (rev 10) | Broadcom BCM4318 (AirForce One 54g) 802.11g Wireless LAN Controller (rev 02) | N/A | Suspend to RAM: not tested
Suspend to Disk: not tested
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Odd on battery, Yes on A/C | not tested | Hot keys: Yes, for sound and WLAN. No, for DVD and Multimedia button | -- |
| HP Pavilion dv6605ed | 2007.08-2 | Intel X3100 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)) | Intel 82801H (*snd-hda-intel*) | RTL8101e (*r8139*) | Broadcom BCM94311MCG driver *b43*: No (may need different firmware)
*ndiswrapper*: Yes | N/A | ACPI: Yes
Suspend to RAM: Yes
Suspend to Disk: No
Battery: Yes
Display dimming: Yes
CPU frequency scaling: Yes (*p4-clockmod*) | not tested | Hot keys: Yes *(HP keymap)*
Remote: Yes, *except for DVD, Quickplay, and Windows MCE buttons*
LightScribe: not tested | -- |
| HP Pavilion dv9530em | 2009.06 | nVidia GeForce 8400M GS | Realtek ALC268 | RTL8168b/8111b | Intel 3945 *(iwl3945)* | Yes | Suspend to RAM: Yes
Suspend to Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | Hot keys: Yes
LightScribe: not tested | -- |
| HP Pavilion TX1220US (GA647UA) | Overlord | nVidia GeForce Go 6150 (works with *nvidia*) | nVidia MCP51 HD Audio (works with *snd-hda-intel*) | nVidia MCP51 Ethernet Controller (works with *forcedeth*) | Broadcom 4321 card (works with *ndiswrapper* and Broadcom-released Linux driver: [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)) | not tested | not tested | not tested | Touch screen: (appears to work; have not calibrated)
Remote: not working
Hot keys: not tested
LightScribe: not tested | People with this same laptop have gotten the hot keys and touch screen to work on other distributions. |
| HP Elitebook 8560w | 2012 | NVIDIA quadro 1000M (*nvidia/nouveau driver*) | Intel sound card: *snd-hda-intel* | *e1000e* | Intel wireless: *iwlwifi* | Yes | ACPI: Yes
Suspend to RAM: No
Suspend to Disk: Yes
Battery: Yes
Display dimming: Yes (using *nvidiabl for nvidia driver*)
CPU frequency scaling: Yes (*acpi-cpufreq*) | not tested | Hot keys: Yes
DVD/CD: Not tested
SD slot: Not tested
Touchkeys: N/A
FireWire: Not tested | If using nvidia driver, nvidiabl should be used to allow backlight adjustments. |
| HP Compaq 8510w | 2008 | NVIDIA FX570M (*nvidia driver*) | Intel sound card: *snd-hda-intel)* | *e1000* | Intel wireless: *iwl4965* | -- | ACPI: Yes
Suspend to RAM: Yes
Suspend to Disk: Yes
Battery: Yes
Display dimming: Yes (using *nvclock*)
CPU frequency scaling: Yes (*acpi-cpufreq*) | not tested | Hot keys: Yes
DVD/CD: Yes
SD slot: Yes
Touchkeys: Yes
FireWire: untested | [#Troubleshooting](#Troubleshooting) |
| [HP tx2z](/index.php/HP_tx2z "HP tx2z") | 2009.08 | Radeon HD 3200 driver: *radeon* | Intel HDA driver: *snd-hda-intel* | RTL8111/8168B driver: *r8169* | Broadcom 4322 driver: [broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl) | not tested | not tested | not tested | Hot keys: yes
LightScribe: not tested
webcam: yes
touchscreen: works
stylus: still working on
Media reader: works | some known successes with touchscreen and stylus in Ubuntu |
| [HP Pavilion DV3-2155MX](/index.php/HP_Pavilion_DV3-2155MX "HP Pavilion DV3-2155MX") | 2010.05 | -- | -- | -- | -- | -- | -- | -- | -- | -- |
| HP Pavilion dv6-2115sa | 2010.05 | Radeon HD 4200 series
Works well with open-source Radeon driver | Intel HDA driver: *snd-hda-intel* | unknown | Broadcom wireless works out-of-the-box | not tested | ACPI: Yes
Suspend to RAM: No
Suspend to Disk: Yes, with TuxOnIce
Battery: Yes
Remote: Some buttons do not work
Display dimming: Yes
CPU frequency scaling: Yes, with K8 Driver | not tested | Hot keys: yes
LightScribe: not tested
Webcam: yes | To prevent output to both headphones and speakers simultaneously, add `options snd-hda-intel model=hp-dv5` to `/etc/modprobe.d/modprobe.conf` |
| HP 625 | 2010.05 | Radeon HD 4200 series drivers: *radeon* or *catalyst* | ATI RS880 Audio Device driver: *snd-hda-intel* | RTL8101E/8102E driver: *r8169* | Broadcom BCM4313 driver: *brcmsmac* (in kernel) | not tested | ACPI: Yes
Suspend to RAM: Yes
Suspend to Disk: Yes
Battery: Yes
Display dimming: Yes
CPU frequency scaling: Yes | not tested | Hot keys: yes
LightScribe: untested
Webcam: yes
Card reader: yes | -- |
| HP Pavilion g4 | 2013 | AMD Radeon HD 7660G+HD 7670M Dual Graphics (A10 APU). APU graphics work with *radeon* driver, but *catalyst* is required for switchable graphics. | Intel sound card: *snd-hda-intel* | RTL8105\. Driver: *r8169* | Ralink RT3290\. Works (poorly) with *rt2800pci*, for best results use *rt3290sta*, from [rt3290sta-dkms in the AUR](https://aur.archlinux.org/packages/rt3290sta-dkms/) | Not working as of Oct 2014 | ACPI: Yes
Suspend to RAM: Yes
Suspend to Disk: Yes
Battery: Yes
Display dimming: Yes
CPU frequency scaling: Yes | not tested | Hot keys: yes
LightScribe: untested
Webcam: yes
Card reader: yes | -- |
| [HP ENVY TouchSmart 17-j113tx](/index.php/HP_ENVY_TouchSmart_17-j113tx "HP ENVY TouchSmart 17-j113tx") | 2014.11 | Intel HD 4600 (*i915*) + NVIDIA GeForce GT 740M (*nouveau* or proprietary *NVIDIA*) as an Optimus setup. | Intel HD Audio (*snd_hda_intel*) | Realtek, exact model is unclear (*r8169*) | Intel 7260 (*iwlwifi*) | Intel Bluetooth, works | ACPI: Yes, Suspend to RAM: Yes, Suspend to Disk: Yes, Battery: Yes, Display Dimming: Yes, CPU Frequency Scaling: Yes | Not included. | Optical Disk Drive, TouchScreen, Webcam, SD Card Reader | See article. |
| HP Pavilion Ultrabook 15-b030st | 2015.05 | Intel Core i5-3317U + NVIDIA GeForce GT 630M (*nouveau* or proprietary *NVIDIA*) as an Optimus setup. | Intel HD Audio (*snd_hda_intel*) | ??? | Ralink RT3290 | Not working | -- | Works | -- | -- |
| HP Pavilion g6-2379sr | 2016.09 | Intel Core i5-3230M, Intel HD 4000 (*i915*) + AMD Radeon 7670M HD (*radeon*)
Needs [PRIME](/index.php/PRIME "PRIME") configuration to use hybrid graphics | Intel sound card: *snd-hda-intel* | RTL8101\. Driver: *r8169* | Ralink RT3290\. Works very bad with driver *rt2800pci* and stop work after installing *[rt3290sta-dkms](https://aur.archlinux.org/packages/rt3290sta-dkms/)* | Not work even after installing *[rtbth-dkms](https://aur.archlinux.org/packages/rtbth-dkms/)* | ACPI: Works
Suspend to RAM: Working properly
Suspend to Disk: Not work (don't turn off pc, just freeze on black screen)
Battery: Works
Display dimming: Works
CPU frequency scaling: Works | No modem installed | Hot keys: Works
LightScribe: Works
Webcam: Works
Card reader: Works | Big problems with WiFi card RT3290\. Best choice it's to use LAN Internet, or change WiFi card.
Poor sound quality when using *snd-hda-intel*, but can't do anythink with it on any Linux distributions. |
| [HP ProBook 440 G4](/index.php/HP_ProBook_440_G4 "HP ProBook 440 G4") | 2016.10 | Intel Core i5-7200U, Intel HD Graphics 620 (*i915*) | Intel sound card: *snd-hda-intel* | RTL8111\. Driver: *r8169* | Intel 7265\. Driver: *iwlwifi* | *not tested as per 30.10.16* | ACPI: Works
Suspend to RAM: Working properly
Suspend to Disk: not tested
Battery: Works
Display dimming: Works
CPU frequency scaling: Works | No modem installed | Hot keys: Works
Webcam: Works
Card reader: not tested as per 30.10.16 | -- |
| HP Envy 15-as010ur | 2016.09 | Intel Core i7-6560U, Intel Iris Graphics 540 | Intel sound card(Conexant CX8200): *snd-hda-intel* | No | Intel DB 7265(*iwlwifi*) | Yes(btusb). Successfully sent a picture to the phone. | ACPI: Works
Suspend to RAM: Works
Suspend to Disk: Not tested
Battery: Works
Display dimming: Works
CPU frequency scaling: Works(only performance and powersave governors*[CPU frequency scaling#Scaling governors](/index.php/CPU_frequency_scaling#Scaling_governors "CPU frequency scaling")[[1]](http://www.phoronix.com/scan.php?page=news_item&px=MTM3NDQ)*) | --- | Hotkeys: Works
Webcam: Works
Card reader: not tested | There is small problem with p2p wpa_supplicant, possible solution: p2p_disabled=1.
Can't set mute-key led light. |
| HP Stream 11-r004nf | 2017.01 | Intel Celeron N3050, Intel HD 400 | Intel sound card: *snd-hda-intel* | No | Realtek RTL8723be (*rtl8723be*) | Yes(btusb). | ACPI: Works
Suspend to RAM: Works
Suspend to Disk: Yes
Battery: Works
Display dimming: Works
 | --- | Hotkeys: Works
Webcam: Works
Card reader: Works | The wifi signal is weak. It is better to use module from lwfinger's rtlwifi_new repo [[2]](https://github.com/lwfinger/rtlwifi_new) with ant_sel=2 option for the module [[rtlwifi_new-dkms](https://aur.archlinux.org/packages/rtlwifi_new-dkms/)] |
| HP Stream 11-y008nf | 2017.08 | Intel Celeron N3060, Intel HD 400 | Intel sound card: *snd-hda-intel* | No | Intel Wireless 7265 (*iwlwifi*) | Yes (*btusb*) | ACPI: works
Suspend to RAM: works
Suspend to Disk: not tested
Battery: works
Display dimming: works
 | No | Hotkeys: works
Webcam: works
Card reader: not tested | Can't set mute-key led light. |
| HP ENVY 13-ad140ng | 2017.12 | Intel UHD Graphics 620 | *hdajackretask* should be used to enable the top speaker *0x14* override to *Internal Speaker*, *0x17* override to *Internal Speaker Back* | Not present | Intel Wireless 7265 | Yes | not tested | No modem installed | Webcam: works | Can't set mute-key led light. |
| HP ProBook 450 G5 | 2018.03 | Intel Core i7-8550u, Intel HD Graphics 620 (*i915*); NVIDIA GeForce MX130 (2 GB DDR5 dedicated) | Intel sound card: *snd-hda-intel* | RTL8111\. Driver: *r8169* | Intel 8265/8275\. Driver: *iwlwifi* | Yes | ACPI: works
Suspend to RAM: works
Suspend to Disk: works
Battery: works
Display dimming: works
CPU frequency scaling: works | Not present | Hot keys: works
Webcam: works
Card reader: works
Fingerprint scanner: works with [libfprint-vfs_proprietary-git](https://aur.archlinux.org/packages/libfprint-vfs_proprietary-git/) and [fprintd-vfs_proprietary](https://aur.archlinux.org/packages/fprintd-vfs_proprietary/), following the [Fprint](/index.php/Fprint "Fprint") tutorial
Keyboard backlit: works
 | Secure boot works with GRUB, coexists with Windows Pro. Windows partition is accessible disabling Bitlocker. (installed from Archiso) -- |
| HP ProBook 450 G6 | 2019.03 | Intel Core i5-8265U, UHD Graphics 620 (Whiskey Lake) - works out of the box; NVIDIA GeForce MX130 (2 GB DDR5 dedicated) - untested | Intel sound card: *snd-hda-intel* | RTL8111\. Driver: *r8169* | Intel 8265/8275\. Driver: *iwlwifi* | Works. | ACPI: works
Suspend to RAM: works
Suspend to Disk: not tested
Battery: works
Display dimming: works
CPU frequency scaling: not tested | Not present | Hot keys: Works
Webcam: not tested
Card reader: not tested
Fingerprint scanner: not tested
Keyboard backlit: works | Secure boot works with GRUB. FN button light is constantly on. FN + F11 (wifi) can't be set (the other "special" buttons are fine). Microphone quality is average. The audio quality is decent. No wifi/eth cable connectivity issues. The touchpad may lag after hibernation. -- |
| HP EliteBook 830 G5 | 2018.11 | Intel Core i5-8250u, Intel UHD Graphics 620 (*i915*) | Intel sound card: *snd-hda-intel* | Realtek RTL8111HSH-CG 10/100/1000 GbE NIC | Intel 9560\. Driver: *iwlwifi* | Yes | ACPI: works
Suspend to RAM: works
Suspend to Disk: work
Battery: works
Display dimming: works
CPU frequency scaling: works
Ambiant light sensor: works with iio-sensor-proxy | Not tested | Hot keys: Works
Webcam: Works
Fingerprint scanner: not tested
Keyboard backlight: works | Secure boot works with SYSLINUX. (installed from Archiso) -- |
| HP Pavilion 15-cw0xxx | 2018.09 | AMD Raven Ridge: *amdgpu* | Intel HDA driver: *snd_hda_intel* ; pulseaudio requires a line to explicitly load an alsa sink for the speaker sound card | RTL8111\. Driver: *r8169* | Realtek RTL8822BE driver: *r8822be* | Yes | ACPI: works Suspend to RAM: works Suspend to Disk: untested Battery: works Display dimming: works CPU frequency scaling: works Rotation sensor: untested | not tested | Volume keys: work keyboard backlight: works | Make sure to install [amd-ucode](https://www.archlinux.org/packages/?name=amd-ucode) to enable full CPU speed. If not cores are capped to 2.0 GHz |
| [HP Pavilion 15-ab214nt](/index.php/HP_Pavilion_15-ab214nt "HP Pavilion 15-ab214nt") | 2019.05 | Intel Core i5-6200U, Intel HD Graphics 520 (*i915*) | Intel sound card: *snd-hda-intel* | RTL810xE. Driver: *r8169* | Realtek RTL8723BE driver: *rtl8723be* | Yes | ACPI: works Suspend to RAM: works Suspend to Disk: works Battery: works Display dimming: works CPU frequency scaling: works Rotation sensor: untested | Not tested | Hot keys: work Webcam: works Smart card reader: works | System will hang on boot or on shutdown without the `pci=nomsi` kernel parameter |
| [HP Spectre x360 - 13-ap0xxxx](/index.php/HP_Spectre_x360_-_13-ap0xxxx "HP Spectre x360 - 13-ap0xxxx") | 2018.12 | Intel Core i7-8565U, Intel UHD Graphics 620 (*i915*) | Intel sound card: *snd-hda-intel* / Internal mic does not work | None | Intel Ac9560 Driver: *iwlwifi* | Yes | ACPI: works
Suspend to RAM: works
Suspend to Disk: untested
Battery: works
Display dimming: works
CPU frequency scaling: works
Rotation sensor: works with iio-sensor-proxy and screen-rotator | Not tested | Hot keys: Works
Webcam: Works
Fingerprint scanner: do not work ( undetected Synaptic SecurePad )
Keyboard backlight: works | TO be able to boot, need to remove the initrd intel and amd patches / install and boots without issues without it -- |
| [HP Elitebook x360 1030 g3](/index.php?title=HP_Elitebook_x360_1030_g3&action=edit&redlink=1 "HP Elitebook x360 1030 g3 (page does not exist)") | 2019.07 | Intel Core i5-8250U, Intel UHD Graphics 620 (*i915*) | Working
hwC0D2: Intel
hwC0D0: Conexant | None | Intel 8265/8275 Driver: *iwlwifi* | Yes | ACPI: works
Suspend to RAM: works
Suspend to Disk: works
Battery: works
Display dimming: works
CPU frequency scaling: works
Rotation sensor: works with iio-sensor-proxy and screen-rotator | Not tested | Hot keys: Works with acpi_backlight=native
Webcam: Works
Fingerprint scanner: Not tested
Keyboard backlight: works |
| [HP Pavilion Laptop 14-ce0xxx](/index.php?title=HP_Pavilion_Laptop_14-ce0xxx&action=edit&redlink=1 "HP Pavilion Laptop 14-ce0xxx (page does not exist)") | 2019.07 | Intel i7-8550U (8) @ 4.000GHz | Working with Alsa | RTL8111/8168/8411 | RTL8821CE | Untested | ACPI: Working
Suspend to RAM: Working
Suspend to Disk: Working
Battery: Working
Display dimming: Working
CPU frequency scaling: Untested
Rotation sensor: Untested | Untested | Hot Keys: Working
Webcam: Untested
Keyboard backlight: Working | For WiFi you need to download an unofficial version from GitHub. |
| Model version | Arch Linux Install CD version | Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other | Remarks |
| Hardware support |

## Troubleshooting

### Fan noise

Since Linux 4.1x laptop's fan may not spin down to a lower rev step (and noise) effectively appearing stuck at higher spinning speed with no apparent temperature reason. Possible workarounds are a quick suspend to ram or power off for more than 10 minutes. Related: [[3]](https://bbs.archlinux.org/viewtopic.php?id=192255) [[4]](https://bugzilla.kernel.org/show_bug.cgi?id=153281)

### HP Compaq 8510w

Follow the steps outlined in [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate"). The suspend to disk process works correctly but the laptop does not power itself off. To fix this create the following file:

 `/etc/systemd/system/sleep.conf` 
```
[Sleep]
HibernateMode=shutdown
```

This file tells [Systemd](/index.php/Systemd "Systemd") to write `shutdown` instead of `platform` to `/sys/power/disk` before writing `disk` to `/sys/power/state`.

### HP Compaq nc8000

Install [TLP](/index.php/TLP "TLP") if suspend to ram fails.