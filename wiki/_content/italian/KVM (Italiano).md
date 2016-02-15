**KVM**, Kernel Based Virtual Machine, è un hypervisor inserito direttamente all'interno del kernel 2.6 (e 3.x) a partire dalla versione 2.6.20\. Il suo utilizzo ha scopi simili a quelli di [Xen](/index.php/Xen "Xen") ma è più immediato. Per cominciare ad utilizzare l'hypervisor è sufficiente caricare i moduli appropriati. Come per la virtualizzazione completa di Xen, anche per utilizzare KVM è necessario disporre di un processore che supporti le estensioni VT di Intel, o AMD-V in caso di sistema AMD.

Utilizzando KVM, è possibile avviare macchine virtuali multiple che eseguano immagini non modificate di Linux, Windows, o di molti altri sistemi. (Consultare [Guest Support Status](http://www.linux-kvm.org/page/Guest_Support_Status)). Ogni macchina virtuale ha il suo hardware virtualizzato privato: scheda di rete, adattatore grafico, etc. Consultare [KVM Howto](http://www.linux-kvm.org/page/HOWTO)

Le differenze tra KVM, Xen, VMware e QEMU sono elencate su [KVM FAQ](http://www.linux-kvm.org/page/FAQ#General_KVM_information).

KVM è utilizzato insieme a [Libvirt](/index.php/Libvirt "Libvirt") per una migliore gestione attraverso il set di comandi "virsh".

## Contents

*   [1 Installare i pacchetti](#Installare_i_pacchetti)
*   [2 Configurare i moduli del kernel](#Configurare_i_moduli_del_kernel)
*   [3 Come utilizzare KVM](#Come_utilizzare_KVM)
*   [4 Sistema guest paravirtualizzato (virtio)](#Sistema_guest_paravirtualizzato_.28virtio.29)
    *   [4.1 Preparare un sistema guest (Arch) linux](#Preparare_un_sistema_guest_.28Arch.29_linux)
    *   [4.2 Preparare un sistema guest Windows](#Preparare_un_sistema_guest_Windows)
*   [5 Ridimensionare l'immagine](#Ridimensionare_l.27immagine)
    *   [5.1 Metodo attuale](#Metodo_attuale)
    *   [5.2 Vecchio metodo](#Vecchio_metodo)
*   [6 Abilitare KSM](#Abilitare_KSM)
*   [7 Agevolazioni per i nuovi utenti](#Agevolazioni_per_i_nuovi_utenti)
*   [8 Integrazione del mouse](#Integrazione_del_mouse)
*   [9 Montare immagini qemu](#Montare_immagini_qemu)
*   [10 Eseguire le macchine virtuali all'avvio](#Eseguire_le_macchine_virtuali_all.27avvio)
*   [11 Trucchi e Consigli](#Trucchi_e_Consigli)
    *   [11.1 Configurazione di rete semplificata](#Configurazione_di_rete_semplificata)

## Installare i pacchetti

I kernel Arch forniscono i [moduli del kernel](/index.php/Kernel_modules_(Italiano) "Kernel modules (Italiano)") appropriati. Si può verificare se il proprio kernel supporti kvm tramite il seguente comando (ammesso che il proprio kernel sia compilato con la flag `CONFIG_IKCONFIG_PROC)`:

 `$ zgrep KVM /proc/config.gz` 

KVM necessita di un processore sulla macchina host che supporti la virtualizzazione (tecnologia nota come VT-x per i processori Intel e AMD-V per quelli prodotti da AMD). È possibile verificare questo requisito col seguente comando:

 ` $ lscpu` 

Se il processore supporta la virtualizzazione, verrà mostrata anche una riga che lo afferma esplicitamente. Altrimenti la compatibilità può essere controllata anche con

 ` grep -E "(vmx|svm)" --color=always /proc/cpuinfo` 

Se non viene restituito alcun output, il proprio processore _non_ supporta la virtualizzazione, e non è quindi possibile utilizzare QEMU-KVM.

KVM necessita inoltre di una versione modificata di QEMU per poter lanciare e gestire le macchine virtuali. È possibile sceglierne una tra le seguenti in base alle proprie esigenze:

1.  Il pacchetto [qemu-kvm](https://www.archlinux.org/packages/?name=qemu-kvm) è disponibile nei [Repository Ufficiali](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)") _(scelta raccomandata)_

1.  Se è necessario anche l'uso di QEMU, si può scegliere di installare una versione di [qemu](https://www.archlinux.org/packages/?name=qemu) superiore alla 0.9.0, che va in conflitto con il pacchetto [qemu-kvm](https://www.archlinux.org/packages/?name=qemu-kvm). Comunque oramai anche il pacchetto [qemu](https://www.archlinux.org/packages/?name=qemu) fornisce un eseguibile (`qemu -enable-kvm`) che si avvantaggia di tale tecnologia.

## Configurare i moduli del kernel

Innanzitutto è necessario aggiungere il proprio utente al gruppo `kvm` in modo da consentirgli di utilizzare la periferica `/dev/kvm`

 `# gpasswd -a <Proprio_Nome_Utente> kvm` 

Successivamente bisogna scegliere quale modulo caricare in base al processore che si possiede.

1.  Successivamente, caricare i moduli `kvm` e `kvm-intel` se si possiede un processore Intel (estensione VT-x)

 `# modprobe kvm`  `# modprobe kvm-intel` 

oppure i moduli `kvm` e `kvm-amd` nel caso si possieda un processore AMD con estensione AMD-V (nome in codice Pacifica)

 `# modprobe kvm`  `# modprobe kvm-amd` 

Se il caricamento del modulo `kvm` dovesse andare a buon fine, ma si dovessero riscontrare problemi nel caricamento di `kvm-intel` o `kvm-amd` (nonostante /proc/cpuinfo confermi la presenza di estensioni di virtualizzazione), verificare le impostazioni del proprio BIOS, in quanto alcuni produttori (sopratutto di sistemi portatili) disabilitano la VT di default. Per verificare se il problema sia dovuto alla disabilitazione delle estensioni, consultare l'output di `dmesg` subito dopo il fallimento del caricamento dei moduli.

Se si vuole che questi moduli vengano caricati all'avvio, sfruttare `/etc/rc.conf`

## Come utilizzare KVM

1.  Creare un'immagine del sistema guest

 `$ qemu-img create -f qcow2 <Image_Name> <size>` 

1.  Installare il sistema guest. Per l'installazione può essere utilizzata un'immagine cd/dvd (file ISO)

 `$ qemu-kvm -hda <Nome_Immagine> -m 512 -cdrom </Percorso/all/immagine/ISO> -boot d -vga std` 

1.  Eseguire il sistema

 `$ qemu-kvm -hda <Nome_Immagine> -m 512 -vga std` 
**Nota:** Si potrebbe volere assegnare più di una cpu al sistema guest tramite lo switch `-smp X` (dove X è il numero di cpu). Il numero massimo di cpu assegnabili per un singolo sistema è 16.

**Nota:** La memoria di default di KVM è di 128MB, per modificarla utilizzare il parametro `-m` e specificare il quantitativo di memoria desiderata in megabytes (es. `-m 1024`). Tenere presente inoltre che i sistemi Microsoft più recenti (testato con Vista e Seven) richiedono il tipo di immagine `qcow2`, restituendo altrimenti un codice di errore 0x80070057 durante l'installazione.

Consultare **[QEMU](/index.php/QEMU "QEMU")** per tutte le altre informazioni, e la sezione _[Using the Kernel-based Virtual Machine](/index.php/QEMU#Using_the_Kernel-based_Virtual_Machine "QEMU")_.

## Sistema guest paravirtualizzato (virtio)

KVM offre ai sistemi guest la possibilità di utilizzare la paravirtualizzazione di periferiche a blocchi e di rete, che consente migliori prestazioni e minor sovraccarico. Linux ha questa capacità con i suoi moduli virtio dalla versione 2.6.25. Per windows un driver di periferica di rete paravirtualizzata è disponibile [a questo indirizzo](http://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers%7C).

Una periferica a blocchi virtio richiede l'opzione `-drive` anzichè la semplice `-hd*`, più `if=virtio`:

 `$ qemu-kvm -boot order=c -drive file=drive.img,if=virtio` 
**Nota:** `-boot order=c` è assolutamente necessario se si desidera eseguire il boot da questa periferica. Non c'è alcun tipo di autorilevamento, come invece avviene con `-hd*`

All'incirca lo stesso metodo si utilizza per le periferiche di rete

 `$ qemu-kvm -net nic,model=virtio` 

### Preparare un sistema guest (Arch) linux

Per utilizzare periferiche virtio su di un sistema guest Arch Linux, i seguenti moduli devono essere caricati: `virtio, virtio_pci, virtio_blk, virtio_net e virtio_ring` ( per sistemi guest a 32 bit, il modulo `virtio` non è necessario). Se si vuole eseguire il boot da un disco-vitio, il ramdisk iniziale deve essere [rigenerato](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)"). Aggiungere i moduli appropriati all'interno di `/etc/mkinitcpio.conf` in questo modo:

 `/etc/mkinitcpio.conf`  `MODULES="virtio virtio_blk virtio_pci virtio_net virtio_ring"` 

e rigenerare:

 `# mkinitcpio -p linux` 

I dischi virtio sono rilevati col prefisso _**v**_ (come ad esempio vda, vdb, etc...). Devono quindi essere effettuate le opportune modifiche all'interno di `/etc/fstab` e `/boot/grub/menu.lst` (se si esegue il boot da uno di questi dischi; ovviamente se si utilizza un sistema che fa riferimento ai dischi tramite [uuids](/index.php/Persistent_block_device_naming_(Italiano) "Persistent block device naming (Italiano)"), non deve essere modificato nulla.)

Modificare o creare `/boot/grub/device.map`  `(hd0) /dev/vda` 

Grub ha alcuni problemi nel riconoscimento di dischi virtio. Perciò, se il bootloader non è installato, o se lo si vuole re-installare, è necessario modificare (o creare, nel caso non sia presente, eventualità molto frequente) anche il file `/boot/grub/device.map` in maniera coerente:

 `/boot/grub/device.map`  `(hd0) /dev/vda` 

Ulteriori informazioni sulla paravirtualizzazione in KVM: [[1]](http://www.linux-kvm.org/page/Boot_from_virtio_block_device) sezione nel qemu-book tedesco: [[2]](http://qemu-buch.de/de/index.php/QEMU-KVM-Buch/_Virtuelle_Hardware/_Paravirtualisierte_Ger%C3%A4tetreiber)

### Preparare un sistema guest Windows

Preparare un sistema guest Windows che funzioni tramite dispositivi virtio è alquanto macchinoso.

Nel proprio host KVM (che esegue Arch Linux) scaricare il driver virtio da [Fedora repository](http://www.linux-kvm.org/page/WindowsGuestDrivers/Download_Drivers). Ora bisogna creare una nuova immagine del disco, che imponga a Windows la ricerca del driver. Per fare ciò, interrompere l'esecuzione della macchina virtuale e dare il seguente comando:

 `qemu-img create -f qcow2 fake.img 1G` 

Eseguire il guest Windows originale (ancora in modalità IDA). Aggiungere il disco fasullo ed un cdrom con il driver.

 `qemu-kvm -drive file=windows.img,if=ide,boot=on -m 512 -drive file=fake.img,if=virtio -cdrom virtio-win-0.1-15.iso -vga std` 

Windows rileverà il disco fasullo e cercherà un driver per gestirlo.. Se dovesse fallire, andare in Gestione Periferiche, individuare il drive SCSI con un punto esclamativo a fianco, clickare su "Aggiorna Driver" e navigare fino alla directory appropriata sul cdrom.

Quando l'installazione è completata con successo, è possibile spegnere la macchina virtuale e ri-eseguirla, ora con il driver `virtio`

 `qemu-kvm -drive file=windows.img,if=virtio,boot=on -m 512 -vga std` 
**Nota:** Se si riscontrano problemi di BSOD, assicurarsi di aver settato un quantitativo sufficiente di memoria tramite lo switch `-m`

## Ridimensionare l'immagine

**Attenzione:** ridimensionare un'immagine contenente un filesystem ntfs d'avvio, potrebbe rendere la VM installata su di esso inavviabile. Una soluzione (estremamente macchinosa ed adatta solo ad utenti esperti), è mostrata a questo indirizzo insieme ad una approfondita spiegazione del problema [http://tjworld.net/wiki/Howto/ResizeQemuDiskImages](http://tjworld.net/wiki/Howto/ResizeQemuDiskImages).

### Metodo attuale

Dalla versione 0.13.0 of [qemu](https://www.archlinux.org/packages/?name=qemu), è stata aggiunta una nuova opzione all'eseguibile `qemu-img`, l'opzione `resize`. Tramite questo switch è possibile ridimensionare un'immagine qcow2 direttamente, senza la necessità del passaggio intermedio per il formato raw. Ad es., il seguente comando incrementerà la dimensione dell'immagine my_image.qcow2 di 10 Gigabytes.

 `qemu-img resize my_image.qcow2 +10G` 

### Vecchio metodo

È possibile incrementare la dimensione di un'immagine `qcow2` successivamente, almeno con `ext3`. Convertirla in immagine `raw`, espandere la sua dimensione con `dd`, riconvertirla in `qcow2`, rimpiazzare la partizione con una più grande, effettuare un `fsck` e ridimensionare il filesystem.

```
$ qemu-img convert -O raw image.qcow2 image.img
$ dd if=/dev/zero of=image.img bs=1G count=0 seek=[NUMBER_OF_GB]
$ qemu-img convert -O qcow2 -o cluster_size=64K image.img imageplus.qcow2
$ qemu-kvm -hda imageplus.qcow2 -m 512 -cdrom </Path/to/the/ISO/Image> -boot d -vga std
$ fdisk /dev/sda [Tenere presente che il questo comando cancellerà la partizione, creandone una nuova che andrà ad occupare l'intero disco.]
$ e2fsck -f /dev/sda1
$ resize2fs /dev/sda1
```

## Abilitare KSM

KSM (Kernel Samepage Merging) è una funzione del kernel Linux introdotta con la versione 2.6.32\. KSM consente alle applicazioni registrate di condividere alcune delle loro pagine di memoria. Per quanto riguarda KVM, il meccanismo KSM consente alle macchine virtuali create di operare questa condivisione. In uno scenario all'interno del quale siano presenti diversi sistemi operativi guest simili tra loro, questa scelta può comportare un significativo risparmio di memoria impiegata. Per abilitare KSM, assicurarsi per prima cosa di disporre di una versione di [qemu-kvm](https://www.archlinux.org/packages/?name=qemu-kvm) uguale o superiore alla 0.12.0.

 `# pacman -Qi qemu-kvm | grep Version`  `Version        : 0.12.1.2-1` 

e di una versione del kernel uguale o superiore alla 2.6.32.

 `$ uname -r`  `3.0-ARCH` 

Se i due requisiti sono soddisfatti, dovrebbe quindi essere presente la directory `/sys/kernel/mm/ksm/`, contenente vari file. È possibile abilitare/disabilitare KSM modificando ad 1 o 0 il file `/sys/kernel/mm/ksm/run`

 `# echo 1 > /sys/kernel/mm/ksm/run` 

Se KSM è in esecuzione, e ci sono pagine da condividere (ad esempio, se sono in esecuzione due o più macchine virtuali simili) allora il file `/sys/kernel/mm/ksm/pages_shared` avrà un valore diverso da 0\. Come spiegato nella documentazione del kernel `Documentation/vm/ksm.txt` lo stato effettivo di KSM e di MADV_MERGEABLE è mostrato all'interno di `/sys/kernel/mm/ksm/`:

```
pages_shared     - how many shared unswappable kernel pages KSM is using
pages_sharing    - how many more sites are sharing them i.e. how much saved
pages_unshared   - how many pages unique but repeatedly checked for merging
pages_volatile   - how many pages changing too fast to be placed in a tree
full_scans       - how many times all mergeable areas have been scanned

```

```
Un rapporto alto tra pages_sharing e pages_shared indica una buona condivisione, ma 
un rapporto alto tra pages_unshared e pages_sharing indica tentativi inutili
pages_volatile è funzione di diversi tipi di attività, ma un valore alto potrebbe indicare un uso limitato di madvise MADV_MERGEABLE.

```

Una maniera semplice per varificare le effettive performance del KSM, consiste nello stampare il contenuto dei file in questa directory

 `# for ii in /sys/kernel/mm/ksm/* ; do echo -n "$ii: " ; cat $ii ; done` 

```
/sys/kernel/mm/ksm/full_scans: 151
 /sys/kernel/mm/ksm/max_kernel_pages: 246793
 /sys/kernel/mm/ksm/pages_shared: 92112
 /sys/kernel/mm/ksm/pages_sharing: 131355
 /sys/kernel/mm/ksm/pages_to_scan: 100
 /sys/kernel/mm/ksm/pages_unshared: 123942
 /sys/kernel/mm/ksm/pages_volatile: 1182
 /sys/kernel/mm/ksm/run: 1
 /sys/kernel/mm/ksm/sleep_millisecs: 20
```

## Agevolazioni per i nuovi utenti

Se è stato installato il pacchetto [qemu](https://www.archlinux.org/packages/?name=qemu), è possibile utilizzare delle interfacce grafiche, come [qtemu](https://www.archlinux.org/packages/?name=qtemu) per un uso semplificato oppure [qemu-launcher](https://www.archlinux.org/packages/?name=qemu-launcher) per un utilizzo più approfondito, per gestire le proprie macchine virtuali. È necessario modificare il valore di `QEMU start command` nel pannello di configurazione da `qemu` a `qemu-kvm`/`qemu-system-x86_64` o aggiungere `-enable-kvm` alle opzioni di avvio addizionali. Con le nuove versioni di [qemu](https://www.archlinux.org/packages/?name=qemu), potrebbe non essere più necessario aggiungere l'opzione `-enable-kvm`, in quanto lìeseguibile `qemu` dovrebbe rilevare l'esecuzione di kvm e partire con i corretti parametri. Se si avvia la propria macchina virtuale tramite un'interfaccia grafica, e si riscontra una installazione mlto lenta, sarà il caso di verificare la corretta esecuzione di KVM, in quanto QEMU potrebbe aver fallito il rilevamento, ed essere partito con una emulazione puramente software.

## Integrazione del mouse

Per evitare che il mouse venga catturato quando si clicca all'interno della finestra del sistema guest aggiungere l'opzione `-usbdevice tablet`. Ciò significa che QEMU sarà in grado di rilevare la posizione del mouse senza doverlo catturare. Quando attivata, questa opzione sovrascrive inoltre l'emulazione della porta PS/2.

 `$ qemu-kvm -hda <Image_Name> -m 512 -vga std -usbdevice tablet` 

## Montare immagini qemu

 `# modprobe nbd max_part=63`  `# qemu-nbd -c /dev/nbd0 [image.img]`  `# mount /dev/nbd0p1 [/mnt/qemu]` 

## Eseguire le macchine virtuali all'avvio

Se si utilizzano [virt-manager](https://www.archlinux.org/packages/?name=virt-manager) e `virsh` per la gestione delle proprie VM, l'operazione è molto semplice. Per impostare da riga di comando l'esecuzione di una macchina virtuale all'avvio

 `virsh autostart <domain>` 

per disabilitare l'autostart

 `virsh autostart --disable <domain>` 

Con virt-manager è altrettanto semplice, avendo la possibilità di spuntare la relativa checkbox nelle opzioni di avvio della VM.

**Nota:** VMs avviate da QEMU e KVM da linea di comando non sono gestibile da virt-manager

Consultare [QEMU#Starting_qemu_virtual_machines_on_boot](/index.php/QEMU#Starting_qemu_virtual_machines_on_boot "QEMU")

## Trucchi e Consigli

### Configurazione di rete semplificata

Configurare un bridging di rete potrebbe risultare complesso, a volte. Se l'unico scopo della creazione della macchina virtuale è quello di sperimentare, una soluzione più semplice può essere quella di connettersi tramite tunneling SSH.

I passi fondamentali sono i seguenti:

*   configurare un server SSH sul sistema host
*   (opzionale) creare un utente designato ad effettuare il tunneling
*   installare SSH sulla macchina virtuale
*   configurare l'autenticazione

Consultare [la pagina SSH](/index.php/SSH_(Italiano) "SSH (Italiano)") per configurare quest'ultimo, in particolare la sezione [SSH (Italiano)#Effettuare il Forwarding di altre porte](/index.php/SSH_(Italiano)#Effettuare_il_Forwarding_di_altre_porte "SSH (Italiano)") Quando si usano le impostazioni di rete di default, l'host è raggiungibile all'indirizzo `10.0.2.2`

Se tutto funziona, e si è in grado di accede in SSH all'host, è sufficiente aggiungere quanto segue

 `/etc/rc.local` 

```
# Local SSH Server
echo "Starting SSH tunnel"
sudo -u vmuser ssh tunneluser@10.0.2.2 -N -R 2213:127.0.0.1:22 -f
# Random remote port (e.g. from another VM)
echo "Starting random tunnel"
sudo -u vmuser ssh tunneluser@10.0.2.2 -N -L 2345:127.0.0.1:2345 -f

```

In questo esempio viene creato un tunnel sul server SSH della macchina virtuale ed una porta dell'host scelta arbitrariamente viene collegata nella macchina virtuale.

Questa è una maniera molto essenziale di configurare la rete con le macchina virtuali. È comunque piuttosto sicura, e dovrebbe essere adegauata in gran parte delle circostanze.