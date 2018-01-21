[OpenNTPD](http://www.openntpd.org/) (part of the OpenBSD project) is a daemon that can be used to synchronize the system clock to internet time servers using the Network Time Protocol, and can also act as a time server itself if needed. It implements the Simple Network Time Protocol version 4, as described in RFC 5905, and the Network Time Protocol version 3, as described in RFC 1305.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Client](#Client)
    *   [2.2 Server](#Server)
*   [3 Usage](#Usage)
    *   [3.1 Start OpenNTPD at boot](#Start_OpenNTPD_at_boot)
    *   [3.2 Making openntpd dependent upon network access](#Making_openntpd_dependent_upon_network_access)
        *   [3.2.1 Using NetworkManager dispatcher](#Using_NetworkManager_dispatcher)
        *   [3.2.2 Using wicd](#Using_wicd)
        *   [3.2.3 Using dhclient hooks](#Using_dhclient_hooks)
        *   [3.2.4 Using dhcpcd hooks](#Using_dhcpcd_hooks)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Error adjusting time](#Error_adjusting_time)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [openntpd](https://www.archlinux.org/packages/?name=openntpd) package. The default configuration is actually usable if all you want is to sync the time of the local computer.

## Configuration

To configure OpenNTPD, you need to edit `/etc/ntpd.conf`. See [ntpd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ntpd.conf.5) for all available options.

**Tip:** After configuring, check the configuration file for validity by executing:
```
$ ntpd -n

```

**Note:** [HTTPS constraint feature](https://marc.info/?l=openbsd-tech&m=142356166731390&w=2) is not supported by [openntpd](https://www.archlinux.org/packages/?name=openntpd), it requires OpenNTPD to be built with LibreSSL. [openntpd](https://www.archlinux.org/packages/?name=openntpd) is built with OpenSSL.

### Client

To sync to a single particular server, uncomment and edit the "server" directive.

 `/etc/ntpd.conf` 
```
server ntp.example.org

```

The "servers" directive works the same as the "server" directive, however, if the DNS name resolves to multiple IP address, ALL of them will be synced to. The default, "pool.ntp.org" is working and should be acceptable in most cases. You can find the server's URL in your area at [www.pool.ntp.org/zone/@](http://www.pool.ntp.org/zone/@).

 `/etc/ntpd.conf` 
```
servers pool.ntp.org

```

Any number of "server" or "servers" directives may be used.

### Server

If you want the computer you run OpenNTPD on to also be a time server, simply uncomment and edit the "listen" directive.

For example:

 `/etc/ntpd.conf` 
```
listen on *

```

will listen on all interfaces, and

 `/etc/ntpd.conf` 
```
listen on 127.0.0.1
listen on ::1

```

will only listen on the loopback interface.

Your time server will only begin to serve time after it has synchronized itself to a high resolution. This may take hours, or days, depending on the accuracy of your system.

## Usage

### Start OpenNTPD at boot

[Enable](/index.php/Enable "Enable") `openntpd.service`.

### Making openntpd dependent upon network access

If you have intermittent network access (you roam around on a laptop, you use dial-up, etc), it does not make sense to have `openntpd` running as a system daemon on start up. Here are a few ways you can control `openntpd` based on the presence of a network connection.

#### Using NetworkManager dispatcher

OpenNTPD can be brought up/down along with a network connection through the use of [NetworkManager's dispatcher scripts](/index.php/NetworkManager#Network_services_with_NetworkManager_dispatcher "NetworkManager").

Install [networkmanager-dispatcher-openntpd](https://www.archlinux.org/packages/?name=networkmanager-dispatcher-openntpd).

#### Using wicd

Create these two scripts and mark them executable using [chmod](/index.php/Chmod "Chmod").

 `/etc/wicd/scripts/postconnect/openntpd-start.sh` 
```
#!/bin/sh
systemctl start openntpd.service

```
 `/etc/wicd/scripts/predisconnect/openntpd-stop.sh` 
```
#!/bin/sh
systemctl stop openntpd.service

```

#### Using dhclient hooks

Another possibility is to use dhclient hooks to start and stop openntpd. When dhclient detects a change in state it will run the following scripts:

*   `/etc/dhclient-enter-hooks`
*   `/etc/dhclient-exit-hooks`

See [dhclient-script(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhclient-script.8)

#### Using dhcpcd hooks

 `/etc/dhcpcd.exit-hook` 
```
if $if_up; then
	systemctl start openntpd.service
elif $if_down; then
	systemctl stop openntpd.service
fi

```

See [dhcpcd-run-hooks(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd-run-hooks.8)

## Troubleshooting

### Error adjusting time

If you find your time set incorrectly and in log you see:

```
openntpd adjtime failed: Invalid argument

```

Try:

```
# ntpd -s -d

```

This is also how you would manually sync your system.

## See also

*   [http://www.openntpd.org](http://www.openntpd.org)
*   [OpenNTPD Portable](https://github.com/openntpd-portable/openntpd-portable)