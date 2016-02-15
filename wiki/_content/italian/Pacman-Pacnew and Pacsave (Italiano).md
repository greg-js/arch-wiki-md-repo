## Contents

*   [1 Per Iniziare](#Per_Iniziare)
*   [2 File di backup dei pacchetti](#File_di_backup_dei_pacchetti)
*   [3 Spiegazione dei Tipi](#Spiegazione_dei_Tipi)
    *   [3.1 .pacnew](#.pacnew)
    *   [3.2 .pacsave](#.pacsave)
    *   [3.3 .pacorig](#.pacorig)
*   [4 Localizzare i file .pac*](#Localizzare_i_file_.pac.2A)
*   [5 Gestire i file .pacnew](#Gestire_i_file_.pacnew)
    *   [5.1 Usare Meld per sistemare le Differenze](#Usare_Meld_per_sistemare_le_Differenze)
*   [6 Risorse](#Risorse)

## Per Iniziare

Durante degli aggiornamenti o rimozioni di pacchetti, [Pacman](/index.php/Pacman "Pacman") vi informerà di alcuni file (solitamente dei file di configurazione in `/etc`) che sono stati installati con una estensione `.pacnew` o di cui è stata fatta una copia con una estensione `.pacsave`.

Un file `.pacnew` può essere creato durante un aggiornamento con (`pacman -Syu`, `pacman -Su` o (`pacman -U`) per evitare di sovrascrivere una configurazione già esistente e precedentemente modificata dall'utente. Quando ciò accade, apparirà un messaggio nell'output di pacman simile al seguente:

```
warning: /etc/pam.d/usermod installed as /etc/pam.d/usermod.pacnew

```

Un file `.pacsave` può essere creato durante la rimozione di un pacchetto (`pacman -R`), o durante una sostituzione di pacchetto (che forza la rimozione di un pacchetto che andrà a sostituire). Quando nel database di pacman c'è una registrazione che un certo file posseduto da un pacchetto debba essere salvato, verrà creato un file `.pacsave`. Quando ciò accade, pacman avviserà con un messaggio simile al seguente:

```
warning: /etc/pam.d/usermod saved as /etc/pam.d/usermod.pacsave

```

Questi file richiedono l'intervento manuale dell'utente, ed è buona pratica sistemarli subito dopo una rimozione o aggiornamento di quei pacchetti. Se lasciati in giro, configurazioni errate possono portare a malfunzionamenti di qualche software o addirittura impedire l'avvio degli stessi.

## File di `backup` dei pacchetti

Un `PKGBUILD` di un pacchetto può specificare quali particolari file debbano essere preservati o backup-pati quando il relativo pacchetto venga aggiornato o rimosso. Per esempio, il `PKGBUILD` di `pulseaudio` contiene la riga seguente:

```
backup=('etc/pulse/client.conf' 'etc/pulse/daemon.conf' 'etc/pulse/default.pa')

```

## Spiegazione dei Tipi

I tipi differenti dei file *.pac* sono i seguenti:

### .pacnew

Per ogni file `backup` di un pacchetto che sta per essere aggiornato, pacman fa una comparazione incrociata di tre [md5sums](https://en.wikipedia.org/wiki/Md5sum "wikipedia:Md5sum") generati dal contenuti dei file stessi: uno per la versione originariamente installata dal pacchetto, una per la versione corrente, e una per la versione che sta per essere installata con l'aggiornamento. Se il file attualmente presente sul sistema è stato modificato rispetto alla versione originale, pacman non può conoscere come importare questi cambiamenti nella nuova versione dello stesso file. Dunque, invece di sovrascrivere il file vecchio con quello nuovo, pacman salverà la nuova versione del file di configurazione con l'estensione _.pacnew_ e lascerà la versione già presente sul sistema intatta.

Nel dettaglio, il controllo triplo delle somme MD5 possono portare ad uno dei casi seguenti:

	originale = _X_, attuale = _X_, nuovo = _X_ 

	tutte e tre le versioni hanno contenuti identici, quindi sovrascrivere non porta a problemi. Verrà quindi sovrascritto il file e non verranno fatte notifiche all'utente. (nonostante ciò, questa sovrascrittura porterà all'aggiornamento delle informazioni del filesystem relative alle date di installazione, modifica e accesso oltre che alla modifica dei permessi se necessarie.)

	originale = _X_, attuale = _X_, nuovo = _Y_ 

	la versione corrente del file è identica alla originale, ma la nuova versione è differente. Dato che l'utente non ha dunque modificato la configurazione attuale, e che la nuova versione può contenere miglioramenti o risoluzione di qualche bug, il file corrente verrà sovrascritto con quello nuovo, ancora senza notifiche all'utente. Questa è l'unica maniera che ha pacman per aggiornare i contenuti di un file.

	originale = _X_, attuale = _Y_, nuovo = _X_ 

	il pacchetto originale e quello nuovo contengono la stessa versione del file, ma quello sul sistema è stato modificato. In questo caso, verrà lasciata la versione correntemente sul sistema, senza notifiche all'utente.

	originale = _X_, attuale = _Y_, nuovo = _Y_ 

	la versione nuova è identica a quella installata sul sistema. Anche qui, verrà effettuata la sovrascrittura senza notifiche all'utente. (nonostante ciò, questa sovrascrittura porterà all'aggiornamento delle informazioni del filesystem relative alle date di installazione, modifica e accesso oltre che alla modifica dei permessi se necessarie.)

	originale = _X_, attuale = _Y_, nuovo = _Z_ 

	le tre versioni del file sono differenti: in questo caso, verrà conservata la versione corrente al suo posto, la nuova versione verrà installata con estensione `.pacnew` e l'utente verrà avvisato dell'esistenza della nuova versione. In questo caso, l'utente deve intervenire per fare le dovute modifiche al nuovo file e sostituirlo manualmente alla versione corrente.

### .pacsave

Se l'utente ha modificato uno dei file specificati nella sezione `backup` allora questo file verrà rinominato con una estensione `.pacsave` e verrà conservato nel filesystem qualora il pacchetto venga rimosso.

**Note:** L'uso dell'opzione `-n` con il comando `pacman -R` equivarrà all'ordine di rimuovere **qualsiasi** file relativo al pacchetto da rimuovere; in questo caso nessun file `.pacsave` verrà creato.

### .pacorig

Quando un file (solitamente un file di configurazione posizionato in `/etc`) che viene incontrato durante un installazione o aggiornamento non appartiene a nessun pacchetto installato ma è elencato in quelli `backup` per il pacchetto che si sta per installare, sarà salvato con estensione `.pacorig` e rimpiazzato con la versione del pacchetto. Solitamente questo accade quando un file di configurazione è stato spostato da un pacchetto all'altro. Se questi file non fossero elencati nella sezione `backup`, pacman annullerebbe l'operazione per un errore di conflitto fra pacchetti.

**Note:** Poichè i file `.pacorig` tendono ad essere creati per circostanze speciali, non esiste un metodo universale per gestirli. Può essere utile consultare le [Arch News](https://www.archlinux.org/news/) per delle istruzioni in caso ci si trovi davanti a qualche aggiornamento particolare.

## Localizzare i file .pac*

Arch Linux non fornisce utility ufficiali per gestire i file `.pacnew`. L'utente dovrà dunque gestirseli a mano autonomamente. Per fare ciò, innanzitutto dovrete sapere dove sono. Quando si aggiorna o rimuove una gran quantità di pacchetti, potreste non accorgervi di qualche file *.pac* da sistemare. Per scoprire quali sono:

Sarà innanzitutto necessario cercarli nel luogo dove di solito sono i file di configurazione:

```
find /etc -name "*.pac*"

```

o nel disco intero:

```
find / -name "*.pac*"

```

In alternativa sarà possibile sfruttare il file log di pacman per trovarli:

```
egrep "pac(new|orig|save)" /var/log/pacman.log

```

Notare che il log non tiene traccia di quali file attualmente sono già presenti sul sistema o di quelli che sono già stati rimossi.

## Gestire i file .pacnew

Una volta che tutti i file `.pacnew` esistenti sono stati localizzati, l'utente potrà gestirli manualmente tramite varie utilità di unione come [vimdiff](/index.php/Vim#Merging_Files_.28Vimdiff.29 "Vim"), ediff (parte di [emacs](/index.php/Emacs "Emacs")), meld (una utilità grafica per Gnome), o Kompare (una utilità grafica per KDE GUI gui), per poi eliminare il file `.pacnew` una volta fatte le modifiche.

Ci sono alcune utilità di terze parti che forniscono vari livelli di automatizzazione di queste operazioni, disponibili sul [repository community](/index.php/Community_repository "Community repository") e su [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"):

*   [Dotpac](/index.php/Dotpac "Dotpac") - Script interattivo basilare, basato su interfaccia ncurses e che fornisce istruzioni passo-passo. Nessuna funzione di unione automatica.
*   [pacdiff](https://aur.archlinux.org/packages.php?ID=15326) - Script minimale e non documentato per terminale. Fa parte del pacchetto `pacman` nel repo `community`.
*   [pacdiffviewer](https://aur.archlinux.org/packages.php?ID=5863) - Completo Script da terminale con capacità di unione automatica. fa parte di [`yaourt`](/index.php/Yaourt_(Italiano) "Yaourt (Italiano)").
*   [diffpac](https://aur.archlinux.org/packages/diffpac/) - Versione di pacdiffviewer autonoma.

### Usare Meld per sistemare le Differenze

È possibile usare meld in loop per effettuare tutti i cambiamenti necessari. Questo script vi permetterà di sistemare i file uno ad uno, permettendovi di osservarne le differenze:

```
#!/bin/bash
# pacnew-update - merge *.pacnew files with original configurations with meld

pacnew=$(find /etc -type f -name "*.pacnew")

for config in $pacnew; do
  # Merge with meld
  kdesu meld ${config%\.*} $config &
  wait
done
```

Nello script viene utilizzato `kdesu`, comando della suite KDE, per ottenere permessi di root tramite GUI grafica. Usate `gksudo` se avete un sistema Gnome/XFCE. Eventualmente potete aggiungere la riga `sudo rm -i $config` per rimuovere i file dopo averli modificati, ma ciò richiederà privilegi particolari per l'utente. Una maniera migliore per fare ciò è eseguire il comando seguente dopo che avrete effettuato tutte le modifiche, in modo da eliminare tutti i file `*.pacnew`:

```
find /etc -type f -name "*.pacnew" -exec rm {} \;

```

## Risorse

*   Arch Linux Forums: [Dealing With .pacnew Files](https://bbs.archlinux.org/viewtopic.php?id=53532) (in inglese)