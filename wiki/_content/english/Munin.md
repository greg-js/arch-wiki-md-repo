[Munin](http://munin-monitoring.org/) is a networked resource monitoring tool that can help analyze resource trends and bottlenecks. Munin has a master/node architecture in which the master regularly fetches the data from the nodes and presents the information in graphs through a web interface. A default installation provides a lot of graphs with almost no work and new graphs can be easily created added as plugins. [[1]](http://munin-monitoring.org/)

You can check out University of Oslo's [Munin install](http://munin.ping.uio.no/) for an example.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Munin Master](#Munin_Master)
        *   [2.1.1 Directories](#Directories)
        *   [2.1.2 Cron](#Cron)
            *   [2.1.2.1 crontab](#crontab)
            *   [2.1.2.2 systemd timer](#systemd_timer)
        *   [2.1.3 Permissions](#Permissions)
        *   [2.1.4 Testing](#Testing)
    *   [2.2 Munin Node](#Munin_Node)
        *   [2.2.1 Daemon](#Daemon)
        *   [2.2.2 IPv6](#IPv6)
        *   [2.2.3 Customization](#Customization)
        *   [2.2.4 Plugins](#Plugins)
            *   [2.2.4.1 Adding](#Adding)
            *   [2.2.4.2 Additional Plugins](#Additional_Plugins)
            *   [2.2.4.3 Removing](#Removing)
            *   [2.2.4.4 Debugging](#Debugging)
        *   [2.2.5 Permissions](#Permissions_2)
*   [3 Web Server (Optional)](#Web_Server_.28Optional.29)
    *   [3.1 Apache](#Apache)
        *   [3.1.1 Apache VirtualHost examples](#Apache_VirtualHost_examples)
        *   [3.1.2 Basic static html](#Basic_static_html)
        *   [3.1.3 Static html with DynaZoom feature](#Static_html_with_DynaZoom_feature)
        *   [3.1.4 Full dynamic](#Full_dynamic)
    *   [3.2 Nginx](#Nginx)
        *   [3.2.1 Munin 2.0.x](#Munin_2.0.x)
        *   [3.2.2 Munin 2.1.x](#Munin_2.1.x)
*   [4 Tips and Tricks](#Tips_and_Tricks)
    *   [4.1 MySQL](#MySQL)
    *   [4.2 S.M.A.R.T.](#S.M.A.R.T.)
    *   [4.3 lm_sensors](#lm_sensors)

## Installation

[Install](/index.php/Install "Install") [munin](https://www.archlinux.org/packages/?name=munin) on the master machine and [munin-node](https://www.archlinux.org/packages/?name=munin-node) on the devices that you whish to monitor.

You can also install them both on the same machine so that the master machine monitors itself.

Further documentation may be found on the [Munin documentation wiki](http://munin-monitoring.org/wiki/Documentation).

## Configuration

### Munin Master

#### Directories

Create a directory where the *munin-master* will write the generated HTML and graph images. The munin user must have write permission to this directory.

The following example uses `/srv/http/munin`, so the generated output can be viewed at [http://localhost/munin/](http://localhost/munin/), provided that a web server is installed and running:

```
# mkdir /srv/http/munin
# chown munin:munin /srv/http/munin

```

Uncomment the `htmldir` entry in `/etc/munin/munin.conf` and change it to the directory created in the previous step:

```
htmldir /srv/http/munin

```

#### Cron

##### crontab

Run the following to have Munin collect data and update the generated HTML and graph images every 5 minutes:

```
# crontab /etc/munin/munin-cron-entry -u munin

```

Configure the email server to send mails to the *munin* user. If using postfix, add the following:

 `/etc/postfix/aliases` 
```
munin:    root

```

And run:

```
# newaliases

```

##### systemd timer

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

Now, reload systemd configuration, enable and start `munin-cron.timer`

```
# systemctl daemon-reload
# systemctl enable --now munin-cron.timer

```

and verify that everything is working:

```
# journalctl --unit munin-cron.service
# less /var/log/munin/munin-update.log

```

#### Permissions

When `graph_strategy cgi` is enabled in `/etc/munin/munin.conf` ensure the directory `/var/lib/munin/cgi-tmp` is owned by user and group `munin` so that the `/usr/share/munin/cgi/munin-cgi-graph` script is able to write the png files to this directory.

```
# chown munin: /var/lib/munin/cgi-tmp

```

#### Testing

Once `munin-cron` is configured to run Munin will be ready to start generating graphs. Ensure the `munin-node.service` is running on each of the nodes. It may be useful to jump ahead to the Munin Node section and return here once the node are up and running.

Change to the `munin` user with the following `su` command, the `-s`/`--shell` option is for specifiying the shell (in this case bash). This needs to be done from root shell, since the `munin` user does not have a password:

```
# su -s /bin/bash munin

```

By runnning the `munin-cron` command manually it will trigger the generation of HTML and graph images immediately without having to wait for the next cron run:

```
munin> munin-cron

```

If the munin logging is configured, the logs are usually found in `/var/log/munin/`. Watching the `munin-update.log` log in a seperate terminal after running the `munin-cron` command can be helpful in diagnosing issues.

```
# tail -f /var/log/munin/munin-update.log

```

And finally test the interface by pointing your browser to the output directory or [http://localhost/munin/](http://localhost/munin/).

**Note:** It might take a while for the graphs to have data, so be patient. Wait for about 30 minutes to an hour.

### Munin Node

#### Daemon

On the nodes, start and enable `munin-node`.

```
# systemctl enable --now munin-node

```

#### IPv6

For IPv6 support on *munin-node*, using:

 `/etc/munin/munin-node.conf` 
```
host :::1

```

Install:

*   [perl-socket6](https://www.archlinux.org/packages/?name=perl-socket6)
*   [perl-io-socket-inet6](https://www.archlinux.org/packages/?name=perl-io-socket-inet6)

#### Customization

Before running munin, you might want to setup the hostname of your system. In `/etc/munin/munin.conf`, the default hostname is `myhostname`. This can be altered to any preferred hostname. The hostname will be used to group and name the `.rrd` files in `/var/lib/munin` and further, used to group the html files and graphs in your selected *munin-master* directory.

#### Plugins

Run `munin-node-configure` with the `--suggest` option to have Munin suggest plugins it thinks will work on your installation:

```
# munin-node-configure --suggest

```

If there is a suggestion for a plugin you want to use, follow that suggestion and run the command again. When you are satisfied with the plugins suggested by `munin-node-configure`, run it with the `--shell` option to have the plugins configured:

```
# munin-node-configure --shell | sh

```

##### Adding

Basically all plugins are added in the following manner (although there are exceptions, review each plugin!):

Download a plugin, then copy or move it to `/usr/lib/munin/plugins`:

```
# cp *plugin* /usr/lib/munin/plugins/

```

Then link the plugin to `/etc/munin/plugins`:

```
# ln -s /usr/lib/munin/plugins/*plugin* /etc/munin/plugins/

```

**Note:** Some plugins - known as wildcard plugins - can be used with multiple devices at once by linking them with different names. These plugins end with an underscore and are linked as `<plugin>_<device>` to be used on `<device>`. See the `if_` plugin for an example.

Now test your plugin. You do not need to use the full path to the plugin, `munin-run` should be able to figure it out:

```
# munin-run *plugin*

```

And [restart](/index.php/Restart "Restart") `munin-node.service`. Finally, refresh the web page.

##### Additional Plugins

There are many Munin plugins out there just waiting to be installed. The [MuninExchange](http://muninexchange.projects.linpro.no/) is an excellent place to start looking, and if you cannot find a plugin that does what you want it is easy to write your own. Have a look at [Developing Plugins](http://guide.munin-monitoring.org/en/latest/develop/plugins/) at the Munin documentation wiki to learn how.

##### Removing

If you want to remove a plugin, simply delete the linked file in `/etc/munin/plugins` - there is no need to remove the plugin from `/usr/lib/munin/plugins`.

```
# rm /etc/munin/plugins/*plugin*

```

##### Debugging

If you come across a plugin that is not working as expected (for example giving you no output at all) it might be interesting to run it directly. Fortunately there is a way to do this. Following the instructions until here, you will for example notice, that the plugin `apache_accesses` gives no output at all, when enabled. In order to run the plugin directly:

```
# munin-run apache_accesses

```

The following error:

```
LWP::UserAgent not found at /etc/munin/plugins/apache_accesses line 86.

```

indicates that a perl function could not be found. To resolve the problem, [install](/index.php/Install "Install") the missing library, in this case, [perl-libwww](https://www.archlinux.org/packages/?name=perl-libwww).

#### Permissions

Because many plugins read log files, it is useful to [add](/index.php/Users_and_groups#Example_adding_a_user "Users and groups") `munin` user into `log` group:

```
# usermod -a -G log munin

```

## Web Server (Optional)

This guide sets up Munin to generate static HTML and graph images and write them in a directory of your choosing. You can view these generated files locally with any web browser. If you want to view the generated files from a remote machine, then you will need to install and configure one of the following web servers:

*   [Apache](/index.php/Apache "Apache")
*   [Lighttpd](/index.php/Lighttpd "Lighttpd")
*   [Nginx](/index.php/Nginx "Nginx")

Or one of the other servers found in the [web server](/index.php/Web_server "Web server") category.

### Apache

#### Apache VirtualHost examples

Based on information found here:

*   [http://guide.munin-monitoring.org/en/stable-2.0/example/webserver/apache-virtualhost.html](http://guide.munin-monitoring.org/en/stable-2.0/example/webserver/apache-virtualhost.html)
*   [http://munin-monitoring.org/wiki/MuninConfigurationMasterCGI](http://munin-monitoring.org/wiki/MuninConfigurationMasterCGI)

In the next major release of Munin, things will be much simpler. Check it out:

*   [http://guide.munin-monitoring.org/en/latest/example/webserver/apache-virtualhost.html](http://guide.munin-monitoring.org/en/latest/example/webserver/apache-virtualhost.html)

#### Basic static html

```
<VirtualHost *:80>
    ServerName localhost
    ServerAdmin  root@localhost

    DocumentRoot /srv/http/munin

    ErrorLog /var/log/httpd/munin-error.log
    CustomLog /var/log/httpd/munin-access.log combined
</VirtualHost>

```

#### Static html with DynaZoom feature

Install [perl-cgi-fast](https://www.archlinux.org/packages/?name=perl-cgi-fast).

You must enable one of these:

*   `mod_cgid` (or `mod_cgi` if using mpm_prefork_module) by uncommenting the line in `httpd.conf`.
*   Or install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) and add `LoadModule mod_fcgid modules/mod_fcgid.so` in `httpd.conf`.

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
       <IfModule !mod_fcgid.c>
           SetHandler cgi-script
       </IfModule>
   </Directory>
</VirtualHost>

```

#### Full dynamic

Use this VirtualHost if you want to set `html_strategy` and `graph_strategy` to `cgi`. Page loads will take longer because all the HTML and PNG files will be dynamically generated, but the munin-cron run will take less time because it will not execute munin-html and munin-graph. This feature may become necessary for you if your master polls many nodes and the munin-cron risks taking more than 5 minutes.

Install [perl-cgi-fast](https://www.archlinux.org/packages/?name=perl-cgi-fast).

You must enable one of these:

*   `mod_cgid` (or `mod_cgi` if using mpm_prefork_module) by uncommenting the line in `httpd.conf`.
*   Or install [mod_fcgid](https://www.archlinux.org/packages/?name=mod_fcgid) and add `LoadModule mod_fcgid modules/mod_fcgid.so` in `httpd.conf`.

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
   RewriteCond %{REQUEST_URI} .html$ [or]
   RewriteCond %{REQUEST_URI} =/
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
       <IfModule !mod_fcgid.c>
           SetHandler cgi-script
       </IfModule>
   </Directory>
</VirtualHost>

```

### Nginx

#### Munin 2.0.x

This example Nginx setup is based on a Munin 2.0.x `munin` master installation. It requires FastCGI and uses the `html_strategy cgi` and `graph_strategy cgi` in the `munin.conf` configuration.

[Install](/index.php/Install "Install") the [nginx](https://www.archlinux.org/packages/?name=nginx), [perl-cgi-fast](https://www.archlinux.org/packages/?name=perl-cgi-fast) and [perl-html-template-expr](https://www.archlinux.org/packages/?name=perl-html-template-expr) packages on the Munin-Master.

As we will be using the *cgi* strategy the systemd socket files need to be enabled. So the `/run/munin/fcgi-graph.sock` and `/run/munin/fcgi-html.sock` sockets are created for the Nginx FastCGI configuration to hook into.

```
# systemctl enable --now munin-graph.socket
# systemctl enable --now munin-html.socket

```

Create the munin vhost configuration file

 `/etc/nginx/sites-available/munin` 
```
server {
    server_name yourhost.example.com;
    listen 80;
    access_log /var/log/nginx/munin-access.log;
    error_log /var/log/nginx/munin-error.log info;
    location ^~ /munin-cgi/munin-cgi-graph/ {
        fastcgi_split_path_info ^(/munin-cgi/munin-cgi-graph)(.*);
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_pass unix:/run/munin/fcgi-graph.sock;
        include fastcgi_params;
    }
    location /munin/static/ {
        alias /etc/munin/static/;
    }
    location /munin/ {
        fastcgi_split_path_info ^(/munin)(.*);
        fastcgi_param PATH_INFO $fastcgi_path_info;
        fastcgi_pass unix:/run/munin/fcgi-html.sock;
        include fastcgi_params;
    }
}

```

Then restart the webserver

```
# systemctl restart nginx

```

If all goes well, point your browser to your host **[http://yourhost.example.com/munin/](http://yourhost.example.com/munin/)** and you should see the Munin Overview page.

#### Munin 2.1.x

Although Munin 2.1.x versions are not yet available in the Arch repository. It is worth mentioning that the 2.1.x series will no longer use FastCGI and will be replaced with [munin-httpd](http://guide.munin-monitoring.org/en/latest/reference/munin-httpd.html#munin-httpd) This [page](http://guide.munin-monitoring.org/en/latest/example/webserver/nginx.html) already contains an example configuration.

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