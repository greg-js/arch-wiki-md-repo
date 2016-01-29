# Laptop/Other

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Use notes instead of squashing all this text into columns (Discuss in [Talk:Laptop/Other#](https://wiki.archlinux.org/index.php/Talk:Laptop/Other))

| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - **Other** |

## Model List

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| Clevo M350 | Noodle | Yes | AC'97 with [ALSA](/index.php/ALSA "ALSA") | Yes | N/A | N/A | Suspend-to-RAM: Yes
Suspend-to-disk: No | Yes, with slmodem | IEEE-1394 not tested | Front panel keys does not work |
| Clevo W150HRM | 2011.08.19 | Intel 950GMA and Nvidia Optimus (Bumblebee works) | Intel HDA (OK) | Yes | Yes | Not tested | -- | -- | -- | -- |
| Clevo W110ER (April 2013) | 2013.04.01 | Intel HD Graphics 4000 (i915) and Nvidia GeForce GT 650M with Optimus (nvidia).

HDMI out works.

[Bumblebee](/index.php/Bumblebee "Bumblebee") (3.1-6 and later) works with primus.

[bbswitch](/index.php/Bumblebee#Default_power_state_of_NVIDIA_card_using_bbswitch "Bumblebee") ([bbswitch-dkms-git](https://aur.archlinux.org/packages/bbswitch-dkms-git/)<sup><small>AUR</small></sup> from the AUR, Dec 2013) works. The GT 650M powers down despite ACPI saying otherwise in dmesg.

nvidia binary driver works only sporadically with the default kernel ("GPU has fallen off the bus" in dmesg since [linux](https://www.archlinux.org/packages/?name=linux) 3.10). However, nvidia 331.20 does load and work properly with [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup> kernel (linux-ck-ivybridge 3.12.5-1 from [repo-ck](/index.php/Repo-ck "Repo-ck")) if boot parameter `rcutree.rcu_idle_gp_delay=2` is given. See [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1357590).

 | ALSA (snd_hda_intel) with [PulseAudio](/index.php/PulseAudio "PulseAudio")

Integrated microphone works.

HDMI audio out works.

Analog headphone out works if the "Independent HP" switch in `alsamixer` is set to Off.

External microphone jack not tested.

 | Realtek 8168 (_r8169_) works. | Intel Centrino Advanced-N 6235 ([iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration")), unreliable on some 802.11n networks. A workaround is to disable 802.11n with module parameter `11n_disable=1`. | Intel Centrino Advanced-N 6235, [works after an initial](/index.php/Bluetooth#hcitool_scan:_Device_not_found "Bluetooth") `sudo hciconfig hci0 up` which persists after reboot. | [Suspend](/index.php/Suspend "Suspend") to disk and RAM works (see note on card reader). | N/A | Web cam works (_uvcvideo_).

All Fn-keys work.

Screen brightness control works.

Touchpad works with multitouch support.

USB 3.0 not tested.

Card reader Realtek 5289 works (_rtsx_pci_).

Battery reports percentage of charge, not the time left, which is a BIOS/ACPI limitation.

 | A highly Linux-friendly machine. Tested only in BIOS mode, not in UEFI. |
| MX6961 | 2007.05 | intel_agp, intelfb, i915, [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Use 915resolution to get 1280x800 | Intel HD Audio with [ALSA](/index.php/ALSA "ALSA") | Yes, using the _sky2_ module | Yes, ipw3945 | Yes | Suspend-to-RAM works fine; hibernate untested | Untested | SD card: module _tifm_core_. | Fn keys for brightness and volume unsupported |
| CF-Y2 Toughbook (CF-Y2EWAZZBM) | 2008.06 | Intel 855GM (rev 02) - works perfectly at 1400x1050 with xf86-video-intel package and 'intel' xorg driver | Intel ICH4 AC'97 (rev 03) - works perfectly with default ALSA | Realtek RTL-8139 (rev 10) - works perfectly with default Linux 2.6 kernel | Intel 2915ABG (rev 05) - works perfectly with default Linux wireless drivers | NA | Suspend to
RAM: Yes, via /sys/power/state

* * *

Suspend to Disk: Yes, tuxonice

* * *

Battery: Yes

* * *

Dimming of display: Yes (with pcc module)

* * *

Frequency scaling of CPU: Yes | Not recognized by Linux | CardBus slot: not tried

* * *

SD card slot: not tried | Use "vbetool post" after resume from Suspend to RAM to fix dark screen problem. |
| CF-27 Toughbook (CF-27EB6GCAM) | 2010.05 | Neomagic NM2200 [MagicGraph 256AV] (Rev 20) - max resolution of 800x600 with xf86-video-neomagic package and 'neomagic' xorg driver | Yamaha YMF-744B [DS-1S] (Rev 03) - works with default ALSA. Bootup messages say BUSY and then FAIL when loading modules. However, sound files play just fine using aplay. | None provided. Cardbus used...
Dynex DX-E201, Realtek RTL-8139 (8139too). | None provided. Cardbuses used...
AirLink 101 AWLC5025 MIMO XR - worked with rt2x00 drivers (rt61pci)

* * *

Belkin Wireless G+ F5D7011 v2000 - works with b43 driver and b43-fwcutter install method. | NA | Not tested | Present but disabled in BIOS | TouchPad seen as standard PS/2 mouse, not Synaptics apparently.

* * *

BIOS says touchscreen is enabled but unsure of what drivers would work.

* * *

OSD and some Fn buttons work - brightness, volume control, battery check. | Pentium II, 300MHz, 320MB RAM, 30GB drive, DVD-ROM, USB 1.0 (untested) |

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Other&oldid=398858](https://wiki.archlinux.org/index.php?title=Laptop/Other&oldid=398858)"