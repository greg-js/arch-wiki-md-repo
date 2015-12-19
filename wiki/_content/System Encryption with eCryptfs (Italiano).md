# System Encryption with eCryptfs (Italiano)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Introduzione](#Introduzione)
*   [2 Nozioni di base](#Nozioni_di_base)
    *   [2.1 Setup](#Setup)
    *   [2.2 Montare la cartella](#Montare_la_cartella)
    *   [2.3 Rimozione dei file e della cartella](#Rimozione_dei_file_e_della_cartella)
*   [3 Auto-mount al login](#Auto-mount_al_login)
*   [4 Nozioni avanzate](#Nozioni_avanzate)
    *   [4.1 PAM_Mount](#PAM_Mount)

# Introduzione

Questo articolo descrive l'utilizzo di base di [eCryptfs](https://launchpad.net/ecryptfs) e guiderà attraverso il processo di creazione di una cartella privata, cifrata e sicura, in _$HOME_, dove sarà possibile salvare tutti i dati sensibili. Se la domanda è "_Perché dovrei usare la crittografia?_" allora è bene iniziare leggendo l'articolo su [dm-crypt](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") che risponde alle domande di base sulla sicurezza.

A livello di implementazione eCryptfs differisce da dm-crypt: questo fornisce un layer virtuale cifrato su un dispositivo a blocchi, mentre eCryptfs è un filesystem a tutti gli effetti, per l'esattezza un filesystem con [cifratura a livello di filesystem stesso](http://en.wikipedia.org/wiki/Cryptographic_filesystems). Questa [tabella](http://ecryptfs.sourceforge.net/ecryptfs-faq.html#compare) compara i due sistemi.

In sintesi eCryptfs permette di non doversi preoccupare di pre-allocare spazio su disco per memorizzare i propri file, come ad esempio il dover creare partizioni separate: è possibile montare eCryptfs sopra a qualunque cartella per proteggerla. Sono incluse, ad esempio, l'intera $HOME di un utente oppure filesystem di rete (avendo condivisioni NFS cifrati). Tutti i metadata crittografici sono memorizzati negli header dei file così che i dati cifrati possono essere spostati o salvati per backup e poi recuperati senza problemi. Ci sono altri vantaggi, ma anche degli inconvenienti: eCryptfs non può cifrare intere partizioni per cui non può essere utilizzato per proteggere lo spazio di swap (per far ciò può essere però utilizzato congiuntamente con dm-crypt).

# Nozioni di base

eCryptfs fa parte di Linux fin dalla versione 2.6.19, ma per poterlo utilizzare sono richiesti gli strumenti per gestire lo spazio utente: va perciò installato il pacchetto [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) che a sua volta richiede il pacchetto [keyutils](https://www.archlinux.org/packages/?name=keyutils) (che contiene gli strumenti per gestire le chiavi di cifratura del portachiavi del kernel). Entrambi i pacchetti sono presenti in **AUR**.

Dopo l'installazione di questi pacchetti, potete caricare il modulo ecryptfs e continuare con il setup:

```
# modprobe ecryptfs

```

Il pacchetto ecryptfs-utils è distribuito con alcuni script che aiutano con la gestione della chiave ed altri compiti simili. Alcuni sono stati scritti per automatizzare l'intero processo di setup delle cartelle cifrate (_ecryptfs-setup-private_) o per aiutare a combinare ecryptfs con dm-crypt per proteggere lo spazio di swap (_ecryptfs-setup-swap_). Questa guida però non li utilizzerà descrivendo invece come procedere a livello manuale così da capire per bene come le cose vengono gestite.

Prima di procedere è bene consultare la documentazione di eCryptfs: questo tool è distribuito infatti con un completo e ben fatto insieme di pagine esplicative.

## Setup

La prima cosa da fare è creare la cartella privata. Nell'esempio che segue è stata chiamata per comodità _Private_:

```
$ mkdir ~/Private
$ chmod 700 ~/Private

```

(chmod 700 serve ad assegnare i permessi di accesso al solo proprietario). Adesso eCryptfs può essere montato sopra ad essa con

```
$ sudo mount -t ecryptfs ~/Private ~/Private

```

eCryptfs chiederà di rispondere ad alcune domande e di fornire una _passphrase_, cioè una frase di cifratura che sarà utilizzata per montare la cartella in futuro. E' comunque possibile avere differenti chiavi di cifratura per crittare differenti dati (per ulteriori informazioni si legga più sotto): per comodità questa guida si limiterà ad esaminare il caso di una unica chiave e di una unica _passphrase_. Ecco un esempio di primo montaggio con ecryptfs:

```
Key type: passphrase
Passphrase: FraseDiCifraturaCortaEMoltoDebole
Cypher: aes
Key byte: 16
Plaintext passtrough: no
Filename encryption: no
Add signature to cache: yes 

```

Analizziamo le varie voci:

*   La _passphrase_ è la **passphrase di montaggio** che sarà combinata con un _salt_ (un valore, il più delle volte casuale, che in crittografia viene aggiunto alla chiave per aumentare la robustezza della stessa): del risultato ottenuto verrà calcolato l'hash e quest'ultimo sarà poi inserito nel portachiavi del kernel.
    *   In ambito eCryptfs, il risultato del precedente passaggio è definito come "chiave di cifratura", o **fekek**.
*   eCryptfs supporta alcuni cifrari: AES, Blowfish, Twofish... E' possibile informarsi su di essi sulla Wikipedia.
*   "_Plaintext passtrough_" permette di salvare nella cartella cifrata file _non cifrati_.
*   La cifratura dei nomi dei file ("_Filename encryption_") è disponibile dal kernel Linux 2.6.29 e permette di rendere illeggibili anche i nomi dei file, non solo il loro contenuto.
    *   In ambito eCryptfs, la chiave utilizzata per proteggere i nomi dei file è nota come "chiave di cifratura dei nomi dei file" ("_Filename encryption key_"), o **fnek**.
*   La firma digitale della chiave (o delle chiavi) sarà salvata in /root/.ecryptfs/sig-cache.txt

Il setup è adesso completato e la cartella risulterà montata. E' ora possibile salvare qualunque dato nella cartella ~/Private, che sarà subito crittografato. Prima di proseguire è bene ispezionare il file **/etc/mtab**, in particolare la voce relativa ad ecryptfs (l'importanza di ciò sarà trattata a breve).

Per verificare se il setup è stato correttamente eseguito, basta copiare alcuni file nella cartella privata e poi smontarla: dovrebbero apparire illeggibili, cioè cifrati. Per riportarli alla normalità dobbiamo rieseguire il montaggio della cartella:

## Montare la cartella

Quando si rende necessario accedere ai file protetti basta ripetere la precedente operazione di montaggio utilizzando la stessa _passphrase_ e le stesse opzioni se si vuole accedere ai file precedentemente cifrati oppure utilizzare una _passphrase_ differente (e volendo anche opzioni diverse) se per qualche ragione si vuole avere differenti chiavi a protezione di differenti dati (un possibile scenario è quello in cui un'unica cartella è condivisa da più utenti, i quali salvano i propri file utilizzando ognuno la propria chiave).

In ogni caso il dover ogni volta ripetere questa procedura può risultare alla fine un po' noioso. La prima soluzione è quella di fornire tutte le opzioni al comando _mount_ (a questo punto entra in gioco il file **mtab** che è stato esaminato in precedenza), eccezion fatta per la _passphrase_, che sarà inserita su richiesta:

```
$ sudo mount -t ecryptfs -o ecryptfs_cipher=aes,ecryptfs_key_bytes=16,key=passphrase,ecryptfs_unlink_sigs,ecryptfs_passthrough=no,ecryptfs_enable_filename_crypto=no

```

La seconda soluzione è quella di inserire nel file **/etc/fstab** il punto di montaggio della cartella privata:

```
# eCryptfs mount points
/home/_username_/Private /home/_username_/Private ecryptfs rw,user,noauto,ecryptfs_sig=XXXXXXXXXX,ecryptfs_cipher=aes,ecryptfs_key_bytes=16,ecryptfs_unlink_sigs 0 0

```

Alcune precisazioni:

*   l'opzione _user_ è stata inserita per permettere all'utente di poter montare la cartella privata;
*   nell'opzione **ecryptfs_sig** va sostituito il valore "XXXXXXXXXX" con la firma digitale della propria chiave, ricavabile dal file **mtab** (come detto precedentemente) oppure dal file **sig-cache.txt**.

C'è un solo "problema" riguardo a questa soluzione: la _passphrase_. Quando la cartella privata viene smontata, la chiave viene cancellata dal portachiavi del kernel, per cui per poter eseguire un successivo montaggio bisogna inserirla in detto portachiavi un'altra volta. Per far ciò si può utilizzare una fra le utility **ecryptfs-add-passphrase** e **ecryptfs-manager** (contenute nel pacchetto ecryptfs-utils), che si appoggiano a loro volta all'utility **keyctl** contenuta nel pacchetto _keyutils_, installato come dipendenza.

Una volta che la chiave è stata inserita nel portachiavi, si può effettuare il montaggio della cartella:

```
$ ecryptfs-add-passphrase
  Passphrase: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx

$ mount -i /home/_username_/Private

```

Da notare che questa volta è stata utilizzata l'opzione "**-i**", che disattiva il richiamo dell'helper del comando mount. L'uso dell'opzione -i monta la cartella con le seguenti opzioni predefinite: **nosuid, noexec** e **nodev**. Per avere i file eseguibili all'interno della cartella privata occorre aggiungere l'opzione **exec** al punto di montaggio relativo alla cartella privata nel file /etc/fstab.

## Rimozione dei file e della cartella

Se si vuole spostare un file dalla cartella privata ad un'altra cartella, basta muoverlo nella sua nuova destinazione mentre ~/Private risulta montata.

Per rimuovere la cartella privata, basta accertarsi che risulti smontata e cancellarla, compresi tutti i file in essa contenuti.

# Auto-mount al login

eCryptfs ha una interessante caratteristica, sfruttata in alcune distribuzioni: quella di poter effettuare in automatico il montaggio della cartella privata al login dell'utente. Questa funzionalità non è molto documentata perché potrebbe esporre i propri dati personali a potenziali vulnerabilità: l'auto-mount decifra i file al login dell'utente ed essi rimangono accessibili ("in chiaro") fino al successivo logout dell'utente stesso. E' bene quindi utilizzare questa caratteristica solo in determinati casi, ad esempio quando si è certi che il proprio computer non sia accessibile da altri durante l'utilizzo. Risulta però comoda perché non obbliga tutte le volte ad inserire una lunga e complessa _passphrase_: basta la propria password di login. eCryptfs si interfaccia infatti con PAM ed usa la password di login dell'utente per decifrare la _passphrase_ che viene utilizzata poi per sbloccare la cartella privata. In questo modo la _passphrase_ "emerge" solo dopo che l'utente ha eseguito con successo il login.

Installato ecryptfs-utils, va caricato il modulo ecryptfs nel kernel con

```
# modprobe ecryptfs

```

Il resto del processo sarà eseguito direttamente dallo script **ecryptfs-setup-private** (contenuto sempre in ecryptfs-utils), lanciato come utente normale. Questo script esegue diverse operazioni in automatico, tra cui creare le 2 cartelle _~/Private_ (che conterrà il mount "in chiaro" dei dati cifrati) e _~/**.**Private_ (la cartella nascosta che conterrà i dati cifrati), dopodiché provvederà a richiedere la password di login e la _passphrase_ utilizzata per la cifratura vera e propria, che sarà cifrata con la prima. Ai fini della sicurezza, è bene che la _passphrase_ sia lunga e composta da lettere minuscole, maniuscole, numeri, segni di punteggiatura e quant'altro. E' anche possibile lasciare allo script il compito di crearne una semplicemente premendo "invio" alla richiesta di inserimento.

Infine inserirà la _passphrase_ nel portachiavi del kernel, in modo che al successivo login essa possa essere recuperata dal portachiavi e decifrata con la chiave di login dell'utente.

E' doveroso segnalare che ecryptfs-setup-private tenta, alla fine del processo, di eseguire alcune operazioni di test sulla nuova cartella cifrata ma su Arch questa operazione terminerà con un errore, anche se il processo è stato completato correttamente: si tratta solo di un problema nel tentativo di montaggio/smontaggio della cartella cifrata per cui non date peso al messaggio di errore e proseguite tranquillamente.

A questo punto bisogna editare il file relativo al tipo di login che l'utente effettua quando si collega al sistema: **/etc/pam.d/gdm** per Gnome, **/etc/pam.d/kde** per KDE o **/etc/pam.d/login** per il terminale. Ecco un esempio di modifica:

```
#%PAM-1.0
auth            requisite       pam_nologin.so
auth            required        pam_env.so
auth            required        pam_unix.so
#la linea seguente è stata aggiunta
**auth            required        pam_ecryptfs.so unwrap**
auth            optional        pam_gnome_keyring.so
account         required        pam_unix.so
session         required        pam_limits.so
session         required        pam_unix.so
#la linea seguente è stata aggiunta
**session         required        pam_ecryptfs.so unwrap**
session         optional        pam_gnome_keyring.so auto_start
password        required        pam_unix.so
#la linea seguente è stata aggiunta
**password        required        pam_ecryptfs.so**

```

Le linee da aggiungere sono quelle in grassetto.

**Attenzione**: è importante inserirle esattamente nei punti indicati altrimenti il processo di recupero della password non funzionerà in automatico.

Infine va modificato anche il file **/etc/rc.conf** inserendo il modulo _ecryptfs_ in MODULES, la lista dei moduli da caricare all'avvio.

Fatto questo, basta chiudere la propria sessione ed eseguire nuovamente il login. Se tutto è stato eseguito correttamente, la cartella ~/Private risulterà accessibile in chiaro come qualunque altra cartella del sistema mentre la cartella ~/.Private, che è il luogo dove materialmente saranno salvati, conterrà gli stessi file ma in forma cifrata.

# Nozioni avanzate

Questo articolo ha analizzato le nozioni di base necessarie a creare una cartella cifrata personale. C'è anche un altro articolo sull'uso di eCryptfs con Arch Linux, articolo che tratta della _cifratura dell'intera cartella $HOME_ e della _cifratura dello spazio di swap senza compromettere l'ibernazione (sospensione su disco)_. Esso analizza molti altri punti (ad esempio l'utilizzo dei moduli PAM ed il montaggio automatico) e l'autore ha deciso di non replicarlo qui perché non c'è solo un solo modo "giusto" di fare le cose. L'autore propone molte soluzioni e discute delle implicazioni che esse hanno sulla sicurezza, ma esse sono le sue soluzioni e potrebbero non essere le migliori né sono approvate dal progetto eCryptfs in alcun modo.

E' possibile leggere l'articolo qui: [eCryptfs and $HOME](http://sysphere.org/~anrxc/j/articles/ecryptfs/index.html)

## PAM_Mount

L'articolo citato nel precedente paragrafo utilizza un profilo per montare la cartella $HOME. Lo stesso può essere fatto utilizzando **pam_mount**, con il beneficio che la cartella $HOME viene smontata quando tutte le sessioni vengono chiuse. Dato che eCryptfs necessita dell'opzione -i, le impostazioni di lclmount devono essere modificate aggiungendo al file **pam_mount.conf.xml** quanto segue:

```
<lclmount>mount -i %(VOLUME) "%(before=\"-o\" OPTIONS)"</lclmount>

```

Per evitare di sprecare tempo inutilmente ad effettuare l'operazione di recupero della chiave è possibile creare uno script che controlla pmvarrun per vedere il numero di sessioni aperte:

```
#!/bin/sh
#/usr/bin/doecryptfs
exit $(/usr/sbin/pmvarrun -u$PAM_USER -o0)

```

Va anche aggiunta la seguente linea prima del modulo _unwrap_ nel file **/etc/pam.d/login**:

```
auth    [success=ignore default=1]    pam_exec.so     quiet /usr/bin/doecryptfs
auth    required                      pam_ecryptfs.so unwrap

```

Questa modifica deve però essere aggiunta ad ogni file di login contenuto in /etc/pam.d che viene usato (ad esempio /etc/pam.d/kde o /etc.pam.d/gdm).

Retrieved from "[https://wiki.archlinux.org/index.php?title=System_Encryption_with_eCryptfs_(Italiano)&oldid=412732](https://wiki.archlinux.org/index.php?title=System_Encryption_with_eCryptfs_(Italiano)&oldid=412732)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Security (Italiano)](/index.php/Category:Security_(Italiano) "Category:Security (Italiano)")
*   [File systems (Italiano)](/index.php/Category:File_systems_(Italiano) "Category:File systems (Italiano)")