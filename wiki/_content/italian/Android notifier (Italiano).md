Android Notifier è una applicazione Linux che permette di ricevere notifiche sullo stato di SMS, MMS oppure riguardo al livello di batteria ed altro ancora dal proprio telefono al proprio pc Linux, Mac oppure Windows. Questo articolo spiega come installare ed eseguire in background su Arch Linux. Sarà necessario aver installato sul proprio telefono l'applicazione Remote Notifier che è disponibile gratuitamente sul Market di Android.

## Contents

*   [1 Requisiti](#Requisiti)
*   [2 Installazione](#Installazione)
*   [3 Fix per Arch Linux (bugfix)](#Fix_per_Arch_Linux_.28bugfix.29)
*   [4 Configurazione](#Configurazione)
*   [5 Avviare android-notifier](#Avviare_android-notifier)

## Requisiti

*   Applicazioni Android installate sul proprio telefono: Remote Notifier by Rodrigo Damazio, dal Market.
    *   [Sito dell'autore](http://code.google.com/p/android-notifier/)
    *   [Altro su Appbrain](http://www.appbrain.com/app/remote-notifier-for-android/org.damazio.notifier/)
*   La porta 10600 tcp/udp aperta sul proprio firewall (in arrivo le regole per iptables...)

## Installazione

Installare [android-notifier-desktop](https://aur.archlinux.org/packages/android-notifier-desktop/) da [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)"), installare anche come sua dipendenza: [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk).

## Fix per Arch Linux (bugfix)

**Nota:** A partire dalla versione 0.5.1-2 (uscita il 25-07-2011) questo bugfix viene incorporato nel [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)") non è quindi necessario modificare manualmente il file.

Modificare il file `/usr/share/android-notifier-desktop/run.sh`

 `/usr/share/android-notifier-desktop/run.sh` 
```
.....
java -DconfigDir=$configDir -Djava.util.prefs.userRoot=$configDir/android-notifier-desktop -Djava.net.preferIPv4Stack=true -client -Xms8m -Xmx32m -jar android-notifier-desktop.jar $1
```

in

 `/usr/share/android-notifier-desktop/run.sh` 
```
.....
java -DconfigDir=$configDir -Djava.util.prefs.userRoot=$configDir/android-notifier-desktop -Djava.net.preferIPv4Stack=true -client -Xms8m -Xmx32m -jar /usr/share/android-notifier-desktop/android-notifier-desktop.jar $1
```

(viene usato il percorso completo al file `/usr/share/android-notifier-desktop/android-notifier-desktop.jar`)

Se non viene applicata tale modifica, l'errore *"The file android-notifier-desktop.jar couldn't be found"* sarà mostrato e l'applicazione non si avvierà.

[Maggiori informazioni riguardo al bugfix](http://code.google.com/p/android-notifier/issues/detail?id=270)

## Configurazione

Per configurare android-notifier, eseguire:

```
$ /usr/share/android-notifier-desktop/run.sh -p 

```

Per mostrare informazioni sull'uso del comando eseguire:

```
$ /usr/share/android-notifier-desktop/run.sh -h

```

## Avviare android-notifier

Aggiungere questo comando ad esempio in `~/.xinitrc` oppure nell'avvio automatico del proprio Desktop Environment:

```
/usr/share/android-notifier-desktop/run.sh &

```

Oppure eseguirlo in un terminale.