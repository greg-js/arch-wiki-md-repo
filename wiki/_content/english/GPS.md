There is a variety of [Global Positioning System](https://en.wikipedia.org/wiki/Global_Positioning_System "wikipedia:Global Positioning System") (GPS) hardware receivers supported in Arch Linux:

*   [Bluetooth](/index.php/Bluetooth "Bluetooth") GPS adapters
*   USB GPS adapters (internal or external)
*   WWAN-integrated adapters (some HP EliteBook modules for example)
*   smartphones are able to relay GPS data over USB or Bluetooth with additional software

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Drivers](#Drivers)
*   [2 Interfaces](#Interfaces)
    *   [2.1 GPSD](#GPSD)
    *   [2.2 ModemManager](#ModemManager)
        *   [2.2.1 View locationing capabilities](#View_locationing_capabilities)
        *   [2.2.2 Enable GPS](#Enable_GPS)
        *   [2.2.3 Display location](#Display_location)
        *   [2.2.4 Disable GPS](#Disable_GPS)
*   [3 Clients](#Clients)
    *   [3.1 Time Synchronization](#Time_Synchronization)
*   [4 See also](#See_also)

## Drivers

Usually a GPS device is presented as a serial device and the kernel uses a standard driver, but in some cases the drivers such as [mtkbabel](https://aur.archlinux.org/packages/mtkbabel/) or [mbm-gpsd-pl4nkton-git](https://aur.archlinux.org/packages/mbm-gpsd-pl4nkton-git/) need to be installed.

## Interfaces

GPS does not have a very unified interfacing and configuration in Linux. The raw GPS data is printed on the serial device and programs interpret the location by themselves, occupying the device in the process. Sharing the GPS adapter to multiple applications is possible with [gpsd](https://www.archlinux.org/packages/?name=gpsd).

### GPSD

[GPSD](http://www.catb.org/gpsd/) is a deamon to query the serial GPS device and make its output available on a TCP server. It is the most standard GPS interface in Linux and GPS-aware applications usually support it.

### ModemManager

ModemManager is some kind of a Linux WWAN modem support package which interfaces with [NetworkManager](/index.php/NetworkManager "NetworkManager"). It also supports querying GPS coordinates from GPS-enabled WWAN cards and it even displays the location in the [modem-manager-gui](https://www.archlinux.org/packages/?name=modem-manager-gui). The most important commands are:

#### View locationing capabilities

```
mmcli -m 0 --location-status

```

#### Enable GPS

```
mmcli -m 0 --location-enable-gps-raw --location-enable-gps-nmea

```

#### Display location

```
watch mmcli -m 0 --location-get

```

#### Disable GPS

```
mmcli -m 0 --location-disable-gps-raw --location-disable-gps-nmea

```

## Clients

The [gpsd](https://www.archlinux.org/packages/?name=gpsd) package provides `cgps`, a simple console-based client for showing the current GPS device status.

### Time Synchronization

See [Network_Time_Protocol_daemon#Using_ntpd_with_GPS](/index.php/Network_Time_Protocol_daemon#Using_ntpd_with_GPS "Network Time Protocol daemon")

## See also

*   [Enabling GPS location in ModemManager](https://sigquit.wordpress.com/2012/03/29/enabling-gps-location-in-modemmanager/)