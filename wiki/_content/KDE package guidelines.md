# KDE package guidelines

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – **KDE** – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

The [KDE](/index.php/KDE "KDE") packages on Arch Linux follow a certain schema.

## Contents

*   [1 Build directory](#Build_directory)
*   [2 Install prefix](#Install_prefix)
*   [3 Build type](#Build_type)
*   [4 Force Qt4](#Force_Qt4)
    *   [4.1 KDE4](#KDE4)
    *   [4.2 KF5](#KF5)
*   [5 KDE4 package naming](#KDE4_package_naming)
    *   [5.1 KDE Config Module](#KDE_Config_Module)
    *   [5.2 Plasma widgets](#Plasma_widgets)
    *   [5.3 Runners](#Runners)
    *   [5.4 Service menus](#Service_menus)
    *   [5.5 Themes](#Themes)
*   [6 KF5 package naming](#KF5_package_naming)
    *   [6.1 Plasma widgets](#Plasma_widgets_2)
    *   [6.2 Runners](#Runners_2)
    *   [6.3 Service menus](#Service_menus_2)
    *   [6.4 Themes](#Themes_2)
*   [7 .install files](#.install_files)

## Build directory

A good way of building [CMake](https://en.wikipedia.org/wiki/CMake "wikipedia:CMake") packages is to make a build directory outside the root of the project and run cmake from that directory. The [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") should look this way:

```
prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../${pkgname}-${pkgver}
}

```

## Install prefix

Every packages must set the `CMAKE_INSTALL_PREFIX` variable, but also we have to respect custom built versions of KDE, so please use:

```
-DCMAKE_INSTALL_PREFIX=$(kde4-config --prefix)

```

When a package is moved to [extra] or [community] that line must be changed to:

```
-DCMAKE_INSTALL_PREFIX=/usr

```

## Build type

Please specify the build type; this makes it really simple to rebuild a package with debug symbols by just using a sed rule.

```
-DCMAKE_BUILD_TYPE=Release

```

## Force Qt4

### KDE4

On systems where both [qt4](https://www.archlinux.org/packages/?name=qt4) and [qt5-base](https://www.archlinux.org/packages/?name=qt5-base) are installed, `qmake` refers to the 5.x version, so force cmake to use Qt4 this way:

```
 export QT_SELECT=4

```

or using this option in cmake:

```
-DQT_QMAKE_EXECUTABLE=/usr/bin/qmake-qt4

```

### KF5

The same rules as for KDE4, but you need force cmake to use Qt5 instead of Qt4:

```
 export QT_SELECT=5

```

## KDE4 package naming

### KDE Config Module

KDE Config Module packages should be named `kcm-_module_`.

### Plasma widgets

Plasma widgets (formerly Plasmoids) packages should be named `kdeplasma-applets-_widgetname_` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages; this also distinguishes them from the official packages.

### Runners

Plasma runners packages should be named `kdeplasma-runners-_runnername_` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages; this also distinguishes them from the official packages.

### Service menus

Service menus packages should be named `kde-servicemenus-_servicename_` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages

### Themes

Plasma themes packages should be named `kdeplasma-themes-_themename_` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages.

## KF5 package naming

### Plasma widgets

Plasma widgets (formerly Plasmoids) packages should be named `plasma5-applets-_widgetname_` so that they are recognizable as [Plasma 5](/index.php?title=Plasma_5&action=edit&redlink=1 "Plasma 5 (page does not exist)")-related packages; this also distinguishes them from the official packages.

### Runners

Plasma runners packages should be named `plasma5-runners-_runnername_` so that they are recognizable as [Plasma 5](/index.php?title=Plasma_5&action=edit&redlink=1 "Plasma 5 (page does not exist)")-related packages; this also distinguishes them from the official packages.

### Service menus

Service menus packages should be named `kf5-servicemenus-_servicename_` so that they are recognizable as [KF5](/index.php?title=KF5&action=edit&redlink=1 "KF5 (page does not exist)")-related packages

### Themes

Plasma themes packages should be named `plasma5-themes-_themename_` so that they are recognizable as [Plasma 5](/index.php?title=Plasma_5&action=edit&redlink=1 "Plasma 5 (page does not exist)")-related packages.

## .install files

For many [KDE](/index.php/KDE "KDE") packages, all `.install` files look almost exactly the same. Some packages install icons in the hicolor icon theme; use the `xdg-icon-resource` utility provided by the [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils) package, which is a dependency of the [qt4](https://www.archlinux.org/packages/?name=qt4) package. So use this line:

```
xdg-icon-resource forceupdate --theme hicolor &> /dev/null

```

Many packages install Freedesktop.org compatible `.desktop` files and register MimeType entries in them. Running `update-desktop-database` in `post_install` is recommended as that tool is provided by the [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) package which is a dependency of the [qt4](https://www.archlinux.org/packages/?name=qt4) package. So use this line:

```
update-desktop-database -q

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=KDE_package_guidelines&oldid=357447](https://wiki.archlinux.org/index.php?title=KDE_package_guidelines&oldid=357447)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")