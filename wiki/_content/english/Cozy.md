Related articles

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")

[Cozy](https://cozy.io) is a personal cloud platform free, and self-hostable, written in [Node.js](/index.php/Node.js "Node.js") (the future version, v3, will be written in [Go](/index.php/Go "Go") instead).

The platform aims at simplifying the use of a personal cloud and at allowing the users to take back ownership of their privacy. Its base applications' features include hosting, sharing and synchronising files, pictures, contacts and calendars, along with an email client.

Third-party apps are available through a marketplace and can be used to extend Cozy's default features, with task management, blog hosting, bank account overview, etc.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Pre-configuration](#Pre-configuration)
    *   [1.2 Configuring CouchDB](#Configuring_CouchDB)
    *   [1.3 Starting the controller](#Starting_the_controller)
    *   [1.4 Installing the Cozy stack](#Installing_the_Cozy_stack)
    *   [1.5 Configuring](#Configuring)
        *   [1.5.1 Configuring the domain](#Configuring_the_domain)
        *   [1.5.2 Configuring the background](#Configuring_the_background)
*   [2 Reverse proxying](#Reverse_proxying)
    *   [2.1 Apache](#Apache)
    *   [2.2 nginx](#nginx)
    *   [2.3 Caddy](#Caddy)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Upgrading to CouchDB 2.x from an existing install](#Upgrading_to_CouchDB_2.x_from_an_existing_install)

## Installation

Just install the [cozy](https://aur.archlinux.org/packages/cozy/) package. It provides the core (cozy-controller and cozy-monitor) plus related configuration files, as well as the required dependencies.

**Note:** This will install Node.js version 4.x provided by [nodejs-lts-argon](https://www.archlinux.org/packages/?name=nodejs-lts-argon). While Cozy **may** totally work with newer versions (e.g. 6.x, 8.x), they are not officially supported, as Cozy officially supports only Node.js v4.x. If you still want to use the Node.js version currently in Archlinux's official repository, you will need to change the dependency in the PKGBUILD.

### Pre-configuration

You will need to add two users accounts manually:

```
# useradd -MU cozy-data-system
# useradd -MU cozy-home

```

### Configuring CouchDB

We will now configure the database. Cozy stores almost everything in a [CouchDB](/index.php/CouchDB "CouchDB") database, and needs a CouchDB administrator to manage this database. This administrator's credentials must be placed in `/etc/cozy/couchdb.login` so Cozy can use them.

To create an administrator, first generate the credentials (with [pwgen](https://www.archlinux.org/packages/?name=pwgen) for example), store them, and send them to CouchDB. Do not forget to give the appropriate rights to the file.

**Note:** The following curl commands will setup CouchDB 2.0 in “single node” mode. If you don’t use CouchDB for anything else, this is likely what you want.

```
# pwgen -1 > /etc/cozy/couchdb.login
# pwgen -1 >> /etc/cozy/couchdb.login
# chown cozy-data-system /etc/cozy/couchdb.login
# chmod 640 /etc/cozy/couchdb.login
# curl -X PUT 127.0.0.1:5984/_node/couchdb@localhost/_config/admins/$(head -n1 /etc/cozy/couchdb.login) -d "\"$(tail -n1 /etc/cozy/couchdb.login)\""
# curl -X PUT $(head -n1 /etc/cozy/couchdb.login):$(tail -n1 /etc/cozy/couchdb.login)@127.0.0.1:5984/_users
# curl -X PUT $(head -n1 /etc/cozy/couchdb.login):$(tail -n1 /etc/cozy/couchdb.login)@127.0.0.1:5984/_replicator
# curl -X PUT $(head -n1 /etc/cozy/couchdb.login):$(tail -n1 /etc/cozy/couchdb.login)@127.0.0.1:5984/_global_changes

```

**Note:** You should also take a look at [CouchDB#Single node setup & Security](/index.php/CouchDB#Single_node_setup_.26_Security "CouchDB").

### Starting the controller

Cozy needs its controller (cozy-controller) up and running in order to work. As it is supposed to run as a background task, it is better to run it in systemd. The service file is provided by the package, and has couchdb in its dependencies so that starting/enabling cozy-controller.service is enough.

### Installing the Cozy stack

You can now use cozy-monitor to install and start each component of Cozy's base stack:

```
# cozy-monitor install-cozy-stack

```

### Configuring

Cozy will now need some basic configuration, in order to know the homepage's background and on which domain it will be accessed by the user.

#### Configuring the domain

```
# coffee /var/lib/cozy/apps/home/commands.coffee setdomain <your domain>

```

**Note:** Because of the way it works, it is recommended to use a whole domain (or sub-domain) for Cozy, such as `cozy.example.tld`.

#### Configuring the background

```
# curl -X POST [http://localhost:9103/api/instance](http://localhost:9103/api/instance) -H "Content-Type: application/json" -d '{"background":"background-07"}'

```

**Note:** This setting can be changed at any time in the "Settings" page in the Cozy instance.

## Reverse proxying

As a security measure, Cozy needs to be served over HTTPS, which means it needs a reverse proxy in front of it. This can managed by either a proxying software like [HAproxy](/index.php/HAproxy "HAproxy") or a webserver such as [Apache](/index.php/Apache "Apache"), [nginx](/index.php/Nginx "Nginx") or [Caddy](https://caddyserver.com/).

You will also need SSL certificates, either self-signed or provided by a trusted authority.

Below are example configuration files for some common web servers.

### Apache

 `**/etc/httpd/conf/extra/cozy.conf**` 
```
<IfModule mod_ssl.c>
 <VirtualHost *:443>
        ServerName      cozy.example.tld
        ServerAdmin     admin@server

        SSLEngine               On
        SSLCertificateFile      /etc/cozy/server.crt
        SSLCertificateKeyFile   /etc/cozy/server.key

        RewriteEngine           On
        RewriteCond             %{REQUEST_URI} ^/.*socket\.io [NC]
        RewriteCond             %{THE_REQUEST} websocket [NC]
        RewriteRule             /(.*)           ws://127.0.0.1:9104/$1 [P,L]

        ProxyPass               / [http://127.0.0.1:9104/](http://127.0.0.1:9104/) retry=0 Keepalive=On timeout=1600
        ProxyPassReverse        / [http://127.0.0.1:9104/](http://127.0.0.1:9104/)
        setenv proxy-initial-not-pooled 1

        CustomLog               /var/log/apache2/cozy-access.log "%t %h %{SSL_PROTOCOL}x %{SSL_CIPHER}x \"%r\" %b"
        ErrorLog                /var/log/apache2/cozy-error.log

 </VirtualHost>

 <VirtualHost *:80>
        ServerName      cozy.example.tld
        ServerAdmin     admin@server

	Redirect permanent / [https://cozy.example.tld/](https://cozy.example.tld/)

 </VirtualHost>
</IfModule>
```

### nginx

 `**/etc/nginx/cozy.conf**` 
```
server {
    listen 443;

    server_name cozy.example.tld;

    ssl_certificate /etc/cozy/server.crt;
    ssl_certificate_key /etc/cozy/server.key;
    ssl_dhparam /etc/cozy/dh.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    ssl_prefer_server_ciphers on;
    ssl on;

    gzip_vary on;
    client_max_body_size 1024M;

    add_header Strict-Transport-Security max-age=2678400;

    location / {
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_redirect http:// https://;
        proxy_pass [http://127.0.0.1:9104](http://127.0.0.1:9104);
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    access_log /var/log/nginx/cozy.log;
}

# Always redirect http:// to https://
server {
    listen 80;
    server_name cozy.example.tld;

    return 301 [https://$host$request_uri](https://$host$request_uri);
}
```

**Note:** Do not forget to include `/etc/nginx/cozy.conf` in `/etc/nginx/nginx.conf`!

### Caddy

 `**/etc/caddy/Caddyfile**` 
```
cozy.example.tld {
    tls admin@server
    proxy / 127.0.0.1:9104 {
        transparent
        websocket
    }
}
```

## Troubleshooting

### Upgrading to CouchDB 2.x from an existing install

If you are updating CouchDB from version 1.x to version 2.x, Cozy may not be able to run because of CouchDB's sharding (which is not supported by Cozy yet). This updates changes the default database directory, making Cozy's database not found by CouchDB. Here is the path to follow to make Cozy work again.

*   Stop the `couchdb` service. Backup `/var/lib/couchdb/cozy.couch` somewhere else and remove everything under `/var/lib/couchdb` (don’t do this if you happen to use couchdb for anything else than Cozy! In that case, you probably need to check carefully what’s in there, and find the appropriate migration process for every database).

*   Edit `/etc/couchdb/local.ini` and add the following:

 `**/etc/couchdb/local.ini**` 
```
[cluster]
q=1
n=1
```

*   Start the `couchdb` service. At this point, you should have files under `/var/lib/couchdb` again, and especially `/var/lib/couchdb/shards/00000000-ffffffff/cozy.<unix time of creation>.couch`.

*   Stop the `couchdb` service again, copy (don’t move, rather be safe) your backuped `cozy.couch` to `/var/lib/couchdb/shards/00000000-ffffffff/cozy.<unix time of creation>.couch`.

*   Start the `couchdb` service. Now, everything should be working.