Related articles

*   [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming")
*   [NTFS Write Support](/index.php/NTFS_Write_Support "NTFS Write Support")
*   [Firefox Ramdisk](/index.php/Firefox_Ramdisk "Firefox Ramdisk")
*   [Boot debugging](/index.php/Boot_debugging "Boot debugging")
*   [udev](/index.php/Udev "Udev")

Az [/etc/fstab](https://en.wikipedia.org/wiki/Fstab "wikipedia:Fstab") fájl határozza meg, hogy a lemezek partícióit, más blokkeszközöket, vagy távoli fájlrendszereket hogyan csatolunk a fájlrendszerünkbe.

Minden csatolandó fájlrendszert különálló sor ír le. Ezek a leírások rendszer indításakor dinamikusan [systemd](/index.php/Systemd "Systemd") csatolási egységgé (mount unit) konvertálódnak, valamint akkor, amikor a rendszerkezelőt újratöltjük. Az alapértelmezett beállítások automatikusan ellenőrzik (fsck) és csatolják a fájlrendszereket, mielőtt az azok felcsatolását igénylő szolgáltatások elindulnának. Például a systemd magától megbizonyosodik róla, hogy a távoli fájlrendszerek, mint az [NFS](/index.php/NFS "NFS") vagy a [Samba](/index.php/Samba "Samba") csak azután induljanak, hogy a hálózatunk már működőképes. Ezért a helyi és távoli fájlrendszer-csatolások, melyek az `/etc/fstab`-ban szerepelnek, külső beavatkozás nélkül is működőképesek. Lásd a [systemd.mount(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.mount.5) leírást részletekért.

A `mount` parancs az fstab-ot hasznája, ha parancsként csak a könyvtárt vagy az eszköz nevét (pl. mount /dev/sdb2 vagy mount /my/mount) adjuk meg, s a parancs ilyenkor az fstab-ból keresi vissza a másik paramétert. Ha így teszünk, az fstab-ban foglalt csatolási opciók lesznek használatosak.

## Contents

*   [1 Példa az fstab állományra](#P.C3.A9lda_az_fstab_.C3.A1llom.C3.A1nyra)
*   [2 A mezők definíciói](#A_mez.C5.91k_defin.C3.ADci.C3.B3i)
*   [3 A fájlrendszerek azonosítása](#A_f.C3.A1jlrendszerek_azonos.C3.ADt.C3.A1sa)
    *   [3.1 Rendszermag szerinti leíró](#Rendszermag_szerinti_le.C3.ADr.C3.B3)
    *   [3.2 Címke](#C.C3.ADmke)
    *   [3.3 UUID](#UUID)
*   [4 Tippek és trükkök](#Tippek_.C3.A9s_tr.C3.BCkk.C3.B6k)
    *   [4.1 Automatikus csatolás systemd-vel](#Automatikus_csatol.C3.A1s_systemd-vel)
    *   [4.2 Szóköz az elérési utakban](#Sz.C3.B3k.C3.B6z_az_el.C3.A9r.C3.A9si_utakban)
    *   [4.3 Külső meghajtók](#K.C3.BCls.C5.91_meghajt.C3.B3k)
    *   [4.4 atime opciók](#atime_opci.C3.B3k)
    *   [4.5 tmpfs](#tmpfs)
        *   [4.5.1 Használata](#Haszn.C3.A1lata)
            *   [4.5.1.1 Fordítási idők javítása](#Ford.C3.ADt.C3.A1si_id.C5.91k_jav.C3.ADt.C3.A1sa)
                *   [4.5.1.1.1 Egy munkamenetre](#Egy_munkamenetre)
                *   [4.5.1.1.2 Véglegesítve](#V.C3.A9gleges.C3.ADtve)
    *   [4.6 A FAT32 írása egyszerű felhasználóként](#A_FAT32_.C3.ADr.C3.A1sa_egyszer.C5.B1_felhaszn.C3.A1l.C3.B3k.C3.A9nt)
    *   [4.7 A root partíció újracsatolása](#A_root_part.C3.ADci.C3.B3_.C3.BAjracsatol.C3.A1sa)
*   [5 Lásd még](#L.C3.A1sd_m.C3.A9g)

## Példa az fstab állományra

Egyszerű `/etc/fstab` fájl, mely kernel név szerinti leírókat használ:

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass>
/dev/sda1              /             ext4      defaults,noatime      0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      defaults,noatime      0      2
```

## A mezők definíciói

Az `/etc/fstab` állomány a következő szóközzel vagy tabulátorral elválasztott mezőket tartalmazza:

```
 <file system>        <dir>         <type>    <options>             <dump> <pass>

```

*   **<file system>** - (fájlrendszer) a csatolandó partíció vagy tárolóeszköz.
*   **<dir>** - (könyvtár) a csatolási pont, ahova a <file system> csatolásra kerül.
*   **<type>** - (típus) a csatolandó partíció vagy tárolóeszköz fájlrendszerének típusa. Sok különböző fájlrendszer támogatott: `ext2`, `ext3`, `ext4`, `btrfs`, `reiserfs`, `xfs`, `jfs`, `smbfs`, `iso9660`, `vfat`, `ntfs`, `swap` és `auto`. Az `auto` típus a mount parancsra bízza a használandó fájlrendszer típusának meghatározását. Ez hasznos lehet az optikai adathordozók esetén (CD/DVD).
*   **<options>** - (opciók) az adott fájlrendszer csatolási opciói. Jegyezzük meg, hogy egyes csatolási opciók csak egy-egy fájlrendszerre jellemzők ([mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8)). A leggyakoribbak a következők:

*   `auto` - Csatoljuk automatikusan a rendszer indításakor, vagy ha a `mount -a` parancs kerül használatra.
*   `noauto` - Csak akkor csatoljuk, ha ezt külön paranccsal kérjük.
*   `exec` - Engedélyezi a bináris fájlok végrehajtását a fájlrendszeren.
*   `noexec` - Tiltja a bináris fájlok végrehajtását a fájlrendszeren.
*   `ro` - Csak olvashatóan csatolja a fájlrendszert.
*   `rw` - Írhatóan és olvashatóan csatolja a fájlrendszert.
*   `user` - Bármely felhasználónak engedélyezi a fájlrendszer csatolását. Ez automatikusan maga után vonja a `noexec`, `nosuid` és `nodev` opciókat, kivéve, ha ezt külön jelezzük.
*   `users` - Bármely felhasználónak, aki része az users csoportnak, engedélyezi a fájlrendszer csatolását.
*   `nouser` - Csak root csatolhatja a fájlrendszert.
*   `owner` - Csak az eszköz tulajdonosa csatolhatja a fájlrendszert.
*   `sync` - Az I/O szinkronizáltan történik.
*   `async` - I/O nem szinkronizáltan történik.
*   `dev` - Értelmezi a speciális blokkeszközöket a fájlrendszeren.
*   `nodev` - Nem értelmezi a speciális blokkeszközöket a fájlrendszeren.
*   `suid` - Engedélyezi az suid és sgid bitek működését a fájlrendszeren. Ezek teszik lehetővé, hogy a felhasználók időlegesen megemelt privilégiumokkal bináris kódot hajtsanak végre egy bizonyos cél érdekében.
*   `nosuid` - Meggátolja az suid és sgid bitek működését.
*   `noatime` - Nem frissíti az inode-ok elérési idejét a fájlrendszeren - növelheti a teljesítményt, lásd [atime opciók](#atime_options)).
*   `nodiratime` - Nem frissíti a könyvtár inode-ok elérési idejét a fájlrendszeren - növelheti a teljesítményt, lásd [atime opciók](#atime_options)).
*   `relatime` - Az inode-ok elérési idejét a módosítás vagy változtatás idejéhez képest frissíti. Az elérési idő csak akkor frissül, ha az előző elérés előbb történt, mint a jelenlegi módosítási vagy változtatási idő. (Hasonló a noatime-hoz, de nem gátolja a mutt és a hasonló programok működését, melyeknek tudniuk kell, hogy egy állomány már olvasásra került-e a legutóbbi módosítása óta.) Növelheti a teljesítményt, lásd az [atime opciókat](/index.php/Fstab#atime_options "Fstab")).
*   `discard` - Hajtson végre [TRIM](/index.php/SSD#TRIM "SSD") parancsokat az alatta elhelyezkedő blokkeszközön, amikor blokkok szabadulnak fel. Használata erősen javasolt, ha a fájlrendszer [SSD](/index.php/SSD "SSD") meghajtón foglal helyet.
*   `flush` - A `vfat` opció, mellyel az adat gyakrabban kerül tisztításra, így a másolási párbeszédablakok és állapotjelző csíkok megmaradnak, míg minden adat ténylegesen írásra kerül.
*   `nofail` - Csatoljuk fel az eszközt, ha elérhető, de ne vegyünk róla tudomást, ha nem az. Ezzel kiküszöbölhetők a hibaüzenetek, ha hordozható eszközről indítjuk a rendszert.
*   `defaults` - Az adott fájlrendszer alapértelmezett csatolási opciói kerülnek használatra. Ezek például az ext4 esetén: `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, `async`.

*   **<dump>** - (kiírás) a dump eszköz használja annak eldöntésére, hogy készítsen-e biztonsági másolatot, vagy sem. A dump ellenőrzi ezt a mezőt, s annak számértékéből állapítja meg, hogy szükség van-e a fájlrendszer másolatának létrehozására. A lehetséges értékek 0 és 1\. Ha 0, a dump nem vesz tudomást a fájlrendszerről; ha 1, a dump készít egy másolatot. Mivel a legtöbb felhasználó nem használ dump-ot, ez a bejegyzés 0 maradhat.

*   **<pass>** - (menet) Az [fsck](/index.php/Fsck "Fsck") eszköz használja annak megállapítására, hogy milyen sorrendben ellenőrizze le a fájlrendszereket. A lehetséges értékek a 0, 1 és a 2\. A root fájlrendszeré az 1-es, legmagasabb prioritás (kivéve, ha ez [btrfs](/index.php/Btrfs "Btrfs") fájlrendszer, amikor is ez 0) - minden más ellenőrzendő fájlrendszer prioritása legyen 2-es. Az olyan fájlrendszerek, ahol 0 értéket állítunk be, nem kerülnek ellenőrzésre.

## A fájlrendszerek azonosítása

Háromféle módja van a partíciók vagy tárolóeszközök azonosításának az `/etc/fstab`-ban: a rendszermag szerinti leíró (kernel name descriptor) alapján, címke vagy UUID alapján. Az UUID vagy a címkék használatának előnye az, hogy nem függenek attól a sorrendtől, ahogy a meghajtók fizikai összeköttetésbe kerültek a géppel. Mindez nagyon hasznos lehet, ha a BIOS-ban a tárolóegységek sorrendje megváltozik, vagy egyszerűen csak változtatunk a kábelezésükön. Emellett a BIOS olykor magától is megváltoztathatja a tárolóegységek sorrendjét. Erről a [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") cikkben olvashatunk többet.

A partíciókról alapvető információt az alábbi paranccsal szerezhetünk:

 `$ lsblk -f` 
```
NAME   FSTYPE LABEL      UUID                                 MOUNTPOINT
sda                                                           
├─sda1 ext4   Arch_Linux 978e3e81-8048-4ae1-8a06-aa727458e8ff /
├─sda2 ntfs   Windows    6C1093E61093B594                     
└─sda3 ext4   Storage    f838b24e-3a66-4d02-86f4-a2e73e454336 /media/Storage
sdb                                                           
├─sdb1 ntfs   Games      9E68F00568EFD9D3                     
└─sdb2 ext4   Backup     14d50a6c-e083-42f2-b9c4-bc8bae38d274 /media/Backup
sdc                                                           
└─sdc1 vfat   Camera     47FA-4071                            /media/Camera
```

### Rendszermag szerinti leíró

Futassuk az `lsblk -f` parancsot a partíciók listázásához, és helyezzük eléjük a `/dev` előtagot.

Lásd a [példát](#File_example).

### Címke

**Megjegyzés:** Az esetleges ütközéseket kiküszöbölendő, minden címkének egyedinek kell lennie.

Arról, hogy hogyan lássunk el címkével partíciókat vagy meghajtókat, [Persistent block device naming#by-label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming") cikkben olvashatunk. A root partíció újranevezését valamiféle "live" médiumról kell elvégeznünk, mert a partíciót első körben le kell választanunk.

Futtassuk az `lsblk -f` parancsot a partíciók listázásához, és helyezzük eléjük a `LABEL=` előtagot:

 `/etc/fstab` 
```
# <file system>        <dir>         <type>    <options>             <dump> <pass> 
LABEL=Arch_Linux       /             ext4      defaults,noatime      0      1
LABEL=Arch_Swap        none          swap      defaults              0      0
```

### UUID

Minden partíciónak és tárolóegységnek van egy egyedi UUID-je. Ezt a fájlrendszerek segédprogramjai generálják (pl.: `mkfs.*`), amikor a partíciót létrehozzuk vagy formázzuk. Lássuk a [Persistent block device naming#by-uuid](/index.php/Persistent_block_device_naming#by-uuid "Persistent block device naming") cikket.

Futtassuk az `lsblk -f` parancsot a partíciók listázásához, és lássuk el őket a `UUID=` előtaggal:

**Tip:** Ha csak az UUID-kat akarjuk listázni, használjuk a következőt:
```
$ lsblk -no UUID /dev/sda2

```

 `/etc/fstab` 
```
# <file system>                            <dir>     <type>    <options>             <dump> <pass>
UUID=24f28fc6-717e-4bcd-a5f7-32b959024e26  /         ext4      defaults,noatime      0      1
UUID=03ec5dd3-45c0-4f95-a363-61ff321a09ff  /home     ext4      defaults,noatime      0      2
UUID=4209c845-f495-4c43-8a03-5363dd433153  none      swap      defaults              0      0
```

## Tippek és trükkök

### Automatikus csatolás systemd-vel

Ha a `/home` partíciónk nagyméretű, jobb, ha a `/home`-tól nem függő szolgáltatásaink már akkor is indulhatnak, míg a `/home` *fsck* ellenőrzés alatt áll. Ezt úgy érhetjük el, hogy az alábbi opciókat adjuk az `/etc/fstab`-ban a `/home` partícióhoz:

```
noauto,x-systemd.automount

```

Ez akkor ellenőrzi és csatolja a `/home` partíciót, amikor azt először elérjük, a kernel pedig tárolja az összes fájlelérést, míg a `/home` nem áll készen.

**Megjegyzés:** Ezzel a kis trükkel a `/home` partíció fájlrendszerének típusa csatoláskor `autofs` lesz, melyet az [mlocate](/index.php/Mlocate "Mlocate") figyelmen kívül hagy. Ezáltal tehát a `/home` automatikus felcsatolása a rendszerünktől függően egy-két másodperc alatt fog megtörténni, tehát lehet, hogy ez a trükk nem is túl hasznos.

Ugyanez vonatkozik a távoli fájlrendszerek felcsatolására is. Ha azt akarjuk, hogy csak az első hozzáféréskor csatolódjanak, ugyanígy a `noauto,x-systemd.automount` paramétereket kell használnunk. Ehhez még használhatjuk a `x-systemd.device-timeout=#` opciót egy bizonyos várakozási idő megadásához, ha a hálózati erőforrás esetleg nem lenne elérhető.

Ha kulcsokkal titkosított fájlrendszereink vannak, a `noauto` paramétert a megfelelő bejegyzésekhez adhatjuk az `/etc/crypttab`-ban. A *systemd* így nem nyitja meg a titkosított eszközt a rendszer indulásakor, hanem vár, míg valaki hozzá akar férni, s megnyitja a megjelölt kulccsal, mielőtt felcsatolja. Ez induláskor megspórolhat pár másodpercet, ha például titkosított RAID eszközt használunk, mivel a systemd-nek nem kell várnia, míg az eszköz elérhető lesz. Például:

 `/etc/crypttab`  `data /dev/md0 /root/key noauto` 

### Szóköz az elérési utakban

Ha bármely csatolási pont szóközt tartalmaz, használjuk az escape karaktert `\`, melyet `040` háromjegyű nyolcas számrendszerű kód követ, hogy a szóközt emulálja:

 `/etc/fstab` 
```
UUID=47FA-4071     /home/username/Camera<font color="grey">\040</font>Pictures   vfat  defaults,noatime       0  0
/dev/sda7          /media/100<font color="grey">\040</font>GB<font color="grey">\040</font>(Storage)       ext4  defaults,noatime,user  0  2
```

### Külső meghajtók

A külső eszközök, melyeket jelenlétükben csatolunk, de ha nincsenek jelen, figyelmen kívül hagyunk, a `nofail` opciót igénylik. Így nem kapunk hibaüzeneteket rendszerindításkor.

 `/etc/fstab`  `/dev/sdg1        /media/backup    jfs    defaults,nofail    0  2` 

### atime opciók

A `noatime`, `nodiratime` vagy `relatime` opciók használata hatással lehet a meghajtó teljesítményére.

*   Az `atime` egy állomány minden egyes elérésekor frissíti annak *atime*-ját. Ez a leghasznosabb, ha az ember szervert üzemeltet; ám egy asztali rendszer esetében nem sok értelme van. Az `atime` opció használatának egyik hátulütője az, hogy még a gyorsítótárból való olvasás (ha memóriából olvasunk a lemez helyett)is íráshoz vezet!

	A `noatime` opció teljesen kikapcsolja az elérések írását a lemezen, ahányszor csak olvasunk egy állományt. Ez legtöbbször nagyon jól működik, kivéve egyes ritka esetekben ([Mutt](/index.php/Mutt "Mutt")), melyeknek épp erre az információra van szükségük. A mutt használatához a `relatime` opciót kell használni.

	A `nodiratime` opció kikapcsolja az elérések írását a lemezen, de csak könyvtárak elérésekor, míg minden más állomány elérése továbbra is írásra kerül.

**Megjegyzés:** A `noatime` eleve magában foglalja a `nodiratime`-ot. [Nem kell mindkettőt jelölni](http://lwn.net/Articles/244941/).

*   A `relatime` engedélyezi az elérés idejének írását, de csak akkor, ha az állomány módosul (a `noatime`-mal ellenben, ahol a hozzáférési idő nem módosul és mindig régebbi lesz, mint a módosítás ideje). A legjobb kompromisszum ezen opció használata lehet, mert a [Mutt](/index.php/Mutt "Mutt") és a hozzá hasonló programok működni fognak, de bizonyos mértékben a teljesítmény is megnő, hiszen az állományaink elérési ideje csak módosításkor változik. Ez az opció használatos, ha csak a `defaults` kulcsszót, vagy semmiféle opciót nem adunk meg az *fstab*-ban egy adott csatolási ponthoz.

### tmpfs

A [tmpfs](https://en.wikipedia.org/wiki/Tmpfs "wikipedia:Tmpfs") egy ideiglenes fájlrendszer, mely a memóriában és/vagy a cserehelyen található, attól függően, hogy mennyire töltjük meg. Ha könyvtárakat csatolunk tmpfs fájlrendszerként, azzal jelentősen meggyorsul tartalmuk és állományaik elérési ideje; illetve ez biztossá teszi, hogy tartalmuk újraindításkor kiürüljön.

A tmpfs-ként használt könyvtárak között van például a [/tmp](http://www.pathname.com/fhs/2.2/fhs-3.15.html), [/var/lock](http://www.pathname.com/fhs/2.2/fhs-5.9.html) és [/var/run](http://www.pathname.com/fhs/2.2/fhs-5.13.html). NE HASZNÁLJUK a [/var/tmp](http://www.pathname.com/fhs/2.2/fhs-5.15.html) esetében, mert ebben a könyvtárban olyan ideiglenes állományok foglalnak helyet, melyeknek két újraindítás közt is meg kell őrződniük. Az Arch tmpfs-t használ a `/run` könyvtárhoz, ahol a `/var/run` és a `/var/lock` csak symlinks-ként létezik a kompatibilitás kedvéért. A systemd alapértelmezett működése szerint a `/tmp`-hez is használatos, ebben az esetben nem igényel külön bejegyzést az `/etc/fstab`-ban, csak ha különösebb beállításokat igénylünk.

**Megjegyzés:** Ha [systemd](/index.php/Systemd "Systemd")-t használunk, a tmpfs könyvtárakban levő ideiglenes állományokat a [tmpfiles.d](/index.php/Systemd#Temporary_files "Systemd") használatával újra létrehozhatjuk indításkor.

Alapesetben egy tmpfs partíció mérete a teljes RAM felére állítódik be, de ez igény szerint szerkeszthető. Jegyezzük meg, hogy a tényleges memória/swap fogyasztás csak a kitöltöttségtől függ, mivel a tmpfs partíciók nem fogyasztanak RAM-ot, míg ténylegesen nem szükséges.

Hogy beállítsuk a saját szükségeink szerinti méretet, ebben a példában a `/tmp` csatolásán változtatva, használjuk a `size` csatolási opciót:

 `/etc/fstab`  `tmpfs   /tmp         tmpfs   nodev,nosuid,size=2G          0  0` 

Következzék egy kissé kihegyezettebb példa egy tmpfs csatolására. Ez hasznos lehet weboldalak, ideiglenes mysql állományok, `~/.vim/`, és sok minden más esetében. Az igazán fontos az, hogy az ideális opciókat találjuk meg ahhoz, amit csinálni szeretnénk. A cél az, hogy a beállításaink biztonságosak legyenek. Ha a méretet és a hozzáférési jogot korlátozzuk (uid és gid értékek, valamint mode érték megadásával, az nagyon biztonságos. Ebben a tárgyban tájékozódhatunk még a [#See also](#See_also) lista alapján.

 `/etc/fstab`  `tmpfs   /www/cache    tmpfs  rw,size=1G,nr_inodes=5k,noexec,nodev,nosuid,uid=648,gid=648,mode=1700   0  0` 

Lásd a `mount` parancs man oldalát több információért. One useful mount option in the man page is the `default` option. At least understand that.

A változtatások érvénybe léptetéséhez indítsuk újra a rendszert. Jegyezzük meg, hogy bár csábító lehet a `mount -a` használata az azonnali hatás érdekében, ez az említett könyvtárak állományait hozzáférhetetlenné teszi (ez különösen problémás lehet lock fájlokat használó programok esetén); ám ha mindegyik üres, biztonságos lehet a `mount -a` használata (vagy egyenkénti, manuális felcsatolásuk) az újraindítás helyett.

A válzoztatások érvénybe léptetése után leellenőrizhetjük, hogy minden í kívánt módon működik-e, belenézve a `/proc/mounts`-ba és a `findmnt`-vel:

 `$ findmnt --target /tmp` 
```
TARGET SOURCE FSTYPE OPTIONS
/tmp   tmpfs  tmpfs  rw,nosuid,nodev,relatime
```

#### Használata

Általánosságban, az I/O-intenzív folyamatok és programok, melyek gyakran futtatnak írás/olvasás műveleteket, hasznot húzhatnak egy tmpfs könyvtár használatából. Bizonyos alkalmazásoknak kifejezetten az előnyére válhat, ha néhány (vagy az összes) adatuk a megosztott memóriába kerül. Így például a [Firefox profil RAM-ba való áthelyezése](/index.php/Firefox_Ramdisk "Firefox Ramdisk") jelentős teljesítmény-növekedést eredményez.

##### Fordítási idők javítása

A csomagfordítás rengeteg apró fájl kezelését és számtalan I/O műveletet igényel; ezért ez az egyik olyan folyamat, mely a legtöbb előnyét élvezi, ha [#tmpfs](#tmpfs)-be helyezzük a munkakönyvtárát.

###### Egy munkamenetre

A `BUILDDIR` értéket parancshéjban exportálhatjuk, hogy a [makepkg](/index.php/Makepkg "Makepkg") munkakönyvtárt ideiglenesen valamely létező [tmpfs](/index.php/Tmpfs "Tmpfs")-ben helyezzen el:

```
$ BUILDDIR=/tmp/makepkg makepkg

```

###### Véglegesítve

Csak vegyük ki a kommentet a `BUILDDIR` sor elől a `/etc/makepkg.conf` fájlban, lásd a [Makepkg#Improving compile times](/index.php/Makepkg#Improving_compile_times "Makepkg") cikket a részletekért.

### A FAT32 írása egyszerű felhasználóként

A FAT32 partíciókra való íráshoz pár változást kell eszközölni az `/etc/fstab` állományban.

 `/etc/fstab`  `/dev/sdxY    /mnt/some_folder  vfat   user,rw,umask=000              0  0` 

A `user` zászló annyit tesz, hogy bármely (nem root) felhasználó képes fel-, vagy lecsatolni az `/dev/sdX` fájlrendszert. A `rw` írás-olvasási hozzáférést ad; `umask` opció elveszi a kijelölt jogokat - például a `umask=111` elveszi a végrehajtás jogát. A gond az, hogy ez elveszi a végrehajtás jogát a könyvtárakról is, ezért a `dmask=000` opcióval kell korrigálnunk. Lásd [Umask](/index.php/Umask "Umask").

Ezen opciók nélkül minden fájl végrehajtható lenne. A `showexec` opció is használható a umask és dmask helyett, mely a végrehajtható Windows fájlokat (com, exe, bat) végrehajtható színnel jelöli.

Összegzésként, ha például a FAT32 partíciónk a `/dev/sda9`, és a `/mnt/fat32` alá akarjuk csatolni, a következőt kell használnunk:

 `/etc/fstab`  `/dev/sda9    /mnt/fat32        vfat   user,rw,umask=111,dmask=000    0  0` 

### A root partíció újracsatolása

Ha valamilyen okból a root partíciót helytelenül csak olvashatóként csatoltuk, a következő paranccsal írható/olvasható-ként csatolhatjuk fel:

```
# mount -o remount,rw /

```

## Lásd még

*   [Teljes eszközlista, beleértve a blokkeszközöket is](http://www.kernel.org/pub/linux/docs/lanana/device-list/devices-2.6.txt)
*   [Fájlrendszer Hierarchia Standard](http://www.pathname.com/fhs/2.2/index.html)
*   [30x Gyorsabb Weblapok](http://www.askapache.com/web-hosting/super-speed-secrets.html) (Részletezett tmpfs)
*   [Adjunk Samba megosztásokat az /etc/fstab-hoz](/index.php/Samba#Add_Share_to_.2Fetc.2Ffstab "Samba")