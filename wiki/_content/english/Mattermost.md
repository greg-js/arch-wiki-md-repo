From [Mattermost's homepage:](http://www.mattermost.org/)

	Mattermost is an open source, self-hosted Slack-alternative. As an alternative to proprietary SaaS messaging, Mattermost brings all your team communication into one place, making it searchable and accessible anywhere.

This article aims at describing how to install Mattermost in production mode on one, two or thee machines. This article is directly managed by the Mattermost community and is linked from the official Mattermost documentation. If you intend to make modifications, please post to the talk page first.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Preview Docker Setup installation](#Preview_Docker_Setup_installation)
    *   [1.2 Production Docker Setup installation](#Production_Docker_Setup_installation)
    *   [1.3 Production Manual installation](#Production_Manual_installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Set up a database server](#Set_up_a_database_server)
        *   [2.1.1 MySQL/MariaDB](#MySQL.2FMariaDB)
        *   [2.1.2 PostgreSQL using TCP/IP socket connection](#PostgreSQL_using_TCP.2FIP_socket_connection)
        *   [2.1.3 PostgreSQL using Unix-domain socket connection](#PostgreSQL_using_Unix-domain_socket_connection)
    *   [2.2 Configuring Mattermost](#Configuring_Mattermost)
    *   [2.3 Starting Mattermost](#Starting_Mattermost)
    *   [2.4 Testing Mattermost](#Testing_Mattermost)
    *   [2.5 Post-Installation Mattermost Configuration](#Post-Installation_Mattermost_Configuration)
*   [3 Useful tips](#Useful_tips)
    *   [3.1 TLS/SSL via reverse web-proxy](#TLS.2FSSL_via_reverse_web-proxy)
        *   [3.1.1 nginx](#nginx)
        *   [3.1.2 Lighttpd2](#Lighttpd2)

## Installation

Mattermost can be installed in two ways on Arch Linux:

*   Using [Docker](/index.php/Docker "Docker");
*   Using the [AUR](/index.php/AUR "AUR") package;

### Preview Docker Setup installation

**Warning:** The Preview Docker installation is not meant for production use, but only development and testing purposes, like testing if translations are [correcly translated in context](https://docs.mattermost.com/developer/localization.html#test-translations).

*   Step 1: Install Docker using the following commands as root:

```
pacman -S docker
systemctl enable docker.service
systemctl start docker.service
gpasswd -a <username> docker
newgrp docker

```

*   Step 2: Start Docker container:

```
docker run --name mattermost-preview -d --publish 8065:8065 mattermost/mattermost-preview

```

*   Step 3: When Docker is done fetching the image, open `[http://localhost:8065/](http://localhost:8065/)` in your browser.

### Production Docker Setup installation

By using Docker, you do not need to install a database server and configure Mattermost dependencies. Since the docker image comes with all the dependencies automatically bundled, this is less work for you.

However, the tradeoff is that you cannot choose the database backend or web server you want, but ony those provided in the docker images, unless you make your own.

*   Install Docker using the following commands as root:

```
pacman -S docker
systemctl enable docker.service
systemctl start docker.service
gpasswd -a <username> docker
newgrp docker

```

*   Build the docker container, from the community maintained repository:

```
git clone https://github.com/mattermost/mattermost-docker.git -b team-and-enterprise
cd mattermost-docker
docker-compose build
docker-compose up -d

```

*   When Docker is done building the image, open `[http://localhost:8065/](http://localhost:8065/)` in your browser.

Please [refer to the official guide](https://docs.mattermost.com/install/prod-docker.html) to know how to configure TLS, email, enable Enterprise features and use several server nodes using Docker Compose.

There are also some Docker images provided on the [Official Mattermost Docker Hub page](https://hub.docker.com/r/mattermost/). Please also refer to [the repository of the Mattermost Docker images](https://github.com/mattermost/mattermost-docker).

### Production Manual installation

Simply install the unofficial package [mattermost](https://aur.archlinux.org/packages/mattermost/) from the [AUR](/index.php/AUR "AUR"). Please read [AUR](/index.php/AUR "AUR") articles if you are not familiar with this Arch Linux concept.

*   User and group `mattermost` have been created during installation;
*   The mattermost directory is located at `/var/lib/mattermost` and is owned by `mattermost:root`.

Then continue with the [#Configuration](#Configuration).

## Configuration

### Set up a database server

Mattermost requires a database backend. If you plan to run it on the same machine, first install either [MySQL](/index.php/MySQL "MySQL")/MariaDB or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") as database. Follow one of the following sections and then proceed with [#Configuring Mattermost](#Configuring_Mattermost).

While MySQL is officially supported, please note the official guide goes through the PostgreSQL steps only.

#### MySQL/MariaDB

 `$ mysql -u root -p` 
```
CREATE DATABASE mattermost;
CREATE USER mmuser IDENTIFIED BY 'mmuser_password';
GRANT ALL ON mattermost.* TO mmuser;
exit;

```

#### PostgreSQL using TCP/IP socket connection

**Note:** When Mattermost and postgresql are on the same machine, it is recommended to use unix socket mechanism for the connection between Mattermost and Postgresql, as it is more secure and faster. Settings specific to the unix socket connection are detailed in the section [#PostgreSQL using Unix-domain socket connection](#PostgreSQL_using_Unix-domain_socket_connection) below.

Here are the instructions are for a connection via the TCP/IP socket using PostgreSQL. This guide we will assume this server has an IP address of `10.10.10.1`. If you are installing on the same machine substitute `10.10.10.1` with `127.0.0.1`.

*   Step 1: Install PostgreSQL:

```
# pacman -Syu postgresql postgresql-libs

```

	Please note the main configuration files are `postgresql.conf`, `ph_hba.conf`, `pg_ident.conf`. After installation, you will find a sample of these files in the `/usr/share/postgresql` directory. Please copy these files in the `/var/lib/postgres/data` default directory, remove the `.sample` at the end of the file name and edit them according to your needs.

	For more details, please refer to the [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") article.

*   Step 2: Start and enable the systemd service:

```
# systemctl start postgresql.service
# systemctl enable postgresql.service

```

*   Step 3: During instalation, PostgreSQL created a user account called `postgres`. Log into that account:

```
$ sudo -i -u postgres

```

*   Step 4: Initialize the database cluster. This has to be done once:

```
[postgres]$ initdb --locale $LANG -E UTF8 -D '/var/lib/postgres/data'

```

*   Step 5: Connect to the postgreSQL server as user postgres:

```
[postgres]$ psql

```

*   Step 6: Create the Mattermost database:

```
postgres=# CREATE DATABASE mattermost;

```

*   Step 7: Create the Mattermost user:

```
postgres=# CREATE USER mmuser WITH PASSWORD 'mmuser_password';

```

*   Step 8: Grant the user access to the Mattermost database:

```
postgres=# GRANT ALL PRIVILEGES ON DATABASE mattermost to mmuser;

```

*   Step 9: Exit out of PostgreSQL:

```
postgres=# \q

```

*   Step 10: Exit the postgres user:

```
[postgres]$ exit

```

*   Step 11: Allow Postgres to listen on all assigned IP Addresses.

	Edit the config file `/var/lib/postgres/data/postgresql.conf`.

	In the connections and authentications section, uncomment the `listen_addresses` line and edit to your needs::

```
listen_addresses = 'localhost,my_local_ip_address'

```

	You can use `*` to listen on all local addresses

*   Step 12: Allow the mattermost server to talk to the postgres database

	Edit the config file `/var/lib/postgres/data/pg_hba.conf`.

	Add the following line to the `IPv4 local connections`:

```
host all all 10.10.10.2/32 md5

```

*   Step 13: Reload Postgres database:

```
# systemctl restart postgresql.service

```

	Check with `netstat` or the default `ss` tool from [iproute2](https://www.archlinux.org/packages/?name=iproute2) command to see postgresql actually running on given ip and port::

```
# netstat -anp | grep 5432

```

```
# ss -autnp src :5432

```

*   Step 14: Attempt to connect with the new created user to verify everything looks good:

```
$ psql --host=10.10.10.1 --dbname=mattermost --username=mmuser --password
mattermost=> \q

```

#### PostgreSQL using Unix-domain socket connection

Below are the instructions specific to a connection between Postgresql and Mattermost via an Unix-domain socket. Only changes from the original setup described above are mentioned.

Based on the [section above](#PostgreSQL_using_TCP.2FIP_socket_connection), change the steps accordingly:

*   Step 5: Name the database `mattermost_db`
*   Step 6: Name the user `mattermost`
*   Step 11: Add the following line instead:

```
local   mattermost_db       mattermost          peer       map=mattermap

```

	Append the following line to `/var/lib/pgsql/9.4/data/pg_ident.conf`:

```
mattermap      mattermost              mattermost

```

	It maps unix user `mattermost` to psql user `mattermost`.

*   Step 13: Verify everything looks good::

```
$ su mattermost
$ psql --dbname=mattermost_db --username=mattermost
mattermost_db=>

```

Continue by following the following section [#Configuring Mattermost](#Configuring_Mattermost) and apply changes related to the UNIX socket.

### Configuring Mattermost

You'll find the configuration file at `/etc/webapps/mattermost/config.json`.

There are essentially two things you need to change, depending on which database you are using.

The `"DriverName": "..."` setting:

*   For MySQL (default), make sure it is set to `"mysql"`.
*   For PostgreSQL, set it to `"postgres"` (*not* `postgre**sql**`).

The connection string `"DataSource": "..."` should match your database and user settings:

*   For MySQL, set it to something like `"**mmuser**:**mmuser_password**@unix(/run/mysqld/mysqld.sock)/**mattermost**?charset=utf8mb4,utf8"`.
*   For PostgreSQL
    *   using a network socket : set it to something like `"postgres://**mmuser**:**mmuser_password**@127.0.0.1:5432/**mattermost**?sslmode=disable&connect_timeout=10"`.
    *   using an unix socket : set it to `"postgres:///mattermost?host=/run/postgresql"` ; take care of the 3 slashes after `"postgres:"`, `"mattermost"` is the name of the database and `"/run/postgresql"` is the directory containing your socket

**Note:** Be sure to replace `mmuser_password` with whatever password you configured the user to have

### Starting Mattermost

The package provides `mattermost.service`, which can be normally [started](/index.php/Started "Started") and [enabled](/index.php/Enabled "Enabled").

### Testing Mattermost

Open up a browser and navigate to [http://localhost:8065/](http://localhost:8065/) and that should give you a mattermost chat startpage.

### Post-Installation Mattermost Configuration

*   Step 1: Navigate to your Matterost install and create a team and user.

*   Step 2: The first user in the system is automatically granted the `system_admin` role, which gives you access to the System Console.

*   Step 3: From the `town-square` channel click the dropdown and choose the `System Console` option.

*   Step 4: Update `Notification > Email` settings to setup an SMTP email service. The example below assumes AmazonSES.

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

*   Step 5: Update `File > Storage` settings by changing `Local Directory Location` from `./data/` to `/mattermost/data`.

*   Step 6: Update `General > Logging` settings by setting `Log to The Console` to `false`.

*   Step 7: Feel free to modify other settings.

*   Step 8: Restart the Mattermost Service by typing:

```
# systemctl restart mattermost.service

```

## Useful tips

### TLS/SSL via reverse web-proxy

Since Mattermost doesn't support self signed TLS/SSL keys in their [Android](/index.php/Android "Android") or [iOS](/index.php/IOS "IOS") app, a good thing to do is to [setup a reverse web proxy](https://docs.mattermost.com/install/config-proxy-nginx.html?highlight=proxy#configuring-nginx-as-a-proxy-for-mattermost-server).

The main benefits of a proxy are:

*   SSL termination
*   http to https redirect
*   Port mapping 80 to 8065
*   Standard request logs

Proxying can be achieved either through:

*   [nginx](/index.php/Nginx "Nginx")
*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")

#### nginx

*   Step 1: Install [nginx-mainline](https://www.archlinux.org/packages/?name=nginx-mainline). Since [nginx](/index.php/Nginx "Nginx") has two flavors and Mattermost is using quite recent technologies, it is recommended to choose the nginx flavor mainline and not the stable branch. To learn the differences, please read [this article](https://www.nginx.com/blog/nginx-1-6-1-7-released/).

*   Step 2: Enable and start the server:

```
# systemctl enable nginx
# systemctl start nginx

```

	The default served page at `[http://127.0.0.1](http://127.0.0.1)` is located at `/usr/share/nginx/html/index.html`.

	The following command should return a `Welcome to NGINX!` page:

```
$ curl http://127.0.0.1

```

*   Step 3: Map a FQDN (fully qualified domain name) like `mattermost.example.com` to point to the nginx server.

*   Step 4: Configure nginx to proxy connections from the internet to the Mattermost Server. Create and edit the nginx configuration file `/etc/nginx/sites-available/mattermost`.

```
upstream backend {
    server 127.0.0.1:8065;
}

proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=mattermost_cache:10m max_size=3g inactive=120m use_temp_path=off;

server {
    listen 80;
    server_name    mattermost.example.com;

    location /api/v3/users/websocket {
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
        proxy_read_timeout 600s;
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

*   Step 5: Enable the mattermost server:

```
# mkdir /etc/nginx/servers-enabled
# ln -s /etc/nginx/servers-available/mattermost /etc/nginx/server-enabled/mattermost

```

*   Step 6: Restart nginx:

```
# systemctl restart nginx.service

```

*   Step 7: Verify you can see Mattermost thru the proxy by typing:

```
curl http://localhost

```

	You should see a page titled `Mattermost`.

*   Step 8: As there is now a free and an open certificate security called [let's encrypt](https://letsencrypt.org/), let's take benefit of it and install a certificate using the recommended tool called [Certbot](https://certbot.eff.org) ACME client. Follow instructions for [nginx on Arch Linux client](https://certbot.eff.org/#arch-nginx).

	Install the Certbot client::

```
# pacman -Syu certbot

```

*   Step 9: Obtain a cert using the [webroot plugin](https://certbot.eff.org/docs/using.html#webroot):

```
# certbot certonly --webroot -w /var/www/example -d example.com -d www.example.com

```

	The above command will obtain a single cert for `example.com` and `www.example.com`, assuming the root of these servers is located at `/var/www/example`. Certbot will try to place a file in directory `/var/www/example/.well-known/acme-challenge` and then read it.

*   Step 10: Modify your nginx configuration file accordingly `/etc/nginx/sites-available/mattermost`:

```
upstream backend {
    server 10.10.10.2:8065;
}

server {
    listen         80;
    server_name    mattermost.example.com;
    return         301 https://$server_name$request_uri;
}

proxy_cache_path /var/cache/nginx levels=1:2 keys_zone=mattermost_cache:10m max_size=3g inactive=120m use_temp_path=off;

server {
    listen 443 ssl;
    server_name mattermost.example.com;

    ssl on;
    ssl_certificate /etc/letsencrypt/live/yourdomainname/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/yourdomainname/privkey.pem;
    ssl_session_timeout 5m;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers 'EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH';
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    location /api/v3/users/websocket {
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header X-Forwarded-Ssl on;
        client_max_body_size 50M;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Frame-Options SAMEORIGIN;
        proxy_buffers 256 16k;
        proxy_buffer_size 16k;
        proxy_read_timeout 600s;
        proxy_pass http://backend;
    }

    location / {
        proxy_set_header X-Forwarded-Ssl on;
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

*   Step 11: Restart nginx:

```
# systemctl restart nginx.service

```

*   Step 12: Run the following command to check your setup is correct:

```
# certbot renew --dry-run

```

*   Step 13: Write the systemd service file `/etc/systemd/system/letsencrypt.renewal.service` to start the setup the Letsencrypt cert automatic renewal:

```
[Unit]
Description=Renew let's encrypt certificates

[Service]
ExecStart=/usr/bin/certbot renew --quiet

```

*   Step 14: Write the [systemd timer](/index.php/Systemd/Timers "Systemd/Timers") `/etc/systemd/system/letsencrypt.renewal.timer`:

```
[Unit]
Description=start letsencrypt.renewal.service every 12 hours

[Timer]
OnUnitActiveSec=12hours

[Install]
WantedBy=timers.target

```

*   Step 15: Start and enable these two systemd files.

*   Step 16: Check that your SSL certificate is set up correctly.

	Test the SSL certificate by visiting a site such as [ssllabs](https://www.ssllabs.com/ssltest/index.html).

	If there’s an error about the missing chain or certificate path, there is likely an intermediate certificate missing that needs to be included.

#### Lighttpd2

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

Assuming you have a certificate at `/etc/lighttpd2/certs/lighttpd2.pem` this would serve as a descent reverse web proxy for mattermost on standard web-ports. See [mod_vhost](http://doc.lighttpd.net/lighttpd2/mod_vhost.html) if you want to transfer the `proxy "127.0.0.1:8065"` line into a virtual host domain.