## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Configurare l'ambiente live per usare SSH](#Configurare_l'ambiente_live_per_usare_SSH)
*   [3 Collegarsi al PC di destinazione tramite SSH](#Collegarsi_al_PC_di_destinazione_tramite_SSH)
    *   [3.1 Note](#Note)
*   [4 Passi successivi](#Passi_successivi)

## Introduzione

Questo articolo ha lo scopo di mostrare agli utenti come installare Arch da remoto tramite una connessione SSH. Considerare questo approccio, rispetto a quello standard, nell'eventualità degli scenari seguenti:

Configurare Arch su...

*   HTPC senza monitor corretto (cioè un SDTV).
*   Un PC che si trova in un'altra città, stato, nazione.
*   Un PC in cui si preferisca l'installazione da remoto, per esempio, dalla comodità della propria postazione di lavoro con capacità copia/incolla dal wiki di Arch.

**Nota:** I primi due passaggi richiedono l'accesso fisico alla macchina. Ovviamente, se fisicamente localizzata altrove, ciò dovrà essere coordinato con un'altra persona!

## Configurare l'ambiente live per usare SSH

**Nota:** I seguenti comandi devono essere eseguiti come utente root. Il simbolo di prompt # è stato omesso volontariamente per permettere il copia/incolla direttamente dal testo.

A questo punto dovrebbe venire visualizzato il prompt di root **[root@archiso ~]#**.

In primo luogo, configurare la rete sul computer di destinazione:

```
aif -p partial-configure-network

```

Viene presentata una lista di interfacce note; digitare l'interfaccia che si desidera utilizzare (ad esempio: eth0 per interfaccia Ethernet cablata)

In secondo luogo, sincronizzare l'ambiente live ad un mirror, installare il pacchetto [openssh](https://www.archlinux.org/packages/?name=openssh), ed avviare il demone:

**Nota:** Questa operazione non è più richiesta. Il media di installazione è già pronto con installato openssh

```
pacman -Syy openssh
rc.d start sshd

```

**Nota:** A seconda di quanto è recente il supporto di installazione, pacman potrebbe richiederne un aggiornamento come primo passo. Poiché l'obiettivo è quello di installare semplicemente il pacchetto OpenSSH, si consiglia di negare questa richiesta ed installare semplicemente il pacchetto in questione.

Infine, autorizzare le connessioni `sshd` e impostare una password di root, necessaria per la connessione SSH; la password Arch di default per root è vuota.

```
passwd

```

## Collegarsi al PC di destinazione tramite SSH

Collegarsi al computer di destinazione tramite il seguente comando:

```
$ ssh root@ip.address.of.target

```

A questo punto viene presentato l'ambiente live con il messaggio di benvenuto, e si è in grado di amministrare il computer di destinazione come se si fosse seduti fisicamente alla sua tastiera.

```
$ ssh root@10.1.10.105
root@10.1.10.105's password: 
Last login: Thu Dec 23 08:33:02 2010 from 10.1.10.200
**************************************************************
* To begin installation, run /arch/setup                     *
* You can find documentation at                              *
*  /usr/share/aif/docs/official_installation_guide_en        *
*                                                            *
* i18n: Use the 'km' utility to change your keyboard layout  *
*       and console font.                                    *
*                                                            *
* If you are looking to install Arch on something more       *
* exotic, such as your kerosene-powered cheese grater,       *
* please consult [https://wiki.archlinux.org](https://wiki.archlinux.org).                *
*                                                            *
**************************************************************
[root@archiso ~]#

```

### Note

*   Se la macchina di destinazione è dietro un firewall/router, la porta SSH di default 22 avrà ovviamente bisogno di essere impostata all'indirizzo LAN IP della macchina di destinazione. L'utilizzo del "port forwarding" non viene trattato in questa guida.
*   Si può modificare `/etc/ssh/sshd_config` nell'ambiente live prima di avviare il demone, ad esempio per l'esecuzione su una porta non standard, se desiderato.

## Passi successivi

Il cielo è l'unico limite. Se il proposito è quello di installare semplicemente Arch dal supporto live, eseguire il comando `/arch/setup`. Se il proposito è invece quello di apportare delle modifiche su un'installazione Linux difettosa, seguire l'articolo wiki [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux").

Si vuole optare per [grub2](/index.php/Grub2 "Grub2") o la possibilità di utilizzare supporti [GPT](/index.php/GPT "GPT")?

*   Partizionare manualmente i supporti HDD/SDD di destinazione usando l'utilità [gdisk](https://www.archlinux.org/packages/?name=gdisk) installata tramite `pacman -S gdisk` prima di avviare il programma di installazione. Quando viene presentata la possibilità di installare un bootloader nel quadro d'installazione, rispondere no e tornare indietro al root prompt dell'ambiente live d'installazione.
*   L'installazione di grub2 è banale a questo punto. Basta eseguire il chroot nella nuova installazione Arch (di default è già montato se si esce dal programma di installazione), e poi installare e configurare grub2:

```
cd /mnt
rm console ; mknod -m 600 console c 5 1 
rm null ; mknod -m 666 null c 1 3 
rm zero ; mknod -m 666 zero c 1 5
mount -t proc proc /mnt/proc
mount -t sysfs sys /mnt/sys
mount -o bind /dev /mnt/dev
chroot /mnt /bin/bash

```

Ora all'interno della chroot di Arch:

```
pacman -S grub2
grep -v rootfs /proc/mounts > /etc/mtab

```

Modificare `/etc/defualt/grub` a proprio piacimento. Installare grub e generare il file grub.cfg

```
grub-install /dev/sdX --no-floppy
grub-mkconfig -o /boot/grub/grub.cfg

```

**Nota:** Quanto sopra presuppone che se l'utente intende fare il boot da un disco GPT, ha pienamente letto e compreso gli articoli wiki di cui sopra e ha creato una partizione di 1M ef02 per grub2.

Quando si è pronti a riavviare la nuova installazione di Arch, uscire dal chroot e smontare le partizioni prima di riavviare il sistema.

```
exit
umount /mnt/boot   # se montata in una partizione separata
umount /mnt/{proc,sys,dev}
umount /mnt

```