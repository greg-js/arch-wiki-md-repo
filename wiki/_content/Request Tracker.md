# Request Tracker

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Install the packages](#Install_the_packages)
    *   [1.2 Configure Apache](#Configure_Apache)
    *   [1.3 Create a MySQL database](#Create_a_MySQL_database)
    *   [1.4 Configure RT](#Configure_RT)
*   [2 Using RT](#Using_RT)
    *   [2.1 Tweaking RT_SiteConfig.pm](#Tweaking_RT_SiteConfig.pm)
    *   [2.2 Further Reading](#Further_Reading)

## Installation

This guide will help create a new RT (Request Tracker) server using [MySQL](/index.php/MySQL "MySQL"), [Apache](/index.php/Apache "Apache"), and mod_perl with a location of [http://localhost/rt](http://localhost/rt). RT also supports other database types, web servers (even as a daemon on it's own), Perl engines, and configurations that are not explained here (please consult the [appropriate RT documentation](https://github.com/bestpractical/rt/blob/stable/docs/web_deployment.pod)).

### Install the packages

Build and install the RT package from the AUR [here](https://aur.archlinux.org/packages.php?ID=53167). Be prepared to install a truckload of Perl dependencies: you'll need about 70 from the AUR and approximately 90 from the mirrors! An AUR wrapper will definitely help you out here. You will also want to install [Apache](/index.php/Apache "Apache") (also referred to as httpd) if it isn't on your server already.

### Configure Apache

Add this line to your LoadModule section in /etc/httpd/conf/httpd.conf:

```
LoadModule perl_module modules/mod_perl.so

```

Then, add this to the bottom of httpd.conf:

```
AddDefaultCharset UTF-8
DocumentRoot "/opt/rt4/share/html"

<Location "/rt">
  Order allow,deny
  Allow from all

  SetHandler modperl
  PerlResponseHandler Plack::Handler::Apache2
  PerlSetVar psgi_app /opt/rt4/sbin/rt-server
</Location>

<Directory "/opt/rt4/share/html">
  Order allow,deny
  Allow from all
</Directory>

<Perl>
  use Plack::Handler::Apache2;
  Plack::Handler::Apache2->preload("/opt/rt4/sbin/rt-server");
</Perl>

```

### Create a MySQL database

A [MySQL](/index.php/MySQL "MySQL") server needs to be installed and running. Create a database for RT by running the following as root (as it writes to /opt/rt4/etc/schema.mysql):

```
# /opt/rt4/sbin/rt-setup-database --action init

```

### Configure RT

Edit /opt/rt4/etc/RT_SiteConfig.pm (**not** RT_Config.pm) to make system-level changes to RT. RT_Config.pm is the "default" config file that can be used as a reference for what variables are legal in RT_SiteConfig.pm. It follows a perl syntax like so:

```
Set($_variable_, '_**setting'**_);

```

**At the very least, make two important changes.** _WebPath_ depicts where on the DocumentRoot RT is served (in our case, http://_ip_address_/rt) and is necessary for the CSS and images to load properly. _DatabasePassword_ is the [MySQL](/index.php/MySQL "MySQL") database password RT will use when connecting with the internal user (defaults to _rt_user_). Append this to RT_SiteConfig.pm:

```
Set($WebPath, '/rt');
Set($DatabasePassword, '_**your_password'**_);

```

After setting a database password, connect to the database ([like so](http://dev.mysql.com/tech-resources/articles/mysql_intro.html#SECTION0003000000)) and update the [MySQL](/index.php/MySQL "MySQL") user accordingly:

```
USE mysql;
UPDATE user SET password=PASSWORD('_**your_password'**_) WHERE user='rt_user';
FLUSH PRIVILEGES;

```

**Tip:** Since the internal user will barely, if ever, be used to manually log in to your [MySQL](/index.php/MySQL "MySQL") server, make the password nice and strong. There is a program in the mirrors called _pwgen_ for this. A good, random, 50-character password should work just fine for keeping the crackers out ;)

## Using RT

After completing the sections above, (re)start httpd and try connecting to [http://localhost/rt](http://localhost/rt)! The default admin credentials are root:password.

### Tweaking RT_SiteConfig.pm

Depending on your setup, RT may suggest altering your RT_SiteConfig.pm file to better suit your configuration by writing lines to /var/log/httpd/error_log. Please be advised that an ideal configuration will write no errors to error_log when loading pages in RT.

### Further Reading

Now that you've got RT up and running on your webserver, use it! See [Best Practical's online documentation](http://bestpractical.com/rt/docs.html) for configuring RT.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Request_Tracker&oldid=388054](https://wiki.archlinux.org/index.php?title=Request_Tracker&oldid=388054)"