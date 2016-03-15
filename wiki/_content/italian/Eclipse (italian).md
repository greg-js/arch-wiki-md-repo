[Eclipse](http://eclipse.org) è un progetto open source basato su una community, con l'obiettivo di fornire una piattaforma di sviluppo universale. Il progetto Eclipse è conosciuto soprattutto per il suo ambiente di sviluppo integrato (IDE) e multipiattaforma. I pacchetti per Arch Linux (e questa guida) si riferiscono specificamente all'ambiente di sviluppo.

L'IDE di Eclipse è scritto per la maggior parte in Java ma può essere usato per sviluppare applicazioni in molti altri linguaggi, tra cui Java, C/C++, PHP e Perl. L'IDE fornisce anche supporto per la sottoversione SVN (vedere sotto) e la gestione dei processi (per questo scopo usa la sua TOTO list integrata o il pacchetto aggiuntivo eclipse-mylyn).

## Contents

*   [1 Installazione](#Installazione)
*   [2 Plugins](#Plugins)
    *   [2.1 Supporto C/C++](#Supporto_C.2FC.2B.2B)
        *   [2.1.1 Eclipse CDT](#Eclipse_CDT)
    *   [2.2 Supporto Perl](#Supporto_Perl)
        *   [2.2.1 EPIC](#EPIC)
    *   [2.3 Supporto PHP](#Supporto_PHP)
        *   [2.3.1 Eclipse PDT](#Eclipse_PDT)
        *   [2.3.2 PHPEclipse](#PHPEclipse)
        *   [2.3.3 Aptana PHP](#Aptana_PHP)
    *   [2.4 Supporto Python](#Supporto_Python)
        *   [2.4.1 PyDev](#PyDev)
    *   [2.5 Web development (HTML, CSS, JavaScript...)](#Web_development_.28HTML.2C_CSS.2C_JavaScript....29)
        *   [2.5.1 Aptana Studio](#Aptana_Studio)
    *   [2.6 Supporto SVN](#Supporto_SVN)
        *   [2.6.1 Subclipse](#Subclipse)
        *   [2.6.2 Eclipse Subversive](#Eclipse_Subversive)
    *   [2.7 Supporto Git](#Supporto_Git)
        *   [2.7.1 EGit](#EGit)
*   [3 Aggiornamenti](#Aggiornamenti)
*   [4 Abilitare l'integrazione di javadoc](#Abilitare_l.27integrazione_di_javadoc)
    *   [4.1 Versione online](#Versione_online)
    *   [4.2 Versione offline](#Versione_offline)
*   [5 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [5.1 Crash di autocompletamento e javadoc render](#Crash_di_autocompletamento_e_javadoc_render)
    *   [5.2 Crash al primo avvio o scegliendo "Help -> Welcome"](#Crash_al_primo_avvio_o_scegliendo_.22Help_-.3E_Welcome.22)

## Installazione

È molto facile installare Eclipse SDK in Arch Linux:

```
# pacman -S eclipse

```

Questo pacchetto di base supporta già lo sviluppo di applicazioni Java.

## Plugins

Ci sono due modi di installare un plugin per Eclipse:

*   usando [pacman](/index.php/Pacman "Pacman") per installare i plugin presenti nei repository di Arch (vedere [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") per ulteriori informazioni);
*   usando il plugin manager di Eclipse per scaricare e installare plugin dai repository originali; in questo caso è necessario trovare i repository necessari dal sito dei plugin, quindi su Eclipse selezionare *Help -> Install New Software...*, compilare il campo *Work with* con il repository, selezionare il plugin da installare nella lista e seguire le istruzioni.

**Attenzione:**

*   Installando con il plugin manager, è consigliato eseguire Eclipse come root: in questo modo i plugin saranno installati in `/usr/share/eclipse/plugins/`; installando come utente normale verranno memorizzati nella cartella `~/.eclipse/` e non verranno più riconosciuti dopo un eventuale aggiornamento di Eclipse.
*   Si raccomanda comunque di non utlizzare Eclipse come root per l'uso normale.

### Supporto C/C++

#### Eclipse CDT

*   Homepage del progetto: [http://www.eclipse.org/cdt/](http://www.eclipse.org/cdt/)
*   Disponibile in [extra]: [eclipse-cdt](https://www.archlinux.org/packages/?name=eclipse-cdt)

### Supporto Perl

#### EPIC

*   Homepage del progetto: [http://www.epic-ide.org/](http://www.epic-ide.org/)
*   Disponibile in [AUR](/index.php/AUR "AUR"): [eclipse-epic](https://aur.archlinux.org/packages/eclipse-epic/)

### Supporto [PHP](/index.php/PHP "PHP")

#### Eclipse PDT

*   Homepage del progetto: [http://www.eclipse.org/pdt/](http://www.eclipse.org/pdt/)
*   Disponibile in [AUR](/index.php/AUR "AUR"): [eclipse-pdt](https://aur.archlinux.org/packages/eclipse-pdt/)

#### PHPEclipse

*   Homepage del progetto: [http://www.phpeclipse.com/](http://www.phpeclipse.com/)
*   Disponibile in [community]: [eclipse-phpeclipse](https://aur.archlinux.org/packages/eclipse-phpeclipse/)

#### Aptana PHP

Vedere Aptana Studio più avanti nella pagina.

### Supporto [Python](/index.php/Python "Python")

#### PyDev

*   Homepage del progetto: [http://pydev.org/](http://pydev.org/)
*   Disponibile in [AUR](/index.php/AUR "AUR"): [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

### Web development (HTML, CSS, JavaScript...)

#### Aptana Studio

*   Homepage del progetto: [http://www.aptana.org/](http://www.aptana.org/)
*   Per il plugin di Eclipse, utilizzare il plugin manager
*   Per la versione indipendente, il pacchetto è disponibile in [AUR](/index.php/AUR "AUR"): [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

### Supporto SVN

#### Subclipse

*   homepage del progetto: [http://subclipse.tigris.org/](http://subclipse.tigris.org/)
*   Disponibile in [community]: [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)
*   [Come utilizzare la SVN con Eclipse](http://www-128.ibm.com/developerworks/opensource/library/os-ecl-subversion/)

#### Eclipse Subversive

*   Homepage del progetto: [http://www.eclipse.org/subversive/](http://www.eclipse.org/subversive/)
*   Disponibile in [AUR](/index.php/AUR "AUR"): [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

### Supporto [Git](/index.php/Git "Git")

#### EGit

*   Homepage del progetto: [http://www.eclipse.org/egit/](http://www.eclipse.org/egit/)
*   Disponibile in [AUR](/index.php/AUR "AUR"): [egit](https://aur.archlinux.org/packages/egit/)

## Aggiornamenti

*   Eclipse e i plugin installati con pacman vengono aggiornati con pacman stesso
*   Per i plugin installati con il plugin manager di Eclipse, è necessario avviare Eclipse e selezionare *Help -> Check for Updates* (se i plugin sono stati installati come root, anche l'aggiornamento deve essere controllato e installato come root).

Perché i plugin siano aggiornati, occorre controllare di avere abilitato i repository in *Window -> Preferences -> Install/Update -> Available Software Sites*: i repository dei plugin si trovano sui siti di riferimento dei rispettivi progetti. Per aggiungere, modificare e rimuovere i repository è sufficiente utilizzare i pulsanti a destra del pannello *Available Software Sites*. Per Eclipse 3.7 (Indigo), assicurarsi di aver abilitato questa repository:

```
[http://download.eclipse.org/releases/indigo](http://download.eclipse.org/releases/indigo)

```

Per ricevere notifiche di aggiornamento, andare su *Window -> Preferences -> Install/Update -> Automatic Updates*. Se si vogliono ricevere le notifiche anche per i plugin installati come root, bisogna esportare la lista dei relativi repository con *Export*, quindi reimportarla utilizzando *Import* come utente normale.

## Abilitare l'integrazione di javadoc

### Versione online

Se la propria macchina è costantemente connessa a Internet, si può utilizzare la documentazione online fornita da Sun. Per fare ciò:

1.  Andare su Window/Preferences, quindi scegliere Java/Installed JREs.
2.  Ce ne dovrebbe essere uno chiamato "java" con il tipo "Standard VM". Selezionarlo e scegliere Edit.
3.  Selezionare l'elemento `/opt/java/jre/lib/rt.jar` sotto "JRE system libraries:", quindi scegliere "Javadoc Location...".
4.  Compilare il campo "Javadoc location path:" con "[http://java.sun.com/javase/6/docs/api/](http://java.sun.com/javase/6/docs/api/)".

### Versione offline

Se non si vuole utilizzare la documentazione online la si può memorizzare localmente.

1.  Scaricare "Java SE 6 Documentation" dal sito [http://java.sun.com/javase/downloads/index.jsp](http://java.sun.com/javase/downloads/index.jsp)
2.  Seguire le istruzioni per il download del file "jdk-6-doc.zip".
3.  Andare su Window/Preferences, quindi scegliere Java/Installed JREs.
4.  Ce ne dovrebbe essere uno chiamato "java" con il tipo "Standard VM". Selezionarlo e scegliere Edit.
5.  Selezionare l'elemento `/opt/java/jre/lib/rt.jar` sotto a "JRE system libraries:", quindi scegliere "Javadoc Location...".
6.  Selezionare la voce "Javadoc in archive"
7.  Compilare il campo "Archive path:" con il percorso del file scaricato precedentemente.

## Risoluzione dei problemi

### Crash di autocompletamento e javadoc render

Per qualche motivo, libxul potrebbe crashare. Per ovviare al problema, si può provare ad installare [libwebkit](https://www.archlinux.org/packages/?name=libwebkit) e aggiungere le seguenti linee al proprio file `/usr/share/eclipse/eclipse.ini`:

```
-Dorg.eclipse.swt.browser.UseWebKitGTK=true

```

Se questo non funziona (o non si desidera utilizzare libwebkit) si può tentare un'altra soluzione:

	1\. Scaricare [http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/1.9.0.11/runtimes/xulrunner-1.9.0.11.en-US.linux-i686.tar.bz2](http://releases.mozilla.org/pub/mozilla.org/xulrunner/releases/1.9.0.11/runtimes/xulrunner-1.9.0.11.en-US.linux-i686.tar.bz2)

	2\. Decomprimerlo in /home/<Username>/.xulrunner (o in un'altra destinazione a piacere)

	3\. Aggiungere questa linea al file di configurazione di Eclipse `/usr/share/eclipse/eclipse.ini`:

```
-Dorg.eclipse.swt.browser.XULRunnerPath=/home/<Username>/.xulrunner

```

	A questo punto il prroblema dovrebbe essere risolto.

### Crash al primo avvio o scegliendo "Help -> Welcome"

Seguire le istruzioni sopra.