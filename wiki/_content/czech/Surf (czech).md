[surf](http://surf.suckless.org/) je minimalistický webobvý prohlížeč postavený na technologii WebKit/GTK+. Umožňuje prohlížet webové stránky a pracovat s odkazy. It supports the XEmbed protocol which makes it possible to embed it in another application. Furthermore, one can point surf to another URI by setting its XProperties.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
*   [3 Extended usage](#Extended_usage)
    *   [3.1 Patches & additional features](#Patches_&_additional_features)
    *   [3.2 Tabbed browsing](#Tabbed_browsing)
*   [4 See also](#See_also)

## Instalace

Balíček [surf](https://www.archlinux.org/packages/?name=surf) může být [nainstalován](/index.php/Pacman "Pacman") z [Official Repositories](/index.php/Official_repositories_(%C4%8Cesky) "Official repositories (Česky)"). K dispozici je ještě balíček [surf-git](https://aur.archlinux.org/packages/surf-git/) v uživatelském repozitáři [AUR](/index.php/AUR "AUR").

Volitelné:

*   [dmenu](https://www.archlinux.org/packages/?name=dmenu) pro URL adresní řádek

## Konfigurace

Aplikaci surf lze konfigurovat pomocí `config.h` souboru. A sample `config.def.h` file is included with the source and should be instructive.

As with other packages such as [dwm](/index.php/Dwm "Dwm"), consider using the Arch Build System ([ABS](/index.php/ABS "ABS")) and maintaining your own [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") with sources and md5sums for your own configuration and source files.

## Extended usage

### Patches & additional features

There are many user-created [patches](http://surf.suckless.org/patches/) available from the offical site that greatly extend the functionality of surf. Patches can be applied to both the source `surf.c` file and the `config.h` file:

```
$ cd src/surf-[version]/
$ patch -p1 < path/to/patch.diff

```

### Tabbed browsing

The [tabbed](https://www.archlinux.org/packages/?name=tabbed) program can be used with surf to create a simple tabbed browsing experience.

A basic set-up:

```
$ tabbed surf -e

```

Note that to achieve a similar effect to Firefox or Chromium where upon closing the last tab, the browswer exits, use instead:

```
$ tabbed -c surf -e

```

See the man page for tabbed for more details and possibilities.

## See also

*   [surf's official website](http://surf.suckless.org/)
*   [dmenu](/index.php/Dmenu "Dmenu") - Simple application launcher from the developers of dwm
*   [Hacking surf thread](https://bbs.archlinux.org/viewtopic.php?id=167804/)