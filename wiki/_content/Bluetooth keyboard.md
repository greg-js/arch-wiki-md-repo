# Bluetooth keyboard

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article describes how to set up a Bluetooth HID keyboard with Arch Linux, bluez version 5.

## Contents

*   [1 Pairing process](#Pairing_process)
*   [2 Manually enabling a Bluetooth Keyboard](#Manually_enabling_a_Bluetooth_Keyboard)
*   [3 Automatically enabling a Bluetooth Keyboard](#Automatically_enabling_a_Bluetooth_Keyboard)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 Xorg](#Xorg)

## Pairing process

Login to the affected computer by a wired keyboard or by ssh.

First, make sure the local BT controller (e.g. a BT dongle the built in BT radio) is recognized:

 `# lsusb` 

```
Bus 001 Device 004: ID 0a12:0001 Cambridge Silicon Radio, Ltd Bluetooth Dongle (HCI mode)
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
Bus 001 Device 002: ID 0424:9512 Standard Microsystems Corp. LAN9500 Ethernet 10/100 Adapter / SMSC9512/9514 Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

```

The above output is from a Raspberry-Pi revision 'B' with archlinux-arm and a Keysonic BT Dongle.

Start bluetooth service with _systemctl_, or even better, enable it permanently in the start up process. See [systemd](/index.php/Systemd "Systemd").

Three items worth remembering:

*   BT devices (keyboard) and controllers (dongle) need to be paired once.
*   The BT controller needs to be powered up after every boot.
*   The BT controller needs to be told to connect to the keyboard after every boot.

_Pairing_ is a one time process, required only once. There are BT keyboards sold with a BT dongle which come already paired, but that's not certain. We will use the `bluetoothctl` command from bluez5 to pair our dongle and the keyboard.

_Power up_ can be done with `bluetoothctl`, or with `hciconfig` which is more suitable for scripting. See below.

Same for _connecting_, either `bluetoothctl` or `hcitool` can be used, the latter is more useful for scripting.

We will use `bluetoothctl` for the pairing process:

 `# bluetoothctl -a` 

```
[bluetooth]#

```

puts you at the `[bluetooth]#` prompt. If you are on a colour console: the word "bluetooth" is in the default colour as long as no devices are available, and blue as soon as required devices and/or controllers have been found.

While in _bluetoothctl_ power up the controller:

 `[bluetooth]# power on` 

```
Changing power on succeeded
[CHG] Controller 06:05:04:03:02:01 Powered: yes

```

Next, tell `bluetoothctl` to look only for keyboards, and make that the default agent:

 `[bluetooth]# agent KeyboardOnly` 

```
Agent registered

```

 `[bluetooth]# default-agent` 

```
Default agent request successful

```

Next, put your controller (the local dongle) in _pairable_ mode:

 `[bluetooth]# pairable on` 

```
Changing pairable on succeeded

```

Next, put your keyboard in an active mode, where it is _discoverable_, i.e. pairable. Some keyboards have a special button for this on the underside, or require a special key combination to be pressed. See the documentation of your keyboard. Please note that this _discoverability_ of a device is time limited, some devices are only visible 30 seconds, other for 2 minutes. Your mileage may vary.

Next, let the controller scan the BT frequencies for a suitable device:

 `[bluetooth]# scan on` 

```
Discovery started
[CHG] Controller 06:05:04:03:02:01 Discovering: yes

```

After a few seconds the adress of the keyboard should be listed as found. This line will repeat over and over, but won't stop you from entering new commands.

Next, actually do the pairing. The address used is the BT-MAC address of the keyboard:

 `[bluetooth]# pair 01:02:03:04:05:06` 

```
Pairing successful

```

Next, make this a trusted device (this allows the device to establish the connection on itself). Again, the BT-MAC address is the address of the keyboard device:

 `[bluetooth]# trust 01:02:03:04:05:06` 

```
Trusted 

```

Next and finally connect to the device (keyboard). Again, the BT-MAC address is the address of the keyboard device:

 `[bluetooth]# connect 01:02:03:04:05:06` 

```
Connection successful

```

Done. Leave the `bluetoothctl` utility:

```
[bluetooth]# quit

```

Now the external device (i.e. keyboard) and the USB BT dongle are paired permanently, unless you break the pairing intenionally. This does not mean that the keyboard will connect automatically to your BT device after a boot. _Power up_ of the controller and _connecting_ device and controller needs to be done after every startup of your computer.

## Manually enabling a Bluetooth Keyboard

Although the device and the controller are now paired (see above), you need to connect them every time the computer starts.

First the BT controller (i.e. BT Dongle) needs to be powered up. This is done with the `hciconfig` utility. We assume that you have only one BT device connected, and this one has the symbolic name `hci0`.

```
# hciconfig hci0 up

```

Next, make the connection, now using the `hcitool` utility. Make sure that the keyboard is powered up and connectable, i.e. not in a power saving sleep state.

```
# hcitool cc 01:02:03:04:05:06

```

Your BT keyboard should be useable now, even if an error message ("Can't create connection: Input/output error") is shown. Next we will discuss how to automate this process with [systemd](/index.php/Systemd "Systemd").

## Automatically enabling a Bluetooth Keyboard

Remember that you have to pair and trust your device in bluetoothctl to cause autoconnect. Then you can power up your adapter automatically in several ways:

**Custom systemd service file:**

Create a config file `/etc/btkbd.conf`

```
# Config file for btkbd.service
# change when required (e.g. keyboard hardware changes, more hci devices are connected)
BTKBDMAC = ''mac_address_of_your_device''
HCIDEVICE = ''hci_device_identifier''

```

`_mac_address_of_your_device_` can be found with the `scan on` command of the _bluetoothctl_ utility.

`_hci_device_identifier_` can be found with:

 `# hcitool dev` 

```
Devices:
   hci0   06:05:04:03:02:01

```

We are looking for the identifier `hci0` in this case. The MAC address shown here is the address of the controller, not the address of the keyboard itself.

Next, create a new service file at `/etc/systemd/system/btkbd.service`.

```
[Unit]
Description=systemd Unit to automatically start a Bluetooth keyboard
Documentation=https://wiki.archlinux.org/index.php/Bluetooth_Keyboard
Requires=dbus-org.bluez.service
After=dbus-bluez.org.service
ConditionPathExists=/etc/btkbd.conf
ConditionPathExists=/usr/bin/hcitool
ConditionPathExists=/usr/bin/hciconfig

[Service]
Type=oneshot
EnvironmentFile=/etc/btkbd.conf
ExecStart=
ExecStart=/usr/bin/hciconfig ${HCIDEVICE} up
# ignore errors on connect, spurious problems with bt? so start next command with -
ExecStart=-/usr/bin/hcitool cc ${BTKBDMAC}

[Install]
WantedBy=multi-user.target

```

And then enable this service with systemd's tools.

Or **udev rule:**

Create new file `/etc/udev/rules.d/10-local.rules`

```
# Set bluetooth power up
ACTION=="add", KERNEL=="hci0", RUN+="/usr/bin/hciconfig hci0 up"

```

## Troubleshooting

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** TBD (Discuss in [Talk:Bluetooth keyboard#](https://wiki.archlinux.org/index.php/Talk:Bluetooth_keyboard))

*   What if the BT controller does not show up in `lsusb` ?
*   What if the BT controller is not visible in `bluetoothctl` ?
*   My BT keyboard still does not work. What to do?
    *   Check: Does it have power?
    *   Check: Did it connect to the BT controller? If not, try with another controller or your smart phone.

## Xorg

Device should be added as `/dev/input/event*` and your Xorg should add it automatically if you did not disable such feature.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bluetooth_keyboard&oldid=383061](https://wiki.archlinux.org/index.php?title=Bluetooth_keyboard&oldid=383061)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Bluetooth](/index.php/Category:Bluetooth "Category:Bluetooth")
*   [Keyboards](/index.php/Category:Keyboards "Category:Keyboards")

Hidden category:

*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")