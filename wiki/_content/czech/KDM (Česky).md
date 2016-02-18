## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
*   [3 Konfigurace](#Konfigurace)
    *   [3.1 Témata](#T.C3.A9mata)
    *   [3.2 Tvorba témat](#Tvorba_t.C3.A9mat)
    *   [3.3 kdmrc](#kdmrc)
        *   [3.3.1 ServerArgsLocal](#ServerArgsLocal)
        *   [3.3.2 SessionsDirs](#SessionsDirs)
        *   [3.3.3 Session](#Session)
*   [4 Problémy](#Probl.C3.A9my)
    *   [4.1 Mapování klávesnice](#Mapov.C3.A1n.C3.AD_kl.C3.A1vesnice)

# Úvod

KDM (KDE Display Manager) je přihlašovací manažer pro KDE. Podporuje témata, automatické logování, výběr typu sezení atd.

# Instalace

*Instalační instrukce viz [Display manager](/index.php/Display_manager "Display manager").*

# Konfigurace

KDM může být konfigurováno přímo z programu KDE System Settings, ovšem je třeba spustit jej jako root:

*   v KDEMod se automaticky zeptá na heslo roota
*   v KDE můžete použít kdesu:

```
$ `kdesu systemsettings`

```

## Témata

Témata Archlinux KDM mohou být instalována takto:

```
# pacman -S archlinux-themes-kdm

```

Mnoho dalších témat KDM 4 je dostupných na [http://kde-look.org/index.php?xcontentmode=41](http://kde-look.org/index.php?xcontentmode=41). Témata lze zvolit v programu KDE System Settings (spuštěném jako root), jak je popsáno výše.

## Tvorba témat

Soubory témat jsou v adresáři `/usr/share/apps/kdm/themes`.

Formát témat je stejný jako pro GDM, dokumentace je zde: [Detailní popis XML formátu témat](http://projects.gnome.org//gdm/docs/2.18/thememanual.html#descofthemeformat).

## kdmrc

Hlavní konfigurační soubor je v `/usr/share/config/kdm/kdmrc`. Defaultní soubor obsahuje kompletní popis funkcí každé položky.

### ServerArgsLocal

K potlačení počtu DPI z X serveru přidejte parametr -dpi do ServerArgsLocal. Běžně užívaná hodnota je 96 DPI.

```
ServerArgsLocal=-dpi 96 -nolisten tcp

```

### SessionsDirs

Tato proměnná obsahuje seznam adresářů obsahujících definice typů sezení v `.desktop` formátu, seřazených podle sestupné priority. V Arch Linuxu někteří [správci oken](/index.php/Window_manager "Window manager") instalují takové soubory do `/etc/X11/sessions` nebo do `/usr/share/xsessions`. Přidejte je do seznamu v pořadí, v jakém budou dostupné v KDM.

```
SessionsDirs=/usr/share/config/kdm/sessions,/usr/share/apps/kdm/sessions,/etc/X11/sessions,/usr/share/xsessions

```

### Session

V proměnné Session je jméno programu, který je spuštěn pod přihlášeným uživatelem. Očekává se interpretace parametrů sezení (viz SessionsDirs) a spuštění požadovaným způsobem. Někdo si tento parametr může přát upravit pro sezení správce oken, např. pro nastavení wallpaperu a spuštění šetřiče. Udělat to způsobem, který přežije aktualizace pacmana (zničí soubor Xsession) lze následovně:

```
cp /usr/share/config/kdm/Xsession /usr/share/config/kdm/Xsession.custom

```

V kdmrc nastavte

```
Session=/usr/share/config/kdm/Xsession.custom

```

A pak editujte požadovaným způsobem Xsession.custom

# Problémy

## Mapování klávesnice

Klávesnice v KDM je závislá na Xorg. Změnu je třeba nastavit v souboru xorg.conf.

*Viz instrukce [v článku Xorg](/index.php/Xorg#Keyboard_settings "Xorg").*