# Acer C720 Chromebook

Related articles

*   [Chrome OS devices](/index.php/Chrome_OS_devices "Chrome OS devices")
*   [Laptop](/index.php/Laptop "Laptop")

**Warning:** This article relies on third-party scripts and modifications, and may irreparably damage your hardware or data. Proceed at your own risk.

The Acer C720 Chromebook (and newer Chromebooks in general) features a "legacy boot" mode that makes it easy to boot Linux and other operating systems. The legacy boot mode is provided by the [SeaBIOS](http://www.coreboot.org/SeaBIOS) payload of [Coreboot](http://www.coreboot.org/). SeaBIOS behaves like a traditional BIOS that boots into the MBR of a disk, and from there into your standard bootloaders like Syslinux and GRUB.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Touchpad Configuration](#Touchpad_Configuration)
    *   [2.2 Improving WLAN and BT performance](#Improving_WLAN_and_BT_performance)
        *   [2.2.1 Bluetooth coexistence](#Bluetooth_coexistence)
        *   [2.2.2 Power saving](#Power_saving)
        *   [2.2.3 Improving signal quality](#Improving_signal_quality)
    *   [2.3 Fix wakeup from suspend on lid close](#Fix_wakeup_from_suspend_on_lid_close)
    *   [2.4 Enabling the light sensor](#Enabling_the_light_sensor)
*   [3 Locating the Write-Protect Screw](#Locating_the_Write-Protect_Screw)
*   [4 Known Issues](#Known_Issues)
    *   [4.1 System freezes](#System_freezes)
*   [5 See also](#See_also)

## Installation

Go to the [Chromebook](/index.php/Chromebook "Chromebook") page, read the [Introduction](/index.php/Chromebook#Introduction "Chromebook") and continue by following the [Installation](/index.php/Chromebook#Installation "Chromebook") guide.

## Configuration

For information on general Chromebook post installation configuration (hotkeys, power key handling ...) see the [Post installation configuration](/index.php/Chromebook#Post_installation_configuration "Chromebook") on the [Chromebook](/index.php/Chromebook "Chromebook") page.

### Touchpad Configuration

[Add](/index.php/Edit "Edit") the Xorg touchpad configuration below for better usability (increases touchpad sensitivity).

 `/etc/X11/xorg.conf.d/50-cros-touchpad.conf` 

```
Section "InputClass" 
    Identifier      "touchpad peppy cyapa" 
    MatchIsTouchpad "on" 
    MatchDevicePath "/dev/input/event*" 
    MatchProduct    "cyapa" 
    Option          "FingerLow" "10" 
    Option          "FingerHigh" "10" 
EndSection
```

If you want to remove the "right-click" behavior from the touchpad from the bottom right area (you can still right-click with two finger clicks), you should add two lines to following section from `/etc/X11/xorg.conf.d/50-cros-touchpad.conf`

 `/etc/X11/xorg.conf.d/50-cros-touchpad.conf` 

```

Section "InputClass"
    Identifier      "touchpad peppy cyapa"
    MatchIsTouchpad "on"
    MatchDevicePath "/dev/input/event*"
    MatchProduct    "cyapa"
    Option          "FingerLow" "8"
    Option          "FingerHigh" "16"
    Option "SoftButtonAreas" "0% 0 0% 0 0 0 0 0"
    Option "AreaBottomEdge" "0%"
EndSection

```

### Improving WLAN and BT performance

The C720 comes with Atheros AR9462 WLAN and Bluetooth chip which supported by `ath9k` kernel module, the following options to the `ath9k` module can help to affect the performance, quality and power consumption of the chip.

#### Bluetooth coexistence

Both Bluetooth and WiFi can use 2.4 GHz, which can cause interference. You can enable Bluetooth coexistence to improve the performance of the card with the option `btcoex_enable=1`.

#### Power saving

You can enable power savings with the option `ps_enable=1` to reduce power usage, though it has been [suggested](https://bbs.archlinux.org/viewtopic.php?pid=1481644#p1481644) that enabling it might be related to system freezes and also to dropouts so if you encounter such issues then you might want to make sure it's disabled (`ps_enable=0`).

#### Improving signal quality

Enable antenna diversity with the option `bt_ant_diversity=1` to improve the signal quality and boost performance. However, keep in mind that [this disables the bluetooth interface](https://wireless.wiki.kernel.org/en/users/drivers/ath9k/antennadiversity) and, as such, bluetooth coexistence must not be loaded at the same time.

To add the desired module options, just create a `ath9k.conf` file as shown here:.

 `/etc/modprobe.d/ath9k.conf`  `options ath9k bt_ant_diversity=1 ps_enable=0` 

### Fix wakeup from suspend on lid close

When the lid of the C720 is closed, the top of the screen presses against the touchpad, instantly waking the computer from suspend. To disable wakeup by touchpad, create the following file:

 `/etc/tmpfiles.d/disable-touchpad-wakeup.conf`  `w /proc/acpi/wakeup - - - - TPAD` 

To check the current state:

```
# cat /proc/acpi/wakeup | grep TPAD

```

Alternatively, it may be toggled manually by running:

```
# su
# echo TPAD > /proc/acpi/wakeup

```

This method does not persist after a reboot.

### Enabling the light sensor

Intersil ISL29018 is the light sensor in the C720, as default its module is disabled on build time so in order to use the sensor the kernel should be recompiled with `CONFIG_SENSORS_ISL29018` enabled.

## Locating the Write-Protect Screw

*   Remove the bottom panel of the laptop by removing the 12 visible screws and another one underneath the warranty sticker.
*   Separate the plastic starting at the back.
*   Remove completely the write-protect screw from the motherboard, which is labelled as #7 in [this picture](http://www.chromium.org/_/rsrc/1381990807648/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook/c720-chromebook-annotated-innards.png).

## Known Issues

### System freezes

See power saving section at [Improving WLAN and BT performance](#Improving_WLAN_and_BT_performance).

## See also

*   [Chromium OS Acer C720 & C720P Developer Page](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook)
*   [BBS topic](https://bbs.archlinux.org/viewtopic.php?id=173418)
*   Unbricking with [flashrom](https://www.archlinux.org/packages/?name=flashrom) [using the Raspberry Pi](http://flashrom.org/RaspberryPi), requires [SOIC clip](http://www.hmcelectronics.com/product/Pomona/5250), See [GPIO matrix](http://elinux.org/Rpi_Low-level_peripherals#General_Purpose_Input.2FOutput_.28GPIO.29) and [pictures](https://drive.google.com/folderview?id=0B9f62MH0umbmRTA2Xzd5WHhjWEU&usp=sharing). also there's a [BeagleBone method](http://www.tnhh.net/2014/08/25/unbricking-chromebook-with-beaglebone.html).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_C720_Chromebook&oldid=413880](https://wiki.archlinux.org/index.php?title=Acer_C720_Chromebook&oldid=413880)"