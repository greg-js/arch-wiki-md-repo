# Umap

[Umap](https://bitbucket.org/yohanboniface/umap) is an open-source web application based on the [Python](/index.php/Python "Python") framework [Django](/index.php/Django "Django"). It offers you to create OpenStreetMap-based maps where you can add own information and notes with a convenient web editor.

## Contents

*   [1 Server setup](#Server_setup)
    *   [1.1 Installation](#Installation)
    *   [1.2 Configuration](#Configuration)
    *   [1.3 Starting](#Starting)
*   [2 See also](#See_also)

## Server setup

### Installation

uMap can be [installed](/index.php/Installed "Installed") with the [umap](https://aur.archlinux.org/packages/umap/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/umap)]</sup> package. The preferred database back-end is [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") which is required in combination with the [postgis](https://www.archlinux.org/packages/?name=postgis) package.

### Configuration

Setup a postgresql database:

```
$ sudo -u postgres psql

```

```
postgres=# CREATE DATABASE umap;
CREATE DATABASE
postgres=# CREATE ROLE umap WITH PASSWORD 'umap' LOGIN;
CREATE ROLE
postgres=# GRANT ALL PRIVILEGES ON DATABASE umap to umap;
GRANT

```

Copy sample uMap configuration file:

```
# cp /usr/share/webapps/umap/umap/settings/local.py.sample /usr/share/webapps/umap/settings/local.py

```

You have to define a `SECRET_KEY` in the configuration file and define database connection settings:

 `/usr/share/webapps/umap/settings/local.py` 

```
SECRET_KEY = ''

DATABASES = {
    'default': {
        'ENGINE': 'django.contrib.gis.db.backends.postgis',
        'NAME': 'umap',
        'USER': 'umap',
        'PASSWORD': 'umap',
    }
}
```

Initialize uMap installation:

```
# python2 manage.py syncdb --migrate

```

### Starting

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `umap` service.

## See also

*   [Official documentation](https://bitbucket.org/yohanboniface/umap)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Umap&oldid=392756](https://wiki.archlinux.org/index.php?title=Umap&oldid=392756)"