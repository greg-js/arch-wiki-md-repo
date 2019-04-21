[Zabbix](http://zabbix.com) is a full-featured monitoring solution for larger networks. It can discover all kind of networking devices using different methods, check machine states and applications, sending pre-defined alarm messages and visualize complex data correlations.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Server setup](#Server_setup)
    *   [1.1 Installation](#Installation)
        *   [1.1.1 Zabbix-server installation](#Zabbix-server_installation)
        *   [1.1.2 Zabbix-frontend installation](#Zabbix-frontend_installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 ICMP/ping discovery](#ICMP/ping_discovery)
    *   [1.4 Starting](#Starting)
*   [2 Agent setup](#Agent_setup)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration_2)
    *   [2.3 Starting](#Starting_2)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Debugging a Zabbix agent](#Debugging_a_Zabbix_agent)
    *   [3.2 Monitor Arch Linux system updates](#Monitor_Arch_Linux_system_updates)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Error "Specified key was too long; max key length is 767 bytes"](#Error_"Specified_key_was_too_long;_max_key_length_is_767_bytes")
*   [5 See also](#See_also)

## Server setup

### Installation

#### Zabbix-server installation

Install the [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server) package. This includes the necessary scripts for use with MariaDB or PostgreSQL. The rest of this guide will assume that you will be using MariaDB.

#### Zabbix-frontend installation

Install the [zabbix-frontend-php](https://www.archlinux.org/packages/?name=zabbix-frontend-php) package. You also have to choose a web server with PHP support, e.g.:

*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [nginx](/index.php/Nginx "Nginx")

Or one of the other servers found in [Category:Web server](/index.php/Category:Web_server "Category:Web server").

### Configuration

Symlink the Zabbix web application directory to your http document root, e.g.:

```
$ ln -s /usr/share/webapps/zabbix /srv/http/zabbix

```

Make sure to adjust following variables to these minimal values in your `/etc/php/php.ini`:

```
extension=bcmath
extension=gd
extension=sockets
extension=mysqli
extension=gettext
post_max_size = 16M
max_execution_time = 300
max_input_time = 300
date.timezone = "UTC"

```

In this example, we create on localhost a MariaDB database called `zabbix` for the user `zabbix` identified by the password `test` and then import the database templates. This connection will be later used by the Zabbix server and web application:

```
$ mysql -u root -p -e "create database zabbix character set utf8"
$ mysql -u root -p -e "grant all on zabbix.* to zabbix@localhost identified by 'test'"
$ mysql -u zabbix -p zabbix < /usr/share/zabbix-server/mysql/schema.sql
$ mysql -u zabbix -p zabbix < /usr/share/zabbix-server/mysql/images.sql
$ mysql -u zabbix -p zabbix < /usr/share/zabbix-server/mysql/data.sql

```

Now edit `/etc/zabbix/zabbix_server.conf` with the database settings:

 `/etc/zabbix/zabbix_server.conf` 
```
DBName=zabbix
DBUser=zabbix
DBPassword=test
```

### ICMP/ping discovery

To use ICMP discovery (e.g. ping) in Zabbix, [install](/index.php/Install "Install") the [fping](https://www.archlinux.org/packages/?name=fping) package.

### Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `zabbix-server-mysql.service` unit, if you are using MariaDB.

Finally you can access Zabbix via your local web server, e.g.: [http://localhost/zabbix/](http://localhost/zabbix/), finish the installation wizard and access the frontend the first time. The default username is `Admin` and password `zabbix`.

See appendix for a link to the official documentation, which explains all further steps in using it.

## Agent setup

### Installation

Install [zabbix-agent](https://www.archlinux.org/packages/?name=zabbix-agent) for each monitoring target, including your monitoring server where [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server) is installed. [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server) does no longer include `zabbix-agent`.

### Configuration

Simply edit the `zabbix_agentd.conf` and replace the server variable with the IP of your monitoring server. Only servers from this/these IP will be allowed to access the agent.

```
Server=<IP of Zabbix server>
ServerActive=<IP of Zabbix server>

```

Further make sure the port `10050` on your device being monitored is not blocked and is properly forwarded.

### Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `zabbix-agent` service.

## Tips and tricks

### Debugging a Zabbix agent

On the client site, you can check the state of an item like this:

```
$ zabbix_agentd -t hdd.smart[sda,Temperature_Celsius]

```

On the server/monitoring site, try this:

```
$ zabbix_get -s *host* -k hdd.smart[sda,Temperature_Celsius]

```

### Monitor Arch Linux system updates

Here is an approach on how to monitor your Arch Linux clients for available system update using a custom `UserParameter`:

 `/etc/zabbix/zabbix_agentd.conf`  `Include=/etc/zabbix/zabbix_agentd.conf.d/*.conf`  `/etc/zabbix/zabbix_agentd.conf.d/archlinuxupdates.conf`  `UserParameter=archlinuxupdates,checkupdates | wc -l` 

You have to restart `zabbix-agentd` to apply the new configuration. The keyword for the item you later use in the web frontend is `archlinuxupdates`. It returns an integer representing the count of available updates.

## Troubleshooting

### Error "Specified key was too long; max key length is 767 bytes"

While importing the databases, you might get this error message. In order to solve this, you will have to change the code page configuration for your MariaDB database: [MariaDB#Using UTF8MB4](/index.php/MariaDB#Using_UTF8MB4 "MariaDB").

## See also

*   [Official manual](https://www.zabbix.com/documentation/)