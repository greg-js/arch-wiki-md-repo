# Drupal

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [LAMP](/index.php/LAMP "LAMP")
*   [LAPP](/index.php/LAPP "LAPP")
*   [SQLite](/index.php/SQLite "SQLite")
*   [MySQL](/index.php/MySQL "MySQL")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")
*   [Sendmail](/index.php/Sendmail "Sendmail")
*   [PostFix](/index.php/PostFix "PostFix")

_"Drupal is a free and open source content management system (CMS) and Content Management framework (CMF) written in PHP and distributed under the GNU General Public License."_ - [Wikipedia](http://en.wikipedia.org/wiki/Drupal)

This article describes how to setup Drupal and configure [Apache](/index.php/Apache "Apache"), [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [PHP](/index.php/PHP "PHP"), and [Postfix](/index.php/Postfix "Postfix") to work with it. It is assumed that you have some sort of [LAMP](/index.php/LAMP "LAMP") (Apache, MySQL, PHP) or LAPP (Apache, PostgreSQL, PHP) server already setup.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Drupal](#Drupal)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Sending Mail](#Sending_Mail)
    *   [3.2 Scheduling with Cron](#Scheduling_with_Cron)
    *   [3.3 Upload progress not enabled](#Upload_progress_not_enabled)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [drupal](https://www.archlinux.org/packages/?name=drupal) from the AUR.

## Configuration

### PHP

Edit `/etc/php/php.ini`:

*   Uncomment the `extension=gd.so` line.
*   Enable a PDO extension for your database. For MySQL, the line `extension=pdo_mysql.so` should be uncommented.

### Apache

Copy the example Apache configuration file:

```
# cp /etc/webapps/drupal/apache.example.conf /etc/httpd/conf/extra/drupal.conf

```

And include it at the bottom of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/drupal.conf

```

In `/etc/httpd/conf/httpd.conf`, also uncomment the `LoadModule rewrite_module modules/mod_rewrite.so` line.

### Drupal

Edit `/usr/share/webapps/drupal/.htaccess` and replace `Require all denied` by `Require all granted`.

Finally, [restart](/index.php/Daemons#Restarting "Daemons") Apache (`httpd.service`). You can now access the Drupal installation at [http://localhost/drupal](http://localhost/drupal) .

## Tips and tricks

### Sending Mail

Drupal needs a Sendmail-compatible MTA like [Sendmail](https://www.archlinux.org/packages/?name=Sendmail), [Postfix](https://www.archlinux.org/packages/?name=Postfix) or [Exim](https://www.archlinux.org/packages/?name=Exim) if you plan to send mail from your local setup. Alternatively there are multiple solutions to send mail via external mail servers through SMTP or other means like [SMTP](https://drupal.org/project/smtp) or [PHPMailer](https://drupal.org/project/phpmailer). Use the [search page](https://www.drupal.org/search/site/mail) to find more possibilities.

### Scheduling with Cron

Drupal recommends running cron jobs hourly. Cron can be executed from the browser by visiting [http://localhost/drupal/cron](http://localhost/drupal/cron). It is also possible to run cron via script by copying the appropriate file from the "scripts" folder into `/etc/cron.hourly` and making it executable.

### Upload progress not enabled

Upon successful installation you may see the following message in the Status Report:

 `Your server is capable of displaying file upload progress, but does not have the required libraries. It is recommended to install the PECL uploadprogress library (preferred) or to install APC.` 

First, install the [php-pear](https://aur.archlinux.org/packages/php-pear/)<sup><small>AUR</small></sup> package. Next, use the **pecl** command to automatically download, compile and install the library:

```
# pecl install uploadprogress

```

Finally, add to `/etc/php/php.ini`

```
extension=uploadprogress.so

```

Restart Apache.

## See also

*   [Official Drupal documentation](http://drupal.org/handbook)
*   [Simple guide to install Drupal on Xampp](http://drupal.org/node/307956)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Drupal&oldid=415735](https://wiki.archlinux.org/index.php?title=Drupal&oldid=415735)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")