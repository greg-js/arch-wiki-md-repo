# Laptop/Dell

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - **Dell** - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

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

<td>e1405</td>

<td>Any</td>

<td>3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.0, native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.3 (1440x900)</td>

<td>Intel HD Audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes</td>

<td>Yes, ipw3945</td>

<td>Yes</td>

<td>Suspend-to-RAM is shaky; hibernate is flawless</td>

<td>Untested</td>

<td>SD card reader works out-of-the-box</td>

<td>Everything else works without a hitch</td>

</tr>

<tr>

<td>E6420</td>

<td>2011.08.19</td>

<td>Intel HD3000 [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)</td>

<td>Intel HD Audio with ALSA</td>

<td>Yes, e1000e</td>

<td>Yes, bcma-pci-bridge</td>

<td>Untested</td>

<td>Suspend-to-RAM good, hibernate not working</td>

<td>No modem</td>

<td>SD card reader works out-of-the-box, smart card reader works with ccid, opensc, pcsc-tools. Touchpad (alps a10) pointer aspens by default, install [psmouse-elantech](https://aur.archlinux.org/packages/psmouse-elantech/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/psmouse-elantech)]</sup> from the [AUR](/index.php/AUR "AUR") to fix it ([psmouse-alps](https://aur.archlinux.org/packages/psmouse-alps/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/psmouse-alps)]</sup> does not work anymore)</td>

<td>Ethernet was not working in fresh installation, had to clone repositories to HDD and update</td>

</tr>

<tr>

<td>E6530</td>

<td>2014.10.01</td>

<td>NVIDIA NVS5200 3D works flawlessly with either [nvidia](https://www.archlinux.org/packages/?name=nvidia) or [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) (1600x900).</td>

<td>Intel HD Audio with ALSA</td>

<td>Yes</td>

<td>Intel Centrino A-N (with iwlwifi)</td>

<td>Flawless. File transfer and Audio streaming works</td>

<td>Suspend-to-RAM perfect. Hibernate perfect. Disk spindown perfect.</td>

<td>Untested</td>

<td>SD card reader, ALPS touchpad with gestures, and Webcam work flawlessly. Integrated and external microphone ports work flawlessly. Backlit keyboard, monitor backlight, audio up/down/mute controls all work flawlessly.</td>

<td>HDMI video works but must disable Optimus in bios. HDMI audio out works. If Optimus enabled, Intel HD4000 will be used and optirun works. Prevents use of HDMI (VGA only) but otherwise works.</td>

</tr>

<tr>

<td>d420</td>

<td>Duke</td>

<td>[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.2 (1280x800)</td>

<td>Intel HD Audio with ALSA</td>

<td>Yes (with tg3)</td>

<td>Yes (with ipw3945)</td>

<td>N/A</td>

<td>Untested</td>

<td>Have not tested SD card reader</td>

<td>External D-Bay DVD/CD-RW works, docking station mostly works (can un-dock, but locks up on re-docking)</td>

</tr>

<tr>

<td>d620</td>

<td>Duke</td>

<td>3D with NVIDIA, native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.2 (1440x900)  
3D with Intel 945GM, native resolution 1440x900</td>

<td>Intel HD Audio with ALSA</td>

<td>Yes</td>

<td>Yes, bcm4311 PCI-E with bcm43xx. Yes for some models with iwl3945\.</td>

<td>N/A</td>

<td>Suspend-to-RAM perfect, hibernate works fine.</td>

<td>Untested</td>

<td>not tested smart card reader</td>

<td>Everything else works without a hitch</td>

</tr>

<tr>

<td>d820</td>

<td>Duke</td>

<td>3D with NVIDIA drivers</td>

<td>Intel HD Audio with ALSA</td>

<td>Yes</td>

<td>Yes, IPW3945</td>

<td>Yes</td>

<td>Suspending with [KDE](/index.php/KDE "KDE") works</td>

<td>Untested</td>

<td>Everything works, even fingerprint reader with _bioapi_ and _pam_bioapi_</td>

<td>Everything else works without a hitch</td>

</tr>

<tr>

<td>Inspiron 1420</td>

<td>2012.09</td>

<td>3D with [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau)</td>

<td>Intel HD Audio with ALSA</td>

<td>Yes</td>

<td>Yes, [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> needed from the AUR</td>

<td>Untested</td>

<td>Untested</td>

<td>Untested</td>

<td>Untested</td>

<td>Everything that I have tested works great without any problems</td>

</tr>

<tr>

<td>Inspiron 1501</td>

<td>Duke</td>

<td>3D with proprietary ATI fglrx</td>

<td>Intel HD audio with ALSA</td>

<td>Yes</td>

<td>Yes, BCM4311 PCI-E with bcm43xx</td>

<td>N/A</td>

<td>Untested</td>

<td>Untested</td>

<td>Smart card reader works out-of-the-box</td>

<td>Everything else works without a hitch</td>

</tr>

<tr>

<td>XPS M1210</td>

<td>Duke</td>

<td>3D with NVIDIA open source drivers</td>

<td>SigmaTel audio with ALSA</td>

<td>_b44_ module, out-of-the-box</td>

<td>IPW 3945, command-line [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools)</td>

<td>Untested</td>

<td>Untested</td>

<td>Untested</td>

<td>rico card reader worked out-of-the-box, hot keys using keytouch, web cam works but is unstable. In [MPlayer](/index.php/MPlayer "MPlayer"), use `driver=v4l2:device=/dev/video0`</td>

<td>Everything else works without a hitch</td>

</tr>

<tr>

<td>XPS L322</td>

<td>2013_03</td>

<td>Intel HD 4000, with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)</td>

<td>Intel HD Audio with ALSA</td>

<td>No Ethernet port</td>

<td>Yes</td>

<td>Untested</td>

<td>Yes</td>

<td>No modem</td>

<td>No SD card slot</td>

<td>ALPS Touchpad recognized only as PS/2 mouse, two-finger scroll, finger tap-to-click, etc... does not work. Some new mouse drivers suggest a fix but have not worked.</td>

</tr>

<tr>

<td>Inspiron 1520</td>

<td>Core Dump</td>

<td>3D with NVIDIA</td>

<td>SigmaTel audio with ALSA</td>

<td>_b44_ module, out of the box</td>

<td>_b43_, need firmware</td>

<td>Yes</td>

<td>Both hibernate and suspend-to-RAM and works with [pm-utils](/index.php/Pm-utils "Pm-utils")</td>

<td>Untested</td>

<td>Hot keys work out-of-the-box</td>

<td>Everything else works without a hitch</td>

</tr>

<tr>

<td>[Inspiron 1525](/index.php/Dell_Inspiron_1525 "Dell Inspiron 1525")</td>

<td>Arch Linux 2008.06 - "Overlord" FTP Install</td>

<td>3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.4.3, native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.5.3 (1280x800)</td>

<td>Intel HD Audio (SigmaTel STAC9228 codec) with ALSA</td>

<td>Marvell Yukon Gb Ethernet: Yes (_sky2_ module)</td>

<td>PRO/Wireless 3945ABG with _iwlwifi-3945-ucode_ 15.28.2.8</td>

<td>Untested (does not have)</td>

<td>Untested</td>

<td>Untested</td>

<td>SD card reader works out-of-the-box</td>

<td>`Fn+Up/Down` (LCD brightness control) works independently of the OS. Everything else work out-of-the-box.</td>

</tr>

<tr>

<td>Inspiron 1525</td>

<td>Core Dump (2008.03 ISO)</td>

<td>3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.2, native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.4 (1280x800)</td>

<td>Intel HD Audio (SigmaTel STAC9228 codec) with ALSA</td>

<td>Marvell Yukon Gb Ethernet: Yes (_sky2_ module)</td>

<td>Broadcom BCM4310: Yes, [ndiswrapper](/index.php/Ndiswrapper "Ndiswrapper") ([AUR](/index.php/AUR "AUR") [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> works, but must blacklist `ssb` module)</td>

<td>Untested (does not have)</td>

<td>Untested</td>

<td>Untested</td>

<td>SD card reader (Ricoh) works out-of-the-box</td>

<td>`Fn+Up/Down` (LCD brightness control) works independently of the OS; media keys configured with KeyTouch. DVD-RW drive and everything else work out-of-the-box.</td>

</tr>

<tr>

<td>[Inspiron 1564](/index.php/Dell_Inspiron_1564 "Dell Inspiron 1564")</td>

<td>Core Dump</td>

<td>3D with either [Catalyst](/index.php/Catalyst "Catalyst") or [xf86-video-ati](/index.php/ATI "ATI"); both work flawlessly.</td>

<td>Intel HD Audio with ALSA</td>

<td>Realtek RTL8101E Ethernet Controller</td>

<td>Intel WiFi Link 5100 with _iwlagn_ driver</td>

<td>Untested</td>

<td>Both suspend and hibernate work flawlessly with [pm-utils](/index.php/Pm-utils "Pm-utils")</td>

<td>Untested</td>

<td>Realtek card reader works out-of-the-box. LCD brightness works out-of-the-box; volume keys need configuring through key bindings.</td>

<td>Overall, this laptop is Linux friendly.</td>

</tr>

<tr>

<td>Inspiron 1764</td>

<td>2011.08.19</td>

<td>3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)</td>

<td>Works well with ALSA</td>

<td>Realtek RTL8101E 10/100 Ethernet Controller</td>

<td>[Broadcom BCM43224](/index.php/Broadcom_wireless "Broadcom wireless") 802.11a/b/g/n works well with [brcmsmac](/index.php/Broadcom_wireless#brcmsmac.2Fbrcmfmac "Broadcom wireless")</td>

<td>Untested</td>

<td>Untested</td>

<td>Does not have a modem</td>

<td>SD card reader and LCD brightness `Fn` keys work out-of-the-box</td>

<td>Fan control/monitoring is completely broken with [i8kutils](https://aur.archlinux.org/packages/i8kutils/)<sup><small>AUR</small></sup></td>

</tr>

<tr>

<td>Inspiron 1300</td>

<td>Don't Panic (Core Dump version)</td>

<td>3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)</td>

<td>Intel</td>

<td>_b44_ module works out-of-the-box</td>

<td>BCM4318-based card, works with [ndiswrapper](/index.php/Ndiswrapper "Ndiswrapper")</td>

<td>N/A</td>

<td>Untested</td>

<td>Untested</td>

<td>--</td>

<td>Everything works out-of-the-box except wireless and sometimes screen resolution</td>

</tr>

<tr>

<td>Inspiron Duo 1090 (hybrid touchscreen netbook/tablet)</td>

<td>2014.10.01</td>

<td>Intel Atom Integrated VGA graphics controller. Software 3D, works out-of-the-box (1366x768).</td>

<td>Intel HD Audio with ALSA</td>

<td>No.</td>

<td>Yes, Qualcomm Atheros (ath9k)</td>

<td>Untested</td>

<td>Suspend-to-RAM works flawlessly. Hibernate untested.</td>

<td>No.</td>

<td>eGalax touchscreen and Synaptics touchpad work flawlessly. All function keys (Power manager, Wifi on/off, touchpad on/off, brightness and audio up/down work flawlessly. Webcam and integrated microphone work.</td>

<td>Audio out works, no standard audio-in or video out ports. USB audio-in and USB video-out untested.</td>

</tr>

<tr>

<td>[Dell XPS M1330](/index.php/Dell_XPS_M1330 "Dell XPS M1330")</td>

<td>Don't Panic (2007.08-2)</td>

<td>For dedicated graphics (NVIDIA 8400m) works with NVIDIA package</td>

<td>Works with Intel HD Audio and ALSA, but need to configure microphone</td>

<td>Yes</td>

<td>Works with iwl4965</td>

<td>Can set Bluetooth but have not tested with any devices</td>

<td>Suspend works fine with [pm-utils](/index.php/Pm-utils "Pm-utils") (_acpi_cpufreq_ problem: [see forums](https://bbs.archlinux.org/viewtopic.php?id=44500))</td>

<td>Untested</td>

<td>2.0 MP web cam works with _uvcvideo_, media keys work with keytouch or esekeyd, IR remote works, SD card works</td>

<td>Everything basically worked out-of-the-box except the microphone</td>

</tr>

<tr>

<td>Dell Latitude D830</td>

<td>Don't Panic (2007.08-2)</td>

<td>NVIDIA Quadro NVS 140M with proprietary NVIDIA drivers</td>

<td>ALSA with the `snd_hda_intel` module</td>

<td>Yes, with `tg3` module</td>

<td>Yes, with `iwl3965` module</td>

<td>Yes</td>

<td>Yes, with [pm-utils](/index.php/Pm-utils "Pm-utils")</td>

<td>Untested</td>

</tr>

<tr>

<td>Dell Studio XPS M1640</td>

<td>(2009.08)</td>

<td>ATI HD4670 Mobile works with [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) (see the forums for 3D support); Catalyst drivers untested</td>

<td>Works with Intel HD Audio and ALSA.</td>

<td>Yes</td>

<td>Works with iwlagn</td>

<td>Bluetooth works</td>

<td>Works but when using [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati), there is video corruption upon boot</td>

<td>N/A</td>

<td>Web cam works, media keys work with the `dell_laptop` kernel module, IR works, card reader works</td>

<td>Everything basically worked out-of-the-box</td>

</tr>

<tr>

<td>Studio 1749</td>

<td>2013.01.04</td>

<td>Radeon HD 5650M, `xf86-video-ati` is almost flawless (just slower 3D), `catalyst` is faster but has various issues.</td>

<td>HDA Intel MID, works with ALSA after adding `options snd-hda-intel index=0 model=dell-m6-dmic` to `/etc/modprobe.d/alsa-base.conf`. HDMI audio has some issues.</td>

<td>Yes</td>

<td>BCM43224, brcmsmac and [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> both work</td>

<td>N/A</td>

<td>Suspend works; hibernate untested.</td>

<td>N/A</td>

<td>SD card reader works, media keys work, web cam, and microphone both work.</td>

<td>Flawless except for poor 3D performance and battery life.</td>

</tr>

<tr>

<td>Precision M4800</td>

<td>2014.04.01</td>

<td>System not usable if booted without kernel parameter `nomodeset`. Nvidia Quadro K2100M works with [nvidia](https://www.archlinux.org/packages/?name=nvidia), but [Nouveau](/index.php/Nouveau "Nouveau") does not work because it requires KMS.</td>

<td>Untested</td>

<td>Yes</td>

<td>Yes</td>

<td>Untested</td>

<td>Untested</td>

<td>No modem</td>

<td>N/A</td>

<td>`nomodeset` is _required_ to boot to a usable system, both with the Arch installation media and post-installation.</td>

</tr>

<tr>

<td>Inspiron 15 7000 Series (model 7537)</td>

<td>2014.10.01</td>

<td>Intel® HD Graphics 4400</td>

<td>Untested</td>

<td>Yes RJ45 Ethernet</td>

<td>Came with Intel® 7260BGN + BT4.0 but never tested it. I switched the card to an Intel® 7260AG + BT4.0 Dual Band (IEEE 802.11AC) Works perfectly with iwlwifi driver</td>

<td>Yes, check wifi section for details.</td>

<td>Suspend-to-RAM perfect. Hibernate perfect. Disk spindown untested.</td>

<td>No modem</td>

<td>HDMI is currently untested. The touchpad needs a lot of modifying to scroll properly.</td>

<td>All of the hardware works flawlessly. Volume up / down button needs some modifying to work all other buttons work with drivers that come with the kernel. Kernel 4.2.x causes ACPI battery to not be detected, [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) works fine.</td>

</tr>

<tr>

<td>Inspiron 15 7000 Series (model 7548)</td>

<td>2015.05</td>

<td>AMD Radeon® R7 M270</td>

<td>Untested</td>

<td>N/A</td>

<td>Yes, works out of the box</td>

<td>Yes, works out of the box</td>

<td>Suspend-to-RAM perfect. Hibernate untested. Disk spindown untested.</td>

<td>No modem</td>

<td>HDMI is currently untested. The touchpad (clickpad) needs some tweaking to work properly.</td>

<td>Webcam works, SD card reader untested</td>

</tr>

<tr>

<td>Inspiron M5030</td>

<td>Any</td>

<td>[ATI](/index.php/ATI "ATI") works fine, [catalyst](/index.php/Catalyst "Catalyst") untested</td>

<td>Yes, works out of the box</td>

<td>Yes</td>

<td>Yes, works out of the box</td>

<td>N/A</td>

<td>Untested</td>

<td>N/A</td>

<td>Everything works alright, and out of the box.</td>

<td>[i8kutils](https://aur.archlinux.org/packages/i8kutils/)<sup><small>AUR</small></sup> required for fan control</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Dell&oldid=403655](https://wiki.archlinux.org/index.php?title=Laptop/Dell&oldid=403655)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")