[SquirrelMail](http://squirrelmail.org/index.php) is a lightweight webmail package written in PHP with IMAP/IMAPS support. SquirrelMail has many plugins (calendar, spelling, etc.) and good browser support (uses HTML 4.0 and does not require JavaScript).

## Installation

### Available versions

[Install](/index.php/Install "Install") the [squirrelmail](https://aur.archlinux.org/packages/squirrelmail/) package, or [squirrelmail-dev-svn](https://aur.archlinux.org/packages/squirrelmail-dev-svn/) for the development version.

### Install details

You will need to configure your mail package before you can use SquirrelMail. Installing SquirrelMail is straight forward:

1.  Download SquirrelMail from [[1]](http://squirrelmail.org/download.php).
2.  Place the contents (the entire squirrelmail directory) in your document root. For Arch, that will be under `/srv/http`.
3.  Create directories **outside of your document root** for the SquirrelMail "data" and "attachment" directories. Example: `mkdir -p /usr/local/share/sqmail/{data,attach}` which will create the directories under `/usr/local/share/sqmail`. You then must make the directories readable and writable by the web server. On Arch, `chown -R http:http /usr/local/share/sqmail`
4.  Configure SquirrelMail (as root) by running the perl script `/srv/http/squirrelmail/config/conf.pl`. Simply fill in the information specific to your configuration. Note, there are preconfigured setting groups for different mail packages (dovecot, courier, UW, etc...)
5.  Make sure you turn on the option under "11\. tweaks" to "Allow remote config test" to allow you to check the configuration if you are not doing your configuration from localhost. (turn it off when you are done with all test and your satisfied with your setup)
6.  You will need to modify `/etc/php/php.ini` to change a few setting to accommodate SquirrelMail. Open `/etc/php/php.ini` and modify the following settings:
    ```
    memory_limit = 128M  ; must be at least 32M
    post_max_size = 16M  ; controls the maximum attachment size
    open_basedir = /srv/http/:/srv/www:/home/:/tmp/:/usr/share/pear/:/usr/local/share/sqmail/
    ```
    You simply need to add the path to your SquirrelMail data and attachment directories, shown above as `:/usr/local/share/sqmail/`.
7.  [Reload](/index.php/Reload "Reload") the webserver.
8.  When you are done with the setting and choosing plugins in `conf.pl` and done with modifying `php.ini`, just point your browser to [http://localhost/squirrelmail/configcheck.php](http://localhost/squirrelmail/configcheck.php) to test your configuration. Fix any problems you encounter.
9.  Disable "Allow remote config test" in `conf.pl`.

Now you should be able to point your browser to [http://localhost/squirrelmail](http://localhost/squirrelmail) and log in.