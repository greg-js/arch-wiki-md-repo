This article covers the Arch Linux support for the Lenovo Yoga 2 11 Laptop.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Booting the Install USB](#Booting_the_Install_USB)
    *   [1.2 Network Connection](#Network_Connection)
*   [2 Hardware](#Hardware)
    *   [2.1 lspci](#lspci)
    *   [2.2 lsusb](#lsusb)
*   [3 Configuration](#Configuration)
    *   [3.1 TrackPad](#TrackPad)
    *   [3.2 TouchScreen](#TouchScreen)
    *   [3.3 Video](#Video)
        *   [3.3.1 Colour Calibration](#Colour_Calibration)
    *   [3.4 Wireless](#Wireless)
    *   [3.5 Sound](#Sound)
    *   [3.6 Webcam](#Webcam)
    *   [3.7 Power](#Power)
        *   [3.7.1 Power Down](#Power_Down)
        *   [3.7.2 Suspend](#Suspend)
    *   [3.8 ACPI](#ACPI)
    *   [3.9 Laptop Mode Tools](#Laptop_Mode_Tools)
    *   [3.10 CPU Frequency Scaling](#CPU_Frequency_Scaling)
    *   [3.11 KVM](#KVM)
*   [4 Issues](#Issues)
    *   [4.1 Tablet Mode](#Tablet_Mode)

## Installation

Installation was performed with the Arch Linux ISO 2014.08.01, with kernel 3.15.7.

### Booting the Install USB

To access the boot menu and BIOS, use the "alternative" power button: a small circular one on the right, next to the main power button.

Disable secure boot from the BIOS. Only the UEFI boot mode appears to be available, but the Arch Linux install ISO used supports UEFI boot.

### Network Connection

To enable the wifi card, first run

```
rfkill unblock all

```

The command

```
wifi-menu wlp1s0

```

returned no scanning results, however

```
iwlist wlp1s0 scan

```

confirmed the wifi card was working. I was able to get a connection by setting up a [netctl](/index.php/Netctl "Netctl") profile manually.

## Hardware

Tested model 20332 on **Kernel 3.16.1** (stable).

| Device | Working? (Yes/No) |
| Video | Yes (xf86-video-intel and intel-dri for 3D) |
| Ethernet | N/A |
| Wireless | Yes (module: ath9k) |
| Bluetooth | Yes (module: bluetooth) |
| Audio | Yes (module: snd_hda_intel) |
| Web Camera | Yes (tested with Skype) |
| Card Reader | Not Tested |

### lspci

```
00:00.0 Host bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register (rev 0c)
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0c)
00:13.0 SATA controller: Intel Corporation Device 0f23 (rev 0c)
00:14.0 USB controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB xHCI (rev 0c)
00:1a.0 Encryption controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine (rev 0c)
00:1b.0 Audio device: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller (rev 0c)
00:1c.0 PCI bridge: Intel Corporation Device 0f48 (rev 0c)
00:1f.0 ISA bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit (rev 0c)
00:1f.3 SMBus: Intel Corporation Device 0f12 (rev 0c)
01:00.0 Network controller: Qualcomm Atheros QCA9565 / AR9565 Wireless Network Adapter (rev 01)

```

### lsusb

```
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 048d:8386 Integrated Technology Express, Inc. 
Bus 001 Device 003: ID 03eb:8c1d Atmel Corp. 
Bus 001 Device 009: ID 0cf3:3004 Atheros Communications, Inc. AR3012 Bluetooth 4.0
Bus 001 Device 005: ID 1bcf:2c66 Sunplus Innovation Technology Inc. 
Bus 001 Device 002: ID 05e3:0608 Genesys Logic, Inc. Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Configuration

### TrackPad

TrackPad works fine with [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

### TouchScreen

Touchscreen works out of the box with evdev. The wacom driver (package: [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom)) may also be used, and provides two-finger right-click, scroll, and pinch to zoom.

The packages [easystroke](https://www.archlinux.org/packages/?name=easystroke) or [touchegg](/index.php/Touchegg "Touchegg") can also be used with X11 to provide further input gestures.

### Video

See [Intel graphics](/index.php/Intel_graphics "Intel graphics"), [xrandr](/index.php/Xrandr "Xrandr") and [Backlight](/index.php/Backlight "Backlight").

#### Colour Calibration

Colours in [xorg](/index.php/Xorg "Xorg") were on the dark side out of the box. Using a program such as [monica](https://www.archlinux.org/packages/?name=monica) to configure the best colour settings is recommended.

### Wireless

Works out of the box.

### Sound

Works out of the box.

### Webcam

Works out of the box. Tested using Skype.

### Power

#### Power Down

The power button works out of the box, however the system reboots after shutdown. This appears to be an [xhci-hcd kernel module bug](https://bugzilla.kernel.org/show_bug.cgi?id=66171) and can be worked around by unloading the xhci_hcd module before shutdown. This can be done via [systemd](/index.php/Systemd "Systemd") by creating a unit file /etc/systemd/system/xhci.service containing

```
[Unit]
Description=rmmod xhci_hcd

[Service]
Type=oneshot
ExecStart=/bin/true
ExecStop=/usr/bin/rmmod xhci_hcd
RemainAfterExit=yes

[Install]
WantedBy=default.target

```

and enabling it with

```
systemctl enable xhci

```

To use the unit immediately, you will also have to start it

```
systemctl start xhci

```

#### Suspend

Suspend has been tested with

```
systemctl suspend

```

Initially, waking the machine resulted in the wifi card being soft-blocked and had to be repaired by installing [rfkill](https://www.archlinux.org/packages/?name=rfkill) and running

```
rfkill unblock 0

```

The problem has not recurred since installing rfkill.

### ACPI

[acpid](/index.php/Acpid "Acpid") appears to work.

### Laptop Mode Tools

[Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") provides power saving features. I found it didn't work too well out of the box, and ran into the following issues. In the end I switched it for [TLP](/index.php/TLP "TLP"). The laptop mode tools problems are listed below.

The use of HAL ends up disabling the touchscreen. HAL can be disabled by editing /etc/laptop-mode/conf.d/hal-polling.conf and changing CONTROL_HAL_POLLING to 0.

The [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") did not work: the frequency governer remained on "powersave" at all times.

The wireless power saving setting resulted in an "Operation not supported" error at boot. It can be disabled by editing /etc/laptop-mode/conf.d/wireless-power.conf and setting CONTROL_WIRELESS_POWER_SAVING to 0.

### CPU Frequency Scaling

By default the CPUs use the intel_pstate driver and provide the following governors: powersave, performance. Packages such as [Laptop Mode Tools](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") and [TLP](/index.php/TLP "TLP") assumed "ondemand" as the default powersaving option, hence must be configured to use powersave instead.

### KVM

KVM can be enabled in the BIOS via the "Intel Virtual Technology" option.

## Issues

### Tablet Mode

The laptop folds fully into a tablet. Out of the box, the keyboard is automatically disabled in this mode, but the touchpad remains active.

There is also a Windows button by the screen, however key down events are only reported when the button is released (in tandem with the key release event).