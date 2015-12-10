# HP Envy TouchSmart 15j

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Specifications](#Specifications)
*   [2 Installation](#Installation)
*   [3 Booting](#Booting)
*   [4 Hardware](#Hardware)
    *   [4.1 Video](#Video)
        *   [4.1.1 Screen brightness](#Screen_brightness)
    *   [4.2 Touchscreen](#Touchscreen)
    *   [4.3 Networking](#Networking)
    *   [4.4 Wireless](#Wireless)
    *   [4.5 Bluetooth](#Bluetooth)
    *   [4.6 Sound](#Sound)
    *   [4.7 Fingerprint reader](#Fingerprint_reader)
    *   [4.8 SD card reader](#SD_card_reader)
    *   [4.9 Touch pad](#Touch_pad)
    *   [4.10 Webcam](#Webcam)
    *   [4.11 Power management](#Power_management)
*   [5 Issues](#Issues)
    *   [5.1 Gummiboot menu misaligned](#Gummiboot_menu_misaligned)
    *   [5.2 EFI stub booting (rEFIned, grummiboot) doesn't work](#EFI_stub_booting_.28rEFIned.2C_grummiboot.29_doesn.27t_work)
    *   [5.3 Dual-booting](#Dual-booting)

## Specifications

[Product homepage](http://h10025.www1.hp.com/ewfrf/wc/product?cc=us&dlc=en&lc=en&os=4158&product=5404664&sw_lang=)

I've created this page based on my HP ENVY TouchSmart 15-j004sa (model number E6B23EA) with the following specifications

<table class="wikitable">

<tbody>

<tr>

<td>Microprocessor</td>

<td>Intel Core i7-4700MQ (2.4 GHz, 6 MB cache, 4 cores)</td>

</tr>

<tr>

<td>Chipset</td>

<td>Intel HM87 Express</td>

</tr>

<tr>

<td>Memory</td>

<td>16 GB DDR3 SDRAM</td>

</tr>

<tr>

<td>Video Graphics</td>

<td>NVIDIA GeForce GT 740M (2 GB DDR3 dedicated)</td>

</tr>

<tr>

<td>Hard Drive</td>

<td>1 TB 5400 rpm SATA</td>

</tr>

<tr>

<td>Display</td>

<td>39.6 cm (15.6”) full HD BrightView LED-backlit Touchscreen (1920 x 1080)</td>

</tr>

<tr>

<td>Network Card</td>

<td>Integrated 10/100/1000 Gigabit Ethernet LAN (RJ-45 connector)</td>

</tr>

<tr>

<td>Wireless Connectivity</td>

<td>Intel 802.11b/g/n with Widi; Bluetooth</td>

</tr>

<tr>

<td>Sound</td>

<td>Beats Audio with 4 speakers and two HP Triple Bass Reflex Subwoofer</td>

</tr>

<tr>

<td>Pointing Device</td>

<td>HP Clickpad supporting multi-touch gestures</td>

</tr>

<tr>

<td>Camera</td>

<td>HP TrueVision HD Webcam with integrated dual array digital microphone</td>

</tr>

<tr>

<td>External Ports</td>

<td>Multi-format digital media card reader for SD cards

1 HDMI  
1 headphone-out/microphone-in combo  
4 USB 3.0 (1 Boost)  
1 RJ45

</td>

</tr>

</tbody>

</table>

## Installation

The laptop doesn't have a CD drive, use a USB key to load the installer.

2013.11 installer did not boot, 2013.09 booted and worked fine with `nomodeset=1`

If the screen turns off, check the brightness level, sometimes it turned all the way down for me and I thought the installer froze, but it was just the brightness.

## Booting

The UEFI implemantation in the laptop is buggy. It likes to overwrite the boot order and default's to Windows if there is a Windows install available. One might consider using legacy booting, which will use a little longer boot time but cause less headaches. Refer to [UEFI](/index.php/UEFI "UEFI").

The laptop has en ampty mSATA slot, where you can place an SSD. With the latest BIOS version the the UEFI firmware refused to boot from the SSD's EFI partition automatically, but it worked after choosing it from the boot menu. Placeing an EFI partition on the HDD is the easiest solution.

## Hardware

### Video

```
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
01:00.0 3D controller: NVIDIA Corporation GK208M [GeForce GT 740M] (rev ff)
```

The intel card cannot be disabled and it is the default card, the nvidia card cannot be used alone.

This is an [NVIDIA Optimus](/index.php/NVIDIA_Optimus "NVIDIA Optimus") machine. Use [Bumblebee](/index.php/Bumblebee "Bumblebee").

The HDMI output works.

#### Screen brightness

Screen brightness can be turned all the way down and off.

### Touchscreen

 `Bus 003 Device 005: ID 0eef:a103 D-WAV Scientific Co., Ltd` 

Touchscreen works out of the box.

### Networking

 `0f:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0c)` 

Works.

### Wireless

 `07:00.0 Network controller: Intel Corporation Centrino Wireless-N 2230 (rev c4)` 

Works great with the `iwlwifi` module. Wifi available from the installer.

The hardware switch (Fn-F12) does nothing however, but the device was enabled by default, don't think it will ever cause any problem.

### Bluetooth

Works.

Did not test this too much, I paired a device and it worked.

### Sound

 `00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)` 

The laptop contains several speakers. I think 2 front speakers and one on the back. With the default ALSA configuration only the 2 front speakers produce any sound. Their volume is low and a little distorted. Better sound can be achieved by rearranging the pins.

Install [alsa-tools](https://www.archlinux.org/packages/?name=alsa-tools), and use `hdajackretask` with the following configuration. Use `Show unconnected pins` to show all available options.

<table class="wikitable">

<tbody>

<tr>

<th>Pin ID</th>

<th>override</th>

</tr>

<tr>

<td>0x0d</td>

<td>Internal speaker</td>

</tr>

<tr>

<td>0x0f</td>

<td>Internal speaker</td>

</tr>

<tr>

<td>0x10</td>

<td>Internal speaker (LFE)</td>

</tr>

</tbody>

</table>

Orange mute LED works as expected.

The audio jack works fine, the speakers mute after inserting a headphone.

### Fingerprint reader

 `Bus 003 Device 006: ID 138a:0050 Validity Sensors, Inc.` 

The fingerprint reader does not work, but people are working on it ([blog entry](http://paydensutherland.com/2013/12/validity-sensors-fingerprint-reader-linux-driver-138a-0050-updates/)) and hopefully the work will be done and merged into libfprint soon.

### SD card reader

Works.

### Touch pad

Touchpad works. Multitouch works. It has physical buttons under the bottom left and right side.

The cursor movement is not fully smooth with the touchpad, but it is the same under Windows so this is a hardware issue.

### Webcam

Works.

### Power management

Sleep works. Power usage is on-par with Windows 8\. The laptop runs cool and quietly.

## Issues

### Gummiboot menu misaligned

The default text mode was not using the whole screen ([like this](http://i.imgur.com/yReSrd7.jpg)). Updating to the latest firmware fixed this.

### EFI stub booting (rEFIned, grummiboot) doesn't work

My Arch Linux installation sometimes did not start when I was using gummiboot. More about this bug [here](https://bugs.archlinux.org/task/33745) and [here](https://bbs.archlinux.org/viewtopic.php?id=168417).

The solution for me was to switch to grub2.

### Dual-booting

Dual-booting with Windows works, but the UEFI firmware sometimes decides to change the default boot loader to the Windows loader.

Soft-rebooting from Linux to Windows can cause issues, I experience that the audio jack stops working after a soft reboot. The solution is to power off the machine from Linux and start it again and boot Windows first.

Retrieved from "[https://wiki.archlinux.org/index.php?title=HP_Envy_TouchSmart_15j&oldid=384466](https://wiki.archlinux.org/index.php?title=HP_Envy_TouchSmart_15j&oldid=384466)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [HP](/index.php/Category:HP "Category:HP")