# PKGBUILD

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [Arch packaging standards](/index.php/Arch_packaging_standards "Arch packaging standards")
*   [Arch Build System](/index.php/Arch_Build_System "Arch Build System")
*   [Creating packages](/index.php/Creating_packages "Creating packages")
*   [Category:Package development](/index.php/Category:Package_development "Category:Package development")
*   [Pacman tips](/index.php/Pacman_tips "Pacman tips")
*   [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository")
*   [makepkg](/index.php/Makepkg "Makepkg")
*   [pacman](/index.php/Pacman "Pacman")

This article discusses variables definable by the maintainer in a PKGBUILD. For information on the PKGBUILD functions and creating packages in general, refer to [Creating packages](/index.php/Creating_packages "Creating packages"). Also read `man PKGBUILD`.

A PKGBUILD is a shell script containing the build information required by [Arch Linux](/index.php/Arch_Linux "Arch Linux") packages.

Packages in Arch Linux are built using the [makepkg](/index.php/Makepkg "Makepkg") utility. When _makepkg_ is run, it searches for a `PKGBUILD` file in the current directory and follows the instructions therein to either compile or otherwise acquire the files to build a package archive (`_pkgname_.pkg.tar.xz`). The resulting package contains binary files and installation instructions, readily installable with [pacman](/index.php/Pacman "Pacman").

Mandatory variables are `pkgname`, `pkgver`, `pkgrel`, and `arch`. `license` is not strictly necessary to build a package, but is recommended for any PKGBUILDs shared with others, as _makepkg_ will produce a warning if not present.

It is a common practice to define the variables in the PKGBUILD in same order as given here. However, this is not mandatory, as long as correct [Bash](/index.php/Bash "Bash") syntax is used.

## Contents

*   [1 Package name](#Package_name)
    *   [1.1 pkgbase](#pkgbase)
    *   [1.2 pkgname](#pkgname)
*   [2 Version](#Version)
    *   [2.1 pkgver](#pkgver)
    *   [2.2 pkgrel](#pkgrel)
    *   [2.3 epoch](#epoch)
*   [3 Generic](#Generic)
    *   [3.1 pkgdesc](#pkgdesc)
    *   [3.2 arch](#arch)
    *   [3.3 url](#url)
    *   [3.4 license](#license)
    *   [3.5 groups](#groups)
*   [4 Dependencies](#Dependencies)
    *   [4.1 depends](#depends)
    *   [4.2 optdepends](#optdepends)
    *   [4.3 makedepends](#makedepends)
    *   [4.4 checkdepends](#checkdepends)
*   [5 Package relations](#Package_relations)
    *   [5.1 provides](#provides)
    *   [5.2 conflicts](#conflicts)
    *   [5.3 replaces](#replaces)
*   [6 Others](#Others)
    *   [6.1 backup](#backup)
    *   [6.2 options](#options)
    *   [6.3 install](#install)
    *   [6.4 changelog](#changelog)
*   [7 Sources](#Sources)
    *   [7.1 source](#source)
    *   [7.2 noextract](#noextract)
    *   [7.3 validpgpkeys](#validpgpkeys)
*   [8 Integrity](#Integrity)
    *   [8.1 md5sums](#md5sums)
    *   [8.2 sha1sums](#sha1sums)
    *   [8.3 sha256sums](#sha256sums)
    *   [8.4 sha224sums, sha384sums, sha512sums](#sha224sums.2C_sha384sums.2C_sha512sums)
*   [9 See also](#See_also)

## Package name

### pkgbase

An optional global directive is available when building a split package. `pkgbase` is used to refer to the group of packages in the output of _makepkg_ and in the naming of source-only tarballs. If not specified, the first element in the `pkgname` array is used. The variable is not allowed to begin with a hyphen. All values for split packages default to the global ones given in the PKGBUILD. Everything, except [#makedepends](#makedepends), [#Sources](#Sources), and [#Integrity](#Integrity) variables can be overridden within each split package's `package()` function.

### pkgname

The name(s) of the package(s). This should consist of lowercase alphanumerics and any of the following characters: `@`, `.`, `_`, `+`, `-` (at symbol, dot, underscore, plus, hyphen). Names are not allowed to start with hyphens. For the sake of consistency, `pkgname` should match the name of the source tarball of the software: for instance, if the software is in `foobar-2.5.tar.gz`, use `pkgname=foobar`. The name of the directory containing the PKGBUILD should also match the `pkgname`.

Split packages should be defined as an array, e.g. `pkgname=('foo' 'bar')`.

## Version

### pkgver

The version of the package. This should be the same as the version released by the author of the package. It can contain letters, numbers, periods and underscores, but **not** a hyphen (`-`). If the author of the software uses one, replace it with an underscore (`_`). If the `pkgver` variable is used later in the PKGBUILD, then the underscore can easily be substituted for a hyphen, e.g. `source=("$pkgname-${pkgver//_/-}.tar.gz")`.

**Note:** If upstream uses a timestamp versioning such as `30102014`, ensure to use the reversed date, i.e. `20141030` ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601 "wikipedia:ISO 8601") format). Otherwise it will not appear as a newer version.

**Tip:** [makepkg](/index.php/Makepkg "Makepkg") can automatically [update](http://allanmcrae.com/2013/04/pacman-4-1-released/) this variable by defining a `pkgver()` function in the PKGBUILD. See [VCS package guidelines#The pkgver() function](/index.php/VCS_package_guidelines#The_pkgver.28.29_function "VCS package guidelines") for details

### pkgrel

The release number. This is usually a positive integer number that allows to differentiate between consecutive builds of the same version of a package. As fixes and additional features are added to the PKGBUILD that influence the resulting package, the `pkgrel` should be incremented by 1\. When a new version of the software is released, this value must be reset to 1\. In exceptional cases other formats can be found in use, such as _major.minor_.

### epoch

**Warning:** `epoch` should only be used when absolutely required to do so.

Used to force the package to be seen as newer than any previous version with a lower epoch. This value is required to be a positive integer; the default is 0\. It is used when the version numbering scheme of a package changes (or is alphanumeric), breaking normal version comparison logic. For example:

```
pkgver=5.13
pkgrel=2
epoch=1
```

 `1:5.13-2` 

See [pacman(8)](https://www.archlinux.org/pacman/pacman.8.html) for more information on version comparisons.

## Generic

### pkgdesc

The description of the package. This is recommended to be 80 characters or less and should not include the package name in a self-referencing way, unless the application name differs from the package name. For example, use `pkgdesc="Text editor for X11"` instead of `pkgdesc="Nedit is a text editor for X11"`.

Also it is important to use keywords wisely to increase the chances of appearing in relevant search queries.

### arch

An array of architectures that the PKGBUILD is intended to build and work on. Arch officially supports only `i686` and `x86_64`, but projects like [Arch Linux ARM](http://archlinuxarm.org/) provide support for other architectures such as `arm` for armv5, `armv6h` for armv6 hardfloat, `armv7h` for armv7 hardfloat, and `aarch64` for armv8 64bit.

If a package is architecture-independent in its compiled state (shell scripts, fonts, themes, many types of extensions, etc.) then use `arch=('any')`. Please note that, as this is intended for packages that can be built once and used on any architecture, it will cause the package to be labeled `-any` as opposed to `-i686`, `-x86_64`, etc.

If instead a package can be compiled for any architecture, but is architecture-specific once compiled, specify all architectures officially supported by Arch, i.e. `arch=('i686' 'x86_64')`.

The target architecture can be accessed with the variable `$CARCH` during a build.

### url

The URL of the official site of the software being packaged.

### license

The license under which the software is distributed. The [licenses](https://www.archlinux.org/packages/?name=licenses) package from the [official repositories](/index.php/Official_repositories "Official repositories") contains many commonly used licenses, which are installed to `/usr/share/licenses/common`. If a package is licensed under one of these licenses, the value should be set to the directory name, e.g. `license=('GPL')`. If the appropriate license is not included, several things must be done:

1.  Add `custom` to the `license` array. Optionally, you can replace `custom` with `custom:_name of license_`. Once a license is used in two or more packages in an official repository (including `[community]`), it becomes a part of the [licenses](https://www.archlinux.org/packages/?name=licenses) package.
2.  Install the license in: `/usr/share/licenses/_pkgname_/`, e.g. `/usr/share/licenses/foobar/LICENSE`.
3.  If the license is only found in a website, then you need to separately include it in the package.

*   The [BSD](https://en.wikipedia.org/wiki/BSD_License "wikipedia:BSD License"), [MIT](https://en.wikipedia.org/wiki/MIT_License "wikipedia:MIT License"), [zlib/png](https://en.wikipedia.org/wiki/ZLIB_license "wikipedia:ZLIB license") and [Python](https://en.wikipedia.org/wiki/Python_License "wikipedia:Python License") licenses are special cases and could not be included in the [licenses](https://www.archlinux.org/packages/?name=licenses) package. For the sake of the `license` array, it is treated as a common license (`license=('BSD')`, `license=('MIT')`, `license=('ZLIB')` and `license=('Python')`), but technically each one is a custom license, because each one has its own copyright line. Any packages licensed under these four should have its own unique license stored in `/usr/share/licenses/_pkgname_`. Some packages may not be covered by a single license. In these cases, multiple entries may be made in the `license` array, e.g. `license=('GPL' 'custom:_name of license'_)`.
*   (L)GPL has many versions and permutations of those versions. For (L)GPL software, the convention is:
    *   (L)GPL — (L)GPLv2 or any later version
    *   (L)GPL2 — (L)GPL2 only
    *   (L)GPL3 — (L)GPL3 or any later version
*   If after researching the issue no license can be determined, [PKGBUILD.proto](https://projects.archlinux.org/pacman.git/tree/proto/PKGBUILD.proto) suggests using `unknown`. However, upstream should be contacted about the conditions under which the software is (and is not) available.

**Tip:** Some software authors do not provide separate license file and describe distribution rules in section of common `ReadMe.txt`. This information can be extracted to a separate file during `build()` with something like `sed -n '/**This software**/,/ **thereof.**/p' ReadMe.txt > LICENSE`

### groups

The [group](/index.php/Pacman#Installing_package_groups "Pacman") the package belongs in. For instance, when installing the [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/) package, it installs all packages belonging in that group.

## Dependencies

**Note:** Additional architecture-specific arrays can be used by appending an underscore and the architecture name, e.g. `depends_x86_64=()`, `optdepends_x86_64=()`.

### depends

An array of packages that must be installed before the software can be run. Version restrictions can be specified with comparison operators, e.g. `depends=('foobar>=1.8.0')`; if multiple restrictions are needed, the dependency can be repeated for each, e.g. `depends=('foobar>=1.8.0' 'foobar<2.0.0')`.

Dependencies that are provided by other dependencies do not need to be listed. For instance, if a package _foo_ depends on both _bar_ and _baz_, and the _bar_ package depends in turn on _baz_ too, _baz_ does not need to be included in _foo'_s `depends` array.

### optdepends

An array of packages that are not needed for the software to function, but provide additional features. This may imply that not all executables provided by a package will function without the respective optdepends.[[1]](https://lists.archlinux.org/pipermail/arch-general/2014-December/038124.html) If the software works on multiple alternative dependencies, all of them can be listed here, instead of the `depends` array.

A short description of the extra functionality each optdepend provides should also be noted:

```
optdepends=('cups: printing support'
            'sane: scanners support'
            'libgphoto2: digital cameras support'
            'alsa-lib: sound support'
            'giflib: GIF images support'
            'libjpeg: JPEG images support'
            'libpng: PNG images support')

```

### makedepends

An array of packages that are **only** required to build the software. The minimum dependency version can be specified in the same format as in the `depends` array.

**Tip:** The following can be used to see if a particular package is either in the [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) group or pulled in by a members of the group:

```
$ pacman -Si $(pactree -rl _package_) 2>/dev/null | grep -q "^Groups *:.*base-devel"

```

**Note:** The group [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) is assumed to be already installed when building with _makepkg_. Members of this group **should not** be included in `makedepends` array.

### checkdepends

An array of packages that the software depends on to run its test suite, but are not needed at runtime. Packages in this list follow the same format as `depends`. These dependencies are only considered when the [check()](/index.php/Creating_packages#check.28.29 "Creating packages") function is present and is to be run by makepkg.

**Note:** The group [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) is assumed to be already installed when building with _makepkg_. Members of this group **should not** be included in `checkdepends` array.

## Package relations

**Note:** Additional architecture-specific arrays can be used by appending an underscore and the architecture name, e.g. `provides_x86_64=()`, `conflicts_x86_64=()`.

### provides

An array of additional packages that the software provides the features of (or a virtual package such as `cron` or `sh`). Packages providing the same item can be installed side-by-side, unless at least one of them uses a `conflicts` array.

**Warning:** A version that the package provides should be mentioned (`pkgver` and perhaps the `pkgrel`), if packages needing the software may require one. For instance, a modified _qt_ package version 3.3.8, named _qt-foobar_, should use `provides=('qt=3.3.8')`; using `provides=('qt')` would cause the dependencies that require a specific version of _qt_ to fail. Do not add `pkgname` to the `provides` array, as it is done automatically.

### conflicts

An array of packages that conflict with, or cause problems with the package, if installed. All these packages and packages providing this item will need to be removed. The version properties of the conflicting packages can also be specified in the same format as the `depends` array.

### replaces

An array of obsolete packages that are replaced by the package, e.g. [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk) uses `replaces=('wireshark')`. When syncing, _pacman_ will immediately replace an installed package upon encountering another package with the matching `replaces` in the repositories. If providing an alternate version of an already existing package or uploading to the [AUR](/index.php/AUR "AUR"), use the `conflicts` and `provides` arrays, which are only evaluated when actually installing the conflicting package.

## Others

### backup

An array of files that can contain user-made changes and should be preserved during upgrade or removal of a package, primarily intended for configuration files in `/etc`.

Files in this array should use **relative** paths without the leading slash (`/`) (e.g. `etc/pacman.conf`, instead of `/etc/pacman.conf`).

When updating, new versions may be saved as `file.pacnew` to avoid overwriting a file which already exists and was previously modified by the user. Similarly, when the package is removed, user-modified files will be preserved as `file.pacsave` unless the package was removed with the `pacman -Rn` command.

See also [Pacnew and Pacsave files](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files").

### options

This array allows overriding some of the default behavior of _makepkg_, defined in `/etc/makepkg.conf`. To set an option, include the name in the array. To reverse the default behavior, place an **`!`** at the front.

The full list of the available options can be found in [PKGBUILD(5)](https://www.archlinux.org/pacman/PKGBUILD.5.html).

### install

The name of the `.install` script to be included in the package. This should be the same as `pkgname`. _pacman_ has the ability to store and execute a package-specific script when it installs, removes or upgrades a package. The script contains the following functions which run at different times:

*   `pre_install` — The script is run right before files are extracted. One argument is passed: new package version.
*   `post_install` — The script is run right after files are extracted. One argument is passed: new package version.
*   `pre_upgrade` — The script is run right before files are extracted. Two arguments are passed in the following order: new package version, old package version.
*   `post_upgrade` — The script is run right after files are extracted. Two arguments are passed in the following order: new package version, old package version.
*   `pre_remove` — The script is run right before files are removed. One argument is passed: old package version.
*   `post_remove` — The script is run right after files are removed. One argument is passed: old package version.

Each function is run [chrooted](/index.php/Chroot "Chroot") inside the _pacman_ install directory. See [this thread](https://bbs.archlinux.org/viewtopic.php?pid=913891).

**Tip:** A prototype `.install` is provided at [/usr/share/pacman/proto.install](https://projects.archlinux.org/pacman.git/plain/proto/proto.install).

### changelog

The name of the package changelog. To view changelogs for installed packages (that have this file):

```
$ pacman -Qc _pkgname_

```

## Sources

### source

**Note:** Additional architecture-specific arrays can be added by appending an underscore and the architecture name, e.g. `source_x86_64=()`. There must be a corresponding integrity array with checksums, e.g. `sha256sums_x86_64=()`.

An array of files needed to build the package. It must contain the location of the software source, which in most cases is a full HTTP or FTP URL. The previously set variables `pkgname` and `pkgver` can be used effectively here (e.g. `source=("https://example.com/$pkgname-$pkgver.tar.gz")`).

Files can also be supplied directly in the location of the `PKGBUILD` and added to this array. These paths are resolved relative to the directory of the `PKGBUILD`. Before the actual build process is started, all of the files referenced in this array will be downloaded or checked for existence, and _makepkg_ will not proceed, if any are missing.

**Note:** _.install_ files should not be included.

**Tip:** An alternative source name for the downloaded file can be specified with the syntax `source=('_filename_::_fileuri_')`: `source=("project_name::hg+https://googlefontdirectory.googlecode.com/hg/")` 

Files in the source array with extensions _.sig_, _.sign_, or _.asc_ are recognized by _makepkg_ as PGP signatures and will be automatically used to verify the integrity of the corresponding source file.

### noextract

An array of files listed under `source`, which should not be extracted from their archive format by _makepkg_. This can be used with archives that cannot be handled by `/usr/bin/bsdtar` or those that need to be installed as-is. If an alternative unarchiving tool is used (e.g. [lrzip](https://www.archlinux.org/packages/?name=lrzip)), it should be added in the `makedepends` array and the first line of the [prepare()](/index.php/Creating_packages#prepare.28.29 "Creating packages") function should extract the source archive manually; for example:

```
prepare() {
  lrzip -d _source_.tar.lrz
}

```

Note that while the `source` array accepts URLs, `noextract` is **just** the file name portion:

```
source=("http://foo.org/bar/foobar.tar.xz")
noextract=('foobar.tar.xz')

```

To extract _nothing_, you can do something like this (taken from [firefox-i18n's PKGBUILD](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/firefox-i18n#n123)):

```
noextract=("${source[@]%%::*}")

```

### validpgpkeys

An array of PGP fingerprints. If used, _makepkg_ will only accept signatures from the keys listed here and will ignore the trust values from the keyring. If the source file was signed with a subkey, _makepkg_ will still use the primary key for comparison.

Only full fingerprints are accepted. They must be uppercase and must not contain whitespace characters.

**Note:** You can use `gpg --list-keys --fingerprint <KEYID>` to find out the fingerprint of the appropriate key.

## Integrity

These variables are arrays whose items are checksum strings that will be used to verify the integrity of the respective files in the [source](#source) array. You can also insert `SKIP` for a particular file, and its checksum will not be tested.

Checksums are intended to verify the _integrity_ of the downloaded files, **not** their _authenticity_: for this reason, even though the MD5 algorithm is known to have considerable [vulnerabilities](https://en.wikipedia.org/wiki/MD5#Security "wikipedia:MD5") when used for other purposes, it is recommended for file integrity as a faster alternative to SHA-2 hashes, especially when large files are present in the `source` array. If possible, however, always test the authenticity of the files by adding their signatures to the `source` array: in this case you will also be able to safely skip their checksum verification altogether, as described above.

The values for these variables can be auto-generated by [makepkg](/index.php/Makepkg "Makepkg")'s `-g`/`--geninteg` option, then commonly appended with `makepkg -g >> PKGBUILD`. The `updpkgsums` command is able to update the variables wherever they are in the PKGBUILD. Both tools will use the variable that is already set in the PKGBUILD, or fall back to `md5sums` if none is set.

The file integrity checks to use can be set up with the `INTEGRITY_CHECK` option in `/etc/makepkg.conf`. See [makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html).

### md5sums

An array of 128-bit [MD5](https://en.wikipedia.org/wiki/MD5 "wikipedia:MD5") checksums of the files listed in the `source` array.

### sha1sums

An array of 160-bit [SHA-1](https://en.wikipedia.org/wiki/SHA-1 "wikipedia:SHA-1") checksums of the files listed in the `source` array.

### sha256sums

An array of [SHA-2](https://en.wikipedia.org/wiki/SHA-2 "wikipedia:SHA-2") checksums with digest size of 256 bits.

### sha224sums, sha384sums, sha512sums

An array of SHA-2 checksums with digest sizes 224, 384, and 512 bits, respectively. These are less common alternatives to `sha256sums`.

## See also

*   [PKGBUILD(5) Manual Page](https://www.archlinux.org/pacman/PKGBUILD.5.html)
*   [Example PKGBUILD file](http://ix.io/kXu)

Retrieved from "[https://wiki.archlinux.org/index.php?title=PKGBUILD&oldid=410746](https://wiki.archlinux.org/index.php?title=PKGBUILD&oldid=410746)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Package development](/index.php/Category:Package_development "Category:Package development")