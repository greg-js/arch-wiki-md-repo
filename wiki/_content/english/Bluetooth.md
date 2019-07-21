Related articles

*   [Bluetooth mouse](/index.php/Bluetooth_mouse "Bluetooth mouse")
*   [Bluetooth keyboard](/index.php/Bluetooth_keyboard "Bluetooth keyboard")
*   [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset")
*   [Blueman](/index.php/Blueman "Blueman")
*   [ObexFTP](/index.php/ObexFTP "ObexFTP")

[Bluetooth](https://en.wikipedia.org/wiki/Bluetooth "wikipedia:Bluetooth") is a standard for the short-range wireless interconnection of cellular phones, computers, and other electronic devices. In Linux, the canonical implementation of the Bluetooth protocol stack is [BlueZ](http://www.bluez.org/).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Front-ends](#Front-ends)
        *   [1.1.1 Console](#Console)
        *   [1.1.2 Graphical](#Graphical)
*   [2 Pairing](#Pairing)
*   [3 Configuration](#Configuration)
    *   [3.1 Auto power-on after boot](#Auto_power-on_after_boot)
*   [4 Audio](#Audio)
*   [5 Bluetooth serial](#Bluetooth_serial)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Deprecated BlueZ tools](#Deprecated_BlueZ_tools)
    *   [6.2 gnome-bluetooth](#gnome-bluetooth)
    *   [6.3 Bluetooth USB Dongle](#Bluetooth_USB_Dongle)
        *   [6.3.1 Audio devices start to skip at short distance from dongle](#Audio_devices_start_to_skip_at_short_distance_from_dongle)
    *   [6.4 Logitech Bluetooth USB Dongle](#Logitech_Bluetooth_USB_Dongle)
    *   [6.5 hcitool scan: Device not found](#hcitool_scan:_Device_not_found)
    *   [6.6 rfkill unblock: Do not unblock](#rfkill_unblock:_Do_not_unblock)
    *   [6.7 My computer is not visible](#My_computer_is_not_visible)
    *   [6.8 Logitech keyboard does not pair](#Logitech_keyboard_does_not_pair)
    *   [6.9 HSP/HFP profiles](#HSP/HFP_profiles)
    *   [6.10 Foxconn / Hon Hai / Lite-On Broadcom device](#Foxconn_/_Hon_Hai_/_Lite-On_Broadcom_device)
    *   [6.11 Intel combined wifi and bluetooth cards](#Intel_combined_wifi_and_bluetooth_cards)
    *   [6.12 Device connects, then disconnects after a few moments](#Device_connects,_then_disconnects_after_a_few_moments)
    *   [6.13 Device does not connect with an error in journal](#Device_does_not_connect_with_an_error_in_journal)
    *   [6.14 Device does not show up in scan](#Device_does_not_show_up_in_scan)
    *   [6.15 Interference between Headphones and Mouse](#Interference_between_Headphones_and_Mouse)
    *   [6.16 Failed to pair: org.bluez.Error.ConnectionAttemptFailed](#Failed_to_pair:_org.bluez.Error.ConnectionAttemptFailed)

## Installation

1.  [Install](/index.php/Install "Install") the [bluez](https://www.archlinux.org/packages/?name=bluez) package, providing the Bluetooth protocol stack.
2.  [Install](/index.php/Install "Install") the [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) package, providing the `bluetoothctl` utility. Alternatively install [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/) to additionally have the [deprecated BlueZ tools](#Deprecated_BlueZ_tools).
3.  The generic Bluetooth driver is the `btusb` Kernel module. [Check](/index.php/Kernel_module#Obtaining_information "Kernel module") whether that module is loaded. If it's not, then [load the module](/index.php/Kernel_module#Manual_module_handling "Kernel module").
4.  [Start/enable](/index.php/Start/enable "Start/enable") `bluetooth.service`.

**Note:**

*   By default the bluetooth daemon will only give out bnep0 devices to users that are a member of the `lp` group. Make sure to add your user to that group if you intend to connect to a bluetooth tether. You can change the group that is required in the file `/usr/share/dbus-1/system.d/bluetooth.conf`.
*   Some Bluetooth adapters are bundled with a Wi-Fi card (e.g. [Intel Centrino](http://www.intel.com/content/www/us/en/wireless-products/centrino-advanced-n-6235.html)). These require that the Wi-Fi card is firstly enabled (typically a keyboard shortcut on a laptop) in order to make the Bluetooth adapter visible to the kernel.
*   Some Bluetooth cards (e.g. Broadcom) conflict with the network adapter. Thus, you need to make sure that your Bluetooth device get connected before the network service boot.
*   Some tools such as hcitool and hciconfig have been deprecated upstream, and are no longer included in [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils). Since these tools will no longer be updated, it is recommended that scripts be updated to avoid using them. If you still desire to use them, install [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/). See [FS#53110](https://bugs.archlinux.org/task/53110) and [the Bluez mailing list](https://www.spinics.net/lists/linux-bluetooth/msg69239.html) for more information.

### Front-ends

#### Console

*   **bluetoothctl** — Pairing a device from the shell is one of the simplest and most reliable options.

	[http://www.bluez.org/](http://www.bluez.org/) || [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils)

**Tip:** To automate bluetoothctl commands, use `echo -e "<command1>
<command2>
" | bluetoothctl` or `bluetoothctl -- command`

#### Graphical

The following packages allow for a graphical interface to customize Bluetooth.

*   **GNOME Bluetooth** — [GNOME](/index.php/GNOME "GNOME")'s Bluetooth tool.
    *   [gnome-bluetooth](https://www.archlinux.org/packages/?name=gnome-bluetooth) provides the back-end
    *   [gnome-shell](https://www.archlinux.org/packages/?name=gnome-shell) provides the status monitor applet
    *   [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) provides the configuration front-end GUI that can be accessed by typing Bluetooth on the Activities overview, or with the `gnome-control-center bluetooth` command.
    *   You can also launch the `bluetooth-sendto` command directly to send files to a remote device.
    *   To receive files, open the Bluetooth settings panel; you can only receive whilst the Bluetooth panel is open.
    *   To add a Bluetooth entry to the *Send To* menu in Thunar's file properties menu, see instructions [here](http://docs.xfce.org/xfce/thunar/send-to). (The command that needs to be configured is `bluetooth-sendto %F`).

	[https://wiki.gnome.org/Projects/GnomeBluetooth](https://wiki.gnome.org/Projects/GnomeBluetooth) ||

*   **Bluedevil** — [KDE](/index.php/KDE "KDE")'s Bluetooth tool. If there is no Bluetooth icon visible in Dolphin and in the system tray, enable it in the system tray options or add a widget. You can configure Bluedevil and detect Bluetooth devices by clicking the icon. An interface is also available from the KDE System Settings.

	[https://projects.kde.org/projects/kde/workspace/bluedevil](https://projects.kde.org/projects/kde/workspace/bluedevil) || [bluedevil](https://www.archlinux.org/packages/?name=bluedevil)

*   **Blueberry** — Linux Mint's spin-off of GNOME Bluetooth, which works in all desktop environments. *Blueberry* does not support receiving files through Obex Object Push.

	[https://github.com/linuxmint/blueberry](https://github.com/linuxmint/blueberry) || [blueberry](https://www.archlinux.org/packages/?name=blueberry)

*   **[Blueman](/index.php/Blueman "Blueman")** — A full featured Bluetooth manager.

	[https://github.com/blueman-project/blueman](https://github.com/blueman-project/blueman) || [blueman](https://www.archlinux.org/packages/?name=blueman)

*   **[ObexFTP](/index.php/ObexFTP "ObexFTP")** — A tool for transferring files to/from any OBEX enabled device.

	[http://dev.zuckschwerdt.org/openobex/wiki/ObexFtp](http://dev.zuckschwerdt.org/openobex/wiki/ObexFtp) || [obexftp](https://aur.archlinux.org/packages/obexftp/)

## Pairing

**Note:** Before using the bluetooth device, make sure that it is not blocked by [rfkill](/index.php/Rfkill "Rfkill").

This section describes directly configuring *bluez5* via the *bluetoothctl* CLI, which might not be necessary if you are using an alternative front-end tool (such as GNOME Bluetooth).

The exact procedure depends on the devices involved and their input functionality. What follows is a general outline of pairing a device using `bluetoothctl`.

Start the `bluetoothctl` interactive command. Input `help` to get a list of available commands.

1.  (optional) Select a default controller with `select *MAC_address*`.
2.  Enter `power on` to turn the power to the controller on. It is off by default and will turn off again each reboot, see [#Auto power-on after boot](#Auto_power-on_after_boot).
3.  Enter `devices` to get the MAC Address of the device with which to pair.
4.  Enter device discovery mode with `scan on` command if device is not yet on the list.
5.  Turn the agent on with `agent on` or choose a specific agent: if you press tab twice after `agent` you should see a list of available agents, e.g. DisplayOnly KeyboardDisplay NoInputNoOutput DisplayYesNo KeyboardOnly off on.
6.  Enter `pair *MAC_address*` to do the pairing (tab completion works).
7.  If using a device without a PIN, one may need to manually trust the device before it can reconnect successfully. Enter `trust *MAC_address*` to do so.
8.  Enter `connect *MAC_address*` to establish a connection.

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

## Configuration

### Auto power-on after boot

By default, your Bluetooth adapter will not power on after a reboot. The former method by using `hciconfig hci0 up` is deprecated, see the [release note](http://www.bluez.org/release-of-bluez-5-35/). Now you just need to add the line `AutoEnable=true` in `/etc/bluetooth/main.conf` at the bottom in the `[Policy]` section:

 `/etc/bluetooth/main.conf` 
```
[Policy]
AutoEnable=true
```

## Audio

In order to be able to use audio equipment like bluetooth headphones or speakers, you need to install the additional [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) package. With a default PulseAudio installation you should immediately be able to stream audio from a bluetooth device to your speakers.

If you have a system-wide PulseAudio setup make sure the user running the daemon (usually `pulse`) is in the `lp` group and you load the bluetooth modules in your PulseAudio config:

 `/etc/pulse/system.pa` 
```
...
load-module module-bluetooth-policy
load-module module-bluetooth-discover
...
```

Please have a look at the [Bluetooth headset](/index.php/Bluetooth_headset "Bluetooth headset") page for more information about bluetooth audio and bluetooth headsets.

## Bluetooth serial

To get bluetooth serial communication working on Bluetooth-to-Serial modules (HC-05, HC-06) do the following steps:

Pair your bluetooth device using `bluetoothctl` as described [above](#Pairing).

Install [bluez-rfcomm](https://aur.archlinux.org/packages/bluez-rfcomm/) and [bluez-hcitool](https://aur.archlinux.org/packages/bluez-hcitool/), as they provide certain functionality which is missing from newer tools.

Bind paired device MAC address to tty terminal:

```
# rfcomm bind rfcomm0 <MAC address of bluetooth device>

```

Now you can open `/dev/rfcomm0` for serial communication.

## Troubleshooting

### Deprecated BlueZ tools

Eight BlueZ tools [were deprecated](https://git.kernel.org/pub/scm/bluetooth/bluez.git/commit/?id=b1eb2c4cd057624312e0412f6c4be000f7fc3617) and removed from [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), although not all of them were superseded by newer tools. The [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/) package provides an alternative version of [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils) with the deprecated tools.

| Deprecated tool | Most likely replacement |
| [gatttool](https://manpages.debian.org/stretch/bluez/gatttool.1.en.html) | btgatt-client, [D-Bus Gatt API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/gatt-api.txt) |
| [hciattach](https://manpages.debian.org/stretch/bluez/hciattach.1.en.html) | btattach |
| [hciconfig](https://manpages.debian.org/stretch/bluez/hciconfig.1.en.html) | btmgmt (and bluetoothctl?) |
| [hcidump](https://manpages.debian.org/stretch/bluez-hcidump/hcidump.1.en.html) | btmon (and btsnoop) |
| [hcitool](https://manpages.debian.org/stretch/bluez/hcitool.1.en.html) | missing, [D-Bus Device API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt) available |
| [rfcomm](https://manpages.debian.org/stretch/bluez/rfcomm.1.en.html) | missing, implement with [D-Bus Profile1 API](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/profile-api.txt)? |
| [ciptool](https://manpages.debian.org/stretch/bluez/ciptool.1.en.html) |
| [sdptool](https://manpages.debian.org/stretch/bluez/sdptool.1.en.html) | missing, functionality seems to be scattered over different D-Bus objects: [Profile](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/profile-api.txt), [Advertising](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/advertising-api.txt), and the UUIDs arrays in [device](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/device-api.txt) and [adapter](https://git.kernel.org/cgit/bluetooth/bluez.git/tree/doc/adapter-api.txt). |

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

*   On some laptops (e.g. Dell Studio 15, Lenovo Thinkpad X1) you have to switch the Bluetooth mode from HID to HCI. Install the [bluez-hid2hci](https://www.archlinux.org/packages/?name=bluez-hid2hci) package, then [udev](/index.php/Udev "Udev") should do this automatically. Alternatively, you can run this command to switch to HCI manually:

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

The device should now be available. See [BBS#162688](https://bbs.archlinux.org/viewtopic.php?id=162688) for information on making these changes persistent.

### Intel combined wifi and bluetooth cards

See [Wireless network configuration#Bluetooth coexistence](/index.php/Wireless_network_configuration#Bluetooth_coexistence "Wireless network configuration").

### Device connects, then disconnects after a few moments

If you see messages like the following in `journalctl` output, and your device fails to connect or disconnects shortly after connecting:

```
bluetoothd: Unable to get connect data for Headset Voice gateway: getpeername: Transport endpoint is not connected (107)
bluetoothd: connect error: Connection refused (111)

```

This may be because you have already paired the device with another operating system using the same bluetooth adapter (e.g., dual-booting). Some devices cannot handle multiple pairings associated with the same MAC address (i.e., bluetooth adapter). You can fix this by re-pairing the device. Start by removing the device:

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

try installing [pulseaudio-bluetooth](https://www.archlinux.org/packages/?name=pulseaudio-bluetooth) and restarting [PulseAudio](/index.php/PulseAudio "PulseAudio"). This error can manifest even while using only file transfer.

### Device does not show up in scan

Some devices using bluetooth low energy do not appear when scanning with bluetoothctl, for example the Logitech MX Master. The simplest way I have found to connect them is by installing [bluez-utils-compat](https://aur.archlinux.org/packages/bluez-utils-compat/), then [start](/index.php/Start "Start") `bluetooth.service` and do:

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

### Interference between Headphones and Mouse

If you experience audio stuttering while using a bluetooth mouse and keyboard simultaneously, you can try the following as referenced in #23 [https://bugs.launchpad.net/ubuntu/+source/bluez/+bug/424215](https://bugs.launchpad.net/ubuntu/+source/bluez/+bug/424215)

```
# hciconfig hci0 lm ACCEPT,MASTER
# hciconfig hci0 lp HOLD,SNIFF,PARK

```

### Failed to pair: org.bluez.Error.ConnectionAttemptFailed

When getting this error on pairing via `bluetoothctl`, among other things (search the internet), rebooting can help.