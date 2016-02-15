## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Come ottenere nuovi plasmoidi](#Come_ottenere_nuovi_plasmoidi)
*   [3 Consigli & trucchi](#Consigli_.26_trucchi)
    *   [3.1 Dividere la Dashboard dal Desktop](#Dividere_la_Dashboard_dal_Desktop)
        *   [3.1.1 Introduzione](#Introduzione_2)
        *   [3.1.2 Creare un nuovo desktop](#Creare_un_nuovo_desktop)
        *   [3.1.3 Chiudere plasma](#Chiudere_plasma)
        *   [3.1.4 Modificare i file](#Modificare_i_file)
        *   [3.1.5 Riavviare plasma](#Riavviare_plasma)
        *   [3.1.6 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [3.2 Dividere la Dashboard dal Desktop – il metodo di plasma](#Dividere_la_Dashboard_dal_Desktop_.E2.80.93_il_metodo_di_plasma)
    *   [3.3 Aggiungere un pannello in stile OSX chiamato anche "fancy"](#Aggiungere_un_pannello_in_stile_OSX_chiamato_anche_.22fancy.22)
    *   [3.4 Tenere sfondi differenti per ogni faccia del cubo](#Tenere_sfondi_differenti_per_ogni_faccia_del_cubo)
    *   [3.5 Miscelazione del Desktop e delle attività di visualizzazione delle cartelle in un cubo](#Miscelazione_del_Desktop_e_delle_attivit.C3.A0_di_visualizzazione_delle_cartelle_in_un_cubo)

# Introduzione

Plasma è la componente del progetto [KDE](/index.php/KDE "KDE") che attualmente mostra il desktop (lo sfondo, i pannelli, ecc) utilizzando i 'contenitori'. I contenitori sono composti dai widget qui chiamati 'plasmoidi'.

# Come ottenere nuovi plasmoidi

Puoi ottenere nuovi plasmoidi da [kde-look.org](http://www.kde-look.org/index.php?xsortmode=new&logpage=0&xcontentmode=70x77x78&page=0).

Ci sono molti plasmoidi in pacchetti su AUR come [kde-extragear-plasmoids](https://aur.archlinux.org/packages.php?ID=21084), che contiene plasmoidi popolari su [kde-look.org](http://www.kde-look.org/index.php?xsortmode=new&logpage=0&xcontentmode=70x77x78&page=0) e li raggruppa in un unico pacchetto.

Gli utenti di KDEmod possono facilmente installare i nuovi plasmoidi dal repository kdemod-extragear.

# Consigli & trucchi

## Dividere la Dashboard dal Desktop

### Introduzione

La Dashboard è ciò che appare quando premi i tasti Ctrl+F12 (se Plasma è in esecuzione e non hai cambiato la scorciatoia di tasti). <cite>Di default questo “porta avanti” il tuo desktop e contribuisce a risolvere il problema “ma io non vedo mai il mio desktop!”</cite>, spiega Aaron Seigo in [HOWTO: dividere la dashboard dal desktop (en)](http://aseigo.blogspot.com/2008/09/howto-decoupling-dashboard-from-desktop.html).

**Nota:** su KDE 4.2 non esiste un'interfaccia utente per le seguenti operazioni, quindi dovremo modificare a mano i file di configurazione di Plasma, non propriamente un approccio amichevole per l'utente.

**Attenzione:** dovresti fare un backup della configurazione di Plasma prima di partire.

### Creare un nuovo desktop

La prima cosa da fare è creare un nuovo “Desktop” che diventerà la nostra Dashboard:

1.  effettuare lo zoom cliccando sull'icona dell'anacardio nell'angolo superiore-destro del tuo desktop;
2.  cercare un pulsante per aggiungere un'Attività (potresti dover sbloccare i plasmoidi per far comparire questo pulsante)

### Chiudere plasma

La seconda fase consiste nel chiudere Plasma in modo che non interferisca mentre modificheremo i suoi file di configurazione:

*   eseguire `kquitapp plasma`

**Nota:** non sentirti disorientato perché il tuo desktop è scomparso, le tue applicazioni sono sempre lì e puoi usare Alt+Tab e KRunner (Alt+F2)!

### Modificare i file

Cerchiamo e teniamo nota dei **2 numeri** nel seguente file:

 `~/.kde4/share/config/plasma-appletsrc` 

```
[Containments][**$desktop_activity_number**]
...
plugin=desktop      # search for these lines to easily find the Desktops
...

[Containments][**$dashboard_activity_number**]
...
plugin=desktop
...
```

Nel secondo file diremo a Plasma di usare la nuova Attività come Dashboard del nostro Desktop:

 `~/.kde4/share/config/plasmarc` 

```
[ViewIds]
...
# find the line below to find out the **$desktop_view_id**, if the line doesn't exist just add it using an unused view id
**$desktop_activity_number**=**$desktop_view_id**
...

[PlasmaViews][**$desktop_view_id**]    # find or add this section
...
DashboardContainment=**$dashboard_activity_number**    # add this line
```

### Riavviare plasma

Puoi ora riavviare plasma e premere Ctrl+F12 o qualsiasi scorciatoia tu abbia impostato per la Dashboard per controllare di aver eseguito tutto correttamente.

### Risoluzione di problemi

Se questo non funziona probabilmente questo esempio con numeri veri ti aiuterà a trovare il tuo errore:

 `~/.kde4/share/config/plasma-appletsrc` 

```
[Containments][**13**]
...
plugin=desktop
...

[Containments][**25**]
...
plugin=desktop
...
```

 `~/.kde4/share/config/plasmarc` 

```
[ViewIds]
...
**13**=**8**
...

[PlasmaViews][**8**]
...
DashboardContainment=**25**
```

## Dividere la Dashboard dal Desktop – il metodo di plasma

cliccare sull'icona dell'anacardio nell'angolo superiore-destro, effettuare lo zoom, (new screen, look at new menu top left) configure plasma - use a separate dashboard

## Aggiungere un pannello in stile OSX chiamato anche "fancy"

Tasto destro sul desktop – aggiungi pannello - fancy panel

**Attenzione:** Nel momento in cui scrivo è possibile modificare un pannello fancy estesamente, ma non si ricorderà alcuna impostazione.

## Tenere sfondi differenti per ogni faccia del cubo

click on top right cashew - zoom out - (new screen, look at new menu top left) configure plasma - different activity for each desktop

## Miscelazione del Desktop e delle attività di visualizzazione delle cartelle in un cubo

click on top right cashew - zoom out - (new screen, look at new menu top left) configure plasma - different activity for each desktop