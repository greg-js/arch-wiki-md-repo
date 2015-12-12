# Creating packages (Česky)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Tento článek je zaměřen na pomoc uživatelům při vytváření vlastních balíčků v Arch Linuxu (a systémech z něj vycházejících). Obsahuje vytvoření [PKGBUILD](/index.php/PKGBUILD_(%C4%8Cesky) "PKGBUILD (Česky)") – soubor obsahující instrukce pro sestavení pomocí `makepkg`, který vytvoří binární balíček ze zdrojového kódu.

## Contents

*   [1 Přehled](#P.C5.99ehled)
*   [2 Příprava](#P.C5.99.C3.ADprava)
    *   [2.1 Potřebný software](#Pot.C5.99ebn.C3.BD_software)
    *   [2.2 Stažení a test instalace](#Sta.C5.BEen.C3.AD_a_test_instalace)
*   [3 Vytváření PKGBUILDu](#Vytv.C3.A1.C5.99en.C3.AD_PKGBUILDu)

## Přehled

Balíčky v Arch Linuxu jsou sestavovány nástrojem [makepkg](/index.php/Makepkg "Makepkg") pomocí informací v souboru [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"). `makepkg` při startu hledá soubor `PKGBUILD` v pracovním adresáři a řídí se jeho instrukcemi pro kompilaci. Výsledný balíček obsahuje binární soubory a instrukce k své instalaci pro [pacman](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)").

Balíček Archu není nic než tar archív komprimovaný xz nebo 'tarball', který obsahuje:

*   Binární soubory k instalaci

*   `.PKGINFO`: obsahující všechna metadata, které pacman potřebuje pro ostaní balíčky, závislosti atp.

*   `.INSTALL`: volitelný soubor používaný pro spuštění příkazů po instalaci/upgradu/odstranění stage. (Tento soubor je přítomný pouze tehdy, pokud je uveden v `PKGBUILD`.)

*   `.Changelog`: volitelný soubor dokumentující změny v balíčku. (Není přítomný ve všech balíčcích.)

## Příprava

### Potřebný software

Nejprve se ujistěte, že potřebné nástroje jsou nainstalované. Skupina balíčků s názvem "base-devel" by měla stačit; obsahuje _make_ a další nástroje potřebné ke kompilaci ze zdrojového kódu.

```
# pacman -S base-devel

```

Jeden z klíčů pro sestavení balíčků je [makepkg](/index.php/Makepkg "Makepkg"), který dělá následující:

1.  Kontroluje, jestli jsou nainstalované závislosti.
2.  Stáhne zdrojový soubor (soubory) z uvedeného (uvedených) serveru(serverů).
3.  Rozpakuje zdrojový soubor (soubory).
4.  Zkompiluje software a nainstaluje v fakeroot prostředí.
5.  Oddělí symboly od binárních souborů a knihoven.
6.  Generuje meta soubor balíčku, který obashuje každý balíček.
7.  Zkomprimuje fakeroot prostředí do souboru balíčku.
8.  Uloží soubor balíčku v nakonfigurované cílové složce, výchozí nastavení je pracovní složka.

### Stažení a test instalace

Stáhněte zdrojový tarball softwaru, kterého chcete mít balíček, rozbalte jej a řiďte se kroky autora programu. Zapište každý příkaz a/nebo krok potřebný pro kompilaci a instalaci. Stejné kroky budete opakovat v _PKGBUILD_ souboru.

Většina autorů softwaru se zůstávají u tří kroků:

```
./configure
make
make install

```

Toto je vhodný čas pro ujištění, jestli program pracuje správně.

## Vytváření PKGBUILDu

Když spustíte `makepkg`, bude hledat `[PKGBUILD](/index.php/PKGBUILD_(%C4%8Cesky) "PKGBUILD (Česky)")` soubor v pracovním adresáři. Když je soubor `PKGBUILD` nalezen, proběhne stažení zdrojového kódu softwaru a kompilace podle instrukcí v souboru`PKGBUILD`. Uvedené instrukce musí být plně interpretovatelné [Bashem](https://en.wikipedia.org/wiki/Bash "wikipedia:Bash") shellem. Po úspěšném provedení, výsledný binární soubor/soubory a metadata, to je balíček a závislosti jsou zapakované v `jmeno_balicku.pkg.tar.xz` souboru balíčku, který může být nainstalovaný pomocí `pacman -U [soubor_balicku]`.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Creating_packages_(Česky)&oldid=411563](https://wiki.archlinux.org/index.php?title=Creating_packages_(Česky)&oldid=411563)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [About Arch (Česky)](/index.php/Category:About_Arch_(%C4%8Cesky) "Category:About Arch (Česky)")
*   [Package development (Česky)](/index.php/Category:Package_development_(%C4%8Cesky) "Category:Package development (Česky)")