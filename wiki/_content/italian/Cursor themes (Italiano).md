Esistono molti cursori disponibili per il Sistema Grafico X11 oltre il puntatore nero di default. Questa guida punta ad indicarvi dove poterli ottenere, come installarli e quindi configurarli.

## Contents

*   [1 Ottenere temi di cursori](#Ottenere_temi_di_cursori)
*   [2 Installare i temi dei cursori](#Installare_i_temi_dei_cursori)
*   [3 Configurare il tema del cursore](#Configurare_il_tema_del_cursore)
*   [4 Maggiori informazioni](#Maggiori_informazioni)

## Ottenere temi di cursori

In primo luogo, verificare quali temi sono già installati:

```
ls /usr/share/icons/*

```

Ricerca di directory con sottocartelle di cursori.

Controllare inoltre i repository ufficiali di Arch per temi cursore: [search "xcursor-"](https://www.archlinux.org/packages/?sort=&q=xcursor-&maintainer=&last_update=&flagged=&limit=50). Un tema particolarmente diffuso in molte distribuzioni è xcursor-vanilla-dmz (bianco) o la sua versione nera xcursor-vanilla-dmz-aa. Per utilizzare uno o entrambi, questi sono i comandi per installarli:

```
pacman -S xcursor-vanilla-dmz  #white
pacman -S xcursor-vanilla-dmz-aa  #black

```

**Note:** Il pacchetto [xcursor-themes](https://www.archlinux.org/packages/?name=xcursor-themes) è installato in maniera predefinita nel gruppo [xorg](https://www.archlinux.org/groups/x86_64/xorg/), e contiene già al momento dell'installazione i temi "redglass" and "whiteglass", localizzabili in `/usr/share/icons`.

Questi temi sono anche disponibili su: [AUR](https://aur.archlinux.org/packages.php?O=0&L=0&C=17&K=cursor&SeB=nd&SB=n&SO=a&PP=50&do_Search=Go).

Questi sono link dove potete trovare decine (se non centinaia) di temi di cursori:

*   [KDE Look](http://kde-look.org/index.php?xcontentmode=36)
*   [Freshmeat](http://themes.freshmeat.net/browse/982/)
*   [Customize.org](http://www.customize.org/list/xcursors)

## Installare i temi dei cursori

This manual installation method is only required if you are not using pacman to install themes like described above.

**Estraete il pacchetto del tema:**

```
$ tar -zxvf foobar-cursor-theme-package-foo.tar.gz

```

oppure

```
$ tar -jxvf foobar-cursor-theme-package-foo.tar.bz2

```

**Create una directory per il tema del cursore:**

*Esempio:* FooBar-AweSoMe-Cursors-v2.98beta

Installazione per il singolo utente corrente:

```
$ mkdir -p ~/.icons/foobar/cursors

```

Installazione *system-wide* (tutto il sistema):

```
# mkdir -p /usr/share/icons/foobar/cursors

```

**Note:** Per semplificare il nome del tema (in caso lo si debba riscrivere in seguito), il nome (ad esempio) 'foobar' è consigliabile rispetto a 'FooBar-AweSoMe-Cursors-v2.98beta' quando si vanno a creare le directory soprastanti.

**Copiare i file del cursore nelle appropriate directory:**

Installazione singolo utente:

```
$ cp -a FooBar-AweSoMe-Cursors-v2.98beta/cursors/* ~/.icons/foobar/cursors/

```

Installazione *system-wide*:

```
# cp -a FooBar-AweSoMe-Cursors-v2.98beta/cursors/* /usr/share/icons/foobar/cursors/

```

Se il pacchetto include il file index.theme controllare che abbia la riga "Inherits" all'interno. In caso affermativo, controllare che il tema esista già nel sistema con lo stesso nome. (In caso contrario rinominarlo).

**Copiare il file index.theme nella cartella appropriata:**

Installazione singolo utente:

```
$ cp -a FooBar-AweSoMe-Cursors-v2.98beta/index.theme ~/.icons/foobar/index.theme

```

Installazione *system-wide*:

```
# cp -a FooBar-AweSoMe-Cursors-v2.98beta/index.theme /usr/share/icons/foobar/index.theme

```

Se il pacchetto non include il file index.theme o al suo interno non compare la riga "Inherits", non c'è bisogno di eseguire il passaggio.

**Create i link ai cursori mancanti:**

Alcune applicazioni potrebbe continuare ad usare i cursori di default di X11 se il nuovo tema non ne ha a disposizione. Se questo problema affligge il nuovo tema, è possibile risolverlo aggiungendo semplicemente dei link per tutti i cursori. Per esempio:

```
$ cd ~/.icons/foobar/cursors/
$ ln -s right_ptr arrow
$ ln -s cross crosshair
$ ln -s right_ptr draft_large
$ ln -s right_ptr draft_small
$ ln -s cross plus
$ ln -s left_ptr top_left_arrow
$ ln -s cross tcross
$ ln -s hand hand1
$ ln -s hand hand2
$ ln -s left_side left_tee
$ ln -s left_ptr ul_angle
$ ln -s left_ptr ur_angle
$ ln -s left_ptr_watch 08e8e1c95fe2fc01f976f1e063a24ccd

```

Se i link qui riportati non risolvono il problema, cercare in `/usr/share/icons/whiteglass/cursors` dei cursori addizionali che il proprio tema potrebbe non avere, quindi creare i link come riportato sopra.

## Configurare il tema del cursore

Se si utilizza un ambiente desktop come Gnome, è possibile utilizzare il tool specifico per scegliere i temi dei cursori.

Per cambiare localmente il tema del cursore, basta aggiungere la seguente riga al file `~/.Xresources`:

```
Xcursor.theme: foobar

```

Assicurarsi che il tema del cursore sia richiamato al caricamento dal proprio window manager. Se così non fosse si può forzarlo a caricare prima il gestore di finestre mettendo il seguente comando in `~/.xinitrc` o [.xprofile](/index.php/.xprofile ".xprofile") (dipende dalla propria configurazione).

```
xrdb ~/.Xresources &

```

Fare riferimento alla documentazione del proprio window manager per maggiori informazioni.

Alternativamente, si può creare un link simbolico (un *symlink*) "default" in `~/.icons`, che punti al tema desiderato:

```
$ ln -s /usr/share/icons/foobar/ ~/.icons/default

```

Se invece si opta per cambiare a livello di sistema il tema del cursore (e renderlo omogeneo ad esempio anche al login con kdm, gdm, ...), o si riscontrano problemi con i metodi illustrati sopra (ad esempio con Firefox), creare la directory `/usr/share/icons/default/` **(solo se necessario)**:

```
# mkdir -p /usr/share/icons/default  **(solo se necessario)**

```

Modificare o creare il file `/usr/share/icons/default/index.theme` e aggiungere la riga seguente:

```
 [icon theme] 
Inherits=foobar

```

Se invece si ha o si vuole solo ~/.icons, creare la directory `~/.icons/default/`:

```
$ mkdir -p ~/.icons/default

```

Quindi creare il file `~/.icons/default/index.theme` con lo stesso contenuto del soprastante `/usr/share/icons/default/index.theme`.

In caso il proprio tema supporti diverse dimensioni, è possibile aggiungere al file `~/.Xdefaults` la seguente riga:

```
Xcursor.size:  32       #  32, 48 o 64 sono probabili buone dimensioni

```

Se non si conoscono le dimensioni supportate dal proprio tema, far partire X11 senza la precedente opzione. Il window manager sceglierà la dimensione automaticamente.

## Maggiori informazioni

Per maggiori informazioni sui cursori in X11 (directory supportate, formati, compatibilità, ecc.) riportatevi alla pagina di manuale:

```
$ man Xcursor

```

**Nota:** Se le animazioni soffrono di uno sfarfallio su macchine con scheda video Nvidia, aggiungere la seguente riga al file `/etc/X11/xorg.conf`, nella sezione device, per risolvere il problema:

```
Option "HWCursor" "off"

```