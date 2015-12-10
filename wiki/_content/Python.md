# Python

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines")
*   [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv")
*   [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi")

From [Wikipedia](https://en.wikipedia.org/wiki/Python_(programming_language) "wikipedia:Python (programming language)"):

_Python is a widely used general-purpose, high-level programming language. Its design philosophy emphasizes code readability, and its syntax allows programmers to express concepts in fewer lines of code than would be possible in languages such as C. The language provides constructs intended to enable clear programs on both a small and large scale._

_Python supports multiple programming paradigms, including object-oriented, imperative and functional programming or procedural styles. It features a dynamic type system and automatic memory management, and has a large and comprehensive standard library._

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
*   [2 Dealing with version problem in build scripts](#Dealing_with_version_problem_in_build_scripts)
*   [3 Getting completion in Python shell](#Getting_completion_in_Python_shell)
*   [4 Widget bindings](#Widget_bindings)
*   [5 Old versions](#Old_versions)
*   [6 Tips and tricks](#Tips_and_tricks)
*   [7 See also](#See_also)

## Installation

### Python 3

Python 3 is the latest version of the language, and is incompatible with Python 2\. The language is mostly the same, but many details, especially how built-in objects like dictionaries and strings work, have changed considerably, and a lot of deprecated features have finally been removed. Also, the standard library has been reorganized in a few prominent places. For an overview of the differences, visit [Python2orPython3](http://wiki.python.org/moin/Python2orPython3) and their relevant [chapter](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) in Dive into Python 3.

To install the latest version of Python 3, [install](/index.php/Install "Install") the [python](https://www.archlinux.org/packages/?name=python) package from the [official repositories](/index.php/Official_repositories "Official repositories").

If you would like to build the latest RC/betas from source, visit [Python Downloads](http://www.python.org/download/). The [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") also contains good [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). If you do decide to build the RC, note that the binary (by default) installs to `/usr/local/bin/python3.x`.

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Python#](https://wiki.archlinux.org/index.php/Talk:Python))

Starting a new project inside a VirtualEnv is as simple as running:

```
$ python -m venv newproj
$ source newproj/bin/activate
(newproj)$ pip install <dependency>

```

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
$ python2 _myScript.py_

```

Finally, you may not be able to control the script calls, but there is a way to trick the environment. It only works if the scripts use `#!/usr/bin/env python`. It will not work with `#!/usr/bin/python`. This trick relies on `env` searching for the first corresponding entry in the `PATH` variable.

First create a dummy folder:

```
$ mkdir ~/bin

```

Then add a symlink `python` to _python2_ and the config scripts in it:

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

Finally put the new folder _at the beginning_ of your `PATH` variable:

```
$ export PATH=~/bin:$PATH

```

**Note:** This method of changing [environment variables](/index.php/Environment_variables "Environment variables") is not permanent and is only active in the current terminal session.

To check which python interpreter is being used by `env`, use the following command:

```
$ which python

```

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

[![Tango-user-trash-full.png](/images/e/ee/Tango-user-trash-full.png)](/index.php/File:Tango-user-trash-full.png)

**This article or section is being considered for deletion.**

**Reason:** All this does is mangle the PATH variable, see [[1]](https://gist.github.com/IngCr3at1on/3f5260581901e3035d9e)<sup>[[dead link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot") 2015-08-08]</sup> (Discuss in [Talk:Python#](https://wiki.archlinux.org/index.php/Talk:Python))

A similar approach in tricking the environment, which also relies on `#!/usr/bin/env python` to be called by the script in question, is to use a [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv"). When a VirtualEnv is activated, the Python executable pointed to by `PATH` will be the one the VirtualEnv was installed with. Therefore, if the VirtualEnv is installed with Python 2, `python` will refer to Python 2.

To start, [install](/index.php/Install "Install") the [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv) package. Then create a directory, containing the VirtualEnv, with the following command:

```
$ virtualenv2 venv

```

Activate the VirtualEnv, which will update `PATH` to point at Python 2\. Note that this activation is only active for the current terminal session:

```
$ source venv/bin/activate

```

The desired script should then run using Python 2.

## Dealing with version problem in build scripts

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

## Getting completion in Python shell

**Note:** This is relevant only for Python 2, [tab completion](https://docs.python.org/3/tutorial/interactive.html) is enabled by default since Python 3.4.

Copy this into Python's interactive shell:

 `/usr/bin/python` 

```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")
```

Source: [http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html](http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html).

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

## Old versions

Old versions of Python are available via the [AUR](/index.php/AUR "AUR") and may be useful for historical curiosity, old applications that do not run on current versions, or for testing Python programs intended to run on a distribution that comes with an older version (e.g. RHEL 5.x has Python 2.4, or Ubuntu 12.04 has Python 3.1):

*   [python15](https://aur.archlinux.org/packages/python15/)<sup><small>AUR</small></sup>: Python 1.5.2
*   [python24](https://aur.archlinux.org/packages/python24/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python24)]</sup>: Python 2.4.6
*   [python25](https://aur.archlinux.org/packages/python25/)<sup><small>AUR</small></sup>: Python 2.5.6
*   [python26](https://aur.archlinux.org/packages/python26/)<sup><small>AUR</small></sup>: Python 2.6.9
*   [python30](https://aur.archlinux.org/packages/python30/)<sup><small>AUR</small></sup>: Python 3.0.1
*   [python31](https://aur.archlinux.org/packages/python31/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/python31)]</sup>: Python 3.1.5
*   [python32](https://aur.archlinux.org/packages/python32/)<sup><small>AUR</small></sup>: Python 3.2.5
*   [python33](https://aur.archlinux.org/packages/python33/)<sup><small>AUR</small></sup>: Python 3.3.5
*   [python34](https://aur.archlinux.org/packages/python34/)<sup><small>AUR</small></sup>: Python 3.4.3

As of July 2014, Python upstream only supports Python 2.7, 3.2, 3.3, and 3.4 for security fixes. Using older versions for Internet-facing applications or untrusted code may be dangerous and is not recommended.

Extra modules/libraries for old versions of Python may be found on the AUR by searching for `python<_version without period_>`, e.g. searching for "python26" for 2.6 modules.

## Tips and tricks

[IPython](http://ipython.org/) is an enhanced Python command line available in the official repositories as [ipython](https://www.archlinux.org/packages/?name=ipython) and [ipython2](https://www.archlinux.org/packages/?name=ipython2). If you want the IPython notebook, install [jupyter](https://www.archlinux.org/packages/?name=jupyter) for the IPython3 notebook and [ipython2-notebook](https://www.archlinux.org/packages/?name=ipython2-notebook) for the IPython2 notebook. Run

```
$ jupyter notebook

```

to autostart the browser and run the IPython kernel. You can select the python version when creating the notebook in the browser.

[bpython](http://bpython-interpreter.org/) is a ncurses interface to the Python interpreter, available in the official repositories as [bpython](https://www.archlinux.org/packages/?name=bpython) and [bpython2](https://www.archlinux.org/packages/?name=bpython2).

## See also

*   [Learning Python](http://shop.oreilly.com/product/9780596158071.do) is one of the most comprehensive, up to date, and well-written books on Python available today.
*   [Dive Into Python](http://www.diveintopython.net/) is an excellent (free) resource, but perhaps for more advanced readers and [has been updated for Python 3](http://getpython3.com/diveintopython3/).
*   [A Byte of Python](http://www.swaroopch.com/notes/Python) is a book suitable for users new to Python (and scripting in general).
*   [Learn Python The Hard Way](http://learnpythonthehardway.org) the best intro to programming.
*   [Learn Python](http://learnpython.org) nice site to learn python.
*   [Crash into Python](http://stephensugden.com/crash_into_python/) Also known as _Python for Programmers with 3 Hours_, this guide gives experienced developers from other languages a crash course on Python.
*   [Beginning Game Development with Python and Pygame: From Novice to Professional](http://www.apress.com/book/view/9781590598726) for games.
*   [Think Python: How to Think Like a Computer Scientist](http://www.greenteapress.com/thinkpython/) A great introduction to Python programming for beginners.
*   [Pythonspot](https://pythonspot.com) Great Python programming tutorials.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Python&oldid=411377](https://wiki.archlinux.org/index.php?title=Python&oldid=411377)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Programming languages](/index.php/Category:Programming_languages "Category:Programming languages")