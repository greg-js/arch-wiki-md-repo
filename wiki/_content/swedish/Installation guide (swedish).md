Detta är en guide för att installera [Arch Linux](/index.php/Arch_Linux "Arch Linux") från en upstartbar media file. Före installation påbörjas är det rekommenderat att läsa [FAQ](/index.php/FAQ "FAQ"). För konversationer i detta dokument, läs [Help:Reading](/index.php/Help:Reading "Help:Reading"). Speciellt när det gäller kod exemple, för dessa kan inhålla temporära element(formatet är `*italics*`) dess måste ersättas manuellt.

För mer detalierad förklaring, läs de respektive [ArchWiki](/index.php/ArchWiki "ArchWiki") artiklarna eller de vardera programmens [man page](/index.php/Man_page "Man page"). För interaktiv hjäp använd [IRC channel](/index.php/IRC_channel "IRC channel") och [forum](https://bbs.archlinux.org/) är också tillgänglig.

Arch Linux borde fungera på vilken som helst [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64")-kompatibel system, med en minimum mänged av 512MB RAM. En grundläggande installation med all paket från [base](https://www.archlinux.org/packages/?name=base) borde ta mindre än 800MB av hårddisk utrymmet. denna guid anntar en fungerande internet anslutning, för att kunna laddaner paket från internet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Före Installationen](#Före_Installationen)
    *   [1.1 Verifiering signaturer](#Verifiering_signaturer)
    *   [1.2 Startup från installations materialet](#Startup_från_installations_materialet)
    *   [1.3 Välj tangenbords arrangemang](#Välj_tangenbords_arrangemang)
    *   [1.4 Bekräfta uppstartsläge](#Bekräfta_uppstartsläge)
    *   [1.5 Anslut till internet](#Anslut_till_internet)
    *   [1.6 Uppdatera systemklockan](#Uppdatera_systemklockan)
    *   [1.7 Förbered installations media](#Förbered_installations_media)
        *   [1.7.1 Example på installations media arrangemanget](#Example_på_installations_media_arrangemanget)

## Före Installationen

Installations materialet och deras [GnuPG](/index.php/GnuPG "GnuPG") verifications signaturer kan hämtas från [Nerladdnings](https://archlinux.org/download/) sidan.

### Verifiering signaturer

Det är rekommenderat att Verifiera installations materialet dess före användning, specielt om nedladdningen skedde via *HTTP server*, som är mer mottaglig till avlyssning [skadliga serverar](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

Ett system med [GnuPG](/index.php/GnuPG "GnuPG") installerat, gör detta genom att laddaner *PGP signature* (under *Checksums*) till Installations materialets `*directoy*`, efter detta är gjort [verifiera](/index.php/GnuPG#Verify_a_signature "GnuPG") med detta kommando:

```
$ gpg --keyserver-options auto-key-retrieve --verify archlinux-*version*-x86_64.iso.sig

```

Du kan också göra detta från en befintlig [Arch Linux](/index.php/Arch_Linux "Arch Linux") genom att använda:

```
$ pacman-key -v archlinux-*version*-x86_64.iso.sig

```

[Template:Notera](/index.php?title=Template:Notera&action=edit&redlink=1 "Template:Notera (page does not exist)")

### Startup från installations materialet

Installations materialet kan var ett [USB mine](/index.php/USB_flash_installation_media "USB flash installation media"), [optisk skiva](/index.php/Optical_disc_drive#Burning "Optical disc drive") eller via netvärket med [PXE](/index.php/PXE "PXE"). för andra sätt att installera kolla up [Category:Installation process](/index.php/Category:Installation_process "Category:Installation process").

### Välj tangenbords arrangemang

Standard [arrangemanget](/index.php/Console_keymap "Console keymap") är [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Andra arrangemanget kan visas genom att använda:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

För att ändra arrangemanget,

```
# loadkeys sv-latin1

```

### Bekräfta uppstartsläge

### Anslut till internet

### Uppdatera systemklockan

Använd [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) för att Verifiera att klockan stämmer:

```
# timedatectl set-ntp true

```

Bäkrefta tjänsten genom att använda `timedatectl status`.

### Förbered installations media

#### Example på installations media arrangemanget

| BIOS med [MBR](/index.php/MBR "MBR") |
| Mount point | Partition | [Partitionstyp](https://en.wikipedia.org/wiki/Partition_type "w:Partition type") | Recommenderad Storlek |
| `/mnt` | `/dev/sd*X*1` | Linux | Resten av enheten |
| [BYTA] | `/dev/sd*X*2` | Linux byta | Mer än 512 MiB |
| UEFI med [GPT](/index.php/GPT "GPT") |
| Mount point | Partition | [Partitionstyp](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "w:GUID Partition Table") | Recommenderad Storlek |
| `/mnt/boot` eller `/mnt/efi` | `/dev/sd*X*1` | [EFI system partition](/index.php/EFI_system_partition "EFI system partition") | 256–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Linux x86-64 root (/) | Resten av enheten |
| [BYTA] | `/dev/sd*X*3` | Linux byta | Mer än 512 MiB |