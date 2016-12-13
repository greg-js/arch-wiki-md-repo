This article describes how to set up and run Chrony, an alternative NTP client and server that is roaming friendly and designed specifically for systems that are not online all the time.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 NTP Servers](#NTP_Servers)
    *   [2.2 Telling chronyd an internet connection has been made](#Telling_chronyd_an_internet_connection_has_been_made)
*   [3 Usage](#Usage)
    *   [3.1 Starting chronyd](#Starting_chronyd)
    *   [3.2 Synchronising chrony hardware clock from the system clock](#Synchronising_chrony_hardware_clock_from_the_system_clock)
*   [4 Notifying network state](#Notifying_network_state)
    *   [4.1 NetworkManager](#NetworkManager)
    *   [4.2 netctl](#netctl)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [chrony](https://www.archlinux.org/packages/?name=chrony) package.

## Configuration

The smallest useful configuration file (using IP addresses instead of a hostname) would look something like:

 `/etc/chrony.conf` 
```
server 1.2.3.4 offline
server 5.6.7.8 offline
server 9.10.11.12 offline
driftfile /etc/chrony.drift
rtconutc
rtcsync

```

### NTP Servers

The first thing you define in your `/etc/chrony.conf` is the servers your machine will synchronize to. NTP servers are classified in a hierarchical system with many levels called *strata*: the devices which are considered independent time sources are classified as *stratum 0* sources; the servers directly connected to *stratum 0* devices are classified as *stratum 1* sources; servers connected to *stratum 1* sources are then classified as *stratum 2* sources and so on.

It has to be understood that a server's stratum cannot be taken as an indication of its accuracy or reliability. Typically, stratum 2 servers are used for general synchronization purposes: if you do not already know the servers you are going to connect to, you should use the [pool.ntp.org](http://www.pool.ntp.org/) servers ([alternate link](http://support.ntp.org/bin/view/Servers/NTPPoolServers)) and choose the server pool that is closest to your location.

The following lines are just an example:

```
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

```

If your computer is not connected to the internet on startup, it is recommended to use the *offline* option, to tell Chrony not to try and connect to the servers, until it has been given the go:

```
server 0.pool.ntp.org offline
server 1.pool.ntp.org offline
server 2.pool.ntp.org offline
server 3.pool.ntp.org offline

```

It may also be a good idea to either use IP addresses instead of host names, or to map the hostnames to IP addresses in your `/etc/hosts` file, as DNS resolving will not be available until you have made a connection.

### Telling chronyd an internet connection has been made

If you are connected to the internet, run:

```
# chronyc
chronyc> online
200 OK
chronyc> exit

```

You may also be interested in the `activity` option to display status:

```
# chronyc activity
200 OK
3 sources online
0 sources offline
0 sources doing burst (return to online)
0 sources doing burst (return to offline)
0 sources with unknown address

```

Chrony should now connect to the configured time servers and update your clock if needed. To tell chrony that you are not connected to the Internet anymore, execute the following:

```
# chronyc offline
200 OK

# chronyc activity
200 OK
0 sources online
3 sources offline
0 sources doing burst (return to online)
0 sources doing burst (return to offline)
0 sources with unknown address

```

The online/offline status can be automatically handled by dispatcher services for [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) and [connman](https://www.archlinux.org/packages/?name=connman), see below.

In conclusion, do not forget the user guide at `/usr/share/doc/chrony/chrony.txt`, which is likely to answer any doubts you could still have. [It is also available online.](http://chrony.tuxfamily.org/manual.html) See also the related man pages: `man {chrony|chronyc|chronyd|chrony.conf}`).

## Usage

### Starting chronyd

The package provides `chrony.service`, see [systemd](/index.php/Systemd "Systemd") for details.

### Synchronising chrony hardware clock from the system clock

During boot the initial time is read from the hardware clock (RTC) and the system time is then set, and synchronised over a period of minutes once the chrony daemon has been running for a while. If the hardware clock is out of sync then the initial system time can be some minutes away from the true time. If that is the case it may be necessary to reset the hardware clock.

You can use chronyc to force the current system time to be synced to hardware:

```
# chronyc
chronyc> trimrtc
200 OK
chronyc> quit

```

Then exit from chronyc and the RTC and system time should be within a few microseconds of each other and should then be approximately correct on boot and fully synchronise a short time later.

## Notifying network state

If you have specified your pools as offline in `chrony.conf`, you need to tell *chrony* that the network status has changed.

You can either use *chronyc* to notify *chrony* that your network configuration has changed, or you can use a dispatcher for your relevant network configuration manager.

### NetworkManager

*chronyd* can be go into online/offline mode along with a network connection through the use of [NetworkManager's dispatcher scripts](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager"). You can install [networkmanager-dispatcher-chrony](https://aur.archlinux.org/packages/networkmanager-dispatcher-chrony/) from the AUR.

### netctl

Install [netctl-dispatcher-chrony](https://aur.archlinux.org/packages/netctl-dispatcher-chrony/) from the AUR. This adds a hook to netctl which is run automatically for any connection.

## See also

*   [Time](/index.php/Time "Time") (for more information on computer timekeeping)
*   [http://chrony.tuxfamily.org/](http://chrony.tuxfamily.org/)
*   [http://www.ntp.org/](http://www.ntp.org/)
*   [http://support.ntp.org/](http://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [http://www.eecis.udel.edu/~mills/ntp/html/index.html](http://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)