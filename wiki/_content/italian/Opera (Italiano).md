## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Vantaggi](#Vantaggi)
*   [3 Svantaggi](#Svantaggi)
    *   [3.1 Installazione](#Installazione)
*   [4 Altre opzioni](#Altre_opzioni)
    *   [4.1 Microsoft font e Opera](#Microsoft_font_e_Opera)
    *   [4.2 Ulteiori modifiche](#Ulteiori_modifiche)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Mancanza di file](#Mancanza_di_file)
    *   [5.2 Aggiustare menù brutti](#Aggiustare_men.C3.B9_brutti)

## Introduzione

[Opera](http://www.opera.com) è un browser web prodotto da [Opera Software](http://it.wikipedia.org/wiki/Opera_Software) ASA, una compagnia norvegese IT. È il quarto browser più utilizzato dopo Internet Explorer, Mozilla Firefox e Apple Safari.

## Vantaggi

*   E' veloce e leggero.
*   E' conforme agli standard.
*   Tra le sue caratteristiche principali è possibile ricordare i filtri per bloccare le finestre pop-up, un client NNRP per Usenet e uno per le e-mail completo di filtri anti-spam. Inoltre è da segnalare che questo navigatore supporta nativamente lo scaricamento e la ricerca di file BitTorrent. Permette inoltre la navigazione di più siti con l'apertura di un'unica istanza del programma (il cosiddetto tabbed browsing o navigazione a schede).
*   Implementa una serie di gesti per il mouse (mouse gesture), attuabili con una combinazione di clic e trascinamenti del puntatore, che rendono superfluo l'utilizzo delle barre degli strumenti e dei menu.
*   Nessun appesantimento del software, nessuna falla di memoria, nessun freeze o crash.

## Svantaggi

*   Se si utilizza GNOME o qualsiasi window manager basato su GTK+, è necessario caricare librerie aggiuntive perchè Opera è un'applicazione Qt.
*   Alcune pagine non vengono visualizzate correttamente perchè non seguono gli standard web (Opera si attiene allo standard).

### Installazione

Per installare l'ultima versione di Opera:

```
# pacman -S opera

```

## Altre opzioni

### Microsoft font e Opera

Se si possiede al tempo dell'installazione di Opera il pacchetto ttf-ms-fonts il browser userà questi font e potrebbe sembrare brutto. Per far usare ad Opera ed ovviare a questo problema si consiglia di rimuovere il pacchetto ttf-ms-fonts prima dell'installazione.

Notare anche tutti i font sono configurabili dal menu _Strumenti -> Preferenze -> Avanzate -> Fonts_

### Ulteiori modifiche

*   Per rimuovere la tray icon, avviare Opera con l'opzione _--notrayicon_.
*   Per renedere il menu carino: [polymer](https://aur.archlinux.org/packages/polymer/).

Dopo avviare **qtconfig** (sarà allocato in /opt/qt/bin) e impostare il tema polymer per le applicazioni Qt.

*   Per disabilitare i "brutti" anti-aliased font, editare opera:config nella barra degli indirizzi di Opera, cercare l'opzione "core X fonts" e disabilitarla.
*   Per migliorare le prestazioni dei flash plugin in Opera, eseguire semplicemente questo comando prima dell'avvio di Opera oppure aggiungerlo nel proprio /etc/profile :

```
# export OPERAPLUGINWRAPPER_PRIORITY=0

```

## Troubleshooting

### Mancanza di file

*   Se si hanno errori del genere:

```
/usr/lib/opera/9.27-20080331.6/opera: error while loading shared libraries: libqt-mt.so.3: cannot open shared object file: No such file or directory

```

Creare un symlink (da root):

```
# ln -s /opt/qt/lib/libqt-mt.so.3 /usr/lib/libqt-mt.so.3

```

Questo dovrebbe risolvere il problema.

*   Se a volte si hanno problemi di rendering, tipo una linea di pixel duplicata, spuntare l'opzione "Scorrimento uniforme" (_Strumenti -> Preferenze -> Avanzate -> Navigazione -> Scorrimento uniforme'_).

### Aggiustare menù brutti

Esiste un'altra soluzione, però prima di procedere rimuovere il pacchetto Opera.

*   Aggiungere alla fine del file /etc/pacman.conf ( **NB!** Ricordarsi di scegliere la corretta architettura. ( Se già presente saltare questo passaggio)).

```
[archlinuxfr]
Server = [http://repo.archlinux.fr/i686](http://repo.archlinux.fr/i686)

```

```
[archlinuxfr]
Server = [http://repo.archlinux.fr/x86_64](http://repo.archlinux.fr/x86_64)

```

*   Installare Opera usando l'ultima versione:

```
# pacman -S opera-snapshot

```

**Di vitale importanza è aver installato polymer ed eseguito le qtconfig spiegate [precedentemente](/index.php/Opera_(Italiano)#Ulteriori_modifiche "Opera (Italiano)").**