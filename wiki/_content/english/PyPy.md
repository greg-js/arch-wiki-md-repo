[PyPy](http://pypy.org/) is an alternate implementation of the [Python](/index.php/Python "Python") 2.7.10 and 3.2.5 interpreters. PyPy's benefits are in the area of speed, memory usage, sandboxing and stacklessness. It is compatible with CPython with [some exceptions](http://pypy.org/compat.html). PyPy also can be used to compile RPython programs to C code.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Interactive interpreter](#Interactive_interpreter)
    *   [2.2 Run program from file](#Run_program_from_file)
    *   [2.3 Virtual environment creation](#Virtual_environment_creation)
    *   [2.4 Installing pip](#Installing_pip)
*   [3 EasyInstall](#EasyInstall)
    *   [3.1 EasyInstall installation](#EasyInstall_installation)
    *   [3.2 Installing EasyInstall packages](#Installing_EasyInstall_packages)
    *   [3.3 EasyInstall package example](#EasyInstall_package_example)

## Installation

For Python 2.7, install the [pypy](https://www.archlinux.org/packages/?name=pypy) package from the [official repositories](/index.php/Official_repositories "Official repositories"). For Python 3, install the [pypy3](https://www.archlinux.org/packages/?name=pypy3) package.

PyPy is installed in /opt/pypy/ or /opt/pypy3 and the main pypy executable is bin/pypy-c

## Usage

Basic PyPy usage is done through the `pypy` or `pypy3` command and functions similarly to CPython usage. Enter

```
$ pypy -h

```

to view the listing of `pypy` options.

### Interactive interpreter

To load the pypy interactive interpreter run

```
$ pypy

```

### Run program from file

To run a Python program from a file in pypy run

```
$ pypy example.py

```

where example.py is the file name of the program.

### Virtual environment creation

To make a virtual environment with PyPy

```
$ virtualenv --python=/usr/bin/pypy venv-pypy

```

see [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment") for further information

### Installing pip

As python packages for pypy aren't distributed as Arch packages the most convenient thing is to install what you require as your own user.

```
 $ pypy -m ensurepip --user
 $ pypy -m pip install --user --upgrade pip

```

Once you have pip you can install any package you need, eg:

```
 $ pypy -m pip install --user sqlalchemy

```

If you'd prefer to install packages system wide just run the previous commands as root without the --user. Note that this will result in the packages being installed in /opt/pypy without the package manager being aware of them.

## EasyInstall

Python libraries and programs can be installed in PyPy through EasyInstall. PyPy libraries are stored in a different folder then CPython libraries.

### EasyInstall installation

EasyInstall does not come with the PyPy package and must be installed manually. Create the /opt/pypy/site-packages/ folder which will be needed for the EasyInstall installation.

```
# mkdir /opt/pypy/site-packages/

```

Download distribute_setup.py to the folder /opt/pypy/ and run it. distribute_setup.py will install EasyInstall.

```
$ cd /opt/pypy/
# wget python-distribute.org/distribute_setup.py
# pypy distribute_setup.py

```

EasyInstall is located at /opt/pypy/bin/easy_install

### Installing EasyInstall packages

To install EasyInstall package *package_name* into PyPy enter

```
# /opt/pypy/bin/easy_install package_name

```

Packages Will be Located at /opt/pypy/site-packages Installed libraries and applications will be at /opt/pypy/bin Programs installed through EasyInstall on PyPy can usually be ran with `/opt/pypy/bin/program_name` where *program_name* is the name of the PyPy program.

### EasyInstall package example

The following will install the Lamson email framework.

```
# /opt/pypy/bin/easy_install lamson

```

The following will run the framework's gen-project option

```
$ /opt/pypy/bin/lamson gen -project testproject

```