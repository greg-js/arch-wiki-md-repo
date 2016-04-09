[F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") (Flash-Friendly File System) è un file system concepito per l'uso su dispositivi che usano memorie flash con logica NAND. Il kernel Linux supporta F2FS dalla versione 3.8.

## Creare una partizione F2FS

Per creare una partizione F2FS, [installate](/index.php/Pacman_(Italiano) "Pacman (Italiano)") il pacchetto [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").

Dopo di che date il comando:

```
# mkfs.f2fs */dev/sdxY*

```

dove */dev/sdxY* è il volume da formattare.

## Montare una partizione F2FS

Potreste avere bisogno di caircare il relativo modulo prima di montare:

```
# modprobe f2fs

```

Ora siete pronti a montare:

```
# mount -t f2fs /dev/sdxY /mnt

```

## Installare Arch Linux su una partizione F2FS

Dall'immagine di installazione di Arch Linux 2013.04.01, è possibile installare il sistema su una partizione F2FS:

1.  Avviate l'immagine e installate [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools) dai [repository ufficiali](/index.php/Official_repositories_(Italiano) "Official repositories (Italiano)").
2.  Caricate il modulo `f2fs` come [descritto](#Montare_una_partizione_F2FS).
3.  Create la partizione radice formattata in F2FS come [descritto](#Creare_una_partizione_F2FS).
4.  Create la partizione di avvio (*/boot*) formattata in ext4 (o un altro file system supportato).
5.  Montate, installate e cambiate radice come [descritto](/index.php/Beginners%27_guide_(Italiano)#Montare_le_partizioni "Beginners' guide (Italiano)").
6.  Sul sistema installato aggiungete `f2fs` alla sezione moduli del file `/etc/mkinitcpio.conf` e rimuovete `fsck` dalla sezione hooks perchè F2FS non dispone ancora di un *fsck*.
7.  Rigenerate l'immagine compressa del kernel:

	`# mkinitcpio -p linux`