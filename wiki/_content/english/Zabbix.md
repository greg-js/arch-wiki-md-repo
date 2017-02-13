[Zabbix](http://zabbix.com) is a full-featured monitoring solution for larger networks. It can discover all kind of networking devices using different methods, check machine states and applications, sending pre-defined alarm messages and visualize complex data correlations.

## Contents

*   [1 Server setup](#Server_setup)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Starting](#Starting)
*   [2 Agent setup](#Agent_setup)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration_2)
    *   [2.3 Starting](#Starting_2)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Debugging a Zabbix agent](#Debugging_a_Zabbix_agent)
    *   [3.2 Monitor ArchLinux system updates](#Monitor_ArchLinux_system_updates)
*   [4 See also](#See_also)

## Server setup

### Installation

If you want to use the Zabbix server with [MariaDB](/index.php/MariaDB "MariaDB"), install [zabbix-server-mysql](https://aur.archlinux.org/packages/zabbix-server-mysql/) from the [AUR](/index.php/AUR "AUR"). For [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") as database backend, you should use [zabbix-server](https://aur.archlinux.org/packages/zabbix-server/). You also have to choose a web server with PHP support, e.g.:

*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [nginx](/index.php/Nginx "Nginx")

Or one of the other servers found in the [web server](/index.php/Category:Web_server "Category:Web server") category. You may edit the [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD") if you plan to use Nginx as web-server, since by default they have [apache](https://www.archlinux.org/packages/?name=apache) and [php-apache](https://www.archlinux.org/packages/?name=php-apache) as dependency.

### Configuration

Symlink the Zabbix web application directory to your http document root, e.g.:

```
$ ln -s /usr/share/webapps/zabbix /srv/http/zabbix

```

Make sure to adjust following variables to these minimal values in your `php.ini`:

```
extension=bcmath.so
extension=gd.so
extension=sockets.so
extension=mysqli.so
post_max_size = 16M
max_execution_time = 300
max_input_time = 300
date.timezone = "UTC"

```

In this example, we create on localhost a MariaDB database called `zabbix` for the user `zabbix` identified by the password `test` and then import the database templates. This connection will be later used by the Zabbix server and web application:

```
$ mysql -u root -p -e "create database zabbix"
$ mysql -u root -p -e "grant all on zabbix.* to zabbix@localhost identified by 'test'"
$ mysql -u zabbix -p zabbix < /usr/share/zabbix/database/schema.sql
$ mysql -u zabbix -p zabbix < /usr/share/zabbix/database/images.sql
$ mysql -u zabbix -p zabbix < /usr/share/zabbix/database/data.sql

```

Note: If you using PHP 7.1 you need to edit /srv/http/zabbix/include/func.inc.php

```
   function str2mem($val) {
       $val = trim($val);
       $last = strtolower(substr($val, -1));
       switch ($last) {
               case 'g':
                       $val = (int) $val * 1024;
                       /* falls through */
               case 'm':
                       $val = (int) $val * 1024;
                       /* falls through */
               case 'k':
                       $val = (int) $val * 1024;
       }
       return $val;

```

}

### Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `zabbix-server` service.

Finally you can access Zabbix via your local web server, e.g.: [http://127.0.0.1/zabbix](http://127.0.0.1/zabbix), finish the installation wizard and access the frontend the first time. The default username is `Admin` and password `zabbix`.

See appendix for a link to the official documentation, which explains all further steps in using it.

## Agent setup

### Installation

Currently, the server package already includes [zabbix-agent](https://aur.archlinux.org/packages/zabbix-agent/), so you do not have to install this package on your monitoring server. However, for monitoring targets, the client part is more minimal, standalone and easy to deploy, just install [zabbix-agent](https://aur.archlinux.org/packages/zabbix-agent/).

### Configuration

Simply edit the `zabbix_agentd.conf` and replace the server variable with the IP of your monitoring server. Only servers from this/these IP will be allowed to access the agent.

```
Server=<IP of Zabbix server>
ServerActive=<IP of Zabbix server>

```

Further make sure the port `10050` on your device being monitored is not blocked and is properly forwarded.

### Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `zabbix-agentd` service.

## Tips and tricks

### Debugging a Zabbix agent

On the client site, you can check the state of an item like this:

```
zabbix_agentd -t hdd.smart[sda,Temperature_Celsius]

```

On the server/monitoring site, try this:

```
zabbix_get -s *host* -k hdd.smart[sda,Temperature_Celsius]

```

### Monitor ArchLinux system updates

Here's an approach on how to monitor your ArchLinux clients for available system update using a custom `UserParameter`:

 `/etc/zabbix/zabbix_agentd.conf`  `Include=/etc/zabbix/zabbix_agentd.conf.d/*.conf`  `/etc/zabbix/zabbix_agentd.conf.d/archlinuxupdates.conf`  `UserParameter=archlinuxupdates,checkupdates | wc -l` 

You have to restart `zabbix-agentd` to apply the new configuration. The keyword for the item you later use in the web frontend is `archlinuxupdates`. It returns an integer representing the count of available updates.

## See also

*   [Official manual for version 2.0](https://www.zabbix.com/documentation/doku.php?id=2.0)