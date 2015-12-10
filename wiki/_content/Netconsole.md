# Netconsole

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**netconsole** is a kernel module that sends all kernel log messages (i.e. dmesg) over the network to another computer, without involving user space (e.g. syslogd). Name "netconsole" is a misnomer because it's not really a "console", more like a remote logging service.

It can be used either built-in or as a module. Built-in _netconsole_ initializes immediately after NIC cards and will bring up the specified interface as soon as possible. The module is mainly used for capturing kernel panic output from a headless machine, or in other situations where the user space is no more functional.

Documentation is available in the Linux kernel tree under [Documentation/networking/netconsole.txt](https://www.kernel.org/doc/Documentation/networking/netconsole.txt).

## Contents

*   [1 Sender configuration](#Sender_configuration)
    *   [1.1 Built-in Configuration](#Built-in_Configuration)
    *   [1.2 Runtime configuration](#Runtime_configuration)
*   [2 Receiver configuration](#Receiver_configuration)
*   [3 See also](#See_also)

## Sender configuration

### Built-in Configuration

Netconsole can be configured via the `netconsole` [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") in the following format:

```
netconsole=[src-port]@[src-ip]/[<dev>],[tgt-port]@<tgt-ip>/[tgt-macaddr]

```

where the fields have the following meaning:

*   `src-port` — source for UDP packets (defaults to 6665)
*   `src-ip` — source IP to use (interface address)
*   `dev` — network interface (eth0)
*   `tgt-port` — port for logging agent (6666)
*   `tgt-ip` — IP address for logging agent
*   `tgt-macaddr` — ethernet MAC address for logging agent (broadcast)

For example:

```
netconsole=6665@192.168.1.28/eth0,6666@192.168.1.19/00:13:32:20:r9:a5'

```

**Note:** MAC address is optional, but the slash must stay: `...,6666@192.168.1.19/`

The logging level can be set with the `loglevel` kernel parameter, e.g.:

```
loglevel=7

```

### Runtime configuration

Netconsole can be loaded as _kernel module_ manually after boot or automatically during boot depending on the module configuration (see [Kernel modules](/index.php/Kernel_modules "Kernel modules") for details).

To load the `netconsole` module manually any time after boot:

```
# set log level for kernel messages
dmesg -n 8

modprobe configfs
modprobe netconsole
mount none -t configfs /sys/kernel/config

# 'netconsole' dir is auto created if the module is loaded 
mkdir /sys/kernel/config/netconsole/target1
cd /sys/kernel/config/netconsole/target1

# set local IP address
echo 192.168.0.111 > local_ip
# set destination IP address
echo 192.168.0.17 > remote_ip
# set local network device name (find it trough ifconfig, examples: eth0, eno1, wlan0)
echo eno1 > dev_name
# find destination MAC address
arping $(cat remote_ip) -f | grep -o ..:..:..:..:..:.. > remote_mac

echo 1 > enabled

```

Netconsole should now be configured. To verify, run `dmesg | tail` and you should see "netconsole: network logging started". Check available log levels by running `dmesg -h`.

## Receiver configuration

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Netconsole#](https://wiki.archlinux.org/index.php/Talk:Netconsole))

Install [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) or [socat](https://www.archlinux.org/packages/?name=socat) from the [official repositories](/index.php/Official_repositories "Official repositories").

```
nc -u -l 6666

```

or

```
nc -u -l -p 6666

```

Logging is done by your ArchLinux set logger like _syslog-ng_, so available loglevels (output details) are defined in that logger docs, and may differ for each log type. One can also pass _netconsole_ string parameters at kernel runtime (no config file required), then start two _netconsole_ instances on the monitoring PC (one to read output, another for input), and restart it on the PC or device you are logging as shown in _Dynamic Configuration_:

```
# set log level for kernel messages
dmesg -n 8

netconsole=6666@192.168.1.28/eth0,6666@192.168.1.19/00:13:32:20:r9:a5

{{Note| MAC address is optional.}}

nc -l -u -p 6666 &
nc -u 192.168.1.28 6666

# socat as alternative to nc in one command
socat - udp4-datagram:192.168.1.28:6666,bind=6666

```

One may need to switch off PC and router firewall, and setup proper router port forwarding to monitor and input data in _Netconsole_. A more flexible configuration can be achieved if netconsole is setup on a [different subnet](http://archlinuxarm.org/forum/viewtopic.php?f=18&t=3355) so that if the device is moved to a different network IP's won't clash, however [it may require a more complex setup](http://archlinuxarm.org/platforms/armv5/seagate-goflex-home#qt-platform_tabs-ui-tabs3) on the receiver with aliased ethernet interface.

## See also

*   [Boot debugging#netconsole](/index.php/Boot_debugging#netconsole "Boot debugging")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Netconsole&oldid=410376](https://wiki.archlinux.org/index.php?title=Netconsole&oldid=410376)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Kernel](/index.php/Category:Kernel "Category:Kernel")
*   [Networking](/index.php/Category:Networking "Category:Networking")