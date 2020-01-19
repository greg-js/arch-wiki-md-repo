Related articles

*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [PKGBUILD](/index.php/PKGBUILD "PKGBUILD")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [Security package guidelines](/index.php/Security_package_guidelines "Security package guidelines")

When building packages for Arch Linux, **adhere to the package guidelines** below, especially if the intention is to **contribute** a new package to Arch Linux. You should also see the [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) and [makepkg(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/makepkg.8) manpages.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 PKGBUILD prototype](#PKGBUILD_prototype)
*   [2 Package etiquette](#Package_etiquette)
*   [3 Package naming](#Package_naming)
*   [4 Package versioning](#Package_versioning)
*   [5 Package dependencies](#Package_dependencies)
*   [6 Package relations](#Package_relations)
*   [7 Package sources](#Package_sources)
*   [8 Working with upstream](#Working_with_upstream)
*   [9 Directories](#Directories)
*   [10 Makepkg duties](#Makepkg_duties)
*   [11 Architectures](#Architectures)
*   [12 Licenses](#Licenses)
*   [13 Additional guidelines](#Additional_guidelines)

## PKGBUILD prototype

```
# Maintainer: Your Name <youremail@domain.com>
pkgname=NAME
pkgver=VERSION
pkgrel=1
pkgdesc=""
arch=()
url=""
license=('GPL')
groups=()
depends=()
makedepends=()
optdepends=()
provides=()
conflicts=()
replaces=()
backup=()
options=()
install=
changelog=
source=($pkgname-$pkgver.tar.gz)
noextract=()
md5sums=() #autofill using updpkgsums

build() {
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}
```

Other prototypes are found in `/usr/share/pacman/` from the pacman and abs packages.

## Package etiquette

*   Packages should **never** be installed to `/usr/local/`
*   **Do not introduce new variables or functions** into `PKGBUILD` build scripts, unless the package cannot be built without doing so, as these could possibly **conflict** with variables and functions used in makepkg itself.
*   If a new variable or a new function is absolutely required, **prefix its name with an underscore** (`_`), e.g. `_customvariable=` 
*   **Avoid** using `/usr/libexec/` for anything. Use `/usr/lib/$pkgname/` instead.
*   The `packager` field from the package meta file can be **customized** by the package builder by modifying the appropriate option in the `/etc/makepkg.conf` file, or alternatively override it by creating `~/.makepkg.conf`.
*   **Do not use makepkg subroutines** (e.g. `error`, `msg`, `msg2`, `plain`, `warning`) as they might change at any time. To print data, use `printf` or `echo`.
*   All important messages should be echoed during install using an **.install file**. For example, if a package needs extra setup to work, directions should be included.
*   **Dependencies** are the most common packaging error. Please take the time to verify them carefully, for example by running `ldd` on dynamic executables, checking tools required by scripts or looking at the documentation of the software. The [namcap](/index.php/Namcap "Namcap") utility can help you in this regard. This tool can analyze both PKGBUILD and the resulting package tarball and will warn you about bad permissions, missing dependencies, redundant dependencies, and other common mistakes.
*   Any **optional dependencies** that are not needed to run the package or have it generally function should not be included in the **depends** array; instead the information should be added to the **optdepends** array:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

	The above example is taken from the **wine** package in `extra`. The optdepends information is automatically printed out on installation/upgrade so one should **not** keep this kind of information in `.install` files.

*   When creating a **package description** for a package, do not include the package name in a self-referencing way. For example, "Nedit is a text editor for X11" could be simplified to "A text editor for X11". Also try to keep the descriptions to ~80 characters or less.
*   Try to keep the **line length** in the PKGBUILD below ~100 characters.
*   Where possible, **remove empty lines** from the `PKGBUILD` (`provides`, `replaces`, etc.)
*   It is common practice to **preserve the order** of the `PKGBUILD` fields as shown above. However, this is not mandatory, as the only requirement in this context is **correct bash syntax**.
*   **Quote** variables which may contain spaces, such as `"$pkgdir"` and `"$srcdir"`.
*   To ensure the **integrity** of packages, make sure that the [integrity variables](/index.php/PKGBUILD#Integrity "PKGBUILD") contain correct values. These can be updated using the `updpkgsums` tool.

## Package naming

*   Package names can contain only alphanumeric characters and any of `@`, `.`, `_`, `+`, `-`. Names are not allowed to start with hyphens or dots. All letters should be lowercase.
*   Package names should NOT be suffixed with the upstream major release version number (e.g. we do not want libfoo2 if upstream calls it libfoo v2.3.4) in case the library and its dependencies are expected to be able to keep using the most recent library version with each respective upstream release. However, for some software or dependencies, this can not be assumed. In the past this has been especially true for widget toolkits such as GTK and Qt. Software that depends on such toolkits can usually not be trivially ported to a new major version. As such, in cases where software can not trivially keep rolling alongside its dependencies, package names should carry the major version suffix (e.g. gtk2, gtk3, qt4, qt5). For cases where most dependencies can keep rolling along the newest release but some cannot (for instance closed source that needs libpng12 or similar), a deprecated version of that package might be called libfoo1 while the current version is just libfoo.

## Package versioning

*   Package versions (i.e. [PKGBUILD#pkgver](/index.php/PKGBUILD#pkgver "PKGBUILD")) **should be the same as the version released by the author**. Versions can include letters if need be (eg, nmap's version is 2.54BETA32). **Version tags may not include hyphens!** Letters, numbers, and periods only.
*   **Stable packages package stable releases**: Release candidates (i.e. `1.0.0-rc1`), alpha (e.g. `1.0.0-alpha1`) and beta (e.g. `1.0.0-beta1`) releases are not allowed and are only to be used under the following circumstances:
    *   The non-stable release holds **urgent** security fixes (and backporting is non-trivial).
    *   The non-stable release allows for the package to be built (e.g. problems introduced due to updated dependencies) and those changes can not otherwise be backported easily.
    *   The non-stable release allows the distribution to drop an EOL component (e.g. qt4, python2).
*   Package releases (i.e. [PKGBUILD#pkgrel](/index.php/PKGBUILD#pkgrel "PKGBUILD")) are **specific to Arch Linux packages**. These allow users to differentiate between newer and older package builds. When a new package version is first released, the **release count starts at 1**. Then as fixes and optimizations are made, the package will be **re-released** to the Arch Linux public and the **release number will increment**. When a new version comes out, the release count resets to 1\. Package release tags follow the **same naming restrictions as version tags**.

## Package dependencies

*   **Do not rely on [transitive dependencies](https://en.wikipedia.org/wiki/Transitive_dependency "wikipedia:Transitive dependency")** in any of the [PKGBUILD#Dependencies](/index.php/PKGBUILD#Dependencies "PKGBUILD"), as they might break, if one of the dependencies is updated.
*   List all direct library dependencies. To identify them [find-libdeps(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find-libdeps.1) (part of [devtools](https://www.archlinux.org/packages/?name=devtools)) can be used.

## Package relations

*   Do not add `$pkgname` to [PKGBUILD#provides](/index.php/PKGBUILD#provides "PKGBUILD"), as it is always implicitely provided by the package.
*   List all external shared libraries of a package in [PKGBUILD#provides](/index.php/PKGBUILD#provides "PKGBUILD") (e.g. `'libsomething.so'`). To identify them [find-libprovides(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/find-libprovides.1) (part of [devtools](https://www.archlinux.org/packages/?name=devtools)) can be used.

## Package sources

*   HTTPS sources (`https://` for tarballs, `git+https://` for git sources) should be used wherever possible
*   Sources should be verified using PGP signatures wherever possible (this might entail building from a git tag instead of a source tarball, if upstream signs commits and tags but not the tarballs)
*   **Do not diminish the security or validity of a package** (e.g. by removing a checksum check or by removing PGP signature verification), because an upstream release is broken or suddenly lacks a certain feature (e.g. PGP signature missing for a new release)
*   Sources have to be unique in `srcdir` (this might require renaming them when downloading, e.g. `"${pkgname}-${pkgver}.tar.gz::https://${pkgname}.tld/download/${pkgver}.tar.gz"`)
*   Avoid using specific mirrors (e.g. on sourceforge) to download, as they might become unavailable

## Working with upstream

It is considered best-practice to work closely with upstream wherever possible. This entails reporting problems about building and testing a package.

*   Report problems to upstream right away.
*   Upstream patches wherever possible.
*   Add comments with links to relevant (upstream) bug tracker tickets in the [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") (this is particularly important, as it ensures, that other packagers can understand changes and work with a package as well).

## Directories

*   **Configuration files** should be placed in the `/etc` directory. If there is more than one configuration file, it is customary to **use a subdirectory** in order to keep the `/etc` area as clean as possible. Use `/etc/{pkgname}/` where `{pkgname}` is the name of the package (or a suitable alternative, eg, apache uses `/etc/httpd/`).
*   Package files should follow these **general directory guidelines**:

| `/etc` | **System-essential** configuration files |
| `/usr/bin` | Binaries |
| `/usr/lib` | Libraries |
| `/usr/include` | Header files |
| `/usr/lib/{pkg}` | Modules, plugins, etc. |
| `/usr/share/doc/{pkg}` | Application documentation |
| `/usr/share/info` | GNU Info system files |
| `/usr/share/man` | Manpages |
| `/usr/share/{pkg}` | Application data |
| `/var/lib/{pkg}` | Persistent application storage |
| `/etc/{pkg}` | Configuration files for `{pkg}` |
| `/opt/{pkg}` | Large self-contained packages |

*   Packages should not contain any of the following directories:
    *   `/bin`
    *   `/sbin`
    *   `/dev`
    *   `/home`
    *   `/srv`
    *   `/media`
    *   `/mnt`
    *   `/proc`
    *   `/root`
    *   `/selinux`
    *   `/sys`
    *   `/tmp`
    *   `/var/tmp`
    *   `/run`

## Makepkg duties

When [makepkg](/index.php/Makepkg "Makepkg") is used to build a package, it does the following automatically:

1.  Checks if package **dependencies** and **makedepends** are installed
2.  **Downloads source** files from servers
3.  **Checks the integrity** of source files
4.  **Unpacks** source files
5.  Does any necessary **patching**
6.  **Builds** the software and installs it in a fake root
7.  **Strips** symbols from binaries
8.  **Strips** debugging symbols from libraries
9.  **Compresses** manual and, or info pages
10.  Generates the **package meta file** which is included with each package
11.  **Compresses** the fake root into the package file
12.  **Stores** the package file in the configured destination directory (cwd by default)

## Architectures

The `arch` array should contain `'x86_64'` if the compiled package is architecture-specific. Otherwise, use `'any'` for architecture independent packages.

## Licenses

See [PKGBUILD#license](/index.php/PKGBUILD#license "PKGBUILD").

## Additional guidelines

Be sure to read the above guidelines first - important points are listed on this page that will not be repeated in the following guideline pages. These specific guidelines are intended as an addition to the standards listed on this page.

**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[32-bit](/index.php/32-bit_package_guidelines "32-bit package guidelines") – [CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Packages submitted to the AUR must additionally comply with [AUR submission guidelines](/index.php/AUR_submission_guidelines "AUR submission guidelines").