**Nota:** Questo articolo è in fase di traduzione. Seguite per ora le istruzioni della versione inglese.

Chromium è un browser web grafico di Google, bastato sul motore di rendering [WebKit](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit").

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Visualizzare vari caratteri non latini](#Visualizzare_vari_caratteri_non_latini)
    *   [2.2 Usare Chromium senza ambiente desktop](#Usare_Chromium_senza_ambiente_desktop)
    *   [2.3 Resa dei font](#Resa_dei_font)
    *   [2.4 Browser predefinito](#Browser_predefinito)
    *   [2.5 Flash Player](#Flash_Player)
    *   [2.6 Aprire file PDF in Chromium](#Aprire_file_PDF_in_Chromium)
        *   [2.6.1 libpdf.so](#libpdf.so)
        *   [2.6.2 mozplugger](#mozplugger)
        *   [2.6.3 kpartsplugin](#kpartsplugin)
    *   [2.7 Certificati](#Certificati)
*   [3 Tips & tricks](#Tips_.26_tricks)
    *   [3.1 Controllare l'uso della memoria](#Controllare_l.27uso_della_memoria)
    *   [3.2 Collegare il file manager alla funzione "Mostra cartella"](#Collegare_il_file_manager_alla_funzione_.22Mostra_cartella.22)
    *   [3.3 Le icone non vengono mostrate nella scheda download](#Le_icone_non_vengono_mostrate_nella_scheda_download)
    *   [3.4 Cache in tmpfs](#Cache_in_tmpfs)
    *   [3.5 Profilo in tmpfs](#Profilo_in_tmpfs)
        *   [3.5.1 Semplice script in Bash per automatizzare il processo](#Semplice_script_in_Bash_per_automatizzare_il_processo)
        *   [3.5.2 Aggiungere un processo cron per mantenerlo aggiornato](#Aggiungere_un_processo_cron_per_mantenerlo_aggiornato)
        *   [3.5.3 Aggiungere una voce a /etc/rc.local.shutdown](#Aggiungere_una_voce_a_.2Fetc.2Frc.local.shutdown)
    *   [3.6 Abilitare funzionalità sperimentali](#Abilitare_funzionalit.C3.A0_sperimentali)
    *   [3.7 Motori di ricerca](#Motori_di_ricerca)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Profilo predefinito](#Profilo_predefinito)
*   [5 Risorse](#Risorse)

## Installazione

La versione stabile di Chromium può essere installata dal repository ufficiale con:

```
# pacman -S chromium

```

Esiste anche una versione in via di sviluppo che può essere trovata in [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)") sotto il nome di [chromium-dev](https://aur.archlinux.org/packages/chromium-dev/), insieme a [chromium-update](https://aur.archlinux.org/packages/chromium-update/), uno script di aggiornamento che installa o aggiorna alle nightly build di Chromium. C'è anche una versione in binario ([chromium-browser-bin](https://aur.archlinux.org/packages/chromium-browser-bin/)).

**Nota:** La compilazione di chromium-beta o chromium-dev dura all'incirca quanto quella del kernel Linux.

**Nota:** chromium-update installa le nightly build di Chromium che sono pre-compilate dal server Chromium Buildbot

Esistono anche alcuni pacchetti in AUR che forniscono la versione in binario di Google Chrome.

Si veda anche [questo articolo](http://news.softpedia.com/news/Google-Chrome-vs-Chromium-Understanding-Stable-Beta-Dev-Releases-and-Version-No-140060.shtml) per una spiegazione delle differenze tra le tre versioni, Chromium vs. Chrome e la numerazione dei rilasci.

## Configurazione

### Visualizzare vari caratteri non latini

Per visualizzare correttamente caratteri cinesi, giapponesi e coreani, si veda [qui](/index.php/Fonts_(Italiano)#Pacchetti_font "Fonts (Italiano)"), dove ci sono istruzioni dettagliate per installare i vari font TrueType.

### Usare Chromium senza ambiente desktop

A differenza di [Firefox](/index.php/Firefox_(Italiano) "Firefox (Italiano)"), Chromium non mantiene un proprio database di associazioni mimetype-to-application. Si affida invece a `xdg-open` (parte di extra/xdg-utils) per aprire file e, per esempio, i [magnet link](https://en.wikipedia.org/wiki/Magnet_URI_scheme "wikipedia:Magnet URI scheme").

In un [ambiente desktop](/index.php/Desktop_environment "Desktop environment") (es. [Gnome](/index.php/GNOME_(Italiano) "GNOME (Italiano)"), o [Kde](/index.php/KDE_(Italiano) "KDE (Italiano)"), or [Xfce](/index.php/Xfce_(Italiano) "Xfce (Italiano)")), `xdg-open` passa semplicemente gli argomenti all'applicazione che apre i file di quell'ambiente desktop (rispettivamente `gnome-open`, `kde-open`, o `exo-open`), e ciò significa che le associazioni sono lasciate all'ambiente desktop.

Quando non vengono rilevati ambienti desktop invece (per esempio quando viene eseguito un [window manager](/index.php/Window_Manager_(Italiano) "Window Manager (Italiano)") standalone, come [Openbox](/index.php/Openbox_(Italiano) "Openbox (Italiano)")), il comportamento di `xdg-open` diventa piuttosto strano e irritante: molti tipi di file vengono aperti da Firefox o Chromium stessi, non c'è nessun supporto per i magnet link, etc.

Ci sono molte soluzioni a questo problema, elencate qui sotto. È possibile:

*   Ottimizzare xdg-open, rendendolo più svelto (aka "le patch sono benvenute" :P )

*   Usare parti di un ambiente desktop, e più specificatamente, la parte che include l'applicazione che apre il file; per GNOME bisognerebbe installare 'libgnome' (e le sue dipendenze), per xfce, 'exo'. La variabile d'ambiente $DE ha bisogno di essere esportata prima dell'avvio del gestore di finestre. Per esempio:

 `~/.xinitrc` 
```
export DE=gnome
exec  openbox

```

*   Usare [mimeo](https://aur.archlinux.org/packages/mimeo/) (scritto da un utente Arch (trusted)) e [xdg-utils-mimeo](https://aur.archlinux.org/packages/xdg-utils-mimeo/), che rimpiazza extra/xdg-utils e contiene uno script `xdg-open` patchato per fare uso di `mimeo`; allo stesso modo può essere usato `gnome-open`. Associazioni di applicazioni Mimetype<->possono essere personalizzate facilmente in `$XDG_CONFIG_HOME/mimeo.conf` o `~/.config/mimeo.conf`

*   Usare le associazioni file pcmanfm (es. per gli utenti dell'ambiente desktop lxde). Cambiare:

 `/usr/bin/xdg-open` 
```
generic)
pcmanfm "$url"
;;

```

	o modificare il proprio `.profile`

	 `~/.profile` 

```
export DESKTOP_SESSION=LXDE

```

*   Quando si usa openbox e nessun ambiente desktop come KDE, GNOME o XFCE eseguire i comandi:

	 `~/.config/openbox/environment` 

```
export BROWSER=chromium

```

**Attenzione:** Non esportare alcuna variabile dell'ambiente desktop!

Poi è necessario compilare il file `~/.local/share/applications/defaults.list` con le associazioni predefinite. Se questo appare scoraggiante, è possibile usare alcune utility:

*   xdg-mime: non molto intuitivo; es. per usare xpdf come visualizzatore pdf predefinito:

```
$ xdg-mime default xpdf.desktop application/pdf

```

*   mimetype (pacchetto [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo)): più intuitivo; es. per selezionare un'applicazione predefinita per un'estensione data (è necessario un semplice file):

```
$ mimetype -d file.extension

```

Questo dovrebbe creare una voce nel proprio database mime locale:

 `~/.local/share/applications/defaults.list` 
```
[Default Applications]
text/html=chromium.desktop
application/pdf=xpdf.desktop

```

Si riavvii chromium e ora i propri file pdf dovrebbero venire aperti con xpdf.

È stato riscontrato che questo funziona solo come utente normale - come root si possono avere dei problemi poiché non vengono create di cartelle per il mime locale. Si veda anche [questa discussione](https://bbs.archlinux.org/viewtopic.php?id=93956).

Si potrebbe anche provare ad installare [perl-file-mimeinfo](https://www.archlinux.org/packages/?name=perl-file-mimeinfo)

### Resa dei font

Si dà per scontato che Chromium usi le impostazioni in `~/.fonts.conf`, sebbene potrebbero essere state modificate manualmente (si veda [come configurare i font](/index.php/Font_configuration#Basic_settings "Font configuration")). Se i font non sono ancora resi come dovrebbero è possibile usare le impostazioni xft [come suggerito qui](/index.php/Xdefaults "Xdefaults"). Si crei `~/.Xdefaults` qualora non esista e si aggiunga:

```
! Xft settings ---------------------------------------------------------------

Xft.dpi:        96
Xft.antialias:  true
Xft.rgba:       rgb
Xft.hinting:    true
Xft.hintstyle:  hintslight

```

**Nota:** queste impostazioni riguarderanno ogni applicazione che leggerà `~/.Xdefaults`, e non solo Chromium; Un esempio è [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode").

### Browser predefinito

Il modo più semplice per rendere Chromium il browser predefinito è impostare la variabile `$BROWSER=chromium` in `~/.profile`

```
if [ -n "$DISPLAY" ]; then
     BROWSER=chromium
fi

```

Un altro modo è modificare lo script *xdg-open*.

```
$ sudo $YOUR_EDITOR /usr/bin/xdg-open

```

Quasi in fondo al file c'è una lunga lista orizzontale di browser:

```
if [ x"$DE" = x"" ]; then
   # if BROWSER variable is not set, check some well known browsers instead
   if [ x"$BROWSER" = x"" ]; then
       BROWSER=links2:links:lynx:w3m
       if [ -n "$DISPLAY" ]; then
           BROWSER=firefox:mozilla:epiphany:konqueror:chromium-browser:google-chrome:$BROWSER
       fi
   fi
   DE=generic
fi

```

Bisogna aggiungere **chromium:** *(ricordarsi i due punti che separano le voci)* prima di **firefox:mozilla:** ... e salvare. Per provare se questo funziona davvero, inserire in un terminale:

```
$ xdg-open [http://google.com](http://google.com)

```

Se tutto ha funzionato a meraviglia, sarà aperta una nuova scheda o una nuova finestra di Chromium con la homepage di Google, a seconda dalle proprie impostazioni.

Un'altra opzione, quando viene usato **mimeo**, è associare i link "http://" con chromium:

 `~/.config/mimeo.conf` 
```
/usr/bin/chromium
  ^http://

```

Se tutto questo non basta, è possibile provare ad aggiungere la seguente stringa alla lista `[Added Associations]` in `~/.local/share/applications/mimeapps.list`

```
x-scheme-handler/http=chromium.desktop

```

### Flash Player

Installare il plugin flash e riavviare chromium:

```
# pacman -S flashplugin

```

### Aprire file PDF in Chromium

Ci sono due modi per farlo: il primo è usando il plugin per la visualizzazione dei PDF di Google Chrome, il secondo è consentire a Chromium di accedere, per esempio, ad Adobe Reader attraverso il plugin mozplugger. Gli utenti KDE possono anche scegliere KParts Plugin e usare qualsiasi applicazione KDE installata come visualizzatore incorporato.

#### libpdf.so

libpdf è l'implementazione di Google di un lettore PDF. Sebbene compatibile, è attualmente solamente una parte delle release di Chrome, e non di quelle di Chromium.

Il modo più semplice per aggiungerlo a quest'ultimo è usare il pacchetto fornito da AUR — [chromium-stable-libpdf](https://aur.archlinux.org/packages/chromium-stable-libpdf/) per le versioni stabili del browser o, per le versioni dev, [chromium-libpdf](https://aur.archlinux.org/packages/chromium-libpdf/) se il proprio pacchetto di Chromium è installato in `/usr/lib/chromium`, o [chromium-browser-libpdf](https://aur.archlinux.org/packages/chromium-browser-libpdf/) se è installato in `/opt/chromium-browser`.

Per farlo automaticamente, scaricare una versione di Google Chrome che corrisponde alla versione di Chromium che si sta usando:

```
$ wget [https://dl-ssl.google.com/linux/direct/google-chrome-stable_current_i386.deb](https://dl-ssl.google.com/linux/direct/google-chrome-stable_current_i386.deb)
$ wget [https://dl-ssl.google.com/linux/direct/google-chrome-unstable_current_i386.deb](https://dl-ssl.google.com/linux/direct/google-chrome-unstable_current_i386.deb)

```

```
$ wget [https://dl-ssl.google.com/linux/direct/google-chrome-stable_current_amd64.deb](https://dl-ssl.google.com/linux/direct/google-chrome-stable_current_amd64.deb)
$ wget [https://dl-ssl.google.com/linux/direct/google-chrome-unstable_current_amd64.deb](https://dl-ssl.google.com/linux/direct/google-chrome-unstable_current_amd64.deb)

```

Estrarre il file .deb con:

```
$ ar vx <deb-file>

```

Estrarre l'archivio LZMA con:

```
$ tar -xJf <lzma-file>

```

Spostare `libpdf.so` da `opt/google/chrome/` alla cartella appropriata come deciso sopra. Potrebbe essere necessario un cambiamento dei permessi dei file e di proprietà (i permessi di `libpdf.so` dovrebbero essere 755).

Avviare Chromium e aprire *about:plugins*. Dovrebbe ora vedersi "Chrome PDF Viewer"; se necessario, attivarlo.

**Nota:** Nel momento in cui una nuova versione di Chromium non venisse aggiornata, `libpdf.so` potrebbe diventare incompatibile. Perciò e con rispetto per i possibili fix di sicurezza è consigliabile aggiornare entrambi allo stesso tempo.

#### mozplugger

Per usare mozplugger, installare [mozplugger-chromium](https://aur.archlinux.org/packages/mozplugger-chromium/) da AUR. Seguire le istruzioni simili descritte in [Firefox tweaks](/index.php/Firefox_tweaks "Firefox tweaks") per impostare l'applicazione PDF che si vorrebbe usare con mozplugger-chromium.

#### kpartsplugin

Per usare KParts Plugin, installare [kpartsplugin](https://www.archlinux.org/packages/?name=kpartsplugin) da AUR. Il plugin deve essere attivato per aprire PDF in Chromium usando una sessione incorporata di Okular.

### Certificati

Chromium usa [NSS](/index.php/Nss "Nss") per la gestione dei certificati. I certificati possono essere gestiti (e aggiunti) andando in Opzioni -> Preferenze -> Roba da smanettoni -> Gestisci i certificati.

## Tips & tricks

### Controllare l'uso della memoria

*   Chromium offre alcune opzioni a linea di comando per aiutare a controllare quanto è efficiente con la memoria del sistema, determinando quanto spesso dovrebbe rilasciare indietro la memoria al sistema operativo. Questo viene fatto con il flag *--memory-model=X*, dove X può essere *high*, *medium*, o *low*. Impostarlo in high può consentire a Chromium di non rilasciare mai memoria. Medium tende a ridurre lo spazio di lavoro della memoria quando si cambia scheda, e low riduce lo spazio di lavoro quando si cambia scheda e quando il browser non viene usato attivamente. Eseguire chromium con *--memory-model=low* potrebbe veramente migliorare le prestazioni, sebbene questo possa variare.

### Collegare il file manager alla funzione "Mostra cartella"

Quando si usa un gestore di finestre come Openbox in combinazione con un file manager come Thunar invece di un ambiente desktop, questa funzione di Chromium può mostrare solo il percorso della cartella all'interno di Chromium. Comunque, per mostrare file nella cartella usando invece il proprio file manager, installare `perl-file-mimeinfo`.

### Le icone non vengono mostrate nella scheda download

Si potrebbe verificare il caso in cui Chromium nella scheda di download mostra i placeholder delle icone (icone che rappresentano documenti incompleti) invece delle icone appropriate. La causa più probabile è che non è installato un ambiente desktop.

È possibile rimediare a questo installando le icone di GNOME:

```
# pacman -S gnome-icon-theme

```

### Cache in tmpfs

Per chi usa un SSD è preferibile avere la cache di Chromium in un tmpfs, ma non è necessario avere l'interno profilo in un tmpfs. È stata postata [qui](https://bbs.archlinux.org/viewtopic.php?pid=967385#p967385) una soluzione per questo problema.

**Attenzione:** Chiudere Chromium prima di iniziare!
Rimpiazzare *your_user* con il proprio username.

Aggiungere la riga seguente a `/etc/fstab`:

```
cache-chromium /home/your_user/.cache/chromium tmpfs defaults,noatime,mode=1777 0 0

```

Poi cancellare & ricreare la cartella cache per Chromium:

```
rm -r /home/your_user/.cache/chromium
mkdir /home/your_user/.cache/chromium

```

Riavviare la macchina o eseguire **sudo mount -a**

Dopo la cache di Chromium dovrebbe essere in RAM. Si può controllare con **df -h**.

C'è anche un parametro a linea di comando per posizionare la cache da qualche altra parte:

```
--disk-cache-dir=/tmp

```

Questa potrebbe essere un'altra soluzione se, per esempio, `/tmp` è in RAM.

### Profilo in tmpfs

Il profilo predefinito di Chromium è posizionato in `~/.config/chromium`. Questo profilo può essere riposizionato in un filesystem [tmpfs](http://en.wikipedia.org/wiki/Tmpfs), incluso `/tmp`, o `/dev/shm` per miglioramenti nella risposta delle applicazioni una volta che l'intero profilo sia immagazzinato nella RAM. Un altro beneficio è la riduzione delle operazioni di lettura e scrittura del disco, della quale gli SSD beneficiano di più.

#### Semplice script in Bash per automatizzare il processo

Usare il seguente script in Bash per muovere automaticamente il proprio profilo di Chromium in `/dev/shm` e mantenerlo sincronizzato.

`$HOME/bin/sync-chromium`:

```
#!/bin/bash

STATIC=$HOME/.config/chromium-backup
LINK=$HOME/.config/chromium
VOLATILE=/dev/shm/.chromium

[[ ! -d $VOLATILE/cache ]] && mkdir -p $VOLATILE/cache
[[ ! -h $HOME/.cache/chromium ]] && ln -s $VOLATILE/cache $HOME/.cache/chromium
[[ -r $VOLATILE ]] || install -dm755 $VOLATILE

if [[ `readlink $LINK` != $VOLATILE ]]; then
  mv $LINK $STATIC
  ln -s $VOLATILE $LINK
fi

if [[ -e $LINK/.flagged ]]; then
  rsync -a --delete --exclude .flagged $LINK/ $STATIC/
else
  rsync -a $STATIC/ $LINK/
  touch $LINK/.flagged
fi
```

Non dimenticarsi di renderlo eseguibile:

```
$ chmod +x $HOME/bin/sync-chromium

```

Impostare lo script all'accesso copiando il seguente nel proprio `~/.config/autostart`

`~/.config/autostart/sync-chromium.desktop`:

```
[Desktop Entry]
Type=Application
Exec=$HOME/bin/sync-chromium
Hidden=false
Name=ff-sync
```

#### Aggiungere un processo cron per mantenerlo aggiornato

Modificare la tabella di [cron](/index.php/Cron "Cron") dell'utente usando `crontab`:

```
$ crontab -e

```

Aggiungere una riga per avviare lo script ogni 30 minuti,

```
*/30 * * * * *~/bin/sync-chromium*

```

o aggiungere il seguente per farlo ogni 2 ore:

```
0 */2 * * * *~/bin/sync-chromium*

```

#### Aggiungere una voce a `/etc/rc.local.shutdown`

Infine una riga in `/etc/rc.local.shutdown` manterrà il proprio profilo sincronizzato quando la macchina si spengerà.

**Nota:** Sostituire la parola "user" con il nome utente dell'interessato nella riga seguente.

```
# echo "su user -c /home/user/bin/sync-chromium" >> /etc/rc.local.shutdown

```

### Abilitare funzionalità sperimentali

Per abilitare caratteristiche sperimentali di Chromium come WebGL e il rendering delle pagine web con la GPU, digitare "about:flags" nella barra degli indirizzi di Chromium e abilitare funzionalità che si desiderano.

### Motori di ricerca

SI possono rendere siti come wiki.archlinux.org e wikipedia.org facilmente ricercabili eseguendo prima di tutto una ricerca in queste pagine, poi andando in Options>Preferences>Basics e cliccando su "Manage" nella sezione "Default Search". Si può poi, per esempio, "Edit" la voce di Wikipedia e cambiare la sua parola chiave in "w". Poi, si può cercare in Wikipedia "Arch Linux" dalla barra degli indirizzi inserendo semplicemente "w arch linux". "?" è una parola chiave hard-coded per le ricerche in Google search (si comporta differentemente dalle altre parole chiave). Consente di cercare facilmente cose come "/bin/bash".

## Risoluzione dei problemi

### Profilo predefinito

Se non si è in grado di ricevere il proprio profilo predefinito quando si prova ad eseguire chromium:

```
$ chromium
[2630:2630:485325611:FATAL:chrome/browser/browser_main.cc(755)] Check failed: profile. 
Cannot get default profile. Trace/breakpoint trap

```

È necessario correggere il proprietario della cartella `~/.config/chromium`, e funzionerà.

```
$sudo chown -R yourusername:yourusergroup /home/yourusername/.config/chromium

```

## Risorse

*   [Chromium homepage (en)](http://www.chromium.org/Home)
*   [Differenze con Google Chrome (en)](https://en.wikipedia.org/wiki/Chromium_(web_browser)#Differences_from_Google_Chrome "wikipedia:Chromium (web browser)")
*   [Note di annunci e versioni per il browser Google Chrome (en)](http://googlechromereleases.blogspot.com/)