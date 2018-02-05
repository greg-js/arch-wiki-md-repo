Openbox je odlahčený a vysoko konfigurovatelný okenný správca s rozsiahlou podporou štandardov. Jeho možnosti sú dobre zdokumentované na oficiálnej domovskej stránke. Tento článok sa týká spustenia Openboxu v Arch Linuxe.

## Contents

*   [1 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [2 Samostatný správca okien](#Samostatn.C3.BD_spr.C3.A1vca_okien)
*   [3 Správca okien pre desktopové prostredia](#Spr.C3.A1vca_okien_pre_desktopov.C3.A9_prostredia)
    *   [3.1 GNOME](#GNOME)
        *   [3.1.1 GNOME 2.26](#GNOME_2.26)
        *   [3.1.2 GNOME 2.24](#GNOME_2.24)
        *   [3.1.3 GNOME 2.22 a predchádzajúce](#GNOME_2.22_a_predch.C3.A1dzaj.C3.BAce)
    *   [3.2 KDE](#KDE)
    *   [3.3 Xfce4](#Xfce4)
*   [4 Nastavenie](#Nastavenie)
    *   [4.1 Manuálna konfigurácia](#Manu.C3.A1lna_konfigur.C3.A1cia)
    *   [4.2 ObConf](#ObConf)
    *   [4.3 Konfigurácia aplikácií](#Konfigur.C3.A1cia_aplik.C3.A1ci.C3.AD)
*   [5 Menu](#Menu)
    *   [5.1 Manuálna konfigurácia](#Manu.C3.A1lna_konfigur.C3.A1cia_2)
    *   [5.2 MenuMaker](#MenuMaker)
    *   [5.3 Obmenu](#Obmenu)
        *   [5.3.1 Obm-xdg](#Obm-xdg)
    *   [5.4 Skripty pre xdg menu na bázi Pythonu](#Skripty_pre_xdg_menu_na_b.C3.A1zi_Pythonu)
    *   [5.5 Dynamické menu](#Dynamick.C3.A9_menu)
*   [6 Spustenie programov pri štarte](#Spustenie_programov_pri_.C5.A1tarte)
*   [7 Témy a vzhlad](#T.C3.A9my_a_vzhlad)
    *   [7.1 Témy Openboxu](#T.C3.A9my_Openboxu)
    *   [7.2 Témata GTK](#T.C3.A9mata_GTK)
        *   [7.2.1 GTK2/GTK+](#GTK2.2FGTK.2B)
        *   [7.2.2 GTK1](#GTK1)
        *   [7.2.3 GTK fonty](#GTK_fonty)
        *   [7.2.4 GTK ikony](#GTK_ikony)
    *   [7.3 Kurzory myši](#Kurzory_my.C5.A1i)
    *   [7.4 Ikony plochy](#Ikony_plochy)
    *   [7.5 Pozadie plochy](#Pozadie_plochy)
*   [8 Doporučené programy](#Doporu.C4.8Den.C3.A9_programy)
    *   [8.1 Prihlasovacie manažery](#Prihlasovacie_mana.C5.BEery)
    *   [8.2 Kompozitná plocha](#Kompozitn.C3.A1_plocha)
    *   [8.3 Panely, traye a pagery](#Panely.2C_traye_a_pagery)
        *   [8.3.1 Panely](#Panely)
        *   [8.3.2 Traye](#Traye)
        *   [8.3.3 Pagery](#Pagery)
    *   [8.4 Správcovia súborov](#Spr.C3.A1vcovia_s.C3.BAborov)
    *   [8.5 Spúštače aplikácií](#Sp.C3.BA.C5.A1ta.C4.8De_aplik.C3.A1ci.C3.AD)
        *   [8.5.1 dmenu](#dmenu)
        *   [8.5.2 Gmrun](#Gmrun)
        *   [8.5.3 Bashrun](#Bashrun)
        *   [8.5.4 Launchy](#Launchy)
        *   [8.5.5 LXPanel](#LXPanel)
        *   [8.5.6 gnome-panel](#gnome-panel)
    *   [8.6 Správcovia schránky](#Spr.C3.A1vcovia_schr.C3.A1nky)
*   [9 Tipy a triky](#Tipy_a_triky)
    *   [9.1 Kopírovať a vložiť](#Kop.C3.ADrova.C5.A5_a_vlo.C5.BEi.C5.A5)
    *   [9.2 Priehladnosť](#Priehladnos.C5.A5)
    *   [9.3 Xprop premenné pre aplikácie](#Xprop_premenn.C3.A9_pre_aplik.C3.A1cie)
        *   [9.3.1 Xprop pre Firefox](#Xprop_pre_Firefox)
    *   [9.4 Pripojenie menu na príkaz](#Pripojenie_menu_na_pr.C3.ADkaz)
    *   [9.5 Urxvt na pozadí](#Urxvt_na_pozad.C3.AD)
    *   [9.6 Ovládanie hlasitosti z klávesnice](#Ovl.C3.A1danie_hlasitosti_z_kl.C3.A1vesnice)
*   [10 Zdroje](#Zdroje)

## Inštalácia

Openbox je dostupný v repozitári Extra:

```
pacman -S openbox

```

Po nainstalovaní Openboxu sme vyzvaný ku prekopírovaniu súborov `menu.xml` a `rc.xml` do <tt>~/.config/openbox/</tt>.

**Note:** Operáciu robte prihlásený ako bežný uživatel, nie root.

```
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/rc.xml
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/menu.xml

```

Súbor `rc.xml` je hlavný konfiguračný súbor pre Openbox. Nastavujú sa tu klávesové skratky, témy, virtuálne plochy a dalšie možnosti.

Súbor `menu.xml` obsahuje menu aplikácii Openboxu, ktoré sa zobrazia kliknutím na plochu. Štandardných položiek je málo, ale menu je velmi lahko modifikovať podla vaších potrieb. Viac viz sekciu nižšie, venovanú úpravám menu, alebo navštívte [oficiálne stránky Openboxu](http://icculus.org/openbox/).

## Samostatný správca okien

Ku spusteniu samostatného Openboxu stačí pridať na koniec súboru `~/.xinitrc` následujúci riadok:

```
exec openbox-session

```

Pokial ste skôr použili iného správcu okien, napr. Xfce, a Openbox sa nechce spustiť po odhlásení z X, presunte adresár autostart:

```
mv ~/.config/autostart ~/.config/autostart-bak

```

**Note:** [python2-xdg](https://www.archlinux.org/packages/?name=python2-xdg) je vyžadovaný pre spustenie Openboxu

## Správca okien pre desktopové prostredia

### GNOME

#### GNOME 2.26

***Pokračujte podla nasledujúceho návodu pre GNOME 2.24\. Pokial zlyhá, skúste toto:***

Pokial sa po inštalácií openboxu nejde prihlásiť do sedenia 'Gnome/openbox', je pre zachovanie openboxu ako správcu okien pre sedenie 'Gnome' z prihlasovacieho manažéru (xdm, gdm, kdm, entrance, slim atd.) skúsiť následujúce:

1.  Prihlaste sa len do sedenia Gnome (ktoré ako správca okien stále používa metacity).
2.  Nainštalujte openbox, pokial už neni nainštalovaný.
3.  Chodte do menu *System → Preferences → Startup Applications* (alebo s názvom 'Session' pre staršiu verziu Gnome)
4.  Otvorte Startup Application, zvolte '+ Add' a zadajte text, ako je uvedené nižšie a vynechajte text za znakom #.
5.  Teraz stlačte tlačítko 'Add' a uistite sa, že je zatrhnutý checkbox vedla vášho nového záznamu.
6.  Odhláste sa z Gnome a prihláste sa späť - openbox by mal byť teraz nastavený ako správca okien.

```
Name:    Openbox Windox Manager          # Môže byť zmenené
Command: openbox --replace               # Tento riadok by nemal byť odstránený, ale pridaný
Comment: Replaces metacity with openbox  # Môže byť zmenené

```

Toto prida položku do zoznamu, ktorý gnome spúšta vždy, ked je spustené špeciálne uživatelské sedenie Gnome.

#### GNOME 2.24

Vytvorte súbor `/usr/share/applications/openbox.desktop` s nasledujúcím obsahom:

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=OpenBox
Exec=openbox
NoDisplay=true
# name of loadable control center module
X-GNOME-WMSettingsModule=openbox
# name we put on the WM spec check window
X-GNOME-WMName=OpenBox

```

Potom v gconf nastavte **/desktop/gnome/session/required_components/windowmanager** na **openbox**:

```
$ gconftool-2 -s -t string /desktop/gnome/session/required_components/windowmanager openbox

```

Nakoniec vyberte sedenie **GNOME** v menu GDM.

#### GNOME 2.22 a predchádzajúce

1.  Pokial používate GDM, zvolte možnost "GNOME/Openbox"
2.  Pokial používate, pridajte `exec openbox-gnome-session` do súboru `~/.xinitrc`
3.  Zo shellu:

```
$ xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  Pokial používate KDM, zvolte možnost "KDE/Openbox"
2.  Pokal používate startx, pridajte `exec openbox-kde-session` do súboru `~/.xinitrc`
3.  Zo shellu:

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

Prihláste sa do normálneho sedenia Xfce4\. V termináli zadejte:

```
$ killall xfwm4 ; openbox & exit

```

Toto ukončí proces xfwm4, spustí Openbox, a zatvorí terminál.

Odhláste sa, uistite sa, že je zatrhnuté "Save session for future logins". Pri dalšom prihlásení Xfce4 použije Openbox ako svojho správcu okien. Aby išlo ukončiť sedenie xfce4, otvorte súbor `~/.config/openbox/menu.xml` (pokial neexistuje, skopírujte ho z `/etc/xdg/openbox/menu.xml`).

Najdete sekciu:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

a zmente ju na:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Stlačením položky "Exit" v menu ukončíte Openbox a zostanete bez správcu okien.

Pokial vám vadí, že koliesko myši mení virtuálne plochy, otvorte súbor `~/.config/openbox/rc.xml` a zmente priradenie myši u akcií "DesktopPrevious" a "DesktopNext" v súvislosti "Desktop" na súvislosť "Root" (Root možno budete musieť nadefinovať).

Pokial chcete použiť menu Openboxu miesto menu Xfce, môžete ukončiť Xfdesktop týmto príkazom v termináli:

```
$ xfdesktop --quit

```

Xfdesktop ale spravuje pozadie plochy a ikony, takže budete na túto činnosť potrebovať iné nástroje, napr. ROX.

(Po ukončení Xfdesktop hore uvedený problém s virtuálnymi plochami skončí.)

## Nastavenie

Pre nastavenie základných vlastností Openboxu existujú dve možnosti; manuálna editácia súboru `rc.xml`, alebo použiť nástroj ObConf.

### Manuálna konfigurácia

Pre manuálnu konfiguráciu Openboxu otvorte súbor `~/.config/openbox/rc.xml` vo svojom oblúbenom textovom editore. Konfiguračný súbor obsahuje mnoho komentárov, a dalšia úplná dokumentácia je dostupná na [oficiálnom serveri](http://openbox.org/wiki/Configuration).

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) je grafický nástroj pre konfiguráciu Openboxu, ktorým môzte nastaviť mnoho vlastností, napr. témy, virtuálne plochy, vlastnosti okien a okraje plôch.

ObConf sa inštaluje príkazom:

```
# pacman -S obconf

```

**Note:** ObConf nemožno použiť na konfiguráciu klávesových skratiek a dalších rozšírených možností. Pre tieto nastavenia je nutné editovať súbor `rc.xml` manuálne (viz výššie). Dalšia možnosť je program [ObKey](http://code.google.com/p/obkey/) (v repozitári [AUR](/index.php/AUR "AUR")).

### Konfigurácia aplikácií

Openbox ponúka individuálne nastavenie aplikácií, umožňujúce definovať pravidlá pre vaše programy. Napr. môžete:

*   spustiť internetový prehliadač na určitej ploche,
*   spustiť terminál bez okraja okna,
*   spustiť torrent klienta na určitej pozícií obrazovky

Pravidlá sú v súbore `~/.config/openbox/rc.xml`. Môžete si všimnúť, že sú v súbore dobre okomentované. Detaily môžte najsť na servere: [http://icculus.org/openbox/index.php/Help:Applications](http://icculus.org/openbox/index.php/Help:Applications)

## Menu

Defaultné menu Openboxu obsahuje niekolko aplikácií, ale určite si ich budete chcieť upraviť. Môžte to urobiť niekolkými spôsobmi:

### Manuálna konfigurácia

Podobne ako súbor `rc.xml` môžete editovať súbor `~/.config/openbox/menu.xml` vo svojom oblúbenom textovom editore. Aj ked je vetšina možností zrejmá, existuje [kompletná dokumentácia](http://icculus.org/openbox/index.php/Help:Menus).

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) je kvalitný nástroj pre tvorbu menu v XML formáte pre rôzne okenné manažery vrátane Openboxu. MenuMaker prehladá váš počítač a na základe výsledkov nainštalovaných programov vytvorí XML menu. Možte mu nastaviť, aby vynechal programy X, GNOME, KDE, alebo Xfce.

MenuMaker je dostupný v repozitári community:

```
# pacman -S menumaker

```

Po nainštalování môžte vygenerovať kompletné menu príkazom:

```
$ mmaker -v OpenBox3

```

Defaultne MenuMaker neprepíše existujúci súbor menu.xml. Môžete tak učiniť parametrom -f (force):

```
$ mmaker -vf OpenBox3

```

Kompletný zoznam parametrov môžte získať spustením s parametrom `mmaker --help`.

Týmto získate dosť slušné menu. Dalej ho môžete modifikovať ručne editáciou menu.xml alebo po doinštalovaní dalších programov znova vygenerovať.

### Obmenu

Obmenu je grafický editor menu pre Openbox. Je to najlepšia volba pre tých, ktorý nechcú editovať XML kód.

Obmenu je dostupný v repozitári community:

```
# pacman -S obmenu

```

Po nainštalovaní spusťte `obmenu` a pridajte alebo odoberte konkrétne programy.

#### Obm-xdg

<tt>obm-xdg</tt> je nástroj pre príkazový riadok, je súčástou Obmenu. Dokáže vygenerovať kategorizované submenu nainštalovaných programov GTK/GNOME.

Pre použitie obm-xdg pridajte do súboru `~/.config/openbox/menu.xml` riadok:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Potom spusťte `openbox --reconfigure` pre obnovu menu Openboxu. Teraz sa v menu objaví submenu s názvom **xdg**.

**Note:** Pokial nemáte nainštalováný GNOME, je nutné pre beh programu obm-xdg nainštalovať balíček **gnome-menus**.

### Skripty pre xdg menu na bázi Pythonu

Skript môžte nájsť v balíčku Openbox z Fedory. Niekam skript uložte a pridajte do menu položku.

Tu je môj: [http://pastebin.com/f2f827625](http://pastebin.com/f2f827625) A tu je zdrojový: [http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup](http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup)

Niektorý si stiahnite (zrejme budete preferovať zdrojový). Súbor niekam uložte, napr. ~/Documents/build/xdg-menu (položku v menu upravte neskôr podla svojho umiestnenia.)

Otvorte súbor menu.xml v textovom editore a pridajte nasledujúcu položku na miesto, kde chcete mať nové menu (názov samozrejme môžete lubovolne zmeniť):

```
<menu id="apps-menu" label="xdgmenu" execute="python /home/shiki/Documents/build/xdg-menu"/>

```

Uložte súbor a spusťte: `openbox --reconfigure`.

### Dynamické menu

Openbox (a další správcovia okien, napr. WindowMaker a PekWM) umožňujú tvorbu skriptov, ktoré dynamicky tvoria menu za pochodu. Napr. systémové monitory, ovládače prehrávača médií a správy počasia. Mnoho príkladov je uvedených na [stránkach Openboxu](http://openbox.org/wiki/Openbox:Pipemenus).

Xyne vytvoril prehliadač súborov a brisbin33 vytvoril skript pre hladanie / pripojenie sa k bezdrôtovým sietam (vyžaduje netcfg). Fórum pre tieto nástroje [je tu](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1) a [tu](https://bbs.archlinux.org/viewtopic.php?id=78290)

## Spustenie programov pri štarte

Openbox podporuje spustenie programov pri štarte pomocou príkazu "openbox-session".

Existujú dva spôsoby spustenia aplikácií pri štarte:

1.  Pokial používate pre prihlásenie do sedenia X startx/xinit, editujte súbor `~/.xinitrc` a zmeňte riadok: execute *openbox* na execute **openbox-session**.
2.  Pokial používate pre prihlásenie GDM/KDM, zvolte sedenie *Openbox* a to automaticky použije autoštart.

Programy, spustitelné po štarte sa nastavujú v súbore `~/.config/openbox/autostart.sh`. Kompletné inštrukcie sú na [stránkach Openboxu](http://openbox.org/wiki/Help:Autostart).

## Témy a vzhlad

Nasledujúci článok je s výnimkou sekcie Témy Openboxu venovaný uživatelom, ktorí používajú Openbox ako samostatného správcu okien bez asistencie GNOME, KDE či Xfce.

### Témy Openboxu

Témy Openboxu určujú vzhlad okrajov okien, názvu a tlačítok, vzhlad menu aplikacií a on-screen display (OSD).

Doplňkové témy sú dostupne z repozitára:

```
# pacman -S openbox-themes

```

Tento balíček neni konečný. Dalšie témy sú na stiahnutie tu:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

Stiahnuté témy by mali byť rozbalené do adresára <tt>~/.themes</tt> a môžu byť inštalované či menené nástrojom ObConf.

Tvorba nových tém je dosť jednoduchá a [dobre zdokumentovaná](http://icculus.org/openbox/index.php/Help:Themes).

Grafický editor tém je [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### Témata GTK

#### GTK2/GTK+

Témy GTK+ môžu byť lahko spravované nástrojom **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme** alebo **switch2**. Inštalácia príkazom:

```
# pacman -S lxappearance

```

a/alebo

```
# pacman -S gtk-chtheme

```

a/alebo

```
# pacman -S gtk-theme-switch2

```

Teraz môžte jednoducho spustiť `lxappearance`, `gtk-chtheme` alebo `switch2` pre nastavenie témy.

#### GTK1

Pre témy GTK1 nainštalujte balíček **gtk-theme-switch**:

```
# pacman -S gtk-theme-switch

```

Pre výber témy potom spusťte `switch`.

#### GTK fonty

Pre manuálnu zmenu fontov a ich velikosti pridajte do súbora `~/.gtkrc.mine` text:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

kde `[font-name] [size]` je zvolený font a velkosť. Napr.:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Obe polia `font_name` a `gtk-font-name` sú vyžadované z dôvodu spätnej kompatibility.

Pre zmenu fontov môžte tiež použiť nástroje **gtk-chtheme** či **lxappearance**. Viz sekcia vyššie.

#### GTK ikony

Najskôr rozbalte témy ikon do adresára <tt>/usr/share/icons</tt> (nutné root práva) či <tt>~/.icons</tt> (lokálny uživatel), potom:

Do súboru `~/.gtkrc.mine` pridajte:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

kde `[name-of-icon-theme]` je názov adresára témy ikon. Napr.:

```
gtk-icon-theme-name = "Tango"

```

Zistite, či je súbor `~/.gtkrc-2.0` konfigurovaný k prechádzaniu súborov `~/.gtkrc.mine`:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

Pre výber GTK tém ikon môžete použiť nástroj **lxappearance**. Viz sekcia vyššie.

### Kurzory myši

Rozbalte požadované témy kurzorov myši do adresára <tt>/usr/share/icons</tt> (nutné root práva) či <tt>~/.icons</tt> (lokálny uživatel). V repozitároch existuje niekolko balíčkov tém, ktoré môžte pacmanom nainštalovať.

Do súbora `~/.Xdefaults` pridajte:

```
Xcursor.theme:   [name-of-cursor-theme]

```

kde `[name-of-cursor-theme]` je názov adresára témy kurzorov myši. Napr.:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

Zmena velkosti:

```
Xcursor.size: [velkost]

```

### Ikony plochy

Openbox neponúka zobrazovanie ikon na ploche. PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](http://idesk.sourceforge.net) alebo Nautilus (a gnome-settings-daemon) toto môžu nahradiť.

ROX a PCmanFM sú naviac odlahčený správcovia súborou.

### Pozadie plochy

Openbox neobsahuje možnosť zmeny pozadia plochy. Môžte to učiniť programami [Feh](/index.php/Feh "Feh") alebo [Nitrogen](/index.php/Nitrogen "Nitrogen"). Dalšie možnosti sú ImageMagick, hsetroot a xsetbg.

## Doporučené programy

Existuje zoznam [odlahčených programov](/index.php/Lightweight_Applications "Lightweight Applications") v Arch wiki, mnoho z nich sa hodí k Openboxu.

### Prihlasovacie manažery

Pre samostatné sedenie Openboxu sa hodí odlahčený grafický prihlasovací manažer [SLiM](http://slim.berlios.de/). Viz Arch [SLiM](/index.php/SLiM "SLiM") wiki pre detailnejšie informácie.

[Qingy](http://qingy.sourceforge.net/) je ultralahký a konfigurovatelný grafický prihlasovací manažér. Podporuje prihlásenie do konzoly i do sedenia X Windows. Používa [DirectFB](http://www.directfb.org), takže nespustí X Windows pokial nezvolíte X Windows sedenie. Viz článok o [Qingy](/index.php/Qingy "Qingy") v Arch wiki.

### Kompozitná plocha

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") je odlahčený kompozitný manažér schopný zobraziť tiene, blednutie a jednoduchú priehladnosť okien v Openboxu a dalších správcoch okien. (Xcompmgr neni dalej vyvíjaný a niektoré problémy pravdepodobne nebudú vyriešené) (S tint2 0.9 sa ikony v systray majú tendenciu rozpadať)

### Panely, traye a pagery

Existuje mnoho nástrojov, ktoré ponúknu panel (taskbar), system tray a pager pre Openbox. Najbežnejšie sú:

#### Panely

*   [PyPanel](/index.php/PyPanel "PyPanel")
*   [BMPanel](http://nsf.110mb.com/bmpanel/)
*   [tint2](/index.php/Tint2 "Tint2")
*   [LXPanel](http://www.gnomefiles.org/app.php/LXPanel)
*   [fbpanel](http://fbpanel.sourceforge.net)
*   [PerlPanel](http://freshmeat.net/projects/perlpanel/)
*   [fspanel](http://www.chatjunkies.org/fspanel/)
*   [Xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)
*   [GnomePanel](http://live.gnome.org/GnomePanel/)
*   [avant-window-navigator](https://launchpad.net/awn)
*   [cairo-dock](http://developer.berlios.de/projects/cairo-dock/)
*   [wbar](http://code.google.com/p/wbar/)
*   [screenlets](http://www.screenlets.org/)
*   [pancake](http://www.failedprojects.de/pancake/)

#### Traye

*   [Stalonetray](http://stalonetray.sourceforge.net/)
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

#### Pagery

*   [Visibility](http://projects.l3ib.org/trac/visibility)
*   [bbpager](http://bbtools.sourceforge.net/)
*   [netwmpager](https://aur.archlinux.org/packages.php?ID=17563)
*   [IPager](http://useperl.ru/ipager/index.en.html)
*   [neap](http://code.google.com/p/neap/)

Vybrané pridajte do súboru startup. Pokial chcete nastaviť plochu bez pageru, môžete použiť [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/), ktorý je balíčkovou verziou nástroja setlayout z Openbox wiki.

### Správcovia súborov

Najoblúbenejší odlahčený správcovia súborou sú:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar ponúka automatické pripojovanie jednotiek a dalšie plug-iny.
*   [ROX](http://rox.sourceforge.net) (ROX ponúka ikony na plochu)

```
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) (pcmanfm tiež ponúka ikony na plochu)

```
# pacman -S pcmanfm

```

Pre prístup na disky s NTFS s PCManFM si nainštalujte ntfs-3g:

```
# pacman -S ntfs-3g

```

a pridajte uživatela do skupiny hal:

```
# gpasswd -a username hal

```

Pre ešte odlahčenejšiu verziu zvážte [Gentoo](http://www.obsession.se/gentoo/) alebo [emelFM2](http://emelfm2.net/), ktoré obe použivajú dvojpanelový vzhlad 'Midnight Commander'.

Dalšie: Xfe muCommander *(Doplním neskôr, ked ich vyskúšam.)*

Dalej samozrejme môžete použiť Nautilus z GNOME. Aj ked je pomalší ako vyššie uvedené riešenia, má podporu VFS (napr. vzdialené SSH, FTP a Samba pripojenie)

### Spúštače aplikácií

#### dmenu

Nastavte si dmenu podla wiki článku [dmenu](/index.php/Dmenu "Dmenu"). Potom vložte nasledujúcu položku do sekcie <keyboard> v súbore `~/.config/openbox/rc.xml` pre nastavenie skratky pre spustenie dmenu:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### Gmrun

[gmrun](http://sourceforge.net/projects/gmrun) ponúka excelentný Run dialog, podobný možnosti Alt+F2 z Gnome a KDE:

```
# pacman -S gmrun

```

Vložte nasledujúcu položku do sekcie <keyboard> v súbore `~/.config/openbox/rc.xml` pre umožnenie funkčnosti Alt+F2:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun

[bashrun](http://bashrun.sourceforge.net) ponúka odlišnú cestu k run dialogu za použitia špeciálneho bash sedenia s malým oknom xterm. Je dostupný v repozitári community a môžte ho spustiť klávesami Alt+F2\. Aby sa bashrun choval tradičnejšie, pridajte nasledujúcu položku do sekcie <applications> v súbore `~/.config/openbox/rc.xml`:

```
   <application name="bashrun">
     <desktop>all</desktop>
     <decor>no</decor>  # zmeňte na yes, pokial chcete okno s rámom
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Launchy

[Launchy](http://www.launchy.net/) je ešte minimalistickejší; je skinovatelný a ponúka dalšie možnosti ako kalkulačku, počasie atd. Pôvodne pre Windows, rovnako pre Gnome.

```
# pacman -S launchy

```

Spúšta sa klávesami Ctrl+Space.

#### LXPanel

Spúštací dialog LXPanelu môžte spustiť takto:

```
lxpanelctl run

```

#### gnome-panel

Spúštací dialog gnome-panelu môžte spustiť takto:

```
gnome-panel-control --run-dialog

```

### Správcovia schránky

Môžete si priať nainštalovať správcu schránky, aby bolo možné využívať funkcie kopírovať/vložiť. **xfce4-clipman-plugin, parcellite,** alebo **glipper-old** môžu byť nainštalovaný pacmanom. Zvolený pridajte do súboru autostart.sh. V terminály funguje Ctrl+Insert ako kopírovať a Shift+Insert ako vložiť. Z terminálu môžte kopírovať Ctrl+Shift+C a vložiť kliknutím stredného tlačítka myši.

## Tipy a triky

### Kopírovať a vložiť

V terminály Ctrl+Insert kopíruje a Shift+Insert vkladá. Z terminálu môžte kopírovať klávesami Ctrl+Shift+C a vložiť kliknutím stredného tlačítka myši.

### Priehladnosť

Pomocou programu [transset-df](https://www.archlinux.org/packages/?name=transset-df) môžete povoliť priehladnosť okien za behu. Napr. editáciou súbora `~/.config/openbox/rc.xml` môžte nastaviť povolenie či zakázanie priehladnosti skrolovaním kolieska myši hore či dole:

```
    <context name="Titlebar">
     <mousebind button="Left" action="Press">
       <action name="Focus"/>
       <action name="Raise"/>
     </mousebind>
     <mousebind button="Left" action="Drag">
       <action name="Move"/>
     </mousebind>
     <mousebind button="Left" action="DoubleClick">
       <action name="ToggleMaximizeFull"/>
     </mousebind>
     <mousebind button="Middle" action="Press">
     	<action name="Lower"/> 
       <action name="FocusToBottom"/>
       <action name="Unfocus"/>
     </mousebind>
     <mousebind button="Up" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --inc  </execute>
       </action>
     </mousebind>
     <mousebind button="Down" action="Click">
       <action name= "Execute" >
       <execute>transset-df -p .2 --dec </execute>
       </action>
     </mousebind>
     <mousebind button="Right" action="Press">
       <action name="Focus"/>
       <action name="Raise"/>
       <action name="ShowMenu">
         <menu>client-menu</menu>
       </action>
     </mousebind>
   </context>

```

Teraz to funguje, len kded niesu aktívne iné akcie.

### Xprop premenné pre aplikácie

Pokial často použivate nastavenie pre aplikácie, môžete oceniť tento bash alias:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

Použitie spustením **`xp`** a kliknutím na bežiaci program, ktorý chcete definovať s nastavením per-app. Výsledok zobrazí len informácie, vyžadované Openboxom, menovite hodnoty WM_WINDOW_ROLE a WM_CLASS (meno a trieda):

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop pre Firefox

Z nejakého dôvodu Firefox a jeho open source alternatívy ignorujú pravidlá aplikacií (napr. <desktop>) pokial je použitý `class="Firefox*"`, bez ohladu na to, čo xprop hlási ako aktuálne hodnoty WM_CLASS.

### Pripojenie menu na príkaz

Niektorí uživatelia chcú pripojiť menu Openboxu či iné na príkaz. Je to praktické napr. pre vytvorenie tlačítka menu v panely. Aj ked toto Openbox nepodporuje, velmi jednoduchý skript, xdotool, dokáže simulovať stlačenie klávesy spustením príkazu. Xdotool je dostupný v [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). Použitie pridaním nasledujúceho kódu do sekcie <keyboard> v súbore `rc.xml`:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Reštartujte/rekonfigurujte Openbox. Teraz môžete magicky vyvolať svoje menu na pozicií kurzora myši spustením nasledujúceho príkazu:

```
# xdotool key ctrl+alt+q

```

Samozrejme môžete lubovolné skratku zmeniť.

### Urxvt na pozadí

V Openboxu môžte lahko spustiť terminál na pozadí plochy.

Najskôr musíme povoliť priehladnosť v súbore `.Xdefaults` (pokial neexistuje, vytvorte ho vo svojom domovskom adresári).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #Nepouživam terminál na celú obrazovku, pokial to chcete, ignorujte tento riadok a pokračujte dalej
URxvt*borderLess:true
URxvt*foreground:Black   #Farba písma. Môj wallpaper je biely, môžete to chcieť zmeniť na bielu farbu.

```

Potom editujte súbor `.config/openbox/rc.xml`:

```
<application name="URxvt">
  <decor>no</decor>
  <focus>yes</focus>
  <position>
    <x>center</x>
    <y>20</y>
  </position>
  <layer>below</layer>
  <desktop>all</desktop>
  <maximized>true</maximized> #Len pokial chcete terminál v plnej velkosti.
</application>

```

Kúzlo je na riadku `<layer>below</layer>`, ktorý umiestni aplikáciu pod všetky ostatné. Urxvt je zobrazený na všetkých plochách, zmeňte to podla svojho.

Note: Miesto mena <application name="URxvt"> môžete použiť (např. "URxvt-bg") a použiť parameter -name pri spustení uxrvt. Týmto spôsobom sa len urxvt terminály, ktoré pomenujete URxvt-bg budú ovládať a chovať podla pravidiel zo súboru rc.xml. Napr.: urxvt -name URxvt-bg (je citlivé na velkosť písmen)

### Ovládanie hlasitosti z klávesnice

Pokial ako výstup zvuku používate ALSA, môžete pre zmenu hlasitosti použiť program amixer. Môžte pre to nastaviť klávesové skratky, alebo môžte namapovať ozajstné multimediálne klávesy, pokial ich vaša klávesnica obsahuje. Napr. v sekcií <keyboard> v súbore rc.xml:

```
   <keybind key="W-Up">
     <action name="Execute">
       <command>amixer set Master 5%+</command>
     </action>
   </keybind>

```

Stlačením klávesy Windows + šipka hore zvýšite hlasitosť o 5%. Rovnaké nastavenie pre zníženie hlasitosti:

```
   <keybind key="W-Down">
     <action name="Execute">
       <command>amixer set Master 5%-</command>
     </action>
   </keybind>

```

## Zdroje

*   [Openbox Website](http://openbox.org/) – Oficiálna stránka
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox novinky
*   [Box-Look.org](http://www.box-look.org/) – Dobrý zdroj tém a artworku