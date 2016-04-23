This is a guide of steps aggregated from other sources to installation of Arch on the Lenovo ThinkPad P70\. This guide was written for ARCH_201604\. The hardware from which this guide was created is as follows:

Intel Xeon E3-1505M v5 vPro

17.3" 4K IPS Display

32 GB ECC RAM

512 GB SSD PCIe-NVMe

512 GB SSD SATA

NVIDIA Quadro M3000M 4 GB

DVD Burner [read tested, write untested]

TrackPoint and Trackpad

720p Camera [untested]

Fingerprint Reader [Untested]

Pantone Color Calibration [Untested]

Intel 8260AC+BT 2x2 vPro [BT untested]

Shipping OS: Windows 10 Home

**Preliminaries**

1\. Create a recovery device in Windows 10\. It required a USB-only (no SD card, no optical media?) flash drive greater than 8 GB. Formatting FAT32 works.

2\. [Update the BIOS.](https://support.lenovo.com/us/en/documents/yast-3jwkjx) [As of this writing, the BIOS was 2.00 (2016-04-17).] You may be able to do this in Linux/OS-independently.

3\. Getting INTO the BIOS is pretty annoying, so [here are some instructions](https://support.lenovo.com/us/en/documents/sf13-t0025) that seemed to work. The easiest way was through Windows 10.

4\. In the BIOS, you'll want to disable UEFI Secure Boot, change the boot order to look at USB devices first, allow F12 to bypass the BIOS, and possibly enable the verbose mode because it's easier to press the appropriate buttons on time.

**Installation**

This section assumes that you've successfully created bootable Arch install media (hint: unetbootin) to a USB drive. The label of the USB installer must be correct (ARCH_201604 in this case). Restart the computer boot from the USB drive. You may need to press F12 at some point to trigger a boot order override.

You need an internet connection; this guide got both ethernet and wifi to work.

Ethernet: turn on DHCP with

```
# dhcpcd enp0s31f6

```

Wifi: wifi-menu worked here, the appropriate SSID was selected with the right password.

The font sizes will make you feel very far away. To deal with this, fonts are in /usr/share/kbd/consolefonts.

You can see the currently selected font with showconsolefont. The font was changed here to sun12x22 with: setfont sun12x22\. It's a little better.

Following the Beginner's Guide to install Arch.

Shutdown, remove the USB drive, and then boot the computer, and make sure the installed drive is first in the BIOS.

**Configuration**

**Keyboard**

**Sound**

**NVIDIA/Bumblebee**

**HiDPI**

**Xfce**

**Compiz/Emerald**