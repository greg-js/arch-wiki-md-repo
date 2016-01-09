# Lenovo ThinkPad Helix

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

<table class="wikitable"><caption>Hardware Information</caption>

<tbody>

<tr>

<th>Form Factor</th>

<td>Tablet/Ultrabook Convertible (detachable keyboard dock)</td>

</tr>

<tr>

<th>Display</th>

<td>11.6" 1920x1080 LCD with Capacitive and Pen Digitisers</td>

</tr>

<tr>

<th>CPU</th>

<td>3rd Generation (Ivy Bridge) Core i5-3427U or i7-3667U</td>

</tr>

<tr>

<th>RAM</th>

<td>4GiB (i5) or 8GiB (i7) DDR3L RAM (dependent upon CPU)</td>

</tr>

<tr>

<th>Storage</th>

<td>128/160/256GB mSATA SSD</td>

</tr>

<tr>

<th>WiFi</th>

<td>Intel Centrino Advanced-N 6205S mPCI WLAN</td>

</tr>

<tr>

<th>Bluetooth</th>

<td>Broadcom BCM20702 Bluetooth 4.0 (USB connected)</td>

</tr>

<tr>

<th>Camera</th>

<td>5MP Rear and 2MP Front (also USB)</td>

</tr>

</tbody>

</table>

## Contents

*   [1 Installation](#Installation)
*   [2 Hardware Configuration](#Hardware_Configuration)
    *   [2.1 Bluetooth](#Bluetooth)
    *   [2.2 Digitisers](#Digitisers)
    *   [2.3 Screen Rotation](#Screen_Rotation)
*   [3 BIOS/Firmware Updates](#BIOS.2FFirmware_Updates)

## Installation

**Note:** As this model includes no physical recovery media, it's highly recommended to create a Windows reinstallation flash drive just in case using the recovery media creation tool included with your preinstalled Windows system.

Due to the fact that there is no optical drive, you need to [install Arch from USB stick](/index.php/USB_Installation_Media "USB Installation Media").

The Arch install media will happily boot under UEFI, so it is recommended to disable legacy boot in the system setup utility. If legacy boot is needed for some reason, it does work fine as well.

Booting using [Systemd-boot](/index.php/Systemd-boot "Systemd-boot") works perfectly. Again, if legacy boot is needed, [GRUB](/index.php/GRUB "GRUB") is perfectly functional as well.

## Hardware Configuration

To fully support all hardware in X, one needs to ensure that the following driver packages are installed:

*   [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) (for the clickpad)
*   [xf86-input-wacom](https://www.archlinux.org/packages/?name=xf86-input-wacom) (for the digitisers)
*   [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) (for the GPU)

Nearly everything works fine with no special configuration. The sensors (accelerometer, gyroscope, magnetometer, ambient light sensor) don't seem to be recognised yet.

### Bluetooth

If the Broadcom USB device isn't showing up, you likely need to turn it on with `echo 1 > /sys/devices/platform/thinkpad_acpi/rfkill/rfkill0/state`

### Digitisers

The pen digitiser should be recognised by the wacom driver out of the box. The capacitive (touch) digitiser works with the same driver, but is not recognised as compatible by default. To fix this, add Atmel to the first MatchProduct entry in the wacom driver configuration file:

 `/etc/X11/xorg.conf.d/50-wacom.conf` 

```
Section "InputClass"
    Identifier "Wacom class"
    MatchProduct "Wacom|WACOM|Hanwang|PTK-540WL|Atmel"
    MatchDevicePath "/dev/input/event*"
    Driver "wacom"
EndSection

```

Everything should work after a reboot.

If you find yourself frustrated by the capacitive digitiser while trying to use the pen, you may have interest in the [thinkpad-helix-utils](https://aur.archlinux.org/packages/thinkpad-helix-utils/)<sup><small>AUR</small></sup> package. It contains a script, `helix-toggle-touch`, which will toggle the capacitive digitiser on and off with a simple command.

### Screen Rotation

If you have both digitisers configured through the xf86-input-wacom driver, they will automatically rotate with the display and you can use a simple command like `xrandr --output eDP1 --rotate left` to rotate the screen with ease.

If you want to use the bezel buttons (or some other hotkey) to cycle through orientations (or toggle between two specific ones), `helix-rotate`, also from from [thinkpad-helix-utils](https://aur.archlinux.org/packages/thinkpad-helix-utils/)<sup><small>AUR</small></sup>, provides an easy-to-bind command that may serve your needs well.

There is also [Magick Rotation](https://launchpad.net/magick-rotation/), which is supposed to automatically rotate the screen based on input events, but it only seems to respond to docking/undocking the tablet.

## BIOS/Firmware Updates

Helpfully, Lenovo now provides [bootable ISO images](http://support.lenovo.com/en_US/downloads/detail.page?DocID=DS034628) for the purpose of installing BIOS updates. While it is not stated on their site, these bootable images also include updated firmware for the keyboard dock MPU. It is uncertain as to whether the USB hub firmware is also updated via this utility.

**Note:** While the update utility states that all expansion units should be disconnected, it is only referring to external (USB and DisplayPort) devices. Ensure that the tablet is in the dock and connected only to AC power and the utility boot media before starting the process.

If you do not have access to a USB optical drive and writable media, the information on [ThinkWiki](http://www.thinkwiki.org/wiki/BIOS_Upgrade/X_Series) is extremely helpful.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Helix&oldid=414748](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_Helix&oldid=414748)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")