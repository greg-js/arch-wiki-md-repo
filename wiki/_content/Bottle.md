# Bottle

From [Bottle: Python Web Framework](http://bottlepy.org/docs/dev/):

	_Bottle is a fast, simple and lightweight WSGI micro web-framework for Python. It is distributed as a single file module and has no dependencies other than the Python Standard Library._

## Contents

*   [1 Features](#Features)
*   [2 Installing Bottle](#Installing_Bottle)
*   [3 Hello World](#Hello_World)
*   [4 FastCGI](#FastCGI)
*   [5 Reloading](#Reloading)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 My application works, but only locally](#My_application_works.2C_but_only_locally)
    *   [6.2 Bottle isn't automatically reloading when I make changes to one of my files!](#Bottle_isn.27t_automatically_reloading_when_I_make_changes_to_one_of_my_files.21)

## Features

*   Routing:

	Requests to function-call mapping with support for clean and dynamic URLs.

*   Templates:

	Fast and pythonic built-in template engine and support for mako, jinja2 and cheetah templates.

*   Utilities:

	Convenient access to form data, file uploads, cookies, headers and other HTTP related metadata.

*   Server:

	Built-in HTTP development server and support for paste, fapws3, bjoern, Google App Engine, cherrypy or any other WSGI capable HTTP server.

## Installing Bottle

Install [python-bottle](https://www.archlinux.org/packages/?name=python-bottle) (for Python 3) or [python2-bottle](https://www.archlinux.org/packages/?name=python2-bottle) (for Python 2) from the [official repositories](/index.php/Official_repositories "Official repositories").

## Hello World

To get started with your first bottle server, here is a basic hello world example:

```
from bottle import route, run

@route('/:name')
def index(name='World'):
    return '**Hello %s!**' % name

run(host='localhost', port=8080)

```

To start Bottle, just simply run it using python

```
python server.py

```

You should see this next:

```
Bottle server starting up (using WSGIRefServer())...
Listening on [http://localhost:8080/](http://localhost:8080/)
Use Ctrl-C to quit.

```

## FastCGI

FastCGI is a great way of interfacing with Bottle (from lighttpd, nginx, etc). To use it however we must hook Bottle into something. For a simple example, let's use FLUP (for python2.x)

```
pacman -S python-flup

```

And now for our hello world application:

```
from bottle import route, run, FlupFCGIServer

@route('/:name')
def index(name='World'):
    return '**Hello %s!**' % name

run(host='localhost', port=8080, server=FlupFCGIServer)

```

more details on alternative servers [here](http://bottlepy.org/docs/dev/tutorial.html?highlight=flup#multi-threaded-server)

## Reloading

By default, Bottle does not support reloading of files. However there is an option to allow such a feature. Bottle does this by starting a new server in parallel to the one currently running, switching over to it, and then removing the older version.

```
from bottle import route, run

@route('/:name')
def index(name='World'):
    return '**Hello %s!**' % name

run(host='localhost', port=8080, reloader=True)

```

and to set the interval in which it reloads itself (default of 1 second):

```
run(host='localhost', port=8080, reloader=True, interval=0.5)

```

## Troubleshooting

### My application works, but only locally

Be sure if you are using Bottle directly as a web server (good for development, not recommend for production) to set the host to the ip address it will be accessed from and not 'localhost'

```
run(host='192.168.2.3', port=8080)

```

### Bottle isn't automatically reloading when I make changes to one of my files!

The Bottle reloader checks on which applications have changed by monitoring the imported files. Make sure that you are globally importing the application modules that you want to be reloaded.

```
import myapp

```

will work but not:

```
@route('/:name')
def index(name='World'):
    import myapp
    return myapp.init(name)

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Bottle&oldid=388015](https://wiki.archlinux.org/index.php?title=Bottle&oldid=388015)"