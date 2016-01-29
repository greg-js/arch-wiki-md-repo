# Pacserve

[Pacserve](http://xyne.archlinux.ca/projects/pacserve/) allows to easily share pacman packages between computers. This is very useful, if you have a slow internet connection, but multiple machines running Arch Linux.

## Contents

*   [1 Installation](#Installation)
*   [2 Standalone usage](#Standalone_usage)
*   [3 Configure Pacman to use Pacserve](#Configure_Pacman_to_use_Pacserve)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Problems if using external downloaders in pacman.conf](#Problems_if_using_external_downloaders_in_pacman.conf)

## Installation

You can either install [pacserve](https://aur.archlinux.org/packages/pacserve/)<sup><small>AUR</small></sup> manually from the [AUR](/index.php/AUR "AUR"), or from one of the [xyne-any](/index.php/Unofficial_user_repositories#xyne-any "Unofficial user repositories"), [xyne-x86_64](/index.php/Unofficial_user_repositories#xyne-x86_64 "Unofficial user repositories") or [xyne-i686](/index.php/Unofficial_user_repositories#xyne-i686 "Unofficial user repositories") unofficial repositories.

Finally [start/enable](/index.php/Start/enable "Start/enable") `pacserve.service`.

In case you use [iptables](/index.php/Iptables "Iptables"), you will probably want to start `pacserve-ports.service` too.

## Standalone usage

Instead of pacman, use the _pacsrv_ wrapper to perform an update, install packages and so on. It will automatically download all packages from the LAN, if someone hosts them with pacserve there. Otherwise it will just download them from the internet mirrors, as usually. For example:

```
# pacsrv -Syu
# pacsrv -S openssh

```

## Configure Pacman to use Pacserve

If you are always running the pacserve daemon and want pacman to use it without the wrapper, add the following line below **each** repository in /etc/pacman.conf:

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

Alternatively (for official mirrors only), you may insert the _Include..._-line at the top of the Pacman mirrorlist file or let _pacman.conf-insert_pacserve_ generate a _pacman.conf_ file for you.

## Troubleshooting

### Problems if using external downloaders in pacman.conf

If you are using an external downloader such as [wget](/index.php/Wget "Wget"), _pacsrv_ may return errors when downloading. To work around these errors, simply quote the url and output formatting strings (`%u` resp. `%o`) using single quotes:

```
XferCommand = /usr/bin/wget --timeout=6 --passive-ftp -c -O '%o' '%u'

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Pacserve&oldid=408558](https://wiki.archlinux.org/index.php?title=Pacserve&oldid=408558)"