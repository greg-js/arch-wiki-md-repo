Toto je seznam Pacman GUI frontendů, Pacman/AUR pohlížečů balíčků a tray ohlašovatelů. Je také rozdělen na Gtk2 a Qt kategorie.

**Warning:** Žádný z těchto nástrojů není oficiálně podporován vývojáři Arch Linuxu.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Pacman Frontendy](#Pacman_Frontendy)
    *   [1.1 GNOME/GTK+](#GNOME/GTK+)
        *   [1.1.1 GNOME PackageKit](#GNOME_PackageKit)
    *   [1.2 KDE/Qt](#KDE/Qt)
        *   [1.2.1 KPackageKit](#KPackageKit)
        *   [1.2.2 AppSet](#AppSet)
    *   [1.3 NCurses](#NCurses)
        *   [1.3.1 pcurses](#pcurses)
*   [2 Pacman/AUR Prohlížeč balíčků](#Pacman/AUR_Prohlížeč_balíčků)
    *   [2.1 PkgBrowser](#PkgBrowser)
*   [3 Tray ohlašovatelé](#Tray_ohlašovatelé)
    *   [3.1 Aarchup](#Aarchup)
*   [4 Neaktivní projekty](#Neaktivní_projekty)

# Pacman Frontendy

## GNOME/GTK+

### GNOME PackageKit

GNOME PackageKit je na distribuci nezávislá sbírka nástrojů na správu balíčků. Využívá pacman-glib backend (ve vývoji), poskytuje tyto možnosti:

*   Instalace a odinstalace z repositářů.
*   Automatické obnovování databáze balíčků a upozornění na aktualizaci.
*   Instalace z tarů.
*   Vyhledávání balíčků podle jména, popisu, kategorie nebo souboru.
*   Zobrazení závislostí, souborů a obrácených závislostí.
*   Inorování IgnorePkgs a držení HoldPkgs.
*   Nahlašování doplňkových závislostí, .pacnew souborů...

Je možné změnit odstraňování z -Rc na -Rsc pomocí GConf klíče /apps/gnome-packagekit/enable_autoremove.

Známé problémy:

*   Občas se packagekit daemon zastaví když jsou instalační scripty hodoty. Pokud se to stane, packagekitd proces může mít potomka se stejným jménem (packagekitd), který má dalšího s názvem sh. Je bezpečné zabít potomka packagekitd, pokud jeho potomek sh je zombie. Nicméně tím ztratíte výstup skriptů. Problém opraven s pacmanem 3.5.
*   Nekteré chyby nejsou ohlášeny GNOME PackageKitem.
*   PackageKit nenajde repositáře pokud je `Architecture` nastaveno na `auto` v `/etc/pacman.conf`. Změňte to na `Architecture = i686` popř. `Architecture = x86_64` k odstranění chyby.

Balíčky: [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

## KDE/Qt

### KPackageKit

KPackageKit - pacman GUI frontend, jehož rozhraní pacmana využívá pacman-glib a packagekit-qt. Tento grafický nástroj umožňuje z KDE systemsettings provádět následující úkony:

*   Instalace, odinstalace a aktualizace balíčků
*   Vyhledávání a filtrace balíčků
*   Získání informací o balíčcích
*   Obnoivení databáze balíčků
*   Výběr repositářů k aktualizaci
*   Automatické obnovení databáze (Hodiny, dny...)
*   Automatické aktualizace balíčků

KPackageKit - relativně nový frontend pro pacmana, funguje bez větších problémů, snadno použitelný, jednoduchost a dobrá integrace do KDE (a PolicyKit).

Známé problémy:

*   Viz [#GNOME PackageKit](#GNOME_PackageKit)

**AUR:** [https://aur.archlinux.org/packages.php?ID=20413](https://aur.archlinux.org/packages.php?ID=20413)
**Snímky obrazovky** [http://kde-apps.org/content/show.php/KPackageKit?content=84745](http://kde-apps.org/content/show.php/KPackageKit?content=84745)

### AppSet

AppSet - rozšířený a na funkce bohatý GUI frontend správce balíčků. Má tyto funkce:

*   Kategorie softwaru (hry, kancelář, multimedia, internet atd.)
*   Zobrazuje domovské stránky balíčků v zabudovaném prohlížeči
*   Zobrazuje informace o distribuci v zabudovaní čtečce
*   Aktualizace, instalace a odinstalace balíčků
*   Zobrazuje dostupné aktualizace v trayi
*   Automatické aktualizace databáze
*   Informuje o závislostech (např: při pokusu o odstranění balíčku který je potřeba jiným)
*   Příkaz k vyčištění cache (uvolní místo na disku)
*   Chytrý spouštěč který používá nainstalované programy pro zisk oprávnění k instalaci (hledá kdesu, gksu, případně xterm a sudo)
*   AUR s Packer backendem

AppSet potřebuje jen QT knihovny k instalaci. Může být použit v jakémkoliv prostření. Nyní podporuje jen Archlinux (pacman).

**Domovská stránka:** [http://appset.sourceforge.net/](http://appset.sourceforge.net/)
**AUR:** [appset-qt](https://aur.archlinux.org/packages/appset-qt/)
**Snímky obrazovky** [http://sourceforge.net/project/screenshots.php?group_id=376825](http://sourceforge.net/project/screenshots.php?group_id=376825)

## NCurses

### pcurses

Správce balíčků v curses, obsahuje:

*   regexp filtrování a hledání jakýchkoli vlastností balíčku
*   volitelné barvy
*   upravitelné řazení
*   externí příkazy pro úpravy seznamu balíčků
*   uživatelem definovatelné makra a klávesové zkratky

**Domovská stránka:** [https://github.com/schuay/pcurses](https://github.com/schuay/pcurses)
**AUR:** [pcurses](https://www.archlinux.org/packages/?name=pcurses)
**Snímky obrazovky** [https://bbs.archlinux.org/viewtopic.php?id=122749](https://bbs.archlinux.org/viewtopic.php?id=122749)

# Pacman/AUR Prohlížeč balíčků

### PkgBrowser

Pkgbrowser - program k hledání a prohlížení Arch balíčků, zobrazuje detaily o označeném balíčku.

*   Hledání a prohlížení Arch balíčků i z AUR
*   Pouze informační aplikace, nedokáže instalovat, odinstalovat ani aktualzovat balíčky
*   Záměrně je to doplněk pro CLI správu balíčků pres pacmana
*   Další detaily o používání přístupné přes help menu

**Fórum:** [https://bbs.archlinux.org/viewtopic.php?id=117297](https://bbs.archlinux.org/viewtopic.php?id=117297)
**AUR:** [pkgbrowser](https://aur.archlinux.org/packages/pkgbrowser/)
**Snímky obrazovky a zdrojový kód:** [http://code.google.com/p/pkgbrowser/](http://code.google.com/p/pkgbrowser/)

# Tray ohlašovatelé

### Aarchup

Aarchup - fork archupu. Nabízí stejné možnosti a nějaké navíc (viz [https://bbs.archlinux.org/viewtopic.php?id=119129](https://bbs.archlinux.org/viewtopic.php?id=119129)).

*   Domovská stránka: [https://github.com/aericson/aarchup/](https://github.com/aericson/aarchup/)
*   AUR: [aarchup](https://aur.archlinux.org/packages/aarchup/)
*   Snímky obrazovky: [http://i.imgur.com/yTNvg.png](http://i.imgur.com/yTNvg.png)

# Neaktivní projekty

*   [GtkPacman](http://gtkpacman.berlios.de/)
*   [Guzuta](http://guzuta.berlios.de/)
*   [Shaman](http://chakra-project.org/wiki/index.php/Shaman)
*   [PacmanManager](https://opensvn.csie.org/PacmanManager/)
*   [pacmon](http://code.google.com/p/pacmon/)
*   [Paku](https://gna.org/projects/paku/)
*   [YAPG](http://www.kde-apps.org/content/show.php/YAPG+-+Yet+Another+Pacman+Gui+?content=60052)
*   [zenity_pacgui](http://sourceforge.net/projects/zenitypacgui/)