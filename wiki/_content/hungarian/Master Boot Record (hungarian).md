Related articles

*   [Arch boot process](/index.php/Arch_boot_process "Arch boot process")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Partitioning](/index.php/Partitioning "Partitioning")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")

A Master Boot Record (MBR) egy tárolóeszköz első 512 bájtja. Az MBR nem valamiféle partíció, hanem a rendszerbetöltő és a partíciós tábla számára fenntartott hely. Az MBR újabb alternatívája a [GUID Partíciós Tábla](/index.php/GUID_Partition_Table_(Magyar) "GUID Partition Table (Magyar)"), mely része a [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") specifikációnak.

## Contents

*   [1 Rendszerindítás (Boot)](#Rendszerind.C3.ADt.C3.A1s_.28Boot.29)
*   [2 Történet](#T.C3.B6rt.C3.A9net)
*   [3 Mentés és helyreállítás](#Ment.C3.A9s_.C3.A9s_helyre.C3.A1ll.C3.ADt.C3.A1s)
*   [4 A Windows boot record helyreállítása](#A_Windows_boot_record_helyre.C3.A1ll.C3.ADt.C3.A1sa)
*   [5 TestDisk MBR Kód](#TestDisk_MBR_K.C3.B3d)
*   [6 Lásd még](#L.C3.A1sd_m.C3.A9g)

## Rendszerindítás (Boot)

A bootolás több szakaszból áll. A legtöbb PC a hardver alkotóelemeit a [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS")-nak (Basic Input/Output System) nevezett firmware segítségével inicializálja, mely rendszerint az alaplap erre külön kijelölt ROM chipjében foglal helyet. Miután a hardverelemek inicializálásra kerültek, a BIOS az az első felismert tárolóegységen (merevlemez, SSD, CD/DVD, USB eszköz) MBR-én megkeresi a rendszerbetöltőt, vagy ezen eszköz első partícióján. Ezt a programot aztán végrehajtja. A rendszerbetöltő beolvassa a partíciós táblát, majd betölti a megfelelő partícióról az operációs rendszert. A leggyakoribb GNU/Linux rendszerbetöltők manapság a [GRUB](/index.php/GRUB "GRUB") és a [Syslinux](/index.php/Syslinux "Syslinux").

## Történet

Az MBR egy rövidke assembly kódból (az eredeti rendszerbetöltő – 446 bájt), a 4 elsődleges partíció táblájából (darabja 16 bájt) és *sentinel*-ből (0xAA55) áll.

A "Hagyományos" Windows/DOS MBR rendszerbetöltő kód csak egyetlen *aktív* partíciót keres, beolvas X szektort erről a partícióról, majd átadja az ellenőrzést az operációs rendszernek. A Windows/DOS betöltő *nem tud* Arch Linux partícióról indítani, mert nem arra készült, hogy betölthesse a Linux rendszermagot, valamint csak és kizárólag *aktív*, *elsődleges* partíciót kezel csak (ezt a GRUB biztonságosan megkerüli).

A [GRand Unified Bootloader (GRUB)](/index.php/GRUB "GRUB") afféle norma a GNU/Linux rendszerbetöltők közt, és erősen ajánlott, hogy telepítsük az MBR-re, hogy bármiféle partícióról indíthassunk, legyen az elsődleges vagy logikai.

## Mentés és helyreállítás

Mivel az MBR a merevlemezen van, elmenthető és visszaállítható.

Az MBR elmentése:

```
# dd if=/dev/sda of=/path/mbr-backup bs=512 count=1

```

Az MBR helyreállítása:

```
# dd if=/path/mbr-backup of=/dev/sda bs=512 count=1

```

**Figyelem:** Az MBR helyreállítása, ha a partíciós táblánk megváltozott, olvashatatlanná és majdnem biztosan helyreállíthatatlanná teszi adatainkat. Ha csak a rendszerbetöltőt kell újratelepítenünk, használjuk a [GRUB](/index.php/GRUB "GRUB")-ot vagy a [Syslinux](/index.php/Syslinux "Syslinux")-ot.

Ahhoz, hogy töröljük az MBR-t (hasznos lehet más operációs rendszer teljes újratelepítésekor), csak az első 446 bájtot kell "nulláznunk", hiszen a maradék a partíciós táblát tartalmazza:

```
# dd if=/dev/zero of=/dev/sda bs=446 count=1

```

## A Windows boot record helyreállítása

Hagyományosan (és a telepítés megkönnyítése végett), a Windows általában az első partícióra kerül, és partíciós tábláját, rendszerbetöltőjének referenciáját e partíció első szektorán helyezi el. Ha véletlenül rendszerbetöltőt (pl. GRUB-ot) telepítünk e Windows partícióra, vagy a boot bejegyzést valamilyen más módon sérülés éri, azt valamilyen eszközzel kell helyreállítani. A Microsoft egy `FIXBOOT` nevű boot szektor javító eszközt és egy `FIXMBR` nevű MBR javítót is kiadott helyreállító-lemezein, és olykor telepítőin. E módszert használva javítható a rendszerbetöltő fájl referenciája az első partíció boot szektorán, és megjavítható az MBR referenciája az első partíción. Ezután a [GRUB újratelepítése](/index.php/GRUB#Bootloader_installation "GRUB") következik, az MBR-en (a GRUB rendszerbetöltő használható a Windows rendszerbetöltőjének betöltésére is, ezt hívjuk "chainload"-nak).

Ha a rendszert csak Windows alatt szeretnénk használni a továbbiakban, a `FIXBOOT` parancsot használjuk, mely az MBR-ről az első partíció boot szektorára ugrik, hogy helyreállítsa a Windows operációs rendszer normális, automatikus betöltését.

Jegyezzük meg, létezik egy Linux eszköz, melynek neve `ms-sys` ([ms-sys](https://aur.archlinux.org/packages/ms-sys/) csomag az AUR-ban) mely képes MBR-t telepíteni. Mindazonáltal ez a segédeszköz jelenleg csak új MBR-t tud írni (minden OS-t és fájlrendszert támogat) valamint boot szektort (avagy indítórekordot; ez a FAT fájlrendszerek `FIXBOOT`)-jának megfelelője. A legtöbb LiveCD-n nem található meg ez az eszköz, azaz használat előtt telepíteni kell, vagy olyan helyreállító-rendszert érdemes keresni, ami tartalmazza, mint a [Parted Magic](http://partedmagic.com/).

Először írjuk újra a partíciókról szóló információt (táblát):

```
# ms-sys --partition /dev/sda1

```

Majd írjuk ki a Windows 2000/XP/2003 MBR-t:

```
# ms-sys --mbr /dev/sda  # Lásd az opciókat a különféle verziókkal kapcsolatban

```

Ezután írjunk új boot szektort (indítórekordot):

```
# ms-sys -(1-6)          # Lásd az opciókat a megfelelő FAT rekord típussal kapcsolatban

```

`ms-sys` tud még Windows 98, ME, Vista és 7 MBR-t írni is, lásd `ms-sys -h`.

## TestDisk MBR Kód

A [hivatalos tárolók](/index.php/Official_repositories "Official repositories")-ból telepíthető A [testdisk](https://www.archlinux.org/packages/?name=testdisk) program képes saját [kódját](http://www.cgsecurity.org/wiki/Menu_MBRCode) az MBR-re írni, mely ezek után képes a Windowst indítani. A csomag a telepítőmédiumon is megtalálható.

## Lásd még

*   [What is a Master Boot Record (MBR)?](http://kb.iu.edu/data/aijw.html)