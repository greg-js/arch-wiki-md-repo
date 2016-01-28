# Dotclear

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** The most important part - how to install it - is missing ... (Discuss in [Talk:Dotclear#](https://wiki.archlinux.org/index.php/Talk:Dotclear))

## Contents

*   [1 Introduction](#Introduction)
*   [2 Before You Install](#Before_You_Install)
*   [3 Installation](#Installation)
    *   [3.1 PHP configuration](#PHP_configuration)
    *   [3.2 Prepare MySQL Database](#Prepare_MySQL_Database)
    *   [3.3 Install dotclear](#Install_dotclear)

# Introduction

This document describes how to set up the dotclear open source blogging engine on an Arch Linux system.

# Before You Install

**Note:** This howto assumes you have a LAMP already setup and ready to go. If you haven't set one up yet, see [LAMP](/index.php/LAMP "LAMP").

# Installation

## PHP configuration

Make sure the following extensions are uncommented in `/etc/php/php.ini`:

```
extension=gd.so
extension=gettext.so
extension=iconv.so
extension=mysqli.so

```

## Prepare MySQL Database

You need to create a dotclear database for the blog to write stuff to. One can choose **dotclear2** for the db name, **dotclear** for the username, and **dotclearpass** for the password. Assuming you've already accessed your mysql install and set a root password:

 `$ mysql -u root -p` 

```
mysql> CREATE DATABASE dotclear2;
mysql> GRANT ALL PRIVILEGES ON dotclear2.* TO "dotclear2"@"localhost" IDENTIFIED BY "dotclearpass";
mysql> FLUSH PRIVILEGES;
mysql> QUIT;
```

## Install dotclear

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dotclear&oldid=411120](https://wiki.archlinux.org/index.php?title=Dotclear&oldid=411120)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")

Hidden category:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")