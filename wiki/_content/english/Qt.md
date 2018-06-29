Related articles

*   [KDE](/index.php/KDE "KDE")
*   [Uniform Look for Qt and GTK Applications](/index.php/Uniform_Look_for_Qt_and_GTK_Applications "Uniform Look for Qt and GTK Applications")
*   [GTK+](/index.php/GTK%2B "GTK+")

[Qt](http://qt-project.org/) is a cross-platform application and widget toolkit that uses standard C++ but makes extensive use of a special code generator (called the [Meta Object Compiler](http://qt-project.org/doc/qt-4.8/moc.html), or *moc*) together with several macros to enrich the language. Some of its more important features include:

*   Running on the major desktop platforms and some of the mobile platforms.
*   Extensive internationalization support.
*   A complete library that provides SQL database access, XML parsing, thread management, network support, and a unified cross-platform application programming interface (API) for file handling.

The Qt framework is emerging as a major development platform and is the basis of the [KDE](/index.php/KDE "KDE") software community, among other important open source and proprietary applications such as [VLC](/index.php/VLC "VLC"), [VirtualBox](/index.php/VirtualBox "VirtualBox"), [Mathematica](/index.php/Mathematica "Mathematica") and many others.

## Contents

*   [1 Installation](#Installation)
*   [2 Default Qt toolkit](#Default_Qt_toolkit)
    *   [2.1 Using environment variables](#Using_environment_variables)
    *   [2.2 Using configuration files](#Using_configuration_files)
*   [3 Appearance](#Appearance)
    *   [3.1 Qt4](#Qt4)
    *   [3.2 Qt5](#Qt5)
    *   [3.3 Qt Style Sheets](#Qt_Style_Sheets)
    *   [3.4 GTK+ and Qt](#GTK.2B_and_Qt)
    *   [3.5 Configuration of Qt5 apps under environments other than KDE Plasma](#Configuration_of_Qt5_apps_under_environments_other_than_KDE_Plasma)
*   [4 Development](#Development)
    *   [4.1 Supported platforms](#Supported_platforms)
        *   [4.1.1 Android](#Android)
    *   [4.2 Tools](#Tools)
    *   [4.3 Bindings](#Bindings)
        *   [4.3.1 C++](#C.2B.2B)
        *   [4.3.2 QML](#QML)
        *   [4.3.3 Python (PyQt)](#Python_.28PyQt.29)
        *   [4.3.4 Python (PySide)](#Python_.28PySide.29)
        *   [4.3.5 C#](#C.23)
        *   [4.3.6 Ruby](#Ruby)
        *   [4.3.7 Perl](#Perl)
        *   [4.3.8 Lua](#Lua)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Qt programs crash when opening file dialogs under GNOME Wayland](#Qt_programs_crash_when_opening_file_dialogs_under_GNOME_Wayland)
    *   [5.2 Disable/Change Qt journal logging behaviour](#Disable.2FChange_Qt_journal_logging_behaviour)
    *   [5.3 Icon theme is not applied](#Icon_theme_is_not_applied)
    *   [5.4 Theme not applied to root applications](#Theme_not_applied_to_root_applications)
    *   [5.5 Qt4 style not respected](#Qt4_style_not_respected)
    *   [5.6 Applications using QML crash or don't work with Qt 5.8](#Applications_using_QML_crash_or_don.27t_work_with_Qt_5.8)
    *   [5.7 All Qt5-based applications fail to run after Qt5 update](#All_Qt5-based_applications_fail_to_run_after_Qt5_update)
*   [6 See also](#See_also)

## Installation

Two versions of Qt are currently available in the [official repositories](/index.php/Official_repositories "Official repositories"). They can be [installed](/index.php/Pacman "Pacman") with the following packages:

*   **Qt 5.x** is available in the [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) package, with documentation in the [qt5-doc](https://www.archlinux.org/packages/?name=qt5-doc) package.
*   **Qt 4.x** is available in the [qt4](https://www.archlinux.org/packages/?name=qt4) package, with documentation on AUR in the [qt4-doc](https://aur.archlinux.org/packages/qt4-doc/) package.
*   **Qt 3.x** is available from the AUR in the [qt3](https://aur.archlinux.org/packages/qt3/) package, with documentation on AUR in the [qt3-doc](https://aur.archlinux.org/packages/qt3-doc/) package.

## Default Qt toolkit

Qt packages do not provide the usual bins (e.g. *qmake*) in `/usr/bin` anymore. Instead `-qt5`, `-qt4` and `-qt3` symlinks are provided (e.g. `qmake-qt5`, `qmake-qt4`, `qmake-qt3`). This may cause compilation failures in Qt3/4 applications.

By installing [qtchooser](https://aur.archlinux.org/packages/qtchooser/) you can restore the usual bins (e.g. *qmake*) in `/usr/bin` and setup the Qt toolkit to use. By default Qt5 is used.

**Warning:** [qtchooser](https://aur.archlinux.org/packages/qtchooser/) now is conflict with [qt5-base](https://www.archlinux.org/packages/?name=qt5-base). You can install it in /usr/local if you really need it, but it's not officially supported[[1]](https://bugs.archlinux.org/task/51308).

### Using environment variables

To define default Qt toolkit, you can create `QT_SELECT` [environment variable](/index.php/Environment_variable "Environment variable"). For example, to set Qt4, do `export QT_SELECT=4` in your shell's init file (e.g. `~/.bash_profile` or `~/.zprofile`).

### Using configuration files

You can set default Qt toolkit by creating a symlink `~/.config/qtchooser/default.conf` to one of *.conf* files in `/etc/xdg/qtchooser/` directory. For example, to set Qt4 symlink `/etc/xdg/qtchooser/4.conf` to `~/.config/qtchooser/default.conf`:

```
$ ln -s `/etc/xdg/qtchooser/4.conf` `~/.config/qtchooser/default.conf`

```

## Appearance

### Qt4

Qt4 application will try to mimic the behavior of the desktop environment they are running on, unless they run into some problems or hard-coded settings.

*   In KDE Plasma, it uses the actually selected Qt style. It can be configured using *KDE System Settings* (*systemsettings5*), the settings can be found in *Appearance > Application Style > Widget Style*.
*   In Cinnamon, GNOME, Xfce, it uses GTK+ ([QGtkStyle](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications")).
*   In other desktop environments, it uses Windows.

For those who want to change the look and feel of Qt4 applications, the *Qt Configuration* (*qtconfig-qt4*) GUI tool is provided by the [qt4](https://www.archlinux.org/packages/?name=qt4) package. It offers a simple interface to configure the appearance of Qt4 applications including style, colors, fonts and some further options.

**Note:** If you use *GTK+* style, then color and font settings will be ignored, and inherited from GTK+ 2.

Qt keeps all its configuration information in `/etc/xdg/Trolltech.conf` (system-wide) or `~/.config/Trolltech.conf` (user-specific). The file is rather difficult to navigate because it contains a lot of information not related to appearance, but for any changes you can just add to the end of the file and overwrite any previous values (make sure to add your modification under the [Qt] header).

For example, to change the theme to QtCurve, add:

 `~/.config/Trolltech.conf` 
```
...
[Qt]
style=QtCurve

```

The following styles are included in Qt4: *CDE*, *Cleanlooks*, *GTK+*, *Motif*, *Plastique*, *Windows*. Others can be installed from the official repositories or the [AUR](/index.php/AUR "AUR") (most are written for KDE Plasma Desktop):

*   **Breeze** — Artwork, styles and assets for the Breeze visual style for the Plasma Desktop.

	[https://cgit.kde.org/breeze.git](https://cgit.kde.org/breeze.git) || [breeze-kde4](https://www.archlinux.org/packages/?name=breeze-kde4)

*   **[Oxygen](https://en.wikipedia.org/wiki/Oxygen_Project "wikipedia:Oxygen Project")** — KDE Oxygen style.

	[https://cgit.kde.org/oxygen.git](https://cgit.kde.org/oxygen.git) || [oxygen-kde4](https://www.archlinux.org/packages/?name=oxygen-kde4)

*   **QtCurve** — A configurable set of widget styles for KDE and Gtk.

	[https://cgit.kde.org/qtcurve.git](https://cgit.kde.org/qtcurve.git) || [qtcurve-qt4](https://www.archlinux.org/packages/?name=qtcurve-qt4)

*   **Adwaita-Qt** — A style to bend Qt applications to look like they belong into GNOME Shell.

	[https://github.com/MartinBriza/adwaita-qt](https://github.com/MartinBriza/adwaita-qt) || [adwaita-qt4](https://aur.archlinux.org/packages/adwaita-qt4/)

### Qt5

Qt5 decides the style to use based on what desktop environment is used:

*   In KDE Plasma, it uses the actually selected Qt style. It can be configured using *KDE System Settings* (*systemsettings5*), the settings can be found in *Appearance > Application Style > Widget Style*.
*   In Cinnamon, GNOME, MATE, LXDE, Xfce, it uses GTK+ ([QGtkStyle](/index.php/Uniform_look_for_Qt_and_GTK_applications#QGtkStyle "Uniform look for Qt and GTK applications")).
*   In other desktop environments, it uses Fusion.

To force a specific style, you can set the `QT_STYLE_OVERRIDE` [environment variable](/index.php/Environment_variable "Environment variable"). Specifically, set it to `gtk2` if you want to use the [GTK+](/index.php/GTK%2B "GTK+") theme (Note: you will need to install the Qt style plugins mention below to get the GTK+ style). Qt5 applications also support the `-style` flag, which you can use to launch a Qt5 application with a specific style.

The following styles are included in Qt5: *Fusion*, *Windows*. Others can be installed from the official repositories:

*   **Breeze** — Artwork, styles and assets for the Breeze visual style for the Plasma Desktop.

	[https://cgit.kde.org/breeze.git](https://cgit.kde.org/breeze.git) || [breeze](https://www.archlinux.org/packages/?name=breeze)

*   **Oxygen** — KDE Oxygen style.

	[https://cgit.kde.org/oxygen.git](https://cgit.kde.org/oxygen.git) || [oxygen](https://www.archlinux.org/packages/?name=oxygen)

*   **QtCurve** — A configurable set of widget styles for KDE and Gtk.

	[https://cgit.kde.org/qtcurve.git](https://cgit.kde.org/qtcurve.git) || [qtcurve-qt5](https://www.archlinux.org/packages/?name=qtcurve-qt5)

*   **Adwaita-Qt** — A style to bend Qt applications to look like they belong into GNOME Shell.

	[https://github.com/MartinBriza/adwaita-qt](https://github.com/MartinBriza/adwaita-qt) || [adwaita-qt5](https://aur.archlinux.org/packages/adwaita-qt5/)

*   **Qt style plugins** — Additional style plugins for Qt5, including *GTK+*, *Cleanlooks*, *Motif*, *Plastique*.

	[http://code.qt.io/cgit/qt/qtstyleplugins.git](http://code.qt.io/cgit/qt/qtstyleplugins.git) || [qt5-styleplugins](https://www.archlinux.org/packages/?name=qt5-styleplugins)

### Qt Style Sheets

An interesting way of customizing the look and feel of a Qt application is using Style Sheets, which are just simple CSS files. Using Style Sheets, one can modify the appearance of every widget in the application.

To run an application with a different style just execute:

```
$ qt_application -stylesheet *style.qss*

```

For more information on Qt Style Sheets see the [official documentation](http://doc.qt.io/qt-5/stylesheet-reference.html) or other [tutorials](http://thesmithfam.org/blog/2009/09/10/qt-stylesheets-tutorial/). As an example Style Sheet see this [Dolphin modification](http://kde-apps.org/content/show.php/roxydoxy?content=125979).

### GTK+ and Qt

If you have GTK+ and Qt applications, their looks might not exactly blend in very well. If you wish to make your GTK+ styles match your Qt styles please read [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

### Configuration of Qt5 apps under environments other than KDE Plasma

Unlike Qt4, Qt5 doesn't ship a qtconfig utility to configure fonts, icons or styles. Instead, it will try to use the settings from the running DE. In KDE Plasma or GNOME this works well, but in other less popular DEs or WM it can lead to missing icons in Qt5 applications. One way to solve this is to fake the running desktop environment by setting `XDG_CURRENT_DESKTOP=KDE` or `GNOME`, and then using the corresponding configuration application to set the desired icon set.

Another solution is provided by the [qt5ct](https://www.archlinux.org/packages/?name=qt5ct) package, which provides a DE independent Qt5 QPA and a configuration utility. After installing the package, run `qt5ct` to set an icon theme, and set the environment variable `QT_QPA_PLATFORMTHEME="qt5ct"` so that the settings are picked up by Qt applications. Alternatively, use `--platformtheme qt5ct` as argument to the Qt5 application.

To automatically set `QT_QPA_PLATFORMTHEME` for user session, add the following line to `~/.xprofile`.

```
[ "$XDG_CURRENT_DESKTOP" = "KDE" ] || [ "$XDG_CURRENT_DESKTOP" = "GNOME" ] || export QT_QPA_PLATFORMTHEME="qt5ct"

```

This will export `QT_QPA_PLATFORMTHEME` environment variable for the whole user session. Note that this doesn't work on [enlightenment](/index.php/Enlightenment "Enlightenment") because it has its own custom environment variable setting instead of getting it from `~/.profile` file.

If the below errors are received, and some icons still do not appear in some of the apps, install [oxygen](https://www.archlinux.org/packages/?name=oxygen) and [oxygen-icons](https://www.archlinux.org/packages/?name=oxygen-icons):

```
Icon theme "oxygen" not found.
Icon theme "oxygen" not found.
Error: standard icon theme "oxygen" not found!

```

## Development

### Supported platforms

Qt supports most platforms that are available today, even some of the more obscure ones, with more ports appearing every once in a while. For a more complete list see the [Qt Wikipedia article](https://en.wikipedia.org/wiki/Qt_(framework)#Platforms "wikipedia:Qt (framework)").

#### Android

First of all you need an [Android SDK](/index.php/Android "Android") and NDK. Install SDK [android-sdk](https://aur.archlinux.org/packages/android-sdk/) (some tools have been removed) or [android-sdk-25.2.5](https://aur.archlinux.org/packages/android-sdk-25.2.5/) and NDK [android-ndk-10e](https://aur.archlinux.org/packages/android-ndk-10e/) from [AUR](/index.php/AUR "AUR") or using [Android Studio](/index.php/Android_Studio "Android Studio"). It is highly recommended to install NDK version [10e](https://developer.android.com/ndk/downloads/older_releases.html#ndk-10c-downloads) because of some [known issues](https://wiki.qt.io/Qt_for_Android_known_issues). Next you are going to need Qt 5 for Android. You can install it from [AUR](/index.php/AUR "AUR") as described bellow or build it yourself, you can find build instructions on Qt [wiki](http://wiki.qt.io/Android) page.

*   [android-qt5-arm64-v8a](https://aur.archlinux.org/packages/android-qt5-arm64-v8a/) - arm64-v8a [ABI](https://developer.android.com/ndk/guides/abis.html)
*   [android-qt5-armeabi](https://aur.archlinux.org/packages/android-qt5-armeabi/) - armeabi
*   [android-qt5-armeabi-v7a](https://aur.archlinux.org/packages/android-qt5-armeabi-v7a/) - armeabi-v7a
*   [android-qt5-mips](https://aur.archlinux.org/packages/android-qt5-mips/) - mips
*   [android-qt5-x86](https://aur.archlinux.org/packages/android-qt5-x86/) - x86
*   [android-qt5-x86_64](https://aur.archlinux.org/packages/android-qt5-x86_64/) - x86_64

Or you can use a [Qt Installer](https://download.qt.io/official_releases/qt/5.11/5.11.1/qt-opensource-linux-x64-5.11.1.run), for a full list see [Official Qt installers](https://download.qt.io/official_releases/qt/).

### Tools

The following are official Qt tools:

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — A cross-platform IDE tailored for Qt that supports all of its features.

	[http://doc.qt.io/qtcreator/](http://doc.qt.io/qtcreator/) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **Qt Linguist** — A set of tools that speed the translation and internationalization of Qt applications.

	[http://doc.qt.io/qt-5/qtlinguist-index.html](http://doc.qt.io/qt-5/qtlinguist-index.html) || Qt 5: [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **Qt Assistant** — A configurable and redistributable documentation reader for Qt *qch* files.

	[http://doc.qt.io/qt-5/qtassistant-index.html](http://doc.qt.io/qt-5/qtassistant-index.html) || Qt 5: [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **Qt Designer** — A powerful cross-platform GUI layout and forms builder for Qt widgets.

	[http://doc.qt.io/qt-5/qtdesigner-manual.html](http://doc.qt.io/qt-5/qtdesigner-manual.html) || Qt 5: [qt5-tools](https://www.archlinux.org/packages/?name=qt5-tools), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **Qt Quick Designer** — A visual editor for QML files which supports WYSIWYG. It allows you to rapidly design and build Qt Quick applications and components from scratch.

	[http://doc.qt.io/qtcreator/creator-using-qt-quick-designer.html](http://doc.qt.io/qtcreator/creator-using-qt-quick-designer.html) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **qmlscene** — A tool for loading QML documents that makes it easy to quickly develop and debug QML applications.

	[http://doc.qt.io/qt-5/qtquick-qmlscene.html](http://doc.qt.io/qt-5/qtquick-qmlscene.html) || Qt 5: [qt5-declarative](https://www.archlinux.org/packages/?name=qt5-declarative), Qt 4 QML Viewer: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **[qmake](https://en.wikipedia.org/wiki/Qmake "wikipedia:Qmake")** — A tool that helps simplify the build process for development project across different platforms, similar to [cmake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake"), but with fewer options and tailored for Qt applications.

	[http://doc.qt.io/qt-5/qmake-manual.html](http://doc.qt.io/qt-5/qmake-manual.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **uic** — A tool that reads **.ui* XML files and generates the corresponding C++ files.

	[http://doc.qt.io/qt-5/uic.html](http://doc.qt.io/qt-5/uic.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **rcc** — A tool that is used to embed resources (such as pictures) into a Qt application during the build process. It works by generating a C++ source file containing data specified in a Qt resource (.qrc) file.

	[http://doc.qt.io/qt-5/rcc.html](http://doc.qt.io/qt-5/rcc.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

*   **moc** — A tool that handles Qt's C++ extensions (the signals and slots mechanism, the run-time type information, and the dynamic property system, etc.).

	[http://doc.qt.io/qt-5/moc.html](http://doc.qt.io/qt-5/moc.html) || Qt 5: [qt5-base](https://www.archlinux.org/packages/?name=qt5-base), Qt 4: [qt4](https://www.archlinux.org/packages/?name=qt4)

### Bindings

Qt has bindings for all of the more popular languages, for a full list see [this list](https://en.wikipedia.org/wiki/Qt_(framework)#Programming_language_bindings "wikipedia:Qt (framework)").

The following examples display a small 'Hello world!' message in a window.

#### C++

*   Package:
    *   [qt4](https://www.archlinux.org/packages/?name=qt4) - Version 4.x of the Qt toolkit.
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

*   Package: [qt4](https://www.archlinux.org/packages/?name=qt4) or [qt5-declarative](https://www.archlinux.org/packages/?name=qt5-declarative).
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
    *   [python-pyqt4](https://www.archlinux.org/packages/?name=python-pyqt4) - Python 3.x bindings for Qt 4
    *   [python2-pyqt4](https://www.archlinux.org/packages/?name=python2-pyqt4) - Python 2.x bindings for Qt 4
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

See [QtSharp](https://gitlab.com/ddobrev/QtSharp).

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

## Troubleshooting

### Qt programs crash when opening file dialogs under GNOME Wayland

Under a GNOME Wayland environment, Qt programs such as Smplayer and Calibre may crash when opening a "FileDiag" (e.g. the "Open file" or "Save as" dialogs), because by default Qt tries to use the native GTK FileDiag, but the invocation assumes the use of X11 and would segfault in Wayland. This issue can be worked around in two ways:

*   Force the use of X11 GDK backend for these Qt programs.

```
GDK_BACKEND=x11 some_qt_program

```

*   Install the latest git snapshot of [qgnomeplatform-git](https://aur.archlinux.org/packages/qgnomeplatform-git/), which contains a fix. The platform plugin should work automatically under GNOME (3.20 or later); if not, manually set the [environment variable](/index.php/Environment_variables#Using_pam_env "Environment variables"): `QT_QPA_PLATFORMTHEME=qgnomeplatform` . This also has the effect of [uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications").

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

If pure Qt4 (non-KDE) applications do not stick with your selected Qt4 style, then you'll probably need to tell Qt4 how to find KDE's styles (Oxygen, Phase etc.). You just need to set the environment variable `QT_PLUGIN_PATH`. E.g. put

```
export QT_PLUGIN_PATH=$HOME/.kde4/lib/kde4/plugins/:/usr/lib/kde4/plugins/

```

into your `/etc/profile` (or `~/.profile` if you do not have root access). `qtconfig-qt4` should then be able to find your kde styles and everything should look nice again!

Alternatively, you can symlink the Qt4 styles directory to the KDE4 styles one:

```
# ln -s /usr/lib/{kde,qt}4/plugins/styles/[theme name]

```

### Applications using QML crash or don't work with Qt 5.8

Starting with Qt 5.8, applications that rely on QML (such as [SDDM](/index.php/SDDM "SDDM") or some [KDE](/index.php/KDE "KDE") programs) may crash or fail to function correctly if they do not have execution privileges under `/home` or `/var` (e.g. if these are separate filesystems mounted as '`noexec`'). This is a result of the **qmlcache** feature, which relies on being able to write files out to `.cache` directories and then execute them. See also BBS thread [222486: sddm-helper crashes](https://bbs.archlinux.org/viewtopic.php?id=222486).

If you do not want to -- or cannot -- allow such execution privileges, a workaround is to set the following as appropriate in your [environment variables](/index.php/Environment_variables "Environment variables"):

 `QML_DISABLE_DISK_CACHE=1` 

### All Qt5-based applications fail to run after Qt5 update

If you get an error similar to

```
Qt FATAL: Cannot mix incompatible Qt library (version 0x50900) with this library (version 0x50901)

```

then you are most likely using a Qt5 platform theme or style plugin which has not been recompiled against the latest version of Qt5\. These usually use Qt private headers which means they depend on an exact version of Qt and not just a matching soname. Figure out which theme/style you are using by checking the `QT_STYLE_OVERRIDE` and `QT_QPA_PLATFORMTHEME` environment variables, and rebuild the AUR package that provides it.

## See also

*   [Official Website](http://qt.io/)
*   [Qt Documentation](http://doc.qt.io/)
*   [Planet Qt](http://planet.qt.io/)
*   [Qt Applications](http://qt-apps.org/)