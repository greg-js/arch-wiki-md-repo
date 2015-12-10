# Acer Aspire 7720

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

For 64-bit install, update BIOS first to fix ACPI and wireless problems. If you use 32-bit there shouldn't be problems.

## What doesn't work

Hibernation (is still flaky). Suspend seems to work OK with kernel 2.6.35, xorg 1.9.

<table class="wikitable">

<tbody>

<tr>

<th>Hardware</th>

<th>Details</th>

<th>Status</th>

</tr>

<tr>

<td>HDD</td>

<td>WDC WD2500BEVS-22UST0 250GB</td>

<td>Works.</td>

</tr>

<tr>

<td>Screen/Graphics</td>

<td>Acer 17" (1440x900), Intel x3100</td>

<td>Works fully.</td>

</tr>

<tr>

<td>Wireless</td>

<td>Intel 3945</td>

<td>Works after you install the firmware. I used netcfg2 or wicd for management of WLAN.</td>

</tr>

<tr>

<td>Ethernet</td>

<td>Broadcom BCM5787 (tg3 driver)</td>

<td>Works out of box.</td>

</tr>

<tr>

<td>Audio</td>

<td>Realtek ALC268</td>

<td>Working well. Recording from the internal microphone is flawed, however.</td>

</tr>

<tr>

<td>Card Reader</td>

<td>5-in-1 card reader supports optional MultiMediaCard™, Secure Digital card, Memory Stick®, Memory Stick PRO™ or xD-Picture Card™</td>

<td>Works only for SD? MS is not recognized?</td>

</tr>

<tr>

<td>Webcam</td>

<td>Acer "Crystal Eye" Webcam</td>

<td>Works (uvcvideo)</td>

</tr>

<tr>

<td>Touchpad</td>

<td>ALPS PS/2</td>

<td>Works (with current X releases no need to configure).</td>

</tr>

<tr>

<td>Bluetooth</td>

<td>Broadcom "A-Link BlueUsbA2"</td>

<td>Works</td>

</tr>

<tr>

<td>Remote control sensor</td>

<td>Works: install LIRC, the driver is lirc_ene0100\. I successfully command MPD and MPlayer with it.</td>

</tr>

</tbody>

</table>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_7720&oldid=304875](https://wiki.archlinux.org/index.php?title=Acer_Aspire_7720&oldid=304875)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")