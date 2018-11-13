Každý nový archista by měl po čerstvé instalaci dokončit pár věcí. V tomto dokumentu najdete pár tipů a další užitečné informace pro nováčky.

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Detekce](#Detekce)
    *   [1.2 Zrychlení bootovacího procesu LILO](#Zrychlení_bootovacího_procesu_LILO)
    *   [1.3 Výkon harddisku](#Výkon_harddisku)
*   [2 Pauza na konci bootovacího procesu](#Pauza_na_konci_bootovacího_procesu)
*   [3 Podpora myši v konzoli (gpm)](#Podpora_myši_v_konzoli_(gpm))
*   [4 Povolení zvuku (ALSA/OSS)](#Povolení_zvuku_(ALSA/OSS))
*   [5 Start X at login](#Start_X_at_login)
*   [6 Sestavení vlastního kernelu](#Sestavení_vlastního_kernelu)
*   [7 ABS k sestavení vlastního balíčku (programu)](#ABS_k_sestavení_vlastního_balíčku_(programu))
*   [8 Optimalizace balíčků](#Optimalizace_balíčků)
*   [9 Kernel Updates](#Kernel_Updates)
*   [10 Osobní příkazové aliasy](#Osobní_příkazové_aliasy)
*   [11 Snížení "Sleeping time" při vypínání](#Snížení_"Sleeping_time"_při_vypínání)
*   [12 Nastavení časové zóny](#Nastavení_časové_zóny)
*   [13 Vypnutí IPv6](#Vypnutí_IPv6)
*   [14 PDF prohlížeč (kghostview)](#PDF_prohlížeč_(kghostview))
*   [15 Užitečné programy & příkazy](#Užitečné_programy_&_příkazy)
    *   [15.1 Pacman](#Pacman)
    *   [15.2 makepkg](#makepkg)
    *   [15.3 abs](#abs)
*   [16 Popis souborů](#Popis_souborů)
*   [17 Extrakce komprimovaných souborů](#Extrakce_komprimovaných_souborů)
*   [18 Nastavení zrcadel a repozitářů](#Nastavení_zrcadel_a_repozitářů)
*   [19 Nastavení grafického zobrazování](#Nastavení_grafického_zobrazování)

### Hardware

#### Detekce

*   `lshwd` je nástroj pro rozpoznávání a detekci hardwaru. Informuje uživatele, který modul je třeba nahrát a nastavit.
*   Nebo můžete použíte také `hwdetect`. Někdy může být rychlejší než hwd. A nezapoměňte také na `lshal`.

#### Zrychlení bootovacího procesu LILO

*   Ke zrychlení bootovacího procesu, pokud požíváte LILO, zadejte do souboru `/etc/lilo.conf` následující parametr:

```
 compact

```

#### Výkon harddisku

*   Výkon harddisku znásobíte, pokud použijete program hdparm. Nejlepší místo, kde ho použít, je `/etc/rc.sysinit`. Příklad parametrů:

*   *   -a1024 = nastaví read_ahead buffer na 1024 bajtů
    *   -c3 = nastaví IO na 32 bitů se synchronizací (zkuste také c2)
    *   -d1 = zapne podporu [DMA](/index.php?title=DMA&action=edit&redlink=1 "DMA (page does not exist)")
    *   -m16 = nastaví multiple buffers [l18n fixme] na 16

příklad:

```
 hdparm -a1024 -c3 -d1 -m16 /dev/hda

```

(Poznámka: nová jádra 2.6.20+ už nepoužívají hdx, ale sdx - takže použijte adekvátní označení.)

### Pauza na konci bootovacího procesu

*   Pokud chcete získat pauzu na konci bootovacího procesu - než se zobrazí login - přidejte na konec `/etc/rc.local` následující (obvykle se používá pro zjištění chyb během bootu):

```
 read KEY

```

### Podpora myši v konzoli (gpm)

*   I v konzoli můžete používat myš - nainstalujte gpm:

```
pacman -S gpm

```

*   Pokud se kurzor chová zmateně a myš nelze používat, bude třeba změnit `/etc/conf.d/gpm`.

**Pro PS/2 myši nahraďte existující řádek následujícím:**

```
GPM_ARGS="-m /dev/psaux -t ps2"

```

**Pro USB myši nahraďte existující řádek následujícím:**

```
GPM_ARGS="-m /dev/input/mice -t imps2"

```

*   Pokud to funguje, můžete přidat `gpm` do pole `DAEMONS` v souboru `/etc/rc.conf`, aby se spouštěl při startu.

### Povolení zvuku (ALSA/OSS)

*   [Nastavení ALSA](/index.php/ALSA_(%C4%8Cesky) "ALSA (Česky)"): ALSA je zvukový systém na Linuxu
*   [OSS Setup](/index.php/OSS "OSS"): Svobodný, ale proprietární ovladač

### Start X at login

*   [Start X at login](/index.php/Start_X_at_login "Start X at login")

### Sestavení vlastního kernelu

*   Při sestavování vlastního jádra ([Kernel/Hardware Issues](https://bbs.archlinux.org/viewforum.php?f=22&sid=7565520b3217f47ccc4ffc6f43f4744a)) musí být následující volby nastaveny a slinkovány a NE jako moduly:
    *   *   Code maturity level options
        *   Prompt for development and/or incomplete code/drivers = on
        *   Device Drivers
        *   File systems
        *   Pseudo filesystems
        *   `/dev` file system support = on
        *   Automatically mount at boot = on
    *   **k možnosti zvýšení výkonu hd pomocí hdparm, nastavte :**
        *   Device Drivers
        *   ATA/ATAPI/MFM/RLL support = on
        *   Enhanced IDE/MFM/RLL disk/cdrom/tape/floppy support = on
        *   Generic PCI bus-master DMA support = on
        *   Intel PIIXn chipsets support = on
        *   <and your IDE hdw...> = on
*   Ke zvýšení rychlosti načítání jádra nastavte statický link VEŠKERÉHO hardwaru ke specifickým ovladačům (které budete načítat stejně použitím `/etc/modprobe.d/modprobe.conf` nebo jinak) místo vytvoření jako modul.

### ABS k sestavení vlastního balíčku (programu)

*   Pokud používáte abs k sestavování vlastních balíčků, nezapomeňte prvně zkopírovat cílový adresář balíčku do `/var/abs/local/<pkgname>`, vyhnete se tak přepsání souborů a konfigurace při příštím updatu abs..

### Optimalizace balíčků

*   Pro optimalizaci balíčků sestavených pomocí makepkg (kernel je dobrý příklad) nastavte požadované vlastnosti gcc v `/etc/makepkg.conf`:

```
 (příklad pro athlon cpu)
 export CFLAGS="-march=athlon -O2 -pipe -fomit-frame-pointer"
 export CXXFLAGS="-march=athlon -O2 -pipe -fomit-frame-pointer"

```

### Kernel Updates

*   Nezapomeňte spustit `lilo` po každém updatu kernelu (např. pokaždé když nahradíte boot image, obvykle nazvaný `/boot/vmlinuzXX`, atd.).
    *   Pokud jste zapoměli a potřebujete provést obnovu z CD, tady je pár kroků:

```
 modprobe xfs
 mount -t xfs /dev/discs/discX/partY /mnt
 mount -t xfs /dev/discs/discV/partW /mnt/boot (pokud máte)
 mount -t devfs none /mnt/dev
 mount -t proc none /mnt/proc
 chroot /mnt /sbin/lilo

```

### Osobní příkazové aliasy

*   Můžete si vytvořit vlastní příkazové aliasy použitím `<homedir>/.bashrc` nebo `/etc/profile`. Obojí může být použito k vytvoření vlastních:

```
 #alias ls="ls --color=auto" není nutné v ARCH LINUXu
 alias ll="ls -lh"
 alias la="ls -a"
 alias exit="clear; exit"
 alias x="startx"

```

### Snížení "Sleeping time" při vypínání

*   Můžete snížit systémový "Sleeping time" při vypínání změnou "sleep" parametrů v `/etc/rc.shutdown` a `/etc/rc.single`.

### Nastavení časové zóny

*   K nastavení časové zóny (tak aby se zobrazoval správný čas) najděte v `/usr/share/zoneinfo/` svoji časovou zónu a změňte proměnnou `TIMEZONE` v `/etc/rc.conf`:

```
TIMEZONE=Europe/Prague

```

### Vypnutí IPv6

Do obecného rozšíření IPv6 můžete čerpat z [disabling the IPv6 module](/index.php/IPv6_-_Disabling_the_Module "IPv6 - Disabling the Module").

### PDF prohlížeč (kghostview)

*   K opravě PDF prohlížeče (kghostview) nainstalujte ghostscript pomocí:

 `pacman -S ghostscript` 

*   a změňte sekci Ghostscript v `<homedir>/.kde/share/config/kghostviewrc` na:

```
  Antialiasing arguments=-sDEVICE=x11 -dTextAlphaBits=4 -dGraphicsAlphaBits=<2 -dMaxBitmap=10000000
  GS Version=
  Interpreter=/usr/bin/gs
  Non-antialiasing arguments=-sDEVICE=x11
  Redetection Counter=2 

```

### Užitečné programy & příkazy

*   `grep` - vyhledávání souborů dle obsahu. (příklad: `grep -i syslog /etc/*` hledání v /etc pro soubory obsahující slovo "syslog", NEcitlivost na velikost písmen (použitím `-i` parametru))
*   `killall <process_name>` - "zabije"(ukončí) proces podle jména (příklad: `killall kdm`)
*   `ps` - zobrazení statusu procesu (příklad: `ps -xau` zobrazí všechny aktivní procesy)
*   `locate` - rychlá lokalizace souborů na disku (použijte `locate -u` prvně k vytvoření/updatu souboru db...) (příklad: `locate Xservers` nalezne všechny soubory pojmenované Xservers)

#### Pacman

[Pacman](/index.php/Pacman "Pacman") je automatizovaný nástroj pro správu balíčků - lokálně nebo pomocí webu. Sám si řeší závislosti jednotlivých balíčků, což je největší problém ve světě balíčkovacích distrubucí linuxu (-tak-jak-víme:)). Pro zlepšení výkonu pacman může být čas od času optimalizován:

 `pacman-optimize` 

#### makepkg

Automatický nástroj pro tvorbu balíčků - ve skutečnosti automatizuje `./configure && make && make install` proceduru.Používá soubor jménem PKGBUILD, který musí být ve stejném adresáři, ve kterém budete sestavovat balíček. Prohlídněte si PKGBUIL soubor a přečtěte si instalační dokument k pochopení jak pracovat s makepkg.

#### abs

Automatický nástroj, který umožňuje znovu sestavení kteréhokoliv balíčku (tak že můžete poskytnout své vlastní nastavení kompilátoru a linkeru pro lepší optimalizaci, info o debugging atd.). Spuštění abs synchronizuje všechny Vaše PKGBUILD skripty z CVS repozitáře do `/var/abs`.

### Popis souborů

*   `<homedir>/.xinitrc` - kontroluje, které programy jsou spuštěny na startu; poslední řádka musí být Váš preferovaný window manager a musí být před ním `exec`
*   `/etc/profile` - profilový soubor systému; načítá konfiguraci prostředí dle profilu. (kernel musí podporovat profily)
*   `/etc/rc.conf` - hlavní konfigurační soubor,něco jako config.sys v steroids...
*   `/etc/rc.sysinit` - je to jako hlavní soubor autoexec.bat, který se stará o načítání a nastavování systému
*   `/etc/rc.single` - skript pro jednouživatelský systém
*   `/etc/rc.multi` - skript pro víceuživatelský systém
*   `/etc/rc.local` - kript pro místní víceuživatelský systém
*   `/etc/rc.shutdown` - skript pro vypínání
*   `/etc/rc.d/*` - konfiguruje démony.

### Extrakce komprimovaných souborů

```
 file.tar : tar xvf file.tar
 file.tgz : tar xvzf file.tgz
 file.tar.gz : tar xvzf file.tar.gz
 file.bz : bzip -cd file.bz | tar xvf -
 file.bz2 : tar xvjf file.tar.bz2 **NEBO** bzip2 -cd file.bz2 | tar xvf -
 file.zip : unzip file.zip
 file.rar : unrar x file.rar

```

* * *

WikiMigration & Rewrite--[dlanor](/index.php/User:Dlanor "User:Dlanor") 15:36, 23 Jul 2005 (EDT)

## Nastavení zrcadel a repozitářů

Pokud jste si již běhěm instalace neurčili, jaká zrcadla chcete využívat pro stahování balíčků, nebo vám prostě z nějakého důvodu nefungují tak, jak byste si přáli, měli byste se podívat do souboru `/etc/pacman.conf`.

```
 nano /etc/pacman.conf

```

V tomto souboru nenastavujete, jaké konkrétní zrcadlo budete využívat. Zde nastavujete, jaký druh repozitářů budete sledovat - nastavení tohoto souboru určuje, jaké balíky budete moci stáhnout jednoduchým použitím

```
 pacman -S Název_balíku

```

Nastavení probíhá formou odkomentování (smazání mřížky na začátku řádky) řádku obsahujícího název repozitáře v hranatých závorkách a k němu příslušícímu řádku ve tvaru "include=Cesta_k_souboru_obsahujímu_název_zrcadla".

Je vhodné mít odkomentované repozitáře Current, Extra a Community. Testing a Unstable odkomentujte, pouze tehdy, [pokud víte](/index.php/Ofici%C3%A1ln%C3%AD_repozit%C3%A1%C5%99e_(%C4%8Cesky)#.5Bunstable.5D "Oficiální repozitáře (Česky)"), co děláte.

Nastavení jednotlivých zrcadel najdete ve výše zmíněných souborech a to, které zrcadlo chcete využívat, určíte opět odkomentováním příslušného řádku.

Více se o Pacmanovi a jeho funkcích dozvíte na jeho [stránce](/index.php/Pacman_(%C4%8Cesky) "Pacman (Česky)").

## Nastavení grafického zobrazování

Nastavení [X serveru](/index.php/Xorg_(%C4%8Cesky) "Xorg (Česky)") (programu, který má na starosti grafické zobrazování), se stejně jako v drtivé většině současných linuxových distribucí nachází v souboru `/etc/X11/xorg.conf`. Je možné, že tam ještě svoje vlastní nastavení nemáte (po instalaci), můžete jej tedy vytvořit pomocí

```
 hwd -x

```

Tento příkaz vytvoří soubor v `/etc/X11/xorg.conf.hwd`, je tedy vhodné ho zkopírovat na jeho správné místo (místo, kde ho Xserver hledá).

```
 cp /etc/X11/xorg.conf.hwd /etc/X11/xorg.conf

```

Nyní můžete v tomto souboru měnit jednotlivé informace. Viz [Nastavení Xorg](/index.php/Xorg_(%C4%8Cesky) "Xorg (Česky)")