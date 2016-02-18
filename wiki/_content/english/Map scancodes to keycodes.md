**Note:** This page assumes that you have read [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys"), which provides wider context to the problem.

Mapping *scancodes* to *keycodes* is universal and not specific to Linux console or Xorg, which means that changes to this mapping will be effective in both.

There are two ways of mapping *scancodes* to *keycodes*:

*   Using [udev](/index.php/Udev "Udev")
*   Using *setkeycodes*

The preferred method is to use *udev* because it uses hardware information (which is a quite reliable source) to choose the keyboard model in a database. It means that if your keyboard model has been found in the database, your keys are recognized *out of the box*.

## Contents

*   [1 Identifying scancodes](#Identifying_scancodes)
*   [2 Using udev](#Using_udev)
    *   [2.1 Example for custom hwdb](#Example_for_custom_hwdb)
    *   [2.2 Updating the Hardware Database Index](#Updating_the_Hardware_Database_Index)
    *   [2.3 Reloading the Hardware Database Index](#Reloading_the_Hardware_Database_Index)
    *   [2.4 Querying the database](#Querying_the_database)
*   [3 Using setkeycodes](#Using_setkeycodes)

## Identifying scancodes

You need to know the *scancodes* of keys you wish to remap. See [Extra keyboard keys#Scancodes](/index.php/Extra_keyboard_keys#Scancodes "Extra keyboard keys") for details.

## Using udev

[udev](/index.php/Udev "Udev") provides a builtin function called *hwdb* to maintain the hardware database index in `/etc/udev/hwdb.bin`. The database is compiled from files with *.hwdb* extension located in directories `/usr/lib/udev/hwdb.d/`, `/run/udev/hwdb.d/` and `/etc/udev/hwdb.d/`. The default *scancodes-to-keycodes* mapping file is `/usr/lib/udev/hwdb.d/60-keyboard.hwdb`. See `man udev` for details.

**Note:** From systemd 220 the udev ABI changed. Users using custom udev hwdb rules should update them according to the new ABI

The *.hwdb* file can contain multiple blocks of mappings for different keyboards, or one block can be applied to multiple keyboards. The `evdev:` prefix is used to match a block against a hardware, the following hardware matches are supported:

*   Generic input devices (also USB keyboards) identified by the usb kernel modalias: `evdev:input:b*<bus_id>*v*<vendor_id>*p*<product_id>*e*<version_id>*-*<modalias>*` where `*<vendor_id>*`, `*<product_id>*` and `*<version_id>*` are the 4-digit hex uppercase vendor, product and version IDs (you can find those by running the `lsusb` command) and `*<modalias>*` is an arbitrary length input-modalias describing the device capabilities. `*<bus_id>*` is the 4-digit hex bus id and should be 0003 for usb devices. The possible `*<bus_id>*` values are defined in `/usr/include/linux/input.h` (you can use the following command to get a list `awk '/BUS_/ {print $2, $3}' /usr/include/linux/input.h`).
*   AT keyboard DMI data matches: `evdev:atkbd:dmi:bvn*:bvr*:bd*:svn*<vendor>*:pn*<product>*:pvr*` where `*<vendor>*` and `*<product>*` are the firmware-provided strings exported by the kernel DMI modalias.
*   Input driver device name and DMI data match: `evdev:name:*<input device name>*:dmi:bvn*:bvr*:bd*:svn*<vendor>*:pn*` where `*<input_device_name>*` is the name device specified by the driver and `*<vendor>*` is the firmware-provided string exported by the kernel DMI modalias.

The format of each line in the block body is `KEYBOARD_KEY_*<scancode>*=*<keycode>*`. The value of `*<scancode>*` is hexadecimal, but without the leading `0x` (i.e. specify `a0` instead of `0xa0`), whereas the value of `*<keycode>*` is the lower-case keycode name string as listed in `/usr/include/linux/input.h` (see the `KEY_*<KEYCODE>*` variables), a sorted list is available at [[1]](http://hal.freedesktop.org/quirk/quirk-keymap-list.txt). It is not possible to specify decimal value in `*<keycode>*`.

### Example for custom hwdb

The example hwdb file will match all AT keyboards:

 `/etc/udev/hwdb.d/90-custom-keyboard.hwdb` 
```
evdev:atkbd:dmi:bvn*:bvr*:bd*:svn*:pn*:pvr*
 KEYBOARD_KEY_10=suspend
 KEYBOARD_KEY_a0=search

```

Here is an example of rebinding modifiers on a laptop and USB keyboard:

 `/etc/udev/hwdb.d/10-my-modifiers.hwdb` 
```
evdev:input:b0003v05AFp8277* # was tested on Kensington Slim Type USB (with old ABI)
 KEYBOARD_KEY_70039=leftalt  # bind capslock to leftalt
 KEYBOARD_KEY_700e2=leftctrl # bind leftalt to leftctrl

evdev:atkbd:dmi:*            # built-in keyboard: match all AT keyboards for now
 KEYBOARD_KEY_3a=leftalt     # bind capslock to leftalt
 KEYBOARD_KEY_38=leftctrl    # bind leftalt to leftctrl

```

### Updating the Hardware Database Index

After changing the configuration files, the hardware database index, `hwdb.bin`, needs to be rebuilt.

*   Update `hwdb.bin` manually by running

```
# udevadm hwdb --update

```

*   Update automatically on each reboot by commenting out `ConditionNeedsUpdate` in `systemd-udev-hwdb-update.service`.

 `/usr/lib/systemd/system/systemd-udev-hwdb-update.service` 
```
#  This file is part of systemd.
.
.
#ConditionNeedsUpdate=/etc
.
.

```

After `systemd-udev-hwdb-update.service` finished loading `systemd-udev-trigger.service` will reload the changes from `hwdb.bin`.

*   Automatically after [Systemd](/index.php/Systemd "Systemd") upgrade.

On each upgrade of [Systemd](/index.php/Systemd "Systemd"), the installation script rebuilds `hwdb.bin` by running `# udevadm hwdb --update` so we do not need to care about it.

### Reloading the Hardware Database Index

The kernel loads `hwdb.bin` as part of the boot process, rebooting the system will promise the loading of the updated `hwdb.bin`.

With `udevadm` it is possible to load new key mapping from the updated `hwdb.bin` by running

```
# udevadm trigger

```

Be aware that with `udevadm` only added or changed key mapping are loaded so if we delete a mapping from the config file, rebuild `hwdb.bin` and run `# udevadm trigger` then the deleted mapping still kept by the kernel, at least until a reboot.

### Querying the database

You can check that your configuration was loaded either by pressing keys, or by running `udevadm info`. For the USB keyboard in the above example, this outputs the mapping we configured as follows:

```
# udevadm info /dev/input/by-path/*-usb-*-kbd | grep KEYBOARD_KEY
E: KEYBOARD_KEY_70039=leftalt
E: KEYBOARD_KEY_700e2=leftctrl

```

## Using setkeycodes

*setkeycodes* is a tool to load *scancodes*-to-*keycodes* mapping table into Linux kernel. Its usage is:

```
# setkeycodes *scancode* *keycode* ...

```

It is possible to specify multiple pairs at once. *Scancodes* are given in hexadecimal, *keycodes* in decimal.

**Note:** Apparently *setkeycodes* does not work with USB keyboards (Linux 3.14.44-1-lts):
```
# setkeycodes 45 30     # bind NumLock (0x45) to KEY_A (30) on AT keyboard
(successful)
# setkeycodes 70053 30  # bind NumLock (0x70053) to KEY_A (30) on USB keyboard
KDSETKEYCODE: Invalid argument
failed to set scancode 620d3 to keycode 31

```