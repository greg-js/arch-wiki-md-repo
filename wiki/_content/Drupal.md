# Drupal

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

_"Drupal is a free and open source content management system (CMS) and Content Management framework (CMF) written in PHP and distributed under the GNU General Public License."_ - [Wikipedia](http://en.wikipedia.org/wiki/Drupal)

This article describes how to setup Drupal and configure [Apache](/index.php/Apache "Apache"), [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [PHP](/index.php/PHP "PHP"), and [Postfix](/index.php/Postfix "Postfix") to work with it. It is assumed that you have some sort of [LAMP](/index.php/LAMP "LAMP") (Apache, MySQL, PHP) or LAPP (Apache, PostgreSQL, PHP) server already setup.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installing Postfix](#Installing_Postfix)
*   [2 Configuration](#Configuration)
    *   [2.1 PHP](#PHP)
    *   [2.2 Apache](#Apache)
    *   [2.3 Drupal](#Drupal)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Scheduling with Cron](#Scheduling_with_Cron)
    *   [3.2 Upload progress not enabled](#Upload_progress_not_enabled)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [drupal](https://www.archlinux.org/packages/?name=drupal) package.

### Installing Postfix

In order to send e-mails with Drupal, you will need to install [Postfix](/index.php/Postfix "Postfix"). Drupal uses e-mails for account verification, password recovery, etc. First install [postfix](https://www.archlinux.org/packages/?name=postfix).

1.  Edit Postfix configuration file `/etc/postfix/main.cf` as needed. All that you should have to do is change the hostnames under "Internet Host and Domain Names" `myhostname = hostname1`
2.  [Start](/index.php/Start "Start") `postfix.service`.
3.  Send a test e-mail to yourself: `mail myusername@localhost`. Enter a subject, some words in the body, then press `Ctrl+d` to exit and send the letter. Wait 10 seconds, and then type `mail` to check your mail. If you've gotten it, excellent.
4.  Make sure port 25 is fowarded if you have a router so that mails can be sent to the Internet at large
5.  Edit the file `/etc/php/php.ini`. Find the line that starts with, `;sendmail_path=""` and change it to `sendmail_path="/usr/sbin/sendmail -t -i"`
6.  Restart the Apache web server.

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

### Scheduling with Cron

Drupal recommends running cron jobs hourly. Cron can be executed from the browser by visiting [http://localhost/drupal/cron](http://localhost/drupal/cron). It is also possible to run cron via script by copying the appropriate file from the "scripts" folder into `/etc/cron.hourly` and making it executable.

### Upload progress not enabled

Upon successful installation you may see the following message in the Status Report:

 `Your server is capable of displaying file upload progress, but does not have the required libraries. It is recommended to install the PECL uploadprogress library (preferred) or to install APC.` 

First, install the [php-pear](https://www.archlinux.org/packages/?name=php-pear) package. Next, use the **pecl** command to automatically download, compile and install the library:

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
*   [LAMP (How to setup an Apache server)](/index.php/LAMP "LAMP")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Drupal&oldid=413731](https://wiki.archlinux.org/index.php?title=Drupal&oldid=413731)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")