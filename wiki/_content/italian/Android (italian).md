<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Sviluppo Android su Arch](#Sviluppo_Android_su_Arch)
    *   [1.1 Ottenere SDK e i plugins IDE](#Ottenere_SDK_e_i_plugins_IDE)
        *   [1.1.1 Configurare Eclipse](#Configurare_Eclipse)
        *   [1.1.2 Configurare Netbeans](#Configurare_Netbeans)
    *   [1.2 Binari Android](#Binari_Android)
        *   [1.2.1 Installazione automatica](#Installazione_automatica)
        *   [1.2.2 Ottenerlo da AUR](#Ottenerlo_da_AUR)
        *   [1.2.3 Installazione manuale](#Installazione_manuale)
    *   [1.3 Android Debug Bridge (ADB) - Connettere un device reale](#Android_Debug_Bridge_(ADB)_-_Connettere_un_device_reale)
        *   [1.3.1 Trovare gli ID del proprio dispositivo](#Trovare_gli_ID_del_proprio_dispositivo)
        *   [1.3.2 Aggiungere le regole di udev](#Aggiungere_le_regole_di_udev)
        *   [1.3.3 Funziona?](#Funziona?)
    *   [1.4 Strumenti specifici per la piattaforma NVIDIA Tegra](#Strumenti_specifici_per_la_piattaforma_NVIDIA_Tegra)
*   [2 Tethering](#Tethering)
*   [3 Tips & Tricks](#Tips_&_Tricks)
    *   [3.1 Durante il Debug "Source not found"](#Durante_il_Debug_"Source_not_found")
    *   [3.2 Distribuzione linux sulla sdcard](#Distribuzione_linux_sulla_sdcard)
    *   [3.3 Android SDK su Arch 64](#Android_SDK_su_Arch_64)

## Sviluppo Android su Arch

### Ottenere SDK e i plugins IDE

(Se si sta usando Arch64, è necessario abilitare [il repo multilib](/index.php/Arch64_FAQ#Multilib_Repository_-_Multilib_Project "Arch64 FAQ"), per poter installare le dipendenze richieste usando [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)").)

Installare i componenti core SDK da [AUR](/index.php/Arch_User_Repository "Arch User Repository"):

1.  [android-sdk](https://aur.archlinux.org/packages/android-sdk/)
2.  [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/)

Il luogo tipico di installazione è `/opt/android-sdk`.

Quando si usa [Eclipse](/index.php/Eclipse "Eclipse") come IDE è necessario installare il plugin ADT e i pacchetti relativi. Se si riceve un messaggio riguardo a dipendenze irrisolvibili, installare [Java](/index.php/Java "Java") manualmente e provare di nuovo. Altrimenti è possibile usare [Netbeans](/index.php/Netbeans "Netbeans") per lo sviluppo dopo l'installazione di plugin in accordo con [queste istruzioni](http://www.nbandroid.org/p/installation.html).

#### Configurare Eclipse

Molta roba richiesta per lo sviluppo Android in Eclipse è già pacchettizzata su AUR:

Plugin ufficiale di Google – [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html):

1.  [eclipse-android](https://aur.archlinux.org/packages/eclipse-android/)

Dipendenze:

1.  [eclipse-emf](https://aur.archlinux.org/packages/eclipse-emf/)
2.  [eclipse-gef](https://aur.archlinux.org/packages/eclipse-gef/)
3.  [eclipse-wtp-wst](https://aur.archlinux.org/packages/eclipse-wtp-wst/)

Inserire il percorso per la posizione dell'Android SDK in

```
Windows -> Preferences -> Android

```

#### Configurare Netbeans

Se si preferisce usare Netbeans come proprio IDE e sviluppare applicazioni android, scaricare [nbandroid](http://www.nbandroid.org) andando in:

```
Tools -> Plugins -> Settings

```

Aggiungere il seguente URL: [http://kenai.com/projects/nbandroid/downloads/download/updatecenter/updates.xml](http://kenai.com/projects/nbandroid/downloads/download/updatecenter/updates.xml)

Poi andare in **Available Plugins** e installare i plugin **Android** e **Android Test Runner** per la propria versione dell'IDE. Una volta installati, andare in:

```
Tools -> Options -> Miscellaneous -> Android

```

e selezionare il percorso in cui è installato l'SDK. Ecco fatto, ora è possibile creare un nuovo progetto Android e iniziare a sviluppare usando Netbeans.

### Binari Android

Prima di sviluppare applicazioni android è necessario almeno installare una piattaforma Android; questo può essere fatto sia automaticamente che manualmente.

#### Installazione automatica

L'installazione automatica viene fatta attraverso l'Android SDK e il gestore di dispositivi, che è accessibile richiamando (assumendo che la `$PATH` [variabile](/index.php/Environment_variables "Environment variables") contenga il percorso alla cartella `tools` dell'Android SDK):

```
android

```

o in alternativa:

```
./<path_to_android-sdk>/tools/android

```

Se l'installazione automatica dà errore allora è necessario o avviare il tool di Android con privilegi superiori o impostare il proprio account utente come proprietario della cartella. Per cambiare l'ID del proprietario per tutte le cartelle SDK, eseguire il seguente comando come amministratore:

```
 chown -R USER /opt/android-sdk

```

Per cambiare l'ID del gruppo, invece, (raccomandato per utenti multipli), prima bisogna creare il gruppo, nell'esempio chiamato *android*, e aggiungere ad esso il proprio account:

```
 groupadd android
 gpasswd -a USER android

```

Poi, cambiare i permessi della cartella:

```
 chgrp -R android /opt/android-sdk
 chmod -R g+w /opt/android-sdk
 find /opt/android-sdk -type d -exec chmod g+s {} \;

```

Il comando finale imposta il bit *setgid* in tutte le sottocartelle, in modo che ogni nuovo file creato in esse riceva il giusto group ID.

Per un'installazione automatica passo-passo, si veda: [Installare componenti SDK (en)](http://developer.android.com/sdk/adding-components.html).

#### Ottenerlo da AUR

AUR attualmente contiene più pacchetti con i binari Android, a volte duplicati o con permessi sbagliati impostati. Sono tutti elencati alla pagina [android-sdk](https://aur.archlinux.org/packages/android-sdk/) (guardare la lista di pacchetti dipendenti).

#### Installazione manuale

Per l'installazione manuale:

1.  Scaricare il binario che si vuole sviluppare. [Questo sito](http://qdevarena.blogspot.com/2010/05/download-android-sdk-standalone-for.html) fornisce link online per vari componenti dell'Android SDK.
2.  Estrarre le tarball in `/<path_to_android-sdk>/platforms`.

Ora si dovrebbe vedere il binario scelto installato nella finestra Pacchetti installati dell'Android SDK e del gestore di dispositivi.

### Android Debug Bridge (ADB) - Connettere un device reale

Per far connettere ADB a un dispositivo reale o a un telefono sotto Arch, è necessario installare le regole [udev](/index.php/Udev "Udev") per connettere il dispositivo alla giusta voce /dev/. Questo può essere fatto manualmente oppure si può ricorrere al pacchetto AUR [android-udev](https://www.archlinux.org/packages/?name=android-udev) per usare una lista comune di vendor ID.

Ogni dispositivo android ha un USB vendor/product ID. Un esempio per HTC Evo è:

```
vendor id: 0bb4
product id: 0c8d

```

#### Trovare gli ID del proprio dispositivo

Inserire il proprio dispositivo ed eseguire:

```
# lsusb

```

Dovrebbe venir fuori qualcosa di questo tipo:

```
Bus 002 Device 006: ID 0bb4:0c8d High Tech Computer Corp.

```

#### Aggiungere le regole di udev

Usare le seguenti regole di udev come un template, e sostituire [VENDOR ID] e [PRODUCT ID]con i propri. Copiare queste regole in `/etc/udev/rules.d/51-android.rules`:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="[VENDOR ID]", MODE="0666"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_adb"
SUBSYSTEM=="usb",ATTR{idVendor}=="[VENDOR ID]",ATTR{idProduct}=="[PRODUCT ID]",SYMLINK+="android_fastboot"
```

Poi, per ricaricare le nuove regole di udev, eseguire:

```
# udevadm control --reload-rules

```

#### Funziona?

Dopo aver impostato le regole udev, scollegare e ricollegare il proprio dispositivo.

Dopo aver eseguito:

```
$ adb devices

```

si dovrebbe ottenere qualcosa del genere:

```
List of devices attached 
HT07VHL00676    device

```

Se non si ha il programma "adb" (di solito avviabile in */opt/android-sdk/platform-tools/*), significa che non sono stati installati i platform tools.

Se si ottiene una lista vuota (non c'è il dispositivo richiesto), potrebbe essere perché non è stato abilitata la modalità USB debug sul dispositivo. Si può fare questo andando in Impostazioni => Applicazioni => Sviluppo e abilitando il debug USB.

Bisognerà poi avviare adb come root per i corretti permessi di root per vedere il device. Se adb è già in esecuzione dare

```
$ sudo adb kill-server
$ sudo adb start-server

```

### Strumenti specifici per la piattaforma NVIDIA Tegra

Se la propria applicazione è destinata alla piattaforma NVIDIA Tegra, si potrebbe aver bisogno di installare anche strumenti, esempi e la documentazione messa a disposizione da NVIDIA. Nella [NVIDIA Developer Zone for Mobile](http://developer.nvidia.com/category/zone/mobile-development) ci sono due pacchetti - [Tegra Android Development Pack](http://developer.nvidia.com/tegra-resources), reperibile da AUR come [tegra-devpack](https://aur.archlinux.org/packages/tegra-devpack/) e [Tegra Toolkit](http://developer.nvidia.com/tegra-resources), reperibile su AUR come [tegra-toolkit](https://aur.archlinux.org/packages/tegra-toolkit/).

Il pacchetto [tegra-toolkit](https://aur.archlinux.org/packages/tegra-toolkit/) fornisce strumenti (la maggior parte dei quali collegati all'ottimizzazione della CPU e della GPU), esempi e documentazione, mentre [tegra-devpack](https://aur.archlinux.org/packages/tegra-devpack/)fornisce strumenti (NVIDIA Debug Manager) collegati a [Eclipse ADT](http://developer.android.com/sdk/eclipse-adt.html) e alla sua documentazione.

## Tethering

Si veda [Android tethering](/index.php/Android_tethering "Android tethering")

## Tips & Tricks

### Durante il Debug "Source not found"

Molto probabilmente il debugger vuole lavorare sul codice Java. Quando il codice sorgente di Android non arriva con l'Android SDK, questo porta ad un errore. La soluzione migliore è usare filtri passo passo per non saltare nel codice sorgente di Java. Gli step filter non sono attivati di default. Per attivarli:

```
Window -> Preferences -> Java -> Debug -> Step Filtering

```

Si consideri di selezionarli tutti. Se appropriato si può aggiungere il pacchetto android.* . Dare un'occhiata al post nel forum per maggiori informazioni: [http://www.eclipsezone.com/eclipse/forums/t83338.rhtml](http://www.eclipsezone.com/eclipse/forums/t83338.rhtml)

### Distribuzione linux sulla sdcard

È possibile installare Debian come in questo [thread](http://forum.xda-developers.com/showthread.php?t=631389), o adattarlo per installare Arch Linux. You should replace all debootstrap stuff by:

```
mkdir -p /data/local/mnt/var/{cache/pacman/pkg,lib/pacman}
pacman --root /data/local/mnt --cachedir /data/local/mnt/var/cache/pacman/pkg -Sy base

```

### Android SDK su Arch 64

Quando si usa l'Android SDK e il plugin Eclipse su un sistema a 64 bit, e l'emulatore va sempre in crash con un segfault, fare la seguente cosa: Disporre un file localtime file in /usr/share/zoneinfo/localtime e.g.:

```
 sudo cp /usr/share/zoneinfo/Europe/Rome /usr/share/zoneinfo/localtime

```