# Open Database Connectivity

Open Database Connectivity, commonly ODBC, is an open specification for providing application developers with a predictable API with which to access Data Sources. An ODBC **engine** needs **drivers** to be able to interact with **databases**.

## Contents

*   [1 ODBC engines](#ODBC_engines)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
*   [2 Drivers](#Drivers)
    *   [2.1 FreeTDS](#FreeTDS)
        *   [2.1.1 Installation](#Installation_2)
        *   [2.1.2 Configuration](#Configuration_2)
    *   [2.2 Myodbc](#Myodbc)
        *   [2.2.1 Installation](#Installation_3)
        *   [2.2.2 Configuration](#Configuration_3)
        *   [2.2.3 Create A Symbolic Link](#Create_A_Symbolic_Link)
*   [3 Databases](#Databases)
    *   [3.1 Microsoft SQL Server 2000](#Microsoft_SQL_Server_2000)
    *   [3.2 Mariadb](#Mariadb)
        *   [3.2.1 Create A Test Database](#Create_A_Test_Database)
        *   [3.2.2 Testing the ODBC](#Testing_the_ODBC)
        *   [3.2.3 A Couple Useful Websites](#A_Couple_Useful_Websites)

## ODBC engines

You have two options to chose from: [unixODBC](http://www.unixodbc.org/) and [iODBC](http://en.wikipedia.org/wiki/IODBC). Apparently unixODBC is more widely supported. This document shows how to set up unixODBC. First to access your database on your localhost and then extends the steps to configure MySQL to allow remote access through ODBC.

Additionally you can choose from various [Devart ODBC drivers](https://www.devart.com/odbc/) for SQL Server, Oracle, MySQL, SQLite, Firebird, PostgreSQL, Interbase.

### Installation

```
# pacman -S unixodbc

```

### Configuration

At /etc/odbcinst.ini is where drivers are declared, and /etc/odbc.ini where connections. More instruction at each driver section.

## Drivers

### FreeTDS

**FreeTDS** is a set of libraries for Unix and Linux that allows your programs to natively talk to Microsoft SQL Server and Sybase databases. Technically speaking, FreeTDS is an open source implementation of the TDS (Tabular Data Stream) protocol used by these databases for their own clients.

#### Installation

```
pacman -S freetds

```

#### Configuration

/etc/odbcinst.ini

```
[FreeTDS]
Driver          = /usr/lib/libtdsodbc.so
UsageCount      = 1

```

### Myodbc

Modbc is ODBC driver/connector for mariadb.

#### Installation

Install [myodbc](https://www.archlinux.org/packages/?name=myodbc) from [official repositories](/index.php/Official_repositories "Official repositories").

#### Configuration

Starting with odbcinst.ini, which lists all installed drivers. Su to root and set up your /etc/odbcinst.ini file as follows

```
[MySQL]
Description     = ODBC Driver for MySQL
Driver          = /usr/lib/libmyodbc.so
Setup           = /usr/lib/libodbcmyS.so
FileUsage       = 1

```

#### Create A Symbolic Link

Next we need to create a symlink for libmyodbc.so. To do this we need to go to "/usr/lib/" and set up a symlink to libmyodbc.so

```
 cd /usr/lib/
 ln -s ./libmyodbc5w.so ./libmyodbc.so

```

## Databases

### Microsoft SQL Server 2000

/etc/odbc.ini

```
[server_name]
Driver      = FreeTDS
#Trace       = Yes
#TraceFile   = /tmp/odbc
Servername  = server_name
Database    = database_name

```

/etc/freetds/freetds.conf

```
[server_name]
host = 192.168.0.2 # Host name or IP address.
port = 1433 # Default port.
tds version = 7.1
client charset = UTF-8

```

SQL Server ODBC driver connection strings and [configuration guide](https://www.devart.com/odbc/sqlserver/docs/driver_configuration_and_conne.htm)

### Mariadb

Set up your data sources in "/etc/odbc.ini" (system wide) or "~/.odbc" (current user). If a data source is defined in both of these files, the one in your home directory take precedence.

```
[MySQL-test]
Description     = MySQL database test
Driver          = MySQL
Server          = localhost
Database        = test
Port            = 3306
Socket          = /var/run/mysqld/mysqld.sock
Option          =
Stmt            =

```

MariaDB ODBC driver connection strings and [configuration guide](https://www.devart.com/odbc/mysql/docs/using_odbc_driver.htm)

#### Create A Test Database

Create a new database "test". You can use one of the MySQL front-ends [mysql-gui-tools](https://aur.archlinux.org/packages/mysql-gui-tools/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mysql-gui-tools)]</sup> [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench) or the commandline.

```
mysqladmin -h localhost -u root -p create test

```

#### Testing the ODBC

To test the ODBC connection

```
isql MySQL-test

```

If the connection is established, you will see

```
+---------------------------------------+
| Connected!                            |
|                                       |
| sql-statement                         |
| help [tablename]                      |
| quit                                  |
|                                       |
+---------------------------------------+
SQL>

```

If you have a problem connecting then check the error message by running

```
isql MySQL-test -v

```

#### A Couple Useful Websites

[http://www.unixodbc.org/doc/OOoMySQL.pdf](http://www.unixodbc.org/doc/OOoMySQL.pdf)

This website got me going on ODBC with MySQL but left out some things that were necessary for me to get isql up and running. However this might be a good reference for the OpenOffice part.

[http://mail.easysoft.com/pipermail/unixodbc-support/2004-August/000111.html](http://mail.easysoft.com/pipermail/unixodbc-support/2004-August/000111.html)

To work around error messages this URL proved helpful so here it is as well.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Open_Database_Connectivity&oldid=392512](https://wiki.archlinux.org/index.php?title=Open_Database_Connectivity&oldid=392512)"