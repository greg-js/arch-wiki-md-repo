# Mozilla Firefox Sync Server

From [Wikipedia](https://en.wikipedia.org/wiki/Firefox_Sync "wikipedia:Firefox Sync"):

	_Firefox Sync, originally branded Mozilla Weave, is a browser synchronization feature that allows users to partially synchronize bookmarks, browsing history, preferences, passwords, filled forms, add-ons and the last 25 opened tabs across multiple computers._

	_It keeps user data on Mozilla servers, but the data is encrypted in such a way that no third party, not even Mozilla, can access user information. It is also possible for the user to host their own Firefox Sync servers, or indeed, for any entity to do so._

This page details how you should proceed to host your own (Mozilla) Firefox Sync Server (shortened to FFSync), version 1.1 or version 1.5, and how to host your own Firefox Account server.

**Note:** The 1.1 version of the Mozilla Firefox Sync Server has been deprecated in Firefox 29 and support has been removed from version 32\. Version 1.5 of the Mozilla Firefox Sync Server is available for Firefox 29+. However, this now requires users create a Firefox Account. See the following links for details:

*   [https://wiki.mozilla.org/Identity/Firefox_Accounts](https://wiki.mozilla.org/Identity/Firefox_Accounts)
*   [https://blog.mozilla.org/blog/2014/02/07/introducing-mozilla-firefox-accounts/](https://blog.mozilla.org/blog/2014/02/07/introducing-mozilla-firefox-accounts/)
*   [https://blog.mozilla.org/services/2014/02/07/a-better-firefox-sync/](https://blog.mozilla.org/services/2014/02/07/a-better-firefox-sync/)
*   [https://blog.mozilla.org/futurereleases/2014/02/07/test-the-new-firefox-sync-and-customize-the-new-ui-in-firefox-aurora/](https://blog.mozilla.org/futurereleases/2014/02/07/test-the-new-firefox-sync-and-customize-the-new-ui-in-firefox-aurora/)

**Note:** The 1.1 and 1.5 versions are currently conflicting for simplicity but one could have the two versions alongside on the same server with some changes. The databases should probably not be shared between different versions however.

**Tip:** Enter `about:sync-log` in the Firefox URL bar to get a list of logs related to Firefox Sync.

## Contents

*   [1 Version 1.5](#Version_1.5)
    *   [1.1 Installation](#Installation)
    *   [1.2 Server configuration](#Server_configuration)
    *   [1.3 Running behind nginx](#Running_behind_nginx)
    *   [1.4 Client configuration](#Client_configuration)
    *   [1.5 Firefox Account Server](#Firefox_Account_Server)
*   [2 Version 1.1](#Version_1.1)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Server configuration](#Server_configuration_2)
        *   [2.2.1 Basic configuration](#Basic_configuration)
        *   [2.2.2 Disable debug mode](#Disable_debug_mode)
        *   [2.2.3 Set email](#Set_email)
        *   [2.2.4 Storage backend](#Storage_backend)
        *   [2.2.5 Disk quota](#Disk_quota)
        *   [2.2.6 Running behind a Web Server](#Running_behind_a_Web_Server)
            *   [2.2.6.1 Apache combined with mod_wsgi](#Apache_combined_with_mod_wsgi)
            *   [2.2.6.2 nginx with Gunicorn](#nginx_with_Gunicorn)
        *   [2.2.7 Not recommended setup with default web server](#Not_recommended_setup_with_default_web_server)
    *   [2.3 Client configuration](#Client_configuration_2)
*   [3 See also](#See_also)

## Version 1.5

This is for Firefox version 29 and onward.

**Warning:** I could not get the 1.5 version to work when running behind nginx with HTTPS. I'm affected by the bug described in [https://mail.mozilla.org/pipermail/sync-dev/2014-August/000955.html](https://mail.mozilla.org/pipermail/sync-dev/2014-August/000955.html) and I do not understand how the problem got resolved. It works for me with plain HTTP connexions though. [Siosm](/index.php/User:Siosm "User:Siosm") ([talk](/index.php?title=User_talk:Siosm&action=edit&redlink=1 "User talk:Siosm (page does not exist)")) 09:32, 12 September 2014 (UTC)

### Installation

[mozilla-firefox-sync-server-git](https://aur.archlinux.org/packages/mozilla-firefox-sync-server-git/) is available in the [AUR](/index.php/AUR "AUR").

The setup creates an isolated Python environment in which all necessary dependencies are downloaded and installed. Afterwards, running the server only relies on the isolated Python environment, independently of the system-wide Python.

### Server configuration

One file is available to configure a FFsync server: `/opt/mozilla-firefox-sync-server/syncserver.ini`. Most options are explained clearly in the [official documentation](http://docs.services.mozilla.com/howtos/run-sync-1.5.html). Here is a full example with comments:

```
# Use a Unix socket and the Gunicorn server
[server:main]
use = egg:gunicorn#main
bind = unix:/run/ffsync/syncserver.sock
workers = 2
timeout = 60
syslog = true
syslog_prefix = ffsync
syslog_facility = daemon

[app:main]
use = egg:syncserver

[syncserver]
# This must be edited to point to the public URL of your server,
# i.e. the URL as seen by Firefox.
public_url = http://example.com/ffsync/

# This defines the database in which to store all server data.
sqluri = sqlite:////var/lib/ffsync/sync_storage.db

# This is a secret key used for signing authentication tokens.
# It should be long and randomly-generated.
# The following command will give a suitable value on *nix systems:
#
#    head -c 20 /dev/urandom
```

### Running behind nginx

A sample from the nginx config:

```
# Firefox sync config
        location /ffsync/ {
            rewrite  ^/ffsync(.+)$ $1 break;
            proxy_pass http://unix:/run/ffsync/syncserver.sock;
            proxy_set_header Host $http_host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header X-Forwarded-Proto $scheme;
            proxy_redirect off;
            proxy_read_timeout 120;
            proxy_connect_timeout 10;
            gzip        off;
        }
```

### Client configuration

To configure desktop Firefox to talk to your new Sync server, go to `about:config`, search for `services.sync.tokenServerURI` and change its value to the URL of your server with a path of `token/1.0/sync/1.5`:

 `services.sync.tokenServerURI: http://example.com/ffsync/token/1.0/sync/1.5` 

### Firefox Account Server

Until this section is completed, you will have to use the official Firefox Accounts service provided by Mozilla. You can try running your own by following the instructions from the [official documentation](http://docs.services.mozilla.com/howtos/run-fxa.html).

## Version 1.1

This is for Firefox version up to but not including version 32.

### Installation

[mozilla-firefox-sync-server-hg](https://aur.archlinux.org/packages/mozilla-firefox-sync-server-hg/) is available in the [AUR](/index.php/AUR "AUR").

The setup creates an isolated Python environment in which all necessary dependencies are downloaded and installed. Afterwards, running the server only relies on the isolated Python environment, independently of the system-wide Python.

### Server configuration

Two files are used to configure a FFsync server: `/opt/mozilla-firefox-sync-server/development.ini` and `/opt/mozilla-firefox-sync-server/etc/sync.conf`.

#### Basic configuration

The fallback node URL must reflect the server's visible URL (here `https://example.com/ffsync/`). In `/opt/mozilla-firefox-sync-server/etc/sync.conf`, change:

```
[nodes]
fallback_node = http://localhost:5000/
```

to:

```
[nodes]
fallback_node = https://example.com/ffsync/
```

#### Disable debug mode

In `/opt/mozilla-firefox-sync-server/development.ini`, set:

```
[DEFAULT]
debug = False
```

#### Set email

In `/opt/mozilla-firefox-sync-server/etc/sync.conf`, set:

```
[smtp]
sender = ffsync@example.com
```

#### Storage backend

The default storage backend is sqlite which should be fine if you do not have a lot of users. To split the various databases into several files, edit the `sqluri` fields in `/opt/mozilla-firefox-sync-server/etc/sync.conf`.

The [Official FFsync server Howto](http://docs.services.mozilla.com/howtos/run-sync.html) details setup with MySQL or LDAP as a backend.

#### Disk quota

The default disk quota is quite restrictive and will quickly be filled if a lot of bookmarks are stored. Bump the disk quota from 5 to 25 MB in `/opt/mozilla-firefox-sync-server/etc/sync.conf`:

```
[storage]
...
quota_size = 25600
...
```

#### Running behind a Web Server

The default configuration runs a built-in server which should not be used in production.

##### Apache combined with mod_wsgi

See the [Official FFsync server Howto](http://docs.services.mozilla.com/howtos/run-sync.html).

##### nginx with Gunicorn

The [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") available in the [AUR](/index.php/AUR "AUR") installs the Gunicorn server, in the python `virtualenv`, by default. Enable it by changing the following lines in `/opt/mozilla-firefox-sync-server/development.ini`:

```
[server:main]
use = egg:gunicorn#main
host = unix:/run/ffsync/syncserver.sock
use_threadpool = True
threadpool_workers = 60
```

Create the `/etc/tmpfiles.d/ffsync.conf` file to create the `/run/ffsync/` folder at boot:

 `D /run/ffsync 0750 ffsync http` 

Create this folder now by running:

 `# systemd-tmpfiles --create ffsync.conf` 

Enable and start the Gunicorn serveur using the systemd service unit provided in [mozilla-firefox-sync-server-hg](https://aur.archlinux.org/packages/mozilla-firefox-sync-server-hg/):

```
# systemctl enable ffsync
# systemctl start ffsync
```

Use this config extract to configure nginx:

```
# Firefox sync config
location /ffsync/ {
    rewrite  ^/ffsync(.+)$ $1 break;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $http_host;
    proxy_redirect off;
    proxy_pass http://unix:/run/ffsync/syncserver.sock;
}
```

#### Not recommended setup with default web server

(Outdated) systemd service unit:

 `/etc/systemd/system/ffsync.service` 

```
[Unit]
Description=Mozilla Firefox Syn Server
After=network.target

[Service]
Type=simple
User=ffsync
Group=ffsync
WorkingDirectory=/opt/mozilla-firefox-sync-server
ExecStart=/opt/mozilla-firefox-sync-server/bin/python2 /opt/mozilla-firefox-sync-server/bin/paster serve /opt/mozilla-firefox-sync-server/development.ini
StandardOutput=/var/log/ffsync/sync-messages.log

[Install]
WantedBy=multi-user.target
Alias=ffsync.service

```

### Client configuration

Use the Sync Configuration Wizard in Firefox' Settings to create a new account on the server. Do not forget to choose "Custom server..." in the list, and input the server address: `https://example.com/ffsync/`

The "Advanced Settings" button allows fine tuning of the synchronized elements list, and the definition of the client hostname.

## See also

*   [Official Mozilla Firefox Sync Server Howto](http://docs.services.mozilla.com/howtos/run-sync.html)
*   [Howto with Apache support by Eric Hameleers](http://alien.slackbook.org/blog/setting-up-your-own-mozilla-sync-server/)
*   [Howto with nginx and systemd support by Timothée Ravier](https://tim.siosm.fr/blog/2012/12/11/firefox-sync-nginx-systemd/)
*   [Howto with nginx support](http://amnesiak.org/blog/mozilla-sync-server-with-nginx.html)
*   [Howto using MySQL](http://terminal28.com/how-to-install-and-configure-own-firefox-sync-server-weave-debian/)
*   [OwnCloud](/index.php/OwnCloud "OwnCloud") has mozilla sync server application

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mozilla_Firefox_Sync_Server&oldid=388043](https://wiki.archlinux.org/index.php?title=Mozilla_Firefox_Sync_Server&oldid=388043)"