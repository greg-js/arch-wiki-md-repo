<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Packaging Standards](#Packaging_Standards)
    *   [1.1 PKGBUILD Prototype](#PKGBUILD_Prototype)
    *   [1.2 Package Etiquette](#Package_Etiquette)
    *   [1.3 Package Naming](#Package_Naming)
    *   [1.4 Directories](#Directories)
    *   [1.5 Makepkg Duties](#Makepkg_Duties)
    *   [1.6 Architectures](#Architectures)
    *   [1.7 Licenses](#Licenses)
    *   [1.8 Submitting Packages to the AUR](#Submitting_Packages_to_the_AUR)
*   [2 Dodatna uputstva](#Dodatna_uputstva)
    *   [2.1 VCS (SVN, GIT, HG, etc) Packages](#VCS_(SVN,_GIT,_HG,_etc)_Packages)
    *   [2.2 Eclipse Plugin Packages](#Eclipse_Plugin_Packages)
    *   [2.3 Gnome Paketi](#Gnome_Paketi)
    *   [2.4 Haskell Paketi](#Haskell_Paketi)
    *   [2.5 Java Paketi](#Java_Paketi)
    *   [2.6 Kernel Module Paketi](#Kernel_Module_Paketi)
    *   [2.7 Lisp Paketi](#Lisp_Paketi)
    *   [2.8 OCaml Paketi](#OCaml_Paketi)
    *   [2.9 Perl Paketi](#Perl_Paketi)
    *   [2.10 Python Paketi](#Python_Paketi)
    *   [2.11 Ruby Gem Paketi](#Ruby_Gem_Paketi)
    *   [2.12 Wine Paketi](#Wine_Paketi)
    *   [2.13 MinGW Paketi](#MinGW_Paketi)

## Packaging Standards

**The submitted PKGBUILDs must not build applications already in any of the official binary repositories under any circumstances. Exception to this strict rule may only be packages having extra features enabled and/or patches in comparison to the official ones. In such an occasion, the pkgname array should be different.**

When building packages for Arch Linux, **adhere to the package guidelines** below, especially if the intention is to **contribute** a new package to Arch Linux. You should also see the [PKGBUILD](https://archlinux.org/pacman/PKGBUILD.5.html) and [makepkg](https://archlinux.org/pacman/makepkg.8.html) manpages.

#### PKGBUILD Prototype

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
md5sums=() #generate with 'makepkg -g'

build() {
  cd "$srcdir/$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  make DESTDIR="$pkgdir/" install
}

```

Other prototypes are found in /usr/share/pacman from the pacman and abs packages.

#### Package Etiquette

*   Packages should **never** be installed to `/usr/local`
*   **Do not introduce new variables** into `PKGBUILD` build scripts, unless the package cannot be built without doing so, as these could possibly **conflict** with variables used in makepkg itself. If a new variable is absolutely required, **prefix the variable name with an underscore** (`_`), e.g. `_customvariable=` 

    The AUR cannot detect the use of custom variables and so cannot use them in substitutions. This can most often be seen in the source array e.g.

     `http://downloads.sourceforge.net/directxwine/$patchname.$patchver.diff.bz2` 

    Such a situation defeats the effective functionality of the AUR.

*   **Avoid** using `/usr/libexec/` for anything. Use `/usr/lib/${pkgname}/` instead.
*   The `packager` field from the package meta file can be **customized** by the package builder by modifying the appropriate option in the `/etc/makepkg.conf` file, or alternatively override it by creating ~/.makepkg.conf
*   All important messages should be echoed during install using an **.install file**. For example, if a package needs extra setup to work, directions should be included.
*   Any **optional dependencies** that aren't needed to run the package or have it generally function shouldn't be included; instead the information should be added to the **optdepends** array:
    ```
    optdepends=('cups: printing support'
                'sane: scanners support'
                'libgphoto2: digital cameras support'
                'alsa-lib: sound support'
                'giflib: GIF images support'
                'libjpeg: JPEG images support'
                'libpng: PNG images support')

    ```

    The above example is taken from the **wine** package in <tt>extra</tt>. The optdepends information is automatically printed out on installation/upgrade so one should **not** keep this kind of information in .install files.

*   When creating a **package description** for a package, do not include the package name in a self-referencing way. For example, "Nedit is a text editor for X11" could be simplified to "A text editor for X11". Also try to keep the descriptions to ~80 characters or less.
*   Try to keep the **line length** in the PKGBUILD below ~100 characters.
*   Where possible, **remove empty lines** from the `PKGBUILD` (`provides`, `replaces`, etc.)
*   It is common practice to **preserve the order** of the `PKGBUILD` fields as shown above. However, this is not mandatory, as the only requirement in this context is **correct bash syntax**.

#### Package Naming

*   Package names should consist of **alphanumeric characters only**; all letters should be **lowercase**.
*   Package versions **should be the same as the version released by the author**. Versions can include letters if need be (eg, nmap's version is 2.54BETA32). **Version tags may not include hyphens!** Letters, numbers, and periods only.
*   Package releases are **specific to Arch Linux packages**. These allow users to differentiate between newer and older package builds. When a new package version is first released, the **release count starts at 1**. Then as fixes and optimizations are made, the package will be **re-released** to the Arch Linux public and the **release number will increment**. When a new version comes out, the release count resets to 1. Package release tags follow the **same naming restrictions as version tags**.

#### Directories

*   **Configuration files** should be placed in the `/etc` directory. If there's more than one configuration file, it's customary to **use a subdirectory** in order to keep the `/etc` area as clean as possible. Use `/etc/{pkgname}/` where `{pkgname}` is the name of the package (or a suitable alternative, eg, apache uses `/etc/httpd/`).
*   Package files should follow these **general directory guidelines**:

| `/etc` | 

**System-essential** configuration files

 |
| `/usr/bin` | Application binaries |
| `/usr/sbin` | System binaries |
| `/usr/lib` | Libraries |
| `/usr/include` | Header files |
| `/usr/lib/{pkg}` | Modules, plugins, etc. |
| `/usr/share/doc/{pkg}` | Application documentation |
| `/usr/share/info` | GNU Info system files |
| `/usr/share/man` | Manpages |
| `/usr/share/{pkg}` | Application data |
| `/var/lib/{pkg}` | Persistent application storage |
| `/etc/{pkg}` | Configuration files for `{pkg}` |
| `/opt/{pkg}` | 

Large self-contained packages such as Java, etc.

 |

*   Package should not contain following directories:
    *   /dev
    *   /home
    *   /srv
    *   /media
    *   /mnt
    *   /proc
    *   /root
    *   /selinux
    *   /sys
    *   /tmp
    *   /var/tmp

#### [Makepkg](/index.php/Makepkg "Makepkg") Duties

When makepkg is used to build a package, it does the following automatically:

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

#### Architectures

The <tt>arch</tt> array should contain <tt>'i686'</tt> and/or <tt>'x86_64'</tt> depending on which architectures it can be built on. You can also use <tt>'any'</tt> for architecture independent packages.

#### [Licenses](/index.php/Licenses "Licenses")

The license array is being implemented in the official repos, and it **should** be used in your packages as well. Use it as follows:

*   A licenses package has been created in [core] that stores common licenses in /usr/share/licenses/common ie. /usr/share/licenses/common/GPL. If a package is licensed under one of these licenses, the licenses variable will be set to the directory name e.g. license=('GPL')
*   If the appropriate license is not included in the official licenses package, several things must be done:
    1.  The license file(s) should be included in /usr/share/licenses/$pkgname/ e.g. /usr/share/licenses/dibfoo/LICENSE. One good way to do this is by using: `install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"` 
    2.  If the source tarball does NOT contain the license details and the license is only displayed on a website for example, then copy the license to a file and include it. Remember to call it something appropriate too.
    3.  Add 'custom' to the licenses array. Optionally, you can replace 'custom' with 'custom:"name of license"'.
*   Once a licenses is used in two or more packages in an official repo, including [community], it becomes common
*   The MIT, BSD, zlib/libpng and Python licenses are special cases and cannot be included in the 'common' licenses pkg. For the sake of the license variable, it's treated like a common license (license=('BSD'), license=('MIT'), license=('ZLIB') or license=('Python')) but for the sake of the filesystem, it's a custom license, because each one has its own copyright line. Each MIT, BSD, zlib/libpng or Python licensed package should have its unique license stored in /usr/share/licenses/$pkgname/.
*   Some packages may not be covered by a single license. In these cases multiple entries may be made in the license array e.g. license=("GPL" "custom:some commercial license"). For the majority of packages these licenses apply in different cases, as opposed to applying at the same time. When pacman gets the ability to filter on licenses (so you can say, "I only want GPL and BSD licensed software") dual (or more) licenses will be treated by pacman using OR, rather than AND logic, thus pacman will consider the above example as GPL licensed software, regardless of the other licenses listed.
*   The (L)GPL has many versions and permutations of those versions. For (L)GPL software, the convention is:
    *   (L)GPL - (L)GPLv2 or any later version
    *   (L)GPL2 - (L)GPL2 only
    *   (L)GPL3 - (L)GPL3 or any later version

#### Submitting Packages to the AUR

Note the following before submitting any packages to the AUR:

1.  The submitted PKGBUILDs **MUST NOT** build applications already in any of the official binary repositories under any circumstances. Exception to this strict rule may only be packages having extra features enabled and/or patches in compare to the official ones. In such an occasion the pkgname array should be different to express that difference. eg. A GNU screen PKGBUILD submitted containing the sidebar patch, could be named screen-sidebar etc. Additionally the **provides=('screen')** PKGBUILD array should be used in order to avoid conflicts with the official package.
2.  To ensure the security of pkgs submitted to the AUR please **ensure** that you have correctly filled the `md5sum` field. The `md5sum`'s can be generated using the `makepkg -g` command.
3.  Please **add a comment line** to the top of the `PKGBUILD` file that follows this format. Remember to disguise your email to protect against spam: `# Maintainer: Your Name <address at domain dot com>` 

    If you are assuming the role of maintainer for an existing PKGBUILD, add your name to the top as described above and change the title of the previous Maintainer(s) to Contributor:

    ```
    # Maintainer: Your Name <address at domain dot com>
    # Contributor: Previous Name <address at domain dot com>
    ```

4.  Verify the package **dependencies** (eg, run `ldd` on dynamic executables, check tools required by scripts, etc). The TU team **strongly** recommend the use of the `namcap` utility, written by [Jason Chu](https://www.archlinux.org/fellows/#jason), to analyze the sanity of packages. `namcap` will warn you about bad permissions, missing dependencies, un-needed dependencies, and other common mistakes. You can install the `namcap` package with `pacman`. Remember `namcap` can be used to check both pkg.tar.gz files and PKGBUILDs
5.  **Dependencies** are the most common packaging error. Namcap can help detect them, but it is not always correct. Verify dependencies by looking at source documentation and the program website.
6.  **Don't use <tt>replaces</tt>** in a PKGBUILD unless the package is to be renamed, for example when *Ethereal* became *Wireshark*. If the package is an alternate version of an already existing package, use <tt>conflicts</tt> (and <tt>provides</tt> if that package is required by others). The main difference is: after syncing (-Sy) pacman immediately wants to replace an installed, 'offending' package upon encountering a package with the matching <tt>replaces</tt> anywhere in its repositories; <tt>conflicts</tt> on the other hand is only evaluated when actually installing the package, which is usually the desired behavior because it is less invasive.
7.  All files uploaded to the AUR should be contained in a **compressed tar file** containing a directory with the **`PKGBUILD`** and **additional build files** (patches, install, ...) in it.
    ```
    foo/PKGBUILD
    foo/foo.install
    foo/foo_bar.diff
    foo/foo.rc.conf
    ```

    The archive name should contain the name of the package e.g. foo.tar.gz.

    One can easily build a tarball containing all the required files by using <tt>makepkg --source</tt>. This makes a tarball named <tt>$pkgname-$pkgver-$pkgrel.src.tar.gz</tt>, which can then be uploaded to the AUR.

    The tarball **should not** contain the binary tarball created by makepkg, nor should it contain the filelist

## Dodatna uputstva

Be sure to read the above guidelines first - important points are listed on this page that will not be repeated in the following guideline pages. These specific guidelines are intended as an addition to the standards listed on this page.

#### VCS (SVN, GIT, HG, etc) Packages

Please see the [Arch VCS PKGBUILD guidelines](/index.php/Arch_CVS_%26_SVN_PKGBUILD_guidelines "Arch CVS & SVN PKGBUILD guidelines")

#### Eclipse Plugin Packages

Please see the [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines")

#### Gnome Paketi

Please see the [GNOME package guidelines](/index.php/GNOME_package_guidelines "GNOME package guidelines")

#### Haskell Paketi

Please see the [Haskell package guidelines](/index.php/Haskell_package_guidelines "Haskell package guidelines")

#### Java Paketi

Please see the [Java package guidelines](/index.php/Java_package_guidelines "Java package guidelines")

#### Kernel Module Paketi

Please see the [Kernel module package guidelines](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines")

#### Lisp Paketi

Please see the [Lisp package guidelines](/index.php/Lisp_package_guidelines "Lisp package guidelines")

#### OCaml Paketi

Please see the [OCaml package guidelines](/index.php/OCaml_package_guidelines "OCaml package guidelines")

#### Perl Paketi

Please see the [Perl package guidelines](/index.php/Perl_package_guidelines "Perl package guidelines")

#### Python Paketi

Please see the [Python package guidelines](/index.php/Python_package_guidelines "Python package guidelines")

#### Ruby Gem Paketi

Please see the [Ruby Gem package guidelines](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines")

#### Wine Paketi

Please see the [Arch wine PKGBUILD guidelines](/index.php/Arch_wine_PKGBUILD_guidelines "Arch wine PKGBUILD guidelines")

#### MinGW Paketi

Please see the [MinGW PKGBUILD guidelines](/index.php/MinGW_PKGBUILD_guidelines "MinGW PKGBUILD guidelines")