MythWeb is a web interface for [MythTV](/index.php/MythTV "MythTV")

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 MythTV integration](#MythTV_integration)
    *   [2.2 MythWeb](#MythWeb)
    *   [2.3 PHP](#PHP)
*   [3 Set rights for mythtv dir and create the link to mythweb](#Set_rights_for_mythtv_dir_and_create_the_link_to_mythweb)
*   [4 Using MythWeb](#Using_MythWeb)
*   [5 Securing MythWeb](#Securing_MythWeb)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 See also](#See_also)

## Installation

Before installing MythWeb, first set up Apache with PHP as described in [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") and [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Install the [mythplugins-mythweb](https://aur.archlinux.org/packages/mythplugins-mythweb/) package.

## Configuration

### MythTV integration

MythWeb looks in the `video_dir` directory for [MythTV](/index.php/MythTV "MythTV") recordings. Create a link to the folder where your MythTV recordings are stored:

```
# ln -s *recording_dir* /var/lib/mythtv/mythweb/video_dir

```

### MythWeb

Copy the MythWeb configuration file `mythweb.conf` to the [Apache](/index.php/Apache "Apache") configuration directory.

```
# cp /var/lib/mythtv/mythweb/mythweb.conf.apache /etc/httpd/conf/extra/mythweb.conf

```

And include it at the bottom of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/mythweb.conf

```

If you want to use MythWeb with the recent default `mythweb.conf` options enabled you will also need to uncomment the following lines in `httpd.conf`:

```
LoadModule rewrite_module modules/mod_rewrite.so
LoadModule deflate_module modules/mod_deflate.so

```

You will also need to enable CGI uncomment the following lines in `httpd.conf`:

```
<IfModule !mpm_prefork_module>
        LoadModule cgid_module modules/mod_cgid.so
</IfModule>
<IfModule mpm_prefork_module>
        LoadModule cgi_module modules/mod_cgi.so
</IfModule>

```

Edit `mythweb.conf` to point it to the installation directory for mythweb (near the beginning of the file):

```
<Directory "/srv/http/mythweb/data">

```

```
<Directory "/srv/http/mythweb" >

```

Then check that the configuration matches your [MythTV](/index.php/MythTV "MythTV") setup. If you have changed the database login or password, you will need to change the following section. Double-check the following lines are uncommented in any case:

```
setenv db_server        "localhost"
setenv db_name          "mythconverg"
setenv db_login         "mythtv"
setenv db_password      "mythtv"

```

### PHP

Edit the [PHP](/index.php/PHP "PHP") configuration file `/etc/php/php.ini`

Uncomment the following lines in the *Dynamic extensions* section.

```
extension=mysqli

```

Make sure `open_basedir` contains `/srv/http/` and `/var/lib/mythtv/mythweb` to allow file operation in the MythWeb directory. Starting with MythTV 0.23, you will also need to permit access to `/usr/share/mythtv/`.

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/var/lib/mythtv/mythweb:/usr/share/mythtv/

```

Enable the `allow_url_fopen` option for MythWeb's status page to work.

```
allow_url_fopen = On

```

## Set rights for mythtv dir and create the link to mythweb

```
chmod 755 -R /var/lib/mythtv/

```

```
ln -s /var/lib/mythtv/mythweb /srv/http/

```

## Using MythWeb

You can now start the Apache daemon by [starting](/index.php/Start "Start") the `httpd.service` systemd unit. *mythbackend* must already be running.

Open MythWeb in your browser.

```
[http://localhost/mythweb](http://localhost/mythweb)

```

## Securing MythWeb

It is also probably a good idea to set up password protection for MythWeb, if you intend to allow connections from the Internet. To enable authentication uncomment the authentication section (near the beginning):

 `/etc/httpd/conf/extra/mythweb.conf` 
```
AuthType           Digest
AuthName           "MythTV"
AuthUserFile       /var/www/htdigest
Require            valid-user
BrowserMatch       "MSIE"      AuthDigestEnableQueryStringHack=On
Order              allow,deny
Satisfy            any
```

Now, we need to fix the configuration to match the MythWeb set up, change the `AuthUserFile` to

```
AuthUserFile       /etc/httpd/conf/extra/httpd-passwords

```

If you do not want to access MythWeb from IE, you can delete the BrowserMatch line.

You also probably do not want to have to enter your password when you are connecting from your local computer, so add the following line between the last two lines:

```
Allow from 127\. 192.168.1.

```

This will cause passwordless access from both your local machine **and** your local network (provided you are using the 192.168.1.0 255.255.255.0 subnet)

The configuration should now look something like:

```
AuthType           Digest
AuthName           "MythTV"
AuthUserFile       /etc/httpd/conf/extra/httpd-passwords
Require            valid-user
Order              allow,deny
Allow from 127\. 192.168.1.
Satisfy            any

```

Save the file.

Next, we will create the `httpd-passwords` file

```
# htdigest -c /etc/httpd/conf/extra/httpd-passwords MythTV *myuser*

```

Where *myuser* is the username you want to use to access MythWeb. Enter the login password when prompted.

If you need more users, omit `-c` - otherwise you will overwrite the current file:

```
# htdigest /etc/httpd/conf/extra/httpd-passwords MythTV *myuser2*

```

Now all we need to do now is [restart](/index.php/Restart "Restart") apache's `httpd.service` for the changes to take effect.

## Troubleshooting

If you get a 403 Forbidden error, recheck your paths in `mythweb.conf`

If you can not start the apache service, and you get and error like this:

```
$ journalctl -u httpd -xn
...
AH00013: Pre-configuration failed
...

```

Comment out the following line in `httpd.conf`:

```
LoadModule mpm_event_module modules/mod_mpm_event.so

```

and use the prefork module instead:

```
LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

```

## See also

*   [MythTV Wiki page on MythWeb](http://www.mythtv.org/wiki/MythWeb)