From the [project web page](http://munin-monitoring.org/):

	_Munin_ the monitoring tool surveys all your computers and remembers what it saw. It presents all the information in graphs through a web interface. Its emphasis is on plug and play capabilities. After completing a installation a high number of monitoring plugins will be playing with no more effort.

	Using Munin you can easily monitor the performance of your computers, networks, SANs, applications, weather measurements and whatever comes to mind. It makes it easy to determine "what's different today" when a performance problem crops up. It makes it easy to see how you're doing capacity-wise on any resources.

	Munin uses the excellent [RRDTool](http://oss.oetiker.ch/rrdtool/) (written by Tobi Oetiker) and the framework is written in Perl, while plugins may be written in any language. Munin has a master/node architecture in which the master connects to all the nodes at regular intervals and asks them for data. It then stores the data in RRD files, and (if needed) updates the graphs. One of the main goals has been ease of creating new plugins (graphs). [[1]](http://munin-monitoring.org/)

Simply put, Munin allows you to make graphs about system statistics. You can check out University of Oslo's [Munin install](http://munin.ping.uio.no/) to see some examples of what it can do.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 munin and munin-node](#munin_and_munin-node)
    *   [1.2 Optional web server](#Optional_web_server)
    *   [1.3 IPv6](#IPv6)
*   [2 Configuration](#Configuration)
    *   [2.1 Daemon](#Daemon)
    *   [2.2 Plugins](#Plugins)
    *   [2.3 Directories](#Directories)
    *   [2.4 Customization](#Customization)
    *   [2.5 Cron](#Cron)
    *   [2.6 systemd timer](#systemd_timer)
    *   [2.7 Permissions](#Permissions)
*   [3 Testing](#Testing)
*   [4 Plugins](#Plugins_2)
    *   [4.1 Adding](#Adding)
    *   [4.2 Removing](#Removing)
    *   [4.3 Debugging](#Debugging)
*   [5 Apache VirtualHost examples](#Apache_VirtualHost_examples)
    *   [5.1 Basic static html](#Basic_static_html)
    *   [5.2 Static html with DynaZoom feature](#Static_html_with_DynaZoom_feature)
    *   [5.3 Full dynamic](#Full_dynamic)
*   [6 Tips and Tricks](#Tips_and_Tricks)
    *   [6.1 MySQL](#MySQL)
    *   [6.2 S.M.A.R.T.](#S.M.A.R.T.)
    *   [6.3 lm_sensors](#lm_sensors)

## Installation

_Munin_ relies on a client-server model. The client is _munin-node_, and the server is _munin_ (referred as to "munin-master" in the documentation).

You will only need to install _munin_ on a single machine, but _munin-node_ will need to be installed on all machines you wish to monitor. This article will focus on a single-machine installation. Further documentation may be found on the [Munin documentation wiki](http://munin-monitoring.org/wiki/Documentation).

### munin and munin-node

[Install](/index.php/Install "Install") the [munin](https://www.archlinux.org/packages/?name=munin) (munin master) and [munin-node](https://www.archlinux.org/packages/?name=munin-node) packages.

### Optional web server

The following guide sets up Munin to generate static HTML and graph images and write them in a directory of your choosing. You can view these generated files locally with any web browser. If you want to view the generated files from a remote machine, then you want to install and configure one of the following web servers:

*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Nginx](/index.php/Nginx "Nginx")

Or one of the other servers found in the [web server](/index.php/Category:Web_server "Category:Web server") category.

### IPv6

For IPv6 support on _munin-node_, using:

 `/etc/munin/munin-node.conf` 

```
host :::1

```

Install:

*   [perl-socket6](https://www.archlinux.org/packages/?name=perl-socket6)
*   [perl-io-socket-inet6](https://www.archlinux.org/packages/?name=perl-io-socket-inet6)

## Configuration

### Daemon

[Enable](/index.php/Enable "Enable") the `munin.service`, so _Munin_ will be started at boot.

### Plugins

Run `munin-node-configure` with the `--suggest` option to have Munin suggest plugins it thinks will work on your installation:

```
# munin-node-configure --suggest

```

If there is a suggestion for a plugin you want to use, follow that suggestion and run the command again. When you are satisfied with the plugins suggested by `munin-node-configure`, run it with the `--shell` option to have the plugins configured:

```
# munin-node-configure --shell | sh

```

### Directories

Create a directory where the _munin-master_ will write the generated HTML and graph images. The munin user must have write permission to this directory.

The following example uses `/srv/http/munin`, so the generated output can be viewed at [http://localhost/munin/](http://localhost/munin/), provided that a web server is installed and running:

```
# mkdir /srv/http/munin
# chown munin:munin /srv/http/munin

```

Uncomment the `htmldir` entry in `/etc/munin/munin.conf` and change it to the directory created in the previous step:

```
htmldir /srv/http/munin

```

### Customization

Before running munin, you might want to setup the hostname of your system. In `/etc/munin/munin.conf`, the default hostname is `myhostname`. This can be altered to any preferred hostname. The hostname will be used to group and name the `.rrd` files in `/var/lib/munin` and further, used to group the html files and graphs in your selected _munin-master_ directory.

### Cron

Run the following to have Munin collect data and update the generated HTML and graph images every 5 minutes:

```
# crontab /etc/munin/munin-cron-entry -u munin

```

Configure the email server to send mails to the _munin_ user. If using postfix, add the following:

 `/etc/postfix/aliases` 

```
munin:    root

```

And run:

```
# newaliases

```

### systemd timer

Instead of a cron job a systemd timer can be used.

This needs a service unit configuration:

 `/etc/systemd/system/munin-cron.service` 

```
[Unit]
Description=Survey monitored computers
After=network.target

[Service]
User=munin
ExecStart=/usr/bin/munin-cron
```

And a timer unit configuration:

 `/etc/systemd/system/munin-cron.timer` 

```
[Unit]
Description=Survey monitored computers every five minutes

[Timer]
OnCalendar=*-*-* *:00/5:00

[Install]
WantedBy=multi-user.target
```

Now, [reload](/index.php/Reload "Reload") systemd configuration, [start](/index.php/Start "Start") `munin-cron.timer` and verify that everything is working:

```
$ journalctl --unit munin-cron.service
$ less /var/log/munin/munin-update.log

```

Finally, [enable](/index.php/Enable "Enable") `munin-cron.timer`.

### Permissions

Because many plugins read log files, it is useful to [add](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") `munin` user into `log` group:

When `graph_strategy cgi` is enabled in `/etc/munin/munin.conf` ensure the directory `/var/lib/munin/cgi-tmp` is owned by user and group `munin` so that the `/usr/share/munin/cgi/munin-cgi-graph` script is able to write the png files to this directory.

```
# chown munin: /var/lib/munin/cgi-tmp

```

## Testing

Munin should be able to run now. To make sure everything works, [start](/index.php/Start "Start") `munin-node.service`.

Change the user to `munin` and open the shell with `-s`/`--shell` (this needs to be done from root shell, since `munin` doesn't have a password):

```
# su -s /bin/bash munin

```

Then run `munin-cron` manually to generate the HTML and graph images:

```
munin> munin-cron

```

And finally test the interface by pointing your browser to the output directory or [http://localhost/munin/](http://localhost/munin/).

**Note:** It might take a while for the graphs to have data, so be patient. Wait for about 30 minutes to an hour.

## Plugins

There are many Munin plugins out there just waiting to be installed. The [MuninExchange](http://muninexchange.projects.linpro.no/) is an excellent place to start looking, and if you cannot find a plugin that does what you want it is easy to write your own. Have a look at [HowToWritePlugins](http://munin-monitoring.org/wiki/HowToWritePlugins) at the Munin documentation wiki to learn how.

### Adding

Basically all plugins are added in the following manner (although there are exceptions, review each plugin!):

Download a plugin, then copy or move it to `/usr/lib/munin/plugins`:

```
# cp _plugin_ /usr/lib/munin/plugins/

```

Then link the plugin to `/etc/munin/plugins`:

```
# ln -s /usr/lib/munin/plugins/_plugin_ /etc/munin/plugins/

```

**Note:** Some plugins - known as wildcard plugins - can be used with multiple devices at once by linking them with different names. These plugins end with an underscore and are linked as `<plugin>_<device>` to be used on `<device>`. See the `if_` plugin for an example.

Now test your plugin. You do not need to use the full path to the plugin, `munin-run` should be able to figure it out:

```
# munin-run _plugin_

```

And [restart](/index.php/Restart "Restart") `munin-node.servce`. Finally, refresh the web page.

### Removing

If you want to remove a plugin, simply delete the linked file in `/etc/munin/plugins` - there is no need to remove the plugin from `/usr/lib/munin/plugins`.

```
# rm /etc/munin/plugins/_plugin_

```

### Debugging

If you come across a plugin that is not working as expected (for example giving you no output at all) it might be interesting to run it directly. Fortunately there is a way to do this. Following the instructions until here, you will for example notice, that the plugin `apache_accesses` gives no output at all, when enabled. In order to run the plugin directly:

```
# munin-run apache_accesses

```

The following error:

```
LWP::UserAgent not found at /etc/munin/plugins/apache_accesses line 86.

```

indicates that a [perl](/index.php?title=Perl&action=edit&redlink=1 "Perl (page does not exist)") function could not be found. To resolve the problem, [install](/index.php/Install "Install") the missing library, in this case, [perl-libwww](https://www.archlinux.org/packages/?name=perl-libwww).

## Apache VirtualHost examples

Based on information found here:

*   [http://guide.munin-monitoring.org/en/stable-2.0/example/webserver/apache-virtualhost.html](http://guide.munin-monitoring.org/en/stable-2.0/example/webserver/apache-virtualhost.html)
*   [http://munin-monitoring.org/wiki/MuninConfigurationMasterCGI](http://munin-monitoring.org/wiki/MuninConfigurationMasterCGI)

In the next major release of Munin, things will be much simpler. Check it out:

*   [http://guide.munin-monitoring.org/en/latest/example/webserver/apache-virtualhost.html](http://guide.munin-monitoring.org/en/latest/example/webserver/apache-virtualhost.html)

### Basic static html

```
<VirtualHost *:80>
    ServerName localhost
    ServerAdmin  root@localhost

    DocumentRoot /srv/http/munin

    ErrorLog /var/log/httpd/munin-error.log
    CustomLog /var/log/httpd/munin-access.log combined
</VirtualHost>

```

### Static html with DynaZoom feature

Install [perl-cgi-fast](https://www.archlinux.org/packages/?name=perl-cgi-fast).

You must enable one of these:

*   **mod_cgid** (or **mod_cgi** if using mpm_prefork_module) by uncommenting the line in httpd.conf.
*   Or install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) and add "**LoadModule mod_fcgid modules/mod_fcgid.so**" in httpd.conf.

```
<VirtualHost *:80>
    ServerName localhost
    ServerAdmin  root@localhost

    DocumentRoot /srv/http/munin

    ErrorLog /var/log/httpd/munin-error.log
    CustomLog /var/log/httpd/munin-access.log combined

    # Rewrites
    RewriteEngine On

    # Images
    RewriteRule ^/munin-cgi(.*) /usr/share/munin/cgi/$1 [L] 

    # Ensure we can run (fast)cgi scripts
    <Directory "/usr/share/munin/cgi">
        Require all granted
        Options +ExecCGI
        <IfModule mod_fcgid.c>
            SetHandler fcgid-script
        </IfModule>
        <IfModule !mod_fcgid.c>
            SetHandler cgi-script
        </IfModule>
    </Directory>
</VirtualHost>

```

### Full dynamic

Use this VirtualHost if you want to set **html_strategy** and **graph_strategy** to "**cgi**". Page loads will take longer because all the HTML and PNG files will be dynamically generated, but the munin-cron run will take less time because it will not execute munin-html and munin-graph. This feature may become necessary for you if your master polls many nodes and the munin-cron risks taking more than 5 minutes.

Install [perl-cgi-fast](https://www.archlinux.org/packages/?name=perl-cgi-fast).

You must enable one of these:

*   **mod_cgid** (or **mod_cgi** if using mpm_prefork_module) by uncommenting the line in httpd.conf.
*   Or install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) and add "**LoadModule mod_fcgid modules/mod_fcgid.so**" in httpd.conf.

```
<VirtualHost *:80>
    ServerName localhost
    ServerAdmin  root@localhost

    DocumentRoot /srv/http/munin

    ErrorLog /var/log/httpd/munin-error.log
    CustomLog /var/log/httpd/munin-access.log combined

    # Rewrites
    RewriteEngine On

    # Static content in /static
    RewriteRule ^/favicon.ico /etc/munin/static/favicon.ico [L] 
    RewriteRule ^/static/(.*) /etc/munin/static/$1          [L] 

    # HTML
    RewriteCond %{REQUEST_URI} .html$ [or]
    RewriteCond %{REQUEST_URI} =/
    RewriteRule ^/(.*)          /usr/share/munin/cgi/munin-cgi-html/$1 [L] 

    # Images
    RewriteRule ^/munin-cgi(.*) /usr/share/munin/cgi/$1 [L] 

    <Directory "/etc/munin/static">
        Require all granted
    </Directory>

    # Ensure we can run (fast)cgi scripts
    <Directory "/usr/share/munin/cgi">
        Require all granted
        Options +ExecCGI
        <IfModule mod_fcgid.c>
            SetHandler fcgid-script
        </IfModule>
        <IfModule !mod_fcgid.c>
            SetHandler cgi-script
        </IfModule>
    </Directory>
</VirtualHost>

```

## Tips and Tricks

### MySQL

The MySQL plugin has extra dependencies available in the AUR: [perl-dbi](https://www.archlinux.org/packages/?name=perl-dbi), [perl-cache-cache](https://aur.archlinux.org/packages/perl-cache-cache/), and [perl-ipc-sharelite](https://aur.archlinux.org/packages/perl-ipc-sharelite/)

Additionally it is recommended to access the database through a separate [MySQL](/index.php/MySQL "MySQL") user. To make another user via the following MySQL commands:

```
MariaDB> CREATE USER 'muninuser'@'localhost' IDENTIFIED BY 'muninpassword';
MariaDB> GRANT SUPER,PROCESS ON *.* TO 'muninuser'@'localhost';
MariaDB> GRANT SELECT ON mysql.* TO 'muninuser'@'localhost';
MariaDB> FLUSH PRIVILEGES; 
```

To configure Munin to use this new user, create:

 `/etc/munin/plugin-conf.d/mysql_` 

```
[mysql_*]
     env.mysqlconnection DBI:mysql:mysql;host=127.0.0.1;port=3306
     env.mysqluser muninuser
     env.mysqlpassword muninpassword
```

### S.M.A.R.T.

To enable monitoring of S.M.A.R.T. data, install the [smartmontools](https://www.archlinux.org/packages/?name=smartmontools) package, and use:

 `/etc/munin/plugin-conf.d/munin-node` 

```
[smart_*]
    user root
    group disk
```

Then create the appropriate symlink for each disk to be monitored. As an example for `sda`: `# ln -s /usr/lib/munin/plugins/smart_ /etc/munin/plugins/smart_**sda**` 

### lm_sensors

Install [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors) and configure according to [lm_sensors#Setup](/index.php/Lm_sensors#Setup "Lm sensors"). Assuming all goes correctly, create some symlinks:

```
# ln -s /usr/lib/munin/plugins/sensors_ /etc/munin/plugins/sensors_fan 
# ln -s /usr/lib/munin/plugins/sensors_ /etc/munin/plugins/sensors_temp
# ln -s /usr/lib/munin/plugins/sensors_ /etc/munin/plugins/sensors_volt
```