**翻译状态：** 本文是英文页面 [Qt](/index.php/Qt "Qt") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-10-6，点击[这里](https://wiki.archlinux.org/index.php?title=Qt&diff=0&oldid=277311)可以查看翻译后英文页面的改动。

[Qt](http://qt-project.org/) 是一个跨平台的应用程序，组件工具使用标准 C++，但也大量使用了特殊的代码生成器（称为 [Meta Object Compiler](http://qt-project.org/doc/qt-4.8/moc.html)，或者 moc）以及数个宏来充实语言。它有一些更重要的特性：

*   运行于主流桌面平台和部分手机平台。
*   广泛的国际化支持。
*   提供 SQL 数据访问、XML 解析、线程管理、网络支持和统一的文件处理跨平台应用编程接口（API）的完整类库。

Qt 框架正在成为主要的开发平台，同时是 [KDE](/index.php/KDE "KDE") 软件社区和重要的开源和闭源应用，如 [VLC](/index.php/VLC "VLC")、[VirtualBox](/index.php/VirtualBox "VirtualBox")、[Opera](/index.php/Opera "Opera")、[Mathematica](/index.php/Mathematica "Mathematica")、[Skype](/index.php/Skype "Skype")以及许多其它应用的基石。

## Contents

*   [1 安装](#.E5.AE.89.E8.A3.85)
*   [2 默认 Qt 库](#.E9.BB.98.E8.AE.A4_Qt_.E5.BA.93)
    *   [2.1 修改环境变量](#.E4.BF.AE.E6.94.B9.E7.8E.AF.E5.A2.83.E5.8F.98.E9.87.8F)
    *   [2.2 使用配置文件](#.E4.BD.BF.E7.94.A8.E9.85.8D.E7.BD.AE.E6.96.87.E4.BB.B6)
*   [3 外观](#.E5.A4.96.E8.A7.82)
    *   [3.1 配置](#.E9.85.8D.E7.BD.AE)
        *   [3.1.1 主题](#.E4.B8.BB.E9.A2.98)
        *   [3.1.2 字体](#.E5.AD.97.E4.BD.93)
        *   [3.1.3 图标](#.E5.9B.BE.E6.A0.87)
    *   [3.2 手动配置](#.E6.89.8B.E5.8A.A8.E9.85.8D.E7.BD.AE)
    *   [3.3 Qt 样式表](#Qt_.E6.A0.B7.E5.BC.8F.E8.A1.A8)
    *   [3.4 GTK+ 和 Qt](#GTK.2B_.E5.92.8C_Qt)
*   [4 开发](#.E5.BC.80.E5.8F.91)
    *   [4.1 支持的平台](#.E6.94.AF.E6.8C.81.E7.9A.84.E5.B9.B3.E5.8F.B0)
    *   [4.2 工具](#.E5.B7.A5.E5.85.B7)
    *   [4.3 绑定](#.E7.BB.91.E5.AE.9A)
        *   [4.3.1 C++](#C.2B.2B)
        *   [4.3.2 QML](#QML)
        *   [4.3.3 Python](#Python)
        *   [4.3.4 C#](#C.23)
        *   [4.3.5 Ruby](#Ruby)
        *   [4.3.6 Java](#Java)
        *   [4.3.7 Perl](#Perl)
        *   [4.3.8 Lua](#Lua)
*   [5 资源](#.E8.B5.84.E6.BA.90)

## 安装

现在[官方源](/index.php/Official_repositories "Official repositories")中有三个版本的 Qt，能用以下软件包来[安装](/index.php/Pacman "Pacman")：

*   **Qt 5.x** 在软件包 [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) 内，文档在软件包 [qt5-doc](https://www.archlinux.org/packages/?name=qt5-doc) 内。
*   **Qt 4.x** 在软件包 [qt4](https://www.archlinux.org/packages/?name=qt4) 内。
*   **Qt 3.x** 在软件包 [qt3](https://aur.archlinux.org/packages/qt3/) 内，文档在软件包 [qt3-doc](https://aur.archlinux.org/packages/qt3-doc/) 内。

**警告:** Qt软件包不再提供通常的二进制文件`/usr/bin/qmake`,而是将它们改名为 qmake-qt5, qmake-qt4, qmake-qt3 软链接，这可能导致 Qt3/4 程序编译失败。

## 默认 Qt 库

安装[qtchooser](https://www.archlinux.org/packages/?name=qtchooser)可以恢复 `/usr/bin/qmake` 并设置要使用的 Qt 版本，默认是使用 Qt5。

### 修改环境变量

要使用 Qt4，可以在`~/.{bash,zsh}_profile.`中设置`QT_SELECT=4`。

### 使用配置文件

要使用 Qt4，将 `/etc/xdg/qtchooser/4.conf` 软链接到 `~/.config/qtchooser/default.conf`。

## 外观

### 配置

Qt 应用程序会尝试模仿所运行的桌面环境的行为，除非碰到了某些问题或者硬编码的配置。要修改 Qt 程序的外观，可以使用 Qt 配置工具(`qtconfig-qt4` 或 `qt3config`).

尽管不是 Qt 的一部分，*KDE 系统设置* 提供了许多定制设置，Qt 程序也会使用这些设置。

#### 主题

Qt 已经包含数种样式，例如 GTK+ 样式、Windows 样式、CDE 样式等，但其它的主题（大多数为 KDE 桌面编写）可以从官方源或者 [AUR](/index.php/AUR "AUR") 中安装：

*   **[Oxygen](https://en.wikipedia.org/wiki/Oxygen_Project "wikipedia:Oxygen Project")** — A desktop theme that comes with the KDE desktop.

	[http://www.oxygen-icons.org/](http://www.oxygen-icons.org/) || [kdebase-runtime](https://www.archlinux.org/packages/?name=kdebase-runtime)

*   **[QtCurve](https://en.wikipedia.org/wiki/QtCurve "wikipedia:QtCurve")** — A very configurable and popular desktop theme with support for GTK+ and Qt applications.

	[http://kde-look.org/content/show.php?content=40492](http://kde-look.org/content/show.php?content=40492) || [qtcurve-kde3](https://aur.archlinux.org/packages/qtcurve-kde3/) [qtcurve-kde4](https://www.archlinux.org/packages/?name=qtcurve-kde4)

*   **Skulpture** — A GUI style addon for KDE and Qt programs that features a classical three dimensional artwork with shadows and smooth gradients to enhance the visual experience.

	[http://kde-look.org/content/show.php/?content=59031](http://kde-look.org/content/show.php/?content=59031) || [skulpture](https://aur.archlinux.org/packages/skulpture/)

*   **Polymer** — A port of the KDE Plastik Style to Qt3.

	[http://kde-look.org/content/show.php?content=21748](http://kde-look.org/content/show.php?content=21748) || [polymer](https://aur.archlinux.org/packages/polymer/)

*   **Bespin** — A very configurable KDE theme.

	[http://cloudcity.sourceforge.net/frame.php](http://cloudcity.sourceforge.net/frame.php) || [bespin-svn](https://aur.archlinux.org/packages/bespin-svn/)

#### 字体

Qt fonts can be configured from *QtConfig* under *Fonts > Default Font*.

#### 图标

There is no way of setting the icon theme from *QtConfig*, but since Qt follows the [Freedesktop.org Icon Specification](http://standards.freedesktop.org/icon-naming-spec/icon-naming-spec-latest.html), any theme set for X is picked up by Qt.

### 手动配置

Qt keeps all its configuration information in `~/.config/Trolltech.conf`. The file is rather difficult to navigate because it contains a lot of information not related to appearance, but for any changes you can just add to the end of the file and overwrite any previous values (make sure to add your modification under the `[Qt]` header).

For example, to change the theme to QtCurve, add:

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=QtCurve

```

### Qt 样式表

An interesting way of customizing the look and feel of a Qt application is using Style Sheets, which are just simple CSS files. Using Style Sheets, one can modify the appearance of every widget in the application.

To run an application with a different style just execute:

```
$ qt_application --stylesheet style.qss

```

For more information on Qt Style Sheets see the [official documentation](http://qt-project.org/doc/qt-4.8/stylesheet-reference.html) or other [tutorials](http://thesmithfam.org/blog/2009/09/10/qt-stylesheets-tutorial/). As an example Style Sheet see this [Dolphin modification](http://kde-apps.org/content/show.php/roxydoxy?content=125979).

### GTK+ 和 Qt

如果你有 GTK+ 和 Qt 应用程序，它们的外观可能无法融合到一起。如果你希望使 GTK+ 风格与 Qt 风格匹配，请阅读 [统一 GTK+ 和 Qt 应用程序外观](/index.php/Uniform_Look_for_QT_and_GTK_Applications_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Uniform Look for QT and GTK Applications (简体中文)").

## 开发

### 支持的平台

Qt supports most platforms that are available today, even some of the more obscure ones, with more ports appearing every once in a while. For a more complete list see the [Qt Wikipedia article](https://en.wikipedia.org/wiki/Qt_(framework)#Platforms "wikipedia:Qt (framework)").

### 工具

以下是官方 Qt 工具：

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — A cross-platform IDE tailored for Qt that supports all of its features.

	[http://qt-project.org/doc/qtcreator/](http://qt-project.org/doc/qtcreator/) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **Qt Linguist** — A set of tools that speed the translation and internationalization of Qt applications.

	[http://qt-project.org/doc/qt-4.8/linguist-manual.html](http://qt-project.org/doc/qt-4.8/linguist-manual.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **Qt Assistant** — A configurable and redistributable documentation reader for Qt *qch* files.

	[http://qt-project.org/doc/qt-4.8/assistant-manual.html](http://qt-project.org/doc/qt-4.8/assistant-manual.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **Qt Designer** — A powerful cross-platform GUI layout and forms builder for Qt widgets.

	[http://qt-project.org/doc/qt-4.8/designer-manual.html](http://qt-project.org/doc/qt-4.8/designer-manual.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **Qt Quick Designer** — A visual editor for QML files which supports WYSIWYG. It allows you to rapidly design and build Qt Quick applications and components from scratch.

	[http://qt-project.org/doc/qtcreator-2.8/creator-using-qt-quick-designer.html](http://qt-project.org/doc/qtcreator-2.8/creator-using-qt-quick-designer.html) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **QML Viewer** — A tool for loading QML documents that makes it easy to quickly develop and debug QML applications.

	[http://qt-project.org/doc/qt-4.8/qmlviewer.html](http://qt-project.org/doc/qt-4.8/qmlviewer.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **[qmake](https://en.wikipedia.org/wiki/Qmake "wikipedia:Qmake")** — A tool that helps simplify the build process for development project across different platforms, similar to [cmake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake"), but with fewer options and tailored for Qt applications.

	[https://qt-project.org/doc/qt-4.8/qmake-manual.html](https://qt-project.org/doc/qt-4.8/qmake-manual.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **uic** — A tool that reads **.ui* XML files and generates the corresponding C++ files.

	[http://qt-project.org/doc/qt-4.8/uic.html](http://qt-project.org/doc/qt-4.8/uic.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **rcc** — A tool that is used to embed resources (such as pictures) into a Qt application during the build process. It works by generating a C++ source file containing data specified in a Qt resource (.qrc) file.

	[http://qt-project.org/doc/qt-4.8/rcc.html](http://qt-project.org/doc/qt-4.8/rcc.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

*   **moc** — A tool that handles Qt's C++ extensions (the signals and slots mechanism, the run-time type information, and the dynamic property system, etc.).

	[http://doc.qt.digia.com/4.7-snapshot/moc.html](http://doc.qt.digia.com/4.7-snapshot/moc.html) || [qt](https://www.archlinux.org/groups/x86_64/qt/)

### 绑定

Qt has bindings for all of the more popular languages, for a full list see [this list](https://en.wikipedia.org/wiki/Qt_(framework)#Programming_language_bindings "wikipedia:Qt (framework)").

以下示例会在一个窗口中显示一句 'Hello world!' 消息。

#### C++

*   Package: [qt4](https://www.archlinux.org/packages/?name=qt4)
*   Website: [http://qt-project.org/](http://qt-project.org/)
*   Build with: `g++ `pkg-config --cflags --libs QtCore QtGui` -o hello hello.cpp`
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

*   Package: [qt4](https://www.archlinux.org/packages/?name=qt4)
*   Website: [http://qt-project.org/](http://qt-project.org/)
*   Run with: `qmlviewer hello.qml`

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

#### Python

*   Package:
    *   [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) - Python 3.x bindings
    *   [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) - Python 2.x bindings
*   Website: [http://www.riverbankcomputing.co.uk/software/pyqt/intro](http://www.riverbankcomputing.co.uk/software/pyqt/intro)
*   Run with: `python hello-pyqt.py` or `python2 hello-pyqt.py`

 `hello-pyqt.py` 
```
import sys
from PyQt4 import QtGui

app = QtGui.QApplication(sys.argv)
label = QtGui.QLabel("Hello world!")

label.show()
sys.exit(app.exec_())

```

*   Package:
    *   [python-pyside](https://www.archlinux.org/packages/?name=python-pyside) - Python 3.x bindings
    *   [python2-pyside](https://www.archlinux.org/packages/?name=python2-pyside) - Python 2.x bindings
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

*   Package: [kdebindings-qyoto](https://aur.archlinux.org/packages/kdebindings-qyoto/)
*   Website: [http://techbase.kde.org/Development/Languages/Qyoto](http://techbase.kde.org/Development/Languages/Qyoto)
*   Build with: `mcs -pkg:qyoto hello.cs`
*   Run with: `mono hello.exe`

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

#### Java

*   Package: [qtjambi](https://aur.archlinux.org/packages/qtjambi/)
*   Website: [http://qt-jambi.org/](http://qt-jambi.org/)

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

## 资源

*   [官方网站](http://qt.digia.com/)
*   [Qt 项目](http://qt-project.org/)
*   [Qt 文档](http://qt-project.org/doc/qt-4.8/)
*   [Planet Qt](http://planet.qt-project.org/)
*   [Qt 应用程序](http://qt-apps.org/)