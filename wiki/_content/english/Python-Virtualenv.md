*virtualenv* is a Python tool written by Ian Bicking and used to create isolated environments for [Python](/index.php/Python "Python") in which you can install packages without interfering with the other virtualenvs nor with the system Python's packages. The present article covers the installation of the *virtualenv* package and its companion command line utility *virtualenvwrapper* designed by Doug Hellmann to (greatly) improve your work flow. A quick how-to to help you to begin working inside virtual environment is then provided.

## Contents

*   [1 Virtual Environments at a glance](#Virtual_Environments_at_a_glance)
*   [2 Virtualenv](#Virtualenv)
    *   [2.1 Installation](#Installation)
    *   [2.2 Basic Usage](#Basic_Usage)
*   [3 Virtualenvwrapper](#Virtualenvwrapper)
    *   [3.1 Installation](#Installation_2)
    *   [3.2 Basic Usage](#Basic_Usage_2)
*   [4 See Also](#See_Also)

## Virtual Environments at a glance

*virtualenv* is a tool designated to address the problem of dealing with packages' dependencies while maintaining different versions that suit projects' needs. For example, if you work on two Django web sites, say one that needs Django 1.2 while the other needs the good old 0.96\. You have no way to keep both versions if you install them into /usr/lib/python2/site-packages . Thanks to virtualenv it's possible, by creating two isolated environments, to have the two development environment to play along nicely.

*vitualenvwrapper* takes *virtualenv* a step further by providing convenient commands you can invoke from your favorite console.

*venv* is [a built-in module](https://docs.python.org/3/library/venv.html) added in version 3.3, implementing a similar API to *virtualenv*.

## Virtualenv

*virtualenv* supports Python 2.6+ and Python 3.x. See [Python#Python 3](/index.php/Python#Python_3 "Python") for an overview of the different versions of Python.

### Installation

[Install](/index.php/Install "Install") [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv), or [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) for the legacy version.

### Basic Usage

An extended tutorial on how use *virtualenv* for sandboxing can be found [here](http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox). If the link does not work, try [the archive link](http://web.archive.org/web/20120304235158/http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox). A simple use case is as follows:

*   Create a virtualenv:

```
$ virtualenv my_env

```

*   Activate the virtualenv:

```
$ source my_env/bin/activate

```

*   Install some package inside the virtualenv (say, Django):

```
(my_env)$ pip install django

```

*   Do your things
*   Leave the virtualenv:

```
(my_env)$ deactivate

```

## Virtualenvwrapper

*virtualenvwrapper* allows more natural command line interaction with your virtualenvs by exposing several useful commands to create, activate and remove virtualenvs. This package is a wrapper for both [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv) and [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

### Installation

[Install](/index.php/Install "Install") the [python-virtualenvwrapper](https://www.archlinux.org/packages/?name=python-virtualenvwrapper) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Now add the following lines to your `~/.bashrc`:

```
export WORKON_HOME=~/.virtualenvs
source /usr/bin/virtualenvwrapper.sh

```

If you are not using python3 by default (check the output of `$ python --version`) you also need to add the following line to your `~/.bashrc` prior sourcing the `virtualenvwrapper.sh` script. The current version of the `virtualenvwrapper-python` package only works with python3\. It can create python2 virtualenvs fine though.

```
VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3

```

Re-open your console and create the `WORKON_HOME` folder:

```
$ mkdir $WORKON_HOME

```

### Basic Usage

The main information source on virtualenvwrapper usage (and extension capability) is Doug Hellmann's [page](http://www.doughellmann.com/docs/virtualenvwrapper/).

*   Create the virtualenv:

```
$ mkvirtualenv -p /usr/bin/python2.7 my_env

```

*   Activate the virtualenv:

```
$ workon my_env

```

*   Install some package inside the virtualenv (say, Django):

```
(my_env)$ pip install django

```

*   Do your things
*   Leave the virtualenv:

```
(my_env)$ deactivate

```

## See Also

*   [virtualenv Pypi page](https://pypi.python.org/pypi/virtualenv)
*   [Tutorial for virtualenv](http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox)
*   [virtualenvwrapper page at Doug Hellmann's](http://www.doughellmann.com/docs/virtualenvwrapper/)