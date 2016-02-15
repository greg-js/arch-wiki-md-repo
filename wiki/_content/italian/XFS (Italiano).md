## Contents

*   [1 Manutenzione del FileSystem](#Manutenzione_del_FileSystem)
    *   [1.1 Controllare il grado di frammentazione](#Controllare_il_grado_di_frammentazione)
    *   [1.2 Deframmentazione del FileSystem](#Deframmentazione_del_FileSystem)
    *   [1.3 Attenzioni particolari](#Attenzioni_particolari)

## Manutenzione del FileSystem

### Controllare il grado di frammentazione

Per visualizzare su terminale il grado di frammentazione di una partizione XFS si usa il comando **xfs_db**

```
xfs_db -r <device>

xfs_db> frag
actual 269349, ideal 268587, fragmentation factor 0.28%
xfs_db> 

```

L'opzione **-r** apre il device, o anche solo un file, in modalità **read-only**. Per uscire dal programma poi è sufficiente

```
xfs_db> quit

```

### Deframmentazione del FileSystem

La deframmentazione viene effettuata dal programma **xfs_fsr**, che si occupa di ricollocare i file presenti (o solamente un file) nel device selezionato. Invocandolo senza parametri avviamo il processo che legge le partizione XFS presenti in **/etc/mtab** e per 7200 secondi (2 ore) riorganizza i file uno alla volta. Se non termina la procedura, verrà salvato un file **/var/tmp/.xfslast** con la situazione corrente, in modo da continuare la deframmentazione al prossimo avvio dell'applicazione conoscendo i file già riallocati. Se vogliamo effettuare l'operazione per un periodo di tempo diverso

```
xfs_fsr -t <secondi>

```

Questa opzione è utile per configurare un job da far eseguire durante i tempi morti, è sconsigliato infatti effettuare questa operazione durante il normale utilizzo del computer

### Attenzioni particolari

**xfs_fsr** non lavora sui file mappati in memoria, per cui potrebbero essere esposti a video degli errori se si usa l'opzione **-v**. Inoltre non è necessario solitamente effettuare questa operazione su **/**, **/boot**, **/usr**. L'operazione può risultare nell'impossibilità di avviare il computer se si effettua la deframmentazione di _/boot_ in presenza del bootloader **LILO**: in questo caso è necessario lanciare il comando

```
lilo 

```

dopo aver deframmentato.