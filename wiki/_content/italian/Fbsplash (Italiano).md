[Fbsplash](http://fbsplash.berlios.de/) (conosciuto anche come gensplash) è un'implementazione in userspace di uno splash screen per sistemi Linux. Questo fornisce un ambiente grafico durante l'avvio del sistema usando le funzionalità framebuffer di Linux.

## Contents

*   [1 Installazione](#Installazione)
    *   [1.1 Fbsplash](#Fbsplash)
    *   [1.2 Scripts](#Scripts)
    *   [1.3 Temi](#Temi)
    *   [1.4 Suspend To Disk](#Suspend_To_Disk)
*   [2 Configurazione](#Configurazione)
    *   [2.1 Parametri di avvio del Kernel](#Parametri_di_avvio_del_Kernel)
    *   [2.2 File di configurazione](#File_di_configurazione)
*   [3 Avviare fbsplash nella initcpio](#Avviare_fbsplash_nella_initcpio)
*   [4 Sfondi per console](#Sfondi_per_console)
*   [5 Links](#Links)

## Installazione

### Fbsplash

Il pacchetto [fbsplash](https://aur.archlinux.org/packages/fbsplash/) è disponibile in AUR. Per sfondi console (descritto più avanti in questo articolo) è necessario installare un kernel patchato con fbcondecor come [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/).

### Scripts

Per avere gli scripts per le funzionalità di base come i messaggi di controllo del filesystem, il supporto per l'avvio di servizi ed altro, si può installare anche il pacchetto [fbsplash-extras](https://aur.archlinux.org/packages/fbsplash-extras/)

### Temi

Installa uno o più pacchetti dei temi di fbsplash cercando su AUR [fbsplash-theme](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go) o da [GNOME-look.org](http://gnome-look.org) o da [KDE-look.org](http://kde-look.org).

**Note:** Il pacchetto fbsplash non include nessun tema

### Suspend To Disk

Se vuoi utilizzare l'ibernazione con fbsplash:

*   Se utilizzi Uswsusp, installa il pacchetto [uswsusp-fbsplash](https://aur.archlinux.org/packages/uswsusp-fbsplash/) da AUR. Per maggiori informazioni leggere le wiki di [pm-utils](/index.php/Pm-utils#Using_another_sleep_backend_.28like_uswsusp.29 "Pm-utils") ed [hibernate-script](/index.php/Suspend_to_Disk#Uswsusp_method_.28hibernate-script.29 "Suspend to Disk")
*   Se utilizzi TuxOnIce, il pacchetto [tuxonice-userui](https://aur.archlinux.org/packages/tuxonice-userui/) permette di utilizzare i temi di fbsplash.

In questa wiki sono presenti ulteriori informazioni su [uswsusp](/index.php/Suspend_to_Disk#Uswsusp_method "Suspend to Disk") e [TuxOnIce](/index.php/TuxOnIce_(Italiano) "TuxOnIce (Italiano)").

## Configurazione

### Parametri di avvio del Kernel

Il bootloader necessita di essere configurato per Fbsplash. L'esempio seguente vale per [Grub2](/index.php/Grub2 "Grub2") e `/boot/grub/grub.cfg` ([GRUB](/index.php/GRUB "GRUB") e [LILO](/index.php/LILO "LILO") seguono lo stesso criterio):

```
linux /boot/vmlinuz-linux root=/dev/... quiet loglevel=3 logo.nologo console=tty1 splash=silent,fadein,fadeout,theme:arch-banner-icons

```

Si può anche editare il file `/etc/default/grub` ed aggiungere le opzioni del kernel alla riga `GRUB_CMDLINE_LINUX_DEFAULT=""`:

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="quiet loglevel=3 logo.nologo vga=790 console=tty1 splash=silent,fadein,fadeout,theme:arch-banner-icons"` 

Per rigenerare `grub.cfg` eseguire:

 `# grub-mkconfig -o /boot/grub/grub.cfg` 

Il parametro `loglevel=3` impedisce i messaggi del kernel anche con hardware non adatto (di recente gli initscripts non lo impostano più di default). `quiet` è necessario inoltre per non visualizzare i messaggi initcpio. `logo.nologo` rimuove il logo di boot (non necessario con [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/) dato che non ne hanno comunque). `console=tty1` reindirizza i messaggi di sistema a tty1 e `splash=silent,fadein,fadeout,theme:arch-banner-icons` crea la dissolvenza del tema 'arch-banner-icons'.

### File di configurazione

Aggiungere uno o più temi installati in `/etc/conf.d/splash`. E' possibile aggiungere anche la risoluzione dello schermo per avere spazi initcpio:

 `/etc/conf.d/splash` 
```
SPLASH_THEMES="
    arch-black
    arch-banner-icons/1280x1024.cfg
    arch-banner-noicons/1280x1024.cfg"
```

**Note:** Il tema **arch-banner-icons** contiene link simbolici ad **arch-banner-noicons**. Quindi se uno di essi è inserito totalmente, lo spazio rimanente sarà salvato limitando le risoluzioni.

## Avviare fbsplash nella initcpio

Aggiungere **fbsplash** all'array HOOKS nel file `/etc/[mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf")`:

 `/etc/mkinitcpio.conf`  `HOOKS="base fbsplash ..."` 

oppure:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev ... uresume fbsplash ..."` 

o in caso di crittografia di sistema:

 `/etc/mkinitcpio.conf`  `HOOKS="base ... keymap encrypt fbsplash ..."` 

Rigenera il tuo initcpio via mkinitcpio. Vedere [il wiki di Mkinitcpio](/index.php/Mkinitcpio_(Italiano) "Mkinitcpio (Italiano)") per maggiori informazioni.

**Note:** Con i vecchi kernel che non supportano devtmpfs, **udev** è necessario prima di **fbsplash** per avviare lo splash (/dev/fb0 per il framebuffer, etc.) e/o evitare schermate visualizzate dal kernel patchato con Fbcondecor. Per evitare interferenze, il componente **uresume** fornito con *uswsusp-fbsplash* aspetterà che qualsiasi estensione **fadein** di Fbcondecor finisca. Per un veloce recupero, è raccomandato mettere **uswsusp** prima di **fbsplash** o addirittura omettere fadein se si una un kernel Fbcondecor.

Se si dovessero avere problemi di fbsplash con KMS (Kernel Mode Setting), provare ad [aggiungere il driver appropriato in mkinitcpio.conf](/index.php/Intel_(Italiano)#KMS_.28Kernel_Mode_Setting.29 "Intel (Italiano)").

## Sfondi per console

Se si dispone di un kernel che supporta Fbcondecor (es. [linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)), è possibile avere sfondi grafici nella schermata iniziale. Basta cercare in AUR per [fbsplash-tema](https://aur.archlinux.org/packages.php?O=0&K=fbsplash-theme&do_Search=Go).

Dopo aver installato il kernel patchato ed fbsplash, aggiungere `fbcondecor` all'array `DAEMONS` nel file `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")`:

 `/etc/rc.conf`  `DAEMONS=(... fbcondecor ...)` 

C'è anche un file di configurazione `/etc/conf.d/fbcondecor` per impostare i terminali virtuali da utilizzare.

Si può anche avviare con uno sfondo ed i messaggi di boot al posto della schermata iniziale. Basta cambiare la riga di comando del kernel per utilizzare la modalità verbose:

```
 quiet console=tty1 splash=verbose,theme:arch-banner-icons

```

## Links

*   [http://fbsplash.berlios.de/](http://fbsplash.berlios.de/) (nuova homepage)
*   [http://dev.gentoo.org/~spock/projects/gensplash/](http://dev.gentoo.org/~spock/projects/gensplash/) (vecchia homepage)