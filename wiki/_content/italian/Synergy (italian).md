[Synergy](http://synergy-foss.org/) permette di condividere facilmente un mouse ed una tastiera tra più computer (anche con differenti sistemi operativi) senza la necessità di hardware specifico. È stato concepito per utenti con più computer sulla propria scrivania, dato che ogni sistema utilizza il proprio (o i propri) monitor.

Per reindirizzare mouse e tastiera è sufficiente muovere il mouse oltre il bordo dello schermo. Synergy, poi, unifica la funzione del copia-incolla tra i vari sistemi, in maniera da poter copiare qualcosa da un computer ed incollarlo su un altro. Inoltre sincronizza gli screen saver in maniera che si avviino e terminino insieme e, se il blocco dello schermo è abilitato, è sufficiente inserire la password in uno solo per sbloccarli tutti.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Arch Linux](#Arch_Linux)
    *   [1.2 Windows e Mac OS X](#Windows_e_Mac_OS_X)
    *   [1.3 Compilare i sorgenti](#Compilare_i_sorgenti)
*   [2 Pre-configurazione](#Pre-configurazione)
*   [3 Configurazione del server](#Configurazione_del_server)
    *   [3.1 Arch Linux](#Arch_Linux_2)
    *   [3.2 Windows](#Windows)
    *   [3.3 Mac OS X](#Mac_OS_X)
    *   [3.4 Esempi di configurazione](#Esempi_di_configurazione)
*   [4 Configurazione dei client](#Configurazione_dei_client)
    *   [4.1 Arch Linux](#Arch_Linux_3)
        *   [4.1.1 Autoavvio](#Autoavvio)
    *   [4.2 Windows](#Windows_2)
    *   [4.3 Mac OS X](#Mac_OS_X_2)
*   [5 Problemi conosciuti](#Problemi_conosciuti)
*   [6 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [6.1 Ripetizione dei tasti](#Ripetizione_dei_tasti)
    *   [6.2 Mappatura della tastiera](#Mappatura_della_tastiera)
    *   [6.3 messages.log viene spammato da synergyc](#messages.log_viene_spammato_da_synergyc)
*   [7 Altre risorse](#Altre_risorse)

## Installazione

### Arch Linux

È possibile [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [synergy](https://www.archlinux.org/packages/?name=synergy) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

### Windows e Mac OS X

Scaricare ed eseguire [l'installatore più recente](http://synergy-foss.org/download) dal sito ufficiale.

### Compilare i sorgenti

Anzitutto scaricare e compilare il codice sorgente per creare i binari synergyc e synergys dal [repo svn](http://synergy-foss.org/pm/projects/synergy/tabs/source).

 `$ svn co http://synergy-plus.googlecode.com/svn/trunk/ synergy-trunk && cd synergy-trunk && cmake . && make` 
```
...
[  0%] Built target gtest
[ 94%] Built target synergy
Linking CXX executable synergyc
[ 96%] Built target synergyc
Linking CXX executable synergys
[ 98%] Built target synergys
[100%] Built target tests
```

Poi cambiare l'owner;group a `root:root` e copiare i binari creati nel proprio `$PATH`, ad esempio `/usr/local/bin`.

 `$ sudo chown root:root synergyc synergys && sudo cp -v synerygyc synergys /usr/local/bin` 
```
changed ownership of `synergyc' to root:root
changed ownership of `synergys' to root:root
`synergyc' -> `/usr/local/bin/synergyc'
`synergys' -> `/usr/local/bin/synergys'
```

**Suggerimento:** Sono anche disponibili le versioni BETA di Synergy.

*   Leggere [la guida ufficiale per la compilazione](http://synergy-foss.org/pm/projects/synergy/wiki/Compiling).

## Pre-configurazione

Determinare gli indirizzi IP e gli [hostname](/index.php/Configuring_Network_(Italiano)#Impostare_il_nome_del_PC "Configuring Network (Italiano)") per ogni macchina ed assicurarsi che ognuna abbia un file hosts settato correttamente.

*   Arch Linux - `/etc/hosts`
*   Windows - `C:\WINDOWS\system32\drivers\etc\hosts`
*   Mac OS X - [Come aggiungere degli host al file hosts locale](http://support.apple.com/kb/TA27291?viewlocale=en_US).

 `/etc/hosts` 
```
10.10.66.1        archserver.localdomain       archserver
10.10.66.100      archleft.localdomain         archleft
10.10.66.105      archright.localdomain        archright
```

**Nota:** Controllare che i client riescano a comunicare con il server.

## Configurazione del server

Leggere [Formato del File di Configurazione di Synergy](http://synergy2.sourceforge.net/configuration.html) per una descrizione dettagliata di tutte le sezioni ed opzioni disponibili.

### Arch Linux

Il file di configurazione per Arch Linux si trova in `/etc/synergy.conf`. Se tale file non esiste, crearlo basandosi su `/etc/synergy.conf.example`, i cui commenti dovrebbero fornire sufficienti informazioni per una configurazione di base; se si ha bisogno di approfondimenti, leggere la guida citata sopra.

**Suggerimento:** È anche possibile usare [qsynergy](https://aur.archlinux.org/packages/qsynergy/) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") oppure [quicksynergy](https://aur.archlinux.org/packages/quicksynergy/) dall'[AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"), che forniscono una GUI per semplificare la procedura di configurazione.

Per avviare il demone server, eseguire:

```
# rc.d start synergys

```

Se si verificano dei problemi e si desidera eseguire il server in foreground (mostrando l'output nella console), si può invece eseguire:

```
# synergys -f

```

Se si vuole avviare il demone server di Synergy ad ogni avvio di Arch Linux, si può aggiungere `synergys` all'array dei demoni in `/etc/rc.conf`:

 `/etc/rc.conf` 
```
...
DAEMONS=(... synergys ...)
```

### Windows

1.  Aprire il programma Synergy
2.  Selezionare l'opzione *Server (share this computer's mouse and keyboard)*
3.  Selezionare *Configure interactively*
4.  Cliccare il pulsante *Configure Server...*
5.  Questo apre una finestra nella quale si possono aggiungere schermi a seconda di quanti computer/schermi si hanno: basta trascinare l'icona dello schermo dall'angolo in alto a destra fino nell'area degli schermi, e poi farci doppio click per modificare la sua configurazione
6.  Cliccare su *OK* per chiudere la finestra degli schermi quando si è pronti, poi cliccare su *Start* per avviare il client

Su Windows, la configurazione viene salvata per default in un file `synergy.sgc`, ma il suo nome e il percorso possono essere modificati a piacere.

Se si vuole avviare il server ad ogni avvio di Windows bisogna lanciare Synergy **come amministratore**, poi andare se *Edit -> Services* e selezionare *Install* nella sezione *Server*; notare che al riavvio seguente Synergy sarà sì autoavviato, ma l'icona nell'area notifiche non si mostrerà automaticamente (almeno nella versione 1.4.2 beta su Windows 7). Per disinstallare il servizio bisogna fare la stessa cosa ma ovviamente selezionando *Uninstall*.

Se si vuole avviare il server dalla linea di comando, questa è una linea che si può mettere in un file `.bat` o semplicemente eseguirla da `cmd.exe`:

 `C:\Program Files\Synergy+\bin\synergys.exe  -f --debug ERROR --name left --log c:\windows\synergy.log -c C:/windows/synergy.sgc --address 10.66.66.2:24800` 

Consultare [la documentazione ufficiale](http://synergy-foss.org/docs) per maggiori informazioni.

### Mac OS X

Mac OS X ha una configurazione simile a Unix: consultare [la documentazione ufficiale](http://synergy-foss.org/docs) per maggiori informazioni.

### Esempi di configurazione

Questo è un esempio per una configurazione a 3 computer:

 `/etc/synergy.conf` 
```
section: screens
	server-fire:
	archright-fire:
	archleft-fire:
end

section: links
	archleft-fire:
		right = server-fire
	server-fire:
		right = archright-fire
		left = archleft-fire
	archright-fire:
		left = server-fire
end

```

Questo dovrebbe essere l'esempio fornito insieme al pacchetto di Arch Linux:

 `/etc/synergy.conf` 
```
section: screens
        # three hosts named:  moe, larry, and curly
        moe:
        larry:
        curly:
end

section: links
        # larry is to the right of moe and curly is above moe
        moe:
                right = larry
                up    = curly

        # moe is to the left of larry and curly is above larry.
        # note that curly is above both moe and larry and moe
        # and larry have a symmetric connection (they're in
        # opposite directions of each other).
        larry:
                left  = moe
                up    = curly

        # larry is below curly.  if you move up from moe and then
        # down, you'll end up on larry.
        curly:
                down  = larry
end

section: aliases
        # curly is also known as shemp
        curly:
                shemp
end
```

Il seguente è un esempio più personalizzato:

 `synergy.sgc` 
```
section: screens
	leftpc:
		halfDuplexCapsLock = false
		halfDuplexNumLock = false
		halfDuplexScrollLock = false
		xtestIsXineramaUnaware = false
		switchCorners = none +top-left +top-right +bottom-left +bottom-right 
		switchCornerSize = 0
	rightpc:
		halfDuplexCapsLock = false
		halfDuplexNumLock = false
		halfDuplexScrollLock = false
		xtestIsXineramaUnaware = false
		switchCorners = none +top-left +top-right +bottom-left +bottom-right 
		switchCornerSize = 0
end

section: aliases
leftpc:
10.66.66.2
rightpc:
10.66.66.1
end

section: links
	leftpc:
		right = rightpc
	rightpc:
		left = leftpc
end

section: options
	heartbeat = 1000
	relativeMouseMoves = false
	screenSaverSync = false
	win32KeepForeground = false
	switchCorners = none +top-left +top-right +bottom-left +bottom-right 
	switchCornerSize = 4
end
```

## Configurazione dei client

**Nota:** Si presuppone che sia stato correttamente configurato un server. Assicurarsi che ci sia già un server pronto ad accettare dei client prima di continuare.

### Arch Linux

Nella finestra di un terminale, digitare:

```
$ synergyc server-host-name

```

Oppure, per eseguire synergy in foreground (mostrando l'output nella console):

```
$ synergyc -f server-host-name

```

In queste linee, `server-host-name` è l'hostname del server.

#### Autoavvio

Esistono vari modi per autoavviare il client per Synergy, ed effettivamente sono i soliti metodi che possono essere usati per ogni altra applicazione.

**Nota:** In ognuno dei seguenti esempi bisogna sempre sostituire `server-host-name` con il nome reale del server.

*   Si può aggiungere la seguente linea al proprio [`~/.xinitrc`](/index.php/Xinitrc "Xinitrc"):

 `~/.xinitrc` 
```
...

#replace server-host-name with the real name
synergyc server-host-name

...
```

Il seguente codice è un'alternativa:

 `~/.xinitrc` 
```
XINIT_CMD='/usr/bin/synergyc -d FATAL -n galileo-fire 10.66.66.2:24800'
/usr/bin/pgrep -lxf "$XINIT_CMD" || ( ( $XINIT_CMD ) & )
```

*   Altrimenti, se si sta usando un [display manager](/index.php/Display_manager "Display manager") (kdm, gdm, [SLiM](/index.php/SLiM "SLiM"), ...), oppure un [window manager](/index.php/Window_manager "Window manager") standalone (Openbox, ...), è possibile sfruttare il suo script di startup e aggiungerci:

```
synergyc server-host-name

```

o, nel caso si sia creato il demone *synergyc* daemon (leggere più sotto):

```
/etc/rc.d/synergyc stop   #verify synergy is closed
/etc/rc.d/synergyc start

```

Ad esempio, se si usa *kdm* si dovrebbe modificare `/usr/share/config/kdm/Xsetup`.

*   Si può anche avviare *synergyc* direttamente nella init chain aggiungendo le righe seguenti a `/etc/rc.local`:

 `/etc/rc.local` 
```
...

echo "Starting Synergy client"
#replace server-host-name with the real name
synergyc server-host-name
```

*   Un risultato simile può essere ottenuto creando un demone e aggiungendolo all'array dei demoni in `/etc/rc.conf`; basta creare un file `/etc/rc.d/synergyc` con il contenuto seguente, assicurandosi di settare i suoi permessi con `chmod 755`:

 `/etc/rc.d/synergyc` 
```
#!/bin/bash
. /etc/rc.conf
. /etc/rc.d/functions

#Put the server host name in the following line
SERVERALIAS="server-host-name"

PID=`pidof -o %PPID /usr/bin/synergyc`
case "$1" in
 start)
   stat_busy "Starting Synergy Client"
   [ -z "$PID" ] && /usr/bin/synergyc "$SERVERALIAS"
   if [ $? -gt 0 ]; then
     stat_fail
   else
     /usr/bin/xset r on
     add_daemon synergyc
     stat_done
   fi
   ;;
 stop)
   stat_busy "Stopping Synergy Client"
   [ ! -z "$PID" ] && kill -9 $PID
   if [ $? -gt 0 ]; then
     stat_fail
   else
     rm_daemon synergyc
     stat_done
   fi
   ;;
 restart)
   $0 stop
   sleep 1
   $0 start
   ;;
 *)
   echo "usage: $0 {start|stop|restart}"
esac
exit 0
```

L'autoavvio di Synergy è documentato anche nella sua [pagina ufficiale di riferimento](http://synergy2.sourceforge.net/autostart.html).

### Windows

Dopo l'installazione, aprire il programma Synergy, selezionare l'opzione *Client (use another computer's keyboard and mouse)* e digitare l'hostname del server nella casella di testo, poi cliccare su *Start* per avviare il client.

**Nota:** Per terminare il client si può usare l'icona nell'area notifiche.

Se si vuole avviare il client ad ogni avvio di Windows bisogna lanciare Synergy **come amministratore**, poi andare su *Edit -> Services* e selezionare *Install* nella sezione *Client*.

Se si vuole avviare il client dalla linea di comando, questa è una linea che si può mettere in un file `.bat` o semplicemente eseguirla da `cmd.exe`. Questa punta ad un file di configurazione in `C:\synergy.sgc` e viene eseguita in background come un servizio.

 `START /MIN /D"C:\Program Files\Synergy+\bin" synergys.exe -d ERROR -n m6300 -c C:\synergy.sgc -a 10.66.66.2:24800` 

### Mac OS X

Individuare il programma synergyc nella cartella synergyc e trascinarlo nella finestra del terminale: vi apparirà in suo percorso completo. Ora aggiungere in fondo l'hostname del server in maniera che il comando completo somigli a questo:

 `/path/to/synergyc/synergyc server-host-name` 

Poi premere `Invio`.

## Problemi conosciuti

Se Arch viene usato come client in un'installazione di Synergy, il server potrebbe non essere in grado di riattivare il monitor del client. Ci sono alcune soluzioni per questo, come eseguire il comando seguente via [SSH](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)"), se ACPI è abilitato (leggere: [modificare la configurazione di DPMS e ScreenSaver con xset](/index.php/Display_Power_Management_Signaling#Modifying_DPMS_and_screensaver_settings_using_xset "Display Power Management Signaling")):

 `# xset dpms force on` 

## Risoluzione di problemi

La documentazione ufficiale ha [una pagina per le FAQ](http://synergy-foss.org/pm/projects/synergy/wiki/UserFAQ) e [una per la risoluzione dei problemi](http://synergy2.sourceforge.net/trouble.html).

### Ripetizione dei tasti

Se si hanno problemi con la ripetizione dei tasti sul computer client (host Linux), digita semplicemente:

 `# /usr/bin/xset r on` 

in una console.

### Mappatura della tastiera

Se si hanno problemi con la mappatura della tastiera usando la tastiera del server in una finestra del client (ad esempio un terminale), riconfigurare la mappatura della tastiera in X dopo aver avviato synergyc potrebbe risolvere il problema. Il seguente comando configura la mappatura della tastiera al suo valore attuale:

```
# setxkbmap $(setxkbmap -query | grep "^layout:" | awk -F ": *" '{print $2}')

```

### messages.log viene spammato da synergyc

Se si esegue *synergyc* come descritto sopra, il proprio file `/var/log/messages.log` sarà spammato con messagi del genere:

```
 May 26 22:30:46 localhost Synergy 1.4.6: 2012-05-26T22:30:46 INFO: entering screen
         /build/src/synergy-1.4.6-Source/src/lib/synergy/CScreen.cpp,103
 May 26 22:30:47 localhost Synergy 1.4.6: 2012-05-26T22:30:47 INFO: leaving screen
         /build/src/synergy-1.4.6-Source/src/lib/synergy/CScreen.cpp,121

```

Per evitare ciò eseguire *synergyc* con l'opzione `-d WARNING`. Quest'opzione del *livello di debug* istruisce synergy a loggare solamente i messaggi che sono del livello *WARNING* o superiore.

```
 synergyc -d WARNING server-host-name

```

È anche possibile editare la linea che lancia *synergyc* se si usa un file `/etc/rc.d/synergyc`.

```
    [ -z "$PID" ] && /usr/bin/synergyc -d WARNING "$SERVERALIAS"

```

## Altre risorse

*   Sito ufficiale di Synergy: [http://synergy-foss.org](http://synergy-foss.org)
*   Documentazione ufficiale: [http://synergy-foss.org/docs](http://synergy-foss.org/docs)