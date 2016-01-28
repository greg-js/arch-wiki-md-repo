# Acer TimelineX

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** please use the first argument of the template to provide a brief explanation. (Discuss in [Talk:Acer TimelineX#](https://wiki.archlinux.org/index.php/Talk:Acer_TimelineX))

Hardware is a 4820TG/5820TG, but should be similar for all these laptops.

<table class="wikitable">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel</td>

<td style="color:green">**Working**</td>

<td>xf86-video-intel</td>

</tr>

<tr>

<td>Ati</td>

<td style="color:orange">**Partially Working**</td>

<td>xf86-video-ati</td>

</tr>

<tr>

<td>Ati</td>

<td style="color:green">**Working**</td>

<td>fglrx</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="color:green">**Working**</td>

<td>bluetooth</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="color:green">**Working**</td>

<td>atl1c (2.6.36)</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>ath9k / wl</td>

</tr>

<tr>

<td>Wireless</td>

<td style="color:green">**Working**</td>

<td>bcm4357 / wl</td>

</tr>

<tr>

<td>Audio</td>

<td style="color:green">**Working**</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Camera</td>

<td style="color:green">**Working**</td>

<td>uvcvideo</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="color:green">**Working**</td>

</tr>

<tr>

<td>Function Keys</td>

<td style="color:green">**Working**</td>

</tr>

</tbody>

</table>

## Contents

*   [1 ACPI](#ACPI)
*   [2 Hardware](#Hardware)
    *   [2.1 Bluetooth](#Bluetooth)
    *   [2.2 Wi-Fi](#Wi-Fi)
        *   [2.2.1 TimelineX 5820](#TimelineX_5820)
        *   [2.2.2 TimelineX 4820TG](#TimelineX_4820TG)
        *   [2.2.3 TimelineX 3820TG](#TimelineX_3820TG)
    *   [2.3 Camera](#Camera)
    *   [2.4 Card Reader](#Card_Reader)
    *   [2.5 Display brightness control](#Display_brightness_control)
*   [3 Info](#Info)
    *   [3.1 lspci](#lspci)
    *   [3.2 lspci - TimelineX 4820TG (with Broadcom 4357 wifi)](#lspci_-_TimelineX_4820TG_.28with_Broadcom_4357_wifi.29)
    *   [3.3 lspci - TimelineX 3820TG-5464G50iks](#lspci_-_TimelineX_3820TG-5464G50iks)
*   [4 Issues](#Issues)
*   [5 Links](#Links)

## ACPI

ACPI works with BIOS v1.18 and higher.

[BIOS v1.19 for 4820tg](http://global-download.acer.com/GDFiles/BIOS/BIOS/BIOS_Acer_1.19_A_A.zip?acerid=634217844152767304&Step1=Notebook&Step2=Aspire&Step3=Aspire%204820TG&OS=722&LC=en&BC=Acer&SC=PA_6)

[BIOS v1.19 for 3820tg](http://global-download.acer.com/GDFiles/BIOS/BIOS/BIOS_Acer_1.19_A_A.zip?acerid=634308246297660203&Step1=Notebook&Step2=Aspire&Step3=Aspire%203820TG&OS=722&LC=en&BC=Acer&SC=PA_6)

If you do not have Windows installed, you can flash with a [FreeDOS thumb drive](http://en.gentoo-wiki.com/wiki/FreeDOS_Flash_Drive).

## Hardware

### Bluetooth

Works out of the box. On some machines, Bluetooth cannot turn on because of `Fn`+`F3` switching only WLAN. [Fixed DSDT table](http://ubuntuforums.org/showpost.php?p=10021228&postcount=183) seems to solve the problem.

On the 3820TG, Bluetooth might not work even if `Fn`+`F3` is used to turn it on. (Symptoms include "usb disconnect" messages in dmesg, and the adapter not showing up in _hcitool dev_.) In this case, copying `/lib/firmware/ath3k-2.fw` to `/lib/firmware/ath3k-1.fw` helps, see [this mailing list thread](http://www.mail-archive.com/ubuntu-bugs@lists.ubuntu.com/msg2579867.html). If it does not work for you, please change this note!

For some models of 4820TG, Bluetooth can be turned on with acer_wmi driver. To check that the driver is installed:

```
lsmod | grep acer_wmi

```

To check bluetooth state (1 is on, 0 is off):

 `cat /sys/devices/platform/acer-wmi/rfkill/rfkill2/{name,state}` 

```
acer-bluetooth
0
```

To turn on bluetooth:

```
echo -n 1 > /sys/devices/platform/acer-wmi/rfkill/rfkill2/state

```

### Wi-Fi

Works out of the box and supports injection and AP mode.

#### TimelineX 5820

Wi-Fi driver needs to be installed. Open source [brcm80211](/index.php/Broadcom_wireless#brcmsmac.2Fbrcmfmac "Broadcom wireless") driver causes kernel panics; the proprietary [broadcom-wl](/index.php/Broadcom_wireless#broadcom-wl "Broadcom wireless") driver works fine.

#### TimelineX 4820TG

Wi-Fi driver does not work by default. You need to install [broadcom-wl](https://aur.archlinux.org/packages/broadcom-wl/)<sup><small>AUR</small></sup> and [b43-firmware](https://aur.archlinux.org/packages/b43-firmware/)<sup><small>AUR</small></sup>. See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless") for details.

#### TimelineX 3820TG

Works out of the box, `lspci` lists the chip as

```
05:00.0 Network controller: Atheros Communications Inc. AR9287 Wireless Network Adapter (rev 01)

```

### Camera

Works out of the box.

### Card Reader

Works out of the box, tested with a SD card.

### Display brightness control

Sometimes brightness control for integrated card does not work (at least with the 2.6.36.2-1 kernel). You may add `acpi_osi=Linux` to the kernel line in the [GRUB](/index.php/GRUB "GRUB") config to fix this.

## Info

### lspci

```
00:00.0 Host bridge: Intel Corporation Core Processor DRAM Controller (rev 12)
00:01.0 PCI bridge: Intel Corporation Core Processor PCI Express x16 Root Port (rev ff)
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 12)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:1a.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 05)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 05)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 05)
00:1c.5 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 6 (rev 05)
00:1d.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 05)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a5)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 4 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 05)
00:1f.6 Signal processing controller: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem (rev 05)
01:00.0 VGA compatible controller: ATI Technologies Inc Device 68e0 (rev ff)
01:00.1 Audio device: ATI Technologies Inc Device aa68 (rev ff)
02:00.0 Ethernet controller: Atheros Communications AR8151 v1.0 Gigabit Ethernet (rev c0)
03:00.0 Network controller: Atheros Communications Inc. AR928X Wireless Network Adapter (PCI-Express) (rev 01)
7f:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers (rev 02)
7f:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 02)
7f:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 02)
7f:02.1 Host bridge: Intel Corporation Core Processor QPI Physical 0 (rev 02)
7f:02.2 Host bridge: Intel Corporation Core Processor Reserved (rev 02)
7f:02.3 Host bridge: Intel Corporation Core Processor Reserved (rev 02)
```

### lspci - TimelineX 4820TG (with Broadcom 4357 wifi)

```
00:00.0 Host bridge: Intel Corporation Core Processor DRAM Controller (rev 12)
00:01.0 PCI bridge: Intel Corporation Core Processor PCI Express x16 Root Port (rev 12)
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 12)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:1a.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 05)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 05)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 05)
00:1c.5 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 6 (rev 05)
00:1d.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 05)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a5)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 4 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 05)
00:1f.6 Signal processing controller: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem (rev 05)
01:00.0 VGA compatible controller: ATI Technologies Inc Redwood [Radeon HD 5600 Series]
01:00.1 Audio device: ATI Technologies Inc Redwood HDMI Audio [Radeon HD 5600 Series]
02:00.0 Ethernet controller: Atheros Communications AR8151 v1.0 Gigabit Ethernet (rev c0)
03:00.0 Network controller: Broadcom Corporation Device 4357 (rev 01)
7f:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers (rev 02)
7f:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 02)
7f:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 02)
7f:02.1 Host bridge: Intel Corporation Core Processor QPI Physical 0 (rev 02)
7f:02.2 Host bridge: Intel Corporation Core Processor Reserved (rev 02)
7f:02.3 Host bridge: Intel Corporation Core Processor Reserved (rev 02)

```

### lspci - TimelineX 3820TG-5464G50iks

```
00:00.0 Host bridge: Intel Corporation Core Processor DRAM Controller (rev 18)
00:01.0 PCI bridge: Intel Corporation Core Processor PCI Express x16 Root Port (rev 18)
00:02.0 VGA compatible controller: Intel Corporation Core Processor Integrated Graphics Controller (rev 18)
00:16.0 Communication controller: Intel Corporation 5 Series/3400 Series Chipset HECI Controller (rev 06)
00:1a.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 05)
00:1b.0 Audio device: Intel Corporation 5 Series/3400 Series Chipset High Definition Audio (rev 05)
00:1c.0 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 1 (rev 05)
00:1c.1 PCI bridge: Intel Corporation 5 Series/3400 Series Chipset PCI Express Root Port 2 (rev 05)
00:1d.0 USB Controller: Intel Corporation 5 Series/3400 Series Chipset USB2 Enhanced Host Controller (rev 05)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev a5)
00:1f.0 ISA bridge: Intel Corporation Mobile 5 Series Chipset LPC Interface Controller (rev 05)
00:1f.2 SATA controller: Intel Corporation 5 Series/3400 Series Chipset 4 port SATA AHCI Controller (rev 05)
00:1f.3 SMBus: Intel Corporation 5 Series/3400 Series Chipset SMBus Controller (rev 05)
00:1f.6 Signal processing controller: Intel Corporation 5 Series/3400 Series Chipset Thermal Subsystem (rev 05)
02:00.0 VGA compatible controller: ATI Technologies Inc Redwood [Radeon HD 5600 Series] (rev ff)
02:00.1 Audio device: ATI Technologies Inc Redwood HDMI Audio [Radeon HD 5600 Series] (rev ff)
03:00.0 Ethernet controller: Atheros Communications AR8151 v1.0 Gigabit Ethernet (rev c0)
05:00.0 Network controller: Atheros Communications Inc. AR9285 Wireless Network Adapter (PCI-Express) (rev 01)
ff:00.0 Host bridge: Intel Corporation Core Processor QuickPath Architecture Generic Non-core Registers (rev 05)
ff:00.1 Host bridge: Intel Corporation Core Processor QuickPath Architecture System Address Decoder (rev 05)
ff:02.0 Host bridge: Intel Corporation Core Processor QPI Link 0 (rev 05)
ff:02.1 Host bridge: Intel Corporation Core Processor QPI Physical 0 (rev 05)
ff:02.2 Host bridge: Intel Corporation Core Processor Reserved (rev 05)
ff:02.3 Host bridge: Intel Corporation Core Processor Reserved (rev 05)

```

## Issues

ATI chip has no 3D acceleration.

Ethernet chip driver is buggy in the 2.6.35 kernel.

## Links

1.  [Ubuntu-it thread](http://forum.ubuntu-it.org/index.php/topic,382092.0.html)
2.  [Usind acpi_call module to switch on/off](http://linux-hybrid-graphics.blogspot.com/2010/07/using-acpicall-module-to-switch-onoff.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_TimelineX&oldid=393348](https://wiki.archlinux.org/index.php?title=Acer_TimelineX&oldid=393348)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")

Hidden category:

*   [Pages or sections flagged with Template:Out of date](/index.php/Category:Pages_or_sections_flagged_with_Template:Out_of_date "Category:Pages or sections flagged with Template:Out of date")