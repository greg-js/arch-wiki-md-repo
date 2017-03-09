[XAMPP](http://www.apachefriends.org/en/xampp.html) is an easy to install Apache distribution containing MySQL, PHP and Perl. It contains: Apache, MySQL, PHP & PEAR, Perl, ProFTPD, phpMyAdmin, OpenSSL, GD, Freetype2, libjpeg, libpng, gdbm, zlib, expat, Sablotron, libxml, Ming, Webalizer, pdf class, ncurses, mod_perl, FreeTDS, gettext, mcrypt, mhash, eAccelerator, SQLite and IMAP C-Client.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Using AUR package](#Using_AUR_package)
    *   [1.2 Manual Installation](#Manual_Installation)
    *   [1.3 Removal](#Removal)
*   [2 Configuration](#Configuration)
    *   [2.1 Autostart on boot](#Autostart_on_boot)
*   [3 Usage](#Usage)
*   [4 Hosting files outside the htdocs directory](#Hosting_files_outside_the_htdocs_directory)
*   [5 Debugging and profiling with Xdebug and Xampp](#Debugging_and_profiling_with_Xdebug_and_Xampp)
*   [6 PhpMyAdmin 403 Access Forbidden](#PhpMyAdmin_403_Access_Forbidden)
*   [7 Local test server security](#Local_test_server_security)

## Installation

#### Using AUR package

Install [xampp](https://aur.archlinux.org/packages/xampp/).

#### Manual Installation

Download the installer from: [the website](https://www.apachefriends.org/index.html).

The downloaded file is an installer script. Make it executable and run it by typing:

```
# chmod +x xampp-linux-**version**-installer.run 
# ./xampp-linux-**version**-installer.run 

```

#### Removal

Be sure to stop all lampp services.

```
# /opt/lampp/lampp stop

```

All the files needed by Xampp to be installed are located in the previous `/opt/lampp` folder. So, to uninstall Xampp:

```
# rm -rf /opt/lampp

```

**Note:** If you created symlinks, you may need to destroy them too.

## Configuration

Setting the individual parts of XAMPP can by made by editing following files:

`/opt/lampp/etc/httpd.conf` - Apache configuration. For example you can change folder with web page's source files.

`/opt/lampp/etc/php.ini` - PHP configuration.

`/opt/lampp/phpmyadmin/config.inc.php` - phpMyAdmin configuration.

`/opt/lampp/etc/proftpd.conf` - proFTP configuration.

`/opt/lampp/etc/my.cnf` - MySQL configuration.

If you would like to set up security of server, you can do it simply by this command:

```
# /opt/lampp/lampp security

```

You will be asked step by step to choose passwords for web page's access, user "pma" for phpMyAdmin, user "root" for MySQL and user "nobody" for proFTP.

### Autostart on boot

In order to start Xampp at boot, service needs to be created, in the following file:

```
# vim /etc/systemd/system/xampp.service

```

Put these lines:

[Unit] Description=XAMPP [Service] ExecStart=/opt/lampp/lampp start ExecStop=/opt/lampp/lampp stop Type=forking [Install] WantedBy=multi-user.target

Enable autostart like this:

```
# systemctl enable xampp.service

```

## Usage

Use the following commands to control XAMPP: `# /opt/lampp/lampp start,stop,restart` 

If you get this error when you start it:

```
Starting XAMPP for Linux 1.7.7...
/opt/lampp/lampp: line 21: netstat: command not found
/opt/lampp/lampp: line 21: netstat: command not found
XAMPP: Starting Apache with SSL (and PHP5)...
/opt/lampp/lampp: line 241: /bin/hostname: No such file or directory
/opt/lampp/lampp: line 21: netstat: command not found
XAMPP: Starting MySQL...
/opt/lampp/bin/mysql.server: line 263: hostname: command not found
/opt/lampp/lampp: line 21: netstat: command not found
XAMPP: Starting ProFTPD...
XAMPP for Linux started.

```

Install [net-tools](https://www.archlinux.org/packages/?name=net-tools) and [inetutils](https://www.archlinux.org/packages/?name=inetutils) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Hosting files outside the htdocs directory

The document root (web root) directory is located at `/opt/lampp/htdocs/`. All files placed in this directory will be processed by the web server.

To host other files on your system with XAMPP, you can configure an alias with apache.

*   Edit apache's httpd.conf with your favorite editor.

```
# vim /opt/lampp/etc/httpd.conf

```

*   Find "DocumentRoot", you will see something like:

```
DocumentRoot "/opt/lampp/htdocs"
<Directory "/opt/lampp/htdocs">
    ...    
    ...

</Directory>
```

*   In the next line after "</Directory>" paste this:

```
<Directory "/yourDirectory/">
    Options Indexes FollowSymLinks ExecCGI Includes
    AllowOverride All
    Require all granted
</Directory>
```

*   Next find the "<IfModule alias_module>":

```
<IfModule alias_module>

    #
    # Redirect: Allows you to tell clients about documents that used to 
    # exist in your server's namespace, but do not anymore. The client 
    # will make a new request for the document at its new location.
    # Example:
    # Redirect permanent /foo [http://www.example.com/bar](http://www.example.com/bar)
  ...
</IfModule>

```

*   And before the "</IfModule>" paste this:

```
Alias /yourAlias /yourDirectory/

```

*   Now do not forget to restart Apache:

```
# /opt/lampp/lampp restart

```

This will allow you to host files from your home directory (or any other directory) with XAMPP.

In the above example, you can access the files by pointing your web browser to **localhost/yourAlias**.

## Debugging and profiling with Xdebug and Xampp

For detailed instructions go [here](http://xdebug.org/find-binary.php).

You must first download the Xampp Development Tools from the same download page [here](http://www.apachefriends.org/en/xampp-linux.html).

Extract this into your Xampp directory:

```
# tar xvfz xampp-linux-devel-x.x.x.tar.gz -C /opt

```

You should be able to successfully run

```
/opt/lampp/bin/phpize

```

in your xdebug folder.

## PhpMyAdmin 403 Access Forbidden

If your [http://localhost/phpmyadmin](http://localhost/phpmyadmin) returns "403 Access Forbidden", you need to edit the following settings in `/opt/lampp/etc/extra/httpd-xampp.conf`:

```
<Directory "/opt/lampp/phpmyadmin">
	AllowOverride AuthConfig Limit
	#Order allow,deny
	#Allow from all
	Require all granted
</Directory>

```

## Local test server security

Apache and MySQL can be configured so that they only listen to requests from your own computer. For most test systems this is fine and it greatly reduces the risk because the services are not reachable from the Internet.

Before you start XAMPP for the first time find and edit these files:

For Apache edit the files xampp\apache\conf\httpd.conf and xampp\apache\conf\extra\httpd-ssl.conf. Look for lines starting with "Listen" such as

```
Listen 80

```

and replace them with

```
Listen 127.0.0.1:80

```

For MySQL open the file xampp\mysql\bin\my.cnf find the section "[mysqld]" and add this line

```
bind-address=localhost

```

After starting the services, verify the result by going to a command window and start and execute:

```
netstat -a -n

```

For the entries marked as LISTEN in the last column, look at the Listen column. It should always start with 127.0.0.1 or ::1 but not with 0.0.0.0.