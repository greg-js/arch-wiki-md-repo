# Lenovo S20-30

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Touchpad](/index.php/Touchpad "Touchpad")
*   [Acpid](/index.php/Acpid "Acpid")
*   [Powertop](/index.php/Powertop "Powertop")

This is one of the products from the [Lenovo S-series](http://shop.lenovo.com/de/de/laptops/lenovo/s-series), which is different from the IdeaPad S-Series.

## Contents

*   [1 Hardware specifications](#Hardware_specifications)
    *   [1.1 PCI devices](#PCI_devices)
    *   [1.2 USB devices](#USB_devices)
*   [2 Configuration](#Configuration)
    *   [2.1 BIOS](#BIOS)
    *   [2.2 Wireless](#Wireless)
    *   [2.3 Bluetooth](#Bluetooth)
    *   [2.4 Graphics](#Graphics)
    *   [2.5 Backlight](#Backlight)
    *   [2.6 Audio](#Audio)
    *   [2.7 SD Card Reader](#SD_Card_Reader)
    *   [2.8 Webcam](#Webcam)
    *   [2.9 Changing fan mode](#Changing_fan_mode)

## Hardware specifications

*   CPU: [Intel Celeron N2830](http://en.wikipedia.org/wiki/Silvermont#Mobile_processors_.28Bay_Trail-M.29) (2x 2.16 GHz, turbo 2.41 GHz)
*   Memory: 4048 MB internal - can not be changed
*   WiFi: Broadcom BCM43142
*   Bluetooth: Broadcom BCM43142A0
*   Hard-Drive: 320GB (Seagate)
*   Optical Drive: None
*   Integrated Graphics: Intel HD Graphics i915 (4 EU, 313 MHz, turbo 750 MHz)
*   Sound: Intel HD Audio
*   Screen: 11,6" LCD (1366x768, anti-glare)
*   SD Card Reader: Realtek RST5129
*   Webcam: Lenovo (Acer) EasyCamera

 `inxi -F -M` 

```
System:    Host: XXX Kernel: 3.16.1-1-ARCH x86_64 (64 bit) Desktop: LXDE (Openbox 3.5.2) Distro: Arch Linux
Machine:   System: LENOVO product: 20421 v: Lenovo S20-30
           Mobo: LENOVO model: Edonis 2A1 v: SDK0F82993Pro Bios: LENOVO v: ACCN10WW date: 05/08/2014
CPU:       Dual core Intel Celeron N2830 (-MCP-) cache: 1024 KB 
           Clock Speeds: 1: 699 MHz 2: 699 MHz
Graphics:  Card: Intel Atom Processor Z36xxx/Z37xxx Series Graphics & Display
           Display Server: X.Org 1.16.0 driver: intel Resolution: 1366x768@60.02hz
           GLX Renderer: Mesa DRI Intel Bay Trail GLX Version: 3.0 Mesa 10.2.6
Audio:     Card Intel Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller driver: snd_hda_intel
           Sound: Advanced Linux Sound Architecture v: k3.16.1-1-ARCH
Network:   Card-1: Realtek RTL8101E/RTL8102E PCI Express Fast Ethernet controller driver: r8169
           IF: enp1s0 state: down mac: XX:XX:XX:XX:XX:XX
           Card-2: Broadcom BCM43142 802.11b/g/n driver: wl
           IF: wlp2s0 state: up mac: XX:XX:XX:XX:XX:XX
Drives:    XXX
Partition: XXX
Sensors:   System Temperatures: cpu: 34.0C mobo: N/A
           Fan Speeds (in rpm): cpu: N/A
Info:      Processes: 105 Uptime: 2:08 Memory: 852.2/3843.1MB Client: Shell (zsh) inxi: 2.2.3

```

### PCI devices

 `lspci -nn` 

```
00:00.0 Host bridge [0600]: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register [8086:0f00] (rev 0e)
00:02.0 VGA compatible controller [0300]: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display [8086:0f31] (rev 0e)
00:13.0 SATA controller [0106]: Intel Corporation Device [8086:0f23] (rev 0e)
00:14.0 USB controller [0c03]: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB xHCI [8086:0f35] (rev 0e)
00:1a.0 Encryption controller [1080]: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine [8086:0f18] (rev 0e)
00:1b.0 Audio device [0403]: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller [8086:0f04] (rev 0e)
00:1c.0 PCI bridge [0604]: Intel Corporation Device [8086:0f48] (rev 0e)
00:1c.1 PCI bridge [0604]: Intel Corporation Device [8086:0f4a] (rev 0e)
00:1f.0 ISA bridge [0601]: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit [8086:0f1c] (rev 0e)
00:1f.3 SMBus [0c05]: Intel Corporation Device [8086:0f12] (rev 0e)
01:00.0 Ethernet controller [0200]: Realtek Semiconductor Co., Ltd. RTL8101E/RTL8102E PCI Express Fast Ethernet controller [10ec:8136] (rev 08)
02:00.0 Network controller [0280]: Broadcom Corporation BCM43142 802.11b/g/n [14e4:4365] (rev 01)

```

### USB devices

 `lsusb` 

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 004: ID 105b:e065 Foxconn International, Inc. BCM43142A0 Bluetooth module
Bus 001 Device 003: ID 05e3:0610 Genesys Logic, Inc. 4-port hub
Bus 001 Device 002: ID 5986:054a Acer, Inc 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Configuration

### BIOS

The BIOS and the boot menu can be accessed by using the _alternative_ power button, which is a small circular one on the left side near by the main power button.

### Wireless

Works after installing the proprietary driver module [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> or [broadcom-wl-dkms](https://aur.archlinux.org/packages/broadcom-wl-dkms/)<sup><small>AUR</small></sup>, which supports Broadcom BCM43142\. See the detailed [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") page for further information.

### Bluetooth

The BCM43142A0 Bluetooth module should be recognized by the next kernel version right after 4.2.5\. More information can be found in the commit message at [kernel.org](https://git.kernel.org/cgit/linux/kernel/git/bluetooth/bluetooth.git/commit/drivers/bluetooth/btusb.c?id=2faf71ce90782d02e1710c12a19a2084fbbec5cc) and in the [Bluetooth](/index.php/Bluetooth#Foxconn_.2F_Hon_Hai_.2F_Lite-On_Broadcom_device "Bluetooth") article.

### Graphics

See [Intel graphics](/index.php/Intel_graphics "Intel graphics") and [xrandr](/index.php/Xrandr "Xrandr").

### Backlight

Backlight control works after adding the following [Kernel boot parameter](/index.php/Kernel_parameters "Kernel parameters"), which is set by default since [linux](https://www.archlinux.org/packages/?name=linux) kernel version 3.16:

```
video.use_native_backlight=1

```

Use one of the [backlight utilities](/index.php/Backlight#Backlight_utilities "Backlight") (tested with [light](https://aur.archlinux.org/packages/light/)<sup><small>AUR</small></sup>) to adjust the backlight and control it with keyboard shortcuts [by the method of your choice](/index.php/Extra_keyboard_keys_in_Xorg "Extra keyboard keys in Xorg").

With kernel 4.0.x backlight can still be changed, but the keys for increasing or decreasing backlight brightness do not work anymore.

### Audio

Install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils). See [ALSA](/index.php/ALSA "ALSA") and [Openbox#ALSA](/index.php/Openbox#ALSA "Openbox") for detailed information. To turn on the internal microphone, start `alsamixer` and increase the volume.

### SD Card Reader

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** Pending discussion at [User_talk:Thiagowfx#Arch Linux and Realtek RTS5129 SD card reader](/index.php/User_talk:Thiagowfx#Arch_Linux_and_Realtek_RTS5129_SD_card_reader "User talk:Thiagowfx") (Discuss in [Talk:Lenovo S20-30#](https://wiki.archlinux.org/index.php/Talk:Lenovo_S20-30))

This requires the `rtsx_usb` module [[1]](http://cateee.net/lkddb/web-lkddb/MFD_RTSX_USB.html). [Load the module](/index.php/Kernel_modules#Loading "Kernel modules") and [blacklist](/index.php/Kernel_modules#Blacklisting "Kernel modules") `sdhci`, `sdhci_acpi` and `sdhci_pci`, or install [lenovo-s20-30](https://aur.archlinux.org/packages/lenovo-s20-30/)<sup><small>AUR</small></sup> from the [AUR](/index.php/AUR "AUR"). Then [rebuild the kernel image](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") with `mkinitcpio -P linux` as root.

### Webcam

Works with [samsung-tools](https://aur.archlinux.org/packages/samsung-tools/)<sup><small>AUR</small></sup> and [cheese](https://www.archlinux.org/packages/?name=cheese). Turn the device on with

```
$ samsung-tools -w on

```

Since kernel 4.0.x everything works out of the box, i.e. samsung-tools is not needed anymore.

### Changing fan mode

The fan mode can be changed with `echo 'X'>/sys/bus/platform/drivers/ideapad_acpi/VPC2004:00/fan_mode` provided by the ideapad-laptop kernel module, where X defines the fan cooling mode, i.e X can be one of the following possibilities:

*   1 = interval cooling
*   2 = regulate fan speed depending on temperature (default, but shows 133 or 5 by inspecting with `cat`)

In fan cooling mode 2, the fan starts, if the CPU temperature reaches 35°C and stops after the temperature is lower than 31°C.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_S20-30&oldid=413854](https://wiki.archlinux.org/index.php?title=Lenovo_S20-30&oldid=413854)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")

Hidden category:

*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")