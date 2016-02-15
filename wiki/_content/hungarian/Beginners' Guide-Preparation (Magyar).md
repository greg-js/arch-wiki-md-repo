**Tip:** Ez az oldal a teljes Beginners' Guide (Magyar) útmutató egyik részoldala. Ha az útmutatót teljes egészében akarod olvasni, akkor **[kattints ide](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**.

## Contents

*   [1 Előkészületek](#El.C5.91k.C3.A9sz.C3.BCletek)
    *   [1.1 Szerezzük be a legfrissebb telepítőt](#Szerezz.C3.BCk_be_a_legfrissebb_telep.C3.ADt.C5.91t)
        *   [1.1.1 A letöltött telepítő épségének ellenőrzése](#A_let.C3.B6lt.C3.B6tt_telep.C3.ADt.C5.91_.C3.A9ps.C3.A9g.C3.A9nek_ellen.C5.91rz.C3.A9se)
        *   [1.1.2 CD-ről történő telepítés](#CD-r.C5.91l_t.C3.B6rt.C3.A9n.C5.91_telep.C3.ADt.C3.A9s)
        *   [1.1.3 Memóriakártyáról vagy pendrive-ról történő telepítés](#Mem.C3.B3riak.C3.A1rty.C3.A1r.C3.B3l_vagy_pendrive-r.C3.B3l_t.C3.B6rt.C3.A9n.C5.91_telep.C3.ADt.C3.A9s)
            *   [1.1.3.1 Microsoft Windows-os módszer](#Microsoft_Windows-os_m.C3.B3dszer)
        *   [1.1.4 Telepítés hálózatról](#Telep.C3.ADt.C3.A9s_h.C3.A1l.C3.B3zatr.C3.B3l)
        *   [1.1.5 Telepítés virtuális rendszerként](#Telep.C3.ADt.C3.A9s_virtu.C3.A1lis_rendszerk.C3.A9nt)
    *   [1.2 Arch Linux telepítő bootolása](#Arch_Linux_telep.C3.ADt.C5.91_bootol.C3.A1sa)
        *   [1.2.1 Bootolás a meghajtóról](#Bootol.C3.A1s_a_meghajt.C3.B3r.C3.B3l)
        *   [1.2.2 Az operációs rendszer indítása](#Az_oper.C3.A1ci.C3.B3s_rendszer_ind.C3.ADt.C3.A1sa)
        *   [1.2.3 Billentyűzetkiosztás megváltoztatása](#Billenty.C5.B1zetkioszt.C3.A1s_megv.C3.A1ltoztat.C3.A1sa)
        *   [1.2.4 Dokumentáció](#Dokument.C3.A1ci.C3.B3)

## Előkészületek

**Megjegyzés:** Ha egy másik partición lévi már meglévő GNU/Linux disztribúció vagy LiveCD mellé szeretnéd telepíteni, akkor kérlek nézd meg [ezt a wiki bejegyzést](/index.php/Install_from_Existing_Linux "Install from Existing Linux") a teendőid lépéseiről. Ez különösen hasznos tud lenni, ha az Arch-odat [VNC](/index.php/VNC "VNC") vagy [SSH](/index.php/SSH "SSH") segítségével távolról szeretnéd feltenni. Ez az útmutató a hagyományos módon történő telepítést mutatja be.

### Szerezzük be a legfrissebb telepítőt

Az Arch hivatalos telepítőjét [itt](https://archlinux.org/download/) szerezheted be. A jelenlegi legfrissebb kiadás a 2012.10.06-os és az útmutató ehhez a kiadáshoz tartozik. Az új kiadás előtti telepítők is elérhetőek és letölthetőek [innen](https://releng.archlinux.org/isos/). **Ezek nem hivatalos telepítők, így hivatalos támogatás sincsen hozzájuk** Ezeket csak akkor érdemes használni, ha a hivatalos telepítő valamiért nem működne a számítógépeden amihez tartozó drivereket az újabb telepítők tartalmazhatják.

#### A letöltött telepítő épségének ellenőrzése

Töltsd le a jelenlegi telepítőhöz tartozó ellenőrző fájlt [innen](https://www.archlinux.org/iso/2012.10.06/sha1sums.txt) majd másold be a telepítővel megegyező könyvtárba! A `cd` paranccsal navigálj el abba a könyvtárba, ahova a telepítőt letöltötted, majd használd a `sha1sum` parancsot:

 `$ sha1sum --check name_of_checksum_file.txt` 

Ha azt írja ki, hogy "RENDBEN", a telepítő hibátlan. Ha a "RENDBEN" üzenet nem jelenik meg, töltsd le a megfelelő fájlokat újra.

Az md5sum ellenőrző hasonlóan működik.

#### CD-ről történő telepítés

Írd ki a .iso fájlt egy CD-re vagy DVD-re a számodra megfelelő meghajtóval és szoftverrel, majd [indítsd el az Arch Linux telepítőt](#Arch_Linux_telep.C3.ADt.C5.91_bootol.C3.A1sa) róla.

**Megjegyzés:** Az író és a korong minősége változó lehet. Lassú sebességen történő írás ajánlott a biztos eredményhez; Egyesek _**4x-es, vagy akár 2x-es írási sebességet**_ ajánlanak. Ha rendellenes viselkedést tapasztalsz, akkor próbáld meg a lehető leglassabb sebességgel írni.

#### Memóriakártyáról vagy pendrive-ról történő telepítés

Ehhez nézd meg a [Telepítés pendrive-ról](/index.php/USB_Installation_Media "USB Installation Media") című bejegyzést!

Ez a telepítési mód mind pendrive-ról, mind memóriakártyáról működik, ha támogatja róla a bootolást a BIOS-od.

Ne feledd, hogy a telepítő médiumon lévő összes adatod véglegesen elveszik!

##### Microsoft Windows-os módszer

Töltsd le a telepítő kiírására szolgáló szoftvert [innen](https://launchpad.net/win32-image-writer/+download). Csatlakoztasd a flash eszközöd. Indítsd el a letöltött alkalmazást, válaszd ki a képfájlt (A program alapból csak *.img kiterjesztések között keres, ezért a keresendő telepítőfájlt "*.iso" kiterjesztéssel kell beírnod, hogy láthasd az Arch telepítőt). Válaszd ki a flash eszközödnek megfelelő betűvel ellátott meghajtót, majd kattints az "Write"-ra.

Ezen felül még van számos megoldás, hogy [bootolható ISO képet helyezel a pendrivera](/index.php/Install_from_a_USB_flash_drive#On_Windows "Install from a USB flash drive"). Ha problémád akad a pendrive csatlakoztatásával, próbáld meg másik aljzatba dugni, vagy más kábellel csatlakoztatni.

Folytatás az [Arch Linux telepítő bootolásával](#Arch_Linux_telep.C3.ADt.C5.91_bootol.C3.A1sa).

#### Telepítés hálózatról

A CD-ről vagy pendriveról bootolás helyett választhatod a .iso fájl hálózatról bootolást is. Ez remekül működik, ha van egy működő szervered. Kérlek további teendőkhöz [ezt a bejegyzést](/index.php/Install_Arch_from_network_(via_PXE) "Install Arch from network (via PXE)") nézd meg, ez után pedig itt folytasd [Arch Linux telepítő bootolása](#Arch_Linux_telep.C3.ADt.C5.91_bootol.C3.A1sa).

#### Telepítés virtuális rendszerként

A [virtuális rendszerként](https://hu.wikipedia.org/wiki/Virtu%C3%A1lis_sz%C3%A1m%C3%ADt%C3%B3g%C3%A9p) történő feltelepítés egy jó módja annak, hogy megismerd az Arch linuxot és annak telepítési eljárását anélkül, hogy törölnöd kéne a jelenlegi operációs rendszeredet, vagy particionálnod kéne a meghajtódat; valamint az is mellette szól, hogy a telepítés alatt is tudod olvasni ezt az internetes segédanyagot. A virtuális telepítés mellett szól továbbá az Arch felhasználók számára is, hogy a jelenlegi rendszerük megzavarása nélkül tudják kipróbálni az új frissítéseket.

Egy-két példa virtualizáló programra [VirtualBox](/index.php/VirtualBox "VirtualBox"), [VMware](/index.php/VMware "VMware"), [QEMU](/index.php/QEMU "QEMU"), [Xen](/index.php/Xen "Xen"), [Parallels](/index.php/Parallels "Parallels").

A módja, hogy hogyan tudod telepíteni a rendszert virtuális gépként, függ a virtualizáló programodtól, de a folyamat nagyjából így kell kinézzen:

1.  Készíts egy virtuális meghajtót a gazdagépen
2.  Megfelelően állítsd be a virtuális gépet
3.  Bootolj a letöltött .iso képről a virtuális gépben
4.  Majd itt folytasd [Arch Linux telepítő bootolásával](#Arch_Linux_telep.C3.ADt.C5.91_bootol.C3.A1sa).

A következő bejegyzések hasznosak lehetnek a számodra:

*   [Arch Linux VirtualBox Guest](/index.php/Arch_Linux_VirtualBox_Guest "Arch Linux VirtualBox Guest")
*   [Installing Arch Linux from VirtualBox](/index.php/Installing_Arch_Linux_from_VirtualBox "Installing Arch Linux from VirtualBox")
*   [VirtualBox Arch Linux Guest On Physical Drive](/index.php/VirtualBox_Arch_Linux_Guest_On_Physical_Drive "VirtualBox Arch Linux Guest On Physical Drive")
*   [Installing Arch Linux in VMware](/index.php/Installing_Arch_Linux_in_VMware "Installing Arch Linux in VMware")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

### Arch Linux telepítő bootolása

**Tip:** Az alapvető telepítés memóriaigénye 64 MB RAM.

**Tip:** A telepítés folyamán az automatikus képernyő kikapcsolás aktiválódhat. Ha aktiválódik, nyomd meg az Alt gombot, hogy visszakapd a képet!

#### Bootolás a meghajtóról

Helyezd be a CD-t, vagy a flash meghajtót amit választottál. A számítógéped BIOS-ában be kell állítanod a helyes bootolási sorrendet. Hogy ezt megtedd, meg kell nyomnod egy gombot (általában `Delete`, `F1`, `F2`, `F11` vagy `F12`) amíg a BIOS logó látható (bekapcsolás utáni hardverellenőrzés).

**Főmenü:** Ezután a főmenünek kell megjelennie. A billentyűzeten található nyilak segítségével válaszd ki a számodra megfelelő opciót, majd üss `Enter`-t. A menü képfájlonként (.iso) eltérhet.

#### Az operációs rendszer indítása

Válaszd a "Boot Arch Linux" feliratú menüt, majd üss `Enter`-t, ezzel kezdetét veheti a telepítés. A rendszer betöltése után egy karakteres felület fogad. Automatikusan rendszergazdaként (ún. root-ként) leszel bejelentkeztetve.

**Megjegyzés:** Azok a felhasználók, akik az Arch Linux-ot [SSH](/index.php/SSH "SSH") kapcsolaton keresztül szeretnék telepíteni, ezen a ponton szükségük lehet néhány extra beállításra, azért hogy létre tudják hozni az SSH kapcsolatot közvetlenül a CD környezetbe. Ha ezt a módszert választod, nézd meg az [Install from SSH](/index.php/Install_from_SSH "Install from SSH") cikket!

Ha Intel videó chipset van a számítógépedben, és a rendszerbetöltés során a képernyő elfeketedik, akkor a kernelmód beállításoknál keresd a megoldást. A megoldás valószínűleg az lesz, hogy újraindítod a gépet, és a főmenüben nyomsz egy `Tab` gombot, hogy a kernel beállításait előhívd. A kernel sor végére szúrd be a következőt:

```
i915.modeset=0

```

Esetleg ezt:

```
video=SVIDEO-1:d

```

ami (amennyiben működik) nem fogja letiltani a kernelmód beállításokat.

További információért olvasd el az [Intel](/index.php/Intel_(Magyar) "Intel (Magyar)") bejegyzést.

Ha a képernyő _nem_ nem válik feketévé a bootolás során, de megakad, amikor a kernelt próbálja betölteni, nyomj `Tab` billentyűt, hogy szerkeszd a kernel sort, majd írd bele a következőt:

```
acpi=off

```

Ha ezzel megvagy, csak üss `Entert`, hogy a rendszer az általad megadott opciókkal bootoljon.

#### Billentyűzetkiosztás megváltoztatása

Ha nem amerikai kiosztású billentyűzeted van, akkor a következő paranccsal tudod a billentyűzetkiosztást és a konzol betűkészletét átállítani:

 `# km` 

vagy használd a loadkeys parancsot:

 `# loadkeys _layout_` 

ahol _layout_ a billentyűzeted kiosztása, mint például `fr` vagy `be-latin1`

#### Dokumentáció

A telepítési útmutató kényelmesen elérhető az általad bootolt live rendszeren is. Ehhez, válts át tty2-re (virtuális konzol #2) az `Alt+F2` billentyűk lenyomásával, majd jelentkezz be mint rendszergazda (root). Ez után használd a `less` parancsot, hogy lapozható formában érd el a dokumentációt:

 `# less /usr/share/aif/docs/official_installation_guide_en` 

Válts vissza tty1-re az `Alt+F1` billentyűzetekkel, hogy folytasd a telepítést. Bármikor visszaválthatsz tty2-re (`Alt+F2`) a telepítés folyamán, ha szükséged van az útmutató segítségére.

**Tip:** Ne feledd, hogy a hivatalos telepítési útmutató csak az alaprendszer feltelepítését és beállítását tartalmazza. Ha a telepítéssel végeztél, erősen ajánlott a wiki oldalon a telepítés utáni teendőket és az egyéb hasznos beállítások leírását véginézni.

**[Útmutató kezdőknek](/index.php/Beginners%27_Guide_(Magyar) "Beginners' Guide (Magyar)")**

* * *

[Előszó](/index.php/Beginners%27_Guide/Preface_(Magyar) "Beginners' Guide/Preface (Magyar)") >> **Előkészületek** >> [Telepítés](/index.php/Beginners%27_Guide/Installation_(Magyar) "Beginners' Guide/Installation (Magyar)") >> [Telepítés után](/index.php/Beginners%27_Guide/Post-Installation_(Magyar) "Beginners' Guide/Post-Installation (Magyar)") >> [Extra/Függelék](/index.php?title=Beginners%27_Guide/Extra_(Magyar)&action=edit&redlink=1 "Beginners' Guide/Extra (Magyar) (page does not exist)")