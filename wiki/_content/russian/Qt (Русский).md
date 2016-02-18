[Qt](http://qt-project.org/) — кроссплатформенный набор инструментов для создания приложений и виджетов, который использует стандартный язык программирования C++, а также специальный генератор кода ([Meta Object Compiler](http://qt-project.org/doc/qt-4.8/moc.html), или *moc*) вместе с набором макросов, расширяющих возможности языка. Набор предоставляет широкие возможности по разработке приложений; среди наиболее важных:

*   Работа на основных компьютерных платформах и операционных системах, а также на некоторых мобильных платформах.
*   Обширная поддержка возможностей интернационализации.
*   Полнофункциональная библиотека с поддержкой SQL баз данных, парсинга XML, управления потоками, сети и унифицированный кроссплатформенный программный интерфейс (API) для работы с файлами.

На основе фреймворка Qt развивается сообщество и программное обеспечение [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)"). Qt лежит в основе других важных проприетарных и открытых программных проектов, таких как [VLC](/index.php/VLC "VLC"), [VirtualBox](/index.php/VirtualBox "VirtualBox"), [Opera](/index.php/Opera "Opera"), [Mathematica](/index.php/Mathematica "Mathematica"), [Skype](/index.php/Skype "Skype") и многих других.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Выбор набора Qt по умолчанию](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.BD.D0.B0.D0.B1.D0.BE.D1.80.D0.B0_Qt_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [2.1 Используя переменные окружения](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BE.D0.BA.D1.80.D1.83.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.2 Используя файл конфигурации](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
*   [3 Внешний вид](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B9_.D0.B2.D0.B8.D0.B4)
    *   [3.1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [3.1.1 Темы](#.D0.A2.D0.B5.D0.BC.D1.8B)
        *   [3.1.2 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
        *   [3.1.3 Значки](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8)
    *   [3.2 Ручная настройка](#.D0.A0.D1.83.D1.87.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.3 Таблицы стилей Qt](#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D1.8B_.D1.81.D1.82.D0.B8.D0.BB.D0.B5.D0.B9_Qt)
    *   [3.4 GTK+ и Qt](#GTK.2B_.D0.B8_Qt)
*   [4 Разработка](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BA.D0.B0)
    *   [4.1 Поддержка платформ](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.BF.D0.BB.D0.B0.D1.82.D1.84.D0.BE.D1.80.D0.BC)
    *   [4.2 Инструменты](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D1.8B)
    *   [4.3 Другие языки программирования](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D1.8F.D0.B7.D1.8B.D0.BA.D0.B8_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [4.3.1 C++](#C.2B.2B)
        *   [4.3.2 QML](#QML)
        *   [4.3.3 Python (PyQt)](#Python_.28PyQt.29)
        *   [4.3.4 Python (PySide)](#Python_.28PySide.29)
        *   [4.3.5 C#](#C.23)
        *   [4.3.6 Ruby](#Ruby)
        *   [4.3.7 Java](#Java)
        *   [4.3.8 Perl](#Perl)
        *   [4.3.9 Lua](#Lua)
*   [5 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

В настоящее время две версии Qt доступны в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"). Они могут быть [установлены](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") со следующими пакетами:

*   **Qt 5.x** входит в пакет [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), документация — [qt5-doc](https://www.archlinux.org/packages/?name=qt5-doc).
*   **Qt 4.x** предоставляется пакетом [qt4](https://www.archlinux.org/packages/?name=qt4), документация — [qt4-doc](https://aur.archlinux.org/packages/qt4-doc/).
*   **Qt 3.x** можно установить из [AUR](/index.php/AUR "AUR") с пакетом [qt3](https://aur.archlinux.org/packages/qt3/), документация — [qt3-doc](https://aur.archlinux.org/packages/qt3-doc/).

**Важно:** Пакеты Qt больше не помещают исполняемые файлы утилит вроде *qmake* в `/usr/bin`. Вместо этого создаются символические ссылки с суффиксом версии, например `qmake-qt5`, `qmake-qt4`, `qmake-qt3`. Это может вызвать проблемы со сборкой проектов для Qt версий 3 и 4\. Как установить исполняемые файлы в `/usr/bin` показано в разделе [#Выбор набора Qt по умолчанию](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.BD.D0.B0.D0.B1.D0.BE.D1.80.D0.B0_Qt_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E).

## Выбор набора Qt по умолчанию

Установив [qtchooser](https://www.archlinux.org/packages/?name=qtchooser), вы сможете выбрать, для какого набора Qt из установленных необходимо перенести исполняемые файлы (например, *qmake*) в `/usr/bin`. По умолчанию используется Qt5.

### Используя переменные окружения

Чтобы выбрать конкретный набор Qt, вы можете создать [переменную окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)") `QT_SELECT`. Например, чтобы выбрать Qt4, добавьте `export QT_SELECT=4` в файл инициализации вашей командной оболочки (например, `~/.bash_profile` или `~/.zsh_profile`).

### Используя файл конфигурации

Вы можете выбрать версию набора Qt по умолчанию, создав символическую ссылку `~/.config/qtchooser/default.conf` на один из файлов *.conf* в каталоге `/etc/xdg/qtchooser`. Например, чтобы выбрать Qt4, создайте ссылку на `/etc/xdg/qtchooser/4.conf`:

```
$ ln -s `/etc/xdg/qtchooser/4.conf` `~/.config/qtchooser/default.conf`

```

## Внешний вид

### Настройка

Приложения Qt, по возможности, пытаются подражать внешнему вид и поведению других приложений в той среде рабочего стола, где они запускаются. Если вы хотите поменять внешний вид и поведение интерфейса приложения Qt, вы можете использовать утилиту Qt Configuration (*qtconfig-qt4* или *qt3config*). Она позволяет легко и просто настроить внешний вид приложений: стиль, цвета, шрифты и многие другие параметры.

Обратите внимание, что утилита была исключена в версии Qt5\. Если вы хотите принудительно установить внешний вид и поведение интерфейса приложений Qt5, установите переменную окружения `QT_STYLE_OVERRIDE` с названием желаемого стиля (например, `gtk`).

Панель KDE System Settings (Настройки Системы) также предоставляет доступ ко многим параметрам графического интерфейса, которые используются в приложениях Qt.

#### Темы

Несколько стилей поставляются вместе с Qt, например GTK+, Windows или CDE, однако вы можете установить многие другие стили из официальных репозиториев или [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") (большинство созданы для рабочего стола KDE):

*   **[Oxygen](https://en.wikipedia.org/wiki/Oxygen_Project "wikipedia:Oxygen Project")** — Одна из стандартных тем рабочего стола KDE.

	[http://www.oxygen-icons.org/](http://www.oxygen-icons.org/) || [kdebase-runtime](https://www.archlinux.org/packages/?name=kdebase-runtime)

*   **QtCurve** — Очень гибкая в настройке и популярная тема рабочего стола с поддержкой приложений GTK+ и Qt.

	[http://kde-look.org/content/show.php?content=40492](http://kde-look.org/content/show.php?content=40492) || [qtcurve](https://www.archlinux.org/groups/x86_64/qtcurve/)

*   **Skulpture** — Еще одна тема для KDE и Qt.

	[http://kde-look.org/content/show.php/?content=59031](http://kde-look.org/content/show.php/?content=59031) || [skulpture](https://aur.archlinux.org/packages/skulpture/)

*   **Polymer** — Порт темы KDE Plastik для Qt3.

	[http://kde-look.org/content/show.php?content=21748](http://kde-look.org/content/show.php?content=21748) || [polymer](https://aur.archlinux.org/packages/polymer/)

*   **Bespin** — Тема KDE с широкими возможностями настройки.

	[http://cloudcity.sourceforge.net/frame.php](http://cloudcity.sourceforge.net/frame.php) || [bespin-svn](https://aur.archlinux.org/packages/bespin-svn/)

#### Шрифты

Шрифты в Qt могут быть настроены с помощью Qt Configuration в меню `Fonts` → `Default Font`.

**Обратите внимание:** Если у вас рабочий стол GTK+ (например, вы используете [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") или [Xfce](/index.php/Xfce_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xfce (Русский)")), и опция `GUI Style` установлена в `Desktop Settings (default)` или `GTK+`, эта настройка будет проигнорирована.

#### Значки

С помощью Qt Configuration нельзя установить тему значков, но, так как Qt следует [спецификации именования значков Freedesktop.org](http://standards.freedesktop.org/icon-naming-spec/icon-naming-spec-latest.html), любая тема установленная для [X](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)") будет использоваться и в Qt.

### Ручная настройка

Qt хранит все настройки в файле `~/.config/Trolltech.conf`. В его содержимом довольно трудно ориентироваться, так как он содержит множество опций не связанных с внешним видом приложений. Однако, для внесения любых изменений вы можете всего-лишь дописать новые значения в конец файла и тем самым переопределить любые ранее установленные значения (убедитесь, что добавляете свои изменения в секцию `[Qt]`).

Например, чтобы изменить тему на QtCurve, добавьте:

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=QtCurve

```

### Таблицы стилей Qt

Интересным способом модификации внешнего вида приложений Qt является использование таблиц стилей, которые представляют собой обычные CSS-файлы. Используя таблицы стилей, пользователь может изменить внешний вид любого виджета в приложении.

Чтобы запустить приложение, используя указанную таблицу стилей просто передайте путь к файлу в опции `--stylesheet`:

```
$ qt_application --stylesheet *style.qss*

```

Для получения подробной информации о таблицах стилей Qt смотрите [официальную документацию](http://qt-project.org/doc/qt-4.8/stylesheet-reference.html) или [руководство](http://thesmithfam.org/blog/2009/09/10/qt-stylesheets-tutorial/). Пример таблицы стилей вы можете найти на [этой странице](http://kde-apps.org/content/show.php/roxydoxy?content=125979).

### GTK+ и Qt

Если вы используете одновременно приложения GTK+ и Qt, их внешний вид может несколько различаться. Если вы хотите, чтобы стили отображения в точности соответствовали друг другу, смотрите статью [Единый вид приложений GTK и Qt](/index.php/Uniform_Look_for_QT_and_GTK_Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Uniform Look for QT and GTK Applications (Русский)").

## Разработка

### Поддержка платформ

Qt поддерживает большинство доступных сегодня платформ, включая даже весьма малоизвестные. Полный список поддерживаемых платформ вы можете найти в [статье на Wikipedia](https://en.wikipedia.org/wiki/Qt_(framework)#Platforms "wikipedia:Qt (framework)").

### Инструменты

Список официальных инструментов разработки для Qt:

*   **[Qt Creator](https://en.wikipedia.org/wiki/ru:Qt_Creator "wikipedia:ru:Qt Creator")** — Кроссплатформенная среда разработки, созданная для разработки приложений Qt.

	[http://qt-project.org/doc/qtcreator/](http://qt-project.org/doc/qtcreator/) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **Qt Linguist** — Набор инструментов для упрощения перевода и интернационализации приложений Qt.

	[http://qt-project.org/doc/qt-4.8/linguist-manual.html](http://qt-project.org/doc/qt-4.8/linguist-manual.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **Qt Assistant** — Справочная система для чтения документации по Qt.

	[http://qt-project.org/doc/qt-4.8/assistant-manual.html](http://qt-project.org/doc/qt-4.8/assistant-manual.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **Qt Designer** — Инструмент для разметки графического интерфейса приложений Qt и создания форм для виджетов.

	[http://qt-project.org/doc/qt-4.8/designer-manual.html](http://qt-project.org/doc/qt-4.8/designer-manual.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **Qt Quick Designer** — Визуальный редактор файлов QML, поддерживающий режим WYSIWYG. Он позволяет с нуля проектировать и разрабатывать приложения и компоненты Qt Quick.

	[http://qt-project.org/doc/qtcreator-2.8/creator-using-qt-quick-designer.html](http://qt-project.org/doc/qtcreator-2.8/creator-using-qt-quick-designer.html) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **QML Viewer** — Инструмент для быстрой разработки и отладки приложений QML.

	[http://qt-project.org/doc/qt-4.8/qmlviewer.html](http://qt-project.org/doc/qt-4.8/qmlviewer.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **[qmake](https://en.wikipedia.org/wiki/Qmake "wikipedia:Qmake")** — Средство автоматизации процесса сборки приложений Qt на различных платформах, похожее на [cmake](https://en.wikipedia.org/wiki/ru:CMake "wikipedia:ru:CMake"), но с меньшим количеством опции и ориентированное на приложения Qt.

	[https://qt-project.org/doc/qt-4.8/qmake-manual.html](https://qt-project.org/doc/qt-4.8/qmake-manual.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **uic** — Генератор кода C++ на основе *.ui*-файлов.

	[http://qt-project.org/doc/qt-4.8/uic.html](http://qt-project.org/doc/qt-4.8/uic.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **rcc** — Инструмент для упаковки ресурсов (например, изображений) в приложение при сборке. По сути генерирует код на C++, содержащий данные, указанные в файле ресурсов (*.qrc*).

	[http://qt-project.org/doc/qt-4.8/rcc.html](http://qt-project.org/doc/qt-4.8/rcc.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **moc** — Препроцессор исходных файлов, обрабатывающий расширения Qt для C++ (например, директивы механизма сигналов и слотов, RTTI, аннотации).

	[http://doc.qt.digia.com/4.7-snapshot/moc.html](http://doc.qt.digia.com/4.7-snapshot/moc.html) || [qt4](https://www.archlinux.org/packages/?name=qt4)

### Другие языки программирования

Qt имеет привязки ко многим популярным языкам программирования. Полный список поддерживаемых языков вы можете найти в статье [Qt в Wikipedia](https://en.wikipedia.org/wiki/Qt_(framework)#Programming_language_bindings "wikipedia:Qt (framework)").

Приведенные ниже примеры отображают окно с сообщением 'Hello world!'.

#### C++

*   Пакет: [qt4](https://www.archlinux.org/packages/?name=qt4)
    *   [qt4](https://www.archlinux.org/packages/?name=qt4) — версия 4.x
    *   [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) — версия 5.x
*   Сайт: [http://qt-project.org/](http://qt-project.org/)
*   Команда сборки:
    *   Версия Qt4: `g++ $(pkg-config --cflags --libs QtGui) -o hello hello.cpp`
    *   Версия Qt5: `g++ $(pkg-config --cflags --libs Qt5Widgets) -o hello hello.cpp`
*   Команда запуска: `./hello`

 `hello.cpp` 
```
#include <QApplication>
#include <QLabel>

int main(int argc, char **argv)
{
    QApplication app(argc, argv);
    QLabel hello("Hello world!");

    hello.show();
    return app.exec();
}

```

#### QML

*   Пакет: [qt4](https://www.archlinux.org/packages/?name=qt4) или [qt5-declarative](https://www.archlinux.org/packages/?name=qt5-declarative).
*   Сайт: [http://qt-project.org/](http://qt-project.org/)
*   Команда запуска: `qmlviewer-qt4 hello.qml`

 `hello.qml` 
```
import QtQuick 1.0

Rectangle {
    id: page
    width: 400; height: 100
    color: "lightgray"

    Text {
        id: helloText
        text: "Hello world!"
        anchors.horizontalCenter: page.horizontalCenter
        anchors.verticalCenter: page.verticalCenter
        font.pointSize: 24; font.bold: true
    }
}

```

**Обратите внимание:** Для Qt 5.x нужно импортировать QtQuick 2.y.

#### Python (PyQt)

*   Пакеты:
    *   [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) — привязки Python 3.x для Qt 4
    *   [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) — привязки Python 2.x для Qt 4
    *   [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5) — привязки Python 3.x для Qt 5
    *   [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) — привязки Python 2.x для Qt 5
*   Сайт: [http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro)
*   Команда запуска: `python hello-pyqt.py` или `python2 hello-pyqt.py`.

 `hello-pyqt.py` 
```
import sys
from PyQt4 import QtGui

app = QtGui.QApplication(sys.argv)
label = QtGui.QLabel("Hello world!")

label.show()
sys.exit(app.exec_())

```

The Qt 5.x version is slighly different:

 `hello-pyqt.py` 
```
import sys
from PyQt5 import QtWidgets

app = QtWidgets.QApplication(sys.argv)
label = QtWidgets.QLabel("Hello world!")

label.show()
sys.exit(app.exec_())

```

#### Python (PySide)

*   Пакеты:
    *   [python-pyside](https://www.archlinux.org/packages/?name=python-pyside) — привязки Python 3.x
    *   [python2-pyside](https://www.archlinux.org/packages/?name=python2-pyside) — привязки Python 2.x
*   Сайт: [http://www.pyside.org/](http://www.pyside.org/)
*   Команда запуска: `python hello-pyside.py` или `python2 hello-pyside.py`

 `hello-pyside.py` 
```
import sys
from PySide.QtCore import *
from PySide.QtGui import *

app = QApplication(sys.argv)
label = QLabel("Hello world!")

label.show()
sys.exit(app.exec_())

```

#### C#

*   Пакет: [kdebindings-qyoto](https://aur.archlinux.org/packages/kdebindings-qyoto/)
*   Сайт: [http://techbase.kde.org/Development/Languages/Qyoto](http://techbase.kde.org/Development/Languages/Qyoto)
*   Команда сборки: `mcs -pkg:qyoto hello.cs`
*   Команда запуска: `mono hello.exe`

 `hello.cs` 
```
using System;
using Qyoto;

public class Hello {
    public static int Main(String[] args) {
        new QApplication(args);
        new QLabel("Hello world!").Show();

        return QApplication.Exec();
    }
}

```

#### Ruby

*   Пакет: [kdebindings-qtruby](https://aur.archlinux.org/packages/kdebindings-qtruby/)
*   Сайт: [http://rubyforge.org/projects/korundum/](http://rubyforge.org/projects/korundum/)
*   Команда запуска: `ruby hello.rb`

 `hello.rb` 
```
require 'Qt4'

app = Qt::Application.new(ARGV)
hello = Qt::Label.new('Hello World!')

hello.show
app.exec

```

#### Java

*   Пакет: [qtjambi](https://aur.archlinux.org/packages/qtjambi/) или [qtjambi-beta](https://aur.archlinux.org/packages/qtjambi-beta/).
*   Сайт: [http://qt-jambi.org/](http://qt-jambi.org/)
*   Команда сборки: `javac Hello.java -cp /opt/qtjambi-beta/qtjambi-linux64-community-4.7.0/qtjambi-4.7.0.jar`.
*   Команда запуска: `java -cp /opt/qtjambi-beta/qtjambi-linux64-community-4.7.0/qtjambi-4.7.0.jar:. Hello`.

 `Hello.java` 
```
import com.trolltech.qt.gui.*;

public class Hello
{
    public static void main(String args[])
    {
        QApplication.initialize(args);
        QLabel hello = new QLabel("Hello World!");

        hello.show();
        QApplication.exec();
    }
}

```

**Обратите внимание:** Инструкции сборки и пример были протестированы на бета-версии Qt Jambi 4.7.0.

#### Perl

*   Пакет: [kdebindings-perlqt](https://aur.archlinux.org/packages/kdebindings-perlqt/)
*   Сайт: [http://code.google.com/p/perlqt4/](http://code.google.com/p/perlqt4/)
*   Команда запуска: `perl hello.pl`

 `hello.pl` 
```
use QtGui4;

my $a = Qt::Application(\@ARGV);
my $hello = Qt::Label("Hello World!", undef);

$hello->show;
exit $a->exec;

```

#### Lua

*   Пакет: [libqtlua](https://aur.archlinux.org/packages/libqtlua/)
*   Сайт: [http://www.nongnu.org/libqtlua/](http://www.nongnu.org/libqtlua/)
*   Команда запуска: `qtlua hello.lua`

 `hello.lua` 
```
label = qt.new_widget("QLabel")

label:setText("Hello World!")
label:show()

```

**Обратите внимание:** QtLua не позволяет писать приложения Qt на чистом Lua; вместо этого, он предлагает расширение возможностей приложения на C++ с помощью скриптового языка.

## Смотрите также

*   [Официальная страница Qt](http://qt.digia.com/)
*   [Сайт проекта](http://qt-project.org/)
*   [Документация Qt 4.8](http://qt-project.org/doc/qt-4.8/)
*   [Planet Qt](http://planet.qt-project.org/)
*   [Приложения Qt](http://qt-apps.org/)