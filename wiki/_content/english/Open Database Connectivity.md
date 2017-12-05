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
        *   [2.2.3 Create a symbolic link](#Create_a_symbolic_link)
*   [3 Databases](#Databases)
    *   [3.1 Microsoft SQL Server 2000](#Microsoft_SQL_Server_2000)
    *   [3.2 Mariadb](#Mariadb)
        *   [3.2.1 Create a test database](#Create_a_test_database)
        *   [3.2.2 Testing the ODBC](#Testing_the_ODBC)
        *   [3.2.3 A couple useful websites](#A_couple_useful_websites)
    *   [3.3 Virtuoso / SPARQL](#Virtuoso_.2F_SPARQL)

## ODBC engines

You have two options to chose from: [unixODBC](http://www.unixodbc.org/) and [iODBC](https://en.wikipedia.org/wiki/IODBC "wikipedia:IODBC"). Apparently unixODBC is more widely supported. This document shows how to set up unixODBC. First to access your database on your localhost and then extends the steps to configure MySQL to allow remote access through ODBC.

Additionally you can choose from various [Devart ODBC drivers](https://www.devart.com/odbc/) for SQL Server, Oracle, MySQL, SQLite, Firebird, PostgreSQL, Interbase.

### Installation

[Install](/index.php/Install "Install") the [unixodbc](https://www.archlinux.org/packages/?name=unixodbc) package.

### Configuration

Driver are declared in `/etc/odbcinst.ini`, and connections in `/etc/odbc.ini`. More instruction at each driver section.

## Drivers

### FreeTDS

**FreeTDS** is a set of libraries for Unix and Linux that allows your programs to natively talk to Microsoft SQL Server and Sybase databases. Technically speaking, FreeTDS is an open source implementation of the TDS (Tabular Data Stream) protocol used by these databases for their own clients.

#### Installation

[Install](/index.php/Install "Install") the [freetds](https://www.archlinux.org/packages/?name=freetds) package.

#### Configuration

 `/etc/odbcinst.ini` 
```
[FreeTDS]
Driver          = /usr/lib/libtdsodbc.so
UsageCount      = 1

```

The configuration file of FreeTDS itself is `/etc/freetds/freetds.conf`.

### Myodbc

Myodbc is ODBC driver/connector for mariadb.

#### Installation

Install the [myodbc](https://aur.archlinux.org/packages/myodbc/) package.

#### Configuration

Starting with `odbcinst.ini`, which lists all installed drivers.

 `/etc/odbcinst.ini` 
```
[MySQL]
Description     = ODBC Driver for MySQL
Driver          = /usr/lib/libmyodbc.so
Setup           = /usr/lib/libodbcmyS.so
FileUsage       = 1

```

#### Create a symbolic link

Next we need to create a symlink for `libmyodbc.so`. To do this we need to go to `/usr/lib/` and set up a symlink to `libmyodbc.so`

```
# cd /usr/lib/
# ln -s ./libmyodbc5w.so ./libmyodbc.so

```

## Databases

### Microsoft SQL Server 2000

 `/etc/odbc.ini` 
```
[server_name]
Driver      = FreeTDS
#Trace       = Yes
#TraceFile   = /tmp/odbc
Servername  = server_name
Database    = database_name

```
 `/etc/freetds/freetds.conf` 
```
[server_name]
host = 192.168.0.2 # Host name or IP address.
port = 1433 # Default port.
tds version = 7.1
client charset = UTF-8

```

SQL Server ODBC driver connection strings and [configuration guide](https://www.devart.com/odbc/sqlserver/docs/driver_configuration_and_conne.htm)

### Mariadb

Set up your data sources in `/etc/odbc.ini` (system wide) or `~/.odbc` (current user). If a data source is defined in both of these files, the one in your home directory take precedence.

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

#### Create a test database

Create a new database "test". You can use one of the MySQL front-ends such as [mysql-workbench](https://www.archlinux.org/packages/?name=mysql-workbench), or the command-line *mysqladmin* command:

```
$ mysqladmin -h localhost -u root -p create test

```

#### Testing the ODBC

To test the ODBC connection

```
$ isql MySQL-test

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
$ isql MySQL-test -v

```

#### A couple useful websites

[http://www.unixodbc.org/doc/OOoMySQL.pdf](http://www.unixodbc.org/doc/OOoMySQL.pdf)

This website got me going on ODBC with MySQL but left out some things that were necessary for me to get isql up and running. However this might be a good reference for the OpenOffice part.

[http://mail.easysoft.com/pipermail/unixodbc-support/2004-August/000111.html](http://mail.easysoft.com/pipermail/unixodbc-support/2004-August/000111.html)

To work around error messages this URL proved helpful so here it is as well.

### Virtuoso / SPARQL

 `/etc/odbc.ini` 
```
[ODBC Data Sources]
VOS = Virtuoso

[VOS]
Driver = virtuoso-odbc
Description = Virtuoso Open-Source Edition
Address = localhost:1111

```
 `/etc/odbcinst.ini` 
```
[virtuoso-odbc]
Driver = /usr/lib/virtodbc.so

```

Opening a connection using the default credentials (username: "dba", password: "dba"):

```
$ isql VOS dba dba

```