[Postorius](https://gitlab.com/mailman/postorius) is a [Django](/index.php/Django "Django") based management interface for [Mailman](/index.php/Mailman "Mailman")3.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Hosting](#Hosting)
    *   [3.1 Nginx and uWSGI](#Nginx_and_uWSGI)
*   [4 Setup](#Setup)
*   [5 See also](#See_also)

## Installation

To use Postorius, a working [web server](/index.php/Web_server "Web server") setup is required (e.g. using [Apache](/index.php/Apache "Apache") to forward to the [WSGI](https://en.wikipedia.org/wiki/Wsgi "wikipedia:Wsgi") directly, or using [Nginx](/index.php/Nginx "Nginx") forwarding requests to an application server such as [UWSGI](/index.php/UWSGI "UWSGI")).

[Install](/index.php/Install "Install") the [postorius](https://www.archlinux.org/packages/?name=postorius) package.

**Warning:** Postorius should only be accessed over [TLS](/index.php/TLS "TLS") (unless only accessed directly from the machine running it for testing purposes), as it otherwise exposes passwords and user data to the network.

## Configuration

The web application is configured in `/etc/webapps/postorius/settings.py`.

**Note:** Postorius should store user sensitive data (e.g. sqlite database) in `/var/lib/postorius/data`, as that directory is only accessible by root and the application itself.

Change the default secret for the application:

 `/etc/webapps/postorius/settings.py` 
```
SECRET_KEY = 'something-very-secret'

```

Make sure to disable debugging when running in production:

 `/etc/webapps/postorius/settings.py` 
```
DEBUG = False

```

Add a valid email configuration (so that the [Django](/index.php/Django "Django") application can verify subscribers):

 `/etc/webapps/postorius/settings.py` 
```
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'localhost'
EMAIL_PORT = 25
EMAIL_HOST_USER = <username>
EMAIL_HOST_PASSWORD = <password>

```

**Note:** The `DEFAULT_FROM_MAIL` and `SERVER_MAIL` configuration options can be used to define the `From:` header of mails sent for internal authentication and error reporting (respectively).

The valid hosts or domain names for the application need to be defined:

 `/etc/webapps/postorius/settings.py` 
```
ALLOWED_HOSTS = [
    'localhost',
    'lists.example.com'
]

```

## Hosting

**Note:** Postorius needs to be run as its own user and group (i.e. `postorius`). It's using `/etc/webapps/postorius`, `/var/lib/postorius` and `/run/postorius` for configurations, static caches and (potentially) sockets (respectively)!

### Nginx and uWSGI

Postorius comes with a working [uWSGI](/index.php/UWSGI "UWSGI") configuration file in `/etc/uwsgi/postorius.ini`.

[Install](/index.php/Install "Install") [nginx](https://www.archlinux.org/packages/?name=nginx) and [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php), create a per-application socket for [uWSGI](/index.php/UWSGI "UWSGI") (see [UWSGI#Accessibility of uWSGI socket](/index.php/UWSGI#Accessibility_of_uWSGI_socket "UWSGI") for reference) and [activate](/index.php/Systemd#Using_units "Systemd") the `uwsgi-secure@postorius.socket` unit.

For a local test setup, serving Postorius at [http://127.0.0.1:80/postorius](http://127.0.0.1:80/postorius) add the following [Nginx](/index.php/Nginx "Nginx") configuration to your setup:

 `/etc/nginx/postorius.conf` 
```
server {
  listen 80;
  server_name localhost;
  charset utf-8;
  client_max_body_size 75M;
  access_log /var/log/nginx/access.postorius.log;
  error_log /var/log/nginx/error.postorius.log;

  location /static {
    alias /usr/share/webapps/postorius/static;
  }

  location /postorius {
    include /etc/nginx/uwsgi_params;
    uwsgi_pass unix:/run/postorius/postorius.sock;
  }

  location /accounts/login {
    include /etc/nginx/uwsgi_params;
    uwsgi_pass unix:/run/postorius/postorius.sock;
  }

  location /accounts/signup {
    include /etc/nginx/uwsgi_params;
    uwsgi_pass unix:/run/postorius/postorius.sock;
  }
}

```

## Setup

After first installation make sure to generate a database:

```
$ sudo -u postorius django-admin migrate --pythonpath /usr/share/webapps/postorius/ --settings settings

```

Afterwards, the static data for the application needs to be collected:

```
$ sudo -u postorius django-admin collectstatic --pythonpath /usr/share/webapps/postorius/ --settings settings

```

## See also

*   [Postorius Documentation](https://postorius.readthedocs.io/en/latest/) - The upstream documentation
*   [Mailman Suite Documentation](https://docs.mailman3.org/en/latest/) - The (high level) upstream documentation for the entire Mailman Suite (Mailman, Hyperkitty and Postorius)