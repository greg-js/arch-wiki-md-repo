Related articles

*   [Gogs](/index.php/Gogs "Gogs")
*   [Git](/index.php/Git "Git")

[Gitea](https://gitea.io/) is a community managed fork of [Gogs](/index.php/Gogs "Gogs"), lightweight code hosting solution written in Go and published under the MIT license.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 MariaDB/MySQL](#MariaDB.2FMySQL)
*   [3 Usage](#Usage)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Enable SSH Support](#Enable_SSH_Support)
        *   [4.1.1 Setup git user](#Setup_git_user)
        *   [4.1.2 Configure SSH](#Configure_SSH)
        *   [4.1.3 Add SSH-keys for an user](#Add_SSH-keys_for_an_user)
    *   [4.2 Disable HTTP protocol](#Disable_HTTP_protocol)
    *   [4.3 Configure nginx as reverse proxy](#Configure_nginx_as_reverse_proxy)
    *   [4.4 Enable Dark Theme](#Enable_Dark_Theme)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Database error on startup after upgrade to 1.5.0](#Database_error_on_startup_after_upgrade_to_1.5.0)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [gitea](https://aur.archlinux.org/packages/gitea/), [gitea-bin](https://aur.archlinux.org/packages/gitea-bin/) or, [gitea-git](https://aur.archlinux.org/packages/gitea-git/) package.

Gitea requires the use of a database backend, the following are supported:

*   [MariaDB](/index.php/MariaDB "MariaDB")/[MySQL](/index.php/MySQL "MySQL")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [SQLite](/index.php/SQLite "SQLite")
*   [TiDB](https://github.com/pingcap/tidb)

## Configuration

The user configuration file should be located at `/etc/gitea/app.ini`. Do **not** edit the main configuration file (`/var/lib/gitea/conf/app.ini`), since this file is included in the binary and will be overwritten on each update. Instead copy (if not exists already) `/var/lib/gitea/custom/conf/app.ini.sample` to `/etc/gitea/app.ini`.

Gitea repository data will be saved into `/var/lib/gitea/repos/`, or if using [gitea-git](https://aur.archlinux.org/packages/gitea-git/) into `/home/gitea/gitea-repositories`. It is possible to set overrule this location in `/etc/gitea/app.ini`.

See the [Gitea docs](https://docs.gitea.io/en-us/customizing-gitea/) for more configuration examples.

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

**Note:** If you want Gitea to listen on all interfaces, set `HTTP_ADDR = 0.0.0.0` in `/etc/gitea/app.ini`.

## Tips and tricks

### Enable SSH Support

Make sure [SSH](/index.php/SSH "SSH") has been properly configured and running.

#### Setup git user

**Note:** The package [gitea-git](https://aur.archlinux.org/packages/gitea-git/) uses `gitea` as [user](/index.php/User "User")/[group](/index.php/Group "Group") instead of `git`. Users should only have to [#Configure SSH](#Configure_SSH).

Create the `git` [group](/index.php/Group "Group") and home directory for `git`:

```
# groupadd --system git
# usermod -d /home/git -s /usr/bin/bash git
# mkhomedir_helper git

```

Update `/etc/gitea/app.ini` with the home-directory of the user:

 `/etc/gitea/app.ini` 
```
[server]
; Disable SSH feature when not available
DISABLE_SSH = **false**
; Domain name to be exposed in clone URL
SSH_DOMAIN = %(DOMAIN)s
; Port number to be exposed in clone URL
SSH_PORT = **22**
; Root path of SSH directory, default is '~/.ssh', but you have to use '/home/git/.ssh'.
SSH_ROOT_PATH = **/home/git/.ssh** ; /home/gitea/.ssh when using gitea-git
```

#### Configure SSH

Update the [SSH configuration](/index.php/Secure_Shell#Configuration_2 "Secure Shell") with `AuthorizedKeysFile .ssh/authorized_keys` and `AllowUsers git` or `AllowUsers gitea` when using [gitea-git](https://aur.archlinux.org/packages/gitea-git/), e.g.:

 `/etc/ssh/sshd_config` 
```
Port 22
AuthorizedKeysFile **.ssh/authorized_keys**
UseDNS no
PermitUserEnvironment **yes**
PermitRootLogin no
PasswordAuthentication no
PermitEmptyPasswords no
AllowUsers archie **git**
PubkeyAuthentication yes
PrintMotd no
Subsystem sftp /usr/lib/ssh/sftp-server
```

Make sure to set the correct [permissions](/index.php/SSH_keys#Key_ignored_by_the_server "SSH keys") for the [SSH keys](/index.php/SSH_keys "SSH keys").

[Restart](/index.php/Restart "Restart") `gitea.service` and `sshd.service`

#### Add SSH-keys for an user

Generate a [SSH key pair](/index.php/SSH_keys#Generating_an_SSH_key_pair "SSH keys") on the **client** (if not exists already).

Copy the contents of the (newly) generated `~/.ssh/id_rsa.pub` to **Add Key** on the **Your Settings**, **SSH Keys** on the Gitea webinterface.

You should now be able to use SSH-authentication to manage the repositories, without entering an username/password.

### Disable HTTP protocol

By default, the ability to interact with repositories by HTTP protocol is enabled. You may want to disable HTTP-support if using [SSH](/index.php/SSH "SSH"), by setting `DISABLE_HTTP_GIT` to `true`.

### Configure nginx as reverse proxy

**Tip:** [Let’s Encrypt](/index.php/Let%E2%80%99s_Encrypt "Let’s Encrypt") is a free, automated, and open certificate authority. A plugin is available to request valid SSL certificates straight from the command line and automatic configuration.

The following is an example of using [nginx](/index.php/Nginx#Managing_server_entries "Nginx") as reverse proxy for Gitea including [OpenSSL](/index.php/OpenSSL "OpenSSL"):

 `/etc/nginx/servers-available/git` 
```
upstream gitea {
    server 127.0.0.1:3000;
}

server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name git.domain.tld;
    root /var/lib/gitea/public;
    access_log off;
    error_log off;

    location / {
      try_files maintain.html $uri $uri/index.html @node;
    }

    location @node {
      client_max_body_size 0;
      proxy_pass [http://localhost:3000](http://localhost:3000);
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Real-IP $remote_addr;
      proxy_set_header Host $http_host;
      proxy_set_header X-Forwarded-Ssl on;
      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_max_temp_file_size 0;
      proxy_redirect off;
      proxy_read_timeout 120;
    }
}
```

Update the *server* section of `app.ini`:

 `/etc/gitea/app.ini` 
```
[server]
PROTOCOL               = http
DOMAIN                 = git.domain.tld
```

**Note:** You do not need to activate any SSL certificate options in `/etc/gitea/app.ini`.

Finally update the *cookie* section - set `COOKIE_SECURE` to `true`.

### Enable Dark Theme

In the *ui* section, you can set the `DEFAULT_THEME` to `arc-green` for making the web interface use a dark background.

## Troubleshooting

### Database error on startup after upgrade to 1.5.0

A problem can appear after the upgrade to 1.5.0\. The service will not start, and the following error is present in the logs:

 `/var/log/gitea/gitea.log`  `2018/08/21 16:11:12 [...itea/routers/init.go:60 GlobalInit()] [E] Failed to initialize ORM engine: migrate: do migrate: Sync2: Error 1071: Specified key was too long; max key length is 767 bytes` 

To fix this problem, run the following command as the `root` user on your MySQL/MariaDB server

 `$ mysql -u root -p`  `MariaDB> set global innodb_large_prefix = `ON`;` 

gitea should stop complaining about key size and startup properly.

## See also

*   [Gitea Documentation](https://docs.gitea.io/)