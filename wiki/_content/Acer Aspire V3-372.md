# Acer Aspire V3-372

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table class="wikitable" style="float: right;">

<tbody>

<tr>

<td>**Device**</td>

<td>**Status**</td>

<td>**Modules**</td>

</tr>

<tr>

<td>Intel</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>i915</td>

</tr>

<tr>

<td>Ethernet</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>r8168</td>

</tr>

<tr>

<td>Wireless</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">not working</td>

<td>ath10k_pci</td>

</tr>

<tr>

<td>Audio</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>snd_hda_intel</td>

</tr>

<tr>

<td>Touchpad</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

<td>see below</td>

</tr>

<tr>

<td>Camera</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Untested</td>

<td>uvcvideo</td>

</tr>

<tr>

<td>Card Reader</td>

<td style="background: #ffa; color: inherit; vertical-align: middle; text-align: center;">Untested</td>

<td>rtsx_usb</td>

</tr>

<tr>

<td>Bluetooth</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Working</td>

</tr>

</tbody>

</table>

Information for the Acer Aspire V3-372 51EK (Core i5-6200U, 4GiB RAM, 128GB SSD). Because the device is rather new many drivers still need to be developed for it (_05\. November 2015_).

## Contents

*   [1 Devices](#Devices)
*   [2 Configuration](#Configuration)
    *   [2.1 Booting Arch Linux from USB](#Booting_Arch_Linux_from_USB)
    *   [2.2 Video](#Video)
    *   [2.3 Solid State Drive](#Solid_State_Drive)
    *   [2.4 Touchpad](#Touchpad)
    *   [2.5 Wireless](#Wireless)

## Devices

 `# lspci` 

```
00:00.0 Host bridge: Intel Corporation Sky Lake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation Sky Lake Integrated Graphics (rev 07)
00:14.0 USB controller: Intel Corporation Device 9d2f (rev 21)
00:14.2 Signal processing controller: Intel Corporation Device 9d31 (rev 21)
00:15.0 Signal processing controller: Intel Corporation Device 9d60 (rev 21)
00:15.1 Signal processing controller: Intel Corporation Device 9d61 (rev 21)
00:16.0 Communication controller: Intel Corporation Device 9d3a (rev 21)
00:17.0 SATA controller: Intel Corporation Device 9d03 (rev 21)
00:1c.0 PCI bridge: Intel Corporation Device 9d10 (rev f1)
00:1c.4 PCI bridge: Intel Corporation Device 9d14 (rev f1)
00:1c.5 PCI bridge: Intel Corporation Device 9d15 (rev f1)
00:1f.0 ISA bridge: Intel Corporation Device 9d48 (rev 21)
00:1f.2 Memory controller: Intel Corporation Device 9d21 (rev 21)
00:1f.3 Audio device: Intel Corporation Device 9d70 (rev 21)
00:1f.4 SMBus: Intel Corporation Device 9d23 (rev 21)
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 15)
03:00.0 Network controller: Qualcomm Atheros QCA6174 802.11ac Wireless Network Adapter (rev 32)

```

## Configuration

### Booting Arch Linux from USB

To disable Secure Boot, set the [supervisor password](https://acer.custhelp.com/app/answers/detail/a_id/29349/) in the BIOS settings. Then you should be able to boot Arch.

If you set up your installation media (USB drive) via [Rufus](/index.php/USB_flash_installation_media#Using_Rufus "USB flash installation media") i had the most success by using _GPT_ as partition table (in UEFI mode).

### Video

Install the xf86-video-intel package as shown [here](https://wiki.archlinux.org/index.php/Intel_graphics#Installation)

### Solid State Drive

For tips visit [SSD](/index.php/SSD "SSD").

### Touchpad

Set the touchpad to basic in the BIOS to get it working. Then enable it by pressing _FN + F7_.

### Wireless

The driver _ath10k_pci_ needs to be installed manually. Firmware is available on Github by [Kvalo](https://github.com/kvalo/ath10k-firmware) and [Sumdog](https://github.com/sumdog/ath10k-firmware).

By enabling [testing] and updating the linux-firmware package the device is visible:

 `# ip link` 

```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP mode DEFAULT group default qlen 1000
    link/ether 30:65:ec:87:7f:4e brd ff:ff:ff:ff:ff:ff
3: wlp3s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether b8:86:87:fd:61:23 brd ff:ff:ff:ff:ff:ff

```

Enabling it doesn't work though and gives the following output

 `# ip link set wlp3s0 up` 

```
RTNETLINK answers: Resource temporarily unavailable

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_V3-372&oldid=408427](https://wiki.archlinux.org/index.php?title=Acer_Aspire_V3-372&oldid=408427)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")