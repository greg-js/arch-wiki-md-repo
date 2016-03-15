## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Installare bootchart](#Installare_bootchart)
*   [3 Eseguire Bootchart](#Eseguire_Bootchart)
    *   [3.1 Impostazione Gestore di Avvio](#Impostazione_Gestore_di_Avvio)
        *   [3.1.1 Grub](#Grub)
        *   [3.1.2 Grub 2](#Grub_2)
        *   [3.1.3 Lilo](#Lilo)
    *   [3.2 impostazione rc.sysinit](#impostazione_rc.sysinit)
        *   [3.2.1 Modificare /etc/rc.sysinit](#Modificare_.2Fetc.2Frc.sysinit)
        *   [3.2.2 Fermare bootchartd dopo l'accesso](#Fermare_bootchartd_dopo_l.27accesso)
*   [4 Generare un grafico](#Generare_un_grafico)
    *   [4.1 Risoluzione problemi](#Risoluzione_problemi)
    *   [4.2 Esempi di bootchart](#Esempi_di_bootchart)
        *   [4.2.1 Avvio in 5 secondi](#Avvio_in_5_secondi)
*   [5 Collegamenti esterni](#Collegamenti_esterni)

# Introduzione

Bootchart è un programma utilizzato per l'analisi dei processi d'avvio (ad esempio può essere utile per ottimizzare e velocizzare il boot). È composto dal demone bootchartd e da bootchart-render; una volta usato genererà una tabella per ogni avvio che fornisce indicazioni su come, quanto e quali processi sono in esecuzione, utilizzo di cpu, memoria e tempi di accesso al disco.

# Installare bootchart

[Installare](/index.php/Pacman "Pacman") [bootchart](https://www.archlinux.org/packages/?name=bootchart), pacchetto disponibile nel [repository ufficiale](/index.php/Official_Repositories_(Italiano) "Official Repositories (Italiano)").

# Eseguire Bootchart

Per usare bootchart, va impostato come processo init nel gestore di avvio (ad esempio aggiungendo alla riga di avvio di GRUB 'init=/usr/bin/bootchartd') od avviarlo manualmente da uno degli script di init (preferibilmente `rc.sysinit`). Nota che se avvii bootchartd manualmente, devi anche fermarlo manualmente. In generale, bisogna essere molto attenti con quest'ultimo metodo.

## Impostazione Gestore di Avvio

In generale si deve fare una copia delle opzioni di avvio che si vogliono usare (in questo modo si avrà sia la voce normale che con bootchart) ed aggiungervi `init=/usr/bin/bootchartd`. Quando avviato dal gestore di avvio, bootchart si fermerà una volta arrivati al gestore di accesso.

### Grub

Aprire `/boot/grub/menu.lst`, e fare copia/incolla della voce di cui si vuole che bootchart generi un log. Aggiungere `init=/usr/bin/bootchartd` alla riga del kernel. Esempio:

```
# (1) Arch Linux Bootchart
title  Arch Linux
root   (hd0,0)
kernel /vmlinuz-linux root=/dev/disk/by-uuid/d531ff5b-de65-499a-9942-d18682375163 ro quiet **init=/usr/bin/bootchartd**
initrd /initramfs-linux.img

```

### Grub 2

Aprire `/boot/grub/grub.cfg`, fare copia/incolla dell'opzione di avvio che si vuole usare e modificarla perché appaia così:

```
# (0) Arch Linux
menuentry "Arch Linux" {
set root=(hd0,1)
linux /boot/vmlinuz-linux root=/dev/sda1 ro quiet
initrd /boot/initramfs-linux.img
}
# (1) Arch Linux with Bootchart
menuentry "Arch Linux with Bootchart" {
set root=(hd0,1)
linux /boot/vmlinuz-linux root=/dev/sda1 ro quiet init=/usr/bin/bootchartd
initrd /boot/initramfs-linux.img
}

```

Ora si può riavviare e scegliere la nuova opzione con bootchart.

### Lilo

Da fare

## impostazione rc.sysinit

Questo è pericoloso (si può rendere arch inavviabile) - usarlo solo se l'altro metodo non funziona. Quando si usa questo metodo non solo si deve fermare bootchartd manualmente dopo l'avvio (o riempirà completamente il disco) ma partirà ogni volta che avvierai il computer. Inoltre ogni cambiamento a `/etc/rc.sysinit` sarà annullato la prossima volta che verrà aggiornato il pacchetto initscripts. Una nota positiva è che così bootchart mostra cosa succede dopo l'accesso, ovvero darà un quadro completo del vero avvio di un sistema operativo, includendo il caricamento dell'ambiente di lavoro.

### Modificare /etc/rc.sysinit

Bisogna modificare `/etc/rc.sysinit` aggiungendo questa riga:

```
/usr/bin/bootchartd start

```

Non può essere messa molto in alto (ovvero all'inizio), perché pootrebbe rendere il sistema inavviabile, ma allo stesso tempo metterla molto in basso (ovvero alla fine) nello script nasconderà ogni cosa che succede prima dell'avviod di bootchart. Dovrebbe essere sicuro metterla appena prima della sezione che avvia l'orologio di sistema. Per farlo cercare questa riga:

```
stat_busy "Configuring System Clock"

```

E mettere

```
/usr/bin/bootchartd start

```

prima di essa.

### Fermare bootchartd dopo l'accesso

Come scritto in precedenza, occorre fermare manualmente bootchartd (il demone di bootchart). Per farlo eseguire da root:

```
/usr/bin/bootchartd stop

```

Oppure da sudo se è stato impostato:

```
sudo /usr/bin/bootchartd stop

```

# Generare un grafico

Per generare un grafico, eseguire:

```
bootchart-render

```

in una cartella per cui si abbiano permessi di scrittura. Questo genererà un'immagine `bootchart.png` col grafico. Occorre avere Java runtime installato ed appropiatamente impostato per poter fare il grafico.

## Risoluzione problemi

bootchart-render non può generare un'immagine 'bootchart.png' e mostra il seguente messaggio d'errore:

```
/var/log/bootchart.tgz not found

```

Probabilmente significa che bootchartd non è stato in grado di determinare quando il processo d'avvio è finito. Questo può succedere se si stanno usando gestori di accesso diversi da [GDM](/index.php/GDM "GDM") o [KDM](/index.php/KDM "KDM"), come [SLIM](/index.php/SLIM "SLIM") od altri. Occorre aprire lo script `/usr/bin/bootchartd` ed aggiungere quelle applicazioni alla variabile `exit_proc`, ad esempio:

```
# The processes we have to wait for
local exit_proc="gdmgreeter gdm-binary kdm_greet kdm slim"

```

Se non si sta usando nessun gestore di accesso, modificare la variabile `exit_proc` in questo modo:

```
# The processes we have to wait for
local exit_proc="login"

```

## Esempi di bootchart

### Avvio in 5 secondi

[Articolo di LWN sull'avvio veloce di netbooks](http://lwn.net/Articles/299483/)

Questo articolo è davvero interessante ed insieme ad un mucchio di grafici fornisce qualche consiglio su come avviare più velocemente. Alcuni di quelle migliorie sono aldilà della portata dell'utente comune (mettere patch a X.org, al kernel, ecc...).

# Collegamenti esterni

*   [Bootchart home page](http://www.bootchart.org/)