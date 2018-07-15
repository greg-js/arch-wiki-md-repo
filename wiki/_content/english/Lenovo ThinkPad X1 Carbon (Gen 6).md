Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

## Contents

*   [1 Model description](#Model_description)
    *   [1.1 Support](#Support)
*   [2 BIOS](#BIOS)
    *   [2.1 Updates](#Updates)
*   [3 Suspend issues](#Suspend_issues)
    *   [3.1 Suspend-to-RAM (S3) not supported by default](#Suspend-to-RAM_.28S3.29_not_supported_by_default)
    *   [3.2 S0i3 sleep support](#S0i3_sleep_support)
    *   [3.3 BIOS configurations](#BIOS_configurations)
*   [4 Power management/Throttling issues](#Power_management.2FThrottling_issues)
    *   [4.1 Temporary fix](#Temporary_fix)
*   [5 TrackPoint and Touchpad issues](#TrackPoint_and_Touchpad_issues)
*   [6 References](#References)
*   [7 Additional resources](#Additional_resources)

## Model description

The Lenovo ThinkPad X1 Carbon, 6th generation is an ultrabook introduced in early 2018\. It comes in several variants(`20KH*` and `20KG*`) and features a 14" screen, 8th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 6th

```

### Support

| **Device** | **Working** | **Modules** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes | i915, (intel_agp) |
| [Wireless network](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes | iwlmvm |
| Native Ethernet with [included dongle](https://www3.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-TP-OneLink%2B-to-RJ45-Adapter/p/4X90K06975) | Yes |  ? |
| Mobile broadband | No*** |  ? |
| Audio | Yes | snd_hda_intel |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes* | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| Camera | Yes | uvcvideo |
| Fingerprint Reader | No** |  ? |
| [Power management](/index.php/Power_management "Power management") | Yes |  ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| microSD card reader | Yes | scsi_mod |
| Keyboard Backlight | Yes | thinkpad_acpi |
| Function/Multimedia Keys | Yes |  ? |

* via [workaround](#TrackPoint_and_Touchpad_issues)

** [progress being made](https://github.com/nmikhailov/Validity90) on driver

*** no working linux pcie driver for Fibocom L850-GL [forum link](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) - also see [this forum](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more progress.

## BIOS

The most convenient way to install Arch Linux is by disabling "Secure Boot" `Security -> Secure Boot - Set to "Disabled"`. However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

[BIOS update 1.25](https://pcsupport.lenovo.com/de/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-6th-gen-type-20kh-20kg/downloads) was released on 2018-06-28\. Obtain [geteltorito](https://aur.archlinux.org/packages/geteltorito/) and run `./geteltorito.pl -o bios-update.img n23ur08w.iso` on the downloaded ISO file to create a valid [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard)) image file, then flash this file on a USB drive via `dd` like you would flash [Arch installation media](/index.php/USB_flash_installation_media "USB flash installation media"). For further information see [flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux").

The ThinkPad X1 Carbon supports setting a custom splash image at the earliest boot stage(instead of the red "Lenovo" logo), more information can be found in the `README.TXT` located in the `FLASH` folder of the update image.

## Suspend issues

### Suspend-to-RAM (S3) not supported by default

The 6th Generation X1 Carbon supports S0i3 (also known as Windows Modern Standby) and does not support the S3 sleep state. A guide exists with [instructions for patching ACPI DSDT tables](https://delta-xi.net/#056) to add S3 support.

A [forum thread](https://bbs.archlinux.org/viewtopic.php?id=234913) has further discussion related to this issue.

### S0i3 sleep support

From [the Lenovo forums](https://forums.lenovo.com/t5/Linux-Discussion/X1-Carbon-Gen-6-cannot-enter-deep-sleep-S3-state-aka-Suspend-to/m-p/4016317/highlight/true#M10682): Add the following [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") to enable s0i3 sleep support:

```
acpi.ec_no_wakeup=1

```

**Note:** This disables wakeup/resume via lid open.

You might also need to disable the Realtek memory card reader (which appears to use a constant 2-3 W) either via the BIOS or via

```
echo "2-3" | sudo tee /sys/bus/usb/drivers/usb/unbind

```

### BIOS configurations

*   `Config -> Thunderbolt BIOS Assist Mode - Set to "Enabled"`. When disabled, on Linux, power usage appears to be significantly higher because of a substantial number of CPU wakeups during s2idle.

## Power management/Throttling issues

Due to wrong configured power management registers the CPU may consume a lot less power than under windows and the thermal throttling occurs at 80°C (97°C when using Windows, see [T480s throttling bug](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/)).

There is a [post in the official Lenovo forum](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489) to inform Lenovo about this issue.

### Temporary fix

Until Lenovo fixes this issue, you can manually set the limit.

To begin, install [msr-tools](https://www.archlinux.org/packages/?name=msr-tools).

Create the file `/usr/local/bin/cpu-throttling.sh` (making it executable) containing the following:

```
#!/bin/bash

/bin/modprobe msr
wrmsr -a 0x1a2 0x3000000 # which sets the offset to 3 C, so the new trip point is 97 C 

```

Then create the associated service file `/etc/systemd/system/cpu-throttling.service`:

```
[Unit]
Description=set cpu heating limit to 97°c

[Service]
ExecStart=/usr/local/bin/cpu-throttling.sh
RemainAfterExit=no

[Install]
WantedBy=timers.target

```

And also the timer in `/etc/systemd/system/cpu-throttling.timer`:

```
[Unit]
Description=set cpu heating limit to 97°c every minute

[Timer]
OnActiveSec=60
OnUnitActiveSec=60
Unit=cpu-throttling.service

[Install]
WantedBy=timers.target

```

Then, enable it:

```
# systemctl enable cpu-throttling.timer

```

Reboot and check with:

```
# rdmsr -f 29:24 -d 0x1a2

3

```

## TrackPoint and Touchpad issues

On the 20KG model, the Touchpad(Synaptics) and TrackPoint(Elantech) do not work together, one has to disable the TrackPoint in BIOS to get the Touchpad to work reliably out of the box. The root of the issue seems to be that the default loading of the TrackPoint via ancient PS/2 drivers conflicts with Touchpad loading. Synaptics has introduced a new way of doing things named RMI(4) that fixes some those issues. Further explanation is collected [in this thread](https://bbs.archlinux.org/viewtopic.php?id=236367).

As a workaround, add `synaptics_intertouch=1` to the `psmouse` [kernel module](/index.php/Kernel_module "Kernel module") options, for example in the cmdline of the [boot loader](/index.php/Boot_loader "Boot loader"):

```
 [...] root=/dev/sda1 rw psmouse.synaptics_intertouch=1 [...]

```

or by editing `/etc/modprobe.d/psmouse.conf`:

```
 options psmouse synaptics_intertouch=1

```

**Note:** When using [TLP](/index.php/TLP "TLP") with default powersaving settings, there might be occasional hiccups such as dropouts of tap-to-click functionality for the Touchpad, as well as the TrackPoint not surviving suspends and needing to be re-initialized

Reconnecting dead trackpad

```
echo -n "none" | sudo tee /sys/bus/serio/devices/serio1/drvctl
echo -n "reconnect" | sudo tee /sys/bus/serio/devices/serio1/drvctl
```

## References

*   [A good night's sleep for the Lenovo X1 Carbon Gen6](https://delta-xi.net/#056): Patching ACPI DSDT tables to add S3 support
*   [Lenovo forums: Cannot enter deep sleep S3](https://forums.lenovo.com/t5/Linux-Discussion/X1-Carbon-Gen-6-cannot-enter-deep-sleep-S3-state-aka-Suspend-to/td-p/3998182/highlight/true)
*   [Thread: No deep sleep](https://bbs.archlinux.org/viewtopic.php?id=234913): Includes DSDT patching solution and further discussion
*   [T480s throttling bug](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/), affects X1C6 as well
*   [Lenovo forums: T480s low cTDP and trip temperature in Linux](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489)
*   [Thread: TrackPoint/Touchpad issues, 20KG model](https://bbs.archlinux.org/viewtopic.php?id=236367)
*   [StackExchange: Success with enabling RMI4 config flags for Touchpad and TrackPoint](https://unix.stackexchange.com/a/431820)
*   [Kernel patch - Input: elantech - add support for SMBus devices](https://patchwork.kernel.org/patch/10324633/)
*   [Kernel patch - Input: synaptics - add Lenovo 80 series ids to SMBus](https://patchwork.kernel.org/patch/10330857/)

## Additional resources

*   [ThinkWiki X1 Carbon 6th Gen page](https://www.thinkwiki.org/wiki/Category:X1_Carbon_(6th_Gen))
*   Benjamin Tissoires, kernel maintainer of peripherals, has explained how input bugs get fixed in his talk [Tools to debug a broken input device](https://www.youtube.com/watch?v=Bl_0xYxcYd8) ([Slides](https://www.x.org/wiki/Events/XDC2015/Program/tissoires_input_debug_tools.html)), especially interesting are slides 16 onward.
*   [Dell XPS 13 9370 quirks](https://gist.github.com/greigdp/bb70fbc331a0aaf447c2d38eacb85b8f): Some pointers on getting Watt usage down to ~2W, Intel video powersaving features might be interesting, see also [Intel Graphics Powersaving](/index.php/Intel_graphics#Module-based_Powersaving_Options "Intel graphics")
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)"): Shares some hardware with the X1C6
*   [Intel Blog: Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues), including the [pm-graph](https://github.com/01org/pm-graph) tool to analyze power usage during suspend