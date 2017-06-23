uWSGI is a fast, self-healing and developer/sysadmin-friendly application container server coded in pure C.

There are alternatives written in Python such as [gunicorn](https://aur.archlinux.org/packages/gunicorn/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Web applications](#Web_applications)
        *   [2.1.1 Python](#Python)
        *   [2.1.2 PHP](#PHP)
    *   [2.2 Web server](#Web_server)
        *   [2.2.1 Nginx](#Nginx)
        *   [2.2.2 Nginx (in chroot)](#Nginx_.28in_chroot.29)
*   [3 Running uWSGI](#Running_uWSGI)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Socket activation](#Socket_activation)
    *   [4.2 Hardening uWSGI](#Hardening_uWSGI)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the package [uwsgi](https://www.archlinux.org/packages/?name=uwsgi) from the [official repositories](/index.php/Official_repositories "Official repositories"). Note, that the package does not come with plugins. They have to be installed separately:

*   [uwsgi-plugin-cgi](https://www.archlinux.org/packages/?name=uwsgi-plugin-cgi) for CGI support
*   [uwsgi-plugin-jvm](https://www.archlinux.org/packages/?name=uwsgi-plugin-jvm) for [Java](/index.php/Java "Java") support
*   [uwsgi-plugin-lua51](https://www.archlinux.org/packages/?name=uwsgi-plugin-lua51) for Lua support
*   [uwsgi-plugin-mono](https://www.archlinux.org/packages/?name=uwsgi-plugin-mono) for [Mono](/index.php/Mono "Mono") support
*   [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php) for [PHP](/index.php/PHP "PHP") support
*   [uwsgi-plugin-psgi](https://www.archlinux.org/packages/?name=uwsgi-plugin-psgi) for Perl support
*   [uwsgi-plugin-pypy](https://www.archlinux.org/packages/?name=uwsgi-plugin-pypy) for [PyPy](/index.php/PyPy "PyPy") support
*   [uwsgi-plugin-python](https://www.archlinux.org/packages/?name=uwsgi-plugin-python) for [Python](/index.php/Python "Python") support
*   [uwsgi-plugin-python2](https://www.archlinux.org/packages/?name=uwsgi-plugin-python2) for Python2 support
*   [uwsgi-plugin-rack](https://www.archlinux.org/packages/?name=uwsgi-plugin-rack) for [Ruby](/index.php/Ruby "Ruby") Rack support
*   [uwsgi-plugin-webdav](https://www.archlinux.org/packages/?name=uwsgi-plugin-webdav) for [WebDAV](/index.php/WebDAV "WebDAV") support

## Configuration

Web applications (e.g. [Wordpress](/index.php/Wordpress "Wordpress"), [ownCloud](/index.php/OwnCloud "OwnCloud"), [Mailman](/index.php/Mailman "Mailman"), [cgit](/index.php/Cgit "Cgit")) served by uWSGI are configured in `/etc/uwsgi/`, where each of them requires its own configuration file (ini-style). Details can be found [in the uWSGI documentation](http://uwsgi-docs.readthedocs.org/en/latest/).

Alternatively, you can run uWSGI in [Emperor mode](http://uwsgi-docs.readthedocs.org/en/latest/Emperor.html) (configured in `/etc/uwsgi/emperor.ini`). It enables a single uWSGI instance to run a set of different apps (called vassals) using a single main supervisor (called emperor).

### Web applications

uWSGI supports many different languages and thus also many web applications. As an example the configuration file `/etc/uwsgi/example.ini` and the prior installation of the plugin needed for your web application is assumed. For further common configuration examples, have a look at this [blog post](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/).

#### Python

The following is a simple example for a [Python](/index.php/Python "Python") application.

 `/etc/uwsgi/example.ini` 
```
[uwsgi]
 chdir = /srv/http/example
 module = example
 plugins = python
```

It is also possible to run uWSGI separately with the following syntax for instance:

**Note:** It seems --wsgi-file option is not available from [uwsgi](https://www.archlinux.org/packages/?name=uwsgi). Official guides suggest building from source. [[1]](http://uwsgi-docs.readthedocs.org/en/latest/WSGIquickstart.html#installing-uwsgi-with-python-support)

```
$ uwsgi --socket 127.0.0.1:3031 --plugin python2 --wsgi-file ~/foo.py --master --processes 4 --threads 2 --stats 127.0.0.1:9191 --uid --gid

```

You should avoid running this command as root.

**Note:** Pay attention to operational mode in use, preforking without --lazy-apps may cause non-obvious behavior. By default the Python plugin does not initialize the GIL. This means your app-generated threads will not run. If you need threads, remember to enable them with enable-threads. Running uWSGI in multithreading mode (with the threads options) will automatically enable threading support. This "strange" default behaviour is for performance reasons, no shame in that. [[2]](https://uwsgi-docs.readthedocs.io/en/latest/ThingsToKnow.html)

#### PHP

The following is a simple example for a [PHP](/index.php/PHP "PHP") based website.

 `/etc/uwsgi/example.ini` 
```
[uwsgi]
; maximum number of worker processes
processes = 4
; the user and group id of the process once it’s started
uid = http
gid = http
socket = /run/uwsgi/%n.sock
master = true
chdir = /srv/http/%n
; php
plugins = php
; jail our php environment
php-docroot = /srv/http/%n
php-index = index.php
; clear environment on exit
vacuum = true
```

### Web server

uWSGI can be the backend to many web servers, that support the forwarding of access. The following are examples for configurations.

#### Nginx

[nginx](/index.php/Nginx "Nginx") can redirect access towards unix sockets or ports (on localhost or remote machine), depending on your web application.

 `/etc/nginx/example.conf` 
```
# ...
# forward all access to / towards 
location / {
  root /usr/share/nginx/html;
  index index.html index.htm;
  include uwsgi_params;
  # this is the correct uwsgi_modifier1 parameter for a php based application
  uwsgi_modifier1 14;
  # uncomment the following if you want to use the unix socket instead
  # uwsgi_pass unix:/var/run/uwsgi/example.sock;
  # access is redirected to localhost:3031
  uwsgi_pass 127.0.0.1:3031;
}
# ...

```

**Tip:** Have a look at [the documentation](https://uwsgi-docs.readthedocs.io/en/latest/Protocol.html#packet-descriptions) for the list of `uwsgi_modifier1` parameters fitting to your web application.

#### Nginx (in chroot)

**Note:** Please refer to the below tips if you have deployed Nginx as described here: [Nginx#Installation in a chroot](/index.php/Nginx#Installation_in_a_chroot "Nginx")

**Note:** It is assumed your Nginx chroot is located within `/srv/http`

**Note:** You will most likely want to read through uWSGI documentation to understand your configuration from both performance and security point of view

First create ini file that will point to your application:

 `/etc/uwsgi/application1.ini` 
```
[uwsgi]
chroot = /srv/http
chdir = /www/application1
wsgi-file = application1.py
plugins = python
socket = /run/application1.sock
uid = http
gid = http
threads = 2
stats = 127.0.0.1:9191
vacuum = true

```

Since we are chrooting to `/srv/http` above configuration will result in following unix socket being created `/srv/http/run/application1.sock`

**Note:** Your application must be placed within `/srv/http/www/application1` before service is started. Depending on configuration your application may be cached so you may need to restart the service when you modify it

**Note:** If you are deploying python application you may need to copy standard python libraries - if you develop under python 3 then you can copy them from `/lib/python3.4` to `/srv/http/lib/python3.4`

You can try to run following:

```
# cp -r -p /lib/python3.4 /srv/http/lib
# cp -r -p /lib/*python*so /srv/http/lib

```

You will need to disable notifications within your service file:

 `/etc/systemd/system/multi-user.target.wants/uwsgi\@application1.service` 
```
[Unit]
Description=uWSGI service unit
After=syslog.target

[Service]
PIDFile=/run/%I.pid
RemainAfterExit=yes
ExecStart=/usr/bin/uwsgi --ini /etc/uwsgi/%I.ini
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -INT $MAINPID
Restart=always
StandardError=syslog
KillSignal=SIGQUIT

[Install]
WantedBy=multi-user.target

```

**Note:** PID file will be created within `/run` rather than `/srv/http/run`

After modification make sure to [reload](/index.php/Reload "Reload") to incorporate the new or changed units.

You are then free to [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") `uwsgi@application1.service`.

Edit `/srv/http/etc/nginx/nginx.conf` and add new `server` section within it that would contain at least following:

 `/srv/http/etc/nginx/nginx.conf` 
```
...
    server
    {
        listen       80;
        server_name  127.0.0.1;
        location /
        {
            root   /www/application1;
            include uwsgi_params;
            uwsgi_pass unix:/run/application1.sock;
        }

        error_page   500 502 503 504  /50x.html;
        location = /50x.html
        {
            root   /usr/share/nginx/html;
        }
    }
...

```

Make sure to now [restart](/index.php/Restart "Restart") `nginx.service` to have your `application1` be served at `127.0.0.1`.

## Running uWSGI

**Note:** This assumes the used web application has been properly configured, is being served by your web server, which redirects towards the socket or port it is using and was configured in `/etc/uwsgi/`.

If you plan on using a web application all the time (without it being activated on demand), you can simply [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `uwsgi@example`.

If you plan on having your web application be started on demand you can [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `uwsgi@example.socket`.

To use the Emperor mode, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `emperor.uwsgi.service`.

To use socket activation of this mode [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `emperor.uwsgi.socket`.

## Tips and tricks

Some functionality, that uWSGI offers is not accessible by using the [systemd](/index.php/Systemd "Systemd") service files provided in the [official repositories](/index.php/Official_repositories "Official repositories"). Changes to them are explained in the following sections. For further information about this, [read this blog post](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/).

### Socket activation

Using socket activation, you want to

*   direct your web server to a unix socket and thereby start your uWSGI instance running the application
*   you most likely want to have the application be closed by uWSGI after a certain idle time
*   you want your web server be able to start the application again, once it is accessed

uWSGI offers settings, with which you can have the instance close the application:

 `/etc/uwsgi/example.ini` 
```
[uwsgi]
# ...

# set idle time in seconds
idle = 600
# kill the application after idle time was reached
kill-on-idle = true

# ...

```

The current `uwsgi@.service` file however doesn't allow this, because [systemd](/index.php/Systemd "Systemd") treats non-zero exit codes as failure and thereby marking the unit as failed and additionally the `Restart=always` directive makes a closing after idle time useless. A fix for this is to add the exit codes, that uWSGI may provide after closing an application by itself to a list, that [systemd](/index.php/Systemd "Systemd") will treat as success by using the `SuccessExitStatus` directive (for further information [read this blog post](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/))

 `/etc/systemd/system/uwsgi-socket@.service` 
```
[Unit]
Description=uWSGI service unit
After=syslog.target

[Service]
ExecStart=/usr/bin/uwsgi --ini /etc/uwsgi/%I.ini
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -INT $MAINPID
Type=notify
SuccessExitStatus=15 17 29 30
StandardError=syslog
NotifyAccess=all
KillSignal=SIGQUIT

[Install]
WantedBy=multi-user.target

```

This will allow for proper socket activation with kill-after-idle functionality.

### Hardening uWSGI

Web applications are exposed to the wild and depending on their quality and the security of their underlying languages, some are more dangerous to run, than others. A good way to start dealing with possible unsafe web applications is to jail them. [systemd](/index.php/Systemd "Systemd") has some functionality, that can be put to use. Have a look at the following example (and for further information read the [systemd.exec manual](https://www.freedesktop.org/software/systemd/man/systemd.exec.html) and [this blog post](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/)):

 `/etc/systemd/system/uwsgi-secure@.service` 
```
[Unit]
Description=uWSGI service unit
After=syslog.target

[Service]
ExecStart=/usr/bin/uwsgi --ini /etc/uwsgi/%I.ini
ExecReload=/bin/kill -HUP $MAINPID
ExecStop=/bin/kill -INT $MAINPID
Type=notify
SuccessExitStatus=15 17 29 30
StandardError=syslog
NotifyAccess=all
KillSignal=SIGQUIT
PrivateDevices=yes
PrivateTmp=yes
ProtectSystem=full
ReadWriteDirectories=/etc/webapps /var/lib/
ProtectHome=yes
NoNewPrivileges=yes

[Install]
WantedBy=multi-user.target

```

**Note:** Using `NoNewPrivileges=yes` doesn't work with [Mailman](/index.php/Mailman "Mailman")'s cgi frontend! Remove this setting, if you want to use it in conjunction with it.

**Note:** If you want to harden your uWSGI app further, the use of namespaces is advisable. You can get a first glance on that topic in the [uWSGI namespaces documentation](http://uwsgi-docs.readthedocs.io/en/latest/Namespaces.html).

## See also

*   [Official Documentation](http://uwsgi-docs.readthedocs.org/en/latest)
*   [uWSGI Github](https://github.com/unbit/uwsgi-docs)
*   [Securely serving webapps using uWSGI](https://sleepmap.de/2016/securely-serving-webapps-using-uwsgi/)
*   [Fluffy White Stuff Benchmark](http://blog.kgriffs.com/)
*   [Flask uWSGI deploying](http://flask.pocoo.org/docs/deploying/uwsgi/)
*   [Django and uWSGI](https://docs.djangoproject.com/en/dev/howto/deployment/wsgi/uwsgi/)
*   [Apache and uWSGI](http://uwsgi-docs.readthedocs.org/en/latest/Apache.html)