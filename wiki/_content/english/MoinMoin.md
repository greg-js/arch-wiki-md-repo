"[MoinMoin](https://moinmo.in/) is an advanced, easy to use and extensible WikiEngine with a large community of users. Said in a few words, it is about collaboration on easily editable web pages." MoinMoin is written in [Python](/index.php/Python "Python") 2.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 uWSGI](#uWSGI)
        *   [2.1.1 nginx](#nginx)
        *   [2.1.2 Systemd unit file for MoinMoin with uWSGI](#Systemd_unit_file_for_MoinMoin_with_uWSGI)
*   [3 First steps](#First_steps)

## Installation

1.  Install [moinmoin](https://aur.archlinux.org/packages/moinmoin/).
2.  Make a new directory for MoinMoin under `/var/lib/moin/` for non static files.
3.  Copy the folders `/usr/share/moin/data/`, `/usr/share/moin/underlay/` and the configuration file `/usr/share/moin/config/wikiconfig.py` into `/var/lib/moin/`.
4.  Change the owner of `/var/lib/moin/` to the user under which your web server is running (in most cases "http").

You can also run MoinMoin directly from `/usr/share/moin/` if you're ok with non static files in `/usr/`.

## Configuration

### uWSGI

If using [uWSGI](/index.php/UWSGI "UWSGI"), copy the file `/usr/share/moin/server/moin.wsgi` to `/var/lib/moin`. In the file, replace the string `'/path/to/wikiconfigdir'` with `'/var/lib/moin'` and uncomment the line.

Install [uwsgi-plugin-python2](https://www.archlinux.org/packages/?name=uwsgi-plugin-python2) and create the file `/var/lib/moin/uwsgi.ini` with the following content.

```
[uwsgi]
socket = /run/uwsgi/moin.sock
chmod-socket = 660
plugin = python2

chdir = /var/lib/moin/
wsgi-file = /var/lib/moin/moin.wsgi

master
workers = 3
max-requests = 200
harakiri = 60
die-on-term

```

Start uWSGI with `uwsgi --ini /var/lib/moin/uwsgi.ini`. Make sure uWSGI has read and write rights for `/var/lib/moin/` and your web server has read and write rights for `/run/uwsgi/moin.sock`. If you're following this guide you should start uwsgi under the "http" user.

#### nginx

[nginx](/index.php/Nginx "Nginx") can be set adding the following server block to your `/etc/nginx/nginx.conf`:

```
server {
   listen       80;
   server_name  wiki.*your.domain*;

   location / {
      uwsgi_pass unix:/run/uwsgi/moin.sock;
      include /etc/nginx/uwsgi_params;
   }

   location ~ /moin_static[0-9]+/(.*) {
      alias /usr/lib/python2.7/site-packages/MoinMoin/web/static/htdocs/$1;
   }

   location /favicon.ico {
      alias /usr/lib/python2.7/site-packages/MoinMoin/web/static/htdocs/favicon.ico;
   }
}

```

#### Systemd unit file for MoinMoin with uWSGI

Create the [systemd unit](/index.php/Systemd#Using_units "Systemd") the following for easily starting/stopping the service:

 `/etc/systemd/system/moinmoin.service` 
```
[Unit]
Description=Start uwsgi for moinmoin wiki
After=network.target

[Service]
Type=simple
User=http
ExecStart=/usr/bin/uwsgi --ini /var/lib/moin/uwsgi.ini

[Install]
WantedBy=multi-user.target
```

## First steps

You should now be able to reach your wiki under wiki.your.domain. For further information on how to configure MoinMoin refer to the [MoinMoinWiki](http://moinmo.in/).