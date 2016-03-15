**NUOVO ed altro ancora in arrivo:** è disponibile uno script bash testato a fondo che automatizza l'intero processo di compilazione manuale elencato di seguito e che incoraggia la filosofia "bleeding edge" quando si tratta dell'ultimo kernel Linux. Questo script permette di usare makepkg con un metodo alternativo, facile e sicuro. Include un'opzione facile da usare per patchare un rilascio MAINLINE(RC) del Kernel. Test recenti del kernel mainline con patch linux-3.1-rc3-git1 (24 Agosto 2011) dimostrano la riuscita della compilazione e dell'installazione. (`uname -a: Linux Galicja 3.1.0-rc3-git1-ARCHMOD #1 PREEMPT Wed Aug 24 03:08:37 CEST 2011 x86_64 Genuine Intel(R) CPU 575 @ 2.00GHz GenuineIntel GNU/Linux`).

**Procedure:**

*   Scaricare lo script (vedere link dopo Procedure).

*   Prima di aprire o eseguire inizialmente il file `linux_kernel.sh`, accedere a root (#) ed usare chmod per dare i permessi di esecuzione appropriati (755):

```
# chmod 755 linux_kernel.sh

```

*   Scaricare i sorgenti del kernel stabile, mainline (rc) e gli snapshot (git/patch) dal [sito del Kernel Linux](http://www.kernel.org) ponendo i file nella cartella opportuna (`/usr/src`).

*   Aprire `linux_kernel.sh` ed inserire con attenzione di **soltanto 5 variabili** che sono richieste per eseguire lo script, quindi salvare il file (Vedere esempi di area input dopo Procedure).

*   Una volta inseriti i valori e scaricati i sorgenti, eseguire lo script da root (#):

```
# ./linux_kernel.sh

```

*   Durante l'esecuzione saranno necessarie una o due pause in cui si richiede un breve intervento dell'utente, le quali si verificheranno all'inizio (primo minuto). L'attuale fiel `.config` del kernel verrà estratto e copiato da `/proc/config.gz` alla cartella del nuovo kernel, 'menuconfig' sarà invocato automaticamente e il valore CONFIG_LOCALVERSION in `.config` sarà riutilizzato. Si tenga presente che questo script non sovrascriverà o eliminerà **mai** alcun file originale (solo soft-link) senza prima avvertire o terminare automaticamente. Ci sono diversi controlli e verifiche presenti in esso per garantire un'esecuzione sicura. Lo script funziona MOLTO bene, quindi, buon divertimento!

**Nota:** Si prega gli utenti NVIDIA di fare correzioni addizionali NECESSARIE dopo il completamento dello script, PRIMA di riavviare. Ci si senta liberi di contattare l'autore per qualsiasi assistenza e/o suggerimento.

**Scaricare lo scipt**

```
   **[linux_kernel.sh](https://docs.google.com/leaf?id=0B8L9kuJ0hMgaYzU5NTYyMWYtNTNmZC00NTM2LThkNjQtODBjYWYxZDk0OTQ3&hl=en_US)** su Google Docs (ultimo aggiornamento: Mercoledì 24 Agosto 2011, 10:53 CET)

```

**Esempio di input area dello script BASH linux_kernel.sh per le 5 variabili richieste:**

```
#==========================================================================
# Enter 5 Kernel Variable Values Here (You MUST fill in ALL values after "="):

# Directory Name holding "mainline", "stable" and/or "snapshot"(patch) source files from kernel.org
# Must end with "/"
kern_src_dir=/usr/src/

# File Name of "mainline" or "stable" Linux Kernel (Must be downloaded and reside in the "kern_src_dir" (/usr/src/)
kern_file_name=linux-3.1-rc3.tar.bz2

# Is a Patch file involved? YES or NO (Must be CAPITALIZED Letters)
patch=YES

# If patch=YES, File Name of "snapshot" patch (Ex. patch-2.6.37-rc1-git12.bz2) residing in "kern_src_dir" (/usr/src/)
# If patch=NO, then this value does NOT matter. If you wish, enter NONE (patch=NONE)
patch_file_name=patch-3.1-rc3-git1.bz2

# To build the kernel in a multithreaded (faster) way, the -j option is used with the 'make' program
# It is BEST to give a number to the -j option that corresponds to TWICE the number of processors in the system
# ( Ex. Machine with 1 processor: jval=2, Machine with 2 processors: jval=4, etc.)
# To disable this option, enter the value zero ("0"): ( Ex. jval=0 )
jval=0
#==========================================================================

```

**Esempio di output al termine dello script:**

```
                            *Summary of Changes - File(s) Created and/or Deleted*

                               8 File(s) Created:

                               /usr/src/linux-3.1-rc3-git1-KNL/
                               /boot/vmlinuz-3.1-rc3-git1-ARCHMOD
                               /boot/kernel30-3.1-rc3-git1-ARCHMOD.img
                               /lib/modules/3.1.0-rc3-git1-ARCHMOD/
                               /usr/src/linux
                               /usr/src/linux-3.0
                               /boot/System.map-3.1-rc3-git1
                               /boot/System.map

                               3 File(s) Deleted:

                               /boot/System.map
                               /usr/src/linux
                               /usr/src/linux-3.0

                                   *SUCCESS - Main Processes COMPLETE*

                      *NVIDIA users, please make additional NECESSARY adjustments*

          *Please Configure /boot/grub/menu.lst accordingly and you are done. Then REBOOT & TEST!*

```