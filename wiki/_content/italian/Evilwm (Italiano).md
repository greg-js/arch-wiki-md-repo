[evilwm](http://www.6809.org.uk/evilwm/) è un window manager minimalista per il sistema X. È minimalista ne senso che non fornisce utilità non indispensabili come ad esempio decorazioni o cornici alle finestre ed icone. È comunque molto usabile e fornisce un ottimo controllo da tastiera con riposizionamento e massimizzazioni, trascinamento finestre, supporto snap-to-border, e desktop virtuali. La dimensione dei pacchetti binari installati è di soli 0.07 MB.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Avviare evilwm](#Avviare_evilwm)
    *   [2.2 Configurazioni d'avvio](#Configurazioni_d.27avvio)
*   [3 Uso di evilwm](#Uso_di_evilwm)
    *   [3.1 Controlli della tastiera](#Controlli_della_tastiera)
    *   [3.2 Controllo del mouse](#Controllo_del_mouse)
    *   [3.3 Desktop virtuali](#Desktop_virtuali)
*   [4 Suggerimenti](#Suggerimenti)
    *   [4.1 Massimizzazione orizzontale delle finestre](#Massimizzazione_orizzontale_delle_finestre)
    *   [4.2 Uscire da evilwm chiudendo un programma](#Uscire_da_evilwm_chiudendo_un_programma)
    *   [4.3 Ridimensionamento finestre usando la tastiera](#Ridimensionamento_finestre_usando_la_tastiera)
*   [5 Lost focus bug fix](#Lost_focus_bug_fix)
*   [6 Links](#Links)

## Installazione

Evilwm è reperibile nei repository extra, così l'installazione da console sarà:

```
# pacman -S evilwm

```

## Configurazione

### Avviare evilwm

Per avviare evilwm (senza opzioni) via *startx*, assicurarsi che il file `~/.xinitrc` contenga:

```
exec evilwm

```

evilwm non controlla direttamente lo sfondo del desktop o il cursore del mouse, perciò sarà conveniente specificarli attraverso il file `~/.xinitrc`. Ad esempio , per un colore solido come sfondo ed il bottone sinistro del tema del mouse attuale:

```
xsetroot -solid \#3f3f3f
xsetroot -cursor_name left_ptr

```

Per maggiori dettagli sulle varie opzioni possibili consultare *man xsetroot*.

### Configurazioni d'avvio

evilwm non utilizza un file di configurazione, ma delle opzioni di "interruttore" quando si avvia il window manager. Alcuni esempi di configurazione:

*   <tt>-fg *color*</tt> (colore della finestra attiva)
*   <tt>-bw *borderwidth*</tt> (larghezza dei bordi finestra in pixels)
*   <tt>-term *termprog*</tt> (specifica un programma terminale. il default è xterm)
*   <tt>-snap *number*</tt> (abilita supporto snap-to-border oltre che la vicinanza in pixels per lo snap)
*   <tt>-mask1 *modifier*</tt> (sovrascrive il predefinito ctrl+alt da tastiera con altro)
*   <tt>-nosoliddrag</tt> (disegna un contorno alla finestra quando si ridimensiona o massimizza)

Una lista completa di opzioni di configurazione per evilwm è consultabile con *man evilwm*.

In maniera predefinita, evilwm disegna un bordo d'ro di un pixel intorno alla finestra attiva. Un esempio di modifica può essere `~/.xinitrc`:

```
exec evilwm -snap 10 -bw 2 -fg red

```

che abiliterà l'opzione snap-to-border a 10 pixel di distanza e cambierà la larghezza del bordo di default a 2 ed il colore della finestra attiva a rosso.

**Nota:** evilwm può anche leggere le opzioni, una per riga, da un file chiamato `.evilwmrc` da situare nella home directory dell'utente. Le opzioni elencate in questo file di configurazione devono omettere il trattino di primo piano. Le opzioni specificate nella riga di comando per lanciare evilwm hanno la precedenza rispetto a quelle che si trovano nel file di configurazione.

## Uso di evilwm

Dop l'avvio di evilwm non si vedrà altro che il cursore del mouse e uno sfondo nero sul desktop (o un altro sfondo se diversamente specificato come descritto sopra). Per aprire un terminale, usare la combinazione tasti Ctrl+Alt+Return. I programmi possono venir eseguiti dal terminale dando *Nomedelprogramma&*.

### Controlli della tastiera

Usando sulla tastiera la combinazione Ctrl+Alt più un terzo tasto si richiameranno le seguenti funzioni:

*   Return – Apre un nuovo terminale
*   Escape – Chiude la finestra corrente
*   Insert – Minimizza la finestra corrente
*   H,J,K,L – Muove la finestra a sinistra, giù, su, 16 pixels a destra
*   Y,U,B,N – Muove la finestra in alto a sninistra, in alto a destra, in basso a sinistra, in basso a destra
*   I – Mostra informazioni sulla finestra attiva
*   = – Massimizza verticalmente la finestra attiva (toggle)
*   X – Massimizza la finestra attiva a tutto schermo (toggle)

### Controllo del mouse

Mantenendo premuto il tasto Alt si otterranno dal mouse i seguenti comportamenti:

*   Button 1 – Muove la finestra
*   Button 2 – Richiama la finestra
*   Button 3 – Minimizza la finestra

### Desktop virtuali

Con la combinazione di tasti Ctrl+Alt più un terzo tasto si otterranno i seguenti comportamenti dei desktop virtuali:

*   1-8 – Cambia il desktop virtuale
*   left – Desktop virtuale precedente
*   right – Desktop virtuale seguente
*   F – Fissa o sgancia la finestra attiva

Per muovere una finestra da un desktop virtuale all'altro, fissarla, cambiare desktop, e poi sganciarla. Alt+Tab può anche essere impiegato per muoversi da una finestra all'altra all'interno dello stesso desktop

## Suggerimenti

### Massimizzazione orizzontale delle finestre

La combinazione Ctrl+Alt+= massimizza le finestre verticalmente. Per massimizzarle orizzontalmente, usare prima Ctrl+Alt+= e poi Ctrl+Alt+X per massimizzarle orizzontalmente (al contrario usare solo Ctrl+Alt+X per la massimizzazione a pieno schermo).

### Uscire da evilwm chiudendo un programma

In modo predefinito evilwm non ha un'opzione per uscire. Per farlo, semplicemente uccidere X (Ctrl+Alt+Backspace). Si può anche terminare evilwm chiudendo un determinato programma. Invece di usare *exec evilwm* nel file `~/.xinitrc`, spostare exec ad un'altro programma. Chiudendo quest'altro programma si uscirà da evilwm. Per esempio:

```
# start evilwm (snap-to-border within 10 pixels option, 2 pixel window border, active window border red)
/usr/bin/evilwm -snap 10 -bw 2 -fg red&

```

```
# transfer exec control to xclock
# killing xclock (with ctrl+alt+escape, say) will exit evilwm
exec xclock -digital

```

### Ridimensionamento finestre usando la tastiera

Anche se non menzionato nella man-page, si possono ridimensionare le finestre con la tastiera efficacemente come con il mouse. Usando la stessa combinazione di tasti con cui si muovono le finestre, solo aggiungendo il tasto *Shift*.

Ctrl+Alt+*Shift*:

```
H,J,K,L - Rimpicciolisce la finestra orizzontalmente, ingrandisce verticalmente, rimpicciolisce verticalmente, ingrandisce horizontalmente.

```

## Lost focus bug fix

Alcuni utenti riportano un bug da cui evilwm perde il focus dopo aver chiuso una finestra. Questo comporta che evilwm non risponde più alle scorciatoie di tastiera, e se non vi è un'altra finestra aperta per ristabilire il focus con il mouse evilwm diventa inusabile e bisogna riavviarlo.

Finora la soluzione è aggiungere una linea al codice sorgente, recompilare evilwm e installarlo manualmente (non con pacman). Per correggere il bug, scaricare i sorgenti dal sito ufficiale, scompattarlo e aprire "client.c" con un editor di testo. Localizzare la funzione "remove_client" ed aggiungere quanto segue alla fine della descrizione (dopo "LOG_DEBUG"):

```
XSetInputFocus(dpy, PointerRoot, RevertToPointerRoot, CurrentTime);

```

compilare ed installare evilwm eseguendo "make" e "make install" (l'ultimo con privilegi di root).

L'autore di evilwm è a conoscenza del bug e del modo di correggerlo, ma al momento non ha ancora rilasciato una nuova versione di evilwm con le citate correzioni.

## Links

*   [evilwm](http://www.6809.org.uk/evilwm/) - Il sito ufficiale di evilwm.