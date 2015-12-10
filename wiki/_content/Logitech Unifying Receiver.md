# Logitech Unifying Receiver

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The [Logitech Unifying Receiver](http://www.logitech.com/349/6072) is a wireless receiver that can connect up to six compatible wireless mice and keyboards to your computer. The input device that comes with the receiver is already paired with it and should work out of the box through plug and play. Logitech officially supports pairing of additional devices just through their Windows and Mac OS X software. Pairing on Linux is supported by [a small program from Benjamin Tissoires](https://lkml.org/lkml/2011/9/22/367). That tool does not provide any feedback though. Other developers have built more complete pairing tools that give feedback and allow unpairing as well.

[ltunify](https://lekensteyn.nl/logitech-unifying.html) is a command-line C program that can perform pairing, unpairing and listing of devices. [Solaar](http://pwr.github.io/Solaar/) is a graphical Python program that integrates in your system tray and allows you to configure additional features of your input device such as swapping the functionality of Fn keys.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 ltunify](#ltunify)
    *   [2.2 Solaar](#Solaar)
    *   [2.3 pairingtool](#pairingtool)
*   [3 Known Problems](#Known_Problems)
    *   [3.1 Wrong device (pairing tool only)](#Wrong_device_.28pairing_tool_only.29)
    *   [3.2 Keyboard layout via xorg.conf](#Keyboard_layout_via_xorg.conf)
    *   [3.3 Solaar 'Permission denied'](#Solaar_.27Permission_denied.27)
    *   [3.4 Wireless Keyboard doesn't work while booting (can't enter luks passphrase)](#Wireless_Keyboard_doesn.27t_work_while_booting_.28can.27t_enter_luks_passphrase.29)

## Installation

Benjamin's program can directly be installed from AUR: [pairing_tool](https://aur.archlinux.org/packages/pairing_tool/)<sup><small>AUR</small></sup>.

Solaar is also available from the AUR: [solaar](https://aur.archlinux.org/packages/solaar/)<sup><small>AUR</small></sup>. At installation the Solaar package is creating the group plugdev. After installation add you user to the plugdev group (`# gpasswd -a $USER plugdev`) to use Solaar as non-root user.

ltunify is now also available from the AUR: [ltunify-git](https://aur.archlinux.org/packages/ltunify-git/)<sup><small>AUR</small></sup>. Create the plugdev group before installation and add yourself to it (to avoid the need of running ltunify as root). After installation, you can edit the file `/etc/udev/rules.d/42-logitech-unify-permissions.rules` to change the device group (the default group is plugdev).

## Usage

pairingtool can only be used for pairing and does not provide feedback, it also needs to know the device name for pairing. ltunify and Solaar can detect the receiver automatically.

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
$ solaar-cli unpair mouse
Unpaired 1: Wireless Mouse M525 [M525:DAFA335E]
$ solaar-cli pair
Pairing: turn your new device on (timing out in 20 seconds).
Paired device 1: Wireless Mouse M525 [M525:DAFA335E]
$ solaar-cli show
-: Unifying Receiver [/dev/hidraw0:08D89AA6] with 1 devices
1: Wireless Mouse M525 [M525:DAFA335E] 

```

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

With kernel 3.2 the Unifying Receiver got its own kernel module _hid_logitech_dj_ which does not work flawlessly together with keyboard layout setting set via [xorg.conf](/index.php/Xorg#Keyboard_settings "Xorg"). A temporary workaround is to use [xorg-setxkbmap](https://www.archlinux.org/packages/?name=xorg-setxkbmap) and set the layout manually. For example for a German layout with no deadkeys one has to execute:

```
$ setxkbmap -layout de -variant nodeadkeys

```

To automate this process one could add this line to [xinitrc](/index.php/Xinitrc "Xinitrc").

### Solaar 'Permission denied'

Is it possible to have the error:

```
$ solaar-cli show
solaar-cli: error: [Errno 13] Permission denied: '/dev/hidraw2'

```

In this case, you can physically remove the Unifying Receiver and re-insert it, and re-run the command (as described in the second point of installation part on the official site [[1]](https://pwr.github.io/Solaar/installation.html)).

### Wireless Keyboard doesn't work while booting (can't enter luks passphrase)

While booting it's impossible to input anything with a Logitech wireless Keyboard (e. g. Logitech MK700). The cause of the problem is the own hid module for Logitech devices since Kernel 3.2.

To fix the problem, just add "hid-logitech-hidpp" to MODULES in /etc/mkinitcpio.conf like this:

```
MODULES="hid-logitech-hidpp"

```

and recreate the initrd for the kernel.

```
$ mkinitcpio -p linux

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Logitech_Unifying_Receiver&oldid=409595](https://wiki.archlinux.org/index.php?title=Logitech_Unifying_Receiver&oldid=409595)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Input devices](/index.php/Category:Input_devices "Category:Input devices")