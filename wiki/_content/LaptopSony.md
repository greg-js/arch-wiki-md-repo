# Laptop/Sony

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table style="background-color: #f3f9ff; margin: 1em 2.5% 0 2.5%; border: 1px solid #aaa;">

<tbody>

<tr>

<td align="center" style="padding: 0.5em; font-size: medium;">[Laptop main page](/index.php/Laptop "Laptop")</td>

</tr>

<tr>

<td align="center" style="padding: 0.5em;">[Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - **Sony** - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other")</td>

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

<td>Vaio VGN-S5M</td>

<td>Any</td>

<td>3D with nvidia driver</td>

<td>Intel audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes</td>

<td>Yes, ipw2200bg</td>

<td>--</td>

<td>Suspend-to-RAM with suspend2</td>

<td>Untested</td>

<td>Memory stick reader does not work</td>

<td>Everything else (Fn Keys, DVD-RW drive, FireWire...) works without a hitch</td>

</tr>

<tr>

<td>Vaio VGN-C2Z</td>

<td>Any</td>

<td>3D with nvidia driver</td>

<td>Intel audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>Yes</td>

<td>Yes, ipw3945</td>

<td>Modules look fine but due to lack of a Bluetooth client not tested</td>

<td>Suspend-to-RAM with vanilla kernel & [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup></td>

<td>Untested</td>

<td>Memory stick reader not tested</td>

<td>Everything else (Fn Keys, DVDRW drive, Firewire...) works without a hitch</td>

</tr>

<tr>

<td>Vaio VGN-FS742/W  
VGN-FS630/W</td>

<td>Kernel 2.6.23.12-3</td>

<td>i810</td>

<td>Intel audio with [ALSA](/index.php/ALSA "ALSA")</td>

<td>e100</td>

<td>ipw2200</td>

<td>No</td>

<td>acpi_cpufreq, sonyacpi</td>

<td>Untested</td>

<td>Memory stick might work</td>

<td>Fn keys with FSFN</td>

</tr>

<tr>

<td>Vaio VGN-NR320FH</td>

<td>2008-06</td>

<td>Intel GMA965/X3100 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver)</td>

<td>Intel audio with ALSA</td>

<td>Do not know, but works out-of-the-box</td>

<td>Atheros AR5006EG/AR242x (madwifi 0.9.4.3844-2)</td>

<td>No</td>

<td>acpi_cpufreq, sony-laptop</td>

<td>Untested</td>

<td>Memory stick might work</td>

<td>Fn keys with sony-laptop and sonypid. Using `vga` option in kernel line in [GRUB](/index.php/GRUB "GRUB") might give problems with resolution. Pretty cool laptop, everything works out-of-the-box except Fn keys for which I needed to do some research.</td>

</tr>

<tr>

<td>Vaio VGN-N130G</td>

<td>2010 (right now with kernel 2.6.34)</td>

<td>[xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver</td>

<td>Intel audio with ALSA</td>

<td>Do not know, but works out-of-the-box</td>

<td>ipw3945</td>

<td>No</td>

<td>Untested</td>

<td>Untested</td>

<td>Memory stick might work</td>

<td>The only problem I have had is with the Wi-Fi randomly cutting out (`netcfg -r` to reconnect). I think this is a problem with MY laptop, rather than this model in general.</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Sony&oldid=375512](https://wiki.archlinux.org/index.php?title=Laptop/Sony&oldid=375512)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Sony](/index.php/Category:Sony "Category:Sony")