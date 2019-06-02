Related articles

*   [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines")
*   [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment")
*   [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi")
*   [Django](/index.php/Django "Django")

От [Уикипедия](https://en.wikipedia.org/wiki/bg:Python "wikipedia:bg:Python"):

	Python е интерпретируем, интерактивен, обектно-ориентиран език за програмиране, създаден от Гуидо ван Росум в началото на 90-те години. Кръстен е на телевизионното шоу на BBC „Monty Python’s Flying Circus“. Често бива сравняван с Tcl, Perl, Scheme, Java и Ruby.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Инсталиране](#Инсталиране)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
    *   [1.3 Други имплементации](#Други_имплементации)
    *   [1.4 Стари версии](#Стари_версии)
*   [2 Управление на Python пакети](#Управление_на_Python_пакети)
*   [3 Widget bindings](#Widget_bindings)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Alternative shells](#Alternative_shells)
    *   [4.2 Virtual environment](#Virtual_environment)
    *   [4.3 Tab completion in Python shell](#Tab_completion_in_Python_shell)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Dealing with version problem in build scripts](#Dealing_with_version_problem_in_build_scripts)
*   [6 See also](#See_also)

## Инсталиране

### Python 3

Python 3 е последната версия на езика и тя е несъвместима с Python 2\. Като цяло, езикът е същият, но много детайли, включително това как работят вградените обекти като речници и стрингове, са променени значително и много от остарелите характеристики на езика са най-сетне изтрити. Също така, стандартната библиотека е разделена на няколко важни части. Посетете [Python2orPython3](https://wiki.python.org/moin/Python2orPython3) и съответно [тази глава](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) в Dive into Python 3 книгата за общ преглед на разликите между двете версии.

За да инсталирате последната версия на Python 3, [инсталирайте](/index.php/%D0%98%D0%BD%D1%81%D1%82%D0%B0%D0%BB%D0%B8%D1%80%D0%B0%D0%B9%D1%82%D0%B5 "Инсталирайте") [python](https://www.archlinux.org/packages/?name=python) пакета.

Ако искате да компилирате последното [RC](https://en.wikipedia.org/wiki/Software_release_life_cycle#Release_candidate "wikipedia:Software release life cycle") или бета от изходния код, посетете [Изтегляне на Python](https://www.python.org/downloads/). [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") също съдържа добри [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")-ове. Ако не компилирате от изходен код, тогава по подразбиране бинарният пакет се инсталира в `/usr/local/bin/python3.x`.

### Python 2

За да инсталирате последната версия на Python 2, [инсталирайте](/index.php/%D0%98%D0%BD%D1%81%D1%82%D0%B0%D0%BB%D0%B8%D1%80%D0%B0%D0%B9%D1%82%D0%B5 "Инсталирайте") [python2](https://www.archlinux.org/packages/?name=python2) пакета.

Не е проблем да имате инсталирани и двете версии на Python. Тази версия се изпълнява от `python2` командата.

Всяка програма, работеща с Python 2 трябва да използва `/usr/bin/python2` вместо `/usr/bin/python`, което е свързано с Python 3\. За да го настроите, отворете програмата (или скрипта) в любимия си текстов редактор и променете първия ред. Той ще изглежда подобно на:

```
#!/usr/bin/env python

```

или

```
#!/usr/bin/python

```

И в двата случая просто променете `python` на `python2` и програмата ще използва Python 2 вместо Python 3.

Друг начин за налагането на python2 над програмата, без да се променя тя, е изричното ѝ извикване с `python2`:

```
$ python2 *myScript.py*

```

В случай, че нямате контрол над извикването на програмата, съществува начин за подлъгването на средата, в която се изпълнява. Работи само ако програмата използва `#!/usr/bin/env python`. Няма да проработи с `#!/usr/bin/python`. Подлъгването се състои в търсенето на `env` за съответния запис в `PATH` системната променлива.

Първо си създайте примерна папка:

```
$ mkdir ~/bin

```

След това добавете символична връзка (symlink) `python` към *python2* и конфигурационните скриптове в папката:

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

Най-накрая добавете новата папка *в началото* на вашата `PATH` системна променлива:

```
$ export PATH=~/bin:$PATH

```

**Note:** Този метод на променяне на системни променливи не е постоянен и е валиден само за текущата терминална сесия.

За да проверите кой python интерпретатор се използва от `env`, използвайте следната команда:

```
$ which python

```

Подобен подход за подлъгване на средата, който също зависи от това `#!/usr/bin/env python` да бъден извикан от изпълняващата програма, е да се използва виртуална среда ([virtual environment](#Virtual_environment)).

### Други имплементации

Python може да се разглежда като спецификация за програмен език, която може да бъде имплементирана по много различни начини. Горните раздели са свързани с референтната имплементация на Python (имплементацията по подразбиране), наречена CPython. Някои други известни имплементации са:

*   [PyPy](/index.php/PyPy "PyPy") е Python 2.7/3.5 имплементация, използваща JIT компилатор. Тя е по-бърза и използва по-малко памет, но не е напълно съвместима с CPython (макар че повечето код и пакети ще работят без необходима промяна).
*   [Jython](http://www.jython.org/) е Python 2.7 имплементация, написана на Java. Тя позволява лесно интегриране на Python и Java код, но също не е напълно съвместима с всички CPython библиотеки. Често се използва, за да позволи използването на Python като скриптов език в по-големи Java приложения.
*   [IronPython](http://ironpython.net/) е Python 2.7 имплементация, написана на .NET - тя е много подобна на Jython, но е съвместима с езици, които работят върху .NET платформата(като C#/VB).
*   [MicroPython](https://micropython.org/) е ограничена Python 3.4 имплементация, насочена към микроконтролери и други вградени системи (като UEFI), като е несъвместима с повечето стандартни пакети заради [малки промени в синтаксиса и много ограничена стандартна библиотека](http://docs.micropython.org/en/latest/pyboard/genrst/index.html). Често се използва за прототипиране във вградените системи, тъй като осигурява Python [REPL](https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop "wikipedia:Read–eval–print loop").
*   [Съществуват и още имплементации](https://en.wikipedia.org/wiki/Python_(programming_language)#Implementations "wikipedia:Python (programming language)"), въпреки че повечето вече не се поддържат заради подобренията в по-известните имплементации.

### Стари версии

**Warning:** Версии на Python, по-стари от 2.7 и съответно 3.4, не са получавали актуализации—включително пачове за сигурност—от поне 2014 година. Използването на по-стари версии за интернет-ориентирани приложения или за несигурен/непроверяван код може да бъде опасно и не се препоръчва.

Стари версии на Python има в [AUR](/index.php/AUR "AUR") и могат да бъдат от полза за проследяването на развитието на езика, стари приложения, които не вървят на новите версии на езика, или за тестването на Python програми, предназначени за изпълнение в среда, която разполага с по-стара версия на Python:

*   Python 3.6: [python36](https://aur.archlinux.org/packages/python36/)
*   Python 3.5: [python35](https://aur.archlinux.org/packages/python35/)
*   Python 3.4: [python34](https://aur.archlinux.org/packages/python34/)
*   Python 2.6: [python26](https://aur.archlinux.org/packages/python26/)
*   Python 2.5: [python25](https://aur.archlinux.org/packages/python25/)
*   Python 1.5: [python15](https://aur.archlinux.org/packages/python15/)

Допълнителни модули/библиотеки за старите версии на Python могат да бъдат намерени в AUR, като търсите `python<*версия без разделителна точка*>`, примерно "python26" за 2.6 модули.

## Управление на Python пакети

Въпреки че много Python пакети са вече достъпни в [официалните репозиторита](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D0%BD%D0%B8%D1%82%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D1%82%D0%B0 "Официалните репозиторита") и [AUR](/index.php/AUR "AUR"), екосистемата на Python осигурява собствени мениджъри на пакети за работа с [PyPI](https://pypi.org/) - репозитори съдържащо хиляди Python пакети:

*   **pip** — PyPA инструмент за инсталиране на пакети.

	[https://pip.pypa.io/](https://pip.pypa.io/) || [python-pip](https://www.archlinux.org/packages/?name=python-pip), [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)

*   **setuptools** — Лесно теглене, билдване, инсталиране, актуализиране и деинсталиране на пакети.

	[https://setuptools.readthedocs.io/](https://setuptools.readthedocs.io/) || [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools), [python2-setuptools](https://www.archlinux.org/packages/?name=python2-setuptools)

За кратко сравнение между двете, посетете [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install). Добри практики за управлението на Python пакети са разгледани [тук](https://packaging.python.org/).

Ако се налага да използвате *pip*, използвайте [виртуална среда](#Virtual_environment), или `pip install --user`, за да избегнете конфликти с пакети, намиращи се в `/usr`. Винаги е за предпочитане [да използвате pacman за инсталиране на софтуер](/index.php/System_maintenance#Use_the_package_manager_to_install_software "System maintenance").

**Note:** Съществуват инструменти за интегриране на *pip* с *pacman* чрез автоматично генериране на PKGBUILD-ове за съответните pip пакети: вижте [Creating packages#PKGBUILD generators](/index.php/Creating_packages#PKGBUILD_generators "Creating packages").

**Tip:** [pipenv](https://docs.pipenv.org/) осигурява единичен конзолен интерфейс за [Pipfile](https://github.com/pypa/pipfile), *pip* и [virtualenv](/index.php/Virtualenv "Virtualenv"). Достъпен е като [python-pipenv](https://www.archlinux.org/packages/?name=python-pipenv) и [python2-pipenv](https://www.archlinux.org/packages/?name=python2-pipenv).

## Widget bindings

The following [widget toolkit](https://en.wikipedia.org/wiki/Widget_toolkit "wikipedia:Widget toolkit") bindings are available:

*   **TkInter** — Tk bindings

	[https://wiki.python.org/moin/TkInter](https://wiki.python.org/moin/TkInter) || standard module

*   **pyQt** — [Qt](/index.php/Qt "Qt") bindings

	[https://riverbankcomputing.com/software/pyqt/intro](https://riverbankcomputing.com/software/pyqt/intro) || [python2-pyqt4](https://aur.archlinux.org/packages/python2-pyqt4/) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://aur.archlinux.org/packages/python-pyqt4/) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide2** — [Qt](/index.php/Qt "Qt") bindings

	[https://wiki.qt.io/PySide2](https://wiki.qt.io/PySide2) || [pyside2](https://www.archlinux.org/packages/?name=pyside2) [pyside2-tools](https://www.archlinux.org/packages/?name=pyside2-tools)

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

*   **ptpython** — Fancy interface for the Python interpreter based on [prompt-toolkit](https://github.com/jonathanslenders/python-prompt-toolkit) input interface.

	[https://github.com/jonathanslenders/ptpython](https://github.com/jonathanslenders/ptpython) || [ptpython](https://aur.archlinux.org/packages/ptpython/) [ptpython2](https://aur.archlinux.org/packages/ptpython2/)

### Virtual environment

Python provides tools to create isolated environments in which you can install packages without interfering with the other virtual environments nor with the system Python's packages. It could change the *python* interpreter used for a specific application.

See [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment") for details.

### Tab completion in Python shell

Since Python 3.4 [tab completion](https://docs.python.org/3/tutorial/interactive.html) is enabled by default, for Python 2 you can manually enable it by adding the following lines to a file referenced by the `PYTHONSTARTUP` environment variable: [[1]](https://docs.python.org/2/library/rlcompleter.html)

```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")

```

Note that readline completer will only complete names in the global namespace. You can rely on [python-jedi](https://www.archlinux.org/packages/?name=python-jedi) and/or [python2-jedi](https://www.archlinux.org/packages/?name=python2-jedi) for a more richer tab completion experience [[2]](https://jedi.readthedocs.io/en/latest/docs/usage.html#tab-completion-in-the-python-shell).

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