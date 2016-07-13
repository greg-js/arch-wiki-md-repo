*virtualenv* is a tool used to create an isolated workspace for a [Python](/index.php/Python "Python") application. It has various advantages such as the ability to install modules locally, export a working environment, and execute a [Python](/index.php/Python "Python") program in that environment.

## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
    *   [2.1 Packages](#Packages)
*   [3 Usage](#Usage)
    *   [3.1 Creation](#Creation)
        *   [3.1.1 pyvenv](#pyvenv)
        *   [3.1.2 virtualenv](#virtualenv)
    *   [3.2 Activation](#Activation)
*   [4 Python versions](#Python_versions)
*   [5 virtualenvwrapper](#virtualenvwrapper)
    *   [5.1 Installation](#Installation_2)
    *   [5.2 Basic usage](#Basic_usage)
*   [6 See also](#See_also)

## Overview

A virtual environment is a directory into which some binaries and shell scripts are installed. The binaries include *python* for executing scripts and *pip* for installing other modules within the environment. There are also shell scripts (one for [bash](/index.php/Bash "Bash"), csh, and [fish](/index.php/Fish "Fish")) to activate the environment. Essentially, a virtual environment mimics a full system install of [Python](/index.php/Python "Python") and all of the desired modules without interfering with any system on which the application might run.

## Installation

[Python](/index.php/Python "Python") 3.3+ comes with a tool called *pyvenv* and an API called *venv* for extending the native implementation. For applications that require an older version of Python, *virtualenv* must be used.

### Packages

[Install](/index.php/Install "Install") one of these packages from the [official repositories](/index.php/Official_repositories "Official repositories") to use a Python virtual environment.

*   Python 3.3+: [python](https://www.archlinux.org/packages/?name=python)
*   Python 3: [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv)
*   Python 2: [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv)

## Usage

All three tools use a similar workflow.

### Creation

Use *pyvenv* or *virtualenv* to create the virtual environment within your project directory. Be sure to exclude the venv directory from version control--a copy of `pip freeze` will be enough to rebuild it.

#### pyvenv

This tool is provided by [python](https://www.archlinux.org/packages/?name=python) (3.3+).

```
$ pyvenv venv

```

#### virtualenv

Use *virtualenv* for Python 3, available in [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv).

```
$ virtualenv venv

```

And *virtualenv2* for Python 2, available in [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

```
$ virtualenv2 venv

```

### Activation

Use one of the provided shell scripts to activate and deactivate the environment. This example assumes bash is used.

```
$ source venv/bin/activate
(venv) $

```

Once inside the virtual environment, modules can be installed with *pip* and scripts can be run as normal.

To exit the virtual environment, run the function provided by `bin/activate`:

```
(venv) $ deactivate

```

## Python versions

The binary versions depend on which virtual environment tool was used. For instance, the *python* command used in the Python 2 example points to `bin/python2.7`, while the one in the *pyvenv* example points to `bin/python3.5`.

One major difference between *pyvenv* and *virtualenv* is that the former uses the system's Python binary by default:

```
$ ls -l pyvenv/bin/python3.5
lrwxrwxrwx 1 foo foo 7 Jun  3 19:57 pyvenv/bin/python3.5 -> /usr/bin/python3

```

The *virtualenv* tool uses a separate Python binary in the environment directory:

```
$ ls -l venv3/bin/python3.5
lrwxrwxrwx 1 foo foo 7 Jun  3 19:58 venv3/bin/python3.5 -> python3

```

## virtualenvwrapper

*virtualenvwrapper* allows more natural command line interaction with your virtual environemnts by exposing several useful commands to create, activate and remove virtual environments. This package is a wrapper for both [python-virtualenv](https://www.archlinux.org/packages/?name=python-virtualenv) and [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv).

### Installation

[Install](/index.php/Install "Install") the [python-virtualenvwrapper](https://www.archlinux.org/packages/?name=python-virtualenvwrapper) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Now add the following lines to your `~/.bashrc`:

```
$ export WORKON_HOME=~/.virtualenvs
$ source /usr/bin/virtualenvwrapper.sh

```

If you are not using python3 by default (check the output of `python --version`) you also need to add the following line to your `~/.bashrc` prior sourcing the `virtualenvwrapper.sh` script. The current version of the [python-virtualenvwrapper](https://www.archlinux.org/packages/?name=python-virtualenvwrapper) package only works with python3\. It can create python2 virtual environments fine though.

```
VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3

```

Re-open your console and create the `WORKON_HOME` folder:

```
$ mkdir $WORKON_HOME

```

### Basic usage

The main information source on virtualenvwrapper usage (and extension capability) is Doug Hellmann's [page](http://www.doughellmann.com/docs/virtualenvwrapper/).

Create the virtual environment:

```
$ mkvirtualenv -p /usr/bin/python2.7 my_env

```

Activate the virtual environment:

```
$ workon my_env

```

Install some package inside the virtual environment (say, Django):

```
(my_env) $ pip install django

```

After you have done your things, leave the virtual environment:

```
(my_env) $ deactivate

```

## See also

*   [Python venv (pyvenv)](https://docs.python.org/3/library/venv.html)
*   [virtualenv Pypi page](https://pypi.python.org/pypi/virtualenv)
*   [Tutorial for virtualenv](http://wiki.pylonshq.com/display/pylonscookbook/Using+a+Virtualenv+Sandbox)
*   [virtualenvwrapper page at Doug Hellmann's](http://www.doughellmann.com/docs/virtualenvwrapper/)