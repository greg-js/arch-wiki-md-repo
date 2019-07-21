Related articles

*   [Lenovo ThinkPad X1 Carbon](/index.php/Lenovo_ThinkPad_X1_Carbon "Lenovo ThinkPad X1 Carbon")
*   [Lenovo ThinkPad X1 Carbon (Gen 2)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_2) "Lenovo ThinkPad X1 Carbon (Gen 2)")
*   [Lenovo ThinkPad X1 Carbon (Gen 3)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_3) "Lenovo ThinkPad X1 Carbon (Gen 3)")
*   [Lenovo ThinkPad X1 Carbon (Gen 4)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_4) "Lenovo ThinkPad X1 Carbon (Gen 4)")
*   [Lenovo ThinkPad X1 Carbon (Gen 6)](/index.php/Lenovo_ThinkPad_X1_Carbon_(Gen_6) "Lenovo ThinkPad X1 Carbon (Gen 6)")

**Tip:** A great resource for thinkpads is [https://www.thinkwiki.org/wiki/ThinkWiki](https://www.thinkwiki.org/wiki/ThinkWiki)

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Model description](#Model_description)
    *   [1.1 Support](#Support)
    *   [1.2 Fingerprint Reader](#Fingerprint_Reader)
    *   [1.3 Bug: Fans blowing at max speed after resuming](#Bug:_Fans_blowing_at_max_speed_after_resuming)
    *   [1.4 Bug: Trackpoint/Trackpad not working](#Bug:_Trackpoint/Trackpad_not_working)
        *   [1.4.1 Solution 1](#Solution_1)
        *   [1.4.2 Solution 2](#Solution_2)
    *   [1.5 Bug: TrackPoint stops working after waking up from suspend](#Bug:_TrackPoint_stops_working_after_waking_up_from_suspend)
    *   [1.6 Bug: System occasionally hanging during startup](#Bug:_System_occasionally_hanging_during_startup)
*   [2 Configuration](#Configuration)
    *   [2.1 Keyboard Fn Shortcuts](#Keyboard_Fn_Shortcuts)
    *   [2.2 Special buttons](#Special_buttons)
    *   [2.3 Display](#Display)
    *   [2.4 Backlight Control](#Backlight_Control)
    *   [2.5 TrackPoint Scrolling](#TrackPoint_Scrolling)
    *   [2.6 Lenovo ThinkPad Thunderbolt 3 Dockingstation](#Lenovo_ThinkPad_Thunderbolt_3_Dockingstation)
    *   [2.7 HP Thunderbolt 3 Dock](#HP_Thunderbolt_3_Dock)
    *   [2.8 Lenovo p27h-10 (USB Type C)](#Lenovo_p27h-10_(USB_Type_C))

## Model description

Lenovo ThinkPad X1 Carbon, Gen 5.

To ensure you have this version, [install](/index.php/Install "Install") the package [dmidecode](https://www.archlinux.org/packages/?name=dmidecode) and run:

```
# dmidecode -t system | grep Version

Version: ThinkPad X1 Carbon 5th

```

### Support

| **Device** | **Working** |
| [Intel graphics](/index.php/Intel_graphics "Intel graphics") | Yes |
| [Wireless network configuration#iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration") | Yes |
| Native Ethernet with [Dongle](http://shop.lenovo.com/us/en/itemdetails/4X90F84315/460/D60A78A4A48A422E9761BD184AD3750A) | Yes |
| Mobile broadband | Yes |
| [ALSA](/index.php/ALSA "ALSA") | Yes |
| [Touchpad](/index.php/Touchpad "Touchpad") | Yes |
| [TrackPoint](/index.php/TrackPoint "TrackPoint") | Yes* |
| Camera | Yes |
| Fingerprint Reader | Yes |
| [Power management](/index.php/Power_management "Power management") | Yes |
| [Bluetooth](/index.php/Bluetooth "Bluetooth") | Yes |
| microSD card reader | Yes |

*   Lenovo uses several different trackpoint types in the 5th generation X1 Carbon. Only the standard ALPS variant has Linux support.

### Fingerprint Reader

The fingerprint reader included with this model is `138a:0097 Validity Sensors, Inc`. There's a patched libfprint which adds partial support for 138a:0097\. [libfprint-vfs0097-git](https://aur.archlinux.org/packages/libfprint-vfs0097-git/) It allows fingerprint authentication, but only if fingers are previously enrolled on the device from Windows. [libfrprint issue](https://gitlab.freedesktop.org/libfprint/libfprint/issues/54#note_1991)

### Bug: Fans blowing at max speed after resuming

There is a bug in the current kernel, causing the fans to often go on full throttle non-stop after resuming from suspend-to-ram.

**This bug is fixed since the kernel 4.12.4-1.**

Set of patches available for older version: [https://bugzilla.kernel.org/show_bug.cgi?id=196129#c26](https://bugzilla.kernel.org/show_bug.cgi?id=196129#c26)

If you have an older version of the kernel, you need to manually patch the kernel or work around the issue by repeatedly suspend (<kbd>Fn+4</kbd>) and resume (<kbd>Fn</kbd>) until it resumes without the fans starting with a short burst of activity. For me, the issue arises in about 2/3 resumes without the patches and never with kernel 4.12.0-2 with patches.

### Bug: Trackpoint/Trackpad not working

Several different trackpoints are used with the X1 Carbon Gen 5\. There are at least three different trackpoints in use. You can identify them in dmesg as either LEN0071, LEN0072 or LEN0073\.

There is a bug in Synaptics drivers that prevent both Trackpoint and Trackpad to function properly if Trackpoint is enabled at boot. This issue affects the Elantech trackpoint as well as one of the ALPS variants.

If you have the Elantech trackpoint, identified as LEN0073 you will see the following in your dmesg log.

```
kernel: psmouse serio1: TouchPad at isa0060/serio1/input0 lost sync at byte 1
kernel: psmouse serio1: TouchPad at isa0060/serio1/input0 lost sync at byte 1
kernel: psmouse serio1: TouchPad at isa0060/serio1/input0 lost sync at byte 1
kernel: psmouse serio1: TouchPad at isa0060/serio1/input0 lost sync at byte 1
kernel: psmouse serio1: TouchPad at isa0060/serio1/input0 lost sync at byte 1
kernel: psmouse serio1: issuing reconnect request

```

#### Solution 1

Since kernel v4.14 you can workaround this by adding `psmouse.synaptics_intertouch=1` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

#### Solution 2

If you uses a kernel older than 4.14, you can patch it using [https://gist.github.com/ursm/6d1007f44a1d6beeb670b3c3a6a78ea4](https://gist.github.com/ursm/6d1007f44a1d6beeb670b3c3a6a78ea4). Note that this only works on the Elantech trackpoint (LEN0073).

### Bug: TrackPoint stops working after waking up from suspend

A workaround is to manually insert the elan_i2c module after waking up from suspend:

```
# modprobe elan_i2c

```

See this [bugticket](https://bugzilla.redhat.com/show_bug.cgi?id=1560723) for details.

### Bug: System occasionally hanging during startup

Using the SDDM login manager, the system hangs on every second or third boot on startup before X starts. This is caused by a bug in version 0.16.0 of SDDM, reported here:

[https://github.com/sddm/sddm/issues/905](https://github.com/sddm/sddm/issues/905)

It can be solved by letting SDDM wait a little bit before starting. Just create the file **/etc/systemd/system/sddm.service.d/override.conf** with this content:

```
[Service]
ExecStartPre=/bin/sleep 2
```

**this bug is fixed as of sddm-0.16.0-3**

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

| Key combination | Scancode | Keycode |
| `Fn+F11` | `0x49` | `374` `KEY_KEYBOARD` |
| `Fn+F12` | `0x45` | `364` `KEY_FAVORITES` |

You can remap unsupported keys using [udev hwdb](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes"):

 `/etc/udev/hwdb.d/90-thinkpad-keyboard.hwdb` 
```
evdev:name:ThinkPad Extra Buttons:dmi:bvn*:bvr*:bd*:svnLENOVO*:pn*
 KEYBOARD_KEY_45=prog1
 KEYBOARD_KEY_49=prog2

```

Update hwdb after editing the rule.

```
# udevadm hwdb --update
# udevadm trigger --sysname-match="event*"

```

### Display

There are two options for displays:

*   14" FHD IPS (1920 x 1080): Works
*   14" WQHD (2560 x 1440): Works

### Backlight Control

I had issues with the thinkpad_acpi module in linux-4.12 and linux-4.13\. When loaded no acpi events are generated for Fn+F5 and Fn+F6 keypress by default, because

```
kernel: thinkpad_acpi: This ThinkPad has standard ACPI backlight brightness control, supported by the ACPI video driver
kernel: thinkpad_acpi: Disabling thinkpad-acpi brightness events by default...
kernel: thinkpad_acpi: Standard ACPI backlight interface available, not loading native one

```

Setting the acpi_brightness=vendor kernel parameter helped but gave issues with brightness save/restore. In linux-4.14 this issue is resolved.

### TrackPoint Scrolling

TrackPoint Scrolling is working out of the box in GNOME and MATE. In some WindowManagers, the TrackPoint middle-button scrolling can be enabled by [installing](/index.php/Install "Install") the [xorg-xinput](https://www.archlinux.org/packages/?name=xorg-xinput) package from the [official repositories](/index.php/Official_repositories "Official repositories") and appending the following line to your [.xinitrc](/index.php/.xinitrc ".xinitrc"):

 `xinput set-prop "TPPS/2 ALPS TrackPoint" "libinput Scroll Method Enabled" 0 0 1` 

### Lenovo ThinkPad Thunderbolt 3 Dockingstation

The USB-C Dock is a Thunderbolt 3 device. Plugging it in results in a whole lot of PCI entries:

```
06:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:00.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:01.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:02.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
07:04.0 PCI bridge: Intel Corporation JHL6540 Thunderbolt 3 Bridge (C step) [Alpine Ridge 4C 2016] (rev 02)
3c:00.0 USB controller: Intel Corporation Device 15d4 (rev 02)

```

As of stock kernel 5.2.1, the dock is fully functional with appropriate kernel modules enabled. In particular, you must enable the `r8152` kernel module. See also the [Kernel module](/index.php/Kernel_module "Kernel module") article on how to enable `r8152` persistently. This driver allows the kernel to recognize the USB devices and ethernet port of the dock.

Finally, in order for the internal USB hub in the dock to work, you need to set Thunderbolt 3 security appropriately.

The easiest, but insecure, way to do so is to change the "Security Level" to "No Security" under Thuderbolt settings in the BIOS. Be aware, however, that this directly exposes the PCIe bus to any device plugged into your laptop, leaving you vulnerable to attacks such as [DMA attacks](https://en.wikipedia.org/wiki/DMA_attack "wikipedia:DMA attack") and [Thunderstrike](https://trmm.net/Thunderstrike_2). As of July 2019, this is not necessary as the more secure method below works with stock packages.

The more secure way to enable USB ports on the dock is to use the `bolt` tool, which can be installed via [bolt](https://www.archlinux.org/packages/?name=bolt). To use this tool, set "Security level" in the Thunderbolt settings in the BIOS to "Secure". After booting, attach the dock and (using the laptop's own keyboard) run `boltctl list` to find the UUID of your dock. Following that, run `boltctl enroll --policy=auto <uuid>` to give the dock permission to access the PCIe bus automatically whenever it is plugged in. This procedure is verified to work with the X1 Carbon Gen 5 and Lenovo's dock. It may or may not work with other docks.

Also remember to enable the "Support in pre boot environment" for USB peripherals connected to the dock to work at all.

### HP Thunderbolt 3 Dock

The HP Thunderbolt 3 Dock is working out of the box with the insecure method described above. It is not known whether the secure method works with this dock.

### Lenovo p27h-10 (USB Type C)

Charging while using the monitor via USB-Type-C is working but the dock functionality needs investigation (e.g. speakers, mouse, directly from the monitor).