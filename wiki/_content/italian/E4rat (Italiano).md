[E4rat](http://e4rat.sourceforge.net/) (ext4 reduced access time) è un software di Andreas Rid e Gundolf Kiefer che si compone di tre parti: e4rat-collect, e4rat-realloc ed e4rat-preload.

## Contents

*   [1 Utilizzo](#Utilizzo)
    *   [1.1 Quando funziona e quando è inutile](#Quando_funziona_e_quando_.C3.A8_inutile)
*   [2 Installazione](#Installazione)
*   [3 e4rat-collect](#e4rat-collect)
*   [4 e4rat-realloc](#e4rat-realloc)
*   [5 e4rat-preload](#e4rat-preload)

## Utilizzo

Il funzionamento di divide in tre parti:

*   **e4rat-collect** - Raccoglie i files durante il boot per 120 secondi
*   **e4rat-realloc** - Rialloca i file
*   **e4rat-preload** - Carica i file riallocati durante il boot

### Quando funziona e quando è inutile

E4rat funziona solo per filesystem ext4 e per HD: gli SSD non ne subiscono gli effetti in quanto non hanno parti in movimento e hanno una latenza molto bassa. Inoltre la riduzione di tempo si nota principalmente per gli avvii grafici: nei server o nei sistemi che utilizzano solo la CLI la differenza si nota molto meno.

## Installazione

[Installa](/index.php/Pacman "Pacman") [e4rat](https://aur.archlinux.org/packages/e4rat/) da [AUR](/index.php/AUR "AUR").

## e4rat-collect

Per generare una lista dei file da caricare è necessario aggiungere `init=/sbin/e4rat-collect` ai [Parametri del Kernel](/index.php/Kernel_parameters "Kernel parameters"), per esempio:

```
linux /vmlinuz-linux root=UUID=your-root-UUID ro init=/usr/bin/e4rat-collect

```

Durante il boot, e4rat-coolect raccoglie dati per 120 secondi. Per fermare la raccolta di informazioni si può usare il comando:

```
e4rat-collect -k

```

oppure

```
pkill e4rat-collect

```

Dopo aver effettuato l'avvio e aver raccolto i dati, bisogna togliere il parametro dal kernel e riallocare i file.

## e4rat-realloc

Quest'operazione può essere effettuate anche da ambiente grafico ma si consiglia di passare al runlevel 1\. Con systemd:

```
# systemctl rescue

```

con initscript

```
# init 1

```

Dopo essersi loggati come root, dare il comando

```
 e4rat-realloc  /var/lib/e4rat/startup.log

```

ci potrebbe volere un momento in base alle dimensioni dei file da riallocare.

## e4rat-preload

Ora non resta che aggiungere `init=/sbin/e4rat-preload` ai parametri del kernel in modo permanente e riavviare il sistema.