# Lenovo ThinkPad Edge E430

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The following is regarding the Lenovo Thinkpad Edge E430 with 3rd Generation Ivy Bridge Intel processor, released in mid 2012\. The E430 is intended to be an affordable, yet still entirely capable business machine. Unlike some of its siblings, it is not to military specs, but is still a well built and quite durable machine. If you are reading this with the intention of ordering yourself this machine, do yourself a favor and opt for the Intel WiFi card for the extra ~$20\. The default Realtek works, albiet with a bit of coaxing. Ergo, this article is meant to suppliment the current [Installation guide](/index.php/Installation_guide "Installation guide") or [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 UEFI](#UEFI)
*   [2 Hardware](#Hardware)
    *   [2.1 Realtek Ethernet Compatibility](#Realtek_Ethernet_Compatibility)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 SD Card Reader](#SD_Card_Reader)
*   [3 Fingerprint Reader](#Fingerprint_Reader)
*   [4 Trackpoint](#Trackpoint)
*   [5 Fans](#Fans)
*   [6 X Crashes with Dual Monitors](#X_Crashes_with_Dual_Monitors)

## Installation

With the release of 2012.07.15 and chroot installation process, the documented installation procedure is recommended.

### UEFI

For UEFI info to E430 go to [HCL/Firmwares/UEFI#Lenovo Thinkpad Edge E430 3254-DAQ](/index.php?title=HCL/Firmwares/UEFI&action=edit&redlink=1 "HCL/Firmwares/UEFI (page does not exist)").

## Hardware

As of kernel 3.4.6-1

<table class="wikitable">

<tbody>

<tr>

<th>Device</th>

<th>Works</th>

</tr>

<tr>

<td>Video (Intel HD4000)</td>

<td>Yes</td>

</tr>

<tr>

<td>Ethernet (Realtek RTL8111/8168B)</td>

<td>Yes*</td>

</tr>

<tr>

<td>Wireless (Realtek RTL8188CE/Thinkpad b/g/n)</td>

<td>Yes*</td>

</tr>

<tr>

<td>Bluetooth</td>

<td>Centrino 2230 - Yes (01/07/13)</td>

</tr>

<tr>

<td>Audio (Intel HD Audio)</td>

<td>Yes</td>

</tr>

<tr>

<td>Camera</td>

<td>Yes (01/07/13)</td>

</tr>

<tr>

<td>Finger Print Reader</td>

<td>Yes</td>

</tr>

<tr>

<td>Card Reader (Realtek RTS5229)</td>

<td>Yes*</td>

</tr>

</tbody>

</table>

As usual, Realtek devices require a little work. See below.

### Realtek Ethernet Compatibility

The Realtek RTL8111/8168B ethernet controller may be relatively unreliable with the r8169 module. Better Ethernet connectivity can be achieved with the [r8168](https://www.archlinux.org/packages/?name=r8168) module. See [Network configuration#Realtek RTL8111/8168B](/index.php/Network_configuration#Realtek_RTL8111.2F8168B "Network configuration") for instructions.

### Wireless

If the Thinkpad in question has the Thinkpad branded WiFi adapter, it semi-works out of the box. There may be a delay preceding any attempted network activity, which can be resolved by disabling the power saving feature. The usual

```
# ip link <interface> power off

```

is not a feature of this particular card. Instead, the over aggressive power saving feature may be turned off upon loading the module on boot. (<interface> may no longer be wlan0)

This may be achieved in two ways.

```
# echo "options rtl8192ce fwlps=0" >> /etc/modprobe.d/modprobe.conf

```

Or you may add the following to your kernel boot parameters:

```
rtl8192ce.fwlps=0

```

This will turn off the **f**irm**w**are **l**ow**p**ower**s**tate or fwlps.

If you have not yet ordered your computer, it is advisable to spend the extra money to have it include the Intel Centrino wlan/bluetooth 4.0 card, as it is much better supported. Also, because Lenovo is one of a few companies that whitelist wlan cards, replacing/upgarding can be challenging, costly, or just downright impossible. For example, this model with the Ivy Bridge is new, ergo the wlan cards with the proper FRU (Field Replaceable Unit) number to pass the whitelist, can not yet (7-31-2012) be found on sites such as ebay. To find what FRU's this machine accepts, go the the Lenovo support site where you should be able to find the necessary documentation.

If, like me, you failed to realize that the wireless card was a horribly supported Realtek, and you are now kicking yourself because of the above mentioned whitelist, you do have an option to change it without ordering a Lenovo specific card. Some kind souls are willing to help others modify their BIOS' in various ways, one of which is removal of the whitelist. In this [thread](http://forums.mydigitallife.info/threads/5866-LENOVO-(IBM)-Bioses-especially-Thinkpad/page470?p=643803&viewfull=1#post643803), I was able to get Serg008 to remove the whitelist for the E430\. If you go this route, proceed with caution, as upgrading the BIOS (and messing up) can render your machine a brick. Also, there are legitimate warranty concerns with unauthorized BIOS modifications.

**Note:** Recently, I had to have my motherboard replaced, and ended up with a Lenovo Windows 8 BIOS. Apparently the removal of the whitelist is not as straight forward as in the past. That being the case, I set out to find the compatible FRU for this model. The card is an Intel Centrino Wireless-N 2230, and the Lenovo specific FRU is 04W3765.

### SD Card Reader

**As of 3.8 a 3rd party module is not needed, device is accessible @ /dev/mccX**

The card reader will not work out-of-the-box pre-3.8, but thanks to Icetonic, the necessary kernel module, [rts5229](https://aur.archlinux.org/packages.php?ID=60832), can be found from the Realtek website or from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). Download the tarball and install with [makepkg](/index.php/Makepkg "Makepkg").

**Note:** <s>My personal experience with the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") was that Realtek uses some ridiculous "login" for their ftp download link, thereby dynamically changing the address. I was able to navigate to the site and copy the download link address and insert it into the PKGBUILD so that I could create a pkg.tar.gz and install it with [pacman](/index.php/Pacman "Pacman").</s> Thanks to gehidore for hosting this file. This problem is now fixed.

## Fingerprint Reader

Typically with older hardware, one can get the fingerprint reader to function by using one of two open-source fingerprint reader projects. They are [thinkfinger] and [fprint], but unfortunately both are no longer active, so the newest generations are not supported by these projects. Instead, Ubuntu has put together a system that includes drivers included in these previous projects, as well as including proprietary drivers for the newest models. In typical Ubuntu fashion, it is gui driven and appropriately named [fingerprint-gui](https://aur.archlinux.org/packages.php?ID=40054) and it is available from the [Arch User Repository].

The fingerprint reader included on the newest generation of Thinkpad E430 is a Upek. To verify the model of the device in a given machine, one may use lsusb.

```
$ lsusb
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
_**Bus 001 Device 003: ID 147e:1002 Upek**_

```

The '147e:1002 Upek' being the relevant information here. For help setting up this device, see [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui")

## Trackpoint

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [TrackPoint](/index.php/TrackPoint "TrackPoint").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad Edge E430#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_Edge_E430))

The trackpoint works out of the box, though scroll wheel emulation button needs a bit of configuring. The following will set the middle Trackpoint button to scroll, though it will also disable the possibility of using it to generate a middle click, to enable middle click with scroll set "Emulate3Buttons" to "true"(01/07/13). Create the file /etc/X11/xorg.conf.d/20-thinkpad.conf as root with the following:

```
Section "InputClass"
	Identifier	"Trackpoint Wheel Emulation"
	MatchProduct	"TPPS/2 IBM TrackPoint"
	MatchDevicePath	"/dev/input/event*"
	Option		"EmulateWheel"		"true"
	Option		"EmulateWheelButton"	"2"
        ## set Emulate3Buttons to true to allow middle click (01/07/13)
	Option		"Emulate3Buttons"	"false" 
	Option		"XAxisMapping"		"6 7"
	Option		"YAxisMapping"		"4 5"
EndSection

```

This information was taken from Thinkwiki's page regarding the Trackpoint. You can find it here: [http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint](http://www.thinkwiki.org/wiki/How_to_configure_the_TrackPoint) . Keep in mind that your Trackpoint might be identified by a different "MatchProduct", so you may want to determine the exact indentifier. The easiest way to do this is with the [hwinfo](https://www.archlinux.org/packages/?name=hwinfo) package available in the [Official repositories](/index.php/Official_repositories "Official repositories"). Simply run 'hwinfo' as a normal user or root and look for the PS/2 information.

## Fans

If you so desire, the Thinkfan may be used to control the fan speed. This is probably not necessary as the BIOS seems to typically handle the fan speed just fine. On top of this, these machines typically have enough power to run fairly cool during typical operation, depending, of course, on what typical is for you, the user.

**Warning:** Thinkfan has been [reported](https://bbs.archlinux.org/viewtopic.php?id=151028) to not work on this model currently. Tread lightly.

The thinkpad_acpi kernel module needs to be configured so user space programs can control the fan speed.

 `/etc/modprobe.d/modprobe.conf`  `options thinkpad_acpi fan_control=1` 

The thinkfan configuration file also needs to know how to set the fan speed. Replace the default sensor settings with the following.

 `/etc/thinkfan.conf` 

```
sensor /sys/devices/platform/coretemp.0/temp1_input

```

Direct fan control can be achieved by using "echo" to apply the desired level. Set the speed as shown in the following examples:

```
# echo engage > /proc/acpi/ibm/fan
# echo level auto > /proc/acpi/ibm/fan
# echo level 1 > /proc/etc/ibm/fan

```

Once thinkpad_acpi has been loaded with fan_control=1, available settings can be displayed like so:

```
$ cat /proc/acpi/ibm/fan

```

**Note:** I ordered my computer without a camera or bluetooth because I never use those two things. Other reports I have come across seem to indicate these work without issue, though a bit of configuration is needed.

## X Crashes with Dual Monitors

Starting X on an E430 with an Intel Core i7-3612QM and monitors plugged into both the HDMI and VGA ports results in a crash. Only "fix" I've found is to wait until starting X before plugging in one of the monitors.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Edge_E430&oldid=376872](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Edge_E430&oldid=376872)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")