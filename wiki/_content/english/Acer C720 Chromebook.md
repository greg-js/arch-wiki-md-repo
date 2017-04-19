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
        *   [2.2.4 Fixing decrease in bandwidth](#Fixing_decrease_in_bandwidth)
    *   [2.3 Enabling the light sensor](#Enabling_the_light_sensor)
*   [3 Suspend](#Suspend)
    *   [3.1 Fix wakeup from suspend on lid close](#Fix_wakeup_from_suspend_on_lid_close)
    *   [3.2 Lots of ehci errors in dmesg after resume](#Lots_of_ehci_errors_in_dmesg_after_resume)
*   [4 Locating the Write-Protect Screw](#Locating_the_Write-Protect_Screw)
*   [5 Known Issues](#Known_Issues)
    *   [5.1 System freezes](#System_freezes)
    *   [5.2 Internal microphone not working](#Internal_microphone_not_working)
    *   [5.3 System shutdown on battery](#System_shutdown_on_battery)
*   [6 See also](#See_also)

## Installation

Go to the [Chrome OS devices](/index.php/Chrome_OS_devices "Chrome OS devices") page, read the [Introduction](/index.php/Chrome_OS_devices#Introduction "Chrome OS devices") and continue by following the [Installation](/index.php/Chrome_OS_devices#Installation "Chrome OS devices") guide.

## Configuration

For information on general Chromebook post installation configuration (hotkeys, power key handling ...) see the [Post installation configuration](/index.php/Chrome_OS_devices#Post_installation_configuration "Chrome OS devices") on the [Chrome OS devices](/index.php/Chrome_OS_devices "Chrome OS devices") page.

### Touchpad Configuration

See the [libinput](/index.php/Libinput "Libinput") article on how to install and setup your touchpad.

### Improving WLAN and BT performance

The C720 comes with Atheros AR9462 WLAN and Bluetooth chip which supported by `ath9k` kernel module, the following options to the `ath9k` module can help to affect the performance, quality and power consumption of the chip.

To add the desired module options, just create a `ath9k.conf` file as shown here with some example settings:

 `/etc/modprobe.d/ath9k.conf`  `options ath9k bt_ant_diversity=1 ps_enable=0` 

Details of possible settings are below.

#### Bluetooth coexistence

Both Bluetooth and WiFi can use 2.4 GHz, which can cause interference. You can enable Bluetooth coexistence to improve the performance of the card with the option `btcoex_enable=1`.

#### Power saving

You can enable power savings with the option `ps_enable=1` to reduce power usage, though it has been [suggested](https://bbs.archlinux.org/viewtopic.php?pid=1481644#p1481644) that enabling it might be related to system freezes and also to dropouts so if you encounter such issues then you might want to make sure it's disabled (`ps_enable=0`).

#### Improving signal quality

Enable antenna diversity with the option `bt_ant_diversity=1` to improve the signal quality and boost performance. However, keep in mind that [this disables the bluetooth interface](https://wireless.wiki.kernel.org/en/users/drivers/ath9k/antennadiversity) and, as such, bluetooth coexistence must not be loaded at the same time.

#### Fixing decrease in bandwidth

If you are experiencing a decrease in bandwidth at seemingly random times try switching from hardware to software wireless encryption as explained in [Wireless network configuration#ath9k](/index.php/Wireless_network_configuration#ath9k "Wireless network configuration").

### Enabling the light sensor

Intersil ISL29018 is the light sensor in the C720, as default its module is disabled on build time so in order to use the sensor the kernel should be recompiled with `CONFIG_SENSORS_ISL29018` enabled. You can also compile just the single module. Follow the preparation instructions as [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module"), enable the module in your `.config` and execute

```
$ make SUBDIRS=drivers/staging/iio/light modules

```

then follow [Compile kernel module#Module installation](/index.php/Compile_kernel_module#Module_installation "Compile kernel module") to install the module.

## Suspend

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

### Lots of ehci errors in dmesg after resume

See [Chrome OS devices#Fixing suspend](/index.php/Chrome_OS_devices#Fixing_suspend "Chrome OS devices"). Additionally, [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1364521#p1364521), [[2]](https://github.com/vonbrownie/linux-post-install/blob/master/config/c720_jessiebook/lib/systemd/system-sleep/ehci-pci.sh), [[3]](https://philipalban.wordpress.com/2014/04/25/fixing-suspend-in-xubuntu-on-the-acer-c720-a-simplified-guide/), and [[4]](https://bugzilla.redhat.com/show_bug.cgi?id=1218734) may be helpful.

One symptom may be that it cannot properly shut down or reboot.

## Locating the Write-Protect Screw

*   Remove the bottom panel of the laptop by removing the 12 visible screws and another one underneath the warranty sticker.
*   Separate the plastic starting at the back.
*   Remove completely the write-protect screw from the motherboard, which is labelled as #7 in [this picture](http://www.chromium.org/_/rsrc/1381990807648/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook/c720-chromebook-annotated-innards.png).

## Known Issues

### System freezes

See power saving section at [Improving WLAN and BT performance](#Improving_WLAN_and_BT_performance).

Additionally see [SSD#Troubleshooting](/index.php/SSD#Troubleshooting "SSD") if the system freezes are associated with hard drive errors in the system's journal.

### Internal microphone not working

If your internal microphone is not working (for example, in Skype), select "Microphone (unplugged)" as your input source in the PulseAudio Volume Control. Your internal microphone should now work. [[5]](http://forums.bodhilinux.com/index.php?/topic/9975-microphone-support-on-acer-c720/)

See also [Chrome OS devices#Fixing audio](/index.php/Chrome_OS_devices#Fixing_audio "Chrome OS devices") for another possible solution.

### System shutdown on battery

If you are on battery and the system shutdown when you use the keyboard, it's probably a battery switch mulfunction (cover don't press it all time), labbeled #5 in [this picture](http://www.chromium.org/_/rsrc/1381990807648/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook/c720-chromebook-annotated-innards.png). It is a safety mechanism to prevent the Acer C720 from being powered by the battery while the cover is removed.

You can bypass this switch with a screw inserted in hole #6.

## See also

*   [Chromium OS Acer C720 & C720P Developer Page](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/acer-c720-chromebook)
*   [BBS topic](https://bbs.archlinux.org/viewtopic.php?id=173418)
*   Unbricking with [flashrom](https://www.archlinux.org/packages/?name=flashrom) [using the Raspberry Pi](http://flashrom.org/RaspberryPi), requires [SOIC clip](http://www.hmcelectronics.com/product/Pomona/5250), See [GPIO matrix](http://elinux.org/Rpi_Low-level_peripherals#General_Purpose_Input.2FOutput_.28GPIO.29) and [pictures](https://drive.google.com/folderview?id=0B9f62MH0umbmRTA2Xzd5WHhjWEU&usp=sharing). also there is a [BeagleBone method](http://www.tnhh.net/2014/08/25/unbricking-chromebook-with-beaglebone.html).
*   [Configuration files with optimization tweaks for Haswell devices used by default in the GalliumOS Linux distribution](https://github.com/GalliumOS/galliumos-haswell).