**Состояние перевода:** На этой странице представлен перевод статьи [Python](/index.php/Python "Python"). Дата последней синхронизации: 21 декабря 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Python&diff=0&oldid=413030).

Из [Википедии](https://en.wikipedia.org/wiki/ru:Python "wikipedia:ru:Python"):

	*Python — высокоуровневый язык программирования общего назначения, ориентированный на повышение производительности разработчика и читаемости кода. Синтаксис ядра Python минималистичен. В то же время стандартная библиотека включает большой объём полезных функций.*

	*Python поддерживает несколько парадигм программирования, в том числе структурное, объектно-ориентированное, функциональное, императивное и аспектно-ориентированное. Основные архитектурные черты — динамическая типизация, автоматическое управление памятью, полная интроспекция, механизм обработки исключений, поддержка многопоточных вычислений и удобные высокоуровневые структуры данных. Код в Python организовывается в функции и классы, которые могут объединяться в модули (они, в свою очередь, могут быть объединены в пакеты).*

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Python 3](#Python_3)
    *   [1.2 Python 2](#Python_2)
*   [2 Решение проблемы с версией Python в скриптах сборки](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B5.D0.B9_Python_.D0.B2_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0.D1.85_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8)
*   [3 Включение автодополнения в оболочке Python](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B5_Python)
*   [4 Привязки к графическим библиотекам](#.D0.9F.D1.80.D0.B8.D0.B2.D1.8F.D0.B7.D0.BA.D0.B8_.D0.BA_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.BC_.D0.B1.D0.B8.D0.B1.D0.BB.D0.B8.D0.BE.D1.82.D0.B5.D0.BA.D0.B0.D0.BC)
*   [5 Старые версии](#.D0.A1.D1.82.D0.B0.D1.80.D1.8B.D0.B5_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8)
*   [6 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [python](https://www.archlinux.org/packages/?name=python) и/или [python2](https://www.archlinux.org/packages/?name=python2). Оба пакета доступны в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### Python 3

Python 3 - это свежая версия языка, несовместимая с Python 2\. Синтаксис в ней, по большей части, такой же, но многие вещи, например, то, как работают встроенные объекты наподобие словарей, значительно изменились, а многие устаревшие функции были окончательно удалены. Помимо этого стандартная библиотека была разбита на несколько отдельных частей. Чтобы подробнее узнать о различиях, прочитайте статью [Python2orPython3](http://wiki.python.org/moin/Python2orPython3), а также относящуюся к ней [главу](http://getpython3.com/diveintopython3/porting-code-to-python-3-with-2to3.html) книги "Погружение в Python 3".

Для получения свежей версии Python 3 [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [python](https://www.archlinux.org/packages/?name=python) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Если вы хотите собрать еще более свежую RC/бета-версию из исходников, посетите страницу [Python Downloads](http://www.python.org/download/). В [пользовательском репозитории Arch](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") также есть несколько отличных [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)")'ов. Если вы решили собрать RC-версию, обратите внимание, что исполняемый файл устанавливается (по умолчанию) в каталог `/usr/local/bin/python3.x`.

Начать работу над новым проектом внутри виртуального окружения (virtualenv) очень просто:

```
$ python -m venv newproj
$ source newproj/bin/activate
(newproj)$ pip install <dependency>

```

### Python 2

Для получения последней версии Python 2 [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [python2](https://www.archlinux.org/packages/?name=python2).

Python 2 будет успешно запускаться и функционировать, даже если в ваше системе также установлен Python 3\. Для использования этой версии необходимо прописать `python2`.

Любая программа, которой необходим Python 2, должна ссылаться на `/usr/bin/python2` вместо `/usr/bin/python`, который использует Python 3\. Чтобы добиться этого, откройте программу или скрипт в [текстовом редакторе](/index.php/List_of_applications/Documents_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A2.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D1.8B.D0.B5_.D1.80.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.BE.D1.80.D1.8B "List of applications/Documents (Русский)") и измените первую строку. Будет написано что-либо из этого:

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

Помимо этого, вы можете использовать [Python VirtualEnv](/index.php/Python_VirtualEnv "Python VirtualEnv"), в котором реализуется такой же способ "обмана" окружения: вызов `#!/usr/bin/env python`. Когда VirtualEnv активирован, он будет использовать исполняемый файл Python, указанный в переменной `$PATH`. Соответственно, если VirtualEnv установлен совместно с Python 2, будет использоваться Python 2.

Для начала [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [python2-virtualenv](https://www.archlinux.org/packages/?name=python2-virtualenv). Затем создайте каталог, содержащий VirtualEnv, при помощи следующей команды:

```
$ virtualenv2 venv

```

Активируйте VirtualEnv, который обновит значение переменной `$PATH`, заставив ее указывать на Python 2\. Помните, что эта активация действует только в текущем сеансе терминала:

```
$ source venv/bin/activate

```

После этого скрипты должны запускаться через Python 2.

## Решение проблемы с версией Python в скриптах сборки

Сборочные скрипты многих проектов предполагают, что `python` обращается к Python 2, и в конце концов это может привести к ошибке, обычно гласящей, что `print 'foo'` - неправильный синтаксис. К счастью, многие из них вызывают `python` через переменную `$PATH`, а не содержат в себе жестко прописанный `#!/usr/bin/python`. Благодаря этому, вместо редактирования установочных скриптов, вы можете создать файл `/usr/local/bin/python` с содержимым наподобие этого:

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

Где `/path/to/project1/*|/path/to/project2/*|/path/to/project3*` - список шаблонов, разделенных символом `|` и соответствующих всем веткам проекта.

Не забудьте сделать файл исполняемым:

```
# chmod +x /usr/local/bin/python

```

После этого соответствующие скрипты будут запускаться через Python 2.

## Включение автодополнения в оболочке Python

**Примечание:** Этот совет относится только к Python 2, начиная с версии 3.4 [автодополнение по клавише Tab](https://docs.python.org/3/tutorial/interactive.html) по умолчанию включено

Скопируйте следующее в интерактивную оболочку Python:

 `/usr/bin/python` 
```
import rlcompleter
import readline
readline.parse_and_bind("tab: complete")
```

Источник: [http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html](http://algorithmicallyrandom.blogspot.com.es/2009/09/tab-completion-in-python-shell-how-to.html).

## Привязки к графическим библиотекам

Доступны следующие привязки к [библиотекам графических элементов](https://en.wikipedia.org/wiki/widget_toolkit "wikipedia:widget toolkit"):

*   **TkInter** — привязки к Tk

	[http://wiki.python.org/moin/TkInter](http://wiki.python.org/moin/TkInter) || стандартный модуль

*   **pyQt** — привязки к [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")

	[http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro) || [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5)

*   **pySide** — привязки к [Qt](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)")

	[http://www.pyside.org/](http://www.pyside.org/) || [python2-pyside](https://www.archlinux.org/packages/?name=python2-pyside) [python-pyside](https://www.archlinux.org/packages/?name=python-pyside)

*   **pyGTK** — привязки к [GTK+ 2](/index.php/GTK%2B "GTK+")

	[http://www.pygtk.org/](http://www.pygtk.org/) || [pygtk](https://www.archlinux.org/packages/?name=pygtk)

*   **PyGObject** — привязки к [GTK+ 2/3](/index.php/GTK%2B "GTK+") при помощи GObject Introspection

	[https://wiki.gnome.org/PyGObject_ru](https://wiki.gnome.org/PyGObject_ru) || [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) [python2-gobject](https://www.archlinux.org/packages/?name=python2-gobject) [python-gobject2](https://www.archlinux.org/packages/?name=python-gobject2) [python-gobject](https://www.archlinux.org/packages/?name=python-gobject)

*   **wxPython** — привязки к wxWidgets

	[http://wxpython.org/](http://wxpython.org/) || [wxpython](https://www.archlinux.org/packages/?name=wxpython)

Для использования этих привязок в Python, скорее всего, потребуется установить соответствующие наборы библиотек.

## Старые версии

Устаревшие версии Python доступны в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") и могут быть полезны, если старые приложения не запускаются, вам необходимо протестировать работу своих программ или вас просто одолевает историческое любопытство:

*   [python15](https://aur.archlinux.org/packages/python15/): Python 1.5.2
*   [python24](https://aur.archlinux.org/packages/python24/): Python 2.4.6
*   [python25](https://aur.archlinux.org/packages/python25/): Python 2.5.6
*   [python26](https://aur.archlinux.org/packages/python26/): Python 2.6.9
*   [python30](https://aur.archlinux.org/packages/python30/): Python 3.0.1
*   [python31](https://aur.archlinux.org/packages/python31/): Python 3.1.5
*   [python32](https://aur.archlinux.org/packages/python32/): Python 3.2.5
*   [python33](https://aur.archlinux.org/packages/python33/): Python 3.3.5
*   [python34](https://aur.archlinux.org/packages/python34/): Python 3.4.3

По состоянию на июль 2014 г. Python upstream предоставляет обновления безопасности лишь для версий 2.7, 3.2, 3.3 и 3.4\. Использование других версий для работы приложений с непроверенным кодом или имеющих отношение к интернету может быть весьма опасным и не рекомендуется.

Дополнительные модули/библиотеки для старых версий Python можно найти в AUR по слову "python" с указанием версии без точки. Например, введите "python26" для поиска модулей версии 2.6.

## Советы и рекомендации

[IPython](http://ipython.org/) - это расширенная командная строка Python, доступная в официальных репозиториях в пакетах [ipython](https://www.archlinux.org/packages/?name=ipython) и [ipython2](https://www.archlinux.org/packages/?name=ipython2).

[bpython](http://bpython-interpreter.org/) - интерфейс ncurses для интерпретатора Python, доступный в официальных репозиториях в пакетах [bpython](https://www.archlinux.org/packages/?name=bpython) и [bpython2](https://www.archlinux.org/packages/?name=bpython2).

## Смотрите также

*   [Learning Python](http://shop.oreilly.com/product/9780596158071.do) - одна из самых исчерпывающих, актуальных и хорошо написанных книг про Python
*   [Dive Into Python](http://www.diveintopython.net/) - великолепный бесплатный ресурс, предназначенный для продвинутых пользователей и имеющий [обновленную версию для Python 3](http://getpython3.com/diveintopython3/)
*   [A Byte of Python](http://www.swaroopch.com/notes/Python) - книга, подходящая для тех, кто только начинает осваивать Python (и, в особенности, создание скриптов)
*   [Learn Python The Hard Way](http://learnpythonthehardway.org) - лучшее введение в программирование
*   [Learn Python](http://learnpython.org) - хороший ресурс для изучения Python
*   [Crash into Python](http://stephensugden.com/crash_into_python/) - также известное под названием *Python for Programmers with 3 Hours*, это руководство предоставляет опытным разработчикам на других языках интенсивный курс по освоению Python
*   [Beginning Game Development with Python and Pygame: From Novice to Professional](http://www.apress.com/book/view/9781590598726) - о разработке игр
*   [Pythonspot](https://pythonspot.com) - великолепные руководства по программированию на Python