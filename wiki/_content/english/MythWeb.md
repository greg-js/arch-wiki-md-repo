MythWeb is a web interface for [MythTV](/index.php/MythTV "MythTV")

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Link to the Video Directory](#Link_to_the_Video_Directory)
*   [2 Configuration](#Configuration)
    *   [2.1 MythWeb](#MythWeb)
    *   [2.2 PHP](#PHP)
*   [3 Set rights for mythtv dir and create the link to mythweb](#Set_rights_for_mythtv_dir_and_create_the_link_to_mythweb)
*   [4 Using MythWeb](#Using_MythWeb)
*   [5 Securing MythWeb](#Securing_MythWeb)
*   [6 Troubleshooting](#Troubleshooting)
*   [7 External Links](#External_Links)

## Installation

Before installing MythWeb, first set up Apache with PHP as described in [Apache HTTP Server](/index.php/Apache_HTTP_Server "Apache HTTP Server") and [Apache HTTP Server#PHP](/index.php/Apache_HTTP_Server#PHP "Apache HTTP Server").

Install the [mythplugins-mythweb](https://www.archlinux.org/packages/?name=mythplugins-mythweb) package.

### Link to the Video Directory

MythWeb looks in the *video_dir* directory for *[MythTV](/index.php/MythTV "MythTV")* recordings. You will need to create a link to the folder where your MythTV recordings are stored.

```
# ln -s <recording_dir> /var/lib/mythtv/mythweb/video_dir

```

## Configuration

### MythWeb

Copy the MythWeb configuration file *mythweb.conf* to the [Apache](/index.php/Apache "Apache") configuration directory.

```
# cp /var/lib/mythtv/mythweb/mythweb.conf.apache /etc/httpd/conf/extra/mythweb.conf

```

And include it add the bottom of `/etc/httpd/conf/httpd.conf`:

```
Include conf/extra/mythweb.conf

```

If you want to use MythWeb with the recent default mythweb.conf options enabled you will also need to uncomment the following lines in httpd.conf:

```
LoadModule rewrite_module modules/mod_rewrite.so
LoadModule deflate_module modules/mod_deflate.so

```

Edit *mythweb.conf* to point it to the directory where you'll be installing mythweb (near the beginning of the file).

```
<Directory "/srv/http/mythweb/data">

```

```
<Directory "/srv/http/mythweb" >

```

Then check that the configuration matches your [MythTV](/index.php/MythTV "MythTV") setup. If you have changed the database login or password you will need to change the following section.

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
extension=mysqli.so

```

Make sure *open_basedir* contains */srv/http/* and */var/lib/mythtv/mythweb* to allow file operation in the MythWeb directory. Starting with MythTV 0.23, you will also need to permit access to */usr/share/mythtv/*.

```
open_basedir = /srv/http/:/home/:/tmp/:/usr/share/pear/:/var/lib/mythtv/mythweb:/usr/share/mythtv/

```

Enable the *allow_url_fopen* option for MythWeb's status page to work.

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

It is also probably a good idea to set up password protection for MythWeb if you intend to allow connections from the Internet. To enable authentication open the */etc/httpd/conf/extra/mythweb.conf* file and uncomment the authentication section (near the beginning):

```
AuthType           Digest
AuthName           "MythTV"
AuthUserFile       /var/www/htdigest
Require            valid-user
BrowserMatch       "MSIE"      AuthDigestEnableQueryStringHack=On
Order              allow,deny
Satisfy            any

```

Now we need to fix the configuration to match how we have MythWeb set up, change the *AuthUserFile* so it reads

```
AuthUserFile       /etc/httpd/conf/extra/httpd-passwords

```

If you do not want to access MythWeb from IE you can delete the BrowserMatch line.

You also probably do not want to have to enter your password when you're connecting from your local computer, so add the following line between the last two lines:

```
Allow from 127\. 192.168.1.

```

This will cause passwordless access from both your local machine **AND** your local network (provided you're using the 192.168.1.0 255.255.255.0 subnet)

Your config should now look something like:

```
AuthType           Digest
AuthName           "MythTV"
AuthUserFile       /etc/httpd/conf/extra/httpd-passwords
Require            valid-user
Order              allow,deny
Allow from 127\. 192.168.1.
Satisfy            any

```

Save the file. Now we'll create the httpd-passwords file,

```
# htdigest -c /etc/httpd/conf/extra/httpd-passwords MythTV MYUSER

```

Where MYUSER is the username you want to use to access MythWeb. Enter the login password when prompted.

If you need more users:

```
# htdigest /etc/httpd/conf/extra/httpd-passwords MythTV MYUSER

```

NOTE: No -c after initial user, otherwise you will overwrite the current file.

Now all we need to do now is restart the apache server for the changes to take effect.

```
# systemctl restart httpd.service

```

## Troubleshooting

If you get a 403 Forbidden error, recheck your paths in mythweb.conf

If you can't start the httpd service, and you get and error like this: journalctl -u httpd -xn ... AH00013: Pre-configuration failed ... Comment the line in httpd.conf: LoadModule mpm_event_module modules/mod_mpm_event.so

and use prefork module instead:

LoadModule mpm_prefork_module modules/mod_mpm_prefork.so

# External Links

*   [MythTV Wiki page on MythWeb](http://www.mythtv.org/wiki/MythWeb)