From [Mattermost's homepage:](http://www.mattermost.org/)

	Mattermost is an open source, self-hosted Slack-alternative.

	As an alternative to proprietary SaaS messaging, Mattermost brings all your team communication into one place, making it searchable and accessible anywhere.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Setting up the database](#Setting_up_the_database)
        *   [2.1.1 PostgreSQL](#PostgreSQL)
        *   [2.1.2 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [2.2 Configuring Mattermost](#Configuring_Mattermost)
*   [3 Starting mattermost](#Starting_mattermost)
*   [4 Testing](#Testing)
*   [5 Useful tips](#Useful_tips)
    *   [5.1 TLS/SSL via reverse web-proxy](#TLS.2FSSL_via_reverse_web-proxy)
        *   [5.1.1 TLS/SSL via Lighttpd2](#TLS.2FSSL_via_Lighttpd2)

## Installation

**Note:** Mattermost requires a database backend. If you plan to run it on the same machine, first install either [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). The official guide goes through the PostgreSQL steps hence we will focus on it here as well.

**Note:** There are quicker ways to install mattermost using [Docker](/index.php/Docker "Docker"). There's a [one-line install](http://docs.mattermost.com/install/docker-local-machine.html#arch) that works great.

[Install](/index.php/Install "Install") the [mattermost](https://aur.archlinux.org/packages/mattermost/) package.

## Configuration

### Setting up the database

Mattermost requires either [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") or [MySQL](/index.php/MySQL "MySQL")/MariaDB as database. Follow one of the following sections and then proceed with [#Configuring Mattermost](#Configuring_Mattermost).

#### PostgreSQL

```
user$ sudo -i -u postgres
postgres$ psql

```

```
postgres=# CREATE DATABASE mattermost;
postgres=# CREATE USER mmuser WITH PASSWORD 'mmuser_password';
postgres=# GRANT ALL PRIVILEGES ON DATABASE mattermost TO mmuser;
postgres=# \q
postgres$ exit
```

Verify that your new user and database works from your normal user:

```
psql --host=127.0.0.1 --dbname=mattermost --username=mmuser --password

```
 `mattermost=> \q` 

#### MySQL/MariaDB

 `$ mysql -u root -p` 
```
CREATE DATABASE mattermost;
CREATE USER mmuser IDENTIFIED BY 'mmuser_password';
GRANT ALL ON mattermost.* TO mmuser;
exit;

```

### Configuring Mattermost

You'll find the configuration file at `/etc/webapps/mattermost/config.json`.

There are essentially two things you need to change, depending on which database you are using.

The `"DriverName": "..."` setting:

*   For MySQL (default), make sure it is set to `"mysql"`.
*   For PostgreSQL, set it to `"postgres"` (*not* `postgre**sql**`).

The connection string `"DataSource": "..."` should match your database and user settings:

*   For MySQL, set it to something like `"**mmuser**:**mmuser_password**@unix(/run/mysqld/mysqld.sock)/**mattermost**?charset=utf8mb4,utf8"`.
*   For PostgreSQL, set it to something like `"postgres://**mmuser**:**mmuser_password**@127.0.0.1:5432/**mattermost**?sslmode=disable&connect_timeout=10"`.

**Note:** Be sure to replace `mmuser_password` with whatever password you configured the user to have

## Starting mattermost

The package provides `mattermost.service`, which can be normally [started](/index.php/Started "Started") and [enabled](/index.php/Enabled "Enabled").

## Testing

Open up a browser and navigate to [http://localhost:8065/](http://localhost:8065/) and that should give you a mattermost chat startpage.

## Useful tips

### TLS/SSL via reverse web-proxy

Since Mattermost doesn't support self signed TLS/SSL keys in their [Android](/index.php/Android "Android") or [iOS](/index.php/IOS "IOS") app, a good thing to do is to setup a reverse web proxy.

Some alterantives are:

*   [Nginx](/index.php/Nginx "Nginx")
*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd") or [lighttpd2-git](https://aur.archlinux.org/packages/lighttpd2-git/)

#### TLS/SSL via Lighttpd2

A quick example using [lighttpd2-git](https://aur.archlinux.org/packages/lighttpd2-git/) with nothing but acting as a proxy for mattermost and mattermost only.

 `/etc/lighttpd2/lighttpd.conf` 
```
setup {

    module_load [
        "mod_accesslog",
        "mod_proxy",
        "mod_openssl"
    ];

    openssl [
        "listen" => "0.0.0.0:443",
        "listen" => "[::]:443",
        "pemfile" => "/etc/lighttpd2/certs/lighttpd2.pem",
        "options" => ["ALL", "NO_TICKET"],
        "verify" => true,
        "verify-any" => true,
        "verify-depth" => 9
    ];

    listen "0.0.0.0:80";
    listen "[::]:80";

    log ["debug" => "", default => "/var/log/lighttpd2/error.log"];
    accesslog "/var/log/lighttpd2/access.log";
    accesslog.format "%h %V %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}\"";

    static.exlude_extensions [ ".php", ".pl", ".fcgi", "~", ".inc" ];

}

openssl.setenv "client-cert";
keepalive.timeout 360;

docroot "/srv/http";
index [ "index.php", "index.html", "index.htm" ];

include "/etc/lighttpd2/mimetypes.conf";

proxy "127.0.0.1:8065";
```

Assuming you have a certificate at `/etc/lighttpd2/certs/lighttpd2.pem` this would serve as a descent reverse web proxy for mattermost on standard web-ports. See [mod_vhost](http://doc.lighttpd.net/lighttpd2/mod_vhost.html) if you want to transfer the `proxy "127.0.0.1:8065"` line into a virtual host domain.