[grub-gfx](https://aur.archlinux.org/packages/grub-gfx/) è una versione di GRUB, modificata per abilitare le immagini di sfondo al bootloader.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Configurazione](#Configurazione)
*   [3 Immagini di Splash](#Immagini_di_Splash)
*   [4 Risoluzione Problemi](#Risoluzione_Problemi)
    *   [4.1 Schermo nero; nessun menu; prompt lampeggiante](#Schermo_nero.3B_nessun_menu.3B_prompt_lampeggiante)
*   [5 Link esterni](#Link_esterni)

## Installazione

Il pacchetto [grub-gfx](https://aur.archlinux.org/packages/grub-gfx/) è nel repository Community. Controllate `/etc/[pacman.conf](/index.php/Pacman "Pacman")` e siate sicuri che la linea `[community]` non sia commentata.

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Fate un backup della configurazione di [GRUB](/index.php/GRUB "GRUB"). (Durante l'installazione del pacchetto, ciò dovrebbe accadere automaticamente; è un passaggio precauzionale.)

```
# cp /boot/grub/menu.lst /boot/grub/menu.lst.bak

```

Adesso scaricate e installate [grub-gfx](https://aur.archlinux.org/packages/grub-gfx/). L'installazione dovrebbe anche rimuovere automaticamente il pacchetto [grub](https://www.archlinux.org/packages/?name=grub) se è installato.

```
# pacman -S grub-gfx

```

Dopo l'installazione controllate `/boot/grub/menu.lst`. Modificate il file seguendo il backup effettuato in precedenza. Se non avete creato il backup, o questo è andato perso, cercate in `/boot/grub/menu.lst.pacsave`. Potete anche semplicemente sovrascrivere il file di backup sul nuovo `menu.lst` e procedere alla configurazione sottostante.

## Configurazione

L'unica modifica da effettuare nel file di configurazione riguarda la linea `splashimage`. Nel `/boot/grub/menu.lst` predefinito troverete:

```
# general configuration:
timeout   5
default   0
color light-blue/black light-cyan/blue
splashimage /boot/grub/arch.xpm.gz

```

In caso l'ultima riga manchi, basta aggiungerla al file `menu.lst`. Questa linea punta al percorso del file che vorrete usare come sfondo alla schermata di selezione dei sistemi avviabili.

**Note:** Questa linea è relativa alla partizione di root di GRUB, il che significa che se avete la partizione indipendente `/boot`, l'istruzione precedente deve essere modificata in:

```
splashimage /grub/arch.xpm.gz

```

Infine, è necessario (re)installare GRUB per sovrascrivere la corrente installazione di GRUB sull'MBR (Master Boot Record). Leggete [GRUB](/index.php/GRUB "GRUB") se non avete esperienza in questa procedura. In un'installazione standard di GRUB è necessario esclusivamente il comando:

```
# grub-install /dev/sda

```

Ricordate comunque di eseguire le operazioni basandovi sulla vostra installazione.

## Immagini di Splash

Le immagini "splash" (gli sfondi) devono possedere l'estensione `.xpm.gz`, una risoluzione di 640x480, e 14 colori.

Per installare una nuova immagine di splash, è necessario copiarla nella directory di GRUB (molto spesso `/boot/grub/`) quindi aggiornare `menu.lst` in modo che punti all'immagine. Non vi è bisogno di reinstallare GRUB; riavviate e potrete osservare la nuova immagine.

## Risoluzione Problemi

### Schermo nero; nessun menu; prompt lampeggiante

Dovreste essere ancora in grado di selezionare un sistema e avviarlo. Una volta tornati al vostro sistema, controllate il file `menu.lst` nuovamente. Assicuratevi che il percorso all'immagine splash sia corretto. Ricordate, la linea `splashimage` è relativa alla partizione in cui risiede GRUB. Se avete GRUB installato sulla partizione `/boot`, la linea cambierà in `splashimage /grub/arch.xpm.gz`. Infine, controllate che l'immagine richiesta si trovi realmente all'indirizzo indicato.

## Link esterni

[Collection of GRUB splashes](http://www.schultz-net.dk/grub.html)