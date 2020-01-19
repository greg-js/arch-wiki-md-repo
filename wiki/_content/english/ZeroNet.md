[ZeroNet](https://zeronet.io/) gives access to "open, free and uncensorable websites, using Bitcoin cryptography and the BitTorrent network".

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

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

By default, ZeroNet uses clearnet and Tor if available. To enable Tor support you first need to install [Tor](/index.php/Tor "Tor"). Then, give ZeroNet access to control Tor using the following instructions.

```
# usermod -a -G tor zeronet

```

[Append](/index.php/Append "Append") or edit the following options in `/etc/tor/torrc`:

```
ControlPort 9051
DataDirectoryGroupReadable 1
CacheDirectoryGroupReadable 1
CookieAuthentication 1
CookieAuthFileGroupReadable 1
CookieAuthFile /var/lib/tor/control_auth_cookie

```

You may also want to [start/enable](/index.php/Start/enable "Start/enable") `tor.service`.

Eventually check Tor file permissions

```
stat -c%a /var/lib/tor

```

should print `750`. if not, run `sudo chmod 0750 /var/lib/tor`

To force all ZeroNet connections through Tor,
append to your `/etc/zeronet.conf` file

```
tor = always

```

## Creating ZeroNet sites

All operations, including editing ZeroNet site files, should be done as user `zeronet`. Use `--config_file` to specify the configuration file. `/etc/zeronet.conf` use `/var/lib/zeronet` as data directory by default. For example:

```
$ sudo -u zeronet python2 zeronet.py --config_file /etc/zeronet.conf

```

Or

```
$ sudo su - zeronet
$ cd /opt/zeronet
$ python2 zeronet.py --config_file /etc/zeronet.conf

```

All sites you create will have their initial data folder setup in /var/lib/zeronet/[address]. For more information on how to create a Zite, please follow the guidelines on the [Zeronet FAQ](http://zeronet.readthedocs.io/en/latest/using_zeronet/create_new_site/).

## See also

*   [Official ZeroNet website](https://zeronet.io/)
*   [ZeroNet - Read the Docs](https://zeronet.readthedocs.io/en/latest/)