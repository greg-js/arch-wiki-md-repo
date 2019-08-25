[OpenVAS](http://www.openvas.org/) stands for Open Vulnerability Assessment System and is a network security scanner with associated tools like a graphical user front-end. The core component is a server with a set of network vulnerability tests (NVTs) to detect security problems in remote systems and applications.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pre-install](#Pre-install)
    *   [1.1 Redis](#Redis)
    *   [1.2 haveged](#haveged)
*   [2 Installation](#Installation)
*   [3 Initial setup](#Initial_setup)
*   [4 Getting started](#Getting_started)
*   [5 Systemd](#Systemd)
*   [6 Migration to new major versions](#Migration_to_new_major_versions)
*   [7 See also](#See_also)

## Pre-install

### Redis

Configure [redis](https://www.archlinux.org/packages/?name=redis) as prescribed by the [OpenVAS redis configuration](https://github.com/greenbone/openvas-scanner/blob/v5.0.9/doc/redis_config.txt). In summary, amend the following to your /etc/redis.conf

```
unixsocket /var/lib/redis/redis.sock
unixsocketperm 700
port 0
timeout 0
databases 128

```

**Note:** See the previous `OpenVAS redis configuration` document on how to calculate the `databases` number.

Additionally comment out the following (and similar) `save` lines if present to avoid a stuck connection of the `openvas-scanner` to `redis`:

```
save 900 1
save 300 10
save 60 10000

```

Create `/etc/openvas/openvassd.conf` and add the following:

```
kb_location = /var/lib/redis/redis.sock

```

Finally restart `redis`:

```
# systemctl restart redis

```

### haveged

If running OpenVAS in a virtual machine or any other system having a low entropy, you can optionally [install](/index.php/Install "Install") [haveged](https://www.archlinux.org/packages/?name=haveged) to gather more entropy. This is required for the key material used for the encrypted credentials saved within the `openvas-manager` database.

## Installation

[Install](/index.php/Install "Install") the [openvas](https://www.archlinux.org/packages/?name=openvas) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Alternatively install [greenbone-vulnerability-manager](https://www.archlinux.org/groups/x86_64/greenbone-vulnerability-manager/) which provides [openvas](https://www.archlinux.org/packages/?name=openvas), the Greenbone Vulnerability Manager ([gvmd](https://www.archlinux.org/packages/?name=gvmd)) and Greenbone Security Assistant (gsa) [greenbone-security-assistant](https://www.archlinux.org/packages/?name=greenbone-security-assistant)) OpenVAS web frontend.

## Initial setup

Create certificates for the server and clients, default values were used:

```
# openvas-manage-certs -a

```

Update the plugins and vulnerability data:

```
# greenbone-nvt-sync
# greenbone-scapdata-sync
# greenbone-certdata-sync

```

**Note:** If GSA complains that the scapdata database is missing, it may be necessary to use greenbone-scapdata-sync --refresh.

[Start](/index.php/Start "Start") the `openvas-scanner` service, then rebuild the database:

```
# openvasmd --rebuild --progress

```

Add an administrator user account, be sure to copy the password:

```
# openvasmd --create-user=admin --role=Admin

```

You can also change the password of the user later on

```
# openvasmd --user=admin --new-password=<password>

```

## Getting started

Start the `openvasmd` daemon

```
# openvasmd -p 9390 -a 127.0.0.1

```

Start the [Greenbone Security Assistant](http://www.greenbone.net/technology/openvas.html) WebUI (optional)

```
# gsad -f --listen=127.0.0.1 --mlisten=127.0.0.1 --mport=9390

```

Point your web browser to [http://127.0.0.1](http://127.0.0.1) and login with your admin crendentials

**Note:** By default, `gsad` will bind to port 80\. If you are already running a webserver, this will obviously cause problems. Pass the `--port` switch to `gsad` for an alternate port. Read the `gsad` man page for options like `--http-only`, `--no-redirect`, and more.

**Note:** The [Greenbone Security Assistant](http://www.greenbone.net/technology/openvas.html) WebUI requires the [texlive-most](https://www.archlinux.org/groups/x86_64/texlive-most/) package in order to provide PDF downloads of the reports.

## Systemd

Redhat based systemd units are in an AUR package named [openvas-systemd](https://aur.archlinux.org/packages/openvas-systemd/). The contain a few tweaks such as better TLS settings.

## Migration to new major versions

The database needs to be migrated when moving to a new major version:

```
# openvasmd --migrate --progress

```

## See also

*   [Wikipedia:OpenVAS](https://en.wikipedia.org/wiki/OpenVAS "wikipedia:OpenVAS")
*   [OpenVAS](http://www.openvas.org/) Official OpenVAS website.