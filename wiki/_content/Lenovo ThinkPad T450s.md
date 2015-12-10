# Lenovo ThinkPad T450s

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Components](#Components)
    *   [1.2 Support](#Support)
*   [2 Configuration](#Configuration)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Sound](#Sound)
    *   [2.3 Fingerprint Reader](#Fingerprint_Reader)
    *   [2.4 Function Keys](#Function_Keys)
    *   [2.5 LEDs](#LEDs)
    *   [2.6 Intel Rapid Start Technology (IRST)](#Intel_Rapid_Start_Technology_.28IRST.29)
*   [3 See also](#See_also)

## Model description

Lenovo ThinkPad T450s

### Components

<table class="wikitable">

<tbody>

<tr>

<td>**PCI (lspci)**</td>

<td>**Driver**</td>

</tr>

<tr>

<td>Intel Corporation Broadwell-U Host Bridge -OPI (rev 09)</td>

<td>bdw_uncore</td>

</tr>

<tr>

<td>Intel Corporation Broadwell-U Integrated Graphics (rev 09)</td>

<td>i915</td>

</tr>

<tr>

<td>Intel Corporation Broadwell-U Audio Controller (rev 09)</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP USB xHCI Controller (rev 03)</td>

<td>xhci_hcd; xhci_pci</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP MEI Controller #1 (rev 03)</td>

<td>mei_me</td>

</tr>

<tr>

<td>Intel Corporation Ethernet Connection (3) I218-LM (rev 03)</td>

<td>e1000e</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP High Definition Audio Controller (rev 03)</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP PCI Express Root Port (rev e3)</td>

<td>pcieport; shpchp</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP USB EHCI Controller (rev 03)</td>

<td>ehci-pci; ehci_pci</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP LPC Controller (rev 03)</td>

<td>lpc-ich; lpc_ich</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP SATA Controller [AHCI Mode] (rev 03)</td>

<td>ahci</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP SMBus Controller (rev 03)</td>

<td>i801_smbus; i2c_i801</td>

</tr>

<tr>

<td>Intel Corporation Wildcat Point-LP Thermal Management Controller (rev 03)</td>

</tr>

<tr>

<td>Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)</td>

<td>rtsx_pci</td>

</tr>

<tr>

<td>Intel Corporation Wireless 7265 (rev 59)</td>

<td>iwlwifi</td>

</tr>

</tbody>

</table>

<table class="wikitable">

<tbody>

<tr>

<td>**USB (usb-devices/lsusb)**</td>

<td>**Driver**</td>

</tr>

<tr>

<td>Intel Corporation USB root hub</td>

<td>hub</td>

</tr>

<tr>

<td>Validity Sensors Fingerprint Reader</td>

</tr>

<tr>

<td>Intel Corporation Bluetooth</td>

<td>btusb</td>

</tr>

<tr>

<td>Chicony Electronics Integrated Camera</td>

<td>uvcvideo</td>

</tr>

</tbody>

</table>

### Support

<table class="wikitable">

<tbody>

<tr>

<td>**Device**</td>

<td>**Working**</td>

</tr>

<tr>

<td>[Intel graphics](/index.php/Intel_graphics "Intel graphics")</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

</tr>

<tr>

<td>[Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration")</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Manual</td>

</tr>

<tr>

<td>[ALSA](/index.php/ALSA "ALSA")</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

</tr>

<tr>

<td>[Touchpad](/index.php/Touchpad "Touchpad")</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Manual</td>

</tr>

<tr>

<td>[Trackpad](/index.php?title=Trackpad&action=edit&redlink=1 "Trackpad (page does not exist)")</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

</tr>

<tr>

<td>[Camera](/index.php?title=Camera&action=edit&redlink=1 "Camera (page does not exist)")</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

</tr>

</tbody>

</table>

## Configuration

### Touchpad

You can install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) and see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for configuration.

In the alternative, install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput) and see [Libinput](/index.php/Libinput "Libinput") for configuration.

### Sound

See [ALSA#Set the default sound card](/index.php/ALSA#Set_the_default_sound_card "ALSA") to set the default sound card to Intel PCH (speakers and headphones).

 `/etc/modprobe.d/thinkpad-t450s.conf`  `options snd_hda_intel index=1,0` 

### Fingerprint Reader

I compiled libfprint-git from the AUR, although it is possible that the version from the repos might work. Then set up [Fprint](/index.php/Fprint "Fprint") or [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui").

### Function Keys

All "special" keys either function or map to Xorg special key classes out of the box. Mappings are below:

<table class="wikitable">

<tbody>

<tr>

<td>**Key**</td>

<td>**Console Keycode**</td>

<td>**XF86 Keysym**</td>

<td>**Windows 7 Function**</td>

<td>Needs script</td>

</tr>

<tr>

<td>F1</td>

<td>113</td>

<td>XF86AudioMute</td>

<td>Mute speakers</td>

<td>No</td>

</tr>

<tr>

<td>F2</td>

<td>114</td>

<td>XF86AudioLowerVolume</td>

<td>Decreases the speaker volume</td>

<td>No</td>

</tr>

<tr>

<td>F3</td>

<td>115</td>

<td>XF86AudioRaiseVolume</td>

<td>Increases the speaker volume</td>

<td>No</td>

</tr>

<tr>

<td>F4</td>

<td>190</td>

<td>XF86AudioMicMute</td>

<td>Mutes/unmutes microphone</td>

<td>No</td>

</tr>

<tr>

<td>F5</td>

<td>224</td>

<td>XF86MonBrightnessDown</td>

<td>Darkens display</td>

<td>No</td>

</tr>

<tr>

<td>F6</td>

<td>225</td>

<td>XF86MonBrightnessUp</td>

<td>Brightens display</td>

<td>No</td>

</tr>

<tr>

<td>F7</td>

<td>227</td>

<td>XF86Display</td>

<td>Switch between internal and external display</td>

<td>No</td>

</tr>

<tr>

<td>F8</td>

<td>238</td>

<td>XF86WLAN</td>

<td>Enable/disable wireless</td>

<td>Yes</td>

</tr>

<tr>

<td>F9</td>

<td>171</td>

<td>XF86Tools</td>

<td>Open "Control Panel"</td>

<td>No</td>

</tr>

<tr>

<td>F10</td>

<td>217</td>

<td>XF86Search</td>

<td>Open "Windows Search"</td>

<td>No</td>

</tr>

<tr>

<td>F11</td>

<td>120</td>

<td>XF86LaunchA</td>

<td>View open programs</td>

<td>No</td>

</tr>

<tr>

<td>F12</td>

<td>144</td>

<td>XF86Explorer</td>

<td>Open "Computer"</td>

<td>No</td>

</tr>

<tr>

<td>Fn+4</td>

<td>142</td>

<td>XF86Sleep</td>

<td>Enters sleep mode</td>

<td>Yes</td>

</tr>

<tr>

<td>Fn+p</td>

<td>119</td>

<td>Pause</td>

<td>Pause</td>

<td>Yes</td>

</tr>

<tr>

<td>Fn+s</td>

<td>56+99</td>

<td>Sys_Req</td>

<td>SysReq</td>

<td>Yes</td>

</tr>

<tr>

<td>Fn+K</td>

<td>70</td>

<td>Scroll_Lock</td>

<td>Scroll Lock</td>

<td>Yes</td>

</tr>

<tr>

<td>Fn+B</td>

<td>29+119</td>

<td>Break</td>

<td>Break</td>

<td>Yes</td>

</tr>

<tr>

<td>Fn+Spacebar</td>

<td>NONE</td>

<td>XF86Wakeup</td>

<td>Adjusts keyboard backlight</td>

<td>No</td>

</tr>

</tbody>

</table>

Note that there is a BIOS option to change the function keys so that F1 - F12 are the primary and the listed functions are only triggered by the "Fn" key.

### LEDs

There are six LEDs, all of which work out of the box. See the Lenovo manual for location and functionality of LEDs.

### Intel Rapid Start Technology (IRST)

The T450s has firmware support for IRST. This will only be available if the T450s has an SSD rather than a traditional spinning-disc drive.

[Per Matthew Garrett](https://mjg59.dreamwidth.org/26022.html),

"[t]he concept of IRST is pretty simple. There's a firmware mechanism for setting a sleep timeout. If you suspend your computer and this timeout expires, it'll resume. However, instead of handing control back to the OS, the firmware just copies the entire contents of RAM to a special partition and turns the computer off. Next time you hit the power button, the firmware dumps the partition contents back into RAM and resumes as if nothing had changed. This takes a few seconds longer than resume from S3 but is far faster than resume from hibernation since it starts the moment the system gets power."

More specifically:

"[t]he first thing to know about this feature is that it's entirely invisible unless your hard drive is set up correctly. There needs to be a partition that's at least the size of your system's physical RAM. For GPT systems, this needs to have a type GUID of D3BFE2DE-3DAF-11DF-BA-40-E3A556D89593\. For MBR systems, you need a partition type of 0x84\. If the firmware doesn't find an appropriate partition then the OS will get no indication that the firmware supports it."

If you are not wiping and repartitioning your disk entirely as you prepare your drive for Arch installation, merely retain the existing IRST partition. It should show up as an unformatted partition whose size is equal to that of the T450s's RAM.

If you are wiping and repartitioning your disk, then create an empty partition with a size equal to your T450s's RAM. Then set the flag for the partition to "irst" using [parted](/index.php/Parted "Parted") or [GParted](/index.php/GParted "GParted").

Now if you leave your T450s suspended to RAM for an extended period of time (3 hours is the default in BIOS) it will copy the contents of RAM to the IRST partition. When you restart the laptop, it will copy the contents of the partition to RAM and resume from where you left off.

## See also

*   [Lenovo T450s support page](http://support.lenovo.com/us/en/products/laptops%20and%20netbooks/thinkpad%20t%20series%20laptops/thinkpad%20t450s) (including downloadable technical manual)
*   [Installing Debian Jessie on Thinkpad 450s](https://wiki.debian.org/InstallingDebianOn/Thinkpad/T450s/jessie)
*   [Phoronix article Fedora on Thinkpad 450s](http://www.phoronix.com/scan.php?page=article&item=lenovo-t450s-linux&num=1)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T450s&oldid=410692](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T450s&oldid=410692)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")