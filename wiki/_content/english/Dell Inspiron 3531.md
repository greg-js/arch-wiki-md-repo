This page describes Arch's issues with Dell Inspiron 15 3531 (Dell's budget model of autumn 2014).

## Contents

*   [1 Hardware Specifications](#Hardware_Specifications)
    *   [1.1 lspci Output](#lspci_Output)
    *   [1.2 lsusb Output](#lsusb_Output)
*   [2 Installation in MBR mode](#Installation_in_MBR_mode)
*   [3 Kernel](#Kernel)
    *   [3.1 Video artifacts at boot](#Video_artifacts_at_boot)
*   [4 Hardware](#Hardware)
    *   [4.1 Video](#Video)
    *   [4.2 HDMI output](#HDMI_output)
    *   [4.3 Input](#Input)
        *   [4.3.1 Touchpad](#Touchpad)
        *   [4.3.2 SD card reader](#SD_card_reader)
    *   [4.4 Networking](#Networking)
        *   [4.4.1 Wired](#Wired)
        *   [4.4.2 Wireless](#Wireless)
        *   [4.4.3 3G Modem](#3G_Modem)
    *   [4.5 Audio](#Audio)
    *   [4.6 Backlight (and XFCE)](#Backlight_.28and_XFCE.29)

## Hardware Specifications

This cheap stripped down model has:

*   no optical drive (and, although there is a slot for the drive, motherboard has no SATA connector),
*   no Bluetooth,
*   no CPU fan,
*   no external microphone jack
*   no Ethernet (RJ45) jack.

### lspci Output

```
00:00.0 Host bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series SoC Transaction Register (rev 0e)
00:02.0 VGA compatible controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Graphics & Display (rev 0e)
00:13.0 SATA controller: Intel Corporation Device 0f23 (rev 0e)
00:1a.0 Encryption controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Trusted Execution Engine (rev 0e)
00:1b.0 Audio device: Intel Corporation Atom Processor Z36xxx/Z37xxx Series High Definition Audio Controller (rev 0e)
00:1c.0 PCI bridge: Intel Corporation Device 0f48 (rev 0e)
00:1c.1 PCI bridge: Intel Corporation Device 0f4a (rev 0e)
00:1c.2 PCI bridge: Intel Corporation Device 0f4c (rev 0e)
00:1c.3 PCI bridge: Intel Corporation Device 0f4e (rev 0e)
00:1d.0 USB controller: Intel Corporation Atom Processor Z36xxx/Z37xxx Series USB EHCI (rev 0e)
00:1f.0 ISA bridge: Intel Corporation Atom Processor Z36xxx/Z37xxx Series Power Control Unit (rev 0e)
00:1f.3 SMBus: Intel Corporation Device 0f12 (rev 0e)
02:00.0 Network controller: Qualcomm Atheros AR9485 Wireless Network Adapter (rev 01)

```

### lsusb Output

```
Bus 001 Device 005: ID 0bda:0129 Realtek Semiconductor Corp. RTS5129 Card Reader Controller
Bus 001 Device 004: ID 0bda:58c2 Realtek Semiconductor Corp. 
Bus 001 Device 002: ID 8087:07e6 Intel Corp. 
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

## Installation in MBR mode

The only installation method possible on this computer is from a USB key. Create one following [this page](/index.php/USB_flash_installation_media "USB flash installation media").

In the following the MBR booting mode is assumed (UEFI boot mode was not tested). To turn on the Legacy BIOS boot mode (aka MBR) in the BIOS menu, press F2 at startup. Set secure boot to off and set boot list order to legacy. Also change function keys from the multimedia mode.

Then follow [Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide").

## Kernel

The standard Arch kernel works fine.

### Video artifacts at boot

After the GRUB menu a first couple of lines are garbage. To remedy add to /etc/mkinitcpio.conf the line

```
MODULES="i915" 

```

and run

```
sudo mkinitcpio -p linux

```

## Hardware

### Video

Install the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver.

### HDMI output

More details to come as I test it.

### Input

#### Touchpad

To make it work install the [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics) driver.

Hypersensity of the touchpad can be reduced by editing /etc/X11/xorg.conf.d/50-synaptics.conf

```
Section "InputClass"
       Identifier "touchpad catchall"
       ....
       Option "FingerLow" "35"  <-- add this
       Option "FingerHigh" "45" <-- add this
       ....
EndSection

```

Tune the values to your taste (increasing reduces sensitivity).

#### SD card reader

The laptop has an RTS5129 controller which is now handled by modules rtsx_usb and rtsx_usb_sdmmc. To load temporarily:

```
sudo modprobe rtsx_usb 
sudo modprobe rtsx_usb_sdmmc

```

To enable permanently create file /etc/modules-load.d/sdcard.conf with two lines:

```
rtsx_usb 
rtsx_usb_sdmmc

```

### Networking

#### Wired

Works out of the box through a USB-to-Ethernet adaptor.

#### Wireless

Atheros AR9485 works out of the box. [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) was used to manage networks.

#### 3G Modem

A test device Huawei E173 (connected via a USB hub) was detected and worked fine with [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet), [modem-manager-gui](https://www.archlinux.org/packages/?name=modem-manager-gui), [usb_modeswitch](https://www.archlinux.org/packages/?name=usb_modeswitch) and [mobile-broadband-provider-info](https://www.archlinux.org/packages/?name=mobile-broadband-provider-info) packages.

### Audio

Built-in microphone does not work out of the box. To enable, create a file /etc/modeprobe.d/modeprobe.conf with a line

```
options snd-hda-intel model=laptop

```

and *unmute* microphones in alsamixer (press 'M' on devices with an "MM" annotation).

### Backlight (and XFCE)

For those with sensitive eyes the default handling of backlight in XFCE can be troublesome. The range of the intel_backlight on this laptop is 7812 steps, however [xfce4-power-manager](https://www.archlinux.org/packages/?name=xfce4-power-manager) uses only [hardcoded 10 steps](https://forum.xfce.org/viewtopic.php?pid=29952#p29952) what might be too coarse. Adding acpi_backlight=vendor to the kernel parameters creates /sys/class/backlight/dell_backlight/ with max_brightness=15, and power-manager now steps with 20% of it (3 points), which may also be suboptimal.

The usual workaround to assign commands "xbacklight +5" and "xbacklight -5" to the function keys Fn+F5/F4 (using Settings->Keyboard) to finer-grained control does not solve the problem, because the power manager intercepts keystrokes. [Disabling the brightness keys in the power manager](http://www.n0nb.us/blog/2012/02/restoring-screen-brightness-step-size-on-xfce4/) AND enabling the above keyboard shotcuts somehow works (decreasing brightness and increasing it again does not always give you the same number). Test it to see if you are fine with such a behavior.

Finest grained control of the backlight can be achieved with the direct setting

```
echo 100 | sudo tee /sys/class/backlight/intel_backlight/brightness

```

(change 100 to your number of choice). To complicate things even more, this value is not saved after reboot if it's less than 390, because systemd is hardcoded to have at least [5% of max_brightness at start-up](http://lists.freedesktop.org/archives/systemd-devel/2014-March/017823.html). If your favorite brightness is below 390, the only way is to run this number on every boot.