| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") (discontinued) - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - <a class="mw-selflink selflink">Other</a> |

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Clevo N130BU | 2017.09 | Intel HD Graphics 620: OK | PuseAudio OK | Yes | Yes | Yes | Not tested | Not tested | Fn keys not working out of the box : volume, brightness

Touchpad works with libinput but awkard default config ("Tapping" disabled)

 | Highly compatible linux machine but many small annoyances as some functionalities are not working out of the box. |
| Clevo M350 | Noodle | Yes | AC'97 with [ALSA](/index.php/ALSA "ALSA") | Yes | N/A | N/A | Suspend-to-RAM: Yes
Suspend-to-disk: No | Yes, with slmodem | IEEE-1394 not tested | Front panel keys does not work |
| Clevo W150HRM | 2011.08.19 | Intel 950GMA and Nvidia Optimus (Bumblebee works) | Intel HDA (OK) | Yes | Yes | Not tested | -- | -- | -- | -- |
| Clevo W110ER (April 2013) | 2013.04.01 | Intel HD Graphics 4000 (i915) and Nvidia GeForce GT 650M with Optimus (nvidia).

HDMI out works.

[Bumblebee](/index.php/Bumblebee "Bumblebee") (3.1-6 and later) works with primus.

[bbswitch](/index.php/Bumblebee#Default_power_state_of_NVIDIA_card_using_bbswitch "Bumblebee") ([bbswitch-dkms-git](https://aur.archlinux.org/packages/bbswitch-dkms-git/) from the AUR, Dec 2013) works. The GT 650M powers down despite ACPI saying otherwise in dmesg.

nvidia binary driver works only sporadically with the default kernel ("GPU has fallen off the bus" in dmesg since [linux](https://www.archlinux.org/packages/?name=linux) 3.10). However, nvidia 331.20 does load and work properly with [linux-ck](https://aur.archlinux.org/packages/linux-ck/) kernel (linux-ck-ivybridge 3.12.5-1 from [Unofficial user repositories/Repo-ck](/index.php/Unofficial_user_repositories/Repo-ck "Unofficial user repositories/Repo-ck")) if boot parameter `rcutree.rcu_idle_gp_delay=2` is given. See [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1357590).

 | ALSA (snd_hda_intel) with [PulseAudio](/index.php/PulseAudio "PulseAudio")

Integrated microphone works.

HDMI audio out works.

Analog headphone out works if the "Independent HP" switch in `alsamixer` is set to Off.

External microphone jack not tested.

 | Realtek 8168 (*r8169*) works. | Intel Centrino Advanced-N 6235 ([iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration")), unreliable on some 802.11n networks. A workaround is to disable 802.11n with module parameter `11n_disable=1`. | Intel Centrino Advanced-N 6235, [works after an initial](/index.php/Bluetooth#hcitool_scan:_Device_not_found "Bluetooth") `sudo hciconfig hci0 up` which persists after reboot. | [Suspend](/index.php/Suspend "Suspend") to disk and RAM works (see note on card reader). | N/A | Web cam works (*uvcvideo*).

All Fn-keys work.

Screen brightness control works.

Touchpad works with multitouch support.

USB 3.0 not tested.

Card reader Realtek 5289 works (*rtsx_pci*).

Battery reports percentage of charge, not the time left, which is a BIOS/ACPI limitation.

 | A highly Linux-friendly machine. Tested only in BIOS mode, not in UEFI. |
| Gigabyte Aero 14k | 2018.01 | Intel integrated graphics: ok
Nvidia GTX 1050 Ti: ok
switching with optimus [bumblebee](https://www.archlinux.org/packages/?name=bumblebee) | Intel HD Audio with [ALSA](/index.php/ALSA "ALSA"), [Jack](/index.php/Jack "Jack") and [PulseAudio](/index.php/PulseAudio "PulseAudio") | yes, with the included USB dongle | yes, but there is some data corruption when communicating with my NAS (only there, no other machine combinations are affected, so it might be a router or NAS problem) | not tested | Suspend-to-RAM and hibernation both work fine | -- | Macro keys not yet tested |
| MX6961 | 2007.05 | intel_agp, intelfb, i915, [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Use 915resolution to get 1280x800 | Intel HD Audio with [ALSA](/index.php/ALSA "ALSA") | Yes, using the *sky2* module | Yes, ipw3945 | Yes | Suspend-to-RAM works fine; hibernate untested | Untested | SD card: module *tifm_core*. | Fn keys for brightness and volume unsupported |
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
| Model version | Arch Linux Install CD version | Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other | Remarks |
| Hardware support |