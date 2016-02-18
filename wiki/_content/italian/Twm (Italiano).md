TWM è un window manager per X11\. Si tratta di un piccolo programma, in fase di costruzione contro Xlib invece di usare una libreria di widget, e come tale è molto leggero sulle risorse di sistema. Anche se semplice, è altamente configurabile, caratteri, colori, larghezza dei bordi, barra del titolo e pulsanti possono essere impostati dall'utente

## Contents

*   [1 Breve storia di Twm](#Breve_storia_di_Twm)
*   [2 Installazione](#Installazione)
*   [3 Avviare twm con X](#Avviare_twm_con_X)
*   [4 Configurazione (modificare il file .twmrc)](#Configurazione_.28modificare_il_file_.twmrc.29)
*   [5 Risorse](#Risorse)
*   [6 Referenze](#Referenze)

### Breve storia di Twm

Twm è stato scritto da Tom LaStrange, uno sviluppatore che era frustrato dalle limitazioni di [uwm (Ultrix Window Manager)](http://en.wikipedia.org/wiki/UWM_(computing)), il primo gestore di finestre che girava su X11 al momento del suo rilascio. TWM ha soppiantato UWM come window manager predefinito fornito con X11 dal rilascio in X11R4 nel 1989 .

Twm è sinonimo di*Tom's Window Manager*, *Tab Window Manager* e più recentemente di *Timeless Window Manager*.

## Installazione

Twm si trova nei [repository ufficiali](/index.php/Official_repositories "Official repositories") di Arch Linux ed è fornito dal pacchetto [xorg-twm](https://www.archlinux.org/packages/?name=xorg-twm):

 `pacman -S xorg-twm` 

## Avviare twm con X

Per fare in modo di avviare twm come vostro gestore delle finestre, modificare il file `~/.xinitrc` aggiungendo la seguente stringa:

```
exec twm

```

Ora lo si può avviare digitando:

 `$ startx` 

al prompt dei comandi, il server X partirà utilizzando twm come window manager.

Se si desidera configurare [X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") (e twm) per avviare al boot (o quando si effettua il login) consultare la pagina del wiki [Start X at Login](/index.php/Start_X_at_Login_(Italiano) "Start X at Login (Italiano)").

## Configurazione (modificare il file .twmrc)

Per impostazione predefinita, twm appare molto datato e poco intuitivo. Modificando il file `~/.twmrc` è possibile personalizzare twm per renderla più piacevole.

## Risorse

*   La pagina man di twm fornisce tutti i dettagli dei comandi che possono essere usati nel file `.Twmrc`. Lo potete consultare sia online  oppure, una volta installato digitando quanto segue nel propt dei comandi:

```
man twm

```

*   Molti files `.twmrc` già modificati si possono reperire online . Il sito xwinman  contiene molti file `.twmrc` comprensivi di immagini a cui potete ispirarvi per le vostre modifiche. Anche una ricerca su Google search per `twmrc` può essere utile per trovare nuove idee .
*   Ulteriori informazioni su twm si possono reperire nella relativa pagina su wikipedia .
*   Esiste una versione non patchata, nei repository, con funzionalità aggiornate come la trasparenza. Uno script di descrizione e di compilazione è disponibile sulla mailing list di xorg.  Può essere provato con l'installazione di [xcompmgr](/index.php/Xcompmgr "Xcompmgr"). Eseguire lo script di compilazione, mettendo i file risultanti `twm` e `dot.twmrc` in una directory conveniente, e modificare il file `~/.xinitrc` in modo che le ultime due righe risultino:

```
xcompmgr -o 0.3  -c -r 8 -t -10 -l -12 &
/path-to-directory/twm -visual TrueColor -depth 32 -f /path-to-directory/dot.twmrc

```

## Referenze

1.  Proffitt, Brian. "[From the Desktop: Tom LaStrange Speaks!](http://www.linuxplanet.com/linuxplanet/reports/3000/2/)", *LinuxPlanet*, February 6, 2001\. Retrieved October 22, 2009.
2.  "[UWM (computing)](http://en.wikipedia.org/wiki/UWM_(computing))", *Wikipedia*. Retrieved October 22, 2009.
3.  "[Twm](http://en.wikipedia.org/wiki/Twm)", *Wikipedia*. Retrieved October 22, 2009.
4.  "[Pkg: xorg-twm - Arch Linux Package Details](https://www.archlinux.org/packages/extra/i686/xorg-twm/)", *Arch Linux package search*. Retrieved October 22, 2009.
5.  "[Twm man page](http://linux.die.net/man/1/twm)", *linux.die.net*. Retrieved October 22, 2009.
6.  "[Sample twmrc](http://www.custompc.plus.com/twm/configs/twmrc09)", *custompc.plus.com*. Retrieved August 12, 2013.
7.  "[Window Managers for X: TWM/VTWM](http://xwinman.org/vtwm.php)", *xwinman.org*. Retrieved October 22, 2009.
8.  "[Google search for twmrc](http://www.google.com/search?q=twmrc)", *google.com*. Retrieved October 22, 2009.
9.  Kask, Eeri. "[TWM -- Revised Edition -- Again](http://lists.x.org/archives/xorg/2010-January/048401.html)", *lists.x.org*, January 3, 2010.