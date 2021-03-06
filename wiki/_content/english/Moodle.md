Related articles

*   [MySQL](/index.php/MySQL "MySQL")
*   [LAMP](/index.php/LAMP "LAMP")

[Moodle](https://moodle.org/) is a free and open-source e-learning software platform, written in [PHP](/index.php/PHP "PHP").

This article describes how to set up the Moodle server.

## Contents

*   [1 Installation](#Installation)
*   [2 Preconfiguration](#Preconfiguration)
    *   [2.1 File access](#File_access)
    *   [2.2 Create the MoodleData Directory](#Create_the_MoodleData_Directory)
    *   [2.3 Configure PHP extension](#Configure_PHP_extension)
    *   [2.4 Restart Apache](#Restart_Apache)
    *   [2.5 Mariadb](#Mariadb)
*   [3 Installation](#Installation_2)

## Installation

[Installation quick guide](https://docs.moodle.org/en/Installation_quick_guide):

> You will need a working web server (e.g. [Apache](/index.php/Apache "Apache")), a database (e.g. [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")) and have [PHP](/index.php/PHP "PHP") configured.

There is also an AUR package [moodle](https://aur.archlinux.org/packages/moodle/) for the installation. Either you can use this way:

Download the most current version of Moodle from [http://download.moodle.org/](http://download.moodle.org/) - this installation was done with 2.3.1+, and there may be minor changes to the install routine in later versions.

Unzip it into `/srv/http`:

```
# tar xzvf moodle-latest-23.tgz -C /srv/http

```

Make it read/writeable by Apache:

```
# chown -R http:http /srv/http/moodle

```

## Preconfiguration

Some changes need to be made to the default setup so Moodle will work.

### File access

Add `/srv` to `/etc/php/php.ini`:

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/**:/srv/**

```

This allows PHP to access the `/srv/moodledata directory` (thanks to forum user "Ravenman") for this fix.

### Create the MoodleData Directory

This needs to be readable and writeable by Apache:

```
# mkdir /srv/moodledata
# chown http:http /srv/moodledata

```

### Configure PHP extension

Install [php-intl](https://www.archlinux.org/packages/?name=php-intl) and [php-gd](https://www.archlinux.org/packages/?name=php-gd) from the [official repositories](/index.php/Official_repositories "Official repositories").

Uncomment the following lines in `/etc/php/php.ini` (remove the semicolon from the start of the line):

```
extension=curl
extension=gd
extension=gettext
extension=iconv
extension=intl
extension=mysqli
extension=soap
extension=xmlrpc
extension=zip

```

### Restart Apache

You now need to [restart](/index.php/Restart "Restart") Apache's `httpd.service` to make these changes current. Note that if you get any errors while installing Moodle, and make subsequent changes, you will need to restart Apache after each set of changes.

### Mariadb

If you are using mariadb and the moodle installer complains about the wrong version of mysql edit config.php in /srv/http/moodle

```
$CFG->dbtype    = 'mariadb'; 
$CFG->dblibrary = 'native';

```

## Installation

Go to `[http://localhost/moodle/install.php](http://localhost/moodle/install.php)` - this starts the Moodle installer. There then follows a sequence of configuration screens, most of which should be left at the defaults.

*   Select the language

*   You should pass the first page of tests (PHP Settings). If not check you installed libGD, the most likely problem.

*   Leave the default locations as they are. An error here is likely to be a data directory problem - check the directory exists, that it has the right ownership and that open_basedir in /etc/php/php.ini is set correctly.

*   On the MySQL Screen, enter the user (root) and that user's password in the screen. If you get an error here, go to the test.php created when you set up the LAMP stack and check mysql is working, and also check the passwords.

*   On the Environment screen, you should pass all the tests - if not the errors give you a clue what is missing - an uninstalled program or a failure to uncomment one of the lines in /etc/php/php.ini

*   If you are English, you do not need to download language packs.

*   If the config.php has failed - probably because of lack of write access to the moodle subdirectory - the most likely reason is the ownership of the /srv/http/moodle structure which should be http:http - this was set earlier but you might have skipped that bit.

*   The remainder of the install should be automatic. It takes 2 or 3 minutes on my computer to set up all the SQL Databases and so on.

*   The final page allows you to set up the administrator user for Moodle. You need to enter a password, name and set the country as a bare minimum. *Don't* forget the password !

Happy Moodling !