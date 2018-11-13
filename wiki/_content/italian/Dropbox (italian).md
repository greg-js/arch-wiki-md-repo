[Dropbox](https://www.dropbox.com) è un sistema di condivisione file che recentemente ha introdotto un client GNU/Linux. Viene utilizzato per sincronizzare file in modo trasparente attraverso computer e architetture. Spostando i file nella propria cartella `~/Dropbox` essi verranno automaticamente sincronizzati con il proprio repository centralizzato.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Pacchetti opzionali](#Pacchetti_opzionali)
    *   [1.2 Avviare automaticamente Dropbox nel proprio DE/WM](#Avviare_automaticamente_Dropbox_nel_proprio_DE/WM)
*   [2 Alternativa all'installazione: usare l'interfaccia web](#Alternativa_all'installazione:_usare_l'interfaccia_web)
*   [3 Systemd](#Systemd)
*   [4 Senza Nautilus (Un altro metodo)](#Senza_Nautilus_(Un_altro_metodo))
*   [5 Rendere sicuro il proprio Dropbox](#Rendere_sicuro_il_proprio_Dropbox)
*   [6 Sessioni di Dropbox multiple](#Sessioni_di_Dropbox_multiple)
*   [7 Dropbox sui computer portatili](#Dropbox_sui_computer_portatili)
*   [8 Problemi conosciuti](#Problemi_conosciuti)
    *   [8.1 Dropbox continua a dire: Downloading files](#Dropbox_continua_a_dire:_Downloading_files)
    *   [8.2 Cambiare la directory di lavoro di Dropbox direttamente dal wizard](#Cambiare_la_directory_di_lavoro_di_Dropbox_direttamente_dal_wizard)
    *   [8.3 Connecting...](#Connecting...)
    *   [8.4 Dropbox non parte - "Questo avviene di solito per un errore di permessi"](#Dropbox_non_parte_-_"Questo_avviene_di_solito_per_un_errore_di_permessi")
        *   [8.4.1 Controllare i permessi](#Controllare_i_permessi)
        *   [8.4.2 Re-linking del proprio account](#Re-linking_del_proprio_account)
        *   [8.4.3 Errori causati dall'esaurimento dello spazio](#Errori_causati_dall'esaurimento_dello_spazio)
        *   [8.4.4 Errori causati dal LOCALE](#Errori_causati_dal_LOCALE)
        *   [8.4.5 Unable to monitor filesystem](#Unable_to_monitor_filesystem)
*   [9 Alternative](#Alternative)

## Installazione

[dropbox](https://aur.archlinux.org/packages/dropbox/) può essere installato da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"). Altrimenti è possibile provare [dropbox-experimental](https://aur.archlinux.org/packages/dropbox-experimental/).

1.  Dopo aver installato il pacchetto è possibile avviare Dropbox dal proprio menu applicazioni o eseguendo `dropboxd` da linea di comando. L'icona del client apparirà nel vassoio di sistema.
2.  Alla fine un popup chiederà di eseguire l'accesso con il proprio account Dropbox, o di creare un nuovo account. Inserire le proprie credenziali.
3.  Dopo un po' sarà possibile vedere un popup "Benvenuto in Dropbox", che darà l'opportunità di visualizzare una breve panoramica di Dropbox.
4.  Fare clic su "Finish and go to My Dropbox".

Per gli utenti [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") non sono necessari altri passaggi, infatti KDE avvierà automaticamente al boot il demone di Dropbox. Per gli utenti che usano [xfce](/index.php?title=XFCE_(Italiano)&action=edit&redlink=1 "XFCE (Italiano) (page does not exist)") invece sarà necessario copiare `dropbox.desktop` in `~/.config/autostart`.

### Pacchetti opzionali

*   Per un'interfaccia a linea di comando è possibile installare [dropbox-cli](https://aur.archlinux.org/packages/dropbox-cli/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").
*   Per un'integrazione in Nautilus si installi [nautilus-dropbox](https://aur.archlinux.org/packages/nautilus-dropbox/) da AUR. Il plugin di Nautilus partirà automaticamente.
*   Per un'integrazione con Nemo, installare [nemo-dropbox-git](https://aur.archlinux.org/packages/nemo-dropbox-git/) da AUR.
*   Per un'integrazione con [Thunar](/index.php/Thunar_(Italiano) "Thunar (Italiano)"), installare [thunar-dropbox](https://aur.archlinux.org/packages/thunar-dropbox/) da AUR.
*   Per gli utenti [KDE](/index.php/KDE_(Italiano) "KDE (Italiano)") è disponibile un client di KDE: [kfilebox](https://aur.archlinux.org/packages/kfilebox/) da AUR.

### Avviare automaticamente Dropbox nel proprio DE/WM

Dropbox può essere avviato automaticamente aggiungendo `dropboxd` a `~/.xinitrc` (o `~/.config/openbox/autostart`, in base alle proprie impostazioni).

## Alternativa all'installazione: usare l'interfaccia web

Se tutto ciò di cui si ha bisogno è un accesso basilare ai file nel proprio Dropbox, è possibile usare l'interfaccia web in [https://www.dropbox.com](https://www.dropbox.com) per caricare e scaricare file dal proprio Dropbox. Questa può essere una valida alternativa all'esecuzione di un demone di Dropbox e al salvataggio di tutti i file sulla propria macchina.

## Systemd

Le ultime versioni di dropbox, vengono rilasciate con un service per [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)"). Quindi è facile avviare dropbox al boot:

```
# systemctl enable dropbox@<user>

```

## Senza Nautilus (Un altro metodo)

Un altro metodo di usare Dropbox senza Nautilus ma con un altro gestore file come Thunar è descritto qui sotto:

1\. Creare uno script in Nautilus fittizio che lanci Thunar:

```
   $ sudo touch /usr/bin/nautilus && sudo chmod 667 /usr/bin/nautilus && sudoedit /usr/bin/nautilus

```

2\. Inserire questo testo nel file, salvare e uscire:

```
   #!/bin/bash
   exec thunar $2
   exit 0

```

3\. Lanciare Dropbox

```
   $ dropboxd

```

4\. Cliccare sull'icona di Dropbox nel vassoio di sistema per aprire la propria cartella di Dropbox in Thunar.

**Nota:** Se si ha Nautilus installato, ma non lo si vuole usare, non occorre modificare il file esistente sotto `/usr/bin`, ma basta cambiare `/usr/bin` con `/opt/dropbox` nella fase 2 sopra, in questo modo: `$ sudo touch /opt/dropbox/nautilus && sudo chmod +x /opt/dropbox/nautilus && sudoedit /opt/dropbox/nautilus`. Dropbox controllerà questo percorso prima!

## Rendere sicuro il proprio Dropbox

Se si desidera memorizzare dati sensibili nel proprio Dropbox bisognerebbe prima cifrarlo. La sincronizzazione con Dropbox è cifrata, ma tutti i file sono (per il momento) memorizzati sul server come messi nel proprio Dropbox.

*   Dropbox funziona con [TrueCrypt](/index.php/TrueCrypt "TrueCrypt"), e dopo aver caricato il volume TrueCrypt su Dropbox le prestazioni saranno abbastanza ragionevoli, perché Dropbox ha un lavoro binario diverso.

*   Un'altra possibilità è usare [EncFS](/index.php/EncFS "EncFS"), che ha il vantaggio che tutti i file sono cifrati separatamente, e quindi non occorre determinare in anticipo le dimensioni del contenuto che si vuole cifrare e la propria cartella cifrata crescerà o si ridurrà mentre si aggiungono/cancellano/modificano/ file dentro di essa. Si può anche montare un volume cifrato all'avvio usando l'opzione `-S` di `encfs` per evitare di inserire la passphrase, ma si noti che i propri file non sono in questo modo sicuri rispetto a chi accede direttamente al proprio computer.

## Sessioni di Dropbox multiple

Se si desidera separare o distinguere i propri dati, personali e di lavoro per esempio, è possibile inscriversi a Dropbox con differenti indirizzi email e tenere più cartelle sincronizzate con differenti sessioni. Il principio di base e la guida generale sono descritti nel [Wiki di Dropbox](http://wiki.dropbox.com/TipsAndTricks/MultipleInstancesOnUnix).

**Nota:** Quando si mettono insieme sessioni multiple occorre selezionare la cartella di destinazione, che l'installer di Dropbox chiede nell'ultimo passaggio; un esempio può essere `/home/dropbox-personal`, `/home/dropbox-work`, e così via.

Qui c'è uno script che può essere usato per portare a termine l'operazione: basta creare una cartella nella lista "dropboxes" per avere un'altra sessione di Dropbox riferita alla cartella e caricata all'avvio dallo script.

```
#!/bin/bash                                                                                              

 #*******************************                                                                        
 # Multiple dropbox instances                                                                            
 #*******************************                                                                        

 dropboxes=(.dropbox-personal .dropbox-work)                                                            

 for dropbox in ${dropboxes[@]}                                                                          
 do                                                                                                      
     if ! [ -d $HOME/$dropbox ];then                                                                     
         mkdir $HOME/$dropbox                                                                            
     fi                                                                                                  
     HOME=$HOME/$dropbox/ /usr/bin/dropbox start -i                                                      
 done   

```

## Dropbox sui computer portatili

Dropbox di per sé è abbastanza bravo nell'affrontare i problemi di connettività. Se si ha un portatile e il roaming tra diversi ambienti di rete Dropbox potrebbe avere problemi nel riconnettersi se non viene riavviato. Il modo più semplice per risolvere questo problema è con [netcfg](/index.php/Netcfg_(Italiano) "Netcfg (Italiano)") usando POST_UP e PRE_DOWN.

In ogni profilo di rete (o nella [configurazione tramite interfaccia](/index.php/Netcfg_(Italiano)#Configurazione_tramite_interfaccia "Netcfg (Italiano)")) utilizzato aggiungere i comandi appropriati:

```
POST_UP="any other code; su -c 'DISPLAY=:0 /usr/bin/dropboxd &' your_user"
PRE_DOWN="any other code; killall dropbox"

```

Ovviamente your_user deve essere modificato e 'any other code;' può essere omesso se non serve. Questo script si assicurerà che Dropbox sia in esecuzione solo se c'è un profilo di rete attivo.

Se si hanno problemi di connessione con il [Network Manager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)"), [questa discussione](https://bbs.archlinux.org/viewtopic.php?pid=790905,) sul forum potrebbe essere utile.

## Problemi conosciuti

### Dropbox continua a dire: Downloading files

Succede a volte che Dropbox rimanga fermo su "Downloading files" mentre in realtà i file risultano sincronizzati. Questo succede se la cartella in condivisione è situata su una partizione NTFS. In tal caso prestare attenzione alla sintassi del proprio `/etc/fstab`. Evitare gli spazi nel punto di mount sembra essere la soluzione:

```
UUID=01CD2ABB65E17DE0 /run/media/username/Windows ntfs-3g uid=username,gid=users 0 0

```

### Cambiare la directory di lavoro di Dropbox direttamente dal wizard

Sembra sia successo ad alcuni utenti di non riuscire a cambiare la directory di default `~/Dropbox` in una personalizzata come ad esempio `/media/dati/Dropbox`. In tal caso, selezionare la finestra per il cambio delle directory e dare un `Ctrl + L`, quindi selezionare la cartella prescelta premendo prima "choose" e poi "open".

### Connecting...

**Nota:** Questo problema sembra esser stato risolto dalle ultime release di Dropbox. Prima di usare questo script testare Dropbox normalmente

Potrebbe accadere che Dropbox non riesce a connettersi con successo perché viene caricato prima che venga stabilita una connessione di rete. Per risolvere il problema il contenuto del file /opt/dropbox/dropboxd ha bisogno di essere sostituito con il seguente:

```
#!/bin/sh

# Copyright 2008 Evenflow, Inc., 2010 Dropbox
#
# Environment script for the dropbox executable.

start_dropbox() {
PAR=$(dirname $(readlink -f $0))
OLD_LD_LIBRARY_PATH=$LD_LIBRARY_PATH
LD_LIBRARY_PATH=$PAR:$LD_LIBRARY_PATH 

TMP1=`ps ax|grep dropbox|grep -v grep`
if [ -n "$TMP1" ]; then
  kill -9 $(pidof dropbox) >/dev/null 2>&1
fi
exec $PAR/dropbox $@ &
}

do_dropbox() {
start_dropbox >/dev/null 2>&1
while [ 1 ]; do
  sleep 5
  ERROR="$(net_test)"
  if [ -n "$ERROR" ]; then
    LAST_ERROR=1
  else
    if [ -n "$LAST_ERROR" ]; then
      # Connection seems to be up but last cycle was down
      LAST_ERROR=""
      start_dropbox >/dev/null 2>&1
    fi
  fi
done

}

net_test() {
TMP1="$(ip addr |grep "inet" |grep -v "127.0.0.1")"
[ -z "$TMP1" ] && echo "error"
}

do_dropbox

```

Il seguente script è una valida alternativa. Prima di avviare Dropbox, controlla la presenza di una connessione attiva usando curl per controllare hosts e ip disponibili. Se le condizioni non lo consentono, Dropbox non viene avviato subito. Un nuovo tentativo verrà eseguito dopo qualche secondo. Questo script riproverà ad avviare dropbox un po' di volte ma non per sempre. La logica è questa: parte da un tempo di attesa di 5 secondi e ogni qualvolta non ci sia una connessione internet tale attesa viene moltiplicato per 1,5 fino a 1500 secondi (25 minuti).

```
#!/bin/bash

# Copyright 2008 Evenflow, Inc., 2010 Dropbox
#
# Environment script for the dropbox executable.

WAIT_TIME=5 #initial time to wait between checking the internet connection
#HOSTS="www.google.com www.wikipedia.org 8.8.8.8 208.67.222.222"
HOSTS="www.google.com www.wikipedia.org "

PAR=$(dirname $(readlink -f $0))
OLD_LD_LIBRARY_PATH=$LD_LIBRARY_PATH
LD_LIBRARY_PATH=$PAR${LD_LIBRARY_PATH:+:}$LD_LIBRARY_PATH

#non-zero exit code iff none of the hosts could be reached
check_net() {
        local ret=1
        for i in $HOSTS; do
                #ping -w2 -c2 $i > /dev/null 2>&1 && ret=0 && break
                curl -o /dev/null $i > /dev/null 2>&1 && ret=0 && break
        done
        echo $ret
}

#if dropbox is running; kill it. Then start dropbox
start_dropbox() {
local tmp=`ps ax|grep -E "[0-9] $PAR/dropbox"|grep -v grep`
        if [ -n "$tmp" ]; then
                kill -9 $(pidof dropbox) > /dev/null 2>&1
        fi
        exec $PAR/dropbox $@ > /dev/null 2>&1 &
}

#loop over: start dropbox iff check_net returns 0
#loop (and with it, the entire script) terminates when dropbox has been restarted,
#+ or the waiting time has exeeded 1500 seconds (it grows 50% with each iteration of the loop)
attempt_startup() {
        while [ $WAIT_TIME -lt 1500  ] ; do
                if [ $(check_net) -eq 0 ]; then
                        start_dropbox
                        exit
                fi
                sleep $WAIT_TIME
                #WAIT_TIME=$(($WAIT_TIME+$WAIT_TIME/2))
                let "WAIT_TIME += WAIT_TIME/2"
        done
}

start_dropbox
attempt_startup &

```

### Dropbox non parte - "Questo avviene di solito per un errore di permessi"

#### Controllare i permessi

Controllare le cartelle del proprio Dropbox prima di eseguire l'applicazione. Queste includono

*   `~/.dropbox` - Cartella di configurazione di Dropbox
*   `~/Dropbox` - Cartella di scaricamento di Dropbox (predefinita)

Si può avere la certezza che queste non diano problemi cambiando il loro proprietario con `chown -R`.

Questo errore potrebbe anche essere causato dalla pienezza di `/var`.

#### Re-linking del proprio account

[Le FAQ di Dropbox](https://www.dropbox.com/help/72) suggeriscono che questo errore può essere causato da errori di configurazione e può essere risolto rimovendo la cartella di configurazione corrente:

```
# mv ~/.dropbox ~/.dropbox.old

```

e riavviando Dropbox.

#### Errori causati dall'esaurimento dello spazio

Un errore comune che potrebbe accadere è che non ci sia più spazio nelle proprie partizioni `/tmp` e `/var`. Se accade questo Dropbox andrà in errore all'avvio con il seguente errore nel suo log:

```
Exception: Not a valid FileCache file

```

Una cronologia dettagliata di questo evento può essere trovata nel [forum](https://bbs.archlinux.org/viewtopic.php?pid=973458). Assicurarsi che ci sia abbastanza spazio disponibile prima di lanciare Dropbox.

#### Errori causati dal LOCALE

Provare ad avviare `dropboxd` con questo codice:

```
LANG=$LOCALE
dropboxd

```

(È possibile usare anche un altro valore per LANG; deve essere nel formato "en_US.UTF-8") Questo aiuta quando si esegue da uno script di Bash o da una shell Bash nella quale è stato caricato `/etc/rc.d/functions`.

#### Unable to monitor filesystem

Se si hanno molti file da sincronizzare nella directory ~/Dropbox è possibile che si ottenga questo errore:

```
Unable to monitor filesystem
Please run: echo 100000 | sudo tee /proc/sys/fs/inotify/max_user_watches and restart Dropbox to correct the problem.

```

Per risolvere questo problema è sufficiente aggiungere:

```
fs.inotify.max_user_watches = 100000

```

al file `/etc/sysctl.d/99-sysctl.conf`. Sarà necessario riavviare il computer.

## Alternative

*   [Spider Oak](https://spideroak.com/) - [spideroak](https://aur.archlinux.org/packages/spideroak/)
*   [KFileBox](http://kdropbox.deuteros.es/) - [kfilebox](https://aur.archlinux.org/packages/kfilebox/)
*   [Wuala](https://www.wuala.com/) - [wuala](https://aur.archlinux.org/packages/wuala/)