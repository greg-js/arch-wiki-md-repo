Related articles

*   [Django](/index.php/Django "Django")
*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [Nginx](/index.php/Nginx "Nginx")
*   [OpenSSL](/index.php/OpenSSL "OpenSSL")
*   [Certbot](/index.php/Certbot "Certbot")
*   [Redis](/index.php/Redis "Redis")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")

Quoting the [main documentation page](https://docs.funkwhale.audio/index.html):

	[Funkwhale](https://funkwhale.audio/) is a self-hosted, modern, free and open-source music server, heavily inspired by Grooveshark.

Instances can be federated with the ActivityPub protocol.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Installation from AUR](#Installation_from_AUR)
    *   [1.2 Manual install](#Manual_install)
    *   [1.3 Docker install](#Docker_install)
*   [2 Configuration](#Configuration)
    *   [2.1 Host config](#Host_config)
    *   [2.2 Configure nginx](#Configure_nginx)
    *   [2.3 Configure apache](#Configure_apache)
    *   [2.4 Configure PostgreSQL](#Configure_PostgreSQL)
    *   [2.5 Configure Redis](#Configure_Redis)
*   [3 Initialization](#Initialization)
    *   [3.1 Setup](#Setup)
        *   [3.1.1 Log in as funkwhale user](#Log_in_as_funkwhale_user)
    *   [3.2 Database setup](#Database_setup)
*   [4 Version upgrade](#Version_upgrade)
*   [5 Usage](#Usage)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Proxy logs](#Proxy_logs)

## Installation

Funkwhale requires a reverse proxy ([[1]](https://docs.funkwhale.audio/installation/index.html)), so [nginx](/index.php/Nginx "Nginx") or [Apache](/index.php/Apache "Apache") needs to be installed.

It also needs a configured [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") database and a [Redis](/index.php/Redis "Redis") cache server. See [#Configuration](#Configuration) and the respective pages for information.

### Installation from AUR

[Install](/index.php/Install "Install") the [funkwhale](https://aur.archlinux.org/packages/funkwhale/) package.

**Warning:** This installation does not use a python virtualenv, so all the python dependencies are installed, mainly from the AUR. Package versions may be different from the upstream requirements and cause problem.

### Manual install

Follow instructions for the Arch installation at [[2]](https://docs.funkwhale.audio/installation/debian.html). This will install all the components in `/srv/funkwhale`.

### Docker install

Follow instructions for the Docker installation at [[3]](https://docs.funkwhale.audio/installation/docker.html).

## Configuration

The following sections assume that Funkwhale was installed from AUR, for a manual installation, change the folders appropriately.

It also assume that you are using Funkwhale on a local network. See the official [documentation](https://docs.funkwhale.audio/index.html) for making it accessible outside, especially for the certificates using [Certbot](/index.php/Certbot "Certbot").

### Host config

Make sure your `/etc/hosts` file is setup correctly. The Funkwhale server is running on `127.0.0.1` with alias `funkwhale.local`, but this can be changed.

Your `/etc/hosts` file should look something like the following,

```
#<ip-address>   <hostname.domain.org>   <hostname>
127.0.0.1       localhost
::1             localhost
127.0.0.1       funkwhale.local
```

### Configure nginx

See upstream documentation.

**Note:** This section needs to be filled for the AUR installation

### Configure apache

**Note:** You will need [Apache](/index.php/Apache "Apache") configured to run with [Redis](/index.php/Redis "Redis"), [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") and Apache [TLS](/index.php/TLS "TLS") support.

A template Apache configuration file is provided in `/etc/webapps/funkwhale/apache-funkwhale.conf`. It configures the Funkwhale instance to be accessible at `[https://funkwhale.local](https://funkwhale.local)`.

The folder names should be change to fit your installation. More explanation on which lines need to be modified is provided in [[4]](https://docs.funkwhale.audio/installation/index.html#reverse-proxy-setup).

Copy the template to the apache configuration folder,

```
$ cp /etc/webapps/funkwhale/apache-funkwhale.conf /etc/httpd/conf/extra/funkwhale.conf

```

Next, edit the [Apache](/index.php/Apache "Apache") configuration file and add the following:

 `# /etc/httpd/conf/httpd.conf` 
```
Include conf/extra/funkwhale.conf

```

For the changes to be applied, you need to restart `httpd.service` (Apache) using [systemd](/index.php/Systemd#Using_units "Systemd").

### Configure PostgreSQL

Here we follow the official documentation: [[5]](https://docs.funkwhale.audio/installation/external_dependencies.html)

Connect to the [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") command line using the `postgres` user to create the `funkwhale` user and the database.

 `$ sudo -u postgres psql` 
```
postgres=# CREATE DATABASE "funkwhale"
postgres=#  WITH ENCODING 'utf8';
postgres=# CREATE USER funkwhale;
postgres=# GRANT ALL PRIVILEGES ON DATABASE funkwhale TO funkwhale;
postgres=# \c funkwhale;
postgres=# CREATE EXTENSION "unaccent";
```

The last two lines load the `unaccent` extension, which is needed for funkwhale to work.

### Configure Redis

There is no particular configuration for Redis.

## Initialization

### Setup

Funkwhale should be run as the `funkwhale` user. It is automatically created by the AUR package, if you followed the manual installation, create it with,

```
$ useradd -r -d /srv/funkwhale -m funkwhale -c "Funkwhale music server -s /sbin/nologin"

```

Next, the folder where Funkwhale will store the users data should be created in `/srv/funkwhale`. It should be owned by the `funkwhale` user,

```
$ mkdir /srv/funkwhale
$ chown funkwhale:funkwhale /srv/funkwhale

```

To work, Funkwhale needs several environment variables to be present, these should be defined in the environment file `/srv/funkwhale/config/env`. There is a template at `/etc/webapps/funkwhale/env.template`, copy it and modify it to fit your installation.

```
$ mkdir /srv/funkwhale/config
$ cp /etc/webapps/funkwhale/env.template /srv/funkwhale/config/env
$ chown -R funkwhale:funkwhale /srv/funkwhale/config

```

The `FUNKWHALE_HOSTNAME` variable should correspond to the hostname in `/etc/hosts`. `DJANGO_ALLOWED_HOSTS` needs also to match the address where the funkwhale instance will be reached. You should generate a unique `DJANGO_SECRET_KEY` and change the paths accordingly to your installation.

#### Log in as funkwhale user

The next commands should be run as the `funkwhale` user. Create sub-folders for api files and to store the music,

 `$ sudo -u funkwhale -H bash` 
```
[funkwhale]$ cd /srv/funkwhale
[funkwhale]$ mkdir -p api data/static data/media data/music
```

**Tip:** As you will need to run several commands as the `funkwhale` user with the environment variables loaded, you can use the following command-line after logging in:

`[funkwhale]$ export $(cat /srv/funkwhale/config/env`

For convenience, you can copy this line to /srv/funkwhale/.bashrc (or whichever shell you are using), so it is loaded automatically everytime you log in.

### Database setup

You need to initialize the database before launching the application,

 `$ sudo -u funkwhale -H bash`  `[funkwhale]$ python /usr/share/webapps/funkwhale/api/manage.py migrate` 

Then create a superuser for your Funkwhale instance,

```
[funkwhale]$ python /usr/share/webapps/funkwhale/api/manage.py createsuperuser

```

You also need to collect the static files for the webapp,

```
[funkwhale]$ python /usr/share/webapps/funkwhale/api/manage.py collectstatic

```

## Version upgrade

All the command should be entered as `funkwhale` [user](#Log_in_as_funkwhale_user). [Stop](/index.php/Stop "Stop") the `funkwhale.service` before upgrading.

The static files have to be collected again,

```
[funkwhale]$ python /usr/share/webapps/funkwhale/api/manage.py collectstatic --no-input

```

Then apply database migrations,

```
[funkwhale]$ python /usr/share/webapps/funkwhale/api/manage.py migrate

```

**Warning:** Check that the apache or nginx configuration file did not change before restarting the service. Consult the official documentation for incompatible changes.

The `funkwhale.service` can be [started](/index.php/Started "Started") again.

**Note:** All the instructions for upgrading are given on the official documentation [[6]](https://docs.funkwhale.audio/upgrading/index.html).

## Usage

Upstream provides systemd services that are already installed by the AUR package.

To start the instance, just [start](/index.php/Start "Start") `funkwhale.service`.

This starts three services, you can check their status with:

```
$ systemctl status funkwhale-\*

```

## Troubleshooting

### Proxy logs

Apache logs for funkwhale are available,

```
$ tail -f /var/log/httpd/funkwhale/error.log

```