This article describes how to set up a [Bluetooth](/index.php/Bluetooth "Bluetooth") mouse through the command line without relying upon a graphical application.

## Contents

*   [1 Installation](#Installation)
*   [2 Bluez5 instructions](#Bluez5_instructions)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Mouse lag](#Mouse_lag)
    *   [3.2 Problems with the USB dongle](#Problems_with_the_USB_dongle)

## Installation

Install the [bluez](https://www.archlinux.org/packages/?name=bluez) package which contains the current Linux bluetooth stack (Bluez5). You may also want to install [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) which provides the *bluetoothctl* utility. See [Bluetooth](/index.php/Bluetooth "Bluetooth") for more information.

## Bluez5 instructions

**Tip:** Ensure that the bluetooth daemon is started before continuing.

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