[OpenOffice](http://www.openoffice.org/) je významný open-source kancelářský balík, určený pro zpracování textu, tabulek, prezentací, grafiky, databází atd.

## Contents

*   [1 OpenOffice v Arch Linuxu](#OpenOffice_v_Arch_Linuxu)
*   [2 Instalace](#Instalace)
    *   [2.1 Správa rozšíření a kontrola pravopisu pro OpenOffice 3.x](#Spr.C3.A1va_roz.C5.A1.C3.AD.C5.99en.C3.AD_a_kontrola_pravopisu_pro_OpenOffice_3.x)
        *   [2.1.1 Další standardně nainstalovaná rozšíření](#Dal.C5.A1.C3.AD_standardn.C4.9B_nainstalovan.C3.A1_roz.C5.A1.C3.AD.C5.99en.C3.AD)
    *   [2.2 Nastavení prostředí OOo](#Nastaven.C3.AD_prost.C5.99ed.C3.AD_OOo)
        *   [2.2.1 Globální konfigurace prostředí OOo](#Glob.C3.A1ln.C3.AD_konfigurace_prost.C5.99ed.C3.AD_OOo)
        *   [2.2.2 Skripty pro nastavení prostředí OOo](#Skripty_pro_nastaven.C3.AD_prost.C5.99ed.C3.AD_OOo)
    *   [2.3 Vzhled a chování KDE4 pro OpenOffice](#Vzhled_a_chov.C3.A1n.C3.AD_KDE4_pro_OpenOffice)
        *   [2.3.1 Alternativní konfigurace](#Alternativn.C3.AD_konfigurace)
*   [3 Spouštění OpenOffice](#Spou.C5.A1t.C4.9Bn.C3.AD_OpenOffice)
*   [4 Zrychlení OpenOffice](#Zrychlen.C3.AD_OpenOffice)
*   [5 Problémy](#Probl.C3.A9my)
    *   [5.1 Náhrada fontů](#N.C3.A1hrada_font.C5.AF)
    *   [5.2 Vyhlazování](#Vyhlazov.C3.A1n.C3.AD)
    *   [5.3 Detekce TrueType fonů](#Detekce_TrueType_fon.C5.AF)
    *   [5.4 Qt vzhled v KDE >4](#Qt_vzhled_v_KDE_.3E4)
    *   [5.5 Francouzský slovník](#Francouzsk.C3.BD_slovn.C3.ADk)
    *   [5.6 Tmavá GTK témata a gtk-qt-engine](#Tmav.C3.A1_GTK_t.C3.A9mata_a_gtk-qt-engine)

## OpenOffice v Arch Linuxu

Arch nabízí 4 druhy binárních balíčků pro OpenOffice s těmito názvy:

**openoffice-base**

Toto je vždy poslední vydaná, stabilní verze OpenOffice.
Současná verze: 3.2.0
Spouští se příkazem "soffice" nebo z menu desktopu.

**openoffice-base-beta**

Tento balíček existuje pouze v případě, kdy se blíží nová stabilní verze. Bude to verze alpha, beta a release candidate nejbližší stabilní verze.
Současná verze: 3.2.0_ooo320_m12-1 (cesta k=3.1.1rcX) (verze z větve DEV320_m12 povedou k další stabilní verzi 3.2.x)
Spouští se příkazem "soffice-beta" nebo z menu desktopu.
Je bezpečné, pokud se nainstaluje dohromady se stabilní i vývojovou verzí.
Prosím důkladně ji otestujte, chyby hlaste do OpenOffice a chyby balíčků do Archu.
Mapa vývoje: [http://wiki.services.openoffice.org/wiki/OOoRelease311](http://wiki.services.openoffice.org/wiki/OOoRelease311)

**openoffice-base-devel**

Tento balíček je aktualizován čas od času a je určen k testování posledních novinek a sestavení balíčků. Prosím otestujte jej a připomínky hlaste na [http://www.openoffice.org/issues/query.cgi](http://www.openoffice.org/issues/query.cgi)
Současná verze: 3.3_dev300_m70-1 / snímek DEV300_m70 (snímky ze stabilní větve 3.2 povedou k vydání verze 3.3 a dalším)
Spouští se příkazem "soffice-dev" nebo z menu desktopu.
Je bezpečné, pokud se nainstaluje dohromady se stabilní i beta verzí.
Mapa vývoje: [http://wiki.services.openoffice.org/wiki/OOoRelease33](http://wiki.services.openoffice.org/wiki/OOoRelease33)

**go-openoffice**

Jako doplněk existuje balíček pro go-openoffice, také nazývaný ooo-build - "větev Novell" v repozitáři extra, který obsahuje rozšíření a funkce, známé z verzí openoffice.org dostupných v Ubuntu, OpenSuSE a dalších distribucích. Pro uživatele Archu, kteří přišli z jiných distribucí může být go-openoffice mnohem známější. Vždy to je poslední stabilní verze v repozitáři extra, vycházející z balíčku openoffice-base. Budoucí beta/vývojové verze jsou v repozitáři testing.
go-openoffice nemůže být instalován souběžně s ostatními větvemi openoffice; berte ho jako náhradu.

**Note:** Pokud používáte více než jednu verzi openoffice-base, je důrazně doporučeno vždy zálohovat konfigurační adresář ~/.openoffice{2,3}.

## Instalace

*   Nejdříve nainstalujte prostředí Java Runtime Environment (volitelné, důrazně doporučeno). Viz: [Java](/index.php/Java "Java")

*   Dále nainstalujte tyto fonty, nebo se budou zobrazovat místo písma jen obdélníčky:

```
# pacman -S ttf-dejavu artwiz-fonts ttf-ms-fonts (a další, potřebné pro váš jazyk)

```

*   Nainstalujte si stabilní, beta, vývojovou či go-o verzi:

```
# pacman -S openoffice-base openoffice-base-beta openoffice-base-devel go-openoffice

```

*   Stáhněte si jazykový balíček. Základní instalace obsahuje pouze soubory s jazykem en_US, ovšem repozitáře nabízí všechny dostupné jazykové balíčky, s výjimkou pro go-openoffice.

```
# pacman -S openoffice-cs...

```

### Správa rozšíření a kontrola pravopisu pro OpenOffice 3.x

Balíčky v Archu již obsahují některé slovníky. Zkuste pomocí Správce rozšíření, zda je váš slovník k dispozici - spusťte libovolný OO program (např. Writer) a otevřete Správce rozšíření z menu Nástroje. Sem zadejte následující cestu k instalaci slovníku:

```
/usr/lib/openoffice/share/extension/install/

```

**Note:** Pokud instalujete go-openoffice, cesta je: /usr/lib/go-openoffice/share/extension/install/

Existují další způsoby:

*   1) Použijte pro stáhnutí a instalaci Správce rozšíření z menu OOo - rozšíření nainstaluje pouze pro konkrétního uživatele do jeho adresáře ~/.openoffice.org/3/user/uno_packages/cache
*   2) Stáhněte rozšíření a instalujte ho pro konkrétního uživatele použitím programu "/usr/lib/openoffice/program/unopkg add extension" nebo
*   3) Stáhněte rozšíření a instalujte ho pro všechny uživatele použitím programu "/usr/lib/openoffice/program/unopkg add --shared extension" (vyžaduje práva root)

##### Další standardně nainstalovaná rozšíření

(Seznam je platný pro go-openoffice)

*   pdfimport.oxt: schopnost importovat soubory PDF do Draw a Impress
*   presenter-screen.oxt: při použití dvou obrazovek tento plugin nabízí větší kontrolu nad prezentací
*   sun-presentation-minimizer.oxt: redukuje velikost souboru konkrétní prezentace
*   wiki-publisher.oxt: umožňuje vytvářet Wiki články na servery MediaWiki bez znalosti syntaxe jazyka MediaWiki

### Nastavení prostředí OOo

OpenOffice podporuje použití několika vykreslovacích nástrojů a dokáže se čistě integrovat do rozličných desktopových prostředí. Ručně je nutno zadat proměnnou OOO_FORCE_DESKTOP.

Pro běh OpenOffice.org v módu GTK2 (předevolená, standardní možnost), zadejte (v bash):

```
 # OOO_FORCE_DESKTOP=gnome soffice

```

Pro běh OpenOffice.org v módu QT/KDE3, zadejte (v bash):

```
 # OOO_FORCE_DESKTOP=kde soffice

```

Pro běh OpenOffice.org v módu QT4/KDE4, zadejte (v bash):

```
 # OOO_FORCE_DESKTOP=kde4 soffice

```

**Note:** Protože byl vzhled KDE z Openoffice3 odstraněn, je doporučeno použít pro všechny uživatele mód GTK. KDE4 integrace je v experimentálním stádiu v go-openoffice a v openoffice-base-devel (od verze m56)

#### Globální konfigurace prostředí OOo

Pro nastavení konkrétního vzhledu OpenOffice při každém jeho spuštění je nutno zadat proměnnou **<tt>OOO_FORCE_DESKTOP</tt>** do souboru /etc/profile.d/openoffice.sh, nebo do souboru /usr/bin/soffice, s hodnotou **<tt>gnome</tt>**, **<tt>kde</tt>** nebo **<tt>kde4</tt>**.

#### Skripty pro nastavení prostředí OOo

Pokud z jakéhokoliv důvodu nechcete konfigurovat vzhled globálně, můžete mít jako uživatel, nepoužívající GNOME/KDE problém s nastavením proměnné v *box menu vašeho prostředí, protože tato menu nemají ráda zadávání proměnných.

Tento skript spustí openoffice s použitím vzhledu GTK a nadále akceptuje příkazy z příkazové řádky - např. -writer.

```
#!/bin/sh

#### openoffice-gtk - Skript pro spuštění openoffice v protředí GNOME/GTK

OOO_FORCE_DESKTOP=gnome /usr/bin/soffice "$@"

```

Použijte tento skript ve svém menu (či spouštěči) jako příkaz (např. /usr/bin/openoffice-gtk).

**Note:** Pokud soubor otevřete ve správci souborů, např. v Thunaru, bude použit výchozí vzhled, protože se na váš skript asociace souborů nepoužije.

### Vzhled a chování KDE4 pro OpenOffice

OOO_FORCE_DESKTOP=gnome takový způsob nenabídne. Lze to obejít nastavením (jako root):

```
export SAL_GTK_USE_PIXMAPPAINT=1

```

v souboru /etc/profile.d/openoffice.sh. V nastavení KDE4 musí být zvoleno "použít můj styl KDE v aplikacích GTK" - Vzhled > GTK styly a písma (musí být nainstalován gtk-qt-engine).

#### Alternativní konfigurace

Můžete si přát nastavit DPI z Xorg serveru v konfiguraci [KDM](/index.php/KDM "KDM").

Nevybírejte "použít můj styl KDE v aplikacích GTK". Místo toho zvolte nativní styl a font pro GTK2 aplikace.

```
# pacman -S gtk-chtheme
# pacman -S gtk-engines

```

Změňte styl pomocí gtk-chtheme (v základu odlišný od KDE) a font (může být stejný jako váš KDE systémový font). Existují další balíčky pro GTK engine.

V nastavení OOo jsou dvě důležité obrazovky, Vzhled a Písma:

*   Vzhled
    *   nastavit měřítko na 100%
    *   nastavit použití sytémového fontu na OFF (jinak nebude tabulka náhrad použita)
    *   nastavit antialiasing na OFF

*   Písma
    *   vybrat "Použít tabulku náhrad"
    *   změnit "Andale Sans UI" (*musíte* to přepsat -- není na to nabídka) za jiný font (váš KDE systémový font nebo jiný, pokud nevypadá dobře)
    *   zatrhnout fajfku, aby se seznam aktualizoval
    *   vybrat "vždy" a "pouze obrazovka"
    *   stisknout OK

Při výběru fontů pro OpenOffice mějte na paměti, že jednoduchý renderovací engine, obsažený v balíčku, nedokáže vykreslit detaily fontu stejným způsobem, jako ostatní desktopové aplikace. Použijte lupu `kmag` k průzkumu tvarů každého písma.

## Spouštění OpenOffice

Pokud si přejete spustit konkrétní program OpenOffice.org (místo předvoleného Startcentra soffice), např. textový editor (Write), tabulkový procesor (Calc) nebo program pro prezentace (Impress), použijte následující parametry:

Writer

```
 /usr/bin/soffice -writer

```

Calc

```
 /usr/bin/soffice -calc

```

Impress

```
 /usr/bin/soffice -impress

```

Draw

```
 /usr/bin/soffice -draw

```

Math (Editor rovnic)

```
 /usr/bin/soffice -math

```

Base (Databáze)

```
 /usr/bin/soffice -base

```

Administrace tiskáren (doporučeno spustit jako root)

```
 /usr/bin/spadmin

```

## Zrychlení OpenOffice

Některá nastavení mohou zlepšit rychlost spouštění a odezvy OpenOffice. Nicméně mohou zvýšit nároky na paměť RAM, takže je používejte opatrně. Všechny jsou dostupné v menu *Nástroje > Volby*.

*   V menu *Paměť*:
    *   Redukovat počet kroků Zpět na méně než 100, na 20 až 30 kroků.
    *   V Grafická vyrovnávací paměť nastavte Použít pro OpenOffice.org na 128 MB (navýšit z původních 20MB).
    *   Nastavit Paměť na objekt na 20MB (navýšit z původních 5MB).
    *   Pokud používáte OpenOffice často, zvolte OpenOffice.org Quickstarter.
*   V menu *Java*, odtrhněte Použít běhové prostředí jazyka Java (JRE).

## Problémy

### Náhrada fontů

Toto lze změnit v nastavení OpenOffice.org. Z menu vyberte *Nástroje > Volby > OpenOffice.org > Písma*. Zatrhněte volbu *Použít tabulku náhrad*. Napište `Andale Sans UI` do řádky fontů a vyberte žádaný font pro položku *Zaměnit za*. Když je hotovo, klikněte na *zatržítko*. Pak zvolte *Vždy* a *Pouze obrazovka* v boxu níže. Klikněte na OK. Potom jděte do *Nástroje > Volby > OpenOffice.org > Vzhled* a odškrtněte "Použít systémový font pro uživatelské rozhraní". Pokud použijete nevyhlazovaný font, např. Arial, musíte dále odškrtnout "Vyhlazování fontu obrazovky", aby se font menu zobrazoval korektně.

### Vyhlazování

Spusťte

```
$ echo "Xft.lcdfilter: lcddefault" | xrdb -merge

```

Aby se změny zachovaly trvale, vložte "`Xft.lcdfilter: lcddefault`" do vašeho souboru `~/.Xresources`. [[1]](https://bugs.launchpad.net/ubuntu/+source/openoffice.org/+bug/271283/comments/19).

Pokud to nefunguje, můžete zkusit přidat "`Xft.lcdfilter: lcddefault`" do souboru `~/.Xdefaults`. Pokud soubor neexistuje, vytvořte jej.

### Detekce TrueType fonů

Viz [Font configuration#Programs can no longer access TrueType fonts](/index.php/Font_configuration#Programs_can_no_longer_access_TrueType_fonts "Font configuration"). Pro přidání k již existujícím v OpenOffice spusťte `spadmin`.

### Qt vzhled v KDE >4

OpenOffice byl převeden do Qt 4, takže vzhled aplikací nemůže být měněn nástroji pro Qt 3.

### Francouzský slovník

Od openoffice 3.0.0-2 obsahuje francouzský slovník chyby kvůli kódování znaků. K vyřešení je nutno spustit tyto příkazy (potřebujete balíčky **zip** a **unzip**):

```
$ cp /usr/lib/openoffice/share/extension/install/dict-fr.oxt dict-fr.oxt
$ unzip dict-fr.oxt -d dict-fr
$ cd dict-fr
$ iconv -f ISO-8859-15 -t UTF-8 dictionaries.xcu > dictionaries.xcu.utf
$ mv dictionaries.xcu.utf dictionaries.xcu
$ zip ../dict-fr.oxt *
$ cd ../
$ rm -r dict-fr

```

potom jděte do Správce rozšíření v openoffice (menu Nástroje) a instalujte slovník z nového souboru dict-fr.oxt

### Tmavá GTK témata a gtk-qt-engine

Pro rychlou opravu navštivte [openoffice-dark-gtk-fix](https://aur.archlinux.org/packages/openoffice-dark-gtk-fix/) nebo když máte go-openoffice navštivte [go-openoffice-dark-gtk-fix](https://aur.archlinux.org/packages.php?ID=28879) v repozitáři AUR. Nastaví to i 'OOO_FORCE_DESKTOP=gnome'. Další opravou je exportovat SAL_USE_VCLPLUGIN=gen (generické X11). Viz [další info](http://user.services.openoffice.org/en/forum/viewtopic.php?f=16&t=27216#p123942)