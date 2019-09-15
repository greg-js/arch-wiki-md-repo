Related articles

*   [IPod](/index.php/IPod "IPod")

Unless disabled by your provider, it is possible to share your iPhone's mobile data connection over **WiFi**, **USB** or **Bluetooth**:

*   WiFi requires no additional configuration provided your computer can connect to wireless networks,
*   Instructions for USB and Bluetooth tethering are provided below.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tethering over USB](#Tethering_over_USB)
    *   [1.1 Using systemd-networkd](#Using_systemd-networkd)
    *   [1.2 Troubleshooting](#Troubleshooting)
*   [2 Tethering over Bluetooth](#Tethering_over_Bluetooth)
    *   [2.1 Hardware Requirements](#Hardware_Requirements)
    *   [2.2 Setup](#Setup)
        *   [2.2.1 Gnome/XFCE](#Gnome/XFCE)
        *   [2.2.2 netcfg](#netcfg)

## Tethering over USB

Tethering natively over USB is the optimal choice as it provides a more stable connection and uses less batteries than bluetooth or wifi.

To tether your iPhone over USB, you will need to install [libimobiledevice](https://www.archlinux.org/packages/?name=libimobiledevice).

Next enable *Personal Hotspot* on your iPhone and plug it into your computer. At this point you will have a new ethernet device available and should be able to use any [network manager](/index.php/List_of_applications#Network_managers "List of applications") to connect to the internet through the new iPhone ethernet device, just like you would any other ethernet connection.

#### Using systemd-networkd

If [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") is used for network management, you can easily configure it to connect to the internet through the iPhone, as you would with any other adaptater.

If for example *enp0s26u1u2c4i2* is the name of the network device that is created from the iPhone as displayed by `networkctl list`, create the following *.network* file:

 `/etc/systemd/network/30-tethering.network` 
```
[Match]
Name=enp0s26u1u2c4i2

[Network]
DHCP=yes
```

#### Troubleshooting

If the iPhone appears in the device list but does not connect, it is possible that you may need to connect your iPhone and pair it with your computer before connecting (iPhones using a PIN unlock?):

```
# idevicepair pair

```

## Tethering over Bluetooth

Tethering over Bluetooth will drain the batteries relatively quickly, but simultaneous charging from an USB port works well.

### Hardware Requirements

*   iPhone running OS 3.0 with tethering enabled. See *Settings* > *General* > *Network* and turn on the tethering option.
*   Bluetooth adapter or similar, preferably with EDR (*Enhanced Data Rate*) for acceptable speeds. Tested with a *Belkin F8T016NE*.

### Setup

See the main article [Bluetooth](/index.php/Bluetooth "Bluetooth") and setup the bluetooth daemon.

#### Gnome/XFCE

Install the [Blueman](/index.php/Blueman "Blueman") GTK Bluetooth manager.

A Bluetooth icon should appear in your notification area. Note: the icon may not appear if bluetooth was not turned on at startup. Click it, and search for nearby devices, adding your iPhone (note, you may need to have the Bluetooth setting screen up on your iPhone for discovery to work).

Once the iPhone has been added to the devices list, open the Device menu and select pair. This will require the usual entering of a PIN on the computer then the iPhone. Now open the Device menu again, and choose *Network Access* > *Network Access Point*. If everything goes well, blueman reports a success and the status bar on your iPhone should glow blue, indicating a successful tether.

Blueman will have created a new network interface, typically bnep0\. To connect to it, run the following as root.

```
# dhcpcd bnep0

```

#### netcfg

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