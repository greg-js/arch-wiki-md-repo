Molti programmi per Windows possono essere utili anche su Linux, è quindi possibile che esista un apposito pacchetto per questi programmi. La differenza tra i due sistemi operativi rende questo compito un po’ complesso. In questa guida parleremo degli eseguibili Win32, dato che i progetti i cui codici sorgente sono disponibili saranno già compilati per Linux.

## Contents

*   [1 Cose da controllare attentamente](#Cose_da_controllare_attentamente)
    *   [1.1 Licenza](#Licenza)
    *   [1.2 Installer](#Installer)
    *   [1.3 Portabilità e pulizia](#Portabilit.C3.A0_e_pulizia)
*   [2 Breve guida](#Breve_guida)
    *   [2.1 Installazione](#Installazione)
    *   [2.2 Lo script in /usr/bin](#Lo_script_in_.2Fusr.2Fbin)
*   [3 Esempio](#Esempio)
*   [4 Gecko](#Gecko)

## Cose da controllare attentamente

*   La licenza, la licenza permette la pacchettizzazione del programma?
*   L'installer, è possibile effettuare l'installazione da linea di comando(silent installation)? O meglio, esiste una versione senza installer?
*   Portabilità e pulizia, il programma è portabile? il programma è pulito?

Si definisce portabile un programma che non scrive **mai** all'interno del registro di sistema o fuori dalla sua cartella di installazione; si definisce pulito se esso non scrive **mai** all'interno della sua cartella di installazione, ma può salvare le proprie impostazioni all'interno della cartella dell'utente. Un programma può essere entrambi (es. non salva impostazioni) o nessuno dei due(es. salva nella cartella di installazione, salva in altre destinazioni, e modifica il registro...).

### Licenza

Solitamente le licenze sono contenute in file di testo all'interno della cartella di installazione. Se non si riesce a trovarla, provare ad cercarla nelle finestre di dialogo durante l'installazione. Se non viene impedita la pacchettizzazione sarà possibile proseguire. All'autore non interessa. Altrimenti la licenza può non consentire di rimuovere file o di pacchettizzare il software. Nel primo caso sarà necessario fare attenzione che durante il processo di [makepkg](/index.php/Makepkg_(Italiano) "Makepkg (Italiano)") non venga perso nessun file, sarà possibile rimuovere file non necessari(es. gli unistaller) nella fase di `post_install()`; nell'altro caso tutti i processi di installazione dovranno essere eseguiti nella fase di `post_install()`. La fase di `build()` si occuperà solo di copiare i file di installazione.

### Installer

Risulta molto più semplice utilizzare archivi compressi come **.zip** piuttosto che l'installer grafico di Windows. Se non si ha scelta, dato che l'autore del programma lo distribuisce solo nella versione con l'installer, cercare documentazione alla ricerca di una installazione da linea di comando(silently oppure silent installation). Il sito [MSFN](http://unattended.msfn.org/unattended.xp/page/list/switch/) solitamente è un buon posto dove cercare queste informazioni. Se non si trova un modo, provare estraendo l'installer con [cabextract](https://www.archlinux.org/packages/?name=cabextract), [unrar](https://www.archlinux.org/packages/?name=unrar) oppure altri software di estrazione; a volte funziona.

### Portabilità e pulizia

Un programma portabile non necessita del proprio filesystem emulato da wine, quindi controllare sul sito [Portable Freeware](http://www.portablefreeware.com) se il programma che si vuole pacchettizzare sia portabile.

## Breve guida

L'idea di base alla pacchettizzazione di un programma per Windows è quella di usare i file del programma come semplici dati che wine interpreterà, proprio come si comportano JVM e java bytecode.

Quindi il programma sarà installato in `/usr/share/"$pkgname"` ed esso salverà tutto ciò che deve salvare in `"$HOME"/."$pkgname"`. Tutto sarà preparato da un piccolo script salvato in `/usr/bin/"$pkgname"` che creerà la cartella, la preparerà se necessario ed infine avvierà il programma.

Nella prossima sezione saranno discussi tutti i passi.

In questo modo tutti gli utenti avranno le proprie configurazioni e le loro decisioni non influenzeranno gli altri utenti.

### Installazione

Se il programma non ha un installer, la sua installazione consiste nell'estrarre l'archivio; decomprimere l'archivio in `"$pkgdir"/usr/share/$pkgname`, assicurarsi che i permessi siano corretti. Questi comandi eseguiranno quanto detto:

```
find "$pkgdir"/usr/share -type -f -exec chmod 644 "{}" \;
find "$pkgdir"/usr/share -type -d -exec chmod 755 "{}" \;

```

Se il programma non può essere installato secondo il metodo più semplice, allora sarà necessario creare un ambiente Wine:

```
install -m755 -d "$srcdir"/tmp "$srcdir"/tmp/env "$srcdir"/tmp/local
export WINEPREFIX="$srcdir"/tmp/env
export XDG_DATA_HOME="$srcdir"/tmp/local
wine "$srcdir"/installer.exe /opzionisilent

```

Ancora non è stata discussa definizione di portabilità, ma se il programma non necessita di modificare il registro di sistema, sarà possibile copiare la cartella da:

```
"$srcdir"/tmp/env/drive_c/Program\ Files/programname

```

Altrimenti sarà necessario copiare tutti i file del registro ed eventualmente gli altri file. `"$srcdir"/tmp/local` conterrà i menù, le icone ed i desktop file, se saranno necessari posso essere inseriti nel pacchetto. Se non esiste un modo di eseguire l'installazione da linea di comando(modalità silent). Può essere creato un archivio **.tar.gz** e caricato su qualche servizio di hosting? Se non è possibile automatizzare l'installazione, forzare l'utente a seguire l'installer, e sperare che non vengano effettuati errori, è consigliato quindi utilizzare alcuni controlli prima di copiare una cartella alla cieca,che magari non esiste(es. l'utente ha premuto 'Cancel'.).

### Lo script in /usr/bin

Questo script preparerà le cartelle di configurazione ed avvierà il programma. Se il programma è portabile, sarà simile a questo:

```
#!/bin/bash
unset WINEPREFIX
if [ ! -d "$HOME"/.nomeprogramma ] ; then
   mkdir -p "$HOME"/.nomeprogramma
   #preparare l'ambiente quì
fi
WINEDEBUG=-all wine "$HOME"/.nomeprogramma/nomeprogramma "$@"

```

Se è pulito, invece sarà simile a questo:

```
#!/bin/bash
export WINEPREFIX="$HOME"/.nomeprogramma/wine
if [ ! -d "$HOME"/.nomeprogramma ] ; then
   mkdir -p "$HOME"/.nomeprogramma/wine
   wineboot -u
   #copiare i file di registro se necessario
fi
WINEDEBUG=-all wine /usr/share/nomeprogramma "$@"

```

Come si può vedere, nel secondo caso, non viene preparato nessun ambiente. Infatti un programma pulito sarà avviato direttamente da `/usr/share` dato che non ha bisogno di scrivere nella sua cartella di installazione, quindi le sue impostazioni saranno salvate all'interno del filesystem emulato.

Se l'applicazione non è ne pulita ne portabile, le due idee devono essere combinate.

Se il programma non salva nessuna impostazione, saltare l'istruzione `**if**` e cominciare da `/usr/share`.

I compiti della preparazione dell'ambiente possono differire enormemente a seconda delle applicazioni, ma seguono queste linee guida:

*   se il programma...
    *   ...necessita soltanto di leggere un file, creare un link ad esso.
    *   ...necessita di scrivere in un file, copiarlo.
    *   ...non usa un file, ignorarlo.

Il minimo essenziale consiste nell'avviare `WINEDEBUG=-all wine /usr/share/programname "$@"`.

Solitamente l'ambiente sarà ricreato con dei link simbolici tra la cartella `"$HOME"/.nomeprogramma` ed i file in `/usr/share/nomeprogramma`. Ma dato che alcuni programmi per Windows hanno spesso dei percorsi per le cartelle molto differenti tra loro, può essere necessario creare il link direttamente alla cartella `"$HOME"/.nomeprogramma/wine/drive_c/Program\ Files/nomeprogramma`.

Chiaramente questa è solo un idea per integrare le applicazioni Win32 in un ambiente Linux, non dimenticate di usare intelligenza e buonsenso.

Un esempio, **utorrent** normalmente è un'applicazione pulita, ma con un semplice passaggio può essere usata come portabile. Dato che è composto da un singolo file ed è molto piccolo creare un ambiente wine (circa 5MB) è probabilmente troppo limitante. Risulta un metodo migliore creare all'interno della cartella `$HOME/.utorrent` un link simbolico al file eseguibile ed un file vuoto dal nome `settings.dat` in modo da renderlo portabile. Con il vantaggio aggiuntivo che semplicemente visitando la cartella `$HOME/.utorrent` sarà possibile visualizzare i file **.torrent** scaricati.

## Esempio

Verrà costruito un pacchetto per [eMule](http://www.emule-project.net/). Secondo [Portable Freeware](http://www.portablefreeware.com/?q=emule), eMule non è completamente portabile dato che scrive alcune (inutili) chiavi nel registro di sistema.

D'altro canto non è nemmeno pulito, dato che salva i suoi file di configurazione e salva i download nella cartella di installazione.

Fortunatamente esiste una versione [installer-less(priva di installer)](http://prdownloads.sourceforge.net/emule/eMule0.49b.zip).

Ecco come sarà scritto il [PKGBUILD](/index.php/PKGBUILD_(Italiano) "PKGBUILD (Italiano)"); l'unica dipendenza sarà [wine](https://www.archlinux.org/packages/?name=wine). Il valore md5sums dovrebbe essere inserito.

```
# Maintainer: You <youremail>
pkgname=emule
pkgver=0.49b
pkgrel=1
pkgdesc="One of the biggest and most reliable peer-to-peer file sharing
clients around the world."
arch=(i686 x86_64)
url="[http://www.emule-project.net](http://www.emule-project.net)"
license=('GPL')
depends=()
depends=(wine)
makedepends=(unzip)
source=(emule [http://prdownloads.sourceforge.net/emule/eMule$pkgver.zip](http://prdownloads.sourceforge.net/emule/eMule$pkgver.zip))
noextract=()
options=(!strip)

build() {
  rm -f src/eMule"$pkgver"/license* #la licenza è GPL

  install -d -m755 pkg/usr/share/emule
  cp -ra src/eMule"$pkgver"/* pkg/usr/share/emule
  find pkg/usr/share/emule -type d -exec chmod 755 "{}" \;
  find pkg/usr/share/emule -type f -exec chmod 644 "{}" \;

  install -d -m755 pkg/usr/bin
  install -m755 emule pkg/usr/bin 
  }

```

Ora verrà creato il file `**emule**`, che come definito in `build()` verrà copiato e reso eseguibile in `/usr/bin`.

```
#!/bin/bash
export WINEARCH=win32 WINEPREFIX="$HOME/.emule/wine"

if [ ! -d "$HOME"/.emule ] ; then
  mkdir -p "$HOME"/.emule/wine || exit 1
  #Ogni utente avrà la sua configurazione, si copiano i file di default
  #dato che emule scirve in essi.
  cp -r /usr/share/emule/config "$HOME"/.emule || exit 1
  #Vengono creati i link simbolici ai file che devono essere letti durante l'esecuzione
  ln -s /usr/share/emule/emule.exe "$HOME"/.emule/emule || exit 1
  ln -s -T /usr/share/emule/lang "$HOME"/.emule/lang || exit 1
  ln -s -T /usr/share/emule/webserver "$HOME"/.emule/webserver || exit 1
fi

wine "$HOME"/.emule/emule "$@"

```

Per essere più precisi, si potrebbe aggiungere un messaggio nel file .install per avvertire l'utente che è possibile disabilitare la cronologia di ricerca, in quanto wine non visualizza correttamente quel menu. Sarà inoltre possibile fornire delle configurazioni di default o ottimizzate. Ed è fatta, eseguire `makepkg`, controllare la cartella del pacchetto per essere sicuri, ed installare.

## Gecko

Gecko è un motore html usato da Wine per effettuare il rendering html per quei programmi che normalmente usano Explorer. Solo pochi programmi attualmente necessitano di questa caratteristica, ma Wine richiederà l'installazione di Gecko se non si è provveduto. Per disabilitare la visualizzazione della richiesta si può: installare Gecko, usare una _dlloverride_.

Il metodo più facile per installare Gecko è usando [winetricks](https://www.archlinux.org/packages/?name=winetricks) (dall'omonimo pacchetto):

```
$ wineboot -u #(Cliccare cancel quando richiesto)
$ winetricks -q gecko

```

Per disabilitare il rendering html ed il messaggio sara necessario usare un _dlloverride_ nel proprio script.

```
export WINEDLLOVERRIDES="mshtml="

```

è possibile disabilitarlo anche tramite `winecfg`: semplicemente impostando _mshtml_ a **Disable**.