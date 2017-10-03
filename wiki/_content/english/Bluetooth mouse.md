Related articles

*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   [Bluez4](/index.php/Bluez4 "Bluez4")
*   [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate")

This article describes how to set up a [Bluetooth](/index.php/Bluetooth "Bluetooth") mouse through the command line without relying upon a graphical application.

## Contents

*   [1 Installation](#Installation)
*   [2 Bluez5 instructions](#Bluez5_instructions)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Mouse lag](#Mouse_lag)
    *   [3.2 Problems with the USB dongle](#Problems_with_the_USB_dongle)
    *   [3.3 Mouse always disconnect](#Mouse_always_disconnect)
    *   [3.4 Apple Magic Mouse scroll speed](#Apple_Magic_Mouse_scroll_speed)
    *   [3.5 Apple Magic Mouse middle click](#Apple_Magic_Mouse_middle_click)
    *   [3.6 Mouse pairing and dual boot](#Mouse_pairing_and_dual_boot)

## Installation

Install the [bluez](https://www.archlinux.org/packages/?name=bluez) package which contains the current Linux bluetooth stack (Bluez5). You may also want to install [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) which provides the *bluetoothctl* utility. See [Bluetooth](/index.php/Bluetooth "Bluetooth") for more information.

## Bluez5 instructions

**Tip:**

*   Ensure that the bluetooth daemon is started before continuing.
*   Ensure that the bluetooth device is not blocked by [rfkill](/index.php/Rfkill "Rfkill").

The *bluetoothctl* utility provides a simple interface for configuring bluetooth devices. The text below is an example of how you can connect a bluetooth mouse using *bluetoothctl*:

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

**Tip:** In case you were using USB Bluetooth dongle and moved it to another USB port, you may need to remove the mouse's MAC address in *bluetoothctl* with *remove <mouse mac>* command and repeat the entire procedure again.

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

### Mouse always disconnect

If the mouse stops working but works again after restarting bluetooth, you may need to [disable USB autosuspend](/index.php/Power_management#USB_autosuspend "Power management") for the selected device.

### Apple Magic Mouse scroll speed

If the scroll speed is too slow, you can try

```
# rmmod hid_magicmouse
# modprobe hid_magicmouse scroll_acceleration=1 scroll_speed=55

```

Scroll speed can be set from 0 to 63.

If the speed suits you, you can make the change permanent in `/etc/modprobe.d/`

 ` /etc/modprobe.d/hid_magicmouse.conf `  `options hid_magicmouse scroll_acceleration=1 scroll_speed=55` 

### Apple Magic Mouse middle click

If you find the middle click to be too finicky, you can disable it

```
# rmmod hid_magicmouse
# modprobe hid_magicmouse emulate_3button=0

```

If this setting suits you, you can make the change permantent in `/etc/modprobe.d/`

 ` /etc/modprobe.d/hid_magicmouse.conf `  `options hid_magicmouse emulate_3button=0` 

### Mouse pairing and dual boot

When dual booting Windows and Linux, you may find yourself having to repair your Bluetooth mouse again and again. This will happen every time you switch OS, because when you pair your device, your Bluetooth service generates a unique set of pairing keys.

First, your computer stores the Bluetooth device's mac address and pairing key. Second, your Bluetooth device stores your computer's mac address and the matching key. This usually works fine, but the mac address for your Bluetooth port will be the same on both Linux and Windows (it is set on the hardware level). However, when you re-pair the device in Windows or Linux, it generates a new key. That key overwrites the previously stored key on the Bluetooth device. Windows overwrites the Linux key and vice versa.

To fix the problem, follow the instructions on [this post at StackExchange](https://unix.stackexchange.com/questions/255509/bluetooth-pairing-on-dual-boot-of-windows-linux-mint-ubuntu-stop-having-to-p).