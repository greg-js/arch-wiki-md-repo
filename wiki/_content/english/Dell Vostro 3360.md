## Contents

*   [1 Specifications](#Specifications)
*   [2 Hardware](#Hardware)
    *   [2.1 Wi-Fi](#Wi-Fi)
    *   [2.2 Ethernet](#Ethernet)
    *   [2.3 Touchpad](#Touchpad)
    *   [2.4 Webcam](#Webcam)
    *   [2.5 Card reader](#Card_reader)
    *   [2.6 Video](#Video)
    *   [2.7 Sound](#Sound)
    *   [2.8 Multimedia keys](#Multimedia_keys)
    *   [2.9 Fingerprint Reader](#Fingerprint_Reader)
*   [3 Actions](#Actions)
    *   [3.1 Brightness adjustment](#Brightness_adjustment)
    *   [3.2 Hibernation](#Hibernation)
    *   [3.3 Suspend to RAM](#Suspend_to_RAM)

## Specifications

On manufacturer site: [[1]](http://www.dell.com/en/business/p/vostro-3360/pd)

lspci output:

```
00:00.0 Host bridge: Intel Corporation 3rd Gen Core processor DRAM Controller (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 3rd Gen Core processor Graphics Controller (rev 09)
00:14.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB xHCI Host Controller (rev 04)
00:16.0 Communication controller: Intel Corporation 7 Series/C210 Series Chipset Family MEI Controller #1 (rev 04)
00:1a.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #2 (rev 04)
00:1b.0 Audio device: Intel Corporation 7 Series/C210 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 1 (rev c4)
00:1c.4 PCI bridge: Intel Corporation 7 Series/C210 Series Chipset Family PCI Express Root Port 5 (rev c4)
00:1d.0 USB controller: Intel Corporation 7 Series/C210 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM77 Express Chipset LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 7 Series Chipset Family 6-port SATA Controller [AHCI mode] (rev 04)
00:1f.3 SMBus: Intel Corporation 7 Series/C210 Series Chipset Family SMBus Controller (rev 04)
01:00.0 Network controller: Atheros Communications Inc. AR9485 Wireless Network Adapter (rev 01)
02:00.0 Ethernet controller: Atheros Communications Inc. AR8161 Gigabit Ethernet (rev 10)

```

lsusb output:

```
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 138a:0011 Validity Sensors, Inc. VFS5011 Fingerprint Reader
Bus 001 Device 004: ID 0bda:0129 Realtek Semiconductor Corp. 
Bus 001 Device 005: ID 0c45:648b Microdia 
Bus 002 Device 004: ID 0cf3:e004 Atheros Communications, Inc.

```

## Hardware

### Wi-Fi

Works out-of-the-box.

### Ethernet

Works out-of-the-box.

### Touchpad

Touchpad works out-of-the-box.

To turn the touchpad LED on:

```
echo 255 >/sys/class/leds/dell-laptop::touchpad/brightness

```

and off:

```
echo 0 >/sys/class/leds/dell-laptop::touchpad/brightness

```

### Webcam

Works out-of-the-box. You don't need GSPCA for that.

### Card reader

Works out-of-the-box.

### Video

Intel HD4000 works out-of-the-box.

### Sound

Works out-of-the-box. Cirrus HDA codec is in use.

### Multimedia keys

Fn keys work out of the box. Three extra keys on the top right side are not working and require either dell-wmi driver patching (work in progress [[2]](http://lkml.iu.edu/hypermail/linux/kernel/1711.2/02894.html)) or DSDT mangling.

### Fingerprint Reader

libfprintd has upstreamed VFS5011 protocol, so it works out of the box.

## Actions

### Brightness adjustment

Works out of the box. Both KDE 5 slider and Fn keys work okay.

### Hibernation

Works out of the box if you follow [Power management/Suspend and hibernate#Hibernation](/index.php/Power_management/Suspend_and_hibernate#Hibernation "Power management/Suspend and hibernate") guide.

### Suspend to RAM

Works out-of-the-box.