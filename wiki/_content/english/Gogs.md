Related articles

*   [Gitea](/index.php/Gitea "Gitea")

[Gogs](http://gogs.io/) (Go Git Service) is a Self Hosted Git service, which was written in the [Go](/index.php/Go "Go") programming language.

## Contents

*   [1 Packages](#Packages)
*   [2 Installation](#Installation)
*   [3 First start](#First_start)
*   [4 Configuration](#Configuration)
    *   [4.1 SSH](#SSH)
    *   [4.2 .gitignore and license files](#.gitignore_and_license_files)
    *   [4.3 Database](#Database)
        *   [4.3.1 SQLite](#SQLite)
        *   [4.3.2 PostgreSQL](#PostgreSQL)
        *   [4.3.3 MariaDB](#MariaDB)
*   [5 Theme](#Theme)
*   [6 Restart after Upgrade](#Restart_after_Upgrade)
*   [7 SSH port](#SSH_port)
*   [8 See also](#See_also)

## Packages

*   [gogs](https://aur.archlinux.org/packages/gogs/) - Release package
*   [gogs-git](https://aur.archlinux.org/packages/gogs-git/) - Git `master` branch package [GitHub master branch](https://github.com/gogits/gogs)
*   [gogs-dev-git](https://aur.archlinux.org/packages/gogs-dev-git/) - Git `dev` branch package [GitHub dev branch](https://github.com/gogits/gogs/tree/develop)

Each package provides multiple options for configuring the backend/storage for the service, see [#Configuration](#Configuration)

## Installation

Installing Gogs from the [AUR](/index.php/AUR "AUR") instead of manually has the added benefit that lots of steps have been taken care of for you (e.g. permissions and ownership for files, etc).

Also before installing the Gogs package from the [AUR](/index.php/AUR "AUR"), you need to choose a database backend if you're planning to host Gogs on the same machine as the database:

*   SQLite: [sqlite](https://www.archlinux.org/packages/?name=sqlite) - For configuration of Gogs with SQLite see [#SQLite](#SQLite).
*   PostgreSQL: [postgresql](https://www.archlinux.org/packages/?name=postgresql) - Read [PostgreSQL#Installing PostgreSQL](/index.php/PostgreSQL#Installing_PostgreSQL "PostgreSQL") to set it up and start the [daemon](/index.php/Daemon "Daemon") and for configuration of Gogs with PostgreSQL see [#PostgreSQL](#PostgreSQL).
*   MariaDB: [mariadb](https://www.archlinux.org/packages/?name=mariadb) - Read [MariaDB#Installation](/index.php/MariaDB#Installation "MariaDB") to set it up and start the [daemon](/index.php/Daemon "Daemon") and for configuration of Gogs with MariaDB see [#MariaDB](#MariaDB).

If you plan to use SSH to interact with your repositories, make sure to add the `gogs` user to the `AllowUsers` entry in `/etc/ssh/sshd_config`.

## First start

After [starting](/index.php/Start "Start") `gogs.service`, you can access the running service over the url `http://[server]:3000`. At first load, you will be redirected to the installation page where you can configure some options. In order to be able to save changes made using the initial configuration page the permissions of the configuration file (owned by root) will have to be modified (either temporary or permanently), for example:

```
# chown gogs:gogs /etc/gogs/app.ini

```

In the configuration file `/etc/gogs/app.ini`, you can change more values (for example the port number).

## Configuration

The Gogs configuration file is located at `/etc/gogs/app.ini`. When you want to edit a configuration option, you need to edit this file and restart the Gogs service before changes will take effect.

### SSH

In order to interact with the git repositories using ssh, and to be able to use the uploaded public keys:

*   set `SSH_ROOT_PATH` in `/etc/gogs/app.ini` to `/var/lib/gogs/.ssh` (see also [documentation](https://gogs.io/docs/advanced/configuration_cheat_sheet)), and ensure that `DISABLE_SSH` is `false`.

*   Add `gogs` to `AllowUsers` in `/etc/ssh/sshd_config`.

*   create `/var/lib/gogs/.ssh` and hand over ownership to the `gogs` user:

```
> mkdir -p /var/lib/gogs/.ssh
> chown -R gogs:gogs /var/lib/gogs/.ssh

```

Public keys will be added by the `gogs` user to `/var/lib/gogs/.ssh/authorized_keys`

### .gitignore and license files

A set of gitignore and license files are included in the package and are stored at `/usr/share/gogs/conf/gitignore` and `/usr/share/gogs/conf/license` respectively.

You can get or create your own .gitignore files [here](http://www.gitignore.io/).

### Database

#### SQLite

Install [sqlite](https://www.archlinux.org/packages/?name=sqlite) and select SQLite on the installation page. Use an absolute path in `/etc/gogs/app.ini` (`PATH` variable in the `[database]` section) for the SQLite database file. To be consistent with the other settings, use `/var/lib/gogs/data/gogs.db` (see also issue [4298](https://github.com/gogits/gogs/issues/4298)).

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

## Theme

The current package (gogs-git* and gogs>=0.4.2) support custom themes. The location for Gogs themes is `/usr/share/themes/gogs/`. Gogs comes with one default theme, but you can easily create a own theme. Just copy the default `theme` directory and change whatever you want. In the `public` directory is every javascript, stylesheet and font file and in the `template` directory are the HTML templates. The current selected theme can be changed over the `app.ini` configuration parameter `STATIC_ROOT_PATH`. Changed it with the absolute path to the new theme.

## Restart after Upgrade

Gogs needs to be restarted after every upgrade because the paths of javascript/css assets will change and therefore break the website. To automate this the following pacman hook can be inserted at `/etc/pacman.d/hooks/gogs.hook`:

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
# setcap CAP_NET_BIND_SERVICE=+eip /usr/share/gogs/gogs

```

Configure gogs SSH server in `/etc/gogs/app.ini`:

```
START_SSH_SERVER       = true
SSH_PORT               = 22
SSH_LISTEN_PORT        = 22

```

## See also

*   [Official Documentation](https://gogs.io/docs)