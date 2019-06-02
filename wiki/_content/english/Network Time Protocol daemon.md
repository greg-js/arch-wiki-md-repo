[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") is the most common method to synchronize the [software clock](/index.php/System_time "System time") of a GNU/Linux system with internet time servers. It is designed to mitigate the effects of variable network latency and can usually maintain time to within tens of milliseconds over the public Internet. The accuracy on local area networks is even better, up to one millisecond.

[The NTP Project](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project) provides a reference implementation of the protocol called simply NTP. This article further describes how to set up and run the NTP daemon, both as a client and as a server.

See [System time#Time synchronization](/index.php/System_time#Time_synchronization "System time") for other NTP implementations.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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
    *   [4.4 Restrict listening sockets](#Restrict_listening_sockets)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [ntp](https://www.archlinux.org/packages/?name=ntp) package. By default, *ntpd* works in client mode without further configuration. You can skip to [#Usage](#Usage), if you want to use the Arch Linux default configuration file for it. For server configuration, see [#NTP server mode](#NTP_server_mode).

## Configuration

The main daemon is *ntpd*, which is configured in `/etc/ntp.conf`. Refer to [ntp.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntp.conf.5) for detail.

### Connection to NTP servers

NTP servers are classified in a hierarchical system with many levels called *strata*: the devices which are considered independent time sources are classified as *stratum 0* sources; the servers directly connected to *stratum 0* devices are classified as *stratum 1* sources; servers connected to *stratum 1* sources are then classified as *stratum 2* sources and so on.

It has to be understood that a server's stratum cannot be taken as an indication of its accuracy or reliability. Typically, stratum 2 servers are used for general synchronization purposes: if you do not already know the servers you are going to connect to, you should choose a server pool close to your location from the [pool.ntp.org](http://www.pool.ntp.org/) servers ([alternative link](http://support.ntp.org/bin/view/Servers/NTPPoolServers)).

Since *ntp* version 4.2.7.p465-2, Arch Linux uses its own default vendor pool of NTP servers provided by [the NTP Pool Project](http://www.pool.ntp.org) (see [FS#41700](https://bugs.archlinux.org/task/41700)). Modify those to suit your needs, e.g. if you want to use your country's servers with an option:

 `/etc/ntp.conf` 
```
server 0.fr.pool.ntp.org iburst
server 1.fr.pool.ntp.org iburst
server 2.fr.pool.ntp.org iburst
server 3.fr.pool.ntp.org iburst

```

The `iburst` option is recommended, and sends a burst of packets only if it cannot obtain a connection with the first attempt. The `burst` option always does this, even on the first attempt, and should never be used without explicit permission and may result in blacklisting.

### NTP server mode

If setting up an NTP server, you need to add [*local clock*](http://www.ntp.org/ntpfaq/NTP-s-refclk.htm#Q-LOCAL-CLOCK) as a server, so that, in case it loses internet access, it will continue serving time to the network; add *local clock* as a stratum 10 server (using the *fudge* command) (you can set up to [stratum 15](http://www.ntp.org/ntpfaq/NTP-s-algo.htm#Q-ALGO-BASIC-STRATUM)) so that it will never be used unless internet access is lost:

```
server 127.127.1.1
fudge  127.127.1.1 stratum 12

```

Next, define the rules that will allow clients to connect to your service (*localhost* is considered a client too) using the *restrict* command; you should already have a line like this in your file:

```
restrict default nomodify nopeer noquery

```

This restricts everyone from modifying anything and prevents everyone from querying the status of your time server: `nomodify` prevents reconfiguring *ntpd* (with *ntpq* or *ntpdc*), and `noquery` is important to [prevent](https://mailman.archlinux.org/pipermail/arch-dev-public/2014-February/025872.html) dumping status data from *ntpd* (also with *ntpq* or *ntpdc*).

You can also add other options:

```
restrict default kod nomodify notrap nopeer noquery

```

**Note:** This still allows other people to query your time server. You need to add `noserve` to stop serving time. It will also block time synchronization since it blocks all packets except *ntpq* and *ntpdc* queries.

If you want to change any of these, see the full docs for the "restrict" option in [ntp.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntp.conf.5), the detailed ntp [instructions](https://support.ntp.org/bin/view/Support/AccessRestrictions) and [#Usage](#Usage).

Following this line, you need to tell *ntpd* what to allow through into your server; the following line is enough if you are not configuring an NTP server:

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

**Note:** Defining the log file is not mandatory, but it is always a good idea to have feedback for *ntpd* operations.

## Usage

The package has a default client-mode configuration and its own user and group to drop root privileges after starting. If you start it from the console, you should always do so with the `-u` option:

```
# ntpd -u ntp:ntp

```

The `-u` option is employed by the two included systemd services. These services also use the `-g` option, which disables a threshold (so-called *panic-gate*). Hence, they will synchonize time even in case the ntp-server's time exceeds the threshold deviation from the system clock.

**Warning:** One reason the panic-gate was introduced is that background jobs/services may be susceptible to time-jumps. If the system's clock was never synchronized before, consider stopping them before running *ntpd* for the first time.

Both services are tied to the system's resolver, and will start synchronizing when an active network connection is detected.

### Start ntpd at boot

[Enable](/index.php/Enable "Enable") the daemon with `ntpd.service`. See also [#Running in a chroot](#Running_in_a_chroot).

**Note:** The systemd command *timedatectl* can only be used to control [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd"). Executing `timedatectl set-ntp 1` as root will inadvertedly stop a running `ntpd.service`.[[1]](http://lists.freedesktop.org/archives/systemd-devel/2015-April/030277.html)

Use *ntpq* to see the list of configured peers and status of synchronization:

```
$ ntpq -p

```

The delay, offset and jitter columns should be non-zero. The servers *ntpd* is synchronizing with are prefixed by an asterisk. It can take several minutes before *ntpd* selects a server to synchronize with; try checking after 17 minutes (1024 seconds).

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

*ntpd* can be started by your network manager, so that the daemon only runs when the computer is online.

	Netctl

Append the following lines to your [netctl](/index.php/Netctl "Netctl") profile:

```
ExecUpPost='/usr/bin/ntpd || true'
ExecDownPre='killall ntpd || true'

```

	NetworkManager

The *ntpd* daemon can be brought up/down along with a network connection through the use of NetworkManager's [dispatcher](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager") scripts. The [networkmanager-dispatcher-ntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-ntpd) package installs one, pre-configured to start and stop the [ntpd service](#Start_ntpd_at_boot) with a connection.

	Wicd

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

**Note:** You are advised to customize the options for the *ntpd* command as explained in [#Usage](#Usage).

See also [Wicd#Scripts](/index.php/Wicd#Scripts "Wicd").

	KDE

KDE can use NTP (ntp must be installed) by right clicking the clock and selecting *Adjust date/time*. However, this requires the ntp daemon to be [disabled](/index.php/Disable "Disable") before configuring KDE to use NTP. [[2]](https://bugs.kde.org/show_bug.cgi?id=178968)

### Using ntpd with GPS

Most of the articles online about configuring *ntpd* to receive time from a GPS suggest to use the SHM (shared memory) method. However, at least since *ntpd* version 4.2.8 a *much better* method is available. It connects directly to *gpsd*, so [gpsd](https://www.archlinux.org/packages/?name=gpsd) needs to be installed.

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

This will work as long as you have *gpsd* working. It connects to *gpsd* via the local socket and queries the "gpsd_json" object that is returned.

To test the setup, first ensure that *gpsd* is working by running:

```
 $ cgps -s 

```

Then wait a few minutes and run `ntpq -p`. This will show if *ntpd* is talking to *gpsd*:

 `$ ntpq -p` 
```
remote           refid            st t when poll reach   delay   offset  jitter
 ==================================================================================
*GPSD_JSON(0)    .GPS.            0 l   55   64  377    0.000    2.556  14.109
```

**Tip:** If the *reach* column is 0, it means *ntpd* has not been able to talk to *gpsd*. Wait a few minutes and try again. Sometimes it takes *ntpd* a while.

**Note:** *ntpd* expects that your GPS device is called e.g. `/dev/gps0`. If your GPS device is connected via USB, it may appear as `/dev/ttyUSB0` instead, and you may have to create a symlink `ln -s /dev/ttyUSB0 /dev/gps0` and run *gpsd* on that linked `/dev/gps0` so that the `GPSD_JSON` line appears as expected. *gpsd* should be run with the `-n` flag on the `GPSD_OPTIONS` line and use `/dev/gps0` on the `DEVICES` line in the `/etc/default/gpsd` config file.

### Running in a chroot

**Note:** *ntpd* should be started as non-root (default in the Arch Linux package) before attempting to jail it in a chroot, since chroots are relatively useless at securing processes running as root.

Create a new directory `/etc/systemd/system/ntpd.service.d/` if it does not exist and a file named `customexec.conf` inside with the following content:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -g -u ntp:ntp **-i /var/lib/ntp**

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
# mkdir /var/lib/ntp/usr /var/lib/ntp/usr/lib
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
/usr/lib	  /var/lib/ntp/usr/lib none bind 0 0
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

It is relatively difficult to be sure that your driftfile configuration is actually working without waiting a while, as *ntpd* does not read or write it very often. If you get it wrong, it will log an error; if you get it right, it will update the timestamp. If you do not see any errors about it after a full day of running, and the timestamp is updated, you should be confident of success.

### Restrict listening sockets

You can limit sockets *ntpd* is listening to using the *interface* option:

```
interface [listen | ignore | drop] [all | ipv4 | ipv6 | wildcard | name | address[/prefixlen]]

```

like

 `/etc/ntp.conf` 
```
interface listen lo
interface listen enp3s0
interface ignore enp5s0
```

## See also

*   [http://www.ntp.org/](http://www.ntp.org/)
*   [https://support.ntp.org/](https://support.ntp.org/)
*   [http://www.pool.ntp.org/](http://www.pool.ntp.org/)
*   [https://www.eecis.udel.edu/~mills/ntp/html/index.html](https://www.eecis.udel.edu/~mills/ntp/html/index.html)
*   [http://www.akadia.com/services/ntp_synchronize.html](http://www.akadia.com/services/ntp_synchronize.html)