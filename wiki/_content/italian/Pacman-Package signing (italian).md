Pacman-key è un nuovo tool disponibile con pacman 4\. Con la nuova implementazione dei pacchetti firmati, permette all'utente di amministrarne la lista delle chiavi affidabili in pacman.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduzione](#Introduzione)
*   [2 Installazione](#Installazione)
    *   [2.1 Configurare pacman](#Configurare_pacman)
    *   [2.2 Inizializzare il portachiavi](#Inizializzare_il_portachiavi)
*   [3 Gestire il portachiavi](#Gestire_il_portachiavi)
    *   [3.1 Verificare le cinque chiavi principali o master-key](#Verificare_le_cinque_chiavi_principali_o_master-key)
    *   [3.2 Aggiungere le chiavi degli sviluppatori](#Aggiungere_le_chiavi_degli_sviluppatori)
    *   [3.3 Aggiungere chiavi non ufficiali](#Aggiungere_chiavi_non_ufficiali)
    *   [3.4 Debugging con gpg](#Debugging_con_gpg)
*   [4 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [4.1 Impossibile importare le chiavi](#Impossibile_importare_le_chiavi)
    *   [4.2 Disabilitare il controllo delle firme](#Disabilitare_il_controllo_delle_firme)
    *   [4.3 Resettare tutte le chiavi](#Resettare_tutte_le_chiavi)
    *   [4.4 Rimuovere pacchetti non aggiornati](#Rimuovere_pacchetti_non_aggiornati)
    *   [4.5 Aggiornamento chiavi via proxy](#Aggiornamento_chiavi_via_proxy)
    *   [4.6 gpg: keyserver receive failed: No dirmngr](#gpg:_keyserver_receive_failed:_No_dirmngr)
*   [5 Fonti aggiuntive](#Fonti_aggiuntive)

## Introduzione

Il sistema di firmatura pacchetti in pacman utilizza il modello ["web of trust"](https://it.wikipedia.org/wiki/Web_of_trust) per assicurare che i pacchetti vengano dagli sviluppatori e non da qualcuno che si sostituisca a loro indebitamente. Gli sviluppatori dei pacchetti e i Trusted User hanno chiavi PGP individuali che utilizzano per firmare i propri pacchetti. Questo significa che loro garantiscono il contenuto del pacchetto. Anche l'utente comune possiede una PGP key unica, che viene generata quando questi configura pacman-key.

Le chiavi possono essere usate per firmare *altre* key. Ciò significa che il proprietario della chiave firmante garantisce per l'autenticità della chiave firmata. Per verificare un pacchetto, è necessario avere una catena di firme dalla propria chiave PGP al pacchetto stesso. Con la struttura di chiavi Arch questo può avventire in tre modi:

*   **Pacchetti personali (custom)**: l'utente crea da sé il proprio pacchetto e lo firma con una key personale.
*   **Pacchetti non ufficiali (unofficial)**: uno sviluppatore fa un pacchetto e lo firma. L'utente utilizza la propria key per firmare quella dello sviluppatore.
*   **Pacchetti ufficiali (official)**: uno sviluppatore fa un pacchetto e lo firma. La chiave dello sviluppatore viene convalidata dalle chiavi principali (master-key). L'utente fa poi affidamento su queste ultime per garantire gli sviluppatori.

Per un po' di storia sulla questione, si rimanda a questi articoli blog: [[1]](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/) [[2]](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/) [[3]](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/) [[4]](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/) e alla [proposta di controllo delle firme in Pacman](/index.php/Package_Signing_Proposal_for_Pacman "Package Signing Proposal for Pacman") della wiki.

**Nota:** Il protocollo HKP usa la porta 11371/tcp per comunicare. Per ricevere le chiavi firmate dai server (usando pacman-key), è richiesto che questa porta sia aperta.

## Installazione

### Configurare pacman

Prima di tutto, si deve decidere che livello di controllo si desidera. A determinarlo è l'opzione `SigLevel` nel file `/etc/pacman.conf`. Alcune possibilità sono menzionate nei commenti di quel file. Per un'esposizione più dettagliata, si rimanda alla [pagina di manuale `pacman.conf`](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking). Fondamentalmente si può abilitare il controlle delle firme a livello globale o per repository. Si tenga presente che settando il SigLevel a livello globale (globally) nella sezione [options], non sarà permesso di installare i propri pacchetti usando il comando `pacman -U`, a meno che siano firmati da una trusted key.

**Warning:** L'opzione `SigLevel` `TrustAll` esiste per uno scopo di debugging. Essa rende molto facile convalidare key che non sono state verificate. L'utente dovrebbe usare l'opzione `TrustedOnly` per tutti i repository ufficiali.

**Note:** Ad ora, Aprile 2012, il sistema di firme del database non è ancora stato completato, quindi si dovrebbe aggiungere l'opzione `DatabaseOptional` se si usa un livello di controllo `Required`, ad esempio: `SigLevel = Required DatabaseOptional TrustedOnly` In questo modo pacman installerà soltanto i pacchetti che sono firmati da chiavi che l'utente ha convalidato.

**Note:** Sembra che `SigLevel = PackageRequired` stia per diventare l'opzione standard per la verifica dei pacchetti ufficiali:
```
[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

### Inizializzare il portachiavi

Per inizializzare il portachiavi di pacman, usare il comando:

```
# pacman-key --init

```

Per questa inizializzazione è richiesta [entropia](https://en.wikipedia.org/wiki/Entropia "wikipedia:Entropia"). Per generarla, muovere il proprio mouse, premere caratteri a caso nella tastiera o avviare attività basata sul disco (ad esempio in un'altra console dare `ls -R /` o `find / -name foo` o `dd if=/dev/sda8 of=/dev/tty7`). Se il proprio sistema non ha già sufficiente entropia, questo potrebbe richiedere delle ore. Invece, generare in modo attivo entropia permette di completare il passaggio molto più velocemente.

La casualità creata viene utilizzate per impostae un nuovo portachiavi (`/etc/pacman.d/gnupg`) e la chiave GPG firmante principale del proprio sistema.

Affinché pacman comincia a controllare le firme dei pacchetti, si devono importare le chiavi degli sviluppatori nel proprio portachiavi. La prossima sezione spiegherà come fare.

**Nota:** Se si ha la necessità di eseguire `pacman-key --init` su un computer che non genera abbastanza entropia (ad esempio su un server headless), la generazione delle chiavi potrebbe richiedere molto tempo. Per generare della pseudo-entropia, si installi il pacchetto [haveged](https://www.archlinux.org/packages/?name=haveged) oppure [rng-tools](https://www.archlinux.org/packages/?name=rng-tools) sulla macchina in questione.

Si [avvii](/index.php/Systemd_(Italiano)#Usare_le_unità "Systemd (Italiano)") il servizio `haveged.service` prima di eseguire `pacman-key --init` da root.

## Gestire il portachiavi

### Verificare le cinque chiavi principali o master-key

L'installazione iniziale delle chiavi è ottenuta usando

```
# pacman-key --populate archlinux

```

È opportuno prendersi del tempo per verificare le [Chiavi principali](https://www.archlinux.org/master-keys/) quando vengono mostrate, in quanto sono usate per co-firmare (e convalidare) tutte le altre chiavi degli sviluppatori.

Le chiavi PGP di solito sono troppo grandi (2048 bit o più) perché le persone possano lavorarci, quindi di solito sono spezzate per creare una fingerprint a 40 cifre esadecimali, che possono essere usate per controllare a mano che le due chiavi siano le medesime. Le ultime otto cifre sono note come "key ID" (versione corta) e rappresentano una sorta di "nome" della key. Le ultime sedici cifre del fingerprint corrispondono all'ID lungo.

### Aggiungere le chiavi degli sviluppatori

Le chiavi degli sviluppatori ufficiali e dei Trusted User vengono firmate dalle master-key, quindi all'utente non sarà necessario usare pacman-key per firmarle in locale. Nel caso in cui pacman incontri una key e non la riconosca, domanderà all'utente se desidera scaricarla dal `keyserver` impostato in `/etc/pacman.d/gnupg/gpg.conf` (o usasndo l'opzione `--keyserver` da riga di comando). Wikipedia mette a disposizione una [lista di keyserver](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

Una volta che la chiave di uno sviluppatore è stata scaricata, non sarà necessario farlo una seconda volta: quella key verrà usata per verificare ogni pacchetto da lui firmato.

**Nota:** Il pacchetto [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) (una dipendenza di pacman) contiene le ultime chiavi.

E' possibile aggiornarle manualmente eseguendo:

```
# pacman-key --refresh-keys

```
Facendo `--refresh-keys`, anche la propria chiave locale sarà controllata sul keyserver remoto, e si riceverà una notifica sul fatto che non è stata trovata. Non è nulla di cui preoccuparsi.

### Aggiungere chiavi non ufficiali

È possibile utilizzare questo metodo per aggiungere la propria key al keyring di pacman, o quando si abilita un [repository firmato non ufficiale](/index.php/Unofficial_user_repositories "Unofficial user repositories").

**Nota:** Potrebbe essere necessario eseguire `dirmngr` come root: si veda [#gpg: keyserver receive failed: No dirmngr](#gpg:_keyserver_receive_failed:_No_dirmngr).

Prima di tutto, ci si deve procurare l'ID dal proprietario della key, quindi si deve aggiungere la chiave al keyring.

*   Se la chiave si trova su un keyserver, la si importi con: `# pacman-key -r <keyid>` 
*   Se invece viene fornito un link ad un keyfile, lo si scarichi e si esegua: `# pacman-key --add */percorso/al/keyfile*` 

Assicurarsi di verificare il fingerprint, come si farebbe per una chiave principale, o con ogni altra chiave che si stia per convalidare:

```
$ pacman-key -f *keyid*

```

Sarà quindi necessario firmare localmente la chiave appena importata:

 `# pacman-key --lsign-key *keyid*` 

In questo modo si permetterà alla chiave di firmare i pacchetti.

### Debugging con gpg

È possibile accedere al keyring di pacman direttamente tramite **gpg**. Esempio:

```
# gpg --homedir /etc/pacman.d/gnupg --list-keys

```

## Risoluzione dei problemi

**Attenzione:** *pacman-key* dipende dall'[orario](/index.php/System_time "System time") di sistema. Se è impostato in maniera errata, si avrà il seguente errore:
```
error: PackageName: signature from "User <email@archlinux.org>" is invalid
error: failed to commit transaction (invalid or corrupted package (PGP signature))
Errors occured, no packages were upgraded.
```

### Impossibile importare le chiavi

Questo problema può essere causato da:

*   Pacchetto [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) non aggiornato
*   Data incorretta
*   Il proprio ISP blocca le porte per l'importazione delle chiavi PGP
*   La propria cache di pacman contiene copie di pacchetti non firmati creati con tentativi precedenti

Si potrebbe essere impossibilitati a portare a termine un aggiornamento se il proprio pacchetto [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) non è aggiornato. Si provi ad [aggiornare il sistema](/index.php/Pacman_(Italiano)#Aggiornare_il_sistema "Pacman (Italiano)").

Se quanto sopra non funziona e la data è corretta si può provare ad utilizzare il keyserver MIT, che fornisce una porta alternativa. Per farlo, si modifichi `/etc/pacman.d/gnupg/gpg.conf` e si cambi la riga *keyserver* in:

```
keyserver hkp://pgp.mit.edu:11371

```

Se anche quanto sopra non è d'aiuto, si utilizzi il keyserver *kjsl*, che fornisce il servizio attraverso la porta 80 (HTTP).

```
keyserver hkp://keyserver.kjsl.com:80

```

Se si è disabilitato IPv6, gpg non funzionerà se verrà specificato un indirizzo IPv6\. Utilizzare quindi un keyserver IPv4 come:

 `keyserver hkp://ipv4.pool.sks-keyservers.net:11371` 

Qualora ci si fosse dimenticati di avviare `pacman-key --populate archlinux` si potrebbero avere degli errori tentando di importare le chiavi.

Se nessuno dei metodi di cui sopra funziona, è possibile che la propria cache di pacman, situata in `/var/cache/pacman/pkg/`, contenga copie di pacchetti non firmati creati con tentativi precedenti. Si provi ad eliminare la cache manualmente o eseguendo:

```
# pacman -Sc

```

Questo comando elimina dalla cache tutti i pacchetti non installati.

### Disabilitare il controllo delle firme

**Warning:** Usare con cautela. Disabilitare la firma dei pacchetti permette a pacman di installare automaticamente pacchetti inaffidabili.

Se non si è interessati alla firma dei pacchetti, è possibile disabilitare il controllo delle firme PGP completamente. È sufficiente modificare `/etc/pacman.conf` e scommentare la linea seguente sotto [options]:

```
SigLevel = Never

```

Inoltre, nei singoli repository, è necessario commentare ogni settaggio del SigLevel specifico, in quanto essi sovrascrivono la configurazione globale. Da ciò consegue l'assenza di controllo delle firme (il comportamento predefinito prima di pacman 4). Se si decide di farlo, non è necessario impostare un portachiavi con pacman-key. Sarà possibile modificare tale opzione, qualora si decida di abilitare la verifica dei pacchetti.

### Resettare tutte le chiavi

Se si desidera rimuovere ogni chiave installata nel proprio sistema, basta eliminare da root la cartella `/etc/pacman.d/gnupg` e dare di nuovo il comando `pacman-key --init` per generare una nuova chiave catena personale. Quindi sarà possibile procedere ad aggiungere nuove chiavi come meglio si desidera.

### Rimuovere pacchetti non aggiornati

Se gli stessi pacchetti continuano a fallire l'installazione o l'aggiornamento e si è certi di aver eseguito il procedimento d'installazione di pacman-key in maniera corretta, si provi a rimuovere questi pacchetti con `rm /var/cache/pacman/pkg/pacchettocattivo*`. In questo modo saranno riscaricati dal processo di aggiornamento.

Questa potrebbe essere la soluzione anche qualora si stia ricevendo un messaggio come `error: linux: signature from "Some Person <Some.Person@example.com>" is invalid` o simili quando si sta aggiornando (es. si potrebbe non essere vittima di un attacco MITM, dopo di tutto: semplicemente il pacchetto scaricato potrebbe essere corroto).

### Aggiornamento chiavi via proxy

Un bug in *gnupg* impedisce di aggiornare le chiavi tramite proxy ([https://bugs.g10code.com/gnupg/issue1786](https://bugs.g10code.com/gnupg/issue1786)).

Per aggirare il problema, è possibile procedere come segue:

Modificare `/etc/hosts`:

 `/etc/hosts` 
```
127.0.0.1 pool.sks-keyservers.net

```

Creare un tunnel con [socat](https://www.archlinux.org/packages/?name=socat). Il programma dovrà rimanere in ascolto sulla porta TCP 80, quindi sarà necessario eseguirlo da root:

```
# socat TCP-LISTEN:80,reuseaddr,fork PROXY:localhost:pool.sks-keyservers.net:80,proxyport=3128

```

Aggiornare le chiavi:

```
# pacman-key --refresh-keys

```

Annullare le modifiche apportate quando il proxy non è più necessario.

### gpg: keyserver receive failed: No dirmngr

Si veda [FS#42798](https://bugs.archlinux.org/task/42798). Si esegua:

```
# dirmngr < /dev/null

```

## Fonti aggiuntive

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/DeveloperWiki:Package_Signing_Proposal_for_Pacman "DeveloperWiki:Package Signing Proposal for Pacman")
*   [Firma dei pacchetti di Pacman – 1: Makepkg e Aggiunta Repo](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [Firma dei pacchetti di Pacman – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [Firma dei pacchetti di Pacman – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [Firma dei pacchetti di Pacman – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)