# mod_wsgi

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Introduction](#Introduction)
*   [2 Installation](#Installation)
*   [3 Apache configuration](#Apache_configuration)
*   [4 Module test](#Module_test)
*   [5 See Also](#See_Also)

## Introduction

According to the [project's site](http://code.google.com/p/modwsgi/) :

The aim of mod_wsgi is to implement a simple to use Apache module which can host any Python application which supports the Python WSGI interface. The module would be suitable for use in hosting high performance production web sites, as well as your average self managed personal sites running on web hosting services.

mod_wsgi is an [Apache](/index.php/Apache "Apache") module that embeds a [Python](http://www.python.org) application within the server and allow them to communicate through the Python WSGI interface as defined in the [Python PEP 333](http://www.python.org/dev/peps/pep-0333/). WSGI is one of the Python ways to produce high quality and high performance web applications.

WSGI provide a standard way to interface different web-apps without hassle. Several well-know python applications or frameworks provide wsgi for easy deployment and embedding. It means that you can embed your Django-powered blog and your project's Trac into a single Pylons application that wraps around them to deals with, say, authentication without modifying the formers.

Example:

*   [Pylons](http://www.pylonsproject.org/)
*   [Django](http://www.djangoproject.com/)
*   [Turbo-gear](http://turbogears.org/)
*   [Trac](http://trac.edgewall.org/)
*   [Moin-moin](http://moinmo.in/)
*   [Zope](http://www.zope.org/)

## Installation

Two packages are present in community :

*   **[mod_wsgi](https://www.archlinux.org/packages/?name=mod_wsgi)** provide the module works with all common versions of Python (2.x and 3.x)
*   **[mod_wsgi2](https://www.archlinux.org/packages/?name=mod_wsgi2)** provide the module can only run with 2.x versions of Python

To install the package with pacman :

```
pacman -S mod_wsgi

```

or

```
pacman -S mod_wsgi2

```

## Apache configuration

*   As indicated during installation, add the following line to the configuration file of Apache :

 `/etc/httpd/conf/httpd.conf`  `LoadModule wsgi_module modules/mod_wsgi.so` 

*   Restart Apache :

```
systemctl restart httpd

```

*   Check that Apache is running properly

If the previous command returned nothing, It's that the launch of Apache went well. Otherwise, you can see errors with the following command :

```
systemctl -l status httpd.service

```

## Module test

*   Add this line in Apache configuration file :

 `/etc/httpd/conf/httpd.conf`  `WSGIScriptAlias /wsgi_app /srv/http/wsgi_app.py` 

*   Create a test file :

 `/srv/http/wsgi_app.py` 

```
#-*- coding: utf-8 -*-
def wsgi_app(environ, start_response):
    import sys
    output = sys.version.encode('utf8')
    status = '200 OK'
    headers = [('Content-type', 'text/plain'),
               ('Content-Length', str(len(output)))]
    start_response(status, headers)
    yield output

# mod_wsgi need the *application* variable to serve our small app
application = wsgi_app
```

*   Restart Apache :

```
systemctl restart httpd

```

*   You can check the proper functioning by going to the following address : [http://localhost/wsgi_app](http://localhost/wsgi_app)

## See Also

*   [LAMP](/index.php/LAMP "LAMP")
*   [mod_wsgi project's site](http://code.google.com/p/modwsgi/)
*   [Quick Configuration Guide](http://code.google.com/p/modwsgi/wiki/QuickConfigurationGuide)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mod_wsgi&oldid=388040](https://wiki.archlinux.org/index.php?title=Mod_wsgi&oldid=388040)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Web server](/index.php/Category:Web_server "Category:Web server")