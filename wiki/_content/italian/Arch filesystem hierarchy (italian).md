Tratto dal sito di [FHS](http://www.pathname.com/fhs):

	"*Il filesystem standard è stato progettato per essere utilizzato dagli sviluppatori della distribuzione Unix, gli sviluppatori del pacchetto, e implementatori di sistema. Tuttavia, è principalmente destinato a essere un riferimento e non è un tutorial su come gestire un filesystem Unix o una gerarchia di directory.*"

Arch Linux è tra le molte distribuzioni che seguono il *f*ilesystem *h*ierarchy *s*tandard. Oltre a spiegare tutte le directory con le loro denominazioni, in questo articolo verranno illustrate anche le modifiche specifiche per Arch.

## Contents

*   [1 Distinzione tra i file condivisibili e non condivisibili](#Distinzione_tra_i_file_condivisibili_e_non_condivisibili)
*   [2 Il filesystem root](#Il_filesystem_root)
*   [3 /bin: Comandi binari indispensabili](#.2Fbin:_Comandi_binari_indispensabili)
*   [4 /boot: File statici del bootloader](#.2Fboot:_File_statici_del_bootloader)
*   [5 /dev: File dei dispositivi](#.2Fdev:_File_dei_dispositivi)
*   [6 /etc: Configurazioni specifiche host](#.2Fetc:_Configurazioni_specifiche_host)
    *   [6.1 /etc/conf.d](#.2Fetc.2Fconf.d)
    *   [6.2 /etc/rc.d](#.2Fetc.2Frc.d)
    *   [6.3 /etc/X11](#.2Fetc.2FX11)
        *   [6.3.1 /etc/X11/xinit](#.2Fetc.2FX11.2Fxinit)
        *   [6.3.2 /etc/X11/xinit/xinitrc](#.2Fetc.2FX11.2Fxinit.2Fxinitrc)
*   [7 /home: Directory utente](#.2Fhome:_Directory_utente)
*   [8 /lib: Librerie condivise essenziali e moduli del kernel](#.2Flib:_Librerie_condivise_essenziali_e_moduli_del_kernel)
*   [9 /lost+found: Dati recuperabili specifici del Filesystem](#.2Flost.2Bfound:_Dati_recuperabili_specifici_del_Filesystem)
*   [10 /media: Punti di montaggio per i supporti rimovibili](#.2Fmedia:_Punti_di_montaggio_per_i_supporti_rimovibili)
*   [11 /mnt: Punti di mount temporaneo](#.2Fmnt:_Punti_di_mount_temporaneo)
*   [12 /opt: Pacchetti problematici](#.2Fopt:_Pacchetti_problematici)
*   [13 /proc: Informazioni di elaborazione](#.2Fproc:_Informazioni_di_elaborazione)
*   [14 /root: Directory dell'amministratore](#.2Froot:_Directory_dell.27amministratore)
*   [15 /sbin: Binari di sistema](#.2Fsbin:_Binari_di_sistema)
*   [16 /srv: Servizio dati](#.2Fsrv:_Servizio_dati)
*   [17 /tmp: File temporanei](#.2Ftmp:_File_temporanei)
*   [18 /usr: Dati di sola lettura condivisibili](#.2Fusr:_Dati_di_sola_lettura_condivisibili)
    *   [18.1 /usr/bin: Binari](#.2Fusr.2Fbin:_Binari)
    *   [18.2 /usr/include: File di intestazione](#.2Fusr.2Finclude:_File_di_intestazione)
    *   [18.3 /usr/lib: Librerie](#.2Fusr.2Flib:_Librerie)
    *   [18.4 /usr/sbin: Binari di sistema](#.2Fusr.2Fsbin:_Binari_di_sistema)
    *   [18.5 /usr/share: Dati indipendenti dall'architettura](#.2Fusr.2Fshare:_Dati_indipendenti_dall.27architettura)
    *   [18.6 /usr/src: Codice sorgente](#.2Fusr.2Fsrc:_Codice_sorgente)
    *   [18.7 /usr/local: Gerarchia locale](#.2Fusr.2Flocal:_Gerarchia_locale)
*   [19 /var: File variabili](#.2Fvar:_File_variabili)
    *   [19.1 /var/abs](#.2Fvar.2Fabs)
    *   [19.2 /var/cache/pacman/pkg](#.2Fvar.2Fcache.2Fpacman.2Fpkg)
    *   [19.3 /var/lib: Informazioni di stato](#.2Fvar.2Flib:_Informazioni_di_stato)
    *   [19.4 /var/lock: Dati incondivisibili bloccati](#.2Fvar.2Flock:_Dati_incondivisibili_bloccati)
    *   [19.5 /var/log: File di log](#.2Fvar.2Flog:_File_di_log)
    *   [19.6 /var/mail: Posta utente](#.2Fvar.2Fmail:_Posta_utente)
    *   [19.7 /var/run: Informazioni di stato](#.2Fvar.2Frun:_Informazioni_di_stato)
    *   [19.8 /var/spool: Code](#.2Fvar.2Fspool:_Code)
        *   [19.8.1 /var/spool/mail](#.2Fvar.2Fspool.2Fmail)
    *   [19.9 /var/tmp: File temporanei conservabili](#.2Fvar.2Ftmp:_File_temporanei_conservabili)

## Distinzione tra i file condivisibili e non condivisibili

**Condivisibili** sono definiti quei file che possono essere memorizzati su un host e utilizzati su altri. **Non condivisibili** sono, come da definizione, quelli che non sono condivisibili. Ad esempio, i file nelle directory home sono condivisibili, considerando che i file di blocco del dispositivo non lo sono.

I file **statici** includono file binari, librerie, file di documentazione e altri non modificabili senza l'intervento dell'amministratore di sistema. Vengono definiti file **variabili**, tutti quei file che non sono statici.

## Il filesystem root

Il filesystem di root, rappresentato dal simbolo slash (**/**), è il filesystem principale da cui derivano tutti gli altri filesystem, il vertice della gerarchia. Tutti i file e le directory appaiono sotto la directory root "/", anche se sono memorizzati su dispositivi fisici differenti. Il contenuto del filesystem root deve essere adeguato per l'avvio, il ripristino, il recupero e/o la correzione del sistema.

## /bin: Comandi binari indispensabili

È l'ubicazione per tutti quei binari che devono essere disponibili in modalità singolo utente ed accessibili a tutti gli utenti (ad esempio cat, ls, cp). /bin/ fornisce programmi che devono essere disponibili anche se è montata solo la partizione contenente /. Questa situazione può verificarsi in caso si abbia necessità di riparare altre partizioni, ma non si abbia accesso alle directory condivise (ad esempio, si è in modalità singolo utente e quindi non si ha accesso alla rete). A differenza di /sbin, la directory /bin contiene diversi comandi utili, disponibili sia all'utente root che agli utenti normali.

## /boot: File statici del bootloader

È una directory statica, non condivisibile, contenente le immagini kernel e ramdisk, così come il file di configurazione del bootloader, e le varie fasi del bootloader stesso. /boot inoltre memorizza i dati che vengono utilizzati prima che il kernel inizi l'esecuzione dei programmi userspace. Ciò può includere settori di master boot salvati e file di tipo "sector-map".

## /dev: File dei dispositivi

I nodi dei dispositivi essenziali creati da udev durante il processo di avvio, così come l'hardware della macchina, vengono rilevati da "events". Questa directory mette in luce un aspetto importante del filesystem UNIX - tutto è un file o una directory. L'esplorazione di questa directory rivelerà molti file, ognuno dei quali rappresenta un componente hardware del sistema. La maggior parte dei dispositivi sono dispositivi "block" o "character", ma possono essere creati anche altri tipi di dispositivi. In generale, i "dispositivi a blocchi" sono dispositivi che memorizzano o detengono dati, mentre i "character devices" possono essere definiti come dispositivi che trasmettono o trasferiscono dati. Ad esempio, hard disk e unità ottiche sono classificati come dispositivi a blocchi, mentre le porte seriali, mouse e porte USB sono tutti dispositivi "character".

## /etc: Configurazioni specifiche host

Le specifiche host, file di configurazione non condivisibili, troveranno posto nella directory /etc. Se è necessario più di un file di configurazione per una determinata applicazione, è consuetudine utilizzare una sottodirectory, in modo da mantenere l'area del file /etc/ il più pulita possibile. È buona norma effettuare dei backup di questa directory con una certa frequenza, dal momento che contiene tutti i file di configurazione del sistema.

### /etc/conf.d

Alcuni script dei demoni avranno un corrispondente file di configurazione in questa directory che contiene alcuni utili valori di default. Quando viene avviato un demone, il primo luogo da dove attinge le impostazioni è dal suo file di configurazione all'interno di questa directory, e successivamente da /etc/rc.conf. L'approccio allo scripting di Arch è semplice e trasparente, e consente di centralizzare facilmente tutte le opzioni di configurazione dei demoni in /etc/rc.conf, semplicemente impostando un valore appropriato variabile o, suddividere la configurazione in più file, se si preferisce un approccio più decentrato a questo proposito.

### /etc/rc.d

Tutti i demoni Arch risiedono qui. Script personalizzati possono eventualmente essere aggiunti e invocati qui, nella stringa DAEMONS in /etc/rc.conf.

### /etc/X11

File di configurazione per il sistema X Window.

#### /etc/X11/xinit

File di configurazione xinit. "Xinit" è un metodo di configurazione per avviare una sessione X, progettato per essere utilizzato come parte di uno script.

#### /etc/X11/xinit/xinitrc

File xinitrc globale, utilizzato da tutte le sessioni di X iniziate da xinit (startx). Il suo utilizzo è deprecato a favore del file .xinitrc, presente nella directory home dell'utente.

## /home: Directory utente

UNIX è un ambiente multi-utente. Di conseguenza, ad ogni utente è assegnata anche una directory specifica che è accessibile solo a lui e all'utente root. Queste sono le home directory degli utenti, che si trovano sotto "/home/$USER" (~/). Nell'ambito delle propria home directory, l'utente può scrivere file, cancellarli, installare programmi, ecc. Le home directory degli utenti contengono i loro dati e file di configurazione personali, i cosiddetti "dot files" (il loro nome è preceduto da un punto), che sono "nascosti". Per visualizzare i file nascosti, attivare l'apposita opzione nel file manager o eseguire ls con l'opzione -a. Nell'eventualità di un conflitto tra file personali e file di configurazione di sistema, le impostazioni personali prevarranno. I file nascosti che saranno probabilmente più modificati dall'utente finale sono .xinitr e .bashrc, i file di configurazione per xinit e Bash, rispettivamente. Conferiscono all'utente la possibilità di cambiare il window manager da avviare al momento del login e gli alias, comandi specificati dall'utente e variabili d'ambiente, rispettivamente. Quando viene creato un nuovo utente, i dotfile personali possono venir copiati dalla directory /etc/skel, dove risiedono i file di esempio di sistema.

La directory /home può col passare del tempo, occupare molto spazio, in quanto viene generalmente utilizzata per immagazzinare i download, la compilazione, l'installazione e l'esecuzione di programmi, la posta, le collezioni di file multimediali, ecc.

## /lib: Librerie condivise essenziali e moduli del kernel

Contiene i moduli del kernel e le immagini delle librerie condivise essenziali (la libreria di programmazione del codice C) necessari per avviare il sistema ed eseguire i comandi sotto /bin/ e /sbin/. Le librerie sono raccolte di routines (sequenze di istruzioni) dei programmi di uso frequente e sono facilmente identificabili attraverso l'estensione dei loro file *.so. Sono essenziali per la funzionalità di base del sistema. I moduli del kernel (driver) sono nella sottodirectory /lib/modules/<kernel-version>.

## /lost+found: Dati recuperabili specifici del Filesystem

I sistemi operativi del tipo UNIX devono eseguire una corretta sequenza di arresto. A volte, un sistema può andare in crash, o una mancata alimentazione potrebbe spegnere brutalmente la macchina. In entrambi i casi, al seguente avvio, viene eseguito un controllo del filesystem utilizzando il programma *fsck*. *Fsck* analizzerà il sistema nel tentativo di recuperare eventuali file danneggiati. I risultati di questa operazione di recupero verranno ubicati in questa directory. I file recuperati non saranno necessariamente completi né perfettamente integri, ma è sempre una possibilità in più che qualche cosa di utile possa essere ripristinato.

## /media: Punti di montaggio per i supporti rimovibili

CDROM, DVD, e chiavette USB dispongono di un adeguato punto di mount in /media/. Il motivo per la creazione di questa directory è che storicamente ci sono state una serie di altri luoghi utilizzati per il montaggio di supporti rimovibili come /cdrom, /mnt o /mnt/cdrom. Posizionando il mount point di tutti i supporti rimovibili direttamente nella directory principale potrebbe portare ad un gran numero di ulteriori cartelle in /. Anche se l'uso delle sottodirectory in /mnt come punto di montaggio è stato recentemente molto diffuso, va in conflitto con la tradizione precedente di usare /mnt direttamente come punto di montaggio temporaneo. Pertanto, Arch alloca /media come punto di mount per i supporti rimovibili. Nei sistemi in cui esiste più di un dispositivo per il montaggio di un certo tipo di media, le directory di montaggio vengono create aggiungendo un numero al nome di quelle disponibili in precedenza a partire da "0", anche se il nome non determinato deve tuttavia esistere.

Il demone "hal" (Hardware Abstraction Layer) monta i supporti rimovibili in /media come /media/<name_of_removable_filesystem>

## /mnt: Punti di mount temporaneo

Questo è un punto di mount generico per i filesystem temporanei o dispositivi. Il montaggio è il processo di creazione di un filesystem a disposizione del sistema. Dopo il montaggio, i file saranno accessibili sotto il punto di mount. Ulteriori mount point (sottodirectory) possono essere creati sotto /mnt/. Non ci sono limiti alla creazione di un punto di mount in qualsiasi parte del sistema, ma per convenzione e per praticità, disseminare un filesystem con punti di montaggio vari, dovrebbe essere una pratica da evitare.

## /opt: Pacchetti problematici

I pacchetti e i file statici di grandi dimensioni che non rientrano perfettamente nel layout del filesystem possono essere collocati in /opt. Un pacchetto che posiziona i file nella directory /opt/ crea una directory che presenta lo stesso nome del pacchetto. Questa directory, a sua volta contiene i file che altrimenti sarebbero sparsi in tutto il file system. Per esempio, il pacchetto Acrobat contiene le cartelle di Browser, Reader e Resource, ubicate allo stesso livello della directory bin. Questo non rientra in una normale struttura di un filesystem GNU Linux, così Arch sistema tutti i file in una sottodirectory di /opt.

## /proc: Informazioni di elaborazione

La directory /proc è molto particolare in quanto è anche un filesystem virtuale. A volte è denominata *process information pseudo-file system*. Non contiene file "reali", ma piuttosto, le informazioni del sistema runtime (ad esempio la memoria di sistema, i dispositivi montati, la configurazione hardware, ecc). Per questa ragione può essere considerata come un centro di controllo e di informazione per il kernel. In realtà, un sacco di utilità di sistema vengono richiamate semplicemente ai file in questa directory. Per esempio, "lsmod" è lo stesso di "cat/proc/modules" mentre "lspci" è sinonimo di "cat/proc/pci". Alterando i file che si trovano in questa directory, i parametri del kernel possono essere letti e/o modificati (sysctl) mentre il sistema è in esecuzione.

L'aspetto più distintivo dei file in questa directory è il fatto che tutti hanno una dimensione pari a 0, ad eccezione di **kcore, mounts** e **self**.

## /root: Directory dell'amministratore

È la home directory dell'amministratore di sistema, "root". Questo può risultare un po' confuso ("/root sotto root"), ma come da tradizione, "/" era la home directory di root (da qui il nome dell'account di amministratore). Per mantenere le cose più ordinate, "root" alla fine ha ottenuto la propria directory home. Ma perché non in "/home"? Perché "/home" è spesso situata in una partizione diversa o addirittura su un altro sistema e sarebbe quindi inaccessibile a "root" quando (per ovvi motivi), solo "/" è montata.

## /sbin: Binari di sistema

UNIX discrimina tra gli eseguibili "normali" e quelli utilizzati per la manutenzione del sistema e/o per i compiti amministrativi. I secondi risiedono qui o, quelli meno importanti, in /usr/sbin. I programmi eseguiti dopo /usr (quando non ci sono problemi) sono generalmente messi in /usr/sbin. Questa directory contiene i file binari che sono essenziali per il funzionamento del sistema. Questi includono l'amministrazione di sistema, nonché programmi di manutenzione e configurazione hardware. [GRUB](/index.php/GRUB "GRUB") (il comando), fdisk, init, route, ifconfig, ecc., sono ubicati tutti qui.

## /srv: Servizio dati

Sito di dati specifici in servizio al sistema. Lo scopo principale è che così gli utenti possono trovare il percorso dei file dati per un particolare servizio, e in modo che i servizi che richiedono un singolo albero per i dati di sola lettura, dati scrivibili e script (come gli script CGI), possono essere ubicati razionalmente. I dati di interesse per un utente specifico saranno ubicati nella home directory dell'utente.

## /tmp: File temporanei

Questa directory contiene file che sono necessari solo temporaneamente. Molti programmi la utilizzano per creare file di blocco e per l'archiviazione temporanea di dati. Non rimuovere i file da questa directory se non si sa esattamente cosa si sta facendo! Molti di questi file sono importanti per i programmi in esecuzione e la loro eliminazione può causare un crash del sistema. Su molti sistemi, questa directory viene ripulita durante l'avvio o l'arresto da parte del sistema locale. La base di questa particolare funzionalità risale alle tradizioni Unix, ed è una pratica comune.

## /usr: Dati di sola lettura condivisibili

Mentre root è il filesystem primario, /usr è la gerarchia secondaria per i dati utente, contenente la maggior parte delle (multi) utility e applicazioni dell'utente. /Usr è condivisibile, in sola lettura dati. Questo significa che /usr è condivisibile tra host diversi e non deve avere permessi di scrittura, tranne nel caso di intervento dell'amministratore di sistema (installazione, aggiornamento, avanzamento). Tutte le informazioni che sono specifiche del computer ospite o varia con il tempo sono memorizzate altrove.

Oltre a /home/, /usr/ contiene in genere la quota maggiore di dati su un sistema. Quindi, questa è una delle directory più importanti del sistema, in quanto contiene tutti i file binari degli utenti, la loro documentazione, librerie, file di intestazione, ecc. X, e relative librerie di supporto, può essere trovato qui. I programmi utente come telnet, ftp, ecc, sono anch'essi posizionati qui. Nelle implementazioni UNIX originali, /usr/ (per *utente*), era il luogo dove le home directory degli utenti del sistema venivano messe (vale a dire, /usr/ *nomeutente* è stata poi la directory ora nota come /home/ *nomeutente*). Nel corso del tempo, /usr/ è diventato il luogo in cui i programmi userspace e i dati (in contrapposizione ai programmi e dati "kernelspace") risiedono. Il nome non è cambiato, ma il suo significato si è ristretto e allungato da *tutto ciò che è correlato all'utente* a *dati utente e programmi utilizzabili*. Come tale, venne creato l'acronimo "**U**ser **S**ystem **R**esources".

### /usr/bin: Binari

Comandi binari non essenziali (non necessari in modalità utente singolo), per tutti gli utenti. Questa directory contiene la grande maggioranza dei file binari (applicazioni) del sistema. Gli eseguibili in questa directory variano notevolmente. Ad esempio vi, gcc e gnome-session risiedono qui.

### /usr/include: File di intestazione

Header file necessari per la compilazione del codice sorgente userspace.

### /usr/lib: Librerie

Librerie per i binari in /usr/bin/ e /usr/sbin/.

### /usr/sbin: Binari di sistema

Binari di sistema non essenziali utilizzati dall'amministratore di sistema. È qui che risiedono i demoni di rete del sistema, insieme ad altri binari ai quali (in generale) solo l'amministratore di sistema ha accesso, ma che non sono necessari per la manutenzione del sistema e la sua riparazione. Normalmente, queste directory non fanno parte dei percorsi dell'utente normale, ma solo di quelli di root (PATH è una variabile d'ambiente che controlla la sequenza di posizioni alle quali il sistema cerca di puntare per i comandi).

### /usr/share: Dati indipendenti dall'architettura

Questa directory contiene file indipendenti dall'architettura e "condivisibili", (documenti, icone, font, ecc.) Si noti, tuttavia, che "/usr/share" non è generalmente destinata ad essere condivisa da sistemi operativi diversi o da diversi rilasci del sistema in uso. Qualsiasi programma o pacchetto che contenga o richieda dati che non devono essere modificati devono conservare questi dati in "/usr/share/" (o "/usr/local/share/", se installato manualmente vedere più sotto). Si raccomanda di utilizzare una sottodirectory in /usr/share a questo scopo.

### /usr/src: Codice sorgente

La sotto-directory "linux" contiene i sorgenti del kernel Linux e degli header-files.

### /usr/local: Gerarchia locale

Gerarchia terziaria opzionale per i dati locali. L'idea originale alla base di "/usr/local" era di avere una directory "/usr/" separata (locale) su ogni macchina oltre a "/usr/", che potesse essere montata in sola lettura da un altro luogo. Copia la struttura di "/usr/". Attualmente, "/usr/local/" è ampiamente considerato come un buon posto in cui mantenere il materiale auto-compilato o programmi di terze parti. Questa directory è vuota di default su Arch Linux. Può inoltre essere utilizzata per installazioni di software compilato manualmente se lo si desidera. [pacman](/index.php/Pacman "Pacman") installa in /usr/, quindi il software compilato manualmente e installato in /usr/local/ può tranquillamente coesistere con il software di sistema di pacman.

## /var: File variabili

File variabili, come i log, file di spool, e file temporanei e-mail. In Arch, l'albero [ABS](/index.php/ABS "ABS") e la cache di pacman risiedono qui. Perché non mettere dati variabili e transitori in /usr/? Perché ci possono essere circostanze in cui /usr/ è montato in sola lettura, ad esempio se è su un CD o su un altro computer. "/var/" contiene dati variabili, vale a dire i file e le directory che il sistema deve essere in grado di scrivere durante il funzionamento, mentre /usr/ contiene solo dati statici. Alcune directory possono essere messe su partizioni o sistemi separati, ad esempio, per facilitare i backup, a causa della topologia di rete o problemi di sicurezza. Altre directory devono essere presenti nella partizione di root, in quanto sono di vitale importanza per il processo di avvio. Le directory "montabili" sono: "/home", "/mnt", "/tmp", "/usr" e "/var". Essenziali per l'avvio sono: "/bin", "/boot", "/dev", "/etc", "/lib", "/proc" e "/sbin".

### /var/abs

L'albero [ABS](/index.php/ABS "ABS"). Una gerarchia per il sistema di compilazione dei pacchetti stile "ports-like", contenente gli script di compilazione all'interno di sottodirectory corrispondenti a tutti i software installabili Arch.

### /var/cache/pacman/pkg

La cache dei pacchetti di pacman.

### /var/lib: Informazioni di stato

Dati persistenti modificati dai programmi durante l'esecuzione (ad esempio database, sistema di impacchettamento dei metadati, ecc).

### /var/lock: Dati incondivisibili bloccati

File che mantengono la traccia delle risorse attualmente in uso.

### /var/log: File di log

File di log del sistema.

### /var/mail: Posta utente

Directory condivisibile per le mailbox degli utenti.

### /var/run: Informazioni di stato

Dati non condivisibili sul sistema operativo dall'ultimo boot (ad esempio gli utenti attualmente registrati e i demoni in esecuzione).

### /var/spool: Code

Spool per le attività in attesa di essere elaborate (ad esempio le code di stampa e la posta non letta).

#### /var/spool/mail

Posizione sconsigliata per le mailbox degli utenti.

### /var/tmp: File temporanei conservabili

File temporanei da conservare tra i riavvii.