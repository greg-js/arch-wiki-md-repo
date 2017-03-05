From [ZeroNet](https://zeronet.io/) gives access to "open, free and uncensorable websites, using Bitcoin cryptography and BitTorrent network".

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Starting](#Starting)
    *   [2.2 Tor](#Tor)
*   [3 Creating ZeroNet sites](#Creating_ZeroNet_sites)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [zeronet](https://aur.archlinux.org/packages/zeronet/) package.

The latest development version is also available in the [zeronet-git](https://aur.archlinux.org/packages/zeronet-git/) package

## Configuration

### Starting

To start ZeroNet [start/enable](/index.php/Start/enable "Start/enable") `zeronet.service`.

### Tor

By default, ZeroNet uses clearnet and Tor if available. To enable Tor support you first neet to install [Tor](/index.php/Tor "Tor") via [tor](https://www.archlinux.org/packages/?name=tor). Then, give ZeroNet access to control Tor using the following instructions.

```
# usermod -a -G tor zeronet
# mkdir -m 750 /var/lib/tor-auth
# chown tor:tor /var/lib/tor-auth

```

[Append](/index.php/Append "Append") the following lines to `/etc/tor/torrc`:

```
CookieAuthentication 1
CookieAuthFileGroupReadable 1
CookieAuthFile /var/lib/tor-auth/control_auth_cookie

```

## Creating ZeroNet sites

All operations, including editing ZeroNet site files, should be done as user `zeronet` and configuration must be passed for data directory to be selected to `/var/lib/zeronet`. For example:

```
$ sudo -u zeronet python2 zeronet.py --config_file /etc/zeronet.conf

```

Or

```
$ sudo su - zeronet
$ cd /opt/zeronet
$ python2 zeronet.py --config_file /etc/zeronet.conf

```

All zites you create will have their initial data folder setup in /var/lib/zeronet/[address]. For more information on how to create a Zite, please follow the guidelines on the [Zeronet FAQ](http://zeronet.readthedocs.io/en/latest/using_zeronet/create_new_site/).

## See also

*   [Official ZeroNet website](https://zeronet.io/)
*   [ZeroNet - Read the Docs](https://zeronet.readthedocs.io/en/latest/)