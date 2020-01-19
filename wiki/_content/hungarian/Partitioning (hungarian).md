Related articles

*   [fstab](/index.php/Fstab "Fstab")
*   [LVM](/index.php/LVM "LVM")
*   [Swap](/index.php/Swap "Swap")
*   [File Systems_(Magyar)](/index.php/File_Systems_(Magyar) "File Systems (Magyar)")

Egy merevlemez *particionálása* lehetővé teszi a felhasználható hely logikai szakaszokra történő felosztását, melyek ezáltal egymástól függetlenül is kezelhetők lesznek.

Egy merevlemez egyetlen partícióvá is alakítható, vagy a felhasználható tárhely akár több partícióra is osztható. Bizonyos helyzetek megkövetelik több partíció létrehozását: a kettős-, vagy multiboot, vagy épp a [cserehely](/index.php/Swap_(Magyar) "Swap (Magyar)") partíció használata. Más esetekben a particionálás egyszerűen csak az adatok logikai "elszigetelésének" eszköze, mint például amikor különböző partíciókat készítünk hang-, és videó állományainknak. Alább részletesen beszélünk majd a leggyakoribb partíciós sémákról.

Minden partíciót valamilyen típusú [fájlrendszerre](/index.php/File_systems_(Magyar) "File systems (Magyar)") kell formázni, mielőtt használni lehet.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Partíciós tábla](#Partíciós_tábla)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
    *   [1.2 GUID Partíciós Tábla](#GUID_Partíciós_Tábla)
    *   [1.3 Btrfs Particionálás](#Btrfs_Particionálás)
    *   [1.4 Válasszunk GPT és MBR közül](#Válasszunk_GPT_és_MBR_közül)
*   [2 Partíciós séma](#Partíciós_séma)
    *   [2.1 Egy root partíció](#Egy_root_partíció)
    *   [2.2 Különálló partíciók](#Különálló_partíciók)
    *   [2.3 Csatolási pontok](#Csatolási_pontok)
        *   [2.3.1 Root partíció](#Root_partíció)
        *   [2.3.2 /boot](#/boot)
        *   [2.3.3 /home](#/home)
        *   [2.3.4 /var](#/var)
        *   [2.3.5 /tmp](#/tmp)
        *   [2.3.6 Cserehely (Swap)](#Cserehely_(Swap))
        *   [2.3.7 Milyen méretűek legyenek a partíciók?](#Milyen_méretűek_legyenek_a_partíciók?)
*   [3 Particionáló eszközök](#Particionáló_eszközök)
*   [4 SSD paríció eltolása](#SSD_paríció_eltolása)
*   [5 GPT használata- a modernebb módszer](#GPT_használata-_a_modernebb_módszer)
    *   [5.1 A gdisk használatának összefoglalása](#A_gdisk_használatának_összefoglalása)
*   [6 MBR használata - régi módszer](#MBR_használata_-_régi_módszer)
    *   [6.1 Az fdisk használatának összefoglalója](#Az_fdisk_használatának_összefoglalója)
*   [7 Lásd még](#Lásd_még)

## Partíciós tábla

A partíciókról minden információ a partíciós táblában tárolódik; ezeknek két manapság leginkább használatos fő formájuk van: a klasszikus [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (vagy MBR) és a modern [GUID Partíciós tábla](/index.php/GUID_Partition_Table "GUID Partition Table"). Utóbbi fejlettebbnek számít, mert "túlnő" az MBR számos korlátján.

### Master Boot Record

[Wikipedia:Master boot record](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record")

Az MBR eredetileg legfeljebb 4 partíció létrehozását támogatta. Később - e limitációt megkerülendő - bevezették a kiterjesztett és logikai partíciók használatát.

3 partíciótípus létezik:

*   Elsődleges
*   Kiterjesztett
    *   Logikai

Az **elsődleges** partíciók indíthatók, és lemezenként vagy RAID tömbönként legfeljebb 4 lehet belőlük. Ha a particionálási séma négynél több partíciót igényelne, **kiterjesztett** partíciót használunk, mely **logikai** partíciókat tartalmaz. A kiterjesztett partíciókra egyfajta, a logikai partíciók számára létrehozott tárolóként kell gondolni. Egy merevlemez legfeljebb egy ilyen kiterjesztett partíciót tartalmazhat. EZ a kiterjesztett partíció a maximális partíciószám szempontjából elsődleges partíciónak számít, így, ha a merevlemezen már van egy kiterjesztett partíció, legfeljebb három elsődleges hozható még létre mellette (tehát három elsődleges és egy kiterjesztett partíciót kaphatunk). Azonban a kiterjesztett partícióban helyet foglaló logikai partíciók számának nincs határa. Az olyan rendszereken, melyeknek Windows-szal közös kettős boot-ot használnak, a Windowst elsődleges partícióra kell telepítenünk.

A hagyományos számozási séma szerint elsődleges partícióink *sda1*-től *sda3*-ig tartanak, majd a kiterjeszett *sda4* partíció következik. Az *sda4*-ben foglat logikai partíciók számozása *sda5*, *sda6*, stb. lesz.

### GUID Partíciós Tábla

[Wikipedia:GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table")

Csak egyetlen partíciótípus létezik, az **elsődleges**. A lemezenkénti vagy RAID tömbönkénti partíciók száma nem korlátozott.

### Btrfs Particionálás

[Wikipedia:Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs")

A Btrfs a teljes adattárolót képes használni és felváltani az [MBR](/index.php/MBR "MBR") vagy [GPT](/index.php/GPT "GPT") particionálási sémákat. Lásd a [Btrfs particionálás](/index.php/Btrfs#Partitioning "Btrfs") szócikket további részletekért.

### Válasszunk GPT és MBR közül

A [GUID Partíciós tábla](/index.php/GUID_Partition_Table "GUID Partition Table") (GPT) egy alternatív, modern particiónálási típus. A régi [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") (MBR) rendszer felváltására készült. A GPT-nek számos előnye van az MBR-rel szemben, melynek az MS-DOS-os időkből datálódó sallangjai vannak. Az *fdisk* (MBR) és *gdisk* (GPT) formázóeszközök legutóbbi fejlesztéseinek hála, egyenlőképp könnyűvé vált a GPT or MBR használata, s emellett a maximális teljesítmény elérése.

Nos, a választásnak az alábbiak alapján illene eldőlnie:

*   Ha a GRUB legacy rendszerbetöltőt használjuk, MBR-t kell használnunk.
*   A Windows-szal közös kettős boot (32 vagy 64 bit), ha régi típusú BIOS-t használunk, MBR-t kell használnunk.
*   64 bites Windowssal közös kettős boot és BIOS helyett [UEFI](/index.php/UEFI "UEFI") használatakor GPT-t használunk.
*   Ha a fentiek egyike sem illik esetünkre, szabadon választhatunk GPT és MBR közt. Mivel a GPT modernebb, ez a javasolt.
*   Tanácsos mindig GPT-t használnunk [UEFI](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") boot esetén, mivel egyes UEFI firmware-k nem engedélyezik az UEFI-MBR indítást.

## Partíciós séma

Nincsenek szigorú szabályok arra nézve, hogy hogyan particionáljunk, de az alábbi tanácsokat érdemes fontolóra venni. Egy lemez logikai felosztása olyan tényezőktől függ, mint a megfelelő rugalmasság, sebesség, biztonság, vagy épp a szabad tárolókapacitás határa. Elsősorban azonban személyes ízlés kérdése. Ha kettős boot-ot akarsz használni Arch Linux-szal és Windows-szal, kérjük, olvasd át a [Windows and Arch Dual Boot](/index.php/Windows_and_Arch_Dual_Boot "Windows and Arch Dual Boot") cikket.

**Figyelem:** Ne felejts helyet hagyni a rendszerbetöltőnek. Ez nem merült fel az MBR és a GRUB-Legacy használatakor, de a moldernebb partíciós sémák számára már szükséges egy speciális, apró partíció.

### Egy root partíció

Ez a séma a legegyszerűbb és a legtöbb esetben elegendő is. Egy [cserefájl](/index.php/Swapfile "Swapfile") is létrehozható és könnyen át is méretezető. Legtöbbször a különálló `/` partícióból szokás elindulni, majd másokat a felhasználásuk módja alapján leválasztani róla, úgymint RAID, titkosítás, megosztott média partíciók, stb. Ne feledjuk, ha GRUB-ot telepítünk GPT-vel felosztott BIOS rendszerre, szükségünk lesz egy további BIOS partícióra.

### Különálló partíciók

Egy útvonal partícióként történő elhatárolása lehetővé teszi a különböző fájlrendszerek és csatolási opciók használatát. Egyes esetekben, mint például egy média partíciónál, így megoszthatóvá válhatnak operációs rendszerek között.

### Csatolási pontok

A következő csatolási pontok választhatók különálló partíciók használatakor, szükségeid szerint dönthetsz.

#### Root partíció

A root könyvtár a hierarchia csúcsán áll, ez az a pont, ahova az elsődleges fájlrendszert csatoljuk, s ahova az összes többi fájlrendszer fog kapcsolódni. Minden állomány és könyvtár a root `/` könyvtár alatt jelenik meg, még akkor is, ha fizikailag nem ugyanazon a tárolóeszközön találhatók. A root fájlrendszer tartalmának megfelelőnek kell lennie, hogy a rendszer indítható, helyreállítható, és/vagy javítható legyen. Ezért bizonyos könyvtárak a `/` alatt nem helyezhetők át más partíciókra.

A `/` partíció vagy root partíció is szükséges és mind közül a legfontosabb. Minden más partíciót helyettesíthet.

**Figyelem:** Az indításhoz szükséges könyvtáraknak (kivéve `/boot`) ugyanazon a partíción **kell** lenniük, mint a `/`, vagy korai userspace-ben kell felcsatolni őket az [initramfs](/index.php/Initramfs "Initramfs") által. Ezek a következők könyvtárak: `/etc` és `/usr` [[1]](http://freedesktop.org/wiki/Software/systemd/separate-usr-is-broken).

#### /boot

A `/boot` könyvtárban helyezkedik el a kernel és a ramdisk image-k, éppúgy, mint a rendszerbetöltő konfigurációja és különböző szakaszai. Olyan adatokat is tárol, melyek a kernel által indított user-space programok előtt használhatók. A külön `/boot` partíció nem feltétlenül szükséges a rendszer normális működéséhez, csak a rendszer indításakor és a rendszermag frissítésekor (amikor a kezdeti ramdisk-et hozzuk létre).

Külön `/boot` partíció szükséges, ha szoftveres RAID0 (összefűzés) rendszert telepítünk.

#### /home

A `/home` könyvtár tartalmazza az egyes felhasználók egyéni beállításait, gyorsítótárait, programadatait és médiáját.

A külön `/home` partíció létrehozása lehetővé teszi a `/` tőle független újraparticionálását, de jegyezzük meg, hogy az Arch újratelepíthető akkor is, ha a `/home` érintetlen, még ha nincs is külön partíción - a többi vele egyenrangú könyvtárat kell csak eltávolítani, majd a pacstrap-et futtatni.

Nem szabad megosztani a home könyvtárakat különböző disztribúciók használói között, mivel jó eséllyel nem kompatibilis szoftver-verziókat és javításokat használnak. Ehelyett jobb megoldás lehet egy közös média partíció létrehozása vagy legalábbis külön home könyvtárak használata ugyanazon a `/home` partíción.

#### /var

A `/var` könyvtár olyan gyakran változó adatokat tárol, mint a puffer könyvtárak és állományok, adminisztratív és naplózott adatok a [pacman](/index.php/Pacman "Pacman") gyorsítótár, az [ABS](/index.php/ABS "ABS") fa, stb. Gyorsítótárazásra és naplózásra használatos, épp ezért nagyon gyakran olvassuk vagy írjuk tartalmát. Ha külön partíción tároljuk, nem a teljes rendszerünk tárolókapacitása telik fel túlontúl bőbeszédű naplók és hasonlók miatt.

Azért létezik, hogy a `/usr` útvonalat csak olvashatóként is csatolhassuk. Mindennek, ami régebben a `/usr`-be került és írhatónak kell lennie a rendszer működéséhez, (a telepítéssel és a szoftverkezeléssel ellentétben) a `/var` alatt kell helyet foglalnia.

**Megjegyzés:** A `/var` rengeteg kisméretű állományt tartalmaz. A megfelelő fájlrendszer-típus kiválasztásakor ezt vegyük figyelembe, ha külön partícióra költöztetjük.

#### /tmp

Ez egy eleve különálló partíció, hiszen a systemd *tmpfs*-ként fűzi be.

#### Cserehely (Swap)

A [cserehely (swap)](/index.php/Swap "Swap") partíció virtuális RAM-ként használható memóriát szolgáltat. A [cserefájl](/index.php/Swap#Swap_file "Swap") használata is megfontolandó lehet, mivel szinte semmiben nem más a teljesítménye, de szükség esetén sokkal könnyebben átméretezhető. A cserehely partítió *elvben* megosztható operációs rendszereink között, de semmiképpen sem, ha hibernációra használjuk.

#### Milyen méretűek legyenek a partíciók?

**Megjegyzés:** Az alábbiak egyszerű irányvonalak; nincs aranyszabály a partíciók méretére vonatkozólag.

A partíciók mérete egyéni ízlésünk és szükségleteink szerint alakul, de a következő információk hasznosak lehetnek:

	/boot - 200 MB 

	Mindössze 100 MB-ra van szüksége, de ha több rendszermagot is használnánk, 200 vagy 300 MB jobb döntés lehet.

	/ - 15-20 GB 

	Hagyományosan tartalmazza a `/usr` könyvtárt, melynek mérete jelentősen megnövekedhet a telepített szoftver mennyiségének függvényében. 15-20 GB elegendő lehet a legtöbb modern merevlemezzel rendelkező asztali rendszer számára.

	/var - 8-12 GB 

	Más adatok mellet az [ABS](/index.php/ABS "ABS") fát és a [pacman](/index.php/Pacman "Pacman") gyorsítótárat tartalmazza. A gyorsítótárazott csomagok megtartása hasznos és rugalmas megoldás lehet, hiszen képessé válunk korábbi szoftververziókhoz való visszatérésre. Ennek eredményeképp a `/var` mérete ugrásszerűen megnövekedhet. A pacman gyorsítótár egyre csak hízik, ahogy a rendszert bővítjük és frissítjük. Mindazonáltal biztonságosan tisztítható, ha helyszűkébe kerülnénk. 8-12 GB-nak elegendőnek kell lennie egy asztali rendszeren a `/var` számára, attól függően, hogy mennyi szoftvert telepítünk.

	/home - [változó] 

	Rendszerint ezen a helyen tároljuk a felhasználók állományait, a letöltéseket, a multimédiás fájlokat. Egy asztali rendszeren a `/home` tipikusan a legnagyobb méretű fájlrendszer.

	swap (cserehely) - [változó] 

	Régebben az a szokás uralkodott, hogy mérete a rendelkezésre álló fizikai RAM kétszerese legyen. Ahogy a számítógépek egyre több RAM befogadására váltak képessé, ez a szabály egyre elhanyagolhatóbbá vált. Ha legfeljebb 512MB RAM-mal rendelkezünk, a kétszeres szabályt még érdemes betartanunk. Ha elegendő (több mint 1024MB) a RAM-unk, kisebb, vagy akár semmiféle cserehely használata is lehetséges. Ha már több mint 2GB fizikai RAM-unk van, jó teljesítményre számíthatunk akár cserehely nélkül is.

**Megjegyzés:** Ha azt tervezzük, hogy cserehelyre, vagy -fájlra hibernálunk, olvassuk át a [Felfüggesztés és Hibernálás#A cserehely/cserefájl méretéről](/index.php/Suspend_and_hibernate#About_swap_partition/file_size "Suspend and hibernate") cikket.

	/data - [változó] 

	Megfontolásra kerülhet egy "data" partíció befűzése, melyeken több felhasználó számára megosztott állományokat helyezünk el. Ugyancsak megfelelő, ha a `/home` partíciót használjuk erre a célra.

**Megjegyzés:** Ha szükséges, 25% extra (szabad) hely a partícióinkon lehetővé teszi, hogy később könnyedén bővítsük őket, illetve védelmet nyújt a töredezettségtől.

## Particionáló eszközök

*   **fdisk** — A Linux-ban foglalt particionáló, terminálban.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **cfdisk** — Ncurses alapú particionáló, terminálban.

	[https://www.kernel.org/](https://www.kernel.org/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

**Figyelem:** A *cfdisk* által létrehozott első partíció a 63-ik szektornál kezdődik, a megszokott 2048-ik helyett. Ez csökkent teljesítményhez vezethet fejlettebb (4k szektoros formátumú) SSD meghajtók esetében. Problémákhoz vezethet a [GRUB2](/index.php/GRUB2#msdos-style_error_message "GRUB2") használatakor. A legacy GRUB és a Syslinux azonban így is működőképes.

*   **gdisk** — Az fdisk [GPT](/index.php/GPT "GPT") változata.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **cgdisk** — A cfdisk GPT változata.

	[http://www.rodsbooks.com/gdisk/](http://www.rodsbooks.com/gdisk/) || [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk)

*   **GNU Parted** — Particionáló terminálban.

	[http://www.gnu.org/software/parted/parted.html](http://www.gnu.org/software/parted/parted.html) || [parted](https://www.archlinux.org/packages/?name=parted)

*   **[GParted](/index.php/GParted "GParted")** — GTK-ban írt grafikus particionáló.

	[http://gparted.sourceforge.net/](http://gparted.sourceforge.net/) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **Partitionmanager** — QT-ban írt grafikus particionáló.

	[http://sourceforge.net/projects/partitionman/](http://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)

*   **QtParted** — Hasonló a Partitionmanager-hez, az [AUR](/index.php/AUR "AUR")-ból telepíthető.

	[http://qtparted.sourceforge.net/](http://qtparted.sourceforge.net/) || [qtparted](https://aur.archlinux.org/packages/qtparted/)

## SSD paríció eltolása

**A megfelelő partíció eltolás szükséges az optimális teljesítmény eléréséhez és a hosszú élettartam megőrzéséhez.** Az eltolás kulcsa a legalább az SSD EBS (erase block size, törlési blokkméret) értékéhez igazított particionálás.

**Megjegyzés:** Az EBS nagyban a gyártótól függ.

Ha a partíciók nincsenek úgy eltolva, hogy az EBS többszöröseinél (pl. 512 KiB-nál) kezdődjenek, a fájlrendszer eltolása teljesen felesleges, mert minden a partíció eltolásának "résével" megegyező módon tolódik rossz helyre. Hagyományosan a merevlemezeket a *cilinder*, *fej* és *szektor* szerint címezték, melyeken aztán az adat olvasásra vagy írásra került. Ezek a sugárirányú helyzetet jelölték, a meghajtó fejének ( = lemez és oldal ), valamint az adatnak az axiális helyzetét. Az LBA (logical block addressing, logika blokk címzés) bevezetésével mindez már nem szükséges. Ehelyett az egész merevlemez egyetlen adatfolyamként címezhető.

## GPT használata- a modernebb módszer

### A gdisk használatának összefoglalása

Ha GPT-t használunk, a megfelelő partíció-szerkesztő eszközünk a *gdisk* lesz. Ez az eszköz képes a partíciók automatikus, 2048 szektormérethez igazított eltolására (ez 1024 KiB-ot jelent), aminek kompatibilisnek kell lennie az SSD-k túlnyomó többségével, ha nem minddel. A GNU parted program is támogatja a GPT-t, de [kevésbé felhasználóbarát](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813), ha partíciók eltolására kerül sor. Az Arch ISO telepítőkörnyezete magában foglalja a *gdisk* parancsot. Ha a későbbiekben a telepített rendszeren is szükség van rá, a *gdisk* a [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk) csomagból elérhető.

Összefoglaló a *gdisk* általános felhasználásáról:

*   A *gdisk*-et indítsuk egy bizonyos lemezen mint root felhasználó (a *merevlemez* lehet pl. `/dev/sda`):

```
# gdisk *merevlemez*

```

*   Ha a lemez vadonatúj, vagy épp mindent újra akarunk rajta kezdeni, nyissunk új GUID partíciós táblát az `o` paranccsal.
*   Hozzunk létre új partíciót az `n` paranccsal (elsődleges típusú/első partíció).
*   Feltételezve, hogy a partíció új, *gdisk* a lehető legmagasabb eltolást fogja használni. Más esetben a kettő hatványa, ahol a kitevő a partíciók réseinek legnagyobb közös osztója.
*   Ha egy partíciónak a 2048-ik szektor előtti kezdetet adunk meg, a *gdisk* automatikusan 2048-ra váltja ezt az értéket. Ezzel biztossá válik a 2048 szektoros eltolás (mivel egy szektor 512B, ez 1024KiB-os eltolás, mely minden SSD NAND törlési blokkhoz illeszkedni fog).
*   Ezután a `+*x*{M,G}` formátumban adjuk meg, hogy a partíció *x* mebibyte vagy gibibyte méretig terjeszkedjen; valamint, ha ez a méret nem az eltolási méret (1024 KiB) többszöröse lenne, a *gdisk* összehúzza a partíciót a legkisebb többszörösig. Ha tehát 15 Gib-os partíciót akarunk létrehozni, `+15G`-t kell beütnünk.
*   A következő lépés a partíció típusának megjelölése, az alapértelmezett a `Linux filesystem` azaz a Linux fájlrendszer (a kódja `8300`), megfelelő a legtöbb esetben. A kódok listája az `L` billentyűvel hívható elő. Ha LVM-et akarnánk használni, válasszuk ki a `Linux LVM`-et (`8e00`).
*   Ugyanilyen módon folytassuk a többi partícióval.
*   Ha végeztünk, a tábát a `w` paranccsal írjuk a lemezre és kilépünk.
*   Formázzuk le a partíciókat valamely [fájlrendszerre](/index.php/File_systems "File systems").

**Megjegyzés:**

*   A GPT partíciós táblát használó lemezről történő rendszerindításhoz létre kell hozni (lehetőleg a lemez elején) egy [BIOS boot partíciót](/index.php/GRUB2#GUID_Partition_Table_(GPT)_specific_instructions "GRUB2"), melyen nincs fájlrendszer, s melynek partíció típusa `BIOS boot` vagy `bios_grub` (*gdisk* a kódja `EF02`) ha a lemez [GRUB](/index.php/GRUB "GRUB")-ot használva indul. A [Syslinux](/index.php/Syslinux "Syslinux")-hoz nincs szükség ennek a `bios_grub` partíciónak létrehozására, de szükség lesz különálló `/boot` partícióra és engedélyezzük a `Legacy BIOS Bootable partition` attrbútumot ezen a partíción a (a *gdisk* használatával).
*   A [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") nem támogatja a GPT-t, a felhsználóknak a [BURG](/index.php/BURG "BURG"), a GRUB vagy a Syslinux közül kell választania.

**Figyelem:** Ha kettős bootolást tervezünk Windows-szal BIOS módban (ez az egyetlen lehetőség 32 bites Windows verziókkal, illetve 64 bites Windows XP-vel), **semmiképp se** használjunk GPT-t mivel a Windows **nem** támogatja a GPT lemezről való indítást BIOS rendszeren. Ilyenkor kénytelenek vagyunk MBR particionálást használni és BIOS módban indítani a rendszert, az alábbi leírás szerint. Ez a korlátozás nem érvényes a modernebb 64 bites Windows rendszerek UEFI módú indítására.

## MBR használata - régi módszer

Ha MBR-t használunk, a használandó particionáló eszköz az *fdisk* lesz. Az *fdisk* újabb verziói már elvetették az elavult cilinderekben történő számítást és kijelzést, akárcsak az MS-DOS kompatibilitást. A legutóbbi *fdisk* automatikusan tolja el az összes partíciót 2048 szektorral, avagy 1024 Kib-tal, amely az összes mai SSD gyártó által használt EBS méretnél megfelelő. Ez annyit tesz, hogy az alapértelmezett beállításokkal megfelelő lesz a partíciók eltolása.

Jegyezzük meg, hogy régebben az *fdisk* cilinderekben számolt, és olyan MS-DOS kompatibilitási módot tartalmazott, ami teljesen felborította az SSD eltolást. Épp ezért az interneten még mindig számos olyan, 2008-2009 környéki anyag található, melyek mélyre menően taglalják, hogy mi a particionálás megfelelő menete. A legutóbbi *fdisk*-kel jóval egyszerűbb a dolgunk, miként ez ebből az útmutatóból is kiderül.

### Az fdisk használatának összefoglalója

*   Indítsuk root-ként az *fdisk*-et valamely eszközünkön (a *merevlemez* lehet például `/dev/sda`):

```
# fdisk *merevlemez*

```

*   Ha a lemez vadonatúj, vagy mindent újra akarunk kezdeni rajta, készítsünk egy új és üres DOS partíciós táblát az `o` paranccsal.
*   Az `n` paranccsal készítsünk egy új partíciót (elsődleges típusú/első partíció).
*   Használjuk a `+*x*G` formátumú parancsot, hogy a partíciót *x* gibibájtig terjesszük ki. Ha tehát 15GiB méretű partíciót szeretnénk, a parancs `+15G` lesz.
*   Változtassuk a partíció azonosítóját az alapértelmezett Linux-ról (`a kódja 83`) valami másra, ha szükséges, a `t` paranccsal. Ez nem kötelező, csak akkor szükséges, ha valami más partíciótípust akarunk létrehozni, mint például a cserehely, az NTFS vagy az LVM. A partíciótípusok listáját a `l` paranccsal bármikor lekérdezhetjük.
*   Ugyanilyen módon folytassuk a többi partícióval.
*   A `w` paranccsal írjuk a lemezre a partíciós táblát.
*   Formázzuk új partícióinkat valamilyen [fájrendszerre](/index.php/File_systems "File systems").

## Lásd még

*   [Creating ext4 partitions from scratch](/index.php/Ext4#Creating_ext4_partitions_from_scratch "Ext4")
*   [Wikipedia:Disk partitioning](https://en.wikipedia.org/wiki/Disk_partitioning "wikipedia:Disk partitioning")
*   [Manually Partitioning Your Hard Drive with fdisk](http://www.novell.com/coolsolutions/feature/19350.html)