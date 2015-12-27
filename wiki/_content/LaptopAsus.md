# Laptop/Asus

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - **Asus** - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

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

<td>K55N</td>

<td>2014.11.12</td>

<td>Radeon HD 7520G - install [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)</td>

<td>snd,snd_hda_codec works out of the box using pulseaudio</td>

<td>r8169 module, out of the box</td>

<td>ath9k module, out of the box</td>

<td>not present</td>

<td>Overheats and immediately shuts down on modern 3D games. Use thermald to control temp using acpi_cpufreq</td>

<td>webcam works</td>

<td>Fix fn brightness keys with "acpi_osi="!Windows 2012" video.use_native_backlight=1". Don't enable early radeon hook to prevent blank screen after hibernation. Fix blank screen on suspend to ram with "sysctl -w kernel.acpi_video_flags=3".</td>

</tr>

<tr>

<td>X401U</td>

<td>2014.01.05</td>

<td>Radeon HD 7340 - install [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati)</td>

<td>did not work out of the box, never configured correctly, using pulse, everything works</td>

<td>not tested</td>

<td>Wi-Fi out of the box</td>

<td>none to support</td>

<td>all power options work just fine</td>

<td>webcam works</td>

<td>overall performance is satisfactory</td>

</tr>

<tr>

<td>X401A/X401A1</td>

<td>2013.05.01</td>

<td>Integrated Intel HD Graphics - install [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) and [libva-intel-driver](https://www.archlinux.org/packages/?name=libva-intel-driver), enable SNA</td>

<td>hda-intel works, headphone jack, mic works</td>

<td>Realtek, out of the box</td>

<td>Wi-Fi out of the box</td>

<td>not tested</td>

<td>all power options work just fine, only brightness control needs module asus-nb-wmi to be loaded and `acpi_backlight=intel acpi_osi=` [GRUB](/index.php/GRUB "GRUB") options as of kernel 3.9.4</td>

<td>webcam works</td>

<td>overall performance is satisfactory</td>

</tr>

<tr>

<td>W7S</td>

<td>Don't Panic</td>

<td>3D with NVIDIA drivers</td>

<td>hda-intel</td>

<td>r8169 module, out of the box</td>

<td>Intel 4965 works with iwlwifi</td>

<td>works out of the box</td>

<td>suspend works with [pm-utils](/index.php/Pm-utils "Pm-utils"); hibernation is extremely unstable</td>

<td>webcam works with uvc drivers, but it is mounted upside down</td>

<td>ACPI works with acpi4asus and acpid</td>

</tr>

<tr>

<td>[N80Vn-X5](/index.php/ASUS_N80VN "ASUS N80VN")</td>

<td>2009.02RC2</td>

<td>3D with NVIDIA drivers</td>

<td>hda-intel plus adding `options snd-hda-intel enable=1 model=g50v position_fix=0` to `/etc/modprobe.d/modprobe.conf`</td>

<td>Out of box with r8169 module</td>

<td>out of box with ath9k</td>

<td>out of box</td>

<td>suspend and hibernate both work with [pm-utils](/index.php/Pm-utils "Pm-utils")</td>

<td>webcam and card reader both work out of the box</td>

<td>ACPI works fine with the `asus_laptop` module</td>

</tr>

<tr>

<td>F8SN</td>

<td>2009.08</td>

<td>only tried with open source NV drivers (got 1280x800 pixels default without xorg edit), 3D proprietary will probably work</td>

<td>hda-intel</td>

<td>Ethernet works out of the box</td>

<td>Intel 4965 works with iwlwifi</td>

<td>untested-but is recognized by kernel</td>

<td>untested-battery status can be detected and customization options exist</td>

<td>Syntek Sonic web cam and Ricoh Card reader work out of the box (might need to allow user mount privileges just as you would for other ext. drives)</td>

<td>Highly compatible with Arch Linux</td>

</tr>

<tr>

<td>L3000D</td>

<td>Most recent as of 2010-02-13</td>

<td>Works out of box</td>

<td>Works out of box</td>

<td>Works out of box</td>

<td>Not contains</td>

<td>Not contains</td>

<td>Works perfectly</td>

<td>Untested</td>

</tr>

<tr>

<td>[N53JN](/index.php/ASUS_N53JN "ASUS N53JN")</td>

<td>Most recent as of 2010-11-03</td>

<td>Contains NVIDIA Optimus, so only Intel graphic card works. Waiting for NVIDIA to support Optimus on Linux</td>

<td>Works, needs some editing of modprobe files</td>

<td>Works out of box</td>

<td>ath9k</td>

<td>Untested</td>

<td>Hibernate untested, suspend works but with problems due to USB3 controller</td>

<td>Web cam works, touchpad works, media buttons work</td>

</tr>

<tr>

<td>N53SV</td>

<td>Most recent as of 2011-06-26</td>

<td>Contains NVIDIA Optimus, so only Intel graphic card works.</td>

<td>hda-intel</td>

<td>r8169 module, works out of box</td>

<td>ath9k needs madwifi</td>

<td>Untested</td>

<td>[BBS thread](https://bbs.archlinux.org/viewtopic.php?pid=910195)</td>

<td>Web cam works, touchpad works, card reader works. See also [Ubuntu help](https://help.ubuntu.com/community/Asus_N53)</td>

</tr>

<tr>

<td>A8Le</td>

<td>Most recent as of 2011-07-31</td>

<td>Works out of box</td>

<td>Works out of box (with [ALSA](/index.php/ALSA "ALSA"), 'Speaker' channel should be un-muted)</td>

<td>Out of box with r8169 module</td>

<td>Untested</td>

<td>Untested</td>

<td>Untested</td>

<td>Touchpad works</td>

</tr>

<tr>

<td>1005HA</td>

<td>2011.08.19</td>

<td>Works out of box using i915</td>

<td>hda-intel</td>

<td>Works out of box</td>

<td>ath9k</td>

<td>Untested</td>

<td>Untested</td>

</tr>

<tr>

<td>1015E</td>

<td>2014.05.19</td>

<td>Works out of box using i915</td>

<td>hda-intel</td>

<td>Works out of the box.</td>

<td>Wifi out of the box.</td>

<td>Untested</td>

<td>Display brightness and toggle, battery management, power, lid close works out of the box. Suspend works out of the box. Hibernate works after following instructions [here](/index.php/Suspend_and_hibernate#Hibernation "Suspend and hibernate").</td>

<td>Touchpad requires [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) package. Webcam/mic works. Card reader works. USB 3.0 untested.</td>

<td>Overall satisfactory. Keyboard fn keys do not work, except for brightness/display controls and sleep button. Volume controls are recognized inputs but have to be manually assigned.</td>

</tr>

<tr>

<td>[UL30A](/index.php/ASUS_UL30A "ASUS UL30A")</td>

<td>2011.08.19</td>

<td>Works out of box</td>

<td>hda-intel</td>

<td>Works out of box</td>

<td>Untested</td>

<td>Untested</td>

<td>Untested</td>

<td>Web cam works, touchpad works, card reader untested</td>

<td>`acpi_backlight=vendor` in bootloader</td>

</tr>

<tr>

<td>[G73SW](/index.php/ASUS_G73SW "ASUS G73SW")</td>

<td>2011.08.19</td>

<td>nvidia</td>

<td>hda-intel</td>

<td>Works out of box</td>

<td>Works out of box</td>

<td>None</td>

<td>Untested</td>

<td>Backlit keys worked when I installed [GNOME](/index.php/GNOME "GNOME")</td>

<td>Power settings need work...</td>

</tr>

<tr>

<td>Q400A</td>

<td>Works out of box using i915</td>

<td>hda-intel, mic works</td>

<td>AR8151v2 works out of box</td>

<td>Works out of box</td>

<td>Works out of the box</td>

<td>Suspend works, Hibernate untested</td>

<td>Backlit keys work on GNOME 3, screen backlight works with keys in gnome-3.10, touchpad works, webcam works, card reader works, HDMI output untested</td>

</tr>

<tr>

<td>[Q500A](/index.php/Asus_Q500A "Asus Q500A")</td>

<td>2015.02.01</td>

<td>[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel), works out of box</td>

<td>hda-intel, works out of box</td>

<td>r8169, works out of box</td>

<td>iwlwifi, works out of box</td>

<td>untested but detected by bluez</td>

<td>Suspend works, Hibernate works.</td>

<td>Works very well with Arch Linux</td>

</tr>

<tr>

<td>K55VM</td>

<td>2013.04.01</td>

<td>Contains NVIDIA Optimus, both works. Intel and Nvidia(proprietary drivers)</td>

<td>hda-intel</td>

<td>r8168 module, works</td>

<td>ath9k Works out of box</td>

<td>Untested</td>

<td>suspend and hibernate both work with gnome power manager and [laptop-mode-tools](/index.php/Laptop-mode-tools "Laptop-mode-tools")</td>

<td>Web cam works, touchpad works, card reader works, sound card works</td>

<td>Highly compatible with Arch Linux. Technology optimus works with [Bumblebee](/index.php/Bumblebee "Bumblebee")</td>

</tr>

<tr>

<td>[A55VJ](/index.php/ASUS_A55VJ "ASUS A55VJ")</td>

<td>2013.05.01</td>

<td>Contains NVIDIA Optimus, both work (NVIDIA only via [Bumblebee](/index.php/Bumblebee "Bumblebee"))</td>

<td>hda-intel</td>

<td>r8169 module works</td>

<td>iwlwifi</td>

<td>Works with bluez</td>

<td>suspend works out of box with systemd/logind.conf</td>

<td>Web cam works, touchpad works, card reader works</td>

<td>Highly compatible with Arch Linux. Add `i8042.nomux=1` to kernel line to prevent jittery touchpad.</td>

</tr>

<tr>

<td>S300CA</td>

<td>2013.08.01</td>

<td>Intel HD Graphics 4000, works out of the box with xf86-video-intel</td>

<td>hda-intel</td>

<td>Atheros AR8161, works out of the box</td>

<td>Atheros AR9485, works out of the box with ath9k</td>

<td>not tested</td>

<td>works, slightly higher power usage as Windows 8, for backlight add `acpi_osi=Linux acpi_backlight=vendor` to bootloader kernel line</td>

<td>Web cam, touchpad, touchscreen all work, USB 3.0 and car reader not tested yet</td>

<td>Highly compatible with Arch Linux.</td>

</tr>

<tr>

<td>S400CA</td>

<td>2015.02.01</td>

<td>Intel HD Graphics 4000, works out of the box with xf86-video-intel</td>

<td>hda-intel, works out of the box</td>

<td>Atheros AR8161, works out of the box</td>

<td>Atheros AR9485, works out of the box</td>

<td>not tested</td>

<td>works, for backlight add `acpi_osi=Linux acpi_backlight=vendor` to bootloader kernel line</td>

<td>Webcam work out of the box, touchpad work out of the box with xf86-input-synaptics, touchscreen all work, USB 3.0 and card reader not tested yet</td>

<td>Highly compatible with Arch Linux.</td>

</tr>

<tr>

<td>[X502CA](/index.php/X502CA "X502CA")</td>

<td>2013.07.01</td>

<td>Integrated Intel HD Graphics works</td>

<td>hda-intel works</td>

<td>Qualcomm Atheros AR816x/AR817x, did not work during installation, after that works, but check model specific wiki</td>

<td>Ralink RT3290 performs very poorly with standard kernel driver. Check model specific wiki</td>

<td>not tested</td>

<td>suspend works, see model specific wiki for display brightness control</td>

<td>not tested</td>

<td>not a very good choice for Linux due to Wi-Fi problems</td>

</tr>

<tr>

<td>X53BR/K53BR</td>

<td>anything since 3.11 kernel</td>

<td>ATI 6320/ATI 7470 works, but can't disable discrete. Intervention needed since 3.13</td>

<td>hda-intel works</td>

<td>Realtek with r8169 driver, out-of-the-box</td>

<td>Qualcomm Atheros AR9485 with ath9k driver, out-of-the-box</td>

<td>-</td>

<td>three different brightness switches in /sys/class/backlight for the same display, anything else fine</td>

<td>webcam fine</td>

<td>heats up very fast, description coming</td>

</tr>

<tr>

<td>X551CA</td>

<td>2014\. 03\. 24\.</td>

<td>Integrated Intel, works with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)</td>

<td>hda-intel</td>

<td>Realtek r8169, did not tested</td>

<td>Qualcomm Atheros AR9485, oob, but problems with NetworkManager - disabling the wifi hardblocks the card and Fn+F2 doesn't work. Workaround on [Ubuntu forum.](http://ubuntuforums.org/showthread.php?t=2181558)</td>

<td>not tested</td>

<td>I didn't tested yet, but at first sight it seems ok.</td>

<td>not tested.</td>

<td>It seems to work well with Linux</td>

</tr>

<tr>

<td>[N550JV](/index.php/N550JV "N550JV")</td>

<td>2014.03.01\.</td>

<td>Hybrid graphics with integrated [Intel](/index.php/Intel "Intel") and NVIDIA GeForce GT 750M [Nouveau](/index.php/Nouveau "Nouveau") working with [Bumblebee](/index.php/Bumblebee "Bumblebee") ([NVIDIA](/index.php/NVIDIA "NVIDIA") driver works but not tested extensively)</td>

<td>snd_hda_intel works but external speakers pop on sleep/shutdown</td>

<td>Realtek r8169 works out of box</td>

<td>Qualcomm Atheros AR9485 works with ath9k out of the box</td>

<td>not tested</td>

<td>working, USB must be disabled before sleep</td>

<td>no modem</td>

<td>Card reader works out of box, has battery issues when a powered device is left plugged into the USB charging port.</td>

</tr>

<tr>

<td>G550JK</td>

<td>2014.08.01</td>

<td>Uses Nvidia Optimus, works fine with [Bumblebee](/index.php/Bumblebee "Bumblebee") using Nvidia's drivers</td>

<td>snd_hda_intel - some background noises while using headphones: here is a [fix](http://xps13-9333.appspot.com/#background_noise)</td>

<td>Not tested</td>

<td>Works out of the box</td>

<td>Not tested</td>

<td>I didn't tested much but it seems to work</td>

<td>Not tested</td>

<td>touchpad and camera works fine</td>

</tr>

<tr>

<td>X83VB-X2</td>

<td>2014.09.01</td>

<td>GeForce 9300M GS, Works out of the box with xf86-video-intel</td>

<td>Works out of box (with ALSA, 'Speaker' channel should be un-muted)</td>

<td>Ethernet works out of the box</td>

<td>Wifi works out of the box</td>

<td>Bluetooth not tested</td>

<td>Not tested but seems to work fine</td>

<td>Not tested</td>

<td>Touchpad works, Camera not tested</td>

</tr>

<tr>

<td>UX303LN</td>

<td>2014.10.01</td>

<td>GeForce 840M & Intel HD Graphics, Had to install [Bumblebee](/index.php/Bumblebee "Bumblebee") to get both working</td>

<td>Works out of box (with ALSA, 'Speaker' channel should be un-muted)</td>

<td>USB-to-Ethernet devices seem to work fine out of the box</td>

<td>Wifi works out of the box</td>

<td>Bluetooth not tested</td>

<td>Not tested but seems to work fine</td>

<td>Not tested</td>

<td>Touchpad works (no gestures currently), Camera works fine, Touchscreen works (no multi-touch support)</td>

</tr>

<tr>

<td>UX32L(N)</td>

<td>N/A</td>

<td>GeForce 840M & Intel HD Graphics (Haswell-ULT rev09), Use [bbswitch](/index.php/Bumblebee#Default_power_state_of_NVIDIA_card_using_bbswitch "Bumblebee") and the Intel GPU as the proprietary nvidia driver breaks vsync and causes quite a few crashes in Plasma 5\.</td>

<td>Works out of box</td>

<td>Factory-supplied USB-to-Ethernet adapter works fine, consider getting a USB 3.0 1 Gbit/s adapter if you need more than 100 Mbit/s</td>

<td>Qualcomm Atheros AR9462 with ath9k driver, out-of-the-box</td>

<td>Powers on, no further testing done</td>

<td>Suspend and Hibernate work</td>

<td>Set the kernel parameters `video.use_native_backlight=1 acpi_osi=` for working backlight keys and backlight restore. Clickpad may require some fiddling with synaptics settings to get comfortable options, very rarely locks up which can be fixed using `xinput` to disable and re-enable it. Webcam works. Keyboard backlight and adjustment thereof works.</td>

</tr>

<tr>

<td>U32U</td>

<td>2015.02.01</td>

<td>Radeon 6320, Install xf86-video-ati</td>

<td>Works out of box (with ALSA)</td>

<td>Ethernet works fine out of the box</td>

<td>Wifi works out of the box</td>

<td>Bluetooth works with bluez5, optionally install bluetooth manager</td>

<td>Suspend does not work. CPU Fan constantly on.</td>

<td>Webcam works</td>

<td>Needs significant setup to function properly. Power management hard to get right.</td>

</tr>

<tr>

<td>[X553MA](/index.php/ASUS_X553MA "ASUS X553MA")</td>

<td>2015.06.01</td>

<td>Works</td>

<td>Works</td>

<td>Works</td>

<td>[broadcom-wl](/index.php/Broadcom_wireless#broadcom-wl "Broadcom wireless") (causes freezes)</td>

<td>Untested</td>

<td>Suspend works</td>

<td>Set `OS Selection` in BIOS setup to `Windows 7`</td>

</tr>

<tr>

<td>F550J(aka A550J)</td>

<td>2015.09.01</td>

<td>Intel HD4600(integrated, works well witth [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel)), Nvidia 850M(can't enter [GNOME](/index.php/GNOME "GNOME") desktop environment(message "Critical issue") with driver [nvidia](https://www.archlinux.org/packages/?name=nvidia) installed)</td>

<td>Intel HD Audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Works out of box : Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 12)</td>

<td>Broadcom Corporation BCM43142 802.11b/g/n (rev 01), works well with [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)<sup><small>AUR</small></sup> installed (refer to [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless"))</td>

<td>Not tested</td>

<td>Not tested</td>

<td>N/A</td>

<td>You should install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) to enable touchpad</td>

<td>Recommend to disable standalone graphic card</td>

</tr>

<tr>

<td>[N550JX](/index.php/ASUS_N550JX "ASUS N550JX")</td>

<td>2015.12.01</td>

<td>Works</td>

<td>Works</td>

<td>Works</td>

<td>Works</td>

<td>Works</td>

<td>Works</td>

<td>N/A</td>

<td>Read [N550JX](/index.php/ASUS_N550JX "ASUS N550JX")</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Asus&oldid=413584](https://wiki.archlinux.org/index.php?title=Laptop/Asus&oldid=413584)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [ASUS](/index.php/Category:ASUS "Category:ASUS")