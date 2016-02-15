Openbox je odlehčený a vysoce konfigurovatelný okenní správce s rozsáhlou podporou standardů. Jeho možnosti jsou dobře zdokumentované na oficiální domovské stránce. Tento článek se týká spouštění Openboxu v Arch Linuxu.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Samostatný správce oken](#Samostatn.C3.BD_spr.C3.A1vce_oken)
*   [3 Správce oken pro desktopová prostředí](#Spr.C3.A1vce_oken_pro_desktopov.C3.A1_prost.C5.99ed.C3.AD)
    *   [3.1 GNOME](#GNOME)
        *   [3.1.1 GNOME 2.26](#GNOME_2.26)
        *   [3.1.2 GNOME 2.24](#GNOME_2.24)
        *   [3.1.3 GNOME 2.22 a předchozí](#GNOME_2.22_a_p.C5.99edchoz.C3.AD)
    *   [3.2 KDE](#KDE)
    *   [3.3 Xfce4](#Xfce4)
*   [4 Nastavení](#Nastaven.C3.AD)
    *   [4.1 Manuální konfigurace](#Manu.C3.A1ln.C3.AD_konfigurace)
    *   [4.2 ObConf](#ObConf)
    *   [4.3 Konfigurace aplikací](#Konfigurace_aplikac.C3.AD)
*   [5 Menu](#Menu)
    *   [5.1 Manuální konfigurace](#Manu.C3.A1ln.C3.AD_konfigurace_2)
    *   [5.2 MenuMaker](#MenuMaker)
    *   [5.3 Obmenu](#Obmenu)
        *   [5.3.1 Obm-xdg](#Obm-xdg)
    *   [5.4 Skripty pro xdg menu na bázi Pythonu](#Skripty_pro_xdg_menu_na_b.C3.A1zi_Pythonu)
    *   [5.5 Dynamická menu](#Dynamick.C3.A1_menu)
*   [6 Spouštění programů při startu](#Spou.C5.A1t.C4.9Bn.C3.AD_program.C5.AF_p.C5.99i_startu)
*   [7 Témata a vzhled](#T.C3.A9mata_a_vzhled)
    *   [7.1 Témata Openboxu](#T.C3.A9mata_Openboxu)
    *   [7.2 Témata GTK](#T.C3.A9mata_GTK)
        *   [7.2.1 GTK2/GTK+](#GTK2.2FGTK.2B)
        *   [7.2.2 GTK1](#GTK1)
        *   [7.2.3 GTK fonty](#GTK_fonty)
        *   [7.2.4 GTK ikony](#GTK_ikony)
    *   [7.3 Kurzory myši](#Kurzory_my.C5.A1i)
    *   [7.4 Ikony plochy](#Ikony_plochy)
    *   [7.5 Pozadí plochy](#Pozad.C3.AD_plochy)
*   [8 Doporučené programy](#Doporu.C4.8Den.C3.A9_programy)
    *   [8.1 Přihlašovací manažery](#P.C5.99ihla.C5.A1ovac.C3.AD_mana.C5.BEery)
    *   [8.2 Kompozitní plocha](#Kompozitn.C3.AD_plocha)
    *   [8.3 Panely, traye a pagery](#Panely.2C_traye_a_pagery)
        *   [8.3.1 Panely](#Panely)
        *   [8.3.2 Traye](#Traye)
        *   [8.3.3 Pagery](#Pagery)
    *   [8.4 Správci souborů](#Spr.C3.A1vci_soubor.C5.AF)
    *   [8.5 Spouštěče aplikací](#Spou.C5.A1t.C4.9B.C4.8De_aplikac.C3.AD)
        *   [8.5.1 dmenu](#dmenu)
        *   [8.5.2 Gmrun](#Gmrun)
        *   [8.5.3 Bashrun](#Bashrun)
        *   [8.5.4 Launchy](#Launchy)
        *   [8.5.5 LXPanel](#LXPanel)
        *   [8.5.6 gnome-panel](#gnome-panel)
    *   [8.6 Správci schránky](#Spr.C3.A1vci_schr.C3.A1nky)
*   [9 Tipy a triky](#Tipy_a_triky)
    *   [9.1 Kopírovat a vložit](#Kop.C3.ADrovat_a_vlo.C5.BEit)
    *   [9.2 Průhlednost](#Pr.C5.AFhlednost)
    *   [9.3 Xprop proměnné pro aplikace](#Xprop_prom.C4.9Bnn.C3.A9_pro_aplikace)
        *   [9.3.1 Xprop pro Firefox](#Xprop_pro_Firefox)
    *   [9.4 Připojení menu na příkaz](#P.C5.99ipojen.C3.AD_menu_na_p.C5.99.C3.ADkaz)
    *   [9.5 Urxvt na pozadí](#Urxvt_na_pozad.C3.AD)
    *   [9.6 Ovládání hlasitosti z klávesnice](#Ovl.C3.A1d.C3.A1n.C3.AD_hlasitosti_z_kl.C3.A1vesnice)
*   [10 Zdroje](#Zdroje)

## Instalace

Openbox je dostupný v repozitáři Extra:

```
pacman -S openbox

```

Po nainstalování Openboxu jsme vyzváni k překopírování souborů `menu.xml` a `rc.xml` do <tt>~/.config/openbox/</tt>.

**Note:** Operaci provádějte přihlášený jako běžný uživatel, ne root.

```
$ mkdir -p ~/.config/openbox/
$ cp /etc/xdg/openbox/rc.xml ~/.config/openbox/rc.xml
$ cp /etc/xdg/openbox/menu.xml ~/.config/openbox/menu.xml

```

Soubor `rc.xml` je hlavní konfigurační soubor pro Openbox. Nastavují se zde klávesové zkratky, témata, virtuální plochy a další možnosti.

Soubor `menu.xml` obsahuje menu aplikací Openboxu, které se zobrazí kliknutím na plochu. Standardních položek je málo, ale menu lze velmi snadno modifikovat podle vašich potřeb. Více viz sekci níže, věnovanou úpravám menu, nebo navštivte [oficiální stránky Openboxu](http://icculus.org/openbox/).

## Samostatný správce oken

Ke spuštění samostatného Openboxu stačí přidat naspod souboru `~/.xinitrc` následující řádek:

```
exec openbox-session

```

Pokud jste dříve použili jiný správce oken, např. Xfce, a Openbox se nechce spustit po odhlášení z X, přesuňte adresář autostart:

```
mv ~/.config/autostart ~/.config/autostart-bak

```

**Note:** [pyxdg](https://www.archlinux.org/packages/extra/i686/pyxdg/) je vyžadován pro spuštění Openboxu

## Správce oken pro desktopová prostředí

### GNOME

#### GNOME 2.26

_**Pokračujte podle následujícího návodu pro GNOME 2.24\. Pokud selže, zkuste toto:**_

Pokud se po instalaci openboxu nelze přihlásit do sezení 'Gnome/openbox', lze pro zachování openboxu jako správce oken pro sezení 'Gnome' z přihlašovacího manažeru (xdm, gdm, kdm, entrance, slim atd.) zkusit následující:

1.  Přihlašte se pouze do sezení Gnome (které jako správce oken stále používá metacity).
2.  Nainstalujte openbox, pokud již není nainstalován.
3.  Jděte do menu _System → Preferences → Startup Applications_ (nebo s názvem 'Session' pro starší verze Gnome)
4.  Otevřete Startup Application, zvolte '+ Add' a zadejte text, jak je uvedeno níže a vynechte text za znakem #.
5.  Nyní stiskněte tlačítko 'Add' a ujistěte se, že je zatržený checkbox vedle vašeho nového záznamu.
6.  Odhlašte se z Gnome a přihlašte se zpět - openbox by měl být nyní nastavený jako správce oken.

```
Name:    Openbox Windox Manager          # Může být změněno
Command: openbox --replace               # Tento řádek by němel být odstraněn, ale přidán
Comment: Replaces metacity with openbox  # Může být změněno

```

Toto přidá položku do seznamu, který gnome spouští pokaždé, když je spuštěno speciální uživatelské sezení Gnome.

#### GNOME 2.24

Vytvořte soubor `/usr/share/applications/openbox.desktop` s následujícím obsahem:

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

Nakonec vyberte sezení **GNOME** v menu GDM.

#### GNOME 2.22 a předchozí

1.  Pokud používáte GDM, zvolte možnost "GNOME/Openbox"
2.  Pokud používáte, přidejte `exec openbox-gnome-session` do souboru `~/.xinitrc`
3.  Ze shellu:

```
$ xinit /usr/bin/openbox-gnome-session

```

### KDE

1.  Pokud používáte KDM, zvolte možnost "KDE/Openbox"
2.  Pokud používáte startx, přidejte `exec openbox-kde-session` do souboru `~/.xinitrc`
3.  Ze shellu:

```
$ xinit /usr/bin/openbox-kde-session

```

### Xfce4

Přihlašte se do normálního sezení Xfce4\. V terminálu zadejte:

```
$ killall xfwm4 ; openbox & exit

```

Toto ukončí proces xfwm4, spustí Openbox, a zavře terminál.

Odhlašte se, ujistěte se, zda je zatrženo "Save session for future logins". Při dalším přihlášení Xfce4 použije Openbox jako svůj správce oken. Aby šlo ukončit sezení xfce4, otevřete soubor `~/.config/openbox/menu.xml` (pokud neexistuje, zkopírujte jej z `/etc/xdg/openbox/menu.xml`).

Najděte sekci:

```
 <item label="Exit Openbox">
   <action name="Exit">
     <prompt>yes</prompt>
   </action>
 </item>

```

a změňte ji na:

```
 <item label="Exit Openbox">
   <action name="Execute">
     <prompt>yes</prompt>
    <command>xfce4-session-logout</command>
   </action>
 </item>

```

Neboli stiskem položky "Exit" v menu ukončíte Openbox a zůstanete bez správce oken.

Pokud vám vadí, že kolečko myši mění virtuální plochy, otevřete soubor `~/.config/openbox/rc.xml` a změňte přiřazení myši u akcí "DesktopPrevious" a "DesktopNext" v souvislosti "Desktop" na souvislost "Root" (Root možná budete muset nadefinovat).

Pokud chcete použít menu Openboxu místo menu Xfce, můžete ukončit Xfdesktop tímto příkazem v terminálu:

```
$ xfdesktop --quit

```

Xfdesktop ovšem spravuje pozadí plochy a ikony, takže budete na tuto činnost potřebovat jiné nástroje, např. ROX.

(Po ukončení Xfdesktop výše uvedený problém s virtuálními plochami skončí.)

## Nastavení

Pro nastavení základních vlastností Openboxu existují dvě možnosti; manuální editace souboru `rc.xml`, nebo použít nástroj ObConf.

### Manuální konfigurace

Pro manuální konfiguraci Openboxu otevřete soubor `~/.config/openbox/rc.xml` ve svém oblíbeném textovém editoru. Konfigurační soubor obsahuje mnoho komentářů, a další úplná dokumentace je dostupná na [oficiálním serveru](http://openbox.org/wiki/Configuration).

### ObConf

[ObConf](http://icculus.org/openbox/index.php/ObConf:About) je grafický nástroj pro konfiguraci Openboxu, kterým lze nastavit mnoho vlastností, např. témata, virtuální plochy, vlastnosti oken a okraje ploch.

ObConf se instaluje příkazem:

```
# pacman -S obconf

```

**Note:** ObConf nelze použít na konfiguraci klávesových zkratek a dalších rozšířených možností. Pro tato nastavení je nutné editovat soubor `rc.xml` manuálně (viz výše). Další možností je program [ObKey](http://code.google.com/p/obkey/) (v repozitáři [AUR](/index.php/AUR "AUR")).

### Konfigurace aplikací

Openbox nabízí individuální nastavení aplikací, umožňující definovat pravidla pro vaše programy. Např. můžete:

*   spustit internetový prohlížeč na určité ploše,
*   spustit terminál bez okraje okna,
*   spustit torrent klienta na určité pozici obrazovky

Pravidla jsou v souboru `~/.config/openbox/rc.xml`. Můžete si všimnout, že jsou v souboru dobře okomentovaná. Detaily lze najít na serveru: [http://icculus.org/openbox/index.php/Help:Applications](http://icculus.org/openbox/index.php/Help:Applications)

## Menu

Výchozí menu Openboxu obsahuje několik aplikací, ovšem jistě si jej budete chtít upravit. Lze to udělat několika způsoby:

### Manuální konfigurace

Podobně jako soubor `rc.xml` můžete editovat soubor `~/.config/openbox/menu.xml` ve svém oblíbeném textovém editoru. I když je většina možností zřejmá, existuje [kompletní dokumentace](http://icculus.org/openbox/index.php/Help:Menus).

### MenuMaker

[MenuMaker](http://menumaker.sourceforge.net/) je kvalitní nástroj pro tvorbu menu v XML formátu pro různé okenní manažery včetně Openboxu. MenuMaker prohledá váš počítač a na základě výsledků nainstalovaných programů vytvoří XML menu. Lze jej nastavit, aby vynechal programy X, GNOME, KDE, nebo Xfce.

MenuMaker je dostupný v repozitáři community:

```
# pacman -S menumaker

```

Po nainstalování lze vygenerovat kompletní menu příkazem:

```
$ mmaker -v OpenBox3

```

Defaultně MenuMaker nepřepíše existující soubor menu.xml. Lze to učinit parametrem -f (force):

```
$ mmaker -vf OpenBox3

```

Kompletní seznam parametrů lze získat spuštěním s parametrem `mmaker --help`.

Tímto získáte docela slušné menu. Dále jej můžete modifikovat ručně editací menu.xml nebo po doinstalování dalších programů znovu vygenerovat.

### Obmenu

Obmenu je grafický editor menu pro Openbox. Je to nejlepší volba pro ty, kteří nechtějí editovat XML kód.

Obmenu je dostupný v repozitáři community:

```
# pacman -S obmenu

```

Po nainstalování spusťte `obmenu` a přidejte nebo odeberte konkrétní programy.

#### Obm-xdg

<tt>obm-xdg</tt> je nástroj pro příkazovou řádku, je součástí Obmenu. Dokáže vygenerovat kategorizované submenu nainstalovaných programů GTK/GNOME.

Pro použití obm-xdg přidejte do souboru `~/.config/openbox/menu.xml` řádek:

```
<menu execute="obm-xdg" id="xdg-menu" label="xdg"/>

```

Potom spusťte `openbox --reconfigure` pro obnovu menu Openboxu. Nyní se v menu objeví submenu s názvem **xdg**.

**Note:** Pokud nemáte nainstalováno GNOME, je nutné pro běh programu obm-xdg nainstalovat balíček **gnome-menus**.

### Skripty pro xdg menu na bázi Pythonu

Skript lze najít v balíčku Openbox z Fedory. Někam skript uložte a přidejte do menu položku.

Zde je můj: [http://pastebin.com/f2f827625](http://pastebin.com/f2f827625) A zde je zdrojový: [http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup](http://cvs.fedoraproject.org/viewvc/devel/openbox/xdg-menu?view=markup)

Některý si stáhněte (zřejmě budete preferovat zdrojový). Soubor někam uložte, např. ~/Documents/build/xdg-menu (položku v menu upravte později podle svého umístění.)

Otevřete soubor menu.xml v textovém editoru a přidejte následující položku na místo, kde chcete mít nové menu (název samozřejmě můžete libovolně změnit):

```
<menu id="apps-menu" label="xdgmenu" execute="python /home/shiki/Documents/build/xdg-menu"/>

```

Uložte soubor a spusťte: `openbox --reconfigure`.

### Dynamická menu

Openbox (a další správci oken, např. WindowMaker a PekWM) umožňují tvorbu skriptů, které dynamicky tvoří menu za pochodu. Např. systémové monitory, ovladače přehrávačů médií a zprávy počasí. Mnoho příkladů je uvedeno na [stránkách Openboxu](http://openbox.org/wiki/Openbox:Pipemenus).

Xyne vytvořil prohlížeč souborů a brisbin33 vytvořil skript pro hledání / připojení se k bezdrátovým sítím (vyžaduje netcfg). Fórum pro tyto nástroje [je zde](https://bbs.archlinux.org/viewtopic.php?id=77197&p=1) a [zde](https://bbs.archlinux.org/viewtopic.php?id=78290)

## Spouštění programů při startu

Openbox podporuje spouštění programů při startu pomocí příkazu "openbox-session".

Existují dva způsoby spouštění aplikací při startu:

1.  Pokud používáte pro přihlášení do sezení X startx/xinit, editujte soubor `~/.xinitrc` a změňte řádek: execute _openbox_ na execute **openbox-session**.
2.  Pokud používáte pro přihlášení GDM/KDM, zvolte sezení _Openbox_ a to automaticky použije autostart.

Programy, spustitelné po startu se nastavují v souboru `~/.config/openbox/autostart.sh`. Kompletní instrukce jsou na [stránkách Openboxu](http://openbox.org/wiki/Help:Autostart).

## Témata a vzhled

Následující článek je s výjimkou sekce Témata Openboxu věnován uživatelům, kteří používají Openbox jako samostatný správce oken bez asistence GNOME, KDE či Xfce.

### Témata Openboxu

Témata Openboxu určují vzhled okrajů oken, včetně názvu a tlačítek, vzhled menu aplikací a on-screen display (OSD).

Doplňková témata jsou dostupná z repozitářů:

```
# pacman -S openbox-themes

```

Tento balíček není konečný. Další témata jsou ke stažení zde:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

Stažená témata by měla být rozbalena do adresáře <tt>~/.themes</tt> a mohou být instalována či měněna nástrojem ObConf.

Tvorba nových témat je docela snadná a [dobře zdokumentovaná](http://icculus.org/openbox/index.php/Help:Themes).

Grafický editor témat je [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### Témata GTK

#### GTK2/GTK+

Témata GTK+ mohou být snadno spravována nástroji **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme** nebo **switch2**. Instalace příkazem:

```
# pacman -S lxappearance

```

a/nebo

```
# pacman -S gtk-chtheme

```

a/nebo

```
# pacman -S gtk-theme-switch2

```

Nyní lze jednoduše spustit `lxappearance`, `gtk-chtheme` nebo `switch2` pro nastavení tématu.

#### GTK1

Pro témata GTK1 nainstalujte balíček **gtk-theme-switch**:

```
# pacman -S gtk-theme-switch

```

Pro výběr tématu potom spusťte `switch`.

#### GTK fonty

Pro manuální změnu fontů a jejich velikosti přidejte do souboru `~/.gtkrc.mine` text:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

kde `[font-name] [size]` je zvolený font a velikost. Např.:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Obě pole `font_name` a `gtk-font-name` jsou vyžadována z důvodu zpětné kompatibility.

Pro změnu fontů lze také použít nástroje **gtk-chtheme** či **lxappearance**. Viz sekce výše.

#### GTK ikony

Nejdříve rozbalte téma ikon do adresáře <tt>/usr/share/icons</tt> (nutná práva root) či <tt>~/.icons</tt> (lokální uživatel), potom:

Do souboru `~/.gtkrc.mine` přidejte:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

kde `[name-of-icon-theme]` je název adresáře tématu ikon. Např.:

```
gtk-icon-theme-name = "Tango"

```

Zjistěte, zde je soubor `~/.gtkrc-2.0` konfigurován k procházení souboru `~/.gtkrc.mine`:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

Pro výběr GTK témat ikon můžete použít nástroj **lxappearance**. Viz sekce výše.

### Kurzory myši

Rozbalte požadované téma kurzorů myši do adresáře <tt>/usr/share/icons</tt> (nutná práva root) či <tt>~/.icons</tt> (lokální uživatel). V repozitářích existuje několik balíčků témat, které lze pacmanem nainstalovat.

Do souboru `~/.Xdefaults` přidejte:

```
Xcursor.theme:   [name-of-cursor-theme]

```

kde `[name-of-cursor-theme]` je název adresáře tématu kurzorů myši. Např.:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

Změna velikosti:

```
Xcursor.size: [velikost]

```

### Ikony plochy

Openbox nenabízí zobrazování ikona na ploše. PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](http://idesk.sourceforge.net) nebo GNOME Files (a gnome-settings-daemon) toto mohou zastoupit.

ROX a PCmanFM jsou navíc odlehčení správci souborů.

### Pozadí plochy

Openbox neobsahuje možnost změny pozadí plochy. Lze to učinit programy [Feh](/index.php/Feh "Feh") nebo [Nitrogen](/index.php/Nitrogen "Nitrogen"). Další možností jsou ImageMagick, hsetroot a xsetbg.

## Doporučené programy

Existuje seznam [odlehčených programů](/index.php/List_of_applications "List of applications") v Arch wiki, mnoho z nich se hodí k Openboxu.

### Přihlašovací manažery

Pro samostatné sezení Openboxu se hodí odlehčený grafický přihlašovací manažer [SLiM](http://slim.berlios.de/). Viz Arch [SLiM](/index.php/SLiM "SLiM") wiki pro detailnější informace.

[Qingy](http://qingy.sourceforge.net/) je ultralehký a konfigurovatelný grafický přihlašovací manažer. Podporuje přihlášení do konzole i do sezení X Windows. Používá [DirectFB](http://www.directfb.org), takže nespustí X Windows dokud nezvolíte X Windows sezení. Viz článek o [Qingy](/index.php/Qingy "Qingy") v Arch wiki.

### Kompozitní plocha

[Xcompmgr](/index.php/Xcompmgr "Xcompmgr") je odlehčený kompozitní manažer schopný zobrazit stíny, blednutí a jednoduché průhlednosti oken v Openboxu a dalších správcích oken. (Xcompmgr není dále vyvíjen a některé problémy pravděpodobně nebudou vyřešené) (S tint2 0.9 se ikony v systray mají tendenci rozpadat)

Alternativou je [Cairo kompozitní manažer](/index.php/Cairo_Compmgr "Cairo Compmgr") -- všestranný a rozšiřitelný kompozitní manažer, který využívá pro vykreslování cairo.

### Panely, traye a pagery

Existuje mnoho nástrojů, které nabídnou panel (taskbar), system tray a pager pro Openbox. Nejběžnější jsou:

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

Vybrané přidejte do souboru startup. Pokud chcete nastavit plochu bez pageru, můžete použít [obsetlayout](https://aur.archlinux.org/packages/obsetlayout/), který je balíčkovou verzí nástroje setlayout z Openbox wiki.

### Správci souborů

Nejoblíbenější odlehčení správci souborů jsou:

*   [Thunar](/index.php/Thunar "Thunar"). Thunar nabízí automatické připojování jednotek a další plug-iny.
*   [ROX](http://rox.sourceforge.net) (ROX nabízí ikony na plochu)

```
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) (pcmanfm také nabízí ikony na plochu)

```
# pacman -S pcmanfm

```

Pro přístup na disky s NTFS s PCManFM si nainstalujte ntfs-3g:

```
# pacman -S ntfs-3g

```

a přidejte uživatele do skupiny hal:

```
# gpasswd -a username hal

```

Pro ještě odlehčenější verzi zvažte [Gentoo](http://www.obsession.se/gentoo/) nebo [emelFM2](http://emelfm2.net/), které oba používají dvojpanelový vzhled 'Midnight Commander'.

Další: Xfe muCommander _(Doplním později, až je oba vyzkouším.)_

Dále samozřejmě můžete použít GNOME Files. I když je pomalejší než výše uvedená řešení, má podporu VFS (např. vzdálené SSH, FTP a Samba připojení)

### Spouštěče aplikací

#### dmenu

Nastavte si dmenu podle wiki článku [dmenu](/index.php/Dmenu "Dmenu"). Potom vložte následující položku do sekce <keyboard> v souboru `~/.config/openbox/rc.xml` pro nastavení zkratky pro spuštění dmenu:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### Gmrun

[gmrun](http://sourceforge.net/projects/gmrun) nabízí excelentní Run dialog, podobný možnosti Alt+F2 z Gnome a KDE:

```
# pacman -S gmrun

```

Vložte následující položku do sekce <keyboard> v souboru `~/.config/openbox/rc.xml` pro umožnění funkčnosti Alt+F2:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun

[bashrun](http://bashrun.sourceforge.net) nabízí odlišnou cestu k run dialogu za použití speciálního bash sezení s malým oknem xterm. Je dostupný v repozitáři community a lze jej spustit klávesami Alt+F2\. Aby se bashrun choval tradičněji, přidejte následující položku do sekce <applications> v souboru `~/.config/openbox/rc.xml`:

```
   <application name="bashrun">
     <desktop>all</desktop>
     <decor>no</decor>  # změňte na yes, pokud chcete okno s rámem
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Launchy

[Launchy](http://www.launchy.net/) je ještě minimalističtější; je skinovatelný a nabízí další možnosti jako kalkulátor, počasí atd. Původně pro Windows, stejné pro Gnome.

```
# pacman -S launchy

```

Spouští se klávesami Ctrl+Space.

#### LXPanel

Spouštěcí dialog LXPanelu lze spustit takto:

```
lxpanelctl run

```

#### gnome-panel

Spouštěcí dialog gnome-panelu lze spustit takto:

```
gnome-panel-control --run-dialog

```

### Správci schránky

Můžete si přát nainstalovat správce schránky, aby bylo lze využívat funkce kopírovat/vložit. **xfce4-clipman-plugin, parcellite,** nebo **glipper-old** mohou být nainstalováni pacmanem. Zvolený přidejte do souboru autostart.sh. V terminálu funguje Ctrl+Insert jako kopírovat a Shift+Insert jako vložit. Z terminálu lze kopírovat Ctrl+Shift+C a vložit kliknutím prostředního tlačítka myši.

## Tipy a triky

### Kopírovat a vložit

V terminálu Ctrl+Insert kopíruje a Shift+Insert vkládá. Z terminálu lze kopírovat klávesami Ctrl+Shift+C a vložit kliknutím prostředního tlačítka myši.

### Průhlednost

Pomocí programu [transset-df](https://www.archlinux.org/packages/?name=transset-df) můžete povolit průhlednost oken za běhu. Např. editací souboru `~/.config/openbox/rc.xml` lze nastavit povolení či zakázání průhlednosti skrolováním kolečka myši nahoru či dolů, resp. najetím na název okna (je to v sekci <mouse>):

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

Nyní to funguje, pouze když nejsou aktivní jiné akce.

### Xprop proměnné pro aplikace

Pokud často používáte nastavení pro aplikace, můžete ocenit tento bash alias:

```
alias xp='xprop | grep "WM_WINDOW_ROLE\|WM_CLASS" && echo "WM_CLASS(STRING) = \"NAME\", \"CLASS\""'

```

Použití spuštěním **`xp`** a kliknutím na běžící program, který chcete definovat s nastavením per-app. Výsledek zobrazí pouze informace, vyžadované Openboxem, jmenovitě hodnoty WM_WINDOW_ROLE a WM_CLASS (jméno a třída):

```
[thayer@dublin:~] $ xp
WM_WINDOW_ROLE(STRING) = "roster"
WM_CLASS(STRING) = "gajim.py", "Gajim.py"
WM_CLASS(STRING) = "NAME", "CLASS"

```

#### Xprop pro Firefox

Z nějakého důvodu Firefox a jeho open source alternativy ignorují pravidla aplikací (např. <desktop>) dokud je použit `class="Firefox*"`, bez ohledu na to, co xprop hlásí jako aktuální hodnoty WM_CLASS.

### Připojení menu na příkaz

Někteří uživatelé chtějí připojit menu Openboxu či jiné na příkaz. Je to praktické např. pro vytvoření tlačítka menu v panelu. I když toto Openbox nepodporuje, velice jednoduchý skript, xdotool, dokáže simulovat stisknutí klávesy spuštěním příkazu. Xdotool je dostupný v [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=14789&O=0&L=0&C=0&K=xdotool&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd). Použití přidáním následujícího kódu do sekce <keyboard> v souboru `rc.xml`:

```
    <keybind key="A-C-q">
      <action name="ShowMenu">
        <menu>root-menu</menu>
      </action>
    </keybind>

```

Restartujte/rekonfigurujte Openbox. Nyní můžete magicky vyvolat svoje menu na pozici kurzoru myši spuštěním následujícího příkazu:

```
# xdotool key ctrl+alt+q

```

Samozřejmě můžete libovolně zkratku změnit.

### Urxvt na pozadí

V Openboxu lze snadno spustit terminál na pozadí plochy.

Nejdříve musíme povolit průhlednost v souboru `.Xdefaults` (pokud neexistuje, vytvořte jej ve svém domovském adresáři).

```
URxvt*transparent:true
URxvt*scrollBar:false
URxvt*geometry:124x24    #Nepoužívám terminál na celou obrazovku, pokud to chcete, ignorujte tento řádek a pokračujte dál
URxvt*borderLess:true
URxvt*foreground:Black   #Barva písma. Můj wallpaper je bílý, můžete to chtít změnit na bílou barvu.

```

Potom editujte soubor `.config/openbox/rc.xml`:

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
  <maximized>true</maximized> #Pouze pokud chcete terminál v plné velikosti.
</application>

```

Kouzlo je na řádku `<layer>below</layer>`, který umístí aplikaci pod všechny ostatní. Urxvt je zobrazen na všech plochách, změňte to podle svého.

Note: Místo jména <application name="URxvt"> můžete použít (např. "URxvt-bg") a použít parametr -name při spuštění uxrvt. Tímto způsobem se pouze urxvt terminály, které pojmenujete URxvt-bg budou ovládat a chovat podle pravidel ze souboru rc.xml. Např.: urxvt -name URxvt-bg (je citlivé na velikost písmen)

### Ovládání hlasitosti z klávesnice

Pokud jako výstup zvuku používáte ALSA, můžete pro změnu hlasitosti použít program amixer. Lze pro to nastavit klávesové zkratky, nebo lze namapovat opravdové multimediální klávesy, pokud je vaše klávesnice obsahuje. Např. v sekci <keyboard> v souboru rc.xml:

```
   <keybind key="W-Up">
     <action name="Execute">
       <command>amixer set Master 5%+</command>
     </action>
   </keybind>

```

Stiskem kláves Windows + šipka nahoru zvýšíte hlasitost o 5%. Odpovídající nastavení pro snížení hlasitosti:

```
   <keybind key="W-Down">
     <action name="Execute">
       <command>amixer set Master 5%-</command>
     </action>
   </keybind>

```

## Zdroje

*   [Openbox Website](http://openbox.org/) – Oficiální stránka
*   [Planet Openbox](http://planetob.openmonkey.com/) – Openbox novinky
*   [Box-Look.org](http://www.box-look.org/) – Dobrý zdroj témat a artworku