相关文章

*   [KDE (简体中文)](/index.php/KDE_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "KDE (简体中文)")
*   [Uniform Look for QT and GTK Applications (简体中文)](/index.php/Uniform_Look_for_QT_and_GTK_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform Look for QT and GTK Applications (简体中文)")
*   [GTK+ (简体中文)](/index.php/GTK%2B_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "GTK+ (简体中文)")

**翻译状态：** 本文是英文页面 [Qt](/index.php/Qt "Qt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2019-03-01，点击[这里](https://wiki.archlinux.org/index.php?title=Qt&diff=0&oldid=564980)可以查看翻译后英文页面的改动。

[Qt](http://qt-project.org/) 是一个跨平台的应用程序和组件工具，使用标准 C++编写，通过大量使用代码生成器 [Meta Object Compiler(moc)](http://qt-project.org/doc/qt-4.8/moc.html)以及数个宏来扩展语言的功能。它有一些更重要的特性包括：

*   支持各种主流桌面平台和部分手机平台。
*   完善的国际化支持。
*   提供 SQL 数据访问、XML 解析、线程管理、网络支持和统一的文件处理跨平台应用编程接口。

Qt 框架是 [KDE](/index.php/KDE "KDE") 软件社区和其它一些重要开源和闭源应用的基石，例如 [VLC](/index.php/VLC "VLC")、[VirtualBox](/index.php/VirtualBox "VirtualBox")、[Opera](/index.php/Opera "Opera") 和 [Mathematica](/index.php/Mathematica "Mathematica") 等等。

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 安装](#安装)
*   [2 默认 Qt 库](#默认_Qt_库)
    *   [2.1 修改环境变量](#修改环境变量)
    *   [2.2 使用配置文件](#使用配置文件)
*   [3 外观](#外观)
    *   [3.1 Qt5](#Qt5)
    *   [3.2 Qt4](#Qt4)
    *   [3.3 Qt 样式表](#Qt_样式表)
    *   [3.4 GTK+ 和 Qt](#GTK+_和_Qt)
    *   [3.5 Configuration of Qt5 apps under environments other than KDE](#Configuration_of_Qt5_apps_under_environments_other_than_KDE)
*   [4 开发](#开发)
    *   [4.1 支持的平台](#支持的平台)
    *   [4.2 工具](#工具)
    *   [4.3 绑定](#绑定)
        *   [4.3.1 C++](#C++)
        *   [4.3.2 QML](#QML)
        *   [4.3.3 Python (PyQt)](#Python_(PyQt))
        *   [4.3.4 Python (PySide)](#Python_(PySide))
        *   [4.3.5 C#](#C#)
        *   [4.3.6 Ruby](#Ruby)
        *   [4.3.7 Perl](#Perl)
        *   [4.3.8 Lua](#Lua)
*   [5 问题解决](#问题解决)
    *   [5.1 Disable/Change Qt journal logging behaviour](#Disable/Change_Qt_journal_logging_behaviour)
    *   [5.2 Icon theme is not applied](#Icon_theme_is_not_applied)
    *   [5.3 Theme not applied to root applications](#Theme_not_applied_to_root_applications)
    *   [5.4 Qt4 style not respected](#Qt4_style_not_respected)
*   [6 参阅](#参阅)

## 安装

现在[官方源](/index.php/Official_repositories "Official repositories")中有三个版本的 Qt，能用以下软件包来[安装](/index.php/Pacman "Pacman")：

*   **Qt 5.x**：软件包 [qt5-base](https://www.archlinux.org/packages/?name=qt5-base)，文档包是 [qt5-doc](https://www.archlinux.org/packages/?name=qt5-doc)。
*   **Qt 4.x**：软件包 [qt4](https://aur.archlinux.org/packages/qt4/)，文档包是 [qt4-doc](https://aur.archlinux.org/packages/qt4-doc/)。
*   **Qt 3.x**：在软件包 [qt3](https://aur.archlinux.org/packages/qt3/)，文档包是 [qt3-doc](https://aur.archlinux.org/packages/qt3-doc/)。

## 默认 Qt 库

Qt软件包不再提供通常的二进制文件`/usr/bin/qmake`,而是将它们改名为 qmake-qt5, qmake-qt4, qmake-qt3 软链接，这可能导致 Qt3/4 程序编译失败。安装[qtchooser](https://aur.archlinux.org/packages/qtchooser/)可以恢复 `/usr/bin/qmake` 并设置要使用的 Qt 版本，默认是使用 Qt5。

**警告:** 现在 [qtchooser](https://aur.archlinux.org/packages/qtchooser/) 与 [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) 相冲突，可以自行编译并安装到`/usr/local`。Arch 官方不支持这种方式[[1]](https://bugs.archlinux.org/task/51308)。

### 修改环境变量

可以通过 `QT_SELECT` [环境变量](/index.php/Environment_variable "Environment variable") 设置默认的 QT. 例如要使用 Qt4，可以设置 `export QT_SELECT=4`。

### 使用配置文件

创建 `~/.config/qtchooser/default.conf` 软链接，链接到`/etc/xdg/qtchooser/`目录中需要的 *.conf* 文件上。例如要使用 Qt4，将 `/etc/xdg/qtchooser/4.conf` 软链接到 `~/.config/qtchooser/default.conf`。

```
$ ln -s `/etc/xdg/qtchooser/4.conf` `~/.config/qtchooser/default.conf`

```

## 外观

### Qt5

Qt5基于当前使用的桌面环境来决定所使用的样式：

*   In KDE Plasma, it uses the actually selected Qt style. It can be configured using *KDE System Settings* (*systemsettings5*), the settings can be found in *Appearance > Application Style > Widget Style*.
*   In Cinnamon, GNOME, MATE, LXDE, Xfce, it uses GTK+ ([QGtkStyle](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications")).
*   In other desktop environments, it uses Fusion.

如果要强制指定一种样式，你可以设置`QT_STYLE_OVERRIDE`环境变量（[environment variable](/index.php/Environment_variable "Environment variable")）。特别的，如果你想要使用[GTK+](/index.php/GTK%2B "GTK+")主题，把它设置成`gtk2`（注意：你将需要安装在下文中提到的Qt样式插件来获取GTK+样式）。Qt5应用同时也支持`-style`标志，你可以用它来使用指定的样式运行一个Qt5应用程序。

The following styles are included in Qt5: *Fusion*, *Windows*. Others can be installed from the official repositories:

*   **Breeze** — Artwork, styles and assets for the Breeze visual style for the Plasma Desktop.

	[https://projects.kde.org/projects/kde/workspace/breeze](https://projects.kde.org/projects/kde/workspace/breeze) || [breeze](https://www.archlinux.org/packages/?name=breeze)

*   **Oxygen** — KDE Oxygen style.

	[https://projects.kde.org/projects/kde/workspace/oxygen](https://projects.kde.org/projects/kde/workspace/oxygen) || [oxygen](https://www.archlinux.org/packages/?name=oxygen)

*   **QtCurve** — A configurable set of widget styles for KDE and Gtk.

	[https://projects.kde.org/projects/playground/base/qtcurve](https://projects.kde.org/projects/playground/base/qtcurve) || [qtcurve-qt5](https://www.archlinux.org/packages/?name=qtcurve-qt5)

*   **Adwaita-Qt** — A style to bend Qt applications to look like they belong into GNOME Shell.

	[https://github.com/MartinBriza/adwaita-qt](https://github.com/MartinBriza/adwaita-qt) || [adwaita-qt5](https://aur.archlinux.org/packages/adwaita-qt5/)

*   **Qt style plugins** — Additional style plugins for Qt5, including *GTK+*, *Cleanlooks*, *Motif*, *Plastique*.

	[http://code.qt.io/cgit/qt/qtstyleplugins.git](http://code.qt.io/cgit/qt/qtstyleplugins.git) || [qt5-styleplugins](https://www.archlinux.org/packages/?name=qt5-styleplugins)

### Qt4

Qt4 应用程序会尝试模仿所运行的桌面环境的行为，除非碰到了某些问题或者进行了强制配置。要修改 Qt 程序的外观，可以使用 Qt 配置工具(`qtconfig-qt4` 或 `qt3config`).

尽管不是 Qt 的一部分，*KDE 系统设置* 提供了许多定制设置，Qt 程序也会使用这些设置。

*   In KDE Plasma, it uses the actually selected Qt style. It can be configured using *KDE System Settings* (*systemsettings5*), the settings can be found in *Appearance > Application Style > Widget Style*.
*   In Cinnamon, GNOME, Xfce, it uses GTK+ ([QGtkStyle](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications")).
*   In other desktop environments, it uses Windows.

要修改 Qt4 程序的外观，可以使用 [qt4](https://aur.archlinux.org/packages/qt4/) 提供的 Qt 配置工具*qtconfig-qt4*。这个程序可以配置 Qt4 程序的样式、颜色、字体等。

**Note:** 如果使用 *GTK+* 样式，将忽略颜色和字体设置，直接使用 GTK+2 的值。

Qt keeps all its configuration information in `/etc/xdg/Trolltech.conf` (system-wide) or `~/.config/Trolltech.conf` (user-specific). The file is rather difficult to navigate because it contains a lot of information not related to appearance, but for any changes you can just add to the end of the file and overwrite any previous values (make sure to add your modification under the [Qt] header).

For example, to change the theme to QtCurve, add:

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=QtCurve

```

Qt4 已经包含数种样式，例如 GTK+ 样式、Windows 样式、CDE 样式等，其它的主题（大多数为 KDE Plasma 桌面编写）可以从官方源或者 [AUR](/index.php/AUR "AUR") 中安装：

*   **Breeze** — Artwork, styles and assets for the Breeze visual style for the Plasma Desktop.

	[https://projects.kde.org/projects/kde/workspace/breeze](https://projects.kde.org/projects/kde/workspace/breeze) || [breeze-kde4](https://aur.archlinux.org/packages/breeze-kde4/)

*   **[Oxygen](https://en.wikipedia.org/wiki/Oxygen_Project "wikipedia:Oxygen Project")** — KDE Oxygen style.

	[https://projects.kde.org/projects/kde/workspace/oxygen](https://projects.kde.org/projects/kde/workspace/oxygen) || [oxygen-kde4](https://www.archlinux.org/packages/?name=oxygen-kde4)

*   **QtCurve** — A configurable set of widget styles for KDE and Gtk.

	[https://projects.kde.org/projects/playground/base/qtcurve](https://projects.kde.org/projects/playground/base/qtcurve) || [qtcurve-qt4](https://www.archlinux.org/packages/?name=qtcurve-qt4)

*   **Adwaita-Qt** — A style to bend Qt applications to look like they belong into GNOME Shell.

	[https://github.com/MartinBriza/adwaita-qt](https://github.com/MartinBriza/adwaita-qt) || [adwaita-qt4](https://aur.archlinux.org/packages/adwaita-qt4/)

### Qt 样式表

An interesting way of customizing the look and feel of a Qt application is using Style Sheets, which are just simple CSS files. Using Style Sheets, one can modify the appearance of every widget in the application.

To run an application with a different style just execute:

```
$ qt_application -stylesheet *style.qss*

```

For more information on Qt Style Sheets see the [official documentation](http://doc.qt.io/qt-5/stylesheet-reference.html) or other [tutorials](http://thesmithfam.org/blog/2009/09/10/qt-stylesheets-tutorial/). As an example Style Sheet see this [Dolphin modification](http://kde-apps.org/content/show.php/roxydoxy?content=125979).

### GTK+ 和 Qt

如果你有 GTK+ 和 Qt 应用程序，它们的外观可能无法融合到一起。如果你希望使 GTK+ 风格与 Qt 风格匹配，请阅读 [统一 GTK+ 和 Qt 应用程序外观](/index.php/Uniform_look_for_Qt_and_GTK_applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform look for Qt and GTK applications (简体中文)").

### Configuration of Qt5 apps under environments other than KDE

Unlike Qt4, Qt5 doesn't ship a qtconfig utility to configure fonts, icons or styles. Instead, it will try to use the settings from the running DE. In KDE or GNOME this works well, but in other less popular DEs or WM it can lead to missing icons in Qt5 applications. One way to solve this is to fake the running desktop environment by setting `XDG_CURRENT_DESKTOP=KDE` or `GNOME`, and then using the corresponding configuration application to set the desired icon set.

Another solution is provided by the [qt5ct](https://www.archlinux.org/packages/?name=qt5ct) package, which provides a DE independent Qt5 QPA and a configuration utility. After installing the package, run `qt5ct` to set an icon theme, and set the environment variable `QT_QPA_PLATFORMTHEME="qt5ct"` so that the settings are picked up by Qt applications. Alternatively, use `--platformtheme qt5ct` as argument to the Qt5 application.

如果遇到了下列错误，并且一些图标依然不在一些应用程序中出现，安装[oxygen](https://www.archlinux.org/packages/?name=oxygen)和[oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons)：

```
Icon theme "oxygen" not found.
Icon theme "oxygen" not found.
Error: standard icon theme "oxygen" not found!

```

## 开发

### 支持的平台

Qt supports most platforms that are available today, even some of the more obscure ones, with more ports appearing every once in a while. For a more complete list see the [Qt Wikipedia article](https://en.wikipedia.org/wiki/Qt_(framework)#Platforms "wikipedia:Qt (framework)").

### 工具

以下是官方 Qt 工具：

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — A cross-platform IDE tailored for Qt that supports all of its features.

	[http://doc.qt.io/qtcreator/](http://doc.qt.io/qtcreator/) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **Qt Linguist** — A set of tools that speed the translation and internationalization of Qt applications.

	[http://doc.qt.io/qt-5/qtlinguist-index.html](http://doc.qt.io/qt-5/qtlinguist-index.html) || Qt 5: [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **Qt Assistant** — A configurable and redistributable documentation reader for Qt *qch* files.

	[http://doc.qt.io/qt-5/qtassistant-index.html](http://doc.qt.io/qt-5/qtassistant-index.html) || Qt 5: [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **Qt Designer** — A powerful cross-platform GUI layout and forms builder for Qt widgets.

	[http://doc.qt.io/qt-5/qtdesigner-manual.html](http://doc.qt.io/qt-5/qtdesigner-manual.html) || Qt 5: [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **Qt Quick Designer** — A visual editor for QML files which supports WYSIWYG. It allows you to rapidly design and build Qt Quick applications and components from scratch.

	[http://doc.qt.io/qtcreator/creator-using-qt-quick-designer.html](http://doc.qt.io/qtcreator/creator-using-qt-quick-designer.html) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **qmlscene** — A tool for loading QML documents that makes it easy to quickly develop and debug QML applications.

	[http://doc.qt.io/qt-5/qtquick-qmlscene.html](http://doc.qt.io/qt-5/qtquick-qmlscene.html) || Qt 5: [qt5-declarative](https://www.archlinux.org/packages/?name=qt5-declarative), Qt 4 QML Viewer: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **[qmake](https://en.wikipedia.org/wiki/Qmake "wikipedia:Qmake")** — A tool that helps simplify the build process for development project across different platforms, similar to [cmake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake"), but with fewer options and tailored for Qt applications.

	[http://doc.qt.io/qt-5/qmake-manual.html](http://doc.qt.io/qt-5/qmake-manual.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **uic** — A tool that reads **.ui* XML files and generates the corresponding C++ files.

	[http://doc.qt.io/qt-5/uic.html](http://doc.qt.io/qt-5/uic.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **rcc** — A tool that is used to embed resources (such as pictures) into a Qt application during the build process. It works by generating a C++ source file containing data specified in a Qt resource (.qrc) file.

	[http://doc.qt.io/qt-5/rcc.html](http://doc.qt.io/qt-5/rcc.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

*   **moc** — A tool that handles Qt's C++ extensions (the signals and slots mechanism, the run-time type information, and the dynamic property system, etc.).

	[http://doc.qt.io/qt-5/moc.html](http://doc.qt.io/qt-5/moc.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://aur.archlinux.org/packages/qt4/)

### 绑定

Qt 提供了所有流行编程语言的[绑定](https://en.wikipedia.org/wiki/Qt_(framework)#Programming_language_bindings "wikipedia:Qt (framework)")。以下示例会在一个窗口中显示一句 'Hello world!' 消息。

#### C++

*   Package:
    *   [qt4](https://aur.archlinux.org/packages/qt4/) - Version 4.x of the Qt toolkit.
    *   [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) - Version 5.x of the Qt toolkit.
*   Website: [http://qt-project.org/](http://qt-project.org/)
*   Build:
    *   The Qt4 version: `g++ $(pkg-config --cflags --libs QtGui) -o hello hello.cpp`
    *   The Qt5 version: `g++ $(pkg-config --cflags --libs Qt5Widgets) -fPIC -o hello hello.cpp`
*   Run with: `./hello`

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

*   Package: [qt4](https://aur.archlinux.org/packages/qt4/) or [qt5-declarative](https://www.archlinux.org/packages/?name=qt5-declarative).
*   Website: [http://qt-project.org/](http://qt-project.org/)
*   Run with: `qmlviewer-qt4 hello.qml` or `qmlscene-qt5 hello.qml`

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

**Note:** For version 5.x of the Qt toolkit, we need to import QtQuick 2.y.

#### Python (PyQt)

*   Package:
    *   [python-pyqt4](https://aur.archlinux.org/packages/python-pyqt4/) - Python 3.x bindings for Qt 4
    *   [python2-pyqt4](https://aur.archlinux.org/packages/python2-pyqt4/) - Python 2.x bindings for Qt 4
    *   [python-pyqt5](https://www.archlinux.org/packages/?name=python-pyqt5) - Python 3.x bindings for Qt 5
    *   [python2-pyqt5](https://www.archlinux.org/packages/?name=python2-pyqt5) - Python 2.x bindings for Qt 5

*   Website: [http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro)
*   Run with: `python hello-pyqt.py` or `python2 hello-pyqt.py`.

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

*   Package:
    *   [python-pyside](https://aur.archlinux.org/packages/python-pyside/) - Python 3.x bindings
    *   [python2-pyside](https://aur.archlinux.org/packages/python2-pyside/) - Python 2.x bindings
*   Website: [http://www.pyside.org/](http://www.pyside.org/)
*   Run with: `python hello-pyside.py` or `python2 hello-pyside.py`

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

参考: [QtSharp](https://gitlab.com/ddobrev/QtSharp).

#### Ruby

*   Package: [kdebindings-qtruby](https://aur.archlinux.org/packages/kdebindings-qtruby/)
*   Website: [http://rubyforge.org/projects/korundum/](http://rubyforge.org/projects/korundum/)
*   Run with: `ruby hello.rb`

 `hello.rb` 
```
require 'Qt4'

app = Qt::Application.new(ARGV)
hello = Qt::Label.new('Hello World!')

hello.show
app.exec

```

#### Perl

*   Package: [kdebindings-perlqt](https://aur.archlinux.org/packages/kdebindings-perlqt/)
*   Website: [http://code.google.com/p/perlqt4/](http://code.google.com/p/perlqt4/)
*   Run with: `perl hello.pl`

 `hello.pl` 
```
use QtGui4;

my $a = Qt::Application(\@ARGV);
my $hello = Qt::Label("Hello World!", undef);

$hello->show;
exit $a->exec;

```

#### Lua

*   Package: [libqtlua](https://aur.archlinux.org/packages/libqtlua/)
*   Website: [http://www.nongnu.org/libqtlua/](http://www.nongnu.org/libqtlua/)
*   Run with: `qtlua hello.lua`

 `hello.lua` 
```
label = qt.new_widget("QLabel")

label:setText("Hello World!")
label:show()

```

**Note:** QtLua is not designed to develop an application in pure Lua but rather to extend a Qt C++ application using Lua as scripting language.

## 问题解决

### Disable/Change Qt journal logging behaviour

When using [KDE](/index.php/KDE "KDE") and/or any other Qt [desktop environment](/index.php/Desktop_environment "Desktop environment") debug info may be frequently be logged in the [systemd journal](/index.php/Systemd_journal "Systemd journal").

Set `QT_LOGGING_RULES` as [environment variable](/index.php/Environment_variable "Environment variable") to change this behaviour, e.g. to completely disable logging:

 `/etc/environment`  `QT_LOGGING_RULES='*=false'` 

To allow only debug logging, use `QT_LOGGING_RULES="*.debug=false"`.

### Icon theme is not applied

Since Qt 5.1 SVG support has moved into a module. Since [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) does not depend on [qt5-svg](https://www.archlinux.org/packages/?name=qt5-svg) it may happen that the [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) is installed but not [qt5-svg](https://www.archlinux.org/packages/?name=qt5-svg). This results in deceptive icon theme behaviour. Since SVG is not supported the icons are silently skipped and the icon theme may seem to be unused. Installing [qt5-svg](https://www.archlinux.org/packages/?name=qt5-svg) explicitly solves the problem.

### Theme not applied to root applications

As the user theme file (`$XDG_CONFIG_HOME/Trolltech.conf`), are not read by other accounts, the selected theme will not apply to [X applications run as root](/index.php/Running_X_apps_as_root "Running X apps as root"). Possible solutions include:

*   Create symlinks, e.g

```
# ln -s /home/[username]/.config/Trolltech.conf /etc/xdg/Trolltech.conf

```

*   Configure system-wide theme file: `/etc/xdg/Trolltech.conf`
*   Adjust the theme as root

### Qt4 style not respected

If pure Qt4 (non-KDE) applications do not stick with your selected Qt4 style, then you'll probably need to tell Qt4 how to find KDE's styles (Oxygen, Phase etc.). You just need to set the environment variable QT_PLUGIN_PATH. E.g. put

```
export QT_PLUGIN_PATH=$HOME/.kde4/lib/kde4/plugins/:/usr/lib/kde4/plugins/

```

into your `/etc/profile` (or `~/.profile` if you do not have root access). `qtconfig-qt4` should then be able to find your kde styles and everything should look nice again!

Alternatively, you can symlink the Qt4 styles directory to the KDE4 styles one:

```
# ln -s /usr/lib/{kde,qt}4/plugins/styles/[theme name]

```

## 参阅

*   [官方网站](http://qt.digia.com/)
*   [Qt 项目](http://qt-project.org/)
*   [Qt 文档](http://qt-project.org/doc/qt-4.8/)
*   [Planet Qt](http://planet.qt-project.org/)
*   [Qt 应用程序](http://qt-apps.org/)