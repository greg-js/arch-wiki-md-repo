Documenta l'installazione e l'utilizzo dei Fonts su Arch Linux.

**Nota:** Certi pacchetti font possono imporre *alcune* limitazioni legali.

## Contents

*   [1 Font formats](#Font_formats)
    *   [1.1 Altri formati](#Altri_formati)
*   [2 Installazione](#Installazione)
    *   [2.1 Pacman](#Pacman)
    *   [2.2 Creazione di un pacchetto](#Creazione_di_un_pacchetto)
    *   [2.3 Installazione manuale](#Installazione_manuale)
        *   [2.3.1 Applicazioni datate](#Applicazioni_datate)
    *   [2.4 Pango Warnings](#Pango_Warnings)
    *   [2.5 Font e Xorg](#Font_e_Xorg)
*   [3 Pacchetti font](#Pacchetti_font)
    *   [3.1 Braille](#Braille)
    *   [3.2 International users](#International_users)
        *   [3.2.1 Arabo](#Arabo)
        *   [3.2.2 Cinese, Giapponese, Coreano, Vietnamita](#Cinese.2C_Giapponese.2C_Coreano.2C_Vietnamita)
            *   [3.2.2.1 Cinese (principalmente)](#Cinese_.28principalmente.29)
            *   [3.2.2.2 Giapponese](#Giapponese)
            *   [3.2.2.3 Coreano](#Coreano)
        *   [3.2.3 Greco](#Greco)
        *   [3.2.4 Ebraico](#Ebraico)
        *   [3.2.5 Indiano](#Indiano)
        *   [3.2.6 Khmer](#Khmer)
        *   [3.2.7 Singalese](#Singalese)
        *   [3.2.8 Tamil](#Tamil)
    *   [3.3 Math](#Math)
    *   [3.4 Microsoft fonts](#Microsoft_fonts)
    *   [3.5 Monospace](#Monospace)
        *   [3.5.1 TrueType](#TrueType)
        *   [3.5.2 Bitmap](#Bitmap)
    *   [3.6 Sans-serif](#Sans-serif)
    *   [3.7 Script](#Script)
    *   [3.8 Serif](#Serif)
    *   [3.9 Assortiti](#Assortiti)
*   [4 Font per console](#Font_per_console)
    *   [4.1 Anteprima e verifica](#Anteprima_e_verifica)
        *   [4.1.1 Esempi](#Esempi)
    *   [4.2 Modificare il carattere predefinito](#Modificare_il_carattere_predefinito)
        *   [4.2.1 Esempi](#Esempi_2)

## Font formats

La maggior parte dei font usati oggi dai computer sono sia in formato *bitmap* che *outline*. I font Bitmap archiviano immagini fisse per ogni glifo, di ogni dimensione e tipo, per carattere e punto. Il profilo o *vettore* dei font memorizza i caratteri come istruzioni per disegnare ogni linea e curva del glifo, potendo inoltre scalare in un ampio raggio di dimensioni senza problemi.

Le estensioni comuni nei nomi dei font comprendono:

*   `bdf` e `bdf.gz` – (Bitmap Distribution Format), font bitmap compressi in gzip `bdf`
*   `pcf` e `pcf.gz` – (Portable Compiled Font), font bitmap compressi in gzip `pcf`
*   `psf`, `psfu`, `psf.gz` e `psfu.gz` – (Pc Screen Font), (Pc Screen Font Unicode) e le versioni gzip, font bitmap, (incompatibili con Xorg)
*   `pfa` e `pfb` – (PostScript Font A-SCII) e (PostScript Font Binary), font con funzionalità di contorno e font PostScript, per istruzioni built-in delle stampanti.
*   `ttf` – (True Type Font), font con funzionalità di contorno. Originariamente concepito come una sostituzione per i font PostScript.
*   `otf` – (Open Type Font), font con funzionalità di contorno. TrueType con istruzioni tipografiche PostScript.

Nella maggior parte dei casi, le differenze tecniche tra TrueType e OpenType possono essere ignorate, alcuni font con un'estensione `ttf` sono in realtà i font OpenType.

### Altri formati

L'applicazione di composizione *TeX*, ed il suo software font abbinato, *Metafont,* randerizza i caratteri utilizzando metodi propri. Alcune delle estensioni dei file utilizzati per i font da questi due programmi sono `*pk`, `*gf`, `mf` e `vf`.

*FontForge,* è un'applicazione per l'editing dei caratteri in grado di memorizzare i caratteri nel loro formato nativo basato su testo, `sfd`, *s*pline *f*ont *d*atabase.

## Installazione

Vari metodi di installazione dei font.

### Pacman

Font specifici e collezioni di font possono essere installati dai nei repository abilitati utilizzando [pacman](/index.php/Pacman "Pacman"). I font disponibili possono essere trovati utilizzando:

```
$ pacman -Ss font

```

O per ricercare solo i font `ttf`:

```
$ pacman -Ss ttf

```

Alcuni font come *terminus* sono installati in `/usr/share/fonts/local`, che non viene aggiunto al percorso dei font di default. Aggiungendo le seguenti righe a `~/.xinitrc`

```
xset +fp /usr/share/fonts/local
xset fp rehash

```

i font possono essere usati in X11.

### Creazione di un pacchetto

Per avere la possibilità di gestire i font con pacman, è possibile creare un pacchetto per Arch. Questi possono anche essere condivisi con la comunità per mezzo di [AUR](/index.php/AUR "AUR"). Ecco un esempio di come compilare un pacchetto di base. Per ulteriori informazioni sulla creazione di pacchetti, leggere [PKGBUILD](/index.php/PKGBUILD "PKGBUILD").

```
pkgname=ttf-fontname
pkgver=1.0
pkgrel=1
depends=('fontconfig' 'xorg-font-utils')
pkgdesc="custom fonts"
arch=('any')
source=(http://someurl.org/$pkgname.tar.bz2)
install=$pkgname.install

build()
{
  mkdir -p $pkgdir/usr/share/fonts/TTF
  cp $srcdir/$pkgname/*.ttf $pkgdir/usr/share/fonts/TTF
}

```

Questo PKGBUILD presuppone che i font siano TrueType. Dovrà anche essere creato un file di installazione (`ttf-fontname.install`) per aggiornare la cache dei font:

```
post_install() {
  echo -n "Updating font cache... "
  fc-cache -fs >/dev/null
  mkfontscale /usr/share/fonts/TTF /usr/share/fonts/Type1
  mkfontdir /usr/share/fonts/TTF /usr/share/fonts/Type1
  echo "done"
}

post_upgrade() {
  post_install
}

```

### Installazione manuale

Il metodo raccomandato per aggiungere font non disponibili nei repository al sistema, è descritto in [#Creating a package](#Creating_a_package). Questo dà a pacman la possibilità di rimuoverli o aggiornarli in un secondo momento. Possono inoltre essere installati manualmente.

Per installare i font a livello di intero sistema (disponibile per tutti gli utenti), spostare la cartella nella directory `/usr/share/fonts/`. Per installare i font ad un singolo utente, utilizzare invece `~/.fonts/`.

Potrebbe anche essere necessario aggiornare `/etc/X11/xorg.conf` o `/etc/xorg.conf` con la nuova directory. Eseguire una ricerca con chiave `FontPath` per trovare la posizione corretta del file ed aggiungere il nuovo percorso. Consultare [#Fonts with Xorg](#Fonts_with_Xorg) per maggiori informazioni.

Aggiornare infine fontconfig, la cache dei font:

```
$ fc-cache -vf

```

#### Applicazioni datate

Con le vecchie applicazioni che non supportano fontconfig (ad es. le applicazioni GTK1, e `xfontsel`) l'indice dovrà essere creato nella directory dei font:

```
$ mkfontscale
$ mkfontdir

```

O per includere più di una cartella con un solo comando:

```
$ for dir in /font/dir1/ /font/dir2/; do xset +fp $dir; done && xset fp rehash

```

A volte il server X potrebbe non riuscire a caricare la cartella fonts e sarà necessario ripetere l'analisi tutti i file `fonts.dir`:

```
# xset +fp /usr/share/fonts/misc # Inform the X server of new directories
# xset fp rehash                # Forces a new rescan

```

Per controllare che i font siano inclusi:

```
$ xlsfonts | grep fontname

```

### Pango Warnings

Quando [Pango](http://www.pango.org/) è in uso sul proprio sistema sarà letto da [fontconfig](http://fontconfig.org/wiki/) per risolvere da dove leggere i font.

```
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='common'
(process:5741): Pango-WARNING **: failed to choose a font, expect ugly output. engine-type='PangoRenderFc', script='latin'

```

Nel caso si vedano errori simili a questo e/o blocchi invece di caratteri nell'applicazione, sarà necessario aggiungere dei font e aggiornare la cache dei font. Questo esempio utilizza i font [ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation) per illustrare la soluzione e viene eseguito da root, per consentirne l'utilizzo a livello globale nel sistema.

```
# pacman -S ttf-liberation
  -- output abbreviated, assumes installation succeeded -- 

# fc-cache -vfs
/usr/share/fonts: caching, new cache contents: 0 fonts, 3 dirs
/usr/share/fonts/TTF: caching, new cache contents: 16 fonts, 0 dirs
/usr/share/fonts/encodings: caching, new cache contents: 0 fonts, 1 dirs
/usr/share/fonts/encodings/large: caching, new cache contents: 0 fonts, 0 dirs
/usr/share/fonts/util: caching, new cache contents: 0 fonts, 0 dirs
/var/cache/fontconfig: cleaning cache directory   
fc-cache: succeeded

```

È possibile verificare la corretta configurazione di un font di default in questo modo:

```
# fc-match
LiberationMono-Regular.ttf: "Liberation Mono" "Regular"

```

### Font e Xorg

Per abilitare [Xorg](/index.php/Xorg "Xorg") a trovare ed utilizzare i nuovi font installati, è necessario aggiungere i percorsi dei font stessi in `/etc/xorg.conf` (un file di configurazione Xorg diverso potrebbe funzionare comunque).

Ecco un esempio della sezione che deve essere aggiunta a `/etc/xorg.conf`. Aggiungere o rimuovere i percorsi in base agli specifici requisiti dei propri caratteri.

```
# Let Xorg know about the custom font directories
Section "Files"
    FontPath    "/usr/share/fonts/100dpi"
    FontPath    "/usr/share/fonts/75dpi"
    FontPath    "/usr/share/fonts/cantarell"
    FontPath    "/usr/share/fonts/cyrillic"
    FontPath    "/usr/share/fonts/encodings"
    FontPath    "/usr/share/fonts/local"
    FontPath    "/usr/share/fonts/misc"
    FontPath    "/usr/share/fonts/OTF"
    FontPath    "/usr/share/fonts/TTF"
    FontPath    "/usr/share/fonts/util"
EndSection

```

## Pacchetti font

Questa è una lista selettiva, ma riporta la maggior parte dei font reperibili su [AUR](/index.php/AUR "AUR") oltre a quelli nei repository ufficiali. I caratteri sono taggati "Unicode" se provvisti di ampio supporto Unicode; consultarere il progetto o le pagine di Wikipedia per maggiori informazioni.

### Braille

*   [ttf-ubraille](https://www.archlinux.org/packages/?name=ttf-ubraille) - Font per simboli *braille*

### International users

#### Arabo

*   [ttf-sil-lateef](https://aur.archlinux.org/packages/ttf-sil-lateef/) - Font Unicode arabici da SIL *(AUR)*
*   [ttf-sil-scheherazade](https://aur.archlinux.org/packages/ttf-sil-scheherazade/) - Font Unicode arabici da SIL *(AUR)*

#### Cinese, Giapponese, Coreano, Vietnamita

##### Cinese (principalmente)

*   [wqy-microhei](https://www.archlinux.org/packages/?name=wqy-microhei) - Font in stile Sans-Serif, di alta qualità CJK. *(AUR)*
*   [wqy-zenhei](https://www.archlinux.org/packages/?name=wqy-zenhei) - Font cinesi stile Hei Ti (sans-serif) con schema incorporato e bitmap Song Ti (supporto parziale caratteri giapponesi e coreani).
*   [ttf-arphic-ukai](https://www.archlinux.org/packages/?name=ttf-arphic-ukai) - *Kaiti* (colpo di pennello) Font Unicode (consigliato abilitare l'anti-aliasing)
*   [ttf-arphic-uming](https://www.archlinux.org/packages/?name=ttf-arphic-uming) - *Mingti* (stampato) Font Unicode
*   [opendesktop-fonts](https://www.archlinux.org/packages/?name=opendesktop-fonts) - *New Sung* font, questo pacchetto prima si chiamava ttf-fireflysung.
*   [wqy-bitmapfont](https://www.archlinux.org/packages/?name=wqy-bitmapfont) - "wqy-bitmapfont" Font cinese in stile Song Ti (serif)
*   [ttf-hannom](https://www.archlinux.org/packages/?name=ttf-hannom) - Font TrueType Cinese e Vietnamita

##### Giapponese

*   [ttf-sazanami](https://www.archlinux.org/packages/?name=ttf-sazanami) - Set di Font giapponesi TrueType da alternare con la famiglia di font ttf-kochi.
*   [ttf-kochi-substitute](https://aur.archlinux.org/packages/ttf-kochi-substitute/) - Font giapponesi TrueType di alta qualità. Forniscono informazioni "bitmap hinting", quindi sono curati e non risultano frastagliati nella visualizzazione su schermi CRT.
*   [otf-ipafont](https://www.archlinux.org/packages/?name=otf-ipafont) - Set di font giapponesi gothic (san-serif) e Mincho (serif); uno dei font open source di migliore qualità. Di default su openSUSE-ja. *(AUR)*
*   [ttf-vlgothic](https://aur.archlinux.org/packages/ttf-vlgothic/) - Font giapponesi gothic. Default su Debian/Fedora/Vine Linux *(AUR)*
*   [ttf-monapo](https://aur.archlinux.org/packages/ttf-monapo/) - Font giapponesi per visualizzare correttamente [2channel Shift JIS art](http://en.wikipedia.org/wiki/2channel_Shift_JIS_art). *(AUR)*

##### Coreano

*   [ttf-baekmuk](https://www.archlinux.org/packages/?name=ttf-baekmuk) - Collezione di font coreani TrueType

#### Greco

Quasi tutti i font Unicode contengono il set di caratteri greci (polytonic incluso). Alcuni pacchetti di font aggiuntivi, che potrebbero non contenere il set completo Unicode ma utilizzano caratteri tipografici greci di alta qualità (e naturalmente anche latini) sono:

*   [otf-gfs](https://aur.archlinux.org/packages/otf-gfs/) - Selezione di font OpenType dalla Greek Font Society *(AUR)*
*   [ttf-mgopen](https://aur.archlinux.org/packages/ttf-mgopen/) - Font professionale TrueType da Magenta *(AUR)*

#### Ebraico

*   [culmus](https://aur.archlinux.org/packages/culmus/) - Ottima collezione di font in ebraico

#### Indiano

*   [ttf-freebanglafont](https://www.archlinux.org/packages/?name=ttf-freebanglafont) - Font per Bangla
*   [ttf-indic-otf](https://www.archlinux.org/packages/?name=ttf-indic-otf) - Collezione di font OpenType indi (contiene ttf-freebanglafont)

#### Khmer

*   [ttf-khmer](https://www.archlinux.org/packages/?name=ttf-khmer) - Font necessario per i grafi della lingua Khmer
*   [Hanuman](http://code.google.com/webfonts/family?family=Hanuman&subset=khmer) ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))

#### Singalese

*   [ttf-lklug](https://aur.archlinux.org/packages/ttf-lklug/) - Font Unicode Sinhala (*AUR*)

#### Tamil

*   [ttf-tamil](https://aur.archlinux.org/packages/ttf-tamil/) - Font Unicode Tamil (*AUR*)

### Math

*   [font-mathematica](https://www.archlinux.org/packages/?name=font-mathematica) - Font matematici di Wolfram Research, Inc.
*   [ttf-mathtype](https://aur.archlinux.org/packages/ttf-mathtype/) - Font MathType *(AUR)*
*   [ttf-computer-modern-fonts](https://aur.archlinux.org/packages/ttf-computer-modern-fonts/) - Segnalato come non aggiornato dal 2009-11-14 *(AUR)*

### Microsoft fonts

Consultare [MS Fonts](/index.php/MS_Fonts "MS Fonts").

### Monospace

Ecco alcuni suggerimenti: ogni utente ha le proprie preferenze, quindi sperimentare un po' per trovare quello più consono ai propri gusti. Se non si ha voglia di provarli uno alla volta, c'è uno spunto di Dan Benjamin sul suo blog: [*Top 10 Programming Fonts*](http://hivelogic.com/articles/top-10-programming-fonts).

Qui è visualizzabile una discreta lista di font suggeriti da Trevor Lowing: [http://www.lowing.org/fonts/](http://www.lowing.org/fonts/)

#### TrueType

*   [Andalé Mono](https://en.wikipedia.org/wiki/Andal%C3%A9_Mono "wikipedia:Andalé Mono") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Anonymous Pro ([ttf-anonymous-pro](https://www.archlinux.org/packages/?name=ttf-anonymous-pro))
*   [Bitstream Vera Mono](https://en.wikipedia.org/wiki/Bitstream_Vera "wikipedia:Bitstream Vera") ([ttf-bitstream-vera](https://www.archlinux.org/packages/?name=ttf-bitstream-vera))
*   [Consolas](https://en.wikipedia.org/wiki/Consolas "wikipedia:Consolas") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Courier New](https://en.wikipedia.org/wiki/Courier_New "wikipedia:Courier New") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Cousine ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Sostituto di Chrome/Chromium OS per Courier New (compatibilità metrica)
*   [DejaVu Sans Mono](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans Mono](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), inclusi in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   Envy Code R ([ttf-envy-code-r](https://aur.archlinux.org/packages/ttf-envy-code-r/))
*   [FreeMono](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Inconsolata](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata](https://www.archlinux.org/packages/?name=ttf-inconsolata))
*   [Inconsolata-g](https://en.wikipedia.org/wiki/Inconsolata "wikipedia:Inconsolata") ([ttf-inconsolata-g](https://aur.archlinux.org/packages/ttf-inconsolata-g/)) - aggiunge qualche modifica di facile programmazione
*   [Liberation Mono](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Alternativa a Courier New (compatibilità metrica)
*   [Lucida Console](https://en.wikipedia.org/wiki/Lucida_Console "wikipedia:Lucida Console") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Lucida Typewriter](https://en.wikipedia.org/wiki/Lucida_Typewriter "wikipedia:Lucida Typewriter") (inclusi nel pacchetto [jre](https://aur.archlinux.org/packages/jre/))
*   [Monaco](https://en.wikipedia.org/wiki/Monaco_(typeface) ([ttf-monaco](https://aur.archlinux.org/packages/ttf-monaco/))
*   Monofur ([ttf-monofur](https://aur.archlinux.org/packages/ttf-monofur/))

#### Bitmap

*   Default 8x16
*   Dina ([dina-font](https://www.archlinux.org/packages/?name=dina-font))
*   Lime ([artwiz-fonts](https://www.archlinux.org/packages/?name=artwiz-fonts))
*   [ProFont](https://en.wikipedia.org/wiki/ProFont "wikipedia:ProFont") ([profont](https://www.archlinux.org/packages/?name=profont))
*   [Proggy Programming Fonts](https://en.wikipedia.org/wiki/Proggy_Programming_Fonts "wikipedia:Proggy Programming Fonts") ([proggyfonts](https://aur.archlinux.org/packages/proggyfonts/))
*   Tamsyn ([tamsyn-font](https://www.archlinux.org/packages/?name=tamsyn-font))
*   [Terminus](https://en.wikipedia.org/wiki/Terminus_(typeface) ([terminus-font](https://www.archlinux.org/packages/?name=terminus-font))
*   Unifont (glifi come ಠ_ಠ (sguardo di disapprovazione)) ([bdf-unifont](https://www.archlinux.org/packages/?name=bdf-unifont))

### Sans-serif

*   [Andika](http://scripts.sil.org/cms/scripts/page.php?site_id=nrsi&id=andika) ([ttf-andika](https://aur.archlinux.org/packages/ttf-andika/), inclusi in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/))
*   [Arial](https://en.wikipedia.org/wiki/Arial "wikipedia:Arial") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Arial Black](https://en.wikipedia.org/wiki/Arial_Black "wikipedia:Arial Black") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Arimo ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Sostituto di Chrome/Chromium OS per Arial (compatibilità metrica)
*   [Calibri](https://en.wikipedia.org/wiki/Calibri "wikipedia:Calibri") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Candara](https://en.wikipedia.org/wiki/Candara "wikipedia:Candara") ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Constantia](https://en.wikipedia.org/wiki/Constantia_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Corbel](https://en.wikipedia.org/wiki/Corbel_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [DejaVu Sans](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Droid Sans](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), inclusi in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSans](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Impact](https://en.wikipedia.org/wiki/Impact_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Sans](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Alternativa a Arial (compatibilità metrica)
*   [Liberation Sans Narrow](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Alternativa ad Arial Narrow (compatibilità metrica)
*   [Linux Biolinum](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine))
*   [Lucida Sans](https://en.wikipedia.org/wiki/Lucida_Sans "wikipedia:Lucida Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Microsoft Sans Serif](https://en.wikipedia.org/wiki/Microsoft_Sans_Serif "wikipedia:Microsoft Sans Serif") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [PT Sans](https://en.wikipedia.org/wiki/PT_Sans "wikipedia:PT Sans") ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - 3 varianti principali: normale, stretto, e didascalia- Unicode: Latino, Cirillico
*   [Tahoma](https://en.wikipedia.org/wiki/Tahoma_(typeface) ([ttf-tahoma](https://aur.archlinux.org/packages/ttf-tahoma/))
*   [Trebuchet](https://en.wikipedia.org/wiki/Trebuchet_MS "wikipedia:Trebuchet MS") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Ubuntu Font Family](https://en.wikipedia.org/wiki/Ubuntu_Font_Family "wikipedia:Ubuntu Font Family") ([ttf-ubuntu-font-family](https://www.archlinux.org/packages/?name=ttf-ubuntu-font-family))
*   [Verdana](https://en.wikipedia.org/wiki/Verdana "wikipedia:Verdana") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### Script

*   [Comic Sans](https://en.wikipedia.org/wiki/Comic_Sans "wikipedia:Comic Sans") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))

### Serif

*   [Cambria](https://en.wikipedia.org/wiki/Cambria_(typeface) ([ttf-vista-fonts](https://aur.archlinux.org/packages/ttf-vista-fonts/))
*   [Charis](https://en.wikipedia.org/wiki/Charis_SIL "wikipedia:Charis SIL") (inclusi in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode: Latino, Cirillico
*   [DejaVu Serif](https://en.wikipedia.org/wiki/DejaVu_fonts "wikipedia:DejaVu fonts") ([ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu)) - Unicode
*   [Doulos](https://en.wikipedia.org/wiki/Doulos_SIL "wikipedia:Doulos SIL") (inclusi in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode: Latino, Cirillico
*   [Droid Serif](https://en.wikipedia.org/wiki/Droid_(font) ([ttf-droid](https://www.archlinux.org/packages/?name=ttf-droid), inclusi in [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/))
*   [FreeSerif](https://en.wikipedia.org/wiki/GNU_FreeFont "wikipedia:GNU FreeFont") ([ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont)) - Unicode
*   [Gentium](https://en.wikipedia.org/wiki/Gentium "wikipedia:Gentium") ([ttf-gentium](https://www.archlinux.org/packages/?name=ttf-gentium), inclusi in [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/)) - Unicode: Latino, Cirillico, Greco, alfabeto fonetico
*   [Georgia](https://en.wikipedia.org/wiki/Georgia_(typeface) ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   [Liberation Serif](https://en.wikipedia.org/wiki/Liberation_fonts "wikipedia:Liberation fonts") ([ttf-liberation](https://www.archlinux.org/packages/?name=ttf-liberation)) - Alternativa a Times New Roman (metric-compatible)
*   [Linux Libertine](https://en.wikipedia.org/wiki/Linux_Libertine "wikipedia:Linux Libertine") ([ttf-linux-libertine](https://www.archlinux.org/packages/?name=ttf-linux-libertine)) - Unicode: Latino, greco, cirillico, ebraico

*   [Times New Roman](https://en.wikipedia.org/wiki/Times_New_Roman "wikipedia:Times New Roman") ([ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/))
*   Tinos ([ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/)) - Sostituto di Chrome/Chromium OS per Times New Roman (compatibilità metrica)

### Assortiti

*   [ttf-google-fonts-git](https://aur.archlinux.org/packages/ttf-google-fonts-git/) - una vasta collezione di font gratuiti (tra cui ubuntu, inconsolata, droid, ecc.)

**Nota:** La finestra di dialogo dove vengono mostrati i font, nelle singole applicazioni, diventerannò molto lunghe perchè questo pacchetto installa sul sistema più di cento nuovi font

*   [ttf-mph-2b-damase](https://www.archlinux.org/packages/?name=ttf-mph-2b-damase) - Covers full plane 1 and several scripts
*   [ttf-sil-fonts](https://aur.archlinux.org/packages/ttf-sil-fonts/) - Gentium, Charis, Doulos, Andika e Abyssinica da SIL *(AUR)*
*   [font-bh-ttf](https://www.archlinux.org/packages/?name=font-bh-ttf) - Font Xorg Luxi
*   [ttf-cheapskate](https://www.archlinux.org/packages/?name=ttf-cheapskate) - Collezione di font di *dustismo.com*
*   [ttf-junicode](https://www.archlinux.org/packages/?name=ttf-junicode) - Caratteri junius contenenti una collezione di glifi medievali in alfabeto latino
*   [xorg-fonts-type1](https://www.archlinux.org/packages/?name=xorg-fonts-type1) — Set IBM Courier e Adobe Utopia per [Font PostScript](https://en.wikipedia.org/wiki/PostScript_fonts "wikipedia:PostScript fonts")

## Font per console

La console, ovvero un terminale in esecuzione senza *X* Window System, utilizza il carattere ASCII impostato come predefinito. Questo tipo di carattere e la mappa dei tasti utilizzati sono facilmente modificabili.

Un font per la console è limitato a 256 o 512 caratteri. I font si trovano in `/usr/share/kbd/consolefonts/`.

I *Keymaps*, la connessione tra il tasto premuto e il carattere utilizzato dal computer, si trovano nelle sottodirectory di `/usr/share/kbd/keymaps/`.

### Anteprima e verifica

Purtroppo, nessuna libreria organizzata di immagini è disponibile per le anteprime dei font per la console. L'utente può tuttavia, usare `setfont` per cambiare temporaneamente i caratteri e valutare se utilizzarli come predefiniti. I *glifi* o lettere disponibili nel carattere possono anche essere visti come una tabella con il comando `showconsolefont`.

Se il font appena modificato non è adatto, è possibile il ripristino al font di default con il comando `setfont` senza argomenti. Se la console è totalmente illeggibile, questo comando, `setfont`, sarà ancora utile all'utente mentre "digita alla cieca".

Si noti che `setfont` funziona solo sulla console attualmente in uso. Eventuali altre console, attive o inattive, rimangono inalterate.

#### Esempi

Modificare il carattere. Questo è un esempio rappresentativo:

```
$ setfont /usr/share/kbd/consolefonts/gr737b-9x16-medieval.psfu.gz

```

Oppure passare ad un carattere con 512 glifi e impostare la mappatura della tastiera a *ISO 8859-5* per mezzo dell'opzione `-m`:

```
$ setfont /usr/share/kbd/consolefonts/LatArCyrHeb-16.psfu.gz -m 8859-5

```

Poi impartire dei comandi per inviare messaggi di testo sul display, consultare magari una *manpage*, provare *vi* o *nano* e visualizzare la tabella dei glifi con il comando `showconsolefont`.

Ritornare al font di default con:

```
$ setfont

```

### Modificare il carattere predefinito

Per cambiare il font di default, le impostazioni `CONSOLEFONT=` e `CONSOLEMAP=` in `/etc/rc.conf` devono essere modificate. Si ricorda ancora che i caratteri si trovano nella cartella `/usr/share/kbd/consolefonts/` e i keymap si trovano nelle sottodirectory di `/usr/share/kbd/keymaps/`.

#### Esempi

Per la visualizzazione di caratteri come *Č, ž, đ, š* or *Ł, ę, ą, ś* usando i font `lat2-16.psfu.gz`:

```
CONSOLEFONT="lat2-16"

```

Ciò significa che la seconda parte dei caratteri ISO/IEC 8859 sono usati con il formato 16\. È possibile modificare la dimensione del carattere usando altri valori come lat2-08...16\. Per le regioni soggette alle specifiche 8859, vedere [Wikipedia](http://en.wikipedia.org/wiki/ISO/IEC_8859#The_Parts_of_ISO.2FIEC_8859). Si possono usare i caratteri Terminus, consigliati se si lavora molto in console senza server X. Per esempio ter-216b è latin-2 part, dimensione 16, grassetto. ter-216n è lo stesso, ma con peso normale. I font Terminus hanno dimensioni fino a 32.

Ora, impostare il keymap corretto; per lat2-16 sarà:

```
CONSOLEMAP="8859-2"

```

Per utilizzare il carattere specificato nello userspace iniziale, cioè nelle prime fasi del processo di avvio, aggiungere il `consolefont` abbinato a `/etc/mkinitcpio.conf`:

```
HOOKS="base udev autodetect block filesystems **consolefont** **keymap**"

```

Poi ricompilare l'immagine:

```
# mkinitcpio -p linux

```

**Note:** I passi sopra deve essere ripetuti per ogni kernel installato (avendone installati più di uno).

Consultare [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") per maggiori informazioni.