# OpenRC

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [eudev](/index.php/Eudev "Eudev")
*   [init](/index.php/Init "Init")
*   [init Rosetta](/index.php/Init_Rosetta "Init Rosetta")
*   [SysVinit](/index.php/SysVinit "SysVinit")

**Warning:** Arch Linux only has official support for [systemd](/index.php/Systemd "Systemd"). When using OpenRC, please mention so in support requests.

[OpenRC](https://wiki.gentoo.org/wiki/OpenRC) is a service manager maintained by the Gentoo developers. OpenRC is dependency based and works with the system provided init program, normally [SysVinit](/index.php/SysVinit "SysVinit").

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Booting](#Booting)
*   [2 Configuration](#Configuration)
    *   [2.1 Preparation](#Preparation)
    *   [2.2 Services](#Services)
    *   [2.3 Network](#Network)
    *   [2.4 Boot logs](#Boot_logs)
    *   [2.5 Hostname](#Hostname)
    *   [2.6 Kernel modules](#Kernel_modules)
    *   [2.7 Locale](#Locale)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Error while unmounting /tmp](#Error_while_unmounting_.2Ftmp)
    *   [3.2 Disabling IPv6 does not work](#Disabling_IPv6_does_not_work)
    *   [3.3 During shutdown remounting root as read-only fails](#During_shutdown_remounting_root_as_read-only_fails)
    *   [3.4 /etc/sysctl.conf not found](#.2Fetc.2Fsysctl.conf_not_found)
*   [4 Using OpenRC with a desktop environment](#Using_OpenRC_with_a_desktop_environment)
*   [5 See also](#See_also)

## Installation

OpenRC and accompanying packages are available in the [AUR](/index.php/AUR "AUR"). For details on init components, see [Init](/index.php/Init "Init").

Install either the [openrc](https://aur.archlinux.org/packages/openrc/)<sup><small>AUR</small></sup> or [openrc-git](https://aur.archlinux.org/packages/openrc-git/)<sup><small>AUR</small></sup> package. [openrc-sysvinit](https://aur.archlinux.org/packages/openrc-sysvinit/)<sup><small>AUR</small></sup> or [busybox](https://www.archlinux.org/packages/?name=busybox) are used as the init process. Service files are available from the [openrc-arch-services-git](https://aur.archlinux.org/packages/openrc-arch-services-git/)<sup><small>AUR</small></sup> package.

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** [openrc-sysvinit](https://aur.archlinux.org/packages/openrc-sysvinit/)<sup><small>AUR</small></sup> removes [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) (Discuss in [Talk:OpenRC#](https://wiki.archlinux.org/index.php/Talk:OpenRC))

To maintain compability with [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/)<sup><small>AUR</small></sup>, configuration files are installed to `**/etc/openrc/**`. The sysvinit init binary is installed to `/usr/bin/init-openrc` for compability with [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) or similar packages.

### Booting

For booting with OpenRC add `init=/usr/bin/init-openrc` to the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). To switch back to systemd, remove the parameter again.

The `/etc/openrc/conf.d` directory, and the `/etc/openrc/rc.d` file is used for configuration.

## Configuration

For general information on configuring OpenRC, see:

*   [OpenRC manuals](http://www.calculate-linux.org/main/en/openrc_manuals)
*   [OpenRC migration](http://www.gentoo.org/doc/en/openrc-migration.xml)
*   [gentoo wiki](http://wiki.gentoo.org/wiki/OpenRC).

### Preparation

See [Init#Configuration](/index.php/Init#Configuration "Init").

### Services

OpenRC services are enabled by issuing `rc-update add _service_name_ _runlevel_` as root. It is recommended to at least enable the following services:

<table class="wikitable">

<tbody>

<tr>

<th>Service name</th>

<th>[Runlevel](https://wiki.gentoo.org/wiki/OpenRC#Named_runlevels)</th>

<th>Description</th>

</tr>

<tr>

<td>udev</td>

<td>sysinit</td>

<td>Device hot-plugging</td>

</tr>

<tr>

<td>alsa</td>

<td>default</td>

<td>[ALSA](/index.php/ALSA "ALSA") state</td>

</tr>

<tr>

<td>acpid</td>

<td>default</td>

<td>ACPI events</td>

</tr>

<tr>

<td>dbus</td>

<td>default</td>

<td>Messaging bus</td>

</tr>

<tr>

<td>dcron</td>

<td>default</td>

<td>Scheduling</td>

</tr>

<tr>

<td>syslog-ng</td>

<td>default</td>

<td>System logs</td>

</tr>

</tbody>

</table>

See also [Native services](https://wiki.gentoo.org/wiki/Systemd#Native_services) and [Daemons](/index.php/Daemons "Daemons").

### Network

The network is configured through `newnet`. [[1]](https://github.com/funtoo/openrc/blob/master/README.newnet) Modify the `/etc/openrc/conf.d/network` file; both the `ip` ([iproute2](https://www.archlinux.org/packages/?name=iproute2)) and the `ifconfig` ([net-tools](https://www.archlinux.org/packages/?name=net-tools)) commands are supported. Below is an example configuration using `ip`.

```
ip_eth0="192.168.1.2/24"
defaultiproute="via 192.168.1.1"
ifup_eth0="ip link set \$int mtu 1500"

```

The network service is added to the boot runlevel by default, so no further action is required. See [Network configuration](/index.php/Network_configuration "Network configuration") for general networking information.

**Note:** You may also use [NetworkManager](/index.php/NetworkManager "NetworkManager"), [dhcpcd](/index.php/Dhcpcd "Dhcpcd") or [netcfg](https://aur.archlinux.org/packages/netcfg/)<sup><small>AUR</small></sup> by enabling the respective services. _netcfg_ mimics the [netctl](/index.php/Netctl "Netctl") behaviour (see [[2]](https://bbs.archlinux.org/viewtopic.php?pid=1489283#p1489283) if you want to enable profiles connection on booting - requires `wpa_actiond`). You could consult the [official documentation](https://www.archlinux.org/netcfg/features.html) or [old wiki documentation](https://wiki.archlinux.org/index.php?title=Netcfg&oldid=243178) (be aware of consulting version later than [2012-05-13](https://www.archlinux.org/news/netcfg-282-release/))

### Boot logs

To enable boot logging, uncomment the `rc_logger="YES"` line in `/etc/openrc/rc.conf`. When enabled, boot logs are stored in `/var/log/rc.log`.

### Hostname

OpenRC sets the hostname from `/etc/openrc/conf.d/hostname`. The file looks as follows:

```
# Set to the hostname of this machine
hostname="myhostname"
```

### Kernel modules

OpenRC uses `/etc/openrc/conf.d/modules` instead of `/etc/modules-load.d`. For example:

 `/etc/openrc/conf.d/modules` 

```
# You should consult your kernel documentation and configuration
# for a list of modules and their options.

modules="vboxdrv acpi_cpufreq"
```

### Locale

Keyboard layout can be configured via `/etc/openrc/conf.d/keymaps` and `/etc/openrc/conf.d/consolefont`. You can also configure the settings through the `/etc/locale.conf` file, which is sourced via `/etc/profile.d/locale.sh`.

See [[3]](http://wiki.gentoo.org/wiki/Localization/HOWTO#Keyboard_layout_for_the_console) and [Locale](/index.php/Locale "Locale") for details.

## Troubleshooting

### Error while unmounting /tmp

When shutting the system down, you might get an error message such as

```
* Unmounting /tmp ... 
* in use but fuser finds nothing [ !! ]
```

This can be fixed by adding

```
no_umounts="/tmp"

```

to `/etc/openrc/conf.d/localmount`

**Note:** This problem occurs only if your tmp is mounted as a tmpfs.

### Disabling IPv6 does not work

One option is to add:

```
# Disable ipv6
net.ipv6.conf.all.disable_ipv6 = 1

```

in a file with a `.conf` extension under `/etc/openrc/sysctl.d`

### During shutdown remounting root as read-only fails

If the above happens, edit the `/etc/openrc/init.d/mount-ro` file and put:

```
telinit u

```

after the following line:

```
# Flush all pending disk writes now
sync; sync

```

### /etc/sysctl.conf not found

By default, `sysctl --system` is called to load the sysctl configuration. [[4]](https://github.com/OpenRC/openrc/blob/master/init.d/sysctl.Linux.in#L17) This includes `/etc/sysctl.conf`, which is not present in Arch by default. [[5]](https://www.archlinux.org/news/deprecation-of-etcsysctlconf/)

To prevent a missing file error, create the file:

```
# touch /etc/sysctl.conf

```

## Using OpenRC with a desktop environment

If using _OpenRC_ with a [desktop environment](/index.php/Desktop_environment "Desktop environment"), ConsoleKit may help. Install the [service](https://gist.github.com/ad73f9087f39d7cadd8e) to `/etc/openrc/init.d`, and enable it:

```
# rc-update add consolekit default

```

See [ConsoleKit](/index.php/ConsoleKit "ConsoleKit") for more information.

## See also

*   [Wikipedia:OpenRC](https://en.wikipedia.org/wiki/OpenRC "wikipedia:OpenRC")
*   [Gentoo wiki](https://wiki.gentoo.org/wiki/OpenRC)
*   [Forum thread about OpenRC in Arch](https://bbs.archlinux.org/viewtopic.php?id=152606)
*   [Blog: OpenRC on Arch Linux](http://blog.notfoss.com/posts/openrc-on-arch-linux/)
*   [Manjaro wiki](https://wiki.manjaro.org/index.php?title=OpenRC,_an_alternative_to_systemd)

Retrieved from "[https://wiki.archlinux.org/index.php?title=OpenRC&oldid=405242](https://wiki.archlinux.org/index.php?title=OpenRC&oldid=405242)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Boot process](/index.php/Category:Boot_process "Category:Boot process")