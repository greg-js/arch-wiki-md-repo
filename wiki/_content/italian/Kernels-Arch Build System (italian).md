L'[Arch Build System](/index.php/Arch_Build_System "Arch Build System") può essere usato per creare un kernel personalizzato basato sul pacchetto [linux](https://www.archlinux.org/packages/?name=linux) ufficiale. Questo metodo di compilazione automatizza l'intero processo ed è basato su un pacchetto molto ben collaudato. Puoi modificare il PKGBUILD per usare una personale configurazione del kernel o aggiungere altre patch.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Procurarsi gli ingredienti](#Procurarsi_gli_ingredienti)
*   [2 Modificare il PKGBUILD](#Modificare_il_PKGBUILD)
    *   [2.1 Cambiare pkgname](#Cambiare_pkgname)
    *   [2.2 Cambiare build()](#Cambiare_build())
    *   [2.3 Cambiare la funzione package_linux()](#Cambiare_la_funzione_package_linux())
*   [3 Compilare](#Compilare)
*   [4 Installare](#Installare)
*   [5 Boot Loader](#Boot_Loader)

## Procurarsi gli ingredienti

 `# pacman -S abs base-devel` 

Prima di tutto, hai bisogno di un kernel pulito da cui iniziare la tua personalizzazione. Recupera il file del pacchetto del kernel da ABS:

 `$ ABSROOT=. abs core/linux` 

Quindi, procurati qualsiasi altro file di cui hai bisogno (per esempio file di configurazione personali, patch, ecc...) dalle rispettive fonti.

## Modificare il PKGBUILD

Modificare il PKGBUILD del pacchetto linux ufficiale.

### Cambiare pkgname

Le prime righe saranno come queste:

 `PKGBUILD` 
```
# $Id: PKGBUILD 130991 2011-07-09 12:23:51Z thomas $
# Maintainer: Tobias Powalowski <tpowa@archlinux.org>
# Maintainer: Thomas Baechler <thomas@archlinux.org>

pkgbase=linux
pkgname=('linux' 'linux-headers' 'linux-docs') # Build stock -ARCH kernel
# pkgname=linux-custom       # Build kernel with a different name
_kernelname=${pkgname#linux}
...
```

Come puoi vedere, è presente una riga commentata per creare un kernel con nome diverso. Tutto ciò che devi fare qui è decommentare quella riga, cambiare il suffisso '-custom' secondo le tue esigenze e commentare la riga standard. Se vuoi avere due kernel (ARCH e test) devi disabilitare la sezione conflicts. I file linux.install e linux.preset dovranno essere linux-custom.install and linux-custom.preset. Ad esempio, il tuo file potrebbe diventare:

 `PKGBUILD` 
```
...
#pkgname=('linux' 'linux-headers' 'linux-docs') # Build stock -ARCH kernel
pkgname=linux-test       # Build kernel with a different name
...
#next lines give you problems with nvidia drivers which depend on kernel
#provides=('kernel26')
#conflicts=('kernel26')
#replaces=('kernel26')
```

**Nota:** Questo presuppone che tu non abbia bisogno di ricompilare linux-headers, -manpages o -docs. In caso contrario, cambia di conseguenza tutte e tre le stringhe.

Adesso, tutte le variabili del tuo pacchetto saranno cambiare in base al nuovo nome. Per esempio, dopo aver installato il pacchetto, i moduli saranno posizionati in `/lib/modules/<kernel_release>-test/`.

### Cambiare build()

Probabilmente avrai bisogno di un file .config personalizzato. Puoi decommentare una delle alternative mostrate nella funzione build() del PKGBUILD:

 `PKGBUILD` 
```
...
  # load configuration
  # Configure the kernel. Replace the line below with one of your choice.
  #make menuconfig # CLI menu for configuration
  make nconfig # new CLI menu for configuration
  #make xconfig # X-based configuration
  #make oldconfig # using old config from previous kernel version
  # ... or manually edit .config
...

```

Se hai già un file config del kernel, suggeriamo di decommentare uno degli strumenti di configurazione interattivi, come nconfig, e caricare il tuo config da lì. Questo evita i problemi nel rinominare il kernel riscontrati con altri metodi.

**Nota:** Se decommenti *return 1*, puoi cambiare la cartella sorgente del kernel non appena makepkg termina l'estrazione e dopo usare nconfig. Questo ti permette di configurare il kernel in sessioni multiple. Quando sei pronto per compilare, copia il file .config in cima a config o config.x86_64 (in base alla tua architettura), commenta *return 1* e usa **makepkg -i**. Non usare questo metodo per le patch personalizzate, metti i comandi delle tue patch dopo queste righe.

### Cambiare la funzione package_linux()

Ora devi scrivere una tua funzione per dire al sistema come installare il pacchetto. Questo può essere fatto facilmente cambiando il nome della funzione package_linux() in package_linux-test() ed adattando le istruzioni ai tuoi bisogni. Se non hai necessità particolari, il tuo package_linux-test() dovrebbe somigliare a qualcosa del genere:

 `PKGBUILD` 
```
...
package_linux-test() {
 pkgdesc="The Linux Kernel and modules"
...
}
```

## Compilare

**Suggerimento:** [Eseguire più operazioni di compilazione simultaneamente](/index.php/Makepkg_(Italiano)#MAKEFLAGS "Makepkg (Italiano)") può ridurre significativamente il tempo di compilazione su sistemi multi-core.

Puoi adesso procedere con la compilazione del kernel tramite il solito comando `makepkg` Se hai scelto un programma interattivo per configurare i parametri del kernel (come menuconfig), avrai bisogno di essere presente durante la compilazione.

**Nota:** Il kernel necessita di un certo tempo per essere compilato. Un'ora non è inusuale.

## Installare

Dopo makepkg, puoi dare un'occhiata al file linux.install. Vedrai che alcune variabili sono cabiate. Adesso devi soltanto installare il pacchetto come fai solitamente con pacman (o un programma equivalente):

```
# pacman -U <pacchetto_kernel>

```

## Boot Loader

A questo punto, le cartelle e i file del tuo kernel personalizzato sono state create, come `/boot/vmlinuz-linux-test`. Per testare il nuovo kernel aggiorna il tuo bootloader (/boot/grub/menu.lst for GRUB) e aggiungi le nuove voci ('default' e 'fallback') per il kernel personalizzato. In tal modo avrai sia il kernel predefinito che quello personale in parallelo.