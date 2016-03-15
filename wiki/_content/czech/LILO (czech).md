*LI*nux *LO*ader, nebo zkráceně **LILO**, je všeobecně použitelný zavaděč (multi-boot loader) pro Linuxové systémy. Navzdory tomu, že byl mnoho let standardní volbou, byl postupně nahrazován programem [GRUB](/index.php/GRUB "GRUB"), alternativním zavaděčem, který nabízí snadnější konfiguraci a menší šanci, že se systém stane nenabootovatelným.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Konfigurace](#Konfigurace)
    *   [2.1 Příklad nastavení](#P.C5.99.C3.ADklad_nastaven.C3.AD)
*   [3 Zdroje](#Zdroje)

## Instalace

LILO může být instalováno během instalace systému výběrem balíčku [lilo](https://aur.archlinux.org/packages/lilo/). Také může být instalováno dodatečně:

```
# pacman -S lilo

```

## Konfigurace

LILO se konfiguruje editací souboru `/etc/lilo.conf` a následným spuštěním příkazu `lilo`, který aplikuje nové nastavení. Pokud zvolíte LILO během instalace Arch Linuxu, konfigurační soubor by měl již být proveden.

Berte na zřetel, že LILO *vyžaduje* být spuštěno po každém upgradu kernelu, jinak systém zůstane v nebootovatelném stavu.

Další nápověda pro nastavení LILO je na serveru [LILO-mini-HOWTO](http://www.tldp.org/HOWTO/LILO.html).

### Příklad nastavení

Typické nastavení LILO:

**Tip:** Pokud LILO opravdu pomalu spouští bzImage, zkuste přidat parametr `compact` do globální sekce souboru `/etc/lilo.conf`, jak je ukázáno níže.
 `/etc/lilo.conf` 
```
#
# /etc/lilo.conf
#

boot=/dev/hda
# This line often fixes L40 errors on bootup
# disk=/dev/hda bios=0x80

default=Arch
timeout=100
lba32
prompt
**compact**

image=/boot/vmlinuz-linux
        label=Arch
	append="devfs=nomount"
	vga=788
        root=/dev/hda2
        read-only

image=/boot/vmlinuz-linux
        label=ArchRescue
        root=/dev/hda8
        read-only

other=/dev/hda1
        label=Windows

# End of file
```

## Zdroje

*   [Seznam parametrů kernelu, které mohou být použité během bootování](http://www.mjmwired.net/kernel/Documentation/kernel-parameters.txt)
*   [Seznam parametrů kernelu s bližším vysvětlením a seskupených podle nastavení ('Kernel Boot Command-Line Parameter Reference', *Linux Kernel In A Nutshell*)](http://www.kernel.org/pub/linux/kernel/people/gregkh/lkn/lkn_pdf/ch09.pdf)