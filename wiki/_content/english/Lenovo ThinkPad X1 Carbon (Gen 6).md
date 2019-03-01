Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 5)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5) "Lenovo ThinkPad X1 Carbon (Gen 5)")
*   [Lenovo ThinkPad X1 Yoga (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Yoga_(Gen_3) "Lenovo ThinkPad X1 Yoga (Gen 3)")

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
| Mobile broadband Fibocom | No¹ | ? |
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

1.  No working Linux driver for Fibocom L850-GL. See [this thread](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4078413) and [this thread](https://forums.lenovo.com/t5/Linux-Discussion/Linux-support-for-WWAN-LTE-L850-GL-on-T580-T480/td-p/4067969) for more info.
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
        *   [1.1.2 Manual](#Manual)
*   [2 Suspend issues](#Suspend_issues)
    *   [2.1 Enabling S3](#Enabling_S3)
    *   [2.2 Verifying S3](#Verifying_S3)
    *   [2.3 Disabling the memory card reader](#Disabling_the_memory_card_reader)
    *   [2.4 BIOS configurations](#BIOS_configurations)
*   [3 Power management/Throttling issues](#Power_management/Throttling_issues)
    *   [3.1 Throttling fix](#Throttling_fix)
*   [4 Audio crackling](#Audio_crackling)
*   [5 Wireless WAN / LTE](#Wireless_WAN_/_LTE)
    *   [5.1 Settings for Sierra Wireless EM7455](#Settings_for_Sierra_Wireless_EM7455)
        *   [5.1.1 General description](#General_description)
        *   [5.1.2 Step-by-step](#Step-by-step)
        *   [5.1.3 Remarks](#Remarks)
    *   [5.2 WWAN/LTE GUI](#WWAN/LTE_GUI)
*   [6 Configuration](#Configuration)
    *   [6.1 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)
    *   [6.2 Special buttons](#Special_buttons)
    *   [6.3 Bind special keys](#Bind_special_keys)
    *   [6.4 Disabling red LED Thinkpad logo](#Disabling_red_LED_Thinkpad_logo)
    *   [6.5 HDR Display Color Calibration](#HDR_Display_Color_Calibration)
*   [7 Intel Graphics UHD 620 issues](#Intel_Graphics_UHD_620_issues)
    *   [7.1 GNOME Wayland not available](#GNOME_Wayland_not_available)
*   [8 TrackPoint and Touchpad issues](#TrackPoint_and_Touchpad_issues)
*   [9 Thunderbolt dock](#Thunderbolt_dock)
    *   [9.1 Plugable USB-C Mini Docking Station with 85W Power Delivery UD-CAM](#Plugable_USB-C_Mini_Docking_Station_with_85W_Power_Delivery_UD-CAM)
        *   [9.1.1 Bios settings](#Bios_settings)
        *   [9.1.2 TLP blacklisting devices from USB autosuspend](#TLP_blacklisting_devices_from_USB_autosuspend)
    *   [9.2 Lenovo dock](#Lenovo_dock)
*   [10 Full-disk encryption](#Full-disk_encryption)
    *   [10.1 LUKS: Ramdisk module](#LUKS:_Ramdisk_module)
    *   [10.2 OPAL: Hardware based full-disk encryption](#OPAL:_Hardware_based_full-disk_encryption)
*   [11 Tools](#Tools)
    *   [11.1 Diagnostics](#Diagnostics)
*   [12 References](#References)
*   [13 Additional resources](#Additional_resources)

## BIOS

The most convenient way to install Arch Linux is by disabling "Secure Boot" `Security -> Secure Boot - Set to "Disabled"`. However it is possible to self-sign your kernel and boot with it enabled. For further information have a look at the [Secure Boot](/index.php/Secure_Boot "Secure Boot") article.

In case your `efivars` are not properly set it is most likely due to you not being booted into [UEFI](/index.php/UEFI "UEFI"). Should the problem persist be sure to consult the [UEFI#UEFI variables](/index.php/UEFI#UEFI_variables "UEFI") section.

### Updates

#### Automatic (Linux Vendor Firmware Service)

[In August of 2018 Lenovo has joined](https://blogs.gnome.org/hughsie/2018/08/06/please-welcome-lenovo-to-the-lvfs/) the [Linux Vendor Firmware Service(LVFS)](https://fwupd.org/) project, which enables firmware updates from within the OS. BIOS updates (and possibly other firmware such as the Thunderbolt controller) can be queried for and installed through [fwupd](/index.php/Fwupd "Fwupd").

#### Manual

[BIOS update 1.34](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-x-series-laptops/thinkpad-x1-carbon-6th-gen-type-20kh-20kg/downloads) was released on 2018-11-23 (previous version was 1.31). Obtain [geteltorito](https://aur.archlinux.org/packages/geteltorito/) and run `geteltorito.pl -o bios-update.img n23ur12w.iso` on the downloaded ISO file to create a valid [El Torito](https://en.wikipedia.org/wiki/El_Torito_(CD-ROM_standard) image file, then flash this file on a USB drive via `dd` like you would flash [Arch installation media](/index.php/USB_flash_installation_media "USB flash installation media"). For further information see [flashing BIOS from Linux](/index.php/Flashing_BIOS_from_Linux#Bootable_optical_disk_emulation "Flashing BIOS from Linux").

The ThinkPad X1 Carbon supports setting a custom splash image at the earliest boot stage (instead of the red "Lenovo" logo), more information can be found in the `README.TXT` located in the `FLASH` folder of the update image.

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

## Audio crackling

When charging you may hear crackling noise while listening to audio. [The work around](https://www.reddit.com/r/thinkpad/comments/8j8208/audio_crackling_through_both_headphone_jack_and/) for this issue is to disable one of the PINs:

```
sudo hda-verb /dev/snd/hwC0D0 0x1d SET_PIN_WIDGET_CONTROL 0x0

```

There is also a kernel patch for this issue, which can be found [here](https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1805079).

## Wireless WAN / LTE

ThinkPad X1 Carbon (Gen 6) is exclusively shipped with a Fibocom L850-GL LTE modem, which is not supported under Linux and Lenovo doesn't seem to care about it.

It is normally impossible to swap the LTE modem for a supported one due to BIOS-level restrictions ("whitelists" of allowed M.2 expansion cards) implemented in all modern Lenovo laptops. However, a method has been found to configure any Sierra Wireless EM73xx/EM74xx modem to "evade" the whitelist checks, so these modems can be used normally.

### Settings for Sierra Wireless EM7455

#### General description

Use `AT!CUSTOM="FASTENUMEN",0` AT command to disable the modem's *USB fast enumeration* feature. The modem will take a significantly longer time to appear on the USB bus and the firmware will "miss" the modem at boot time.

Alternatively, use `AT!CUSTOM="FASTENUMEN",2` to selectively enable *USB fast enumeration* for warm boots only. The modem will reappear faster on S3 resume but still evade the whitelist checks on regular boots *and* reboots (the mechanism of this effect is not fully clear to the author).

This comes with a downside: because the firmware does not "see" the modem, it will not export the WWAN rfkill but instead it will unconditionally assert the `W_DISABLE` pin of the M.2 slot, forcing the modem into "airplane mode". Use `AT!PCOFFEN=2` AT command to configure the modem to ignore this pin.

#### Step-by-step

1\. Boot the laptop with the stock modem in place and WWAN card access enabled in BIOS setup.

2\. Suspend the laptop (make sure it is configured to use S3).

3\. Hot-swap the stock Fibocom modem with the Sierra Wireless one, then resume. Whitelists are not consulted at S3 resume.

Check that the modem is present on the USB bus:

```
# lsusb
<...>
Bus 001 Device 004: ID 1199:9071 Sierra Wireless, Inc.
<...>

```

Remember the VID (vendor ID) of the modem (`1199` in this example).

4\. Stop ModemManager, if it is running:

```
 # systemctl stop ModemManager

```

5\. Optionally, update the modem firmware with the `qmi-firmware-update` tool:

```
# cd /path/to/extracted/firmware
# qmi-firmware-update -d 1199 -u *.cwe *.nvu

```

6\. Change the modem's USB composition to enable AT command ports:

```
# qmicli -d /dev/cdc-wdm1 --dms-swi-set-usb-composition=8

```

7\. Power-cycle the modem as advised by `qmicli`:

```
# qmicli -d /dev/cdc-wdm1 --dms-set-operating-mode=offline
# qmicli -d /dev/cdc-wdm1 --dms-set-operating-mode=reset

```

8\. Wait for the modem to reappear, then verify:

```
# qmicli -d /dev/cdc-wdm1 --dms-swi-get-usb-composition
[/dev/cdc-wdm1] Successfully retrieved USB compositions:
            USB composition 6: DM, NMEA, AT, QMI
        [*] USB composition 8: DM, NMEA, AT, MBIM
            USB composition 9: MBIM

```

9\. Verify that the three serial ports `/dev/ttyUSB0`, `/dev/ttyUSB1` and `/dev/ttyUSB2` are now available (assuming you do not have any other USB-serial converters plugged in):

```
# ls -l /dev/ttyUSB*
crw-rw---- 1 root uucp 188, 0 Feb 14 20:11 /dev/ttyUSB0
crw-rw---- 1 root uucp 188, 1 Feb 14 20:11 /dev/ttyUSB1
crw-rw---- 1 root uucp 188, 2 Feb 14 20:11 /dev/ttyUSB2

```

10\. Attach to `/dev/ttyUSB2` with a serial terminal emulator of your choice (e. g. `screen`):

```
# screen /dev/ttyUSB2 115200

```

11\. Enter the AT commands (note that you do not need to type `OK`, the replies are included here as part of a session transcript):

11.1\. Enable command echo (if echo is initially disabled, you won't see this command as you type it):

```
ATE1
OK

```

11.2\. Unlock engineering commands:

```
AT!ENTERCND="A710"
OK

```

11.3\. Check customization options (these are the author's options):

```
AT!CUSTOM?
!CUSTOM: 
             GPSENABLE          0x01
             GPSSEL             0x01
             IPV6ENABLE         0x01
             SIMLPM             0x01
             SINGLEAPNSWITCH    0x01

OK

```

11.4\. Configure *USB fast enumeration* (swap `2` for `0` if you want to play it safe):

```
AT!CUSTOM="FASTENUMEN",2
OK

```

11.5\. Verify:

```
AT!CUSTOM?
!CUSTOM: 
             GPSENABLE          0x01
             GPSSEL             0x01
             IPV6ENABLE         0x01
             SIMLPM             0x01
             FASTENUMEN         0x02
             SINGLEAPNSWITCH    0x01

OK

```

*(it should now show the `FASTENUMEN` option alongside others)*

11.6\. Configure the modem to ignore W_DISABLE:

```
AT!PCOFFEN=2
OK

```

11.7\. Verify:

```
AT!PCOFFEN?
2

OK

```

11.8\. Reset the modem:

```
AT!RESET
OK

```

*(the terminal will disconnect after a while)*

12\. Wait for the modem to reappear, then verify configuration by rebooting / powering down / hard resetting the laptop.

#### Remarks

For more information (including the original thought process that led to this discovery), see these [lenovo](https://forums.lenovo.com/t5/Linux-Discussion/X1C-gen-6-Fibocom-L850-GL-Ubuntu-18-04/m-p/4307332/highlight/true#M12232) [threads](https://forums.lenovo.com/t5/Linux-Discussion/Getting-Sierra-EM7455-and-similar-to-work-on-X1C6/td-p/4326043) and this [reddit](https://www.reddit.com/r/thinkpad/comments/a3yd2j/sierra_wireless_em7455_seems_working_with_my/) thread.

You may also apply other useful configuration options described [here](https://github.com/danielewood/sierra-wireless-modems).

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

### Bind special keys

It should be noted that `Fn+F11` which is `KEY_KEYBOARD` and `Fn+F12` which is `KEY_FAVORITES` could be bound respectively with `XF86Launch1` and `XF86Launch2`, as followed :

```
# bindsym XF86Launch1 [your app]
# bindsym XF86Launch2 [your app]

```

### Disabling red LED Thinkpad logo

If you want to shut down Big Brother, (the red led on the "i" letter located on the cover of your x1c6 thinkpad logo) follow these steps :

*   Firstly, add the kernel parameter : **ec_sys.write_support=1** (if you are using UEFI boot as I do, you can add this parameter in /boot/efi/loader/entries/arch.conf in "options")
*   Then, you can disable directly the LED with this command :

```
# echo -n -e "\x0a" | sudo dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

You can also turn the LED off at startup with [Systemd](/index.php/Systemd "Systemd") :

*   Create a sh script (/root/disable_led.sh for instance) and put this :

```
#!/bin/bash
echo -n -e "\x0a" | dd of="/sys/kernel/debug/ec/ec0/io" bs=1 seek=12 count=1 conv=notrunc 2> /dev/null

```

*   Create a service under /etc/systemd/system/ called led.service, and insert the following:

```
Description=Disabling thinkpad led

[Service]
ExecStart=/root/disable_led.sh

[Install]
WantedBy=multi-user.target

```

*   Then start and enable this service

```
# systemctl start led.service
# systemctl enable led.service

```

Say goodbye to Big Brother !

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

**Note:** The following parameter will only work for kernel versions *after* v4.14\. Fore more information, see [Lenovo ThinkPad X1 Carbon (Gen 5)#Bug: Trackpoint/Trackpad not working](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_5)#Bug:_Trackpoint/Trackpad_not_working "Lenovo ThinkPad X1 Carbon (Gen 5)").

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

See [Self-Encrypting_Drives](/index.php/Self-Encrypting_Drives "Self-Encrypting Drives") (Confirmed working)

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
*   [Dell XPS 13 9370 quirks](https://gist.github.com/greigdp/bb70fbc331a0aaf447c2d38eacb85b8f): Some pointers on getting Watt usage down to ~2W, Intel video powersaving features might be interesting, see also the [Intel graphics](/index.php/Intel_graphics "Intel graphics") page for interesting power-saving options.
*   [Dell XPS 13 (9360)](/index.php/Dell_XPS_13_(9360) "Dell XPS 13 (9360)"): Shares some hardware with the X1C6
*   [Intel Blog: Best practice to debug Linux* suspend/hibernate issues](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues), including the [pm-graph](https://github.com/01org/pm-graph) tool to analyze power usage during suspend
*   [A comprehensive example Arch install for the X1C6](https://github.com/ejmg/an-idiots-guide-to-installing-arch-on-a-lenovo-carbon-x1-gen-6)