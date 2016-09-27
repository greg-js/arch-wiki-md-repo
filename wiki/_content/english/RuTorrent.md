**[ruTorrent](https://github.com/Novik/ruTorrent)** is a web interface to [rTorrent](/index.php/RTorrent "RTorrent") (a console based BitTorrent client). It uses rTorrent's built-in XML-RPC server to communicate with it.

It is lightweight, highly extensible, and is designed to look similar to uTorrent.

## Contents

*   [1 Installation](#Installation)
*   [2 Web Server Configuration](#Web_Server_Configuration)
    *   [2.1 Apache](#Apache)
    *   [2.2 Nginx](#Nginx)
    *   [2.3 Nginx (manual installation)](#Nginx_.28manual_installation.29)
*   [3 ruTorrent Configuration](#ruTorrent_Configuration)
*   [4 See Also](#See_Also)
*   [5 External Links](#External_Links)

## Installation

Install [rutorrent](https://aur.archlinux.org/packages/rutorrent/) from the AUR. If you want to use the development version install [rutorrent-git](https://aur.archlinux.org/packages/rutorrent-git/).

## Web Server Configuration

### Apache

Install and configure Apache with PHP according to the [LAMP](/index.php/LAMP "LAMP") page.

*   Edit the *open_basedir* value in /etc/php/php.ini to include:

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

*   Lastly, add the ruTorrent folder to `/etc/httpd/conf/httpd.conf` with something similar to this anywhere after the inital *</Directory>*:

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

*   Edit the *open_basedir* value in /etc/php/php.ini to include:

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

### Nginx (manual installation)

*   Install nginx, php-fpm, rtorrent

*   Download and unpack [rutorrent](https://github.com/Novik/ruTorrent):

 `tree -L 2 /usr/share/nginx/html/` 
```
/usr/share/nginx/html/
├── 50x.html
├── index.html
└── rutorrent
    ├── conf
    ├── css
    ├── images
    ├── index.html
    ├── js
    ├── lang
    ├── LICENSE.md
    ├── php
    ├── plugins
    ├── README.md
    └── share

```

*   Modify premissions:

```
sudo chmod 0777 /usr/share/nginx/html/rutorrent/share/{settings,torrents,users}

```

*   Make necessary changes to rtorrent and nginx:

 `~/.rtorrent.rc` 
```
...
scgi_port = localhost:5000

```
 `/etc/nginx/nginx.conf` 
```
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
    server {
        listen       80;
        server_name  localhost;
        root /usr/share/nginx/html;
        location / {
            index  index.html index.htm;
        }
        location ~ \.php$ {
            fastcgi_pass   unix:/run/php-fpm/php-fpm.sock;
            fastcgi_index  index.php;
            include        fastcgi.conf;
        }
        location /RPC2 {
            include scgi_params;
            scgi_pass localhost:5000;
        }
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   /usr/share/nginx/html;
        }
    }
}

```

**Note:** *open_basedir* is unset by default and does not have to be changed.

*   Start necessary services:

```
sudo systemctl start php-fpm nginx

```

*   Consider using [rtorrent with tmux](https://wiki.archlinux.org/index.php/RTorrent#systemd_service_file_with_tmux_or_screen)
*   Navigate to [http://localhost/rutorrent/](http://localhost/rutorrent/)

## ruTorrent Configuration

See upstream wiki [here](https://github.com/Novik/ruTorrent/wiki/Config). By default the configuration files are symlinked to `/etc/webapps/rutorrent/conf`.

## See Also

*   [LAMP](/index.php/LAMP "LAMP")
*   [RTorrent](/index.php/RTorrent "RTorrent")

## External Links

*   [https://github.com/Novik/ruTorrent/wiki](https://github.com/Novik/ruTorrent/wiki)
*   [http://httpd.apache.org/docs/2.2/configuring.html](http://httpd.apache.org/docs/2.2/configuring.html)