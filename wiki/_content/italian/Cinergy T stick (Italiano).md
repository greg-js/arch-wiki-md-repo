## Contents

*   [1 Descrizione](#Descrizione)
    *   [1.1 Installare i Driver](#Installare_i_Driver)
    *   [1.2 Installare i Driver su Arch 64bit](#Installare_i_Driver_su_Arch_64bit)
    *   [1.3 Installare i Driver da AUR](#Installare_i_Driver_da_AUR)

## Descrizione

La Cinergy T stick della Terratec è un device usb per il DVB-T economico ma di buona qualità costruttiva, compatibile con GNU/Linux (wiki anche dal sito del produttore), perfettamente funzionante con Arch Linux.

### Installare i Driver

Per installare i driver la procedura è abbastanza semplice e immediata, tuttavia per avere un'idea più ampia conviene leggere anche la guida ufficiale linuxtv.org [[1]](http://www.linuxtv.org/wiki/index.php/TerraTec_Cinergy_T_Stick) in particolare sulla nostra Arch box dovremo seguire il metodo A che permette una buona compatibilità anche con i kernel attuali anche se non esplicitamente dichiarati 2.6.31 sia ARCH che PAE funzionano.

Il primo passo necessario è prendere i sorgenti Kernel da AUR

```
yaourt -Sy kernel26-source

```

in alternativa si può scaricare il tarball del kernel da [[2]](http://www.kernel.org/)

poi scompattarlo in /usr/src

A questo punto il sistema dovrebbe essere pronto ad accogliere il driver, quindi scarichiamolo cliccando [[3]](http://tonelli.sns.it/pub/mennucc1/terratec_af9035-a_m.tar.gz)

Estraiamolo e editiamo il MakeFile. La parte importante per le modifiche è qui riportata.

```
#### CONFIGURE THE FOLLOWING LINES
#the precompiled kernel headers
KDIR = /usr/src/linux-2.6.31-ARCH/
#the unpacked kernel source
KSRC = /usr/src/linux-2.6.32
#where the modules will be installed
KINSTALL = /lib/modules/2.6.31-ARCH/misc/
#### END OF CONFIGURABLE LINES

```

Oppure per kernel PAE

```
#### CONFIGURE THE FOLLOWING LINES
#the precompiled kernel headers
KDIR = /usr/src/linux-2.6.31-pae/
#the unpacked kernel source
KSRC = /usr/src/linux-2.6.32
#where the modules will be installed
KINSTALL = /lib/modules/2.6.31-pae/misc/
#### END OF CONFIGURABLE LINES

```

Comunque le parti importanti sono solo i path KDIR, KSRC, KINSTALL che devono essere corretti praticamente solo con il numero del vostro Kernel.

A questo punto dovreste essere pronti per la compilazione del driver, date quindi

```
make

```

e se la compilazione non ha presentato errori

```
sudo make install

```

A questo punto occorre copiare il firmware presente in terratec_af9035-a_m che si chiama dvb-usb-af9035-01.fw in /lib/firmware

A questo punto dovrebbe essere tutto ok. Usate il vostro player preferito per fare la ricerca canali, la sintonizzazione e per vedere la TV. Io ho testato personalmente Kaffeine (ma questo è solo soggettivo).

### Installare i Driver su Arch 64bit

Seconda parte e prova su una arch box 64bit. In questo caso ho utilizzato il metodo C del wiki modificandolo leggermente aiutato da una guida su mandriva 2010 [[4]](http://www.mandrakeitalia.org/guide/installazione-configurazione/terratec-cinergy-t-stick-su-mandriva-2010). Innanzitutto dobbiamo creare una patch da applicare.

quindi creiamo un file .patch ad esempio io ho creato terratec.patch con le seguenti righe

```
72a73
> #define USB_PID_TERRATEC_CINERGY_T 0x0093
78a80
> {USB_DEVICE(USB_VID_TERRATEC, USB_PID_TERRATEC_CINERGY_T)},
146c148
< .num_device_descs =1,
---
> .num_device_descs =2,
152a155,159
> {
> .name = "TerraTec Cinergy T-Stick",
> .cold_ids = {&af903x_usb_id_table[5], NULL},
> .warm_ids = {NULL},
> }, 

```

Fatto ciò installiamo unrar kernel26-headers kernel26-source se non li abbiamo.

Scarichiamo i driver Terratec [[5]](http://linux.terratec.de/files/Linux-Driver-for-T-Stick.rar)

scompattiamo e poi portiamoci in

```
cd Linux_PC_AF9035_Afatech_2008.12.17/ 

```

poi in

```
cd Linux-64bit_AF9035_20081217/ 

```

scompatta AF903x_SRC e cd al suo interno

copiate all'interno di questa directory la patch creata prima e poi eseguite

```
patch af903x-devices.c terratec.patch 

```

ora siccome il driver supporta i kernel solo fino al 2.6.27 dobbiamo creare le condizioni per poter compilare con l'attuale kernel 2.6.32 quindi

```
cd v4l

```

```
mkdir kernel-2.6.32

```

```
cd kernel-2.6.32

```

ora copiamo gli headers del nostro kernel

```
cp /lib/modules/`uname -r`/build/drivers/media/dvb/dvb-core/*h .

```

mancano ancora 3 file headers, 2 di questi li trovate nella directory kernel-2.6.27 e sono dvb-pll.h dvb-usb-ids.h un altro io sono dovuto andarlo a recuperare in /usr/src/linux-2.6.32/drivers/media/dvb/dvb-usb/dvb-usb.h ma dato che avevo fatto altre prove e compilazioni non garantisco che ci sia. Al massimo cercherò di caricare tutta la directory che ho usato io con tutti gli headers funzionanti.

alla fine date un ls e controllate che tutto sia a posto

```
[tux@myhost kernel-2.6.32]$ ls
demux.h  dmxdev.h  dvb_ca_en50221.h  dvb_demux.h  dvbdev.h  dvb_filter.h  dvb_frontend.h  dvb_math.h  dvb_net.h  dvb-pll.h  dvb_ringbuffer.h  dvb-usb.h  dvb-usb-ids.h
[tux@myhost kernel-2.6.32]$

```

risalite nella directory AF903x_SRC dando cd .. 2 volte

editate il Makefile e aggiungete in fondo all'elenco

```
ifneq (,$(findstring 2.6.32,$(CURRENT)))
@cp -f v4l/kernel-2.6.32/* ./
endif 

```

a questo punto c'è un problema di copia incolla almeno con kwrite dovete cancellare gli spazi a riga 54 fino a farla risalire a riga 53 dopo di che date invio e poi TAB.

siete pronti a dare

```
make

```

e poi

```
sudo make install

```

Ora attaccate la pen nella porta USB e controllate che tutto vada bene con

```
dmesg tail

```

a me da un output

```
usbcore: registered new interface driver dvb_usb_af903x
usb 1-1: new high speed USB device using ehci_hcd and address 4
usb 1-1: configuration #1 chosen from 1 choice
        DRIVER_RELEASE_VERSION : v2.0-1
        FW_RELEASE_VERSION     : v8_8_52_0
        API_RELEASE_VERSION    : 200.20081203.0
dvb-usb: found a 'TerraTec Cinergy T-Stick' in warm state.
dvb-usb: will use the device's hardware PID filter (table count: 32).
DVB: registering new adapter (TerraTec Cinergy T-Stick)
DVB: registering adapter 0 frontend 0 (AF903X USB DVB-T)...
dvb-usb: TerraTec Cinergy T-Stick successfully initialized and connected.
generic-usb: probe of 0003:0CCD:0093.0002 failed with error -71
usb 1-1: USB disconnect, address 4
dvb-usb: TerraTec Cinergy T-Stick successfully deinitialized and disconnected.
usb 1-2: new high speed USB device using ehci_hcd and address 5
usb 1-2: configuration #1 chosen from 1 choice
        DRIVER_RELEASE_VERSION : v2.0-1
        FW_RELEASE_VERSION     : v8_8_52_0
        API_RELEASE_VERSION    : 200.20081203.0
dvb-usb: found a 'TerraTec Cinergy T-Stick' in warm state.
dvb-usb: will use the device's hardware PID filter (table count: 32).
DVB: registering new adapter (TerraTec Cinergy T-Stick)
DVB: registering adapter 0 frontend 0 (AF903X USB DVB-T)...
dvb-usb: TerraTec Cinergy T-Stick successfully initialized and connected.
input: TerraTec Cinergy T-Stick as /devices/pci0000:00/0000:00:1a.7/usb1/1-2/1-2:1.1/input/input9
generic-usb 0003:0CCD:0093.0003: input,hidraw0: USB HID v1.01 Keyboard [TerraTec Cinergy T-Stick] on usb-0000:00:1a.7-2/input1
fuse init (API version 7.13)

```

questo significa che funge.

se volete potete installare w_scan da AUR per fare lo scanning dei canali e creare il file channels.conf per VLC oppure usare kaffeine.

io ho fatto entrambe le prove, per kaffeine non credo ci vogliano spiegazioni.

per VLC

```
sudo yaourt -Sy w_scan

```

```
w_scan -c IT -ft -X>>channels.conf

```

Bevete una birra...

poi

```
vlc /home/nome_utente/channels.conf

```

Visualizzate la scaletta....

Arch 64bit come altre distro 64bit ha un problema di visualizzazione in kaffeine se abilitati software con supporto OpenGL io non ho saputo risolvere il problema che mi era dato da Cairo-Dock, e mi faceva sentire l'audio ma non vedere il video. Vedevo trasparente nel riquadro di Kaffeine. Basta disabilitare cairo dock e forzarla con -c.

Momentaneamente ho caricato su MEGAUPLOAD la directory pronta con il file già patchato e tutto pronto. PROVATELA. [[6]](http://www.megaupload.com/?d=N61DP1A0)

### Installare i Driver da AUR

In alternativa, è possibile utilizzare il pacchetto AUR [dvb-usb-af9035](https://aur.archlinux.org/packages/dvb-usb-af9035/) che semplifica e automatizza la procedura di compilazione e installazione del modulo e firmware necessari al corretto funzionamento.

Il pacchetto AUR è stato creato seguendo il metodo A, descritto nella sezione dedicata alla [TerraTec Cinergy T Stick](http://linuxtv.org/wiki/index.php/TerraTec_Cinergy_T_Stick) su linuxtv.org.