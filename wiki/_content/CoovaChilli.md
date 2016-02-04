# CoovaChilli

[http://coova.org/CoovaChilli](http://coova.org/CoovaChilli)

## Contents

*   [1 Installation](#Installation)
*   [2 Example configuration](#Example_configuration)
    *   [2.1 FreeRadius](#FreeRadius)
    *   [2.2 Mysql database setup](#Mysql_database_setup)
*   [3 CoovaChilli](#CoovaChilli)
*   [4 daloRADIUS](#daloRADIUS)
*   [5 Start and enable applications](#Start_and_enable_applications)
*   [6 See also](#See_also)

## Installation

Several other applications are required for an example setup of CoovaChilli. [Install](/index.php/Install "Install") the following:

*   [freeradius](https://www.archlinux.org/packages/?name=freeradius)
*   [nginx](https://www.archlinux.org/packages/?name=nginx)
*   [mariadb](https://www.archlinux.org/packages/?name=mariadb)
*   [php](https://www.archlinux.org/packages/?name=php)
*   [daloradius](https://aur.archlinux.org/packages/daloradius/)
*   [coova-chilli](https://aur.archlinux.org/packages/coova-chilli/).

## Example configuration

Example configuration for a full and working CoovaChilli setup. Consider **eth0** is the interface for our incoming internet connection and **eth1** is the gateway interface for our unknown wifi clients and is coonnected to various hot-spots.

### FreeRadius

 `/etc/raddb/clients.conf` 

```
client 127.0.0.1 {
 secret     = mysecret
}

```

Adjust the following settings:

 `/etc/raddb/sql.conf` 

```
        server = "localhost"
        login = "root"
        password = "xxxx"

```

Uncomment the following settings:

 `/etc/raddb/sites-available/default` 

```
authorize {
          sql
}

accounting {
         sql
}

```

Uncomment the following settings:

 `/etc/raddb/radiusd.conf` 

```
       $INCLUDE sql.conf

```

### Mysql database setup

Setup [MariaDB](/index.php/MariaDB "MariaDB") and choose a password for the mysql root user.

```
$ mysql -u root -p
mysql> CREATE DATABASE radius;
mysql> exit
$ mysql -u root -p radius < /usr/share/nginx/html/daloradius/contrib/db/fr2-mysql-daloradius-and-freeradius.sql

```

## CoovaChilli

 `/etc/chilli/defaults` 

```
HS_NETWORK=192.168.10.0
HS_UAMLISTEN=192.168.10.1

HS_RADSECRET=mysecret
HS_UAMSECRET=uamsecret
HS_UAMFORMAT=https://\$HS_UAMLISTEN/hotspotlogin/hotspotlogin.php
HS_UAMHOMEPAGE=https://\$HS_UAMLISTEN

```

## daloRADIUS

```
$ rm /usr/share/nginx/html/index.html
$ cp -r /usr/share/webapps/daloradius/contrib/chilli/portal2/* /usr/share/nginx/html/
```

Adjust the following config values:

 `/usr/share/nginx/html/daloradius/library/daloradius.conf.php` 

```
$configValues['CONFIG_DB_PASS'] = 'xxxx';
$configValues['CONFIG_MAINT_TEST_USER_RADIUSSECRET'] = 'mysecret';
$configValues['CONFIG_DB_TBL_RADUSERGROUP'] = 'radusergroup';

```

Also in these several files:

 `/usr/share/nginx/html/signup-*/library/daloradius.conf.php` 

```
$configValues['CONFIG_DB_PASS'] = 'xxxx';
$configValues['CONFIG_DB_NAME'] = 'radius';
$configValues['CONFIG_DB_TBL_RADUSERGROUP'] = 'radusergroup';
$configValues['CONFIG_SIGNUP_SUCCESS_MSG_LOGIN_LINK'] = "<br />Click <b>here</b>".
                                        " to return to the Login page and start your surfing<br /><br />";

```

## Start and enable applications

```
$ systemctl enable nginx freeradius mysqld coova-chilli
$ systemctl start nginx freeradius mysqld coova-chilli
```

## See also

*   Original tutorial: [http://linux.xvx.cz/2010/03/debian-wi-fi-hotspot-using-coovachilli-freeradius-mysql-and-daloradius/](http://linux.xvx.cz/2010/03/debian-wi-fi-hotspot-using-coovachilli-freeradius-mysql-and-daloradius/)
*   List of Open Source capative portal software and network access control: [https://mohammadthalif.wordpress.com/2010/12/14/list-of-open-source-captive-portal-software-and-network-access-control-nac/#comment-428](https://mohammadthalif.wordpress.com/2010/12/14/list-of-open-source-captive-portal-software-and-network-access-control-nac/#comment-428)

Retrieved from "[https://wiki.archlinux.org/index.php?title=CoovaChilli&oldid=392035](https://wiki.archlinux.org/index.php?title=CoovaChilli&oldid=392035)"