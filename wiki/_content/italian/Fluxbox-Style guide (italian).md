Articoli correlati

*   [Fluxbox (Italiano)](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)")

Questa è una lista di tutte le opzioni che si possono applicare al file `theme.cfg` con i quali si può personalizzare fluxbox a proprio piacimento.

Questa guida è suddivisa in due parti: la prima parte spiega il significato di ogni elemento, mentre la seconda è un elenco completo delle varie opzioni, che si può copiare ed incollare nel proprio `theme.cfg` per ottenere un file di base.

Per facilitarne la comprensione è stato effettuato un raggruppamento degli elementi per pertinenza.

## Contents

*   [1 Sintassi delle impostazioni](#Sintassi_delle_impostazioni)
    *   [1.1 {texture type}](#.7Btexture_type.7D)
    *   [1.2 {color}](#.7Bcolor.7D)
    *   [1.3 {filename}](#.7Bfilename.7D)
    *   [1.4 {integer}](#.7Binteger.7D)
    *   [1.5 {boolean}](#.7Bboolean.7D)
    *   [1.6 {alpha}](#.7Balpha.7D)
    *   [1.7 {round}](#.7Bround.7D)
    *   [1.8 {justify}](#.7Bjustify.7D)
    *   [1.9 {bullet}](#.7Bbullet.7D)
    *   [1.10 {string}](#.7Bstring.7D)
    *   [1.11 {font}](#.7Bfont.7D)
    *   [1.12 Spiegazione sulle opzioni che possono risultare confuse](#Spiegazione_sulle_opzioni_che_possono_risultare_confuse)
    *   [1.13 Alcune considerazioni prima di iniziare](#Alcune_considerazioni_prima_di_iniziare)
*   [2 Struttura dei vari {item}](#Struttura_dei_vari_.7Bitem.7D)
    *   [2.1 Barra degli strumenti](#Barra_degli_strumenti)
        *   [2.1.1 Impostazioni generali](#Impostazioni_generali)
        *   [2.1.2 Orologio](#Orologio)
        *   [2.1.3 Titolo dell'area di lavoro](#Titolo_dell.27area_di_lavoro)
        *   [2.1.4 La barra delle icone](#La_barra_delle_icone)
        *   [2.1.5 Empty - quando non ci sono finestre sono rappresentate come icone](#Empty_-_quando_non_ci_sono_finestre_sono_rappresentate_come_icone)
        *   [2.1.6 Icona della finestra in primo piano](#Icona_della_finestra_in_primo_piano)
        *   [2.1.7 Icona della finestra in secondo piano](#Icona_della_finestra_in_secondo_piano)
        *   [2.1.8 I pulsanti per la barra degli strumenti prev-workspace, next-workspace, prev-window e next-window](#I_pulsanti_per_la_barra_degli_strumenti_prev-workspace.2C_next-workspace.2C_prev-window_e_next-window)
    *   [2.2 Le finestre](#Le_finestre)
        *   [2.2.1 Impostazioni generali](#Impostazioni_generali_2)
    *   [2.3 Finestre in primo piano e sullo sfondo](#Finestre_in_primo_piano_e_sullo_sfondo)
        *   [2.3.1 Barra del titolo](#Barra_del_titolo)
        *   [2.3.2 Etichetta](#Etichetta)
        *   [2.3.3 Maniglia](#Maniglia)
        *   [2.3.4 grips](#grips)
        *   [2.3.5 Pulsanti](#Pulsanti)
        *   [2.3.6 Pulsanti della finestra](#Pulsanti_della_finestra)
        *   [2.3.7 chiudi](#chiudi)
        *   [2.3.8 massimizza](#massimizza)
        *   [2.3.9 riduci a icona](#riduci_a_icona)
        *   [2.3.10 stick](#stick)
        *   [2.3.11 stuck](#stuck)
    *   [2.4 Il menu](#Il_menu)
        *   [2.4.1 Impostazioni generali](#Impostazioni_generali_3)
        *   [2.4.2 Titolo - Intestazione di ogni menu](#Titolo_-_Intestazione_di_ogni_menu)
        *   [2.4.3 frame - corpo del menu](#frame_-_corpo_del_menu)
        *   [2.4.4 Evidenzia](#Evidenzia)
        *   [2.4.5 Dettagli](#Dettagli)
        *   [2.4.6 Imposta uno sfondo tramite una applicazione](#Imposta_uno_sfondo_tramite_una_applicazione)
        *   [2.4.7 The slit](#The_slit)

## Sintassi delle impostazioni

Ogni impostazione è strutturata in quattro parti: {*main_object*} **.** {*sub_object*} **.** {*item*} **:** {*value*} Es.

```
toolbar.clock.pixmap: value

```

Il valore di {*value*} è strettamente collegato al tipo di oggetto (*item*) che si vuole impostare. Ad esempio ad un *item* `.pixmap` corrisponde come *value* {filemane}

Quindi la voce pixmap necessita di un {filename} E.s

```
toolbar.clock.pixmap:  clock.xpm

```

In pratica tutto quello che bisogna sapere è quale valore può assumere ogni oggetto. Di seguito verranno elencate le varie tipologie che l'opzione **value** può assumere e per ognuno di essi i vari valori disponibili più alcuni esempi. Nella seconda parte si fornisce un elenco completo di tutti gli elementi e il tipo di valore da adottare per ciascuno di essi, e possono essere copiati nel vostro file.

### {texture type}

Per un {item} *pixmap* è richiesto nome file in *.pixmap

```
 pixmap
   tiled

```

Per un {item} *non-pixmap* si utilizza **.color** per i colori degli oggetti, mentre si usa **.colorTo** per i gradienti o per mettere in evidenza

```
 flat
   gradient
     vertical
     horizontal
     diagonal
     crossdiagonal
     pipecross
     elliptic
     rectangle
     pyramid

```

Es.

```
menu.frame: Flat Gradient Vertical

```

oppure

```
   raised
   sunken
     bevel1
     bevel2
       gradient
         vertical
         horizontal
         diagonal
         crossdiagonal
         pipecross
         elliptic
         rectangle
         pyramid

```

Es.

```
menu.title: Raised Bevel1 Gradient Vertical

```

### {color}

Si può utilizzare la la notazione esagesimale per i colori

```
 #ffffff
 #000000

```

Es.

```
menu.title.textColor: #ffffff

```

Oppure un colore espresso in rgb come mostrato in `/usr/X11R6/lib/X11/rgb.txt`

```
rgb:4/3/2

```

Es.

```
menu.title.textColor: rgb:4/3/2

```

O per nome

```
white
black

```

Es.

```
menu.title.textColor: white

```

### {filename}

Il nome di un file con estensione `.xpm` memorizzato in pixmaps, che deve trovarsi nella stessa directory in cui è presente il file `theme.cfg` Es.

```
menu.title.pixmap: iconbarf.xpm

```

### {integer}

Un numero intero che indica l'altezza e la larghezza (*height/width*) di qualcosa ed espresso in pixel Es.

```
window.title.height: 22

```

### {boolean}

Per impostare su on o su off

```
true
false

```

Es.

```
toolbar.shaped: true

```

### {alpha}

Per impostare la trasparenza - deve essere un numero intero compreso tra 0 e 255, dove 0 equivale ad invisibile/trasparente, mentre 255 equivale ad un effetto solido/opaco - il valore 150 è quello comunemente usato

Es.

```
window.alpha: 255

```

### {round}

Opzione per arrotondare gli ancogli

```
TopLeft
TopRight
BottomLeft
BottomRight

```

Es.

```
window.roundCorners: TopLeft TopRight

```

### {justify}

Posizionamento di un testo o di una immagine

```
Center
Left
Right

```

Es.

```
window.justify: Center

```

### {bullet}

Usato solamente per l'oggetto *menu.bullet*: i valori riguardano solo lo stile non-pixmaps.

```
triangle
square
diamond
empty

```

Es.

```
menu.bullet: triangle

```

### {string}

Usato solamente per l'opzione *root.command*: consente di impostare il percorso di una immagine da usare come sfondo e quale applicazione usare per visualizarlo

```
fbsetbg -f wallpaper.png

```

Es.

```
root.command: fbsetbg -a mywallpaper.png

```

### {font}

Il font che si vuole usare e la sua dimensione.

```
font-size

```

Es.

```
menu.frame.font: trebuchet-10

```

Ci sono diverse opzioni che possono essere usate in qualsiasi combinazione.

```
bold
shadow
italic

```

esse devono essere separate da una virgola o da due punti.

```
font-size:bold:shadow:italic

```

Es.

```
menu.title.font: trebuchet-10:shadow:bold

```

### Spiegazione sulle opzioni che possono risultare confuse

*   .colorTo - Se si usa un gradiente allora la scelta e tra .color e .colorTo

*   .borderWidth - Crea un bordo di altezza {integer}. 0 equivale a non avere bordi

*   .bevelwidth - è la spaziatura tra il bordo ed un oggetto", ad esempio in un menu : *menu.bevelWidth* aumenta lo spazio tra le voci di menu

*   .picColor - Imposta il colore predefinito di una immagine fluxbox che viene aggiunto in cima ad una voce

Es.

```
toolbar.button.picColor

```

*   .alpha - imposta la trasparenza

### Alcune considerazioni prima di iniziare

*   Uso di **window.label' *e* ***window.title **con** ***window.bevelWidth**.

L'uso di *window.label* si sovrappone all'opzione *window.title*. Tuttavia, se si imposta *window.bevelWidth* il *window.title* mostrerà un bordo attorno a*window.label*. In pratica *window.label* galleggia sopra *window.title*. Questo permette semplici ma fantastici effetti, ma limita i pulsanti nella finestra (vedere sotto)

*   Uso di **toolbar** e **toolbar.iconbar.***, **toolbar.clock**, **toolbar.workspace**, **toolbar.button**.

Come per il punto precedente *toolbar* viene sovrapposto da *toolbar.iconbar.**, *toolbar.clock*, *toolbar.workspace* e *toolbar.button*. Anche in questo caso impostare *toolbar.bevelWidth* permette a tutte questi oggetti di *galleggiare* sopra *toolbar* generando effetto bordo ai livelli.

*   Uso di **window buttons**.

Se *window.bevelWidth* **non** è utilizzato, allora tutti i *window.* buttons* (chiudi, riduci ad icona, ecc.) possono essere di qualsiasi dimensione, ma devono essere **quadrati** e tutti della **stessa dimensione**. Questo permette di creare pulsanti dal design creativo e molti stili di Fluxbox utilizzano questo metodo.

Tuttavia, se *window.bevelWidth* **viene' *utilizzato, i pulsanti avranno le dimensioni ridotte rispettando il* ***font* utilizzato per *window.label*.Qui la cosa migliore da fare è scegliere la dimensione dei caratteri desiderata per *window.label* quindi rendere il vostro pixmaps alla dimensione corretta. Oppure, in questo caso, è possibile impostare le opzioni di *window.button* in modo da dare uno sfondo e permettere a Fluxbox di sovrapposizionarle con il pixmaps predefinito (si può scegliere il colore con *window.button .*. picColor*) o crearne di propri con le dimensioni corrette.

*   . using * (wildcards)

## Struttura dei vari {item}

Un modello di file `theme.cfg` è presentato qui di seguito:

```
 This work is licensed under the Creative Commons
 Attribution-NonCommercial-ShareAlike License.
 To view a copy of this license, visit
 http://creativecommons.org/licenses/by-nc-sa/1.0/
 or send a letter to Creative Commons,
 559 Nathan Abbott Way, Stanford, California 94305, USA.

---------------------------------------------
 FluxMOD http://www.fluxmod.dk
 Style Name:
 Style Author:
 Style Date:
---------------------------------------------

```

### Barra degli strumenti

#### Impostazioni generali

toolbar.borderWidth: {integer}
toolbar.borderColor: {color}

toolbar.shaped: {boolean}
toolbar.alpha: {alpha}
toolbar.height: {integer}

#### Orologio

toolbar.clock.font: {font}
toolbar.clock.textColor: {color}
toolbar.clock.justify: {justify}

toolbar.clock: {texture type}
toolbar.clock.pixmap: {filename}
toolbar.clock.color: {color}
toolbar.clock.colorTo: {color}
toolbar.clock.borderWidth: {integer}
toolbar.clock.borderColor: {color}

#### Titolo dell'area di lavoro

toolbar.workspace.font: {font}
toolbar.workspace.textColor: {color}
toolbar.workspace.justify: {justify}

toolbar.workspace: {texture type}
toolbar.workspace.pixmap: {filename}
toolbar.workspace.color: {color}
toolbar.workspace.colorTo: {color}
toolbar.workspace.borderWidth: {integer}
toolbar.workspace.borderColor: {color}

#### La barra delle icone

Impostata con Iconbar Mode è quella finestra che viene mostrata cliccando col tasto destro sulla barra degli strumenti di Fluxbox

toolbar.iconbar.borderWidth: {integer}
toolbar.iconbar.borderColor: {color}

#### Empty - quando non ci sono finestre sono rappresentate come icone

toolbar.iconbar.empty: {texture type}
toolbar.iconbar.empty.pixmap: {filename}
toolbar.iconbar.empty.color: {color}
toolbar.iconbar.empty.colorTo: {color}

#### Icona della finestra in primo piano

toolbar.iconbar.focused.font: {font}
toolbar.iconbar.focused.textColor: {color}
toolbar.iconbar.focused.justify: {justify}
toolbar.iconbar.focused: {texture type}
toolbar.iconbar.focused.pixmap: {filename}
toolbar.iconbar.focused.color: {color}
toolbar.iconbar.focused.colorTo: {color}
toolbar.iconbar.focused.borderWidth: {integer}
toolbar.iconbar.focused.borderColor: {color}

#### Icona della finestra in secondo piano

toolbar.iconbar.unfocused.font: {font}
toolbar.iconbar.unfocused.textColor: {color}
toolbar.iconbar.unfocused.justify: {justify}
toolbar.iconbar.unfocused: {texture type}
toolbar.iconbar.unfocused.pixmap: {filename}
toolbar.iconbar.unfocused.color: {color}
toolbar.iconbar.unfocused.colorTo: {color}
toolbar.iconbar.unfocused.borderWidth: {integer}
toolbar.iconbar.unfocused.borderColor: {color}

#### I pulsanti per la barra degli strumenti prev-workspace, next-workspace, prev-window e next-window

toolbar.button {texture type}
toolbar.button.pixmap: {filename}
toolbar.button.color: {color}
toolbar.button.colorTo: {color}
toolbar.button.picColor: {color}
toolbar.button.pressed: {texture type}
toolbar.button.pressed.pixmap: {filename}
toolbar.button.pressed.color: {color}
toolbar.button.pressed.colorTo: {color}
toolbar.button.pressed.picColor: {color}

### Le finestre

Con *focus* si intende la finestra in primo piano , mentre con *unfocus* la finestra sullo sfondo

#### Impostazioni generali

window.font: {font}
window.justify: {justify}
window.roundCorners: {round}
window.alpha: {alpha}
window.bevelWidth: {integer}
window.borderWidth: {integer}
window.borderColor: {color}

### Finestre in primo piano e sullo sfondo

#### Barra del titolo

Lo "sfondo" "background" del titolo della finestra. Si tratta di un livello sotto *window.label* - vedere la nota nella prima parte.

window.title.height: {integer}
window.title.focus: {texture type}
window.title.focus.pixmap: {filename}
window.title.focus.color: {color}
window.title.focus.colorTo: {color}
window.title.unfocus: {texture type}
window.title.unfocus.pixmap: {filename}
window.title.unfocus.color: {color}
window.title.unfocus.colorTo: {color}

#### Etichetta

E' il testo di sfondo. Questo è un livello sopra *window.title* - vedere la nota nella prima parte.

window.label.focus: {texture type}
window.label.focus.pixmap: {filename}
window.label.focus.color: {color}
window.label.focus.colorTo: {color}
window.label.focus.textColor: {color}
window.label.unfocus: {texture type}
window.label.unfocus.pixmap: {filename}
window.label.unfocus.color: {color}
window.label.unfocus.colorTo: {color}
window.label.unfocus.textColor: {color}

#### Maniglia

La barra nella parte inferiore della finestra per il ridimensionamento verticale

window.handleWidth: {integer}
window.handle.focus: {texture type}
window.handle.focus.pixmap: {filename}
window.handle.focus.color: {color}
window.handle.focus.colorTo: {color}
window.handle.unfocus: {texture type}
window.handle.unfocus.pixmap: {filename}
window.handle.unfocus.color: {color}
window.handle.unfocus.colorTo: {color}

#### grips

Entrambi i lati della maniglia per il ridimensionamento in senso orizzontale e verticale.

window.grip.focus: {texture type}
window.grip.focus.pixmap: {filename}
window.grip.focus.color: {color}
window.grip.focus.colorTo: {color}
window.grip.unfocus: {texture type}
window.grip.unfocus.pixmap: {filename}
window.grip.unfocus.color: {color}
window.grip.unfocus.colorTo: {color}

#### Pulsanti

imposta lo sfondo per i pulsanti della finestra - non visibile se i pulsanti della finestra (sotto) sono utilizzati

window.button.focus: {texture type}
window.button.focus.pixmap: {filename}
window.button.focus.color: {color}
window.button.focus.colorTo: {color}
window.button.focus.picColor: {color}
window.button.unfocus: {texture type}
window.button.unfocus.pixmap: {filename}
window.button.unfocus.color: {color}
window.button.unfocus.colorTo: {color}
window.button.unfocus.picColor: {color}
window.button.pressed: {texture type}
window.button.pressed.pixmap: {filename}
window.button.pressed.color: {color}
window.button.pressed.colorTo: {color}

#### Pulsanti della finestra

Chiudi, massimizza e minimizza, arrotola , stick e stuck

#### chiudi

window.close.pixmap: {filename}
window.close.unfocus.pixmap: {filename}
window.close.pressed.pixmap: {filename}

#### massimizza

window.maximize.pixmap: {filename}
window.maximize.unfocus.pixmap: {filename}
window.maximize.pressed.pixmap: {filename}

#### riduci a icona

window.iconify.pixmap: {filename}
window.iconify.unfocus.pixmap: {filename}
window.iconify.pressed.pixmap: {filename}

#### stick

window.stick.pixmap: {filename}
window.stick.unfocus.pixmap: {filename}
window.stick.pressed.pixmap: {filename}

#### stuck

window.stuck.pixmap: {filename}
window.stuck.unfocus.pixmap: {filename}

### Il menu

#### Impostazioni generali

menu.borderWidth: {integer}
menu.bevelWidth: {integer}
menu.borderColor: {color}

#### Titolo - Intestazione di ogni menu

menu.title.font: {font}
menu.title.textColor: {color}
menu.title.justify: {justify}
menu.title: {texture type}
menu.title.pixmap: {filename}
menu.title.color: {color}
menu.title.colorTo: {color}

#### frame - corpo del menu

menu.frame.font: {font}
menu.frame.textColor: {color}
menu.frame.disableColor: {color}
menu.frame.justify: {justify}
menu.frame: {texture type}
menu.frame.pixmap: {filename}
menu.frame.color: {color}
menu.frame.colorTo: {color}

#### Evidenzia

Come le opzioni sono evidenziati quando il mouse è su di loro

menu.hilite.textColor: {color}
menu.hilite: {texture type}
menu.hilite.pixmap: {filename}
menu.hilite.color: {color}
menu.hilite.colorTo: {color}

#### Dettagli

menu.roundCorners: {round}
menu.bullet.position: {justify}
menu.bullet: {bullet}
menu.submenu.pixmap: {filename}
menu.selected.pixmap: {filename}
menu.unselected.pixmap: {filename}

#### Imposta uno sfondo tramite una applicazione

rootCommand: {string}

#### The slit

impostazioni per il taglio - non applicabile se è stato settato un alpha del taglio pari a 0

slit: {texture type}
slit.pixmap: {filename}
slit.color: {color}
slit.colorTo: {color}
slit.borderWidth: {integer}
slit.bevelWidth: {integer}
slit.borderColor: {color}