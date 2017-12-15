Related articles

*   [Fonts](/index.php/Fonts "Fonts")
*   [Java fontovi - Sun JRE](/index.php?title=Java_fontovi_-_Sun_JRE&action=edit&redlink=1 "Java fontovi - Sun JRE (page does not exist)")
*   [MS Fonts](/index.php/MS_Fonts "MS Fonts")

Pregled opcija za podesavanje fontova i raznih tehnika za unapredjenje citljivosti fontova.

## Contents

*   [1 Font staze](#Font_staze)
    *   [1.1 Fontconfig](#Fontconfig)
    *   [1.2 Xorg](#Xorg)
*   [2 Fontconfig podesavanja](#Fontconfig_podesavanja)
    *   [2.1 Anti-aliasing](#Anti-aliasing)
    *   [2.2 Hintovanje](#Hintovanje)
        *   [2.2.1 Bajt-kod interpreter (BCI)](#Bajt-kod_interpreter_.28BCI.29)
        *   [2.2.2 Automatsko hintovanje](#Automatsko_hintovanje)
        *   [2.2.3 Hint stil](#Hint_stil)
    *   [2.3 Subpixel renderovanje](#Subpixel_renderovanje)
        *   [2.3.1 LCD filter](#LCD_filter)
        *   [2.3.2 Napredna specifikacija za LCD filter](#Napredna_specifikacija_za_LCD_filter)
    *   [2.4 Iskljucite auto-hinter za bold fontove](#Iskljucite_auto-hinter_za_bold_fontove)
    *   [2.5 Omogucite anti-aliasing samo za vece fontove](#Omogucite_anti-aliasing_samo_za_vece_fontove)
    *   [2.6 Zameni fontove](#Zameni_fontove)
    *   [2.7 Iskljucite bitmap fontove](#Iskljucite_bitmap_fontove)
    *   [2.8 Napravite bold i italic stilove za nekompletne fontove](#Napravite_bold_i_italic_stilove_za_nekompletne_fontove)
    *   [2.9 Izmena predupredjivanja pravila](#Izmena_predupredjivanja_pravila)
    *   [2.10 Primer fontconfig podesavanja](#Primer_fontconfig_podesavanja)
*   [3 Zakrpljeni paketi](#Zakrpljeni_paketi)
    *   [3.1 Originalni LCD paketi](#Originalni_LCD_paketi)
    *   [3.2 Ubuntu](#Ubuntu)
    *   [3.3 Cleartype](#Cleartype)
    *   [3.4 Infinality](#Infinality)
    *   [3.5 Povratak na pakete bez zakrpa](#Povratak_na_pakete_bez_zakrpa)
*   [4 Aplikacije bez fontconfig podrske](#Aplikacije_bez_fontconfig_podrske)
*   [5 Resavanje problema](#Resavanje_problema)
    *   [5.1 Iskrivljeni fontovi](#Iskrivljeni_fontovi)
    *   [5.2 Nedostatak karaktera](#Nedostatak_karaktera)
    *   [5.3 Starije GTK i QT aplikacije](#Starije_GTK_i_QT_aplikacije)
*   [6 Izvori](#Izvori)

## Font staze

Da bi [fontovi](/index.php/Fonts "Fonts") bili poznati aplikacijama, moraju biti razvrstani za lak i brz pristup. [Fontconfig](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig") je biblioteka napravljena da pruzi listu dostupnih fontova za aplikacije, i takodje za podesavanja za nacin prikaza fontova. Iako je fontconfig standard u danasnje vreme u Linux-u, neke aplikacije se jos uvek oslanjaju na originalni metod kategorizacije fontova: Xorg server podesavanja.

### Fontconfig

Fontconfig prikuplja sve podesavanja u centralni fajl (`/etc/fonts/fonts.conf`). Fontconfig-svesne aplikacije iscitavaju ovaj fajl da saznaju raspolozive fontove i nacin na koji se oni prikazuju. Ovaj fajl je skup pravila iz raznih fontconfig konfiguracionih fajlova (globalna podesavanja (`/etc/fonts/local.conf`), prekonfigurisani fajlovi u `/etc/fonts/conf.d/`, i konfiguracioni fajl korisnika (`~/.fonts.conf`).

Staze koje su inicijalno poznate fonconfig-u su: `/usr/share/fonts/` i `~/.fonts/` (koje ce fontconfig skenirati rekurzivno). Radi lakse organizacije i instalacije, preporucuje se upotreba ovih font staza kada [instalirate nove fontove](/index.php/Fonts "Fonts").

Da vidite listu poznatih fontconfig fontova i lako citljivom formatu:

```
$ fc-list | sed 's,:.*,,' | sort -u

```

### Xorg

Proverite Xorg-ove poznate font staze pregledanjem njegovog log-a:

```
$ grep /fonts /var/log/Xorg.0.log

```

Imajte na umu da Xorg ne pretrazuje rekurzivno kroz `/usr/share/fonts` direktorijum kao sto fontconfig to cini. Da dodate stazu, morate da zadate celu adresu:

```
Section "Files"
    FontPath     "/usr/share/fonts/example-font-directory"
EndSection

```

Da vidite listu poznatih Xorg fontova upotrebite `xlsfonts`.

## Fontconfig podesavanja

Paket za renderovanje fontova na Arch Linux-u sadrzi podrsku za *freetype2* sa omogucenim bajtkod interpreterom (BCI). Ali definisanje vasih podesavanja za font ce ponekad biti neophodno. Razmotrite upotrebu [zakrpljenih paketa](#Patched_packages) za bolje renderovanje fontova, pogotovo sa LCD monitorom.

Konfigurisanje se moze obaviti na nivou jednog korisnika preko `~/.fonts.conf`, ili globalno sa `/etc/fonts/local.conf`. Podesavanja za jednog korisnika imaju prednost u odnosu na globalna podesavanja. Oba ova fajla koriste istu sintaksu. Zapamtite da ne editujete `/etc/fonts/fonts.conf` fajl; to je privremeni fajl i nebi trebali da ga editujete jer se on prepisuje tokom fontconfig osvezavanja.

Vec postoji odredjeni broj prekonfigurisanih opcija u direktorijumu `/etc/fonts/conf.avail`. Ova prekonfigurisana podesavanja se mogu linkovati na nivou korisnika ili globalno za brze podesavanje. Imajte na umu da ce ova podesavanja imati prednost u odnosu na podesavanja u njihovim odgovarajucim konfiguracionim fajlovima.

Naprimer, da omogucite sub-pixel RGB renderovanje na globalnom nivou:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/10-sub-pixel-rgb.conf

```

Da ucinite isto ali na nivou podesavanja za jednog korisnika:

```
$ mkdir ~/.fonts.conf.d
$ ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf ~/.fonts.conf.d

```

**Note:** Za neka desktop okruzenja (poput [Gnoma](/index.php/GNOME "GNOME") i [KDE](/index.php/KDE "KDE")) upotreba "Font Control Panel"-a ce automatski napraviti ili prepisati korisnicki fajl za font podesavanja. Jedno od mogucih resenja je da ne koristite graficki interfejs za podesavanje fontova, vec da to obavljate rucno preko tekstualnog fajla za podesavanje.

Konfiguracioni fajlovi zahtevaju informativno zaglavlje pre nego sto se podesavanja mogu uneti:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- podesavanja idu ovde -->

</fontconfig>

```

Da izbegnete ponavljanje, ostatak konfiguracionih primera u ovom clanku ce izbeci ove tagove.

### Anti-aliasing

[Font rasterizacija](https://en.wikipedia.org/wiki/Font_rasterization_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) pretvara vektor font podatke u bitmap podatke tako da moze da se prikaze. Rezultat ce izgledati kao da ima ostre ivice zbog [aliasing-a](https://en.wikipedia.org/wiki/Aliasing "wikipedia:Aliasing"), pa je [anti-aliasing](https://en.wikipedia.org/wiki/Anti-aliasing "wikipedia:Anti-aliasing") ukljucen po difoltu da uveca rezolucija ivica fonta.

```
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

### Hintovanje

[Font hintovanje](https://en.wikipedia.org/wiki/Font_hinting "wikipedia:Font hinting") (takodje poznato zadavanje instrukcija) je upotreba matematickih instrukcija za podesavanje prikaza fonta tako da bude poravnat sa rasterizovanom mrezom, kao sto je piksel mreza na ekranu. Fontovi se nece poravnati ispravno bez hintovanja dok ekran nema 300 [DPI (tacaka po incu)](https://en.wikipedia.org/wiki/Dots_Per_Inch "wikipedia:Dots Per Inch") ili vise. Postoje dva tipa hintovanja.

#### Bajt-kod interpreter (BCI)

Upotrebom normalnog hintovanja, instrukcije za TrueType hintovanje u fontu se interpretiraju od strane freetype Bajt-kod interpretera. Ovo radi najbolje za fontove sa dobrim instrukcijama za hintovanje.

Da omogucite normalno hintovanje:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Automatsko hintovanje

Automatsko otkrivanje za hintovanje. Ovo izgleda gore nego normalno hintovanje za fontove sa dobrim instrukcijama, ali bolje za one sa losim ili nikakvim instrukcijama.

Da ukljucite automatsko hintovanje:

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

**Note:** Nemojte da koristite automatsko hintovanje sa subpixel renderovanjem. Ova dva nisu dizajnirana da rade zajedno. [Infinality](#Infinality) paket popravlja ovaj konflikt.

#### Hint stil

Hint stil je kolicina uticaja koje **hinting** mod ima. Hintovanje moze biti podeseno na: `hintfull`, `hintmedium`, `hintslight` i `hintnone`. Sa BCI hintovanjem, hinfull bi trebalo da radi najbolje za vecinu fontova. Sa autohinter-om, hintslight se preporucuje.

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintfull</const>
    </edit>
  </match>

```

### Subpixel renderovanje

Subpixel renderovanje efikasno utrostrucuje horizontalnu (ili vertikalnu) rezoluciju za fontove upotrebom subpixela.

Vecina monitora proizvedenih u danasnje vreme koristi crvenu, zelenu, plavu (RGB) specifikaciju. Fontconfig ce morati da zna vas tip monitora da bi bio u mogucnosti da prikaze vase fontove na ispravan nacin.

*RGB (najcesci), BGR, V-RGB (vertikalno), ili V-BGR*

Da upalite subpixel renderovanje:

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

Ako primetite neobicne boje oko granica fontova, proverite tip vaseg monitora [ovde](http://www.lagom.nl/lcd-test/subpixel.php).

**Note:** Nemojte da koristite autohinter sa subpixel renderovanjem. Ove dve opcije nisu dizajnirane da rade zajedno. [Infinality](#Infinality) paket popravlja ovaj konflikt.

#### LCD filter

Kada koristite subpixel renderovanje, trebalo bi da upalite lcd filter.

`lcddefault` filter ce raditi za vecinu korisnika. Drugi filteri su dostupni koji se mogu koristiti u specijalnim situacijama: `lcdlight`; laksi filter idealan za fontove koji izgledaju suvise zadebljani (bold) ili mutni, `lcdlegacy`, originalni Cairo filter; i `lcdnone` da ga iskljucite u potpunosti.

```
  <match target="font">
    <edit mode="assign" name="lcdfilter">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### Napredna specifikacija za LCD filter

Ako su dostupni, ugradjeni LCD filteri nisu zadovoljavajuci. Moguce je podesiti font renderovanje vrlo specificno tako sto cete napraviti prilagodjen freetype2 paket i modifikovati tesko kodorane filtere. Ako ne znate kako da napravite i instalirate pakete iz izvornog koda, upoznajte se sa [ABS (Српски)](/index.php?title=ABS_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "ABS (Српски) (page does not exist)")-om prvo.

**Note:** [Infinality](#Infinality) paket pruza mogucnost da dodatno podesite filter podesavanja sa prostornom promenljivom (varijablom), bez rekompajliranja.

Prvo, osvezite freetype2 PKGBUILD kao root:

```
# abs extra/freetype2

```

Ovaj primer koristi `/var/abs/build` kao direktorijum za pravljenje. Promenite ga u skladu sa vasim licnim ABS podesavanjima. Preuzmite i otpakujte freetype2 paket kao obican korisnik:

```
$ cd /var/abs/build
$ cp -r ../extra/freetype2 .
$ cd freetype2
$ makepkg -o

```

Izmenite fajl `src/freetype-VERSION/src/base/ftlcdfil.c` i pogledajte definiciju konstante `default_filter[5]`:

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

Ova konstanta definise low-pass filter primenjen na renderovan glif. Izmenite ga po potrebi. Sacuvajte fajl, napravite i instalirajte prilagodjeni paket:

```
$ makepkg -e
$ sudo pacman -Rd freetype2
$ sudo pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

Restartujte racunar ili samo X. Lcddefault filter bi sada trebalo da renderuje fontove drugacije.

### Iskljucite auto-hinter za bold fontove

Auto-hinter koristi sofisticirane metode za renderovanje fontova, ali obicno pravi bold fontove suvise sirokim. Srecom, to se moze resiti iskljucivanjem autohinter-a samo za bold fontove:

```
...
<match target="font">
    <test name="weight" compare="more">
        <const>medium</const>
    </test>
    <edit name="autohint" mode="assign">
        <bool>false</bool>
    </edit>
</match>
...

```

**Note:** [Infinality](#Infinality) paket pruza mogucnost autohinteru da radi kako treba sa bold fontovima.

### Omogucite anti-aliasing samo za vece fontove

*Takodje pogledajte [sharpfonts.co.cc](http://sharpfonts.co.cc/) za dodatne informacije*

Neki korisnici vise vole ostrije renderovanje koje anti-aliasing ne pruza:

```
...
<match target="font">
    <edit name="antialias" mode="assign">
        <bool>false</bool>
    </edit>
</match>

<match target="font" >
    <test name="size" qual="any" compare="more">
        <double>12</double>
    </test>
    <edit name="antialias" mode="assign">
        <bool>true</bool>
    </edit>
</match>

<match target="font" >
    <test name="pixelsize" qual="any" compare="more">
        <double>17</double>
    </test>
    <edit name="antialias" mode="assign">
        <bool>true</bool>
    </edit>
</match>
...
```

### Zameni fontove

Najpouzdaniji nacin da to uradite je da dodate XML deo slican ovom ispod. Ovo ce rezultirati time da Bitstream Vera Sans bude koriscen umesto Helvetica-e:

```
...
<match target="pattern" name="family" >
    <test name="family" qual="any" >
        <string>Helvetica</string>
    </test>
    <edit name="family" mode="assign">
        <string>Bitstream Vera Sans</string>
    </edit>
</match>
...

```

Alternativni pristup je da podesite "preferirani" font, ali *ovo radi samo ako originalni font nije na sistemu*, u kom slucaju onaj koji je zadat ce biti zamenjen:

```
...
< !-- Zamenite Helvetica sa Bitstream Vera Sans Mono -->
< !-- Napomena, alias za Helvetica bi vec trebalo da postoji u difolt conf fajlovima -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### Iskljucite bitmap fontove

Da iskljucite bitmap fontove u fontconfigu, upotrebite `70-no-bitmaps.conf` (koji nije napravljen od strane fontconfiga po difoltu):

```
# cd /etc/fonts/conf.d
# rm 70-yes-bitmaps.conf
# ln -s ../conf.avail/70-no-bitmaps.conf

```

Mozete da izaberete sa kojim fontovima da zamenite bitmap fontove (Helvetica, Courier i Times bitmap mapira na TTF fontove) sa:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/29-replace-bitmap-fonts.conf

```

### Napravite bold i italic stilove za nekompletne fontove

Freetype ima mogucnost da autmoatski napravi *italic* i **bold** stilove za fontove koji ih nemaju, ali samo ako su eksplicitno zahtevani od strane aplikacije. Dati programi vrlo retko salju ove zahteve. Ova sekcija pokriva manuelno primoravanje generisanja stilova koji nedostaju.

Startujte editovanjem `/usr/share/fonts/fonts.cache-1` kao sto je objasnjeno ispod. Uskladistite kopiju modifikacija u drugi fajl jer font osvezavanje sa `fc-cache` ce prepisati `/usr/share/fonts/fonts.cache-1`.

Pod pretpostavkom da je Dupree font instaliran:

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Duplirajte liniju pa izmenite `style=Regular` na `style=Bold` ili bilo koji drugi stil. Takodje promenite `slant=0` na `slant=100` za italic, `weight=80` na `weight=200` za bold, ili ih kombinujte za ***bold italic***:

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:*etc...*

```

Sada dodajte neophodne modifikacije u `~/.fonts.conf`:

```
...
<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
         <!-- other fonts here .... -->
     </test>
     <test name="weight" compare="more_eq"><int>140</int></test>
     <edit name="embolden" mode="assign"><bool>true</bool></edit>
</match>

<match target="font">
    <test name="family" qual="any">
        <string>Dupree</string>
        <!-- other fonts here .... -->
    </test>
    <test name="slant" compare="more_eq"><int>80</int></test>
    <edit name="matrix" mode="assign">
        <times>
            <name>matrix</name>
                <matrix>
                    <double>1</double><double>0.2</double>
                    <double>0</double><double>1</double>
                </matrix>
        </times>
    </edit>
</match>
...
```

**Tip:** Koristite vrednost 'embolden' za postojece bold fontove da ih ucinite jos vise boldovanim.

### Izmena predupredjivanja pravila

Fontconfig procesira fajlove u `/etc/fonts/conf.d` u obrnutom numerickom redosledu. Ovo omogucava pravilima ili fajlovima da preduprede jedan drugog, ali obicno zbunjuje korisnike o tome koji se fajl parsuje poslednji.

Da obezbedite da ce podesavanja na nivou korisnika imati prednost u odnosu na druga pravila, promenite njihov redosled:

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 00-user.conf

```

Ova izmena je uglavnom bespotrebna za vecinu slucajeva, jer je korisniku data dovoljna kontrola po difoltu da podesi licna font podesavanja, hinting i antialiasing opcije, alias novih fontova u genericke font familije, itd...

### Primer fontconfig podesavanja

Primer fontconfig podesavanja se moze naci na ovoj [stranici](/index.php/Font_configuration/Examples "Font configuration/Examples").

## Zakrpljeni paketi

Ovi zakrpljeni paketi su dostupni u [AUR](/index.php/AUR "AUR")-u i mogu se jednostavno instalirati upotrebom [AUR helper (Српски)](/index.php?title=AUR_helper_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "AUR helper (Српски) (page does not exist)"). Nekoliko napomena:

*   Podesavanje je obicno neophodno.
*   Novo font renderovanje nece proraditi dok se aplikacija ne restartuje.

### Originalni LCD paketi

Cairo 1.10 u [extra] dodaje podrsku za LCD filter. Pogledajte [#LCD filter](#LCD_filter). Mozete da instalirate [fontconfig-lcd](https://aur.archlinux.org/packages.php?ID=16458) iz [AUR](/index.php/AUR "AUR")-a da omogucite `lcddefault` filter automatski.

Da obezbedite filterovanje sa aplikacijama koje koriste libXft za iscrtavanje fontova, morate da instalirate [libxft-lcd](https://aur.archlinux.org/packages.php?ID=37044) iz [AUR](/index.php/AUR "AUR")-a.

### Ubuntu

Ubuntu koristi originalne LCD zakrpljene pakete i dodaje dodatna podesavanja i zakrpe.

Instalirajte zakrpljene pakete iz [AUR](/index.php/AUR "AUR")-a. Imena paketa su:

```
freetype2-ubuntu fontconfig-ubuntu libxft-ubuntu cairo-ubuntu

```

### Cleartype

**Note:** -cleartype paketi su zastareli. Razmotrite upotrebu novijeg freetype2-infinality paketa umesto njega. Mozete da podesite FIR filter prostornu promenljivu da se poklopi sa onim sto su cleartype zakrpe pruzale.

Ovi paketi su pokusali da emuliraju ClearType, tip subpixel renderovanja i filtriranja koji se koristi na Windows-u.

### Infinality

*   [Home stranica](http://www.infinality.net/blog/?p=67).
*   [Forum](http://www.infinality.net/forum/).

Infinality skup zakrpa ima za cilj da u velikoj meri unapredi freetype2 renderovanje fonta. On dodaje vise novih mogucnosti, od kojih su svi podesivi preko prostornih promenljivih u `/etc/profile.d/infinality-settings.sh`.

*   **Emboldening Enhancement**: Iskljucuje Y uvecanje, pruzajuci mnogo lepsi rezultat na fontovima bez bold verzija. Radi na nativnim TT hinter i autohinter.
*   **Auto-Autohint**: Automatski forsira autohint na fontovima koji ne sadrza TT instrukcije.
*   **Autohint Enhancement**: Cini da se autohint talas pruza horizontalno do pixela. Daje rezultat koji deluje kao dobro hintovan truetype font, ali je 100% patent slobodan.
*   **Customized FIR Filter**: Izaberite vase filter vrednosti tokom rada. Radi na prirodnim TT hinter i autohinter.
*   **Stem Alignment**: Poravnava bitmap glifove na optimizovane piksel granice. Radi na nativnim TT hinter i autohinter.
*   **Pseudo Gamma Correction**: Posvetljava i zamracuje glifove na zadatu vrednost, ispod zadate velicine. Radi na nativnim TT hinter i autohinter.
*   **Embolden Thin Fonts**: Uvecava tanke ili lake fontove tako da ostaju vidljiviji. Radi na autohinter.

[freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) se moze instalirati iz [AUR](/index.php/Arch_User_Repository_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Arch User Repository (Српски)")-a.

Dodatno, ako koristite [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) iz [multilib], zamenite ga sa [lib32-freetype2-infinality](https://aur.archlinux.org/packages/lib32-freetype2-infinality/) iz [AUR](/index.php/Arch_User_Repository_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Arch User Repository (Српски)")-a.

Da dobijete filtriranje sa aplikacijama koje koriste libXft za font iscrtavanje, morate da instalirate [libxft-lcd](https://aur.archlinux.org/packages/libxft-lcd/) iz [AUR](/index.php/Arch_User_Repository_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Arch User Repository (Српски)")-a.

**Note:** Infinality paket je dizajniran da radi sa [this local.conf](http://www.infinality.net/files/local.conf). Najverovatnije cete zeleti da napravite izmene na podesavanjima pre nego sto ga upotrebite (pravi dosta font zamena i podesava zeljene fontove na Arial, Times New Roman i Consolas.)

### Povratak na pakete bez zakrpa

Da se vratite na pakete bez zakrpa, reinstalirajte originale:

```
# pacman -S --asdeps freetype2 libxft cairo fontconfig

```

## Aplikacije bez fontconfig podrske

Neke aplikacije poput LibreOffice-a ignorisu fontconfig podesavanja. Ovo je vrlo primetno kada koristite infinality zakrpe koje se u velikoj meri oslanjaju na ispravna podesavanja. Mozete ovo zaobici upotrebom `~/.Xresources`, ali to nije ni priblizno fleksibilno kao fontconfig. Primer (pogledajte [#Fontconfig configuration](#Fontconfig_configuration) za objasnjenja za opcije):

 `~/.Xresources` 
```
Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Uverite se da su podesavanja ucitana ispravno kada X startuje sa `xrdb -q` (pogledajte [Xresources (Српски)](/index.php?title=Xresources_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Xresources (Српски) (page does not exist)") za vise informacija).

## Resavanje problema

### Iskrivljeni fontovi

**Note:** 96 DPI nije standard. Trebalo bi da koristite DPI od vaseg monitora da dobijete ispravno renderovanje fontova, pogotovo kada koristite subpixel-e.

Ako su fontovi i dalje neocekivano veliki ili mali, siromasno proporcionisani ili se jednostavno renderuju lose, moguce je da fontconfig koristi neispravan DPI.

Fontconfig bi trebalo da moze da detektuje DPI parametre koji su utvrdjeni od strane Xorg servera. Mozete da proverite auto-discovered DPI sa xdpyinfo:

 `$ xdpyinfo | grep dots`  `  resolution:    102x102 dots per inch` 

Ako je DPI detektovan netacno (obicno zbog netacnog monitor EDID-a), mozete da ga zadate rucno u Xorg podesavanjima, pogledajte [Xorg (Српски)#Display Size and DPI](/index.php?title=Xorg_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8)&action=edit&redlink=1 "Xorg (Српски) (page does not exist)"). Ovo je preporucljivo resenje, ali postoji mogucnost da nece raditi sa bagovitim drajverima.

Fontconfig ce se vratiti na difolt na Xft.dpi varijablu ako je podesena. Xft.dpi je obicno podesena od strane desktop okruzenja (obicno u Xorg-ovom DPI podesavanju) ili rucno u `~/.Xdefaults` ili `~/.Xresources`. Upotrebite xrdb da izdate upit za vrednoscu:

 `$ xrdb -query | grep dpi`  `Xft.dpi:	102` 

Oni koji i dalje imaju problem mogu rucno da podese dpi koji se koristi od strane fontconfig-a:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>96</double></edit>
</match>
...

```

### Nedostatak karaktera

Ako koristite [Emacs (Српски)](/index.php/Emacs_(%D0%A1%D1%80%D0%BF%D1%81%D0%BA%D0%B8) "Emacs (Српски)"), [xorg-fonts-75dpi](https://www.archlinux.org/packages/?name=xorg-fonts-75dpi) i [xorg-fonts-100dpi](https://www.archlinux.org/packages/?name=xorg-fonts-100dpi) paketi moraju biti instalirani.

### Starije GTK i QT aplikacije

Moderne GTK aplikacije po difoltu ukljucuju Xft, ali to nije bio slucaj pre verzije 2.2\. Ako nije moguce da osvezite ove aplikacije, primorajte Xft za stare GNOM aplikacije dodavanjem u `~/.bashrc`:

```
export GDK_USE_XFT=1

```

Za starije QT aplikacije:

```
export QT_XFT=true

```

## Izvori

*   [Fontovi u X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Oficijalne Xorg font informacije
*   [FreeType 2 pregled](http://freetype.sourceforge.net/freetype2/)