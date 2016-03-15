A [Wikipédiából](https://en.wikipedia.org/wiki/File_system "wikipedia:File system"):

	*A számítástechnika egy fájlrendszer alatt a számítógépes fájlok tárolásának és rendszerezésének a módszerét érti, ideértve a tárolt adatokhoz való hozzáférést és az adatok egyszerű megtalálását is...Precízebben meghatározva: egy fájlrendszer absztrakt adattípusok halmaza, amelyeket adatok tárolására, hierarchikus rendezésére, kezelésére, megtalálására illetve navigálásra, hozzáférésre, és visszakeresésére valósítottak meg.*

Különálló partícióink mindegyikén a sok különböző fájlrendszer valamelyikét használhatjuk. Mindegyiknek megvan a maga előnyi, hátrányai és egyedülálló bogarasságai. Itt egy gyors áttekintést közlünk a támogatott fájlrendszerekről; a Wikipédia oldalaira mutató linkek sokkal több információval kecsegtethetnek.

Mielőtt formázunk, az adathordozónkat [particionálnunk](/index.php/Partitioning_(Magyar) "Partitioning (Magyar)") kell.

## Contents

*   [1 A fájlrendszerek típusai](#A_f.C3.A1jlrendszerek_t.C3.ADpusai)
    *   [1.1 Naplózás](#Napl.C3.B3z.C3.A1s)
    *   [1.2 Arch Linux támogatás](#Arch_Linux_t.C3.A1mogat.C3.A1s)
*   [2 Eszközök formázása](#Eszk.C3.B6z.C3.B6k_form.C3.A1z.C3.A1sa)
    *   [2.1 Feltételek](#Felt.C3.A9telek)
    *   [2.2 Eszközök konzolban](#Eszk.C3.B6z.C3.B6k_konzolban)
    *   [2.3 Grafikus eszközök](#Grafikus_eszk.C3.B6z.C3.B6k)

## A fájlrendszerek típusai

*   [Btrfs](https://en.wikipedia.org/wiki/Btrfs "wikipedia:Btrfs") - A "Better FS" (jobb fájlrendszer) néven is ismert, egy **új fájlrendszer mely olyan hatékony képességekkel bír, mint a Sun/Oracle kitűnő ZFS-e**. Ezek közt említendők a pillanatképek, a több lemez összefűzése vagy tükrözése (tehát szoftveres RAID mdadm nélkül), az ellenőrzőösszegek használata, a különbözeti mentés, az azonnali tömörítés mely nagy teljesítménynövekedéshez vezethet, s mellékesen helyet spórol. 2011 januárjában a Btrfs még nem számított stabilnak, bár kísérleti státusszal a mainline rendszermagba került. A Btrfs a GNU/Linux fájlrendszerek lehetséges jövőjét képviseli, s a nagyobb disztribúciók telepítőin root fájlrendszerként használható.
*   [exFAT](https://en.wikipedia.org/wiki/exFAT "wikipedia:exFAT") - **Flash meghajtókra optimalizált Microsoft fájlrendszer**. Az NTFS-től eltérően az exFAT nem képes nem képes előre allokálni a tárolóhelyet egy fájl számára egyszerűen annak 'allokált'-kénti megjelölésével. Akár a FAT, amikor egy ismert hosszúságú fájlt hoz létre, az exFAT kénytelen olyan hosszan teljes fizikai írást létrehozni, mint annak hosszúsága.
*   [ext2](https://en.wikipedia.org/wiki/ext2 "wikipedia:ext2") - A **Második bővített fájlrendszer** jól bevált, érett és nagyon stabil GNU/Linux fájlrendszer. Hátránya, hogy nem támogatja a naplózást és a sorompót. A naplózás hiánya sajnos adatvesztésben nyilvánulhat meg, ha a rendszer összeomlik, vagy egyszerűen áramszünet van. **Nem** megfelelő root (`/`) és `/home` partíciók számára, mert a fájlrendszer konzisztenciájának ellenőrzése hosszú ideig tarthat. Az ext2 fájlrendszer [átalakítható ext3 fájlrendszerré](/index.php/Convert_ext2_to_ext3 "Convert ext2 to ext3").
*   [ext3](https://en.wikipedia.org/wiki/ext3 "wikipedia:ext3") - A **Harmadik bővített fájlrendszer** lényegében az ext2 naplózással és írási sorompóval ellátva. Visszafelé kompatibilis az ext2-vel, alaposan tesztelt és rendkívül stabil.
*   [ext4](https://en.wikipedia.org/wiki/ext4 "wikipedia:ext4") - A **Negyedik bővített fájlrendszer** újabb fájlrendszer, mely az ext2-vel és az ext3-mal is kompatibilis. Egészen 1 exabyte (értsd 1,048,576 terabyte-ig) méretig támogatja a tárolóeszközöket, a fájlok nagyságát pedig 16 terabyte-ig. Megemeli az ext3 32,000-es alkönyvtár-korlátozását 64,000-re. Mindemellett online töredezettségmentesítésre is képes.
*   [F2FS](https://en.wikipedia.org/wiki/F2FS "wikipedia:F2FS") - **Flash-Barát Fájlrendszer** egy Kim Jaegeuk (koreaiul: 김재극) által kreált flash fájlrendszer, melyet a Samsung-nál készített kifejezetten a Linux rendszermag számára. Az alapötlet az volt, hogy olyan fájlrendszert alkosson, mely a kezdetektől számításba veszi a NAND flash memória alapú tárolóeszközök (tehát SSD-k, eMMC-k, SD kártyák) karakterisztikáit, melyek egyre gyakrabban fordulnak elő, mobilkészülékektől a szerverekig mindenhol.
*   [JFS](https://en.wikipedia.org/wiki/JFS_(file_system) - Az IBM **Journaled File System**-e (naplózott fájlrendszer) volt az első, mellyel lehetővé vált a naplózás. Sok évig fejlesztették az IBM AIX® operációs rendszeren, mielőtt GNU/Linux-ra is megjelent. A JFS veszi a legkevésbé igénybe a processzor erőforrásait az összes GNU/Linux fájlrendszer közül. Formázáskor nagyon gyors, akárcsak csatoláskor és a fájlrendszer ellenőrzésekor (fsck). A JFS nagyon jó általános teljesítményt biztosít, leginkább a deadline I/O ütemező használatával együtt. Nem annyira jól támogatott, mint az ext sorozat vagy a ReiserFS, de nagyon érett és stabil.
*   [NILFS2](https://en.wikipedia.org/wiki/NILFS "wikipedia:NILFS") - A **New Implementation of a Log-structured File System**-et (naplózott struktúrájú fájlrendszer új kivitelben) az NTT fejlesztette ki. Minden adatot egy megszakítatlan naplószerű formátumban tárol, melyhez a rendszer csak "hozzáír" de sosem írja felül. Ezáltal csökken a keresési idő és minimalizálódik az a fajta adatvesztés, mely a hagyományos Linux fájlrendszerek összeomlásakor fordulhat elő.
*   [NTFS](https://en.wikipedia.org/wiki/NTFS "wikipedia:NTFS") - **File system used by Windows** (A Windows által használt fájlrendszer). Az NTFS-nek számos technikai előnye van a FAT és HPFS (High Performance File System, magas teljesítményű fájlrendszer) felett, úgy mint a metaadatok támogatása, fejlettebb adatstruktúrák használata, melyekkel növekszik a teljesítmény, a megbízhatóság, a lemez kihasználhatósága; illetve olyan kiterjesztéseket tartalmaz, mint a biztonsági jogosultságok kezelését (ACL) és a naplózást.
*   [Reiser4](https://en.wikipedia.org/wiki/Reiser4 "wikipedia:Reiser4") - **A ReiserFS fájlrendszer utódja.**, melyet a Namesys épített fel "from scratch", iletve a DARPA és a Linspire szponzorálja, kiegyensúlyozott fa adatszerkezeti megközelítést használ, melyben az alacsony kihasználtságú *node* blokkokat nem vonják össze, míg nem kerülnek írásra, kivéve memória-nyomás hatására vagy míg egy tranzakció végbe nem megy. Ez teszi lehetővé, hogy a Reiser4 állományokat vagy könyvtárakat hozzon létre anélkül, hogy fix blokkokra pazarolná az idejét.
*   [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") - A **Hans Reiser nagy teljesítményű naplózó fájlrendszere (v3)** egy roppant szokatlan és kreatív algoritmust használ az adat átmenő teljesítményének növelésére. Elismerten rendkívül gyors, legfőképp, ha sok kisméretű állományt kell kezelni. A ReiserFS formázáskor nagyon gyors, de a többiekhez képest csatoláskor lassú. Bár érett és stabil rendszer, a ReiserFSv3-at jelenleg nem fejlesztik tovább. Általában nagyon jó választás a `/var` számára.
*   [Swap](https://en.wikipedia.org/wiki/Paging "wikipedia:Paging") - Fájlrendszer, mely cserehelyként használatos.
*   [VFAT](https://en.wikipedia.org/wiki/File_Allocation_Table#VFAT "wikipedia:File Allocation Table") - A **Virtual File Allocation Table (virtuális fájl-allokációs tábla)** technikailag egyszerű és gyakorlatilag minden operációs rendszer támogatja. Ezért nagyon hasznos szilárd memóriakártyák számára, s jó módja az operációs rendszerek közti adatmegosztásnak. A VFAT támogatja a hosszú fájlneveket.
*   [XFS](https://en.wikipedia.org/wiki/XFS "wikipedia:XFS") - **Korai naplózó fájlrendszer, melyet eredetileg a Silicon Graphics fejlesztett** az IRIX operációs rendszerhez, mielőtt átültették GNU/Linux-ra. Nagy az átmenő teljesítménye nagy fájlok vagy fájlrendszerek esetén, nagyon gyors formázáskor és csatoláskor. Az összehasonlító tesztek alapján lassabb, ha több kisebb állományt kell kezelnie. Az XFS nagyon érett és online töredezettség-mentesíthető.
*   [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS") - **Kombinált fájlrendszer és logikai kötetkezelő a Sun Microsystems-től**. A ZFS védelmet nyújt az adatvesztéstől, támogatja a nagyon magas tárolókapacitást, magában foglalja a fájlrendszer és a kötetkezelés koncepcióját, képes pillanatképeket létrehozni, az "írásnál másold" klónozásra, a folyamatos integritás-ellenőrzésre és automatikus javításra, a RAID5-höz hasonló RAID-Z használatára, illetve natívan támogatja az NFSv4 ACL-jeit.

### Naplózás

Az ext2 és FAT16/32 kivételével minden felsorolt fájlrendszer [naplózást](https://en.wikipedia.org/wiki/Journaling_file_system "wikipedia:Journaling file system") használ. A naplózás csökkenti a hibalehetőségeket, mivel jegyzi a változásokat, mielőtt azok a fájlrendszeren módosulnának. Rendszerösszeomlás vagy áramellátási problémák esetén az ilyen rendszerek gyorsabban állíthatók fel, illetve kisebb az esélyük az adatvesztésre. A naplózás a fájlrendszer egy kijelölt helyén történik.

A naplózó-technikák nem egyformák. Csak az ext3 és ext4 használ adatmódú naplózást, mely az adatról és a metaadatról is végez bejegyzéseket. Az adatmódú naplózás hátrányossága a sebességvesztés, így alapértelmezetten nincs engedélyezve. A többi fájlrendszer csak metaadatot naplóz. Míg bármely naplózó fájlrendszer képes felállítani egy összeomlott rendszert, csak az adatmódú naplózás képes az adatvesztést is hatékonyan kiküszöbölni. Ezért nagyobb az ilyen fájlrendszerek teljesítményigénye is, hiszen kétszer írnak a lemezre; egyszer a naplóra, egyszer pedig a tényleges adatra. Amikor fájlrendszert választunk, a rendszer sebességének és az adat biztonságának kérdését gondosan mérlegelnünk kell!

### Arch Linux támogatás

*   **btrfs-progs** — [Btrfs](/index.php/Btrfs "Btrfs") támogatás.

	[http://btrfs.wiki.kernel.org/](http://btrfs.wiki.kernel.org/) || [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs)

*   **dosfstools** — VFAT támogatás.

	[http://www.daniel-baumann.ch/software/dosfstools/](http://www.daniel-baumann.ch/software/dosfstools/) || [dosfstools](https://www.archlinux.org/packages/?name=dosfstools)

*   **exfat-utils** — exFAT támogatás.

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [exfat-utils](https://www.archlinux.org/packages/?name=exfat-utils)

*   **f2fs-tools** — [F2FS](/index.php/F2fs "F2fs") támogatás.

	[https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git](https://git.kernel.org/cgit/linux/kernel/git/jaegeuk/f2fs-tools.git) || [f2fs-tools](https://www.archlinux.org/packages/?name=f2fs-tools)

*   **fuse-exfat** — exFAT csatolás támogatása.

	[http://code.google.com/p/exfat/](http://code.google.com/p/exfat/) || [fuse-exfat](https://www.archlinux.org/packages/?name=fuse-exfat)

*   **e2fsprogs** — ext2, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4") támogatás.

	[http://e2fsprogs.sourceforge.net](http://e2fsprogs.sourceforge.net) || [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs)

*   **jfsutils** — [JFS](/index.php/JFS "JFS") támogatás.

	[http://jfs.sourceforge.net](http://jfs.sourceforge.net) || [jfsutils](https://www.archlinux.org/packages/?name=jfsutils)

*   **nilfs-utils** — NILFS támogatás.

	[http://www.nilfs.org/](http://www.nilfs.org/) || [nilfs-utils](https://www.archlinux.org/packages/?name=nilfs-utils)

*   **ntfs-3g** — [NTFS](/index.php/NTFS "NTFS") támogatás.

	[http://www.tuxera.com/community/ntfs-3g-download/](http://www.tuxera.com/community/ntfs-3g-download/) || [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g)

*   **reiser4progs** — [ReiserFSv4](/index.php/Reiser4 "Reiser4") támogatás.

	[http://sourceforge.net/projects/reiser4/](http://sourceforge.net/projects/reiser4/) || [reiser4progs](https://aur.archlinux.org/packages/reiser4progs/)

*   **reiserfsprogs** — ReiserFSv3 támogatás.

	[https://www.kernel.org/](https://www.kernel.org/) || [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs)

*   **util-linux** — [Swap](/index.php/Swap "Swap") támogatás.

	[http://www.kernel.org/pub/linux/utils/util-linux/](http://www.kernel.org/pub/linux/utils/util-linux/) || [util-linux](https://www.archlinux.org/packages/?name=util-linux)

*   **xfsprogs** — [XFS](/index.php/XFS "XFS") támogatás.

	[http://oss.sgi.com/projects/xfs/](http://oss.sgi.com/projects/xfs/) || [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs)

*   **zfs** — [ZFS](/index.php/ZFS "ZFS") támogatás.

	[http://zfsonlinux.org/](http://zfsonlinux.org/) || [zfs](https://aur.archlinux.org/packages/zfs/)

*   **zfs-fuse** — [ZFS támogatás FUSE-on keresztül](/index.php/ZFS_on_FUSE "ZFS on FUSE").

	[http://zfs-fuse.net/](http://zfs-fuse.net/) || [zfs-fuse](https://aur.archlinux.org/packages/zfs-fuse/)

**Megjegyzés:** A ZFS fájlrendszer nem zsugorítható hagyományos eszközökkel, mint a GParted.

## Eszközök formázása

**Figyelem:** Egy eszköz formázása minden adatot eltüntet róla, minden szükséges adaton mentsünk el.

### Feltételek

Mielőtt nekiindulunk a feladatnak, tudnunk kell, hogy a Linux milyen nevet adott az eszköznek. A merevlemezek és pendrive-ok `/dev/sd*x*`-ként jelennek meg, ahol az *x* egy kisbetű, míg a partícciók a `/dev/sd*xY*` formátumot használják,ahol *Y* egy szám.

Ha a formázandó eszközt már csatolta a rendszer, a következő parancs *MOUNTPOINT* oszlopában meg fog jelenni:

```
$ lsblk

```

Ha még nem csatolta a rendszer, tegyük meg mi:

```
# mount /dev/sd*xY* /valamely/könyvtár

```

Leválasztásához az *umount* parancsot használjuk azon a könyvtáron, ahova csatoltuk:

```
# umount /valamely/könyvtár

```

**Megjegyzés:** Az eszközt le kell választanunk, ha formázni akarjuk és új fájlrendszert hozunk létre rajta.

Változtassuk meg tetszésünk szerint a partíciós táblát. Ehhez MBR esetén az **fdisk**, GPT esetén a **gdisk** eszközt használhatjuk, vagy valamely grafikus programot. Bővebben lásd a [particionálást](/index.php/Partitioning_(Magyar) "Partitioning (Magyar)").

Új fájlrendszereket konzol alapú vagy grafikus programokkal készíthetünk.

### Eszközök konzolban

Egy partíció létrehozásához a **mkfs** parancsot használjuk, mely csak egy egységes front-end különféle `mkfs.*fájlrendszertípus*` eszközök számára. Így például egy ext4 fájlrendszer létrehozása ezzel a paranccsal történik:

```
# mkfs -t ext4 /dev/*partíció*

```

Ha cserehelyet akarunk létrehozni, a **mkswap**-t használjuk:

```
# mkswap /dev/*partíció*

```

### Grafikus eszközök

Több grafikus eszköz is szolgálhat a fájlrendszerek karbantartására:

*   **[Gparted](/index.php/Gparted "Gparted")** — GTK+ Partition Magic klón, a GNU Parted grafikus frontendje.

	[http://gparted.sourceforge.net](http://gparted.sourceforge.net) || [gparted](https://www.archlinux.org/packages/?name=gparted)

*   **gnome-disk-utility** — A GNOME lemezkezelő eszköze.

	[http://www.gnome.org](http://www.gnome.org) || [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility)

*   **KDE Partition Manager** — KDE eszköz, mely lemezeket, partíciókat és fájlrendszereket kezel.

	[https://sourceforge.net/projects/partitionman/](https://sourceforge.net/projects/partitionman/) || [partitionmanager](https://www.archlinux.org/packages/?name=partitionmanager)