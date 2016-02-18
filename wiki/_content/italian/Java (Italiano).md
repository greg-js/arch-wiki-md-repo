"*Java è un linguaggio di programmazione originariamente sviluppato da Sun Microsystems e rilasciato nel 1995 come componente centrale della piattaforma Java della Sun Microsystems. Il linguaggio deriva gran parte della sua sintassi dal C e dal C++ ma ha un modello a oggetti più semplice e una minore quantità di ottimizzazioni a basso livello. Le applicazioni Java sono tipicamente compilate in bytecode che può essere eseguito su qualsiasi Java Virtual Machine (JVM) indipendentemente dall'architettura hardware.*" — [Wikipedia article](https://en.wikipedia.org/wiki/Java_(programming_language) "wikipedia:Java (programming language)")

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 OpenJDK](#OpenJDK)
        *   [1.1.1 Segnalare i pacchetti come out-of-date](#Segnalare_i_pacchetti_come_out-of-date)
    *   [1.2 Oracle Java SE](#Oracle_Java_SE)
        *   [1.2.1 Java SE 6/7](#Java_SE_6.2F7)
        *   [1.2.2 JDK-compat](#JDK-compat)
    *   [1.3 Oracle JRockit](#Oracle_JRockit)
    *   [1.4 VMkit](#VMkit)
    *   [1.5 Parrot VM](#Parrot_VM)
*   [2 Risoluzione problemi](#Risoluzione_problemi)
    *   [2.1 MySQL](#MySQL)
    *   [2.2 Audio applicazioni Java con Pulseaudio](#Audio_applicazioni_Java_con_Pulseaudio)
    *   [2.3 Usare un altro Window Manager](#Usare_un_altro_Window_Manager)
    *   [2.4 I font sono illeggibili](#I_font_sono_illeggibili)
    *   [2.5 Dipendenze mancanti](#Dipendenze_mancanti)
*   [3 Trucchi e consigli](#Trucchi_e_consigli)
    *   [3.1 Miglioramento del font rendering](#Miglioramento_del_font_rendering)
    *   [3.2 GTK LookAndFeel](#GTK_LookAndFeel)
    *   [3.3 Cambiare i symlinks](#Cambiare_i_symlinks)

## Installazione

L'unica implementazione della Java Virtual Machine supportata da Arch Linux è [OpenJDK](http://openjdk.java.net/) (open source). Quest'ultima è quasi perfetta e non dovrebbe essere necessario installare l'implementazione Java proprietaria di Oracle. Se si vuole installare l'implementazione di Oracle a fianco di OpenJDK, si veda la sezione [#JDK-compat](#JDK-compat).

**Nota:** Dopo l'installazione l'ambiente Java deve essere riconosciuto dalla shell (la variabile `$PATH` e `$JAVA_HOME` devono essere aggiornate). Questo può essere fatto dalla linea di comando eseguendo il comando source sul file `/etc/profile`; oppure, per gli ambienti Desktop, sarà sufficiente uscire e rientrare dalla propria sessione di lavoro (logout/login).

### OpenJDK

Il Java Runtime Environment ("JRE") di OpenJDK può essere installato attraverso il pacchetto [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), disponibile nei [repository ufficiali](/index.php/Official_repositories "Official repositories"). È anche disponibile il Java Development Kit ("JDK") installabile attraverso il pacchetto [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk). I file sorgente possono essere reperiti installando il pacchetto [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src).

Se si desidera utilizzare le funzionalità Java negli web browsers ([Java applets](https://en.wikipedia.org/wiki/Java_applet "wikipedia:Java applet") e [Java Web Start](https://en.wikipedia.org/wiki/Java_Web_Start "wikipedia:Java Web Start")), installare il pacchetto [icedtea-web-java7](https://www.archlinux.org/packages/?name=icedtea-web-java7). Per altri dettagli si legga [Browser plugins#Java (IcedTea)](/index.php/Browser_plugins#Java_.28IcedTea.29 "Browser plugins").

#### Segnalare i pacchetti come out-of-date

*   [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) e [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) vanno segnalati come out-of-date in base alla loro [versione *IcedTea*](http://icedtea.wildebeest.org/download/source) (es. `2.4.3`) e non in base alla loro versione Oracle (es. `u45`).
*   [icedtea-web-java7](https://www.archlinux.org/packages/?name=icedtea-web-java7) va segnalato come out-of-date in base alla [versione di *IcedTea Web*](http://icedtea.wildebeest.org/download/source) (es. `1.4.1`), che è completamente indipendente dalla versione di *IcedTea*.

### Oracle Java SE

[AUR](/index.php/AUR "AUR") contiene i pacchetti per l'implementazione Oracle di Java: si vedano i pacchetti [jre](https://aur.archlinux.org/packages/jre/) and [jdk](https://aur.archlinux.org/packages/jdk/).

#### Java SE 6/7

[AUR](/index.php/AUR "AUR") contiene i pacchetti per [jre6](https://aur.archlinux.org/packages/jre6/)/[jre7](https://aur.archlinux.org/packages/jre7/) e [jdk6](https://aur.archlinux.org/packages/jdk6/)/[jdk7](https://aur.archlinux.org/packages/jdk7/) che costituiscono rispettivamente l'implementazione di Oracle per Java SE 6 e Java SE 7.

#### JDK-compat

Il JDK Oracle (sia versione 6 che 7) può essere installato a fianco di un'altra installazione Java (ad esempio OpenJDK). I pacchetti sono disponibili in [AUR](/index.php/AUR "AUR"): [jdk6-compat](https://aur.archlinux.org/packages/jdk6-compat/) e [jdk7-compat](https://aur.archlinux.org/packages/jdk7-compat/).

### Oracle JRockit

[JRockit](https://en.wikipedia.org/wiki/JRockit "wikipedia:JRockit") è la versione JIT di Java fornita da Oracle ed è disponibile su AUR: [jrockit](https://aur.archlinux.org/packages/jrockit/).

### VMkit

[VMkit](http://vmkit.llvm.org/index.html) è un framework basato su LLVM per macchine virtuali JIT. J3 è una JVM eseguita su VMkit. J3 dipende dalle librerie GNU classpath, ma potrebbe anche funzionare con le librerie classpath di Apache. Per installare VMkit si faccia riferimento a questa pagina web: [VMKit - Getting Started](http://vmkit.llvm.org/get_started.html).

### Parrot VM

[Parrot VM](https://www.archlinux.org/packages/?q=parrot) offre uno sperimentale [supporto per Java](http://trac.parrot.org/parrot/wiki/Languages) attraverso due differenti metodi: o come [traduttore di bytecode della Java VM](http://code.google.com/p/parrot-jvm/), o come un [compilatore Java](https://github.com/chrisdolan/perk) avente come obiettivo la Parrot VM. È possibile installare Parrot VM attraverso [AUR](/index.php/AUR "AUR"): [parrot-git](https://aur.archlinux.org/packages/parrot-git/).

## Risoluzione problemi

### MySQL

A causa del fatto che i JDBC-drivers usano spesso la porta nell'URL per stabilire una connessione col database, quest'ultimo viene considerato "remoto" nonostante JDBC e MySQL possano essere in esecuzione sullo stesso host (ad esempio: MySQL non è in ascolto di connessioni "remote" con la sua configurazione di default). Quindi, per usare JDBC e MySQL, si dovrebbe abilitare l'accesso remoto a MySQL seguendo le istruzioni nella [pagina su MySQL](/index.php/MySQL#Enable_remote_access "MySQL") dell'ArchWiki.

### Audio applicazioni Java con Pulseaudio

**Nota:** Questa procedura è utile solo per versioni precedenti di Java (Java 6).

Di default Java e [Pulseaudio](/index.php/Pulseaudio "Pulseaudio") non convivono molto bene l'uno con l'altro, ma questo problema è facilmente risolvibile usando padsp.

(Questi percorsi sono corretti per Java della Sun, è necessario cambiarli per OpenJDK)

Per prima cosa, rinominare l'eseguibile `java` in `java.bin`

```
# mv /opt/java/jre/bin/java /opt/java/jre/bin/java.bin

```

Successivamente, creare un nuovo script di esecuzione in `/opt/java/jre/bin/java`

```
#!/bin/sh
padsp /opt/java/jre/bin/java.bin "$@"

```

Infine rendere lo script eseguibile

```
# chmod +x /opt/java/jre/bin/java

```

E' necessario ripetere questa procedura ad ogni aggiornamento di Java.

E' anche possibile provare a sostituire padsp con aoss, che può risolvere il problema anche in Alsa così come in Pulse: scegliere la soluzione che funziona meglio. E' necessario avvisare che questi hack qualche volta funzionano perfettamente ma a volte possono essere anche molto instabili.

### Usare un altro Window Manager

Usando [wmname](https://www.archlinux.org/packages/?name=wmname) da [suckless.org](http://tools.suckless.org/wmname) è possibile ingannare la JVM sul window manager in uso. Questo può risolvere dei problemi di visualizzazione delle Java GUI che si presentano con l'utilizzo di window manager come [Awesome](/index.php/Awesome "Awesome") o [Dwm](/index.php/Dwm "Dwm").

 `$ wmname LG3D` 

(È necessario riavviare l'applicazione in questione dopo aver eseguito il comando wmname.)

Questa soluzione è efficace in quanto la JVM contiene una lista "hard-coded" di window manager non-reparenting noti. Per il massimo dell'ironia, molti utenti preferiscono utilizzare con wmname il window manager non-reparenting [scritto da Sun](http://en.wikipedia.org/wiki/Project_Looking_Glass): `LG3D`.

### I font sono illeggibili

Nonostante l'applicazione dei consigli più in basso ([#Miglioramento del font rendering](#Miglioramento_del_font_rendering)), alcuni font potrebbero ancora non essere leggibili. In questo caso si può provare a installare [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) da AUR.

### Dipendenze mancanti

Installando Java da AUR, si può riscontrare una dipendenza mancante di *java-runtime*. In questo caso potrebbe essere necessario installare uno dei JDK citati in precedenza.

## Trucchi e consigli

**Nota:** I suggerimenti in questa sezione sono applicabili a tutte le applicazioni che usano un JRE esplicitamente installato (esterno all'applicazione). Alcune applicazioni vengono impacchettate con il proprio runtime o usano delle meccaniche proprie per l'interfaccia grafica, il rendering dei font, ecc. Quindi non è garantito che i suggerimenti funzionino sempre.

Il comportamento di molte applicazioni Java può essere controllato fornendo delle variabili predefinite al JRE. Da [questo post](https://bbs.archlinux.org/viewtopic.php?id=72892) del forum, si può vedere che un modo di fare questo consiste nell'aggiungere le seguenti linee nel proprio `~/.bashrc` (oppure in `/etc/profile.d/jre.sh` per avere influenza su tutti i programmi che non sono eseguiti utilizzando come source `~/.bashrc`, come ad esempio le applicazioni lanciate dalla *Vista Applicazioni* di GNOME):

```
export _JAVA_OPTIONS="-D**<option 1>** -D**<option 2>**..."

```

Ad esempio, per usare i font del sistema dotati di anti-aliasing e per far sì che swing usi il "look and feel" GTK si può usare:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'

```

### Miglioramento del font rendering

Sia l'implementazione closed-source, sia quella open-source di Java sono note avere un'implementazione impropria dell'antialiasing dei font. Questo può essere risolto attraverso le seguenti opzioni: `awt.useSystemAAFontSettings=on`, `swing.aatext=true`

Per maggiori informazioni si veda [Java Runtime Environment Fonts](/index.php/Java_Runtime_Environment_Fonts "Java Runtime Environment Fonts").

### GTK LookAndFeel

La grafica delle applicazioni che utilizzano Java potrebbe apparire sgradevole. In tal caso si potrebbe voler impostare diversamente il "look and feel" predefinito dei componenti swing: `swing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

Alcune applicazioni potrebbero ostinarsi ad usare il "look and feel" multipiattaforma chiamato Metal. In questi casi si può forzare l'applicazione ad usare il "look and feel" GTK con il seguente comando:`swing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

### Cambiare i symlinks

Tipicamente, l'installazione di OpenJDK genera dei symlinks in `/usr/bin` per java, javac... ecc. Se si vogliono cambiare questi symlinks (in seguito, ad esempio, all'installazione dell'implementazione Oracle), può essere d'aiuto [questo](https://github.com/d1x/linux-utils/blob/master/replace-java-symlinks.sh) script.