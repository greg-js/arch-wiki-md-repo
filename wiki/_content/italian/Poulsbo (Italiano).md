La serie **Intel GMA 500**, conosciuta anche con il nome in codice **Poulsbo** oppure **[Intel System Controller Hub US15W](http://ark.intel.com/it/products/35444/intel-sch-us15w)**, è una famiglia di adattatori video integrati basati sul processore grafico the PowerVR SGX 535\. È tipicamente montato sulla serie di processori Atom Z. Le caratteristiche includono capacità di decodifica hardware dei contenuti video fino a 720-1080 dpi in vari standard di codec, ad esempio l'H.264.

Il processore grafico PowerVR SGX 535 è stato sviluppato dall' Imagination Technologies e concesso in licenza da Intel, i driver standard opensource [Intel](/index.php/Intel_(Italiano) "Intel (Italiano)") non funzionano con questa periferica.

In questa pagina si trovano informazioni su come ottenere il meglio dal vostro hardware Poulsbo con Arch Linux.

## Contents

*   [1 Modulo del kernel gma500_gfx](#Modulo_del_kernel_gma500_gfx)
*   [2 Modesetting driver e procedura per l'uso di un monitor esterno](#Modesetting_driver_e_procedura_per_l.27uso_di_un_monitor_esterno)
*   [3 Risoluzione di problemi](#Risoluzione_di_problemi)
    *   [3.1 Scarsa performance video](#Scarsa_performance_video)
    *   [3.2 Correzione la sospensione](#Correzione_la_sospensione)
        *   [3.2.1 Vecchi driver fbdev (default)](#Vecchi_driver_fbdev_.28default.29)
        *   [3.2.2 modesetting dei driver xorg](#modesetting_dei_driver_xorg)
    *   [3.3 Impostare la luminosità](#Impostare_la_luminosit.C3.A0)
    *   [3.4 Ottimizzazione della memoria allocata](#Ottimizzazione_della_memoria_allocata)
*   [4 Altre risorse](#Altre_risorse)

## Modulo del kernel gma500_gfx

Con il kernel 2.6.39 [Alan Cox](http://it.wikipedia.org/wiki/Alan_Cox) sviluppò il modulo psb_gfx per supportare la periferica Poulsbo. A partire dal kernel 3.3.rc1 il driver è stato stabilizzato e rinominato come gma500_gfx. ([[1]](http://blog.bodhizazen.net/linux/linux-gma500-poulsbo-driver-moved-out-of-staging/))

**Vantaggi**

*   Risoluzione nativa (1366x768) con i primi KMS (testato su Asus Eee 1101HA)
*   Kernel e server Xorg aggiornati
*   Accelerazione 2D
*   Funziona out-of-the-box

**Svantaggi**

*   Alcuni non sono in grado di ottenere la risoluzione nativa (e.g 1366x768)
*   Nessuna accelerazione 3D
*   Scarsa performance multimediale (l'uso di mplayer con x11 or sdl rende l'utilizzo a schermo intero un po' lento)

Per verificare se i driver sono stati caricati correttamente l'output di `lsmod | grep gma` dovrebbe essere il seguente:

```
gma500_gfx            131893  2 
i2c_algo_bit            4615  1 gma500_gfx
drm_kms_helper         29203  1 gma500_gfx
drm                   170883  2 drm_kms_helper,gma500_gfx
i2c_core               16653  5 drm,drm_kms_helper,i2c_algo_bit,gma500_gfx,videodev

```

Nel caso non si riuscissero a caricare i driver verificare dare il seguente comando e verificare che il campo MODULES contenga la stringa gma500_gfx.

 `# nano /etc/mkinitcpio.conf` 

```
 [...]

 MODULES="gma500_gfx"

 [...]

```

Verificare inoltre che i driver vesa siano disinstallati con il comando:

```
# pacman -Qs xf86-video-vesa

```

Se ricevete un output provvedete a disintallare i driver con il comando:

```
# pacman -R xf86-video-vesa

```

Riavviate e dovreste avere i vostri driver abilitati e funzionanti

## Modesetting driver e procedura per l'uso di un monitor esterno

Puoi impostare una risoluzione diversa a un monitor esterno usando [xrandr](https://wiki.archlinux.org/index.php/Xrandr) scaricando [xorg-xserver](https://www.archlinux.org/packages/?name=xorg-xserver) dai repository ufficiali. Se scegli di usare il pacchetto git ([xf86-video-modesetting-git](https://aur.archlinux.org/packages/xf86-video-modesetting-git/)), ricordati di ricompilarlo dopo ogni aggiornamento di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)"). Dopo l'installazione, un file di [Xorg](/index.php/Xorg_(Italiano) "Xorg (Italiano)") deve essere modificato per usare il driver. Modifica quindi il file `/etc/X11/xorg.conf.d/20-gpudriver.conf` aggiungendo:

```
Section "Device"
   Identifier "gma500_gfx"
   Driver     "modesetting"
   Option     "SWCursor"       "ON" 
EndSection

```

**Note:** Questo file di configurazione rimpiazzerà i driver [xf86-video-fbdev](https://www.archlinux.org/packages/?name=xf86-video-fbdev). Se non vuoi che questo accada basta occorre rimpiazzare `modesetting` con `fbdev`.

## Risoluzione di problemi

### Scarsa performance video

Se hai problemi a riprodurre video a 720 e 1080 dpi è normale fintanto che non verranno sviluppati driver con accelerazione hardware. Si può provare a migliorare fino a un certo punto (sufficente per la maggior parte dei video, anche quelli HD) con questi trucchi:

1.  Aggiungere pm-powersave false a /etc/rc.local.
2.  Utilizzare [xf86-video-modesetting-git](https://aur.archlinux.org/packages/xf86-video-modesetting-git/) come sopra indicato.
3.  Utilizzare sempre [mplayer](/index.php/Mplayer "Mplayer") o una sua variante. [VLC](/index.php/VLC "VLC") e player simili sono spesso troppo pesanti.
4.  Sostituire il normale [mplayer](/index.php/Mplayer "Mplayer") con mplayer-minimal-svn e compilare con le ottimizzazioni:-march = native-fomit-frame-pointer-O3-ffast-matematica '.
5.  Usare linux-lqx in quanto è un kernel con ottime prestazioni. Modifica il file PKGBUILD in modo da poter assicurarsi di selezionare il proprio processore e rimuovere ottimizzazioni generiche per altri processori.

### Correzione la sospensione

#### Vecchi driver fbdev (default)

Se la sospensione non funziona ci sono varie opzioni che puoi provare. Prima di tutto assicurati di avere [pm-utils](https://www.archlinux.org/packages/?name=pm-utils) e [pm-quirks](https://www.archlinux.org/packages/?name=pm-quirks) [installati](/index.php/Pacman "Pacman"). Vedi la pagina man di pm-suspend per una lista di tutto. Un opzione che è stata segnalata è `quirk-vbemode-restore`, che salva e ricarica la modalità Vesa corrente.

Per testarlo apri il terminale e usa il comando:

```
# pm-suspend --quirk-vbemode-restore 

```

Questo dovrebbe sospendere il tuo sistema. Se riesci a ricaricare il sistema in questo modo dai il comando:

```
# echo "ADD_PARAMETERS='--quirk-vbemode-restore'" > /etc/pm/config.d/gma500 

```

In caso contrario prova a dare questo comando:

```
# pm-suspend -quirk-vbemode-restore 

```

**Tip:** Se sei bloccato con una schermata nera dopo la ripresa, devi essere consapevole del fatto che, oltre lo schermo nero, il sistema funziona. Invece dell'hard reset, si potrebbe provare a riavviare alla cieca il sistema. Infatti l'ultima cosa che hai usato prima di la sospensione era il terminale. In alternativa, se si dispone di ssh abilitato sul proprio computer si può fare a distanza.

#### modesetting dei driver xorg

Su alcune macchine, usando i driver modesetting, lo schermo assume dati casuali. Anche se il computer funziona ancora si deve aprire il terminale e killare il server X alla cieca. Per ovviare a questo inconveniente seguire questo procedimento:

In primo luogo, vedere avviare `xrandr` per verificare le impostazioni relative al tuo schermo:

```
 # xrandr
 Screen 0: minimum 320 x 200, current 1280 x 720, maximum 2048 x 2048
 LVDS-0 connected 1280x720+0+0 222mm x 125mm
   1280x720       60.0*+
 HDMI-0 connected 1280x720+0+0 531mm x 298mm
   1920x1080      60.0 +
   1680x1050      59.9  
   1680x945       60.0  
   1400x1050      74.9     59.9  
   1600x900       60.0  
   1280x1024      75.0     60.0  
   1440x900       75.0     59.9  
   1280x960       60.0  
   1366x768       60.0  
   1360x768       60.0  
   1280x800       74.9     59.9  
   1152x864       75.0  
   1280x768       74.9     60.0  
   1280x720       60.0* 
   1024x768       75.1     70.1     60.0  
   1024x576       60.0  
   832x624        74.6  
   800x600        72.2     75.0     60.3     56.2  
   848x480        60.0  
   640x480        72.8     75.0     60.0  
   720x400        70.1

```

Modifica o crea (dando i permessi d'esecuzione) `/etc/pm/sleep.d/99xrandr`, scrivendo la risoluzione e la modalità giusta per te:

```
 #!/bin/sh
 #
 # turn off and on the screens so we force to clean video data
 case "$1" in
 hibernate|||suspend)
 xrandr --output LVDS-0 --off
 xrandr --output HDMI-0 --off
 ;;
 thaw|||resume)
 xrandr --output LVDS-0 --off
 xrandr --output HDMI-0 --off
 xrandr --output LVDS-0 --mode 1280x720
 /usr/local/bin/brillo-
 ;;
 *) exit $NA
 ;;
 esac

```

Nel mio caso, spengo entrambi gli schermi, per attivare solo solo il monitor principale all'avvio. Sentitevi liberi di personalizzare in base alle vostre esigenze. Su alcune macchine, lo schermo si attiva per impostazione predefinita anche quando il sistema è stato spento. È quindi necessario riavviare due volte.

**Note:** Questo funziona solo se richiami `pm-suspend` o `pm-hibernate` all'interno di [X](/index.php/Xorg_(Italiano) "Xorg (Italiano)"). Se questo è richiamato da un demone o tty

### Impostare la luminosità

Tutto ciò che serve per impostare la luminosità è l'invio di un numero (0-100) a `/sys/class/backlight/psblvds/brightness`. Ciò richiede ovviamente sysfs sia abilitato nel kernel. Per impostare la visualizzazione a luminosità minima, il comando da root:

```
# echo 0 > /sys/class/backlight/psb-bl/brightness

```

Per la luminosità massima:

```
# echo 100 > /sys/class/backlight/psb-bl/brightness

```

Puoi ottenere lo stesso risultato con questo script scritto da [mulenmar](https://bbs.archlinux.org/viewtopic.php?pid=813074#p813074).

```
#! /bin/sh
sudo sh -c "echo $1 > /sys/class/backlight/psb-bl/brightness"

```

Basta salvarlo come brightness.sh e dare autorizzazioni di esecuzione. Quindi è possibile utilizzare in questo modo:

Impostare la luminosità al minimo:

```
./brightness.sh 0

```

Impostare la luminosità al massimo:

```
./brightness.sh 50

```

Sudo può ovviamente richiedere la tua password, quindi bisogna essere nel file sudouers o essere nel gruppo `wheel`. Una variante di questo script può essere trovato [qui](https://bbs.archlinux.org/viewtopic.php?pid=1143245#p1143245).

**Note:** Se cambiare `/sys/class/backlight/psblvds/brightness` non funziona, potresti aver bisogno di aggiungere `acpi_osi=Linux acpi_backlight=vendor` ai tuoi [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). Dopo il riavvio apparirà una nuova cartella in `/sys/class/backlight/`; apportare modifiche al file `brightness` dovrebbe risolvere il problema. Per esempio in alcuni netbook Asus la retroilluminazione può essere controllato scrivendo un valore (0-10) al file `/sys/class/backlight/eeepc-wmi/brightness`.

### Ottimizzazione della memoria allocata

Spesso è possibile migliorare le prestazioni, limitando la quantità di RAM utilizzata dal sistema in modo che ce ne sia una quantità maggiore disponibile per la scheda video. Se si dispone di 1 GB di RAM uso `mem=896mb` o se si dispone di 2 GB di RAM uso `mem=1920mb`. Aggiungere i seguenti parametri al file di configurazione del bootloader.

*   [Grub-legacy](/index.php/Grub-legacy "Grub-legacy")

Modifica `/boot/grub/menu.lst`

```
...
kernel /vmlinuz-linux root=/dev/sda2 ro mem=896mb 
...

```

*   [Grub](/index.php/Grub "Grub")

Modifica `/etc/default/grub`

```
...
GRUB_CMDLINE_LINUX="mem=896mb"
...

```

*   [Syslinux](/index.php/Syslinux "Syslinux")

Modifica `/boot/syslinux/syslinux.cfg`

```
...
APPEND root=/dev/sda2 ro mem=896mb 
...

```

## Altre risorse

*   [Discussione relativa all'Hardware Poulsbo su Arch BBS(en)](https://bbs.archlinux.org/viewtopic.php?pid=746439)