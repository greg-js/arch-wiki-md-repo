[KiwiIRC](https://kiwiirc.com) is a hand-crafted IRC client that you can enjoy. Designed to be used easily and freely.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Running](#Running)
    *   [2.1 Apache](#Apache)
    *   [2.2 Lighttpd](#Lighttpd)

## Installation

[Install](/index.php/Install "Install") the [kiwiirc](https://aur.archlinux.org/packages/kiwiirc/) package.

## Running

### Apache

Create the Apache configuration file:

 `/etc/httpd/conf/extra/kiwiirc.conf` 
```
Alias /kiwiirc "/usr/share/webapps/kiwiirc"
<Directory "/usr/share/webapps/kiwiirc">
    AllowOverride All
    Options FollowSymlinks
    Require all granted
</Directory>
```

And include it in `/etc/httpd/conf/httpd.conf`:

```
# kiwiirc configuration
Include conf/extra/kiwiirc.conf

```

After making changes to the Apache configuration file, [restart](/index.php/Restart "Restart") `httpd.service`.

### Lighttpd

Configuring [Lighttpd](/index.php/Lighttpd "Lighttpd"), make sure `mod_alias` has been enabled.

Add the following alias for kiwiirc to the config:

```
 alias.url = ( "/kiwiirc" => "/usr/share/webapps/kiwiirc/")

```