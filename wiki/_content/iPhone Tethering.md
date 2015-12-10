# iPhone Tethering

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Unless disabled by your provider, it's possible to share your iPhone's 3G data connection over WiFi, USB and Bluetooth without needing to jailbreak. WiFi requires no additional configuration provided your computer can connect to wireless networks, and you'll find instructions for USB and Bluetooth below.

## Contents

*   [1 Tethering over USB](#Tethering_over_USB)
    *   [1.1 Tethering over USB using Personal Hotspot](#Tethering_over_USB_using_Personal_Hotspot)
        *   [1.1.1 Using systemd-networkd with udev](#Using_systemd-networkd_with_udev)
        *   [1.1.2 Troubleshooting](#Troubleshooting)
            *   [1.1.2.1 The iPhone appears in the device list but it doesn't connect](#The_iPhone_appears_in_the_device_list_but_it_doesn.27t_connect)
*   [2 Tethering over Bluetooth](#Tethering_over_Bluetooth)
    *   [2.1 Hardware Requirements](#Hardware_Requirements)
    *   [2.2 Setup](#Setup)
        *   [2.2.1 Gnome/XFCE](#Gnome.2FXFCE)
        *   [2.2.2 netcfg](#netcfg)

## Tethering over USB

### Tethering over USB using Personal Hotspot

Tethering natively over USB is the optimal choice as it provides a more stable connection and uses less batteries than bluetooth or wifi.

To tether your iPhone over USB, you will need to install these packages: [usbmuxd](https://www.archlinux.org/packages/?name=usbmuxd), [libimobiledevice](https://www.archlinux.org/packages/?name=libimobiledevice) and [ifuse](https://www.archlinux.org/packages/?name=ifuse).

Then ensure the ipheth module is loaded (currently included in the default and LTS Archlinux kernels)

```
# modprobe ipheth

```

Assuming everything's gone smoothly so far, enable **Personal Hotspot** on your iPhone and plug it into your computer. At this point you'll have a new ethernet device available, but connecting through it might not work quite yet; for some reason, the **ipheth** module only works when the iPhone's filesystem has been mounted by **ifuse**, so unless your system did it automatically when you plugged your iPhone in, you'll need to do it manually:

```
# ifuse /path/to/mountpoint

```

To manually unmount it later, run:

```
# fusermount -u /path/to/mountpoint

```

Once your iPhone's filesystem is mounted, you should be able to use any [network manager](/index.php/List_of_applications#Network_Managers "List of applications") to connect to the internet through the new iPhone ethernet device just like you would any other ethernet connection.

#### Using systemd-networkd with udev

Using [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") you can simply adjust the networking to use the iphone as the gateway.

 `/etc/udev/rules.d/90-iphone-tethering.rules` 

```
# Execute pairing program when appropriate
ACTION=="add|remove", SUBSYSTEM=="net", ATTR{idVendor}=="05ac", ENV{ID_USB_DRIVER}=="ipheth", SYMLINK+="iphone", RUN+="/usr/bin/systemctl restart systemd-networkd.service"

```

 `/etc/systemd/network/enp0s26u1u2c4i2.network` 

```
[Match]
Name=enp0s26u1u2c4i2

[Network]
DHCP=ipv4

```

_enp0s26u1u2c4i2_ being the name of the network device that is created from the iphone.

#### Troubleshooting

##### The iPhone appears in the device list but it doesn't connect

Its possible that you may need to connect your iPhone and pair it with your computer before connecting in some circumstances (iPhones using a PIN unlock?):

```
# idevicepair pair

```

## Tethering over Bluetooth

Tethering over Bluetooth will drain the batteries relatively quickly, but simultaneous charging from an USB port works well.

### Hardware Requirements

*   iPhone running OS 3.0 with tethering enabled. See Settings > General > Network and turn on the tethering option.
*   Bluetooth Adapter or similar, preferably with EDR(Enhanced Data Rate) for acceptable speeds. Tested with a Belkin F8T016NE.

### Setup

See the main article [Bluetooth](/index.php/Bluetooth "Bluetooth") and setup the bluetooth daemon.

#### Gnome/XFCE

Install the [Blueman](/index.php/Blueman "Blueman") GTK+ Bluetooth manager.

A Bluetooth icon should appear in your notification area. Note: the icon may not appear if bluetooth was not turned on at startup. Click it, and search for nearby devices, adding your iPhone (note, you may need to have the Bluetooth setting screen up on your iPhone for discovery to work).

Once the iPhone has been added to the devices list, open the Device menu and select pair. This will require the usual entering of a PIN on the computer then the iPhone. Now open the Device menu again, and choose Network Access > Network Access Point. If everything goes well, blueman reports a success and the status bar on your iPhone should glow blue, indicating a successful tether.

Blueman will have created a new network interface, typically bnep0\. To connect to it, run the following as root.

```
# dhcpcd bnep0

```

#### netcfg

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

[![Tango-dialog-warning.png](/images/d/d8/Tango-dialog-warning.png)](/index.php/File:Tango-dialog-warning.png)

**This article or section is out of date.**

**Reason:** _netcfg_ has been superseded by [netctl](/index.php/Netctl "Netctl") (Discuss in [Talk:IPhone Tethering#](https://wiki.archlinux.org/index.php/Talk:IPhone_Tethering))

Alternatively, you can create a [netcfg](/index.php/Netcfg "Netcfg") network profile to allow easy tethering from the command line, without requiring [Blueman](/index.php/Blueman "Blueman") or Gnome. Assuming an already paired iPhone with address '00:00:DE:AD:BE:EF', simply create a profile in /etc/network.d called - for example - 'tether':

```
 CONNECTION="ethernet"
 DESCRIPTION="Ethernet via pand tethering to iPhone"
 INTERFACE="bnep0"
 IPHONE="00:00:DE:AD:BE:EF"
 PRE_UP="pand -E -S -c ${IPHONE} -e ${INTERFACE} -n 2>/dev/null"
 POST_DOWN="pand -k ${IPHONE}"
 IP="dhcp"

```

Then, either as root or using sudo, execute:

```
# netcfg tether

```

To bring the interface down and un-tether:

```
# netcfg down tether

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=IPhone_Tethering&oldid=397034](https://wiki.archlinux.org/index.php?title=IPhone_Tethering&oldid=397034)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Network sharing](/index.php/Category:Network_sharing "Category:Network sharing")
*   [Mobile devices](/index.php/Category:Mobile_devices "Category:Mobile devices")