The [Lenovo Ideapad Z580](http://shop.lenovo.com/us/en/laptops/ideapad/z-series/z580/#tab-tech_specs) is a laptop computer with a 15.6" screen, 3rd Generation Intel Core i processor, numpad, DVD-RW drive, webcam, microphone, audio in/out, HDMI and VGA out, gigabit ethernet port, 80211n wireless card, bluetooth, 2 USB3 ports, 2 USB2 ports and an SD-card reader. The Z580 is well supported on recent Linux kernels and enjoys good driver support for nearly all of its components, although it does require some binary firmware.

## Contents

*   [1 PCI Devices](#PCI_Devices)
*   [2 USB Devices](#USB_Devices)
*   [3 Hardware Support](#Hardware_Support)
    *   [3.1 UEFI](#UEFI)
    *   [3.2 Video](#Video)
    *   [3.3 Sound](#Sound)
    *   [3.4 Webcam](#Webcam)
    *   [3.5 Ethernet](#Ethernet)
    *   [3.6 Wireless](#Wireless)
    *   [3.7 Touchpad](#Touchpad)
    *   [3.8 Hardware keys](#Hardware_keys)
    *   [3.9 ACPI annoyances](#ACPI_annoyances)

## PCI Devices

```
$ lspci
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C216 Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C216 Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C216 Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C216 Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.1 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 2 (rev c4)
00:1c.2 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 3 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C216 Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM76 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C216 Chipset Family SMBus Controller (rev 04)
02:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8101/2/6E PCI Express Fast/Gigabit Ethernet controller (rev 05)
03:00.0 Network controller: Intel Corporation Centrino Wireless-N 2200 (rev c4)

```

## USB Devices

```
$ lsusb
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 004: ID 0489:e042 Foxconn / Hon Hai Broadcom BCM20702 Bluetooth
Bus 001 Device 003: ID 0bda:0139 Realtek Semiconductor Corp. RTS5139 Card Reader Controller
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 002: ID 04f2:b2e1 Chicony Electronics Co., Ltd 
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Hardware Support

### UEFI

Before installing, disable [Secure Boot](/index.php/Secure_Boot "Secure Boot") in the BIOS. You can access the BIOS and boot menu by pressing the small "NOVO" button next to the power button while the laptop is powered off. While you are at it, you may want to set the "OS Optimized Defaults" to "Win8 64-bit" (see below).

### Video

Works natively with [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

HDMI and VGA out work.

### Sound

Works with no configuration.

### Webcam

Works with no configuration.

### Ethernet

Works out of the box.

### Wireless

The Intel wireless requires firmware in [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware).

**Note:** Lenovo whitelists its wireless cards, so you may be unable to swap this for another card unless it is on the whitelist.

### Touchpad

Works out of the box with [libinput](https://www.archlinux.org/packages/?name=libinput), including two finger scrolling.

### Hardware keys

Volume/mute function keys and media buttons work out of the box in [GNOME](/index.php/GNOME "GNOME").

Brightness function keys only work properly if Windows 8 defaults are loaded in the BIOS. Do this by setting "OS Optimized Defaults" to "Win8 64-bit" on the "Save & Exit" screen, and hitting enter on "Load Default Settings". Then check and adjust adjust other BIOS settings to your liking. If "Other OS" defaults are used, brightness adjustment occurs in very small increments and the brightness reporting in `/sys/class/backlight/acpi_video0/brightness` does not work properly. For example, it will report a minimum brightness when the backlight can still be decreased. This makes the brightness indicators shown in graphical environments fairly useless.

### ACPI annoyances

Currently while on battery power the system logs will be filled with:

```
kernel: ideapad_laptop: Unknown event: 1

```

This is produced by an unhandled ACPI event in the `ideapad_laptop` kernel module. See this [kernel bug #107481](https://bugzilla.kernel.org/show_bug.cgi?id=107481).