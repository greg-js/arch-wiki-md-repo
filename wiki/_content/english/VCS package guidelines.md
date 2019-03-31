**[Package creation guidelines](/index.php/Arch_packaging_standards "Arch packaging standards")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Electron](/index.php/Electron_package_guidelines "Electron package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [R](/index.php/R_package_guidelines "R package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [Rust](/index.php/Rust_package_guidelines "Rust package guidelines") – <a class="mw-selflink selflink">VCS</a> – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

[Version control systems](https://en.wikipedia.org/wiki/Revision_control "wikipedia:Revision control") can be used for retrieval of source code for both usual statically versioned packages and latest (trunk) version of a development branch. This article covers both cases.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Prototypes](#Prototypes)
*   [2 Guidelines](#Guidelines)
    *   [2.1 VCS sources](#VCS_sources)
    *   [2.2 The pkgver() function](#The_pkgver()_function)
        *   [2.2.1 Git](#Git)
        *   [2.2.2 Subversion](#Subversion)
        *   [2.2.3 Mercurial](#Mercurial)
        *   [2.2.4 Bazaar](#Bazaar)
        *   [2.2.5 Fallback](#Fallback)
*   [3 Tips](#Tips)
    *   [3.1 Git Submodules](#Git_Submodules)

## Prototypes

Use only the PKGBUILD prototypes provided in the [pacman](https://www.archlinux.org/packages/?name=pacman) package (`PKGBUILD-split.proto`, `PKGBUILD-vcs.proto` and `PKGBUILD.proto` in `/usr/share/pacman`).

## Guidelines

*   Suffix `pkgname` with `-cvs`, `-svn`, `-hg`, `-darcs`, `-bzr`, `-git` etc. unless the package fetches a specific release.

*   If the resulting package is different after changing the dependencies, URL, sources, etc. increasing the `pkgrel` is mandatory. Touching the `pkgver` is not.

*   `--holdver` can be used to prevent [makepkg](/index.php/Makepkg "Makepkg") from updating the `pkgver` (see: [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html))

*   Include what the package conflicts with and provides (e.g. for [fluxbox-git](https://aur.archlinux.org/packages/fluxbox-git/): `conflicts=('fluxbox')` and `provides=('fluxbox')`).

*   `replaces=()` generally causes unnecessary problems and should be avoided.

*   When using the cvsroot, use `anonymous:@` rather than `anonymous@` to avoid having to enter a blank password or `anonymous:password@`, if one is required.

*   Include the appropriate VCS tool in `makedepends=()` ([cvs](https://www.archlinux.org/packages/?name=cvs), [subversion](https://www.archlinux.org/packages/?name=subversion), [git](https://www.archlinux.org/packages/?name=git), ...).

*   Because the sources are not static, skip the checksum in `md5sums=()` by adding `'SKIP'`.

### VCS sources

**Note:** Pacman 4.1 supports the following VCS sources: `bzr`, `git`, `hg` and `svn`. See the `fragment` section of [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) or [PKGBUILD(5)](https://www.archlinux.org/pacman/PKGBUILD.5.html) for a list of supported VCS.

Starting with [pacman](https://www.archlinux.org/packages/?name=pacman) 4.1, the VCS sources should be specified in the `source=()` array and will be treated like any other source. `makepkg` will clone/checkout/branch the repository into `$SRCDEST` (same as `$startdir` if not set in [makepkg.conf(5)](https://www.archlinux.org/pacman/makepkg.conf.5.html)) and copy it to `$srcdir` (in a specific way to each VCS). The local repository is left untouched, thus invalidating the need for a `-build` directory.

The general format of a VCS `source=()` array is:

```
source=('[folder::][vcs+]url[#fragment]')

```

*   `folder` (optional) is used to change the default repository name to something more relevant (e.g. than `trunk`) or to preserve the previous sources.
*   `vcs+` is needed for URLs that do not reflect the VCS type, e.g. `git+http://some_repo`.
*   `url` is the URL to the distant or local repository.
*   `#fragment` (optional) is needed to pull a specific branch or commit. See [PKGBUILD(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/PKGBUILD.5) for more information on the fragments available for each VCS.

An example Git source array:

```
source=('project_name::git+https://project_url#branch=project_branch')

```

### The pkgver() function

The `pkgver` autobump is now achieved via a dedicated `pkgver()` function. This allows for better control over the `pkgver`, and maintainers should favor a `pkgver` that makes sense. To use `pkgver()`, you still need to declare the `pkgver` variable with the most recent value. makepkg will invoke function `pkgver()`, and update variable `pkgver` accordingly.

It is recommended to have following version format: *RELEASE.rREVISION* where *REVISION* is a monotonically increasing number that uniquely identifies the source tree (VCS revisions do this). If there are no public releases and no repository tags then zero could be used as a release number or you can drop *RELEASE* completely and use version number that looks like *rREVISION*. If there are public releases but repo has no tags then the developer should get the release version somehow e.g. by parsing the project files.

The revision number delimiter ("r" right before REVISION) is important. This delimiter allows to avoid problems in case if upstream decides to make its first release or uses versions with different number of components. E.g. if at revision "455" upstream decides to release version 0.1 then the revision delimiter preserves version monotonicity - `0.1.r456 > r454`. Without the delimiter monotonicity fails - `0.1.456 < 454`.

See [PKGBUILD-vcs.proto](https://projects.archlinux.org/pacman.git/tree/proto/PKGBUILD-vcs.proto#n33) for generic examples showing the intended output.

#### Git

Using the most recent annotated tag reachable from the last commit:

```
pkgver() {
  cd "$pkgname"
  git describe --long | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
```

```
2.0.r6.ga17a017

```

Using the most recent un-annotated tag reachable from the last commit:

```
pkgver() {
  cd "$pkgname"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}
```

```
0.71.r115.gd95ee07

```

In case if the git tag does not contain dashes then one can use simpler sed expression `sed 's/-/.r/;s/-/./'`.

If tag contains a prefix, like `v` or project name then it should be cut off:

```
pkgver() {
  cd "$pkgname"
  # cutting off 'foo-' prefix that presents in the git tag
  git describe --long | sed 's/^foo-//;s/\([^-]*-g\)/r\1/;s/-/./g'
}
```

```
6.1.r3.gd77e105

```

If there are no tags then use number of revisions since beginning of the history:

```
pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}
```

```
r1142.a17a017

```

Version and only commit/revision number (SHA1 omitted; however, without a SHA1 quick referencing of an exact revision is lost if not mindful of versioning):

```
git describe --long | sed -r 's/-([0-9,a-g,A-G]{7}.*)//' | sed 's/-/./'

```

Both methods can also be combined, to support repositories that start without a tag but get tagged later on (uses a bashism):

```
pkgver() {
  cd "$pkgname"
  ( set -o pipefail
    git describe --long 2>/dev/null | sed 's/\([^-]*-g\)/r\1/;s/-/./g' ||
    printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
  )
}
```

```
0.9.9.r27.g2b039da  # if tags exist
r1581.2b039da       # else fallback

```

#### Subversion

```
pkgver() {
  cd "$pkgname"
  local ver="$(svnversion)"
  printf "r%s" "${ver//[[:alpha:]]}"
}
```

```
r8546

```

**Note:** If the project has releases you should use them instead of the `0.`.

#### Mercurial

```
pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(hg identify -n)" "$(hg identify -i)"
}
```

```
r2813.75881cc5391e

```

#### Bazaar

```
pkgver() {
  cd "$pkgname"
  printf "r%s" "$(bzr revno)"
}
```

```
r830

```

#### Fallback

In case no satisfactory `pkgver` can be extracted from the repository, the current date can be used:

```
pkgver() {
  date +%Y%m%d
}
```

```
20130408

```

Although it does not identify source tree state uniquely, so avoid it if possible.

## Tips

### Git Submodules

Git submodules are a little tricky to do. The idea is to add the URLs of the submodules themselves directly to the sources array and then reference them during prepare(). This could look like this:

```
source=("git://somewhere.org/something/something.git"
        "git://somewhere.org/mysubmodule/mysubmodule.git")

prepare() {
  cd something
  git submodule init
  git config submodule.mysubmodule.url $srcdir/mysubmodule
  git submodule update
}

```

The reason for doing it like that is explained in [[1]](http://sprunge.us/HKdJ?md).