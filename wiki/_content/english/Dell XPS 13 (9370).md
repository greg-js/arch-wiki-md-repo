| **Device** | **Status** | **Modules** |
| Video | Working | i915 |
| Wireless | Working | ath10k |
| Bluetooth | Working | btusb |
| Audio | Working | snd_hda_intel |
| Touchpad | Working | hid_multitouch |
| Webcam | Working ¹ | uvcvideo |
| USB-C / Thunderbolt 3 | Working | intel_wmi_thunderbolt |
| Wireless switch | Working | intel_hid |
| Function/Multimedia Keys | Working | ? |
| Fingerprint sensor | Not working | ? |

Related articles

*   [Dell XPS 13 (9333)](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)")
*   [Dell XPS 13 (9343)](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)")
*   [Dell XPS 13 (9350)](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")
*   [Dell XPS 13 2-in-1 (9365)](/index.php/Dell_XPS_13_2-in-1_(9365) "Dell XPS 13 2-in-1 (9365)")

The Dell XPS 13 Early 2018 (9370) is the fifth-generation model of the XPS 13 line. The laptop was released in January 2018 in both a standard edition with Windows installed as well as a Developer Edition with Ubuntu 16.04 installed, featuring kernel 4.4 as of now. There are only minor hardware differences between them, mostly in regards to the mainboard microchip manufacturers. [According to Dell](https://www.dell.com/community/Linux-Developer-Systems/XPS-13-Fingerprint-reader-Linux-support/m-p/5090726/highlight/true#M7295) the fingerprint reader is not present on the Linux variant. Just like the older versions ([9333](/index.php/Dell_XPS_13_(9333) "Dell XPS 13 (9333)"), [9343](/index.php/Dell_XPS_13_(9343) "Dell XPS 13 (9343)"), [9350](/index.php/Dell_XPS_13_(9350) "Dell XPS 13 (9350)"), and [9360](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)")) it is available in different hardware configurations as well. These fifth gen models includes Intel's eighth generation Kaby Lake R processors, and can be configured with up to 16GB LPDDR3 2133 MHz RAM and a 1TB PCI SSD. Unlike previous iterations, the Wi-Fi/BT module is soldered and cannot be replaced, only the Killer 1435 (QCA6174A) is available for consumers, enterprise versions with the Intel 8265 modem also exist.

The installation process for Arch on the XPS 13 does not differ from any other PC. Although you might need to consider upgrading the SSD Firmware first if you have a working Windows installation (see section [#Storage](#Storage)). For installation help, please see the [Installation guide](/index.php/Installation_guide "Installation guide") and [UEFI](/index.php/UEFI "UEFI"). This page covers the current status of hardware support on Arch, as well as post-installation recommendations.

¹ The webcam works with kernel 4.17.4 or later. For earlier kernels this applies: Some users have experienced webcam firmware issues with recent models and there are [many reports of non-functional webcams on new laptops](https://www.dell.com/community/Linux-General/Dell-xps-13-9370-Webcam-support/td-p/6032049). User reports indicate Dell support is responsive to replacing screens to install a webcam that uses linux-compatible UVC 1.0 rather than 1.5 firmware drivers.

## Contents

*   [1 UEFI](#UEFI)
*   [2 Content Adaptive Brightness Control](#Content_Adaptive_Brightness_Control)
*   [3 Video](#Video)
*   [4 Storage](#Storage)
*   [5 Wifi](#Wifi)
*   [6 Bluetooth](#Bluetooth)
*   [7 Keyboard](#Keyboard)
*   [8 Power Management](#Power_Management)
*   [9 Firmware Updates](#Firmware_Updates)
*   [10 Thermal Throttling](#Thermal_Throttling)
*   [11 Thermal Modes / Fan profiles](#Thermal_Modes_.2F_Fan_profiles)
*   [12 Power Saving](#Power_Saving)
*   [13 Touchpad](#Touchpad)
    *   [13.1 Cursor Jump](#Cursor_Jump)
    *   [13.2 Sensitivity](#Sensitivity)
*   [14 Audio](#Audio)
*   [15 USB Type-C ports](#USB_Type-C_ports)
*   [16 Fingerprint reader](#Fingerprint_reader)

## UEFI

Before installing it is necessary to modify some UEFI Settings. They can be accessed by pressing the F2 key repeatedly when booting.

*   Change the SATA Mode from the default "RAID" to "AHCI". This will allow Linux to detect the NVME SSD. If dual booting with an existing Windows installation, Windows will not boot after the change but [this can be fixed without a reinstallation](https://triplescomputers.com/blog/uncategorized/solution-switch-windows-10-from-raidide-to-ahci-operation/).
*   Disable secure boot to allow Linux to boot.
*   To boot from a USB device attached via the USB-C to USB-A adapter included in the box, you'll need to enable Thunderbolt boot. Once enabled, F12 on boot will enter the boot menu.

It is also possible to use the right USB-C port directly without any UEFI adjustment.

## Content Adaptive Brightness Control

In the XPS 13 the display panels (both FHD and 4K UHD) come with Content Adaptive Brightness Control (usually referred to as CABC or DBC) enabled by default. While disabling required flashing the display firmware in previous generations, DBC can now be disabled in recent BIOS versions. To test if DBS is enabled, go to this [test page](https://tylerwatt12.com/dc/).

## Video

The video should work with the `i915` driver of the current [linux](https://www.archlinux.org/packages/?name=linux) kernel. Consult [Intel graphics](/index.php/Intel_graphics "Intel graphics") for a detailed installation and configuration guide as well as for [Intel graphics#Troubleshooting](/index.php/Intel_graphics#Troubleshooting "Intel graphics").

If you have the 4K (3840x2160) model, also check out [HiDPI](/index.php/HiDPI "HiDPI") for UI scaling configurations.

Note that the `enable_psr=1` kernel parameter appears not to work properly, at least on the touchscreen model.

[Some user support requests indicate that currently-shipping 9370 models may bundle webcams that use UVC 1.5 firmware rather than 1.0](https://www.dell.com/community/Linux-General/Dell-xps-13-9370-Webcam-support/td-p/6032049), which was not supported [prior to kernel 4.17.4](https://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git/diff/drivers/media/usb/uvc/uvc_video.c?id=v4.17.4&id2=v4.17.3).

For me the system seems to freeze sometime which is due to enable_psr=1, you can either disable enable_psr=0 where you will loose battery life but get no freezes, or enable_psr=2 where you save battery life like enable_psr=1 but without any freezes. enable_psr=1 maximizes batterylife but for me gives the system freezes, hopefully this will get fixed in the future.

To do so with sudo create a file /etc/modprobe.d/1915.conf:

```
 options i915 enable_psr=2

```

Some other options that save battery life are:

```
 options i915 enable_psr=2 enable_rc6=7 enable_fbc=1 semaphores=1 lvds_downclock=1 enable_guc_loading=1 enable_guc_submission=1

```

## Storage

The nvme SSD is a Toshiba KXG50ZNV256G, KXG50ZNV512G or KXG50ZNV1T02\. The stock firmware version AADA4102 has severe problems when the ssd enters the lowest power state. This results in a unresponsive device (kernel complains about read-only filesystem) The problems can occur any time, but seem to have become way more common on Kernel 4.18 on battery power. [Firmware Version AADA4105](https://www.dell.com/support/home/us/en/19/drivers/driversdetails?driverid=c0pf8) seems to fix the problem. As the upgrade is only possible under windows the following kernel parameter works as a workaround (see [Solid state drive/NVMe](/index.php/Solid_state_drive/NVMe "Solid state drive/NVMe")):

```
 nvme_core.default_ps_max_latency_us=6000   

```

## Wifi

The Wifi adapter contains a Qualcomm Atheros QCA6174 module. It should work out of the box with the `ath10k_pci` driver in recent [linux](https://www.archlinux.org/packages/?name=linux) kernels.

## Bluetooth

The Bluetooth adapter sometimes becomes unavailable after waking up from suspend and can even stay deactivated and invisible after a warm reboot.

## Keyboard

The keyboard backlight has a feature that makes it automatically turn off after a given timeout. This timeout can be adjusted by writing into `/sys/class/leds/dell\:\:kbd_backlight/stop_timeout`. For example,

```
echo "5m" > /sys/class/leds/dell\:\:kbd_backlight/stop_timeout

```

This would set the timeout to 5 minutes. Note that different timeouts are maintained when the machine is connected to AC and when it's running from battery. Before BIOS 1.4.0 [there was an issue](https://github.com/dell/libsmbios/issues/48) that prevented the user from changing the timeout on AC. A kernel workaround was added in 4.18 and it was eventually fixed by BIOS 1.4.0.

## Power Management

If the laptop seems to have an high drain when in sleep mode. As a possible workaround, you can set the machine to enter S3 deep sleep mode. Add `quiet mem_sleep_default=deep` to the [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

According to the manufacturer (see [this upstream kernel bug](https://bugzilla.kernel.org/show_bug.cgi?id=199689)), the machine uses S2 intentionally instead of S3, and they are working towards fixing the power drain on S2.

Note: on older BIOS and/or kernel versions [the power button cannot be used to wake the laptop from sleep](https://www.spinics.net/lists/platform-driver-x86/msg15644.html). In this case the Sleep button (Fn + End, or just End if you have Fn lock enabled) can still wake up the machine. This has been fixed by a BIOS update.

## Firmware Updates

Dell provides firmware updates via Linux Vendor Firmware Service (LVFS). Refer to [Flashing BIOS from Linux#fwupd](/index.php/Flashing_BIOS_from_Linux#fwupd "Flashing BIOS from Linux") for additional information. A package is readily available at [fwupd](https://www.archlinux.org/packages/?name=fwupd). Updates are provided for the Thunderbolt controller as well. [There is an issue](https://github.com/dell/thunderbolt-nvm-linux/issues/10) where the Thunderbolt version number is detected as `00.00` after reflashing (currently being investigated).

Dell has also released updates to the SSD firmware, but these can only be updated from Windows, not from Linux.

## Thermal Throttling

By default thermal throttling activates around 80C resulting in maximum sustained CPU frequency around 2.4Ghz, much lower than in Dell's standard Windows installation.

```
Package temperature above threshold, cpu clock throttled (total events = 971)

```

This can be resolved using [lenovo-throttling-fix-git](https://aur.archlinux.org/packages/lenovo-throttling-fix-git/). Despite originally conceived to resolve the same issue with Lenovo laptops, it works with the XPS 9370 (and should work well with other Skylake or newer laptops).

## Thermal Modes / Fan profiles

Just like in Windows by using Dell Power Manager you can set the thermal configuration and behaviour of the fans of your machine. This is done within a terminal with the following commands.

To find out what thermal mode is set type:

```
# smbios-thermal-ctl -g

```

To find all available thermal modes type:

```
# smbios-thermal-ctl -i

```

And finally to set the desired thermal mode that you identified with the command before type:

```
# smbios-thermal-ctl --set-thermal-mode=THERMAL_MODE

```

## Power Saving

To save more battery use [tlp](/index.php/Tlp "Tlp") package AND/OR [Powertop](/index.php/Powertop "Powertop").

You can monitor the used power and also the temperature of your machine with the [s-tui](https://aur.archlinux.org/packages/s-tui/) tool.

## Touchpad

### Cursor Jump

The touchpad can sometimes produce a "cursor jump". Sometimes this is detected and worked around by libinput, resulting in a similar journal entry:

```
libinput error: event12 - DELL07E6:00 06CB:76AF Touchpad: kernel bug: Touch jump detected and discarded.

```

There is a [libinput bug about this](https://gitlab.freedesktop.org/libinput/libinput/issues/36) where the conclusion was that this is probably a hardware issue or a bug in the kernel driver.

### Sensitivity

By default, the [libinput](/index.php/Libinput "Libinput") driver might not have the desired sensitivity. The acceleration can be changed via [xinput](/index.php/Xinput "Xinput") as follows:

```
 xinput --set-prop $(xinput | grep 'DELL.*Touchpad' | awk '{print $6}' | sed 's/id=//g') 'libinput Accel Speed' 0.5

```

## Audio

Works correctly, but the audio controller cannot figure out what kind of device is plugged into the jack on its own. For this reason the desktop environment (eg. Gnome) will pop up a dialog where you can choose if it was a headset, or microphone, etc.

## USB Type-C ports

The 9370 has only three Type-C ports (and no other ports, just an audio jack). Two of these (on the left side) support Thunderbolt 3\. There is no power jack. A 45 W USB Type-C charger is included in the box. Any of the three Type-C ports can be used for charging. Since the laptop has no USB-A ports, one Dell-branded Type-C to A adapter is included.

Also all three Type-C ports support DisplayPort alternate mode. It is taken care of by the firmware, so it will work even with older kernels that do not otherwise support it. To the operating system it appears as if the laptop had two DisplayPort connectors (in addition to the embedded DP that the internal screen uses). So far I've tested the following adapters. All of these will appear to the operating system as if you plugged something into one of the DP connectors.

*   [Club3D Type-C to DisplayPort 1.2 adapter](https://www.club-3d.com/en/detail/2350/usb_3.1_type_c_to_displayport_1.2/) (tested with 1080p and 4K, both work at 60 Hz)
*   [Dell Type-C to VGA adapter](https://www.dell.com/en-us/shop/dell-adapter-usb-c-to-vga/apd/470-abnc/pc-accessories) (tested with 1080p at 60 Hz)
*   [Dell Type-C to HDMI adapter](https://www.dell.com/en-us/work/shop/dell-adapter-usb-c-to-hdmi/apd/470-abmz/pc-accessories) (tested with 1080p and 4K, both work at 60 Hz)
*   [Moshi USB-C to HDMI Adapter](https://www.moshi.com/en/product/usb-c-to-hdmi-adapter/silver) (tested with 1080p and 4K, both work at 60 Hz)

## Fingerprint reader

The fingerprint reader is not supported. There is a [libfprint feature request](https://gitlab.freedesktop.org/libfprint/libfprint/issues/43).