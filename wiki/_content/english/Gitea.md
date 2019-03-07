Related articles

*   [Gogs](/index.php/Gogs "Gogs")
*   [Git](/index.php/Git "Git")

[Gitea](https://gitea.io/) is a community managed fork of [Gogs](/index.php/Gogs "Gogs"), lightweight code hosting solution written in Go and published under the MIT license.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PostgreSQL](#PostgreSQL)
        *   [2.1.1 With TCP socket](#With_TCP_socket)
        *   [2.1.2 With Unix socket](#With_Unix_socket)
    *   [2.2 MariaDB/MySQL](#MariaDB/MySQL)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Enable SSH Support](#Enable_SSH_Support)
        *   [4.1.1 Setup your domain](#Setup_your_domain)
        *   [4.1.2 Configure SSH](#Configure_SSH)
    *   [4.2 Disable HTTP protocol](#Disable_HTTP_protocol)
    *   [4.3 Binding on restricted ports](#Binding_on_restricted_ports)
    *   [4.4 Enable Dark Theme](#Enable_Dark_Theme)
    *   [4.5 Configure nginx as reverse proxy](#Configure_nginx_as_reverse_proxy)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Database error on startup after upgrade to 1.5.0](#Database_error_on_startup_after_upgrade_to_1.5.0)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gitea](https://www.archlinux.org/packages/?name=gitea) or [gitea-git](https://aur.archlinux.org/packages/gitea-git/) package.

Gitea requires the use of a database backend, the following are supported:

*   [MariaDB](/index.php/MariaDB "MariaDB")/[MySQL](/index.php/MySQL "MySQL")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [SQLite](/index.php/SQLite "SQLite")
*   [TiDB](https://github.com/pingcap/tidb) (not packaged in the repos though)

## Configuration

The user configuration file is located at `/etc/gitea/app.ini`. Do **not** edit the main configuration file (`/var/lib/gitea/conf/app.ini`), since this file is included in the binary and will be overwritten on each update.

Gitea repository data will be saved into `/var/lib/gitea/repos/`. It is possible to overrule this location in `/etc/gitea/app.ini`, if you do so you might need to edit `ReadWritePaths` in the systemd service file.

See the [Gitea docs](https://docs.gitea.io/en-us/customizing-gitea/) for more configuration examples.

### PostgreSQL

[Install](/index.php/PostgreSQL#Installation "PostgreSQL") and [configure](/index.php/PostgreSQL#Initial_configuration "PostgreSQL") [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

Choose between TCP or UNIX Socket, and jump to the corresponding section.

**Note:** When Gitea and PostgreSQL are on the same machine, you should use a Unix socket, as it is faster and more secure.

#### With TCP socket

Create the new user while connecting to the server as `postgres` user (you will be prompted for a password for the new user):

```
[postgres]$ createuser -P gitea

```

Create the Gitea database, owned by `gitea` user:

```
[postgres]$ createdb -O gitea gitea

```

[PostgreSQL#Configure PostgreSQL to be accessible from remote hosts](/index.php/PostgreSQL#Configure_PostgreSQL_to_be_accessible_from_remote_hosts "PostgreSQL")

Verify it works:

```
$ psql --host=*ip_address* --dbname=gitea --username=gitea --password

```

Configure Gitea:

 `/etc/gitea/app.ini` 
```
DB_TYPE             = postgres
HOST                = *hostadress:port*
NAME                = gitea
USER                = gitea
; Use PASSWD = `your password` for quoting if you use special characters in the password.
PASSWD              = **password**
```

#### With Unix socket

Create the new user while connecting to the server as `postgres` user:

```
[postgres]$ createuser gitea

```

Create the Gitea database, owned by `gitea` user:

```
[postgres]$ createdb -O gitea gitea

```

Setup the Unix socket by adding the following line to `/var/lib/postgres/data/pg_hba.conf`:

```
local    gitea           gitea           peer

```

[Restart](/index.php/Restart "Restart") `postgresql.service`.

Verify it works:

```
[gitea]$ psql --dbname=gitea --username=gitea

```

Configure Gitea:

 `/etc/gitea/app.ini` 
```
DB_TYPE             = postgres
HOST                = /run/postgresql/
NAME                = gitea
USER                = gitea
PASSWD              =
```

### MariaDB/MySQL

**Note:** MySQL socket support can be enabled by using `/var/run/mysqld/mysqld.sock` as the listen address.

The following is an example of setting up [MariaDB](/index.php/MariaDB "MariaDB"), setting your desired password:

 `$ mysql -u root -p` 
```
mysql> CREATE DATABASE `gitea` DEFAULT CHARACTER SET `utf8mb4` COLLATE `utf8mb4_unicode_ci`;
mysql> CREATE USER `gitea`@'localhost' IDENTIFIED BY '**password'**;
mysql> GRANT ALL PRIVILEGES ON `gitea`.* TO `gitea`@`localhost`;
mysql> \q
```

Try connecting to the new database with the new user:

```
$ mysql -u **gitea** -p -D gitea

```

Configure MariaDB on first run or update `app.ini`:

 `/etc/gitea/app.ini` 
```
DB_TYPE  = mysql
HOST     = 127.0.0.1:3306 ; or /var/run/mysqld/mysqld.sock
NAME     = gitea
USER     = *gitea*
PASSWD   = **password**
```

## Usage

[Start/enable](/index.php/Start/enable "Start/enable") `gitea.service`, the webinterface should listen on `[http://localhost:3000](http://localhost:3000)`.

When running Gitea for the first time it should redirect to `[http://localhost:3000/install](http://localhost:3000/install)`.

**Note:** You might want to configure a reverse proxy to access remotely, e.g. [nginx](#Configure_nginx_as_reverse_proxy).

**Note:** If you want Gitea to listen on all interfaces, set `HTTP_ADDR = 0.0.0.0` in `/etc/gitea/app.ini`.

## Tips and tricks

### Enable SSH Support

Make sure [SSH](/index.php/SSH "SSH") is properly configured and running.

#### Setup your domain

You might want to set `SSH_DOMAIN`, e.g.:

 `/etc/gitea/app.ini`  `SSH_DOMAIN                 = git.domain.tld` 
**Note:** If you set the `PROTOCOL` to be `unix`, then you need to set `LOCAL_ROOT_URL` to `[http://unix/](http://unix/)`. See this [comment](https://github.com/go-gitea/gitea/issues/3741#issuecomment-377334757)

#### Configure SSH

If you use `AllowUsers` in your [SSH configuration](/index.php/OpenSSH#Configuration_2 "OpenSSH"), add `AllowUsers gitea` to it, e.g.:

 `/etc/ssh/sshd_config` 
```
...
AllowUsers archie **gitea**
...
```

[Restart](/index.php/Restart "Restart") `sshd.service` if you use it (nothing to do if you use `sshd.socket`).

### Disable HTTP protocol

By default, the ability to interact with repositories by HTTP protocol is enabled. You may want to disable HTTP-support if using [SSH](/index.php/SSH "SSH"), by setting `DISABLE_HTTP_GIT` to `true`.

### Binding on restricted ports

If you use the built-in SSH server and want Gitea to bind it on port 22, or if you want to bind Gitea webserver directly on ports 80/443 (that is in a setup without proxy), you will need to add a [drop-in systemd unit override](/index.php/Systemd#Drop-in_files "Systemd"):

 `/etc/systemd/system/gitea.service.d/override.conf` 
```
[Service]
AmbientCapabilities=CAP_NET_BIND_SERVICE
CapabilityBoundingSet=CAP_NET_BIND_SERVICE
PrivateUsers=false
```

### Enable Dark Theme

In the *ui* section, you can set the `DEFAULT_THEME` to `arc-green` for making the web interface use a dark background.

### Configure nginx as reverse proxy

The following is an example of using [nginx](/index.php/Nginx#Managing_server_entries "Nginx") as reverse proxy for Gitea over unix socket (you need to [provide the SSL certificate](/index.php/Transport_Layer_Security#Obtaining_a_certificate "Transport Layer Security")):

 `/etc/nginx/servers-available/gitea.conf` 
```
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name git.domain.tld;

    ssl_certificate /path/to/fullchain.pem;
    ssl_certificate_key /path/to/privkey.pem;

    location / {
        proxy_pass [http://unix:/run/gitea/gitea.socket](http://unix:/run/gitea/gitea.socket);
    }
}
```

Update the `[server]` section of `app.ini`:

 `/etc/gitea/app.ini` 
```
[server]
PROTOCOL                   = unix
DOMAIN                     = git.domain.tld
ROOT_URL                   = [https://git.domain.tld](https://git.domain.tld)
HTTP_ADDR                  = /run/gitea/gitea.socket
LOCAL_ROOT_URL             =
```

**Note:** You do not need to activate any SSL certificate options in `/etc/gitea/app.ini`.

Finally update the *cookie* section - set `COOKIE_SECURE` to `true`.

## Troubleshooting

### Database error on startup after upgrade to 1.5.0

A problem can appear after the upgrade to 1.5.0\. The service will not start, and the following error is present in the logs:

 `/var/log/gitea/gitea.log`  `2018/08/21 16:11:12 [...itea/routers/init.go:60 GlobalInit()] [E] Failed to initialize ORM engine: migrate: do migrate: Sync2: Error 1071: Specified key was too long; max key length is 767 bytes` 

To fix this problem, run the following command as the `root` user on your MySQL/MariaDB server

 `$ mysql -u root -p`  `MariaDB> set global innodb_large_prefix = `ON`;` 

gitea should stop complaining about key size and startup properly.

## See also

*   [Gitea Documentation](https://docs.gitea.io/)