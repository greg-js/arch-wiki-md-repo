# Yaourt

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [AUR helpers](/index.php/AUR_helpers "AUR helpers")
*   [AUR](/index.php/AUR "AUR")
*   [Pacman](/index.php/Pacman "Pacman")

**Warning:** Yaourt is an unofficial, third-party script that is **not** supported by the Arch Linux developers. Report bugs at the [archlinux.fr bugtracker](http://bugs.archlinux.fr).

[Yaourt](https://github.com/archlinuxfr/yaourt) (**Y**et **A**n**O**ther **U**ser **R**epository **T**ool) is a wrapper for pacman which adds automated access to the [AUR](/index.php/AUR "AUR") using the same syntax as [pacman](/index.php/Pacman "Pacman").

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Persistent local source repositories](#Persistent_local_source_repositories)
    *   [2.2 Cache](#Cache)
    *   [2.3 Build directory](#Build_directory)

## Installation

First install [package-query](https://aur.archlinux.org/packages/package-query/)<sup><small>AUR</small></sup> as a dependency, and then the [yaourt](https://aur.archlinux.org/packages/yaourt/)<sup><small>AUR</small></sup> package itself. Since both those packages are available from the AUR, you will have to install them with the official method for installing unsupported packages, which is exhaustively described in the [AUR](/index.php/AUR "AUR") article. It is important that you understand what "unsupported package" really means, and you can take this as an opportunity to learn what are the operations that [AUR helpers](/index.php/AUR_helpers "AUR helpers") like yaourt make automatic.

Alternatively, add the (unsigned) _archlinuxfr_ repository as described on the [yaourt homepage](http://archlinux.fr/yaourt-en).

## Configuration

See the [yaourt(8)](http://archlinux.fr/man/yaourt.8.html) and [yaourtrc(5)](http://archlinux.fr/man/yaourtrc.5.html) pages for general information.

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

[![Tango-go-next.png](/images/f/f0/Tango-go-next.png)](/index.php/File:Tango-go-next.png)

**This article or section is a candidate for moving to [[]].**

**Notes:** The below topics should be covered by yaourtrc(8), not here. (Discuss in [Talk:Yaourt#](https://wiki.archlinux.org/index.php/Talk:Yaourt))

### Persistent local source repositories

By default, yaourt will pull remote repositories for building to /tmp. To avoid having to refetch whole repositories whenever AUR packages update, you can change this directory by uncommenting and setting `DEVELSRCDIR` in yaourtrc to wherever you want source repositories pulled to. Note this will only apply to devel packages, usually suffixed by -git or -svn.

 `/etc/yaourtrc`  `DEVELSRCDIR="/var/abs/local/yaourtbuild"` 

### Cache

Yaourt by default does not save built package tarballs during installation. To save built AUR packages in the default pacman folder `/var/cache/pacman/pkg`, edit `/etc/yaourtrc` and set:

```
# Build
EXPORT=2

```

Alternatively, set up a separate folder for Yaourt packages by changing these lines to:

```
# Build
EXPORT=1
EXPORTDIR="/var/cache/pacman/pkg-local"

```

### Build directory

Yaourt uses `/tmp` (mounted as [tmpfs](/index.php/Tmpfs "Tmpfs"), limited to 50% of RAM) to compile packages, which may be problematic for systems with low RAM or limited swap space. Change the location in `/etc/yaourtrc` by uncommenting and changing the `TMPDIR` variable.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Yaourt&oldid=404365](https://wiki.archlinux.org/index.php?title=Yaourt&oldid=404365)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Arch User Repository](/index.php/Category:Arch_User_Repository "Category:Arch User Repository")