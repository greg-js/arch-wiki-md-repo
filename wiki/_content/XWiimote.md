# XWiimote

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article is about the Nintendo Wii Remote Linux kernel driver. This driver is part of upstream Linux since version 3.1\. It is an easy to use drop-in replacement for the older user-space drivers like [cwiid](/index.php/Wiimote "Wiimote"). You can use your Wii Remote for all purposes with this driver, for instance as an [X](/index.php/X "X") input device or joystick controller for your Linux games.

**Note:** The XWiimote tools are still experimental. Connecting and managing your Wii Remote works well and there is a driver to use the Wii Remote as X11 input, but extended features may still be missing.

## Contents

*   [1 Prerequisites](#Prerequisites)
    *   [1.1 hid-wiimote kernel module](#hid-wiimote_kernel_module)
*   [2 Connect the Wii Remote](#Connect_the_Wii_Remote)
*   [3 Device Handling](#Device_Handling)
    *   [3.1 X.Org Input Driver](#X.Org_Input_Driver)
    *   [3.2 Infrared Sources](#Infrared_Sources)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 The input mapping is very weird](#The_input_mapping_is_very_weird)
    *   [4.2 BlueZ does not include the wiimote plugin](#BlueZ_does_not_include_the_wiimote_plugin)
    *   [4.3 I cannot connect my wiimote](#I_cannot_connect_my_wiimote)
    *   [4.4 Cannot use Wiimote in Dolphin-emu after pairing with xwiimote](#Cannot_use_Wiimote_in_Dolphin-emu_after_pairing_with_xwiimote)
    *   [4.5 My Wii Remote is still not working](#My_Wii_Remote_is_still_not_working)
    *   [4.6 Auto-Reconnect is not working after pairing with red sync-button](#Auto-Reconnect_is_not_working_after_pairing_with_red_sync-button)
*   [5 See also](#See_also)

## Prerequisites

*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   [xwiimote-git](https://aur.archlinux.org/packages/xwiimote-git/)<sup><small>AUR</small></sup>
*   xwiimote kernel driver
*   Wii Remote hardware

The most important software required is [Bluetooth](/index.php/Bluetooth "Bluetooth"), please make sure you have read the [relative wiki page](/index.php/Bluetooth "Bluetooth") to configure it before proceeding.

**NOTE:** most recent bluez package in Arch Linux includes the wiimote plugin, if you are using an older version please see [Troubleshooting BlueZ](#BlueZ_does_not_include_the_wiimote_plugin).

The user-space utilities are available in [AUR](/index.php/AUR "AUR") [xwiimote-git](https://aur.archlinux.org/packages/xwiimote-git/)<sup><small>AUR</small></sup> package; there is also a git-package [xwiimote-tools-git](https://aur.archlinux.org/packages/xwiimote-tools-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xwiimote-tools-git)]</sup> if you want the most recent development revision.

The kernel driver (module `hid-wiimote`) is part of upstream Linux since version 3.1 and it's ever since already included in Arch Linux kernel. However, the module could need to be loaded:

```
# modprobe hid-wiimote

```

Lastly you will need a Wii Remote, this can include (although, are not required) the Nunchuk and Classic Controller attachments.

### hid-wiimote kernel module

If you are using a custom kernel, you can enable the `hid-wiimote` module with `CONFIG_HID_WIIMOTE` and the dependencies `CONFIG_INPUT_FF_MEMLESS`, `CONFIG_LEDS_CLASS`, `CONFIG_POWER_SUPPLY` and `CONFIG_BT_HIDP` embedded in your kernel or as modules, previously loaded. Starting with kernel version 3.3 there is an additional config option `CONFIG_HID_WIIMOTE_EXT` which is enabled by default. It controls whether wiimote extensions like Nunchuck and Classic Controller should be supported.

## Connect the Wii Remote

You can connect to your Wii Remote like any other Bluetooth device. See the [Bluetooth article](/index.php/Bluetooth "Bluetooth") about information on pairing Bluetooth devices. The Wii Remote does not need special handling anymore. The BlueZ wiimote plugin handles all peculiarities in the background for you.

The Wii Remote can be put into discoverable mode by pressing the red sync-button behind the battery cover on the back. The Wii Remote will stay in discoverable mode for 20s. You can also hold the 1+2 buttons to put the Wii Remote into discoverable state. However, the first method works more reliably!

If you are asked for PIN input while bonding the devices, then your BlueZ bluetoothd daemon does not include the wiimote plugin. See [Troubleshooting BlueZ](#BlueZ_does_not_include_the_wiimote_plugin) for more information. If this does not help, you can still connect to your wiimote without pairing/bonding (i.e. not using authentication with a PIN). This should work with any BlueZ version. See [Troubleshooting Pairing](#I_cannot_connect_my_wiimote) if you still cannot connect your wiimote.

## Device Handling

If your Wii Remote is connected, it will appear with several input devices inside `/dev/input/eventX`. You can list all Wii Remotes with:

```
$ ls /sys/bus/hid/devices

```

Then you can get additional device details with:

```
$ ls /sys/bus/hid/devices/<devid>/

```

The default mapping for the input-keys of the Wii Remotes are not very useful. User-space applications exist that re-map the Wii Remote input to more useful keys/actions [[1]](http://github.com/dvdhrm/xwiimote) - available in AUR [xwiimote-git](https://aur.archlinux.org/packages/xwiimote-git/)<sup><small>AUR</small></sup>. If you installed this package you can test your connected Wii Remotes with the `xwiishow` tool:

This will list all connected Wii Remotes:

```
$ xwiishow list

```

If this shows a path to a Wii Remote (lets say `/sys/bus/hid/devices/<did>`) then you can test the device with:

```
$ xwiishow /sys/bus/hid/devices/<did>

```

Or use the index of the listed device:

```
$ xwiishow 1

```

This will display a picture of the Wii Remote and notify you if buttons are pressed. You can use the `'r'` key to enable/disable the rumble motor. Press `'q'` to quit the application. You might need to be root to use these tools.

### X.Org Input Driver

There is an X.Org input driver [[2]](http://github.com/dvdhrm/xf86-input-xwiimote) available in AUR [xf86-input-xwiimote](https://aur.archlinux.org/packages/xf86-input-xwiimote/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xf86-input-xwiimote)]</sup> which automatically provides an input device to your X clients. Install it and read the related man-page for more information:

```
$ man xorg-xwiimote

```

### Infrared Sources

The Wii Remote includes an infrared camera. To use this camera as a pointer input device, you need an IR-rack as an infrared source. Possible infrared sources are:

*   Nintendo Wii Sensor Bar
*   Wireless sensor bar - check eBay!
*   Small candles (should have about 30cm distance)
*   Home made sensor bar ([[3]](http://doctabu.livejournal.com/64758.html))

**Note:** xf86-input-xwiimote has support for mouse-emulation via IR using the `Option "MotionSource" "ir"`

There is currently no user-space application that enables mouse-emulation with the IR-sensor. If you need that, you should consider using the no longer supported [cwiid](/index.php/Wiimote "Wiimote") approach. However, the xwiimote tools are under heavy development and will soon support IR mouse-emulation, too.

## Troubleshooting

### The input mapping is very weird

The default mapping maps the Wii Remote keys to the the key-constants which resemble the Wii Remote's buttons best. This mapping is quite useless by default. To get better mappings, use the [xwiimote userspace tools](#Device_Handling).

### BlueZ does not include the wiimote plugin

Upstream BlueZ includes the _optional_ wiimote plugin since version 4.96\. However, it must be enabled explicitely with `--enable-wiimote` during compilation. The archlinux package includes the wiimote plugin since `bluez-4.96-3`. If you are unsure whether your package includes the wiimote plugin, use:

```
grep wiimote $(which bluetoothd)

```

This should say:

```
Binary file /usr/sbin/bluetoothd matches

```

**Note:** with bluez 5.5, this file resides in `/usr/lib/bluetooth` on ArchLinux. Use the below to check: `grep wiimote /usr/lib/bluetooth/bluetoothd` 

If this matches, then your BlueZ includes the wiimote plugin and no more user-interaction is needed. If this does not match, you need to enable it yourself or work without it. If you do not want to compile your own bluez package, then you can use the wiimote without this plugin by connecting without pairing/bonding. For instance, when using `blueman` or `gnome-bluetooth` you need to select `"Proceed without pairing"` when adding a new device.

If you want to compile the module on your own, then add `--enable-wiimote` to your configure flags and proceed as usual. See the bluez PKGBUILD for further information.

### I cannot connect my wiimote

The BlueZ packages includes a special wiimote plugin since version `4.96` which handles all Wii Remote peculiarities for you. If you cannot pair your Wii Remote like any other device, then you should try connecting without pairing/bonding (i.e. not using authentication with a PIN). If this still does not work, please report your issue to the upstream developers at [XWiimote@GitHub](http://www.github.com/dvdhrm/xwiimote/issues).

Please always use the red sync-button behind the battery cover on the back of the Wii Remote for troubleshooting. This works more reliably than holding the 1+2 buttons.

The Auto-Reconnect feature allows the Wii Remote to reconnect to its last connected host when a key is pressed. This means you do not need to connect your Wii Remote manually each time. However, the Auto-Reconnect feature only works if you paired your Wii-Remote. Connecting without the wiimote plugin will not enable Auto-Reconnect.

### Cannot use Wiimote in Dolphin-emu after pairing with xwiimote

Dolphin uses its own driver so pressing the resync button on the wiimote while dolphin is running should resync the wiimote to dolphin instead of the xwiimote.

### My Wii Remote is still not working

The XWiimote software stack is actively developed. Please report your problems at [XWiimote@GitHub](http://www.github.com/dvdhrm/xwiimote/issues).

There are also other projects which provide Wii Remote support for linux. See the [Wii Remote article](/index.php/Wiimote "Wiimote") for the cwiid project.

### Auto-Reconnect is not working after pairing with red sync-button

It seems that the wiimote needs to be connected directly after pairing in order to store the binding (??) and reconnect automatically to the host.

Use the following sequence in bluetoothctl:

```
power on
agent on
<press red sync button>
scan on
pair <MAC of the found wiimote, use TAB for autocompletion>           # **note:** we do not explicitly connect, we just pair!
connect <MAC of the wiimote>                                          # there seems to be a pretty short timeout, so execute this **immediately after the pairing command**
trust <MAC of the wiimote>
disconnect <MAC of the wiimote>

```

The wiimote should disconnect and the power led go off. Pressing the power button on the wiimote should now re-establish the connection to the host without any further actions.

## See also

*   [Wiimote](/index.php/Wiimote "Wiimote"): Cwiid: An older software stack for linux which provides partial Wii Remote support
*   [[4]](http://dvdhrm.wordpress.com/2012/02/26/xf86-input-xwiimote-0-2/): Developer blog about Wii Remotes

Retrieved from "[https://wiki.archlinux.org/index.php?title=XWiimote&oldid=401024](https://wiki.archlinux.org/index.php?title=XWiimote&oldid=401024)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Other hardware](/index.php/Category:Other_hardware "Category:Other hardware")