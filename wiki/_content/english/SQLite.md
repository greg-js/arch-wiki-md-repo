From the [project home page](http://www.sqlite.org/):

	SQLite is a software library that implements a self-contained, serverless, zero-configuration, transactional SQL database engine. SQLite is the most widely deployed SQL database engine in the world. The source code for SQLite is in the public domain.

## Contents

*   [1 Installation](#Installation)
*   [2 Using sqlite3 command line shell](#Using_sqlite3_command_line_shell)
    *   [2.1 Create a database](#Create_a_database)
    *   [2.2 Create table](#Create_table)
    *   [2.3 Insert data](#Insert_data)
    *   [2.4 Search database](#Search_database)
*   [3 Graphical tools](#Graphical_tools)
*   [4 Using sqlite in shell script](#Using_sqlite_in_shell_script)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [sqlite](https://www.archlinux.org/packages/?name=sqlite) package.

Related packages are:

*   [sqlite-doc](https://www.archlinux.org/packages/?name=sqlite-doc) - most of the static HTML files that comprise this website, including all of the SQL Syntax and the C/C++ interface specs and other miscellaneous documentation
*   [php-sqlite](https://www.archlinux.org/packages/?name=php-sqlite) - sqlite3 module for PHP (do not forget to enable it in `/etc/php/php.ini`)
*   [gambas3-gb-db-sqlite3](https://www.archlinux.org/packages/?name=gambas3-gb-db-sqlite3) - Gambas2 Sqlite3 database access component
*   [sqliteman](https://aur.archlinux.org/packages/sqliteman/) - Developer and/or admin GUI tool for Sqlite3
*   [sqlitebrowser](https://www.archlinux.org/packages/?name=sqlitebrowser) - DB Browser for SQLite is a high quality, visual, open source tool to create, design, and edit database files compatible with SQLite.

## Using sqlite3 command line shell

The SQLite library includes a simple command-line utility named sqlite3 that allows the user to manually enter and execute SQL commands against an SQLite database.

#### Create a database

```
$ sqlite3 *databasename*

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

## Graphical tools

*   **DB Browser for SQLite** — High quality, visual, open source tool to create, design, and edit database files compatible with SQLite.

	[https://sqlitebrowser.org/](https://sqlitebrowser.org/) || [sqlitebrowser](https://www.archlinux.org/packages/?name=sqlitebrowser)

For more, see [List of applications/Documents#Database tools](/index.php/List_of_applications/Documents#Database_tools "List of applications/Documents").

## Using sqlite in shell script

See forum [post](https://bbs.archlinux.org/viewtopic.php?id=109802).

## See also

*   [SQLite homepage](http://www.sqlite.org)
*   [SQLite Hammer](http://www.squidoo.com/sqlitehammer)
*   [Using SQLite - Oreilly Book](http://oreilly.com/catalog/9780596521196)
*   [SQLite - Apress Book](http://www.amazon.com/Definitive-Guide-SQLite-Mike-Owens/dp/1590596730)