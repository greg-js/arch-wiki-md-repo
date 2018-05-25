[OpenVAS](http://www.openvas.org/) stands for Open Vulnerability Assessment System and is a network security scanner with associated tools like a graphical user front-end. The core component is a server with a set of network vulnerability tests (NVTs) to detect security problems in remote systems and applications.

## Contents

*   [1 Installation](#Installation)
*   [2 Initial setup](#Initial_setup)
*   [3 Post-install](#Post-install)
*   [4 Getting started](#Getting_started)
*   [5 Systemd](#Systemd)
*   [6 Migration to new major versions](#Migration_to_new_major_versions)
*   [7 See also](#See_also)

## Installation

Install the [openvas](https://www.archlinux.org/groups/x86_64/openvas/) package group from the [official repositories](/index.php/Official_repositories "Official repositories"). This group provides the [openvas-cli](https://www.archlinux.org/packages/?name=openvas-cli) command-line `omp` interface and [greenbone-security-assistant](https://www.archlinux.org/packages/?name=greenbone-security-assistant) web interface via the `gsad` daemon along with other OpenVAS dependencies.

## Initial setup

Create certificates for the server+client, default values were used

```
# openvas-manage-certs -a

```

Update the plugins and vulnerability data:

```
# greenbone-nvt-sync
# greenbone-scapdata-sync
# greenbone-certdata-sync

```

*Note*: If GSA complains that the scapdata database is missing, it may be necessary to use greenbone-scapdata-sync --refresh

Start the scanner service:

```
# systemctl start openvas-scanner

```

Rebuild the database:

```
# openvasmd --rebuild --progress

```

Add an administrator user account, be sure to copy the password:

```
# openvasmd --create-user=admin --role=Admin

```

## Post-install

Configure [redis](https://www.archlinux.org/packages/?name=redis) as prescribed by the [OpenVAS redis configuration](https://svn.wald.intevation.org/svn/openvas/tags/openvas-scanner-release-5.0.3/doc/redis_config.txt). In summary, amend the following to your /etc/redis.conf

```
unixsocket /var/lib/redis/redis.sock
unixsocketperm 700
port 0
timeout 0

```

Create and add the following to /etc/openvas/openvassd.conf

```
kb_location = /var/lib/redis/redis.sock

```

Finally restart `redis`

```
# systemctl restart redis

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