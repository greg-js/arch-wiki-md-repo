From [Wikipedia](https://en.wikipedia.org/wiki/Python_(programming_language) "wikipedia:Python (programming language)"):

	*Python is a widely used high-level, general-purpose, interpreted, dynamic programming language. Its design philosophy emphasizes code readability, and its syntax allows programmers to express concepts in fewer lines of code than possible in languages such as C++ or Java. The language provides constructs intended to enable writing clear programs on both a small and large scale.*

	*Python supports multiple programming paradigms, including object-oriented, imperative and functional programming or procedural styles. It features a dynamic type system and automatic memory management and has a large and comprehensive standard library.*

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
    *   [1.3 Old versions](#Old_versions)
*   [2 Package management](#Package_management)
*   [3 Widget bindings](#Widget_bindings)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 IPython](#IPython)
    *   [4.2 Virtual environment](#Virtual_environment)
    *   [4.3 Getting completion in Python2 shell](#Getting_completion_in_Python2_shell)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Dealing with version problem in build scripts](#Dealing_with_version_problem_in_build_scripts)
*   [6 See also](#See_also)

## Installation

### Python 3

Python 3 is the latest version of the language, and is incompatible with Python 2\. The language is mostly the same, but many details, especially how built-in objects like dictionaries and strings work, have changed considerably, and a lot of deprecated features have finally been removed. Also, the standard library has been reorganized in a few prominent places. For an overview of the differences, visit [Python2orPython3](http://wiki.python.org/moin/Python2orPython3) and their relevant [chapter](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) in Dive into Python 3.

To install the latest version of Python 3, [install](/index.php/Install "Install") the [python](https://www.archlinux.org/packages/?name=python) package from the [official repositories](/index.php/Official_repositories "Official repositories").

If you would like to build the latest RC/betas from source, visit [Python Downloads](http://www.python.org/download/). The [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") also contains good [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). If you do decide to build the RC, note that the binary (by default) installs to `/usr/local/bin/python3.x`.

### Python 2

To get the latest version of Python 2, [install](/index.php/Install "Install") the [python2](https://www.archlinux.org/packages/?name=python2) package from the [official repositories](/index.php/Official_repositories "Official repositories").

Python 2 will happily run alongside Python 3\. You need to specify `python2` in order to run this version.

Any program requiring Python 2 needs to point to `/usr/bin/python2`, instead of `/usr/bin/python`, which points to Python 3\. To do so, open the program or script in a [text editor](/index.php/List_of_applications/Documents#Text_editors "List of applications/Documents") and change the first line. The line will show one of the following:

```
#!/usr/bin/env python

```

or

```
#!/usr/bin/python

```

In both cases, just change `python` to `python2` and the program will then use Python 2 instead of Python 3.

Another way to force the use of python2 without altering the scripts is to call it explicitly with `python2`:

```
$ python2 *myScript.py*

```

Finally, you may not be able to control the script calls, but there is a way to trick the environment. It only works if the scripts use `#!/usr/bin/env python`. It will not work with `#!/usr/bin/python`. This trick relies on `env` searching for the first corresponding entry in the `PATH` variable.

First create a dummy folder:

```
$ mkdir ~/bin

```

Then add a symlink `python` to *python2* and the config scripts in it:

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

Finally put the new folder *at the beginning* of your `PATH` variable:

```
$ export PATH=~/bin:$PATH

```

**Note:** This method of changing [environment variables](/index.php/Environment_variables "Environment variables") is not permanent and is only active in the current terminal session.

To check which python interpreter is being used by `env`, use the following command:

```
$ which python

```

A similar approach in tricking the environment, which also relies on `#!/usr/bin/env python` to be called by the script in question, is to use a [#Virtual environment](#Virtual_environment).

### Old versions

Old versions of Python are available via the [AUR](/index.php/AUR "AUR") and may be useful for historical curiosity, old applications that do not run on current versions, or for testing Python programs intended to run on a distribution that comes with an older version (e.g. RHEL 5.x has Python 2.4, or Ubuntu 12.04 has Python 3.2):

*   Python 1.5: [python15](https://aur.archlinux.org/packages/python15/)
*   Python 2.5: [python25](https://aur.archlinux.org/packages/python25/)
*   Python 2.6: [python26](https://aur.archlinux.org/packages/python26/)
*   Python 3.0: [python30](https://aur.archlinux.org/packages/python30/)
*   Python 3.2: [python32](https://aur.archlinux.org/packages/python32/)
*   Python 3.3: [python33](https://aur.archlinux.org/packages/python33/)
*   Python 3.4: [python34](https://aur.archlinux.org/packages/python34/)
*   Python 3.5: [python35](https://aur.archlinux.org/packages/python35/)

As of October 2016, Python upstream only supports Python 2.7, 3.4, and 3.5 for security fixes. Using older versions for Internet-facing applications or untrusted code may be dangerous and is not recommended.

Extra modules/libraries for old versions of Python may be found on the AUR by searching for `python<*version without period*>`, e.g. searching for "python26" for 2.6 modules.

## Package management

Although a great number of Python packages are readily available in the [official repositories](/index.php/Official_repositories "Official repositories") and the [AUR](/index.php/AUR "AUR"), the Python ecosystem provides its own package managers for use with [PyPI](https://pypi.python.org/), the Python Package Index.

*   **pip** — The PyPA tool for installing Python packages.

	[https://pip.pypa.io/](https://pip.pypa.io/) || [python-pip](https://www.archlinux.org/packages/?name=python-pip), [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)

*   **setuptools** — Easily download, build, install, upgrade, and uninstall Python packages.

	[https://setuptools.readthedocs.io/](https://setuptools.readthedocs.io/) || [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools), [python2-setuptools](https://www.archlinux.org/packages/?name=python2-setuptools)

For a brief history and feature comparison between the two, see [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install).

Authoritative best practices in Python package management are detailed [here](https://packaging.python.org/).

## Widget bindings

The following [widget toolkit](https://en.wikipedia.org/wiki/Widget_toolkit "wikipedia:Widget toolkit") bindings are available:

*   **TkInter** — Tk bindings

	[http://wiki.python.org/moin/TkInter](http://wiki.python.org/moin/TkInter) || standard module

*   **pyQt** — [Qt](/index.php/Qt "Qt") bindings

	[http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro) || [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide** — [Qt](/index.php/Qt "Qt") bindings

	[http://www.pyside.org/](http://www.pyside.org/) || [python2-pyside](https://www.archlinux.org/packages/?name=python2-pyside) [python-pyside](https://www.archlinux.org/packages/?name=python-pyside)

*   **pyGTK** — [GTK+ 2](/index.php/GTK%2B "GTK+") bindings

	[http://www.pygtk.org/](http://www.pygtk.org/) || [pygtk](https://www.archlinux.org/packages/?name=pygtk)

*   **PyGObject** — [GTK+ 2/3](/index.php/GTK%2B "GTK+") bindings via GObject Introspection

	[https://wiki.gnome.org/PyGObject/](https://wiki.gnome.org/PyGObject/) || [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) [python-gobject2](https://www.archlinux.org/packages/?name=python-gobject2) [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

*   **wxPython** — wxWidgets bindings

	[http://wxpython.org/](http://wxpython.org/) || [wxpython](https://www.archlinux.org/packages/?name=wxpython)

To use these with Python, you may need to install the associated widget kits.

## Tips and tricks

### IPython

[IPython](http://ipython.org/) is an enhanced Python command line available in the official repositories as [ipython](https://www.archlinux.org/packages/?name=ipython) and [ipython2](https://www.archlinux.org/packages/?name=ipython2). If you want the IPython notebook, install [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) for the IPython3 notebook and [ipython2-notebook](https://www.archlinux.org/packages/?name=ipython2-notebook) for the IPython2 notebook. Run

```
$ jupyter notebook

```

to autostart the browser and run the IPython kernel. You can select the python version when creating the notebook in the browser.

[bpython](http://bpython-interpreter.org/) is a ncurses interface to the Python interpreter, available in the official repositories as [bpython](https://www.archlinux.org/packages/?name=bpython) and [bpython2](https://www.archlinux.org/packages/?name=bpython2).

### Virtual environment

Python provides tools to create isolated environments in which you can install packages without interfering with the other virtual environments nor with the system Python's packages. It could change the python interpreter used for a specific application.

See [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment") for details.

### Getting completion in Python2 shell

**Note:** This is relevant only for Python 2, [tab completion](https://docs.python.org/3/tutorial/interactive.html) is enabled by default since Python 3.4.

Copy this into Python's interactive shell:

 `/usr/bin/python2` 
```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")
```

Source: [http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html](http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html).

## Troubleshooting

### Dealing with version problem in build scripts

Many projects' build scripts assume `python` to be Python 2, and that would eventually result in an error — typically complaining that `print 'foo'` is invalid syntax. Luckily, many of them call `python` from the `PATH` instead of hardcoding `#!/usr/bin/python` in the shebang line, and the Python scripts are all contained within the project tree. So, instead of modifying the build scripts manually, there is an easy workaround. Just create `/usr/local/bin/python` with content like this:

 `/usr/local/bin/python` 
```
#!/bin/bash
script=$(readlink -f -- "$1")
case "$script" in (/path/to/project1/*|/path/to/project2/*|/path/to/project3*)
    exec python2 "$@"
    ;;
esac

exec python3 "$@"

```

Where `/path/to/project1/*|/path/to/project2/*|/path/to/project3*` is a list of patterns separated by `|` matching all project trees.

Do not forget to make it executable:

```
# chmod +x /usr/local/bin/python

```

Afterwards scripts within the specified project trees will be run with Python 2.

## See also

*   [Learning Python, 4th edition](http://shop.oreilly.com/product/9780596158071.do)
*   [Dive Into Python](http://www.diveintopython.net/), [Dive Into Python3](http://getpython3.com/diveintopython3/)
*   [A Byte of Python](http://www.swaroopch.com/notes/Python)
*   [Learn Python The Hard Way](http://learnpythonthehardway.org)
*   [Learn Python](http://learnpython.org)
*   [Crash into Python](http://stephensugden.com/crash_into_python/) (assumes familiarity with other programming languages)
*   [Beginning Game Development with Python and Pygame](http://www.apress.com/book/view/9781590598726)
*   [Think Python](http://www.greenteapress.com/thinkpython/)
*   [Pythonspot](https://pythonspot.com)