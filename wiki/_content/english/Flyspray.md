Related articles

*   [LAMP](/index.php/LAMP "LAMP")

[Flyspray](http://www.flyspray.org/) is a bug tracking system written in [PHP](/index.php/PHP "PHP"). FlySpray is notably used by Arch Linux itself (bugs.archlinux.org).

## Status in Arch Linux

Issue [FS#24999](https://bugs.archlinux.org/task/24999) was in progress to migrate away from FlySpray to Bugzilla. Unfortunately the main developer abandoned the project due to lack of time/interest.

## Installation

[Install](/index.php/Install "Install") the [flyspray](https://www.archlinux.org/packages/?name=flyspray) package. Flyspray requires a web server such as [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") with [PHP](/index.php/PHP "PHP"), and an SQL server such as [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL").

### Apache Setup

**Note:** You will need to have [Apache](/index.php/Apache "Apache") configured to run with [PHP](/index.php/PHP "PHP"). Check [Apache#PHP](/index.php/Apache#PHP "Apache") for instructions. Make sure to uncomment `extension=mysqli` in `/etc/php/php.ini`.

You will need to create a config file for apache to find your Flyspray install. Create the following file:

 `/etc/httpd/conf/extra/flyspray.conf` 
```
Alias /flyspray "/usr/share/webapps/flyspray"
<Directory "/usr/share/webapps/flyspray">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
	php_admin_value open_basedir "/srv/http/:/tmp/:/usr/share/webapps/flyspray"
</Directory>
```

You will then need to edit `/etc/webapps/flyspray/.htaccess` and change `deny from all` to `allow from all`. You should now be able to navigate to the flyspray interface (e.g. `[http://localhost/flyspray](http://localhost/flyspray)`) and it will show a page of pre-installation checks. Any issues here should be resolved before continuing.