The [Logitech Unifying Receiver](http://www.logitech.com/349/6072) is a wireless receiver using 2.4 GHz band radio communication that can connect up to six compatible wireless mice and keyboards to your computer. The input device that comes with the receiver is already paired with it and should work out of the box through plug and play. Logitech officially supports pairing of additional devices just through their Windows and macOS software.

Pairing and unpairing on Linux is supported by a number of tools, listed thereafter:

[ltunify](https://lekensteyn.nl/logitech-unifying.html) is a command-line C program that can perform pairing, unpairing and listing of devices. [Solaar](https://pwr-solaar.github.io/Solaar/) is a graphical Python program that integrates in your system tray and allows you to configure additional features of your input device such as swapping the functionality of Fn keys. [libratbag](https://github.com/libratbag/libratbag) is a configurable mice daemon that allows you to configure your devices, it has a GTK based graphical frontend app, [piper](https://github.com/libratbag/piper).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 ltunify](#ltunify)
    *   [2.2 Solaar](#Solaar)
    *   [2.3 libratbag](#libratbag)
    *   [2.4 pairingtool](#pairingtool)
*   [3 Known Problems](#Known_Problems)
    *   [3.1 Wrong device (pairing tool only)](#Wrong_device_(pairing_tool_only))
    *   [3.2 Keyboard layout via xorg.conf](#Keyboard_layout_via_xorg.conf)
    *   [3.3 Logitech touchpad keyboard K400r with unifying receiver M325](#Logitech_touchpad_keyboard_K400r_with_unifying_receiver_M325)
    *   [3.4 Solaar 'Permission denied'](#Solaar_'Permission_denied')
    *   [3.5 Wireless Keyboard doesn't work while booting (can't enter luks passphrase)](#Wireless_Keyboard_doesn't_work_while_booting_(can't_enter_luks_passphrase))
    *   [3.6 MouseJack Vulnerability](#MouseJack_Vulnerability)
    *   [3.7 Keyboard or mouse does not wake pc from sleep](#Keyboard_or_mouse_does_not_wake_pc_from_sleep)
    *   [3.8 Lag of the wireless device during heavy Wi-Fi load](#Lag_of_the_wireless_device_during_heavy_Wi-Fi_load)

## Installation

Several solutions are available:

*   [libratbag](https://www.archlinux.org/packages/?name=libratbag)/[piper](https://www.archlinux.org/packages/?name=piper)
*   [pairing_tool](https://aur.archlinux.org/packages/pairing_tool/)

The following packages use the `plugdev` [user group](/index.php/User_group "User group"), create it if it does not exist, and add users to this group to avoid the need of running these as root:

*   [solaar](https://www.archlinux.org/packages/?name=solaar) or [solaar-git](https://aur.archlinux.org/packages/solaar-git/)
*   [ltunify-git](https://aur.archlinux.org/packages/ltunify-git/)

Do not forget to relogin to apply user's group membership. After installation, run

```
# udevadm control --reload-rules

```

and then replug reciever. After that you will not need root permissions.

## Usage

pairingtool can only be used for pairing and does not provide feedback, it also needs to know the device name for pairing. ltunify, Solaar and libratbag can detect the receiver automatically.

### ltunify

Examples on unpairing a device, pairing a new device and showing a list of all devices:

```
$ ltunify unpair mouse
Device 0x01 Mouse successfully unpaired
$ ltunify pair
Please turn your wireless device off and on to start pairing.
Found new device, id=0x01 Mouse
$ ltunify list
Devices count: 1
Connected devices:
idx=1   Mouse   M525

```

### Solaar

Solaar has a GUI and CLI. Example CLI pairing session:

```
$ solaar unpair mouse
Unpaired 1: Wireless Mouse M525 [M525:DAFA335E]
$ solaar pair
Pairing: turn your new device on (timing out in 20 seconds).
Paired device 1: Wireless Mouse M525 [M525:DAFA335E]
$ solaar show
-: Unifying Receiver [/dev/hidraw0:08D89AA6] with 1 devices
1: Wireless Mouse M525 [M525:DAFA335E]

```

To disable autostart of Solaar, remove `/etc/xdg/autostart/solaar.desktop`.

### libratbag

Currently, piper isn't able to pair/manage devices for unifying receivers but libratbag does include a `lur-command` command line tool that is able to do this.

### pairingtool

To find the device that the receiver has, therefore take a look at the outputs of

```
$ ls -l /sys/class/hidraw/hidraw*/device/driver | awk -F/ '/receiver/{print $5}'

```

This will show the names of your receiver, for example `hidraw0`.

Now switch off the device that you want to pair (if it was on) and execute your compiled program with the appropriate device as argument:

```
# pairing_tool /dev/hidraw0
The receiver is ready to pair a new device.
Switch your device on to pair it (you have thirty seconds to do so).

```

Now switch on the device you want to pair. After a few seconds your new device should work properly.

## Known Problems

### Wrong device (pairing tool only)

On some systems there is more than one device that has the same name. In that case you will receive the following error message when the wrong device is choosen:

```
# pairing_tool /dev/hidraw1
Error: 32
write: Broken pipe

```

### Keyboard layout via xorg.conf

With kernel 3.2 the Unifying Receiver got its own kernel module *hid_logitech_dj* which does not work flawlessly together with keyboard layout setting set via [xorg.conf](/index.php/Xorg#Keyboard_settings "Xorg"). A temporary workaround is to use [xorg-setxkbmap](https://www.archlinux.org/packages/?name=xorg-setxkbmap) and set the layout manually. For example for a German layout with no deadkeys one has to execute:

```
$ setxkbmap -layout de -variant nodeadkeys

```

To automate this process one could add this line to [xinitrc](/index.php/Xinitrc "Xinitrc") or the according [autostart](/index.php/Autostart "Autostart") file of your windows manager respectively desktop environment.

### Logitech touchpad keyboard K400r with unifying receiver M325

The Logitech keyboard K400r with integrated touchpad comes with Logitech unifying receiver M325 so the above mentioned about the keyboard layout will apply here too.

Also the integrated touchpad is recognized as 'pointer' instead of 'touchpad' so you cannot use the [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") drivers. Two finger horizontal scrolling and tapclick will work but in order to have a middle mouse button emulated you will have to add

 `/etc/X11/xorg.conf.d/10-evdev.conf` 
```
Section "InputClass"
        Identifier "evdev pointer catchall"
        MatchIsPointer "on"
        MatchDevicePath "/dev/input/event*"
        Driver "evdev"
        Option "Emulate3Buttons" "true"
EndSection

```

to your evdev.conf. Now third button is emulated by pressing both buttons simultaneously.

### Solaar 'Permission denied'

Is it possible to have the error:

```
$ solaar show
solaar: error: [Errno 13] Permission denied: '/dev/hidraw2'

```

In this case, you can physically remove the Unifying Receiver and re-insert it, and re-run the command (as described in the second point of installation part on the official site [[1]](https://github.com/3v1n0/Solaar/blob/master/docs/installation.md)).

### Wireless Keyboard doesn't work while booting (can't enter luks passphrase)

While booting it's impossible to input anything with a Logitech wireless Keyboard (e. g. Logitech MK700). The cause of the problem is the own hid module for Logitech devices since Kernel 3.2.

A workaround is adding *hid-logitech-hidpp* to MODULES in `/etc/mkinitcpio.conf`:

```
MODULES="hid-logitech-hidpp"

```

and recreate the initrd for the kernel:

```
# mkinitcpio -p linux

```

### MouseJack Vulnerability

Several security vulnerabilities of the system have been reported and you may be in particular affected by the [MouseJack Vulnerability](https://www.bastille.net/research/vulnerabilities/mousejack/affected-devices) if your firmware has not been updated recently.

It is possible to display the current firmware's version by running:

```
ltunify receiver-info

```

RQR12 firmware with version earlier than `012.008.00030` and RQR24 firmware versions earlier than `024.006.00030` are affected by this vulnerability and should be updated.

The firmware can be updated using [fwupd](/index.php/Fwupd "Fwupd") like so:

```
fwupdmgr refresh && fwupdmgr get-updates

```

If everything looks good, apply the update:

```
fwupdmgr update

```

### Keyboard or mouse does not wake pc from sleep

Follow the [Solaar USB installation](https://github.com/3v1n0/Solaar/blob/master/docs/installation.md) instructions.

### Lag of the wireless device during heavy Wi-Fi load

Because the receiver uses the 2.4 GHz frequency band also used by Bluetooth and Wi-Fi 802.11, it is possible in some circumstances of heavy Wi-Fi usage close to the receiver to experience lag or disturbances in communication with the devices. This is unlikely because the receiver confines its communication to channels unused by the majority of 802.11 solutions and it is able to quickly change channel within the band if it detects any interference from another device. However, some users have experienced interferences.

Switching on/off the device will force the search for a "quiet" channel and may solve the issue.