Related articles

*   [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")
*   [systemd](/index.php/Systemd "Systemd")

From the [systemd mailing list](http://lists.freedesktop.org/archives/systemd-devel/2014-May/019537.html):

	*systemd-timesyncd* is a daemon that has been added for synchronizing the system clock across the network. It implements an SNTP client. In contrast to NTP implementations such as [chrony](/index.php/Chrony "Chrony") or the NTP reference server this only implements a client side, and does not bother with the full NTP complexity, focusing only on querying time from one remote server and synchronizing the local clock to it. Unless you intend to serve NTP to networked clients or want to connect to local hardware clocks this simple NTP client should be more than appropriate for most installations. The daemon runs with minimal privileges, and has been hooked up with networkd to only operate when network connectivity is available. The daemon saves the current clock to disk every time a new NTP sync has been acquired, and uses this to possibly correct the system clock early at bootup, in order to accommodate for systems that lack an RTC such as the Raspberry Pi and embedded devices, and make sure that time monotonically progresses on these systems, even if it is not always correct. To make use of this daemon a new system user and group "systemd-timesync" needs to be created on installation of systemd.

## Configuration

[Start/enable](/index.php/Start/enable "Start/enable") `systemd-timesyncd.service` which is available with [systemd](https://www.archlinux.org/packages/?name=systemd).

When starting, *systemd-timesyncd* will read the configuration file from `/etc/systemd/timesyncd.conf`, which looks like this:

 `/etc/systemd/timesyncd.conf` 
```
[Time]
#NTP=
#FallbackNTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
#RootDistanceMaxSec=5
#PollIntervalMinSec=32
#PollIntervalMaxSec=2048
```

To add [time servers](/index.php/Network_Time_Protocol_daemon#Connection_to_NTP_servers "Network Time Protocol daemon") or change the provided ones, uncomment the relevant line and list their host name or IP separated by a space. For example, you can use any servers provided by [the NTP pool project](http://www.pool.ntp.org/) or use [the default Arch ones](https://projects.archlinux.org/svntogit/packages.git/commit/trunk?h=packages/ntp&id=1b485f87c9e1384eaf069d031e415515e8ead92d) (also provided by the NTP pool project):

 `/etc/systemd/timesyncd.conf` 
```
[Time]
NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
FallbackNTP=0.pool.ntp.org 1.pool.ntp.org 0.fr.pool.ntp.org
```

To verify your configuration, use `timedatectl show-timesync --all`:

 `$ timedatectl show-timesync --all` 
```
LinkNTPServers=
SystemNTPServers=
FallbackNTPServers=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org
ServerName=0.arch.pool.ntp.org
ServerAddress=103.47.76.177
RootDistanceMaxUSec=5s
PollIntervalMinUSec=32s
PollIntervalMaxUSec=34min 8s
PollIntervalUSec=1min 4s
NTPMessage={ Leap=0, Version=4, Mode=4, Stratum=2, Precision=-21, RootDelay=177.398ms, RootDispersion=142.196ms, Reference=C342F10A, OriginateTimestamp=Mon 2018-07-16 13:53:43 +08, ReceiveTimestamp=Mon 2018-07-16 13:53:43 +08, TransmitTimestamp=Mon 2018-07-16 13:53:43 +08, DestinationTimestamp=Mon 2018-07-16 13:53:43 +08, Ignored=no PacketCount=1, Jitter=0 }
Frequency=22520548
```

Further to the daemon configuration, NTP servers may also be provided via a [systemd-networkd](/index.php/Systemd-networkd#[NetDev]_section "Systemd-networkd") configuration with a `NTP=` option or, dynamically, via a DHCP server.

The NTP server to be used will be determined using the following rules:

*   Any per-interface NTP servers obtained from `systemd-networkd.service(8)` configuration or via DHCP take precedence.
*   The NTP servers defined in `/etc/systemd/timesyncd.conf` will be appended to the per-interface list at runtime and the daemon will contact the servers in turn until one is found that responds.
*   If no NTP server information is acquired after completing those steps, the NTP server host names or IP addresses defined in `FallbackNTP=` will be used.

**Note:** The service writes to a local file `/var/lib/systemd/timesync/clock` with every synchronization. This location is hard-coded and cannot be changed. This may be problematic for running off read-only root partition or trying to minimize writes to an SD card.

## Usage

To enable and start it, simply run:

```
# timedatectl set-ntp true 

```

The synchronization process might be noticeably slow. This is expected, one should wait a while before determining there is a problem. To check the service status, use `timedatectl status`:

 `$ timedatectl status` 
```
               Local time: Thu 2015-07-09 18:21:33 CEST
           Universal time: Thu 2015-07-09 16:21:33 UTC
                 RTC time: Thu 2015-07-09 16:21:33
                Time zone: Europe/Amsterdam (CEST, +0200)
System clock synchronized: yes
              NTP service: active
          RTC in local TZ: no

```

To see verbose service information, use `timedatectl timesync-status`:

 `$ timedatectl timesync-status` 
```
       Server: 103.47.76.177 (0.arch.pool.ntp.org)
Poll interval: 2min 8s (min: 32s; max 34min 8s)
         Leap: normal
      Version: 4
      Stratum: 2
    Reference: C342F10A
    Precision: 1us (-21)
Root distance: 231.856ms (max: 5s)
       Offset: -19.428ms
        Delay: 36.717ms
       Jitter: 7.343ms
 Packet count: 2
    Frequency: +267.747ppm

```

## See also

*   [Forum: systemd-timesyncd is not syncing time](https://bbs.archlinux.org/viewtopic.php?id=182600)
*   [Forum: Using systemd-timesync instead of NTP](https://bbs.archlinux.org/viewtopic.php?id=182172)
*   [Git Sourcecode of timesyncd](https://github.com/systemd/systemd/blob/master/src/timesync/timesyncd.c)