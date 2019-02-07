Related articles

*   [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs")

[Cozy](https://cozy.io) is a personal cloud platform free, and self-hostable, written in [Go](/index.php/Go "Go") (the former version, v2, was written in [Node.js](/index.php/Node.js "Node.js") instead).

The platform aims at simplifying the use of a personal cloud and at allowing the users to take back ownership of their privacy. Its base applications’ features include hosting, sharing and synchronising files & pictures and collecting your data from several providers. Some other apps are on the roadmap, like a contacts manager and a calendar.

Third-party apps will also be available through a marketplace soon.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Configuring CouchDB](#Configuring_CouchDB)
    *   [2.2 Configuring Cozy admin password](#Configuring_Cozy_admin_password)
    *   [2.3 Starting the stack](#Starting_the_stack)
*   [3 Creating an instance](#Creating_an_instance)
    *   [3.1 Reverse proxying](#Reverse_proxying)
        *   [3.1.1 nginx](#nginx)

## Installation

[Install](/index.php/Install "Install") the [cozy-stack](https://www.archlinux.org/packages/?name=cozy-stack) package. It provides the core plus related configuration files, as well as the minimum required dependencies.

You might also want to install [nsjail](https://www.archlinux.org/packages/?name=nsjail) to run Konnectors in isolated environments, as well as an SMTP server to let Cozy send emails to your users.

## Configuration

Almost everything happens in `/etc/cozy/cozy.yml`. Some defaults are already set, while some placeholders will be replaced during configuration. You can also find an example file at `/usr/share/cozy/cozy.example.yaml`.

### Configuring CouchDB

Cozy stores everything (but actual files) in a [CouchDB](/index.php/CouchDB "CouchDB") database, and needs a CouchDB administrator to manage this database. This administrator’s credentials must be specified as part of the `couchdb url` setting in `/etc/cozy/cozy.yml` so that Cozy can use them. The following supposes you have a running [CouchDB](/index.php/CouchDB "CouchDB") instance, if not you can follow the corresponding wiki page to setup one as single node.

You can generate the credentials with [pwgen](https://www.archlinux.org/packages/?name=pwgen) for example. Once you have them (`couch_user` and `couch_password`), edit your configuration as follow:

 `/etc/cozy/cozy.yaml` 
```
couchdb:
  url: http://<couch_user>:<couch_password>@localhost:5984/
```

And register them to CouchDB (replace `<couchdb_admin>` and `<couchdb_password>` with your CouchDB admin credentials):

```
$ curl -X PUT http://<couchdb_admin>:<couchdb_password>@127.0.0.1:5984/_node/couchdb@localhost/_config/admins/<couch_user> -d "\"<couch_password>\""

```

### Configuring Cozy admin password

Cozy itself requires an admin password for all operations at the stack level. Create it like this:

```
# cozy-stack config passwd /etc/cozy/cozy-admin-passphrase

```

You will be prompted to enter a passphrase. Then fix the ownership:

```
# chown cozy:cozy /etc/cozy/cozy-admin-passphrase

```

### Starting the stack

At this point, you should [Start/Enable](/index.php/Systemd#Using_units "Systemd") the `cozy-stack.service` daemon.

You can check everything is right by running:

```
$ curl [http://localhost:8080/version](http://localhost:8080/version)

```

## Creating an instance

To add an instance (you will be prompted for your Cozy admin password, you might also pass it using COZY_ADMIN_PASSWORD env var):

```
$ cozy-stack instances add <instance>.example.tld --apps home,settings,store

```

This will output you a registration token. You can also specify an email using `--email <address>` at which the registration token will be sent.

You will then need to visit `https://<instance>.example.tld/?registerToken=<token>`, which requires you to have setup a reverse proxy (see below).

### Reverse proxying

As a security measure, Cozy needs to be served over HTTPS, which means it needs a reverse proxy in front of it. This can managed by either a proxying software like [HAproxy](/index.php/HAproxy "HAproxy") or a webserver such as [Apache](/index.php/Apache "Apache"), [nginx](/index.php/Nginx "Nginx") or [Caddy](https://caddyserver.com/).

Cozy needs a full domain name for the instance (something like `<instance>.example.tld`) and use one domain name per application, in the form of `<app>.<instance>.example.tld`.

Thus, you have to setup your domain zone with something like this:

```
   <instance> 1h IN A x.x.x.x
   *.<instance> 1h IN CNAME <instance>

```

You will also need SSL certificates, either a wildcard one covering `*.<instance>.example.tld` and `<instance>.example.tld` or a certificate for `<instance>.example.tld` with apps domains added as SAN. Currently, the list of apps is: onboarding,settings,drive,photos,collect. But this will grow over time, so you will have to expand your certificate regularly. Thus, getting a wildcard one is advised.

Below is an example configuration file for nginx.

#### nginx

 `**/etc/nginx/sites-available/<instance>.conf**` 
```
# Always redirect http:// to https://
server {
    listen 80;
    server_name .<instance>.example.tld <instance>.example.tld;

    return 301 [https://$host$request_uri](https://$host$request_uri);
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name .<instance>.example.tld <instance>.example.tld; 

    ssl_certificate /etc/cozy/<instance>.crt;
    ssl_certificate_key /etc/cozy/<instance>.key;

    client_max_body_size 1g;

    location / {
        proxy_pass [http://127.0.0.1:8080](http://127.0.0.1:8080);
        proxy_http_version 1.1;
        proxy_redirect http:// https://;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection $connection_upgrade;
    }

    access_log /var/log/nginx/<instance>.log;
    error_log /var/log/nginx/<instance>.error.log;
}
```

**Note:** Do not forget to symlink `/etc/nginx/sites-available/<instance>.conf` in `/etc/nginx/sites-enabled`!