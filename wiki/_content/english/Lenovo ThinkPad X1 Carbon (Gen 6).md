Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Carbon (Gen 7)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_7) "Lenovo ThinkPad X1 Carbon (Gen 7)")
*   [Lenovo ThinkPad X1 Yoga (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Yoga_(Gen_3) "Lenovo ThinkPad X1 Yoga (Gen 3)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

The Lenovo ThinkPad X1 Carbon, 6th generation is an ultrabook introduced in early 2018\. It comes in several variants(`20KH*` and `20KG*`) and features a 14" screen, 8th-gen Intel Core processors and integrated [Intel UHD 620 graphics](/index.php/Intel_graphics "Intel graphics").

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# sudo dmidecode -s system-version
ThinkPad X1 Carbon 6th

```

| **Device** | **Working** | **Modules** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes | i915, (intel_agp) |
| [Wireless network](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes | iwlmvm |
| Native Ethernet with [included dongle](https://www3.lenovo.com/us/en/accessories-and-monitors/cables-and-adapters/adapters/CABLE-BO-TP-OneLink%2B-to-RJ45-Adapter/p/4X90K06975) | Yes | ? |
| Mobile broadband Fibocom L850-GL | Yes¹ | cdc_mbim after MBIM-switch (from PCIe) |
| Mobile broadband Sierra EM7455 | Yes | cdc_mbim, cdc_wcm, cdc_ncm |
| Audio | Yes | snd_hda_intel |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes | psmouse, rmi_smbus, i2c_i801 |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes | psmouse, rmi_smbus, i2c_i801 |
| Camera | Yes | uvcvideo |
| Fingerprint Reader | No² | ? |
| [Power management](/index.php/Power_management "Power management") | Yes³ | ? |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes⁴ | btusb |
| NFC | No⁶ | ? |
| microSD card reader | Yes | scsi_mod |
| Keyboard Backlight | Yes | thinkpad_acpi |
| Function/Multimedia Keys | Yes | ? |
| Thunderbolt 3 eGPU | Yes⁵ | nvidia |
| 

1.  ~~No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.~~ [MBIM-Switch](https://github.com/abrasive/xmm7360)
    [kernel-module](https://github.com/juhovh/xmm7360_usb)
    [Discussion](https://forums.lenovo.com/t5/Other-Linux-Discussions/WWAN-Fibocom-L850-GL-and-Linux-support/td-p/4318903)
2.  [The Validity90 project](https://github.com/nmikhailov/Validity90) began reverse engineering the reader, but scanning does not yet work (06cb:009a).
3.  S3 suspend requires changes to BIOS settings - see section on [suspend issues](#Suspend_issues).
4.  See [this blog post](https://200ok.ch/posts/2018-12-17_making_bluetooth_work_on_lenovo_x1_carbon_6th_gen_with_linux.html) for improvements to reliability.
5.  Internal monitor acceleration does not appear to be supported.
6.  Connected via I2C, support was discussed in the [libnfc project](https://github.com/nfc-tools/libnfc/issues/455).

 |

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 BIOS](#BIOS)
    *   [1.1 Updates](#Updates)
        *   [1.1.1 Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service))
        *   [1.1.2 Manual (fwupdmgr)](#Manual_(fwupdmgr))
        *   [1.1.3 Manual (El Torito)](#Manual_(El_Torito))
*   [2 Suspend issues](#Suspend_issues)
    *   [2.1 Enabling S3](#Enabling_S3)
    *   [2.2 Verifying S3](#Verifying_S3)
    *   [2.3 Disabling the memory card reader](#Disabling_the_memory_card_reader)
    *   [2.4 BIOS configurations](#BIOS_configurations)
    *   [2.5 Failed to start Suspend](#Failed_to_start_Suspend)
*   [3 Power management/Throttling issues](#Power_management/Throttling_issues)
    *   [3.1 Throttling fix](#Throttling_fix)
*   [4 Audio crackling](#Audio_crackling)
*   [5 Built-in speakers low volume workaround](#Built-in_speakers_low_volume_workaround)
*   [6 Wireless WAN / LTE](#Wireless_WAN_/_LTE)
    *   [6.1 WWAN/LTE GUI](#WWAN/LTE_GUI)
*   [7 Configuration](#Configuration)
    *   [7.1 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)
    *   [7.2 Special buttons](#Special_buttons)
    *   [7.3 Disabling red LED in Thinkpad logo](#Disabling_red_LED_in_Thinkpad_logo)
    *   [7.4 HDR Display Color Calibration](#HDR_Display_Color_Calibration)
*   [8 Intel Graphics UHD 620 issues](#Intel_Graphics_UHD_620_issues)
    *   [8.1 GNOME Wayland not available](#GNOME_Wayland_not_available)
*   [9 TrackPoint and Touchpad issues](#TrackPoint_and_Touchpad_issues)
*   [10 Thunderbolt dock](#Thunderbolt_dock)
    *   [10.1 Plugable USB-C Mini Docking Station with 85W Power Delivery UD-CAM](#Plugable_USB-C_Mini_Docking_Station_with_85W_Power_Delivery_UD-CAM)
        *   [10.1.1 Bios settings](#Bios_settings)
        *   [10.1.2 TLP blacklisting devices from USB autosuspend](#TLP_blacklisting_devices_from_USB_autosuspend)
    *   [10.2 Lenovo dock](#Lenovo_dock)
*   [11 Full-disk encryption](#Full-disk_encryption)
    *   [11.1 LUKS: Ramdisk module](#LUKS:_Ramdisk_module)
    *   [11.2 OPAL: Hardware based full-disk encryption](#OPAL:_Hardware_based_full-disk_encryption)
*   [12 Tools](#Tools)
    *   [12.1 Diagnostics](#Diagnostics)
*   [13 nvme issues](#nvme_issues)
*   [14 References](#References)
*   [15 Additional resources](#Additional_resources)

## BIOS

The most convenient way to install Arch Linux is by disabling "Secure Boot" `Security -> Secure Boot - Set to "Disabled"`. However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

**Note:** In the BIOS setup menu under `Security -> UEFI BIOS Update Option`, both `Flash BIOS Updating by End-Users` and `Windows UEFI Firmware Update` [must be enabled](https://github.com/fwupd/fwupd/issues/856#issuecomment-440967709) at the time of an update.

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service(LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual (fwupdmgr)

Lenovo provides a cabinet file that can be directly installed with fwupdmgr. Take the most recent `.cab` file from the [Lenovo ThinkPad X1 Carbon (Gen 6) driver website](https://pcsupport.lenovo.com/fr/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-6th-gen-type-20kh-20kg/downloads).

1.  Make sure the AC adapter is firmly connected to the target computer.
2.  Launch Terminal.
3.  Move to the directory where the cabinet file was placed.
4.  Run `fwupdmgr install xxxxxxxx.cab` to schedule firmware update.
5.  Restart the system.
6.  The computer will be restarted and the UEFI BIOS will be updated.

#### Manual (El Torito)

Download the [latest BIOS update ISO](https://pcsupport.lenovo.com/fr/en/products/LAPTOPS-AND-NETBOOKS/THINKPAD-X-SERIES-LAPTOPS/THINKPAD-X1-CARBON-6TH-GEN-TYPE-20KH-20KG/downloads/DS502281). Obtain [geteltorito](https://aur.archlinux.org/packages/geteltorito/) and run `geteltorito.pl -o bios-update.img n23ur12w.iso` on the downloaded ISO file to create a valid [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard) image file, then flash this file on a USB drive via `dd` like you would flash [Arch installation media](/index.php/USB_flash_installation_media "USB flash installation media"). For further information see [flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux").

The ThinkPad X1 Carbon supports setting a custom splash image at the earliest boot stage (instead of the red "Lenovo" logo), more information can be found in the `README.TXT` located in the `FLASH` folder of the update image. This only needs to be done once, as subsequent UEFI upgrades will ask whether you wish to keep your custom logo.

Once the USB drive is flashed, the logo file can be placed in to the root directory of the flash drive.

## Suspend issues

Since BIOS version 1.30, the X1 Carbon supports S3 mode when enabled in the BIOS menu (choose "Linux" sleep mode instead of the default "Windows 10"). See [#Automatic (Linux Vendor Firmware Service)](#Automatic_(Linux_Vendor_Firmware_Service)) for instructions to update and verify your BIOS version.

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

### Failed to start Suspend

**Symptom:** The machine starts entering suspend but comes back online immediately when phone charges through USB-C.

*Note:* just a plain USB-C cable - without attached external device - can cause that too.

```
# journalctl -p err -u systemd-suspend
Failed to suspend system. System resumed again: Device or resource busy

```

```
$ dmesg -Tl err
[Mon Nov 11 20:18:03 2019] PM: pci_pm_suspend(): hcd_pci_suspend+0x0/0x30 returns -16
[Mon Nov 11 20:18:03 2019] PM: dpm_run_callback(): pci_pm_suspend+0x0/0x130 returns -16
[Mon Nov 11 20:18:03 2019] PM: Device 0000:00:14.0 failed to suspend async: error -16
[Mon Nov 11 20:18:04 2019] PM: Some devices failed to suspend, or early wake event detected 

```

**Solution:** Block USB devices from waking up the computer.

Check that `grep XHC /proc/acpi/wakeup` shows `enabled`. If yes, disable XHC wakeup by `echo XHC` . Now, test your computer. If your problem is solved then you have to persist the change as it would get lost on reboot.

**Persistent Solution**

There is no way to persist the config through a configuration file. So create the following systemd unit file and enable the service.

```
[Unit]
Description=Fixes failing suspend by disabling wakeup thourgh USB

[Service]
ExecStart=/bin/bash -c 'grep --silent '^XHC.*disabled' /proc/acpi/wakeup || echo XHC > /proc/acpi/wakeup'
Type=oneshot
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

## Power management/Throttling issues

Due to wrong configured power management registers the CPU may consume a lot less power than under windows and the thermal throttling occurs at 80°C (97°C when using Windows, see [T480s throttling bug](https://www.reddit.com/r/thinkpad/comments/870u0a/t480s_linux_throttling_bug/)).

There is a [post in the official Lenovo forum](https://forums.lenovo.com/t5/Linux-Discussion/T480s-low-cTDP-and-trip-temperature-in-Linux/td-p/4028489) to inform Lenovo about this issue, and a Lenovo employee has [confirmed that they're actively working on a fix](https://forums.lenovo.com/t5/Other-Linux-Discussions/X1C6-T480s-low-cTDP-and-trip-temperature-in-Linux/m-p/4513821/highlight/true#M13563) but also said that it may take some time.

### Throttling fix

An easy package has been written to address the problem until Lenovo completes the [OS agnostic fix](https://www.notebookcheck.net/Lenovo-admits-ThinkPad-CPU-throttling-problem-when-running-Linux-fix-in-development.435549.0.html) for the X1C6.

Install [throttled](https://www.archlinux.org/packages/?name=throttled), then run:

```
sudo systemctl enable --now lenovo_fix.service

```

The script also supports more advance thermal/performance features including CPU undervolting. See the [repository](https://github.com/erpalma/throttled) `README.md` for details.

**Note:** If you installed [thermald](https://aur.archlinux.org/packages/thermald/), it may conflict with the throttling fix in this package. Consider disabling thermald or otherwise work around this.

## Audio crackling

When charging you may hear crackling noise while listening to audio. [The work around](https://www.reddit.com/r/thinkpad/comments/8j8208/audio_crackling_through_both_headphone_jack_and/) for this issue is to disable one of the PINs:

```
sudo hda-verb /dev/snd/hwC0D0 0x1d SET_PIN_WIDGET_CONTROL 0x0

```

There is also a kernel patch for this issue, which can be found [here](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1805079).

## Built-in speakers low volume workaround

If your ThinkPad X1 Carbon (Gen 6) built-in speakers are limited to a maximum of about 20% volume even though the volume is set at 100%, try adding the following parameter to the `snd_hda_intel` module, which can be set through a file in `/etc/modprobe.d/`, e.g.:

 `/etc/modprobe.d/alsa-base.conf`  `options snd-hda-intel model=nofixup` 
**Note:** This stops the LEDs on the mute and mic-mute buttons from working.

## Wireless WAN / LTE

ThinkPad X1 Carbon (Gen 6) is exclusively shipped with a Fibocom L850-GL LTE modem, which is currently not supported out of the box under Linux.

It is normally impossible to swap the LTE modem for a supported one due to BIOS-level restrictions ("whitelists" of allowed M.2 expansion cards) implemented in all modern Lenovo laptops. However, a method has been found to configure any Sierra Wireless EM73xx/EM74xx modem to "evade" the whitelist checks, so these modems can be used normally.

Take a look at [ThinkPad mobile internet: Getting around BIOS-level whitelist restrictions](/index.php/ThinkPad_mobile_Internet#Getting_around_BIOS-level_whitelist_restrictions "ThinkPad mobile Internet") for instructions.

See also the work done in [github: Tools for the Fibocom L850-GL / Intel XMM7360 LTE modem](https://github.com/abrasive/xmm7360), [github: Kernel module for Fibocom L850-GL / Intel XMM7360 LTE modem](https://github.com/juhovh/xmm7360_usb) and [Lenovo Forums: WWAN Fibocom L850-GL and Linux support](https://forums.lenovo.com/t5/Other-Linux-Discussions/WWAN-Fibocom-L850-GL-and-Linux-support/td-p/4318903).

### WWAN/LTE GUI

Install [NetworkManager](/index.php/NetworkManager "NetworkManager") and [network-manager-applet](https://www.archlinux.org/packages/?name=network-manager-applet) to make your life easier founding the correct APN for your SIM card.

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

You can remap unsupported keys so that they can be detected and mapped in X using [udev hwdb](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes"):

Note that `prog1` and `prog2` map to `KEY_PROG1` and `KEY_PROG2` in `/usr/include/linux/input-event-codes.h`. You can use any key code with a defined value less than 255\. The keycode hwdb expects is the lowercased text following `KEY_` in the above input event codes header file. eg: `KEY_COFFEE` would be `coffee`.

 `/etc/udev/hwdb.d/90-thinkpad-keyboard.hwdb` 
```
evdev:name:ThinkPad Extra Buttons:dmi:bvn*:bvr*:bd*:svnLENOVO*:pn*
 KEYBOARD_KEY_49=prog1
 KEYBOARD_KEY_45=prog2

```

To make the changes take effect:

```
# udevadm hwdb --update
# udevadm trigger --sysname-match="event*"

```

### Disabling red LED in Thinkpad logo

To disable the red LED in the ThinkPad logo on the cover:

1\. Enable writing to the embedded controller registers by adding the kernel parameter `ec_sys.write_support=1`. If you use UEFI boot, you can add this parameter in `/boot/efi/loader/entries/arch.conf` under "options".

2\. Then, you can disable directly the LED with this command:

```
# echo -n -e "\x0a" | sudo dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

**To disable the LED at startup, you can create a systemd service:**

1\. Create a sh script (/root/disable_led.sh for instance) and put this :

```
#!/bin/bash
echo -n -e "\x0a" | dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

2\. Create a new service unit file in {{ic|/etc/systemd/system} called "led.service", and insert the following:

```
Description=Disabling thinkpad led

[Service]
ExecStart=/root/disable_led.sh

[Install]
WantedBy=multi-user.target

```

3\. Start and enable this service:

```
# systemctl start led.service
# systemctl enable led.service

```

### HDR Display Color Calibration

For models with the 1440p HDR display, the default color profile can be corrected under Gnome using an ICC calibration provided by [notebookcheck.net's review](https://www.notebookcheck.net/Lenovo-ThinkPad-X1-Carbon-2018-WQHD-HDR-i7-Laptop-Review.284682.0.html).

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

## Intel Graphics UHD 620 issues

*   [Enable GuC/HuC firmware loading](/index.php/Intel_graphics#Enable_GuC_/_HuC_firmware_loading "Intel graphics") suggests to load GPU firmware with warning. However, on Wayland for Carbon X1 gen 6 it cause GPU hang problem. Issues can be reflected as: a) crashing GPU process of Chrome / Chromium / Electron apps and subsequent host freezing; b) crashing of Gnome / Wayland with possibility to reboot via second virtual terminal; c) just host freezing. In dmesg the following can be observed:

```
 kernel: [drm] GPU HANG: ecode 9:0:0x85dffffd, in chrome [18418], reason: hang on rcs0, action: reset
 kernel: [drm] GPU hangs can indicate a bug anywhere in the entire gfx stack, including userspace.
 kernel: [drm] Please file a _new_ bug report on bugs.freedesktop.org against DRI -> DRM/Intel
 kernel: [drm] drm/i915 developers can then reassign to the right component if it's not a kernel issue.
 kernel: [drm] The gpu crash dump is required to analyze gpu hangs, so please always attach it.
 kernel: [drm] GPU crash dump saved to /sys/class/drm/card0/error
 kernel: i915 0000:00:02.0: Resetting rcs0 for hang on rcs0

```

Note that, first line changes depending on the source of crashing application, but the result is the same, so issue is with GPU / firmware. Basically don't enable GuC / HuC firmware loading, at least if on Wayland. There are a number of similar issues reported including [#108717](https://bugs.freedesktop.org/show_bug.cgi?id=108717).

*   The `modesetting` driver causes [tearing](/index.php/Intel_graphics#Tearing "Intel graphics") in some situations. You can install the `xf86-video-intel` driver instead and enable the `"TearFree"` option in your configuration file:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
  Identifier  "Intel Graphics"
  Driver      "intel"
  Option      "TearFree" "true"
EndSection
```

#### GNOME Wayland not available

If you haven't added the i915 to the MODULES list in /etc/mkinitcpio.conf (e.g. following the full disk encryption requirements below), you may be unable to run Wayland on kernel 4.20 (the gnome on Wayland option might not be present on GDM). Adding i915 to the MODULES list in /etc/mkinitcpio.conf and regenerating the ramdisk solves this issue.

## TrackPoint and Touchpad issues

**Note:** Some models of the 6th generation X1 Carbon seem to have issues with the TrackPoint and Touchpad working at the same time.

**Note:** The following parameter will only work for kernel versions *after* v4.14\. Fore more information, see [Lenovo ThinkPad X1 Carbon (Gen 5)#Trackpoint/Trackpad not working](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5)#Trackpoint/Trackpad_not_working "Lenovo ThinkPad X1 Carbon (Gen 5)").

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

## Thunderbolt dock

### Plugable USB-C Mini Docking Station with 85W Power Delivery UD-CAM

If you are using an external plugable [UD-CAM](https://plugable.com/products/ud-cam/) thunderbolt dock connected to the laptop through its USB-C thunderbolt port, you might experience random disconnections (external monitor, bluetooth and ethernet) with this kind of error in dmesg :

 `pcieport 0000:05:00.0: BAR 13: no space for [io  size 0x3000]` 

It should be noted that [bolt](https://www.archlinux.org/packages/?name=bolt) is not working with this [UD-CAM](https://plugable.com/products/ud-cam/) dock.

To avoid random disconnection, proceed as followed by editing the bios and [TLP](/index.php/TLP "TLP")

#### Bios settings

You should then look at your bios settings :

*   Wake by thunderbolt : enable
*   Security level : no security
*   Pre-boot ACL option : enable

#### TLP blacklisting devices from USB autosuspend

If you are using [TLP](/index.php/TLP "TLP") you have to edit /etc/default/tlp and make sure that you exclude all dock devices from USB autosuspend as followed :

 `USB_BLACKLIST="0000:1111 2222:3333 4444:5555"` 

Then reboot and your dock should work correctly.

### Lenovo dock

## Full-disk encryption

### LUKS: Ramdisk module

With LUKS for root, i915 needs to be loaded in ramdisk in order to access the password prompt. Add i915 to MODULES list in `/etc/mkinitcpio.conf` and regenerate the ramdisk.

### OPAL: Hardware based full-disk encryption

See [Self-Encrypting Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives") (Confirmed working)

## Tools

### Diagnostics

`s-tui` ([s-tui](https://www.archlinux.org/packages/?name=s-tui)): an aesthetically pleasing and useful curses-style interface that shows graphs of CPU frequency, utilization, temperature, and power consumption. It also has a built in stress tester.

`intel_gpu_top` ([intel-gpu-tools](https://www.archlinux.org/packages/?name=intel-gpu-tools)): gives you some top-like info for the integrated GPU. This can be quite useful in diagnosing GPU acceleration issues.

`powertop` ([powertop](https://www.archlinux.org/packages/?name=powertop)): provides detailed information about CPU power consumption and recommendations on how to improve it.

`tlp-stat` ([tlp](https://www.archlinux.org/packages/?name=tlp)): a much simpler alternative to remembering which `cat /sys/devices/system/*` to run in many cases. It can give very detailed, structured information about components like the battery, processor, graphics card, etc.

## nvme issues

There is an [issue](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-6th-gen-type-20kh-20kg/solutions/HT508405) with nvme installed in ThinkPad X1 Carbon (Gen 6) resulting in device failure. Be sure to update firmware or reach out to lenovo support for replacement.

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
*   [Dell XPS 13 9370 quirks](https://gist.github.com/greigdp/bb70fbc331a0aaf447c2d38eacb85b8f): Some pointers on getting Watt usage down to ~2W, Intel video powersaving features might be interesting, see also the [Intel graphics](/index.php/Intel_graphics "Intel graphics") page for interesting power-saving options.
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)"): Shares some hardware with the X1C6
*   [Intel Blog: Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues), including the [pm-graph](https://github.com/01org/pm-graph) tool to analyze power usage during suspend
*   [A comprehensive example Arch install for the X1C6](https://github.com/ejmg/an-idiots-guide-to-installing-arch-on-a-lenovo-carbon-x1-gen-6)