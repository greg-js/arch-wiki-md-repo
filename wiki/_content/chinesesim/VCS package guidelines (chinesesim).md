**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

[Version control systems](https://en.wikipedia.org/wiki/Revision_control "wikipedia:Revision control") can be used for retrieval of source code for both usual statically versioned packages and latest (trunk) version of packages. This article covers both cases.

## Contents

*   [1 Prototypes](#Prototypes)
*   [2 Guidelines](#Guidelines)
    *   [2.1 VCS sources](#VCS_sources)
    *   [2.2 The pkgver() function](#The_pkgver.28.29_function)
        *   [2.2.1 Git](#Git)
        *   [2.2.2 Subversion](#Subversion)
        *   [2.2.3 Mercurial](#Mercurial)
        *   [2.2.4 Bazaar](#Bazaar)
        *   [2.2.5 Fallback](#Fallback)
*   [3 Tips](#Tips)
    *   [3.1 A sample Git PKGBUILD for pacman 4.1](#A_sample_Git_PKGBUILD_for_pacman_4.1)
    *   [3.2 Removing VCS leftovers](#Removing_VCS_leftovers)
    *   [3.3 SVN packages that try to get their revision number](#SVN_packages_that_try_to_get_their_revision_number)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Bazaar limitation](#Bazaar_limitation)

## Prototypes

The [ABS](/index.php/ABS "ABS") package provides prototypes for [cvs](/index.php/Cvs "Cvs"), [svn](/index.php/Svn "Svn"), [git](/index.php/Git "Git"), [mercurial](/index.php/Mercurial "Mercurial"), and [darcs](https://en.wikipedia.org/wiki/darcs "wikipedia:darcs") [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"). When [abs](https://www.archlinux.org/packages/?name=abs) is installed, you can find them in `/usr/share/pacman`. Latest versions can be found in the [prototypes directory in the ABS Git repository](https://projects.archlinux.org/abs.git/tree/prototypes).

## Guidelines

*   Suffix `pkgname` with `-cvs`, `-svn`, `-hg`, `-darcs`, `-bzr`, `-git` etc. unless the package fetches a specific release.

*   If the resulting package is different after changing the dependencies, URL, sources, etc. increasing the `pkgrel` is mandatory. Touching the `pkgver` isn't.

*   `--holdver` can be used to prevent [makepkg](/index.php/Makepkg "Makepkg") from updating the `pkgver` (see: [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html))

*   Include what the package conflicts with and provides (e.g. for [fluxbox-git](https://aur.archlinux.org/packages/fluxbox-git/): `conflicts=('fluxbox')` and `provides=('fluxbox')`).

*   `replaces=()` generally causes unnecessary problems and should be avoided.

*   When using the cvsroot, use `anonymous:@` rather than `anonymous@` to avoid having to enter a blank password or `anonymous:password@`, if one is required.

*   Include the appropriate VCS tool in `makedepends` ([cvs](https://www.archlinux.org/packages/?name=cvs), [subversion](https://www.archlinux.org/packages/?name=subversion), [git](https://www.archlinux.org/packages/?name=git), ...).

### VCS sources

**Note:** Pacman 4.1 supports the following VCS sources: `bzr`, `git`, `hg` and `svn`. See the `fragment` section of [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) or [PKGBUILD(5)](https://www.archlinux.org/pacman/PKGBUILD.5.html) for a list of supported VCS.

Starting with [pacman](https://www.archlinux.org/packages/?name=pacman) 4.1, the VCS sources should be specified in the `source=()` array and will be treated like any other source. `makepkg` will clone/checkout/branch the repo into `$SRCDEST` (same as `$startdir` if not set in [makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html)) and copy it to `$srcdir` (in a specific way to each VCS). The local repo is left untouched, thus invalidating the need for a `-build` directory.

The general format of a VCS `source=()` array is:

```
source=('[folder::][vcs+]url[#fragment]')

```

*   `folder` (optional) is used to change the default repo name to something more relevant (e.g. than `trunk`) or to preserve the previous sources
*   `vcs+` is needed for URLs that do not reflect the VCS type, e.g. `git+[http://some_repo](http://some_repo)`.
*   `url` is the URL to the distant or local repo
*   `#fragment` (optional) is needed to pull a specific branch or commit

An example Git source array:

```
source=('project_name::git+[http://project_url#branch=project_branch'](http://project_url#branch=project_branch'))

```

### The pkgver() function

The `pkgver` autobump is now achieved via a dedicated `pkgver()` function. This allows for better control over the `pkgver`, and maintainers should favor a `pkgver` that makes sense. Following are some examples for several VCS.

#### Git

With tags:

```
pkgver() {
  cd "$srcdir"/local_repo
  git describe --always | sed 's|-|.|g'
}

```

Without tags:

```
pkgver() {
  cd "$srcdir"/local_repo
  echo "0.$(git rev-list --count HEAD).$(git describe --always)"
}

```

Using the last commit date:

```
pkgver() {
  cd "$srcdir"/local_repo
  git log -1 --format="%cd" --date=short | sed 's|-||g'
}

```

#### Subversion

```
pkgver() {
  cd "$SRCDEST"/local_repo
  svnversion |tr -d [A-z]
}

```

**Note:** The copy inside `$srcdir` is made using `svn export` which does not create working copies. Any `svn` related command has to be used in the local repo, hence `$SRCDEST`.

#### Mercurial

```
pkgver() {
  cd "$srcdir"/local_repo
  hg identify -ni | awk 'BEGIN{OFS=".";} {print $2,$1}'
}

```

#### Bazaar

```
pkgver() {
  cd "$srcdir"/local_repo
  bzr revno
}

```

#### Fallback

The following can be used in case no satisfactory `pkgver` can be extracted from the repo:

```
pkgver() {
  date +"%Y%m%d"
}

```

## Tips

### A sample Git PKGBUILD for pacman 4.1

```
# Maintainer: Dave Reisner <d@falconindy.com> 
# Contributor: William Giokas (KaiSforza) <1007380@gmail.com>

pkgname=expac-git
_gitname=expac
pkgver=0.0.0
pkgrel=1
pkgdesc="Pacman database extraction utility"
arch=('i686' 'x86_64')
url="[https://github.com/falconindy/expac](https://github.com/falconindy/expac)"
license=('MIT')
depends=('pacman')
makedepends=('git' 'perl')
conflicts=('expac')
provides=('expac')
# Here is the fun bit. Makepkg knows it's a git repo because the URL starts with 'git'
# it then knows to checkout the branch 'pacman41' upon cloning, expediating versioning:
#source=('git+[https://github.com/falconindy/expac.git'](https://github.com/falconindy/expac.git')
source=('[git://github.com/falconindy/expac.git'](git://github.com/falconindy/expac.git')
        'expac_icon.png')
# Because the sources are not static, skip Git checksum:
md5sums=('SKIP'
         '020c36e38466b68cbc7b3f93e2044b49')

pkgver() {
  cd "$srcdir/$_gitname"
  git describe --always | sed 's|-|.|g'
  # To give the total count of commits and the hash of the last one
  # (useful if you're making a repository with git packages so that they can have
  # sequential version numbers, else a "pacman -Syu" may not update the package):
  #echo "0.$(git rev-list --count $branch).$(git describe --always)"
  # Using the last commit date:
  #git log -1 --format="%cd" --date=short | sed 's|-||g'
}

build() {
  cd "$srcdir/$_gitname"
  make
}

package() {
  cd "$srcdir/$_gitname"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 "$srcdir/expac_icon.png" "$pkgdir/usr/share/pixmaps/expac.png"
}

```

### Removing VCS leftovers

To make sure that there are no VCS leftovers use the following at the end of the `package()` function (replacing `**.git**` with `.svn`, `.hg`, etc.):

```
find "$pkgdir" -type d -name "**.git**" -exec rm -r '{}' +

```

### SVN packages that try to get their revision number

If the build system for the program you are packaging calls `svnversion` or `svn info` to determine its revision number, you can add a `prepare()` function similar to this one to make it work:

```
prepare() {
  cp -a "$SRCDEST/$_svnmod/.svn" "$srcdir/$_svnmod/"
}

```

## Troubleshooting

### Bazaar limitation

Currently, bazaar URLs only work in the form of `[http://bazaar.launchpad.net/](http://bazaar.launchpad.net/)`, e.g.:

```
source=('project_name::bzr+[http://bazaar.launchpad.net/~project_team/project_path'](http://bazaar.launchpad.net/~project_team/project_path'))

```

Using any other `http://`, `https://` or `ssh://` URL (including `lp:project_name`) will prevent makepkg from updating the local repo.

The correct URL can be obtained with:

```
$ bzr config parent_location

```