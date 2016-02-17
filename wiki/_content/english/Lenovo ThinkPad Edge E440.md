| **Device** | **Status** | **Modules** |
| Graphics | Working | xf86-video-intel |
| Ethernet | Working | r8169 |
| Wireless | Working | iwlwifi or ath9k |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | xf86-input-synaptics |
| Camera | Working | linux-uvc |
| Card Reader | Working |
| Bluetooth | Not tested |
| Fingerprint scanner | Not working |

For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Tested Configurations](#Tested_Configurations)
*   [2 Configuration](#Configuration)
    *   [2.1 ClickPad](#ClickPad)
    *   [2.2 Keyboard](#Keyboard)
    *   [2.3 Backlight](#Backlight)
    *   [2.4 Audio](#Audio)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Freezing on resume](#Freezing_on_resume)
    *   [3.2 With Fn and Ctrl_L keys swapped, Ctrl_L+s hotkey is mapped into Alt_L](#With_Fn_and_Ctrl_L_keys_swapped.2C_Ctrl_L.2Bs_hotkey_is_mapped_into_Alt_L)
    *   [3.3 Blinking power LED after resume from suspend](#Blinking_power_LED_after_resume_from_suspend)
*   [4 BIOS Update](#BIOS_Update)
*   [5 lspci](#lspci)

## Hardware

### Tested Configurations

Lenovo ThinkPad E440 comes with a wide range of available configurations.

**Tip:** Below are the tested configurations at the time.

| Feature | Configuration |
| System | E440 20C5005LRT |
| CPU | Intel(R) Pentium(R) CPU 3550M @ 2.30GHz |
| Graphics | Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06) |
| RAM | 4GB |
| Disk | 500GB |
| Display | 14" TFT |
| Wi-Fi | Intel Corporation Wireless 7260 (rev 73) |
| Backlight Keyboard | No |
| Fingerprint Scanner | Yes |
| Bluetooth | Yes |
| Cam | Yes |

## Configuration

### ClickPad

Works out of the box.

The only tweak you may want is to resize active area. With default config, you can cosily use as pointer only top 1/3 of ClickPad. See [Touchpad Synaptics#Buttonless touchpads (aka ClickPads)](/index.php/Touchpad_Synaptics#Buttonless_touchpads_.28aka_ClickPads.29 "Touchpad Synaptics") for instructions.

### Keyboard

**Fn and Ctrl keys** can be swapped in BIOS.

**Fn key** lock can be switched with **Fn + Esc**.

### Backlight

Backlight control in GNOME with multimedia keys (**Fn + F[5/6]**) works out of the box. To configure brightness level on startup see [Backlight#Udev rule](/index.php/Backlight#Udev_rule "Backlight").

### Audio

Out of box configuration could point to non-existent device because numbering of HDMI devices does not start with 0\. Suggested solution is to set PCH device to default by placing a configuration file into /etc/modprobe.d. The following thread contains alternative solutions and detailed instructions: [Fixing ALSA device selection](https://bbs.archlinux.org/viewtopic.php?pid=1446773#p1446773).

## Troubleshooting

### Freezing on resume

When system is being suspended, it could freeze on wake up. Most likely, this bug occurs with BIOS v2.16.

Simple solution is to disable USB 3.0 in BIOS. Better solution is to update BIOS to v2.18\. Instructions on update can be found below.

Even with new BIOS version (2.18), hibernation still does not fully work. Use the LTS kernel to fix issues.

### With Fn and Ctrl_L keys swapped, Ctrl_L+s hotkey is mapped into Alt_L

[Lenovo Forums topic](http://forums.lenovo.com/t5/ThinkPad-Edge-S-series/ThinkPad-E440-Ctrl-L-S-maps-as-Alt-L/td-p/1772489)

Issue can be meet on notebook with BIOS older than v2.16. Problem can be solved with BIOS update up to v2.16 or newer. [BIOS v2.16 update changelog](http://download.lenovo.com/ibmdl/pub/pc/pccbbs/mobiles/j9uj16ww.txt).

### Blinking power LED after resume from suspend

This is not a real problem, but can be annoying and has a very simple solution:

```
# echo "0 on" > /proc/acpi/ibm/led

```

For automation, create a script depending on the used [power management](/index.php/Power_management "Power management") tool.

## BIOS Update

Steps below were tested by contributors of this page and work perfectly. **Always, do it at your own risk!**

To update the BIOS from a USB drive, follow these steps (alternatively, you can download the iso, burn it to a CD, and then boot from the CD):

1.  Download the latest firmware from the official [E440 Downloads](http://support.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-edge-laptops/thinkpad-edge-e440?TabName=Downloads) page.
2.  Install the [geteltorito](https://aur.archlinux.org/packages/geteltorito/) utility.
3.  Convert ISO image (change 'XX' to match the filename of downloaded .iso): `geteltorito.pl -o bios.img j9ujXXwd.iso` 
4.  Write the image to the USB drive. Suppose, your drive is `/dev/sdb`. **Warning:** all information on USB stick will be lost!
    1.  Unmount the drive: `sudo umount /dev/sdb` 
    2.  Write image: `sudo dd if=bios.img of=/dev/sdb bs=1M` 
5.  Reboot you PC and boot from your USB drive.
6.  **FOLLOW ALL INSTRUCTIONS** written in the update utility!

## lspci

**Note:** Model: E440 20C500FBRT

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06)
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 04)
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #1 (rev d4)
00:1c.2 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #3 (rev d4)
00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d4)
00:1c.4 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #5 (rev d4)
00:1f.0 ISA bridge: Intel Corporation HM87 Express LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 04)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)
04:00.0 Network controller: Intel Corporation Wireless 7260 (rev 73)

```

**Note:** Model: E440 20C5004YUS

```
00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor DRAM Controller (rev 06)
00:02.0 VGA compatible controller: Intel Corporation 4th Gen Core Processor Integrated Graphics Controller (rev 06)
00:03.0 Audio device: Intel Corporation Xeon E3-1200 v3/4th Gen Core Processor HD Audio Controller (rev 06)
00:14.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB xHCI (rev 04)
00:16.0 Communication controller: Intel Corporation 8 Series/C220 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 8 Series/C220 Series Chipset High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #1 (rev d4)
00:1c.2 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #3 (rev d4)
00:1c.3 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #4 (rev d4)
00:1c.4 PCI bridge: Intel Corporation 8 Series/C220 Series Chipset Family PCI Express Root Port #5 (rev d4)
00:1d.0 USB controller: Intel Corporation 8 Series/C220 Series Chipset Family USB EHCI #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM87 Express LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 8 Series/C220 Series Chipset Family 6-port SATA Controller 1 [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 8 Series/C220 Series Chipset Family SMBus Controller (rev 04)
02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5227 PCI Express Card Reader (rev 01)
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 10)
04:00.0 Network controller: Intel Corporation Wireless 7260 (rev 73)

```