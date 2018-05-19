[Firefox Sync](https://www.mozilla.org/en-US/firefox/features/sync/) is a protocol developed by Mozilla to synchronize a browser configuration and profile between different Firefox instances which could run on different platforms (e.g. mobile and desktop). In a default configuration, the user data is encrypted and stored on Mozilla servers.

This page details on how to setup an own Firefox Sync Server and how to configure the client software to use it.

## Contents

*   [1 Server setup](#Server_setup)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
        *   [1.2.1 Database](#Database)
    *   [1.3 Example nginx and uwsgi setup](#Example_nginx_and_uwsgi_setup)
*   [2 Client configuration](#Client_configuration)
*   [3 See also](#See_also)

## Server setup

### Installation

[mozilla-firefox-sync-server](https://aur.archlinux.org/packages/mozilla-firefox-sync-server/) is available in the [AUR](/index.php/AUR "AUR").

### Configuration

One file is available to configure a firefox sync server: `/etc/webapps/mozilla-firefox-sync-server/syncserver.ini`. Most options are explained clearly in the [official documentation](http://docs.services.mozilla.com/howtos/run-sync-1.5.html). You might want to change to variables, the accepted domain name (`public_url`) and the database backend (`sqluri`):

 `/etc/webapps/mozilla-firefox-sync-server/syncserver.ini` 
```
public_url = https://sync.example.com
sqluri = sqlite:////var/lib/mozilla-firefox-sync-server/syncserver.db

```

#### Database

Other databases can be used as backend for the firefox sync server such as [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") instead of [SQLite](/index.php/SQLite "SQLite"). In order to achieve this it's necesserary to add python packages via pip.

For MySQL `/usr/share/webapps/mozilla-firefox-sync-server/local/bin/pip install PyMySQL` For PostgreSQL `/usr/share/webapps/mozilla-firefox-sync-server/local/bin/pip install psycopg2` 

Then appropriate databases and users must be created in the database engine that will be used.

The syncserver.ini file should also be modified to reflect the change of database and it uses the SQLAlchemy syntax.

For MySQL `/etc/webapps/mozilla-firefox-sync-server/syncserver.ini` 
```
[syncserver]
sqluri = pymysql://username:password@db.example.com/sync

```
For PostgreSQL `/etc/webapps/mozilla-firefox-sync-server/syncserver.ini` 
```
[syncserver]
sqluri = postgresql://username:password@db.example.com/sync

```

### Example nginx and uwsgi setup

It is recommended to serve the firefox sync server with uwsgi in a production environement. In this case you have to install [uwsgi-plugin-python2](https://www.archlinux.org/packages/?name=uwsgi-plugin-python2). Create following uwsgi config file:

 `/etc/uwsgi/mozilla-firefox-sync-server.ini` 
```
[uwsgi]
socket = /run/uwsgi/%n.sock
uid = ffsync
gid = ffsync
chdir = /usr/share/webapps/mozilla-firefox-sync-server
master = true
plugins = python2
file = syncserver.wsgi

```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `uwsgi@mozilla\\x2dfirefox\\x2dsync\\x2dserver` service.

An example [Nginx](/index.php/Nginx "Nginx") configuration looks something like this:

 `/etc/nginx/sites-enabled/sync.example.com` 
```
server {
  server_name sync.example.com;
  access_log /var/log/nginx/sync.example.com.access.log;
  error_log /var/log/nginx/sync.example.com.error.log info;
  server_tokens off;

  client_max_body_size 15M;

  location / {
    include uwsgi_params;
    uwsgi_pass unix:/run/uwsgi/mozilla-firefox-sync-server.sock;
  }
}

```

## Client configuration

**Note:** Since version 1.5 of the protocol, a [Firefox Account](https://www.mozilla.org/en-US/firefox/accounts/) is required in order to use the synchronization service.

To configure desktop Firefox to talk to your new Sync server, go to `about:config`, search for `identity.sync.tokenserver.uri` and change its value to the URL of your server with a path of `token/1.0/sync/1.5`:

 `identity.sync.tokenserver.uri: http://example.com/ffsync/token/1.0/sync/1.5` 
**Tip:** Enter `about:sync-log` in the Firefox URL bar to get a list of logs related to Firefox Sync.

## See also

*   [Official Mozilla Firefox Sync Server Howto](http://docs.services.mozilla.com/howtos/run-sync.html)
*   [Howto with Apache support by Eric Hameleers](http://alien.slackbook.org/blog/setting-up-your-own-mozilla-sync-server/)
*   [Howto with nginx and systemd support by Timothée Ravier](https://tim.siosm.fr/blog/2012/12/11/firefox-sync-nginx-systemd/)
*   [Howto with nginx support](http://amnesiak.org/blog/mozilla-sync-server-with-nginx.html)
*   [Howto using MySQL](http://terminal28.com/how-to-install-and-configure-own-firefox-sync-server-weave-debian/)
*   [OwnCloud](/index.php/OwnCloud "OwnCloud") has mozilla sync server application