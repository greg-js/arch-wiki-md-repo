Related articles

*   [init](/index.php/Init "Init")

**Warning:** Arch Linux only has official support for [systemd](/index.php/Systemd "Systemd"). When using OpenRC, please mention so in support requests.

[OpenRC](https://wiki.gentoo.org/wiki/OpenRC) is a service manager maintained by the Gentoo developers. OpenRC is dependency based and works with the system provided init program, normally [SysVinit](/index.php/SysVinit "SysVinit").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Booting](#Booting)
*   [2 Configuration](#Configuration)
    *   [2.1 Services](#Services)
    *   [2.2 Network](#Network)
    *   [2.3 Boot logs](#Boot_logs)
    *   [2.4 Hostname](#Hostname)
    *   [2.5 Kernel modules](#Kernel_modules)
    *   [2.6 Locale](#Locale)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Quiet booting](#Quiet_booting)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Error while unmounting /tmp](#Error_while_unmounting_/tmp)
    *   [5.2 Disabling IPv6 does not work](#Disabling_IPv6_does_not_work)
    *   [5.3 During shutdown remounting root as read-only fails](#During_shutdown_remounting_root_as_read-only_fails)
    *   [5.4 /etc/sysctl.conf not found](#/etc/sysctl.conf_not_found)
    *   [5.5 opentmpfiles-setup failed to start](#opentmpfiles-setup_failed_to_start)
*   [6 Using OpenRC with a desktop environment](#Using_OpenRC_with_a_desktop_environment)
*   [7 Reverting to systemd](#Reverting_to_systemd)
*   [8 See also](#See_also)

## Installation

**Warning:** [openrc](https://aur.archlinux.org/packages/openrc/) depends (implicitly) on [sysvinit](https://aur.archlinux.org/packages/sysvinit/), which conflicts with [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat). Therefore the system boots with plain sysvinit by default (not OpenRC or systemd), be sure to add a correct `init=*some-init*` kernel parameter.

OpenRC and accompanying packages are available in the [AUR](/index.php/AUR "AUR"). For details on init components, see [Init](/index.php/Init "Init").

Install either the [openrc](https://aur.archlinux.org/packages/openrc/) or [openrc-git](https://aur.archlinux.org/packages/openrc-git/) package. From version 0.25 onward, OpenRC provides its own init at `/usr/bin/openrc-init`. Optionally, you can use other inits from, e.g., [busybox](https://www.archlinux.org/packages/?name=busybox) or [openrc-sysvinit](https://aur.archlinux.org/packages/openrc-sysvinit/). Note that when `openrc-init` is used, it must be paired with `openrc-shutdown`, and *not* the `shutdown` or `reboot` commands from other packages, otherwise you will encounter errors.

A basic set of service files are available from the [openrc-arch-services-git](https://aur.archlinux.org/packages/openrc-arch-services-git/) package. Other packages may have service files provided outside this package; a search on the AUR is recommended.

To maintain compatibility with [initscripts-fork](https://aur.archlinux.org/packages/initscripts-fork/), configuration files are installed to `/etc/openrc/`.

### Booting

For booting with OpenRC set the `init` option in the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").
To use OpenRC's built-in init, set `init=/usr/bin/openrc-init`. To use [SysVinit](/index.php/SysVinit "SysVinit"), provided by [openrc-sysvinit](https://aur.archlinux.org/packages/openrc-sysvinit/), set `init=/usr/bin/init-openrc`.
Note that when using `openrc-init`, the `/etc/inittab` file is not used.

## Configuration

The `/etc/openrc/conf.d` directory, and the `/etc/openrc/rc.d` file is used for configuration.

For general information on configuring OpenRC, see:

*   [OpenRC manuals](http://www.calculate-linux.org/main/en/openrc_manuals)
*   [OpenRC migration](http://www.gentoo.org/doc/en/openrc-migration.xml)
*   [gentoo wiki](http://wiki.gentoo.org/wiki/OpenRC).

For instructions when migrating from [systemd](/index.php/Systemd "Systemd"), see [Init#Configuration](/index.php/Init#Configuration "Init").

### Services

OpenRC services are enabled by issuing `rc-update add *service_name* *runlevel*` as root. It is recommended to at least enable the following services:

| Service name | [Runlevel](https://wiki.gentoo.org/wiki/OpenRC#Named_runlevels) | Description |
| udev | sysinit | Device hot-plugging |
| alsa | default | [ALSA](/index.php/ALSA "ALSA") state |
| acpid | default | ACPI events |
| dbus | default | Messaging bus |
| dcron | default | Scheduling |
| syslog-ng | default | System logs |

**Warning:** If using `init=/usr/bin/openrc-init` in your kernel parameters, you'll need to manually enable [getty](/index.php/Getty "Getty") services, otherwise you'll be left with no interactive TTYs[[1]](https://github.com/OpenRC/openrc/blob/master/agetty-guide.md)

If necessary, create services for each wanted [getty](/index.php/Getty "Getty") by creating symbolic links to `/etc/openrc/init.d/getty`. E.g. for `/dev/tty1`:

```
# ln -s /etc/openrc/init.d/agetty{,.tty1}
# rc-update add agetty.tty1 default

```

See also [Native services](https://wiki.gentoo.org/wiki/Systemd#Native_services) and [Daemons](/index.php/Daemons "Daemons").

### Network

The network is configured through `newnet`. [[2]](https://github.com/funtoo/openrc/blob/master/README.newnet) Modify the `/etc/openrc/conf.d/network` file; both the `ip` ([iproute2](https://www.archlinux.org/packages/?name=iproute2)) and the `ifconfig` ([net-tools](https://www.archlinux.org/packages/?name=net-tools)) commands are supported. Below is an example configuration using `ip`.

```
ip_eth0="192.168.1.2/24"
defaultiproute="via 192.168.1.1"
ifup_eth0="ip link set \$int mtu 1500"

```

The network service is added to the boot runlevel by default, so no further action is required. See [Network configuration](/index.php/Network_configuration "Network configuration") for general networking information.

**Note:** You may also use [NetworkManager](/index.php/NetworkManager "NetworkManager"), [dhcpcd](/index.php/Dhcpcd "Dhcpcd") or [netcfg](https://aur.archlinux.org/packages/netcfg/) by enabling the respective services. *netcfg* mimics the [netctl](/index.php/Netctl "Netctl") behaviour (see [[3]](https://bbs.archlinux.org/viewtopic.php?pid=1489283#p1489283) if you want to enable profiles connection on booting - requires `wpa_actiond`). See [netcfg features](https://www.archlinux.org/netcfg/features.html).

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

See [[4]](http://wiki.gentoo.org/wiki/Localization/HOWTO#Keyboard_layout_for_the_console) and [Locale](/index.php/Locale "Locale") for details.

## Usage

This section draws a parallel between [systemd](/index.php/Systemd "Systemd") and other [init](/index.php/Init "Init") systems.

You can omit the `.service` and `.target` extensions, especially if temporarily editing the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

| systemd | SysVinit | OpenRC | Description |
| `systemctl list-units` | `rc.d list` | `rc-status` | List running services status |
| `systemctl --failed` | `rc-status --crashed` | Check failed services |
| `systemctl --all` | `rc-update -v show` | Display all available services. |
| `systemctl (start, stop, restart, status) daemon.service` | `rc.d (start, stop, restart) daemon` | `rc-service daemon (start, stop, restart, status)` | Change service state. |
| `systemctl (enable, disable) daemon.service` | `chkconfig daemon (on, off)` | `rc-update (add, del) daemon` | Turn service on or off. |
| `systemctl daemon-reload` | `chkconfig daemon --add` | Create or modify configuration. |

## Tips and tricks

### Quiet booting

To hide boot messages from OpenRC, you can edit `/etc/inittab` and add `--quiet` to every openrc command. For further information check with `$ openrc -h`.

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

By default, `sysctl --system` is called to load the sysctl configuration. [[5]](https://github.com/OpenRC/openrc/blob/master/init.d/sysctl.Linux.in#L17) This includes the `/etc/sysctl.conf` file, which was removed from Arch. [[6]](https://www.archlinux.org/news/deprecation-of-etcsysctlconf/)

To prevent a missing file error, create the file:

```
# touch /etc/sysctl.conf

```

### opentmpfiles-setup failed to start

On booting openrc you may see lines like these :

```
* Setting up tmpfiles.d entries ...
chattr: Operation not supported while setting flags on /var/log/journal
chattr: No such file or directory while trying to stat /var/log/journal/%m
chattr: Operation not supported while setting flags on /var/log/journal/remote
[ !! ]
ERROR: opentmpfiles-setup failed to start

```

This is caused by `/usr/lib/tmpfiles.d/journal-nocow.conf` using options that are only valid if journal is on a btrfs filesystem.

See [https://github.com/OpenRC/opentmpfiles/issues/2](https://github.com/OpenRC/opentmpfiles/issues/2) for details

A workaround is to create an empty /etc/tmpfiles.d/journal-nocow.conf to override the settings.

## Using OpenRC with a desktop environment

If using *OpenRC* with a [desktop environment](/index.php/Desktop_environment "Desktop environment"), ConsoleKit may help. Install the [service](https://gist.github.com/ad73f9087f39d7cadd8e) to `/etc/openrc/init.d`, and enable it:

```
# rc-update add consolekit default

```

See [ConsoleKit](/index.php/ConsoleKit "ConsoleKit") for more information.

Begin with OpenRC 0.28 SysVinit is replaced with openrc-init, shutdown is replaced with openrc-shutdown, by using consolekit the system may hang up when shuting down from desktop session. So use [elogind-git](https://aur.archlinux.org/packages/elogind-git/) instead. Enable it with:

```
# rc-update add elogind default

```

Also you need to replace polkit-consolekit with [polkit-elogind](https://aur.archlinux.org/packages/polkit-elogind/), or the system will alarm "not authorized to perform operation" when mounting usb device, and can't reboot or shutdown from the desktop session.

## Reverting to systemd

Reverting to systemd should be straightforward in most cases. It is essentially the reversal of migrating to OpenRC, with care placed on the following:

*   Removal of, or otherwise editing, the `init=` parameter on the kernel command line
*   Replacement of any OpenRC-tailored or no-systemd packages with their stock equivalents (e.g. replacement of [dbus-nosystemd](https://aur.archlinux.org/packages/dbus-nosystemd/) with [dbus](https://www.archlinux.org/packages/?name=dbus))

## See also

*   [Wikipedia:OpenRC](https://en.wikipedia.org/wiki/OpenRC "wikipedia:OpenRC")
*   [Gentoo wiki](https://wiki.gentoo.org/wiki/OpenRC)
*   [Forum thread about OpenRC in Arch](https://bbs.archlinux.org/viewtopic.php?id=152606)
*   [Blog: OpenRC on Arch Linux](http://blog.notfoss.com/posts/openrc-on-arch-linux/)
*   [Manjaro wiki](https://wiki.manjaro.org/index.php?title=OpenRC,_an_alternative_to_systemd)