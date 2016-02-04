# RuTorrent

**[ruTorrent](https://github.com/Novik/ruTorrent)** is a web interface to [rTorrent](/index.php/RTorrent "RTorrent") (a console based BitTorrent client). It uses rTorrent's built-in XML-RPC server to communicate with it.

It is lightweight, highly extensible, and is designed to look similar to uTorrent.

## Contents

*   [1 Installation](#Installation)
*   [2 Web Server Configuration](#Web_Server_Configuration)
    *   [2.1 Apache](#Apache)
    *   [2.2 Nginx](#Nginx)
*   [3 ruTorrent Configuration](#ruTorrent_Configuration)
*   [4 See Also](#See_Also)
*   [5 External Links](#External_Links)

## Installation

Install [rutorrent](https://aur.archlinux.org/packages/rutorrent/) from the AUR.

## Web Server Configuration

### Apache

Install and configure Apache with PHP according to the [LAMP](/index.php/LAMP "LAMP") page.

*   Edit the _open_basedir_ value in /etc/php/php.ini to include:

```
/etc/webapps/rutorrent/conf/:/usr/share/webapps/rutorrent/php/:/usr/share/webapps/rutorrent/

```

Install [mod_scgi](https://aur.archlinux.org/packages/mod_scgi/) from the AUR.

*   Load the SCGI module in `/etc/httpd/conf/httpd.conf`:

```
LoadModule scgi_module modules/mod_scgi.so

```

*   Enable the rTorrent XMLRPC interface: [rTorrent#XMLRPC interface](/index.php/RTorrent#XMLRPC_interface "RTorrent")

*   Enable SCGI on the port you chose for rTorrent by adding this to `/etc/httpd/conf/httpd.conf`:

```
SCGIMount /RPC2 127.0.0.1:5000

```

*   Lastly, add the ruTorrent folder to `/etc/httpd/conf/httpd.conf` with something similar to this anywhere after the inital _</Directory>_:

```
<IfModule alias_module>
  Alias /rutorrent /usr/share/webapps/rutorrent
  <Directory "/usr/share/webapps/rutorrent">
    Order allow,deny
    Allow from all
  </Directory>
</IfModule>

```

For Apache 2.4 the access control would be:

```
<IfModule alias_module>
  Alias /rutorrent /usr/share/webapps/rutorrent
  <Directory "/usr/share/webapps/rutorrent">
    Require all granted
  </Directory>
</IfModule>

```

**Note:** You should enable authentication through Apache if your site is public.

### Nginx

*   Create a link from your web root to rutorrent

```
ln -s /usr/share/webapps/rutorrent/ /usr/share/nginx/html/rutorrent

```

*   Edit the _open_basedir_ value in /etc/php/php.ini to include:

```
/etc/webapps/rutorrent/conf/:/usr/share/webapps/rutorrent/php/:/usr/share/webapps/rutorrent/

```

*   Enable the rTorrent XMLRPC interface: [rTorrent#XMLRPC interface](/index.php/RTorrent#XMLRPC_interface "RTorrent")

*   Add following location to your nginx configuration:

```
           location /RPC2 {
               include scgi_params;
               scgi_pass localhost:5000;
           }

```

*   Restart nginx:

```
# systemctl restart nginx

```

*   You can now access ruTorrent at [http://127.0.0.1/rutorrent](http://127.0.0.1/rutorrent)

## ruTorrent Configuration

See upstream wiki [here](https://github.com/Novik/ruTorrent/wiki/Config).

## See Also

*   [LAMP](/index.php/LAMP "LAMP")
*   [RTorrent](/index.php/RTorrent "RTorrent")

## External Links

*   [https://github.com/Novik/ruTorrent/wiki](https://github.com/Novik/ruTorrent/wiki)
*   [http://httpd.apache.org/docs/2.2/configuring.html](http://httpd.apache.org/docs/2.2/configuring.html)

Retrieved from "[https://wiki.archlinux.org/index.php?title=RuTorrent&oldid=416557](https://wiki.archlinux.org/index.php?title=RuTorrent&oldid=416557)"