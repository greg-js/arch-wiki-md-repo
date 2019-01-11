**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – <a class="mw-selflink selflink">KDE</a> – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

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
*   [7 Icons and .desktop files installation](#Icons_and_.desktop_files_installation)

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

KDE Config Module packages should be named `kcm-*module*`.

### Plasma widgets

Plasma widgets (formerly Plasmoids) packages should be named `kdeplasma-applets-*widgetname*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages; this also distinguishes them from the official packages.

### Runners

Plasma runners packages should be named `kdeplasma-runners-*runnername*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages; this also distinguishes them from the official packages.

### Service menus

Service menus packages should be named `kde-servicemenus-*servicename*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages

### Themes

Plasma themes packages should be named `kdeplasma-themes-*themename*` so that they are recognizable as [KDE](/index.php/KDE "KDE")-related packages.

## KF5 package naming

### Plasma widgets

Plasma widgets (formerly Plasmoids) packages should be named `plasma5-applets-*widgetname*` so that they are recognizable as Plasma 5-related packages; this also distinguishes them from the official packages.

### Runners

Plasma runners packages should be named `plasma5-runners-*runnername*` so that they are recognizable as Plasma 5-related packages; this also distinguishes them from the official packages.

### Service menus

Service menus packages should be named `kf5-servicemenus-*servicename*` so that they are recognizable as KF5-related packages

### Themes

Plasma themes packages should be named `plasma5-themes-*themename*` so that they are recognizable as Plasma 5-related packages.

## Icons and .desktop files installation

Some [KDE](/index.php/KDE "KDE") software provide icons in the hicolor icon theme and `.desktop` files, which must be installed via [pacman hooks](/index.php/Pacman_hooks "Pacman hooks"). Refrain from using installation command for these type of files in a `.install`, as it would result in unnecessary double execution of them.

The [qt4](https://www.archlinux.org/packages/?name=qt4) package already depends on [xdg-utils](https://www.archlinux.org/packages/?name=xdg-utils), [hicolor-icon-theme](https://www.archlinux.org/packages/?name=hicolor-icon-theme) and [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils), so if your package depends [qt4](https://www.archlinux.org/packages/?name=qt4), no other action should be needed (i.e. no need to add these packages to `depends` array).