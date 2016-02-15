Fontconfig è una libreria progettata per fornire un elenco di [fonts](/index.php/Fonts_(Italiano) "Fonts (Italiano)") disponibili per le applicazioni, e anche per la configurazione necessaria ad ottenere il relativo rendering. Vedere il pacchetto [fontconfig](https://www.archlinux.org/packages/?name=fontconfig) e [Wikipedia:Fontconfig](https://en.wikipedia.org/wiki/Fontconfig "wikipedia:Fontconfig"). La libreria Free type (pacchetto [freetype2](https://www.archlinux.org/packages/?name=freetype2)) renderizza i font, sulla base di questa configurazione.

Anche se Fontconfig è l'attuale standard in Linux, alcune applicazioni si basano ancora sul metodo originale di categorizzazione dei font: la configurazione di Xorg server.

I pacchetti rendering dei font su Arch Linux includono il supporto per _freetype2_ con l'interprete bytecode (BCI) abilitato. Esistono dei pacchetti patchati per migliorare il rendering dei fonts, specialmente con monitor LCD. Vedere la sezione [#Pacchetti con patch](#Pacchetti_con_patch) riportata più avanti. Il pacchetto [#Infinality](#Infinality) consente sia l'auto-hinting che il subpixel rendering, permette la regolazione dei filtri LCD senza ricompilare e migliora l'auto-hinting dei caratteri in grassetto.

## Contents

*   [1 Percorso dei fonts](#Percorso_dei_fonts)
*   [2 Configurazione fontconfig](#Configurazione_fontconfig)
    *   [2.1 Presets](#Presets)
    *   [2.2 Anti-aliasing](#Anti-aliasing)
    *   [2.3 Hinting](#Hinting)
        *   [2.3.1 Byte-Code Interpreter (BCI)](#Byte-Code_Interpreter_.28BCI.29)
        *   [2.3.2 Autohinter](#Autohinter)
        *   [2.3.3 Hint style](#Hint_style)
    *   [2.4 Subpixel rendering](#Subpixel_rendering)
        *   [2.4.1 Filtro LCD](#Filtro_LCD)
        *   [2.4.2 Specifiche filtro LCD avanzate](#Specifiche_filtro_LCD_avanzate)
    *   [2.5 Disabilitare l'auto-hinter per i caratteri in grassetto](#Disabilitare_l.27auto-hinter_per_i_caratteri_in_grassetto)
    *   [2.6 Abilitare l'anti-aliasing solo per i caratteri grandi](#Abilitare_l.27anti-aliasing_solo_per_i_caratteri_grandi)
    *   [2.7 Sostituire i font](#Sostituire_i_font)
    *   [2.8 Disattivare i font bitmap](#Disattivare_i_font_bitmap)
    *   [2.9 Creare stili grassetto e corsivo per i font incompleti](#Creare_stili_grassetto_e_corsivo_per_i_font_incompleti)
    *   [2.10 Cambiare le regole di overriding](#Cambiare_le_regole_di_overriding)
    *   [2.11 Esempio configurazione fontconfig](#Esempio_configurazione_fontconfig)
*   [3 Pacchetti con patch](#Pacchetti_con_patch)
    *   [3.1 Infinality](#Infinality)
    *   [3.2 Ubuntu](#Ubuntu)
    *   [3.3 Ripristino dei pacchetti senza patch](#Ripristino_dei_pacchetti_senza_patch)
*   [4 Applicazioni senza supporto fontconfig](#Applicazioni_senza_supporto_fontconfig)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Caratteri distorti](#Caratteri_distorti)
    *   [5.2 Applicazioni GTK e QT meno recenti](#Applicazioni_GTK_e_QT_meno_recenti)
*   [6 Ulteriori risorse](#Ulteriori_risorse)

## Percorso dei fonts

Per poter essere riconosciuti dalle applicazioni, i fonts devono essere catalogati per un accesso facile e veloce.

I percorsi dei font inizialmente noti a Fontconfig sono: `/usr/share/fonts/` e `~/.fonts/` (dei quali Fontconfig esegue la scansione in modo ricorsivo). Per facilità di organizzazione e di installazione, si raccomanda di utilizzare questi percorsi dei font quando si [installano nuovi font](/index.php/Fonts_(Italiano) "Fonts (Italiano)").

Per visualizzare un elenco di caratteri conosciuti da Fontconfig:

```
fc-list : file

```

Vedere `man fc-list` per maggiori informazioni.

Verificare la presenza di percorsi di font Xorg noti esaminando il log:

```
$ grep /fonts /var/log/Xorg.0.log

```

**Suggerimento:** E' possibile vedere la lista dei percorsi dei caratteri riconosciuti da [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") utilizzando il comando `xset q`.

Tenere presente che Xorg non esegue la ricerca in modo ricorsivo attraverso la cartella `/usr/share/fonts` come Fontconfig. Per aggiungere un percorso, bisogna specificarlo in modo completo:

```
Section "Files"
  FontPath  "/usr/share/fonts/local"
EndSection

```

Se si vogliono impostare i percorsi dei caratteri per ogni utente, è possibile aggiungere e rimuovere gli stessi aggiungendo al file `~/.xinitrc` quanto segue:

```
xset +fp /usr/share/fonts/local/  # Prepend a custom font path to Xorg's list of known font paths
xset -fp /usr/share/fonts/sucky_fonts/  # Remove the specified font path from Xorg's list of known font paths

```

Per visualizzare un elenco di caratteri Xorg noti usare `xlsfonts`, dal pacchetto [xorg-xlsfonts](https://www.archlinux.org/packages/?name=xorg-xlsfonts).

## Configurazione fontconfig

Fontconfig è documentato nella relativa man page [fonts.conf](http://fontconfig.org/fontconfig-user.html)

La configurazione può essere effettuata sia per il singolo utente attraverso `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, che globalmente con `/etc/fonts/local.conf`. Le impostazioni di configurazione per il singolo utente hanno la precedenza sulla configurazione globale. Entrambi i file utilizzano la stessa sintassi.

**Nota:** File di configurazione e cartelle: `~/.fonts.conf`, `~/.fonts.conf.d` e `~/.fontconfig/*.cache-*` sono deprecati da fontconfig 2.10.1 ([upstream commit](http://cgit.freedesktop.org/fontconfig/commit/?id=8c255fb185d5651b57380b0a9443001e8051b29d)) e non saranno leggibili nelle future versioni del pacchetto. Utilizzare rispettivamente `$XDG_CONFIG_HOME/fontconfig/fonts.conf`, `$XDG_CONFIG_HOME/fontconfig/conf.d` e `$XDG_CACHE_HOME/fontconfig/*.cache-*`.

Fontconfig raccoglie tutte le configurazioni in un file centrale (`/etc/fonts/fonts.conf`). Questo è un file temporaneo e non deve essere modificato in quanto viene sostituito durante gli aggiornamenti di fontconfig. Fontconfig informa le applicazioni di attingere a questo file per conoscere i font disponibili e come devono venir randerizzati. Questo file è un insieme di regole dalle varie configurazioni di fontconfig (la configurazione globale (`/etc/fonts/local.conf`), i preset configurati in `/etc/fonts/conf.d/`, e il file di configurazione utente (`$XDG_CONFIG_HOME/fontconfig/fonts.conf`).

**Nota:** Per alcuni ambienti desktop (come [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)") e [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)")) utilizzando il _Font Control Panel_ si creerà o sovrascriverà automaticamente il file di configurazione font dell'utente. Per questi ambienti desktop, è meglio far corrispondere le configurazioni già definite dei font per ottenere il comportamento previsto.

I file di configurazione di Fontconfig utilizzano il formato [XML](https://en.wikipedia.org/wiki/XML "wikipedia:XML") e necessitano di questi headers:

```
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <!-- settings go here --> 

</fontconfig>

```

Per evitare ripetizioni, il resto degli esempi di configurazione in questo articolo ometteranno questi tag.

### Presets

Ci sono già una serie di preset configurati nella directory `/etc/fonts/conf.avail`. Questi preset possono essere legati sia all'impostazione del singolo utente, che a quella globale del sistema, tramite la creazione di [link simbolici](https://en.wikipedia.org/wiki/Symbolic_link "wikipedia:Symbolic link"), come descritto in `/etc/fonts/conf.d/README`. I preset sovrascriveranno le impostazioni corrispondenti nei loro rispettivi file di configurazione.

Ad esempio, per abilitare il rendering sub-pixel RGB a livello globale:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/10-sub-pixel-rgb.conf

```

Per fare la stessa cosa modificando la configurazione per il singolo utente:

```
$ mkdir $XDG_CONFIG_HOME/fontconfig/conf.d
$ ln -s /etc/fonts/conf.avail/10-sub-pixel-rgb.conf

```

$XDG_CONFIG_HOME/fontconfig/conf.d

### Anti-aliasing

[Anti-aliasing](https://en.wikipedia.org/wiki/Antialiased_font "wikipedia:Antialiased font") (rasterizzazione dei caratteri) converte i font vettori a bitmap per la visualizzazione, e in tal modo fornisce un effetto di arrotondamento dei font. Senza anti-aliasing (anche a valori DPI maggiori) i caratteri apparirebbero frastagliati, così anti-aliasing è abilitato di default.

```
  <match target="font">
    <edit name="antialias" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

### Hinting

[Font hinting](https://en.wikipedia.org/wiki/Font_hinting "wikipedia:Font hinting") regola la spaziatura dei caratteri in modo che siano allineati con la griglia dei pixel. Conosciuto anche come "instructing", fa uso di istruzioni matematiche per regolare la visualizzazione dei caratteri in modo che si allineino con una griglia rasterizzata, come quella dei pixel in un display. I caratteri non correttamente allineati senza hinting fino alla visualizzazione, hanno valori di 300 [DPI](https://en.wikipedia.org/wiki/Dots_per_inch "wikipedia:Dots per inch") o più. Sono disponibili due tipi di hinting.

#### Byte-Code Interpreter (BCI)

Utilizzando l'hinting normale, le istruzioni TrueType hinting nei font vengono interpretate da freetype "Byte-Code Interpreter". Questo funziona meglio per i font con un buon livello di istruzioni hinting.

Per abilitare il normal hinting:

```
  <match target="font">
    <edit name="hinting" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Autohinter

Un'autoimpostazione per l'hinting. Viene visualizzato peggio che con l'hinting normale per i font con buon livello di instruzioni, ma meglio per quelli con poco o nessun livello di istruzioni. L'autohinter ed il subpixel rendering non sono progettati per lavorare insieme e non dovrebbero essere utilizzati in combinazione.

Per abilitare l'autohinter:

```
  <match target="font">
    <edit name="autohint" mode="assign">
      <bool>true</bool>
    </edit>
  </match>

```

#### Hint style

Hint style è il valore di "incidenza" che la modalità **hinting** può avere. Hinting può essere impostato su: `hintfull`, `hintmedium`, `hintslight` (consigliato) e `hintnone`. Con il BCI hinting, hintfull dovrebbe funzionare meglio per molti font. Senza autohinter, è consigliabile hintslight.

```
  <match target="font">
    <edit name="hintstyle" mode="assign">
      <const>hintslight</const>
    </edit>
  </match>

```

### Subpixel rendering

Subpixel rendering effettivamente triplica la risoluzione orizzontale (o verticale) per i font facendo uso dei subpixel. L'autohinter ed il subpixel rendering non sono progettati per lavorare insieme e non dovrebbero essere utilizzati in combinazione.

La maggior parte dei monitor attuali usano specifiche per il rosso, il verde e il blu (RGB). Fontconfig avrà bisogno di conoscere il tipo di monitor per poter visualizzare correttamente i font.

_RGB (molto comune), BGR, V-RGB (verticale), o V-BGR_

Per abilitare il subpixel rendering:

```
  <match target="font">
    <edit name="rgba" mode="assign">
      <const>rgb</const>
    </edit>
  </match>

```

Se si notano delle imperfezioni o dei colori insoliti attorno ai caratteri, si può correggere l'errata configurazione dei pixel. La pagina [qui](http://www.lagom.nl/lcd-test/subpixel.php) può aiutare ad identificare il monitor.

#### Filtro LCD

Quando si utilizza sub pixel rendering, è necessario abilitare il filtro LCD, che è progettato per ridurre la frangiatura del colore. Ciò è descritto in [LCD filtering](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html) nella FreeType 2 API reference. Altre opzioni sono descritte in [FT_LcdFilter](http://www.freetype.org/freetype2/docs/reference/ft2-lcd_filtering.html#FT_LcdFilter) e sono illustrate nella pagina [LCD filter test](http://www.spasche.net/files/lcdfiltering/).

Il `lcddefault` filtro funzionerà per la maggior parte degli utenti. Altri filtri disponibili che possono essere usati in situazioni particolari: `lcdlight`; un filtro leggero ideale per quei caratteri che sembrano troppo "grossi" o "sfocati", `lcdlegacy`, il filtro Cairo originale; e `lcdnone` per disabilitarlo completamente.

```
  <match target="font">
    <edit mode="assign" name="lcdfilter">
      <const>lcddefault</const>
    </edit>
  </match>

```

#### Specifiche filtro LCD avanzate

Se i filtri incorporati LCD disponibili non sono soddisfacenti, è possibile modificare il rendering dei font molto specificatamente compilando un pacchetto freetype2 personalizzato e modificando i filtri. Per compilare ed installare i pacchetti da sorgente si può utilizzare l'[Arch Build System](/index.php/Arch_Build_System_(Italiano) "Arch Build System (Italiano)").

**Note:** Il pacchetto [Infinality](#Infinality) consente di ottimizzare l'impostazione del filtro con una variabile d'ambiente, senza ricompilare.

Per prima cosa, fare un "refresh" del PKGBUILD di freetype2 da root:

```
# abs extra/freetype2

```

Questo esempio utilizza `/var/abs/build` come la cartella di compilazione, sostituirla secondo la propria configurazione ABS personale. Scaricare ed estrarre il pacchetto freetype2 come utente normale:

```
$ cd /var/abs/build
$ cp -r ../extra/freetype2 .
$ cd freetype2
$ makepkg -o

```

Modificare il file `src/freetype-VERSION/src/base/ftlcdfil.c` e cercare la definizione della costante `default_filter[5]`:

```
static const FT_Byte  default_filter[5] =
    { 0x10, 0x40, 0x70, 0x40, 0x10 };

```

Questa costante definisce un filtro low-pass applicato alla randerizzazione del carattere. Modificarlo in base alle esigenze. Salvare il file, compilare e installare il pacchetto personalizzato:

```
$ makepkg -e
$ sudo pacman -Rd freetype2
$ sudo pacman -U freetype2-VERSION-ARCH.pkg.tar.xz

```

Riavviare o reiniziare X. Il filtro predefinito lcd dovrebbe ora randerizzare i font differentemente.

### Disabilitare l'auto-hinter per i caratteri in grassetto

L'auto-hinter utilizza sofisticati metodi per il rendering dei font, ma spesso rende i caratteri in grassetto troppo grossi. Una soluzione può essere disattivare l'auto-hinter per i caratteri in grassetto, pur mantenendolo per il resto:

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

### Abilitare l'anti-aliasing solo per i caratteri grandi

_Consultare anche [sharpfonts.co.cc](http://sharpfonts.co.cc/) per ulteriori informazioni_

Alcuni utenti preferiscono una visualizzazione più nitida non ottenibile con l'anti-aliasing:

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
        <double>16</double>
    </test>
    <edit name="antialias" mode="assign">
        <bool>true</bool>
    </edit>
</match>
...

```

### Sostituire i font

Il modo più sicuro per farlo è di aggiungere del codice XML simile a quello qui sotto. Questo farà sì che Bitstream Vera Sans venga utilizzato al posto di Helvetica:

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

Un approccio alternativo è quello di impostare il font "preferito", ma _questo funziona solo se il font originale non è presente sul sistema_, nel qual caso quello specificato verrà quindi sostituito:

```
...
< !-- Replace Helvetica with Bitstream Vera Sans Mono -->
< !-- Note, an alias for Helvetica should already exist in default conf files -->
<alias>
    <family>Helvetica</family>
    <prefer><family>Bitstream Vera Sans Mono</family></prefer>
    <default><family>fixed</family></default>
</alias>
...

```

### Disattivare i font bitmap

Per disattivare i font bitmap in fontconfig, usare `70-no-bitmaps.conf` (che di default non è incluso in fontconfig):

```
# cd /etc/fonts/conf.d
# rm 70-yes-bitmaps.conf
# ln -s ../conf.avail/70-no-bitmaps.conf

```

Se non esiste, non è necessario rimuovere `70-yes-bitmaps.conf`. E' possibile scegliere i tipi di carattere per sostituire i font bitmap con (Helvetica, Courier e Times bitmap mapts per i font TTF) da:

```
# cd /etc/fonts/conf.d
# ln -s ../conf.avail/29-replace-bitmap-fonts.conf

```

Per disabilitare i caratteri bitmap incorporati per un carattere specifico:

```
<match target="font">
  <test qual="any" name="family">
    <string>Monaco</string>
  </test>
  <edit name="embeddedbitmap"><bool>false</bool></edit>
</match>

```

### Creare stili grassetto e corsivo per i font incompleti

Freetype ha la capacità di creare automaticamente gli stili _corsivo_ e **grassetto** per i font che non li hanno, ma solo se esplicitamente richiesto dall'applicazione. Dato che di rado i programmi inviano tali richieste, in questa sezione verrà trattata la creazione manuale forzata degli stili mancanti.

Iniziare modificando `/usr/share/fonts/fonts.cache-1` come spiegato di seguito. Conservare una copia delle modifiche su un altro file, poiché un aggiornamento font eseguito con `fc-cache` sovrascriverà `/usr/share/fonts/fonts.cache-1`.

Supponendo che il font Dupree sia installato:

```
"dupree.ttf" 0 "Dupree:style=Regular:slant=0:weight=80:width=100:foundry=unknown:index=0:outline=True:_etc..._

```

Duplicare la riga, e cambiare `style=Regular` con `style=Bold` o qualsiasi altro stile. Modificare inoltre `slant=0` con `slant=100` per corsivo, `weight=80` con `weight=200` per grassetto, o entrambi per _**grassetto corsivo**_:

```
"dupree.ttf" 0 "Dupree:style=Bold Italic:slant=100:weight=200:width=100:foundry=unknown:index=0:outline=True:_etc..._

```

A questo punto aggiungere le modifiche necessarie a `$XDG_CONFIG_HOME/fontconfig/fonts.conf`:

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

**Tip:** Utilizzare il valore "embolden" per i caratteri in grassetto esistenti, al fine di renderli ancora più evidenti.

### Cambiare le regole di overriding

Fontconfig elabora i file in `/etc/fonts/conf.d` in ordine numerico inverso. Questo innesca ed abilita le regole o i file a sovrascriversi, ma spesso confonde l'utente su quale file verrà analizzato per ultimo.

Per garantire che le impostazioni personali prevalgano su tutte le altre regole, cambiare il loro ordine:

```
# cd /etc/fonts/conf.d
# mv 50-user.conf 00-user.conf

```

Questo cambiamento sembra però essere poco utile nella maggior parte dei casi, poiché l'utente ha la facoltà di controllare, in maniera predefinita, le proprie impostazioni e preferenze, come le proprietà hinting e antialiasing, l'aggiunta di font, eccetera.

### Esempio configurazione fontconfig

Esempi di configurazioni fontconfig possono essere trovati in questa [pagina](/index.php/Font_configuration/Examples "Font configuration/Examples").

Un semplice punto di partenza:

 `/etc/fonts/local.conf` 

```
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
 <match target="font">
  <edit mode="assign" name="rgba">
   <const>rgb</const>
  </edit>

  <edit mode="assign" name="hinting">
   <bool>true</bool>
  </edit>

  <edit mode="assign" name="hintstyle">
   <const>hintslight</const>
  </edit>

  <edit mode="assign" name="antialias">
   <bool>true</bool>	
  </edit>

  <edit mode="assign" name="lcdfilter">
    <const>lcddefault</const>	
  </edit>

 </match>

</fontconfig>

```

## Pacchetti con patch

Questi pacchetti con le patch sono disponibili su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"). Alcune considerazioni:

*   La configurazione è di solito necessaria.
*   Il nuovo rendering dei font, non verrà visualizzato fino a quando le applicazioni verranno riavviate.
*   Le applicazioni con [collegamenti statici](https://en.wikipedia.org/wiki/Static_library "wikipedia:Static library") alle librerie non saranno influenzati dalle patch applicate alle librerie di sistema.

### Infinality

**Attenzione:** Dall'[aggiornamento di Fontconfig 2.10.1](https://www.archlinux.org/news/fontconfig-2101-update-manual-intervention-required/), gli utenti Infinality riceveranno molti avvisi simili a:

`Fontconfig warning: "/etc/fonts/infinality/conf.d/60-group-non-tt-fonts.conf", line 483: Having multiple values in <test> isn't supported and may not works as expected`

Attualmente si sta lavorando per evitare questi avvisi. Vedere: [this article](http://www.infinality.net/forum/viewtopic.php?f=2&t=254) per maggiori informazioni.

Il patchset infinality mira a migliorare notevolmente il rendering dei font freetype2\. Aggiunge nuove funzionalità multiple.

*   [Home page](http://www.infinality.net/blog/infinality-freetype-patches/).
*   [Forum](http://www.infinality.net/forum/).

I settaggi di Infinality sono tutti configurabili in fase di esecuzione tramite variabili d'ambiente in `/etc/profile.d/infinality-settings.sh`, ed includono quanto segue:

*   **Emboldening Enhancement**: Disabilita e ingrossa, producendo un risultato migliore sui font senza versioni grassetto. Funziona su hinter nativo TT e autohinter.
*   **Auto-Autohint**: Forza automaticamente l'autohint sui font che non contengono istruzioni TT.
*   **Autohint Enhancement**: Rende lo snap autohint orizzontale ai pixels. Dà un risultato che appare come un buon hinting dei truetype font, ma è 100% libero da licenze.
*   **Customized FIR Filter**: Seleziona [i valori del filtro](http://www.infinality.net/forum/viewtopic.php?f=2&t=19) in fase di esecuzione. Funziona su hinter nativo TT e autohinter.
*   **Stem Alignment**: Allinea i bitmap glyph per ottimizzare gli estremi dei pixel. Funziona su hinter nativo TT e autohinter.
*   **Pseudo Gamma Correction**: Schiarisce e oscura i glyph ai valori dati, sotto a certe dimensioni. Funziona su hinter nativo TT e autohinter.
*   **Embolden Thin Fonts**: Ingrossa caratteri sottili o leggeri per renderli più visibili. Funziona su autohinter.
*   **Force Slight Hinting**: Abilitarlo quando i programmi richiedono più hinting. Se si utilizza il file local.conf (incluso nel pacchetto infinality-settings di fedora) si noteranno dei miglioramenti sui caratteri @font-face.
*   **ChromeOS Style Sharpening**: ChromeOS utilizza una patch per migliorare l'aspetto dei fonts. Questa patch è ora inclusa nel patchset infinality.

Un certo numero di configurazioni pre-impostate sono incluse e possono essere utilizzate impostando la variabile USE_STYLE in `/etc/profile.d/infinality-settings.sh`.

[freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) può essere installato da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"). Inoltre, se si utilizza [lib32-freetype2](https://www.archlinux.org/packages/?name=lib32-freetype2) da [multilib], sostituirlo con [lib32-freetype2-infinality](https://aur.archlinux.org/packages/lib32-freetype2-infinality/) da AUR. AUR contiene anche la versione Git di freetype2 che compilerà l'ultimo snapshot di sviluppo di freetype2 con il patchset Infinality: [freetype2-git-infinality](https://aur.archlinux.org/packages/freetype2-git-infinality/), [lib32-freetype2-git-infinality](https://aur.archlinux.org/packages/lib32-freetype2-git-infinality/).

Si raccomanda di installare anche [fontconfig-infinality](https://aur.archlinux.org/packages/fontconfig-infinality/) per abilitare la selezione degli stili predefiniti in sostituzione dei caratteri e delle impostazioni di antialiasing, oltre alle impostazioni di rendering del motore stesso. Fatto ciò, è possibile selezionare lo stile del carattere (win7, winxp, OSX, Linux, ...) con:

```
# infctl setstyle

```

Se si imposta, ad esempio win7 oppure osx è necessario avere installato i relativi caratteri.

**Nota:** Le impostazioni predefinite di infinality possono far si che alcuni programmi visualizzino caratteri a 72 DPI anzichè a 96\. Se si riscontra il suddetto problema, aprire il file /etc/fonts/infinality/infinality.conf, cercare la sezione DPI e cambiare il valore da 72 a 96\. Questo problema è frequente in particolare su conky, i cui caratteri appariranno più piccoli di quanto dovrebbero. Questo causerà il disallineamento con le immagini.

**Nota:** _Il file README per [freetype2-infinality](https://aur.archlinux.org/packages/freetype2-infinality/) vers. 2.4.8-5 dice: /etc/fonts/local.conf non esiste, o non contiene configurazioni legate ad infinality. Il file local.conf è ora obsoleto e completamente sostituito da questa configurazione._

per maggiori informazioni vedere questo articolo: [http://www.infinality.net/forum/viewtopic.php?f=2&t=77](http://www.infinality.net/forum/viewtopic.php?f=2&t=77)

### Ubuntu

Ubuntu aggiunge configurazioni extra, ed occasionalmente patcha le librerie di rendering dei fonts.

Installare i pacchetti con le patch da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"), i nomi dei pacchetti sono: [freetype2-ubuntu](https://aur.archlinux.org/packages/freetype2-ubuntu/), [fontconfig-ubuntu](https://aur.archlinux.org/packages/fontconfig-ubuntu/), [libxft-ubuntu](https://aur.archlinux.org/packages/libxft-ubuntu/), [cairo-ubuntu](https://aur.archlinux.org/packages/cairo-ubuntu/).

E' necessario aggiungere la configurazione globale. Vedere [Configurazione fontconfig](https://wiki.archlinux.org/index.php/Font_Configuration_%28Italiano%29#Configurazione_fontconfig) per un punto di partenza.

### Ripristino dei pacchetti senza patch

Per ripristinare i pacchetti senza patch, reinstallare gli originali:

```
# pacman -S --asdeps freetype2 libxft cairo fontconfig

```

## Applicazioni senza supporto fontconfig

Alcune applicazioni come [URxvt](/index.php/URxvt "URxvt") ignoreranno le impostazioni di fontconfig. Questo è molto evidente quando si utilizzano le patch infinality, per le quali è molto importante una corretta configurazione. È possibile aggirare questo problema utilizzando `~/.Xresources` , ma non è così flessibile come fontconfig. Esempio (vedere [#Fontconfig configuration](#Fontconfig_configuration) per chiarimenti sulle opzioni):

 `~/.Xresources` 

```
Xft.autohint: 0
Xft.lcdfilter:  lcddefault
Xft.hintstyle:  hintfull
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb

```

Assicurarsi che le impostazioni vengono caricate correttamente all'avvio di X con **xrdb -q** (Consultare [Xresources](/index.php/Xresources "Xresources") per maggiori informazioni).

## Risoluzione dei problemi

### Caratteri distorti

**Nota:** 96 DPI non è uno standard. Per ottenere una corretta visualizzazione dei caratteri si dovrebbero impostare i DPI del proprio monitor, specialmente quando si utilizzano la renderizzazione subpixels.

Se, inaspettatamente, i caratteri continuano ad essere grandi o piccoli, sproporzionati o semplicemente non vengono visualizzati correttamente, fontconfig potrebbe stare utilizzando dei DPI non corretti.

Fontconfig dovrebbe essere in grado di rilevare i parametri DPI, come rilevato dal server Xorg. E' possibile controllare l'auto-rilevazione dei DPI con `xdpyinfo`:

 `$ xdpyinfo | grep dots`  `  resolution:    102x102 dots per inch` 
**Nota:** Per utilizzare il comando _xdpyinfo_, è necessario installare il pacchetto [xorg-xdpyinfo](https://www.archlinux.org/packages/?name=xorg-xdpyinfo).

Se i DPI non sono correttamente rilevati (di solito a causa di un errato EDID monitor), è possibile specificarli manualmente nella configurazione di Xorg, vedere [Dimensione dello schermo e DPI](https://wiki.archlinux.org/index.php/Xorg_%28Italiano%29#Dimensione_dello_schermo_e_DPI). Questa è la soluzione raccomandata, ma potrebbe non funzionare con alcuni driver.

Fontconfig userà il valore di Xft.dpi, se impostato. Xft.dpi è solitamente impostato dal desktop environment (di solito l'impostazione DPI di Xorg) o manualmente in `~/.Xdefaults` o `~/.Xresources`. Utilizzare xrdb per trovare il valore:

 `$ xrdb -query | grep dpi`  `Xft.dpi: 102` 

Se questi problemi dovessero persistere è possibile impostare manualmente i DPI utilizzati da fontconfig:

```
...
<match target="pattern">
   <edit name="dpi" mode="assign"><double>102</double></edit>
</match>
...

```

### Applicazioni GTK e QT meno recenti

Le applicazioni GTK moderne abilitano Xft in maniera predefinita, diversamente dalle versioni precedenti alla 2.2\. Se non è possibile aggiornare queste applicazioni, forzare Xft per le vecchie applicazioni [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), aggiungendo al file `~/.bashrc`:

```
export GDK_USE_XFT=1

```

Per applicazioni QT datate:

```
export QT_XFT=true

```

## Ulteriori risorse

*   [Fonts in X11R6.8.2](http://www.x.org/X11R6.8.2/doc/fonts.html) - Informazioni font Xorg ufficiali
*   [FreeType 2 Overview](http://freetype.sourceforge.net/freetype2/)
*   [Gentoo font-rendering thread](https://forums.gentoo.org/viewtopic-t-723341.html)