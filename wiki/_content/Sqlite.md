# Sqlite

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From the [project home page](http://www.sqlite.org/):

_SQLite is a software library that implements a self-contained, serverless, zero-configuration, transactional SQL database engine. SQLite is the most widely deployed SQL database engine in the world. The source code for SQLite is in the public domain._

## Contents

*   [1 Features](#Features)
*   [2 Installation](#Installation)
*   [3 Using sqlite3 command line shell](#Using_sqlite3_command_line_shell)
    *   [3.1 Create a database](#Create_a_database)
    *   [3.2 Create table](#Create_table)
    *   [3.3 Insert data](#Insert_data)
    *   [3.4 Search database](#Search_database)
*   [4 Using sqlite in shell script](#Using_sqlite_in_shell_script)
*   [5 See also](#See_also)

## Features

From: [SQLite Features](http://www.sqlite.org/features.html)

*   Transactions are atomic, consistent, isolated, and durable even after system crashes and power failures.
*   Zero-configuration - no setup or administration needed.
*   Implements most of SQL92\.
*   A complete database is stored in a single cross-platform disk file.
*   Supports terabyte-sized databases and gigabyte-sized strings and blobs.
*   Small code footprint: less than 325KiB fully configured or less than 190KiB with optional features omitted.
*   Faster than popular client/server database engines for most common operations.
*   Simple, easy to use API.
*   Written in ANSI-C. TCL bindings included. Bindings for dozens of other languages available separately.
*   Well-commented source code with 100% branch test coverage.
*   Available as a single ANSI-C source-code file that you can easily drop into another project.
*   Self-contained: no external dependencies.
*   Cross-platform: Unix (Linux and Mac OS X), OS/2, and Windows (Win32 and WinCE) are supported out of the box. Easy to port to other systems.
*   Sources are in the public domain. Use for any purpose.
*   Comes with a standalone command-line interface (CLI) client that can be used to administer SQLite databases.

## Installation

[Install](/index.php/Pacman "Pacman") [sqlite](https://www.archlinux.org/packages/?name=sqlite) from the [official repositories](/index.php/Official_repositories "Official repositories").

Related packages are:

*   [sqlite-doc](https://www.archlinux.org/packages/?name=sqlite-doc) - most of the static HTML files that comprise this website, including all of the SQL Syntax and the C/C++ interface specs and other miscellaneous documentation
*   [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) - sqlite3 module for PHP (do not forget to enable it in /etc/php/php.ini)
*   [gambas3-gb-db-sqlite3](https://www.archlinux.org/packages/?name=gambas3-gb-db-sqlite3) - Gambas2 Sqlite3 database access component
*   [sqliteman](https://www.archlinux.org/packages/?name=sqliteman) - The best developer's and/or admin's GUI tool for Sqlite3 in the world

## Using sqlite3 command line shell

The SQLite library includes a simple command-line utility named sqlite3 that allows the user to manually enter and execute SQL commands against an SQLite database.

#### Create a database

```
sqlite3 _databasename_

```

#### Create table

```
sqlite> create table tblone(one varchar(10), two smallint);

```

#### Insert data

```
sqlite> insert into tblone values('helloworld',20);
sqlite> insert into tblone values('archlinux', 30);

```

#### Search database

```
sqlite> select * from tblone;
helloworld|20
archlinux|30

```

See the [sqlite docs](http://www.sqlite.org/sqlite.html).

## Using sqlite in shell script

See forum [post](https://bbs.archlinux.org/viewtopic.php?id=109802).

## See also

*   [SQLite homepage](http://www.sqlite.org)
*   [SQLite Hammer](http://www.squidoo.com/sqlitehammer)
*   [Using SQLite - Oreilly Book](http://oreilly.com/catalog/9780596521196)
*   [SQLite - Apress Book](http://www.amazon.com/Definitive-Guide-SQLite-Mike-Owens/dp/1590596730)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sqlite&oldid=409774](https://wiki.archlinux.org/index.php?title=Sqlite&oldid=409774)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Database management systems](/index.php/Category:Database_management_systems "Category:Database management systems")