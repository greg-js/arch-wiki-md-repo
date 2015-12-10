# Laptop/Samsung

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** Merge some of the shorter pages from [Category:Samsung](/index.php/Category:Samsung "Category:Samsung") (Discuss in [Talk:Laptop/Samsung#](https://wiki.archlinux.org/index.php/Talk:Laptop/Samsung))

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - **Samsung** - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

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

<td>R65-Pro T5500 Boteez</td>

<td>2008.06 overlord</td>

<td>GeForce 7600 Go</td>

<td>hda-intel</td>

<td>BCM4401B0 100BaseTX</td>

<td>Intel 3945ABG</td>

<td>N/A</td>

<td>Suspend to RAM: N/A  
Disk: N/A  
Battery: No  
Dimming of display: Yes  
CPU frequency scaling: Yes</td>

<td>N/A</td>

<td>N/A</td>

<td>N/A</td>

</tr>

<tr>

<td>Q45 T5750</td>

<td>2009.02</td>

<td>Intel GMA X3100</td>

<td>hda-intel</td>

<td>Marvel 88E8039 (sky2)</td>

<td>Intel 3945ABG (iwl-3945)</td>

<td>N/A</td>

<td>Suspend to RAM: OK  
Disk: OK  
Dimming of display: Yes (with some tricks)  
CPU frequency scaling: Yes</td>

<td>N/A</td>

<td>3G+ modem option GTM378 (hso)  
Web cam (uvcvideo)</td>

<td>N/A</td>

</tr>

<tr>

<td>NC110</td>

<td>2011.08.19</td>

<td>3D with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) 2.19, native resolution with [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) 1.12 (1024x600), external screens work fine</td>

<td>Intel HD Audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes</td>

<td>Yes; rfkill soft block also works</td>

<td>Recognized; not tested</td>

<td>Suspend to RAM: OK  
Disk: Not tested  
Dimming of display: Yes (with `acpi_backlight=vendor`)  
CPU frequency scaling: Yes</td>

<td>N/A</td>

<td>Web cam works, card reader works, two-fingered scrolling works, only half of the function buttons work out-of-the-box ([samsung-tools](https://aur.archlinux.org/packages/samsung-tools/)<sup><small>AUR</small></sup> needed for rest)</td>

<td>N/A</td>

</tr>

<tr>

<td>QX411 W02UB</td>

<td>2011.08.19</td>

<td>Intel HD Graphics 3000 - i915 same packages as above model (1366x768)</td>

<td>Intel HD Audio with ALSA</td>

<td>Realtek Gigabit Ethernet controller (rev 06</td>

<td>Centrino Wireless-N + WiMAX 6150 (rev 67)</td>

<td>N/A</td>

<td>Suspend to RAM: OK  
Disk: OK  
Dimming of display: Yes  
CPU frequency scaling: Yes</td>

<td>N/A</td>

<td>Web cam (uvcvideo)</td>

<td>No tricky hardware. Fully functional.</td>

</tr>

<tr>

<td>NP730U3E (Series 7 Ultra)</td>

<td>2013.06.01</td>

<td>Intel HD Graphics 4000 @ 1920x1080_60 - works fine (i915 w/KMS and [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel));  
AMD Radeon 8570M (muxless hybrid) - Seems to work with PRIME (Linux 3.11);  
external screens not tested.</td>

<td>Intel HDA + ALSA</td>

<td>Realtek Gigabit Ethernet, r8169 driver</td>

<td>Intel Centrino Advanced-N 6235 (rev 24), _iwlwifi_ driver;  
rfkill works with _samsung-laptop_ module</td>

<td>Not tested</td>

<td>Suspend to RAM: OK  
Disk: Not tested  
Dimming of display: Yes  
CPU frequency scaling: Yes</td>

<td>N/A</td>

<td>Web cam - _uvcvideo_, works ok;  
Card reader Realtek RTS5139 - staging driver, works as of Linux 3.11;  
Fn keys - only brightness and sound out-of-the-box;  
Elan Touchpad works perfectly (Linux 3.11);  
Cannot wake up on lid open;</td>

<td>Somewhat tricky, needs work.</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Samsung&oldid=375511](https://wiki.archlinux.org/index.php?title=Laptop/Samsung&oldid=375511)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Samsung](/index.php/Category:Samsung "Category:Samsung")