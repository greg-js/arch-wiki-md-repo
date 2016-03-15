[SLiM](http://slim.berlios.de/) je zkratka, vytvořená ze slov Simple Login Manager. SLiM je jednoduchý, odlehčený a snadno konfigurovatelný. SLiM je často používán, protože nemá závislosti na [GNOME](/index.php/GNOME "GNOME") nebo [KDE](/index.php/KDE "KDE") a může se uživatelům hodit při stavbě odlehčeného systému, například [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox") či [Fluxbox](/index.php/Fluxbox "Fluxbox").

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 SLiM - spuštění](#SLiM_-_spu.C5.A1t.C4.9Bn.C3.AD)
    *   [2.2 Jednotlivá desktopová prostředí](#Jednotliv.C3.A1_desktopov.C3.A1_prost.C5.99ed.C3.AD)
    *   [2.3 Automatické přihlašování](#Automatick.C3.A9_p.C5.99ihla.C5.A1ov.C3.A1n.C3.AD)
    *   [2.4 Více desktopových prostředí](#V.C3.ADce_desktopov.C3.BDch_prost.C5.99ed.C3.AD)
    *   [2.5 Témata](#T.C3.A9mata)
        *   [2.5.1 Nastavení obrazovky](#Nastaven.C3.AD_obrazovky)
*   [3 Další nastavení](#Dal.C5.A1.C3.AD_nastaven.C3.AD)
    *   [3.1 Změna kurzoru](#Zm.C4.9Bna_kurzoru)
    *   [3.2 Sdílení wallpaperu mezi SLiMem a pracovním prostředím](#Sd.C3.ADlen.C3.AD_wallpaperu_mezi_SLiMem_a_pracovn.C3.ADm_prost.C5.99ed.C3.ADm)
    *   [3.3 Vypnout, restartovat, uspat, ukončit, spustit terminál ze SLiMu](#Vypnout.2C_restartovat.2C_uspat.2C_ukon.C4.8Dit.2C_spustit_termin.C3.A1l_ze_SLiMu)
    *   [3.4 Chyba vypnutí při současném použití Splashy](#Chyba_vypnut.C3.AD_p.C5.99i_sou.C4.8Dasn.C3.A9m_pou.C5.BEit.C3.AD_Splashy)
    *   [3.5 Přihlašovací informace SLiMu](#P.C5.99ihla.C5.A1ovac.C3.AD_informace_SLiMu)
    *   [3.6 SLiM a klíčenka v Gnome](#SLiM_a_kl.C3.AD.C4.8Denka_v_Gnome)
    *   [3.7 Nastavení DPI pro SLiM](#Nastaven.C3.AD_DPI_pro_SLiM)
    *   [3.8 Použití náhodného tématu](#Pou.C5.BEit.C3.AD_n.C3.A1hodn.C3.A9ho_t.C3.A9matu)
*   [4 Zdroje](#Zdroje)

## Instalace

SLiM instalujeme z repozitáře **extra**:

```
# pacman -S slim

```

## Konfigurace

### SLiM - spuštění

SLiM může být po startu spuštěn jako daemon vložením do souboru `rc.conf` nebo modifikací `inittab`. Podrobnosti jsou v sekci [Display manager](/index.php/Display_manager "Display manager").

### Jednotlivá desktopová prostředí

SLiM lze nastavit pro spouštění jednotlivých desktopových prostředí editací souboru `~/.xinitrc`:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Spouštěno programem startx (spustí vaše desktopové prostředí)
#

exec [session-command]

```

Změňte `[session-command]` odpovídajícím parametrem. Zde jsou příklady parametrů pro spuštění některých desktopových prostředí:

```
exec awesome
exec fluxbox
exec fvwm2
exec gnome-session
exec openbox-session
exec startkde
exec startlxde
exec startxfce4

```

Pokud zde není vaše desktopové prostředí uvedeno, vyhledejte si jej na jeho wiki stránce.

### Automatické přihlašování

Automatické přihlašování pomocí SLiMu pod konkrétním uživatelským jménem (bez nutnosti zadat heslo) lze nastavit v souboru /etc/slim.conf na řádku:

```
# default_user        simone

```

Tento řádek odkomentujte, změňte jméno "simone" na jméno uživatele, který se bude automaticky přihlašovat.

```
# auto_login          no

```

Tento řádek odkomentujte a změňte 'no' na 'yes'. Toto povolí automatické přihlašování.

### Více desktopových prostředí

Aby šlo vybírat z více desktopových prostředí, je nutno SLiM nastavit tak, aby umožnil uživateli konkrétní prostředí při přihlašování vybrat.

Vložte do souboru `~/.xinitrc` parametry podle vzoru uvedeného níže a nastavte proměnné v souboru `/etc/slim.conf` tak, aby jména spouštěčů navzájem odpovídala. Desktopové prostředí při přihlašování zvolíte stiskem klávesy F1\. Tato funkce je zatím experimentální.

```
# Následující parametry definují prostředí, které bude spuštěno, pokud si uživatel nezvolí jiné
# Source: http://svn.berlios.de/svnroot/repos/slim/trunk/xinitrc.sample

DEFAULT_SESSION=twm

case $1 in
kde)
	exec startkde
	;;
xfce4)
	exec startxfce4
	;;
icewm)
	icewmbg &
	icewmtray &
	exec icewm
	;;
wmaker)
	exec wmaker
	;;
blackbox)
	exec blackbox
	;;
*)
	exec $DEFAULT_SESSION
	;;
esac

```

### Témata

Můžete si nainstalovat balíček témat [slim-themes](https://www.archlinux.org/packages/?name=slim-themes):

```
# pacman -S slim-themes archlinux-themes-slim

```

Balíček [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) obsahuje několik odlišných témat. Dostupná témata jsou v adresáři `/usr/share/slim/themes`. Název vybraného tématu vložte jako parametr na řádek 'current_theme' v souboru `/etc/slim.conf`:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Náhled tématu, pokud neběží Xorg server, lze provést takto:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

Ukončení: zadejte příkaz "exit" na řádek Login a stiskněte Enter.

Další témata jsou dostupná v repozitáři [AUR](/index.php/AUR "AUR").

#### Nastavení obrazovky

Lze změnit parametry tématu - např. velikost panelu 450 krát 250 bodů v procentech v souboru /usr/share/slim/themes/<your-theme>/slim.theme:

```
input_panel_x           50%
input_panel_y           50%

```

na hodnoty v bodech:

```
# Tyto parametry nastaví panel "archlinux-simplyblack" na střed obrazovky 1440x900
input_panel_x           495
input_panel_y           325

```

```
# Tyto parametry nastaví panel "archlinux-retro" na střed obrazovky 1680x1050
input_panel_x           615
input_panel_y           400

```

Pokud vaše téma obsahuje obrázek pozadí, lze změnit parametr background_style na ('stretch', 'tile', 'center' nebo 'color') tak, aby se obrázek zobrazoval korektně. Další podrobnosti jsou uvedeny zde: [velmi přehledná a jednoduchá oficiální dokumentace k tématům SLiMu](http://slim.berlios.de/themes_howto.php).

## Další nastavení

Několik věcí, které můžete chtít vyzkoušet.

### Změna kurzoru

Pokud chcete změnit předvolený X kurzor na novější design, existuje balíček [slim-cursor](https://aur.archlinux.org/packages/slim-cursor/).

Po instalaci editujte soubor `/etc/slim.conf` a odkomentujte řádek:

```
cursor   left_ptr

```

Kurzor se změní na běžný tvar šipky. Toto nastavení je postoupeno příkazu `xsetroot -cursor_name`. Dostupné názvy kurzorů můžete najít [zde](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) nebo v `/usr/share/icons/<your-cursor-theme>/cursors/`.

Téma kurzoru na přihlašovací obrazovce lze změnit vytvořením souboru `/usr/share/icons/default/index.theme` s tímto obsahem:

```
[Icon Theme]
Inherits=<your-cursor-theme>

```

Změňte parametr <your-cursor-theme> na jméno tématu kurzoru, které chcete použít (např. whiteglass).

### Sdílení wallpaperu mezi SLiMem a pracovním prostředím

Pro sdílení wallpaperu mezi SLiMem a vaším pracovním prostředím přejmenujte aktuální obrázek SLiMu a vytvořte symbolický odkaz na soubor obrázku vašeho pracovního prostředí:

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Vypnout, restartovat, uspat, ukončit, spustit terminál ze SLiMu

Můžete vypnout, restartovat, uspat, ukončit nebo dokonce spustit terminál z přihlašovací obrazovky SLiMu. Příkazy zadávejte jako uživatelské jméno a heslo roota do pole heslo:

*   Pro spuštění terminálu zadejte příkaz **console** jako uživatelské jméno (předvolený je terminál xterm, který musí být nainstalován zvlášť. Terminál lze změnit v soboru `/etc/slim.conf`)
*   Pro vypnutí zadejte příkaz **halt** jako uživatelské jméno
*   Pro restart zadejte příkaz **reboot** jako uživatelské jméno
*   Pro ukončení do bashe zadejte příkaz **exit** jako uživatelské jméno
*   Pro uspání zadejte příkaz **suspend** jako uživatelské jméno (uspání je defaultně zakázáno, editujte jako root soubor `/etc/slim.conf` a odkomentujte řádek `suspend_cmd` a pokud bude třeba, změňte příkaz pro uspání (např. změňte `/usr/sbin/suspend` na `sudo /usr/sbin/pm-suspend`))

### Chyba vypnutí při současném použití Splashy

Pokud používáte Splashy a SLiM dohromady, občas nelze PC vypnout či restartovat z menu GNOME, Xfce, LXDE atd. Zkontrolujte v souborech `/etc/slim.conf` a `/etc/splash.conf` hodnotu parametrů DEFAULT_TTY=7 a xserver_arguments vt07.

### Přihlašovací informace SLiMu

Standardně SLiM selhává při ukládání logů do utmp a wtmp, což způsobuje, že who, last atd. nesprávně hlásí přihlašovací informace. Opravit to lze následujícími úpravami souboru `slim.conf`:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### SLiM a klíčenka v Gnome

Pokud používáte SLiM ke spouštění prostředí Gnome a máte problémy s přístupem ke klíčence, např. nejste automaticky ověřeni při přihlašování, přidejte následující řádky do souboru /etc/pam.d/slim (diskuze je zde: [[1]](https://bugs.archlinux.org/task/18637)).

```
auth		optional	pam_gnome_keyring.so
session		optional	pam_gnome_keyring.so	auto_start

```

### Nastavení DPI pro SLiM

Xorg server zpravidla nastaví DPI sám, ovšem pokud selže, můžete je pro SLiM specifikovat sami. Nastavení DPI s argumentem -dpi 96 v souboru `/etc/X11/xinit/xserverrc` nebude ve SLiMu fungovat. Je nutné změnit v souboru `slim.conf` parametr:

```
 xserver_arguments   -nolisten tcp vt07 

```

na

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### Použití náhodného tématu

Zapište do proměnné current_theme jména témat, oddělená čárkami. Téma bude náhodně vybráno.

## Zdroje

*   [SLiM homepage](http://slim.berlios.de/)
*   [SLiM dokumentace](http://slim.berlios.de/manual.php)