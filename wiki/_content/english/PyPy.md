[PyPy](http://pypy.org/) is an alternate implementation of the [Python](/index.php/Python "Python") 2.7.8 and 3.2.5 interpreters. PyPy's benefits are in the area of speed, memory usage, sandboxing and stacklessness. It is compatible with CPython with [some exceptions](http://pypy.org/compat.html). PyPy also can be used to compile RPython programs to C code.

## Contents

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
    *   [2.1 Interactive Interpreter](#Interactive_Interpreter)
    *   [2.2 Run Program From File](#Run_Program_From_File)
*   [3 EasyInstall](#EasyInstall)
    *   [3.1 EasyInstall Installation](#EasyInstall_Installation)
    *   [3.2 Installing EasyInstall Packages](#Installing_EasyInstall_Packages)
    *   [3.3 EasyInstall Package Example](#EasyInstall_Package_Example)

## Installation

For Python 2.7, install the [pypy](https://www.archlinux.org/packages/?name=pypy) package from the [official repositories](/index.php/Official_repositories "Official repositories"). For Python 3, install the [pypy3](https://www.archlinux.org/packages/?name=pypy3) package.

PyPy is installed in /opt/pypy/ or /opt/pypy3 and the main pypy executable is bin/pypy-c

## Usage

Basic PyPy usage is done through the `pypy` or `pypy3` command and functions similarly to CPython usage. Enter

```
$ pypy -h

```

to view the listing of `pypy` options.

### Interactive Interpreter

To load the pypy interactive interpreter run

```
$ pypy

```

### Run Program From File

To run a Python program from a file in pypy run

```
$ pypy example.py

```

where example.py is the file name of the program.

## EasyInstall

Python libraries and programs can be installed in PyPy through EasyInstall. PyPy libraries are stored in a different folder then Cpython libraries.

### EasyInstall Installation

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

### Installing EasyInstall Packages

To install EasyInstall package *package_name* into PyPy enter

```
# /opt/pypy/bin/easy_install package_name

```

Packages Will be Located at /opt/pypy/site-packages Installed libraries and applications will be at /opt/pypy/bin Programs installed through EasyInstall on PyPy can usually be ran with `/opt/pypy/bin/program_name` where *program_name* is the name of the PyPy program.

### EasyInstall Package Example

The following will install the Lamson email framework.

```
# /opt/pypy/bin/easy_install lamson

```

The following will run the framework's gen-project option

```
$ /opt/pypy/bin/lamson gen -project testproject

```