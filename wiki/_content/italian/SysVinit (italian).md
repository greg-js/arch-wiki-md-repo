**Attenzione:** Sysvinit è obsoleto su Arch Linux ed è stato tolto dai [repositorier ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)"). È necessario [migrare a systemd](#Migrare_a_Systemd).

Nei sistemi basati su Sysvinit *init* è il primo processo che viene eseguito una volta che il kernel Linux è stato caricato. Il programma di init del kernel è `/sbin/init` ed è fornito dal pacchetto [sysvinit](https://aur.archlinux.org/packages/sysvinit/) o [systemd-sysvcompact](https://www.archlinux.org/packages/?name=systemd-sysvcompact) (di default sulle nuove installazioni, vedere [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)")). La parola *init* in questo articolo si riferirà a sysvinit.

*inittab* è il file di configurazione dell'avvio per init e si trova in `/etc`. Esso contiene le cartelle per `init` o quali programmi o script eseguire quando si entra in uno specifico runlervel.

Quando Arch usava `init`, la maggior parte del lavoro veniva delegato ai [principali script di boot](#Principali_Script_di_Boot). Questo articolo tratterà principalmente init ed inittab.

## Contents

*   [1 Migrare a Systemd](#Migrare_a_Systemd)
    *   [1.1 Considerazioni prima di passare a systemd](#Considerazioni_prima_di_passare_a_systemd)
    *   [1.2 Procedura di installazione](#Procedura_di_installazione)
    *   [1.3 Informazioni supplementari](#Informazioni_supplementari)
*   [2 Panoramica di init e inittab](#Panoramica_di_init_e_inittab)
*   [3 Installation](#Installation)
*   [4 Cambiare runlevel](#Cambiare_runlevel)
    *   [4.1 Attraverso il Boot Loader](#Attraverso_il_Boot_Loader)
    *   [4.2 Dopo il boot](#Dopo_il_boot)
*   [5 inittab](#inittab)
    *   [5.1 Default Runlevel](#Default_Runlevel)
    *   [5.2 Principali Script di Boot](#Principali_Script_di_Boot)
    *   [5.3 Avvio in Single User](#Avvio_in_Single_User)
    *   [5.4 Gettys e Login](#Gettys_e_Login)
    *   [5.5 Ctrl-Alt-Del](#Ctrl-Alt-Del)
    *   [5.6 Programmi X](#Programmi_X)
    *   [5.7 Script Power-Sensing](#Script_Power-Sensing)
    *   [5.8 Combinazioni di tasti personalizzati](#Combinazioni_di_tasti_personalizzati)
        *   [5.8.1 Sollevare una kbrequest](#Sollevare_una_kbrequest)
*   [6 Vedere Anche](#Vedere_Anche)
*   [7 Link Esterni](#Link_Esterni)

## Migrare a Systemd

**Note:**

*   [systemd](https://www.archlinux.org/packages/?name=systemd) and [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) are both installed by default on installation media newer than [2012-10-13](https://www.archlinux.org/news/systemd-is-now-the-default-on-new-installations/). This section is aimed at Arch Linux installations that still rely on *sysvinit* and *initscripts*.
*   If you are running Arch Linux inside a VPS, please see [Virtual Private Server#Moving your VPS from initscripts to systemd](/index.php/Virtual_Private_Server#Moving_your_VPS_from_initscripts_to_systemd "Virtual Private Server").

### Considerazioni prima di passare a systemd

*   [Documentarsi](http://freedesktop.org/wiki/Software/systemd/) su systemd.
*   Notare che systemd possiede un sistema **journal** che rimpiazza **syslog**, tuttavia i due possono coesistere. Vedi [la sezione relativa al journal](#Il_Journal) più sotto.
*   Anche se systemd può rimpiazzare le funzionalità di **cron**, **acpid**, o **xinetd**, non c'è nessun bisogno di abbandonare l'uso dei demoni tradizionali a meno con non lo si voglia.
*   Gli scripts interattivi non funzionano in systemd. In particolare, **netcfg-menu** non può essere usato all'avvio del sistema ([FS#31377](https://bugs.archlinux.org/task/31377)).

### Procedura di installazione

1.  [Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") [systemd](https://www.archlinux.org/packages/?name=systemd) dai [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").
2.  Aggiungere il seguente comando ai [parametri del kernel](/index.php/Kernel_line "Kernel line") nel bootloader: `init=/usr/lib/systemd/systemd`
3.  Una volta fatto è possibile abilitare qualsiasi servizio si desideri per mezzo di `systemctl enable <service_name>` (pari a ciò che si trova nella sezione `DAEMONS`. Nuovi nomi possono essere trovati [qui](/index.php/Daemons_List "Daemons List"). ).
4.  Riavviare il proprio sistema e verificare che *systemd* sia attivo utilizzando il seguente comando: `cat /proc/1/comm`. Questo dovrebbe rispondere con la stringa `systemd`.
5.  Assicurarsi che il proprio hostname sia configurato correttamente in systemd: `hostnamectl set-hostname myhostname`.
6.  Procedere rimuovendo *initscripts* e *sysvinit* dal sistema e installando [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat).
7.  A scelta, rimuovere il parametro `init=/usr/lib/systemd/systemd` in quanto non è più necessario. [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat) lo imposta come default.

### Informazioni supplementari

*   Se si utilizza `quiet` nei parametri del kernel, è possibile rimuoverlo durante i primi avvii di systemd per identificare eventuali problemi durante il boot.
*   Aggiungere il vostro utente ai [gruppi](/index.php/Users_and_groups_(Italiano) "Users and groups (Italiano)") (`sys`, `disk`, `lp`, `network`, `video`, `audio`, `optical`, `storage`, `scanner`, `power`, etc.) **non** è necessario per la maggior parte dei casi di uso comune con systemd. I gruppi possono anche causare alcuni malfunzionamenti. Ad esempio, il gruppo `audio` si romperà al cambio rapido di utente e permette di bloccare le applicazioni software di mixaggio. Ogni login di PAM prevede una sessione logind , che per una sessione locale vi darà i permessi tramite le [POSIX ACLs](https://en.wikipedia.org/wiki/Access_control_list "wikipedia:Access control list") sui dispositivi audio/video, e consentirà alcune operazioni come il montaggio di memorizzazione rimovibile tramite [udisks](/index.php/Udisks "Udisks")
*   Si veda l'articolo [Configurazione della Rete](/index.php/Configurazione_della_Rete "Configurazione della Rete") per come impostare i target per la connessione di rete.

## Panoramica di init e inittab

`init` è sempre il processo con PID 1 ed all'infuori della gestione dell'area di swap, è il processo genitore per **tutti** gli altri processi. Può essere notato meglio il ruolo che svolge init nella gerarchia dei processi del proprio sistema usando il comando `pstree`:

 `$ pstree -Ap` 
```
init(1)-+-acpid(3432)
        |-crond(3423)
        |-dbus-daemon(3469)
        |-gpm(3485)
        |-mylogin(3536)
        |-ngetty(3535)---login(3954)---zsh(4043)---pstree(4326)
        |-polkitd(4033)---{polkitd}(4035)
        |-syslog-ng(3413)---syslog-ng(3414)
        `-udevd(643)-+-udevd(3194)
                     `-udevd(3218)

```

Oltre alle comuni inizializzazioni di sistema (come suggerisce il nome), `init` si occupa del riavvio, dello spegnimento e del avvio in recovery mode (single-user-mode). Per supportare tutto questo il file `inittab` raggruppa queste modalità in diversi **runlevel**. I runlevel usati da Arch sono 0 per lo spegnimento, 1 (oppure S che è un suo alias) per il single-user-mode, 3 per il normale boot (multi-user-mode), 5 per [X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") e 6 per il riavvio. Altre distribuzioni possono adottare altre convenzioni, ma l'uso dei runlevel 0, 1 e 6 è universale.

Al momento dell'esecuzione, `init` scansiona `inittab` ed effettua le appropriate azioni. Una voce di `inittab` ha questa forma:

```
id:runlevels:action:process

```

Dove `id` è un identificatore univoco per la voce (solo un nome, non influisce su init), e `runlevels` è una stringa (non delimitata) di runlevel. Se il runlevel in cui entra `init` compare in `runlevels`, allora `action` verrà svolta, eseguendo `process`. Alcune `action` speciali potrebbero portare `init` ad ignorare `runlevels` ed adottare un corrispondente metodo. Maggiori spiegazioni seguono nella sezione successiva.

## Installation

## Cambiare runlevel

### Attraverso il Boot Loader

Per cambiare il runlevel tramite la configurazione del proprio boot loader semplicemente aggiungere sulla stessa riga del kernel il numero del runlevel desiderato `n`. Un'applicazione comune di questo metodo è [Far partire X al boot#inittab](/index.php/Far_partire_X_al_boot#inittab "Far partire X al boot"). Per avviare sul runlevel desiderato aggiungere il relativo numero ai [parametri del kernel](/index.php/Kernel_parameters "Kernel parameters") (es `3` per il runlevel 3).

Se si usa un altro programma di init (ad esempio [systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)")), aggiungere **init=/bin/systemd** o qualcosa di simile alla riga del kernel.

**Nota:** Se si utilizza un init diverso da sysvinit, il parametro runlevel potrebbe essere ignorato.

### Dopo il boot

Dopo che il sistema è stato avviato, è possibile invocare `telinit n` per dire ad `init` di cambiare il runlevel ad `**n**`. `init` quindi leggerà `inittab` e "confronterà" il runlevel `**n**` con quello attuale - effettuando il kill dei processi non presenti nel nuovo runlevel e svolgendo le azioni non presenti nel vecchio runlevel. I processi presenti in entrambi i runlevel rimarranno invariati. La procedura di kill dei processi attualmente è un poco complessa; per maggiori informazioni e dettagli tecnici consultare la pagina di manuale di init.

`init` non riesaminerà `inittab`. Sarà necessario invocare `telinit` esplicitamente per applicare le modifiche apportate ad `inittab`. Il comando `telinit q` farà si che `init` riesamini `inittab` ma non cambierà runlevel.

## inittab

In questa sezione saranno esaminate le voci comuni di `inittab`, nel solito ordine in cui appaiono nel file di default usato da Arch. Successivamente verranno fatti alcuni esempi per aiutare a creare le proprie voci di `inittab`.

**Attenzione:** Testare sempre il file `/etc/inittab` modificato usando il comando `telinit q` prima di effettuare un riavvio, oppure eventuali errori di sintassi potrebbero impedire l'avvio del sistema.

### Default Runlevel

Il runlevel di default è il numero 3\. De commentare o aggiungere questo se si preferisce avviare il sistema nel runlevel 5 (che è comunemente usato per avviare X) come default:

```
id:5:initdefault:

```

### Principali Script di Boot

Questi sono gli script di init principali di Arch.

```
rc::sysinit:/etc/rc.sysinit
rs:S1:wait:/etc/rc.single
rm:2345:wait:/etc/rc.multi
rh:06:wait:/etc/rc.shutdown

```

### Avvio in Single User

A volte il kernel può fallire ad avviarsi, a causa di un file system corrotto o di un disco rotto, file chiave mancanti eccetera. In questo caso la propria immagine di init può automaticamente entrare in **single-user mode** che permette di effettuare il login come root ed usa `/sbin/sulogin` invece di `/sbin/login` per controllare il processo di login. Si può entrare in single-user mode aggiungendo la lettera `S` alla linea di comando del kernel nella configurazione di [GRUB Legacy](/index.php/GRUB_Legacy_(Italiano) "GRUB Legacy (Italiano)"), [GRUB2](/index.php/GRUB2_(Italiano) "GRUB2 (Italiano)") [LILO](/index.php/LILO "LILO"), o [syslinux](/index.php/Syslinux "Syslinux"). Se si vuole eseguire qualcosa di diverso da `sulogin`, specificarlo in questa voce.

```
su:S:wait:/sbin/sulogin -p

```

### Gettys e Login

Queste sono le voci fondamentali, esse eseguono le [getty](/index.php/Getty "Getty") nei terminali. Molte configurazioni di default avranno le getty eseguite sulle `ttys1-6` che effettueranno la visualizzazione della richiesta di login. Vedere anche `openvt, chvt, stty` ed `ioctl`

```
c1:234:respawn:/sbin/agetty 9600 tty1 xterm-color
c5:5:respawn:/sbin/agetty 57600 tty2 xterm-256color

```

### Ctrl-Alt-Del

Quando viene premuta la sequenza di tasti speciali `Ctrl+Alt+Del`, questa voce determina l'azione che verrà eseguita.

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

```

### Programmi X

Se non si è interessati al debug, è possibile avviare ogni tipo di applicazione tramite `inittab`. Un programma utile da avviare è il login manager desiderato quando si entra nel runlevel 5, multi-user-x-mode. Nel seguente esempio si può vedere come avviare [slim](/index.php/SLiM_(Italiano) "SLiM (Italiano)") entrando nel runlevel 5.

```
x:5:respawn:/usr/bin/slim >/dev/null 2>&1
#x:5:respawn:/usr/bin/xdm -nodaemon -confi /etc/X11/xdm/archlinux/xdm-config

```

### Script Power-Sensing

`Init` può comunicare con gli UPS (gruppi di continuità) ed eseguire processi in base allo stato del'UPS. Ecco alcuni esempi:

```
pf::powerfail:/sbin/shutdown -f -h +2 "Power Failure; System Shutting Down"
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

```

### Combinazioni di tasti personalizzati

Le seguenti linee aggiungono funzioni personalizzate quando una sequenza di tasti speciali vengono premuti. Si possono modificare queste sequenze per effettuare ciò che si preferisce, seguendo la sintassi di [ctrl-alt-del](#Ctrl-Alt-Del)

```
kb::kbrequest:/usr/bin/wall "Keyboard Request -- edit /etc/inittab to customize"

```

#### Sollevare una kbrequest

E' possibile simulare la sequenza speciale di tasti **kbrequest** inviando il segnale WINCH al processo di init(1) come root (tramite sudo). In questo esempio, il comando:

```
kill -WINCH 1

```

causa la scrittura da parte di `wall` su tutti i tty di:

```
Broadcast message from root@askapachehost (console) (Wed Oct 27 14:02:26 2010):  
Keyboard Request -- edit /etc/inittab to customize

```

## Vedere Anche

*   [Avviare X all'avvio del sistema](/index.php/Start_X_at_boot_(Italiano) "Start X at boot (Italiano)")
*   [Login automatico in una console virtuale](/index.php/Automatic_login_to_virtual_console_(Italiano) "Automatic login to virtual console (Italiano)")
*   [Display Manager](/index.php/Display_manager_(Italiano) "Display manager (Italiano)")
*   [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages")
*   [il file ~/.xinitrc](/index.php/Xinitrc_(Italiano) "Xinitrc (Italiano)")
*   [SLiM](/index.php/SLiM_(Italiano) "SLiM (Italiano)")

## Link Esterni

*   [Wikipedia:Init](https://en.wikipedia.org/wiki/Init "wikipedia:Init")
*   [Conoscenze di base di Linux e turorial. Runlevel.](http://www.linux-tutorial.info/modules.php?name=MContent&pageid=65)
*   [Linux.com. Introduzione ai runlevel ed inittab(inglese)](http://www.linux.com/articles/114107)
*   [Linux.com. Una introduzione ai servizi, runlevel, ed agli script rc.d.](http://www.linux.com/news/enterprise/systems-management/8116-an-introduction-to-services-runlevels-and-rcd-scripts)