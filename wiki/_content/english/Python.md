Related articles

*   [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines")
*   [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment")
*   [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi")
*   [Django](/index.php/Django "Django")

From [Wikipedia](https://en.wikipedia.org/wiki/Python_(programming_language) "wikipedia:Python (programming language)"):

	Python is a widely used high-level, general-purpose, interpreted, dynamic programming language. Its design philosophy emphasizes code readability, and its syntax allows programmers to express concepts in fewer lines of code than possible in languages such as C++ or Java. The language provides constructs intended to enable writing clear programs on both a small and large scale.

	Python supports multiple programming paradigms, including object-oriented, imperative and functional programming or procedural styles. It features a dynamic type system and automatic memory management and has a large and comprehensive standard library.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
    *   [1.3 Old versions](#Old_versions)
*   [2 Package management](#Package_management)
*   [3 Widget bindings](#Widget_bindings)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Alternative shells](#Alternative_shells)
    *   [4.2 Virtual environment](#Virtual_environment)
    *   [4.3 Tab completion in Python2 shell](#Tab_completion_in_Python2_shell)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Dealing with version problem in build scripts](#Dealing_with_version_problem_in_build_scripts)
*   [6 See also](#See_also)

## Installation

### Python 3

Python 3 is the latest version of the language, and is incompatible with Python 2\. The language is mostly the same, but many details, especially how built-in objects like dictionaries and strings work, have changed considerably, and a lot of deprecated features have finally been removed. Also, the standard library has been reorganized in a few prominent places. For an overview of the differences, visit [Python2orPython3](https://wiki.python.org/moin/Python2orPython3) and the relevant [chapter](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) in Dive into Python 3.

To install the latest version of Python 3, [install](/index.php/Install "Install") the [python](https://www.archlinux.org/packages/?name=python) package.

If you would like to build the latest RC/betas from source, visit [Python Downloads](https://www.python.org/downloads/). The [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") also contains good [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). If you do decide to build the RC, note that the binary (by default) installs to `/usr/local/bin/python3.x`.

### Python 2

To get the latest version of Python 2, [install](/index.php/Install "Install") the [python2](https://www.archlinux.org/packages/?name=python2) package.

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

A similar approach in tricking the environment, which also relies on `#!/usr/bin/env python` to be called by the script in question, is to use a [virtual environment](#Virtual_environment).

### Old versions

**Warning:** Python versions before 2.7 and 3.4 have not received any updates—including security patches—since at least 2014\. Using older versions for Internet-facing applications or untrusted code may be dangerous and is not recommended.

Old versions of Python are available via the [AUR](/index.php/AUR "AUR") and may be useful for historical curiosity, old applications that do not run on current versions, or for testing Python programs intended to run on a distribution that comes with an older version:

*   Python 3.6: [python36](https://aur.archlinux.org/packages/python36/)
*   Python 3.5: [python35](https://aur.archlinux.org/packages/python35/)
*   Python 3.4: [python34](https://aur.archlinux.org/packages/python34/)
*   Python 2.6: [python26](https://aur.archlinux.org/packages/python26/)
*   Python 2.5: [python25](https://aur.archlinux.org/packages/python25/)
*   Python 1.5: [python15](https://aur.archlinux.org/packages/python15/)

Extra modules/libraries for old versions of Python may be found on the AUR by searching for `python<*version without period*>`, e.g. searching for "python26" for 2.6 modules.

## Package management

Although a great number of Python packages are readily available in the [official repositories](/index.php/Official_repositories "Official repositories") and the [AUR](/index.php/AUR "AUR"), the Python ecosystem provides its own package managers for use with [PyPI](https://pypi.org/), the Python Package Index:

*   **pip** — The PyPA tool for installing Python packages.

	[https://pip.pypa.io/](https://pip.pypa.io/) || [python-pip](https://www.archlinux.org/packages/?name=python-pip), [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)

*   **setuptools** — Easily download, build, install, upgrade, and uninstall Python packages.

	[https://setuptools.readthedocs.io/](https://setuptools.readthedocs.io/) || [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools), [python2-setuptools](https://www.archlinux.org/packages/?name=python2-setuptools)

For a brief history and feature comparison between the two, see [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install). Authoritative best practices in Python package management are detailed [here](https://packaging.python.org/).

If you must use *pip*, use a [virtual environment](#Virtual_environment), or `pip install --user` to avoid conflicts with packages in `/usr`. It is always preferred to [use pacman to install software](/index.php/System_maintenance#Use_the_package_manager_to_install_software "System maintenance").

**Note:** There are also tools integrating *pip* with *pacman* by automatically generating PKGBUILDs for specified pip-packages: see [Creating packages#PKGBUILD generators](/index.php/Creating_packages#PKGBUILD_generators "Creating packages").

**Tip:** [pipenv](https://docs.pipenv.org/) provides a single CLI for [Pipfile](https://github.com/pypa/pipfile), *pip* and [virtualenv](/index.php/Virtualenv "Virtualenv"). It is available as [python-pipenv](https://www.archlinux.org/packages/?name=python-pipenv) and [python2-pipenv](https://www.archlinux.org/packages/?name=python2-pipenv).

## Widget bindings

The following [widget toolkit](https://en.wikipedia.org/wiki/Widget_toolkit "wikipedia:Widget toolkit") bindings are available:

*   **TkInter** — Tk bindings

	[https://wiki.python.org/moin/TkInter](https://wiki.python.org/moin/TkInter) || standard module

*   **pyQt** — [Qt](/index.php/Qt "Qt") bindings

	[https://riverbankcomputing.com/software/pyqt/intro](https://riverbankcomputing.com/software/pyqt/intro) || [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide** — [Qt](/index.php/Qt "Qt") bindings

	[https://wiki.qt.io/PySide](https://wiki.qt.io/PySide) || [python2-pyside](https://aur.archlinux.org/packages/python2-pyside/) [python-pyside](https://aur.archlinux.org/packages/python-pyside/)

*   **pyGTK** — [GTK+ 2](/index.php/GTK%2B "GTK+") bindings

	[http://www.pygtk.org/](http://www.pygtk.org/) || [pygtk](https://www.archlinux.org/packages/?name=pygtk)

*   **PyGObject** — [GTK+ 2/3](/index.php/GTK%2B "GTK+") bindings via GObject Introspection

	[https://wiki.gnome.org/PyGObject/](https://wiki.gnome.org/PyGObject/) || [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) [python-gobject2](https://www.archlinux.org/packages/?name=python-gobject2) [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

*   **wxPython** — wxWidgets bindings

	[https://wxpython.org/](https://wxpython.org/) || [python2-wxpython3](https://www.archlinux.org/packages/?name=python2-wxpython3) [python-wxpython](https://www.archlinux.org/packages/?name=python-wxpython)

To use these with Python, you may need to install the associated widget kits.

## Tips and tricks

### Alternative shells

*   **bpython** — Fancy interface for the Python interpreter.

	[https://bpython-interpreter.org/](https://bpython-interpreter.org/) || [bpython](https://www.archlinux.org/packages/?name=bpython) [bpython2](https://www.archlinux.org/packages/?name=bpython2)

*   **[IPython](https://en.wikipedia.org/wiki/IPython "wikipedia:IPython")** — Enhanced interactive Python shell.

	[https://ipython.org/](https://ipython.org/) || [ipython](https://www.archlinux.org/packages/?name=ipython) [ipython2](https://www.archlinux.org/packages/?name=ipython2)

*   **[Jupyter](/index.php/Jupyter "Jupyter") Notebook** — Web interface to IPython.

	[https://jupyter.org/](https://jupyter.org/) || [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook)

### Virtual environment

Python provides tools to create isolated environments in which you can install packages without interfering with the other virtual environments nor with the system Python's packages. It could change the *python* interpreter used for a specific application.

See [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment") for details.

### Tab completion in Python2 shell

Since Python 3.4 [tab completion](https://docs.python.org/3/tutorial/interactive.html) is enabled by default, for Python 2 you can manually enable it by adding the following lines to a file referenced by the `PYTHONSTARTUP` environment variable: [[1]](https://algorithmicallyrandom.blogspot.co.at/2009/09/tab-completion-in-python-shell-how-to.html)

```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")

```

## Troubleshooting

### Dealing with version problem in build scripts

Many projects' build scripts assume `python` to be Python 2, and that would eventually result in an error — typically complaining that `print 'foo'` is invalid syntax. Luckily, many of them call *python* from the `PATH` environment variable instead of hardcoding `#!/usr/bin/python` in the shebang line, and the Python scripts are all contained within the project tree. So, instead of modifying the build scripts manually, there is a workaround. Create `/usr/local/bin/python` with content like this:

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

Where `/path/to/project1/*|/path/to/project2/*|/path/to/project3*` is a list of patterns separated by `|` matching all project trees. For some scripts, the path may not be the first parameter, for example Google SDK it sends "-S" as the first parameter. The readlink command should change to `script=$(readlink -f -- "$1")`.

Do not forget to make it [executable](/index.php/Executable "Executable"). Afterwards scripts within the specified project trees will be run with Python 2.

## See also

*   [O'Reilly's Learning Python, 5th edition](http://shop.oreilly.com/product/0636920028154.do) commercial
*   [Dive Into Python](http://www.diveintopython.net/), [Dive Into Python3](http://getpython3.com/diveintopython3/)
*   [A Byte of Python](https://python.swaroopch.com/)
*   [Learn Python the Hard Way](https://learnpythonthehardway.org/)
*   [Learn Python](https://learnpython.org/)
*   [Crash into Python](https://stephensugden.com/crash_into_python/) (assumes familiarity with other programming languages)
*   [Beginning Game Development with Python and Pygame](https://www.apress.com/book/9781590598726) commercial
*   [Think Python](http://www.greenteapress.com/thinkpython/)
*   [Pythonspot](https://pythonspot.com)
*   [OverIQ Python Tutorial](https://overiq.com/python/3.4/intro-to-python/)
*   [Python Tutorial to Learn Step by Step](https://www.techbeamers.com/python-tutorial-step-by-step/)
*   [awesome-python](https://github.com/vinta/awesome-python) - A curated list of Python frameworks, libraries, software and resources.
*   [boltons](https://github.com/mahmoud/boltons) - Constructs/recipes/snippets that would be handy in the standard library.