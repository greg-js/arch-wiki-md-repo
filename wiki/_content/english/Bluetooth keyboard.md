This article describes how to set up a [Bluetooth](/index.php/Bluetooth "Bluetooth") HID keyboard with Arch Linux, [bluez](https://www.archlinux.org/packages/?name=bluez) version 5.

## Contents

*   [1 Pairing process](#Pairing_process)
*   [2 Legacy method for auto-connect](#Legacy_method_for_auto-connect)
    *   [2.1 Manually enabling a Bluetooth Keyboard](#Manually_enabling_a_Bluetooth_Keyboard)
    *   [2.2 Automatically enabling a Bluetooth Keyboard](#Automatically_enabling_a_Bluetooth_Keyboard)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 Xorg](#Xorg)

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

Three items worth remembering:

*   BT devices (keyboard) and controllers (dongle) need to be paired once.
*   The BT controller needs to be powered up after every boot.
*   The BT controller needs to be told to connect to the keyboard after every boot.

*Pairing* is a one time process, required only once. There are BT keyboards sold with a BT dongle which come already paired, but that's not certain. We will use the `bluetoothctl` command from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) to pair our dongle and the keyboard.

*Power up* can be done with `bluetoothctl`, or automatically in `/etc/bluetooth/main.conf`, see below.

Same for *connecting*, either `bluetoothctl` or `hcitool` can be used, the latter is more useful for scripting.

We will use `bluetoothctl` for the pairing process. Run the command to get at the `[bluetooth]#` prompt.

 `# bluetoothctl` 
```
[bluetooth]#

```

**Note:** If you are on a color console: the word "bluetooth" is in the default color as long as no devices are available, and blue as soon as required devices and/or controllers have been found.

While in *bluetoothctl* power up the controller:

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

Next, put your controller (the local dongle) in *pairable* mode:

 `[bluetooth]# pairable on` 
```
Changing pairable on succeeded

```

Next, put your keyboard in an active mode, where it is *discoverable*, i.e. pairable. Some keyboards have a special button for this on the underside, or require a special key combination to be pressed. See the documentation of your keyboard. Please note that this *discoverability* of a device is time limited, some devices are only visible 30 seconds, other for 2 minutes. Your mileage may vary.

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

**Note:** Some keyboards, such as Microsoft Surface Ergonomic, will send a pass code (e.g. "[agent] Passkey: 501334") which has to be typed in on the bluetooth keyboard followed by the key Enter in order to pair successfully. Use "paired-devices" command to double check if the pairing succeeded.

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

Now the external device (i.e. keyboard) and the USB BT dongle are paired permanently, unless you break the pairing intentionally. This does not mean that the keyboard will connect automatically to your BT device after a boot. This is mainly due to the fact that the bluetooth controller will be automatically turned off after each reboot. So, to automatically connect the keyboard after a reboot, configure your bluetooth to be powered on automatically. To do so, add the line `AutoEnable=true` in `/etc/bluetooth/main.conf` at the bottom of the `[Policy]` section, see [Bluetooth#Configuration via the CLI](/index.php/Bluetooth#Configuration_via_the_CLI "Bluetooth"):

 `/etc/bluetooth/main.conf` 
```
[Policy]
AutoEnable=true
```

## Legacy method for auto-connect

Before Bluez added the feature to automatically power on the bluetooth controller after a reboot, it was necessary to run two commands manually or automatically via a systemd service or a udev rule to *Power up* the controller and *connect* device and controller. In the following, those legacy methods are demonstrated if the new method yields any problems.

### Manually enabling a Bluetooth Keyboard

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

### Automatically enabling a Bluetooth Keyboard

Remember that you have to pair and trust your device in bluetoothctl to cause autoconnect. Then you can power up your adapter automatically in several ways:

**Custom systemd service file:**

Create a config file `/etc/btkbd.conf`

```
# Config file for btkbd.service
# change when required (e.g. keyboard hardware changes, more hci devices are connected)
BTKBDMAC = ''mac_address_of_your_device''
HCIDEVICE = ''hci_device_identifier''

```

`*mac_address_of_your_device*` can be found with the `scan on` command of the *bluetoothctl* utility.

`*hci_device_identifier*` can be found with:

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
ConditionPathExists=/etc/btkbd.conf
ConditionPathExists=/usr/local/bin/hcitool
ConditionPathExists=/usr/local/sbin/hciconfig

[Service]
Type=oneshot
EnvironmentFile=/etc/btkbd.conf
ExecStart=
ExecStart=/usr/local/sbin/hciconfig ${HCIDEVICE} up
# ignore errors on connect, spurious problems with bt? so start next command with -
ExecStart=-/usr/local/bin/hcitool cc ${BTKBDMAC}

[Install]
WantedBy=bluetooth.target

```

And then enable this service with systemd's tools.

Or **udev rule:**

Create new file `/etc/udev/rules.d/10-local.rules`

```
# Set bluetooth power up
ACTION=="add", KERNEL=="hci0", RUN+="/usr/bin/hciconfig hci0 up"

```

## Troubleshooting

What if the BT controller does not show up in `lsusb` ?

*   Load generic bluetooth driver:

```
# modprobe btusb

```

*   Is it an USB adapter or integral to the system? Use `lspci` for integral adapters

What if the BT controller is not visible in `bluetoothctl` ?

*   Check: `bluetoothctl` is started:

```
systemctl status bluetooth

```

*   Check: You run the command with superuser privileges using `su` or `sudo`. Otherwise you have blue *[bluetooth]#* prompt and get the following message when powering on the controller:

```
[bluetooth]# power on
No default controller available

```

My BT keyboard still does not work. What to do?

*   Check: Does it have power?
*   Check: Did it connect to the BT controller? If not, try with another controller or your smart phone.

All went fine but when I type I'm getting "Bluetooth: hci0 ACL packet for unknown connection handle 4"

*   Try reset: hciconfig hci0 reset

## Xorg

Device should be added as `/dev/input/event*` and your Xorg should add it automatically if you did not disable such feature.