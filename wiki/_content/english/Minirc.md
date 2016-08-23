**Warning:** Arch Linux only has official support for [systemd](/index.php/Systemd "Systemd"). When using Minirc, please mention so in support requests.

[Minirc](https://github.com/hut/minirc) is a init script for busybox init maintained by some people on github. Minirc is script based and does not work with other init systems.

## Installation

Minirc is available in the [AUR](/index.php/AUR "AUR"). For details on init components, see [Init](/index.php/Init "Init").

Install the [minirc-git](https://aur.archlinux.org/packages/minirc-git/) package. Minirc replaces /sbin/init so it removes systemd-sysvcompat. It will also conflict with [SysVinit](/index.php/SysVinit "SysVinit"), if you have it installed.

Also if you are using a desktop environment, It might help to install [ConsoleKit](/index.php/ConsoleKit "ConsoleKit").

## Configuration

The main configuration file is /etc/minirc.conf. Startup commands are put in /etc/minirc.local, Shutdown commands are put in /etc/minirc.local.shutdown. Minirc services are enabled by the DAEMONS and ENABLED lines in /etc/minirc.conf.

The local startup and shutdown files are just bash scripts.

To create the local startup and shutdown files you just run

```
touch /etc/minirc.local
touch /etc/minirc.local.shutdown
chmod +X /etc/minirc.local
chmod +X /etc/minirc.local.shutdown

```

The daemons enabled by default are syslog-ng, crond, dhcpcd, and sshd.

If the packages aren't installed then you will get a warning on bootup unless you disable them.

### Custom daemons

You specify custom daemons on the custom_start, custom_stop, and custom_poll functions in /etc/minirc.conf. You just follow the syntax that the other daemons are using. By default there are no custom daemons, these are the ones I put in.

```
custom_start () {
    case "$1" in
    NetworkManager)
        /usr/bin/NetworkManager ;;
    lightdm)
        sleep 1 ; /usr/bin/lightdm ;;
    *)
        default_start "$@";;  # keep the default as fall-back
    esac
}

custom_stop () {
    case "$1" in
    NetworkManager)
        killall NetworkManager;;
    lightdm)
        killall lightdm;;
    *)
        default_stop "$@";;  # keep the default as fall-back
    esac
}

custom_poll () {
    case "$1" in
    NetworkManager)
        pgrep NetworkManager > /dev/null;;
    lightdm)
        pgrep lightdm > /dev/null;;
    *)
        default_poll "$@";;  # keep the default as fall-back
    esac
}

```