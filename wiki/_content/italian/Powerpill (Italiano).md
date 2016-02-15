**Attenzione:** Lo sviluppo di _Powerpill_ è stato ufficialmente terminato: la sua ultima versione non è compatibile con _pacman>=3.5_. Leggere [[1]](https://bbs.archlinux.org/viewtopic.php?id=115660).

**Nota:** Esistono altri modi per usare aria2 per lo scaricamento dei pacchetti. Leggere [Improve pacman performance#Using_aria2](/index.php/Improve_pacman_performance#Using_aria2 "Improve pacman performance")

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
*   [3 Configurazione](#Configurazione)
*   [4 Uso di Reflector](#Uso_di_Reflector)
*   [5 Uso di Base](#Uso_di_Base)
    *   [5.1 Aggiornare il Sistema](#Aggiornare_il_Sistema)
    *   [5.2 Installazione di pacchetti](#Installazione_di_pacchetti)

## Introduzione

Powerpill è uno script scritto da Xyne che incorpora [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)") e velocizza il download dei pacchetti grazie all'utilizzo di aria2c per effettuare download concorrenti e segmentati. Individua i pacchetti obiettivo dell'operazione di aggiornamento richiesta e usa una lista di mirror per creare un metalink. Questo metalink viene poi passato al manager di download aria2 per il download dei pacchetti. Spesso è possibile ottenere una significativa riduzione nei tempi di download grazie agli effetti combinati dei download simultanei e combinati.

Esempio: si vuole effettuare un update e si esegue _pacman -Syu_ il quale restituisce una lista di 20 pacchetti disponibili per un aggiornamento della dimensione totale di 200 mega. Se l'utente effettua il download tramite pacman, i pacchetti verranno scaricati uno alla volta. Se vengono scaricati tramite powerpill, verranno scaricati più pacchetti simultaneamente e nella maggior parte dei casi molto più velocemente (a seconda della velocità della connessione, della disponibilità dei pacchetti sui server, della velocità/carico del server, etc.)

Un confronto tra pacman e powerpill su un sistema ha rilevato una velocità, nello scenario precedente, 4 volte più veloce usando powerpill con una velocità media di download di 1.2 MB/sec contro i 300 kB/sec di pacman.

## Installazione

Nonostante l'abbandono del progetto, Powerpill può ancora essere scaricato da [http://xyne.archlinux.ca/old_projects/powerpill/](http://xyne.archlinux.ca/old_projects/powerpill/)

Assicurarsi di avere installato il pacchetto _perl-crypt-ssleay_, altrimenti non sarà possibile utilizzare **Reflector** (leggere sotto)

```
# pacman -S perl-crypt-ssleay

```

## Configurazione

Powerpill ha un solo file di configurazione `/etc/powerpill.conf` che può essere modificato a piacimento. La maggior parte delle opzioni sono ben commentate e semplici da capire per l'utente.

## Uso di Reflector

Di default, Powerpill è configurato per usare [Reflector](/index.php/Reflector "Reflector") per generare una lista dei 45 server di aggiornamento aggiornati di recente da inserire all'interno della sua lista di server. Questo per essere sicuri che ci sia un numero sufficiente di server all'interno della lista per un significativo aumento di velocità. Questa procedura non prende in considerazione la velocità del singolo server così si può voler impostare la velocità minima di download richiesta all'interno della sezione aria2_options in /etc/powerpill.conf:

```
#lowest-speed-limit=10K

```

E' anche possibile cambiare `Reflect = -l 45` per ottenere i mirror più veloci invece dei più recenti anche se questo non è consigliato in quanto il tempo necessario per misurare i mirror nella maggior parte dei casi sarà maggiore del tempo risparmiato in fase di download dei pacchetti.

E' possibile anche semplicemente commentare la linea "Reflect" ma in questo caso è necessario avere un numero di mirror nel proprio `/etc/pacman.d/mirrorlist` almeno uguale al numero di connessioni massime impostate in /etc/powerpill.conf. Powerpill sfrutta l'accesso a server multipli per velocizzare i download.

## Uso di Base

Per la maggior parte delle operazioni, powerpill funziona esattamente come pacman dal momento che è uno script contenitore di pacman.

### Aggiornare il Sistema

Per aggiornare il sistema (sincronizzare e aggiornare i pacchetti installati) usando powerpill, passare semplicemente l'opzione -Syu come si sarebbe fatto con pacman:

```
# powerpill -Syu

```

### Installazione di pacchetti

Per installare un pachetto e le sue dipendenze, usare semplicemente powerpill con l'opzione -S come si sarebbe fatto con pacman:

```
# powerpill -S package

```

E' possibile anche installare pacchetti multipli nello stesso modo in cui si sarebbe fatto con pacman:

```
# powerpill -S package1 package2 package3

```