This articles details the installation and configuration of Arch Linux on the Dell Mini 10v. The Dell Mini 10v is a netbook with 10" display from Dell. This article covers the configuration of the graphics card, wireless card and touchpad.

## Contents

*   [1 Before you begin](#Before_you_begin)
*   [2 Xorg](#Xorg)
    *   [2.1 Touchpad](#Touchpad)
*   [3 Wireless](#Wireless)
*   [4 Power](#Power)
    *   [4.1 Battery status](#Battery_status)
    *   [4.2 Suspend to RAM](#Suspend_to_RAM)

## Before you begin

This article is intended to assist users with the specifics of installing Arch Linux on the Dell Mini 10v. It is assumed that a user is also following the [Installation guide](/index.php/Installation_guide "Installation guide").

Dell Mini 10v hardware may vary, however the following list of hardware has been assumed in this article:

	Audio

	Intel Corporation 82801G card

	Realtek ALC272 Chip (from alsamixer)

	Video

	Intel Corporation Mobile 945GME

	Wired NIC

	Realtek RTL8101E/RTL8102E

	Wireless NIC

	Broadcom Corporation BCM4312 802.11b/g

	Bluetooth

	Dell 365 Bluetooth 2.1+EDR

	Webcam

	Syntek Integrated Webcam

To list hardware, issue this command:

```
$ lspci && lsusb

```

The Dell Mini 10v does not have an optical drive. This means you will need to install Arch Linux through one of the alternative methods:

*   [USB stick](/index.php/Install_from_USB_stick "Install from USB stick") (recommended)
*   External USB CD-ROM drive.

To select the required boot media to install Arch Linux, press `F12` to open the Boot Menu when booting the Dell Mini 10v.

## Xorg

See [Xorg](/index.php/Xorg "Xorg") and [Intel graphics](/index.php/Intel_graphics "Intel graphics").

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for general information.

Manual configuration is needed as follows to ignore movements, scrolling and tapping on the bottom section of the touchpad, where the touchpad buttons are located. Add the 'JumpyCursorThreshold' and 'AreaBottomEdge' options to `/etc/X11/xorg.conf.d/10-synaptics.conf`:

 `/etc/X11/xorg.conf.d/10-synaptics.conf` 
```
Section "InputClass"
    Identifier "touchpad catchall"
    Driver "synaptics"
    MatchIsTouchpad "on"
        Option "TapButton1" "1"
        Option "TapButton2" "2"
        Option "TapButton3" "3"
        Option "JumpyCursorThreshold" "90"
        Option "AreaBottomEdge" "4100"
EndSection

```

Once X has been restarted, the bottom part of the touchpad will be disabled, allowing a user to click without unintentional movements of the mouse.

## Wireless

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless")

## Power

### Battery status

For utilities to monitor the battery status, see the [Laptop](/index.php/Laptop "Laptop") article.

### Suspend to RAM

See [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").