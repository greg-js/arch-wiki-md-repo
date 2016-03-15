A differenza di altri driver framebuffer, `uvesafb` ha bisogno di un demone di virtualizzazione userspace, chiamato `v86d`. Può sembrare sciocco emulare il codice x86 su x86, ma questo è importante se si vuole utilizzare il codice framebuffer su altre architetture (in particolare quelli non-x86). Un nuovo driver per il framebuffer è stato aggiunto al kernel 2.6.24\. Ha molte più funzioni rispetto al `vesafb` standard, tra cui:

1.  Tranciatura corretta e sospensione hardware dopo il ritardo.
2.  Il supporto per risoluzioni personalizzate come nel BIOS di sistema.

Dovrebbe supportare l'hardware almeno quanto `vesafb`.

## Contents

*   [1 Installazione](#Installazione)
*   [2 Preparare il sistema](#Preparare_il_sistema)
    *   [2.1 Modifiche del bootloader](#Modifiche_del_bootloader)
        *   [2.1.1 GRUB](#GRUB)
        *   [2.1.2 GRUB2](#GRUB2)
    *   [2.2 Aggiungere un hook v86d](#Aggiungere_un_hook_v86d)
*   [3 Configurare uvesafb](#Configurare_uvesafb)
    *   [3.1 Definire una risoluzione](#Definire_una_risoluzione)
    *   [3.2 Rigenerare le immagini initramfs](#Rigenerare_le_immagini_initramfs)
    *   [3.3 Riavvio](#Riavvio)
*   [4 Liste di risoluzioni](#Liste_di_risoluzioni)
*   [5 Uvesafb compilato nel kernel](#Uvesafb_compilato_nel_kernel)
*   [6 Homepage di uvesafb](#Homepage_di_uvesafb)
*   [7 Uvesafb e 915resolution](#Uvesafb_e_915resolution)
    *   [7.1 915resolution-static](#915resolution-static)
    *   [7.2 La risoluzione](#La_risoluzione)
    *   [7.3 La stringa HOOKS](#La_stringa_HOOKS)
*   [8 Risoluzione dei problemi](#Risoluzione_dei_problemi)
    *   [8.1 Uvesafb non può riservare la memoria](#Uvesafb_non_pu.C3.B2_riservare_la_memoria)
    *   [8.2 pci_root PNP0A08:00 address space collision + Uvesafb cannot reserve memory](#pci_root_PNP0A08:00_address_space_collision_.2B_Uvesafb_cannot_reserve_memory)

## Installazione

Installare il pacchetto `uvesafb`:

```
# pacman -S v86d

```

## Preparare il sistema

### Modifiche del bootloader

Rimuovere eventuali framebuffer legati ai parametri di avvio del kernel dalla configurazione del bootloader per disabilitare dal caricamento il vecchio framebuffer vesafb.

#### GRUB

Rimuovere tutti i riferimenti a `vga=xxx` dalle righe del kernel in `/boot/grub/menu.lst` per consentire il corretto funzionamento di `uvesafb`.

#### GRUB2

1.  Editare `/etc/default/grub/` commentando la riga **GRUB_GFXPAYLOAD_LINUX=keep**.
2.  Rigenerare grub.cfg per mezzo dello script standard:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

*   Disabilitare il [KMS](/index.php/KMS "KMS") prima di avviare il sistema in framebuffer. In caso contrario, si otterrà una schermata nera, che non darà altra scelta se non quella di riavviare la macchina con `Ctrl`+`Alt`+`Del`.

Per le schede [Intel](/index.php/Intel "Intel"), aggiungere `i915.modeset=0` alla relativa voce in [GRUB](/index.php/GRUB "GRUB") per disabilitare KMS.

### Aggiungere un hook v86d

Aggiungere l'hook v86d alla stringa `HOOKS` in `/etc/mkinitcpio.conf` per consentire il caricamento di `uvesafb` al boot.

```
HOOKS="base udev v86d ..."

```

## Configurare uvesafb

### Definire una risoluzione

Le opzioni per `uvesafb` possono essere impostate nel file `/etc/modprobe.d/uvesafb.conf` che è il file di default installato dal pacchetto [v86d](https://aur.archlinux.org/packages/v86d/).

```
# This file sets the parameters for uvesafb module.
# The following format should be used:
# options uvesafb mode=<xres>x<yres>[-<bpp>][@<refresh>] scroll=<ywrap|ypan|redraw> ...
#
# For more details see:
# [http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/fb/uvesafb.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/fb/uvesafb.txt)
#
options uvesafb mode=1280x800-32 scroll=ywrap

```

### Rigenerare le immagini initramfs

Le modifiche vengono passate mediante l'avvio nelle immagini initramfs, così, bisognerà rigenerare le immagini initramfs per il/i kernel. Nell'esempio seguente si presuppone che il kernel sia quello di default di Arch Linux:

```
# mkinitcpio -p linux

```

### Riavvio

Riavviare il sistema per vedere i cambiamenti.

## Liste di risoluzioni

Un elenco delle risoluzioni possibili può essere generato tramite il seguente comando:

```
$ cat /sys/bus/platform/drivers/uvesafb/uvesafb.0/vbe_modes

```

Gli utenti possono modificare `/etc/modprobe.d/uvesafb.conf` con una qualsiasi voce restituita.

Può essere usato uno qualsiasi dei seguenti comandi per visualizzare la risoluzione del framebuffer corrente come controprova che le impostazioni sono corrette:

```
$ cat /sys/devices/virtual/graphics/fbcon/subsystem/fb0/virtual_size

```

```
$ cat /sys/class/graphics/fb0/virtual_size

```

## Uvesafb compilato nel kernel

Nel caso si utilizzi un kernel custom, si può scegliere di compilare uvesafb all'interno del kernel ed eseguire v86d più tardi nel processo di avvio, per esempio da `/etc/rc.local`. In questo caso, le opzioni per uvesafb possono essere passate come parametri di avvio al kernel nel formato video=uvesafb:<options>. Questa soluzione non va bene nel caso si voglia combinare uvesafb con 915resolution com suggerito più avanti.

## Homepage di uvesafb

L'homepage di uvesafb è [http://dev.gentoo.org/~spock/projects/uvesafb](http://dev.gentoo.org/~spock/projects/uvesafb), dove si possono trovare informazioni più dettagliate (lasciar perdere le informazioni riguardanti la patch del kernel, dato che che è il file di default installata uvesafb è ora incluso nel kernel vanilla; Inoltre parte della documentazione assume che uvesafb sia compilato all'interno del kernel, mentre nel kernel di Arch Linux è compilato come modulo).

## Uvesafb e 915resolution

In questa sezione, esaminiamo uno scenario più complesso. Alcuni chipset video Intel per notebook con wide screen sono conosciuti per avere un BIOS bacato, che non supportano la risoluzione nativa dello schermo! Per questo motivo, 915resolution è stato creato per patchare il bios all'avvio e permettere al server X di usare la risoluzione widescreen. Al momento, il server X è in grado di fare questo senza l'intervento di 915resolution. Comunque, 915resolution può essere combinato con uvesafb in modo da ottenere un widescreen framebuffer, senza nessun bisogno di lanciare X. In questo caso, devi caricare uvesafb dopo aver eseguito 915resolution, in modo che uvesafb possa utlizzare la risoluzione appropriata.

### 915resolution-static

In questo scenario, 915resolution deve essere compilato staticamente (visto che verrà incluso nella initramfs, non può essere collegato a librerie esterne). Per questo motivo non si può utilizzare il pacchetto 915resolution presente nel repository [community]. È presente su AUR il pacchetto [915resolution-static](https://aur.archlinux.org/packages/915resolution-static/). Questo compila 915resolution staticamente e fornisce un hook 915resolution, in modo che si possa eseguire 915resolution prima di caricare uvesafb ed ottenere una risoluzione personalizzata. Installare dunque 915resolution-static via makepkg e [pacman](/index.php/Pacman "Pacman").

### La risoluzione

Per ottenere la risoluzione da te scelta, devi configurare l'hook 915resolution in modo da definire la modalità del BIOS che vuoi rimpiazzare. Puoi ottenere aiuto su tutte le opzioni per 915resolution con:

```
915resolution -h

```

Quindi editare il file `/lib/initcpio/hooks/915resolution` e modificare le opzioni necessarie.:

```
run_hook ()
{
   msg -n ":: Patching the VBIOS..."
   /usr/sbin/915resolution 5c 1280 800
   msg "done."
}

```

Per default, 5c è il codice della modalità del BIOS da rimpiazzare. Puoi ottenere un lista delle modalità video del BIOS disponibili con il comando: `915resolution -l`.

**Note:** Si deve scegliere il codice di una modalità video di cui non si ha bisogno (nè in framebuffer nè in X), perchè 915resolution la rimpiazzerà con quella desiderata. Nell'esempio, `1280 800` è la nuova risoluzione scelta.

### La stringa HOOKS

Aggiungere gli hook 915resolution e v86d (in quest'ordine) nella stringa HOOKS in `/etc/mkinitcpio.conf`. Posizionare questi hook prima di keymap, resume e filesystems.

```
HOOKS="base udev 915resolution v86d ..."

```

Sarà quindi necessario rigenerare la propria initramfs con mkinitcpio (modificare il seguente comando secondo la propria configurazione):

```
mkinitcpio -p linux

```

## Risoluzione dei problemi

### Uvesafb non può riservare la memoria

Controllare di non aver dimenticato di togliere qualche parametro del kernel`vga=xxx`. Questo sovrascrive il framebuffer UVESA con uno VESA standard.

### pci_root PNP0A08:00 address space collision + Uvesafb cannot reserve memory

Ciò si verifica su Acer Aspire One 751h con il kernel 2.6.34-ARCH; non è noto che si verifichi anche su altri sistemi. Anche senza altri framebuffer ad interferire con l'installazione, uvesafb non può riservare la regione di memoria necessaria.

È possibile risolvere questo problema aggiungendo quanto segue ai parametri del kernel nella configurazione del bootloader.

```
pci=nocrs

```