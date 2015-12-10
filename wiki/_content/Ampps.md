# Ampps

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[AMPPS](http://www.ampps.com/) AMPPS is a LAMP stack of Apache, MySQL, MongoDB, PHP, Perl & Python. It also provides phpMyAdmin, SQLite Manager, RockMongo.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Manual installation](#Manual_installation)
*   [2 Configuration](#Configuration)
*   [3 Hosting files outside the htdocs directory](#Hosting_files_outside_the_htdocs_directory)
*   [4 Debugging and profiling with Xdebug and Ampps](#Debugging_and_profiling_with_Xdebug_and_Ampps)
*   [5 PhpMyAdmin](#PhpMyAdmin)

## Installation

### Manual installation

1.  Download the latest version from [here](http://ampps.com/download).
2.  The downloaded file is an installer script. Make it executable and run it by typing:

```
# chmod +x Ampps-**2.4**-x86.run
# ./Ampps-**2.4**-x86.run

```

assuming version 2.4\. Otherwise adapt the correct version number

Start the Ampps Application from the GUI.

Removal

Be sure to stop all the services.

All the files needed by Ampps to be installed are located in the previous `/usr/local/ampps` folder. So, to uninstall Ampps, consider this command.

```
# rm -rf /usr/local/ampps

```

**Note:** If you created symlinks, you may need to destroy them too.

## Configuration

Configuration of Apache, MySQL, PHP and all Service can be modfied from AMPPS GUI itself.

## Hosting files outside the htdocs directory

1.  You can create Domain from Softaculous Enduser Panel.
2.  You can also create the Alias from Softaculous Enduser Panel.

## Debugging and profiling with Xdebug and Ampps

Xdebug PHP Extension is already provided with the Ampps Package. Add the following line to the PHP Configuration and restart the Apache server:

 `zend_extension=/usr/local/ampps/php/lib/extensions/xdebug.so` 

## PhpMyAdmin

Access the following URL to access phpMyAdmin: [http://localhost/phpmyadmin](http://localhost/phpmyadmin)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ampps&oldid=388009](https://wiki.archlinux.org/index.php?title=Ampps&oldid=388009)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")