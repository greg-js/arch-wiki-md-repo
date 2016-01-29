# Groovebasin

[Groovebasin](http://groovebasin.com/) is a music player server with a web-based user interface.

Run it on a server connected to some speakers in your home or office. Guests can control the music player by connecting with a laptop, tablet, or smart phone. Further, you can stream your music library remotely.

Groove Basin works with your personal music library; not an external music service. Groove Basin will never support DRM content.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Start the Server](#Start_the_Server)
*   [4 Web Interface](#Web_Interface)
*   [5 NGINX Proxy](#NGINX_Proxy)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [nodejs-groovebasin](https://aur.archlinux.org/packages/nodejs-groovebasin/)<sup><small>AUR</small></sup> package from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

## Configuration

A config file is located in `/etc/groovebasin.json` you need to provide groovebasin with a config file or it will create a new one in the current directory named `config.json`.

## Start the Server

To start groovebasin as a regular user run

```
$ groovebasin --start

```

A unit file is also available to start groovebasin as root use:

```
# systemctl start groovebasin.service

```

## Web Interface

Open on your browser [https://localhost:16242/](https://localhost:16242/).

## NGINX Proxy

NGINX can be used to redirect traffic from port 16242 to 80 with the following configuration.

 `/etc/nginx/nginx.conf` 

```
location /groove/ {
        proxy_set_header    X-Real-IP  $remote_addr;
        proxy_set_header    X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header    Host $http_host;
        proxy_redirect      off;
        proxy_http_version  1.1;
        proxy_set_header    Upgrade $http_upgrade;
        proxy_set_header    Connection "upgrade";
        proxy_pass          [http://127.0.0.1:16242/](http://127.0.0.1:16242/);
}

```

## See also

*   [Groovebasin Official Website](http://groovebasin.com/)
*   [Github Repository](https://github.com/andrewrk/groovebasin)
*   [Screenshots](http://groovebasin.com/#screenshots)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Groovebasin&oldid=412092](https://wiki.archlinux.org/index.php?title=Groovebasin&oldid=412092)"