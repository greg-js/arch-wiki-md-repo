LXDM è un display manager leggero per l'ambiente desktop [LXDE](/index.php/LXDE_(Italiano) "LXDE (Italiano)"). L'interfaccia utente è realizzata con [GTK+](/index.php/GTK%2B_(Italiano) "GTK+ (Italiano)") 2\. È ancora nelle prime fasi di sviluppo.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Sessione di Default](#Sessione_di_Default)
        *   [2.1.1 Impostazioni Globali](#Impostazioni_Globali)
        *   [2.1.2 Impostazioni Utente](#Impostazioni_Utente)
    *   [2.2 Autologin](#Autologin)
*   [3 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [3.1 Aggiungere icone utente](#Aggiungere_icone_utente)
    *   [3.2 Utenti in simultanea e Cambio Utente](#Utenti_in_simultanea_e_Cambio_Utente)
    *   [3.3 Temi](#Temi)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Problemi nella gestione del logout](#Problemi_nella_gestione_del_logout)

## Installazione

Il pacchetto [lxdm](https://www.archlinux.org/packages/?name=lxdm) è disponibile nei repository ufficiali. Il pacchetto di sviluppo, [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/), è disponibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

Attualmente, lxdm fornisce il servizio lxdm su [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)") per avviare LXDM al boot.

## Configurazione

I file di configurazione per LXDM sono tutti situati in `/etc/lxdm/`. Il file di configurazione principale è `lxdm.conf`, che è ben documentato nei suoi commenti. Un altro file, Xsession, è il file di configurazione di Xsession e non dovrebbe essere modificato. Gli altri file presenti nella cartella sono tutti degli script di shell che vengono eseguiti quando accadono certi eventi su LXDM.

Questi sono :

1.  `LoginReady` viene eseguito con privilegi di root quando LXDM è pronto a mostrare la finestra di login.
2.  `PreLogin` viene eseguito come root prima del login di un utente.
3.  `PostLogin` viene eseguito come utente connesso subito dopo aver effettuato il login.
4.  `PostLogout` viene eseguito come utente connesso subito dopo aver effettuato il logout.
5.  `PreReboot` viene eseguito come root prima di riavviare con LXDM.
6.  `PreShutdown` viene eseguito come root prima dello spegnimento del sistema con LXDM.

### Sessione di Default

Può essere specificato quale sessione verrà caricata quando gli utenti selezionano la sessione 'Default' dalla lista delle sessioni nella schermata di LXDM. Notare che l'impostazione utente ha la preferenza sulle impostazioni globali.

#### Impostazioni Globali

Modificare `/etc/lxdm/lxdm.conf` e cambiare la linea di sessione con la sessione o il DE desiderato:

 `session=/usr/bin/startlxde` 

Esempio con [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)"):

 `session=/usr/bin/startxfce4` 

Esempio con [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)"):

 `session=/usr/bin/openbox-session` 

Esempio con [GNOME](/index.php/GNOME_(Italiano) "GNOME (Italiano)"):

 `session=/usr/bin/gnome-session` 

Questo è utile per i temi che non hanno alcuna casella di selezione sessione visibile, o che hanno problemi di autologin.

#### Impostazioni Utente

Per definire la sessione preferita di un singolo utente, è sufficiente modificare il suo rispettivo file `~/.dmrc`.

Esempio: Tizio vuole Xfce4, Caio vuole Cinnamon e Sempronio vuole GNOME:

Per Tizio:

```
[Desktop]
Session=xfce

```

Per Caio:

```
[Desktop]
Session=cinnamon

```

Per Sempronio:

```
[Desktop]
Session=gnome

```

### Autologin

Per accedere ad un account automaticamente, senza fornire una password, individuare questa riga in `/etc/lxdm/lxdm.conf` :

```
#autologin=dgod

```

Rimuovere il commento #, e sostituire "dgod" con il nome utente di destinazione.

Questo farà sì che LXDM effettuerà il login automatico sull'utente specificato. Tuttavia, se si dovesse fare il log-out di quell'utente, sarà necessario inserire la password per accedervi di nuovo. Per evitare questo, è necessario eliminare definitivamente la password dell'utente:

```
$ passwd -d username

```

## Trucchi e Consigli

### Aggiungere icone utente

Un'icona utente di 96x96 pixel (jpg o png) può opzionalmente essere visualizzata nella schermata di login. Per impostarla basta copiare (o collegare) l'immagine di destinazione in `$HOME/.FACE`. Il pacchetto [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) fornisce alcune icone predefinite adatte per lxdm . Guardare all'interno di `/usr/share/pixmaps/faces` dopo l'installazione di questo pacchetto.

**Note:** Non è necessario mantenere [gnome-control-center](https://www.archlinux.org/packages/?name=gnome-control-center) installato per utilizzare queste immagini. Basta installarlo, copiare le immagini altrove, e rimuoverlo.

E' possibile cambiare icona utente anche eseguendo il comando:

```
$ lxdm-config

```

### Utenti in simultanea e Cambio Utente

LXDM consente a più utenti di essere registrati in diversi tty allo stesso tempo. Il comando seguente viene utilizzato per consentire a un altro utente di accedere senza effettuare il logout dell'utente corrente:

```
$ lxdm -c USER_SWITCH

```

**Note:** Quando il nuovo utente accede, la sua sessione inizierà su tty7 e successivi. Per esempio, Tizio si logga e usa il comando USER_SWITCH. Poi si logga anche Caio. Caio sarà su tty7 mentre Tizio su tty1.

Se si utilizza il desktop [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)"), per attivare la funzionalità di Cambio Utente potrebbe essere necessario creare lo script eseguibile `/usr/bin/gdmflexiserver` costituito da:

```
#!/bin/sh
/usr/bin/lxdm -c USER_SWITCH

```

così il cambio utente su Xfce dovrebbe funzionare bene anche con LXDM.

[Xscreensaver](/index.php/Xscreensaver_(Italiano) "Xscreensaver (Italiano)") può anche eseguire questa operazione. Per ulteriori informazioni, vedere [questa sezione](/index.php/Xscreensaver_(Italiano)#LXDM "Xscreensaver (Italiano)") della pagina di Xscreensaver.

### Temi

I temi di lxdm sono localizzati in `/usr/share/lxdm/themes`.

C'è solo un tema fornito di default con [lxdm](https://www.archlinux.org/packages/?name=lxdm), vale a dire "Industrial". Per visualizzare l'immagine di sfondo contenuta nel file `wave.svg` di questo tema, assicurarsi di aver installato [librsvg](https://www.archlinux.org/packages/?name=librsvg).

Ci sono 2 temi forniti di default con [lxdm-git](https://aur.archlinux.org/packages/lxdm-git/). ArchStripes e ArchDark. È possibile impostare il tema modificando il file `/etc/lxdm/lxdm.conf` in `theme=*theme_name*`

## Risoluzione dei problemi

### Problemi nella gestione del logout

Potrebbe succedere che, a volte, LXDM abbia qualche problema in fase di log-out. Ad esempio potrebbe non riuscire a uccidere tutti i processi utente e lasciare qualche programma aperto. Per garantire che LXDM effettui il log-out sempre correttamente, aggiungere le seguenti righe allo script `/etc/lxdm/PostLogout`:

 `/etc/lxdm/PostLogout` 
```
# Terminate current user session
/usr/bin/loginctl terminate-session $XDG_SESSION_ID

# Restart lxdm
/usr/bin/systemctl restart lxdm.service

```