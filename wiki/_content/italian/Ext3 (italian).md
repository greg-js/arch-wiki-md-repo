Vi è un gran numero di fan del Third Extended Filesystem ("ext3"). A livello kernel e codice userspace è stato provato, testato, corretto, e migliorato più di quasi tutti gli altri filesystem compatibili con Linux. È semplice, robusto, ed estensibile. In questo articolo si illustreranno alcuni suggerimenti che possono migliorare sia le prestazioni che l'affidabilità del filesystem.

Nel corso di questo articolo, /dev/hdXY sarà utilizzato come una partizione generica. È necessario sostituirla con il nodo del dispositivo effettivo per la partizione, come /dev/hdb1 per la prima partizione del disco slave primario o /dev/sda2 per la seconda partizione del primo disco SCSI o Serial ATA.

## Contents

*   [1 Usare le utilità tune2fs e e2fsck](#Usare_le_utilit.C3.A0_tune2fs_e_e2fsck)
*   [2 Utilizzo di indicizzazione Directory](#Utilizzo_di_indicizzazione_Directory)
*   [3 Abilitare journaling completo](#Abilitare_journaling_completo)
*   [4 Disattivare verifiche lunghe al boot](#Disattivare_verifiche_lunghe_al_boot)
*   [5 Recuperare lo spazio riservato del filesystem](#Recuperare_lo_spazio_riservato_del_filesystem)
*   [6 Assegnazione di un etichetta](#Assegnazione_di_un_etichetta)
*   [7 Esperienze utenti](#Esperienze_utenti)

## Usare le utilità tune2fs e e2fsck

Prima di iniziare, assicurarsi di avere dimestichezza con lo strumento tune2fs per modificare le opzioni dei filesystem di una partizione ext2 o ext3 (o [convertire da ext2 a ext3](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3")). Leggere attentamente la pagina man tune2fs:

```
$ man tune2fs

```

È generalmente una buona idea eseguire un controllo del filesystem utilizzando l'utilità e2fsck dopo aver completato le modifiche desiderate in un filesystem. In questo modo si verifica che il filesystem sia pulito ed eventualmente corretto, se necessario. Si dovrebbe anche leggere la pagina del manuale per l'utilità e2fsck, se non lo si è ancora fatto:

```
$ man e2fsck

```

**WARNING: SOLO DISPOSITIVI SMONTATI:** Assicurarsi che tutti i filesystem siano smontati prima di modificarli con le utilità tune2fs o e2fsck! Avviare da LiveCD come **Archie** o Knoppix se non si può fare diversamente. L'alterazione o la messa a punto di un filesystem mentre è montato può causare gravi danneggiamenti! Siete stati avvertiti!

## Utilizzo di indicizzazione Directory

Questa funzione migliora l'accesso ai file nelle directory di grandi dimensioni o directory contenenti molti file utilizzando un sistema di hash binari per memorizzare le informazioni della directory. È perfettamente sicuro da usare e fornisce un miglioramento sostanziale nella maggior parte dei casi, quindi è una buona idea abilitarlo:

```
# tune2fs -O dir_index /dev/hdXY

```

Questo avrà effetto solo con le directory create su quel filesystem dopo aver eseguito tune2fs. Per applicare questa funzionalità alle directory esistenti, si deve eseguire l'utilità e2fsck per ottimizzare e reindicizzare le directory sul filesystem:

```
# e2fsck -D -f /dev/hdXY

```

**Note:** Questo dovrebbe funzionare sia con filesystem ext2 che ext3\. A seconda delle dimensioni del file system, l'operazione potrebbe richiedere molto tempo.

**Note:** L'indicizzazione della directory è attivata per impostazione predefinita in Arch Linux per mezzo di /etc/mke2fs.conf

## Abilitare journaling completo

Per impostazione predefinita, le partizioni ext3 vengono montate con la modalità dati "ordinata". In questa modalità, tutti i dati vengono scritti nel file system principale, mentre i relativi metadati vengono passati al journal, i cui blocchi sono raggruppati logicamente in transazioni per diminuire gli I/O sul disco. Questo tende a essere un buon valore predefinito per la maggior parte delle persone. Tuttavia, c'è un metodo che aumenta sia l'affidabilità che le prestazioni (in alcune situazioni): passare tutto al journaling, compresi i dati del file stesso (conosciuto come modalità dati "journal"). Normalmente, si potrebbe pensare che passando tutti i dati al journal si diminuiscano le prestazioni, poiché i dati vengono scritti sul disco due volte: una al journal e una al filesystem principale, ma questo non sembra essere il caso. Abilitato su tutte e nove le partizioni nel computer in prova, è stata rilevata solamente una perdita di prestazioni durante la cancellazione di file di grandi dimensioni. In realtà, questo modo può effettivamente migliorare le prestazioni su un filesystem in cui la maggior parte della lettura e scrittura vengono effettuate simultaneamente . Vedere [questo articolo](http://www-106.ibm.com/developerworks/linux/library/l-fs8.html#4) scritto da Daniel Robbins sul sito IBM per maggiori informazioni.

Ci sono due modi per attivare la modalità dati journaling. Il primo è con l'aggiunta di "data=journal" come opzione di mount in /etc/fstab. Se lo si fa in questo modo e si desidera che anche il filesystem root lo usi, si dovrebbe anche aggiungere "rootflags=data=journal" come parametro del kernel nella configurazione del bootloader. Nel secondo metodo, si utilizzerà tune2fs per modificare le opzioni di montaggio predefinite nel superblocco del file system:

```
# tune2fs -O has_journal -o journal_data /dev/hdXY

```

Si prega di notare che il secondo metodo può non funzionare per i kernel più datati. In particolare per Linux 2.4.20 e inferiori, è probabile che le opzioni di mount predefinite sul superblocco vengano ignorate. Chi si sente avventuroso può anche voler ottimizzare le dimensioni del journaling. (Qui si è lasciato il journaling in formato predefinito). Un journaling di dimensioni più grandi può dare prestazioni migliori (al costo di più spazio su disco e un più lungo tempo di recupero). Si raccomanda di leggere la sezione pertinente del manuale tune2fs prima di procedere:

```
# tune2fs -J size=$SIZE /dev/hdXY

```

## Disattivare verifiche lunghe al boot

**WARNING:** Eseguire questa operazione solo su filesystem con journaling come ext3\. Potrebbe funzionare anche su altri filesystem con journaling come ReiserFS o XFS, ma non è stato collaudato a sufficienza. Si potrebbe quindi danneggiare o comunque manomettere altri filesystem. Queste operazioni sono fatte a PROPRIO RISCHIO.

Sembra che filesystem ext3 venga controllato ogni 30 mount, o simili. Questo è un buon valore predefinito per la maggior parte dell'utenza, perché aiuta a prevenire la corruzione del filesystem, soprattutto quando si hanno problemi hardware, come cattivi cablaggi IDE/SATA/SCSI, problemi con l'alimentazione, ecc. Una delle forze trainanti per la creazione dei filesystem journaling è che il filesystem potrebbe essere facilmente ripristinato ad uno stato coerente con il recupero e la riproduzione delle operazioni di journaling necessarie. Quindi, possiamo tranquillamente disattivare questi "conteggi di mount" e "controlli a tempo", se siamo certi che il filesystem sarà rapidamente controllato per recuperare il journal, e se necessario, per ripristinare il file system e la coerenza dei dati. Prima di passare all'esecuzione, assicurarsi che la voce relativa al filesystem in /etc/fstab, abbia un numero intero positivo nel 6º campo (pass), in modo che sia verificata automaticamente al momento del boot. Si può farlo utilizzando il seguente comando:

```
# tune2fs -c 0 -i 0 /dev/hdXY

```

Se si desidera limitare la frequenza dei controlli, senza disabilitarli completamente (per la pace della mente), un ottimo metodo è quello di passare da un certo numero di check ad un controllo fissato per un lasso di tempo. Consultare le pagine di manuale. Nel seguente esempio è impostato una volta al mese.

```
# tune2fs -c 0 -i 1m /dev/hdXY

```

## Recuperare lo spazio riservato del filesystem

Le partizioni ext3 contengono uno spazio speciale, utilizzato al 5% in maniera predefinita. Il motivo principale di tale spazio, è che così root può accedervi anche quando il filesystem viene utilizzato al 100%. Senza questa opzione, l'utente root potrebbe non essere in grado di accedere per "ripulire", dato che il sistema potrebbe diventare instabile, cercando di scrivere i log su un sistema pieno al 100%, per esempio. L'altro motivo è quello di aiutare l'ottimizzazione generale con una minore frammentazione del filesystem.

Il problema è che, con gli hard disk odierni sempre più grandi, il 5% può diventare una grande quantità di spazio sprecato. (Es. 100 GB = 5 GB riservati). Ora, se il filesystem è separato da /home per esempio, potrebbe essere una buona idea fare un po' di aggiustamenti e recuperare quello spazio sprecato. Sarebbe una scommessa sicura lasciare il filesystem / con uno spazio del 5% riservato per ogni evenienza. Lasciare lo spazio riservato per i filesystem che contengono /var e /tmp, altrimenti ci si ritroverà con qualche problema.

Ora per cambiare lo spazio riservato all '1% del disco, che è accettabile per i filesystems non-root:

```
# tune2fs -m 1 /dev/sdXY

```

## Assegnazione di un etichetta

Dopo aver creato e formattato una partizione, è possibile assegnare un'etichetta utilizzando il comando e2label. Questo permette di aggiungere la partizione a /etc/fstab usando un'etichetta invece di utilizzare il percorso del dispositivo (utile per un drive USB). Per aggiungere un'etichetta a una partizione, digitare il seguente comando come root:

```
   e2label /dev/sdXY *new-label*

```

Se l'argomento opzionale *new-label* non è presente, e2label visualizzerà semplicemente l'etichetta del filesystem corrente. Se invece *new-label* è presente, e2label imposterà l'etichetta del filesystem a *new-label*q. Le etichette per filesystem ext2 e ext3 possono essere al massimo 16 caratteri, in caso la nuova etichetta sia più lunga, e2label la troncherà e stamperà un messaggio di avviso.

## Esperienze utenti

Non ho mai avuto problemi con questi suggerimenti su filesystem di grandi dimensioni (> 750). Disabilitare i controlli programmati all'avvio funziona altrettanto bene.

Il filesystem ha prodotto alcuni errori seguendo questi suggerimenti. Non disabilitare il lengthy boot-time.

Se si dispone di partizioni grandi, non attivare il journaling completo su di esse. Ho avuto esperienze di freeze (circa 30 secondi) sulla mia partizione home da 250GB.

	Hai provato ad ottimizzare con bdflush, come descritto [da Daniel Robbins](http://www.ibm.com/developerworks/linux/library/l-fs8.html)?