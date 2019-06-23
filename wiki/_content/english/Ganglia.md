[Ganglia](http://ganglia.sourceforge.net/) is a scalable distributed system monitor tool for high-performance computing systems such as clusters and grids. It allows the user to remotely view live or historical statistics (such as CPU load averages or network utilization) for all machines that are being monitored.

Ganglia is available as the [ganglia](https://aur.archlinux.org/packages/ganglia/) package on the [AUR](/index.php/AUR "AUR"), along with the web frontend [ganglia-web](https://aur.archlinux.org/packages/ganglia-web/). There is also a reduced-dependency version named [ganglia-minimal](https://aur.archlinux.org/packages/ganglia-minimal/), which would be appropriate on boxes where you don't require `gmetad` and want to avoid pulling in `rrdtool` as a dependency, which would in turn pull in Cairo and Mesa.

The [Ganglia Wiki](http://sourceforge.net/apps/trac/ganglia) contains all the information you need to get started with Ganglia.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Ganglia Web Interface](#Ganglia_Web_Interface)
    *   [1.1 Nginx with php-fpm](#Nginx_with_php-fpm)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Issues with IP-address binding or undesirable hostnames](#Issues_with_IP-address_binding_or_undesirable_hostnames)
*   [3 References](#References)

## Ganglia Web Interface

The ganglia web frontend is available as the [ganglia-web](https://aur.archlinux.org/packages/ganglia-web/) package on the AUR.

You will also need a [web server](/index.php/Web_server "Web server") with a working [PHP](/index.php/PHP "PHP") setup. The following sections include some example setups.

Make sure that the `open_basedir` setting in your `/etc/php/php.ini` includes `/tmp`, `/usr/share/webapps` and `/var/lib/ganglia`.

### Nginx with php-fpm

Firstly, install the required packages:

```
pacman -S nginx php-fpm

```

Secondly, read the [Nginx](/index.php/Nginx "Nginx") article. Note its [Nginx#FastCGI](/index.php/Nginx#FastCGI "Nginx") and subsequent php-fpm sections. [Nginx#Adding to main configuration](/index.php/Nginx#Adding_to_main_configuration "Nginx") details a minimum `nginx.conf` to use.

An older minimal configuration for nginx would be something like this:

 `/etc/nginx/nginx.conf` 
```
events {
  worker_connections  1024;
}

http {
  include mime.types;
  default_type application/octet-stream;

  upstream php {
    server unix:/run/php-fpm/php-fpm.sock;
  }

  server {
    listen 80 default_server;

    root /usr/share/webapps;
    index index.php;

    location ~ \.php$ {
      fastcgi_pass php;
      include fastcgi.conf;
    }
  }
}

```

Then start all required services:

```
systemctl start gmetad gmond php-fpm nginx

```

Go to [http://localhost/ganglia](http://localhost/ganglia) and check that your setup is working.

## Troubleshooting

### Issues with IP-address binding or undesirable hostnames

If `bind_hostname = yes` in the `udp_send_channel` section of `gmond.conf`, the `gmond` daemon will determine which **IP** to bind to (and report in the XML data) by determining the IP address of the default hostname. You should be able to replicate this behaviour with one of these commands:

```
$ hostname -i
$ host $(hostname)

```

The **hostname** to report is determined by asking the system to look up a hostname for the chosen IP address, in order to ensure the hostname is that by which other machines on the network identify the monitored machine:

```
$ host <ip-address>

```

The hostname listed at the top of the list is the one that will be reported by `gmond`, and will appear in the web UI. You can influence the returned hostname by modifying your `/etc/hosts` or `/etc/nsswitch.conf` files. In particular, watch out for placing `myhostname` before `dns` on the `hosts` line in `/etc/nsswitch.conf`. This will cause `gmond` to attempt to bind to a UDP port on 127.0.0.1, and it will fail to load.

If you're not able to achieve the desired behaviour, the hostname can be overridden in the `gmond.conf` file by adding the following lines to the `globals` section:

```
globals {
  ...
  override_hostname = myhostname.mydomain
  override_ip = 127.0.0.2
}
```

## References

*   E-mail exchange explaining IP and Hostname lookup: [http://www.mail-archive.com/ganglia-general@lists.sourceforge.net/msg01885.html](http://www.mail-archive.com/ganglia-general@lists.sourceforge.net/msg01885.html)