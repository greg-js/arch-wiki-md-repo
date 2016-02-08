# Bluetooth

[Bluetooth](http://www.bluetooth.org/) is a standard for the short-range wireless interconnection of cellular phones, computers, and other electronic devices. In Linux, the canonical implementation of the Bluetooth protocol stack is [BlueZ](http://www.bluez.org/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration via the CLI](#Configuration_via_the_CLI)
    *   [2.1 Bluetoothctl](#Bluetoothctl)
*   [3 Configuration with a graphical front-end](#Configuration_with_a_graphical_front-end)
    *   [3.1 GNOME Bluetooth](#GNOME_Bluetooth)
    *   [3.2 Bluedevil](#Bluedevil)
    *   [3.3 Blueberry](#Blueberry)
    *   [3.4 Blueman](#Blueman)
*   [4 Using Obex for sending and receiving files](#Using_Obex_for_sending_and_receiving_files)
    *   [4.1 ObexFS](#ObexFS)
    *   [4.2 ObexFTP transfers](#ObexFTP_transfers)
    *   [4.3 Obex Object Push](#Obex_Object_Push)
    *   [4.4 Using your computer's speakers as a bluetooth headset](#Using_your_computer.27s_speakers_as_a_bluetooth_headset)
*   [5 Examples](#Examples)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 bluetoothctl](#bluetoothctl_2)
    *   [6.2 gnome-bluetooth](#gnome-bluetooth)
    *   [6.3 Bluetooth USB Dongle](#Bluetooth_USB_Dongle)
    *   [6.4 Logitech Bluetooth USB Dongle](#Logitech_Bluetooth_USB_Dongle)
    *   [6.5 hcitool scan: Device not found](#hcitool_scan:_Device_not_found)
    *   [6.6 rfkill unblock: Do not unblock](#rfkill_unblock:_Do_not_unblock)
    *   [6.7 My computer is not visible](#My_computer_is_not_visible)
    *   [6.8 Logitech keyboard does not pair](#Logitech_keyboard_does_not_pair)
    *   [6.9 HSP/HFP profiles](#HSP.2FHFP_profiles)
    *   [6.10 Thinkpad Bluetooth Laser Mouse problems](#Thinkpad_Bluetooth_Laser_Mouse_problems)
    *   [6.11 Foxconn / Hon Hai / Lite-On Broadcom device](#Foxconn_.2F_Hon_Hai_.2F_Lite-On_Broadcom_device)

## Installation

[Install](/index.php/Install "Install") the [bluez](https://www.archlinux.org/packages/?name=bluez) and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) packages. The [bluez](https://www.archlinux.org/packages/?name=bluez) package provides the Bluetooth protocol stack, and the [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) package provides the `bluetoothctl` utility.

Load the generic bluetooth driver, if not already loaded:

```
# modprobe btusb

```

Then [start](/index.php/Start "Start") the `bluetooth.service` systemd unit. You can [enable](/index.php/Enable "Enable") it to start automatically at boot time.

**Note:**

*   By default the bluetooth daemon will only give out bnep0 devices to users that are a member of the `lp` group. Make sure to add your user to that group if you intend to connect to a bluetooth tether. You can change the group that is required in the file `/etc/dbus-1/system.d/bluetooth.conf`.
*   Some Bluetooth adapters are bundled with a Wi-Fi card (e.g. [Intel Centrino](http://www.intel.com/content/www/us/en/wireless-products/centrino-advanced-n-6235.html)). These require that the Wi-Fi card is first enabled (typically a keyboard shortcut on a laptop) in order to make the Bluetooth adapter visible to the kernel.
*   Some Bluetooth cards (e.g. Broadcom) conflict with the network adapter. Thus, you need to make sure that your Bluetooth device get connected before the network service boot.

## Configuration via the CLI

### Bluetoothctl

Pairing a device from the shell is one of the simplest and most reliable options. The exact procedure depends on the devices involved and their input functionality. What follows is a general outline of pairing a device using `/usr/bin/bluetoothctl`:

Start the `bluetoothctl` interactive command. There one can input `help` to get a list of available commands.

*   Turn the power to the controller on by entering `power on`. It is off by default.
*   Enter `devices` to get the MAC Address of the device with which to pair.
*   Enter device discovery mode with `scan on` command if device is not yet on the list.
*   Turn the agent on with `agent on`.
*   Enter `pair _MAC Address_` to do the pairing (tab completion works).
*   If using a device without a PIN, one may need to manually trust the device before it can reconnect successfully. Enter `trust _MAC Address_` to do so.
*   Finally, use `connect _MAC_address_` to establish a connection.

An example session may look this way:

```
# bluetoothctl 
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent KeyboardOnly 
Agent registered
[bluetooth]# default-agent 
Default agent request successful
[bluetooth]# scan on
Discovery started
[CHG] Controller 00:10:20:30:40:50 Discovering: yes
[NEW] Device 00:12:34:56:78:90 myLino
[CHG] Device 00:12:34:56:78:90 LegacyPairing: yes
[bluetooth]# pair 00:12:34:56:78:90
Attempting to pair with 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
[CHG] Device 00:12:34:56:78:90 Connected: no
[CHG] Device 00:12:34:56:78:90 Connected: yes
Request PIN code
[agent] Enter PIN code: 1234
[CHG] Device 00:12:34:56:78:90 Paired: yes
Pairing successful
[CHG] Device 00:12:34:56:78:90 Connected: no

```

In order to have the device active after a reboot, a udev rule is needed:

 `/etc/udev/rules.d/10-local.rules` 

```
# Set bluetooth power up
ACTION=="add", KERNEL=="hci0", RUN+="/usr/bin/hciconfig hci0 up"
```

After a suspend/resume-cycle, the device can be powered on automatically using a custom _systemd_ service:

 `/etc/systemd/system/bluetooth-auto-power@.service` 

```
[Unit]
Description=Bluetooth auto power on
After=bluetooth.service sys-subsystem-bluetooth-devices-%i.device suspend.target

[Service]
Type=oneshot
ExecStartPre=/usr/bin/sleep 1
ExecStart=/usr/bin/dbus-send --system --type=method_call --dest=org.bluez /org/bluez/%I org.freedesktop.DBus.Properties.Set string:org.bluez.Adapter1 string:Powered variant:boolean:true

[Install]
WantedBy=suspend.target

```

[Enable](/index.php/Enable "Enable") an instance of the unit using your bluetooth device name, for example `bluetooth-auto-power@hci0.service`.

## Configuration with a graphical front-end

The following packages allow for a graphical interface to customize Bluetooth.

### GNOME Bluetooth

[GNOME Bluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) is [GNOME](/index.php/GNOME "GNOME")'s Bluetooth tool. The [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) package provides the back-end, [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) provides the status monitor applet, and [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) provides the configuration front-end GUI that can be accessed by typing Bluetooth on the Activities overview, or with the `gnome-control-center bluetooth` command. You can also launch the `bluetooth-sendto` command directly to send files to a remote device.

To receive files, you must install the [gnome-user-share](https://www.archlinux.org/packages/?name=gnome-user-share) package. You can then go to _Settings -> Sharing_ to authorize receiving files from paired devices over Bluetooth.

**Tip:** To add a Bluetooth entry to the _Send To_ menu in Thunar's file properties menu, see instructions [here](http://docs.xfce.org/xfce/thunar/send-to). (The command that needs to be configured is `bluetooth-sendto %F`).

### Bluedevil

[Bluedevil](https://projects.kde.org/projects/kde/workspace/bluedevil) is [KDE](/index.php/KDE "KDE")'s Bluetooth tool. It can be [installed](/index.php/Installed "Installed") with the package [bluedevil](https://www.archlinux.org/packages/?name=bluedevil) (KDE Plasma 5).

If there is no Bluetooth icon visible in Dolphin and in the system tray, enable it in the system tray options or add a widget. You can configure Bluedevil and detect Bluetooth devices by clicking the icon. An interface is also available from the KDE System Settings.

### Blueberry

_Blueberry_ is an alternative front-end for GNOME Bluetooth, which works in all desktop environments. It can be installed with the [blueberry](https://www.archlinux.org/packages/?name=blueberry) package. It provides a configuration tool (_blueberry_) and a system tray applet (_blueberry-tray_).

### Blueman

See [Blueman](/index.php/Blueman "Blueman").

## Using Obex for sending and receiving files

### ObexFS

Another option, rather than using KDE or Gnome Bluetooth packages, is ObexFS which allows for the mounting of phones which are treated like any other filesystem.

**Note:** To use ObexFS, one needs a device that provides an ObexFTP service.

Install [obexfs](https://www.archlinux.org/packages/?name=obexfs) and mount supported phones by running:

```
$ obexfs -b _MAC_address_of_device_ /mountpoint

```

Once you have finished, to unmount the device use the command:

```
$ fusermount -u /mountpoint

```

For more mounting options see [http://dev.zuckschwerdt.org/openobex/wiki/ObexFs](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs)

**Note:** Ensure that the bluetooth device you are mounting is **not** set to mount _read-only_. You should be able to do this from the device's settings. If the device is mounted _read-only_ you may encounter a permissions error when trying to transfer files to the device.

### ObexFTP transfers

If your device supports the Obex FTP service but you do not wish to mount the device you can transfer files to and from the device using the obexftp command.

To send a file to a device run the command:

```
$ obexftp -b _MAC_address_of_device_ -p /path/to/file

```

To retrieve a file from a device run the command:

```
$ obexftp -b _MAC_address_of_device_ -g filename

```

**Note:** Ensure that the file you are retrieving is in the device's _exchange folder_. If the file is in a subfolder of the exchange folder then provide the correct path in the command.

### Obex Object Push

For devices that do not support Obex FTP service, check if Obex Object Push is supported.

```
# sdptool browse _XX:XX:XX:XX:XX:XX_

```

Read the output, look for Obex Object Push, remember the channel for this service. If supported, one can use [ussp-push](https://www.archlinux.org/packages/?name=ussp-push) to send files to this device:

```
# ussp-push _XX:XX:XX:XX:XX:XX_@_CHANNEL_ _file_ _wanted_file_name_on_phone_

```

### Using your computer's speakers as a bluetooth headset

This can allow you to do things such as playing what is on your phone through your computer speakers.

Add the following to the file `/etc/bluetooth/audio.conf` (create it if not present):

```
[General]
Enable=Source

```

More info in:

*   [https://gist.github.com/joergschiller/1673341](https://gist.github.com/joergschiller/1673341)
*   [http://www.lightofdawn.org/blog/?viewDetailed=00031](http://www.lightofdawn.org/blog/?viewDetailed=00031)

## Examples

All examples have been moved to the [bluez4](/index.php/Bluez4 "Bluez4") article. They need to be checked and fixed for use with bluez5.

## Troubleshooting

### bluetoothctl

If bluetoothctl cannot find any controller, the bluetooth device may be blocked. Try to unblock it using [rfkill](https://www.archlinux.org/packages/?name=rfkill):

```
# rfkill unblock bluetooth

```

### gnome-bluetooth

If you see this when trying to enable receiving files in bluetooth-properties:

```
Bluetooth OBEX start failed: Invalid path
Bluetooth FTP start failed: Invalid path

```

Then install [xdg-user-dirs](https://www.archlinux.org/packages/?name=xdg-user-dirs) and issue:

```
$ xdg-user-dirs-update

```

You can edit the paths using:

```
$ vi ~/.config/user-dirs.dirs

```

### Bluetooth USB Dongle

If you are using a USB dongle, you should check that your Bluetooth dongle is recognized. You can do that by running `journalctl -f` when you have plugged in the USB dongle (or inspecting `/var/log/messages.log`). It should look something like the following (look out for hci):

```
Feb 20 15:00:24 hostname kernel: [ 2661.349823] usb 4-1: new full-speed USB device number 3 using uhci_hcd
Feb 20 15:00:24 hostname bluetoothd[4568]: HCI dev 0 registered
Feb 20 15:00:24 hostname bluetoothd[4568]: Listening for HCI events on hci0
Feb 20 15:00:25 hostname bluetoothd[4568]: HCI dev 0 up
Feb 20 15:00:25 hostname bluetoothd[4568]: Adapter /org/bluez/4568/hci0 has been enabled

```

If you only get the first two lines, you may see that it found the device but you need to bring it up. Example:

 `hciconfig -a hci0` 

```
hci0:	Type: USB
	BD Address: 00:00:00:00:00:00 ACL MTU: 0:0 SCO MTU: 0:0
	DOWN 
	RX bytes:0 acl:0 sco:0 events:0 errors:0
        TX bytes:0 acl:0 sco:0 commands:0 errors:

```

```
# hciconfig hci0 up

```

 `hciconfig -a hci0` 

```
hci0:	Type: USB
	BD Address: 00:02:72:C4:7C:06 ACL MTU: 377:10 SCO MTU: 64:8
	UP RUNNING 
	RX bytes:348 acl:0 sco:0 events:11 errors:0
        TX bytes:38 acl:0 sco:0 commands:11 errors:0

```

If this fails with an error like:

```
Operation not possible due to RF-kill

```

it could be due either to the `rfkill` utility, in which case it should be resolved with

```
# rfkill unblock all

```

or, it could simply be the hardware switch of the computer. The hardware bluetooth switch (at least sometimes) controls access to USB bluetooth dongles also. Flip/press this switch and try bringing the device up again.

To verify that the device was detected you can use `hcitool` which is part of the `bluez-utils`. You can get a list of available devices and their identifiers and their MAC address by issuing:

 `$ hcitool dev` 

```
Devices:
        hci0	00:1B:DC:0F:DB:40

```

More detailed information about the device can be retrieved by using `hciconfig`.

 `$ hciconfig -a hci0` 

```
hci0:   Type: USB
        BD Address: 00:1B:DC:0F:DB:40 ACL MTU: 310:10 SCO MTU: 64:8
        UP RUNNING PSCAN ISCAN
        RX bytes:1226 acl:0 sco:0 events:27 errors:0
        TX bytes:351 acl:0 sco:0 commands:26 errors:0
        Features: 0xff 0xff 0x8f 0xfe 0x9b 0xf9 0x00 0x80
        Packet type: DM1 DM3 DM5 DH1 DH3 DH5 HV1 HV2 HV3
        Link policy: RSWITCH HOLD SNIFF PARK
        Link mode: SLAVE ACCEPT 
        Name: 'BlueZ (0)'
        Class: 0x000100
        Service Classes: Unspecified
        Device Class: Computer, Uncategorized
        HCI Ver: 2.0 (0x3) HCI Rev: 0xc5c LMP Ver: 2.0 (0x3) LMP Subver: 0xc5c
        Manufacturer: Cambridge Silicon Radio (10)

```

### Logitech Bluetooth USB Dongle

There are Logitech dongles (ex. Logitech MX5000) that can work in two modes: Embedded and HCI. In embedded mode dongle emulates a USB device so it seems to your PC that you are using a normal USB mouse/keyoard.

If you hold the little red Button on the USB BT mini-receiver it will enable the other mode. Hold the red button on the BT dongle and plug it into the computer, and after 3-5 seconds of holding the button, the Bluetooth icon will appear in the system tray. [Discussion](http://ubuntuforums.org/showthread.php?t=1332197)

Alternatively, you can install the [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci) package. When you connect your Logitech dongle it will automatically switch.

### hcitool scan: Device not found

*   On some Dell laptops (e.g. Studio 15) you have to switch the Bluetooth mode from HID to HCI. Install the [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci) package, then [udev](/index.php/Udev "Udev") should do this automatically. Alternatively, you can run this command to switch to HCI manually:

```
# /usr/lib/udev/hid2hci

```

*   If the device will not show up and you have a Windows operating system on your machine, try booting it and enable the bluetooth adapter from windows.

*   Sometimes also this simple command helps:

```
# hciconfig hci0 up

```

### rfkill unblock: Do not unblock

If your device still soft blocked and you run connman, try this:

```
$ connmanctl enable bluetooth

```

### My computer is not visible

Cannot discover computer from your phone? Enable PSCAN and ISCAN:

```
# enable PSCAN and ISCAN
$ hciconfig hci0 piscan 
# check it worked

```

 `$ hciconfig` 

```
hci0:   Type: USB
        BD Address: 00:12:34:56:78:9A ACL MTU: 192:8 SCO MTU: 64:8
        **UP RUNNING PSCAN ISCAN**
        RX bytes:20425 acl:115 sco:0 events:526 errors:0
        TX bytes:5543 acl:84 sco:0 commands:340 errors:0

```

**Note:** Check DiscoverableTimeout and PairableTimeout in `/etc/bluetooth/main.conf`

Try changing device class in `/etc/bluetooth/main.conf` as following:

```
# Default device class. Only the major and minor device class bits are
# considered.
#Class = 0x000100 (from default config)
Class = 0x100100

```

This was the only solution to make my computer visible for my phone.

### Logitech keyboard does not pair

If you do not get the passkey when you try to pair your Logitech keyboard, type the following command:

```
# hciconfig hci0 sspmode 0

```

If after pairing, the keyboard still does not connect, check the output of `hcidump -at`. If the latter indicates repeatedly connections-disconnections like the following message:

```
   status 0x00 handle 11 reason 0x13
   Reason: Remote User Terminated Connection

```

then, the only solution for now is to install [the old Bluetooth stack](/index.php/Bluez4 "Bluez4").

### HSP/HFP profiles

bluez5 removed support for the HSP/HFP profiles (telephony headset for [TeamSpeak](/index.php/TeamSpeak "TeamSpeak"), [Skype](/index.php/Skype "Skype"), etc.). You need to install [PulseAudio](/index.php/PulseAudio "PulseAudio") (>= version 6) or another application that implements HSP/HFP itself.

### Thinkpad Bluetooth Laser Mouse problems

If you are experiencing that your Thinkpad Bluetooth Laser Mouse rapidly connects and then (after a few milliseconds) disconnects again every few seconds (when you move the mouse or press a button), try pairing it with the code `0000` instead pairing without a code.

### Foxconn / Hon Hai / Lite-On Broadcom device

Some of these devices require the firmware to be flashed into the device at boot. The firmware is not provided but can converted from a Microsoft Windows _.hex_ file into a _.hcd_ using [hex2hcd](https://github.com/jessesung/hex2hcd) (which is installed with [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)).

In order to get the right _.hex_ file, try searching the device vendor:product code obtained with _lsusb_, for example:

```
   ...
   Bus 002 Device 004: ID **04ca:2006** Lite-On Technology Corp. Broadcom BCM43142A0 Bluetooth Device
   ...

```

or

```
   Bus 004 Device 004: Id **0489:e031** Foxconn / Hon Hai

```

Alternatively, boot into Windows (a virtual machine installation will suffice) and get the firmware name from the Device Manager utility. If you want to know the model of your device but cannot see it in _lsusb_, you might see it in _lsusb -v_ as `iProduct`.

The _.hex_ file can be extracted from the downloaded Windows driver without having to run Windows for it. Download the right driver, for example [Bluetooth Widcomm](http://www.fujitsupc.com/downloads/mobile/BLUETOOTH_WIDCOMM_V6.5.0.3100_WIN7-32_FPC46-1771-01.EXE) (listed among the drivers for [Lifebook P771](http://support.fujitsupc.com/CS/Portal/supportsearch.do?srch=DOWNLOADS&Series=P%20Series&Model=P771&ProductType=Notebook%20PC)), which contains the drivers for many Broadcomm devices. In case of Bluetooth Widcomm, the driver is a self-extracting RAR archive, so it can be extracted using _[unrar](https://www.archlinux.org/packages/?name=unrar) x_. To find out which of the many _.hex_ files is the right one for you, look in the file `Win32/bcbtums-win7x86-brcm.inf` and search for `[RAMUSB**E031**.CopyList]`, where `E031` should be replaced with the product code (the second hex number in _lsusb_) of your device in upper-case. Underneath you should see the file name of the right _.hex_ file.

Once you have the _.hcd_ file, copy it into `/lib/firmware/brcm/BCM.hcd` - this filename is suggested by `dmesg` and it may change in your case so check your _dmesg_ output in order to verify. Then reload the _btusb_ module:

```
# rmmod btusb
# modprobe btusb

```

In some cases (with older kernels?), you have to flash the _.hcd_ file with the _brcm_patchram_plus_ utility, provided by [brcm_patchram_plus-git](https://aur.archlinux.org/packages/brcm_patchram_plus-git/). First, make sure in _dmesg_ that the device is recognized by _btusb_ as a bluetooth device. Then, run the following (replace _04ca 2006_ with your vendor product pair):

```
# echo '04ca 2006' > /sys/bus/usb/drivers/btusb/new_id

```

Turn on the device:

```
# hciconfig hci0 up

```

Flash the firmware:

```
# brcm_patchram_plus_usb --patchram fw-04ca_2006.hcd hci0

```

The device should now be available. See [BBS#162688](https://bbs.archlinux.org/viewtopic.php?id=162688) for information on making these changes persistent.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bluetooth&oldid=419530](https://wiki.archlinux.org/index.php?title=Bluetooth&oldid=419530)"