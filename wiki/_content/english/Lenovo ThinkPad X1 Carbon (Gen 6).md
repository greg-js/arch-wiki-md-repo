Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")

The Lenovo ThinkPad X1 Carbon, 6th generation is an ultrabook introduced in early 2018\. It comes in several variants(`20KH*` and `20KG*`) and features a 14" screen, 8th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 6th

```

| **Device** | **Working** | **Modules** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes | i915, (intel_agp) |
| [Wireless network](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes | iwlmvm |
| Native Ethernet with [included dongle](https://www3.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-TP-OneLink%2B-to-RJ45-Adapter/p/4X90K06975) | Yes | ? |
| Mobile broadband | No¹ | ? |
| Audio | Yes | snd_hda_intel |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| Camera | Yes | uvcvideo |
| Fingerprint Reader | No² | ? |
| [Power management](/index.php/Power_management "Power management") | Yes³ | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes | btusb |
| microSD card reader | Yes | scsi_mod |
| Keyboard Backlight | Yes | thinkpad_acpi |
| Function/Multimedia Keys | Yes | ? |
| 

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.
2.  [The Validity90 project](https://github.com/nmikhailov/Validity90) began reverse engineering the reader, but updates have stopped recently.
3.  S3 suspend requires changes to BIOS settings - see section on [suspend issues](#Suspend_issues).

 |

## Contents

*   [1 BIOS](#BIOS)
    *   [1.1 Updates](#Updates)
        *   [1.1.1 Automatic Linux Vendor Firmware Service](#Automatic_Linux_Vendor_Firmware_Service)
        *   [1.1.2 Manual Installation](#Manual_Installation)
*   [2 Suspend issues](#Suspend_issues)
    *   [2.1 Enabling S3](#Enabling_S3)
    *   [2.2 Verifying S3](#Verifying_S3)
    *   [2.3 Disabling the memory card reader](#Disabling_the_memory_card_reader)
    *   [2.4 BIOS configurations](#BIOS_configurations)
*   [3 Power management/Throttling issues](#Power_management.2FThrottling_issues)
    *   [3.1 Throttling fix](#Throttling_fix)
*   [4 Configuration](#Configuration)
    *   [4.1 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)
    *   [4.2 Special buttons](#Special_buttons)
    *   [4.3 HDR Display Color Calibration](#HDR_Display_Color_Calibration)
*   [5 TrackPoint and Touchpad issues](#TrackPoint_and_Touchpad_issues)
*   [6 Full-disk encryption](#Full-disk_encryption)
    *   [6.1 Ramdisk module](#Ramdisk_module)
*   [7 Tools](#Tools)
    *   [7.1 Diagnostics](#Diagnostics)
*   [8 References](#References)
*   [9 Additional resources](#Additional_resources)

## BIOS

The most convenient way to install Arch Linux is by disabling "Secure Boot" `Security -> Secure Boot - Set to "Disabled"`. However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

#### Automatic Linux Vendor Firmware Service

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service(LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual Installation

[BIOS update 1.31](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-6th-gen-type-20kh-20kg/downloads) was released on 2018-10-02\. Obtain [geteltorito](https://aur.archlinux.org/packages/geteltorito/) and run `geteltorito.pl -o bios-update.img n23ur12w.iso` on the downloaded ISO file to create a valid [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard) image file, then flash this file on a USB drive via `dd` like you would flash [Arch installation media](/index.php/USB_flash_installation_media "USB flash installation media"). For further information see [flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux").

The ThinkPad X1 Carbon supports setting a custom splash image at the earliest boot stage (instead of the red "Lenovo" logo), more information can be found in the `README.TXT` located in the `FLASH` folder of the update image.

## Suspend issues

Since BIOS version 1.30, the X1 Carbon supports S3 mode when enabled in the BIOS menu (choose "Linux" sleep mode instead of the default "Windows 10"). See [#Automatic Linux Vendor Firmware Service](#Automatic_Linux_Vendor_Firmware_Service) for instructions to update and verify your BIOS version.

### Enabling S3

To enable S3 support, make sure you have at least BIOS version 1.30 installed. Then, go into the BIOS configuration, and `Config -> Power -> Sleep State - Set to "Linux"`. This should make S3 available. To verify, after making the changes in the BIOS configuration, boot into Linux, and run the `dmesg` command again to make sure that S3 is now available.

### Verifying S3

To check whether S3 is recognized and usable by Linux, run:

```
dmesg | grep -i "acpi: (supports"

```

and check for `S3` in the list.

### Disabling the memory card reader

You might also need to disable the Realtek memory card reader (which appears to use a constant 2-3 W) either via the BIOS or via

```
echo "2-3" | sudo tee /sys/bus/usb/drivers/usb/unbind

```

### BIOS configurations

*   `Config -> Thunderbolt BIOS Assist Mode - Set to "Enabled"`. When disabled, on Linux, power usage appears to be significantly higher because of a substantial number of CPU wakeups during s2idle.

## Power management/Throttling issues

Due to wrong configured power management registers the CPU may consume a lot less power than under windows and the thermal throttling occurs at 80°C (97°C when using Windows, see [T480s throttling bug](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/)).

There is a [post in the official Lenovo forum](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489) to inform Lenovo about this issue.

### Throttling fix

An easy package has been written to address the problem until (or if) Lenovo ever solves it.

Install [lenovo-throttling-fix-git](https://aur.archlinux.org/packages/lenovo-throttling-fix-git/), then run:

```
sudo systemctl enable --now lenovo_fix.service

```

The script also supports more advance thermal/performance features including CPU undervolting. See the [lenovo-throttling-fix repository](https://github.com/erpalma/lenovo-throttling-fix) `README.md` for details.

**Note:** If you installed [thermald](https://www.archlinux.org/packages/?name=thermald), it may conflict with the throttling fix in this package. Consider disabling thermald or otherwise work around this.

## Configuration

### Keyboard Fn Shortcuts

*   Fn+4 sends XF86Sleep (puts computer to sleep by default)
*   Fn+S sends Alt_L+Sys_Req
*   Fn+P sends Pause
*   Fn+B sends Control_L+Break
*   Fn+K sends Scroll_Lock
*   Fn+Space toggles the keyboard backlight
*   Fn by itself sends XF86WakeUp (wakes computer from sleep by default)

### Special buttons

Some special buttons are not supported by X server due to keycode number limit.

| Key combination | Scancode | Keycode | Note |
| `Fn+F11` | `0x49` | `374` `KEY_KEYBOARD` | Not recognized in [Wayland](/index.php/Wayland "Wayland") |
| `Fn+F12` | `0x45` | `364` `KEY_FAVORITES` | Recognized correctly on [Wayland](/index.php/Wayland "Wayland") |

You can remap unsupported keys using [udev hwdb](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes"):

 `/etc/udev/hwdb.d/90-thinkpad-keyboard.hwdb` 
```
evdev:name:ThinkPad Extra Buttons:dmi:bvn*:bvr*:bd*:svnLENOVO*:pn*
 KEYBOARD_KEY_49=prog1
 KEYBOARD_KEY_45=prog2

```

Update hwdb after editing the rule.

```
# udevadm hwdb --update
# udevadm trigger --sysname-match="event*"

```

### HDR Display Color Calibration

For models with the 1440p HDR display, the default color profile can be corrected using an ICC calibration provided by [notebookcheck.net's review](https://www.notebookcheck.net/Lenovo-ThinkPad-X1-Carbon-2018-WQHD-HDR-i7-Laptop-Review.284682.0.html).

```
 wget [https://www.notebookcheck.net/uploads/tx_nbc2/B140QAN02_0.icm](https://www.notebookcheck.net/uploads/tx_nbc2/B140QAN02_0.icm)
 colormgr import-profile B140QAN02_0.icm

```

This will import the ICC profile, and next you'll need to activate it for your display. Find your display's object path:

```
 colormgr get-devices | sed -rn 's/Object Path:\s*(.*eDP1.*)/\1/p'

```

And your new color profile object path:

```
 colormgr get-profiles | grep -4 -i B140QAN02

```

And finally activate the profile and set it as the default for this display:

```
 colormgr device-add-profile <device object id> <profile object id>
 colormgr device-make-profile-default <device object id> <profile object id>

```

You can verify the profile is active by running `colormgr get-devices`.

## TrackPoint and Touchpad issues

**Note:** Some models of the 6th generation X1 Carbon seem to have issues with the TrackPoint and Touchpad working at the same time.

To get the TrackPoint and Touchpad to work at the same time, add `synaptics_intertouch=1` to the `psmouse` [kernel module](/index.php/Kernel_module "Kernel module") options, for example in the cmdline of the [boot loader](/index.php/Boot_loader "Boot loader"):

```
 [...] root=/dev/sda1 rw psmouse.synaptics_intertouch=1 [...]

```

or by editing `/etc/modprobe.d/psmouse.conf`:

```
 options psmouse synaptics_intertouch=1

```

**Note:** When using [TLP](/index.php/TLP "TLP") with default powersaving settings, there might be occasional hiccups such as dropouts of tap-to-click functionality for the Touchpad, as well as the TrackPoint not surviving suspends and needing to be re-initialized.

Reconnecting a dead trackpad can be done via

```
echo -n "none" | sudo tee /sys/bus/serio/devices/serio1/drvctl
echo -n "reconnect" | sudo tee /sys/bus/serio/devices/serio1/drvctl
```

A [bug](https://gitlab.freedesktop.org/libinput/libinput/issues/46) in the libinput library that caused dropouts of the tap-to-click functionality of the touchpad on the X1 Carbon 6th Gen has been fixed in libinput 1.11.2, which was released on [3 July 2018](https://lists.freedesktop.org/archives/wayland-devel/2018-July/038782.html).

## Full-disk encryption

### Ramdisk module

With LUKS for root, i915 needs to be loaded in ramdisk in order to access the password prompt. Add i915 to MODULES list in `/etc/mkinitcpio.conf` and regenerate the ramdisk.

## Tools

### Diagnostics

`s-tui` ([s-tui](https://aur.archlinux.org/packages/s-tui/)): an aesthetically pleasing and useful curses-style interface that shows graphs of CPU frequency, utilization, temperature, and power consumption. It also has a built in stress tester.

`intel_gpu_top` ([intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools)): gives you some top-like info for the integrated GPU. This can be quite useful in diagnosing GPU acceleration issues.

`powertop` ([powertop](https://www.archlinux.org/packages/?name=powertop)): provides detailed information about CPU power consumption and recommendations on how to improve it.

`tlp-stat` ([tlp](https://www.archlinux.org/packages/?name=tlp)): a much simpler alternative to remembering which `cat /sys/devices/system/*` to run in many cases. It can give very detailed, structured information about components like the battery, processor, graphics card, etc.

## References

*   [T480s throttling bug](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/), affects X1C6 as well
*   [Lenovo forums: T480s low cTDP and trip temperature in Linux](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489)
*   [Thread: TrackPoint/Touchpad issues, 20KG model](https://bbs.archlinux.org/viewtopic.php?id=236367)
*   [StackExchange: Success with enabling RMI4 config flags for Touchpad and TrackPoint](https://unix.stackexchange.com/a/431820)
*   [Kernel patch - Input: elantech - add support for SMBus devices](https://patchwork.kernel.org/patch/10324633/)
*   [Kernel patch - Input: synaptics - add Lenovo 80 series ids to SMBus](https://patchwork.kernel.org/patch/10330857/)
*   [Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"): Adding i915 to ramdisk

## Additional resources

*   [ThinkWiki X1 Carbon 6th Gen page](https://www.thinkwiki.org/wiki/Category:X1_Carbon_(6th_Gen))
*   Benjamin Tissoires, kernel maintainer of peripherals, has explained how input bugs get fixed in his talk [Tools to debug a broken input device](https://www.youtube.com/watch?v=Bl_0xYxcYd8) ([Slides](https://www.x.org/wiki/Events/XDC2015/Program/tissoires_input_debug_tools.html)), especially interesting are slides 16 onward.
*   [Dell XPS 13 9370 quirks](https://gist.github.com/greigdp/bb70fbc331a0aaf447c2d38eacb85b8f): Some pointers on getting Watt usage down to ~2W, Intel video powersaving features might be interesting, see also the [Intel Graphics](/index.php/Intel_Graphics "Intel Graphics") page for interesting power-saving options.
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)"): Shares some hardware with the X1C6
*   [Intel Blog: Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues), including the [pm-graph](https://github.com/01org/pm-graph) tool to analyze power usage during suspend
*   [A comprehensive example Arch install for the X1C6](https://github.com/ejmg/an-idiots-guide-to-installing-arch-on-a-lenovo-carbon-x1-gen-6)