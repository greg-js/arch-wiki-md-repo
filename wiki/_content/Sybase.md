# Sybase

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Sybase#](https://wiki.archlinux.org/index.php/Talk:Sybase))

Sybase is a multi-threaded, multi-user SQL database. For more information about features, see the [official homepage](http://www.mysql.com).

## Contents

*   [1 Install Sybase Client](#Install_Sybase_Client)
*   [2 Install command line client tool](#Install_command_line_client_tool)
*   [3 Install Sybase Server](#Install_Sybase_Server)
*   [4 Configuration](#Configuration)
    *   [4.1 Enable remote access](#Enable_remote_access)
*   [5 Upgrading](#Upgrading)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 Install Sybase python binding](#Install_Sybase_python_binding)

## Install Sybase Client

For those user do not want to install sybase server, it could install the freetds package:

```
# pacman -S freetds

```

After installing freetds you should edit the config file as root:

```
# vi /etc/freetds/freetds.conf

```

## Install command line client tool

[sqsh](https://aur.archlinux.org/packages/sqsh/)<sup><small>AUR</small></sup> is in the [AUR](/index.php/AUR "AUR").

## Install Sybase Server

## Configuration

### Enable remote access

## Upgrading

## Troubleshooting

### Install Sybase python binding

[Download driver here [http://python-sybase.sourceforge.net/](http://python-sybase.sourceforge.net/)] (v0.39 is workable)

for sybase ocs installed

```
python setup.py install

```

for use freetds

```
root# SYBASE=/usr SYBASE_OCS= CFLAGS="-DHAVE_FREETDS" python setup.py install

```

Sample Code

```
con=Sybase.connect('DSN','USER','PASS','DB',locking=0)
c=con.cursor()
c.execute('select count(*) from TABLE')
c.fetchone()

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Sybase&oldid=277286](https://wiki.archlinux.org/index.php?title=Sybase&oldid=277286)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Database management systems](/index.php/Category:Database_management_systems "Category:Database management systems")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")