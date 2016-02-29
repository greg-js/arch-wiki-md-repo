Uwsgi is a fast, self-healing and developer/sysadmin-friendly application container server coded in pure C.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting service](#Starting_service)
*   [3 Configuring](#Configuring)
    *   [3.1 Application configuration](#Application_configuration)
    *   [3.2 Php applications](#Php_applications)
        *   [3.2.1 Nginx configuration](#Nginx_configuration)
    *   [3.3 Nginx configuration (with chrooted Nginx)](#Nginx_configuration_.28with_chrooted_Nginx.29)
*   [4 See Also](#See_Also)

## Installation

[Install](/index.php/Install "Install") package [uwsgi](https://www.archlinux.org/packages/?name=uwsgi) in the [official repositories](/index.php/Official_repositories "Official repositories"). Note, the package does not come with plugins as it is just a compact package. External plugins have to be installed separately. It is a very efficient software due to the reason it is written in C. There are alternatives written in Python like gunicorn, but they are slower inherently.

## Starting service

**Note:** In the most simple configuration each application (i.e. python application) will get its own instance of uwsgi service.

Before uwsgi service can be enabled/started a configuration file with the same name must be created within `/etc/uwsgi/`

When reading following lines assume that `/etc/uwsgi/helloworld.ini` was created.

To enable the uwsgi service by default at start-up, run:

```
# systemctl enable uwsgi@helloworld

```

This will enable the service for the application configured in `/etc/uwsgi/helloworld.ini`. Otherwise, you can also enable it through the socket interface with the following command:

```
# systemctl enable uwsgi@helloworld.socket

```

Alternatively, you can run the [Emperor mode](http://uwsgi-docs.readthedocs.org/en/latest/Emperor.html) service. This mode enables a single uwsgi instance to run a bunch of different apps (called vassals) using a single main supervisor (called emperor). To enable it, type:

```
# systemctl enable emperor.uwsgi

```

You can also use the socket:

```
# systemctl enable emperor.uwsgi.socket

```

The configuration for this sits in `/etc/uwsgi/emperor.ini`.

## Configuring

**Note:** It seems /etc/uwsgi/archlinux.ini is not shipped with the standard install.

You can create a configuration by editing and putting that in `/etc/uwsgi/`. There is a build file shipped with the package located at `/etc/uwsgi/archlinux.ini`.

More details can be found [in the uwsgi documentation](http://uwsgi-docs.readthedocs.org/en/latest/).

**Note:** Please refer to the following resource for the full list of all options: [http://uwsgi-docs.readthedocs.org/en/latest/Options.html](http://uwsgi-docs.readthedocs.org/en/latest/Options.html)

##### Application configuration

The following is a simple example to get python support. You may need to install the uwsgi-plugin-python or uwsgi-plugin-python2 plugin from the community repository by pacman.

```
[uwsgi]
chdir = /srv/http/helloworld
module = helloworld
plugins = python

```

It is also possible to run uwsgi separately with the following syntax for instance:

**Note:** It seems --wsgi-file option is not available from uwsgi installed through pacman. Official guides suggest building from sources (see [http://uwsgi-docs.readthedocs.org/en/latest/WSGIquickstart.html#installing-uwsgi-with-python-support](http://uwsgi-docs.readthedocs.org/en/latest/WSGIquickstart.html#installing-uwsgi-with-python-support)).

```
uwsgi --socket 127.0.0.1:3031 --plugin python2 --wsgi-file ~/foo.py --master --processes 4 --threads 2 --stats 127.0.0.1:9191 --uid --gid

```

Note, you should avoid running this command as root.

#### Php applications

Install the php plugin for uwsgi: [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php)

 `/etc/uwsgi/mysite.ini` 
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

Nginx configuration

```
location = /index.php {
    include uwsgi_params;
    uwsgi_modifier1 14;
    uwsgi_pass unix:/run/uwsgi/mysite.sock;
}

```

##### Nginx configuration

```
location / {
    root   /usr/share/nginx/html;
    index  index.html index.htm;
    include uwsgi_params;
    # uwsgi_pass unix:/var/run/uwsgi/helloworld.sock;
    uwsgi_pass 127.0.0.1:3031;
}

```

#### Nginx configuration (with chrooted Nginx)

**Note:** Please refer to the below tips if you have deployed Nginx as described here: [Nginx#Installation in a chroot](/index.php/Nginx#Installation_in_a_chroot "Nginx")

**Note:** It is assumed your Nginx chroot is located within `/srv/http`

**Note:** You will most likely want to read through uwsgi documentation to understand your configuration from both performance and security point of view

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

Once modified run:

```
# systemctl daemon-reload

```

Enable your service:

```
# systemctl enable uwsgi@application1

```

Start the service:

```
# systemctl start uwsgi@application1

```

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

Restart nginx

```
# systemctl restart nginx

```

At this point your application should be served, issue `127.0.0.1` on your browser.

## See Also

*   [Official Documentation](http://uwsgi-docs.readthedocs.org/en/latest)
*   [UWsgi Github](https://github.com/unbit/uwsgi-docs)
*   [Fluffy White Stuff Benchmark](http://blog.kgriffs.com/)
*   [Flask uwsgi deploying](http://flask.pocoo.org/docs/deploying/uwsgi/)
*   [Django and uWSGI](https://docs.djangoproject.com/en/dev/howto/deployment/wsgi/uwsgi/)
*   [Flask with uwsgi and nginx video](http://www.youtube.com/watch?v=tD6UCfPCVLA)
*   [Apache and uwsgi](http://uwsgi-docs.readthedocs.org/en/latest/Apache.html)