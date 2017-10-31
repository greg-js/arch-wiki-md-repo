[Onlyoffice Documentserver](https://www.onlyoffice.com/) is a full-featured backend for editing different office documents like Open Document, Word, Excel, etc. online in your browser. The software is open source and can be easily deployed and integrated into existing server software. Available frontends are [Nextcloud](/index.php/Nextcloud "Nextcloud") or the Onlyoffice CommunityServer. It can be also used in own software, see [following examples](https://github.com/ONLYOFFICE/document-server-integration) for PHP, Nodejs, etc.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Database](#Database)
    *   [2.2 Webserver](#Webserver)
*   [3 Starting](#Starting)

## Installation

[Install](/index.php/Install "Install") the [onlyoffice-documentserver](https://aur.archlinux.org/packages/onlyoffice-documentserver/) package. Further you will need [Postgresql](/index.php/Postgresql "Postgresql") as a database backend and the [Redis](/index.php/Redis "Redis") and [rabbitmq](https://www.archlinux.org/packages/?name=rabbitmq) services installed.

## Configuration

### Database

The Postgresql database backend needs to be configured. Here's an example database setup:

```
$ sudo -i -u postgres psql -c "CREATE DATABASE onlyoffice;"
$ sudo -i -u postgres psql -c "CREATE USER onlyoffice WITH password 'onlyoffice';"
$ sudo -i -u postgres psql -c "GRANT ALL privileges ON DATABASE onlyoffice TO onlyoffice;"

```

To migrate the documentserver database schema, run following command:

```
$ psql -hlocalhost -Uonlyoffice -d onlyoffice -f /usr/share/webapps/onlyoffice/documentserver/server/schema/postgresql/createdb.sql

```

### Webserver

Here's an example for the [Nginx](/index.php/Nginx "Nginx") webserver:

 `/etc/nginx/sites-available/onlyoffice-documentserver` 
```
map $http_host $this_host {
  "" $host;
  default $http_host;
}
map $http_x_forwarded_proto $the_scheme {
  default $http_x_forwarded_proto;
  "" $scheme;
}
map $http_x_forwarded_host $the_host {
  default $http_x_forwarded_host;
  "" $this_host;
}
map $http_upgrade $proxy_connection {
  default upgrade;
  "" close;
}
proxy_set_header Host $http_host;
proxy_set_header Upgrade $http_upgrade;
proxy_set_header Connection $proxy_connection;
proxy_set_header X-Forwarded-Host $the_host;
proxy_set_header X-Forwarded-Proto $the_scheme;
server {
  listen 0.0.0.0:80;
  listen [::]:80 default_server;
  server_tokens off;
  rewrite ^\/OfficeWeb(\/apps\/.*)$ /web-apps$1 redirect;
  location / {
    proxy_pass http://localhost:8000;
    proxy_http_version 1.1;
  }
  location /spellchecker/ {
    proxy_pass http://localhost:8080/;
    proxy_http_version 1.1;
  }
}
```

## Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the following services if you wish to use them locally on the same machine: `rabbitmq redis postgresql`. Finally start the documentserver services: `onlyoffice-spellchecker onlyoffice-fileconverter onlyoffice-docservice`.