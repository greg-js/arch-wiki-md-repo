# Laptop/Acer

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">**Acer** - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

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

<td>TravelMate 2413NLC</td>

<td>Gimmick 0.7.2</td>

<td>Intel GMA 915 driver: _i810_</td>

<td>Intel 82801FB with internal microphone</td>

<td>OK</td>

<td>--</td>

<td>--</td>

<td>Suspend to RAM: Yes  
Disk: Yes  
Battery: Yes  
CPU frequency scaling: Yes</td>

<td>untested</td>

<td>Hot keys: untested</td>

</tr>

<tr>

<td>Aspire 5100-3825</td>

<td>0.8 (Voodoo)</td>

<td>ATI Radeon Xpress 1100</td>

<td>Intel</td>

<td>Realtek</td>

<td>Atheros</td>

<td>n/a</td>

<td>untested</td>

<td>Hot keys: untested</td>

</tr>

<tr>

<td>Aspire 1501LMi</td>

<td>0.9 (Don't Panic)</td>

<td>ATI Radeon 9600: HW acceleration only with proprietary driver</td>

<td>VIA: OK</td>

<td>Broadcom: OK</td>

<td>untested</td>

<td>none</td>

<td>Suspend to RAM: ??  
Disk: Yes  
Battery: Yes  
CPU frequency scaling: Yes</td>

<td>untested</td>

<td>Hot keys: untested</td>

</tr>

<tr>

<td>Travelmate 6292</td>

<td>Core Dump,  
Overlord</td>

<td>Intel x3100: HW acceleration with Intel's open-source driver, ~1100 FPS in the glxgears</td>

<td>Intel HDA: OK (model=acer)</td>

<td>Broadcom BCM5787M: OK</td>

<td>Intel iwl4965: OK</td>

<td>Broadcom: OK</td>

<td>Suspend to RAM: ??  
Disk: Ok  
Battery: Yes  
CPU frequency scaling: Yes</td>

<td>untested</td>

<td>Hot keys: untested  
FireWire (Texas Instruments) TSB43AB23: OK(?)</td>

<td>FireWire detects well but I haven't tested it yet</td>

</tr>

<tr>

<td>Aspire 5024</td>

<td>0.7.2</td>

<td>ATI Radeon X700  
Runs Compiz on both fglrx ([catalyst](https://aur.archlinux.org/packages/catalyst/)<sup><small>AUR</small></sup>) >= 8.02 and radeon driver</td>

<td>AC97: OK</td>

<td>Realtek: OK</td>

<td>Broadcom 4318  
Needs _acer_apci_ + firmware or ndiswrapper driver</td>

<td>N/A</td>

<td>Battery: Yes  
Suspend: Video and Wi-Fi problems  
CPU frequency scaling: powernow-k8 driver</td>

<td>untested</td>

<td>KeyTouch works for hot keys  
Volume control, etc.</td>

</tr>

<tr>

<td>[Aspire 7720](/index.php/Acer_Aspire_7720 "Acer Aspire 7720")</td>

<td>2009.02</td>

<td>Intel i965</td>

<td>ALC268: working OK</td>

<td>Broadcom BCM5787M (tg3): OK</td>

<td>Intel 3945: Needs microcode</td>

<td>Detected, works</td>

<td>Battery: Yes  
Suspend: Seems to work ok  
Hibernation: still flaky (often hangs in the middle of restoring)</td>

<td>With linuxant drivers, might work</td>

<td>Web cam driver: _uvcvideo_; card reader: only SD cards seem to work; special keys (Acer Arcade, direct access to browser/mail) seem to not work; volume knob at the side is seen as a multimedia key.</td>

<td>FireWire seems to be recognized, untested. For 64-bit, update BIOS to fix ACPI and wireless problems.</td>

</tr>

<tr>

<td>[Aspire E5-573](/index.php/Acer_Aspire_E5-573 "Acer Aspire E5-573")</td>

<td>2015.12</td>

<td>Intel i965</td>

<td>OK</td>

<td>OK</td>

<td>OK</td>

<td>not detected</td>

<td>OK</td>

<td>not present</td>

<td>...</td>

<td>...</td>

</tr>

<tr>

<td>Aspire 7730</td>

<td>2009.08 i686 & x86_64</td>

<td>Intel Mobile 4 Series  
i810  
Autoconfiguration works. Compiz OK, with indirect rendering.</td>

<td>ALC888  
Playback & internal microphone: OK; microphone input socket: not tested  
`options snd-hda-intel model=laptop` added to `/etc/modprobe.d/sound.conf` to get headphone output working</td>

<td>OK</td>

<td>OK, with iwlagn</td>

<td>None</td>

<td>Suspend to RAM: OK  
Suspend to disk crashes on i686, OK on x86_64  
CPU frequency scaling: OK  
(using cpufreq)</td>

<td>Untested</td>

<td>Hot keys: OK  
Web cam: OK  
HDMI: untested  
Card reader: untested</td>

<td>Problem booting install CD  
Solved with `ln -sf /dev/sr0 /dev/archiso` at ramfs</td>

</tr>

<tr>

<td>TravelMate 8371G (TM8371G-944G32n)</td>

<td>2010.05 x86_64</td>

<td>Intel GM45, works with _i915_. Radeon HD 4330 listed but cannot switch to it.</td>

<td>OK</td>

<td>OK, works with _r8169_</td>

<td>OK, works with _iwlagn_</td>

<td>OK, works with _btusb_</td>

<td>s2ram works (see remarks), s2disk works, CPU scaling works, no fan control</td>

<td>No modem</td>

<td>Web cam works with _uvcvideo_.  
Card reader works.  
Fingerprint reader does not seem to have a driver!</td>

<td>Suspend to RAM only works with the `i8042.reset=1` kernel parameter. Otherwise, it fails to wake up, and ends up rebooting itself uncleanly!  
Generally, this Acer seems to work quite well with Arch Linux :-)</td>

</tr>

<tr>

<td>Aspire 4935</td>

<td>2009.08 x86_64</td>

<td>Nvidia GeForce 9300M GS</td>

<td>OK, Intel HDA</td>

<td>OK</td>

<td>OK</td>

<td>Untested</td>

<td>Suspend to RAM: OK  
Suspend to disk: OK  
Frequency scaling: OK  
(using cpufreq)</td>

<td>Untested</td>

<td>Hot keys: OK  
Audio touch panel NOT working  
Web cam: OK  
HDMI: OK</td>

<td>By "audio touch panel" I mean the illuminated plastic hot key touch panel on the right-hand side of the keyboard.</td>

</tr>

<tr>

<td>AspireOne D255e</td>

<td>[Archboot 2010.12-1](https://wiki.archlinux.org/index.php/Archboot)</td>

<td>Intel GMA 3150</td>

<td>OK</td>

<td>OK, Atheros 8132 worked only with latest Archboot not official images</td>

<td>OK, Broadcom worked only with latest Archboot not official images</td>

<td>Untested</td>

<td>Untested</td>

<td>Untested</td>

<td>Hot keys: OK  
Synaptic Touchpad: OK</td>

</tr>

<tr>

<td>Aspire 2920Z</td>

<td>2009.2</td>

<td>Intel Mobile GM965/GL960 Integrated Graphics Controller</td>

<td>OK, Intel 82801H</td>

<td>OK, Broadcom NetLink BCM5787M Gigabit Ethernet PCI Express</td>

<td>OK, Broadcom BCM4311 802.11b/g WLAN</td>

<td>n/a</td>

<td>Suspend to RAM: OK.  
Suspend to disk: OK.  
CPU frequency scaling: untested</td>

<td>Untested</td>

<td>Hot keys: web, mail, and wireless work. Blue _e_ on the left: not working  
Synaptic touchpad: OK  
</td>

<td>Not everything worked fine on fresh installation. Requires some work.</td>

</tr>

<tr>

<td>Aspire 5735z [[1]](http://panam.acer.com/acerpanam/notebook/0000/Acer/Aspire5735Z/Aspire5735Zsp3.shtml)</td>

<td>archlinux-2014.09.03-dual</td>

<td>Intel GMA 4500M</td>

<td>OK</td>

<td>OK</td>

<td>OK</td>

<td>Untested</td>

<td>Suspend to RAM: OK.  
Suspend to disk: OK.  
CPU frequency scaling: untested</td>

<td>Untested</td>

<td>Hot keys: OK (except Bluetooth: untested)  
Synaptic Touchpad: OK</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Acer&oldid=411299](https://wiki.archlinux.org/index.php?title=Laptop/Acer&oldid=411299)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")