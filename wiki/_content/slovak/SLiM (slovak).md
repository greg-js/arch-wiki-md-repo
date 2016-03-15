[SLiM](http://slim.berlios.de/) je skratka, vytvorená zo slov Simple Login Manager. SLiM je jednoduchý, odlahčený a lahko konfigurovatelný. SLiM je často používaný, pretože nemá závislosti na [GNOME](/index.php/GNOME "GNOME") alebo [KDE](/index.php/KDE "KDE") a môže sa uživatelom hodit pri stavbe odlahčeného systému, napríklad [Xfce](/index.php/Xfce "Xfce"), [Openbox](/index.php/Openbox "Openbox") či [Fluxbox](/index.php/Fluxbox "Fluxbox").

## Contents

*   [1 Inštalácia](#In.C5.A1tal.C3.A1cia)
*   [2 Konfigurácia](#Konfigur.C3.A1cia)
    *   [2.1 SLiM - spustenie](#SLiM_-_spustenie)
    *   [2.2 Jednotlivé desktopové prostredia](#Jednotliv.C3.A9_desktopov.C3.A9_prostredia)
    *   [2.3 Automatické prihlasovanie](#Automatick.C3.A9_prihlasovanie)
    *   [2.4 Viac desktopových prostredí](#Viac_desktopov.C3.BDch_prostred.C3.AD)
    *   [2.5 Témy](#T.C3.A9my)
        *   [2.5.1 Nastavenie obrazovky](#Nastavenie_obrazovky)
*   [3 Dalšie nastavenia](#Dal.C5.A1ie_nastavenia)
    *   [3.1 Zmena kurzora](#Zmena_kurzora)
    *   [3.2 Zdielanie wallpaperu medzi SLiMom a pracovným prostredím](#Zdielanie_wallpaperu_medzi_SLiMom_a_pracovn.C3.BDm_prostred.C3.ADm)
    *   [3.3 Vypnúť, reštartovať, uspať, ukončiť, spustiť terminál zo SLiMu](#Vypn.C3.BA.C5.A5.2C_re.C5.A1tartova.C5.A5.2C_uspa.C5.A5.2C_ukon.C4.8Di.C5.A5.2C_spusti.C5.A5_termin.C3.A1l_zo_SLiMu)
    *   [3.4 Chyba vypnutia pri súčasnom použití Splashy](#Chyba_vypnutia_pri_s.C3.BA.C4.8Dasnom_pou.C5.BEit.C3.AD_Splashy)
    *   [3.5 Prihlasovacie informácie SLiMu](#Prihlasovacie_inform.C3.A1cie_SLiMu)
    *   [3.6 SLiM a klúčenka v Gnome](#SLiM_a_kl.C3.BA.C4.8Denka_v_Gnome)
    *   [3.7 Nastavenie DPI pre SLiM](#Nastavenie_DPI_pre_SLiM)
    *   [3.8 Použitie náhodnej témy](#Pou.C5.BEitie_n.C3.A1hodnej_t.C3.A9my)
*   [4 Zdroje](#Zdroje)

## Inštalácia

SLiM inštalujeme z repozitára **extra**:

```
# pacman -S slim

```

## Konfigurácia

### SLiM - spustenie

SLiM môže byť po štarte spustený ako daemon vloženým do suboru `rc.conf` alebo modifikaciou `inittab`. Podrobnosti su v sekcií [Display manager](/index.php/Display_manager "Display manager").

### Jednotlivé desktopové prostredia

SLiM môžme nastavit pre spustenie jednotlivých desktopových prostredí editaciou suboru `~/.xinitrc`:

```
#!/bin/sh

#
# ~/.xinitrc
#
# Spustené programom startx (spustí vaše desktopové prostredie)
#

exec [session-command]

```

SLiM načíta miestnu konfiguráciu zo súboru `~/.xinitrc` a spustí podla v nom vložených parametrov konkrétne desktopové prostredie. See also [Xinitrc](/index.php/Xinitrc "Xinitrc").

Zmeňte `[session-command]` odpovedajúcím parametrom. Tu sú príklady parametrov pre spustenie niektorých desktopových prostredí:

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

Pokial tu neni vaše desktopové prostredie uvedené, vyhladajte si ho na jeho wiki stránke.

### Automatické prihlasovanie

Automatické prihlasovanie pomocou SLiMu pod konkrétnym uživatelským menom (bez nutnosti zadat heslo) je možné nastaviť v súbore /etc/slim.conf na riadku:

```
# default_user        simone

```

Tento riadok odkomentujte, zmente meno "simone" na meno uživatela, ktorý sa bude automaticky prihlasovať.

```
# auto_login          no

```

Tento riadok odkomentujte a zmeňte 'no' na 'yes'. Toto povoli automatické prihlasovanie.

### Viac desktopových prostredí

Aby šlo vyberať z viac desktopových prostredí, je nutné SLiM nastaviť tak, aby umožnil uživatelovi konkrétne prostredie pri prihlasovaní vybrať.

Vložte do súboru `~/.xinitrc` parametre podla vzoru uvedeného nižšie a nastavte premenné v súbore `/etc/slim.conf` tak, aby mená spúštačov navzájom odpovedali. Desktopové prostredie pri prihlasovaní zvolíte stlačením klávesy F1\. Táto funkcia je zatial experimentálna.

```
# Nasledujúce parametre definujú prostredie, ktoré bude spustené, pokial si uživatel nezvolí iné
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

### Témy

Môžete si nainstalovať balíček tém [slim-themes](https://www.archlinux.org/packages/?name=slim-themes):

```
# pacman -S slim-themes archlinux-themes-slim

```

Balíček [archlinux-themes-slim](https://www.archlinux.org/packages/?name=archlinux-themes-slim) obsahuje niekolko odlišných tém. Dostupné témy sú v adresári `/usr/share/slim/themes`. Názov vybranej témy vložte ako parameter na riadok 'current_theme' v súbore `/etc/slim.conf`:

```
#current_theme       default
current_theme       archlinux-simplyblack

```

Náhlad témy, pokial nebeží Xorg server, môžte spraviť takto:

```
$ slim -p /usr/share/slim/themes/<theme name>

```

Ukončenie: zadajte príkaz "exit" na riadok Login a stlačte Enter.

Dalšie témy sú dostupné v repozitári [AUR](/index.php/AUR "AUR").

#### Nastavenie obrazovky

Môžte zmeniť parametre témy - napr. velkosť panela 450 krát 250 bodov v percentách v súbore /usr/share/slim/themes/<your-theme>/slim.theme:

```
input_panel_x           50%
input_panel_y           50%

```

na hodnoty v bodoch:

```
# Tieto parametre nastavia panel "archlinux-simplyblack" na stred obrazovky 1440x900
input_panel_x           495
input_panel_y           325

```

```
# Tieto parametre nastavia panel "archlinux-retro" na stred obrazovky 1680x1050
input_panel_x           615
input_panel_y           400

```

Pokial vaša téma obsahuje obrázok pozadia, môžte zmeniť parameter background_style na ('stretch', 'tile', 'center' nebo 'color') tak, aby sa obrázok zobrazoval korektne. Dalšie podrobnosti sú uvedené tu: [velmi prehladná a jednoduchá oficiálna dokumentácia k témam SLiMu](http://slim.berlios.de/themes_howto.php).

## Dalšie nastavenia

Niekolko vecí, ktoré môžete chcieť vyskúšať.

### Zmena kurzora

Po inštalácií editujte súbor `/etc/slim.conf` a odkomentujte riadok:

```
cursor   left_ptr

```

Kurzor sa zmení na bežný tvar šípky. Toto nastavenie je postúpené príkazu `xsetroot -cursor_name`. Dostupné názvy kurzorov môžete nájsť [tu](http://cvsweb.xfree86.org/cvsweb/*checkout*/xc/lib/X11/cursorfont.h?rev=HEAD&content-type=text/plain) alebo v `/usr/share/icons/<your-cursor-theme>/cursors/`.

Tému kurzora na prihlasovacej obrazovke môžte zmeniť vytvorením súbora `/usr/share/icons/default/index.theme` s týmto obsahom:

```
[Icon Theme]
Inherits=<your-cursor-theme>

```

Zmeňte parameter <your-cursor-theme> na meno témy kurzora, ktoré chcete použiť (napr. whiteglass).

### Zdielanie wallpaperu medzi SLiMom a pracovným prostredím

Pre zdielanie wallpaperu medzi SLiMom a vaším pracovným prostredím premenujte aktuálny obrázok SLiMu a vytvorte symbolický odkaz na súbor obrázku vášho pracovného prostredia:

```
# mv /usr/share/slim/themes/default/background.jpg{,.bck}
# ln -s /path/to/mywallpaper.jpg /usr/share/slim/themes/default/background.jpg

```

### Vypnúť, reštartovať, uspať, ukončiť, spustiť terminál zo SLiMu

Môžete vypnúť, reštartovať, uspať, ukončiť alebo dokonca spustiť terminál z prihlasovacej obrazovky SLiMu. Príkazy zadávajte ako uživatelské meno a heslo roota do pola heslo:

*   Pre spustenie terminálu zadajte príkaz **console** ako uživatelské meno (predvolený je terminál xterm, ktorý musí byť nainštalovaný zvlášť. Terminál je možné zmenit v súbore `/etc/slim.conf`)
*   Pre vypnutie zadajte príkaz **halt** ako uživatelské meno
*   Pre reštart zadajte príkaz **reboot** ako uživatelské meno
*   Pre ukončenie do bashe zadajte príkaz **exit** ako uživatelské meno
*   Pre uspanie zadajte príkaz **suspend** ako uživatelské meno (uspanie je defaultne zakázané, editujte ako root súbor `/etc/slim.conf` a odkomentujte riadok `suspend_cmd` a pokial bude treba, zmente príkaz pre uspanie (napr. zmente `/usr/sbin/suspend` na `sudo /usr/sbin/pm-suspend`))

### Chyba vypnutia pri súčasnom použití Splashy

Pokial používate Splashy a SLiM dohromady, občas nejde PC vypnúť či reštartovať z menu GNOME, Xfce, LXDE atd. Skontrolujte v súboroch `/etc/slim.conf` a `/etc/splash.conf` hodnotu parametrov DEFAULT_TTY=7 a xserver_arguments vt07.

### Prihlasovacie informácie SLiMu

Štandardne SLiM zlyháva pri ukladaní logov do utmp a wtmp, čo spôsobuje, že who, last atd. nesprávne hlásia prihlasovacie informácie. Opraviť to môžte nasledujúcími úpravami súboru `slim.conf`:

```
 sessionstart_cmd    /usr/bin/sessreg -a -l $DISPLAY %user
 sessionstop_cmd     /usr/bin/sessreg -d -l $DISPLAY %user

```

### SLiM a klúčenka v Gnome

Pokial používate SLiM ku spustení prostredia Gnome a máte problémy s prístupom ku klúčenke, napr. nieste automaticky overený pri prihlasovaní, pridajte nasledujúce riadky do súbora /etc/pam.d/slim (diskuze je zde: [[1]](https://bugs.archlinux.org/task/18637)).

```
auth		optional	pam_gnome_keyring.so
session		optional	pam_gnome_keyring.so	auto_start

```

### Nastavenie DPI pre SLiM

Xorg server spravidla nastaví DPI sám, ale pokial zlyhá, môžete je pre SLiM špecifikovať sami. Nastavenie DPI s argumentom -dpi 96 v súbore `/etc/X11/xinit/xserverrc` nebude v SLiMe fungovať. Je nutné zmeniť v súbore `slim.conf` parameter:

```
 xserver_arguments   -nolisten tcp vt07 

```

na

```
 xserver_arguments   -nolisten tcp vt07 -dpi 96

```

### Použitie náhodnej témy

Zapište do premennej current_theme mená tém, oddelené čiarkami. Téma bude náhodne vybraná.

## Zdroje

*   [SLiM homepage](http://slim.berlios.de/)
*   [SLiM dokumentácia](http://slim.berlios.de/manual.php)