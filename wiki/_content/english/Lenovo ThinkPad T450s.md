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

| **PCI (lspci)** | **Driver** |
| Intel Corporation Broadwell-U Host Bridge -OPI (rev 09) | bdw_uncore |
| Intel Corporation Broadwell-U Integrated Graphics (rev 09) | i915 |
| Intel Corporation Broadwell-U Audio Controller (rev 09) | snd_hda_intel |
| Intel Corporation Wildcat Point-LP USB xHCI Controller (rev 03) | xhci_hcd; xhci_pci |
| Intel Corporation Wildcat Point-LP MEI Controller #1 (rev 03) | mei_me |
| Intel Corporation Ethernet Connection (3) I218-LM (rev 03) | e1000e |
| Intel Corporation Wildcat Point-LP High Definition Audio Controller (rev 03) | snd_hda_intel |
| Intel Corporation Wildcat Point-LP PCI Express Root Port (rev e3) | pcieport; shpchp |
| Intel Corporation Wildcat Point-LP USB EHCI Controller (rev 03) | ehci-pci; ehci_pci |
| Intel Corporation Wildcat Point-LP LPC Controller (rev 03) | lpc-ich; lpc_ich |
| Intel Corporation Wildcat Point-LP SATA Controller [AHCI Mode] (rev 03) | ahci |
| Intel Corporation Wildcat Point-LP SMBus Controller (rev 03) | i801_smbus; i2c_i801 |
| Intel Corporation Wildcat Point-LP Thermal Management Controller (rev 03) |
| Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01) | rtsx_pci |
| Intel Corporation Wireless 7265 (rev 59) | iwlwifi |

| **USB (usb-devices/lsusb)** | **Driver** |
| Intel Corporation USB root hub | hub |
| Validity Sensors Fingerprint Reader |
| Intel Corporation Bluetooth | btusb |
| Chicony Electronics Integrated Camera | uvcvideo |

### Support

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") | Manual |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Manual |
| Trackpad | Yes |
| [Webcam](/index.php/Webcam "Webcam") | Yes |

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

| **Key** | **Console Keycode** | **XF86 Keysym** | **Windows 7 Function** | Needs script |
| F1 | 113 | XF86AudioMute | Mute speakers | No |
| F2 | 114 | XF86AudioLowerVolume | Decreases the speaker volume | No |
| F3 | 115 | XF86AudioRaiseVolume | Increases the speaker volume | No |
| F4 | 190 | XF86AudioMicMute | Mutes/unmutes microphone | No |
| F5 | 224 | XF86MonBrightnessDown | Darkens display | No |
| F6 | 225 | XF86MonBrightnessUp | Brightens display | No |
| F7 | 227 | XF86Display | Switch between internal and external display | No |
| F8 | 238 | XF86WLAN | Enable/disable wireless | Yes |
| F9 | 171 | XF86Tools | Open "Control Panel" | No |
| F10 | 217 | XF86Search | Open "Windows Search" | No |
| F11 | 120 | XF86LaunchA | View open programs | No |
| F12 | 144 | XF86Explorer | Open "Computer" | No |
| Fn+4 | 142 | XF86Sleep | Enters sleep mode | Yes |
| Fn+p | 119 | Pause | Pause | Yes |
| Fn+s | 56+99 | Sys_Req | SysReq | Yes |
| Fn+K | 70 | Scroll_Lock | Scroll Lock | Yes |
| Fn+B | 29+119 | Break | Break | Yes |
| Fn+Spacebar | NONE | XF86Wakeup | Adjusts keyboard backlight | No |

Note that there is a BIOS option to change the function keys so that F1 - F12 are the primary and the listed functions are only triggered by the "Fn" key.

### LEDs

There are six LEDs. All work out of the box except for the mic mute LED. See the Lenovo manual for location and functionality of LEDs.

### Intel Rapid Start Technology (IRST)

The T450s has firmware support for IRST. This will only be available if the T450s has an SSD rather than a traditional spinning-disc drive. The 16GB M.2 cache SSD can also be used for the IRST partition.

[Per Matthew Garrett](https://mjg59.dreamwidth.org/26022.html),

	"[t]he concept of IRST is pretty simple. There's a firmware mechanism for setting a sleep timeout. If you suspend your computer and this timeout expires, it'll resume. However, instead of handing control back to the OS, the firmware just copies the entire contents of RAM to a special partition and turns the computer off. Next time you hit the power button, the firmware dumps the partition contents back into RAM and resumes as if nothing had changed. This takes a few seconds longer than resume from S3 but is far faster than resume from hibernation since it starts the moment the system gets power."

More specifically:

	"[t]he first thing to know about this feature is that it's entirely invisible unless your hard drive is set up correctly. There needs to be a partition that's at least the size of your system's physical RAM. For GPT systems, this needs to have a type GUID of D3BFE2DE-3DAF-11DF-BA-40-E3A556D89593\. For MBR systems, you need a partition type of 0x84\. If the firmware doesn't find an appropriate partition then the OS will get no indication that the firmware supports it."

If you are not wiping and repartitioning your disk entirely as you prepare your drive for Arch installation, merely retain the existing IRST partition. It should show up as an unformatted partition whose size is equal to that of the T450s's RAM.

If you are wiping and repartitioning your disk, then create an empty partition with a size equal to your T450s's RAM. Then set the flag for the partition to "irst" using [parted](/index.php/Parted "Parted") or [GParted](/index.php/GParted "GParted").

Now if you leave your T450s suspended to RAM for a certain period of time (3 hours is the default in BIOS) it will automatically wake back up after the configured period, copy the contents of RAM to the IRST partition, and turn itself off. When you power the laptop back up, instead of the regular boot process, it will copy the contents of the partition to RAM and resume from where you left off.

**Note:** Depending on the size of you RAM and the speed of your SSD, the IRST hibernation process can take 20-60 seconds. The process is completed when the power LED stops blinking.

## See also

*   [Lenovo T450s support page](http://support.lenovo.com/us/en/products/laptops%20and%20netbooks/thinkpad%20t%20series%20laptops/thinkpad%20t450s) (including downloadable technical manual)
*   [Installing Debian Jessie on Thinkpad 450s](https://wiki.debian.org/InstallingDebianOn/Thinkpad/T450s/jessie)
*   [Phoronix article Fedora on Thinkpad 450s](http://www.phoronix.com/scan.php?page=article&item=lenovo-t450s-linux&num=1)