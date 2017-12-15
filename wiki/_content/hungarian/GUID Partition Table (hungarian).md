Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [Partitioning](/index.php/Partitioning "Partitioning")

A GUID Partíciós Tábla (GPT) egy új stílusú particionálási mód, mely része a [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") Specifikációnak, és mely a [globálisan egyedi azonosítót](https://en.wikipedia.org/wiki/Globally_unique_identifier "wikipedia:Globally unique identifier") hasznája az eszközök felismeréséhez. Sokban különbözik a [Master Boot Record (Magyar)](/index.php/Master_Boot_Record_(Magyar) "Master Boot Record (Magyar)")-tól (mely a leginkább használt particionálási mód volt a BIOS érában) és nem kevés előnnyel rendelkezik az MBR-rel szemben.

**Figyelem:** Ha Windows-szal együttes dual bootot használunk, ne feledjük, hogy a Windows nem képes GPT lemezt BIOS módban indítani. Ha már Windowst telepítettünk egy MBR módban particionált lemezre, mely így BIOS módban indít, ne konvertáljuk a meghajtót GPT-be, mert a Windows az általunk használt rendszerbetöltő típusától függetlenül képtelen lesz elindulni. Ilyenkor a Windowst UEFI módben kell telepíteni, majd valamely [UEFI Rendszerbetöltőt](/index.php/UEFI_Bootloaders "UEFI Bootloaders") kell használni a Windows indítására. Ez sajnos a Windows használatának korlátja.

Hogy megértsük a GPT-t, meg kell értenünk, mi is az MBR és mik a hátrányai.

## Contents

*   [1 Master Boot Record](#Master_Boot_Record)
    *   [1.1 Az MBR hátrányai](#Az_MBR_h.C3.A1tr.C3.A1nyai)
*   [2 GUID Partíciós Tábla](#GUID_Part.C3.ADci.C3.B3s_T.C3.A1bla)
    *   [2.1 A GPT előnyei](#A_GPT_el.C5.91nyei)
    *   [2.2 Kernel támogatás](#Kernel_t.C3.A1mogat.C3.A1s)
*   [3 Rendszerbetöltő-támogatás](#Rendszerbet.C3.B6lt.C5.91-t.C3.A1mogat.C3.A1s)
    *   [3.1 UEFI rendszerek](#UEFI_rendszerek)
    *   [3.2 BIOS rendszerek](#BIOS_rendszerek)
*   [4 Partitioning Utilities](#Partitioning_Utilities)
    *   [4.1 GPT fdisk](#GPT_fdisk)
        *   [4.1.1 Az MBR átalakítása GPT-vé](#Az_MBR_.C3.A1talak.C3.ADt.C3.A1sa_GPT-v.C3.A9)
    *   [4.2 Util-linux fdisk](#Util-linux_fdisk)
    *   [4.3 GNU Parted](#GNU_Parted)
*   [5 Lásd még](#L.C3.A1sd_m.C3.A9g)

## Master Boot Record

Az MBR partícós tábla a a merevlemez első szektorában raktároz el információkat a partíciókról, a következő sorrendben:

| Hely a lemezen | A kód célja |
| Első 440 bájt | MBR boot kód, melyet a BIOS indít. |
| 441-446 bájt | MBR lemez-szignatúra. |
| 447-510 bájt | A jelenlegi partíciós tábla, az elsődleges és kiterjesztett partíciók információival. (Jegyezzük meg, hogy a logikai partíciók itt nincsenek bejegyezve) |
| 511-512 bájt | MBR indító-szignatúra 0xAA55. |

Az elsődleges partíciókról szóló teljes információ tehát 64 bájtra nagyságra korlátozódik. Hogy ezt valahogy megnöveljék, bevezették a kiterjesztett partíciók használatát, mely egyszerűen egy az elsődlegeshez hasonló, afféle tárolóként viselkedő partíció, ami más, logikainak nevezett partíciókat tartalmaz. Így vagy 4 elsődleges partíciót használunk, vagy 3 elsődleges és egy kiterjesztett partíciót, ahol az utóbbi több logikai partíciót hordoz.

### Az MBR hátrányai

1.  Csak 4 elsődleges vagy 3 elsődleges + 1 kiterjesztett partíció (melyben meghatározott számú logikai partíció van) definiálható. Ha 3 elsődleges és 1 kiterjesztett partíciónk van, valamint szabad helyünk, mely a kiterjesztett partíción kívül esik, nem hozhatunk létre új partíciót a szabad helyen.
2.  A kiterjesztett partíciókban levő logikaiak metaadatai láncolt lista szerkezetben tárolódnak. Ha egy lánc elveszik, az utána következő összes logikai partíció elveszik.
3.  Az MBR csak 1 bájt nagyságú partíció-típus kódokat támogat, mely sok összeütközéshez vezet.
4.  Az MBR a partíció szektor-információját 32 bites LBA értékeket használva tárolja. Ez az LBA hossz az 512 bájtos szektormérettel együtt (ez a leggyakoribb) a lemezek maximális címezhető méretét 2 [TiB](https://en.wikipedia.org/wiki/TiB "wikipedia:TiB")-ig támogatja. A 2 TiB méreten felüli hely MBR particionálással nem használható.

## GUID Partíciós Tábla

A GUID Partíciós Tábla (GPT) GUID-ket (Linuxban inkább UUID-nak nevezzük őket) használ a partíciók és típusaik definiálására, innen a név. A GPT a következőkből áll:

| Hely a lemezen | Célja |
| A lemez első logikai szektora vagy az első 512 bájt | Protektív MBR - Akár az MBR esetében, de a 64 bájtos tér egyetlen 0xEE típusú a elsődleges partíció bejegyzést tartalmaz, ahol a lemez teljes méretét definiálják, vagy, ha a lemez nagyobb mint 2 [TiB](https://en.wikipedia.org/wiki/TiB "wikipedia:TiB"), 2 TiB méret kerül definiálásra. |
| Második logikai szektor, vagy a következő 512 bájt. | Elsődleges GPT Fejléc (Primary GPT Header) - Ez tartalmazza a lemez egyedi GUID-ját, az elsődleges partíciós tábla helyét, a partíciós tábla lehetséges bejegyzéseinek számát, saját maga és az elsődleges partíciós tábla CRC32 ellenőrzőösszegét, és a Másodlagos (tartalék) GPT Fejléc (Secondary, Backup GPT Header) helyét |
| A második logikai szektort követő 16 KiB (alapértelmezetten) | Elsődleges GPT Tábla - 128 partíciós bejegyzés (alapértelmezetten, de több is lehet), melyek mindegyike 128 bájt méretű (ez adja ki a teljes 16 KiB méretet). A szektorok 64 bites LBA-ként tárolódnak, és minden partíciónak van egy Partíciótípus-azonosító GUID-je és egy Egyedi Partíció GUID-je. |
| A lemez utolsó logikai szektora előtti 16 KiB (alapértelmezetten) | Másodlagos GPT tábla - bájtról bájtra azonos az Elsődleges táblával. Helyreállításra használatos, ha az első tábla megsérül. |
| Utolsó logikai szektor vagy Utolsó 512 bájt | Másodlagos GPT Fejléc - A lemez egyedi GUID-kát tartalmazza, valamint a másodlagos partíciós tábla helyét, a tábla lehetséges bejegyzéseinek számát, önmaga és a másodlagos partíciós tábla CRC32 ellenőrzőösszegét és az Elsődleges GPT Fejléc helyét. Ez a fejléc használható a GPT helyreállítására, ha az elsődleges megsérül. |

### A GPT előnyei

1.  GUID-t (UUID-t) használ a partíciók típusának megállapításához - nincsenek ütközések.
2.  Egyedi lemez GUID-t használ, és partíciónként egyedi partíció GUID-t. - Fájlrendszertől függetlenül tartja számon a partíciókat és lemezeket.
3.  tetszőleges számú partíció, számuk csak a partíciós táblának lefoglalt helytől függ. - Nincs többé szükség kiterjesztett és logikai partíciókra. Alapértelmezett esetben a GPT 128 partíciót képes kezelni, bár ha ennél többet akarunk használni, több helyet is adhatunk a partíciós táblának (ezt jelenleg csak a gdisk eszköz támogatja).
4.  64-bit-es LBA-t használ a tárolásra. - A legnagyobb címezhető lemezméret 2 [ZiB](https://en.wikipedia.org/wiki/ZiB "wikipedia:ZiB").
5.  Tartalék fejlécet és partíciós táblát tárol a lemez végén, mely segít a helyreállításban, ha az elsődleges megsérül.
6.  CRC32 ellenőrzőösszegeket használ a fejlécen és a partíciós táblán a hibák és az adatvesztés megállapítására.

### Kernel támogatás

A `CONFIG_EFI_PARTITION` opció engedélyezi a rendszermag konfigurációjában a kernel GPT támogatását (a félrevezető EFI PARTITION név ellenére). Ennek az opciónak beépítettnek, nem pedig modulként betölthetőnek kell lennie. Még akkor is szükség van rá, ha GPT lemezeket csak tárolásra, nem pedig rendszerindításra használunk. Az opció eleve aktiválva van az Arch [linux](https://www.archlinux.org/packages/?name=linux) és [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) rendszermagjaiban a [core] repóban. Ha valaki saját kernelt használ, a `CONFIG_EFI_PARTITION=y` opcióval aktiválhatja.

## Rendszerbetöltő-támogatás

### UEFI rendszerek

Minden UEFI Rendszerbetöltő támogatja a GPT lemezeket, mivel a GPT része az UEFI specifikációnak, így szükséges az UEFI rendszerindításhoz. Több információért lásd a [Rendszerbetöltők](/index.php/Boot_loaders "Boot loaders") cikket.

### BIOS rendszerek

**Megjegyzés:** Egyes BIOS rendszerek, mint az Intel Desktop Board alaplapok nem indítanak GPT lemezről, kivéve, ha a protektív MBR partíción "Boot" zászlót állítunk be. Az ilyen BIOS rendszereken az [MBR](/index.php/Master_Boot_Record_(Magyar) "Master Boot Record (Magyar)") (avagy msdos particionálás) javasolt GPT helyett, a kompatibilitás megőrzésének érdekében. Lásd a [http://mjg59.dreamwidth.org/8035.html](http://mjg59.dreamwidth.org/8035.html) és [http://rodsbooks.com/gdisk/bios.html](http://rodsbooks.com/gdisk/bios.html) cikket több információért.

*   A [GRUB](/index.php/GRUB "GRUB") a BIOS rendszereken a `core.img` fájl beágyazásához [BIOS Boot Partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")-t igényel, melynek mérete (2 [MiB](https://en.wikipedia.org/wiki/MiB "wikipedia:MiB"), nincs fájlrendszere, típusának kódja pedig `EF02` a gdisk szerint, vagy "bios_grub" zászlóval jelölendő a GNU Parted szerint); mivel az GPT lemezen nincs meg az MBR utáni beágyazó rés. A GPT futásidejű (runtime) támogatását a `part_gpt` modul biztosítja, melynek nincs köze a **BIOS Boot Partition** függőséghez.

*   A [Syslinux](/index.php/Syslinux "Syslinux")-nak szüksége van a `/boot/syslinux/ldlinux.sys`-t tartalmazó partícióra (függetlenül attól, hogy a `/boot` különálló partíción van-e, vagy nem), melyet "Legacy BIOS Bootable" GPT attribútummal kell jelölni (*legacy_boot* zászló a GNU Parted-ben), hogy azonosítani tudja a Syslinux indító állományait tartalmazó partíciót 440 bájtos MBR kódja (`gptmbr.bin`) alapján. Lásd a [Syslinux#GUID Partition Table aka GPT](/index.php/Syslinux#GUID_Partition_Table_aka_GPT "Syslinux") cikket további információkért. Ez az MBR lemezek "boot" zászlójának felel meg.

*   A [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") és a [LILO](/index.php/LILO "LILO") nem támogatja a GPT használatát.

## Partitioning Utilities

### GPT fdisk

A GPT fdisk a a GPT lemezek szerkesztésére szolgáló szöveges alapú eszközkészlet. A gdisk, sgdisk és cgdisk eszközöket tartalmazza, melyek az util-linux (MBR lemezek szerkesztéséhez alkalmazott) fdisk eszközének felelnek meg. Az [extra] tárolóból telepíthető, mint [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

#### Az MBR átalakítása GPT-vé

A gdisk egyik legjobb tulajdonsága (mellyel az sgdisk és a cgdisk is rendelkezik) az, hogy képes MBR és BSD lemezcímkéket GPT-vé alakítani adatvesztés nélkül. A konvertálással minden elsődleges és logikai MBR partíció GPT partícióvá alakul, és mindegyikük megfelelő partíció-típus GUID-t és Egyedi partíció GUID-t kap.

Csak nyissuk meg az MBR lemezt a gdisk-et használva, és lépjünk ki a "w" opcióval, hogy a változásokat a lemezre írjuk (mintha csak az fdisk-et használnánk), s ezzel az MBR lemezt GPT-vé alakítsuk át. **Gondosan figyeljünk bármiféle hibára, s ezeket javítsuk, mielőtt a változásokat a lemezre írnánk**, mert adatot veszíthetünk. Lásd a [http://www.rodsbooks.com/gdisk/mbr2gpt.html](http://www.rodsbooks.com/gdisk/mbr2gpt.html) cikket több információért. Az átalakítás után a rendszerbetöltőket természetesen újra kell telepíteni, és e kell állítani, hogy a GPT lemezről is elinduljanak.

**Megjegyzés:**

*   Emlékezzünk rá, hogy a GTP a másodlagos partíciós táblát a lemez végén tárolja. Ez az adatszerkezet 33 darab 512 bájtos szektort foglal le alapértelmezetten. Az MBR nem rendelkezik ilyesféle adatszerkezettel a lemez végén, ami annyit tesz, hogy az utolsó partíció gyakran a lemez végéig nyújtózik, ezáltal megakadályozva a konverziót. Ebben az esetben vagy el kell felejtenünk az átalakítást, vagy át kell ,méreteznünk az utolsó partíciót, vagy az utolsó partíciót kivéve minden mást át kell alakítanunk.
*   Ne feledjük, hogy ha a Rendszerbetöltőnk a GRUB, annak szüksége lesz egy [BIOS Boot Partícióra](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Ha az MBR Partíciós Sémánk nem túl régi, jó eséllyel a partíciók eltolása miatt az első partíciónk a 2048-as szektornál kezdődik. Ez annyit tesz, hogy van 1007 [KiB](https://en.wikipedia.org/wiki/KiB "wikipedia:KiB") szabad helyünk a lemez elején, ahol a szükséges bios-boot partíciót létrehozhatjuk . Ehhez először végezzük el az mbr->gpt átalakítást a gdisk-kel a fentiek szerint. Ezek után készítsünk új partíciót a gdisk-kel, és manuálisan adjuk meg, hogy pozíciója a 34-es és a 2047-es között legyen, majd állítsuk be a partíció típusát `EF02`-re.

### Util-linux fdisk

Az fdisk segédeszköz, melyet az util-linux szolgáltat (az util-linux libfdisk-én alapulva) részlegesen támogatja a GPT-t, de még mindig béta állapotban van (2013 október 7-én). A kapcsolódó cfdisk és sfdisk eszközök még nem támogatják a GPT-t, általuk sérülhet a GPT fejléc és a partíciós tábla, ha GPT lemezen használjuk.

### GNU Parted

A GNU Parted 3.0 és felette lévő verziói valamint a `parted` parancssori eszköz nem nem támogatják a fájlrendszerekkel kapcsolatos műveleteket, mivel az azokkal kapcsolatban álló kódot eltávolították a libparted-ből, csak annyit meghagyva, amennyire a külső alkalmazásoknak, pl. a GPartednek szüksége van. A kód készítői javasolják a fájlrendszerekkel dolgozó eszközök, vagy a parted valamely grafikus wrapperjének, mint a GParted-nek a használatát (mely magában foglalja az említett külső eszközöket) a fájlrendszereken végzendő műveletekhez.

## Lásd még

1.  A vonatkozó [GPT](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table") és [MBR](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record") Wikipédia oldalakat
2.  [Rod Smith GPT fdisk eszközről szóló honlapja](http://rodsbooks.com/gdisk/) és [Sourceforge.net Projekt lapja - gptfdisk](http://sourceforge.net/projects/gptfdisk/)
3.  Rod Smith oldala [az MBR-ről GPT-re történő konverzióról](http://rodsbooks.com/gdisk/mbr2gpt.html) és a [Rendszerindítás GPT-ről](http://rodsbooks.com/gdisk/booting.html)
4.  Rod Smith oldala [Az Új Partíció-típus GUID-ről](http://www.rodsbooks.com/linux-fs-code/index.html) Linux adat partíciók számára
5.  [A System Rescue CD oldala a GPT-ről](http://sysresccd.org/Sysresccd-Partitioning-The-new-GPT-disk-layout)
6.  A Wikipédia a [BIOS Boot Partícióról](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
7.  [Nagyméretű lemezek GPT-vel és Linux-szal - IBM Developer Works](http://www.ibm.com/developerworks/linux/library/l-gpt/index.html?ca=dgr-lnxw07GPT-Storagedth-lx&S_TACT=105AGY83&S_CMP=grlnxw07)
8.  [A Microsoft Windows és a GPT FAQ](http://www.microsoft.com/whdc/device/storage/GPT_FAQ.mspx)