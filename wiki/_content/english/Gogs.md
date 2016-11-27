[Gogs](http://gogs.io/) (Go Git Service) is a Self Hosted Git service, which was written in the [Go](/index.php/Go "Go") programming language.

## Contents

*   [1 Packages](#Packages)
*   [2 Installation](#Installation)
*   [3 First start](#First_start)
*   [4 Configuration](#Configuration)
    *   [4.1 .gitignore and license files](#.gitignore_and_license_files)
    *   [4.2 Database](#Database)
        *   [4.2.1 SQLite](#SQLite)
        *   [4.2.2 PostgreSQL](#PostgreSQL)
        *   [4.2.3 MariaDB](#MariaDB)
    *   [4.3 SMTP](#SMTP)
    *   [4.4 oAuth](#oAuth)
    *   [4.5 Logging](#Logging)
    *   [4.6 Caching](#Caching)
*   [5 Theme](#Theme)
*   [6 Restart after Upgrade](#Restart_after_Upgrade)
*   [7 SSH port](#SSH_port)
*   [8 See also](#See_also)

## Packages

*   [gogs](https://aur.archlinux.org/packages/gogs/) - Release package
*   [gogs-git](https://aur.archlinux.org/packages/gogs-git/) - Git `master` branch package [GitHub master branch](https://github.com/gogits/gogs)
*   [gogs-git-dev](https://aur.archlinux.org/packages/gogs-git-dev/) - Git `dev` branch package [GitHub dev branch](https://github.com/gogits/gogs/tree/develop)

In all three package is sqlite, redis and memcache activate for compile. To use it, you need to edit the configuration file `app.ini` (see [#Configuration](#Configuration)).

## Installation

Installing Gogs from the [AUR](/index.php/AUR "AUR") instead of manually has the added benefit that lots of steps have been taken care of for you (e.g. permissions and ownership for files, etc).

Also before installing the Gogs package from the [AUR](/index.php/AUR "AUR"), you need to choose a database backend if you're planning to host Gogs it on the same machine as the database:

*   SQLite: [sqlite](https://www.archlinux.org/packages/?name=sqlite) - For configuration of Gogs with SQLite see [#SQLite](#SQLite).
*   PostgreSQL: [postgresql](https://www.archlinux.org/packages/?name=postgresql) - Read [PostgreSQL#Installing PostgreSQL](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL") to set it up and start the [daemon](/index.php/Daemon "Daemon") and for configuration of Gogs with PostgreSQL see [#PostgreSQL](#PostgreSQL).
*   MariaDB: [mariadb](https://www.archlinux.org/packages/?name=mariadb) - Read [MariaDB#Installation](/index.php/MariaDB#Installation "MariaDB") to set it up and start the [daemon](/index.php/Daemon "Daemon") and for configuration of Gogs with MariaDB see [#MariaDB](#MariaDB).

If you plan to use SSH to interact with your repositories, make sure to add the `gogs` user to the `AllowUsers` entry in `/etc/ssh/sshd_config`.

## First start

After [starting](/index.php/Start "Start") `gogs.service`, you can access the running service over the url `http://[server]:3000`. At the first execute, you will redirect to the installation page. Here you can configure some minor configuration options. In the configuration file `/srv/gogs/conf/app.ini`, you can change more values (for example the port number).

## Configuration

After the first start, Gogs created a own configuration file in the directory `/srv/gogs/config`. When you want to edit a configuration option, you need to edit this file.

### .gitignore and license files

Add the files into the directory `/srv/gogs/conf/gitignore` or `/srv/gogs/conf/license`. When the directory not exist, you need to created it in the first step.

You can get or create own .gitignore files on this [page](http://www.gitignore.io/).

### Database

#### SQLite

Install [sqlite](https://www.archlinux.org/packages/?name=sqlite) and select SQLite on the installation page.

#### PostgreSQL

Install [postgresql](https://www.archlinux.org/packages/?name=postgresql) and select Postgresql on the installation page.

```
# su - postgres -c 
# createuser -P gogs
# createdb -O gogs gogs

```

#### MariaDB

Install [mariadb](https://www.archlinux.org/packages/?name=mariadb) and setup a user and database:

```
# CREATE DATABASE `ishouldchangethisdatabasename` DEFAULT CHARACTER SET `utf8` COLLATE `utf8_unicode_ci`;
# CREATE USER 'ishouldchangethisusername'@'localhost' IDENTIFIED BY 'ishouldchangethispassword';
# GRANT ALL ON `ishouldchangethisdatabasename`.* TO 'ishouldchangethisusername'@'localhost';

```

On the installation page select **mysql** and insert your configured user, password and database name.

### SMTP

### oAuth

### Logging

### Caching

## Theme

The current package (gogs-git* and gogs>=0.4.2) support custom themes. The location for Gogs themes is `/usr/share/themes/gogs/`. Gogs comes with one default theme, but you can easily create a own theme. Just copy the default `theme` directory and change what every you want. In the `public` directory is every javascript, stylesheet and font file and in the `template` directory are the HTML templates. The current selected theme can be changed over the `app.ini` configuration parameter `STATIC_ROOT_PATH`. Changed it with the absolute path to the new theme.

## Restart after Upgrade

Gogs needs to be restarted after every upgrade because the paths of javascript/css assets will change and therefor break the website. To automate this the following pacman hook can be inserted to `/etc/pacman.d/hooks/gogs.hook`:

```
[Trigger]
Type = File
Operation = Upgrade
Target = usr/share/gogs/gogs
[Action]
Description = Restart gogs...
When = PostTransaction
Exec = /usr/bin/systemctl try-restart gogs.service

```

## SSH port

If you are using a non-default port for your SSH server, you will get not-so-pretty clone URLs. You can make gogs start its own SSH server, listening on port 22.

Allow gogs binary to bind privileged ports:

```
sudo setcap CAP_NET_BIND_SERVICE=+eip /usr/share/gogs/gogs

```

Configure gogs SSH server in `/srv/gogs/conf/app.ini`:

```
START_SSH_SERVER       = true
SSH_PORT               = 22
SSH_LISTEN_PORT        = 22

```

## See also

*   [Official Documentation](https://gogs.io/docs)