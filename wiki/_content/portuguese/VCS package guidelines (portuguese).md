**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

[Sistema de controle de versões](https://en.wikipedia.org/wiki/pt:Sistema_de_controle_de_vers%C3%B5es "wikipedia:pt:Sistema de controle de versões") pode ser usado para obter o códifo fonte para tanto pacotes versionados estaticamente quanto a última versão (*trunk*) de um ramo de desenvolvimento. Esse artigo cobre ambos casos.

## Contents

*   [1 Protótipos](#Prot.C3.B3tipos)
*   [2 Diretrizes](#Diretrizes)
    *   [2.1 Fontes VCS](#Fontes_VCS)
    *   [2.2 A função pkgver()](#A_fun.C3.A7.C3.A3o_pkgver.28.29)
        *   [2.2.1 Git](#Git)
        *   [2.2.2 Subversion](#Subversion)
        *   [2.2.3 Mercurial](#Mercurial)
        *   [2.2.4 Bazaar](#Bazaar)
        *   [2.2.5 Reserva](#Reserva)
*   [3 Dicas](#Dicas)
    *   [3.1 Submódulos git](#Subm.C3.B3dulos_git)

## Protótipos

Use apenas os protótipos de PKGBUILD fornecidos pelo pacote [pacman](https://www.archlinux.org/packages/?name=pacman) (`PKGBUILD-split.proto`, `PKGBUILD-vcs.proto` e `PKGBUILD.proto` em `/usr/share/pacman`).

## Diretrizes

*   Adicione um sufixo a `pkgname` com `-cvs`, `-svn`, `-hg`, `-darcs`, `-bzr`, `-git` etc. a menos que o pacote obtenha uma versão especifíca.

*   Se o pacote resultante for diferente depois de alterar as dependências, URL, fontes, etc., aumentar o `pkgrel` é obrigatório. Tocar no `pkgver` não é.

*   `--holdver` pode ser usado para evitar que [makepkg (Português)](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") atualize o `pkgver` (veja: [makepkg(8)](https://www.archlinux.org/pacman/makepkg.8.html))

*   Inclua o que o pacote conflita com e fornece (p.ex. para [fluxbox-git](https://aur.archlinux.org/packages/fluxbox-git/): `conflicts=('fluxbox')` e `provides=('fluxbox')`).

*   `replaces=()` geralmente causa problemas desnecessários e deve ser evitado.

*   Ao usar o cvsroot, use `anonymous:@` em vez de `anonymous@` para evitar ter que digitar uma senha em branco ou `anonymous:senha@`, se uma for exigida.

*   Inclua a ferramenta de VCS apropriada em `makedepends=()` ([cvs](https://www.archlinux.org/packages/?name=cvs), [subversion](https://www.archlinux.org/packages/?name=subversion), [git](https://www.archlinux.org/packages/?name=git), ...).

*   Porque os fontes não são estáticos, ignore a verificação de soma em `md5sums=()` adicionando `'SKIP'`.

### Fontes VCS

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
source=('project_name::git+http://project_url#branch=project_branch')

```

### A função pkgver()

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

#### Reserva

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

## Dicas

### Submódulos git

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