This document describes how to set up the [Habari](http://habariproject.org/en/) open source blogging engine on an Arch Linux system. It also tells how to enable your .htaccess file and required php modules that would prevent install errors from occurring.

## Contents

*   [1 Before you install](#Before_you_install)
*   [2 Installation](#Installation)
    *   [2.1 Step 1: Check PHP configuration](#Step_1:_Check_PHP_configuration)
    *   [2.2 Step 2: Prepare MySQL database](#Step_2:_Prepare_MySQL_database)
    *   [2.3 Step 3: Check Apache configuration](#Step_3:_Check_Apache_configuration)
    *   [2.4 Step 4: Prepare Habari directory](#Step_4:_Prepare_Habari_directory)
    *   [2.5 Step 5: Run the installer](#Step_5:_Run_the_installer)
*   [3 External links](#External_links)

## Before you install

Know that Habari is still alpha and there is no package in the main or AUR repositories. While some would claim that wordpress is better, wordpress is bloated and habari makes for an excellent alternative fit for efficient arch user.

**Note:** This howto assumes you have a LAMP already setup and ready to go. If you haven't set one up yet, see [LAMP](/index.php/LAMP "LAMP").

## Installation

### Step 1: Check PHP configuration

Make sure the following extensions are uncommented in `/etc/php/php.ini`:

```
extension=gd.so
extension=gettext.so
extension=iconv.so
extension=mhash.so
extension=pdo_mysql.so
extension=session.so
extension=xmlrpc.so
extension=zlib.so

```

### Step 2: Prepare MySQL database

You need to create a habari database for the blog to write stuff to. One can choose **habaridata** for the db name, **habari** for the username, and **habaripass** for the password. Assuming you've already accessed your mysql install and set a root password:

 `$ mysql -u root` 
```
mysql> CREATE DATABASE habaridata;
mysql> GRANT ALL PRIVILEGES ON habaridata.* TO 'habari'@'localhost' IDENTIFIED BY 'habaripass';
mysql> QUIT;

```

### Step 3: Check Apache configuration

Edit `/etc/httpd/conf/httpd.conf` and uncomment the following line:

```
LoadModule rewrite_module modules/mod_rewrite.so

```

Change all (just to be safe):

```
AllowOverride None

```

To:

```
AllowOverride FileInfo

```

Add (just to be safe):

```
# Habari .htaccess
<Directory /srv/http/blog>
     AllowOverride FileInfo
</Directory>

```

Restart Apache (`httpd.service`).

### Step 4: Prepare Habari directory

```
# cd /srv/http
# mkdir habari (or whatever you want to call the folder that'll house the habari install (e.g., blog, etc.))
# cd habari
# chmod o+w . (this is to make the installation go smoothly, so apache can write to the folder)
# touch .htaccess
# touch config.php
# chmod o+w .htaccess
# chmod o+w config.php
# svn checkout http://svn.habariproject.org/habari/trunk/htdocs .
# mkdir user/files
# chown http:http user/files
# chmod o+w user/files
# chown http:http user/cache
# chmod o+w user/cache

```

### Step 5: Run the installer

Head over to http://yourdomain.com/habari or whatever folder you called it. The habari installer should come up. This is fairly straightforward. Input the database information including the username and password. It is recommended to also have a prefix for the database, if you're mysql for other programs. The hostname will be localhost 99% of the time. You can enable all the plugins including the nifty wordpress importer if you want to migrate from that. The name of the blog can also be specified by changing the default **My Habari**. Click the install button at the very bottom and congratulations; you are now running Habari

## External links

*   Main Habari Install Resource: [http://wiki.habariproject.org/en/Installation](http://wiki.habariproject.org/en/Installation)
*   Habari Troubleshooting: [http://wiki.habariproject.org/en/Troubleshooting](http://wiki.habariproject.org/en/Troubleshooting)
*   For more info on mysql database preparation, see [https://help.ubuntu.com/community/PunBB](https://help.ubuntu.com/community/PunBB)
*   Habari Themes: [http://wiki.habariproject.org/en/Available_Themes](http://wiki.habariproject.org/en/Available_Themes)