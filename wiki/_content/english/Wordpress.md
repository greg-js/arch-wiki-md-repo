Related articles

*   [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server")
*   [PHP](/index.php/PHP "PHP")
*   [MySQL](/index.php/MySQL "MySQL")
*   [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin")

[WordPress](http://wordpress.org) is a free and open source content management system ([CMS](https://en.wikipedia.org/wiki/Content_management_system "wikipedia:Content management system")) created by [Matt Mullenweg](https://en.wikipedia.org/wiki/Matt_Mullenweg "wikipedia:Matt Mullenweg") and first released in 2003\. WordPress has a vast and vibrant community that provides tens of thousands of free plugins and themes to allow the user to easily customize the appearance and function of their WordPress CMS. WordPress is licensed under the GPLv2.

The biggest feature of WordPress is its ease in configuration and administration. [Setting up a WordPress site takes five minutes](http://codex.wordpress.org/Installing_WordPress). The WordPress administration panel allows users to easily configure almost every aspect of their website including fetching and installing plugins and themes. WordPress provides effortless automatic updates.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Installation using pacman](#Installation_using_pacman)
    *   [1.2 Manual install](#Manual_install)
*   [2 Configuration](#Configuration)
    *   [2.1 Host config](#Host_config)
    *   [2.2 Configure apache](#Configure_apache)
    *   [2.3 Configure MySQL](#Configure_MySQL)
        *   [2.3.1 Using MariaDB command-line tool](#Using_MariaDB_command-line_tool)
        *   [2.3.2 Using phpMyAdmin](#Using_phpMyAdmin)
*   [3 WordPress Installation](#WordPress_Installation)
*   [4 Usage](#Usage)
    *   [4.1 Installing a theme](#Installing_a_theme)
        *   [4.1.1 Finding new themes](#Finding_new_themes)
        *   [4.1.2 Install using the admin panel](#Install_using_the_admin_panel)
        *   [4.1.3 Install manually](#Install_manually)
    *   [4.2 Installing a plugin](#Installing_a_plugin)
    *   [4.3 Updating](#Updating)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Appearance is broken (no styling)](#Appearance_is_broken_.28no_styling.29)
    *   [5.2 Plugins are unable to install: Could not create directory](#Plugins_are_unable_to_install:_Could_not_create_directory)
    *   [5.3 Cannot save plugins to localhost](#Cannot_save_plugins_to_localhost)
*   [6 Tips and tricks](#Tips_and_tricks)
*   [7 See also](#See_also)

## Installation

WordPress requires [Apache](/index.php/Apache "Apache"), [PHP](/index.php/PHP "PHP") and [MySQL](/index.php/MySQL "MySQL") to be installed and configured. See the respective pages for information. During PHP configuration, be aware that some WordPress features require [PHP extensions](http://wordpress.stackexchange.com/questions/42098/what-are-php-extensions-and-libraries-wp-needs-and-or-uses) that may not be turned on by default.

### Installation using pacman

[Install](/index.php/Install "Install") the [wordpress](https://www.archlinux.org/packages/?name=wordpress) package.

**Warning:** While it is easier to let pacman manage updating your WordPress install, this is not necessary. WordPress has functionality built-in for managing updates, themes, and plugins. If you decide to install the official community package, you will not be able to install plugins and themes using the WordPress admin panel without a needlessly complex permissions setup, or logging into FTP as root. pacman does not delete the WordPress install directory when uninstalling it from your system regardless of whether or not you have added data to the directory manually or otherwise.

### Manual install

Go to [wordpress.org](http://wordpress.org/download/) and download the latest version of WordPress and extract it to your webserver directory. Give the directory enough permissions to allow your FTP user to write to the directory (used by WordPress).

```
cd /srv/http/*whatever*
wget https://wordpress.org/latest.tar.gz
tar xvzf latest.tar.gz

```

## Configuration

The configuration method used here assumes you are using WordPress on a local network.

### Host config

Make sure your `/etc/hosts` file is setup correctly. This will be important when accessing your WordPress CMS from a local network. Your `/etc/hosts` file should look something like the following,

```
#<ip-address>   <hostname.domain.org>   <hostname>
127.0.0.1       lithium.kaboodle.net    localhost lithium
::1             lithium.kaboodle.net    localhost lithium
```

**Note:** You will need to use a proxy server to access your WordPress installation from mobile devices if you plan on using hostnames to install WordPress, otherwise your website will appear broken [#Appearance is broken (no styling)](#Appearance_is_broken_.28no_styling.29).

### Configure apache

**Note:** You will need [Apache](/index.php/Apache "Apache") configured to run with [PHP](/index.php/PHP "PHP") and [MySQL](/index.php/MySQL "MySQL").

You will need to create a config file for apache to find your WordPress install. Create the following file and edit it your favorite text editor:

 `# /etc/httpd/conf/extra/httpd-wordpress.conf` 
```
Alias /wordpress "/usr/share/webapps/wordpress"
<Directory "/usr/share/webapps/wordpress">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
</Directory>
```

Change `/wordpress` in the first line to whatever you want. For example, `/myblog` would require that you navigate to `[http://hostname/myblog](http://hostname/myblog)` to see your WordPress website.

Also change the paths to your WordPress install folder in case you did a manual install. Do not forget to append the parent directory to the `php_admin_value` variable as well as shown below.

 `# /etc/httpd/conf/extra/httpd-wordpress.conf` 
```
Alias /myblog "/mnt/data/srv/wordpress"
<Directory "/mnt/data/srv/wordpress">
	AllowOverride All
	Options FollowSymlinks
	Require all granted
</Directory>
```

Next edit the [Apache](/index.php/Apache "Apache") configuration file and add the following:

 `# /etc/httpd/conf/httpd.conf` 
```
Include conf/extra/httpd-wordpress.conf

```

Now restart `httpd.service` (Apache) using [systemd](/index.php/Systemd#Using_units "Systemd").

### Configure MySQL

MySQL can be configured using a plethora of tools, but the most common are the command-line or [phpMyAdmin](http://www.phpmyadmin.net/home_page/index.php).

**Tip:** Make sure MariaDB is installed and configured correctly. At a minimum, follow the [installation instructions](/index.php/MySQL#Installation "MySQL") for Arch Linux.

#### Using MariaDB command-line tool

First, login as root. You will be asked for your MariaDB root password:

```
$ mysql -u root -p

```

Then create a user and database:

**Note:** `wordpress` is your Database Name and `wp-user` is your User Name. You can change them if you wish. Also replace `choose_db_password` with your new Password for this database. You will be asked for these values along with `localhost` in the next section.

```
MariaDB> CREATE DATABASE wordpress;
MariaDB> GRANT ALL PRIVILEGES ON wordpress.* TO "wp-user"@"localhost" IDENTIFIED BY "choose_db_password";
MariaDB> FLUSH PRIVILEGES;
MariaDB> EXIT
```

See WordPress.org [official instructions](https://codex.wordpress.org/Installing_WordPress#Using_the_MySQL_Client) for details.

#### Using phpMyAdmin

See [phpMyAdmin](/index.php/PhpMyAdmin "PhpMyAdmin") to install and configure phpMyAdmin.

In your web browser, navigate to your phpMyAdmin host and perform the following steps:

1.  Login to phpMyAdmin.
2.  Click "user" and then click "Add user".
3.  Give the pop up window a name and a password.
4.  Select "Create database with same name and grant all privileges".
5.  Click the "Add user" button to create the user.

## WordPress Installation

Once you have spent a couple of hours setting up your http server, php, and mysql, it is finally time to let WordPress have its five minutes and install itself. So let us begin.

The WordPress installation procedure will use the URL in the address field of your web browser as the default website URL. If you have navigated to [http://localhost/wordpress](http://localhost/wordpress), your website will be accessible from your local network, but it will be broken in appearance and function.

1.  Navigate to `[http://hostname/wordpress](http://hostname/wordpress)`.
2.  Click the "Create a Configuration File" button.
3.  Click the "Let's go!" button.
4.  Fill in you database information created in the previous section
5.  Click "Submit".

If you installed WordPress from the Official repository, then this setup procedure will not have the correct permissions to create the wp-config.php file used by WordPress. You will have to do this step yourself as root using information WordPress will provide.

A page will appear saying WordPress can not write the wp-config.php file. Copy the text in the edit box and open `/usr/share/webapps/wordpress/wp-config.php` as root in your text editor. Paste the copied text into the editor and save the file.

After that, you will have to change permissions of the /usr/share/webapps/wordpress/ and all the files inside it to user `http` and group `http` by using chown so that the webserver can access it.

Finally, Click "Run the install" and WordPress will populate the database with your information. Once complete, you will be shown "Success!" page. Click the login button to finish your installation.

Now would be a good time to access your website from all your devices to be sure your WordPress installation is setup correctly.

## Usage

### Installing a theme

#### Finding new themes

There are tens of thousands of themes available for WordPress. Searching on google for a good theme can be like wading through a river filled with trash. Good places for looking for themes include:

*   [Official WordPress theme website](https://wordpress.org/themes/)
*   [Smashing Magazine](http://www.smashingmagazine.com/)
*   [The Theme Factory](http://thethemefoundry.com/)
*   [Woo Themes](http://www.woothemes.com/)

**Tip:** One can use WordPress' admin interface to install plugins and themes. To do this, make the user that serves WordPress the [owner](/index.php/File_permissions_and_attributes#Changing_permissions "File permissions and attributes") of your WordPress directory. For [Apache](/index.php/Apache_HTTP_Server#Advanced_options "Apache HTTP Server") this user is normally http.

#### Install using the admin panel

Before installing a theme using the admin panel, you will need to setup an [FTP](/index.php/Very_Secure_FTP_Daemon "Very Secure FTP Daemon") server on your WordPress host. To maintain a high level of protection, you might set up a [user](/index.php/User "User") on your system specifically for WordPress, give it the home directory of `<path to your WordPress install>/wp-content`, disallow anonymous login, and allow no more users to log in than for WordPress (and obviously others as required by your setup).

Once the FTP server is setup, login to your WordPress installation and click "Appearance->Install Themes->Upload". From there select your zip file that contains your theme and click "Install Now". You will be presented with a box asking for FTP information, enter it and click "Proceed". You might need to update [file ownership](/index.php/Chown "Chown") and [rights](/index.php/Chmod "Chmod") if WordPress reports that it is unable to write to the directory. If you have been following along closely, you should now have an installed theme. Activate it if you wish.

#### Install manually

Download the archive and extract into the **wp-content/themes** folder

```
# Example for a theme named "MyTheme"
cd /path/to/wordpress/root/directory
cd wp-content/themes

```

```
# get the theme archive and extract
wget http://www.example.com/MyTheme.zip
unzip MyTheme.zip

```

```
# remove the archive (optional)
rm MyTheme.zip

```

Be sure to follow any additional instructions as provided by the theme author.

Select your new theme from the theme chooser ("Appearance->Themes")

### Installing a plugin

The steps for installing a plugin are the same as they are for installing a theme. Just click the "Plugins" link in the left navigation bar and follow the steps.

### Updating

Every now and then when you log into wordpress there will be a notification informing you of updates. If you have correctly installed and configured an FTP client, and have the correct filesystem permissions to write in the WordPress install path then you should be able to perform updates at the click of a button. Just follow the steps.

Alternatively, you can use SSH to update your installation with the [SSH SFTP Updater Support plugin](https://wordpress.org/plugins/ssh-sftp-updater-support/).

## Troubleshooting

### Appearance is broken (no styling)

Your WordPress website will appear to have no styling to it when viewing it in a web browser (desktop or mobile) that does not have its hostnames mapped to ip addresses correctly.

This occurs because you used a url with the hostname of your server, instead of an ip address, when doing the initial setup and WordPress has used this as the default website URL.

To fix this, you will either need to edit your /etc/hosts file or setup a proxy server. For an easy to setup proxy server, see [Polipo](/index.php/Polipo "Polipo"), or if you want something with a little more configuration, see [Squid](/index.php/Squid "Squid").

Another option is changing a value in the database table of your WordPress, specifically the wp_options table. The fix is to change the siteurl option to point directly to the domain name and not "localhost".

### Plugins are unable to install: Could not create directory

Your WordPress site need appropriate permissions to your local files. It doesn't have the permissions to create files/directory. Appache with Arch uses the user `http`.

To give the appropriate permissions run the following command:

 `$ chown -R http:http your-wordpress-directory/wp-content` 

### Cannot save plugins to localhost

WordPress uses by default only a ftp server to download plugins. In order to also download them locally append the following config:

 `# *wordpress_root_location*/wp-config.php` 
```
define('FS_METHOD', 'direct');

```

## Tips and tricks

## See also

*   [WordPress](https://en.wikipedia.org/wiki/WordPress "wikipedia:WordPress")
*   [Content management system](https://en.wikipedia.org/wiki/Content_management_system "wikipedia:Content management system")