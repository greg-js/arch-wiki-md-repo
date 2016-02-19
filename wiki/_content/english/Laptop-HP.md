| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - **HP** - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model List

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| HP EliteBook 2570p | 2011.12 | Intel HD 4000 driver: *i915* | Intel HDA driver: *snd_hda_intel* | Intel 82579LM driver: *e1000e* | Intel 6250 driver: *iwlwifi* | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | smart card reader | has xHCI IRQ issues |
| HP Compaq Mini 730 | 2009.02 | Intel GMA 950 driver: *intel* | Intel HDA driver: *snd_hda_intel* | Broadcom driver: *tg3* | Broadcom 4312 driver: *wl* | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | -- | -- | -- |
| HP Compaq 6715S | 2010.05 | ATI Radeon X1250 driver: *catalyst* | AD1981 driver: *snd_hda_intel* | Broadcom driver: *tg3* | Broadcom 4312 driver: *ndiswrapper*
(Problematic with 64-bit CPU) | Yes | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | Hot keys: Yes
LightScribe: untested | -- |
| HP Compaq 6720S | 2009.2 | Intel X3100 driver: *xf86-video-intel* | Intel HDA driver: *snd_hda_intel* | Intel 10/100 driver: *e1000e* | Intel 3945 driver: *iwl3945*
Broadcom 4312 driver: *wl* [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) | Yes, *bluez-utils* | ACPI: Yes
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
| HP Pavilion dv9530em | 2009.06 | nVidia GeForce 8400M GS | Realtek ALC268 | RTL8168b/8111b | Intel 3945 *(iwl3945)* | yes | Suspend to RAM: Yes
Suspend to Disk: Yes
Battery: Yes
Dimming of display: Yes
Frequency scaling of CPU: Yes | not tested | Hot keys: Yes
LightScribe: not tested | -- |
| HP Pavilion TX1220US (GA647UA) | Overlord | nVidia GeForce Go 6150 (works with *nvidia*) | nVidia MCP51 HD Audio (works with *snd-hda-intel*) | nVidia MCP51 Ethernet Controller (works with *forcedeth*) | Broadcom 4321 card (works with *ndiswrapper* and Broadcom-released Linux driver: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)) | not tested | not tested | not tested | Touch screen: (appears to work; have not calibrated)
Remote: not working
Hot keys: not tested
LightScribe: not tested | People with this same laptop have gotten the hot keys and touch screen to work on other distributions. |
| HP Elitebook 8560w | 2012 | NVIDIA quadro 1000M (*nvidia/nouveau driver*) | Intel sound card: *snd-hda-intel* | *e1000e* | Intel wireless: *iwlwifi* | -- | ACPI: Yes
Suspend to RAM: No
Suspend to Disk: Yes
Battery: Yes
Display dimming: Yes (using *nvidiabl for nvidia driver*)
CPU frequency scaling: Yes (*acpi-cpufreq*) | not tested | Hot keys: Yes
DVD/CD: Not tested
SD slot: Not tested
Touchkeys: N/A
FireWire: Not tested | If using nvidia driver, nvidiabl should be used to allow backlight adjustments. |
| HP Compaq 8510w* | 2008 | NVIDIA FX570M (*nvidia driver*) | Intel sound card: *snd-hda-intel)* | *e1000* | Intel wireless: *iwl4965* | -- | ACPI: Yes
Suspend to RAM: Yes
Suspend to Disk: Yes
Battery: Yes
Display dimming: Yes (using *nvclock*)
CPU frequency scaling: Yes (*acpi-cpufreq*) | not tested | Hot keys: Yes
DVD/CD: Yes
SD slot: Yes
Touchkeys: Yes
FireWire: untested | -- |
| [HP tx2z](/index.php/HP_tx2z "HP tx2z") | 2009.08 | Radeon HD 3200 driver: *radeon* | Intel HDA driver: *snd-hda-intel* | RTL8111/8168B driver: *r8169* | Broadcom 4322 driver: [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/) | not tested | not tested | not tested | Hot keys: yes
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
| HP Pavilion Ultrabook 15-b030st | 2015.05 | Intel Core i5-3317U + NVIDIA GeForce GT 630M (*nouveau* or proprietary *NVIDIA*) as an Optimus setup. | Intel HD Audio (*snd_hda_intel*) |  ??? | Ralink RT3290 | Not working | -- | Works | -- | -- |

## Configuration

### HP Compaq 8510w

Follow the steps outlined in [Suspend and hibernate#Hibernation](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate"). The suspend to disk process works correctly but the laptop does not power itself off. To fix this create the following file:

 `/etc/systemd/system/sleep.conf` 
```
[Sleep]
HibernateMode=shutdown
```

This file tells [Systemd](/index.php/Systemd "Systemd") to write `shutdown` instead of `platform` to `/sys/power/disk` before writing `disk` to `/sys/power/state`.