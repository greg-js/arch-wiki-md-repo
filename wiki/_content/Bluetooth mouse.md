# Bluetooth mouse

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   [Bluez4](/index.php/Bluez4 "Bluez4")
*   [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate")

This article describes how to set up a [Bluetooth](/index.php/Bluetooth "Bluetooth") mouse through the command line without relying upon a graphical application.

## Contents

*   [1 Installation](#Installation)
*   [2 Bluez5 instructions](#Bluez5_instructions)
*   [3 Bluez4 instructions](#Bluez4_instructions)
    *   [3.1 Kernel modules](#Kernel_modules)
    *   [3.2 Test](#Test)
    *   [3.3 Configure bluetooth mouse](#Configure_bluetooth_mouse)
    *   [3.4 Search your mouse](#Search_your_mouse)
    *   [3.5 Connecting the mouse](#Connecting_the_mouse)
        *   [3.5.1 Connecting the mouse at startup](#Connecting_the_mouse_at_startup)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Mouse lag](#Mouse_lag)
    *   [4.2 Problems with the USB dongle](#Problems_with_the_USB_dongle)

## Installation

Install the [bluez](https://www.archlinux.org/packages/?name=bluez) package which contains the current Linux bluetooth stack (Bluez5). You may also want to install [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) which provides the _bluetoothctl_ utility. See [Bluetooth](/index.php/Bluetooth "Bluetooth") for more information.

If you would prefer to configure bluetooth through the older Bluez4 stack then install the [bluez4](https://aur.archlinux.org/packages/bluez4/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/bluez4)]</sup> package from the [AUR](/index.php/AUR "AUR"). Please consult the [Bluez4](/index.php/Bluez4 "Bluez4") article for more information.

**Warning:** Bluez4 has been deprecated. It is strongly recommended that you use Bluez5 instead.

## Bluez5 instructions

**Tip:** Ensure that the bluetooth daemon is started before continuing.

Bluez5 provides the _bluetoothctl_ utility which provides a simple interface for configuring bluetooth devices.

The text below is an example of how you can connect a bluetooth mouse using _bluetoothctl_:

```
# bluetoothctl
[bluetooth]# list
Controller <controller mac> BlueZ 5.5 [default]
[bluetooth]# select <controller mac>
[bluetooth]# power on
[bluetooth]# scan on
[bluetooth]# agent on
[bluetooth]# devices
Device <mouse mac> Name: Bluetooth Mouse
[bluetooth]# pair <mouse mac>
[bluetooth]# trust <mouse mac>
[bluetooth]# connect <mouse mac>

```

In order for the device to start on boot you may have to create a [udev](/index.php/Udev "Udev") rule. Please see [Bluetooth#Bluetoothctl](/index.php/Bluetooth#Bluetoothctl "Bluetooth") for more information.

**Tip:** In case you were using USB Bluetooth dongle and moved it to another USB port, you may need to remove the mouse's MAC address in _bluetoothctl_ with _remove <mouse mac>_ command and repeat the entire procedure again.

## Bluez4 instructions

### Kernel modules

No additional actions are necessary if the bluetooth service is started using systemd. If it does not work try the following command:

```
# modprobe -v btusb bluetooth hidp l2cap

```

It loads the kernel modules you need, if they were not loaded automatically.

### Test

The following command should show your bluetooth adapter:

 `# hciconfig` 

```
hci0:  Type: BR/EDR  Bus: USB
       BD Address: 00:22:43:E1:82:E0  ACL MTU: 1021:8  SCO MTU: 64:1
       UP RUNNING PSCAN 
       RX bytes:1062273 acl:62061 sco:0 events:778 errors:0
       TX bytes:1825 acl:11 sco:0 commands:39 errors:0

```

### Configure bluetooth mouse

The method described here is based in three steps, in this order:

1.  Make the PC learn about the bluetooth mouse.
2.  Grant the mouse permissions to connect.
3.  Make the mouse learn about the PC.

### Search your mouse

First make your mouse discoverable. For example some mouse need to press a button. Then issue the following command:

 `# hcitool scan` 

```
Scanning ...
        00:07:61:F5:5C:3D       Logitech Bluetooth Mouse M555b

```

Your mouse bluetooth mac address will be similar to `12:34:56:78:9A:BC`. You may also find it in the documentation or on the mouse itself.

### Connecting the mouse

To scan the device (you may need to use `su -c` or `sudo`):

```
hidd --search
hcitool inq

```

To connect the device:

```
hidd --connect <bdaddr>

```

To show your currently connected devices:

```
hidd --show

```

The mouse should show up in this list. If it does not, press the reset button to make it discoverable.

**Note:** If you have the ipw3945 module loaded (wifi on HP computer) bluetooth would not work.

#### Connecting the mouse at startup

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** This section of the article discusses instructions for the [SysVinit](/index.php/SysVinit "SysVinit") init system. [SysVinit](/index.php/SysVinit "SysVinit") has been replaced by [Systemd](/index.php/Systemd "Systemd"). (Discuss in [Talk:Bluetooth mouse#](https://wiki.archlinux.org/index.php/Talk:Bluetooth_mouse))

Edit `/etc/conf.d/bluetooth`:

```
# Arguments to hidd
HIDD_OPTIONS="--connect <enter here your bluetooth mouse mac address>"

```

and test the new settings:

```
/etc/rc.d/bluetooth stop
hidd --killall #(drop mouse connection)
/etc/rc.d/bluetooth start

```

**Note:** The above instructions to start the mouse at startup do not work with the now outdated 3.11 bluetooth packages. New versions such as the current (3.32) packages are not affected.

If you are using an older version, then to start the mouse at startup, add:

```
hidd --connect <enter here your bluetooth mouse address (No capitals!!!)>

```

to your `/etc/rc.local file`.

**Note:** You can connect any bluetooth mouse and/or keyboard without any further configuration and without knowing the device address. You can do it by adding the --master and/or --server option in HIDD_OPTIONS depending on your device.

## Troubleshooting

### Mouse lag

If you experience mouse lag you can try to increase the polling rate. See [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate") for more information.

### Problems with the USB dongle

If you have trouble with your USB dongle, you may also want to try:

```
# modprobe -v rfcomm

```

At this point, you should get an hci0 device with:

```
# hcitool dev

```

Sometimes the device is not active right away. Try starting the interface with:

```
# hciconfig hci0 up

```

and searching for devices as shown above.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bluetooth_mouse&oldid=394963](https://wiki.archlinux.org/index.php?title=Bluetooth_mouse&oldid=394963)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Mice](/index.php/Category:Mice "Category:Mice")
*   [Bluetooth](/index.php/Category:Bluetooth "Category:Bluetooth")