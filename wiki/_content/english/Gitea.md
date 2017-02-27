[Gitea](https://gitea.io/) is a community managed fork of [Gogs](/index.php/Gogs "Gogs"), lightweight code hosting solution written in Go and published under the MIT license.

## Contents

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
    *   [3.1 MariaDB/MySQL](#MariaDB.2FMySQL)
    *   [3.2 Enable SSH Support](#Enable_SSH_Support)
    *   [3.3 Disable HTTP protocol](#Disable_HTTP_protocol)
*   [4 Advanced Configuration](#Advanced_Configuration)
    *   [4.1 Configure nginx as reverse proxy](#Configure_nginx_as_reverse_proxy)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gitea](https://aur.archlinux.org/packages/gitea/) or [gitea-git](https://aur.archlinux.org/packages/gitea-git/) package.

Gitea requires the use of a database backend, the following are supported:

*   [MariaDB](/index.php/MariaDB "MariaDB")/[MySQL](/index.php/MySQL "MySQL")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [SQLite](/index.php/SQLite "SQLite")
*   [TiDB](https://github.com/pingcap/tidb)

## Running

**Note:** If you want Gitea to listen on all interfaces, set `HTTP_ADDR = 0.0.0.0` in `/var/lib/gitea/custom/conf/app.ini`.

[Start/enable](/index.php/Start/enable "Start/enable") `gitea.service`, the webinterface should listen on `[http://localhost:3000](http://localhost:3000)`.

When running Gitea for the first time it should redirect to `[http://localhost:3000/install](http://localhost:3000/install)`.

## Configuration

**Note:** [gitea-git](https://aur.archlinux.org/packages/gitea-git/) already provides a basic configuration file of `/var/lib/gitea/custom/conf/app.ini` on first install.

The user configuration file should be located at `/var/lib/gitea/custom/conf/app.ini`. Do **not** edit the main configuration file (`/var/lib/gitea/conf/app.ini`), since this file is included in the binary and will be overwritten on each update. Instead copy (if not exists) `/var/lib/gitea/conf/app.ini` to `/var/lib/gitea/custom/conf/app.ini`.

Gitea application and repository data will be saved into */var/lib/gitea*, however it is possible to set custom locations in `/var/lib/gitea/custom/conf/app.ini`.

### MariaDB/MySQL

**Note:** MySQL socket support can be enabled by using `/var/run/mysqld/mysqld.sock` as the listen address.

The following is an example of setting up [MariaDB](/index.php/MariaDB "MariaDB"):

 `$ mysql -u root -p` 
```
mysql> CREATE DATABASE `gitea` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_general_ci`;
mysql> CREATE USER `gitea`@'localhost' IDENTIFIED BY 'password';
mysql> GRANT ALL PRIVILEGES ON `gitea`.* TO `gitea`@`localhost`;
mysql> \q
```

Try connecting to the new database with the new user:

```
$ mysql -u **gitea** -p -D gitea

```

Configure MariaDB on first run or by updating `app.ini`:

 `/var/lib/gitea/custom/conf/app.ini` 
```
DB_TYPE  = mysql
HOST     = 127.0.0.1:3306 ; or /var/run/mysqld/mysqld.sock
NAME     = gitea
USER     = gitea
PASSWD   = **password**
```

### Enable SSH Support

**Note:**

*   [gitea-git](https://aur.archlinux.org/packages/gitea-git/) provides a `gitea` [group](/index.php/Group "Group") and [user](/index.php/User "User").
*   [gitea](https://aur.archlinux.org/packages/gitea/) uses `git` as [group](/index.php/Group "Group")/[user](/index.php/User "User"), use `git` instead of `gitea` on instructions given below.
*   See [SSH keys#Key ignored by the server](/index.php/SSH_keys#Key_ignored_by_the_server "SSH keys") if the prompt for password keeps active.

**Warning:** If you do all configuration via SSH do not close the session before you tested that everything is working, else you may lock yourself out.

*   Make sure [SSH](/index.php/SSH "SSH") has been properly configured.
*   Create the `gitea` [group](/index.php/Group "Group") and [user](/index.php/User "User") with `/home/gitea` as home directory:

```
# groupadd --system gitea
# useradd --system -c 'Gitea' -g gitea -m -d /home/gitea -s /bin/bash gitea

```

*   Set correct permissions:

```
# chown -R gitea:gitea /var/log/gitea
# chown -R gitea:gitea /var/lib/gitea

```

*   Update `app.ini` to the running [SSH](/index.php/SSH "SSH") configuration:

 `/var/lib/gitea/custom/conf/app.ini` 
```
[server]
; Disable SSH feature when not available
DISABLE_SSH = **false**
; Domain name to be exposed in clone URL
SSH_DOMAIN = %(DOMAIN)s
; Port number to be exposed in clone URL
SSH_PORT = **22**
; Root path of SSH directory, default is '~/.ssh', but you have to use '/home/git/.ssh'.
SSH_ROOT_PATH = **/home/gitea/.ssh**
```

*   Update the [SSH configuration](/index.php/Secure_Shell#Configuration_2 "Secure Shell") with `AuthorizedKeysFile .ssh/authorized_keys` and `AllowUsers gitea`, e.g.:

 `/etc/ssh/sshd_config` 
```
Port 22
AllowUsers archie **gitea**
PermitRootLogin no
StrictModes yes
PubkeyAuthentication yes
AuthorizedKeysFile **.ssh/authorized_keys**
PasswordAuthentication no
PermitEmptyPasswords no
PrintMotd no
Subsystem sftp /usr/lib/ssh/sftp-server
```

*   [Restart](/index.php/Restart "Restart") `gitea.service` and `sshd.service`
*   Generate a [SSH key pair](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") on the **client** (if non exists)
*   Copy the contents of the (newly) generated `~/.ssh/id_rsa.pub` to **Add Key** on the **Your Settings**, **SSH Keys** on the Gitea webinterface.

You should now be able to use SSH-authentication to manage the repositories, without entering an username/password.

### Disable HTTP protocol

By default, the ability to interact with repositories by HTTP protocol is enabled. You may want to disable HTTP-support if using [SSH](/index.php/SSH "SSH"), by setting `DISABLE_HTTP_GIT` to **true**.

## Advanced Configuration

See the [Gogs FAQ's](https://gogs.io/docs/intro/faqs) for more configuration examples.

### Configure nginx as reverse proxy

**Tip:** [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") is a free, automated, and open certificate authority. A plugin is available to request valid SSL certificates straight from the command line and automatic configuration.

An example of using [nginx](/index.php/Nginx "Nginx") as reverse proxy including [OpenSSL](/index.php/OpenSSL "OpenSSL"):

 `/etc/nginx/servers-available/git` 
```
# redirect to ssl
server {
  listen 80;
  listen [::]:80;
  server_name git.domain.tld;
  return 301 [https://$server_name$request_uri](https://$server_name$request_uri);
}

server {
  listen 443 ssl http2;
  listen [::]:443 ssl http2;
  server_name git.domain.tld;
  client_max_body_size 50M;
  ssl_certificate ssl/**cert.crt**;
  ssl_certificate_key ssl/**cert.key**;
  location / {
    proxy_pass [http://localhost:3000](http://localhost:3000);
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
  }
}
```

Update the *server* section of `app.ini`:

 `/var/lib/gitea/custom/conf/app.ini` 
```
[server]
PROTOCOL               = http
DOMAIN                 = git.domain.tld
ROOT_URL               = [https://git.domain.tld/](https://git.domain.tld/)
HTTP_ADDR              = 0.0.0.0
HTTP_PORT              = 3000
```

**Note:** You don't need to activate any SSL certificate options in `app.ini`.

Finally update the *cookie* section - set COOKIE_SECURE to **true**.

## See also

*   [Gitea Documentation](https://docs.gitea.io/)
*   [Gogs Documentation](https://gogs.io/docs)