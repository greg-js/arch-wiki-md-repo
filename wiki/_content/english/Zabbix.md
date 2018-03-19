[Zabbix](http://zabbix.com) is a full-featured monitoring solution for larger networks. It can discover all kind of networking devices using different methods, check machine states and applications, sending pre-defined alarm messages and visualize complex data correlations.

## Contents

*   [1 Server setup](#Server_setup)
    *   [1.1 Installation](#Installation)
        *   [1.1.1 Zabbix-server installation](#Zabbix-server_installation)
        *   [1.1.2 Zabbix-frontend installation](#Zabbix-frontend_installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Starting](#Starting)
*   [2 Agent setup](#Agent_setup)
    *   [2.1 Installation](#Installation_2)
    *   [2.2 Configuration](#Configuration_2)
    *   [2.3 Starting](#Starting_2)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Debugging a Zabbix agent](#Debugging_a_Zabbix_agent)
    *   [3.2 Monitor ArchLinux system updates](#Monitor_ArchLinux_system_updates)
*   [4 Troubleshooting](#Troubleshooting)
*   [5 See also](#See_also)

## Server setup

### Installation

#### Zabbix-server installation

Install [zabbix-server](https://www.archlinux.org/packages/?name=zabbix-server). This will include the necessary scripts in order to use MariaDB or postgresql. This wiki assumes you will be using MariaDB

#### Zabbix-frontend installation

Install the [zabbix-frontend-php](https://www.archlinux.org/packages/?name=zabbix-frontend-php) package.

You also have to choose a web server with PHP support if you want to use *zabbix-frontend*, e.g.:

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

### Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `zabbix-server-mysql` service, if you are using MariaDB.

Finally you can access Zabbix via your local web server, e.g.: [http://127.0.0.1/zabbix](http://127.0.0.1/zabbix), finish the installation wizard and access the frontend the first time. The default username is `Admin` and password `zabbix`.

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

### Monitor ArchLinux system updates

Here is an approach on how to monitor your ArchLinux clients for available system update using a custom `UserParameter`:

 `/etc/zabbix/zabbix_agentd.conf`  `Include=/etc/zabbix/zabbix_agentd.conf.d/*.conf`  `/etc/zabbix/zabbix_agentd.conf.d/archlinuxupdates.conf`  `UserParameter=archlinuxupdates,checkupdates | wc -l` 

You have to restart `zabbix-agentd` to apply the new configuration. The keyword for the item you later use in the web frontend is `archlinuxupdates`. It returns an integer representing the count of available updates.

## Troubleshooting

While importing the databases, you might get an eror "Specified key was too long; max key length is 767 bytes". In order to solve this, you will have to change the codepage configuration for your MariaDB database: [MySQL#Using UTF8MB4](/index.php/MySQL#Using_UTF8MB4 "MySQL").

## See also

*   [Official manual for version 2.0](https://www.zabbix.com/documentation/doku.php?id=2.0)