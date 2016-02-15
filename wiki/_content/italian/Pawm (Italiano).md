Questo wiki descrive nei dettagli l'installazione e la configurazione del gestore delle finestre PAWM su Arch Linux.

**Nota:** Il pacchetto non è più mantenuto. L'ultima versione rilasciata è la 2.3.0.

## Contents

*   [1 Introduzione](#Introduzione)
    *   [1.1 Cenni storici su PAWM](#Cenni_storici_su_PAWM)
*   [2 Installazione](#Installazione)
*   [3 Avviare PAWM](#Avviare_PAWM)
*   [4 Configurazione (migliorare PAWM)](#Configurazione_.28migliorare_PAWM.29)
    *   [4.1 Icone](#Icone)
*   [5 Avvio automatico dei programmi](#Avvio_automatico_dei_programmi)
    *   [5.1 Come avviare le applicazioni](#Come_avviare_le_applicazioni)
*   [6 Usare PAWM](#Usare_PAWM)
*   [7 PAWM Utilities](#PAWM_Utilities)

## Introduzione

[PAWM](https://sites.google.com/site/pleyadestest/david/projects/pawm) è un gestore delle finestre per X11, ed è molto piccolo, veloce e semplice. E 'basato su Xlib e non ha bisogno di altre librerie esterne per essere compilarlo. Esso fornisce un ambiente iniziale minimale di gestione dell finestre per il desktop o per un uso singolo, come:

*   Un browser web per computer usati come terminali.
*   Testare le interfacce grafiche dei programmi.

### Cenni storici su PAWM

PAWM è stato scritto da David Gómez e Raúl Núñez de Arenas Coronado. PAWM è stato creato con l'obbiettivo di avere un piccolo gestore di finestre per eseguire tutte le applicazioni di X, ma che mantenesse al tempo stesso un metodo semplice ed intuitivo di utilizzo.

Il nomePAWM significa _Puto Amo Window Manager_.

## Installazione

[pawm](https://www.archlinux.org/packages/?name=pawm) è reperibile nel repository Community di Arch. Per installare PAWM, digitare da root:

 `# pacman -S pawm` 

## Avviare PAWM

Per avviare PAWM come gestore delle finestre predefinito bisogna modificare, o creare in caso fosse assente, il file `~/.xinitrc` aggiungendo la sequente stringa:

```
exec pawm

```

Se ora si digita:

```
startx

```

al prompt dei comandi, X partirà utilizzando PAWM come window manager.

Se si desidera configurare X (e PAWM) in modo da avviarsi al boot (o quando si effettua il login) consultare la pagina del wiki [Start X at Login](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)").

## Configurazione (migliorare PAWM)

Per impostazione predefinita, PAWM risulta blu, piatto e sostanzialmente datato. Modificando il file `/etc/pawm.conf` è possibile personalizzarlo secondo le proprie esigenze.

I colori sono cambiati con i valori esadecimali. I font può essere modificato attraverso i caratteri fondamentali [[1]](http://en.wikipedia.org/wiki/X_logical_font_description) o con caratteri Xft [[2]](http://www.x.org/archive/X11R6.8.2/doc/fonts.html).

È possibile regolare anche regolare il comportamento degli pabar, paicons, icona pashut o tutti i moduli aggiunti.

### Icone

PAWM supporta soltanto i formati [.xpm](http://en.wikipedia.org/wiki/X_PixMap). Programmi come [GIMP](/index.php/GIMP#GIMP "GIMP") possono essere utili per convertire le immagini nel formato appropriato.

*   Le icone per le **finestre** devono avere la dimensione di 20x20 pixels.
*   Le icone per **Pashut** devono avere la dimensione di 20x20 pixels.
*   LE icone di **Paicon** possono avere diverse dimensioni.

Tutte le icone utilizzate da PAWM **devono** risiedere nel percorso `/usr/share/pawm/icons/`

## Avvio automatico dei programmi

Per prima cosa creare una directory `~/.pawm` . Questo permette ad ogni utente di avere il proprio set di applicazioni.

Ci sono 3 diversi metodi per lanciare i programmi in PAWM.

*   Aggiungendoli al file `~/.xinitrc`.
*   Eseguire il programma da console seguito dal parametro **`-display`**.
*   Utilizzare il lanciatore personalizzato di PAWM.

Questo articolo descriverà la terza opzione.

### Come avviare le applicazioni

Creare un nuovo file nella directory. Per il nostro esempio useremo l'emulatore di terminale [Sakura](http://www.pleyades.net/david/sakura.php).

Il nome del file deve iniziare con il termine **app** seguito da un massimo di 20 caratteri dopo di esso.

```
appSakura

```

Poi aprite il file con il vostro editor di testo preferito. Per funzionare correttamente il file per lanciare l'applicazione necessita di 4 stringhe, i quali corrispondono :

1.  Il nome dell'immagine icona che si vuole utilizzare.
2.  La posizione iniziale dell'icona. Se la si sposta, PAWM permetterà di modificare le coordinate XY di conseguenza.
3.  Testo sotto l'icona. opzione facoltativa.
4.  comando per lanciare l'applicazione. Si può utilizzare sia il percorso relatico che assoluto.

Alla fine il file dovrebbe risultare come segue:

```
sakura.xpm
40 40
Sakura
sakura

```

Al prossimo riavvio PAWM mostrerà l'icona creata, così come ogni icona cambiate, compresa la sua posizione.

## Usare PAWM

Così come PAWM è un gestore di finestre minimale, allo stesso modo anche i vari controlli risultato tali.

*   Doppio clic su una barra del titolo della finestra scorre, rispettivamente, verso l'alto o verso il basso.
*   Vi sono i pulsanti Minimizza Ripristina/Massimizza e Chiudi.
*   Vi è la possibilità di trascinare le finestre.
*   Vi è la possibilità di trascinare le icone per il _launcher_ delle applicazioni.
*   Cliccando su una applicazione aperta direttamente sulla PABar, la minimizza o la rispristina.
*   Alt+Tab scorre tra le finestre.
*   Cliccando su un'icona _Launcher_ avvia il programma.
*   Facendo clic sul pulsante di accensione si attiva una finestra di dialogo per uscire da PAWM.
*   Per rendere effettive le modifiche effettuate bisogna ricaricare PAWM.

## PAWM Utilities

I seguenti pacchetti complementari possono essere trovati su [AUR](/index.php/AUR "AUR").

*   [xsri](https://aur.archlinux.org/packages/xsri/) Un semplice strumento per l'impostazione della finestra principale di sfondo con un'immagine o gradiente. L'ideale è farlo partire da `~/.xinitrc`
*   [thinglaunch](https://aur.archlinux.org/packages/thinglaunch/) è un lanciatore di programmi su X. Lo si può associare a una chiave nel vostro window manager preferito. Quando si vuole avviare un programma, è sufficiente digitare il suo nome. thinglaunch ha un ingombro molto piccolo e dipende solo Xlib.
*   [pawmIcons](https://aur.archlinux.org/packages/pawmIcons/) Una semplice utilità scritta in Python per la creazione di base senza problemi delle icone di avvio. Non supporta le icone personalizzate.