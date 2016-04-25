Lo scopo di questo articolo è quello di configurare un server nfs per condividere file in rete.

*   Nota: per NFSv4, consultare la guida a [NFSv4](/index.php/NFSv4 "NFSv4")
*   nfs-utils è stato aggiornato dal 2009-06-23, ed è ora abilitato il supporto NFS4\. Vedere [news bulletin](https://www.archlinux.org/news/452/).
*   portmap è stato sostituito da rpcbind.

## Contents

*   [1 Pacchetti richiesti](#Pacchetti_richiesti)
*   [2 Configurazione del server](#Configurazione_del_server)
    *   [2.1 File](#File)
        *   [2.1.1 /etc/exports](#.2Fetc.2Fexports)
        *   [2.1.2 /etc/conf.d/nfs-common.conf](#.2Fetc.2Fconf.d.2Fnfs-common.conf)
    *   [2.2 Demoni](#Demoni)
*   [3 Configurazione del client](#Configurazione_del_client)
    *   [3.1 File](#File_2)
        *   [3.1.1 /etc/conf.d/nfs-common.conf](#.2Fetc.2Fconf.d.2Fnfs-common.conf_2)
    *   [3.2 Demoni](#Demoni_2)
    *   [3.3 Montaggio](#Montaggio)
    *   [3.4 Montaggio tramite cifs](#Montaggio_tramite_cifs)
    *   [3.5 Auto-mount all'avvio](#Auto-mount_all.27avvio)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Performance scarse, bassa velocità di trasferimento e/o alto carico del sistema utilizzando NFS con collegamenti gigabit](#Performance_scarse.2C_bassa_velocit.C3.A0_di_trasferimento_e.2Fo_alto_carico_del_sistema_utilizzando_NFS_con_collegamenti_gigabit)
        *   [4.1.1 Async](#Async)
        *   [4.1.2 Packetsize](#Packetsize)
    *   [4.2 Il demone Portmap non si avvia correttamente durante il boot](#Il_demone_Portmap_non_si_avvia_correttamente_durante_il_boot)
    *   [4.3 Nfsd non si avvia, restituendo "nfssvc: No such device"](#Nfsd_non_si_avvia.2C_restituendo_.22nfssvc:_No_such_device.22)
    *   [4.4 rpcbind non si avvia e non mostra errori nell'avvio da terminale](#rpcbind_non_si_avvia_e_non_mostra_errori_nell.27avvio_da_terminale)
    *   [4.5 Nfsd sembra funzionare, ma non ci si connette da clients MacOS X](#Nfsd_sembra_funzionare.2C_ma_non_ci_si_connette_da_clients_MacOS_X)
    *   [4.6 mount.nfs: Operation not permitted](#mount.nfs:_Operation_not_permitted)
    *   [4.7 L'ownership delle condivisioni montate è 4294967294:4294967294](#L.27ownership_delle_condivisioni_montate_.C3.A8_4294967294:4294967294)
*   [5 Trucchi e suggerimenti](#Trucchi_e_suggerimenti)
    *   [5.1 Configurare fixed porte su NFS](#Configurare_fixed_porte_su_NFS)
*   [6 Link utili](#Link_utili)

## Pacchetti richiesti

I pacchetti necessari per l'installazione e la configurazione del server e del client sono pochi. Sarà solo necessario [installare](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils) dai [repositories ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

## Configurazione del server

Ora si potranno modificare i file di configurazione necessari e avviare i demoni.

### File

#### /etc/exports

Questo file (/etc/exports) definisce le varie condivisioni e i relativi permessi sul server nfs. Ad esempio:

```
/files *(ro,sync) # Accesso in sola lettura per chiunque
/files 192.168.0.100(rw,sync) # Accesso in lettura/scrittura da un client su 192.168.0.100
/files 192.168.1.1/24(rw,sync) #  Accesso in lettura/scrittura dai client compresi tra 192.168.1.1 e 192.168.1.255

```

Se si effettuano cambiamenti al file /etc/exports dopo aver avviato il demone, è possibile renderli effettivi digitando il seguente comando:

```
# exportfs -r

```

Se si decide di configurare il server nfs come pubblico e accessibile in scrittura, si può utilizzare l'opzione all_squash in combinazione con le opzioni anonuid e anongid. Per esempio, per impostare i privilegi per l'utente nobody nel gruppo nobody, si possono impostare i seguenti parametri:

```
; Accesso in lettura/scrittura ai client su 192.168.0.100, con accesso rw per l'utente 99 con gid 99
/files 192.168.0.100(rw,sync,all_squash,anonuid=99,anongid=99))

```

Questo inoltre significa che, se si vuole dare diritto di scrittura e lettura a questa direcotry, l'utente nobody.nobody deve essere il possessore della directory condivisa:

```
# chown -R nobody.nobody /files

```

Maggiori e più approfonditi dettagli sui file di export sono disponibili sulla man page exports.

#### /etc/conf.d/nfs-common.conf

**Nota:** Quanto utilizzato in /etc/conf.d/nfs è sostituito da "/etc/conf.d/nfs-common.conf" e "/etc/conf.d/nfs-server.conf".

E' possibile editare il file /etc/conf.d/nfs per passare particolari parametri a run-time a nfsd, mountd, statd, e sm-notify. Lo script di init nfs di default per Arch richiede l'opzione --no-notify per statd. Ad esempio:

```
STATD_OPTS="--no-notify"

```

Altre opzioni possono essere lasciate impostate come di default o cambiate a seconda delle proprie esigenze. E' opportuno far riferimento alle relative pagine di man per maggiori dettagli.

### Demoni

Potete ora avviare i demoni installati con i seguenti comandi:

```
# rc.d start rpcbind (or: rc.d start portmap)
# rc.d start nfs-common (or: rc.d start nfslock)
# rc.d start nfs-server (or: rc.d start nfsd)

```

E' importante notare che i serivzi vanno avviati nell'ordine specificato. Per avviare il server nfs all'avvio del sistema, aggiungere i demoni nella lista DAEMONS del file /etc/rc.conf. È necessario lanciare il demone da root o usando sudo se si fa partire da terminale.

## Configurazione del client

### File

#### /etc/conf.d/nfs-common.conf

Editare il file /etc/conf.d/nfs per passare le appropriate opzioni a run-time a statd - le rimanenti opzioni sono solo per il server. **NON** usare l'opzione --no-notify lato client, se non si conoscono le esatte conseguenze.

Fare riferimento al man di statd per maggiori dettagli.

### Demoni

Avviare i demoni rpcbind e nfs-common:

```
rc.d start rpcbind (or: rc.d start portmap)
rc.d start nfs-common (or: rc.d start nfslock)

```

L'ordine di avvio indicato è obbligatorio.

Per aviare automaticamente i demoni all'avvio del sistema aggiungerli nella lista DAEMONS del file /etc/rc.conf.

### Montaggio

Dopodichè è sufficiente montare normalmente:

```
mount server:/files /files

```

A differenza delle condivisioni CIFS o [rsync](/index.php/Rsync "Rsync"), gli exports NFS devono essere richiamati con il percorso completo sul server; ad esempio, se /home/fred/music è definita in /etc/exports sul server ELROND, si deve chiamare:

```
mount ELROND:/home/fred/music /mnt/point

```

o semplicemente utilizzare:

```
mount ELROND:music /mnt/point

```

altrimenti si otterrà *mount.nfs: access denied by server while mounting*

**Nota:** Se si ottengono i seguenti messaggi allora, probabilmente, non si sono avviati i demoni della [sezione precedente](#Demoni_2) o durante il loro avvio qualcosa è andato storto.
```
mount: wrong fs type, bad option, bad superblock on 192.168.1.99:/media/raid5-4tb,
       missing codepage or helper program, or other error
       (for several filesystems (e.g. nfs, cifs) you might
       need a /sbin/mount.<type> helper program)
       In some cases useful info is found in syslog - try
       dmesg | tail  or so

```

### Montaggio tramite cifs

Montare la stessa condivisione utilizzando cifs è leggermente diverso da NFS. Prima di tutto, è necessario definire la condivisione in Samba. Per fare ciò, vedere l'articolo [Samba](/index.php/Samba_(Italiano) "Samba (Italiano)"). Andiamo a creare una condivisione "ELROND" chiamandola "music". Per montare tale condivisione con cifs, dovrebbe funzionare il seguente comando

```
mount -t cifs -v ELROND:music /mnt/point -o guest,iocharset=utf8

```

Si può provare con:

```
mount -t cifs -v ELROND:music /mnt/point

```

O loggandosi con nome e password:

```
mount -t cifs -v ELROND:music /mnt/point -o username=USERNAME,password=PASSWORD,iocharset=utf8

```

Maggiori informazioni sono disponibili nella sezione [montaggio manuale](/index.php/Samba_(Italiano)#Montare_manualmente_una_condivisione "Samba (Italiano)") del wiki [samba](/index.php/Samba_(Italiano) "Samba (Italiano)"). Ora si è resa accessibile 1 cartella per clients NFS (in genere linux) e clients CIFS (in genere windows).

### Auto-mount all'avvio

Se volete che le directory condivise siano montate automaticamente all'avvio del sistema, assicuratevi che network, rpcbind (portmap), nfs-common (nfslock) e netfs siano presenti nella stringa DAEMONS in /etc/rc.conf nell'esatto ordine qui specificato. E' preferibile non inserire nessuna '@' davanti ai demoni (anche se si potrebbe tranquillamente utilizzare @netfs); ad esempio:

```
DAEMONS=(... network rpcbind nfs-common @netfs ...)

```

oppure

```
DAEMONS=(... network portmap nfslock @netfs ...)

```

aggiungere le opportune righe al file /etc/fstab, ad esempio:

```
server:/files /files nfs defaults 0 0

```

È anche possibile specificare la dimensione dei pacchetti in lettura e scrittura, in tal caso le dimensioni vanno specificate in fstab. I valori riportati di seguito sono quelli default, qualora non ne venissero specificati altri:

```
server:/files /files nfs rsize=32768,wsize=32768 0 0

```

Per ulteriori informazioni fare riferimento alla pagina di man di nfs, che include tutte le opzioni di montaggio disponibili.

## Risoluzione dei problemi

### Performance scarse, bassa velocità di trasferimento e/o alto carico del sistema utilizzando NFS con collegamenti gigabit

#### Async

Verificare che il flag async sia utilizzato in `/etc/exports` Esempio:

```
/nfs4exports		192.168.0.0/24(ro,fsid=0,no_subtree_check,async)
/nfs4exports/data	192.168.0.0/24(rw,no_subtree_check,async,nohide)
/nfs4exports/backup	192.168.0.0/24(rw,no_subtree_check,async,nohide)

```

#### Packetsize

Questo è un risultato delle dimensioni di default dei pacchetti impostate in NFS, che causa una significante frammentazione su reti gigabit. E' possibile modificare questo comportamento cambiando l'rsize e la wsize nei parametri di mount. Utilizzare rsize=32768,wsize=32768 dovrebbe essere sufficiente. E' importante notare che questo problema non si verifica su reti a 100 Mb, a causa di una velocità di trasferimento più bassa.

La dimensione utilizzata di defualt da NFS4 è 32786\. Il massimo è 65536\. Aumentare dal valore di default, a blocchi di 1024 finchè non si raggiunge la velocità massima di trasferimento.

### Il demone Portmap non si avvia correttamente durante il boot

Assicurarsi di aver inserito il demone portmap *prima* di netfs nell'array DAEMONS in /etc/rc.conf.

### Nfsd non si avvia, restituendo "nfssvc: No such device"

Assicurarsi che i moduli nfs e nfsd siano caricati nel kernel.

### rpcbind non si avvia e non mostra errori nell'avvio da terminale

Lanciare il demone da root o usando sudo.

```
sudo rc.d start rpcbind

```

### Nfsd sembra funzionare, ma non ci si connette da clients MacOS X

Quando si prova a connettersi da client MacOS X, dai log risulterà tutto ok, ma MacOS X rifiuterà di montare la condivisione NFS. E' necessario aggiungere l'opzione `insecure` option alla propria condivisione e ri-eseguire `exportfs -r`.

### mount.nfs: Operation not permitted

Dopo l'aggiornamento di nfs-utils alla versione 1.2.1-2, il montaggio della condivisione NFS smette di funzionare. D'ora in poi, nfs-utils utilizza NFSv4 di default al posto di NFSv3\. Il problema può essere risolto utilizzando l'opzione di montaggio `'vers=3'` oppure `'nfsvers=3'` dalla linea di comando:

```
# mount.nfs <remote target> <directory> -o ...,vers=3,...
# mount.nfs <remote target> <directory> -o ...,nfsvers=3,...

```

oppure in `/etc/fstab`:

```
<remote target> <directory> nfs ...,vers=3,... 0 0
<remote target> <directory> nfs ...,nfsvers=3,... 0 0

```

### L'ownership delle condivisioni montate è 4294967294:4294967294

E' necessario impostare in /etc/conf.d/nfs-common.conf (sul client) i due valori che seguono:

```
NEED_STATD="no"
NEED_IDMAPD="yes"

```

## Trucchi e suggerimenti

### Configurare fixed porte su NFS

Se si ha un firewall port-based, si potrebbero voler impostare delle porte. Per rpc.statd e rpc.mountd si dovrebbero impostare i seguenti settaggi in `/etc/conf.d/nfs-common` e `/etc/conf.d/nfs-server` (le porte possono essere differenti):

 `/etc/conf.d/nfs-common`  `STATD_OPTS="-p 4000 -o 4003"`  `/etc/conf.d/nfs-server`  `MOUNTD_OPTS="--no-nfs-version 2 -p 4002"`  `/etc/modprobe.d/lockd.conf` 
```
# Static ports for NFS lockd
options lockd nlm_udpport=4001 nlm_tcpport=4001
```

Quindi è necessario riavviare i demoni nfs e ricaricare il modulo lockd:

```
# modprobe -r lockd 
# modprobe lockd 
# rc.d restart nfs-common nfs-server
```

Dopo aver riavviato i demoni nfs e ricaricato il modulo, è possibile controllare le porte utilizzando il comando:

 `$ rpcinfo -p` 
```
rpcinfo -p
   program vers proto   port  service
    100000    4   tcp    111  portmapper
    100000    3   tcp    111  portmapper
    100000    2   tcp    111  portmapper
    100000    4   udp    111  portmapper
    100000    3   udp    111  portmapper
    100000    2   udp    111  portmapper
    100024    1   udp   4000  status
    100024    1   tcp   4000  status
    100021    1   udp   4001  nlockmgr
    100021    3   udp   4001  nlockmgr
    100021    4   udp   4001  nlockmgr
    100021    1   tcp   4001  nlockmgr
    100021    3   tcp   4001  nlockmgr
    100021    4   tcp   4001  nlockmgr
    100003    2   tcp   2049  nfs
    100003    3   tcp   2049  nfs
    100003    4   tcp   2049  nfs
    100003    2   udp   2049  nfs
    100003    3   udp   2049  nfs
    100003    4   udp   2049  nfs
    100005    3   udp   4002  mountd
    100005    3   tcp   4002  mountd
```

Quindi, è necessario aprire le porte 111-2049-4000-4001-4002-4003 tcp ed udp.

## Link utili

*   Vedere anche [Avahi](/index.php/Avahi "Avahi"), un'implementazione Zeroconf che consente il rilevamento automatico delle condivisioni NFS.
*   HOWTO: [Diskless network boot NFS root](/index.php/Diskless_network_boot_NFS_root "Diskless network boot NFS root")
*   [Veramente utile](http://publib.boulder.ibm.com/infocenter/pseries/v5r3/index.jsp?topic=/com.ibm.aix.prftungd/doc/prftungd/nfs_perf.htm)
*   Se si sta impostando un server Archlinux NFS per utilizzarlo da clients Windows tramite Microsoft's SFU, si risparmierà molto tempo seguendo quanto riportato [in questo post](https://bbs.archlinux.org/viewtopic.php?pid=523934#p523934)
*   [Microsoft Services for Unix NFS Client info](http://blogs.msdn.com/sfu/archive/2008/04/14/all-well-almost-about-client-for-nfs-configuration-and-performance.aspx)
*   [Unix interoperability and Windows Vista](http://blogs.msdn.com/sfu/archive/2007/05/01/unix-interoperability-and-windows-vista.aspx) Pre-requisiti per connettersi da Vista a NFS