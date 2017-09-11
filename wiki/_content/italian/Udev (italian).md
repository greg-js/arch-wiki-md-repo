udev sostituisce in tutte le loro funzioni sia `hotplug` che `hwdetect`.

"udev" è il device manager per il kernel Linux. Principalmente, si occupa di creare i file relativi alle periferiche in `/dev`. Esso è il successore di devfs ed hotplug, si occupa infatti dell'intera cartella `/dev` ed delle eventuali modifiche, come l'inserimento o la rimozione di periferiche, avrà il compito di gestire le operazioni in userspace ed eventualmente caricherà i firmware relativi alle periferiche.

udev carica i moduli del kernel simultaneamente, ciò può quindi comportare una maggiore velocità di avvio del sistema. Comunque uno svantaggio è che non sempre i moduli vengono caricati nel solito ordine ad ogni avvio, questo può causare problemi ad alcune schede audio o di rete(se sono presenti due o più di queste schede). Vedere più avanti per maggiori informazioni riguardo a questo problema.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Le regole di udev](#Le_regole_di_udev)
*   [3 Trucchi e consigli](#Trucchi_e_consigli)
    *   [3.1 UDisks](#UDisks)
        *   [3.1.1 UDisks Wrapper](#UDisks_Wrapper)
        *   [3.1.2 UDisks Shell Functions](#UDisks_Shell_Functions)
    *   [3.2 Mount automatico delle periferiche USB](#Mount_automatico_delle_periferiche_USB)
        *   [3.2.1 Mount in /media; usando l'etichetta della partizione se presente](#Mount_in_.2Fmedia.3B_usando_l.27etichetta_della_partizione_se_presente)
        *   [3.2.2 Mount in /media; usando l'etichetta della partizione se presente; con supporto alla cifratura LUKS](#Mount_in_.2Fmedia.3B_usando_l.27etichetta_della_partizione_se_presente.3B_con_supporto_alla_cifratura_LUKS)
        *   [3.2.3 Mount in /media; usando l'etichetta della partizione se presente; consentire agli utenti lo smontaggio](#Mount_in_.2Fmedia.3B_usando_l.27etichetta_della_partizione_se_presente.3B_consentire_agli_utenti_lo_smontaggio)
        *   [3.2.4 Mount in /mnt; creando un link simbolico in /media](#Mount_in_.2Fmnt.3B_creando_un_link_simbolico_in_.2Fmedia)
        *   [3.2.5 Mount in /media *solo* se la partizione ha una etichetta](#Mount_in_.2Fmedia_solo_se_la_partizione_ha_una_etichetta)
        *   [3.2.6 Mount in /media; usando l'etichetta della partizione se presente; usando ntfs-3g](#Mount_in_.2Fmedia.3B_usando_l.27etichetta_della_partizione_se_presente.3B_usando_ntfs-3g)
        *   [3.2.7 Mount delle SD card](#Mount_delle_SD_card)
        *   [3.2.8 Mount dei CD](#Mount_dei_CD)
        *   [3.2.9 Accedere a Firmware Programmers ed a USB Virtual Comm Devices](#Accedere_a_Firmware_Programmers_ed_a_USB_Virtual_Comm_Devices)
    *   [3.3 Eseguire all’inserimento di un USB](#Eseguire_all.E2.80.99inserimento_di_un_USB)
    *   [3.4 Mount dei supporti di memoria interni come utente non privilegiato](#Mount_dei_supporti_di_memoria_interni_come_utente_non_privilegiato)
    *   [3.5 Marchiare le porte SATA interne come porte eSATA](#Marchiare_le_porte_SATA_interne_come_porte_eSATA)
*   [4 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [4.1 Inserire i moduli in blacklist](#Inserire_i_moduli_in_blacklist)
    *   [4.2 udevd fallisce all’avvio](#udevd_fallisce_all.E2.80.99avvio)
    *   [4.3 Problemi noti relativi all'hardware](#Problemi_noti_relativi_all.27hardware)
        *   [4.3.1 Le periferiche BusLogic smettono di funzionare e quindi causano un blocco durante la fase di avvio.](#Le_periferiche_BusLogic_smettono_di_funzionare_e_quindi_causano_un_blocco_durante_la_fase_di_avvio.)
        *   [4.3.2 Periferiche rimovibili non vengono riconosciute come tali](#Periferiche_rimovibili_non_vengono_riconosciute_come_tali)
    *   [4.4 Problemi noti relativi al caricamento automatico dei moduli](#Problemi_noti_relativi_al_caricamento_automatico_dei_moduli)
        *   [4.4.1 Moduli per lo scaling della frequenza della CPU](#Moduli_per_lo_scaling_della_frequenza_della_CPU)
        *   [4.4.2 Problemi con l'audio o alcuni moduli non vengono caricati automaticamente](#Problemi_con_l.27audio_o_alcuni_moduli_non_vengono_caricati_automaticamente)
        *   [4.4.3 Ordinamento delle periferiche, schede di rete/audio che cambiano ordine ad ogni avvio](#Ordinamento_delle_periferiche.2C_schede_di_rete.2Faudio_che_cambiano_ordine_ad_ogni_avvio)
    *   [4.5 Problemi noti legati all'uso di Kernel personalizzati](#Problemi_noti_legati_all.27uso_di_Kernel_personalizzati)
        *   [4.5.1 Udev non si avvia](#Udev_non_si_avvia)
    *   [4.6 Periferiche IDE CD/DVD](#Periferiche_IDE_CD.2FDVD)
    *   [4.7 Le periferiche ottiche hanno l'ID del gruppo impostato a disk](#Le_periferiche_ottiche_hanno_l.27ID_del_gruppo_impostato_a_disk)
*   [5 Altre risorse](#Altre_risorse)

## Installazione

Udev è ora parte di [systemd](https://www.archlinux.org/packages/?name=systemd) e viene installato di default su Arch Linux. Vedere [systemd-udevd.service(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-udevd.service.8) per ulteriori informazioni.

## Le regole di udev

Le regole di udev scritte dall'amministratore di sistema, si trovano in `/etc/udev/rules.d/`, questi file avranno l'estensione `.rules`. Le regole fornite dall'installazione di vari pacchetti si trovano in `/lib/udev/rules.d/`. Nel caso in cui esistano due regole con lo stesso nome sia sotto `/lib` che sotto `/etc`, la regola che si trova nella cartella `/etc` avrà la precedenza.

Per maggiori informazioni su come scrivere regole per udev consultare [il sito(in inglese)](http://www.reactivated.net/writing_udev_rules.html).

Per ottenere una lista dei possibili attributi di una periferica utilizzabili dalle regole di udev:

```
# udevadm info -a -n [nome periferica]

```

Sostituendo [nome periferica] con la periferica del sistema, come '/dev/sda' oppure '/dev/ttyUSB0'.

Udev rileva i cambiamenti alle file delle regole automaticamente, quindi i cambiamenti avranno effetto immediato senza dover riavviare udev. Comunque, le regole non verranno applicate automaticamente alle periferiche preesistenti, quindi le periferiche rimovibili come le periferiche USB, probabilmente dovranno essere rimosse e reinserite perché le nuove regole siano applicate.

## Trucchi e consigli

### UDisks

[Installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [udisks](https://aur.archlinux.org/packages/udisks/) e tutte le periferiche verranno montate automaticamente in GNOME e KDE SC 4.6\. Non sarà necessario utilizzare regole aggiuntive per questo metodo. In aggiunta, se si utilizza HAL solamente per il mount automatico delle periferiche, a questo punto sarà possibile rimuoverlo.

#### UDisks Wrapper

Un UDisks wrapper ha il vantaggio di essere molto facile da installare e non necessita(oppure solo in minima parte) di configurazioni. Il wrapper monterà automaticamente CD, DVD e le periferiche di archiviazione rimovibili.

*   [devmon](http://igurublog.wordpress.com/downloads/script-devmon/) - ([disponibile su AUR](https://aur.archlinux.org/packages.php?ID=45842)) Si tratta di un script Bash, privo di configurazione, esso permette di effettuare l'automount di periferiche CD/DVD e di dischi esterni. Permette anche di eseguire applicazioni o comandi dopo il mount, di ignorare specifiche periferiche o specifiche etichette dei volumi, e di effettuare l'umount delle periferiche rimovibili.
*   [udiskie](/index.php/Udiskie "Udiskie") - Scritto in Python. Permette il mount automatico e lo smontaggio con ogni utente.
*   [udisksevt](https://aur.archlinux.org/packages.php?ID=38723) - Scritto in Haskell. Permette il mount automatico ad ogni utente. Ideato per essere integrato con [traydevice](https://aur.archlinux.org/packages/traydevice/).
*   [udisksvm](https://aur.archlinux.org/packages.php?ID=46572) è uno script Bash che usa udisks e [traydevice](https://aur.archlinux.org/packages/traydevice/) per effettuare l'automount delle periferiche rimovibili, e ne consente il controllo tramite una interfaccia grafica, mediante l'uso di una icona nell'area di notifica utilizzando i click del mouse per smontare, rimontare o espellere le periferiche.

#### UDisks Shell Functions

Mentre UDisks include dei semplici metodi di mount(ed umount) delle periferiche anche da linea di comando, può essere fastidioso eseguire i comandi ogni volta. Queste funzioni della shell garantiranno un uso più veloce e facile.

*   [udisks_functions](https://bbs.archlinux.org/viewtopic.php?id=109307) - Scritto per Bash.

*   [bashmount](https://bbs.archlinux.org/viewtopic.php?id=117674) - bashmount [(AUR)](https://aur.archlinux.org/packages.php?ID=48524) è uno script bash strutturato a menù, ed ha un semplice file di configurazione che lo rende semplice da configurare ed implementare.

### Mount automatico delle periferiche USB

**Nota:** Nelle seguenti regole, le opzioni per il comando mount sono definite con `ENV{mount_options}="relatime"`, consultare [mount(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)(ed eventualmente [ntfs-3g(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/ntfs-3g.8)) per tutte le possibili opzioni, leggere [Improving performance#Mount options](/index.php/Improving_performance#Mount_options "Improving performance") per informazioni relative alle performance.

**Nota:** L'opzione `users` per il comando mount **non** permetterà comunque agli utenti di smontare il filesystem.

**Tip:** L'opzione `noexec` impedisce l'esecuzione di programmi residenti sul filesystem montato.

#### Mount in /media; usando l'etichetta della partizione se presente

La seguente regola imposta il mount automatico delle partizioni/periferiche identificate come `/dev/sd*` (pendrive USB, hard disk esterni ed in alcuni casi SD card). Se esiste una etichetta, allora il mount sarà effettuato in `/media/<etichetta>`, altrimenti in `/media/usbhd-sd*` (esempio: /media/usbhd-sdb1):

 `/etc/udev/rules.d/11-media-by-label-auto-mount.rules` 
```
KERNEL!="sd[a-z][0-9]", GOTO="media_by_label_auto_mount_end"

# Importa le informazioni sui Filesystem
IMPORT{program}="/sbin/blkid -o udev -p %N"

# Individua l'etichetta se esiste, altrimenti ne crea una
ENV{ID_FS_LABEL}!="", ENV{dir_name}="%E{ID_FS_LABEL}"
ENV{ID_FS_LABEL}=="", ENV{dir_name}="usbhd-%k"

# Opzioni globali per il comando mount 
ACTION=="add", ENV{mount_options}="relatime"
# Opzioni di mount specifiche per i filesystem
ACTION=="add", ENV{ID_FS_TYPE}=="vfat|ntfs", ENV{mount_options}="$env{mount_options},utf8,gid=100,umask=002"

# Effettua il mount della periferica
ACTION=="add", RUN+="/bin/mkdir -p /media/%E{dir_name}", RUN+="/bin/mount -o $env{mount_options} /dev/%k /media/%E{dir_name}"

# Effettua la pulizia delle directory alla rimozione della periferica
ACTION=="remove", ENV{dir_name}!="", RUN+="/bin/umount -l /media/%E{dir_name}", RUN+="/bin/rmdir /media/%E{dir_name}"

# Uscita
LABEL="media_by_label_auto_mount_end"

```

#### Mount in /media; usando l'etichetta della partizione se presente; con supporto alla cifratura LUKS

Come nella regola precedente, ma in questo caso nella periferica risiede una partizione con un filesystem criptato con LUKS, verrà aperto una finestra di `xterm` dove si dovrà inserire la passphrase(supponendo che xterm sia già installato). Consultare anche [questo post sul forum internazionale](https://bbs.archlinux.org/viewtopic.php?pid=696239#p696239).

**Nota:** Può essere necessario modificare il percorso di `cryptsetup`, a seconda della versione (es: < 1.1.1_rc2-1).
 `/etc/udev/rules.d/11-media-by-label-auto-mount.rules` 
```
KERNEL!="sd[a-z]*", GOTO="media_by_label_auto_mount_end"
ACTION=="add", PROGRAM!="/sbin/blkid %N", GOTO="media_by_label_auto_mount_end"

# Non effettua il mount di file system già montati in altri percorsi per evitare che in /media si creino voci per tutte le partizioni locali
ACTION=="add", PROGRAM=="/bin/grep -q ' /dev/%k ' /proc/self/mountinfo", GOTO="media_by_label_auto_mount_end"

# Apre la partizione LUKS se necessario
PROGRAM=="/sbin/blkid -o value -s TYPE %N",  RESULT=="crypto_LUKS", ENV{crypto}="mapper/", ENV{device}="/dev/mapper/%k"
ENV{crypto}=="", ENV{device}="%N"
ACTION=="add", ENV{crypto}!="", PROGRAM=="/usr/bin/xterm -display :0.0 -e 'echo Password for /dev/%k; /sbin/cryptsetup luksOpen %N %k'"
ACTION=="add", ENV{crypto}!="", TEST!="/dev/mapper/%k", GOTO="media_by_label_auto_mount_end"

# Opzioni globali per il comando mount
ACTION=="add", ENV{mount_options}="noatime"
# opzioni di mount specifiche per i filesystem
ACTION=="add", PROGRAM=="/sbin/blkid -o value -s TYPE %E{device}", RESULT=="vfat|ntfs", ENV{mount_options}="%E{mount_options},utf8,gid=100,umask=002"

# Individua l'etichetta se esiste, altrimenti ne crea una
PROGRAM=="/sbin/blkid -o value -s LABEL %E{device}", ENV{dir_name}="%c"
# Utilizza basename per to gestire etichette come ../mnt/foo
PROGRAM=="/usr/bin/basename '%E{dir_name}'", ENV{dir_name}="%c"
ENV{dir_name}=="", ENV{dir_name}="usbhd-%k"

# Effettua il mount della periferica
ACTION=="add", ENV{dir_name}!="", RUN+="/bin/mkdir -p '/media/%E{dir_name}'", RUN+="/bin/mount -o %E{mount_options} /dev/%E{crypto}%k '/media/%E{dir_name}'"

# Effettua la pulizia delle directory alla rimozione della periferica
ACTION=="remove", ENV{dir_name}!="", RUN+="/bin/umount -l '/media/%E{dir_name}'"
ACTION=="remove", ENV{crypto}!="", RUN+="/sbin/cryptsetup luksClose %k"
ACTION=="remove", ENV{dir_name}!="", RUN+="/bin/rmdir '/media/%E{dir_name}'"

# Uscita
LABEL="media_by_label_auto_mount_end"

```

#### Mount in /media; usando l'etichetta della partizione se presente; consentire agli utenti lo smontaggio

Questa è una variante della regola precedente. Utilizza `pmount` (che dovrà essere già installato) anziché `mount`, consentendo agli utenti senza privilegi di root di smontare le periferiche montate da udev, e di rimuovere automaticamente il punto di mount. Sarà necessario specificare nel comando `RUN` della regola il nome utente(nell'esempio 'tomk'), rendendo questa regola non adatta a sistemi multi utente. Il supporto a LUKS è stato rimosso dal seguente esempio ma può essere reinserito come nel precedente esempio. Si dovrà modificare l'uso del comando `/bin/su` in modo da essere eseguito dall'utente giusto per il proprio sistema. Notare che il punto di mount rimarrà se la periferica è montata, ed il sistema, avente la cartella `/media` persistente, viene spento, dato che lo script `rc.shutdown` userà `umount`, che non rimuoverà il punto di mount. Per impedire che nella cartella `/media` rimangano i vecchi punti di mount, una soluzione è quella di effettuare il mount della cartella `/media` come `tmpfs`.

 `/etc/udev/rules.d/11-media-by-label-with-pmount.rules` 
```
KERNEL!="sd[a-z]*", GOTO="media_by_label_auto_mount_end"
ACTION=="add", PROGRAM!="/sbin/blkid %N", GOTO="media_by_label_auto_mount_end"

# Individua l'etichetta
PROGRAM=="/sbin/blkid -o value -s LABEL %N", ENV{dir_name}="%c"
# utilizza basename per to gestire etichette come ../mnt/foo 
PROGRAM=="/usr/bin/basename '%E{dir_name}'", ENV{dir_name}="%c"
ENV{dir_name}=="", ENV{dir_name}="usbhd-%k"

ACTION=="add", ENV{dir_name}!="", RUN+="/bin/su tomk -c '/usr/bin/pmount %N %E{dir_name}'"
ACTION=="remove", ENV{dir_name}!="", RUN+="/bin/su tomk -c '/usr/bin/pumount /media/%E{dir_name}'"
LABEL="media_by_label_auto_mount_end"

```

#### Mount in /mnt; creando un link simbolico in /media

La seguente regola non utilizza l'etichetta per la creazione del punto di mount; invece effettua il mount delle periferiche come usbhd-sdXY in `/mnt` (esempio: /mnt/usbhd-sdb1) e crea un link simbolico in `/media`.

 `/etc/udev/rules.d/11-mnt-auto-mount.rules` 
```
KERNEL!="sd[a-z][0-9]", GOTO="mnt_auto_mount_end"

# Opzioni globali per il comando mount
ACTION=="add", ENV{mount_options}="relatime"
# Opzioni specifiche dei filesystem
ACTION=="add", IMPORT{program}="/sbin/blkid -o udev -p %N"
ACTION=="add", ENV{ID_FS_TYPE}=="vfat|ntfs", ENV{mount_options}="$env{mount_options},utf8,gid=100,umask=002"

# Effettua il mount in /mnt e crea il link simbolico in /media
ACTION=="add", RUN+="/bin/mkdir -p /mnt/usbhd-%k", RUN+="/bin/mount -o $env{mount_options} /dev/%k /mnt/usbhd-%k", RUN+="/bin/ln -s /mnt/usbhd-%k /media/usbhd-%k"

# Effettua la pulizia delle directory alla rimozione della periferica
ACTION=="remove", RUN+="/bin/rm -f /media/usbhd-%k", RUN+="/bin/umount -l /mnt/usbhd-%k", RUN+="/bin/rmdir /mnt/usbhd-%k"

# Uscita
LABEL="mnt_auto_mount_end"

```

#### Mount in /media *solo* se la partizione ha una etichetta

 `/etc/udev/rules.d/11-media-by-label-only-auto-mount.rules` 
```
KERNEL!="sd[a-z][0-9]", GOTO="media_by_label_only_auto_mount_end"

# Importa le informazioni sul Filesystem
IMPORT{program}="/sbin/blkid -o udev -p %N"
ENV{ID_FS_LABEL}=="", GOTO="media_by_label_only_auto_mount_end"

# Opzioni globali per il comando mount 
ACTION=="add", ENV{mount_options}="relatime"
# Opzioni specifiche dei filesystem
ACTION=="add", ENV{ID_FS_TYPE}=="vfat|ntfs", ENV{mount_options}="$env{mount_options},utf8,gid=100,umask=002"

# Effettua il mount della periferica
ACTION=="add", RUN+="/bin/mkdir -p /media/$env{ID_FS_LABEL}", RUN+="/bin/mount -o $env{mount_options} /dev/%k /media/$env{ID_FS_LABEL}"

# Effettua la pulizia delle directory alla rimozione della periferica
ACTION=="remove", ENV{ID_FS_LABEL}!="", RUN+="/bin/umount -l /media/$env{ID_FS_LABEL}", RUN+="/bin/rmdir /media/$env{ID_FS_LABEL}"

# Uscita
LABEL="media_by_label_only_auto_mount_end"

```

#### Mount in /media; usando l'etichetta della partizione se presente; usando ntfs-3g

Ecco un altro esempio, in questo caso viene usato `ntfs-3g` per accedere in lettura e scrittura sui filesystem NTFS:

 `/etc/udev/rules.d/10-my-media-automount.rules` 
```
# vim:enc=utf-8:nu:ai:si:et:ts=4:sw=4:ft=udevrules:
#
# /etc/udev/rules.d/10-my-media-automount.rules

# il controllo inizia da sdb ignorando il disco di sistema
KERNEL!="sd[b-z]*", GOTO="my_media_automount_end"
ACTION=="add", PROGRAM!="/sbin/blkid %N", GOTO="my_media_automount_end"

# importa alcune informazioni utili come variabili
IMPORT{program}="/sbin/blkid -o udev -p %N"

# Individua l'etichetta se esiste, altrimenti ne crea una
ENV{ID_FS_LABEL}!="", ENV{dir_name}="%E{ID_FS_LABEL}"
ENV{ID_FS_LABEL}=="", ENV{dir_name}="usbhd-%k"

# crea la directory in /media
ACTION=="add", RUN+="/bin/mkdir -p '/media/%E{dir_name}'"

# Opzioni globali per il comando mount 
ACTION=="add", ENV{mount_options}="relatime"
# opzioni di mount specifiche per i filesystem (imposta i permessi 777/666 su cartelle/file per ntfs/vfat) 
ACTION=="add", ENV{ID_FS_TYPE}=="vfat|ntfs", ENV{mount_options}="$env{mount_options},gid=100,dmask=000,fmask=111,utf8"

# mount automatico per i filesystem ntfs usando ntfs-3g
ACTION=="add", ENV{ID_FS_TYPE}=="ntfs", RUN+="/bin/mount -t ntfs-3g -o %E{mount_options} /dev/%k '/media/%E{dir_name}'"
# mount automatico per gli altri filesystem
ACTION=="add", ENV{ID_FS_TYPE}!="ntfs", RUN+="/bin/mount -t auto -o %E{mount_options} /dev/%k '/media/%E{dir_name}'"

# Effettua la pulizia delle directory alla rimozione della periferica
ACTION=="remove", ENV{dir_name}!="", RUN+="/bin/umount -l '/media/%E{dir_name}'", RUN+="/bin/rmdir '/media/%E{dir_name}'"

# Uscita
LABEL="my_media_automount_end"

```

#### Mount delle SD card

Le regole sopra possono essere usate anche per il mount automatico delle schede SD, basterà sostituire `sd[a-z][0-9]` con `mmcblk[0-9]p[0-9]`:

 `/etc/udev/rules.d/11-sd-cards-auto-mount.rules` 
```
KERNEL!="mmcblk[0-9]p[0-9]", GOTO="sd_cards_auto_mount_end"

# Opzioni globali per il comando mount
ACTION=="add", ENV{mount_options}="relatime"
# Opzioni specifiche del filesystem 
ACTION=="add", IMPORT{program}="/sbin/blkid -o udev -p %N"
ACTION=="add", ENV{ID_FS_TYPE}=="vfat|ntfs", ENV{mount_options}="$env{mount_options},utf8,gid=100,umask=002"

ACTION=="add", RUN+="/bin/mkdir -p /media/sd-%k", RUN+="/bin/ln -s /media/sd-%k /mnt/sd-%k", RUN+="/bin/mount -o $env{mount_options} /dev/%k /media/sd-%k"
ACTION=="remove", RUN+="/bin/umount -l /media/sd-%k", RUN+="/bin/rmdir /media/sd-%k"
LABEL="sd_cards_auto_mount_end"

```

#### Mount dei CD

Per effettuare l’auto mount dei cd basterà avere installato e configurato uno dei [UDisks wrapper](#UDisks_Wrapper).

**Nota:** Forse questo può essere unito con la sezione Udiscks wrapper.

#### Accedere a Firmware Programmers ed a USB Virtual Comm Devices

La seguente regola consente a normali utenti (appartenenti al gruppo "users") la possibilità di accedere ad [USBtinyISP](http://www.ladyada.net/make/usbtinyisp/) programmatori per micro controllori AVR ed a generici (SiLabs [CP2102](http://www.silabs.com/products/interface/usbtouart)) adattatori da USB a UART. Modificare i permessi secondo le esigenze. Verificato il 11-02-2010.

 `/etc/udev/rules.d/50-embedded_devices.rules` 
```
# USBtinyISP Programmer
SUBSYSTEMS=="usb", ATTRS{idVendor}=="1781", ATTRS{idProduct}=="0c9f", GROUP="users", MODE="0666"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="0479", GROUP="users", MODE="0666"

# USBasp Programmer rules http://www.fischl.de/usbasp/
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="05dc", GROUP="users", MODE="0666"

# Mdfly.com Generic (SiLabs CP2102) 3.3v/5v USB VComm adapter
SUBSYSTEMS=="usb", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", GROUP="users", MODE="0666"

```

### Eseguire all’inserimento di un USB

Consultare la guida riguardante l'[esecuzione di programmi all'inserimento di una pennina USB](/index.php/Execute_on_USB_insert_(Italiano) "Execute on USB insert (Italiano)"), oppure il [il sito dello script wrapper devmon](http://igurublog.wordpress.com/downloads/script-devmon/).

### Mount dei supporti di memoria interni come utente non privilegiato

Se si vuole effettuare il mount di periferiche interne in KDE oppure in GNOME (ma anche in altri Desktop Environment) come utente non privilegiato(senza necessità di inserire la password per elevare i privilegi), basterà creare il seguente file in [PolicyKit](/index.php/PolicyKit "PolicyKit") Local Autority:

 `/etc/polkit-1/localauthority/50-local.d/50-filesystem-mount-system-internal.pkla` 
```
[Mount a system-internal device]
Identity=*
Action=org.freedesktop.udisks.filesystem-mount-system-internal
ResultActive=yes

```

### Marchiare le porte SATA interne come porte eSATA

Se si connette una dock eSATA oppure un qualsiasi adattatore eSATA il sistema riconoscerà queste porte come SATA interne. GNOME e KDE richiederanno quindi la password di root per effettuarne il mount. La seguente regola marchia come eSATA la porta SATA interna specificata. In questo modo un utente normale su GNOME potrà quindi connettere i propri dischi eSata che verranno trattati come dischi USB, senza bisogno di inserire la password di root.

 `/etc/udev/rules.d/10-esata.rules` 
```
DEVPATH=="/devices/pci0000:00/0000:00:1f.2/host4/*", ENV{UDISKS_SYSTEM_INTERNAL}="0"

```

**Nota:** Il valore di DEVPATH può essere ottenuto dopo la connessione del disco eSATA mediante il seguente comando(sostituire `sdb` a seconda delle proprie esigenze):
```
# find /sys/devices/ -name sdb
/sys/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

## Risoluzione di problemi

### Inserire i moduli in blacklist

In rari casi, udev può sbagliarsi e caricare il modulo sbagliato. Per prevenire ciò il modulo in questione può essere inserito in una blacklist.Consultare [blacklisting](/index.php/Blacklisting_(Italiano) "Blacklisting (Italiano)") per maggiori informazioni. Una volta inserito nella blacklist udev non caricherà questo modulo, ne durante la fase di avvio *ne* in caso di inserimento di periferiche hotplug(durante l'inserimento di una pennina USB).

### udevd fallisce all’avvio

Dopo un passaggio ad LDAP oppure dopo un aggiornamento di un sistema LDAP-backend può accadere che `udevd` non si avvii correttamente, lo si nota alla comparsa del messaggio `Starting UDev Daemon`. Questo solitamente è causato da `udevd` che cerca di ottenere un nome da LDAP ma non ci riesce, perché la rete non è ancora attiva. La soluzione consiste nell’assicurarsi che tutti i nomi dei gruppi del sistema siano presenti localmente.

Ottenere l’elenco dei gruppi a cui fa riferimento udev, all’interno delle sue regole, e l’elenco dei gruppi attualmente presenti nel sistema:

```
# fgrep -r GROUP /etc/udev/rules.d/ /lib/udev/rules.d | perl -nle '/GROUP\s*=\s*"(.*?)"/ && print $1;' | sort | uniq > udev_groups
# cut -f1 -d: /etc/gshadow /etc/group | sort | uniq > present_groups

```

Per vedere le differenze, effettuare un `diff` affiancato(side-by-side):

```
# diff -y present_groups udev_groups
...
network                                      <
nobody                                       <
ntp                                          <
optical                                      optical
power                                        |    pcscd
rfkill                                       <
root                                         root
scanner                                      scanner
smmsp                                        < 
storage                                      storage
...

```

In questo caso, il gruppo `pcscd` per qualche ragione non è presente nel sistema. Aggiungere quindi i gruppi mancanti:

```
# groupadd pcscd

```

Assicurarsi anche che le risorse siano bloccate prima di riabilitare LDAP. Nel File `/etc/nsswitch.conf` dovrebbe essere presente questa riga:

```
group: files ldap

```

### Problemi noti relativi all'hardware

#### Le periferiche BusLogic smettono di funzionare e quindi causano un blocco durante la fase di avvio.

Questo è un bug del kernel e non è stato ancora risolto.

#### Periferiche rimovibili non vengono riconosciute come tali

Creare una regola per udev, impostando `UDISKS_SYSTEM_INTERNAL=0`.Per maggiori informazioni consultare le pagine di manuale di udisks.

### Problemi noti relativi al caricamento automatico dei moduli

#### Moduli per lo scaling della frequenza della CPU

L'attuale meccanismo di identificazione del modulo per lo scaling della frequenza non è adeguato, quindi per adesso è stato rimosso dal processo di caricamento automatico dei moduli. Per utilizzare lo [scaling della frequenza della CPU](/index.php/CPU_frequency_scaling_(Italiano) "CPU frequency scaling (Italiano)"), sarà necessario caricare il modulo appropriato esplicitamente all'interno dell'array `MODULES` in `/etc/rc.conf`.

#### Problemi con l'audio o alcuni moduli non vengono caricati automaticamente

Alcuni utenti hanno segnalato questo problema relativo a vecchie configurazioni presenti in `/etc/modprobe.d/sound.conf`. Si consiglia di ripulire il file e riprovare.

**Nota:** A partire da `udev>=171`, il moduli relativi ad OSS (`snd_seq_oss, snd_pcm_oss, snd_mixer_oss`) non vengono caricati automaticamente di default.

#### Ordinamento delle periferiche, schede di rete/audio che cambiano ordine ad ogni avvio

Dato che udev carica i moduli in modo asincrono, questi vengono inizializzati in ordine differente. Questo può causare il cambiamento casuale del loro nome. Ad esempio con due schede di rete, può capitare che il loro ordine venga invertito da `eth0` ad `eth1`.

Un metodo per ordinare le schede di rete è quello di usare una regola che imposti staticamente il nome ad ogni interfaccia di rete. Creare il seguente file per associare al MAC adresss di ogni scheda di rete un determinato nome di interfaccia:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="lan0"
SUBSYSTEM=="net", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="wlan0"

```

Alcune cose da notare:

*   Per ottenere il MAC adress di ogni scheda, usare il seguente comando: `udevadm info -a -p /sys/class/net/<yourdevice>`
*   Assicurarsi di usare caratteri minuscoli per i MAC adress in questa regola. Non funzionerà se si usano caratteri maiuscoli.
*   Alcuni utenti hanno problemi a chiamare le interfacce secondo la vecchia nomenclatura: eth0, eth1 ecc. Provare con nomi come "lan" o "wlan" se si ha questo problema.

Non dimenticare di aggiornare il proprio `/etc/rc.conf` ed ogni altra configurazione che utilizzi la vecchia nomenclatura! .

Un ulteriore metodo per impostare i nomi alle interfacce di rete viene descritto nella [pagina del wiki](/index.php/Configuring_Network_(Italiano)#Nomi_delle_interfacce_differenti "Configuring Network (Italiano)") relativa alla configurazione della rete .

**Nota:** Con una versione recente di udev, questo problema dovrebbe essere risolto automaticamente grazie al programma `/lib/udev/write_net_rules` che esegue lo script `75-persistent-net-generator.rules` che crea il file `70-persistent-net.rules`.

### Problemi noti legati all'uso di Kernel personalizzati

#### Udev non si avvia

Assicurarsi che il kernel in uso sia ad una versione uguale o successiva alla 2.6.32\. Le versioni precedenti non di dispongono degli uevent necessari ad udev per il caricamento automatico dei moduli.

### Periferiche IDE CD/DVD

A partire dalla versione 170 udev non supporta più le periferiche CD-ROM/DVD-ROM, che verranno caricate come periferiche IDE dal modulo `ide_cd_mod` e verranno identificate come `/dev/hd*`. Le periferiche saranno utilizzabili dai tool che accedono direttamente all'hardware, come `cdparanoia`, ma saranno invisibili ad altri programmi come KDE.

Un motivo per cui il modulo `ide_cd_mod` viene caricato piuttosto che altri, come `st_mod` può essere ad esempio che per qualche motivo il modulo `piix` viene caricato dall'initramfs. In questo caso è possibile sostituirlo con `ata_piix` nel proprio `/etc/mkinitcpio.conf`

### Le periferiche ottiche hanno l'ID del gruppo impostato a disk

Se l'ID delle periferiche ottiche è impostato su `disk` e si vuole cambiare in `optical` sarà necessario creare una regola personalizzata di udev:

 `/etc/udev/rules.d` 
```
# permissions for IDE CD devices
SUBSYSTEMS=="ide", KERNEL=="hd[a-z]", ATTR{removable}=="1", ATTRS{media}=="cdrom*", GROUP="optical"

# permissions for SCSI CD devices
SUBSYSTEMS=="scsi", KERNEL=="s[rg][0-9]*", ATTRS{type}=="5", GROUP="optical"
```

## Altre risorse

*   [Homepage di Udev(in inglese)](http://www.kernel.org/pub/linux/utils/kernel/hotplug/udev.html)
*   [Una introduzione ad Udev(in inglese)](http://www.linux.com/news/hardware/peripherals/180950-udev)
*   [Mailing list informativa di Udev](http://vger.kernel.org/vger-lists.html#linux-hotplug)