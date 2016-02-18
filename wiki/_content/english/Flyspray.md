[Flyspray](http://www.flyspray.org/) is a bug tracking system written in PHP.

## Installation

[Install](/index.php/Install "Install") the [flyspray](https://www.archlinux.org/packages/?name=flyspray) package. Flyspray will essentially require a [LAMP](https://en.wikipedia.org/wiki/LAMP_(software_bundle) stack, so that in addition to [PHP](/index.php/PHP "PHP"), you will need an HTTP server such as [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server"), and an SQL server such as [MySQL](/index.php/MySQL "MySQL") or [PostgreSQL](/index.php/PostgreSQL "PostgreSQL"). See the [LAMP](/index.php/LAMP "LAMP") wiki article for more information on how to integrate these.

### Apache Setup

**Note:** You will need to have [Apache](/index.php/Apache "Apache") configured to run with [PHP](/index.php/PHP "PHP"). Check the [LAMP#PHP](/index.php/LAMP#PHP "LAMP") page for instructions. Make sure to enable the `mysqli.so` extension.

You will need to create a config file for apache to find your Flyspray install. Create the following file and edit it your favorite text editor:

 `# /etc/httpd/conf/extra/flyspray.conf` 
```
Alias /flyspray "/usr/share/webapps/flyspray"
<Directory "/usr/share/webapps/flyspray">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
	php_admin_value open_basedir "/srv/http/:/tmp/:/usr/share/webapps/flyspray"
</Directory>
```

You will then need to change the `.htaccess` file at `/usr/share/webapps/flyspray` from deny to allow otherwise Apache will not render it. You should now be able to navigate to the flyspray interface (e.g. `www.yourserver.org/flyspray`) and it will show a page of pre-installation checks. Any issues here should be resolved before continuing.

## See also

*   [Flyspray Official Website](http://www.flyspray.org/)