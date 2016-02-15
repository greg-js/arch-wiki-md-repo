## Contents

*   [1 Úvod](#.C3.9Avod)
*   [2 Instalace](#Instalace)
*   [3 Oprava krachu dialogu tisku](#Oprava_krachu_dialogu_tisku)
*   [4 Změna klávesových zkratek](#Zm.C4.9Bna_kl.C3.A1vesov.C3.BDch_zkratek)
*   [5 Fonty LaTex](#Fonty_LaTex)
*   [6 Externí odkazy](#Extern.C3.AD_odkazy)

## Úvod

**Abiword** je textový procesor, který nabízí odlehčenou alternativu k Writeru z OpenOffice, při stejné rychlosti a zachování skvělé funkcionality. Abiword podporuje mnoho standardních typů dokumentů, např. dokumenty z OpenOffice.org, Microsoft Wordu, WordPerfectu, Rich Text Format dokumenty a HTML stránky.

## Instalace

Nejdříve můžete chtít nainstalovat slovníky kontroly pravopisu:

```
# pacman -S aspell-cs

```

Instalace programu Abiword:

```
# pacman -S abiword

```

Další rozšíření:

```
# pacman -S abiword-plugins

```

Fonty, které opraví drobný kurzor a nezarovnaný text:

```
# pacman -S ttf-freefont ttf-ms-fonts

```

## Oprava krachu dialogu tisku

Z nějakého důvodu současné verze Abiwordu a libgnomeprint nespolupracují korektně. Standardní šablona .abw způsobuje krach programu, když chce uživatel tisknout. Řešením je donutit Abiword místo ní pracovat s formátem .rtf. Podle níže uvedeného postupu lze nastavit předvolený formát dokumentů na .rtf a donutit Abiword používat .rtf jako jeho výchozí šablonu.

Otevřít soubor ~/.AbiSuite/AbiWord.Profile a vložit následující řádek do druhé sekce <scheme>:

```
DefaultSaveFormat=".rtf"

```

Mělo by to vypadat nějak takto:

```
<Scheme
   name="_custom_"
   ZoomPercentage="64"
   DefaultSaveFormat=".rtf"
/>

```

Dále je důležité změnit předvolenou šablonu. Je třeba dodržet přesně následující postup.

1) otevřít Abiword a uložit prázdný dokument pod názvem "normal.rtf" do adresáře ~/.AbiSuite/templates/ Pokud adresář neexistuje, vytvořte jej.

2) Přejmenovat soubor na "normal.awt"

Neukládejte prázdný .awt soubor!! Aby to fungovalo, je třeba donutit Abiword použít šablonu .rtf.

Jakmile bude konflikt mezi Abiwordem a libgnomeprint vyřešen, tyto instrukce nebudou důležité a mohou být smazané.

## Změna klávesových zkratek

Jak změnit předvolené klávesové zkratky v Abiwordu viz [tento článek](http://www.abisource.com/wiki/Keyboard_bindings).

## Fonty LaTex

Balíček "abiword-plugins" obsahuje funkci, která umožňuje uživateli do dokumentu vložit kódy v LaTexu. Aby se matematické symboly zobrazovaly korektně, je třeba stáhnout [latex-xft-fonts](http://movementarian.org/latex-xft-fonts-0.1.tar.gz) a uložit je do adresáře /usr/share/fonts. Font se instaluje rozbalením souboru příkazem

```
# tar -xzf (name of the tar.gz file)

```

a spuštěním příkazu

```
# fc-cache -fv

```

## Externí odkazy

*   [Oficiální homepage](http://www.abisource.com/)