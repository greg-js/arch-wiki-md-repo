# GNOME package guidelines

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – **GNOME** – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

The [GNOME](/index.php/GNOME "GNOME") packages on Arch Linux follow a certain schema.

## Contents

*   [1 GNOME profile initialization](#GNOME_profile_initialization)
*   [2 GConf schemas](#GConf_schemas)
*   [3 GSettings schemas](#GSettings_schemas)
*   [4 Scrollkeeper documentation](#Scrollkeeper_documentation)
*   [5 .desktop files](#.desktop_files)
*   [6 GTK icon cache](#GTK_icon_cache)
*   [7 .install files](#.install_files)
*   [8 Example](#Example)

## GNOME profile initialization

There is no GNOME profile initialization anymore. The old line below should be stripped from any [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"):

 `[ -z "$GNOMEDIR" ] && . /etc/profile.d/gnome.sh` 

## GConf schemas

Many GNOME packages install [GConf schemas](https://en.wikipedia.org/wiki/GConf#Schemas "wikipedia:GConf"). These schemas get installed in the system GConf database, which has to be avoided. Some packages provide a `--disable-schemas-install` switch for **./configure**, which hardly ever works. Therefore, gconftool-2 has a variable called `GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL`, whenever this is set, gconftool-2 will not update any databases.

When creating packages that install schema files, use

 `make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install` 

for the package installation step in the PKGBUILD.

GConf schemas need to be installed and removed in the `.install` file using `pre_remove`, `pre_upgrade` and `post_upgrade` and `post_install`. Use **gconf-merge-schemas** to merge several schemas into one package specific file, install or uninstall them with `usr/sbin/gconfpkg --_(un)_install $pkgname` The usage of **gconfpkg** requres a dependency on [gconf](https://www.archlinux.org/packages/?name=gconf)>=2.18.0.1-4 (or [gconfmm](https://www.archlinux.org/packages/?name=gconfmm)>=2.20.0).

## GSettings schemas

The GConf schemas will be replaced by GSettings schemas in the near future, but some applications (e.g. Empathy) already using it. GSettings uses dconf as backend, so all packages that contain GSettings schemas require dconf as dependency. When a new GSettings schema installed on the system, the GSettings database should be recompiled, but not when packaging. To avoid recompiling GSettings database on packaging, use the `--disable-schemas-compile` switch for **./configure**. To recompile it on install, add the following line to the .install file using post_install, post_upgrade and post_remove:

```
glib-compile-schemas usr/share/glib-2.0/schemas

```

## Scrollkeeper documentation

Starting from GNOME 2.20 there is no need to handle scrollkeeper anymore, as rarian reads OMF files directly. Scrollkeeper-update is a dummy these days. The only required thing now is to makedepend on [gnome-doc-utils](https://www.archlinux.org/packages/?name=gnome-doc-utils)>=0.11.2.

## .desktop files

Many packages install Freedesktop.org compatible `.desktop` files and register MimeType entries in them. Running `update-desktop-database -q` in `post_install` and `post_remove` is recommended (package should depend on [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) in this case).

## GTK icon cache

Quite some packages install icons in the hicolor icon theme. These packages should depend on [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache) and should have `gtk-update-icon-cache -q -t -f usr/share/icons/hicolor` (WITHOUT leading slash) in the `post_install`, `post_upgrade` and `post_remove` function.

## .install files

For many GNOME packages, all .install files look almost exactly the same. The [gedit](https://www.archlinux.org/packages/?name=gedit) package contains a very generic install file: [https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-x86_64/gedit.install](https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-x86_64/gedit.install)

Basically, the only thing that has to be changed is the `pkgname` variable on top of the `.install` file. As long as pacman does not supply us with the `pkgname` variable, we need to supply it in the `.install` file. When packages do not have gconf schemas, hicolor icon files, or `.desktop` files, remove the parts that handle those subjects.

## Example

For an example of above rules, take a look at the gedit PKGBUILD and the `.install` file supplied above: [https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-x86_64/](https://projects.archlinux.org/svntogit/packages.git/tree/gedit/repos/extra-x86_64/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=GNOME_package_guidelines&oldid=395926](https://wiki.archlinux.org/index.php?title=GNOME_package_guidelines&oldid=395926)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")