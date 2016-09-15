OpenVAS stands for Open Vulnerability Assessment System and is a network security scanner with associated tools like a graphical user front-end. The core component is a server with a set of network vulnerability tests (NVTs) to detect security problems in remote systems and applications.

## Contents

*   [1 Installation](#Installation)
*   [2 Initial setup](#Initial_setup)
*   [3 Post-Install](#Post-Install)
*   [4 Getting Started](#Getting_Started)
*   [5 Systemd](#Systemd)
*   [6 Migration to new major versions](#Migration_to_new_major_versions)
*   [7 See Also](#See_Also)

## Installation

Install the [openvas](https://www.archlinux.org/groups/x86_64/openvas/) package group from the [official repositories](/index.php/Official_repositories "Official repositories"). This group provides the [openvas-cli](https://www.archlinux.org/packages/?name=openvas-cli) command-line `omp` interface and [greenbone-security-assistant](https://www.archlinux.org/packages/?name=greenbone-security-assistant) web interface via the `gsad` daemon along with other OpenVAS dependencies.

## Initial setup

Create a certificate for the server, choosing the default values if desired:

```
# openvas-mkcert

```

Create a client certificate:

```
# openvas-mkcert-client -n -i

```

Update the plugins and vulnerability data:

```
# openvas-nvt-sync
# openvas-scapdata-sync
# openvas-certdata-sync

```

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

## Post-Install

Configure [redis](https://www.archlinux.org/packages/?name=redis) as prescribed by the [OpenVAS redis configuration](https://svn.wald.intevation.org/svn/openvas/tags/openvas-scanner-release-5.0.3/doc/redis_config.txt). In summary, amend the following to your /etc/redis.conf

```
unixsocket /var/lib/redis/redis.sock
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

## Getting Started

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

## Systemd

Redhat based systemd units are in an AUR package named [openvas-systemd](https://aur.archlinux.org/packages/openvas-systemd/). The contain a few tweaks such as better TLS settings.

## Migration to new major versions

The database needs to be migrated when moving to a new major version:

```
# openvasmd --migrate --progress

```

## See Also

*   [OpenVAS](http://www.openvas.org/) Official OpenVAS website.