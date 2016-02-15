Gli utenti e i gruppi sono usati nei sistemi GNU/Linux per [il controllo degli accessi](https://en.wikipedia.org/wiki/Access_control#Computer_security "wikipedia:Access control") - ciò permette di determinare quali utenti e servizi sono autorizzati ad accedere ai file, alle cartelle oppure alle periferiche presenti sul sistema. Linux offre dei sistemi relativamente semplici di default. Per avere delle opzioni avanzate, consultare [ACL](/index.php/ACL "ACL") e [LDAP Authentication](/index.php/LDAP_Authentication "LDAP Authentication").

## Contents

*   [1 Panoramica](#Panoramica)
*   [2 Permessi di accesso e proprietà](#Permessi_di_accesso_e_propriet.C3.A0)
*   [3 Lista dei file](#Lista_dei_file)
*   [4 Gestione degli utenti](#Gestione_degli_utenti)
    *   [4.1 Esempio aggiunta di un utente](#Esempio_aggiunta_di_un_utente)
    *   [4.2 Altri esempi di gestione degli utenti](#Altri_esempi_di_gestione_degli_utenti)
*   [5 Database Utente](#Database_Utente)
*   [6 Gestione dei gruppi](#Gestione_dei_gruppi)
*   [7 Lista di gruppi](#Lista_di_gruppi)
    *   [7.1 Gruppi per gli utenti](#Gruppi_per_gli_utenti)
    *   [7.2 Gruppi di sistema](#Gruppi_di_sistema)
    *   [7.3 Gruppi per software](#Gruppi_per_software)
    *   [7.4 Gruppi obsoleti o non utilizzati](#Gruppi_obsoleti_o_non_utilizzati)
        *   [7.4.1 Gruppi usati prima di Systemd](#Gruppi_usati_prima_di_Systemd)

## Panoramica

Un _utente_ è chiunque utilizzi un computer. In questo caso, ci si riferisce ai nomi che rappresentano questi utenti. Questi utenti possono essere Mary o Bill e possono utilizzare il nome di Dragonlady o Pirate al posto del loro nome reale. L'importante è che sul sistema sia presente un nome per ogni account creato, e questo nome sarà quello necessario per accedevi. Anche alcuni servizi vengono eseguiti usando account utente limitati o privilegiati.

La gestione degli utenti è stata creata per motivi di sicurezza per limitare gli accessi in determinati modi specifici. Il superutente (root) ha accesso completo al sistema operativo e la sua configurazione, è destinato solo per uso amministrativo. Gli utenti non privilegiati possono usare i programmi [su](/index.php/Su "Su") e [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") per un utilizzo controllato dei privilegi.

Può capitare che una persona abbia più di un account, a patto che utilizzi nomi diversi per ogni account. Inoltre, ci sono alcuni nomi riservati e non dovranno essere usati, come "root".

Infine, gli utenti possono essere raggruppati in un "gruppo", e gli utenti possono scegliere di far parte di un gruppo per usufruire dei privilegi che esso garantisce.

**Nota:** I principianti dovranno utilizzare questi strumenti con cautela ed evitare di modificare altri account _esistenti_, tranne che il proprio.

## Permessi di accesso e proprietà

Da [In UNIX ogni cosa è un File:](http://ph7spot.com/musings/in-unix-everything-is-a-file):

	_Il sistema UNIX è il risultato di alcune idee e concetti unificatori che hanno modellato il suo design, la sua interfaccia utente, la sua cultura ed evoluzione. Una tra le più importanti è probabilmente il mantra: "ogni cosa è un file", largamente considerata come uno dei punti basilari di UNIX._

	_Questo concetto chiave di design consiste nel fornire un paradigma unificato per l'accesso ad un ampio spettro di risorse input/output: documenti, cartelle, dischi rigidi, lettori CD, modem, tastiere, stampanti, monitor, terminali e perfino alcune comunicazioni tra processi o di rete. Il trucco è fornire un'astrazione comune per tutte queste risorse, ognuna delle quali fu chiamata "file" dai padri di UNIX. Dato che ogni "file" è accessibile per mezzo delle stesse API, si può usare lo stesso set di comandi di base per accedere in lettura/scrittura ad un disco, una tastiera, un documento o un dispositivo di rete._

Da [Estensione dell'Astrazione File di UNIX per il Networking generico](http://www.intel-research.net/Publications/Pittsburgh/101220041324_277.pdf):

	_Un'astrazione fondamentale, efficacissima e coerente, fornita in UNIX e sistemi operativi compatibili, è l'astrazione file. Molti servizi e interfacce per i dispositivi nei sistemi operativi sono implementati per fornire una metafora di file o file system alle applicazioni. Questo permette nuovi utilizzi per le applicazioni esistenti, ed inoltre ne aumenta fortemente le capacità — semplici strumenti con usi specifici possono, con l'astrazione file di UNIX, essere usati in nuove maniere. Un modesto programma come cat, disegnato per leggere uno o più file e mostrare il loro contenuto nello standard output, può essere usato per leggere l'input/output di dispositivi per mezzo di speciali file dispositivo, di solito posti dentro la cartelle `/dev`. Su molti sistemi, la registrazione e la riproduzione audio può essere semplicemente eseguita con i comandi, rispettivamente, "`cat /dev/audio > myfile`" e "`cat myfile > /dev/audio`"._

Ogni file in un sistema GNU/Linux appartiene a un utente e a un gruppo. In aggiunta, ci sono tre tipi di permessi di accesso: il permesso di lettura, di scrittura, e di esecuzione. Differenti tipi di accesso possono essere applicati all'utente proprietario, al gruppo proprietario oppure agli altri(coloro che non ne hanno il possesso). Si possono visualizzare i proprietari ed i permessi dei file usando l'opzione long lisintg del comando `ls`:

 `$ ls -l /boot/` 

```
total 13740
drwxr-xr-x 2 root root    4096 Jan 12 00:33 grub
-rw-r--r-- 1 root root 8570335 Jan 12 00:33 initramfs-linux-fallback.img
-rw-r--r-- 1 root root 1821573 Jan 12 00:31 initramfs-linux.img
-rw-r--r-- 1 root root 1457315 Jan  8 08:19 System.map26
-rw-r--r-- 1 root root 2209920 Jan  8 08:19 vmlinuz-linux
```

Nella prima colonna sono visualizzati i permessi dei file(ad esempio, il file `initramfs-linux.img` ha i permessi `-rw-r--r--`). Nella terza e la quarta sono visualizzati rispettivamente l'utente ed il gruppo proprietari. Nello stesso esempio tutti i file sono posseduti dall'utente _root_ e dal gruppo _root_.

 `$ ls -l /media/` 

```
total 16
drwxrwx--- 1 root vboxsf 16384 Jan 29 11:02 sf_Shared</nowiki>
```

In questo esempio, la cartella `sf_Shared` è posseduta dall'utente _root_ e dal gruppo _vboxsf_. Si possono ottenere maggiori informazioni riguardo ai proprietari ed ai permessi dei file usando il comando `stat`:

L'utente proprietario:

 `$ stat -c %U /media/sf_Shared/`  `root` 

Il gruppo proprietario:

 `$ stat -c %G /media/sf_Shared/`  `vboxsf` 

Permessi di accesso:

 `$ stat -c %A /media/sf_Shared/`  `drwxrwx---` 

I permessi di accesso sono visualizzati in tre gruppi di caratteri, rappresentano rispettivamente i permessi dell'utente proprietario, del gruppo proprietario, e degli altri. Ad esempio i la serie di caratteri `-rw-r--r--` indicano che l'utente proprietario ha i permessi di lettura e scrittura, ma non di esecuzione (`rw-`), mentre gli utenti appartenenti al gruppo proprietario e gli altri hanno solo il permesso di lettura (`r--` e `r--`). Invece, la serie di caratteri `drwxrwx---` indicano che l'utente proprietario e gli utenti appartenenti al gruppo proprietario hanno i permessi di lettura, scrittura ed esecuzione (`rwx` e `rwx`), mentre gli altri utenti viene negato ogni tipo di accesso (`---`). Il primo carattere indica il tipo di file.

Per elencare i file posseduti da un utente o un gruppo con il comando `find`:

```
# find / -group [group]

```

```
# find / -user [user]

```

L'utente ed il gruppo proprietario dei file possono essere cambiati con il comando `chown` (change owner). I permessi di accesso ai file possono essere cambiati con il comando `chmod` (change mode).

Consultare [man chown](http://linux.die.net/man/1/chown), [man chmod](http://linux.die.net/man/1/chmod), e [Linux file permissions](http://www.tuxfiles.org/linuxhelp/filepermissions.html) per maggiori informazioni.

## Lista dei file

**Attenzione:** Non modificare questi file manualmente. Ci sono utility che li gestiscono correttamente e non ne invalidano il formato del database. Vedere la [#Gestione degli utenti](#Gestione_degli_utenti) e la [#Gestione dei gruppi](#Gestione_dei_gruppi) per una panoramica.

| File | Funzione |
| `/etc/shadow` | Informazioni riservate degli account utente |
| `/etc/passwd` | Informazioni degli account utente |
| `/etc/gshadow` | Contiene informazioni riservate dei gruppi di utenti |
| `/etc/group` | Definisce a quali gruppi appartengono i vari utenti |
| `/etc/sudoers` | Lista di chi può eseguire cosa con sudo |
| `/home/*` | Cartelle home |

## Gestione degli utenti

Per visualizzare gli utenti connessi al sistema è possibile usare il comando `who`.

Per aggiungere un nuovo utente, usare il comando `useradd`:

```
# useradd -m -g [gruppo_iniziale] -G [gruppi_aggiuntivi] -s [login_shell] [nomeutente]

```

*   `-m` crea la carella home nel percorso `/home/_nomeutente_`; all'interno della cartella home, un utente non-root può salvare file, cancellarli ed installare programmi.
*   `-g` indica il nome o il numero del gruppo principale di appartenenza dell'utente; il gruppo deve esistere; se non viene specificato, il comportamento di `useradd` dipenderà dalla variabile di ambiente `USERGROUPS_ENAB` definita in `/etc/login.defs`. Il comportamento predefinito (`USERGROUPS_ENAB yes`) è quello di creare un gruppo con lo stesso nome del nome utente, con `GID` pari a `UID`.
*   `-G` precede una lista di gruppi aggiuntivi a cui l'utente appartiene. Ogni gruppo deve essere separato dal successivo da una virgola, senza usare mai gli spazi. Di default non è previsto nessun gruppo aggiuntivo.
*   `-s` definisce il percorso ed il nome del file della shell di login dell'utente; dopo che il processo di avvio è completo, la shell di login di default è quella definita qui. Assicurarsi che la shell indicata sia installata se si sceglie una shell diversa da [bash](/index.php/Bash_(Italiano) "Bash (Italiano)").

**Attenzione:** La shell di login dovrebbe essere una di quelli elencati in `/etc/shells`. Per i programmi che utilizzano PAM, questo viene controllato dal modulo `pam_shells`.

### Esempio aggiunta di un utente

In un tipico sistema desktop per aggiungere un nuovo utente denominato _archie_ specificando [bash](/index.php/Bash_(Italiano) "Bash (Italiano)") come shell di login e aggiungerlo al gruppo `wheel` (si veda [#Gruppi per gli utenti](#Gruppi_per_gli_utenti) per maggiori informazioni) utilizare:

```
# useradd -m -G wheel -s /bin/bash archie

```

Questo comando creerà automaticamente un gruppo denominato `archie` con lo stesso GID pari all' UID dell'utente `archie` e ne fa di questo il gruppo predefinito dell'utente `archie` al login . Creare ad ogni utente il proprio gruppo, è il modo migliore per aggiungere utenti.

Si potrebbe anche dare all'utente un gruppo predefinito preferenziale, come ad esempio `users`:

```
 # useradd -m -g users -G wheel -s /bin/bash archie

```

Tuttavia, questo metodo **non** è consigliato per sistemi multi-utente. In genere, il modo di controllare la sicurezza per consentire ai gruppi di condividere l'accesso in scrittura a un particolare insieme di file/cartelle è quello di impostare all'utente un valore di [umask](/index.php/Umask "Umask") `002`, significa che il gruppo in questione ha sempre accesso in scrittura qualsiasi file creato per impostazione predefinita. In questo modo la cartella home dell'utente, che è di proprietà di un gruppo che ha come nome del gruppo lo stesso nome utente, è ancora in sola lettura per gli altri utenti del sistema, mentre i file/cartelle condivisi possono essere resi scrivibili a tutti per impostazione predefinita utilizzando un gruppo operativo.

### Altri esempi di gestione degli utenti

Per aggiungere un utente ad altri gruppi usare:

```
# usermod -aG _gruppi_aggiuntivi_ _nome_utente_

```

In alternativa , può essere utilizzato gpasswd . Anche se il nome utente può essere aggiunto (o rimosso) solo da un gruppo alla volta .

```
# gpasswd --add _nome_utente_ _gruppo_

```

**Attenzione:** Se l'opzione `-a` viene omessa al comando _usermod_ descritto sopra, l'utente viene rimosso da tutti i gruppi non elencati in `_gruppi_aggiuntivi_` (cioè l' utente sarà membro solo di quei gruppi elencati in `_gruppi_aggiuntivi_`).

Per inserire le informazioni dell'utente per il campo GECOS (es. il nome completo), digitare:

```
# chfn _nomeutente_

```

(in questo modo `chfn` verrà eseguito in modo interattivo).

Per creare la password dell'utente, digitare:

```
# passwd _nomeutente_

```

Per contrassegnare la password di un utente come scaduta, imponendo loro di crearne una nuova la prima volta che effettuano il log-in, digitare:

```
# chage -d 0 _username_

```

Gli account utente possono essere rimossi tramite il comando _userdel_.

```
# userdel -r _nomeutente_

```

L'opzione `-r` specifica che la cartella `home` e la coda (spool) della posta dell'utente verranno cancellati.

## Database Utente

Le informazioni degli utenti locali sono contenute nel file `/etc/passwd`. Per visualizzare gli account utente presenti sul sistema:

```
$ cat /etc/passwd

```

Ogni riga del file fa riferimento ad un account, e segue questo schema:

```
account:password:UID:GID:GECOS:cartella_home:shell

```

dove

*   `account` è il nome utente
*   `password` è la passrword dell'utente
*   `UID` è l'identificativo numerico dell'utente
*   `GID` è l'identificativo numerico del gruppo principale dell'utente
*   `GECOS` questo campo è opzionale e contiene le informazioni aggiuntive dell'utente; di solito contiene il nome completo dell'utente
*   `cartella_home` contiene il percorso della cartella `$HOME` dell'utente
*   `shell` indica l'interprete dei comandi utilizzato dall'utente (il default è `/bin/sh`)

**Nota:** Arch Linux usa le password _shadowed_. Il file `passwd` è leggibile da tutti gli utenti, per cui memorizzare le password (sia criptate che altrimenti) in questo file non sarebbe sicuro. Per questo il campo `password` contiene il carattere segnaposto `x`, il quale indica che la password criptata è salvata nel file ad accesso limitato `/etc/shadow`.

## Gestione dei gruppi

Nel file `/etc/group` sono definiti i gruppi presenti sul sistema (`man group` per maggiori informazioni).

Per visualizzare l'appartenenza ai gruppi con il comando `groups`:

```
$ groups [user]

```

Se il parametro `user` viene omesso, verranno mostrate i gruppi a cui appartiene l'utente corrente.

Il comando `id` fornisce informazioni aggiuntive, come l'UID dell'utente ed i GID associati:

```
$ id [user]

```

Per elencare tutti i gruppi del sistema:

```
$ cat /etc/group

```

Per creare un nuovo gruppo usare il comando `groupadd`:

```
# groupadd [group]

```

Aggiungere un utente ad un gruppo con il comando `gpasswd`:

```
# gpasswd -a [user] [group]

```

Per eliminare un gruppo esistente:

```
# groupdel [group]

```

Per rimuovere un utente da un gruppo:

```
# gpasswd -d [user] [group]

```

Se l'utente è ancora connesso al sistema, sarà necessario che si disconnetta e acceda nuovamente al sistema per far sì che le modifiche abbiano effetto.

## Lista di gruppi

### Gruppi per gli utenti

Gli utenti di pc Workstation/desktop sono soliti aggiungere i propri utenti non-root ai seguenti gruppi per permettere l'accesso alle periferiche e facilitare l'amministrazione del sistema:

| Gruppo | File interessati | Scopo |
| games | `/var/games` | Concede l'accesso ad alcuni giochi. |
| rfkill | `/dev/rfkill` | Permette di controllare lo stato di alimentazione dei dispositivi wireless (utilizzato dal pacchetto [rfkill](https://www.archlinux.org/packages/?name=rfkill)). |
| users | Gruppo standard degli utenti. |
| uucp | `/dev/ttyS[0-9]`, `/dev/tts/[0-9]` | Permette di accedere a periferiche seriali ed USB come modem, controller, porte seriali/RS232. |
| wheel | Gruppo di Amministrazione, comunemente utilizzato per consentire l'accesso alle utility [sudo](/index.php/Sudo_(Italiano) "Sudo (Italiano)") e [su](/index.php/Su "Su") ( non lo usa di default), , configurabili in `/etc/pam.d/su` and `/etc/pam.d/su-l`). Può anche essere usato per avere accesso completo in lettura ai file [journal](/index.php/Systemd_(Italiano)#Journal "Systemd (Italiano)"). |

### Gruppi di sistema

I seguenti gruppi sono usati per scopi di sistema ed è difficile che siano utili agli utenti alle prime armi con Arch:

| Gruppo | File interessati | Scopo |
| bin | none | Storico |
| daemon |
| dbus | usato internamente da [dbus](https://www.archlinux.org/packages/?name=dbus) |
| ftp | `/srv/ftp` | usato da server [FTP](https://en.wikipedia.org/wiki/it:File_Transfer_Protocol "wikipedia:it:File Transfer Protocol") come [Proftpd](/index.php/Proftpd "Proftpd") |
| fuse | Utilizzato da fuse per permettere il montaggio da utente. |
| http |
| kmem | `/dev/port`, `/dev/mem`, `/dev/kmem` |
| mail | `/usr/bin/mail` |
| mem |
| nobody | Gruppo senza privilegi. |
| polkitd | Gruppo di [polkit](/index.php/Polkit "Polkit"). |
| root | `/*` | Accesso completo al sistema ed alla sua amministrazione (root, admin). |
| smmsp | Gruppo di [sendmail](https://en.wikipedia.org/wiki/it:sendmail "wikipedia:it:sendmail"). |
| systemd-journal | `/var/log/journal/*` | Fornisce accesso completo ai log di Systemd. In caso contrario, vengono visualizzati solo i messaggi generati dagli utenti. |
| tty | `/dev/tty`, `/dev/vcc`, `/dev/vc`, `/dev/ptmx` | Ad esempio garantisce l'accesso a `/dev/ACMx` |

### Gruppi per software

Questi gruppi sono utilizzati da alcuni software non essenziale. A volte vengono utilizzati solo internamente, in questi casi non si deve aggiungere l'utente a questi gruppi. Vedere la pagina principale del software per maggiori dettagli.

| Gruppo | File interessati | Scopo |
| adbusers | file dei dispositivi in `/dev/` | Diritti di acesso al Debugging Bridge di [Android](/index.php/Android "Android"). |
| avahi |
| cdemu | `/dev/vhba_ctl` | Permesso per l'utilizzo dell'emulazione con [cdemu](/index.php/Cdemu "Cdemu"). |
| clamav | `/var/lib/clamav/*`, `/var/log/clamav/*` | Usato da [Clam AntiVirus](/index.php/ClamAV_(Italiano) "ClamAV (Italiano)"). |
| gdm | Cartella di autorizzazione del server X (ServAuthDir) | gruppo di [GDM](/index.php/GDM "GDM"). |
| locate | `/usr/bin/locate`, `/var/lib/locate`, `/var/lib/mlocate`, `/var/lib/slocate` | Permette l'uso del comando [updatedb](https://en.wikipedia.org/wiki/updatedb "wikipedia:updatedb"). |
| mpd | `/var/lib/mpd/*`, `/var/log/mpd/*`, `/var/run/mpd/*`, opzionalmente cartelle di musica | gruppo di [MPD](/index.php/Music_Player_Daemon_(Italiano) "Music Player Daemon (Italiano)"). |
| networkmanager | Richiesto per connettersi via wireless se si usa [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)"). Questo gruppo non è incluso in Arch di default, sarà quindi necessario aggiungerlo manualmente. |
| ntp | `/var/lib/ntp/*` | Gruppo di [NTPd](/index.php/NTPd_(Italiano) "NTPd (Italiano)"). |
| thinkpad | `/dev/misc/nvram` | Usato dagli utenti di ThinkPad per accedere a programmi come [tpb](/index.php/Tpb "Tpb"). |
| vboxusers | `/dev/vboxdrv` | Permette l'uso del programma [VirtualBox](/index.php/VirtualBox_(Italiano) "VirtualBox (Italiano)"). |
| vboxsf | cartelle condivise delle macchine virtuali | Usato da [VirtualBox](/index.php/VirtualBox_(Italiano) "VirtualBox (Italiano)"). |
| vmware | Permette l'uso del programma [VMware](/index.php/VMware_(Italiano) "VMware (Italiano)"). |
| wireshark | Ottenere i diritti per catturare i pacchetti con [Wireshark](/index.php/Wireshark "Wireshark"). |

### Gruppi obsoleti o non utilizzati

I seguenti gruppi al momento non sono utilizzati:

| Gruppo | Scopo |
| log | Accesso ai file di log in `/var/log`. |
| Ssh | ~~[Sshd](/index.php/Secure_Shell_(Italiano) "Secure Shell (Italiano)") può essere configurato per consentire solo i membri appartenenti a questo gruppo di effettuare il login.~~ Questo è vero per qualsiasi gruppo arbitrario, il gruppo `ssh` non viene creato per impostazione predefinita, quindi non è standard . |
| stb-admin | **Non utilizzato!** Diritti di accesso a [system-tools-backends](http://system-tools-backends.freedesktop.org/) |
| Kvm | Aggiunta di un utente al al gruppo `kvm` utilizzato per consentire agli utenti non-root di accedere a macchine virtuali utilizzando [KVM](/index.php/KVM "KVM"). Questo è stato deprecato in favore dell'uso delle regole [udev](/index.php/Udev_(Italiano) "Udev (Italiano)"), e questo viene fatto automaticamente. |

#### Gruppi usati prima di Systemd

**Nota:** Questi gruppi erano necessari prima della migrazione di Arch Linux a [Systemd](/index.php/Systemd_(Italiano) "Systemd (Italiano)"). Ora questi non sono più necessari inquanto la sessione _logind_ non soffre più di problemi (si veda [General troubleshooting#Session permissions](/index.php/General_troubleshooting#Session_permissions "General troubleshooting") per controllare). I gruppi possono anche causare alcune mal-funzionalità del sistema. Si veda [migrazione a systemd](/index.php/SysVinit_(Italiano)#Migrare_a_Systemd "SysVinit (Italiano)") per maggiori dettagli.

| Grouppo | File interessati | Scopo |
| audio | `/dev/audio`, `/dev/snd/*`, `/dev/rtc0` | Accesso diretto all'hardware sonoro , per tutte le sessioni (requisito imposto sia da [ALSA](/index.php/ALSA_(Italiano) "ALSA (Italiano)") che da [OSS](/index.php/OSS_(Italiano) "OSS (Italiano)")). Le sessioni locali hanno già la possibilità di modificare i controlli del mixer audio e l'accesso. |
| camera | Accesso alle [Fotocamere digitali](/index.php/Digital_Cameras_(Italiano) "Digital Cameras (Italiano)"). |
| disk | `/dev/sda[1-9]`, `/dev/sdb[1-9]` | Accesso alle periferiche a blocchi che non appartengono ai gruppi _optical_, _floppy_ e _storage_. |
| floppy | `/dev/fd[0-9]` | Accesso ai floppy drive. |
| lp | `/etc/cups`, `/var/log/cups`, `/var/cache/cups`, `/var/spool/cups`, `/dev/parport[0-9]` | Accesso alle stampanti; permette all'utente di gestire le stampe. |
| network | Pemette di cambiare le impostazioni di rete nel caso si usino programmi come [NetworkManager](/index.php/NetworkManager_(Italiano) "NetworkManager (Italiano)"). |
| optical | `/dev/sr[0-9]`, `/dev/sg[0-9]` | Accesso ai dispositivi ottici come lettori CD o DVD. |
| power | Permette l'uso del programma [pm-utils](/index.php/Pm-utils_(Italiano) "Pm-utils (Italiano)") (sospensione, ibernazione...) e dei programmi di controllo del risparmio energetico. |
| scanner | `/var/lock/sane` | Accesso agli scanner. |
| storage | Accesso ai dischi rimovibili come dischi esterni USB, pennine USB, lettori MP3; consente all'utente di montare le periferiche di archiviazione. |
| sys | Permette l'amministrazione delle stampanti in [CUPS](/index.php/CUPS_(Italiano) "CUPS (Italiano)"). |
| video | `/dev/fb/0`, `/dev/misc/agpgart` | Accesso alle periferiche di acquisizione video, DRI/3D accelerazione hardware ([X](/index.php/Xorg_(Italiano) "Xorg (Italiano)") può essere usato anche _senza_ appartenere a questo gruppo). Le sessioni locali hanno già la possibilità di utilizzare l'accelerazione hardware e di acquisizione video. |