KDM (KDE Display Manager) è il gestore del login di [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)"). Esso supporta temi, login automatici, scelta della tipologia di sessione e numerose altre funzionalità.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Temi](#Temi)
    *   [2.2 Creazione temi](#Creazione_temi)
    *   [2.3 File di configurazione](#File_di_configurazione)
        *   [2.3.1 ServerArgsLocal](#ServerArgsLocal)
        *   [2.3.2 SessionsDirs](#SessionsDirs)
        *   [2.3.3 Sessione](#Sessione)
        *   [2.3.4 Opzione di menù Riavvia X server](#Opzione_di_men.C3.B9_Riavvia_X_server)
*   [3 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [3.1 Mappatura tastiera](#Mappatura_tastiera)
    *   [3.2 Avvio KDM lento](#Avvio_KDM_lento)

## Installazione

Installare il pacchetto [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/):

```
# pacman -S kdebase-workspace

```

## Configurazione

Un esempio di configurazione per KDM può essere trovato in `/usr/share/config/kdm/kdmrc`. Per tutte le opzioni vedere `/usr/share/doc/HTML/en/kdm/kdmrc-ref.docbook`.

E' possibile visitare **Impostazioni di Sistema > Schermata d'avvio (login)** ed apportare le proprie modifiche. Premuto "Applica", apparirà una finestra di **KDE Polkit authorization** che richiederà la password di root per salvare i cambiamenti.

Se, lanciando Impostazioni di Sistema da utente, non si è abilitati ad apportare modifiche alle impostazioni di KDM, si può utilizzare kdesu:

```
 $ kdesu kcmshell4 kdm

```

Nella finestra di kdesu, inserire la password di root ed attendere che venga avviato Impostazioni di Sistema. Quindi andare in Schermata d'avvio (login).

**Nota:** Una volta avviato da root, fare attenzione alle modifiche che si apportano. Tutte le configurazioni di Impostazioni di Sistema lanciato da root sono salvate in `/root/.kde4` e non in `~/.kde4` (la propria home).

### Temi

I temi KDM di Archlinux possono essere installati con:

```
# pacman -S archlinux-themes-kdm

```

Molti altri temi di KDM 4 sono disponibili in [http://kde-look.org/index.php?xcontentmode=41](http://kde-look.org/index.php?xcontentmode=41). Selezionarne uno tra quelli installati, in Impostazioni di sistema (da root), come descritto sopra.

### Creazione temi

I file dei temi sono collocati in `/usr/share/apps/kdm/themes`.

Il formato del tema è lo stesso di un tema GDM, la relativa documentazione può essere trovata qui: [Detailed Description of Theme XML format](http://projects.gnome.org//gdm/docs/2.18/thememanual.html#descofthemeformat).

### File di configurazione

Il file di configurazione principale è `/usr/share/config/kdm/kdmrc`. Il file predefinito contiene globalmente commenti relativi alla funzione di ciascun elemento.

#### ServerArgsLocal

Per forzare il numero di punti per pollice del server X, aggiungere l'opzione -dpi al ServerArgsLocal. Un valore comunemente usato è 96 dpi.

```
ServerArgsLocal=-dpi 96 -nolisten tcp

```

#### SessionsDirs

Questa variabile memorizza un elenco di cartelle contenenti le definizioni dei tipi di sessione in formato `.desktop` classificate in ordine di priorità. In Arch Linux alcuni [window managers](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)") installano tali file in `/usr/share/xsessions`. Aggiungere questo percorso alla lista in modo da essere in grado di poter poi selezionare le relative sessioni in KDM.

```
SessionsDirs=/usr/share/config/kdm/sessions,/usr/share/apps/kdm/sessions,/usr/share/xsessions

```

#### Sessione

La variabile Sessione è il nome di un programma che viene eseguito quando l'utente effettua l’accesso. Si suppone di interpretare l'argomento di sessione (vedere SessionsDirs) e avviare la relativa sessione come indicato per quell’argomento. Si potrebbe voler personalizzare questo per le sessioni di window manager, ad esempio per impostare uno sfondo ed avviare uno screensaver. Per fare ciò in modo che sopravvivrà agli aggiornamenti di pacman (che sovrascrive Xsession) agire come indicato di seguito:

```
cp /usr/share/config/kdm/Xsession /usr/share/config/kdm/Xsession.custom

```

In kdmrc impostare

```
Session=/usr/share/config/kdm/Xsession.custom

```

E modificare Xsession.custom come si preferisce.

#### Opzione di menù Riavvia X server

Per consentire agli utenti di riavviare il server X da KDM, modificare la seguente impostazione in kdmrc:

```
 [X-:*-Greeter]
 # [...]
 # Show the "Restart X Server"/"Close Connection" action in the greeter.
 # Default is true
 AllowClose=true

```

Questo renderà disponibile nel menù a discesa l’opzione per riavviare il server X. L’opzione comprende anche la scorciatoia da tastiera Alt-E.

## Risoluzione dei problemi

### Mappatura tastiera

La mappatura tastiera KDM può essere impostata attraverso la configurazione di sistema (nella sezione della schermata di login).

### Avvio KDM lento

Se KDM impiega molto tempo (ad esempio, 15-30 secondi) per mostrare la schermata di login, è possibile provare ad eseguire, da root, i seguenti comandi:

```
# fc-cache -fv

```

Questo ricaricherà la cache dei caratteri X e velocizzerà il caricamento della schermata di login.