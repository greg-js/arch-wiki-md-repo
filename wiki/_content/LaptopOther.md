# Laptop/Other

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Use notes instead of squashing all this text into columns (Discuss in [Talk:Laptop/Other#](https://wiki.archlinux.org/index.php/Talk:Laptop/Other))

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - **Other**</td>

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

<td>Clevo M350</td>

<td>Noodle</td>

<td>Yes</td>

<td>AC'97 with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes</td>

<td>N/A</td>

<td>N/A</td>

<td>Suspend-to-RAM: Yes  
Suspend-to-disk: No</td>

<td>Yes, with slmodem</td>

<td>IEEE-1394 not tested</td>

<td>Front panel keys does not work</td>

</tr>

<tr>

<td>Clevo W150HRM</td>

<td>2011.08.19</td>

<td>Intel 950GMA and Nvidia Optimus (Bumblebee works)</td>

<td>Intel HDA (OK)</td>

<td>Yes</td>

<td>Yes</td>

<td>Not tested</td>

<td>--</td>

<td>--</td>

<td>--</td>

<td>--</td>

</tr>

<tr>

<td>Clevo W110ER (April 2013)</td>

<td>2013.04.01</td>

<td>Intel HD Graphics 4000 (i915) and Nvidia GeForce GT 650M with Optimus (nvidia).

HDMI out works.

[Bumblebee](/index.php/Bumblebee "Bumblebee") (3.1-6 and later) works with primus.

[bbswitch](/index.php/Bumblebee#Default_power_state_of_NVIDIA_card_using_bbswitch "Bumblebee") ([bbswitch-dkms-git](https://aur.archlinux.org/packages/bbswitch-dkms-git/)<sup><small>AUR</small></sup> from the AUR, Dec 2013) works. The GT 650M powers down despite ACPI saying otherwise in dmesg.

nvidia binary driver works only sporadically with the default kernel ("GPU has fallen off the bus" in dmesg since [linux](https://www.archlinux.org/packages/?name=linux) 3.10). However, nvidia 331.20 does load and work properly with [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup> kernel (linux-ck-ivybridge 3.12.5-1 from [repo-ck](/index.php/Repo-ck "Repo-ck")) if boot parameter `rcutree.rcu_idle_gp_delay=2` is given. See [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1357590).

</td>

<td>ALSA (snd_hda_intel) with [PulseAudio](/index.php/PulseAudio "PulseAudio")

Integrated microphone works.

HDMI audio out works.

Analog headphone out works if the "Independent HP" switch in `alsamixer` is set to Off.

External microphone jack not tested.

</td>

<td>Realtek 8168 (_r8169_) works.</td>

<td>Intel Centrino Advanced-N 6235 ([iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration")), unreliable on some 802.11n networks. A workaround is to disable 802.11n with module parameter `11n_disable=1`.</td>

<td>Intel Centrino Advanced-N 6235, [works after an initial](/index.php/Bluetooth#hcitool_scan:_Device_not_found "Bluetooth") `sudo hciconfig hci0 up` which persists after reboot.</td>

<td>[Suspend](/index.php/Suspend "Suspend") to disk and RAM works (see note on card reader).</td>

<td>N/A</td>

<td>Web cam works (_uvcvideo_).

All Fn-keys work.

Screen brightness control works.

Touchpad works with multitouch support.

USB 3.0 not tested.

Card reader Realtek 5289 works (_rtsx_pci_).

Battery reports percentage of charge, not the time left, which is a BIOS/ACPI limitation.

</td>

<td>A highly Linux-friendly machine. Tested only in BIOS mode, not in UEFI.</td>

</tr>

<tr>

<td>MX6961</td>

<td>2007.05</td>

<td>intel_agp, intelfb, i915, [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel). Use 915resolution to get 1280x800</td>

<td>Intel HD Audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes, using the _sky2_ module</td>

<td>Yes, ipw3945</td>

<td>Yes</td>

<td>Suspend-to-RAM works fine; hibernate untested</td>

<td>Untested</td>

<td>SD card: module _tifm_core_.</td>

<td>Fn keys for brightness and volume unsupported</td>

</tr>

<tr>

<td>CF-Y2 Toughbook (CF-Y2EWAZZBM)</td>

<td>2008.06</td>

<td>Intel 855GM (rev 02) - works perfectly at 1400x1050 with xf86-video-intel package and 'intel' xorg driver</td>

<td>Intel ICH4 AC'97 (rev 03) - works perfectly with default ALSA</td>

<td>Realtek RTL-8139 (rev 10) - works perfectly with default Linux 2.6 kernel</td>

<td>Intel 2915ABG (rev 05) - works perfectly with default Linux wireless drivers</td>

<td>NA</td>

<td>Suspend to  
RAM: Yes, via /sys/power/state

* * *

Suspend to Disk: Yes, tuxonice

* * *

Battery: Yes

* * *

Dimming of display: Yes (with pcc module)

* * *

Frequency scaling of CPU: Yes</td>

<td>Not recognized by Linux</td>

<td>CardBus slot: not tried

* * *

SD card slot: not tried</td>

<td>Use "vbetool post" after resume from Suspend to RAM to fix dark screen problem.</td>

</tr>

<tr>

<td>CF-27 Toughbook (CF-27EB6GCAM)</td>

<td>2010.05</td>

<td>Neomagic NM2200 [MagicGraph 256AV] (Rev 20) - max resolution of 800x600 with xf86-video-neomagic package and 'neomagic' xorg driver</td>

<td>Yamaha YMF-744B [DS-1S] (Rev 03) - works with default ALSA. Bootup messages say BUSY and then FAIL when loading modules. However, sound files play just fine using aplay.</td>

<td>None provided. Cardbus used...  
Dynex DX-E201, Realtek RTL-8139 (8139too).</td>

<td>None provided. Cardbuses used...  
AirLink 101 AWLC5025 MIMO XR - worked with rt2x00 drivers (rt61pci)

* * *

Belkin Wireless G+ F5D7011 v2000 - works with b43 driver and b43-fwcutter install method.</td>

<td>NA</td>

<td>Not tested</td>

<td>Present but disabled in BIOS</td>

<td>TouchPad seen as standard PS/2 mouse, not Synaptics apparently.

* * *

BIOS says touchscreen is enabled but unsure of what drivers would work.

* * *

OSD and some Fn buttons work - brightness, volume control, battery check.</td>

<td>Pentium II, 300MHz, 320MB RAM, 30GB drive, DVD-ROM, USB 1.0 (untested)</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Other&oldid=398858](https://wiki.archlinux.org/index.php?title=Laptop/Other&oldid=398858)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Laptops](/index.php/Category:Laptops "Category:Laptops")