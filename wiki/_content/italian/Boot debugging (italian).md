**Note:** La seguente sezione è stata spostata da [GRUB Legacy (Italiano)#Modalità debug avanzata](/index.php/GRUB_Legacy_(Italiano)#Modalit.C3.A0_debug_avanzata "GRUB Legacy (Italiano)").

Il file di grub `menu.lst` prevede un modo conveniente per aggiungere un certo numero di voci con [extended kernel parameters](http://www.kernel.org/doc/Documentation/kernel-parameters.txt) per configurare ogni tipo di impostazioni avanzate per consentire l'avvio rapido e conveniente del proprio sistema esistente, con diversi livelli di output di debug. È molto facile ed utile creare dei livelli di debug con la semplice aggiunta di voci addizionali alla configurazione di grub. E se capitasse di avere qualche problema a causa di una mancanza di corrente o guasto hardware, si possono risparmiare ore di smanettamenti, e naturalmente niente può superare l'output di debug quando si tratta di analizzare il proprio sistema.

## Contents

*   [1 Voci utili nel menu.lst](#Voci_utili_nel_menu.lst)
*   [2 Debug leggero](#Debug_leggero)
*   [3 Debug medio](#Debug_medio)
*   [4 Debug completo](#Debug_completo)
*   [5 Debug estremo](#Debug_estremo)
*   [6 Debug oltre ogni limite](#Debug_oltre_ogni_limite)
    *   [6.1 Pausa di init](#Pausa_di_init)
    *   [6.2 Il debug di init](#Il_debug_di_init)
    *   [6.3 Net Console](#Net_Console)
    *   [6.4 Deviare cmdline](#Deviare_cmdline)

## Voci utili nel menu.lst

A chi interessa il debug, ecco alcune voci del grub per "powerusers": (basta aggiungere al proprio `menu.lst`).

```
title Shutdown the Computer
halt

title Reboot the Computer
reboot

title Command Line
commandline

title Install GRUB to hd0 MBR
root (hd0,0)
setup (hd0)

title Matrix
color green/black light-green/green

title Scan for /boot/grub/menu.lst
find --set-root --ignore-floppies /boot/grub/menu.lst
configfile /boot/grub/menu.lst

title Scan for /boot/menu.lst
find --set-root --ignore-floppies /menu.lst
configfile /boot/menu.lst

# http://www.vortex.prodigynet.co.uk/x86test/
title    Run x86test (CPU Info)
kernel /boot/x86test_zImage.bin
#wget http://www.vortex.prodigynet.co.uk/x86test/x86test_zImage.bin

# http://www.memtest.org/
title    Run memtest86+ (Memory Testing)
kernel /boot/memtest86+-1.70.bin

```

## Debug leggero

Un modo rapido per visualizzare messaggi più dettagliati sulla console è avviare la voce grub normale dopo aver aggiunto **verbose** alla riga del kernel. Questa semplice aggiunta alla riga del kernel innesca un maggior numero di informazioni di log grazie al file `/etc/rc.sysinit`, che nella parte superiore del file, specifica:

```
if /bin/grep -q " verbose" /proc/cmdline; then /bin/dmesg -n 8; fi

```

Un modo semplice di ottenere più messaggi e informazioni di debug nei log.

```
title  Arch Linux DEBUG Light
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro rootwait verbose
initrd /initramfs-linux.img

```

## Debug medio

Quest'altro esempio di voce nel `menu.lst`, si trasforma in una vera e propria registrazione, che viene impostata dal kernel e non da uno script di init. L'ggiunta del parametro **debug** alla riga del kernel, spinge tutta una serie di meccanismi interni del kernel a stampare un debug maggiore rispetto a quello di default.

```
title Arch Linux DEBUG Medium
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro rootdelay=5 panic=10 debug
initrd /initramfs-linux.img

```

## Debug completo

Un parametro del kernel ancora più impressionante è quello **ignore_loglevel**, che fa ìn modo che il sistema ignori qualsiasi livello di log esterno e mantenga il livello di log interno alla massima capacità di debug, fondamentalmente rendendo dmesg in grado di abbassare il livello di debug.

```
title Arch Linux DEBUG Heavy
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro rootdelay=5 panic=10 debug ignore_loglevel
initrd /initramfs-linux.img

```

## Debug estremo

Se l'espressione "Heavy Debug" può far pensare a tanto output, questo è solo la metà del logging prodotto con questo esempio. Si occupa di varie cose: utilizza il parametro **earlyprintk** per preparare il kernel ad una "prima" "stampata" di messaggi sullo schermo, e con il parametro **keep** mantiene più a lungo l'output sullo schermo. Questo permette di vedere i log che normalmente vengono nascosti dal processo di avvio. Questo cambia anche la dimensione del buffer di registro a 10MB, e indica, inoltre, che eventuali segnali "fatals" vengano stampati con **print_fatal_signals**. Per l'ultima opzione, **sched_debug**, si può cercare nell'ottima documentazione del kernel [kernel parameters](http://www.kernel.org/doc/Documentation/kernel-parameters.txt).

```
title Arch Linux DEBUG Extreme
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro debug ignore_loglevel log_buf_len=10M print_fatal_signals=1 LOGLEVEL=8 earlyprintk=vga,keep sched_debug
initrd /initramfs-linux.img

```

## Debug oltre ogni limite

I primi esempi di debug mostrano alcuni parametri del kernel veramente ottimi per ottenere debug molto dettagliati. Questi tipi di debug sono assolutamente fondamentali se si vuole il massimo dal sistema o semplicemente saperne di più su ciò che accade dietro le quinte. Ma c'è un trucco finale che è il mio preferito, e cioè la possibilità di impostare entrambe le variabili d'ambiente e, soprattutto, i parametri dei moduli al boot.

Come esempio, ecco la riga di avvio usata su un vecchio desktop Dell, solo per illustrare i parametri dei moduli e le variabili d'ambiente.

```
title  Arch Linux X-256
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro rootwait pause_on_oops=5 panic=60 i915.modeset=1 no_console_suspend ipv6.disable=1 TERM=xterm-256color quiet 5
initrd /initramfs-linux.img

```

A causa delle limitate risorse di memoria e CPU nel computer d'esempio, è stato disattivato ipv6\. È stato attivato al kernel il modesetting per la scheda video i915, impostato il terminale come xterm a 256 colori, e il boot direttamente in [X](/index.php/Xorg_(Italiano) "Xorg (Italiano)"). Questo permette di utilizzare una configurazione ottimizzata di arch-linux, incredibile in quanto a velocità grazie all'utilizzo di [slim](/index.php/SLiM_(Italiano) "SLiM (Italiano)") come login manager, [ratpoison](/index.php/Ratpoison "Ratpoison") come [window manager](/index.php?title=Display_Manage_(Italiano)&action=edit&redlink=1 "Display Manage (Italiano) (page does not exist)"), e il terminale con [tmux](/index.php/Tmux "Tmux") come shell per il login, il tutto al boot, come illustrato da pstree (oltre a [Synergy](/index.php/Synergy "Synergy")!).

```
init,1  
  |-slim,3096
  |   |-X,3098 -nolisten tcp vt07 -auth /var/run/slim.auth
  |   `-ratpoison,3107,askapache
  |       |-terminal,5341 -x sh -c exec /usr/bin/tmux -2 -l -u -q attach -d -t tmux-askapache
  |       |   |-bash,11165
  |       |   |-tmux,5345 -2 -l -u -q attach -d -t tmux-askapache
  |       |   `-{terminal},5346
  |       `-xscreensaver,3113 -no-splash
  |-synergyc,6121,galileo -f --name galileo-fire --restart 10.66.66.2:26666
  |
  `-tmux,5348,askapache -2 -l -u -q attach -d -t tmux-askapache
      |-bash,5351
      |   `-ssh,9969 lug@askapache.com
      `-bash,5868
         `-vim,11149 -p sda1/grub/menu.lst /boot/grub/menu.lst

```

Questo tipo di sistema ottimizzato è possibile solo se prima si riesce a comprendere il sistema, dal debug del kernel come illustrato in precedenza, da quello del processo init, e, soprattutto, da quello dei moduli attivati per l'hardware/firmware/software del proprio sistema. Il debug dei moduli è impegnativo, ma ne vale la pena, perchè poi si è in grado di fare un debug veramente folle da grub, come nell'esempio seguente. Si noti che la voce grub "reale" è tutta su una riga, qui è divisa in 4 righe per esigenze di impaginatura della pagina wiki. Sostanzialmente si attiva ogni modulo al suo massimo livello di debug. (Consultare [Improve boot performance](/index.php/Improve_boot_performance "Improve boot performance")).

```
title  Arch Linux DEBUG INSANE
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro rootwait ignore_loglevel debug debug_locks_verbose=1 sched_debug initcall_debug mminit_loglevel=4 udev.log_priority=8 
       loglevel=8 earlyprintk=vga,keep log_buf_len=10M print_fatal_signals=1 apm.debug=Y i8042.debug=Y drm.debug=1 scsi_logging_level=1 usbserial.debug=Y 
       option.debug=Y pl2303.debug=Y firewire_ohci.debug=1 hid.debug=1 pci_hotplug.debug=Y pci_hotplug.debug_acpi=Y shpchp.shpchp_debug=Y apic=debug 
       show_lapic=all hpet=verbose lmb=debug pause_on_oops=5 panic=10 sysrq_always_enabled
initrd /initramfs-linux.img

```

Un paio di elementi chiave tra le voci di grub sono **sysrq_always_enabled**, che forza l'"sysrq magic", e che si rivela un salvavita quando il debug a questo livello conduce talvolta la macchina a dei blocchi di sistema. Con sysrq si possono terminare tutti i processi, cambiare i loglevel, smontare i filesystems, o forzare un riavvio. Un'altro parametro chiave è l'**initcall_debug**, che esegue un debug dell'"init process" incredibilmente dettagliato, spesso molto utile. L'ultimo parametro, veramente utilissimo, è **udev.log_priority=8**, che attiva l'[udev](/index.php/Udev_(Italiano) "Udev (Italiano)") logging.

#### Pausa di init

Per esempio, se si aggiunge **break=y** nella riga del kernel, init si interrompe all'inizio del [boot process](/index.php/Arch_boot_process_(Italiano) "Arch boot process (Italiano)") (dopo il caricamento dei moduli) e lancia una shell interattiva sh che può essere utilizzata per la risoluzione dei problemi. (Il boot normale continua dopo il logout.) Questo è molto simile alla shell che presenta se il computer viene spento prima di essere in grado di farlo correttamente. L'tilizzo di questo parametro permette di entrare in questa modalità in modo diverso.

```
title  Arch Linux Init Break
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro rootwait break=y
initrd /initramfs-linux.img

```

#### Il debug di init

Il parametro **udev.log_priority=8** è l'equivalente della modifica del file `/etc/udev/udev.conf`, tranne che per i più brevi tempi di esecuzione, attivando l'output di debug per [udev](/index.php/Udev_(Italiano) "Udev (Italiano)"). Volendo visualizzare ulteriori dettagli del proprio hardware, questo è il parametro perfetto. Un'altro trucco è la modifica di `/etc/udev/udev.conf` in modalità "verbose", che attiva all'immagine initrd il file che rende "verbose" il debug di udev, aggiungendo a `/etc/mkinitcpio.conf` questo:

```
FILES="/etc/modprobe.d/modprobe.conf /etc/udev/udev.conf"

```

che su arch è facile come fare un

```
# mkinitcpio -p linux

```

Il debug di [udev](/index.php/Udev_(Italiano) "Udev (Italiano)") è la chiave fondamentale, perchè [initrd](/index.php?title=Initrd&action=edit&redlink=1 "Initrd (page does not exist)") esegue un [root change](/index.php/Change_root "Change root") alla fine dell'esecuzione per lanciare un programma come /sbin/init in modalità chroot, e se il nuovo file system non ha una directory /dev valida, udev deve essere inizializzato prima di invocare chroot al fine di fornire `/dev/console`.

```
exec chroot . /sbin/init <dev/console >dev/console 2>&1

```

Quindi, fondamentalmente, non si è in grado di visualizzare i log che vengono generati prima che /dev/console sia inizializzata da udev o da uno speciale initrd appositamente compilato. Un metodo che gli sviluppatori del kernel usano per essere in grado di ottenere ancora i messaggi di log generati prima che /dev/console sia disponibile, è quello di fornire una console alternativa attivabile e disattivabile da grub.

#### Net Console

Leggendo la documentazione del kernel per quanto riguarda il debug, si sentirà menzionare "netconsole", che può essere caricata dalla riga del kernel di GRUB, compilata nel kernel, o caricata come modulo durante il tempo di esecuzione. Avere una voce netconsole in `menu.lst` è molto conveniente per il debug di computer più lenti, come vecchi laptop o thin-client. L'utilizzo è molto semplice. Basta impostare un secondo computer (con arch) ad accettare le richieste dei log di sistema su una porta remota, semplice e veloce da fare su arch-linux, basta 1 riga su syslog.conf. Si può usare poi un log-color-parser come ccze per visualizzare tutti i registri syslogs, o consultare everything.log. Poi, dal computer portatile, avviare e selezionare la voce netconsole dal menu di grub, e si inizierà a vedere tutta la registrazione syslog che si desidera sul sistema. Questa tipo di registrazione consente di visualizzare anche i primissimi log disponibili con il parametro del kernel earlyprintk=vga. Netconsole viene utilizzato dagli sviluppatori del kernel, quindi è uno strumento molto potente.

```
title  Arch Linux DEBUG Netconsole
kernel /vmlinuz-linux root=/dev/disk/by-label/ROOT ro netconsole=514@10.0.0.2/12:34:56:78:9a:bc debug ignore_loglevel
initrd /initramfs-linux.img

```

#### Deviare cmdline

Se non si ha accesso al GRUB o alla riga boottime del kernel, come su una macchina virtuale o server, con i privilegi di root è ancora possibile attivare questa specie di verbose semplicistica dei log, usando un puro "hack". Se non è possibile modificare `/proc/cmdline` neanche da root, è possibile inserire il proprio file cmdline in cima a /proc/cmdline, in modo che l'accesso a /proc/cmdline acceda effettivamente al file.

Per esempio se con **cat /proc/cmdline**, si ottiene il seguente:

```
root=/dev/disk/by-label/ROOT ro console=tty1 logo.nologo quiet

```

Con un semplice comando "sed" si potrà sostituire **quiet** con **verbose** così:

```
sed 's/ quiet/ verbose/' /proc/cmdline > /root/cmdline

```

Montare poi /root/cmdline in modo che diventi /proc/cmdline, utilizzando l'opzione **-n** per montarlo, cosicchè il montaggio non venga registrato nel sistema mtab.

```
mount -n --bind -o ro /root/cmdline /proc/cmdline

```

Poi con **cat /proc/cmdline** si otterrà:

```
root=/dev/disk/by-label/ROOT ro console=tty1 logo.nologo verbose

```