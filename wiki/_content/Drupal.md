# Drupal

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

_"Drupal is a free and open source content management system (CMS) and Content Management framework (CMF) written in PHP and distributed under the GNU General Public License."_ - [Wikipedia](http://en.wikipedia.org/wiki/Drupal)

This article describes how to setup Drupal and configure [Apache](/index.php/Apache "Apache"), [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), [PHP](/index.php/PHP "PHP"), and [Postfix](/index.php/Postfix "Postfix") to work with it. It is assumed that you have some sort of [LAMP](/index.php/LAMP "LAMP") (Apache, MySQL, PHP) or LAPP (Apache, PostgreSQL, PHP) server already setup.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Arch repositories](#Arch_repositories)
    *   [1.2 Manual install](#Manual_install)
    *   [1.3 Installing GD](#Installing_GD)
    *   [1.4 Installing Postfix](#Installing_Postfix)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Scheduling with Cron](#Scheduling_with_Cron)
    *   [2.2 Xampp Compatibility](#Xampp_Compatibility)
    *   [2.3 Upload progress not enabled](#Upload_progress_not_enabled)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Browser shows the actual PHP code when visiting localhost](#Browser_shows_the_actual_PHP_code_when_visiting_localhost)
    *   [3.2 Setup page is not the initial page when accessing localhost](#Setup_page_is_not_the_initial_page_when_accessing_localhost)
    *   [3.3 Setup page does not start and shows HTTP ERROR 500](#Setup_page_does_not_start_and_shows_HTTP_ERROR_500)
*   [4 See also](#See_also)

## Installation

### Arch repositories

[Install](/index.php/Pacman "Pacman") the [drupal](https://www.archlinux.org/packages/?name=drupal) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Edit `/etc/php/php.ini`:

*   If PHP version is less than 5.2.0, Find the line with `;extension=json.so` and uncomment it by removing the ";" from the beginning of the line if necessary. If no such line is found, add it to the `[PHP]` section of the file.
*   For Drupal 7, enable a PDO extension for your database. For MySQL, the line `extension=pdo_mysql.so` should be uncommented.
*   Find the line beginning with `open_basedir =`. Add the Drupal install directories, `/usr/share/webapps/drupal/` and `/var/lib/drupal/`. `/srv/http/` can be removed if you do not intend to use it.

Edit `/etc/httpd/conf/httpd.conf`:

*   If your webserver is dedicated to Drupal, find the line `DocumentRoot "/srv/http"` and change it to the Drupal install directory, _i.e._ `DocumentRoot "/usr/share/webapps/drupal"`, then find the section that starts with "`<Directory "/srv/http">`" and change `/srv/http` to the Drupal install directory, `/usr/share/webapps/drupal`. In the same section, make sure it includes a line "`AllowOverride All`" to enable the clean URL's.
*   If you are using Apache Virtual Hosts, see [Apache#Virtual hosts](/index.php/Apache#Virtual_hosts "Apache").

Finally comment out the `deny from all` line of the `/usr/share/webapps/drupal/.htaccess` file to enable httpd access and [restart](/index.php/Daemons#Restarting "Daemons") Apache (httpd). Note that the actual wording of the line might also be `Require all denied`.

### Manual install

Download the latest package from [http://drupal.org](http://drupal.org) and extract it. Move the folders to Apache's htdocs folder. Open a web browser, and navigate to [localhost localhost]. Follow the on-screen instructions.

### Installing GD

You may need the GD library for your Drupal installation. First install the [php-gd](https://www.archlinux.org/packages/?name=php-gd) package. Edit `/etc/php/php.ini`. Find the line with `;extension=gd.so` and uncomment it by removing the ";". If no such line is found, add it to the `[PHP]` section of the file. [Restart](/index.php/Daemons#Restarting "Daemons") Apache (httpd).

### Installing Postfix

In order to send e-mails with Drupal, you will need to install [Postfix](/index.php/Postfix "Postfix"). Drupal uses e-mails for account verification, password recovery, etc. First install [postfix](https://www.archlinux.org/packages/?name=postfix).

1.  Edit Postfix configuration file `/etc/postfix/main.cf` as needed. All that you should have to do is change the hostnames under "Internet Host and Domain Names" `myhostname = hostname1`
2.  Start the Postfix service: `# systemctl start postfix`.
3.  Send a test e-mail to yourself: `mail myusername@localhost`. Enter a subject, some words in the body, then press `Ctrl+d` to exit and send the letter. Wait 10 seconds, and then type `mail` to check your mail. If you've gotten it, excellent.
4.  Make sure port 25 is fowarded if you have a router so that mails can be sent to the Internet at large
5.  Edit the file `/etc/php/php.ini`. Find the line that starts with, `;sendmail_path=""` and change it to `sendmail_path="/usr/sbin/sendmail -t -i"`
6.  Restart the Apache web server.

## Tips and tricks

### Scheduling with Cron

Drupal recommends running cron jobs hourly. Cron can be executed from the browser by visiting [localhost/cron localhost/cron]. It is also possible to run cron via script by copying the appropriate file from the "scripts" folder into `/etc/cron.hourly` and making it executable.

### Xampp Compatibility

The 5.x and 6.x series of Drupal do not support PHP 5.3, and as a result are incompatible with the latest release of [Xampp](/index.php/Xampp "Xampp"). Currently, the last Drupal-compatible version of Xampp is 1.7.1.

Note: Xampp's PHP memory limit currently defaults to 8MB. Also, Xampp ignores php.ini files in the Drupal directory. To fix this:

1.  Edit Xampp's configuration file `/opt/lampp/etc/php.ini` using your favorite editor.
2.  Search for the "memory_limit" line, and replace it with an appropriate value. Most Drupal installations just need 32MB, but sites with a lot of modules may need 100MB or more.
3.  Restart Xampp: `/opt/lampp/lampp restart`

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

## Troubleshooting

### Browser shows the actual PHP code when visiting localhost

You do not have [php-apache](https://www.archlinux.org/packages/?name=php-apache) installed.

Then, enable the PHP module in `/etc/httpd/conf/httpd.conf` by adding the following lines in the appropriate sections:

```
LoadModule php5_module modules/libphp5.so
Include conf/extra/php5_module.conf

```

If, when starting httpd, you get the following error:

```
httpd: Could not reliably determine the server's fully qualified domain name, using 127.0.0.1 for ServerName

```

You should edit `/etc/httpd/conf/httpd.conf`. In that file find the line that looks similar to

```
#ServerName www.example.com:80

```

Uncomment it (remove # from the front) and adjust the address as needed. Restart httpd:

```
# systemctl restart httpd

```

### Setup page is not the initial page when accessing localhost

In this situation, you should navigate in your `/srv` directory and look for the `drupal` folder (most probably it will be in the `http` directory). Then edit `/etc/httpd/conf/httpd.conf`. and look for a line starting with `DocumentRoot` and change the path with that folder's path (for example `DocumentRoot "/srv/http/drupal"`) and also find another line starting with `<Directory` and set the same path there as well. Restart httpd.

### Setup page does not start and shows HTTP ERROR 500

This may be because Drupal needs the `json.so` extension to be activated in your `/etc/php/php.ini`. Just uncomment in `/etc/php/php.ini` the line:

```
;extension=json.so

```

Restart httpd service.

See [this link](http://drupal.org/node/1018824) for info.

This can be caused because Drupal doesn't have access to its .htacccess, to enable this make sure that the directive AllowOverride All is set in your `/etc/httpd/conf/httpd.conf` or for your respective user directory.

See [this link](https://httpd.apache.org/docs/current/mod/core.html#allowoverride) for info.

## See also

*   [Official Drupal documentation](http://drupal.org/handbook)
*   [Simple guide to install Drupal on Xampp](http://drupal.org/node/307956)
*   [LAMP (How to setup an Apache server)](/index.php/LAMP "LAMP")

Retrieved from "[https://wiki.archlinux.org/index.php?title=Drupal&oldid=409161](https://wiki.archlinux.org/index.php?title=Drupal&oldid=409161)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")