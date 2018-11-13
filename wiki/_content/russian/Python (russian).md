Ссылки по теме

*   [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines")
*   [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment")
*   [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi")

**Состояние перевода:** На этой странице представлен перевод статьи [Python](/index.php/Python "Python"). Дата последней синхронизации: 2 июня 2017‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Python&diff=0&oldid=479061).

Из [Википедии](https://en.wikipedia.org/wiki/ru:Python "wikipedia:ru:Python"):

	Python — высокоуровневый язык программирования общего назначения, ориентированный на повышение производительности разработчика и читаемости кода. Синтаксис ядра Python минималистичен. В то же время стандартная библиотека включает большой объём полезных функций.

	Python поддерживает несколько парадигм программирования, в том числе структурное, объектно-ориентированное, функциональное, императивное и аспектно-ориентированное. Основные архитектурные черты — динамическая типизация, автоматическое управление памятью, полная интроспекция, механизм обработки исключений, поддержка многопоточных вычислений и удобные высокоуровневые структуры данных. Код в Python организовывается в функции и классы, которые могут объединяться в модули (они, в свою очередь, могут быть объединены в пакеты).

## Contents

*   [1 Установка](#Установка)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
    *   [1.3 Старые версии](#Старые_версии)
*   [2 Управление пакетами](#Управление_пакетами)
*   [3 Привязки к графическим библиотекам](#Привязки_к_графическим_библиотекам)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 IPython](#IPython)
    *   [4.2 Виртуальное окружение](#Виртуальное_окружение)
    *   [4.3 Включение автодополнения в оболочке Python2](#Включение_автодополнения_в_оболочке_Python2)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Проблемы с версией Python в скриптах сборки](#Проблемы_с_версией_Python_в_скриптах_сборки)
*   [6 Смотрите также](#Смотрите_также)

## Установка

### Python 3

Python 3 - это актуальная на данный момент версия языка, несовместимая с Python 2\. Синтаксис в ней, по большей части, такой же, но многие вещи, например, то, как работают встроенные объекты наподобие словарей и строк, значительно изменились, а многие устаревшие функции были окончательно удалены. Помимо этого стандартная библиотека была разбита на несколько отдельных частей. Чтобы подробнее узнать о различиях, прочитайте статью [Python2orPython3](https://wiki.python.org/moin/Python2orPython3), а также относящуюся к ней [главу](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) книги "Погружение в Python 3".

Для получения самой свежей версии Python 3 [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [python](https://www.archlinux.org/packages/?name=python).

Если вы хотите собрать еще более свежую RC/бета-версию из исходников, посетите страницу [Python Downloads](https://www.python.org/downloads/). В [пользовательском репозитории Arch](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") также есть несколько отличных [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)")'ов. Если вы решили собрать RC-версию, обратите внимание, что исполняемый файл устанавливается (по умолчанию) в каталог `/usr/local/bin/python3.x`.

### Python 2

Для получения последней версии Python 2 [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [python2](https://www.archlinux.org/packages/?name=python2).

Python 2 будет успешно запускаться и функционировать, даже если в ваше системе также установлен Python 3\. Для использования этой версии необходимо писать `python2`.

Любая программа, которой необходим Python 2, должна ссылаться на `/usr/bin/python2`, a не на `/usr/bin/python`, который указывает на Python 3\. Чтобы добиться этого, откройте программу или скрипт в [текстовом редакторе](/index.php/List_of_applications/Documents_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Текстовые_редакторы "List of applications/Documents (Русский)") и измените первую строку. Будет написано что-либо из этого:

```
#!/usr/bin/env python

```

или

```
#!/usr/bin/python

```

И в том, и в другом случае просто замените `python` на `python2`, и программа будет использовать Python 2.

Другой способ, избавляющий от необходимости редактировать скрипты - явно указывать префикс `python2`:

```
$ python2 *мой_скрипт.py*

```

Но бывают ситуации, в которых у вас нет возможности контролировать поведение скриптов. В этом случае можно попробовать обмануть окружение. Правда, такой трюк сработает, только если в скрипте прописано `#!/usr/bin/env python`: в случае с `#!/usr/bin/python` ничего не получится. Все это возможно благодаря указанию `env`, ищущему первое подходящее совпадение в переменной `PATH`.

Итак, для начала создайте необходимый каталог:

```
$ mkdir ~/bin

```

Затем создайте символьную ссылку `python`, указывающую на *python2*, и еще одну для конфигурационных скриптов:

```
$ ln -s /usr/bin/python2 ~/bin/python
$ ln -s /usr/bin/python2-config ~/bin/python-config

```

Наконец, добавьте ваш вновь созданный каталог *в начало* значения вашей переменной `PATH`:

```
$ export PATH=~/bin:$PATH

```

**Примечание:** Изменение [переменных окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") подобным образом не является долговременным и действует только в текущем сеансе терминала

Чтобы узнать, какая версия интерпретатора python будет использоваться, введите следующую команду:

```
$ which python

```

Еще один способ обмана окружения, который также основан на вызове `#!/usr/bin/env python` - использовать [#Виртуальное окружение](#Виртуальное_окружение).

### Старые версии

**Важно:** Все версии Python вплоть до 2.7 и 3.4 не получали никаких обновлений, в том числе обновлений безопасности, как минимум с 2014 г. Использование этих версий для работы приложений с непроверенным кодом или имеющих отношение к интернету может быть весьма опасным и не рекомендуется

Устаревшие версии Python доступны в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") и могут быть полезны, если вас одолевает историческое любопытство, если старые приложения не запускаются, или если вам необходимо протестировать свои программы на возможность работы в дистрибутивах, в которых используются старые версии интерпретатора (например, в RHEL 5.x это Python 2.4, а в Ubuntu 12.04 это Python 3.2):

*   Python 3.5: [python35](https://aur.archlinux.org/packages/python35/)
*   Python 3.4: [python34](https://aur.archlinux.org/packages/python34/)
*   Python 2.6: [python26](https://aur.archlinux.org/packages/python26/)
*   Python 2.5: [python25](https://aur.archlinux.org/packages/python25/)
*   Python 1.5: [python15](https://aur.archlinux.org/packages/python15/)

Дополнительные модули/библиотеки для старых версий Python можно найти в AUR по слову "python" с указанием версии без точки. Например, введите "python26" для поиска модулей версии 2.6.

## Управление пакетами

Огромное количество пакетов Python доступно в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"), однако экосистема Python предоставляет свои собственные пакетные менеджеры, работающие с [PyPI](https://pypi.python.org/) (Python Package Index):

*   **pip** — PyPA, инструмент установки пакетов Python

	[https://pip.pypa.io/](https://pip.pypa.io/) || [python-pip](https://www.archlinux.org/packages/?name=python-pip), [python2-pip](https://www.archlinux.org/packages/?name=python2-pip)

*   **setuptools** — с легкостью скачивайте, собирайте, устанавливайте, обновляйте и удаляйте пакеты Python

	[https://setuptools.readthedocs.io/](https://setuptools.readthedocs.io/) || [python-setuptools](https://www.archlinux.org/packages/?name=python-setuptools), [python2-setuptools](https://www.archlinux.org/packages/?name=python2-setuptools)

Для просмотра краткой истории и сравнения этих двух утилит, обратитесь к странице [pip vs easy_install](https://packaging.python.org/pip_easy_install/#pip-vs-easy-install). Общепризнанные лучшие практики управления пакетами Python описаны [здесь](https://packaging.python.org/).

Если вы собираетесь использовать *pip*, используйте его в [виртуальном окружении](#Виртуальное_окружение) или с опцией `--user` (`pip install --user`), чтобы избежать конфликтов между пакетами в каталоге `/usr`. Во всех случаях предпочтительный способ установки программного обеспечения - это [использование pacman](/index.php/System_maintenance_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Используйте_менеджер_пакетов_для_установки_программного_обеспечения "System maintenance (Русский)").

**Примечание:** Существуют инструменты, автоматически генерирующие PKGBUILDы для пакетов *pip* и таким образом интегрирующие его в *pacman*: [pipman-git](https://aur.archlinux.org/packages/pipman-git/), [pip2arch-git](https://aur.archlinux.org/packages/pip2arch-git/)

## Привязки к графическим библиотекам

Доступны следующие привязки к [библиотекам графических элементов](https://en.wikipedia.org/wiki/widget_toolkit "wikipedia:widget toolkit"):

*   **TkInter** — привязки к Tk

	[https://wiki.python.org/moin/TkInter](https://wiki.python.org/moin/TkInter) || стандартный модуль

*   **pyQt** — привязки к [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")

	[https://riverbankcomputing.com/software/pyqt/intro](https://riverbankcomputing.com/software/pyqt/intro) || [python2-pyqt4](https://aur.archlinux.org/packages/python2-pyqt4/) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://aur.archlinux.org/packages/python-pyqt4/) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide** — привязки к [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")

	[https://wiki.qt.io/PySide](https://wiki.qt.io/PySide) || [python2-pyside](https://aur.archlinux.org/packages/python2-pyside/) [python-pyside](https://aur.archlinux.org/packages/python-pyside/)

*   **pyGTK** — привязки к [GTK+ 2](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)")

	[http://www.pygtk.org/](http://www.pygtk.org/) || [pygtk](https://www.archlinux.org/packages/?name=pygtk)

*   **PyGObject** — привязки к [GTK+ 2/3](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GTK+ (Русский)") при помощи GObject Introspection

	[https://wiki.gnome.org/PyGObject_ru](https://wiki.gnome.org/PyGObject_ru) || [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) [python-gobject2](https://www.archlinux.org/packages/?name=python-gobject2) [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

*   **wxPython** — привязки к wxWidgets

	[https://wxpython.org/](https://wxpython.org/) || [wxpython](https://www.archlinux.org/packages/?name=wxpython)

Для использования этих привязок в Python, скорее всего, потребуется доустановить соответствующие наборы библиотек.

## Советы и рекомендации

### IPython

[IPython](http://ipython.org/) - это расширенная командная строка Python, доступная в официальных репозиториях в пакетах [ipython](https://www.archlinux.org/packages/?name=ipython) и [ipython2](https://www.archlinux.org/packages/?name=ipython2). Если вы хотите использовать IPython notebook, установите пакет [jupyter-notebook](https://www.archlinux.org/packages/?name=jupyter-notebook) для IPython3 или [ipython2-notebook](https://www.archlinux.org/packages/?name=ipython2-notebook) для IPython2\. Затем выполните:

```
$ jupyter notebook

```

чтобы запустить браузер, а в нем - ядро IPython. Вы можете выбрать версию *python* при создании notebook в браузере.

[bpython](https://bpython-interpreter.org/) - интерфейс ncurses для интерпретатора Python, доступный в официальных репозиториях в пакетах [bpython](https://www.archlinux.org/packages/?name=bpython) и [bpython2](https://www.archlinux.org/packages/?name=bpython2).

### Виртуальное окружение

Python предоставляет инструменты для создания изолированных окружений, в которых вы можете устанавливать пакеты, не влияя и никак не взаимодействуя ни на другие виртуальные окружения, ни на системные пакеты Python. Таким образом, в частности, можно изменить интерпретатор *python* для конкретного приложения.

Для получения дополнительной информации смотрите статью [Python/Virtual environment](/index.php/Python/Virtual_environment "Python/Virtual environment").

### Включение автодополнения в оболочке Python2

Начиная с версии Python 3.4, [автодополнение по клавише Tab](https://docs.python.org/3/tutorial/interactive.html) включено по умолчанию. Для Python 2 вы можете включить его самостоятельно, добавив следующие строки в файл, к которому обращается переменная окружения `PYTHONSTARTUP`: [[1]](https://algorithmicallyrandom.blogspot.co.at/2009/09/tab-completion-in-python-shell-how-to.html)

```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")

```

## Решение проблем

### Проблемы с версией Python в скриптах сборки

Сборочные скрипты многих проектов предполагают, что `python` обращается к Python 2, и в конце концов это может привести к ошибке, обычно гласящей, что `print 'foo'` - неправильный синтаксис. К счастью, многие из них вызывают *python* через переменную окружения `PATH`, а не содержат в себе жестко прописанный `#!/usr/bin/python`. Благодаря этому, вместо редактирования установочных скриптов, вы можете создать файл `/usr/local/bin/python` с содержимым наподобие этого:

 `/usr/local/bin/python` 
```
#!/bin/bash
script=$(readlink -f -- "$1")
case "$script" in (/путь/к/проекту1/*|/путь/к/проекту2/*|/путь/к/проекту3*)
    exec python2 "$@"
    ;;
esac

exec python3 "$@"

```

Где `/путь/к/проекту1/*|/путь/к/проекту2/*|/путь/к/проекту3*` - список шаблонов, разделенных символом `|` и соответствующих всем веткам проекта.

Не забудьте сделать файл [исполняемым](/index.php/Help:Reading#Make_executable "Help:Reading"). После этого соответствующие скрипты будут запускаться через Python 2.

## Смотрите также

*   [O'Reilly's Learning Python, пятое издание](http://shop.oreilly.com/product/0636920028154.do) коммерческое
*   [Dive Into Python](http://www.diveintopython.net/), [Dive Into Python3](http://getpython3.com/diveintopython3/)
*   [A Byte of Python](https://python.swaroopch.com/)
*   [Learn Python the Hard Way](https://learnpythonthehardway.org/)
*   [Learn Python](https://learnpython.org/)
*   [Crash into Python](https://stephensugden.com/crash_into_python/) (предполагает владение другими языками программирования)
*   [Beginning Game Development with Python and Pygame](https://www.apress.com/book/9781590598726) коммерческое
*   [Think Python](http://www.greenteapress.com/thinkpython/)
*   [Pythonspot](https://pythonspot.com)