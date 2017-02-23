**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – **GNOME** – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

The [GNOME](/index.php/GNOME "GNOME") packages on Arch Linux follow a certain schema.

## Contents

*   [1 GConf schemas](#GConf_schemas)
*   [2 GSettings schemas](#GSettings_schemas)
*   [3 Scrollkeeper documentation](#Scrollkeeper_documentation)
*   [4 GTK icon cache](#GTK_icon_cache)
*   [5 .desktop files](#.desktop_files)
*   [6 .install files](#.install_files)

## GConf schemas

Some GNOME packages install [GConf schemas](https://en.wikipedia.org/wiki/GConf#Schemas "wikipedia:GConf"), even though many others already migrated to GSettings. Those packages should depend on [gconf](https://www.archlinux.org/packages/?name=gconf).

Gconf schemas get installed in the system GConf database, which has to be avoided. Some packages provide a `--disable-schemas-install` switch for **./configure**, which hardly ever works. However, gconftool-2 has a variable called `GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL` which you can set to tell gconftool-2 to not update any databases.

When creating packages that install GConf schema files, use

 `make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install` 

for the package installation step in the PKGBUILD.

Do not call `gconfpkg` in the .install file, as GConf schemas are automatically installed/removed (while installing/removing the GNOME package) via [pacman hooks](/index.php/Pacman#Hooks "Pacman") since [gconf](https://www.archlinux.org/packages/?name=gconf)=3.2.6-4

## GSettings schemas

The GConf schemas were migrated to GSettings schemas, so many GNOME applications can be found using this new schema file. GSettings uses dconf as backend, so all packages that contain GSettings schemas require [dconf](https://www.archlinux.org/packages/?name=dconf) as dependency. When a new GSettings schema installed on the system, the GSettings database has to be recompiled, but not when packaging.

To avoid recompiling GSettings database on packaging, use the `--disable-schemas-compile` switch for **./configure**.

Do not call `glib-compile-schemas` in the .install file, as GSettings schema databases are automatically recompiled via [pacman hooks](/index.php/Pacman#Hooks "Pacman") since [glib2](https://www.archlinux.org/packages/?name=glib2)=2.48.0-2.

## Scrollkeeper documentation

Starting from GNOME 2.20 there is no need to handle scrollkeeper anymore, as [rarian](https://www.archlinux.org/packages/?name=rarian) reads its OMF files directly. Scrollkeeper-update is a dummy these days. The only required thing now is to makedepend on [gnome-doc-utils](https://www.archlinux.org/packages/?name=gnome-doc-utils)>=0.11.2.

It can be disabled using `--disable-scrollkeeper` switch from **./configure**.

## GTK icon cache

Quite some packages install icons in the hicolor icon theme. These packages should depend on [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache).

Do not call `gtk-update-icon-cache` in the .install file, as the icon cache is updated via [pacman hooks](/index.php/Pacman#Hooks "Pacman") since [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache)=3.20.3-2.

## .desktop files

Many packages install Freedesktop.org compatible `.desktop` files and register MimeType entries in them. They should depend on [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)

Do not call `update-desktop-database` in the .install file, as the database is automatically updated via [pacman hooks](/index.php/Pacman#Hooks "Pacman") since [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)=0.22-2.

## .install files

Previously, most of the GNOME packages had a .install file calling commands like `glib-compile-schemas`, `gtk-update-icon-cache`, and `update-desktop-database` in order to install/update local cache or databases. This is deprecated since pacman 5.0 implemented [hooks](/index.php/Pacman#Hooks "Pacman") which call those commands automatically when installing the package.

To avoid being called twice, the above mentioned commands should be removed from .install file.