From [Mattermost's homepage](http://www.mattermost.org/):

	Mattermost is an open source, self-hosted Slack-alternative. As an alternative to proprietary SaaS messaging, Mattermost brings all your team communication into one place, making it searchable and accessible anywhere.

This article describes how to install and configure the Mattermost server.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 With Docker](#With_Docker)
    *   [1.2 With AUR](#With_AUR)
*   [2 Database setup](#Database_setup)
    *   [2.1 MySQL/MariaDB](#MySQL.2FMariaDB)
    *   [2.2 PostgreSQL](#PostgreSQL)
        *   [2.2.1 With TCP socket](#With_TCP_socket)
        *   [2.2.2 With Unix socket](#With_Unix_socket)
    *   [2.3 Configuring Mattermost](#Configuring_Mattermost)
*   [3 Setting up Mattermost](#Setting_up_Mattermost)
*   [4 Useful tips](#Useful_tips)
    *   [4.1 Valid HTTPS via reverse web-proxy](#Valid_HTTPS_via_reverse_web-proxy)
        *   [4.1.1 nginx](#nginx)
        *   [4.1.2 Lighttpd2](#Lighttpd2)
    *   [4.2 Testing translations and pull requests](#Testing_translations_and_pull_requests)

## Installation

The Mattermost server can be installed in two ways:

*   Using [Docker](/index.php/Docker "Docker") by following the steps described in [#With Docker](#With_Docker);
*   Using an [AUR](/index.php/AUR "AUR") package, by following the steps described in [#With AUR](#With_AUR).

An [Electron](https://electron.atom.io/)-based desktop client is provided by the [mattermost-desktop](https://aur.archlinux.org/packages/mattermost-desktop/) package.

### With Docker

By using Docker, you do not need to manually install a database server and configure Mattermost dependencies. Since the docker image comes with all the dependencies automatically bundled, this is less work for you.

However, the tradeoff is that you cannot choose the database back-end or web server you want, but only those provided in the docker images, unless you make your own.

*   [Install Docker](/index.php/Docker#Installation "Docker").
*   Download the source:

```
$ git clone https://github.com/mattermost/mattermost-docker.git 

```

*   Edit the `docker-compose.yml` file
    *   Uncomment the `args:` line.
    *   For Team edition, remove the comments on the line: `- edition=team`.
    *   Adopt the UID/GID in the section to those of the owner of your `./volumes/app/mattermost/*` folders.
    *   Add the port forwarding statements as a child of `app` section (e.g. between `build` and `restart`)

```
ports:
  - "127.0.0.1:8065:8000"
```

*   Build and start the docker container:

```
$ cd mattermost-docker
$ docker-compose build
$ docker-compose up -d

```

*   Open `[http://localhost:8000/](http://localhost:8000/)` in your browser.

Please refer to [the official guide](https://docs.mattermost.com/install/prod-docker.html) for how to configure TLS, email, enable Enterprise features and use several server nodes using Docker Compose.

There are also some Docker images provided on the [official Mattermost Docker Hub page](https://hub.docker.com/r/mattermost/). Please also refer to [the repository of the Mattermost Docker images](https://github.com/mattermost/mattermost-docker).

### With AUR

[Install](/index.php/Install "Install") the [mattermost](https://aur.archlinux.org/packages/mattermost/) package, or [mattermost-git](https://aur.archlinux.org/packages/mattermost-git/) for the development version.

*   The installation will create the `mattermost` user and group.
*   The mattermost directory is located at `/var/lib/mattermost` and is owned by `mattermost:root`.

Continue with [#Database setup](#Database_setup).

## Database setup

Mattermost requires a database back-end. If you plan to run it on the same machine, first install either [MySQL](/index.php/MySQL "MySQL")/MariaDB or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") as database. Follow one of the following sections and then proceed with [#Configuring Mattermost](#Configuring_Mattermost).

While MySQL is officially supported, please note the official guide goes through the PostgreSQL steps only.

### MySQL/MariaDB

 `$ mysql -u root -p` 
```
CREATE DATABASE mattermostdb;
CREATE USER mmuser IDENTIFIED BY 'mmuser_password';
GRANT ALL ON mattermostdb.* TO mmuser;

```

### PostgreSQL

1\. [Install](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL") and [configure](/index.php/PostgreSQL#Initial_configuration "PostgreSQL") [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

2\. Connect to the server as user `postgres`:

	 `sudo -u postgres psql` 

3.a. Create the Mattermost database:

	 `CREATE DATABASE mattermostdb;` 

**Note:** When Mattermost and PostgreSQL are on the same machine, you should use a Unix socket, as it is faster and more secure.

#### With TCP socket

3.b. Create `mmuser` user and give it the rights on the database:

```
CREATE USER mmuser WITH PASSWORD 'mmuser_password';
GRANT ALL PRIVILEGES ON DATABASE mattermostdb to mmuser;

```

4\. Exit out of `psql` with `\q`.

5\. [PostgreSQL#Configure PostgreSQL to be accessible from remote hosts](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL")

6\. Verify it works:

	 `$ psql --host=*ip_address* --dbname=mattermostdb --username=mmuser --password` 

#### With Unix socket

3.b. Create `mattermost` user and give it the rights on the database:

```
CREATE USER mattermost;
GRANT ALL PRIVILEGES ON DATABASE mattermostdb to mattermost;

```

4\. Exit out of `psql` with `\q`.

5\. Setup the Unix socket by adding the following line to `/var/lib/postgres/data/pg_hba.conf`:

	 `local    mattermostdb    mattermost    peer` 

6\. [Restart](/index.php/Restart "Restart") `postgresql.service`.

7\. Verify it works:

	 `$ sudo -u mattermost psql --dbname=mattermostdb --username=mattermost` 

Continue with [#Setting up Mattermost](#Setting_up_Mattermost).

### Configuring Mattermost

Mattermost is configured in `/etc/webapps/mattermost/config.json`. Strings need to be quoted.

There are two settings you need to adapt to your database.

The `DriverName` setting: `mysql` for MySQL and `postgres` for PostgreSQL.

The `DataSource`:

*   For MySQL, set it to `**mmuser**:**mmuser_password**@unix(/run/mysqld/mysqld.sock)/**mattermostdb**?charset=utf8mb4,utf8`.
*   For PostgreSQL
    *   TCP socket: `postgres://**mmuser**:**mmuser_password**@127.0.0.1:5432/**mattermostdb**?sslmode=disable&connect_timeout=10`
    *   Unix socket: `postgres:///**mattermostdb**?host=/run/postgresql` ; make sure there are 3 slashes after `postgres:`, `mattermostdb` is the name of the database and `/run/postgresql` is the directory containing the Unix socket

**Note:** Be sure to replace `mmuser_password` with the password of the user.

[Start/enable](/index.php/Start/enable "Start/enable") `mattermost.service` and open [http://localhost:8065/](http://localhost:8065/).

## Setting up Mattermost

1\. Navigate to your Matterost install and create a team and user.

2\. The first user in the system is automatically granted the `system_admin` role, which gives you access to the System Console.

3\. From the `town-square` channel click the dropdown and choose the `System Console` option.

4\. Update `Notification > Email` settings to setup an SMTP email service. The example below assumes AmazonSES.

*   Set `Send Email Notifications` to `true`
*   Set `Require Email Verification` to `true`
*   Set `Feedback Name` to `No-Reply`
*   Set `Feedback Email` to `mattermost@example.com`
*   Set `SMTP Username` to `[YOUR_SMTP_USERNAME]`
*   Set `SMTP Password` to `[YOUR_SMTP_PASSWORD]`
*   Set `SMTP Server` to `email-smtp.us-east-1.amazonaws.com`
*   Set `SMTP Port` to `465`
*   Set `Connection Security` to `TLS`
*   Save the Settings

5\. Update `File > Storage` settings by changing `Local Directory Location` from `./data/` to `/mattermost/data`.

6\. Update `General > Logging` settings by setting `Log to The Console` to `false`.

7\. Feel free to modify other settings.

8\. [Restart](/index.php/Restart "Restart") `mattermost.service`.

## Useful tips

### Valid HTTPS via reverse web-proxy

To securely access your Mattermost server from the Android and iOS apps, which do not support self-signed TLS certificates, you can [setup a reverse web proxy](https://docs.mattermost.com/install/config-proxy-nginx.html?highlight=proxy#configuring-nginx-as-a-proxy-for-mattermost-server).

The main benefits of a proxy are:

*   SSL termination
*   HTTP to HTTPS redirect
*   Port mapping 80 to 8065
*   Standard request logs

Proxying can be achieved with most web servers.

#### nginx

1\. Install and run [nginx](/index.php/Nginx "Nginx"), preferably [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline).

2\. Point your domain name eg. `mattermost.example.com` to the server.

3\. Configure nginx to proxy connections from the internet to the Mattermost Server. Create and edit the nginx configuration file `/etc/nginx/sites-available/mattermost`.

```
upstream backend {
    server 127.0.0.1:8065;
    keepalive 32;
}

proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=mattermost_cache:10m max_size=3g inactive=120m use_temp_path=off;

server {
    listen 80;
    server_name    mattermost.example.com;

    location ~ /api/v[0-9]+/(users/)?websocket$ {
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        client_max_body_size 50M;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Frame-Options SAMEORIGIN;
        proxy_buffers 256 16k;
        proxy_buffer_size 16k;
        client_body_timeout 60;
        send_timeout 300;
        lingering_timeout 5;
        proxy_connect_timeout 90;
        proxy_send_timeout 300;
        proxy_read_timeout 90s;
        proxy_pass http://backend;
    }

    location / {
        client_max_body_size 50M;
        proxy_set_header Connection "";
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Frame-Options SAMEORIGIN;
        proxy_buffers 256 16k;
        proxy_buffer_size 16k;
        proxy_read_timeout 600s;
        proxy_cache mattermost_cache;
        proxy_cache_revalidate on;
        proxy_cache_min_uses 2;
        proxy_cache_use_stale timeout;
        proxy_cache_lock on;
        proxy_pass http://backend;
    }
}

```

4\. Enable the mattermost server:

```
# mkdir /etc/nginx/sites-enabled
# ln -s /etc/nginx/sites-available/mattermost /etc/nginx/sites-enabled/mattermost

```

5\. [Restart](/index.php/Restart "Restart") `nginx.service`.

6\. Verify you can access Mattermost through the proxy:

	 `curl [http://localhost/](http://localhost/)` 

	You should see a page titled `Mattermost`.

7\. Set up [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt").

#### Lighttpd2

A configuration sample for [lighttpd2-git](https://aur.archlinux.org/packages/lighttpd2-git/) to act as a proxy for Mattermost, assuming you have a certificate at `/etc/lighttpd2/certs/lighttpd2.pem`.

See [mod_vhost](http://doc.lighttpd.net/lighttpd2/mod_vhost.html) if you want to transfer the proxy into a virtual host.

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
    accesslog.format "%h %V %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}\"";

    static.exlude_extensions [ ".php", ".pl", ".fcgi", "~", ".inc" ];

}

openssl.setenv "client-cert";
keepalive.timeout 360;

docroot "/srv/http";
index [ "index.php", "index.html", "index.htm" ];

include "/etc/lighttpd2/mimetypes.conf";

proxy "127.0.0.1:8065";

```

### Testing translations and pull requests

You can use the unofficial script [mattermost-prepare-pkgbuild](https://github.com/wget/mattermost-prepare-pkgbuild) to test languages and pull requests.