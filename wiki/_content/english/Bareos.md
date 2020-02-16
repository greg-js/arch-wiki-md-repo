**Bareos** (**B**ackup **A**rchiving **Re**covery **O**pen **S**ourced) is a backup software, originally forked from the Bacula project. It is network-based, multi-client and very flexible with an architecture oriented towards scalability. Thus the learning curve might be considered somewhat steep. The project is backed by the commercial company Bareos GmbH & Co. KG, based in Germany.

The open-source project site is located at [http://www.bareos.org](http://www.bareos.org), the source code is hosted on Github [https://github.com/bareos/](https://github.com/bareos/)

## Installation

There is a group of packages in [AUR](/index.php/AUR "AUR") that will install the software, but there is some minor manual labour necessary to make it run. It is recommended to use Bareos with [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"), since use with [MariaDB](/index.php/MariaDB "MariaDB")/MySQL was deprecated with version 19.0.

[Install](/index.php/Install "Install") the requirements first:

*   [apache](https://www.archlinux.org/packages/?name=apache) Apache Webserver
*   [php-apache](https://www.archlinux.org/packages/?name=php-apache) Apache PHP module
*   [postgresql](https://www.archlinux.org/packages/?name=postgresql) PostgreSQL Database

Minimal configuration for [Apache](/index.php/Apache "Apache") and [PHP](/index.php/PHP "PHP"):

*   Follow the steps described in [Apache_HTTP_Server#Using_libphp](/index.php/Apache_HTTP_Server#Using_libphp "Apache HTTP Server")
*   You will also need to enable the `rewrite` module, to do this, modify `/etc/httpd/conf/httpd.conf` and uncomment: `LoadModule rewrite_module modules/mod_rewrite.so` 
*   Then enable the `postgresql` extension in PHP as listed in [PHP#PostgreSQL](/index.php/PHP#PostgreSQL "PHP")

Minimal configuration for [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")

*   Initialize the database by following [PostgreSQL#Initial_configuration](/index.php/PostgreSQL#Initial_configuration "PostgreSQL")

Make sure both [Systemd](/index.php/Systemd "Systemd") services are [enabled](/index.php/Enable "Enable") and [start](/index.php/Start "Start") them:

	`httpd.service` and `postgresql.service`

Install the packages from [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   [bareos-bconsole](https://aur.archlinux.org/packages/bareos-bconsole/)
*   [bareos-common](https://aur.archlinux.org/packages/bareos-common/)
*   [bareos-database-common](https://aur.archlinux.org/packages/bareos-database-common/)
*   [bareos-database-postgresql](https://aur.archlinux.org/packages/bareos-database-postgresql/)
*   [bareos-tools](https://aur.archlinux.org/packages/bareos-tools/)
*   [bareos-director](https://aur.archlinux.org/packages/bareos-director/)
*   [bareos-filedaemon](https://aur.archlinux.org/packages/bareos-filedaemon/)
*   [bareos-storage](https://aur.archlinux.org/packages/bareos-storage/)
*   [bareos-tools](https://aur.archlinux.org/packages/bareos-tools/)
*   [bareos-webui](https://aur.archlinux.org/packages/bareos-webui/)

## Configuration

These steps mostly follow the [Instructions](https://docs.bareos.org/IntroductionAndTutorial/InstallingBareos.html) from docs.bareos.org, and include some Arch-specifics.

Setup the Bareos database

	As user `postgres` run:
```
$ /usr/lib/bareos/scripts/create_bareos_database
$ /usr/lib/bareos/scripts/make_bareos_tables
$ /usr/lib/bareos/scripts/grant_bareos_privileges
```

Copy default config files to the `/etc/bareos/` directory

	As root, run these commands:
```
# cp -r /usr/share/bareos/config/* /etc/bareos/
# chown -R bareos:bareos /etc/bareos
```

Set the correct DB driver in the catalog config file

	edit `/etc/bareos/bareos-dir.d/catalog/MyCatalog.conf` and replace the line containing the placeholder with this line: `dbdriver = "postgresql"` 

The [Systemd](/index.php/Systemd "Systemd") services for Bareos can now be [enabled](/index.php/Enable "Enable") and [started](/index.php/Start "Start"):

	`bareos-dir.service`, `bareos-sd.service` and `bareos-fd.service`

### Configure Web-UI

Use the `bconsole` tool to add a user for the webui.

*   to start the interactive management shell, run: `$ bconsole` 
*   inside the shell, you get a `*` as prompt, where you can enter the following commands (replace `*secret*` with an actual password):
    ```
    *reload
    *configure add console name=admin password=*secret* profile=webui-admin tlsenable=false
    *quit
    ```

Configure Apache to include the config for the Bareos Web-UI

*   we need to fix a path in `/etc/httpd/conf.d/extra/bareos-webui.conf`, inside, replace the two lines:
    ```
    Alias /bareos-webui  /usr/share/bareos-webui
    # ...
    <Directory /usr/share/bareos-webui>
    ```

	with the correct path:
```
Alias /bareos-webui  /usr/share/webapps/bareos-webui
# ...
<Directory /usr/share/webapps/bareos-webui>
```

*   in the file `/etc/httpd/conf/httpd.conf` add the line: `Include conf.d/extra/bareos-webui.conf` 
*   [restart](/index.php/Restart "Restart") Apache `httpd.serive`

Now you can now login to Bareos Webui at `http://localhost/bareos-webui/` and login using the account you just created with `bconsole`.