Ez a dokumentum végigvezet az [Arch Linux](/index.php/Arch_Linux_(Magyar) "Arch Linux (Magyar)") telepítésének folyamatán a live rendszer hivatalos telepítőképről történő indításától kezdve. Telepítés előtt ajánlott átfutni a [GYIK-et](/index.php/FAQ "FAQ"). Egy nagyon részletes, értelmező telepítési útmutatóhoz lásd az [Útmutató kezdőknek](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)") oldalt. A [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") számos további telepítési útmutatót tartalmaz speciális esetekre.

A közösség által karbantartott [Arch wiki](/index.php/Main_page "Main page") egy kiváló forrás, és probléma esetén ehhez javasolt fordulni. Az [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") csatorna ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), és a [fórumok](https://bbs.archlinux.org/) szintén rendelkezésre állnak, ha a válasz nem található meg máshol. Szintén javasolt megnézni a `man` oldalait bármely, általad nem ismert parancsnak; ez általában a `man *parancs*` paranccsal hívható elő.

## Contents

*   [1 Letöltés](#Let.C3.B6lt.C3.A9s)
*   [2 Telepítés](#Telep.C3.ADt.C3.A9s)
    *   [2.1 Billentyűzetkiosztás](#Billenty.C5.B1zetkioszt.C3.A1s)
    *   [2.2 Lemezek particionálása](#Lemezek_particion.C3.A1l.C3.A1sa)
    *   [2.3 Partíciók formázása](#Part.C3.ADci.C3.B3k_form.C3.A1z.C3.A1sa)
    *   [2.4 Partíciók csatolása](#Part.C3.ADci.C3.B3k_csatol.C3.A1sa)
    *   [2.5 Kapcsolódás az internetre](#Kapcsol.C3.B3d.C3.A1s_az_internetre)
        *   [2.5.1 Vezeték nélküli hálózat](#Vezet.C3.A9k_n.C3.A9lk.C3.BCli_h.C3.A1l.C3.B3zat)
    *   [2.6 Az alaprendszer telepítése](#Az_alaprendszer_telep.C3.ADt.C3.A9se)
    *   [2.7 A rendszer beállítása](#A_rendszer_be.C3.A1ll.C3.ADt.C3.A1sa)
    *   [2.8 Boot loader telepítése és beállítása](#Boot_loader_telep.C3.ADt.C3.A9se_.C3.A9s_be.C3.A1ll.C3.ADt.C3.A1sa)
    *   [2.9 Leválasztás és újraindítás](#Lev.C3.A1laszt.C3.A1s_.C3.A9s_.C3.BAjraind.C3.ADt.C3.A1s)
*   [3 Telepítés után](#Telep.C3.ADt.C3.A9s_ut.C3.A1n)

## Letöltés

Töltsd le az új Arch Linux ISO-t az [Arch Linux letöltési oldaláról](https://www.archlinux.org/download/).

*   Egyetlen kép érhető el, ami egy i686 vagy x86_64 live rendszert képes indítani az Arch Linux hálózatról történő telepítéséhez. Olyan médium, amely tartalmazza a [core] tárolót, nem érhető el többé.
*   A telepítési képeket aláírták, és erősen javasolt az aláírások ellenőrzése használat előtt: ehhez töltsd le a *.sig* fájlt a letöltési oldalról (vagy az egyik ott felsorolt tükörről) az *.iso* fájllal megegyező könyvtárba, majd használd a `pacman-key -v *iso-file*.sig` parancsot.
*   A kép kiírható CD-re, felcsatolható ISO fájlként, vagy közvetlenül [pendrive-ra írható](/index.php/USB_Installation_Media "USB Installation Media"). Ez csak új telepítésekhez szükséges; egy meglévő Arch Linux rendszer mindig frissíthető a `pacman -Syu` paranccsal.

## Telepítés

### Billentyűzetkiosztás

Sok országhoz és billentyűzettípushoz a megfelelő kiosztás alapból elérhető. A magyar kiosztás betöltéséhez a `loadkeys hu` parancs használható. További billentyűzetkiosztás-fájlok a `/usr/share/kbd/keymaps/` könyvtárban találhatók (loadkeys használata esetén az útvonal és fájlkiterjesztés elhagyható).

### Lemezek particionálása

Lásd a [particionálást](/index.php/Partitioning "Partitioning") részletekért.

Ha szeretnél készíteni halmozott blokkeszközöket az [LVM-hez](/index.php/LVM "LVM"), [lemeztitkosításhoz](/index.php/Disk_encryption "Disk encryption") vagy [RAID-hez](/index.php/RAID "RAID"), akkor azt most tedd meg.

Ha (U)EFI-t használsz, akkor valószínűleg szükséged lesz egy külön partícióra az UEFI rendszerpartíció számára. Lásd [UEFI rendszerpartició készítése Linuxon](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").

### Partíciók formázása

Lásd a [fájlrendszereket](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems") a részletekért.

### Partíciók csatolása

Most fel kell csatolnod a root partíciót a `/mnt` útvonalra. Ezután könyvtárakat kell létrehoznod minden egyéb partícióhoz (`/mnt/boot`, `/mnt/home`, ...), és fel kell csatolnod, valamint aktiválnod kell a [swap](/index.php/Swap "Swap") partíciót, ha azt szeretnéd, hogy a *genfstab* felismerje azokat.

### Kapcsolódás az internetre

Egy DHCP szolgáltatás alapból engedélyezve van az összes elérhető eszközhöz. Ha be kell állítanod egy statikus IP-t, vagy olyan kezelőeszközöket használsz mint a [Netctl](/index.php/Netctl "Netctl"), akkor először le kell állítanod ezt a szolgáltatást: `systemctl stop dhcpcd.service`. További információért lásd [hálózat beállítása](/index.php/Configuring_network "Configuring network").

#### Vezeték nélküli hálózat

Futtasd a `wifi-menu` parancsot a vezeték nélküli hálózat beállításához. Részletekért lásd [Vezeték nélküli hálózat beállítása](/index.php/Wireless_Setup "Wireless Setup") és [Netctl](/index.php/Netctl "Netctl").

### Az alaprendszer telepítése

Mielőtt telepítesz, érdemes szerkeszteni a `/etc/pacman.d/mirrorlist` fájlt úgy, hogy az általad előnyben részesített [tükör](/index.php/Mirrors "Mirrors") legyen az első helyen. A mirrorlist ezen példányát a `pacstrap` az új rendszerre is telepíti, tehát érdemes ezt most beállítani.

A [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) szkript használatával telepítjük az alaprendszert.

```
# pacstrap /mnt base

```

Egyéb csomagok telepítéséhez add hozzá azok neveit az előbbi parancshoz (szóközökkel elválasztva), beleértve a boot loadert, ha szeretnéd.

### A rendszer beállítása

*   Generálj egy [fstab](/index.php/Fstab "Fstab")-ot a következő paranccsal (ha előnyben részesíted az UUID-k vagy címkék használatát, add hozzá a `-U` vagy `-L` opciót annak megfelelően):

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   [chroot](/index.php/Chroot "Chroot") az újonnan telepített rendszerünkbe:

	 `# arch-chroot /mnt` 

*   Írd a hostname-edet a `/etc/hostname` fájlba.

*   Hozz létre szimbolikus linket a `/etc/localtime` helyről a `/usr/share/zoneinfo/Zone/SubZone` fájlra. Cseréld ki a `Zone`-t és `Subzone`-t a neked megfelelőre. Például Magyarország esetén:

	 `# ln -s /usr/share/zoneinfo/Europe/Budapest /etc/localtime` 

*   Engedélyezd a kiválasztott locale-t a `/etc/locale.gen` fájlban, és generáld azt a `locale-gen` paranccsal. Magyar nyelv esetén ehhez vedd ki a # jelet az alábbi sor elől:

	 `hu_HU.UTF-8 UTF-8` 

*   Állítsd be a [locale](/index.php/Locale#Setting_system-wide_locale "Locale") beállításait a `/etc/locale.conf` fájlban. Magyar nyelv esetén add hozzá az alábbi sort:

	 `LANG=hu_HU.utf8` 

*   Add meg a [paranccsori billenytűzetkiosztás](/index.php/KEYMAP "KEYMAP") és [betűkészlet](/index.php/Fonts#Console_fonts "Fonts") beállításait a `/etc/vconsole.conf` fájlban. Magyar nyelv esetén add hozzá az alábbi sorokat:

```
KEYMAP=hu
FONT=lat2-16
FONT_MAP=8859-2
```

*   Állítsd be az `/etc/mkinitcpio.conf` fájlt szükség szerint (lásd [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")), és hozz létre egy kezdeti RAM lemezt az alábbi paranccsal:

	 `# mkinitcpio -p linux` 

*   Állíts be egy root jelszót a `passwd` paranccsal.
*   Állítsd be a hálózatot újra az újonnan telepített környezetben. Lásd [Hálózat beállítása](/index.php/Network_configuration "Network configuration") és [Vezeték nélküli hálózat beállítása](/index.php/Wireless_Setup "Wireless Setup").

### Boot loader telepítése és beállítása

Lásd [Boot loaderek](/index.php/Boot_loaders "Boot loaders") az elérhető választékért.

### Leválasztás és újraindítás

Ha még mindig a chroot környezetben vagy, írd be a `exit` parancsot, vagy nyomd le a `Ctrl+D` billentyűkombinációt a kilépéshez. Korábban a `/mnt` útvonal alá csatoltuk a partíciókat. Ebben a lépésben lecsatoljuk azokat:

```
# umount -R /mnt

```

Most indíts újra, majd jelentkezz be az új rendszerbe root felhasználóként.

## Telepítés után

Lásd az [Általános ajánlásokat](/index.php/General_recommendations "General recommendations") a rendszerkezelési irányelvekhez és a telepítés utáni útmutatókhoz mint például egy grafikus környezet, hang vagy érintőtábla beállítása.

Alkalmazások listájához, amik érdekelhetnek, lásd [Alkalmazások listája](/index.php/List_of_applications "List of applications").