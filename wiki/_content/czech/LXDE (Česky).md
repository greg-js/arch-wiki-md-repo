Tento článek vás naučí, jak nainstalovat a nastavit různé součásti desktopového prostředí **L**ightweight **X**11 **D**esktop **E**nvironment. LXDE je designováno ke spouštění na počítačích s minimálními hardwarovými požadavky. Vyžaduje několik závislostí. Filosofií LXDE je být odlehčené, ale plně použitelné.

## Contents

*   [1 Vlastnosti](#Vlastnosti)
*   [2 Součásti](#Sou.C4.8D.C3.A1sti)
*   [3 Instalace](#Instalace)
*   [4 Spuštění desktopu](#Spu.C5.A1t.C4.9Bn.C3.AD_desktopu)
*   [5 Tipy a opravy chyb](#Tipy_a_opravy_chyb)
    *   [5.1 Programy, spustitelné při startu](#Programy.2C_spustiteln.C3.A9_p.C5.99i_startu)
    *   [5.2 Nastavení aplletu digitálních hodin](#Nastaven.C3.AD_aplletu_digit.C3.A1ln.C3.ADch_hodin)
    *   [5.3 Editace menu aplikací](#Editace_menu_aplikac.C3.AD)
    *   [5.4 Jméno položky My Documents](#Jm.C3.A9no_polo.C5.BEky_My_Documents)
    *   [5.5 Nastavení fontů](#Nastaven.C3.AD_font.C5.AF)
    *   [5.6 Automatické připojování záznamových jednotek](#Automatick.C3.A9_p.C5.99ipojov.C3.A1n.C3.AD_z.C3.A1znamov.C3.BDch_jednotek)
        *   [5.6.1 NTFS s čínskými znaky](#NTFS_s_.C4.8D.C3.ADnsk.C3.BDmi_znaky)
    *   [5.7 LXNM](#LXNM)
    *   [5.8 Sezení LXDE v KDM](#Sezen.C3.AD_LXDE_v_KDM)
    *   [5.9 lxpanel - přidání programu do launch baru](#lxpanel_-_p.C5.99id.C3.A1n.C3.AD_programu_do_launch_baru)
    *   [5.10 lxpanel - přidáni lokace do launch baru](#lxpanel_-_p.C5.99id.C3.A1ni_lokace_do_launch_baru)
    *   [5.11 Ikony/Kurzory](#Ikony.2FKurzory)
        *   [5.11.1 Kurzory](#Kurzory)
        *   [5.11.2 Ikony pro lxpanel](#Ikony_pro_lxpanel)
        *   [5.11.3 Ikona My Documents](#Ikona_My_Documents)
    *   [5.12 Náhrada správce oken](#N.C3.A1hrada_spr.C3.A1vce_oken)
    *   [5.13 Vypnutí a restart z LXDE](#Vypnut.C3.AD_a_restart_z_LXDE)
    *   [5.14 Problémy po upgradu lxsession na verzi 0.4.1](#Probl.C3.A9my_po_upgradu_lxsession_na_verzi_0.4.1)
    *   [5.15 LXsession - plná verze](#LXsession_-_pln.C3.A1_verze)
    *   [5.16 Použití aplikací KDEmod3 v LXDE](#Pou.C5.BEit.C3.AD_aplikac.C3.AD_KDEmod3_v_LXDE)
*   [6 Zdroje](#Zdroje)

## Vlastnosti

Některé vlastnosti LXDE:

*   **Odlehčenost** - běží s přijatelnými nároky na paměť (po spuštění [Xorg](/index.php/Xorg "Xorg") serveru a LXDE je celkové využití paměti asi 45 MB na i686 PC.)
*   **Rychlost** - běží dobře i na starších strojích (hardwarové požadavky LXDE jsou podobné Windows 98)
*   **Praktický design** - uživatelské prostředí gtk2 a vysoké standardy GNOME.
*   **Nezávislé na desktopu** - součásti mohou být použité bez LXDE.
*   **Vyhovující standardům** - dodržuje specifikace projektu Freedesktop.

## Součásti

Informace o některých součástech:

*   **[PCManFM](/index.php/PCManFM "PCManFM")**: Správce souborů, funkce desktopu a tapeta na plochu.
*   **[LXPanel](http://www.gnomefiles.org/app.php/LXPanel)**: Panel se správcem aplikací, aplikačním menu a spoustou appletů.
*   **[LXSession](http://www.gnomefiles.org/app.php/LXSession)**: Správce sezení s podporou standardů X11 a podporou příkazů shutdown/reboot/suspend (vyžaduje [HAL](/index.php/HAL "HAL")).
*   **[LXAppearance](http://www.gnomefiles.org/app.php/LXAppearance)**: Editor témat, který dokáže změnit témata GTK+, témata ikon a fontů pro aplikace GTK.
*   **[Openbox](http://icculus.org/openbox/index.php/Main_Page)**: Odlehčený, podporující standardy a vysoce konfigurovatlený správce oken (doporučený, ale nevyvíjený projektem LXDE).
*   **[Obconf](http://tr.openmonkey.com/pages/obconf/)** - Nástroj pro konfiguraci témat Openboxu.
*   **[GPicView](http://lxde.sourceforge.net/gpicview/)**: Jednoduchý odlehčený prohlížeč obrázků.
*   **[Leafpad](http://tarot.freeshell.org/leafpad/)**: Odlehčený a jednoduchý textový editor (nevyvíjený projektem LXDE).
*   **[XArchiver](http://xarchiver.xfce.org/)**: Odlehčený archivátor souborů (nevyvíjený projektem LXDE).
*   **[LXNM](http://lxde.sourceforge.net/about.html)** Odlehčený správce sítě pro bezdrátové sítě - ve vývoji. Balíček [lxnm](https://aur.archlinux.org/packages/lxnm/) lze nalézt v repozitáři [AUR](/index.php/AUR "AUR").

## Instalace

LXDE je modulární, takže si můžete zvolit balíčky. které potřebujete. Některé balíčky jsou experimentální a pro jejich instalaci je nutné použít repozitář [AUR](/index.php/AUR "AUR").

Minimální povinné balíčky pro instalaci a spuštění prostředí LXDE jsou [lxde-common](https://www.archlinux.org/packages/?name=lxde-common), [lxsession](https://www.archlinux.org/packages/?name=lxsession), [desktop-file-utils](https://www.archlinux.org/packages/?name=desktop-file-utils) a správce oken.

Skupinu LXDE lze nainstalovat příkazem:

```
# pacman -S lxde

```

Instalace skupiny lxde nainstaluje následující balíčky:

*   gpicview
*   lxappearance
*   lxde-common
*   lxde-icon-theme
*   lxlauncher
*   lxmenu-data
*   lxpanel
*   lxrandr
*   lxsession-lite
*   lxtask
*   lxterminal
*   menu-cache
*   openbox
*   pcmanfm

Možná budete potřebovat nainstalovat [Gamin](/index.php/Gamin "Gamin"). Gamin je monitorovací nástroj pro soubory a adresáře, designovaný jako jiná verze programu FAM. Spouští se na žádost programů, které jej podporují, takže nemusí být spuštěn jako démon, na rozdíl od programu fam. Pokud máte fam nainstalován, odstraňte jej z řetězce DAEMONS v souboru `/etc/rc.conf` a zastavte jeho démona před instalací programu gamin.

```
pacman -S gamin

```

Další odlehčené balíčky, které můžete chtít nainstalovat:

```
pacman -S mousepad xarchiver obconf epdfview

```

Další programy jsou uvedeny v článku [Lightweight_Applications](/index.php/Lightweight_Applications "Lightweight Applications").

## Spuštění desktopu

LXDE lze spustit několika odlišnými způsoby. Pokud používáte přihlašovací manažer - např. [SLiM](/index.php/SLiM "SLiM"), [GDM](/index.php/GDM "GDM") nebo [KDM](/index.php/KDM "KDM"), zvolte si v nich LXDE v možnostech sezení. Pro spuštění z konzole existují další možnosti.

Pro spuštění příkazem **startx** je nutné nadefinovat LXDE v souboru [`~/.xinitrc`](/index.php/Beginners%27_guide#C:_Test_X "Beginners' guide"):

```
exec startlxde

```

Spuštění LXDE z příkazové řádky bez souboru `~/.xinitrc` (pokud soubor `~/.xinitrc` existuje, nebude to fungovat):

```
$ xinit /usr/bin/startlxde

```

Pokud chcete spustit **startx** automaticky při startu systému, přečtěte si návod [spuštění X při startu systému](/index.php/Start_X_at_login#Starting_X_as_preferred_user_without_logging_in "Start X at login").

## Tipy a opravy chyb

Tipy pro programy LXDE a opravy chyb.

### Programy, spustitelné při startu

	pomocí souborů

	.desktop

Nejdříve nalinkujte soubor `.desktop` konkrétního programu do adresáře `~/.config/autostart/`. Nainstalované programy ukládají svoje soubory `.desktop` do adresáře `/usr/share/applications`. Například:

```
$ ln -s /usr/share/applications/lxterminal.desktop ~/.config/autostart/

```

Jakmile jsou přidané soubory `.desktop`, můžete s nimi manipulovat v grafickém konfiguračním prostředí [lxsession-edit](https://aur.archlinux.org/packages/lxsession-edit/).

	pomocí souboru

	autostart

Druhým způsobem je použít soubor `~/.config/lxsession/LXDE/autostart`.

```
$ touch ~/.config/lxsession/LXDE/autostart

```

Přidejte program, který chcete spustit při startu na nový řádek, začínající znakem _@_ (bez znaku _&_ na konci):

```
@lxterminal
@leafpad

```

	globálním souborem

	autostart

Třetím způsobem je použít globální soubor `/etc/xdg/lxsession/LXDE/autostart`. Tento soubor není skriptem shellu; každý řádek reprezentuje odlišný příkaz, který bude spuštěn. Pokud řádek začíná znakem @, bude příkaz za znakem @ automaticky znovu spuštěn, pokud spadne. Pokud existují oba soubory `~/.config/lxsession/LXDE/autostart` a `/etc/xdg/lxsession/LXDE/autostart`, budou spuštěné všechny položky z obou souborů.

### Nastavení aplletu digitálních hodin

Standardní čas (ne vojenský) se zobrazí formátem hh:mm nebo hh:mm:ss - další parametry viz(`man strftime`):

```
%I:%M
%I:%M:%S

```

### Editace menu aplikací

Menu aplikací funguje tak, že vyhledává soubory s informacemi o jejich spuštění a zařazení do kategorií (soubory `.desktop`) uložené v adresáři `/usr/share/applications`. Mnoho desktopových prostředí spouští programy, které nahrazují tato nastavení z důvodu možnosti úprav menu. LXDE zatím nemá editor aplikačního menu. Menu si samozřejmě můžete upravit podle svého.

Přidat program do menu (nebo editovat položku v menu) lze vytvořením nebo nalinkováním souboru `.desktop` do adresáře `~/.local/share/applications`.

Odstranit program z menu lze editací konkrétního souboru `.desktop` a změnou parametru, který zabrání zobrazování daného programu. Nejdříve zkopírujte konkrétní soubor z globálního adresáře do svého uživatelského.

```
cp /usr/share/applications/example.desktop ~/.local/share/applications

```

Pak do souboru přidejte řádek `NoDisplay=true`. Urychlit tento proces pro větší množství souborů lze vytvořením smyčky. Například:

```
cd /usr/share/applications
for i in program1.desktop program2.desktop ...; do cp /usr/share/applications/$i \
/home/user/.local/share/applications/; echo "NoDisplay=true" >> \
/home/user/.local/share/applications/$i; done
```

Funguje to pro všechny aplikace kromě aplikací KDE. Ty lze z menu odstranit pouze přihlášením do prostředí KDE a použitím jeho menu editoru. Pro každou položku, kterou nechcete zobrazit zvolte volbu 'Zobrazit pouze v KDE'.

### Jméno položky My Documents

Název adresáře 'My Documents' na ploše je natvrdo zakódován v programu pcmanfm. V tuto chvíli jej nelze přejmenovat.

### Nastavení fontů

Většina uživatelů LXDE obvykle používá programy GTK, protože je GTK použito jako pozadí pro LXDE. Hlavní font lze nastavit balíčkem [lxappearance](https://www.archlinux.org/packages/?name=lxappearance) a další fonty pomocí ovládacího panelu z Gnome - 'Nastavení fontů'. Instalace:

```
pacman -S gnome-control-center

```

Po dokončení nastavení můžete programy odinstalovat, nastavení zůstanou zachována.

### Automatické připojování záznamových jednotek

Pokud chcete, aby se přídavné záznamové jednotky samy připojovaly pomocí programu [PCManFM](/index.php/PCManFM "PCManFM"), musíte nainstalovat [HAL](/index.php/HAL "HAL") a přidat svůj uživatelský účet do skupiny hal:

```
# gpasswd -a your_username hal

```

Aby šlo jednotky připojovat bez práv root, je nutné nainstalovat balíček pmount:

```
pacman -S pmount

```

Nyní se odhlašte a znovu přihlašte, aby se zařazení do skupiny hal projevilo.

#### NTFS s čínskými znaky

Pro záznamové jednotky se souborovým systémem NTFS je třeba nainstalovat balíček [NTFS-3G](/index.php/NTFS-3G "NTFS-3G"). Obecně funguje PCManFM dobře, ovšem obsahuje chybu, díky které nedokáže korektně zobrazit znaky jiných znakových sad při použití souborového systému NTFS - tyto znaky mohou při otevření nebo připojení jednotky s NTFS zmizet (např: čínské znaky). Způsobuje to lxsession (nebo lxsession-lite), který nedokáže korektně načíst parametry lokalizace. Existuje řešení:

*   Odstraňte symbolický odkaz "/sbin/mount.ntfs-3g".

```
rm /sbin/mount.ntfs-3g

```

*   Vytvořte nový "/sbin/mount.ntfs-3g" s novým bash skriptem:

```
#!/bin/bash
/bin/ntfs-3g $1 $2 -o locale=en_US.UTF-8

```

*   Nastavte jej jako spustitelný:

```
chmod +x /sbin/mount.ntfs-3g 

```

*   Přidejte "NoUpgrade = sbin/mount.ntfs-3g" do souboru pacman.conf v sekci "[options]"

### LXNM

LXNM je skriptovací program, určený ke správě síťového připojení. Používá skripty a snaží se co nejvíce zautomatizovat konfiguraci sítě. Není to kompletní síťový systém jako [NetworkManager](/index.php/NetworkManager "NetworkManager"). Pokud chcete více možností, [Wicd](/index.php/Wicd "Wicd") a Gnome verze [NetworkManager](/index.php/NetworkManager "NetworkManager") v LXDE fungují výborně. [lxnm](https://aur.archlinux.org/packages/lxnm/) je v repozitáři AUR:

```
yaourt -S lxnm

```

Hlavní skript je nutné spustit jako root. Pokud jej budete chtít používat trvale, vložte jej do souboru `/etc/rc.conf`. LXNM funguje s appletem Network Status Monitor v Lxpanelu, takže si jej na panel přidejte. LXNM většinu času funguje korektně, občas mu může chvilku trvat, než se připojí.

### Sezení LXDE v KDM

Od verze KDE 4.3.3 KDM nerozpozná sezení desktopu LXDE. Změnit to lze příkazem:

```
# cp /usr/share/xsessions/LXDE.desktop /usr/share/apps/kdm/sessions/

```

### lxpanel - přidání programu do launch baru

lxpanel má applet launch bar defaultně aktivovaný, takže do něj stačí přidat nové programy:

1.  Ujistit se, zda je applet launch bar aktivovaný:
    *   1a. kliknout pravým tlačítkem na panel
    *   1b. vybrat "add/remove panel items"
    *   1c. ujistit se, zda je položka "application launch bar" zobrazena (pokud ne, zvolte "add" a přidejte ji)
2.  Kliknout pravým tlačítkem na launch bar applet
3.  Vybrat "application launch bar settings"
4.  Zvolit "add"
5.  Přejít na soubor .desktop aplikace, kterou chcete přidat (v adresáři usr/share/applications)

### lxpanel - přidáni lokace do launch baru

Pro přidání lokace do launch baru - např. harddisku nebo adresáře je třeba vytvořit soubor .desktop a uložit jej do adresáře /usr/share/applications. Nyní jej přidáte stejným způsobem, jako program.

Příklad souboru .desktop, editujte řádky "Exec" a "Icon" dle svých požadavků:

```
[Desktop Entry]
Version=1.0
Encoding=UTF-8
Name=media
Exec=pcmanfm /mnt/xbox (program pcmanfm otevře specifikovanou lokaci - v tomto případě /mnt/xbox)
Icon=xbmc.png (jméno ikony v adresáři /usr/share/pixmaps)
Terminal=false
X-MultipleArgs=false
Type=Application
Categories=Application
StartupNotify=true

```

### Ikony/Kurzory

Nastavení ikon a kurzorů.

#### Kurzory

LXDE nemá program pro nastavení kurzoru myši. Je třeba nadefinovat nový kurzor v souboru `~/.Xdefaults`. Viz [X11_Cursors#Configuring_Cursor_Themes](/index.php/X11_Cursors#Configuring_Cursor_Themes "X11 Cursors").

Nejjednodušším způsobem je přidat kurzor do defaultního tématu. Vytvoříme adresář:

```
mkdir /usr/share/icons/default

```

Přidáme do tématu téma nového kurzoru. Použijeme balíček témat kurzoru [xcursor-bluecurve](https://www.archlinux.org/packages/?name=xcursor-bluecurve):

```
echo '[icon theme]
Inherits=Bluecurve' > /usr/share/icons/default/index.theme

```

#### Ikony pro lxpanel

Defaultní ikony lxpanelu jsou uložené v adresáři `/usr/share/pixmaps` a další ikony, které budete chtít použít se tam musí uložit také.

Defaultní ikony pro aplikace lze změnit takto:

1.  Uložte novou ikonu do adresáře /usr/share/pixmaps
2.  V textovém editoru otevřete soubor .desktop programu, jehož ikonu chcete změnit (soubory .desktop jsou v adresáři /usr/share/applications)
3.  Změňte

```
Icon=/default/icon/.png 

```

na

```
Icon=/name/of/new/icon/added/to/pixmaps/.png

```

#### Ikona My Documents

Položku "My Documents" z plochy nelze odstranit. Je kompilována přímo do programu pcmanfm, v souboru src/desktop/desktop-window.c. Používá ikonu gnome-fs-home v folder-home. Pokud zvolené téma ikon tuto ikonu neobsahuje, musí být vytvořena, jinak nebude s touto položkou žádná ikona asociována.

### Náhrada správce oken

OpenBox, předvolený správce oken pro LXDE, může být snadno nahrazen jakýmkoliv jiným správcem, např. fvwm, icewm, dwm či awesome... atd..

Správce oken pro LXDE je definován v souboru:

	/etc/xdg/lxsession/LXDE/config

Defaultně je nastaveno

```
[Session]
window_manager=openbox-lxde

```

Nahraďte openbox-lxde jiným správcem oken.

Za pozornost ještě stojí soubor:

	/etc/xdg/lxsession/LXDE/default

Toto předvolené nastavení je zavržené, viz tato poznámka:

```
! Tento soubor je zachován z důvodu zpětné kompatibility.
! Používán pouze zastaralým programem lxsession, lxsession-lite jej nepoužívá.

```

Tento soubor /etc/xdg/lxsession/LXDE/default může vypadat takto:

```
smproxy
openbox
lxpanel

```

smproxy je program z xorg. Poskytuje podporu správy sezení pro programy, které neznají protokol správy sezení X11 R6. Je doporučeno tento řádek ve vašem systému použít.

### Vypnutí a restart z LXDE

Aby bylo možné počítač vypnout, restartovat, uspat atd. z lxde, ujistěte se, zda běží DBus a HAL. Přidejte své uživatelské jméno do skupiny power.

```
# gpasswd -a <USERNAME> power

```

Pokud problémy přetrvávají, přidejte mezi tagy <config></config> v souboru /etc/PolicyKit/PolicyKit.conf následující řádky:

```
<match action="org.freedesktop.hal.power-management.shutdown">
 <return result="yes"/>
</match>
<match action="org.freedesktop.hal.power-management.reboot">
 <return result="yes"/>
</match>
<match action="org.freedesktop.hal.power-management.suspend">
 <return result="yes"/>
</match>
<match action="org.freedesktop.hal.power-management.hibernate">
 <return result="yes"/>
</match>

```

Potom restartujte HAL.

Nebo přidejte do souboru /etc/dbus-1/system.d/hal.conf:

```
<policy group="power">
   <allow send_destination="org.freedesktop.Hal"
   	   send_interface="org.freedesktop.Hal.Device.SystemPowerManagement"/>
</policy>

```

Potom restartujte HAL.

### Problémy po upgradu lxsession na verzi 0.4.1

Po spuštění programu GTK2 se objeví chyba:

```
 GTK+ icon them is not properly set

```

```
 Znamená to, že neběží správce XSETTINGS. Desktopová prostředí jako je GNOME či XFCE automaticky spouští 
 své správce XSETTING, např. gnome-settings-daemon či xfce-mcs-manager.

```

Konfigurační soubory lxde-settings-daemon byly nedávno spojeny s lxsession. Pokud je upravujete, musíte spojit tyto konfigurační soubory:

```
 /usr/share/lxde/config
 ~/.config/lxde/config

```

do

```
 etc/xdg/lxsession/LXDE/desktop.conf
 ~/.config/lxsession/LXDE/desktop.conf

```

Pro opravu také můžete použít balíček lxappearance z repozitáře community.

### LXsession - plná verze

V lxsession je několik chyb v souvislosti se správou sezení. _**lxsession-lite**_ je verzí lxsession, která neobsahuje možnost správy sezení. lxsession-lite je stabilnější než lxsession, pouze nedokáže ukládat a obnovovat sezení. Je doporučeno použít _**lxsession-lite**_, dokud nebudou chyby v lxsession odstraněny.

### Použití aplikací KDEmod3 v LXDE

Starší verze programů KDEmod[-legacy] nainstalované v /opt/kde/bin nejsou automaticky LXDE rozpoznané. Aby šly použít, je třeba editovat cestu PATH následujícím způsobem:

```
echo 'PATH=$PATH:/opt/kde/bin' >> /etc/rc.local

```

nebo přidejte do souboru /etc/profile.d skript:

```
#!/bin/sh
PATH=$PATH:/opt/kde/bin

```

Uložte jej pod názvem "kde3path.sh" a nastavte jako spustitelný:

```
chmod +x /etc/profile.d/kde3path.sh

```

## Zdroje

*   [LXDE wiki článek, věnovaný Arch Linuxu](http://wiki.lxde.org/en/ArchLinux)
*   [LXDE projekt](http://lxde.sourceforge.net)
*   [LXDE fórum](http://forum.lxde.org)
*   [Nejnovější LX... balíčky](https://sourceforge.net/project/showfiles.php?group_id=180858)
*   [Správce souborů PCMan](https://sourceforge.net/project/showfiles.php?group_id=156956)