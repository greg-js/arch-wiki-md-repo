# AirPort

From [Wikipedia](https://en.wikipedia.org/wiki/AirPort "wikipedia:AirPort"):

	"_AirPort is the name given to a series of Apple products using the (Wi-Fi) protocols (802.11b, 802.11g, 802.11n and 802.11ac). These products comprise a number of wireless routers and wireless cards. The AirPort Extreme name was originally intended to signify the addition of the 802.11g protocol to these products._"

Apple sells a number of AirPort models: AirPort Express, AirPort Extreme, and AirPort Time Capsule. The AirPort Extreme is distinguished from the AirPort Express in that it has better WiFi (802.11ac instead of 802.11n, and 1.3 Gbps instead of 300 Mbps), better Ethernet ports (four gigabit ports instead of two 10/100BASE‑T ports), the ability to connect a hard drive to the USB port to share on the network, and the loss of the ability to stream music. The AirPort Time Capsule is essentially the AirPort Extreme, but with a 2-3 TB hard drive added, depending on which model you buy. All AirPort models have the ability to share printers on the network (through the USB port), and all AirPort models support up to 50 users.

## Configuration

Traditionally, AirPort base stations can be configured two ways, both of which require applications from Apple - AirPort base stations do not have web interfaces, unlike most routers. The first is using the desktop application, which is shipped with all Macs as a part of OS X and can be downloaded separately for Windows. There is no GNU/Linux version.

The second way is to use the AirPort Utility app on an iOS device. If you or a friend has an iPod Touch, iPhone, or iPad lying around, this is probably the most hassle-free way to configure your AirPort base station.

If that's not an option, you basically have two things to try: either run the desktop version of AirPort Utility in [Wine](/index.php/Wine "Wine"), or use [airport-utils](https://launchpad.net/airport-utils). airport-utils is not yet in the [AUR](/index.php/AUR "AUR").

## Music streaming

If you wish to use the music streaming feature of AirPort Express base stations, look for "raop" in the [AUR](/index.php/AUR "AUR"). Googling suggests that you can install [paprefs](https://www.archlinux.org/packages/?name=paprefs) and a RAOP plugin for [PulseAudio](/index.php/PulseAudio "PulseAudio"), but I haven't tried this, so I can't offer any advice. Try Googling.

## Printing

The first step is to scan the Airport Express station. It seems that there are different addresses depending on the model:

 `# nmap 192.168.0.4` 

```
Starting Nmap 4.20 ( http://insecure.org ) at 2007-06-26 00:50 CEST
Interesting ports on 192.168.0.4:
Not shown: 1694 closed ports
PORT      STATE SERVICE
5000/tcp  open  UPnP
9100/tcp  open  jetdirect
10000/tcp open  snet-sensor-mgmt
MAC Address: 00:14:51:70:D5:66 (Apple Computer)

Nmap finished: 1 IP address (1 host up) scanned in 25.815 seconds

```

The Airport station is accessed like an HP JetDirect printer. Note the port of the **jetdirect** service, and edit `printer.conf`. The **DeviceURI** entry should be **socket://**, followed by your station IP address, a colon, and the **jetdirect** port number.

 `/etc/cups/printer.conf` 

```
# Printer configuration file for CUPS v1.2.11
# Written by cupsd on 2007-06-26 00:44
<Printer LaserSim>
Info SAMSUNG ML-1510 gdi
Location SomoStation
DeviceURI socket://192.168.0.4:9100
State Idle
StateTime 1182811465
Accepting Yes
Shared Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
OpPolicy default
ErrorPolicy stop-printer
</Printer>
```

See the [CUPS](/index.php/CUPS "CUPS") wiki page for more information.

Retrieved from "[https://wiki.archlinux.org/index.php?title=AirPort&oldid=391735](https://wiki.archlinux.org/index.php?title=AirPort&oldid=391735)"