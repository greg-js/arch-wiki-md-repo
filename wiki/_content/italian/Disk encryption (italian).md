Articoli correlati

*   [dm-crypt with LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS")
*   [eCryptfs](/index.php/ECryptfs "ECryptfs")
*   [TrueCrypt](/index.php/TrueCrypt "TrueCrypt")
*   [EncFS](/index.php/EncFS "EncFS")

Questo articolo discute le comuni tecniche disponibili in Arch Linux per proteggere in modo crittografico una parte di un disco dati (cartella, partizione, un intero disco), quindi tutti i dati che sono scritti in esso sono automaticamente criptati, e decriptati "al volo" quando sono letti.

"Dischi dati" in questo contesto possono essere hard disk di computer, dispositivi esterni come pen drive USB oppure DVD, così come dischi dati *virtuali* come dispositivi loop-back o cloud *(finché Arch Linux può riconoscerli come dispositivi a blocchi o filesystem)*

## Contents

*   [1 Perché usare la crittografia?](#Perch.C3.A9_usare_la_crittografia.3F)
    *   [1.1 Crittografia dei dati vs crittografia di sistema](#Crittografia_dei_dati_vs_crittografia_di_sistema)
*   [2 Metodi disponibili](#Metodi_disponibili)
    *   [2.1 Cifratura stacked filesystem](#Cifratura_stacked_filesystem)
    *   [2.2 Cifratura dei dispositivi a blocchi](#Cifratura_dei_dispositivi_a_blocchi)
    *   [2.3 Tabella di confronto](#Tabella_di_confronto)
        *   [2.3.1 *sommario*](#sommario)
        *   [2.3.2 *classificazione di base*](#classificazione_di_base)
        *   [2.3.3 *applicazioni pratiche*](#applicazioni_pratiche)
        *   [2.3.4 *caratteristiche di fruibilità*](#caratteristiche_di_fruibilit.C3.A0)
        *   [2.3.5 *caratteristiche di sicurezza*](#caratteristiche_di_sicurezza)
        *   [2.3.6 *caratteristiche di performance*](#caratteristiche_di_performance)
        *   [2.3.7 *specifiche della cifratura dei dispositivi a blocchi*](#specifiche_della_cifratura_dei_dispositivi_a_blocchi)
        *   [2.3.8 *specifiche della cifratura del filesystem stacked*](#specifiche_della_cifratura_del_filesystem_stacked)
        *   [2.3.9 *compatibilità & popolarità*](#compatibilit.C3.A0_.26_popolarit.C3.A0)
*   [3 Preparazione](#Preparazione)
    *   [3.1 Scegliere un setup](#Scegliere_un_setup)
    *   [3.2 Scegliere una buona password](#Scegliere_una_buona_password)
    *   [3.3 Preparare il disco](#Preparare_il_disco)
*   [4 Come funziona la crittografia](#Come_funziona_la_crittografia)
    *   [4.1 Princìpio di base](#Princ.C3.ACpio_di_base)
    *   [4.2 Keyfile e password](#Keyfile_e_password)
    *   [4.3 Ciphers and modes of operation](#Ciphers_and_modes_of_operation)
    *   [4.4 Cryptographic metadata](#Cryptographic_metadata)
    *   [4.5 Data integrity/authenticity](#Data_integrity.2Fauthenticity)
    *   [4.6 Plausible deniability](#Plausible_deniability)
*   [5 Notes & References](#Notes_.26_References)

## Perché usare la crittografia?

La crittografia dei dischi assicura che tutti i file immagazzinati sul disco siano criptati. I file diventeranno disponibili al sistema operativo e alle applicazioni solo quando il sistema corrente sarà sbloccato da un utente fidato. Leggere settori criptati senza i permessi restituirà dati messi a caso invece dei file effettivi.

Per esempio, la crittografia può prevenire visioni non autorizzate dei dati quando il computer o l'hard disk:

*   è situato in un posto dove persono non fidate possono avere accesso mentre voi non ci siete
*   è perso o rubato, come i computer portatili, netbook o dispositivi esterni di dati
*   è in riparazione
*   ha finito il suo ciclo di vita

In aggiunta, la crittografia può essere usata anche per aumentare la sicurezza in caso di attacchi informatici. Per esempio, l'installazione di keyloggers o di cavalli di troia (Trojan) da parte di hacker che hanno l'accesso fisico al sistema mentre non ci siete.

**Attenzione:** La crittografia **non** protegge i tuoi dati da **tutti** gli attacchi.

Compreso quanto segue:

*   Hacker che possono entrare nel tuo sistema (es. attraverso internet) mentre è acceso e dopo che le parti del disco criptate sono state sbloccate e mountate.
*   Hacker che sono capaci di avere l'accesso fisico al computer mentre è acceso, e hanno le risorse per portare a termine un [cold boot attack](https://en.wikipedia.org/wiki/Cold_boot_attack "wikipedia:Cold boot attack").
*   Un'entità governativa che non solo ha le risorse per portare a termine un cold bold attack, ma può semplicemente forzarvi a consegnare le password usando varie tecniche di [coercizione](https://en.wikipedia.org/wiki/Coercizione "wikipedia:Coercizione").Nella maggior parte delle nazioni non democratiche nel mondo, così come negli Stati Uniti e nel Regno Unito, questo è legale per la polizia federale se ha dei sospetti che voi stiate nascondendo qualcosa nel loro interesse.

Un'impostazione di crittografia molto forte (es. crittografia di sistema completa con partizione di boot senza plaintext e controllo di autenticità) è richiesta per avere una possibilità di resistere a hacker professionisti, i quali sono capaci di corrompere il vostro sistema prima che di usarlo. E anche in quel caso non si sa se può davvero prevenire tutti i tipi di attacchi (es. [hardware keylogger](https://en.wikipedia.org/wiki/Hardware_keylogger "wikipedia:Hardware keylogger")). Il miglior rimedio potrebbe essere [hardware-based full disk encryption](https://en.wikipedia.org/wiki/Hardware-based_full_disk_encryption "wikipedia:Hardware-based full disk encryption") (es. [trusted computing](https://en.wikipedia.org/wiki/Trusted_computing "wikipedia:Trusted computing").)

**Attenzione:** La crittografia dei dischi non vi proteggerà da qualcuno semplicemente [cancellando il tuo disco](/index.php/Securely_wipe_disk "Securely wipe disk"). [backup regolari](/index.php/Backup_programs "Backup programs") sono raccomandati per mantenere i tuoi dati sicuri.

### Crittografia dei dati vs crittografia di sistema

[Wikipedia:Disk encryption](https://en.wikipedia.org/wiki/Disk_encryption "wikipedia:Disk encryption") **Crittografia dei dati**, definita come crittografia solo dei dati dell'utente (spesso situati in `/home`, o in un dispositivo rimovibile come un DVD dati) è il metodo più semplice e meno intrusivo di crittografare i dati, ma ha alcuni inconvenienti. Nei moderni sistemi di computer, ci sono molto processi in background che potrebbero immagazzinare informazioni sui dati dell'utente in aree non protette del disco, come:

*   partizioni di swap
    *   *(rimedio: disabilitare la partizione di swap)*
*   `/tmp` (file temporanei creati dalle applicazioni dell'utente)
    *   *(rimedio: evitare queste applicazioni; montare `/tmp` in un [ramdisk](/index.php/Ramdisk "Ramdisk"))*
*   `/var` (file di log e database; per esempio mlocate immagazzina un catalogo di tutti i file in `/var/lib/mlocate/mlocate.db`)

In aggiunta, una crittografia dei dati pura lascerà il sistema vulnerabile agli attacchi offline *(guarda sopra)*.

**Crittografia di sistema**, definita come crittografia del sistema operativo e dei dati dell'utente, aiuta a indirizzare alcune incapacità della crittografia dei dati.

Vantaggi:

*   Previene accessi fisici non autorizzati ai file del sistema operativo *(guarda sopra)*.
*   Previene accessi fisici non autorizzati ai dati privati che potrebbero essere immagazzinati dal sistema.

Svantaggi:

*   Sbloccare/bloccare le parti criptate del disco può non coincidere con il login/logout dell'utente, poichè ora lo sblocco richiede di essere verificato prima o durante l'avvio.

In pratica, non c'è sempre una linea tra la crittografia dei dati e la crittografia di sistema, e non ci sono molti compromessi e impostazioni personalizzate.

In ogni caso, la crittografia dovrebbe essere vista solo come un aggiunta ai meccanismi di sicurezza del sistema operativo - concentrata sul mettere al sicuro accessi fisici offline, mentre si affida a **altre** parti del sistema per fornire cose come la sicurezza della rete e il controllo dell'accesso degli utenti.

## Metodi disponibili

Tutti i metodi di cifratura operano in modo tale che anche se il disco contiene effettivamente dati crittografati, il sistema operativo e le applicazioni vedono essi come i corrispondenti dati normali leggibili finché il contenitore crittografico (ossia la parte logica del disco che contiene i dati crittografati) è "sbloccato" e montato.

Per far accadere questo, alcune informazioni segrete (di solito sono keyfile e/o password) devono essere fornite dall'utente, dal quale la reale chiave di cifratura può essere derivata (e immagazzinata nel portachiavi del kernel per la durata della sessione).

Se non si è del tutto pratici con questo tipo di operazione, per favore leggi prima la sezione [#How the encryption works](#How_the_encryption_works).

I seguenti metodi di cifratura possono essere distinti in due tipi dal layer dell'operazione:

### Cifratura stacked filesystem

Le soluzioni della cifratura Stacked filesystem sono messe in pratica come uno strato che immagazzina all'inizio del filesystem esistente, scrivendo tutti i file in una cartella a cifratura-attiva per essere cifrati 'on-the-fly' prima che il filesystem li scriva nel disco, e decifrati ogni volta che il filesystem li legge dal disco. Con questo metodo, i file sono immagazzinati nel filesystem ospitante in forma cifrata (significa che i loro contenuti, e di solito anche i noi dei file/cartelle, sono sostituiti da caratteri casuali della stessa lunghezza), ma diversamente essi esistono in quel filesystem come se non fossero cifrati, come file normali.

Il modo in cui è applicato, è che per sbloccare la cartella che contiene i file raw cifrati nel filesystem ospitante ("cartella inferiore"), è montato (usando uno speciale stacked pseudo-filesystem) su se stesso o facoltativamente in una posizione differente ("cartella superiore"), dove gli stessi file poi compaiono in forma leggibile - fincheé non è smontato di nuovo, o il sistema si spegne.

Le soluzioni disponibili in questa categoria sono:

	[eCryptfs](/index.php/ECryptfs "ECryptfs")

	*...*

	[EncFS](/index.php/EncFS "EncFS")

	*...*

### Cifratura dei dispositivi a blocchi

I metodi di cifratura dei dispositivi a blocchi, d'altronde, operano sotto lo strato del filesystem e assicurano che tutto sia scritto in un dispositivo a blocchi (ossia un disco intero, o una partizione, o un file che si comporta come un dispositivo virtuale loop-back) cifrato. Ciò significa che mentre il dispositivo a blocchi è spento, il suo intero contenuto assomiglia a una grande macchia di dati casuali, senza la possibilità di determinare che tipo di filesystem sia e quali dati contenga. Si può accedere ai dati, montando il contenitore protetto (in questo caso un dispositivo a blocchi) in una posizione arbitraria in un modo speciale.

Le seguenti soluzioni di cifratura di un dispositivo a blocchi sono disponibili in Arch Linux:

	[loop-AES](/index.php?title=Loop-AES&action=edit&redlink=1 "Loop-AES (page does not exist)")

	*loop-AES è un discendente di cryptoloop ed è una soluzione sicura e veloce per i sistemi di crittografia.*

	*Tuttavia loop-AES è considerato meno user-friendly rispetto alle altre soluzioni e richiede un supporto kernel non-standard.*

	[dm-crypt + LUKS](/index.php/System_Encryption_with_LUKS "System Encryption with LUKS")

	*dm-crypt è la funzionalità standard per cifrare fornita dal kernel Linux. Esso può essere usato direttamente da chi vuole avere il completo controllo di tutti gli aspetti di partizioni e amministrazione delle chiavi.*

	*LUKS è uno strato ulteriore di comodità che memorizza tutti i dati di configurazione necessari per dm-crypt sul disco stesso e riassume l'amministrazione delle partizioni e delle chiavi per migliorare la facilità d'uso.*

	[TrueCrypt](/index.php/TrueCrypt "TrueCrypt")

	*...*

Per le implicazioni pratiche del livello di operazione scelto vedi la seguente [tabella di confronto](#practical_implications) così come [[1]](http://ecryptfs.sourceforge.net/ecryptfs-faq.html#compare).

### Tabella di confronto

| 

##### *sommario*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

tipo

 | cifratura di un dispositivo a blocchi | cifratura stacked filesystem |

principali punti di forza

 | il meno recente; probabilmente il più veloce; funziona sui sistemi legacy | lo standard di fatto per la cifratura dei dispositivi a blocchi su Linux; molto flessibile | molto portabile, ben mantenuto, soluzione auto controllata | leggermente più veloce rispetto a EncFS; cifra file singoli portabili tra i sistemi | il più facile da usare; supporta amministrazione non-root |

disponibilità in Arch Linux

 | bisogna ricompilare il kernel | *moduli kernel:* già caricati con il kernel di default; *strumenti:* [device-mapper](https://www.archlinux.org/packages/?name=device-mapper), [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) [core] | [truecrypt](https://www.archlinux.org/packages/?name=truecrypt) [extra] | *moduli kernel:* già caricati con il kernel di default; *strumenti:* [ecryptfs-utils](https://www.archlinux.org/packages/?name=ecryptfs-utils) [community] | [encfs](https://www.archlinux.org/packages/?name=encfs) [community] |

license

 | GPL | GPL | custom | GPL | GPL |
| 

##### *classificazione di base*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

cifra...

 | interi dispositivi a blocchi | file |

contenitore per i dati cifrati può essere...

 | 

*   un disco o una partizione
*   un file che si comporta come una partizione virtuale

 | 

*   una cartella in un filesystem esistente

 |

relazione con il filesystem

 | opera sotto lo strato del filesystem - non importa se il contenuto del dispositivo a blocchi cifrato è un filesystem, un partition table, un LVM setup, o altro. | aggiunge uno strato aggiuntivo nel filesystem esistente, per cifrare/decifrare automaticamente i file quando sono scritti/letti |

cifratura implementata nel...

 | kernelspace | kernelspace | kernelspace | kernelspace | userspace
*(usando FUSE)* |

metadati cifrati memorizzati in...

 | ? | ? | ? | l'inizio di ogni file cifrato | file di controllo al livello superiore di ogni contenitore EncFS |

chiave di cifratura memorizzata in...

 | ? | ? | ? | la chiave può essere posizionata ovunque | nel file di controllo all'inizio di ogni contenitore EncFS |
| 

##### *applicazioni pratiche*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

metadati (numero di file, struttura delle cartelle, dimensioni dei file, permessi mtimes, etc.) cifrati

 | ✔ | ✖
*(è possibile anche cifrare i nomi dei file e delle cartelle)* |

può essere usato per cifrare interi dischi rigidi (incluse tabelle di partizioni)

 | ✔ | ✖ |

può essere usato per cifrare le partizioni di swap

 | ✔ | ✖ |

può essere usato senza pre-allocare una quantità fissa di spazio per il contenitore di dati cifrati

 | ✖ | ✔ |

può essere usato per proteggere filesystem esistenti senza l'accesso ai dispositivi a blocchi, es. filesystem NFS e Samba, cloud, etc.

 |     ✖ | ✔ |

permette backup dei file cifrati offline

 | ✖ | ✔ |
| 

##### *caratteristiche di fruibilità*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

permette il montaggio automatico dei filesystem al login

 | ? | ? | ? | ? | ✔ |

permette lo smontaggio automatico dei filesystem in caso di inattività

 | ? | ? | ? | ? | ✔ |

utenti non-root posso creare/eliminare contenitori per dati cifrati

 | ✖ | ✖ | ✖ | ✖ | ✔ |

fornisce una GUI

 | ✖ | ✖ | ✔ | ✖ | ✖ |
| 

##### *caratteristiche di sicurezza*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

cifrature supportate

 | AES | AES, Twofish, Serpent | ? | AES, blowfish, twofish... | AES, Twofish |

supporto per il salting

 | ? | ✔
(with LUKS) | ✔ | ✔ | ? |

supporto per cifrature multiple scalate

 | ? | ? | ✔ | ? | ✖ |

supporto per la diffusione di key-slot

 | ? | ✔
(with LUKS) | ? | ? | ? |

protezione contro la forzatura delle chiavi

 | ✔ | ? | ? | ? | ? |

supporto per chiavi multiple usate sugli stessi dati

 | ? | ✔
(with LUKS) | ? | ? | ✖ |
| 

##### *caratteristiche di performance*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

supporto per il multithreading

 | ? | ✖ | ✔ | ? | ? |

supporto per la cifratura con accelerazione hardware

 | ? | ? | ✔ | ✔ | ? |

ottimizzato per il trattamento di file sparsi

 | ? | ? | ? | ✖ | ? |
| 

##### *specifiche della cifratura dei dispositivi a blocchi*

 | Loop-AES | dm-crypt + LUKS | Truecrypt |

supporto per il ridimensionamento manuale del dispositivo a blocchi cifrato

 | ? | ✔ | ✖ |
| 

##### *specifiche della cifratura del filesystem stacked*

 | eCryptfs | EncFs |

filesystem supportati

 | ext3, ext4, xfs (with caveats), jfs, nfs... | ? |

capacità di cifrare i nomi dei file

 | ✔ | ✔ |

capacità di *non* cifrare i nomi dei file

 | ✔ | ✔ |
| 

##### *compatibilità & popolarità*

 | Loop-AES | dm-crypt + LUKS | Truecrypt | eCryptfs | EncFs |

versioni del kernel Linux supportate

 | 2.0 or newer | ? | ? | ? | 2.4 or newer |
 i dati cifrati possono essere letti da... | Windows | ✔ (with ) | ✔ (with ) | ✔ | ? | ? |
 Mac OS X | ? | ? | ✔ | ? |     ✔ |
 FreeBSD | ? | ? | ✖ | ? |     ✔ |

usato da

 | ? | 

*   *Arch Linux installer* (system encryption)
*   *Ubuntu alternate installer* (system encryption)

 | ? | 

*   *Ubuntu installer* (home dir encryption)
*   *Chromium OS* (encryption of cached user data)

 | ? |

## Preparazione

### Scegliere un setup

Il setup di cifratura dei dischi appropriato per te dipende dai tuoi scopi (per favore leggi [#Perché usare la crittografia?](#Perch.C3.A9_usare_la_crittografia.3F) sopra) e le specifiche del tuo sistema..
Tra le altre cose, dovrai rispondere alle seguenti domande:

*   Da che tipo di hacker (attacker) ti vuoi proteggere?
    *   Utente di computer casuale che sta provando a spiare passivamente i contenuti del tuo disco mentre il tuo sistema è spento/non funzionante.
    *   Studente di crittogrammi che può ottenere ripetuti accessi in lettura/scrittura nel tuo sistema dopo che lo hai usato.
    *   niente di simile

*   Quale strategia di cifratura sarà impiegata?
    *   cifratura dei dati
    *   cifratura del sistema
    *   qualcosa di simile
    *   Come ci si potrebbe occupare dello swap? `/tmp`?
        *   lo ignoro, e spero che nessun dato sia stato rubato
        *   Swap disabilitato, oppure montato come ramdisk
        *   Swap cifrato *(come parte di una completa cifratura del disco)*

*   Come dovrebbero essere sbloccati le parti del disco cifrate?
    *   password *(la stessa del login, o diversa)*
    *   file con la chiave *(es. dentro a una pen drive USB, che bisogna tenere in posto sicuro)*
    *   Tutti e due

*   *Quando* le parti cifrate del disco dovrebbero essere sbloccare?
    *   prima dell'avvio
    *   durante l'avvio
    *   al login
    *   manualmente *(after login)*

*   Come sarebbero sistemati gli utenti multipli?
    *   non ci sono
    *   usando una chiave condivisa
    *   più chiavi indipendenti e revocabili per la stessa parte di disco
    *   parti del disco cifrate separate per utenti diversi

Dopo puoi fare le scelte tecniche richieste (vedi [#Metodi disponibili](#Metodi_disponibili) e [#How_the_encryption_works](#How_the_encryption_works) circa:

*   crittografia stacked filesystem vs. cifratura dei dispositivi a blocchi
*   amministrazioni delle chiavi
*   cifratura
*   memorizzazione dei metadatim
*   posizione della "cartella inferiore" (in caso di cifratura stacked filesystem)
*   ...

In pratica, puoi scegliere qualcosa di simile a questo:

	***Esempio 1:*** cifratura dei dati semplice (hard disk interno)

	ve) • **una cartella chiamata "~/Private"** nella cartella home dell'utente cifrata con *EncFS* *├──> versioni cifrate dei file dentro ~/.Private* *└──> sbloccate al momento con una password dedicata*

	***Esempio 2:*** cifratura dei dati semplice (disco rimobivile)

	• **intero disco USBw** cifrato con *TrueCrypt* *└──> sbloccato quando collegato al computer* *(usando una password dedicata + un file .jpg che sarebbe un keyfile*

	***Esempio 3:*** cifratura del sistema parziale

	• ogni **cartella home** dell'utente cifrata con *eCryptfs* *└──> sbloccata al login, usando la password di login* • le partizioni **swap** e **/tmp** cifrate con *dm-crypt+LUKS* *└──> usando un chiave portabile automaticamente generata per sessione* • indicizzazione/cache dei contenuti di /home da slocate (e applicazioni simili) non cifrate

	***Example 4:*** cifratura del sistema

	• **intero hard disk eccetto la partizione di boot** cifrato con *dm-crypt+LUKS* *└──> sbloccato durante l'avvio, usando una pen drive USB con keyfile (condiviso da tutti gli utenti)*

	***Example 5:*** cifratura del sistema paranoica

	• **intero hard disk** cifrato con *dm-crypt+LUKS* *└──> sbloccato prima dell'avvio usando una password dedicata più un keyfile dentro a una pen drive USB* *(differente per ogni utente - indipendentemente revocabile* • **partizione di /boot** posizionata sulla pen drive USB usata prima

Molte e molte altre combinazioni sono possibili. Dovresti pianificare che tipo di setup sarà appropriato per il tuo sistema.

### Scegliere una buona password

Quando fai affidamento a una password, essa deve essere completa abbastanza da non essere facile da indovinare o scavalcare usando attacchi brute-force. I princìpi di una buona password sono basati sulla *lunghezza* e *casualità d'ordine*
Vedi [The passphrase FAQ](http://www.iusmentis.com/security/passphrasefaq/) e considera di usare il metodo [Diceware Passphrase](http://world.std.com/~reinhold/diceware.html).

Un altro aspetto della forza di una password è che non deve essere facilmente recuperabile da altri posti. Se si usa la stessa password per la cifratura del disco e per il login (utile per esempio auto montare la partizione o la cartella cifrata al login), assicurati che `/etc/shadow` non finisca su una partizione cifrata, oppure usa un buon algoritmo hash (cioè sha512/bcrypt, non md5) per la password memorizzata (vedi [SHA password hashes](/index.php/SHA_password_hashes "SHA password hashes") per altre info).

### Preparare il disco

Prima di iniziare il setup della cifratura del disco su un (parte di un) disco, considera di eseguire una pulizia accurata di esso. Questo consiste nel sovrascrivere l'intero disco o partizione con un flusso di zero byte, e va fatto ciò per le seguenti ragioni:

*   **prevenire il recupero dei dati memorizzati precedentemente**

    La cifratura non cambia il fatto che i settori individuali vengano scritti al momento, quando il sistema crea o modifica dei dati in quei particolari settori (vedi [#How_the_encryption_works](#How_the_encryption_works) sotto). I settori che il filesystem considera "non usati al momento" non sono toccati, e potrebbero ancora contenere rimasugli di dati dei filesystem precedenti. L'unico modo per essere sicuri che tutti i dati memorizzati precedentemente sul disco non possano essere [recuperati](https://en.wikipedia.org/wiki/Recupero_dati "wikipedia:Recupero dati"), è di cancellarli manualmente.

*   **prevenire la divulgazione dei modelli d'uso del disco cifrato**

    Idealmente, l'intera parte cifrata del disco dovrebbe essere indistinguibile dai dati casuali. In questo modo, le persone non autorizzate non possono conoscere quali settori contengono effettivamente dati cifrati - che potrebbe essere un obbiettivo desiderabile (come parte della vera riservatezza), ed anche funziona da ostacolo aggiuntivo contro gli attacker che cercano di rompere la cifratura.
    Per questi motivi, ripulire l'hard disk usando dei dati casuali d'alta qualità è decisivo.

Il secondo motivo ha senso con la cifratura del dispositivo a blocchi, perché in caso di cifratura stacked filesystem i dati cifrati sono comunque facilmente identificabili (in forma di distinti file cifrati nel filesystem ospitante). Ricordare anche che se si intende cifrare una cartella particolare, si dovrà cancellare l'intera partizione se si vuole sbarazzare completamente dei file precedentemente memorizzati in quella cartella in forma non cifrata. Se ci sono altre cartelle sulla stessa partizione, si dovrà fare il backup di essi e riposizionarli a fine pulizia.

Non appena si ha deciso quale tipo di disco si vuole impegnare, vedere l'articolo [Securely wipe disk](/index.php/Securely_wipe_disk "Securely wipe disk") per istruzioni tecniche.

**Tip:** Nel decidere quale metodo usare per una sicura cancellazione dell'hard disk, ricorda che non ci sarò bisogno di rifarlo più di una volta fino a quando l'unità non è utilizzata come unità crittografata.

## Come funziona la crittografia

Questa sezione è intesa come un'introduzione di alto livello ai concetti e i processi che sono il cuore delle configurazioni di crittografia del disco.

Essa non va dentro dettagli di tipo tecnico e matematico (consulta l'appropriata letteratura per questo), ma dovrebbe far capire ad un amministratore di sistema come le diverse configurazioni (specialmente l'amministrazione delle chiavi) possono influire sulla sicurezza e l'usabilità.

### Princìpio di base

Per i fini della crittografia del disco, ogni dispositivo a blocchi (o file nel caso di crittografia di stacked filesystem) è diviso in **settori** di uguale lunghezza, per esempio 512 byte (4096 bit). La cifratura/decifratura avviene per ogni singolo settore, quindi il settore "n" del dispositivo a blocchi/file immagazzinerà la versione cifrata del settore "n" dei dati originali.

Ogni volta che il sistema operativo o l'applicazione richiede un certo frammento di dato dal dispositivo a blocchi/file, l'intero settore/i che contiene i dati sarà letto dal disco, decifrato al volo, e temporaneamente immagazzinato nella memoria:

```
           ╔═══════╗
 settore 1 ║"???.."║
           ╠═══════╣         ╭┈┈┈┈┈┈╮
 settore 2 ║"???.."║         ┊chiave┊
           ╠═══════╣         ╰┈┈┬┈┈┈╯
           ⁝        ⁝             │ 
           ╠═══════╣            ▼              ┣┉┉┉┉┉┉┉┫
 settore n ║"???.."║━━━━━━━(decifratura)━━━━━━▶┋"abc.."┋ sector n
           ╠═══════╣                           ┣┉┉┉┉┉┉┉┫
           ⁝        ⁝
           ╚═══════╝

          file o                               dati non
          dispositivo a blocchi                cifrati in
          cifrato                              memoria

```

Analogamente, in ogni operazione di scrittora, tutti i settori interessati devono essere ri-cifrati completamente (mentre il resto dei settore rimane uguale).

### Keyfile e password

Prima di cifrare/decifrare i dati, il sistema di cifratura del disco deve conoscere la "chiave" univoca associata ad esso. Questa è una stringa generata casualmente di una certa lunghezza, per esempio 32 byte (256 bit).

Ogni volta che il dispositivo a blocchi o la cartella cifrata in questione deve essere montata, la sua chiave corrispondente (chiamata d'ora in avanti "master key") deve essere ripresa - di solito da una delle seguenti posizioni:

*   ***memorizzata in un keyfile***

    Semplicemente memorizzando la master key in un file (in forma leggibile), è l'opzione più semplice. Il file - chiamato keyfile - può essere posizionato su una pen drive USB riposta in una posizione sicura e essere usato soltanto quando bisogna montare una parte cifrata del disco (es. durante il boot o il login).

*   ***memorizzata in un keyfile o nel disco stesso in modalità cifrata con password***

    La master key (e quindi i dati cifrati) può essere protetta con una password segreta, che bisogna ricordare ed immettere ogni volta che si vuole montare il dispositivo a blocchi o cartella cifrato.

    Una configurazione comune è applicare la -così chiamata- "key stretching" alla password (attraverso la funzione "key derivation"), e usare la password risultante come chiave per decifrare la master key attuale (che è stata precedentemente memorizzata in forma cifrata):

    ```
     ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮                         ╭┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╮
     ┊ password di mount ┊━━━━━⎛key derivation⎞━━━▶┊chiave di mount┊
     ╰┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈╯ ,───⎝   function   ⎠    ╰┈┈┈┈┬┈┈┈┈┈┈┈┈┈┈╯
     ╭──────╮            ╱                              │
     │ salt │───────────´                               │
     ╰──────╯                                           │
     ╭─────────────────────╮                            ▼          ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
     │ master key cifrata  │━━━━━━━━━━━━━━━━━━━━━━(decifratura)━━━▶┊ master key ┊
     ╰─────────────────────╯                                       ╰┈┈┈┈┈┈┈┈┈┈┈┈╯

    ```

    La **key derivation function** (es. PBKDF2 o scrypt) è deliberatamente lenta (applica molte ripetizioni alla funzione has, es. 1000 ripetizione di HMAC-SHA-512), quindi gli attacchi brute-force che cercano la password sono inattuabili. Per un uso normale di un utente autorizzato, la chiave dovrà essere calcolata solo una volta per sessione, quindi il rallentamento non è un problema.
    Inoltre essa richiede dei dati addizionati, chiamati "**salt**", questo è generato casualmente durante la configurazione della cifratura del disco e memorizzato in modo non protetto come una parte dei metadati cifrati. Poiché ci sarà un valore differente per ogni configurazione, sarà inattuabile per gli hacker velocizzare gli attacchi brute-force unando tabelle 'precomputed' per la 'key derivation function'.

    The **encrypted master key** can be stored on disk together with the encrypted data. This way, the confidentiality of the encrypted data depends completely on the secret passphrase.

    Additional security can be attained by instead storing the encrypted master key in a keyfile on e.g. a USB stick. This provides **two-factor authentication**: Accessing the encrypted data now requires something only you *know* (the passphrase), and additionally something only you *have* (the keyfile).

    Another way of achieving two-factor authentication is to augment the above key retrieval scheme to mathematically "combine" the passphrase with byte data read from one or more external files (located on a USB stick or similar), before passing it to the key derivation function.
    The files in question can be anything, e.g. normal JPEG images, which can be beneficial for [#Plausible deniability](#Plausible_deniability). They are still called "keyfiles" in this context, though.
*   ***randomly generated on-the-fly for each session***

    In some cases, e.g. when encrypting swap space or a `/tmp` partition, it is not necessary to keep a persistent master key at all. A new throwaway key can be randomly generated for each session, without requiring any user interaction. This means that once unmounted, all files written to the partition in question can never be decrypted again by *anyone* - which in those particular use-cases is perfectly fine.

After is has been derived, the master key is securely stored in memory (e.g. in a kernel keyring), for as long as the encrypted block device or folder is mounted.

It is usually not used for de/encrypting the disk data directly, though. For example, in the case of stacked filesystem encryption, each file can be automatically assigned its own encryption key. Whenever the file is to be read/modified, this file key first needs to be decrypted using the main key, before it can itself be used to de/encrypt the file contents:

```
                          ╭┈┈┈┈┈┈┈┈┈┈┈┈╮
                          ┊ master key ┊
  *file on disk:*           ╰┈┈┈┈┈┬┈┈┈┈┈┈╯
 ┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐        │
 ╎╭───────────────────╮╎        ▼          ╭┈┈┈┈┈┈┈┈┈┈╮
 ╎│ encrypted file key│━━━━(decryption)━━━▶┊ file key ┊
 ╎╰───────────────────╯╎                   ╰┈┈┈┈┬┈┈┈┈┈╯
 ╎┌───────────────────┐╎                        ▼           ┌┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┐
 ╎│ encrypted file    │◀━━━━━━━━━━━━━━━━━(de/encryption)━━━▶┊ readable file ┊
 ╎│ contents          │╎                                    ┊ contents      ┊
 ╎└───────────────────┘╎                                    └┈┈┈┈┈┈┈┈┈┈┈┈┈┈┈┘
 └ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘

```

In a similar manner, a separate key (e.g. one per folder) may be used for the encryption of file names in the case of stacked filesystem encryption.

In the case of block device encryption, ...

*Further reading:*

*   [Wikipedia:Passphrase](https://en.wikipedia.org/wiki/Passphrase "wikipedia:Passphrase")
*   [Wikipedia:Key_(cryptography)](https://en.wikipedia.org/wiki/Key_(cryptography) "wikipedia:Key (cryptography)")
*   [Wikipedia:Key_management](https://en.wikipedia.org/wiki/Key_management "wikipedia:Key management")
*   [Wikipedia:Key_derivation_function](https://en.wikipedia.org/wiki/Key_derivation_function "wikipedia:Key derivation function")

### Ciphers and modes of operation

The actual algorithm used for translating between pieces of unencrypted and encrypted data (so-called "plaintext" and "ciphertext") which correspond to each other with respect to a given encryption key, is called a "**cipher**".

Disk encryption employs "block ciphers", which operate on fixed-length blocks of data, e.g. 16 bytes (128 bits). At the time of this writing, the predominantly used ones are:

 block size | key size | comment |
| [AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard "wikipedia:Advanced Encryption Standard") | 128 bits | 128, 192 or 256 bits | *approved by the NSA for protecting "SECRET" and "TOP SECRET" classified US-government information (when used with a key size of 192 or 256 bits)* |
| [Blowfish](https://en.wikipedia.org/wiki/Blowfish_(cipher) | 64 bits | 32–448 bits | *one of the first patent-free secure ciphers that became publicly available, hence very well established on Linux* |
| [Twofish](https://en.wikipedia.org/wiki/Twofish "wikipedia:Twofish") | 128 bits | 128, 192 or 256 bits | *developed as successor of Blowfish, but has not attained as much widespread usage* |

Encrypting/decrypting a sector ([see above](#Basic_principle)) is achieved by dividing it into small blocks matching the cipher's block-size, and following a certain rule-set (a so-called "**mode of operation**") for how to consecutively apply the cipher to the individual blocks.

Simply applying it to each block separately without modification (dubbed the "*electronic codebook (ECB)*" mode) would not be secure, because if the same 16 bytes of plaintext always produce the same 16 bytes of ciphertext, an attacker could easily recognize patterns in the ciphertext that is stored on disk.

The most basic (and common) mode of operation used in practice is "*cipher-block chaining (CBC)*". When encrypting a sector with this mode, each block of plaintext data is combined in a mathematical way with the ciphertext of the previous block, before encrypting it using the cipher. For the first block, since it has no previous ciphertext to use, a special pre-generated data block stored with the sector's cryptographic metadata and called an "**initialization vector (IV)**" is used:

```
                                  ╭──────────────╮
                                  │initialization│
                                  │vector        │
                                  ╰────────┬─────╯
          ╭  ╠══════════╣        ╭─key     │      ┣┉┉┉┉┉┉┉┉┉┉┫        
          │  ║          ║        ▼         ▼      ┋          ┋         . START
          ┴  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"Hello, W"┋ block  ╱╰────┐
    sector n ║          ║                         ┋          ┋ 1      ╲╭────┘
  of file or ║          ║──────────────────╮      ┋          ┋         ' 
 blockdevice ╟──────────╢        ╭─key     │      ┠┈┈┈┈┈┈┈┈┈┈┨
          ┬  ║          ║        ▼         ▼      ┋          ┋
          │  ║"????????"║◀━━━━(cipher)━━━━(+)━━━━━┋"orld !!!"┋ block
          │  ║          ║                         ┋          ┋ 2
          │  ║          ║──────────────────╮      ┋          ┋
          │  ╟──────────╢                  │      ┠┈┈┈┈┈┈┈┈┈┈┨
          │  ║          ║                  ▼      ┋          ┋
          ⁝  ⁝   ...    ⁝        ...      ...     ⁝   ...    ⁝ ...

               ciphertext                         plaintext
                  on disk                         in memory

```

When decrypting, the procedure is reversed analogously.

One thing worth noting is the generation of the unique initialization vector for each sector. The simplest choice is to calculate it in a predictable fashion from a readily available value such as the sector number. However, this might allow an attacker with repeated access to the system to perform a so-called [watermarking attack](https://en.wikipedia.org/wiki/Watermarking_attack "wikipedia:Watermarking attack"). To prevent that, a method called "Encrypted salt-sector initialization vector (**ESSIV**)" can be used to generate the initialization vectors in a way that makes them look completely random to a potential attacker.

There are also a number of other, more complicated modes of operation available for disk encryption, which already provide built-in security agains such attacks. Some can also additionally guarantee authenticity ([see below](#Data_integrity.2Fauthenticity)) of the encrypted data.

*Further reading:*

*   [Wikipedia:Disk_encryption_theory](https://en.wikipedia.org/wiki/Disk_encryption_theory "wikipedia:Disk encryption theory")
*   [Wikipedia:Block_cipher](https://en.wikipedia.org/wiki/Block_cipher "wikipedia:Block cipher")
*   [Wikipedia:Block_cipher_modes_of_operation](https://en.wikipedia.org/wiki/Block_cipher_modes_of_operation "wikipedia:Block cipher modes of operation")

### Cryptographic metadata

### Data integrity/authenticity

*Further reading:*

*   [Wikipedia:Authenticated_encryption](https://en.wikipedia.org/wiki/Authenticated_encryption "wikipedia:Authenticated encryption")

### Plausible deniability

## Notes & References

<small></small>

<small>

1.  [^](#summary) see [http://www.truecrypt.org/legal/license](http://www.truecrypt.org/legal/license)
2.  [^](#practical_implications) well, a single file in those filesystems could be used as a container (virtual loop-back device!) but then one wouldn't actually be using the filesystem (and the features it provides) anymore
3.  [^](#compatibility_.26_prevalence) [CrossCrypt](http://www.scherrer.cc/crypt) - Open Source AES and TwoFish Linux compatible on the fly encryption for Windows XP and Windows 2000
4.  [^](#compatibility_.26_prevalence) [FreeOTFE](http://www.freeotfe.org) - supports Windows 2000 and later (for PC), and Windows Mobile 2003 and later (for PDA)
5.  [^](#compatibility_.26_prevalence) see [EncFs build instructions for Mac](http://www.arg0.net/encfs-mac-build)
6.  [^](#compatibility_.26_prevalence) see [http://www.freshports.org/sysutils/fusefs-encfs/](http://www.freshports.org/sysutils/fusefs-encfs/)
7.  [^](#compatibility_.26_prevalence) see [http://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data](http://www.chromium.org/chromium-os/chromiumos-design-docs/protecting-cached-user-data)

</small>

<small></small>