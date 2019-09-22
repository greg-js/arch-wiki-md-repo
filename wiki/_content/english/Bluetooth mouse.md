Related articles

*   [Bluetooth](/index.php/Bluetooth "Bluetooth")
*   [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate")

This article describes configuration & troubleshooting steps specific to Bluetooth mice. The information here builds on the main [Bluetooth](/index.php/Bluetooth "Bluetooth") article, and assumes the user has already followed any installation, configuration, or troubleshooting from that article.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Apple Magic Mouse scroll speed](#Apple_Magic_Mouse_scroll_speed)
    *   [1.2 Apple Magic Mouse middle click](#Apple_Magic_Mouse_middle_click)
    *   [1.3 Mouse pairing and dual boot](#Mouse_pairing_and_dual_boot)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Mouse lag](#Mouse_lag)
    *   [2.2 Problems with the USB dongle](#Problems_with_the_USB_dongle)
    *   [2.3 Mouse always disconnect](#Mouse_always_disconnect)
    *   [2.4 Thinkpad Bluetooth Laser Mouse problems](#Thinkpad_Bluetooth_Laser_Mouse_problems)
    *   [2.5 Problems with the Logitech BLE mouse (M557, M590, anywhere mouse 2, etc)](#Problems_with_the_Logitech_BLE_mouse_(M557,_M590,_anywhere_mouse_2,_etc))
*   [3 See Also](#See_Also)

## Configuration

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

if using a Bluetooth LE device use [this](https://gist.github.com/5shekel/8b4998a69903438a6aac2f01a44463d3) python script, slightly edited to adapt for arch, originally discussed [here](https://unix.stackexchange.com/a/413831/43422).

## Troubleshooting

### Mouse lag

If you experience mouse lag you can try to increase the polling rate. See [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate") for more information.

You can try to set the minimum/maximum latency for the mouse in BlueZ [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1860951#p1860951):

Add or modify the following section in `/var/lib/bluetooth/<mac-of-your-adapter>/<mac-of-your-mouse>/info` (adapt the path accordingly):

```
[ConnectionParameters]
MinInterval=6
MaxInterval=9
Latency=44
Timeout=216

```

Also, you can use `hcitool` (in [bluez-hcitool](https://aur.archlinux.org/packages/bluez-hcitool/)) to change latency parameters of the device:

```
# HANDLE="$(hcitool con | grep '<Bluetooth Mouse mac address>' | awk '{print $5}')"  # get the device handle
# hcitool lecup --handle $HANDLE --latency 0 --min 6 --max 8

```

Note that this method is only effective for the current connection. If the mouse gets disconnected, you'll need to execute again.

Alternatively, you can change the default latency settings via debugfs. See `/sys/kernel/debug/bluetooth/hci0/conn_{latency,{min,max}_interval}` .

This example will solve the lag problems, but you must un pair and pair the mouse:

```
# echo 0 > /sys/kernel/debug/bluetooth/hci0/conn_latency
# echo 6 > /sys/kernel/debug/bluetooth/hci0/conn_min_interval
# echo 7 > /sys/kernel/debug/bluetooth/hci0/conn_max_interval

```

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

The issue may also lie in the device timeout and HID settings. See [#Thinkpad Bluetooth Laser Mouse problems](#Thinkpad_Bluetooth_Laser_Mouse_problems).

### Thinkpad Bluetooth Laser Mouse problems

If you are experiencing that your Thinkpad Bluetooth Laser Mouse rapidly connects and then (after a few milliseconds) disconnects again every few seconds (when you move the mouse or press a button), try pairing it with the code `0000` instead pairing without a code.

If the above is unhelpful, the issue may be in the device timeout settings. Edit/create the file `/etc/bluetooth/input.conf` and apply the following changes:

```
# Configuration file for the input service
# This section contains options which are not specific to any
# particular interface
[General]

# Set idle timeout (in minutes) before the connection will
# be disconnect (defaults to 0 for no timeout)
IdleTimeout=0

#Enable HID protocol handling in userspace input profile
#Defaults to false(hidp handled in hidp kernel module)
UserspaceHID=true

```

These changes will prevent device timeout in order to remain connected. The second setting enables userspace HID handling for bluetooth devices. Restart `bluetooth.service` to test changes. You also may need a reboot and to re-pair the device.

### Problems with the Logitech BLE mouse (M557, M590, anywhere mouse 2, etc)

In some case, the mouse is paired but not moving when used. The device add to be trusted and unblocked. First of all open a terminal and run `bluetoothctl`

1.  Power off the bluetooth: `[bluetooth] # power off` 
2.  Power on the bluetooth, then enable the pairing method on the mouse if needed" `[bluetooth] # power on` 
3.  List the available bluetooth devices, you have to copy the mouse device ID *XX:XX:XX:XX:XX:XX*: `[bluetooth] # scan on` 
4.  Unpair the device if already paired: `[bluetooth] # remove *XX:XX:XX:XX:XX:XX*` 
5.  **Trust** the device: `[bluetooth] # trust *XX:XX:XX:XX:XX:XX*` 
6.  Pair the mouse with the computer: `[bluetooth] # pair *XX:XX:XX:XX:XX:XX*` 
7.  Connect the computer with the mouse: `[bluetooth] # connect *XX:XX:XX:XX:XX:XX*` 
8.  **Unblock** the device control: `[M585/M590] # unblock` 
9.  Power the bluetooth off and on.

If the mouse does not work directly, just power off and power on the mouse.

## See Also

*   [BlueZ settings storage](https://git.kernel.org/pub/scm/bluetooth/bluez.git/tree/doc/settings-storage.txt)