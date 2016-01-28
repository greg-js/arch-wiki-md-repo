# Lenovo Thinkpad Edge E455

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** See [Category:Laptops](/index.php/Category:Laptops "Category:Laptops") (Discuss in [Talk:Lenovo Thinkpad Edge E455#](https://wiki.archlinux.org/index.php/Talk:Lenovo_Thinkpad_Edge_E455))

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>AMD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>xf86-video-ati</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>r8169</td>

</tr>

<tr>

<td>Wireless</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>rtl8723be</td>

</tr>

<tr>

<td>Audio</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>xf86-input-synaptics</td>

</tr>

<tr>

<td>Camera</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>linux-uvc</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>rtsx_pci</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>bluez</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Tested Configurations](#Tested_Configurations)
*   [2 System Configuration](#System_Configuration)
    *   [2.1 Wifi](#Wifi)
    *   [2.2 Hybrid Graphics](#Hybrid_Graphics)
    *   [2.3 Backlight](#Backlight)
    *   [2.4 Hot Keys](#Hot_Keys)
    *   [2.5 ClickPad](#ClickPad)
    *   [2.6 Suspend to ram](#Suspend_to_ram)
    *   [2.7 Keyboard](#Keyboard)
*   [3 Known issues](#Known_issues)
    *   [3.1 Clickpad](#Clickpad_2)

## Hardware

### Tested Configurations

**Tip:** Below are the tested configurations at the time.

<table class="wikitable sortable">

<tbody>

<tr>

<th>Feature</th>

<th>Configuration</th>

</tr>

<tr>

<td>System</td>

<td>E455 20DE-CTO1WW</td>

</tr>

<tr>

<td>CPU</td>

<td>AMD(R) A10-7300 Radeon R6(R) CPU @ 1.9GHz</td>

</tr>

<tr>

<td>Graphics</td>

<td>AMD Radeon R6 (Integrated Card) + AMD Radeon R7 M260DX (Discrete Card)</td>

</tr>

<tr>

<td>Ram</td>

<td>4GB</td>

</tr>

<tr>

<td>Disk</td>

<td>500GB</td>

</tr>

<tr>

<td>Display</td>

<td>14" WHD</td>

</tr>

<tr>

<td>Wi-Fi</td>

<td>Realtek RTL8723BE PCIe Wireless Network Adapter</td>

</tr>

<tr>

<td>Ethernet</td>

<td>Realtek RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)</td>

</tr>

<tr>

<td>Backlit Keyboard</td>

<td>No</td>

</tr>

<tr>

<td>Fingerprint Scanner</td>

<td>No</td>

</tr>

<tr>

<td>Bluetooth</td>

<td>Yes</td>

</tr>

<tr>

<td>Cam</td>

<td>Yes</td>

</tr>

</tbody>

</table>

## System Configuration

### Wifi

The current driver for RTL8723BE PCIe Wireless Network Adapter can drop signals due to a power saving bug. See [Wireless network configuration#rtl8723be](/index.php/Wireless_network_configuration#rtl8723be "Wireless network configuration").

Also wireless n is unstable so it is recommended to set your router for wireless g modulation.

### Hybrid Graphics

Out of the box, the integrated card is used while the radeon driver dynamically powers off the discrete card. For use of discrete card, see [PRIME](/index.php/PRIME "PRIME").

### Backlight

Due to this system having a [muxless](http://wiki.cchtml.com/index.php/Features#Switchable_Graphic_Chips_Status) hybrid configuration, the backlight controller cannot be detected by the system but it's brightness can be changed by using the /sys/ subsystem. See [Acpid](/index.php/Acpid "Acpid"), to configure brightness functionality.

### Hot Keys

The hotkeys, or the function keys that map into the F[n] buttons, are partially working. The wifi key works out of the box but the sound keys and brightness keys need to be mapped in order to be functional. See [Acpid](/index.php/Acpid "Acpid"), to configure hotkey functionality.

### ClickPad

The clickpad that is used is from Alps. Specifically, it uses Alps protocol 8 which has initial support in kernel 4.1\. While basic functionality works with kernels less than 4.1, there may be issues that occur with use in kernel less than 4.1.

There are two input drivers you can use for touchpad support: synaptics or libinput

Using the synaptics driver,for more advance features such as Vertical Edge Scrolling, see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics"). An interesting quirk that occurs is that in order to be able to use Vertical, or Horizontal, Edge Scrolling you have to enable Two Finger Scrolling. Setting only the Edge Scrolling option in xorg doesn't enable it.

For the libinput driver please see [libinput](/index.php/Libinput "Libinput").

### Suspend to ram

Works out of the box.

### Keyboard

**Fn and Ctrl keys** can be swapped in BIOS.

**Fn key** lock can be switched with **Fn + Esc**.

## Known issues

### Clickpad

**Issue (using the Synaptics Driver):**

After a certain amount of time used, the clickpad interrupts cease to be processed.

**Work-Around (Non-Permanent):**

Reload the "psmouse" kernel module when functionality ceases. Eventually it will cease up again requiring another reload.

 ` # modprobe -r psmouse`  ` # modprobe psmouse` 

**Fix**

In order to fix these problems, use the libinput driver instead of synaptics.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_Thinkpad_Edge_E455&oldid=401532](https://wiki.archlinux.org/index.php?title=Lenovo_Thinkpad_Edge_E455&oldid=401532)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")

Hidden category:

*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")