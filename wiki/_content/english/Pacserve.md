[Pacserve](http://xyne.archlinux.ca/projects/pacserve/) allows to easily share pacman packages between computers. This is very useful if you have a slow internet connection and multiple machines running Arch Linux.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 IPv6](#IPv6)
    *   [2.2 Avahi](#Avahi)
*   [3 Standalone usage](#Standalone_usage)
*   [4 Configure Pacman to use Pacserve](#Configure_Pacman_to_use_Pacserve)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Problems if using external downloaders in pacman.conf](#Problems_if_using_external_downloaders_in_pacman.conf)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") [pacserve](https://aur.archlinux.org/packages/pacserve/).

**Tip:** The package is also available in the [xyne-x86_64](/index.php/Unofficial_user_repositories#xyne-x86_64 "Unofficial user repositories") unofficial repository.

Finally [start/enable](/index.php/Start/enable "Start/enable") `pacserve.service`.

In case you use [iptables](/index.php/Iptables "Iptables"), you will probably want to start `pacserve-ports.service` too. For other [firewalls](/index.php/Firewalls "Firewalls") open TCP and UDP ports `15678`. The UDP port can be limited to multicast traffic only.

## Configuration

The `pacserve.service` can configured by editing `PACSERVE_ARGS` in `/etc/pacserve/pacserve.service.conf`. Run `pacserve --help` to see the available options.

### IPv6

To enable [IPv6](/index.php/IPv6 "IPv6") support add the option `--ipv6` to `PACSERVE_ARGS` in `/etc/pacserve/pacserve.service.conf`.

### Avahi

To announce and discover Pacserve using [mDNS](/index.php/MDNS "MDNS") add the option `--avahi` to `PACSERVE_ARGS` in `/etc/pacserve/pacserve.service.conf`.

## Standalone usage

Instead of pacman, use the *pacsrv* wrapper to perform an update, install packages and so on. It will automatically download all packages from the LAN, if someone hosts them with pacserve there. Otherwise it will just download them from the internet mirrors, as usually. For example:

```
# pacsrv -Syu
# pacsrv -S openssh

```

## Configure Pacman to use Pacserve

If you are always running the pacserve daemon and want pacman to use it without the wrapper, insert the following line (before any other `Include` lines) in **each** repository in `/etc/pacman.conf`.

```
Include = /etc/pacman.d/pacserve

```

Here is an example for the Xyne repository:

 `/etc/pacman.conf` 
```
...
[xyne-x86_64]
SigLevel = Required
**Include  = /etc/pacman.d/pacserve**
Server   = http://xyne.archlinux.ca/repos/xyne
...
```

Alternatively (for official mirrors only), you may insert the `Include` line at the top of the Pacman mirrorlist file or let *pacman.conf-insert_pacserve* generate a `pacman.conf` file for you.

## Troubleshooting

### Problems if using external downloaders in pacman.conf

If you are using an external downloader such as [wget](/index.php/Wget "Wget"), *pacsrv* may return errors when downloading. To work around these errors, simply quote the url and output formatting strings (`%u` resp. `%o`) using single quotes:

```
XferCommand = /usr/bin/wget --timeout=6 --passive-ftp -c -O '%o' '%u'

```

## See also

*   [pacserve thread on the Arch Linux forums](https://bbs.archlinux.org/viewtopic.php?id=117094)