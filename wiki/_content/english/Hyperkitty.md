[Hyperkitty](https://gitlab.com/mailman/hyperkitty) is a [Django](/index.php/Django "Django") based archiver and archive interface for [Mailman](/index.php/Mailman "Mailman") 3.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Hosting](#Hosting)
    *   [3.1 Nginx and uWSGI](#Nginx_and_uWSGI)
*   [4 Setup](#Setup)
*   [5 Tips and tricks](#Tips_and_tricks)
    *   [5.1 Importing mailman2 archives](#Importing_mailman2_archives)
    *   [5.2 Disabling Gravatar support](#Disabling_Gravatar_support)
    *   [5.3 Saving mail attachments to disk](#Saving_mail_attachments_to_disk)
    *   [5.4 Template customization](#Template_customization)
    *   [5.5 Xapian search backend](#Xapian_search_backend)
*   [6 See also](#See_also)

## Installation

To use Hyperkitty, a working [web server](/index.php/Web_server "Web server") setup is required (e.g. using [Apache](/index.php/Apache "Apache") to forward to the [WSGI](https://en.wikipedia.org/wiki/Wsgi) directly, or using [Nginx](/index.php/Nginx "Nginx") forwarding requests to an application server such as [UWSGI](/index.php/UWSGI "UWSGI")).

[Install](/index.php/Install "Install") the [hyperkitty](https://www.archlinux.org/packages/?name=hyperkitty) package.

**Warning:** Hyperkitty should only be accessed over [TLS](/index.php/TLS "TLS") (unless only accessed directly from the machine running it for testing purposes), as it otherwise exposes passwords and user data to the network.

## Configuration

The web application is configured in `/etc/webapps/hyperkitty/settings.py`.

**Note:** Hyperkitty should store user sensitive data (e.g. sqlite database) in `/var/lib/hyperkitty/data`, as that directory is only accessible by root and the application itself.

Change the default secret for the application:

 `/etc/webapps/hyperkitty/settings.py` 
```
SECRET_KEY = 'something-very-secret'

```

Make sure to disable debugging when running in production:

 `/etc/webapps/hyperkitty/settings.py` 
```
DEBUG = False

```

Add a valid email configuration (so that the [Django](/index.php/Django "Django") application can verify subscribers):

 `/etc/webapps/hyperkitty/settings.py` 
```
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'localhost'
EMAIL_PORT = 25
EMAIL_HOST_USER = <username>
EMAIL_HOST_PASSWORD = <password>

```

**Note:** The `DEFAULT_FROM_MAIL` and `SERVER_MAIL` configuration options can be used to define the `From:` header of mails sent for internal authentication and error reporting (respectively).

The valid hosts or domain names for the application need to be defined:

 `/etc/webapps/hyperkitty/settings.py` 
```
ALLOWED_HOSTS = [
    'localhost',
    'lists.example.com'
]

```

## Hosting

**Note:** Hyperkitty needs to be run as its own user and group (i.e. `hyperkitty`). It's using `/etc/webapps/hyperkitty`, `/var/lib/hyperkitty` and `/run/hyperkitty` for configurations, static caches and (potentially) sockets (respectively)!

### Nginx and uWSGI

Postorius comes with a working [uWSGI](/index.php/UWSGI "UWSGI") configuration file in `/etc/uwsgi/hyperkitty.ini`.

[Install](/index.php/Install "Install") [nginx](https://www.archlinux.org/packages/?name=nginx) and [uwsgi-plugin-php](https://www.archlinux.org/packages/?name=uwsgi-plugin-php), create a per-application socket for [uWSGI](/index.php/UWSGI "UWSGI") (see [UWSGI#Accessibility of uWSGI socket](/index.php/UWSGI#Accessibility_of_uWSGI_socket "UWSGI") for reference) and [activate](/index.php/Systemd#Using_units "Systemd") the `uwsgi-secure@hyperkitty.socket` unit.

For a local test setup, serving Hyperkitty at [http://127.0.0.1:80/hyperkitty](http://127.0.0.1:80/hyperkitty) add the following [Nginx](/index.php/Nginx "Nginx") configuration to your setup:

 `/etc/nginx/hyperkitty.conf` 
```
server {
  listen 80;
  server_name localhost;
  charset utf-8;
  client_max_body_size 75M;
  access_log /var/log/nginx/access.hyperkitty.log;
  error_log /var/log/nginx/error.hyperkitty.log;

  location ~^/static/(.*)$ {
    alias /usr/share/webapps/hyperkitty/static;
  }

  location ~^/(accounts|admin|hyperkitty)/(.*)$ {
    include /etc/nginx/uwsgi_params;
    uwsgi_pass unix:/run/hyperkitty/hyperkitty.sock;
  }
}

```

## Setup

After first installation make sure to generate a database:

```
$ sudo -u hyperkitty django-admin migrate --pythonpath /usr/share/webapps/hyperkitty/ --settings settings

```

Afterwards, the static data for the application needs to be collected:

```
$ sudo -u hyperkitty django-admin collectstatic --pythonpath /usr/share/webapps/hyperkitty/ --settings settings

```

To compress the data, run the following:

```
$ sudo -u hyperkitty django-admin compress --pythonpath /usr/share/webapps/hyperkitty/ --settings settings

```

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `hyperkitty-qcluster.service` [systemd](/index.php/Systemd "Systemd") service for required asynchronous operations on the web application.

Populate the database with default data (when setting up for the first time):

```
$ sudo -u hyperkitty django-admin loaddata --pythonpath /usr/share/webapps/hyperkitty/ --settings settings first_start

```

Create a superuser account for the [Django](/index.php/Django "Django") application:

```
$ sudo -u hyperkitty django-admin createsuperuser --pythonpath /usr/share/webapps/hyperkitty --settings settings

```

## Tips and tricks

### Importing mailman2 archives

Hyperkitty can import archives from mailman < 3.0:

```
$ sudo -u hyperkitty django-admin hyperkitty_import --pythonpath /usr/share/webapps/hyperkitty --settings settings -l ADDRESS mbox_file [mbox_file ...]

```

Here `ADDRESS` is the fully-qualified list name (e.g. *list@example.com*) and the `mbox_file` argument represents existing archives (in mbox format) to import (usually found in `/var/lib/mailman/archives/private/LIST_NAME.mbox/LIST_NAME.mbox`).

Afterwards the full-text search index can be updated manually:

```
$ sudo -u hyperkitty django-admin update_index_one_list --pythonpath /usr/share/webapps/hyperkitty --settings settings ADDRESS

```

**Note:** The full-text search index should be created by the minutely running cron-job automatically.

### Disabling Gravatar support

The builtin gravatar support can be disabled in the configuration:

 `/etc/webapps/hyperkitty/settings.py` 
```
GRAVATAR_SECURE_URL = ''

```

### Saving mail attachments to disk

By default Hyperkitty stores mail attachments in its database. However, it can be configured to save the attachments to disk instead:

 `/etc/webapps/hyperkitty/settings.py` 
```
HYPERKITTY_ATTACHMENT_FOLDER = /var/lib/hyperkitty/data/attachments

```

**Note:** The location needs to be accessible and writable by the `hyperkitty` user!

### Template customization

Using [Django](/index.php/Django "Django")'s [TEMPLATES-DIRS](https://docs.djangoproject.com/en/3.0/ref/settings/#std:setting-TEMPLATES-DIRS) capabilities, it's possible to override the following templates to change the looks of the application:

*   `hyperkitty/headers.html`: the content will appear before the `</head>` tag
*   `hyperkitty/top.html`: the content will appear before the `<body>` tag
*   `hyperkitty/bottom.html`: the content will appear before the `</body>` tag

### Xapian search backend

Hyperkitty can make use of a Xapian based search backend. [Install](/index.php/Install "Install") the [python-xapian-haystack](https://www.archlinux.org/packages/?name=python-xapian-haystack) package and configure the backend:

 `/etc/webapps/hyperkitty/settings.py` 
```
HAYSTACK_CONNECTIONS = {
    'default': {
        'ENGINE': 'xapian_backend.XapianEngine',
        'PATH': "/var/lib/hyperkitty/data/xapian_index",
    },
}

```

Make sure to create the search index for all lists afterwards:

```
$ sudo -u hyperkitty django-admin update_index --pythonpath /usr/share/webapps/hyperkitty --settings settings

```

## See also

*   [Hyperkitty Documentation](https://hyperkitty.readthedocs.io/en/latest/) - The upstream documentation
*   [Mailman Suite Documentation](https://docs.mailman3.org/en/latest/) - The (high level) upstream documentation for the entire Mailman Suite (Mailman, Hyperkitty and Postorius)