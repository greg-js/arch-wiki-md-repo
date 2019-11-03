Articoli correlati

*   [Evilwm](/index.php/Evilwm_(Italiano) "Evilwm (Italiano)")
*   [FVWM](/index.php/FVWM_(Italiano) "FVWM (Italiano)")
*   [Fluxbox](/index.php/Fluxbox_(Italiano) "Fluxbox (Italiano)")
*   [IceWM](/index.php/IceWM_(Italiano) "IceWM (Italiano)")
*   [JWM](/index.php/JWM_(Italiano) "JWM (Italiano)")
*   [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)")
*   [Pawm](/index.php/Pawm_(Italiano) "Pawm (Italiano)")
*   [Twm](/index.php/Twm_(Italiano) "Twm (Italiano)")
*   [PekWM](/index.php/PekWM_(Italiano) "PekWM (Italiano)")
*   [Window Maker](/index.php/Window_Maker_(Italiano) "Window Maker (Italiano)")
*   [Awesome3](/index.php/Awesome3_(Italiano) "Awesome3 (Italiano)")

[cwm](http://monkey.org/~marius/pages/?page=cwm) è un gestore delle finestre di X11 che originariamente derivava da [evilwm](/index.php/Evilwm_(Italiano) "Evilwm (Italiano)"). Tuttavia, la base del codice di evilwm non era in grado di accogliere le nuove funzioni che venivano aggiunte, in modo che il codice è stato riscritto da zero. CWM mira ad essere semplice, e offre funzionalità utili come la ricerca per le finestre.

[Qui](http://monkey.org/~marius/cwm/shot-full.png) una immagine di esempio.

## Installazione

Il pacchetto [cwm](https://aur.archlinux.org/packages/cwm/) è reperibile su [AUR](/index.php/AUR "AUR"). Ed ha come dipendenze [libx11](https://www.archlinux.org/packages/?name=libx11) e [libxft](https://www.archlinux.org/packages/?name=libxft), entrambi reperibili nei [repository ufficiali](/index.php/Official_repositories "Official repositories") di Arch.

## Uso

Per avviare Cwm durante il boot aggiungere quanto segue al file `~/.xinitrc` (consultare [xinitrc](/index.php/Xinitrc "Xinitrc") e [Start X at Boot](/index.php/Start_X_at_Boot "Start X at Boot") per maggiori dettagli).

```
/usr/bin/cwm

```

## Documentazione

C'è una pagina di manuale ben scritto sul sito ufficiale([[1]](http://monkey.org/~marius/cwm/cwm.1.a)).