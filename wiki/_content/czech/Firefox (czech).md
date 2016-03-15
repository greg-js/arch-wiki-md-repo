Firefox je open source webový prohlížeč od [Mozilla](https://en.wikipedia.org/wiki/Mozilla "wikipedia:Mozilla"). Firefox balíček v Arch Linuxu je zkompilovany bez oficialniho označení. To znamená, že pokud spustíte Firefox tak použije jako svou ikonu modrý globus a bude se jmenovat dle svého kódového jména.

## Contents

*   [1 Povolení označení Firefox](#Povolen.C3.AD_ozna.C4.8Den.C3.AD_Firefox)
    *   [1.1 Rekompilace](#Rekompilace)
    *   [1.2 Rozšíření](#Roz.C5.A1.C3.AD.C5.99en.C3.AD)
    *   [1.3 Rozšířená konfigurace](#Roz.C5.A1.C3.AD.C5.99en.C3.A1_konfigurace)
*   [2 Rozšíření](#Roz.C5.A1.C3.AD.C5.99en.C3.AD_2)
*   [3 Pluginy](#Pluginy)
*   [4 Tipy](#Tipy)
    *   [4.1 Fonty](#Fonty)
        *   [4.1.1 DPI](#DPI)
        *   [4.1.2 Záměna fontů](#Z.C3.A1m.C4.9Bna_font.C5.AF)
        *   [4.1.3 Konfigurace fontu](#Konfigurace_fontu)
    *   [4.2 Tipy na články](#Tipy_na_.C4.8Dl.C3.A1nky)
*   [5 Alternativy Firefoxu](#Alternativy_Firefoxu)
*   [6 Externí odkazy](#Extern.C3.AD_odkazy)

# Povolení označení Firefox

Pokud chcete povolit označení nebo jednoduše změnit uživatelského agenta existuje několik způsobů jak toho docílit. Můžete rekompilovat, modifikovat, nebo použít rozšířenou konfiguraci.

## Rekompilace

Pro rekompilaci použijeme [ABS](/index.php/ABS "ABS"). Ujistěte se, že máte nainstalovaný **cvsup** a **wget**. Nyní spusťte

```
abs

```

Pokud je to poprvé co ho spouštíte možná to bude chvilku trvat. Další start už bude mnohem rychlejší. Nyní proveďte následující kroky:

```
mkdir /var/abs/local/firefox
cp /var/abs/network/firefox/* /var/abs/local/firefox
cd /var/abs/local/firefox

```

Použijte svůj oblíbený editor a otevřete soubor mozconfig. Přidejte následující řádku na konec tohoto souboru:

```
ac_add_options --enable-official-branding

```

Uložte, ukončete a proveďte:

```
md5sum mozconfig

```

Výslednou hodnotu si uložte a otevřete soubor PKGBUILD. Podívejte se ve zdroji na oddíl md5sums. V nejnovější verzi Firefoxu je Mozconfig druhý v seznamu zdrojů. Takže modifikujeme druhý md5sum hodnotou co jsme získali před chvílí. Nyní scrolujte dolů a podívejte se po dvou řádcích co vypadají jako následující:

```
install -m644 ${startdir}/src/mozilla/browser/app/default.xpm ${startdir}/pkg/opt/mozilla/lib/firefox/chrome/icons/default/
install -m644 ${startdir}/src/mozilla/browser/app/default.xpm ${startdir}/pkg/opt/mozilla/lib/firefox/icons/

```

Přepište je tímto:

```
install -m644 ${startdir}/src/mozilla/dist/branding/default.xpm ${startdir}/pkg/opt/mozilla/lib/firefox/chrome/icons/default/
install -m644 ${startdir}/src/mozilla/dist/branding/default.xpm ${startdir}/pkg/opt/mozilla/lib/firefox/icons/ 

```

Uložte, ukončete a spusťte:

```
makepkg

```

Může to chvilku trvat v závisloti na vašem počítači. Když máme nově vytvořený balíček, odstraňte oficiální verzi Firefoxu pokud ho máte nainstalovaný.

```
pacman -Rd firefox

```

Nainstalujte náš Firefox:

```
pacman -A firefox-*.pkg.tar.gz

```

Můžete se i pokusit updatovat již nainstalovaný firefox.

```
pacman -U firefox-*.pkg.tar.gz

```

Samozřejmě znak * nahraďte číslem vaší verze.

## Rozšíření

*   [CCK Wizard](https://addons.mozilla.org/firefox/2553/) - Umožní vám modifikovat každý aspekt Firefoxu. Nabídku, uživatelského agenta, ikony, grafiku a ještě více.

*   [User Agent Switcher](https://addons.mozilla.org/firefox/59/) - Přidá nabídku a tlačítko pro přepnutí uživatelského agenta.

## Rozšířená konfigurace

Napište `about:config` ve vašem Firefoxu do textového pole pro zadávání adresy a zobrazíte tím rozšířené nastavení. Ve filtru napiště `useragent.extra.firefox`, a uvidíte vašeho hodnotu vašeho uživatelského agenta. Můžete tam zadat cokoliv potřebujete. Pokud chcete povolit zobrazování verze Firefoxu na webových stránkách zadejte: `**Firefox/2.0.0.1**`

# Rozšíření

*   [Adblock Plus](https://addons.mozilla.org/firefox/1865/) - Překvapivě slouží k blokování reklam.
*   [MediaPlayerConnectivity](https://addons.mozilla.org/firefox/446/) - Umožnuje otevírat video z webu v externí aplikaci. Dobrá volba pro ty co mají problémy s pluginy pro média.

# Pluginy

Pokud chcete zjistit jaké pluginy máte nainstalované jednoduše napište `about:plugins` do pole adresy ve Firefoxu.

*   Flash

```
pacman -S flashplugin

```

*   Mplayer

```
pacman -S mplayer-plugin

```

*   Java

```
pacman -S jre

```

# Tipy

## Fonty

### DPI

Modifikace následující hodnoty by měla vylepšit vzhled fontu ve Firefoxu. Do pole adresy napište about:config. Dále napište dpi do filtru, změnte **layout.css.dpi** na **0**.

### Záměna fontů

Další způsob jak vylepšit vzhled fontů je vyměnit ho za jiný. Přidejte nebo vytvořte *.fonts.conf* s následujícím obsahem:

```
<match target="pattern">
    <test qual="any" name="family"><string>tahoma</string></test>
    <edit name="family" mode="assign"><string>Bitstream Vera Sans</string></edit>
</match>

```

Název prvního fontu je ten který chceme nahradit. Druhý font je logicky ten co bude nahrazen.

### Konfigurace fontu

Pro další podrobnější informace ohledně konfigurace fontů čtěte prosím: [Xorg Font Configuration](/index.php/Xorg_Font_Configuration "Xorg Font Configuration")

## Tipy na články

*   [Firefox Tips and Tweaks](/index.php/Firefox_Tips_and_Tweaks "Firefox Tips and Tweaks")
*   [Adding Firefox Search Engines As User](/index.php/Adding_Firefox_Search_Engines_As_User "Adding Firefox Search Engines As User")

# Alternativy Firefoxu

Viz [List of Applications (Česky)#Prohlížeče](/index.php/List_of_Applications_(%C4%8Cesky)#Prohl.C3.AD.C5.BEe.C4.8De "List of Applications (Česky)").

# Externí odkazy

*   [Srovnání rychlosti prohlížečů](http://www.howtocreate.co.uk/browserSpeed.html)
*   [Fakta ohledně Debianu a Mozilla® Firefoxu](http://web.glandium.org/blog/?p=97)
*   [Gnuzilla and IceWeasel](http://www.gnu.org/software/gnuzilla/)