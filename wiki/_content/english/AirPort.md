Related articles

*   [Shairport](/index.php/Shairport "Shairport")

From [Wikipedia](https://en.wikipedia.org/wiki/AirPort "wikipedia:AirPort"):

	"*AirPort is the name given to a series of Apple products using the (Wi-Fi) protocols (802.11b, 802.11g, 802.11n and 802.11ac). These products comprise a number of wireless routers and wireless cards. The AirPort Extreme name was originally intended to signify the addition of the 802.11g protocol to these products.*"

Apple sells a number of AirPort models: AirPort Express, AirPort Extreme, and AirPort Time Capsule. The AirPort Time Capsule is essentially the AirPort Extreme, but with a 2-3 TB hard drive added, depending on which model you buy. All AirPort models have the ability to share printers on the network (through the USB port), and all AirPort models support up to 50 users.

## Configuration

Traditionally, AirPort base stations can be configured two ways, both of which require applications from Apple - AirPort base stations do not have web interfaces, unlike most routers. The first is using the desktop application, which is shipped with all Macs as a part of OS X and can be downloaded separately for Windows. There is no GNU/Linux version.

The second way is to use the AirPort Utility app on an iOS device. If you or a friend has an iPod Touch, iPhone, or iPad lying around, this is probably the most hassle-free way to configure your AirPort base station.

If that's not an option, you basically have two things to try: either run the desktop version of AirPort Utility in [Wine](/index.php/Wine "Wine"), or use [airport-utils](https://launchpad.net/airport-utils). airport-utils is not yet in the [AUR](/index.php/AUR "AUR").

## Music streaming

If you want to emulate the AirPort Express, take a look at [Shairport Sync](/index.php/Shairport_Sync "Shairport Sync"). If you wish to use the music streaming feature of AirPort Express base stations, look for "raop" in the [AUR](/index.php/AUR "AUR").

## Printing

**Note:** Although it is possible to configure [CUPS](/index.php/CUPS "CUPS") to use [Avahi](/index.php/Avahi "Avahi") for automatic printer configuration, it tends to be unreliable and can significantly increase boot time. It is therefore recommended that AirPort printers be configured manually.

Scan the Airport Express station to determine which port is used for printing.

 `# nmap 192.168.0.4` 
```
Starting Nmap 4.20 ( [http://insecure.org](http://insecure.org) ) at 2007-06-26 00:50 CEST
Interesting ports on 192.168.0.4:
Not shown: 1694 closed ports
PORT      STATE SERVICE
5000/tcp  open  UPnP
**9100/tcp  open  jetdirect**
10000/tcp open  snet-sensor-mgmt
MAC Address: 00:14:51:70:D5:66 (Apple Computer)

Nmap finished: 1 IP address (1 host up) scanned in 25.815 seconds

```

Note the port of the **jetdirect** service, and use a [printer URI](/index.php/CUPS#Printer_URI "CUPS") of **socket://**, followed by your station IP address, a colon, and the **jetdirect** port number.

**Note:** In order for this technique to work reliably, the AirPort should have a static local IP address using DHCP settings at the router.

See [CUPS](/index.php/CUPS "CUPS") for more information.