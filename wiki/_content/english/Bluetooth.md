Related articles

*   [Bluez4](/index.php/Bluez4 "Bluez4")
*   [Bluetooth mouse](/index.php/Bluetooth_mouse "Bluetooth mouse")
*   [Bluetooth keyboard](/index.php/Bluetooth_keyboard "Bluetooth keyboard")
*   [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset")
*   [Blueman](/index.php/Blueman "Blueman")

[Bluetooth](http://www.bluetooth.org/) is a standard for the short-range wireless interconnection of cellular phones, computers, and other electronic devices. In Linux, the canonical implementation of the Bluetooth protocol stack is [BlueZ](http://www.bluez.org/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration via the CLI](#Configuration_via_the_CLI)
    *   [2.1 Bluetoothctl](#Bluetoothctl)
        *   [2.1.1 Auto power-on after boot](#Auto_power-on_after_boot)
*   [3 Configuration with a graphical front-end](#Configuration_with_a_graphical_front-end)
    *   [3.1 GNOME Bluetooth](#GNOME_Bluetooth)
    *   [3.2 Bluedevil](#Bluedevil)
    *   [3.3 Blueberry](#Blueberry)
    *   [3.4 Blueman](#Blueman)
*   [4 Using Obex for sending and receiving files](#Using_Obex_for_sending_and_receiving_files)
    *   [4.1 ObexFS](#ObexFS)
    *   [4.2 ObexFTP transfers](#ObexFTP_transfers)
    *   [4.3 Obex Object Push](#Obex_Object_Push)
*   [5 Audio](#Audio)
    *   [5.1 Using your computer's speakers as a bluetooth headset](#Using_your_computer.27s_speakers_as_a_bluetooth_headset)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Shell command _____ is missing from bluez-utils](#Shell_command_is_missing_from_bluez-utils)
    *   [6.2 gnome-bluetooth](#gnome-bluetooth)
    *   [6.3 Bluetooth USB Dongle](#Bluetooth_USB_Dongle)
        *   [6.3.1 Audio devices start to skip at short distance from dongle](#Audio_devices_start_to_skip_at_short_distance_from_dongle)
    *   [6.4 Logitech Bluetooth USB Dongle](#Logitech_Bluetooth_USB_Dongle)
    *   [6.5 hcitool scan: Device not found](#hcitool_scan:_Device_not_found)
    *   [6.6 rfkill unblock: Do not unblock](#rfkill_unblock:_Do_not_unblock)
    *   [6.7 My computer is not visible](#My_computer_is_not_visible)
    *   [6.8 Logitech keyboard does not pair](#Logitech_keyboard_does_not_pair)
    *   [6.9 HSP/HFP profiles](#HSP.2FHFP_profiles)
    *   [6.10 Thinkpad Bluetooth Laser Mouse problems](#Thinkpad_Bluetooth_Laser_Mouse_problems)
    *   [6.11 Foxconn / Hon Hai / Lite-On Broadcom device](#Foxconn_.2F_Hon_Hai_.2F_Lite-On_Broadcom_device)
    *   [6.12 Device connects, then disconnects after a few moments](#Device_connects.2C_then_disconnects_after_a_few_moments)
    *   [6.13 Device does not connect with an error in journal](#Device_does_not_connect_with_an_error_in_journal)
    *   [6.14 Device does not show up in scan](#Device_does_not_show_up_in_scan)

## Installation

[Install](/index.php/Install "Install") the [bluez](https://www.archlinux.org/packages/?name=bluez) and [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) packages. The [bluez](https://www.archlinux.org/packages/?name=bluez) package provides the Bluetooth protocol stack, and the [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) package provides the `bluetoothctl` utility.

The generic Bluetooth driver is the `btusb` Kernel module. [Check](/index.php/Kernel_module#Obtaining_information "Kernel module") whether that module is loaded. If it's not, then [load the module](/index.php/Kernel_module#Manual_module_handling "Kernel module").

Then [start](/index.php/Start "Start") the `bluetooth.service` systemd unit. You can [enable](/index.php/Enable "Enable") it to start automatically at boot time.

**Note:**

*   By default the bluetooth daemon will only give out bnep0 devices to users that are a member of the `lp` group. Make sure to add your user to that group if you intend to connect to a bluetooth tether. You can change the group that is required in the file `/etc/dbus-1/system.d/bluetooth.conf`.
*   Some Bluetooth adapters are bundled with a Wi-Fi card (e.g. [Intel Centrino](http://www.intel.com/content/www/us/en/wireless-products/centrino-advanced-n-6235.html)). These require that the Wi-Fi card is firstly enabled (typically a keyboard shortcut on a laptop) in order to make the Bluetooth adapter visible to the kernel.
*   Some Bluetooth cards (e.g. Broadcom) conflict with the network adapter. Thus, you need to make sure that your Bluetooth device get connected before the network service boot.
*   Some tools such as hcitool and hciconfig have been deprecated upstream, and are no longer included in [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). Since these tools will no longer be updated, it is recommended that scripts be updated to avoid using them. If you still desire to use them, install [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/). See [FS#53110](https://bugs.archlinux.org/task/53110) and [the Bluez mailing list](https://www.spinics.net/lists/linux-bluetooth/msg69239.html) for more information.

## Configuration via the CLI

**Note:** Before using the bluetooth device, make sure that it is not blocked by [rfkill](/index.php/Rfkill "Rfkill").

### Bluetoothctl

Pairing a device from the shell is one of the simplest and most reliable options. The exact procedure depends on the devices involved and their input functionality. What follows is a general outline of pairing a device using `/usr/bin/bluetoothctl`:

Start the `bluetoothctl` interactive command. Input `help` to get a list of available commands.

*   Possibly select a default controller by inputting `select *MAC Address*`
*   Turn the power to the controller on by entering `power on`. It is off by default and will turn off again each reboot, see [#Auto power-on after boot](#Auto_power-on_after_boot).
*   Enter `devices` to get the MAC Address of the device with which to pair.
*   Enter device discovery mode with `scan on` command if device is not yet on the list.
*   Turn the agent on with `agent on` or choose a specific agent: if you press tab twice after `agent` you should see a list of available agents, e.g. DisplayOnly KeyboardDisplay NoInputNoOutput DisplayYesNo KeyboardOnly off on.
*   Enter `pair *MAC Address*` to do the pairing (tab completion works).
*   If using a device without a PIN, one may need to manually trust the device before it can reconnect successfully. Enter `trust *MAC Address*` to do so.
*   Finally, use `connect *MAC_address*` to establish a connection.

An example session may look this way:

```
# bluetoothctl 
[NEW] Controller 00:10:20:30:40:50 pi [default]
[bluetooth]# agent KeyboardOnly 
Agent registered
[bluetooth]# default-agent 
Default agent request successful
[bluetooth]# power on
Changing power on succeeded
[CHG] Controller 00:10:20:30:40:50 Powered: yes
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
[bluetooth]# connect 00:12:34:56:78:90
Attempting to connect to 00:12:34:56:78:90
[CHG] Device 00:12:34:56:78:90 Connected: yes
Connection successful

```

#### Auto power-on after boot

By default, your Bluetooth adapter will not power on after a reboot. The former method by using `hciconfig hci0 up` is deprecated, see the [release note](http://www.bluez.org/release-of-bluez-5-35/). Now you just need to add the line `AutoEnable=true` in `/etc/bluetooth/main.conf` at the bottom in the `[Policy]` section:

 `/etc/bluetooth/main.conf` 
```
[Policy]
AutoEnable=true
```

## Configuration with a graphical front-end

The following packages allow for a graphical interface to customize Bluetooth.

### GNOME Bluetooth

[GNOME Bluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) is [GNOME](/index.php/GNOME "GNOME")'s Bluetooth tool. The [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) package provides the back-end, [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) provides the status monitor applet, and [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) provides the configuration front-end GUI that can be accessed by typing Bluetooth on the Activities overview, or with the `gnome-control-center bluetooth` command. You can also launch the `bluetooth-sendto` command directly to send files to a remote device.

To receive files, open the Bluetooth settings panel; you can only receive whilst the Bluetooth panel is open.

**Tip:** To add a Bluetooth entry to the *Send To* menu in Thunar's file properties menu, see instructions [here](http://docs.xfce.org/xfce/thunar/send-to). (The command that needs to be configured is `bluetooth-sendto %F`).

### Bluedevil

[Bluedevil](https://projects.kde.org/projects/kde/workspace/bluedevil) is [KDE](/index.php/KDE "KDE")'s Bluetooth tool. It can be [installed](/index.php/Installed "Installed") with the package [bluedevil](https://www.archlinux.org/packages/?name=bluedevil) (KDE Plasma 5).

If there is no Bluetooth icon visible in Dolphin and in the system tray, enable it in the system tray options or add a widget. You can configure Bluedevil and detect Bluetooth devices by clicking the icon. An interface is also available from the KDE System Settings.

### Blueberry

*Blueberry* is an alternative front-end for GNOME Bluetooth, which works in all desktop environments. It can be installed with the [blueberry](https://www.archlinux.org/packages/?name=blueberry) package. It provides a configuration tool (*blueberry*) and a system tray applet (*blueberry-tray*).

**Note:** *Blueberry* doesn't support receiving files through Obex Object Push, see *blueman* below if you want to be able to receive files.

### Blueman

[Blueman](/index.php/Blueman "Blueman") is a full featured Bluetooth manager. It provides a graphical settings panel `blueman-manager` and a system tray applet `blueman-applet`. See [Blueman](/index.php/Blueman "Blueman") for more details.

## Using Obex for sending and receiving files

### ObexFS

Another option, rather than using KDE or Gnome Bluetooth packages, is ObexFS which allows for the mounting of phones which are treated like any other filesystem.

**Note:** To use ObexFS, one needs a device that provides an ObexFTP service.

Install [obexfs](https://aur.archlinux.org/packages/obexfs/) and mount supported phones by running:

```
$ obexfs -b *MAC_address_of_device* /mountpoint

```

Once you have finished, to unmount the device use the command:

```
$ fusermount -u /mountpoint

```

For more mounting options see [http://dev.zuckschwerdt.org/openobex/wiki/ObexFs](http://dev.zuckschwerdt.org/openobex/wiki/ObexFs)

**Note:** Ensure that the bluetooth device you are mounting is **not** set to mount *read-only*. You should be able to do this from the device's settings. If the device is mounted *read-only* you may encounter a permissions error when trying to transfer files to the device.

### ObexFTP transfers

If your device supports the Obex FTP service but you do not wish to mount the device you can transfer files to and from the device using the obexftp command.

To send a file to a device run the command:

```
$ obexftp -b *MAC_address_of_device* -p /path/to/file

```

To retrieve a file from a device run the command:

```
$ obexftp -b *MAC_address_of_device* -g filename

```

**Note:** Ensure that the file you are retrieving is in the device's *exchange folder*. If the file is in a subfolder of the exchange folder then provide the correct path in the command.

### Obex Object Push

For devices that do not support Obex FTP service, check if Obex Object Push is supported.

```
# sdptool browse *XX:XX:XX:XX:XX:XX*

```

Read the output, look for Obex Object Push, remember the channel for this service. If supported, one can use [ussp-push](https://aur.archlinux.org/packages/ussp-push/) to send files to this device:

```
# ussp-push *XX:XX:XX:XX:XX:XX*@*CHANNEL* *file* *wanted_file_name_on_phone*

```

## Audio

In order to be able to use audio equipment like bluetooth headphones or speakers, you need to install the additional [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) package.

Please have a look at the [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset") page for more information about bluetooth audio and bluetooth headsets.

### Using your computer's speakers as a bluetooth headset

In order to enable your system to be detected as an A2DP sink (e.g. to play music from your phone via your computer speakers), add the following to the file `/etc/bluetooth/audio.conf` (create it if not present):

```
[General]
Enable=Source

```

More info in:

*   [https://gist.github.com/joergschiller/1673341](https://gist.github.com/joergschiller/1673341)
*   [http://www.lightofdawn.org/blog/?viewDetailed=00031](http://www.lightofdawn.org/blog/?viewDetailed=00031)

## Troubleshooting

### Shell command _____ is missing from bluez-utils

Some tools have been marked as deprecated and removed from the package. At this time they are still available in the AUR package [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/). Their functionality is partially covered by new tools, while some things have yet to be implemented with the new [D-Bus API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/):

| Deprecated tool | Most likely replacement |
| gatttool | btgatt-client, [D-Bus Gatt API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/gatt-api.txt) |
| hciattach | btattach |
| hciconfig | btmgmt (and bluetoothctl?) |
| hcidump | btmon (and btsnoop) |
| hcitool | missing, [D-Bus Device API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt) available |
| rfcomm | missing, implement with [D-Bus Profile1 API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/profile-api.txt)? |
| ciptool |
| sdptool | missing, functionality seems to be scattered over different D-Bus objects: [Profile](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/profile-api.txt), [Advertising](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/advertising-api.txt), and the UUIDs arrays in [device](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt) and [adapter](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/adapter-api.txt). |

### gnome-bluetooth

If you see this when trying to enable receiving files in bluetooth-properties:

```
Bluetooth OBEX start failed: Invalid path
Bluetooth FTP start failed: Invalid path

```

Then make sure that the [XDG user directories](/index.php/XDG_user_directories "XDG user directories") exist.

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

#### Audio devices start to skip at short distance from dongle

If other devices share the same USB host, they can [interrupt communication with audio devices](https://bbs.archlinux.org/viewtopic.php?pid=1440161#p1440161). Make sure it is the only device attached to its bus. For example:

 `$ lsusb` 
```
Bus 002 Device 002: ID 0a12:0001 Cambridge Silicon Radio, Ltd Bluetooth Dongle (HCI mode)
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 004: ID 048d:1345 Integrated Technology Express, Inc. Multi Cardreader
Bus 001 Device 003: ID 0424:a700 Standard Microsystems Corp. 2 Port Hub
Bus 001 Device 002: ID 8087:0024 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

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

### Foxconn / Hon Hai / Lite-On Broadcom device

Some of these devices require the firmware to be flashed into the device at boot. The firmware is not provided but can converted from a Microsoft Windows *.hex* file into a *.hcd* using [hex2hcd](https://github.com/jessesung/hex2hcd) (which is installed with [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)).

In order to get the right *.hex* file, try searching the device vendor:product code obtained with *lsusb*, for example:

```
   ...
   Bus 002 Device 004: ID **04ca:2006** Lite-On Technology Corp. Broadcom BCM43142A0 Bluetooth Device
   ...

```

or

```
   Bus 004 Device 004: Id **0489:e031** Foxconn / Hon Hai

```

Alternatively, boot into Windows (a virtual machine installation will suffice) and get the firmware name from the Device Manager utility. If you want to know the model of your device but cannot see it in *lsusb*, you might see it in *lsusb -v* as `iProduct`.

The *.hex* file can be extracted from the downloaded Windows driver without having to run Windows for it. Download the right driver, for example [Bluetooth Widcomm](http://www.fujitsupc.com/downloads/mobile/BLUETOOTH_WIDCOMM_V6.5.0.3100_WIN7-32_FPC46-1771-01.EXE) (listed among the drivers for [Lifebook P771](http://support.fujitsupc.com/CS/Portal/supportsearch.do?srch=DOWNLOADS&Series=P%20Series&Model=P771&ProductType=Notebook%20PC)), which contains the drivers for many Broadcomm devices. In case of Bluetooth Widcomm, the driver is a self-extracting RAR archive, so it can be extracted using *[unrar](https://www.archlinux.org/packages/?name=unrar) x*. To find out which of the many *.hex* files is the right one for you, look in the file `Win32/bcbtums-win7x86-brcm.inf` and search for `[RAMUSB**E031**.CopyList]`, where `E031` should be replaced with the product code (the second hex number in *lsusb*) of your device in upper-case. Underneath you should see the file name of the right *.hex* file.

Once you have the *.hcd* file, copy it into `/lib/firmware/brcm/BCM.hcd` - this filename is suggested by `dmesg` and it may change in your case so check your *dmesg* output in order to verify. Then reload the *btusb* module:

```
# rmmod btusb
# modprobe btusb

```

In some cases (with older kernels?), you have to flash the *.hcd* file with the *brcm_patchram_plus* utility, provided by [brcm_patchram_plus-git](https://aur.archlinux.org/packages/brcm_patchram_plus-git/). First, make sure in *dmesg* that the device is recognized by *btusb* as a bluetooth device. Then, run the following (replace *04ca 2006* with your vendor product pair):

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

### Device connects, then disconnects after a few moments

If you see messages like the following in `journalctl` output, and your device fails to connect or disconnects shortly after connecting:

```
bluetoothd: Unable to get connect data for Headset Voice gateway: getpeername: Transport endpoint is not connected (107)
bluetoothd: connect error: Connection refused (111)

```

This may be because you have already paired the device with another operating system using the same bluetooth adapter (e.g., dual-booting). Some devices can't handle multiple pairings associated with the same MAC address (i.e., bluetooth adapter). You can fix this by re-pairing the device. Start by removing the device:

```
$ bluetoothctl
[bluetooth]# devices
Device XX:XX:XX:XX:XX:XX My Device
[bluetooth]# remove XX:XX:XX:XX:XX:XX

```

Then [restart](/index.php/Restart "Restart") `bluetooth.service`, turn on your bluetooth adapter, make your device discoverable, re-scan for devices, and re-pair your device. Depending on your bluetooth manager, you may need to perform a full reboot in order to re-discover the device.

### Device does not connect with an error in journal

If you see a message like the following in `journalctl` output while trying to connect to a device:

```
a2dp-source profile connect failed for 9C:64:40:22:E1:3F: Protocol not available

```

try installing [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) and restarting pulseaudio. This error can manifest even while using only file transfer.

### Device does not show up in scan

Some devices using bluetooth low energy do not appear when scanning with bluetoothctl, for example the Logitech MX Master. The simplest way I've found to connect them is by installing [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/), then [start](/index.php/Start "Start") `bluetooth.service` and do:

```
# bluetoothctl
[NEW] Controller (MAC) myhostname [default]
[bluetooth]# power on
[CHG] Controller (MAC) Class: 0x0c010c
Changing power on succeeded
[CHG] Controller (MAC) Powered: yes
[bluetooth]# scan on
Discovery started
[CHG] Controller (MAC) Discovering: yes

```

In another terminal:

```
# hcitool lescan

```

Wait until your device shows up, then Ctrl+C hcitool. bluetoothctl should now see your device and pair normally.