Articoli correlati

*   [Codecs](/index.php/Codecs "Codecs")
*   [MPlayer](/index.php/MPlayer "MPlayer")
*   [dvdbackup](/index.php/Dvdbackup "Dvdbackup")
*   [MEncoder](/index.php/MEncoder "MEncoder")

Da [wikipedia](https://en.wikipedia.org/wiki/Optical_disc_drive "wikipedia:Optical disc drive")

	*In informatica, una unità di disco ottico (ODD), è un disco che utilizza la luce laser o onde elettromagnetiche all'interno, o vicino lo spettro della luce visibile come parte del processo di lettura o scrittura di dati su o da dischi ottici. Alcune unità possono leggere solo i dischi, ma le recenti unità sono comunemente lettori e registratori, chiamati anche masterizzatori. Compact disc, DVD e dischi Blu-ray sono comuni tipi di supporti ottici che possono essere letti e registrati da tali unità. Unità ottica è il nome generico; le unità sono solitamente descritte come "CD", "DVD " o "Blu-ray ", seguito da "Lettore", "Masterizzatore", ecc.*

## Contents

*   [1 Masterizzare](#Masterizzare)
    *   [1.1 Installare le utility per la masterizzazione](#Installare_le_utility_per_la_masterizzazione)
    *   [1.2 Creare un immagine ISO da un file esistente sul disco rigido](#Creare_un_immagine_ISO_da_un_file_esistente_sul_disco_rigido)
    *   [1.3 Montare un'immagine ISO](#Montare_un.27immagine_ISO)
    *   [1.4 Convertire immagini img/ccd in immagini ISO](#Convertire_immagini_img.2Fccd_in_immagini_ISO)
    *   [1.5 Conoscere il nome del drive ottico](#Conoscere_il_nome_del_drive_ottico)
    *   [1.6 Lettura di un'immagine ISO da un CD, DVD o BD](#Lettura_di_un.27immagine_ISO_da_un_CD.2C_DVD_o_BD)
    *   [1.7 Formattare CD-RW e DVD-RW](#Formattare_CD-RW_e_DVD-RW)
    *   [1.8 Masterizzare una immagine ISO su un CD, DVD o BD](#Masterizzare_una_immagine_ISO_su_un_CD.2C_DVD_o_BD)
    *   [1.9 Verificare l'immagine ISO masterizzata](#Verificare_l.27immagine_ISO_masterizzata)
    *   [1.10 ISO 9660 e masterizzazione On-The-Fly](#ISO_9660_e_masterizzazione_On-The-Fly)
    *   [1.11 Multi-sessione](#Multi-sessione)
        *   [1.11.1 Multisessione con wodim](#Multisessione_con_wodim)
        *   [1.11.2 Multisessione con growisofs](#Multisessione_con_growisofs)
        *   [1.11.3 Multisessione con xorriso](#Multisessione_con_xorriso)
    *   [1.12 Gestione dei difetti nei Blu-ray disk](#Gestione_dei_difetti_nei_Blu-ray_disk)
    *   [1.13 Masterizzare un CD audio](#Masterizzare_un_CD_audio)
    *   [1.14 Masterizzazione di un bin/cue](#Masterizzazione_di_un_bin.2Fcue)
        *   [1.14.1 TOC/CUE/BIN per dischi in modalità mista](#TOC.2FCUE.2FBIN_per_dischi_in_modalit.C3.A0_mista)
    *   [1.15 Problemi con i back-end di masterizzazione](#Problemi_con_i_back-end_di_masterizzazione)
    *   [1.16 Masterizzare CD/DVD con una interfaccia grafica](#Masterizzare_CD.2FDVD_con_una_interfaccia_grafica)
        *   [1.16.1 Nero Linux](#Nero_Linux)
*   [2 Riproduzione di DVD](#Riproduzione_di_DVD)
    *   [2.1 Requisiti](#Requisiti)
    *   [2.2 Lettori DVD](#Lettori_DVD)
        *   [2.2.1 MPlayer](#MPlayer)
        *   [2.2.2 VLC](#VLC)
            *   [2.2.2.1 Predefinito in GNOME](#Predefinito_in_GNOME)
        *   [2.2.3 xine](#xine)
*   [3 DVD ripping](#DVD_ripping)
    *   [3.1 dvdbackup](#dvdbackup)
    *   [3.2 dvd::rip](#dvd::rip)
    *   [3.3 FFmpeg](#FFmpeg)
    *   [3.4 HandBrake](#HandBrake)
    *   [3.5 MEncoder](#MEncoder)
    *   [3.6 Hybrid](#Hybrid)
    *   [3.7 DVD-VR](#DVD-VR)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 K3b e l'errore sul locale](#K3b_e_l.27errore_sul_locale)
    *   [4.2 Brasero non riesce a trovare dischi vergini](#Brasero_non_riesce_a_trovare_dischi_vergini)
    *   [4.3 Brasero non riesce a normalizzare CD audio](#Brasero_non_riesce_a_normalizzare_CD_audio)
    *   [4.4 VLC: Error "... could not open the disc /dev/dvd"](#VLC:_Error_.22..._could_not_open_the_disc_.2Fdev.2Fdvd.22)
    *   [4.5 Unità DVD rumorosa](#Unit.C3.A0_DVD_rumorosa)
    *   [4.6 La riproduzione non funziona con il nuovo computer (nuovo dispositivo DVD)](#La_riproduzione_non_funziona_con_il_nuovo_computer_.28nuovo_dispositivo_DVD.29)
    *   [4.7 Nessuno dei programmi elencati è in grado di estrarre/codificare un DVD sul mio disco rigido!](#Nessuno_dei_programmi_elencati_.C3.A8_in_grado_di_estrarre.2Fcodificare_un_DVD_sul_mio_disco_rigido.21)
    *   [4.8 I log del programma con interfaccia grafica indica problemi con il programma di backend](#I_log_del_programma_con_interfaccia_grafica_indica_problemi_con_il_programma_di_backend)
        *   [4.8.1 Caso particolare : Medium error / Write error](#Caso_particolare_:_Medium_error_.2F_Write_error)
*   [5 Altre risorse](#Altre_risorse)

## Masterizzare

Il processo di masterizzazione delle unità disco ottico è costituito dal creare, o ottenere, una immagine e scriverla su di un supporto ottico. L'immagine può essere in linea di principio qualsiasi file di dati. Se si desidera montare il media risultante, allora di solito si tratta di un file di immagine del filesystem ISO 9660\. CD audio e multi-media sono spesso masterizzanti partendo da un file BIN, sotto il controllo di un file TOC, o un file CUE, che descrive il tracciato desiderato.

### Installare le utility per la masterizzazione

Se si desidera utilizzare i programmi con una interfaccia grafica, seguire [questo link per l' elenco di programmi con interfaccia grafica](#Masterizzare_CD.2FDVD_con_una_interfaccia_grafica).

I programmi elencati qui sono i back end che vengono utilizzati dalla maggior parte dei programmi con interfaccia grafica gratuiti per CD, DVD e BD. Sono orientati alla linea di comando. Gli utenti che utilizzano programmi con interfaccia grafica possono utilizzarli quando si tratta di risolvere dei problemi, o per la creazione di script per le attività di masterizzazione.

È necessario avere almeno un programma per la creazione di immagini di filesystem, e un programma che sia in grado di masterizzare i dati sul tipo di supporto desiderato .

Programmi disponibili per la creazione di immagini ISO 9660 sono:

*   `genisoimage` dal pacchetto [cdrkit](https://www.archlinux.org/packages/?name=cdrkit)
*   `mkisofs` dal pacchetto [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   `xorriso` e `xorrisofs`, dal pacchetto [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

La scelta tradizionale è `genisoimage`.

Programmi disponibili per la masterizzazione su supporti sono :

*   `cdrdao` dal pacchetto [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) (solo CD, solo TOC/CUE/BIN)
*   `cdrecord` dal pacchetto [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   `cdrskin` dal pacchetto [libburn](https://www.archlinux.org/packages/?name=libburn)
*   `growisofs` dal pacchetto [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) (solo DVD e BD)
*   `wodim` dal pacchetto [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) (solo CD, deprecato per DVD)
*   `xorriso` e `xorrecord` dal pacchetto [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

Le scelte tradizionali sono `wodim` per CD e `growisofs` per DVD e Blu-ray Disk. Per growisofs e BD-R vedere la soluzione bug qui sotto. Per la scrittura di file TOC/CUE/BIN su CD, installare `cdrdao`.

I programmi ad interfaccia grafica gratuiti per CD, DVD, e BD dipendono almeno da uno dei suddetti pacchetti.

I programmi `genisoimage`, `mkisofs` e `xorrisofs` supportano tutti e tre le opzioni di genisoimage che sono indicati in questo documento.

I programmi `cdrecord`, `cdrskin` e `wodim` supportano tutti e tre le opzioni di wodim mostrate. Il programma `xorrecord` supporta quelle che non riguardano i CD audio.

**Nota:**

*   I pacchetti [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) e [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) andranno in conflitto tra loro, installare solo uno di questi.
*   Assicurarsi di avere la possibilità di creare un pacchetto utilizzando [makepkg](/index.php/Makepkg "Makepkg") ed instalalrlo con [pacman](/index.php/Pacman_(Italiano) "Pacman (Italiano)"). I wrapper di pacman possono risolvere cdrkit allo stesso modo.

### Creare un immagine ISO da un file esistente sul disco rigido

Il modo più semplice per creare una immagine ISO, facendosi aiutare da *genisoimage*, è quello di copiare i file necessari in una cartella `./for_iso` e da successivamente:

```
$ genisoimage -V "ARCHIVE_2013_07_27" -J -r -o isoimage.iso ./for_iso

```

Il significato delle opzioni è :

	-V

	Dà al filesystem un nome che probabilmente apparirà come punto di montaggio se il media viene montato automaticamente. Le specifiche ISO lasciano al massimo solo 32 caratteri, i quali comprendono dalla "A" alla "Z", da "0" a "9", e il carattere speciale "_".

	-J

	Prepara i nomi fino ad un massimo di 64 caratteri UTF-16 per i lettori di MS-Windows. Denominato "Joliet".

	-joliet-long

	Permetterebbe fino a 103 caratteri UTF-16 per i lettori di MS-Windows. Non conforme alle specifiche Joliet.

	-r

	Prepara i nomi fino a 255 caratteri per i lettori Unix e conferisce il permesso di lettura per tutti. Denominato "Rock Ridge".

	-o

	Consente di impostare il percorso del file per l'immagine ISO risultante.

Si piò lasciare che genisoimage raccolga i file e le directory da vari percorsi :

```
 $ genisoimage -V "BACKUP_2013_07_27" -J -r -o backup_2013_07_27.iso \
  -graft-points \
  /photos=/home/utente/foto \
  /mail=/home/utente/mail \
  /photos/holidays=/home/utente/vacanze/foto

```

	-graft-points

	Abilita il riconoscimento dei *pathspecs* che consistono di un indirizzo di destinazione nel filesystem ISO (ad esempio */photos*) e un indirizzo di origine sul disco rigido (ad esempio */home/utente/foto*). Entrambi sono separati da un carattere `=`.

Quindi questo esempio mette le directory presenti sul disco `/home/utente/foto`, `/home/utente/mail` e `/home/utente/vacanze/foto` rispettivamente nell'immagine ISO come directory `/photos`, `/mail` e `/photos/holidays/`.

O programmi `mkisofs` e `xorrisofs` accettano le stesse opzioni. Per un backup sicuro, si consideri di utilizzare `xorrisofs` con l'opzione `-for_backup`, che registra eventuali ACL e memorizza un checksum MD5 per ogni file di dati.

Vedere i manuali dei programmi ISO 9660 per ulteriori informazioni circa le loro opzioni : [genisoimage](http://linux.die.net/man/1/genisoimage) [mkisofs](http://cdrecord.berlios.de/private/man/cdrecord/mkisofs.8.html) [xorrisofs](http://www.gnu.org/software/xorriso/man_1_xorrisofs.html)

### Montare un'immagine ISO

Per verificare se l'immagine ISO è corretta , è possibile montare (come root ) :

```
# mount -t iso9660 -o ro,loop=/dev/loop0 cd_image /cdrom

```

È necessario caricare prima il modulo loop :

```
# modprobe loop

```

Non dimenticare di smontare l'immagine quando il controllo dell'immagine è stato effettuato :

```
# umount /cdrom

```

Si veda [Mounting images as user](/index.php/Mounting_images_as_user "Mounting images as user") per il montaggio senza privilegi di root.

### Convertire immagini img/ccd in immagini ISO

Per convertire un'immagine `img`/`CCD`, è possibile utilizzare [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso) :

```
$ ccd2iso ~/image.img ~/image.iso

```

### Conoscere il nome del drive ottico

Per il resto di questa sezione il nome del dispositivo di registrazione si presume sia `/dev/cdrw`.

Controllarlo con

```
 $ wodim dev=/dev/cdrw -checkdrive

```

che dovrebbe segnalare "Vendor_info" e "Identification" del drive. Eventualmente potrebbe essere `/dev/sr0`.

Se nessuna unità viene trovata, controllare se ogni `/dev/sr*` esiste e se offrono il permesso di lettura e scrittura (`rw-`) a voi o al vostro gruppo.

Se `/dev/sr*` non esiste provare

```
# modprobe sr_mod

```

### Lettura di un'immagine ISO da un CD, DVD o BD

È necessario determinare la dimensione del file system ISO prima di copiarlo sul disco rigido . La maggior parte dei tipi di supporto forniscono più dati di quanto è stato scritto per loro con la più recente esecuzione di masterizzazione.

Utilizzare il programma `isosize` dal pacchetto [util-linux](https://www.archlinux.org/packages/?name=util-linux) per ottenere le dimensioni dell'immagine.

```
 $ blocks=$(expr $(isosize /dev/cdrw) / 2048)

```

Controllare se il numero ottenuto di blocchi è plausibile.

 `$ echo "That would be $(expr $blocks / 512) MB"` 
```
Sarebbe 589 MB

```

Quindi copiare l'importo determinato di dati dal media al disco rigido :

```
 $ dd if=/dev/cdrw of=isoimage.iso bs=2048 count=$blocks

```

Omettere `count=$blocks` se non determinare il formato. Probabilmente otterrete più dati del necessario.

Se il media originario era avviabile, la copia sarà un'immagine avviabile. Potete usarlo come pseudo CD per una macchina virtuale o masterizzarlo su un supporto ottico, che dovrebbe poi diventare avviabile.

### Formattare CD-RW e DVD-RW

I supporti CD-RW devono essere cancellati prima di poter scrivere sopra i dati precedentemente registrati. Questo viene fatto tramite :

```
 $ wodim -v dev=/dev/cdrw blank=fast

```

I supporti DVD-RW non formattati hanno bisogno dello stesso trattamento prima del loro riutilizzo. Ma una formattazione veloce li priva della capacità di multi-sessione e registrazione dei flussi di lunghezza imprevisti. Così si dovrebbe applicare :

```
 $ dvd+rw-format -blank=full /dev/cdrw

```

`dvd+rw-format` fa parte del pacchetto [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools). Comandi alternativi sono :

```
 $ cdrecord -v dev=/dev/cdrw blank=all
 $ cdrskin -v dev=/dev/cdrw blank=all
 $ xorriso -outdev /dev/cdrw -blank as_needed

```

I supporti DVD-RW formattati possono essere sovrascritti senza tale cancellazione. Quindi prendere in considerazione di applicarlo una volta nella loro vita

```
 $ dvd+rw-format -force /dev/cdrw

```

Comandi alternativi sono :

```
 $ cdrskin -v dev=/dev/cdrw blank=format_overwrite
 $ xorriso -outdev /dev/cdrw -format as_needed

```

Tutti gli altri media sono o scrivibili una volta sola (CD-R, DVD-R, DVD+R, BD-R) o sono riscrivibili senza la necessità di formattare (DVD-RAM, DVD+RW, BD-RE).

### Masterizzare una immagine ISO su un CD, DVD o BD

Per masterizzare un file immagine ISO prontamente preparato (`isoimage.iso`), su un supporto ottico, eseguire:

per CD :

```
$ wodim -v -sao dev=/dev/cdrw isoimage.iso

```

Se `/dev/cdrw` non viene trovato è possibile provare con `/dev/sr0` assicurandosi che il modulo necessario sia attivo con

```
$ modprobe sr_mod

```

Per DVD o BD :

```
$ growisofs -dvd-compat -Z /dev/cdrw isoimage.iso

```

I programmi `cdrecord`, `cdrskin` e `xorrecord` possono essere utilizzati su tutti i tipi di media con le opzioni indicate con `wodim`.

**Nota:**

*   Assicurarsi che il supporto non sia montato quando si inizia a scrivere. Il montaggio può avvenire automaticamente se il media contiene un filesystem leggibile. Nel migliore dei casi si impedisce ai programmi di masterizzazione di utilizzare il dispositivo masterizzato. Nel peggiore dei casi non vi sarà nessuna masterizzazione perché le operazioni di lettura disturbato l'unità. Quindi, in caso di dubbio, smontare con:

```
 # umount /dev/cdrw

```

*   `growisofs` ha un piccolo bug con supporti BD-R vuoti. Si emette un messaggio di errore dopo la masterizzazione. Programmi come `k3b` quindi non masterizzano correttamente tali media. Per evitare questo :
    *   Formattare il BD-r vuoto con `dvd+rw-format /dev/cdrw` prima di sottoporlo al growisofs
    *   oppure utilizzare l'opzione per growisofs `-use-the-force-luke=spare:none`

### Verificare l'immagine ISO masterizzata

È possibile verificare l'integrità del media masterizzato per assicurarsi che non contenga errori. Espellere sempre il media e reinserirlo prima di verificarlo. Il kernel sarà in grado di riconoscere il nuovo contenuto da solo dopo tale reinserimento.

In primo luogo calcolare l'md5sum dell'immagine ISO originale :

 `$ md5sum isoimage.iso` 
```
 e5643e18e05f5646046bb2e4236986d8 isoimage.iso

```

Successivamente calcolare il checksum MD5 del file system ISO sul media. Anche se alcuni tipi di supporto forniscono esattamente la stessa quantità di dati , come sono stati sottoposti al programma di masterizzazione, molti altri aggiungono una dimensione fittizia quando viene letto. Così si dovrebbe limitare a leggere la dimensione del file di immagine ISO.

```
 $ blocks=$(expr $(du -b isoimage.iso | awk '{print $1}') / 2048)

```
 `$ dd if=/dev/cdrw bs=2048 count=$blocks | md5sum` 
```
  43992+0 records in
  43992+0 records out

```

Entrambe le piste dovrebbero produrre la stessa somma MD5 (qui: `e5643e18e05f5646046bb2e4236986d8`). Altrimenti si avrà probabilmente anche un messaggio di errore di I/O dall'esecuzione di `dd`. `dmesg` potrebbe poi aiutarvi sugli errori SCSI e sui numeri di blocco, se siete interessati.

### ISO 9660 e masterizzazione On-The-Fly

Non è necessario memorizzare un filesystem ISO sul disco rigido prima di scriverlo sui supporti ottici. Solo i vecchi lettori CD o computer molto vecchi potrebbero subire errori di masterizzazione in caso di Buffer del disco vuoto.

Se si omette l'opzione `-o` da `genisoimage`, allora scriverà l'immagine ISO con un output standard. Questo può essere convogliato dentro lo standard input dei programmi di masterizzazione.

```
 $ genisoimage -V "ARCHIVE_2013_07_27" -J -r ./for_iso | \
  wodim -v dev=/dev/cdrw -waiti -

```

L'opzione `-waiti` non è realmente necessaria. Previene `wodim` dalla scrittura al media prima che `genisoimage` inizi la sua produzione. Ciò consentirebbe a `genisoimage` di leggere il media senza disturbare una già avviata masterizzazione in atto. Vedere la sezione successiva relativa a multi-sessione.

Su DVD e BD si può lasciare che `growisofs` gestisca `genisoimage` al posto vostro, per masterizzare on-the-fly.

```
$ export MKISOFS="genisoimage"

```

```
$ growisofs -Z /dev/cdrw -V "ARCHIVE_2013_07_27" -r -J ./for_iso

```

### Multi-sessione

Una multi-sessione ISO 9660, significa che un media con filesystem leggibile è ancora scrivibile al suo primo indirizzo di blocco non utilizzato, e che un nuovo albero di directory ISO viene scritto su questa parte non utilizzata. Il nuovo albero di directory è accompagnato dai blocchi che contengono i file di dati appena aggiunti o sovrascritti . I blocchi di file di dati, che devono rimanere nel vecchio albero ISO, non verranno scritti nuovamente.

Linux e molti altri sistemi operativi montano l'albero delle directory sul supporto durante l'ultima sessione. L'albero più giovane mostra normalmente anche i file delle sessioni più vecchie.

#### Multisessione con wodim

CD-R e CD-RW possono continuare ad essere scritti (in gergo "appendibili") se è stata utilizzato wodim con l'opzione `-multi` :

```
 $ wodim -v -multi dev=/dev/cdrw isoimage.iso

```

Poi si può indagare il media per i parametri della sessione successiva :

```
$ m=$(wodim dev=/dev/cdrw -msinfo)

```

Con l'aiuto di questi parametri e del supporto leggibile nel lettore è possibile produrre la sessione ISO aggiuntiva :

```
$ genisoimage -M /dev/cdrw -C "$m" \
   -V "ARCHIVE_2013_07_28" -J -r -o session2.iso ./more_for_iso

```

Infine aggiungere la sessione al media e mantenerlo ancora una volta appendibile

```
 $ wodim -v -multi dev=/dev/cdrw session2.iso

```

I programmi `cdrskin` e `xorrecord` fanno questo anche con DVD-R, DVD+R, BD-R e DVD-RW non formattato. Il programma `cdrecord` effettua una multi-sessione con almeno DVD-R e DVD-RW. Naturalmente tutti sono in grado di farlo con supporti CD-R e CD-RW.

La maggior parte dei tipi di supporti riutilizzabili non registrano una cronologia della sessione che sarebbe riconoscibile per un kernel di montaggio. Ma con la ISO 9660 è possibile ottenere l'effetto multi-sessione, anche su tali dispositivi.

`growisofs` e `xorriso` posono farlo nascondendo la maggior parte della complessità.

#### Multisessione con growisofs

`growisofs` è un programma molto avanzato e la maggior parte dei suoi argomenti è compatibile con `mkisofs`. Vedi sopra gli esempi di `genisoimage`. Esso vieta l'opzione `-o` e disapprova l'opzione `-C`. Per impostazione predefinita, viene utilizzato il programma installato denominato *mkisofs*. Si può lasciarlo o sceglierne un altro impostando variabile ambientale `mkisofs`.

```
$ export MKISOFS="genisoimage"

```

```
$ export MKISOFS="xorrisofs"

```

Il desiderio di iniziare con un nuovo filesystem ISO sul supporto ottico è espresso dall'opzione `-Z`

```
$ growisofs -Z /dev/cdrw -V "ARCHIVE_2013_07_27" -r -J ./for_iso

```

Il desiderio di aggiungere più file come una nuova sessione di un filesystem ISO esistente, è espresso dall'opzione `-M`

```
$ growisofs -M /dev/cdrw -V "ARCHIVE_2013_07_28" -r -J ./more_for_iso

```

Per i dettagli vedere il [growisofs(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/growisofs.1) manuale e la documentazione di `genisoimage`, `mkisofs`, `xorrisofs`.

#### Multisessione con xorriso

`xorriso` necessita di iniziare con un nuovo filesystem ISO da un dispositivo ottico vuoto. Quindi è opportuno svuotarlo se contiene dati. Il comando `-blank as_needed` si applica a tutti i tipi di supporti riutilizzabili e anche di immagini ISO in file di dati sul disco rigido. Non causa errore se applicato per una scrittura su una unica unità media vuota.

```
$ xorriso -outdev /dev/cdrw -blank as_needed \
          -volid "ARCHIVE_2013_07_27" -joliet on -add ./for_iso --

```

Su un media non-vuoto riscrivibile, xorriso accoda i file del disco più recenti se il comando `-dev` viene usato al posto di `-outdev`. Naturalmente, nessun comando `-blank` necessità di essere usato qui.

```
 $ xorriso -dev /dev/cdrw \
          -volid "ARCHIVE_2013_07_28" -joliet on -add ./more_for_iso --

```

Per maggiori dettagli vedere il [manuale](http://www.gnu.org/software/xorriso/man_1_xorriso.html) e nello specifico i suoi [esempi](http://www.gnu.org/software/xorriso/man_1_xorriso.html#EXAMPLES)

### Gestione dei difetti nei Blu-ray disk

BD-RE e supporti BD-R formattati sono normalmente scritti con la gestione dei difetti abilitata. Questa funzione legge i blocchi scritti mentre sono ancora memorizzati nel buffer dell'unità. In caso di scarsa qualità di lettura dei blocchi vengono scritti di nuovo, o reindirizzati alla *Spare Area* in cui i dati vengono memorizzati in blocchi di sostituzione.

Questo controllo di lettura riduce la velocità di scrittura al massimo alla metà della velocità nominale del masterizzatore e del supporto BD. A volte anche in modo peggiore. L'uso continuo della *Spare Area* provoca lunghi ritardi durante le operazioni di lettura. Quindi l'opzione *Defect Management* non è sempre auspicabile.

`cdrecord` non formatta BD-R. Però Non ha alcun mezzo per prevenire il *Defect Management* sui media BD-RE.

`growisofs` formatta i BD-R di default. Questo può essere prevenuta con l'opzione `-use-the-force-luke=spare:none`. Anch'esso non ha alcun mezzo per prevenire il *Defect Management* sui media BD-RE.

`cdrskin`, `xorriso` e `xorrecord` non formattano BD-R per impostazione predefinita. Sono in grado di farlo rispettivamente con `cdrskin blank=format_if_needed`, `xorriso -format as_needed` e `xorrecord blank=format_overwrite`.

Questi tre programmi possono disabilitare la gestione ei difetti sui BD-RE e BD-R già formattati, rispettivamente tramite i comandi `cdrskin stream_recording=on`, `xorriso -stream_recording on` e `xorrecord stream_recording=on`.

### Masterizzare un CD audio

Crea le tracce audio e memorizzarle come file non compressi, 16 -bit stereo WAV. Per convertire i file MP3 in WAV, assicurarsi che il pacchetto [lame](https://www.archlinux.org/packages/?name=lame) sia installato, entrate con `cd` nella la Directoy contenente i file MP3, ed eseguire :

```
$ for i in *.mp3; do lame --decode "$i" "$(basename "$i" .mp3)".wav; done

```

Nel caso in cui si verifica un errore quando si tenta di masterizzare i file WAV convertiti con lame provare la decodifica con [mpg123](https://www.archlinux.org/packages/?name=mpg123) :

```
$ for i in *.mp3; do mpg123 --rate 44100 --stereo --buffer 3072 --resync -w $(basename $i .mp3).wav $i; done

```

Nominare i file audio in ordine alfabetico in modo tale che siano inclusi nell'ordine dei brani da voi desiderati, ad esempio `01.wav`, `02.wav`, `03.wav`, ecc... Utilizzare il seguente comando per simulare la masterizzazione dei file wav su un CD audio :

```
$ wodim -dummy -v -pad speed=1 dev=/dev/cdrw -dao -swab *.wav

```

Nel caso in cui si rilevano errori o tracce vuote come :

```
Track 01: audio    0 MB (00:00.00) no preemp pad

```

Provare un altro decoder (ad es mpg123) o provare a utilizzare cdrecord dal pacchetto [cdrtools](https://www.archlinux.org/packages/?name=cdrtools).

Si noti che [cdrkit](https://www.archlinux.org/packages/?name=cdrkit) contiene anche un comando cdrecord, ma è solo un link simbolico a *wodim*.

Se avete avuto esito positivo allora si può togliere il flag `-dummy` e masterizzare realmente il CD.

Per testare il nuovo CD audio , usa [MPlayer](/index.php/MPlayer "MPlayer") :

```
$ mplayer cdda://

```

### Masterizzazione di un bin/cue

Per masterizzare un immagine bin/cue eseguire :

```
$ cdrdao write --device /dev/cdrw image.cue

```

#### TOC/CUE/BIN per dischi in modalità mista

Le immagini ISO memorizzano solo una singola traccia di dati. Se si desidera creare un'immagine di un disco in modalità mista (tenere traccia dei dati con più tracce audio), bisognerà creare un'accoppiata `TOC/BIN`:

```
 $ cdrdao read-cd --read-raw --datafile IMAGE.bin --driver generic-mmc:0x20000 --device /dev/cdrom IMAGE.toc

```

Alcuni software supportano solo accoppiate `CUE/BIN`, si dovrà quindi creare un foglio `CUE` con `toc2cue` (come parte di `cdrdao`):

```
$ toc2cue IMAGE.toc IMAGE.cue

```

### Problemi con i back-end di masterizzazione

In caso di problemi , si può chiedere per consigliare a mailing list [cdwrite@other.debian.org](mailto:cdwrite@other.debian.org). O chiedere consigli agli indirizzi di posta elettronica di supporto, alcuni sono elencati verso la fine della pagina di manuale del programma.

Elencare le righe di comando utilizzate, il tipo di supporto (ad esempio, CD-R, DVD+RW, ... ), ed i sintomi riscontrati (messaggi di programma, delusa aspettativa utente, ...).

Si potrà eventualmente ottenere la versione di rilascio più recente, o di sviluppo del programma interessato, e vi sarà chiesto di effettuare dei test. Ma la risposta potrebbe anche essere, che l'unità non ama in modo particolare il media utilizzato.

### Masterizzare CD/DVD con una interfaccia grafica

[Wikipedia:Comparison of disc authoring software](https://en.wikipedia.org/wiki/Comparison_of_disc_authoring_software "wikipedia:Comparison of disc authoring software")

Ci sono diverse applicazioni disponibili per masterizzare CD/DVD in un ambiente grafico.

*   **[AcetoneISO](https://en.wikipedia.org/wiki/AcetoneISO "wikipedia:AcetoneISO")** — Strumento "tutto in uno" per la gestione di file .iso (supporta BIN, MDF, NRG, IMG, DAA, DMG, CDI, B5I, BWI, PDI and ISO)

	[http://sourceforge.net/projects/acetoneiso](http://sourceforge.net/projects/acetoneiso) || [acetoneiso2](https://www.archlinux.org/packages/?name=acetoneiso2)

*   **BashBurn** — Leggero strumento per masterizzare CD/DVD da terminale provvisto di un menu

	[http://bashburn.dose.se/](http://bashburn.dose.se/) || [bashburn](https://www.archlinux.org/packages/?name=bashburn)

*   **[Brasero](https://en.wikipedia.org/wiki/Brasero_(software) "wikipedia:Brasero (software)")** — Applicazione di masterizzazione su disco per il desktop GNOME che è stato progettato per essere il più semplice possibile. Parte di [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/)

	[http://projects.gnome.org/brasero/](http://projects.gnome.org/brasero/) || [brasero](https://www.archlinux.org/packages/?name=brasero)

*   **cdw** — Frontend Ncurses per cdrecord, mkisofs, growisofs, dvd+rw-mediainfo, dvd+rw-format, xorriso

	[http://cdw.sourceforge.net/](http://cdw.sourceforge.net/) || [cdw](https://aur.archlinux.org/packages/cdw/)

*   **[GnomeBaker](https://en.wikipedia.org/wiki/GnomeBaker "wikipedia:GnomeBaker")** — Applicazione per masterizzare CD/DVD ricco di funzionalità, per il desktop GNOME

	[http://gnomebaker.sourceforge.net/](http://gnomebaker.sourceforge.net/) || [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)

*   **Graveman** — Applicazione per masterizzare CD/DVD basato sulle GTK. Si richiede la configurazione per puntare a dispositivi corretti

	[http://graveman.tuxfamily.org/](http://graveman.tuxfamily.org/) || [graveman](https://aur.archlinux.org/packages/graveman/)

*   **[isomaster](https://en.wikipedia.org/wiki/ISO_Master "wikipedia:ISO Master")** — Editor di immagini ISO

	[http://littlesvr.ca/isomaster](http://littlesvr.ca/isomaster) || [isomaster](https://aur.archlinux.org/packages/isomaster/)

*   **[K3b](https://en.wikipedia.org/wiki/K3b "wikipedia:K3b")** — Applicazione per masterizzare CD/DVD ricco di funzionalità e semplice da usare, basato su Kdelibs

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **[X-CD-Roast](https://en.wikipedia.org/wiki/X-CD-Roast "wikipedia:X-CD-Roast")** — Leggero frontend per cdrtools, per scrivere su CD e DVD

	[http://www.xcdroast.org/](http://www.xcdroast.org/) || [xcdroast](https://aur.archlinux.org/packages/xcdroast/)

*   **Xfburn** — Semplice frontend alle librerie libburnia con supporto per CD/DVD(-RW), immagini ISO e BurnFree

	[http://goodies.xfce.org/projects/applications/xfburn](http://goodies.xfce.org/projects/applications/xfburn) || [xfburn](https://www.archlinux.org/packages/?name=xfburn)

#### Nero Linux

Nero Linux è una suite di masterizzazione commerciale sviluppata dai creatori di Nero per Windows - Nero AG. Il più grande vantaggio di Nero Linux è la sua interfaccia che simile alla versione di windows. Quindi, gli utenti che migrano da tale sistema potrebbero trovarlo facile da usare. La versione per Linux ora include Nero Express, una procedura guidata che porta gli utenti passo passo attraverso il processo di masterizzazione di CD e DVD, gli utenti che provengono da windows avranno già familiarità con questo metodo. Un'altra novità della versione 4 è la gestione dei difetti dei dischi Blu-ray, l'integrazione di Isolinux per la creazione di mezzi di comunicazione e il supporto per Musepack e formati audio AIFF avviabili.

Nero Linux 4 viene venfuto al dettaglio per £17,99 con una versione di prova gratuita disponibile.

*   [Nero Linux 4](http://www.nero.com/enu/linux4.html)
*   [nerolinux](https://aur.archlinux.org/packages/nerolinux/) pacchetto [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)")

Nero Linux offre alcune caratteristiche, come :

*   Facile, interfaccia utente in stile wizard per la masterizzazione guidata di Nero Linux Express 4
*   Pieno supporto alla Masterizzazione dei Blu-ray
*   Supporta la masterizzazione di CD audio (CD-DA), ISO 9660 (supporto Joliet), CD-Text, ISOLINUX avviabile, dischi multi-sessione, DVD-Video e miniDVD, supporto a DVD Double Layer.

**Nota:** Per Nero Linux è necessario caricare il modulo `sg` al momento del boot. Mettere un file omonimo in `/etc/modules-load.d`: `/etc/modules-load.d/sg.config` 
```
sg

```
Dopo gli utlimi aggiornamenti il modulo sg non era più automaticamente caricato e Nero ne ha bisogno.

## Riproduzione di DVD

Un [DVD](https://en.wikipedia.org/wiki/it:DVD "wikipedia:it:DVD"), conosciuto anche come Digital Versatile Disc o Digital Video Disc , è un formato di supporto di archiviazione disco ottico utilizzato per il video e la memorizzazione dei dati .

### Requisiti

Se si desidera riprodurre i DVD criptati , è necessario installare i pacchetti libdvd* :

*   [libdvdread](https://www.archlinux.org/packages/?name=libdvdread)
*   [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)
*   [libdvdnav](https://www.archlinux.org/packages/?name=libdvdnav)

Inoltre, è necessario installare un software per il lettore. I più diffusi lettori DVD sono [MPlayer](/index.php/MPlayer "MPlayer"), [xine](https://en.wikipedia.org/wiki/it:Xine "wikipedia:it:Xine") e [VLC](https://en.wikipedia.org/wiki/VLC "wikipedia:VLC").

**Suggerimento:** Gli utenti possono avere bisogno di appartenere al [gruppo](/index.php/Users_and_groups_(Italiano) "Users and groups (Italiano)") `optical` per essere in grado di accedere all'unità DVD. Per aggiungere un `UTENTE` al gruppo `optical`, eseguire le seguenti operazioni:
```
# gpasswd -a UTENTE optical

```
Non dimenticare di uscire dalal sessione corente e rientrare affinché le modifiche abbiano effetto. È possibile visualizzare i gruppi attuali del vostro utente con il comando `groups`.

### Lettori DVD

Vedere anche : [Multimedia/Lettori Video](/index.php/List_of_applications/Multimedia_(Italiano)#Lettori_Video "List of applications/Multimedia (Italiano)")

#### MPlayer

[MPlayer](/index.php/MPlayer "MPlayer") è efficiente e supporta una vasta gamma di formati multimediali (cioè quasi tutti). Per riprodurre un DVD con MPlayer :

```
$ mplayer dvd://N

```

... dove `N` è il numero del capitolo desiderato. Iniziano da 1 aumentalo se incerto.

Mplayer controlla `/dev/dvd` per impostazione predefinita. Bisogna dirgli di usare `/dev/sr0` con l'opzione da riga di comando `dvd-device`, o impostando la variabile `dvd-device` in `~/.mplayer/config`.

Per riprodurre un file immagine del DVD :

```
$ mplayer -dvd-device movie.iso dvd://N

```

Per abilitare l'utilizzo del menu DVD (NOTA : si utilizzano i tasti freccia per spostarsi e il tasto `Invio` per scegliere) :

```
$ mplayer dvdnav://

```

Per abilitare il supporto del mouse nei menu dei DVD usare :

```
$ mplayer -mouse-movements dvdnav://

```

Per trovare la lingua audio, avviare MPlayer con il flag `-v` per conoscere l'ID dell'uscita audio. Una traccia audio viene selezionato con {`-aid <audio_id>`. Impostare una lingua audio di default modificando `~/.mplayer/config` e aggiungendo la riga `Alang=en` per l'inglese.

Con MPlayer, il DVD può essere impostato su un volume basso. Per aumentare il volume massimo del 400%, usare `softvol=yes` e `softvol-max=400`. Le impostazioni predefinite del volume di avvio per il 100% del volume del software e dei livelli del mixer globali rimarranno intatte. Utilizzando i tasti 9 e 0, il volume può essere regolato tra 0 e 400 per cento.

```
 alang=en
 softvol=yes
 softvol-max=400

```

[MPlayer home page](http://www.mplayerhq.hu/)

#### VLC

[vlc](https://www.archlinux.org/packages/?name=vlc) è un media player open source scritto in Qt, performante e portatile ([VLC home page](http://www.videolan.org/vlc)).

##### Predefinito in GNOME

Copiare il file sul desktop del sistema a quello locale (file .desktop locali sostituiscono quelli globali) :

```
cp /usr/share/applications/vlc.desktop ~/.local/share/applications/

```

Definire i tipi mime (conosciuta come abilità per tipo file per la riproduzione) facendo :

 `sed -i 's|^Mimetype.*$|MimeType=video/dv;video/mpeg;video/x-mpeg;video/msvideo;video/quicktime;video/x-anim;video/x-avi;video/x-ms-asf;video/x-ms-wmv;video/x-msvideo;video/x-nsv;video/x-flc;video/x-fli;application/ogg;application/x-ogg;application/x-matroska;audio/x-mp3;audio/x-mpeg;audio/mpeg;audio/x-wav;audio/x-mpegurl;audio/x-scpls;audio/x-m4a;audio/x-ms-asf;audio/x-ms-asx;audio/x-ms-wax;application/vnd.rn-realmedia;audio/x-real-audio;audio/x-pn-realaudio;application/x-flac;audio/x-flac;application/x-shockwave-flash;misc/ultravox;audio/vnd.rn-realaudio;audio/x-pn-aiff;audio/x-pn-au;audio/x-pn-wav;audio/x-pn-windows-acm;image/vnd.rn-realpix;video/vnd.rn-realvideo;audio/x-pn-realaudio-plugin;application/x-extension-mp4;audio/mp4;video/mp4;video/mp4v-es;x-content/video-vcd;x-content/video-svcd;x-content/video-dvd;x-content/audio-cdda;x-content/audio-player;|' ~/.local/share/applications/vlc.desktop ` 

Poi in **Impostazioni di Sistema > Dettagli >> Applicazioni predefinite** nel menu a disccesa **Video**, selezionare **Open VLC media player** .

#### xine

Un lettore multimediale leggero con supporto ai menu DVD.

[xine home page](http://www.xine-project.org/)

## DVD ripping

Per ripping si intende il processo di copia dei contenuti audio o video su un disco rigido, in genere da un supporto rimovibile o flussi multimediali. [wikipedia:Ripping](https://en.wikipedia.org/wiki/Ripping "wikipedia:Ripping")

Spesso , il processo di ripping di un DVD può essere suddiviso in due fasi :

1.  **Estrazione dei dati** - Copia l'audio e/o i dati video su un disco rigido
2.  [Transcodifica](https://en.wikipedia.org/wiki/Transcode "wikipedia:Transcode") - Converte i dati estratti in un formato adatto.

Alcune utilità di svolgono entrambi i compiti, mentre altri si concentrano su un aspetto o l'altro.

### dvdbackup

[dvdbackup](/index.php/Dvdbackup "Dvdbackup") è usato semplicemente per l'estrazione di dati, e non per transcodificare. Questo strumento è utile per creare *esatte* copie di DVD criptati in collaborazione con il pacchetto [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss), o per decifrare video per altre utility in grado di leggere i DVD criptati.

### dvd::rip

dvd::rip è un front-end per [transcode](https://www.archlinux.org/packages/?name=transcode), utilizzato per estrarre e convertire al volo (on-the-fly).

I seguenti pacchetti dovrebbero essere installati :

*   [dvdrip](https://aur.archlinux.org/packages/dvdrip/) : front-end GTK per [transcode](https://www.archlinux.org/packages/?name=transcode), che esegue il ripping e la codifica
*   [libdv](https://www.archlinux.org/packages/?name=libdv) : Codec software per video DV
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore) : Se volete codificare i file rippati come XviD, un codec video open source MPEG-4 (alternativa gratuita a DivX)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/) : Se volete codificare i file rippati come DivX (disponibile su [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)"))

Le preferenze di dvd::rip sono per lo più ben documentate e autoesplicative. Se avete bisogno di aiuto, vedere [http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

Il ripping di un DVD è spesso una semplice questione di scelta del codec preferito, selezionare i titoli desiderati, quindi fare clic sul pulsante "Rip".

### FFmpeg

[FFmpeg](/index.php/FFmpeg "FFmpeg") è in grado di fare uno ripping diretto in qualsiasi formato (audio/video da un'immagine .iso di un DVD-Video, basta selezionare l'ingresso come immagine *.iso e procedere con le opzioni desiderate. Permette inoltre il downmix, shrinking, spliting e la selezione dei flussi, tra le altre caratteristiche.

### HandBrake

HandBrake è un transcoder video multithreaded, che offre sia un'interfaccia grafica che utilizzo da riga di comando, con molte configurazioni preimpostate. Il pacchetto è disponibile nei [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)") : [handbrake](https://www.archlinux.org/packages/?name=handbrake).

### MEncoder

[MEncoder](/index.php/MEncoder "MEncoder") è uno strumento da linea di comando libero per la decodifica video, la codifica e filtraggio, rilasciato sotto la GNU General Public License. É strettamente correlato a MPlayer e può convertire tutti i formati che MPlayer legge in una varietà di formati compressi e non compressi con codec diversi. Programmi wrapper come [h264enc](https://aur.archlinux.org/packages/h264enc/) e [undvd](https://aur.archlinux.org/packages/undvd/) sono in grado di fornire un'interfaccia di assistenza.

### Hybrid

Hybrid è un frontend multi-piattaforma (Linux/Mac OSX/Windows) basato sulle Qt, che offre molti strumenti e che può convertire quasi ogni ingresso x264/Xvid/VP8 + ac3/ogg/mp3/aac/flac all'interno di un contenitore mp4/m2ts/mkv/webm/mov/avi, un lettore Blu- ray o una struttura AVCHD.

Il pacchetto è disponibile in [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)") : [hybrid-encoder](https://aur.archlinux.org/packages/hybrid-encoder/).

Per informazioni dettagliate visitare il [sito](http://www.selur.de/project).

### DVD-VR

Da [Wikipedia - DVD-VR](https://en.wikipedia.org/wiki/DVD-VR "wikipedia:DVD-VR"):

	*Lo standard DVD-VR definisce un formato logico per la registrazione video su DVD-R, DVD-RW e DVD-RAM, tra cui le versioni a doppio strato di questi mezzi di comunicazione. Al contrario dei supporti registrati con lo standard di registrazione DVD+VR, i media che ne derivano non sono DVD-Video compatibili, e non vengono riprodotti in alcuni lettori DVD-Video. La maggior parte dei videoregistratori DVD del mercato che supportano DVD-R, DVD-RW o DVD-RAM consentirà la registrazione di questi mezzi di comunicazione in modo DVD-VR, così come in una modalità compatibile DVD-Video. E 'possibile utilizzare il formato DVD-VR con DVD+R e DVD+RW, ma non esistono esempi noti da parte di alcuni programmi di utilità di registrazione basati su PC.*

File .VRO estratti da un DVD-VR possono essere facilmente convertiti e suddivisi in regulari file .VOB utilizzando il programma [DVD-VR](http://www.pixelbeat.org/programs/dvd-vr/).

Installare [dvd-vr](https://aur.archlinux.org/packages/dvd-vr/) dae [AUR](/index.php/AUR_(Italiano) "AUR (Italiano)").

## Risoluzione dei problemi

### K3b e l'errore sul locale

Durante l'esecuzione di K3B , se viene visualizzato il seguente messaggio:

```
System locale charset is ANSI_X3.4-1968
Your system's locale charset (i.e. the charset used to encode file names) is 
set to ANSI_X3.4-1968\. It is highly unlikely that this has been done intentionally.
Most likely the locale is not set at all. An invalid setting will result in
problems when creating data projects.Solution: To properly set the locale 
charset make sure the LC_* environment variables are set. Normally the distribution 
setup tools take care of this.

```

Significa che il locale non è impostato bene.

Per risolvere il problema ,

*   Rimuovere `/etc/locale.gen`
*   Re-installare [glibc](https://www.archlinux.org/packages/?name=glibc)
*   Editare `/etc/locale.gen`, decommentare tutte le linee corrispondenti alla vostra lingua ed anche le opzioni `en_US` per la compatibilità:

```
en_US.UTF-8 UTF-8
en_US ISO-8859-1
it_IT.UTF-8
it_IT.ISO-8859-1

```

*   Ri-generare i profili con `locale-gen`:

 `# locale-gen` 
```
 Generating locales...
 en_US.UTF-8... done
 en_US.ISO-8859-1... done
 it_IT.UTF-8... done
 it_IT.ISO-8859-1... done
 Generation complete.

```

Maggiori informazioni [qui](https://bbs.archlinux.org/viewtopic.php?pid=251512%29;).

### Brasero non riesce a trovare dischi vergini

Brasero utilizza [gvfs](https://www.archlinux.org/packages/?name=gvfs) per gestire i dispositivi di masterizzazione CD/DVD.

### Brasero non riesce a normalizzare CD audio

Se si tenta di masterizzare, si può fermare alla prima fase denominata Normalizzazione. Come soluzione alternativa è possibile disattivare il plugin di normalizzazione con la funzione del menu *Modifica > Plugin*.

### VLC: Error "... could not open the disc /dev/dvd"

Se si ottiene l'errore: "**vlc dvdread could not open the disc "/dev/dvd"**" può essere perché non c'è il device `/dev/dvd` sul vostro sistema. Udev non crea più `/dev/dvd` ma invece usa `/dev/sr0`. Per risolvere questo problema, modificare il file di configurazione di VLC (`~/.config/vlc/vlcrc`):

```
# DVD device (string)                                                           
dvd=/dev/sr0
```

### Unità DVD rumorosa

Se durante la riproduzione di DVD video, il sistema diventa molto rumoroso, può essere perché il disco gira più velocemente di quanto dovrebbe. Per modificare temporaneamente la velocità del drive, come root, eseguire :

```
# eject -x 12 /dev/dvd

```

Oppure :

```
# hdparm -E12 /dev/dvd

```

Qualsiasi velocità che viene supportato dal convertitore può essere utilizzata, o `0` per la velocità massima.

### La riproduzione non funziona con il nuovo computer (nuovo dispositivo DVD)

Se la riproduzione non funziona e si ha un nuovo computer (o un nuovo dispositivo DVD), il motivo potrebbe essere che il [codice della regione](https://en.wikipedia.org/wiki/DVD_region_code "wikipedia:DVD region code") non è impostato. È possibile leggere e impostare il codice regionale con [regioLeggi RIAA e reale consentono di backup dei supporti fisici ottenuti in queste condizioninset](https://aur.archlinux.org/packages/regioLeggi+RIAA+e+reale+consentono+di+backup+dei+supporti+fisici+ottenuti+in+queste+condizioninset/) reperibile su [AUR](/index.php/Arch_User_Repository_(Italiano) "Arch User Repository (Italiano)").

```
Leggi RIALeggi RIAA e reale consentono di backup dei supporti fisici ottenuti in queste condizioniA e reale consentono di backupLeggi RIAA e reale consentono di backup dei supporti fisici ottenuti in queste condizioni dei supporti fisici ottenuti in queste condizioni

```

### Nessuno dei programmi elencati è in grado di estrarre/codificare un DVD sul mio disco rigido!

Assicurarsi che la regione del lettore DVD sia impostato correttamente, altrimenti si otterranno molti errori inspiegabili legati a CSS. Usare [regionset](https://aur.archlinux.org/packages/regionset/) per farlo.

### I log del programma con interfaccia grafica indica problemi con il programma di backend

Se si utilizza un programma con interfaccia grafica e riscontrate dei problemi che nel log del programma in questione dà la colpa su qualche a qualche backend, provare a riprodurre il problema con gli argomenti utilizzando direttamente il programma di backend per registrare.

Se si riesce a riprodurli o meno, si possono segnalere le linee di errore, il comando utilizzato e la scoperta di tale malfunzionamento, come menzionato in [Problemi con i back-end di masterizzazione](#Problemi_con_i_back-end_di_masterizzazione).

#### Caso particolare : Medium error / Write error

Ecco alcuni messaggi tipici dove l'unità prende in *antipatia* il dispositivo ottico utilizzato. Questo può essere risolto solo utilizzando una diversa unità o un supporto diverso. Un programma diverso difficilmente aiuterà.

K3b con backend wodim:

```
Sense Bytes: 70 00 03 00 00 00 00 12 00 00 00 00 0C 00 00 00
Sense Key: 0x3 Medium Error, Segment 0
Sense Code: 0x0C Qual 0x00 (write error) Fru 0x0

```

Brasero con backend growisofs:

```
BraseroGrowisofs stderr: :-[ WRITE@LBA=0h failed with SK=3h/ASC=0Ch/ACQ=00h]: Input/output error

```

Brasero con backend libburn :

```
BraseroLibburn Libburn reported an error SCSI error on write(16976,16): [3 0C 00] Write error

```

## Altre risorse

*   RIAA e attuali leggi che consentono il backup dei supporti fisici ottenuti in queste condizioni [RIAA - the law](https://www.riaa.com/physicalpiracy.php?content_selector=piracy_online_the_law).
*   [Convertire qualsiasi filmato per DVD Video](/index.php/Convert_any_Movie_to_DVD_Video "Convert any Movie to DVD Video")
*   [Pagina principale del progetto libburnia](http://libburnia-project.org/)