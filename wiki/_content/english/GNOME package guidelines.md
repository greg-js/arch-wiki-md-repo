**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – <a class="mw-selflink selflink">GNOME</a> – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

The [GNOME](/index.php/GNOME "GNOME") packages on Arch Linux follow a certain schema.

## Contents

*   [1 Source URL](#Source_URL)
    *   [1.1 Using released tarball](#Using_released_tarball)
    *   [1.2 Using a commit from Git repository](#Using_a_commit_from_Git_repository)
*   [2 GConf schemas](#GConf_schemas)
*   [3 GSettings schemas](#GSettings_schemas)
*   [4 Scrollkeeper documentation](#Scrollkeeper_documentation)
*   [5 GTK icon cache](#GTK_icon_cache)
*   [6 .desktop files](#.desktop_files)
*   [7 .install files](#.install_files)

## Source URL

This topic contains the most commonly used source URL used by GNOME packages in both [official repositories](/index.php/Official_repositories "Official repositories") and [AUR](/index.php/AUR "AUR"). For examples, search for GNOME packages in the official repositories[[1]](https://www.archlinux.org/packages/?q=gnome) and in the AUR[[2]](https://aur.archlinux.org/packages/?K=gnome)

### Using released tarball

When downloading a released tarball, you can get it from [https://download.gnome.org](https://download.gnome.org) using the following source array:

```
source=(https://download.gnome.org/sources/$pkgname/${pkgver%.*}/$pkgname-$pkgver.tar.xz)

```

where *${pkgver%.*}* returns the *major*.*minor* package version, by removing the suffix of `pkgver` (which is the *micro* package version). E.g., if *pkgver=3.28.0* then *${pkgver%.*}* would return *3.28*.

### Using a commit from Git repository

Another common practice is to use as source a specific commit from a GNOME software's source code git repository. It doesn't classify as VCS package because Pacman's feature of setting specific commit[[3]](https://www.archlinux.org/pacman/PKGBUILD.5.html#_using_vcs_sources_a_id_vcs_a) makes PKGBUILD not follow latest development commits neither update the `pkgver` field, using the source from the specified commit hash instead.

See a template below:

 `PKGBUILD` 
```
makedepends=(git)
commit=*hash_of_a_commit* 
source=("git+https://git.gnome.org/browse/$pkgname#commit=$_commit")
md5sums=('SKIP')

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/-/+/g'
}
```

Replace *hash_of_a_commit* with the Git commit hash desired.

Please notice that since the source is downloaded with *git*, then [git](https://www.archlinux.org/packages/?name=git) must be in makedepends and checksums must be set to 'SKIP', just like it would happen with any other VCS package. Using `pkgver()` function is highly recommended, so it sets `pkgver` accordingly for the commit hash provided.

**Note:** GNOME is migrating from [https://git.gnome.org](https://git.gnome.org) to [https://gitlab.gnome.org](https://gitlab.gnome.org). A automatic redirection between the old and the new Git server avoids hitting a 404 Error (page not found error), but, if you need, change the source URL to gitlab.gnome.org in order to fix the source URL.

## GConf schemas

Some GNOME packages install [GConf schemas](https://en.wikipedia.org/wiki/GConf#Schemas "wikipedia:GConf"), even though many others already migrated to GSettings. Those packages should depend on [gconf](https://www.archlinux.org/packages/?name=gconf).

Gconf schemas get installed in the system GConf database, which has to be avoided. Some packages provide a `--disable-schemas-install` switch for **./configure**, which hardly ever works. However, gconftool-2 has a variable called `GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL` which you can set to tell gconftool-2 to not update any databases.

When creating packages that install GConf schema files, use

 `make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR=${pkgdir} install` 

for the package installation step in the PKGBUILD.

Do not call `gconfpkg` in the .install file, as GConf schemas are automatically installed/removed (while installing/removing the GNOME package) via [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") since [gconf](https://www.archlinux.org/packages/?name=gconf)=3.2.6-4

## GSettings schemas

The GConf schemas were migrated to GSettings schemas, so many GNOME applications can be found using this new schema file. GSettings uses dconf as backend, so all packages that contain GSettings schemas require [dconf](https://www.archlinux.org/packages/?name=dconf) as dependency. When a new GSettings schema installed on the system, the GSettings database has to be recompiled, but not when packaging.

To avoid recompiling GSettings database on packaging, use the `--disable-schemas-compile` switch for **./configure**.

Do not call `glib-compile-schemas` in the .install file, as GSettings schema databases are automatically recompiled via [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") since [glib2](https://www.archlinux.org/packages/?name=glib2)=2.48.0-2.

## Scrollkeeper documentation

Starting from GNOME 2.20 there is no need to handle scrollkeeper anymore, as [rarian](https://www.archlinux.org/packages/?name=rarian) reads its OMF files directly. Scrollkeeper-update is a dummy these days. The only required thing now is to makedepend on [gnome-doc-utils](https://www.archlinux.org/packages/?name=gnome-doc-utils)>=0.11.2.

It can be disabled using `--disable-scrollkeeper` switch from **./configure**.

## GTK icon cache

Quite some packages install icons in the hicolor icon theme. These packages should depend on [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache).

Do not call `gtk-update-icon-cache` in the .install file, as the icon cache is updated via [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") since [gtk-update-icon-cache](https://www.archlinux.org/packages/?name=gtk-update-icon-cache)=3.20.3-2.

## .desktop files

Many packages install Freedesktop.org compatible `.desktop` files and register MimeType entries in them. They should depend on [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)

Do not call `update-desktop-database` in the .install file, as the database is automatically updated via [pacman hooks](/index.php/Pacman_hooks "Pacman hooks") since [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils)=0.22-2.

## .install files

Previously, most of the GNOME packages had a .install file calling commands like `glib-compile-schemas`, `gtk-update-icon-cache`, and `update-desktop-database` in order to install/update local cache or databases. This is deprecated since pacman 5.0 implemented [hooks](/index.php/Pacman#Hooks "Pacman") which call those commands automatically when installing the package.

To avoid being called twice, the above mentioned commands should be removed from .install file.