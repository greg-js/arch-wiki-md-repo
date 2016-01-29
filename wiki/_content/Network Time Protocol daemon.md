# Network Time Protocol daemon

Related articles

*   [Time](/index.php/Time "Time")
*   [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")
*   [OpenNTPD](/index.php/OpenNTPD "OpenNTPD")
*   [Chrony](/index.php/Chrony "Chrony")

[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") is the most common method to synchronize the [software clock](/index.php/Time "Time") of a GNU/Linux system with internet time servers. It is designed to mitigate the effects of variable network latency and can usually maintain time to within tens of milliseconds over the public Internet. The accuracy on local area networks is even better, up to one millisecond.

[The NTP Project](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project) provides a reference implementation of the protocol called simply NTP. This article further describes how to set up and run the NTP daemon, both as a client and as a server.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Connection to NTP servers](#Connection_to_NTP_servers)
    *   [2.2 NTP server mode](#NTP_server_mode)
*   [3 Usage](#Usage)
    *   [3.1 Start ntpd at boot](#Start_ntpd_at_boot)
    *   [3.2 Synchronize time once per boot](#Synchronize_time_once_per_boot)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Start ntpd on network connection](#Start_ntpd_on_network_connection)
    *   [4.2 Using ntpd with GPS](#Using_ntpd_with_GPS)
    *   [4.3 Running in a chroot](#Running_in_a_chroot)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ntp](https://www.archlinux.org/packages/?name=ntp) package. By default, _ntpd_ works in client mode without further configuration. You can skip to [#Usage](#Usage), if you want to use the Arch Linux default configuration file for it. For server configuration, see [#NTP server mode](#NTP_server_mode).

## Configuration

The main daemon is _ntpd_, which is configured in `/etc/ntp.conf`. Refer to the manual pages for detail: `man ntp.conf` and the related `man {ntpd|ntp_auth|ntp_mon|ntp_acc|ntp_clock|ntp_misc}`.

### Connection to NTP servers

NTP servers are classified in a hierarchical system with many levels called _strata_: the devices which are considered independent time sources are classified as _stratum 0_ sources; the servers directly connected to _stratum 0_ devices are classified as _stratum 1_ sources; servers connected to _stratum 1_ sources are then classified as _stratum 2_ sources and so on.

It has to be understood that a server's stratum cannot be taken as an indication of its accuracy or reliability. Typically, stratum 2 servers are used for general synchronization purposes: if you do not already know the servers you are going to connect to, you should choose a server pool close to your location from the [pool.ntp.org](http://www.pool.ntp.org/) servers ([alternative link](http://support.ntp.org/bin/view/Servers/NTPPoolServers)).

Since _ntp_ version 4.2.7.p465-2, Arch Linux uses its own default vendor pool of NTP servers provided by [the NTP Pool Project](http://www.pool.ntp.org) (see [FS#41700](https://bugs.archlinux.org/task/41700)). Modify those to suit your needs, e.g. if you want to use your country's servers with an option:

 `/etc/ntp.conf` 

```
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst

```

The `iburst` option is recommended, and sends a burst of packets only if it cannot obtain a connection with the first attempt. The `burst` option always does this, even on the first attempt, and should never be used without explicit permission and may result in blacklisting.

### NTP server mode

If setting up an NTP server, you need to add [_local clock_](http://www.ntp.org/ntpfaq/NTP-s-refclk.htm#Q-LOCAL-CLOCK) as a server, so that, in case it loses internet access, it will continue serving time to the network; add _local clock_ as a stratum 10 server (using the _fudge_ command) (you can set up to [stratum 15](http://www.ntp.org/ntpfaq/NTP-s-algo.htm#Q-ALGO-BASIC-STRATUM)) so that it will never be used unless internet access is lost:

```
server 127.127.1.1
fudge  127.127.1.1 stratum 12

```

Next, define the rules that will allow clients to connect to your service (_localhost_ is considered a client too) using the _restrict_ command; you should already have a line like this in your file:

```
restrict default nomodify nopeer noquery

```

This restricts everyone from modifying anything and prevents everyone from querying the status of your time server: `nomodify` prevents reconfiguring _ntpd_ (with _ntpq_ or _ntpdc_), and `noquery` is [important to prevent](https://mailman.archlinux.org/pipermail/arch-dev-public/2014-February/025872.html) dumping status data from _ntpd_ (also with _ntpq_ or _ntpdc_).

You can also add other options:

```
restrict default kod nomodify notrap nopeer noquery

```

**Note:** This still allows other people to query your time server. You need to add `noserve` to stop serving time. It will also block time synchronization since it blocks all packets except _ntpq_ and _ntpdc_ queries.

If you want to change any of these, see the full docs for the "restrict" option in `man ntp_acc`, the detailed [ntp instructions](https://support.ntp.org/bin/view/Support/AccessRestrictions) and [#As a daemon](#As_a_daemon).

Following this line, you need to tell _ntpd_ what to allow through into your server; the following line is enough if you are not configuring an NTP server:

```
restrict 127.0.0.1

```

If you want to force DNS resolution to the IPv6 namespace, write `-6` before the IP address or host name (`-4` forces IPv4 instead), for example:

```
restrict -6 default kod nomodify notrap nopeer noquery
restrict -6 ::1    # ::1 is the IPv6 equivalent for 127.0.0.1

```

Lastly, specify the drift file (which keeps track of your clock's time deviation) and optionally the log file location:

```
driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

A very basic configuration file will look like this:

 `/etc/ntp.conf` 

```
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
server 2.pool.ntp.org iburst
server 3.pool.ntp.org iburst

restrict default kod nomodify notrap nopeer noquery
restrict -6 default kod nomodify notrap nopeer noquery

restrict 127.0.0.1
restrict -6 ::1  

driftfile /var/lib/ntp/ntp.drift
logfile /var/log/ntp.log

```

**Note:** Defining the log file is not mandatory, but it is always a good idea to have feedback for _ntpd_ operations.

## Usage

The package has a default client-mode configuration and its own user and group to drop root privileges after starting. If you start it from the console, you should always do so with the `-u` option:

```
# ntpd -u ntp:ntp

```

The `-u` option is employed by the two included systemd services. These services also use the `-g` option, which disables a threshold (so-called _panic-gate_). Hence, they will synchonize time even in case the ntp-server's time exceeds the threshold deviation from the system clock.

**Warning:** One reason the panic-gate was introduced is that background jobs/services may be susceptible to time-jumps. If the system's clock was never synchronized before, consider stopping them before running _ntpd_ for the first time.

Both services are tied to the system's resolver, and will start synchronizing when an active network connection is detected.

### Start ntpd at boot

[Enable](/index.php/Enable "Enable") the daemon with `ntpd.service`. See also [#Running in a chroot](#Running_in_a_chroot).

**Note:** The systemd command _timedatectl_ can only be used to control [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd"), executing `timedatectl set-ntp 1` as root will inadvertedly stop a running `ntpd.service`.[[1]](http://lists.freedesktop.org/archives/systemd-devel/2015-April/030277.html)

Use _ntpq_ to see the list of configured peers and status of synchronization:

```
$ ntpq -p

```

The delay, offset and jitter columns should be non-zero. The servers _ntpd_ is synchronizing with are prefixed by an asterisk. It can take several minutes before _ntpd_ selects a server to synchronize with; try checking after 17 minutes (1024 seconds).

### Synchronize time once per boot

Alternatively, [enable](/index.php/Enable "Enable") `ntpdate.service` to synchronize time once (option `-q`) and non-forking (option `-n`) per boot, instead of running the daemon in the background. This method is discouraged on servers, and in general on machines that run without rebooting for more than a few days.

If the synchronized time should be written to the hardware clock as well, configure the provided unit as described in [systemd#Editing provided units](/index.php/Systemd#Editing_provided_units "Systemd") before starting it:

 `/etc/systemd/system/ntpdate.service.d/hwclock.conf` 

```
[Service]
ExecStart=/usr/bin/hwclock -w
```

## Tips and tricks

### Start ntpd on network connection

_ntpd_ can be started by your network manager, so that the daemon only runs when the computer is online.

NaN

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** add `-u` and optionally refer to [#Usage](#Usage), or use systemctl if possible (Discuss in [Talk:Network Time Protocol daemon#](https://wiki.archlinux.org/index.php/Talk:Network_Time_Protocol_daemon))

Append the following lines to your [netctl](/index.php/Netctl "Netctl") profile:

```
ExecUpPost='/usr/bin/ntpd || true'
ExecDownPre='killall ntpd || true'

```

NaN

The _ntpd_ daemon can be brought up/down along with a network connection through the use of NetworkManager's [dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") scripts. The [networkmanager-dispatcher-ntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-ntpd) package installs one, pre-configured to start and stop the [ntpd service](#Start_ntpd_at_boot) with a connection.

NaN

For [Wicd](/index.php/Wicd "Wicd"), create a start script in the `postconnect` directory and a stop script in the `predisconnect` directory. Remember to make them executable:

 `/etc/wicd/scripts/postconnect/ntpd` 

```
#!/bin/bash
systemctl start ntpd &

```

 `/etc/wicd/scripts/predisconnect/ntpd` 

```
#!/bin/bash
systemctl stop ntpd &

```

**Note:** You are advised to customize the options for the _ntpd_ command as explained in [#Usage](#Usage).

See also [Wicd#Scripts](/index.php/Wicd#Scripts "Wicd").

NaN

KDE can use NTP (ntp must be installed) by right clicking the clock and selecting _Adjust date/time_. However, this requires the ntp daemon to be [disabled](/index.php/Disable "Disable") before configuring KDE to use NTP. [[2]](https://bugs.kde.org/show_bug.cgi?id=178968)

### Using ntpd with GPS

Most of the articles online about configuring _ntpd_ to receive time from a GPS suggest to use the SHM (shared memory) method. However, at least since _ntpd_ version 4.2.8 a _much better_ method is available. It connects directly to _gpsd_, so [gpsd](https://www.archlinux.org/packages/?name=gpsd) needs to be installed.

Add these lines to your `/etc/ntp.conf`:

 `/etc/ntp.conf` 

```
#=========================================================
#  GPSD native ntpd driver
#=========================================================
# This driver exists from at least ntp version 4.2.8
# Details at
#   [https://www.eecis.udel.edu/~mills/ntp/html/drivers/driver46.html](https://www.eecis.udel.edu/~mills/ntp/html/drivers/driver46.html)
server 127.127.46.0 
fudge 127.127.46.0 time1 0.0 time2 0.0 refid GPS
```

This will work as long as you have _gpsd_ working. It connects to _gpsd_ via the local socket and queries the "gpsd_json" object that is returned.

To test the setup, first ensure that _gpsd_ is working by running:

```
 $ cgps -s 

```

Then wait a few minutes and run `ntpq -p`. This will show if _ntpd_ is talking to _gpsd_:

 `$ ntpq -p` 

```
remote           refid            st t when poll reach   delay   offset  jitter
 ==================================================================================
*GPSD_JSON(0)    .GPS.            0 l   55   64  377    0.000    2.556  14.109
```

**Tip:** If the _reach_ column is 0, it means _ntpd_ has not been able to talk to _gpsd_. Wait a few minutes and try again. Sometimes it takes _ntpd_ a while.

### Running in a chroot

**Note:** _ntpd_ should be started as non-root (default in the Arch Linux package) before attempting to jail it in a chroot, since chroots are relatively useless at securing processes running as root.

Create a new directory `/etc/systemd/system/ntpd.service.d/` if it does not exist and a file named `customexec.conf` inside with the following content:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -g -i /var/lib/ntp -u ntp:ntp -p /run/ntpd.pid

```

Then, edit `/etc/ntp.conf` to change the driftfile path such that it is relative to the chroot directory, rather than to the real system root. Change:

```
driftfile       /var/lib/ntp/ntp.drift

```

to

```
driftfile       /ntp.drift

```

Create a suitable chroot environment so that getaddrinfo() will work by creating pertinent directories and files (as root):

```
# mkdir /var/lib/ntp/etc /var/lib/ntp/lib /var/lib/ntp/proc
# touch /var/lib/ntp/etc/resolv.conf /var/lib/ntp/etc/services

```

and by bind-mounting the aformentioned files:

 `/etc/fstab` 

```
...
#ntpd chroot mounts
/etc/resolv.conf  /var/lib/ntp/etc/resolv.conf none bind 0 0
/etc/services	  /var/lib/ntp/etc/services none bind 0 0
/lib		  /var/lib/ntp/lib none bind 0 0
/proc		  /var/lib/ntp/proc none bind 0 0

```

```
# mount -a

```

Finally, restart `ntpd` daemon again. Once it restarted you can verify that the daemon process is chrooted by checking where `/proc/{PID}/root` symlinks to:

```
# ps -C ntpd | awk '{print $1}' | sed 1d | while read -r PID; do ls -l /proc/$PID/root; done

```

should now link to `/var/lib/ntp` instead of `/`.

It is relatively difficult to be sure that your driftfile configuration is actually working without waiting a while, as _ntpd_ does not read or write it very often. If you get it wrong, it will log an error; if you get it right, it will update the timestamp. If you do not see any errors about it after a full day of running, and the timestamp is updated, you should be confident of success.

## See also

*   [http://www.ntp.org/](http://www.ntp.org/)
*   [https://support.ntp.org/](https://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [https://www.eecis.udel.edu/~mills/ntp/html/index.html](https://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Network_Time_Protocol_daemon&oldid=412005](https://wiki.archlinux.org/index.php?title=Network_Time_Protocol_daemon&oldid=412005)"