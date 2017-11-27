Related articles

*   [ATI](/index.php/ATI "ATI")
*   [NVIDIA](/index.php/NVIDIA "NVIDIA")
*   [Xorg](/index.php/Xorg "Xorg")

Mivel az Intel készít és támogat is nyílt forráskodú drivereket, így az Intel grafikus kártyák lényegében "plug-and-play" (bonyolultabb beállítási igények nélkül) működnek.

**Note:** Parancssorban való, [X](/index.php/X "X") kiszolgáló nélküli, használathoz ezt nézd meg: [Uvesafb](/index.php/Uvesafb "Uvesafb").

## Contents

*   [1 Típusok](#T.C3.ADpusok)
*   [2 Driver](#Driver)
*   [3 Telepítés](#Telep.C3.ADt.C3.A9s)
*   [4 Beállítás](#Be.C3.A1ll.C3.ADt.C3.A1s)
*   [5 KMS (Kernel Mode Setting)](#KMS_.28Kernel_Mode_Setting.29)
    *   [5.1 Lásd még](#L.C3.A1sd_m.C3.A9g)
*   [6 Tippek és trükkök](#Tippek_.C3.A9s_tr.C3.BCkk.C3.B6k)
    *   [6.1 Átméretezés módjának beállítása](#.C3.81tm.C3.A9retez.C3.A9s_m.C3.B3dj.C3.A1nak_be.C3.A1ll.C3.ADt.C3.A1sa)
    *   [6.2 KMS probléma: a terminál nem tölti ki a képernyőt](#KMS_probl.C3.A9ma:_a_termin.C3.A1l_nem_t.C3.B6lti_ki_a_k.C3.A9perny.C5.91t)
*   [7 Támogatott hardverek](#T.C3.A1mogatott_hardverek)
*   [8 Hibaelhárítás](#Hibaelh.C3.A1r.C3.ADt.C3.A1s)
    *   [8.1 A Glxgears alacsony teljesítményt mutat](#A_Glxgears_alacsony_teljes.C3.ADtm.C3.A9nyt_mutat)
    *   [8.2 Sötét képernyő a rendszer töltődése során, "Loading modules" után](#S.C3.B6t.C3.A9t_k.C3.A9perny.C5.91_a_rendszer_t.C3.B6lt.C5.91d.C3.A9se_sor.C3.A1n.2C_.22Loading_modules.22_ut.C3.A1n)
    *   [8.3 A laptophoz csatlakoztatott külső monitor 30 másodpercenként elsötétül](#A_laptophoz_csatlakoztatott_k.C3.BCls.C5.91_monitor_30_m.C3.A1sodpercenk.C3.A9nt_els.C3.B6t.C3.A9t.C3.BCl)

### Típusok

Az emberek gyakran azt hiszik, hogy az "Intel 945G" és "Intel GMA 945" nevek ugyanazt a grafikus chipet jelölik, csak nevükben különböznek. Valójában a második nem is létezik. Az Intel a "GMA" szót a grafikus processzor (GPU) jelölésére használja, minden más az alaplap chipkészletét jelenti: "915G", "945GM", "G965" vagy "G45".

A leggyakoribb GPU-k és a megfelelő alaplap chipkészletek:

*   Intel GMA 900 (910, 915)
*   Intel GMA 950 (945)

Az "i810" chipkészlet (ismételten: az alaplapot, nem a GPU-t jelöli) egy nagyon régi típus, jóval a GMA intergált grafikus kártyákat támogató 9xx sorozat előtt gyártották. Ehhez hasonlóan az újabb 910, 915 és 945 jelölésű chipek neve előtt is szerepelhet "i" betű.

A típusok egy bővebb listájáért látogasd meg [ezt](https://en.wikipedia.org/wiki/Intel_GMA#Table_of_GMA_graphics_cores_and_chipsets "wikipedia:Intel GMA") az oldalt.

### Driver

*   xf86-video-intel

## Telepítés

Előfeltétel: [Xorg](/index.php/Xorg "Xorg")

```
# pacman -S xf86-video-intel

```

64-bites rendszer esetén a 32-bites programok grafikus gyorsításához szükség lehet a lib32-intel-dri telepítésére is.

## Beállítás

Semmilyen beállításra nincs szükség a Xorg működéséhez (nem kell 'xorg.conf' fájl).

Egyetlen dolog, amit már az elején meg kellett tenned, hogy hozzáadod a felhasználókat a kapcsolódó csoporthoz:

```
# gpasswd -a felhasználónév video

```

## KMS (Kernel Mode Setting)

A KMS-re az X futtatásához van szükség (Gnome, KDE, ...stb.).

A [KMS](/index.php/KMS "KMS")-t minden i915 DRM drivert-t használó Intel chipkészlet támogatja, sőt a 2.6.32 verziójú kernel óta ez az alapbeállítás. A xf86-video-intel 2.10 verziója óta a KMS használata [kötelező](https://www.archlinux.org/news/484/). A KMS alapvetően a kernel betöltődése után indul, de lehetőség van rá, hogy engedélyezzük, hogy már bootolás során elinduljon. Így már a boot során a natív felbontáson működhet a kijelző.

**Note:** KMS használata esetén /boot/grub/menu.lst fájlban kernel sorából törölni *kell* minden "vga" vagy "video" opciót

Adjuk hozzá `/etc/mkinitcpio.conf` fájl MODULES sorához a `intel_agp` és `i915` modulokat:

```
MODULES="**intel_agp i915**"

```

Ezután generáljuk le újra az initramfs-t:

```
# mkinitcpio -p kernel26

```

ahol a 26 a kernel jelenlegi **2**.**6**.xx verziójára utal.

Így általában működnie kell, amennyiben mégis problémák akadnak, megpróbálhatod úgy engedélyezni a KMS-t, hogy a /boot/grub/menu.lst kernel sorához hozzáadod a i915.modeset=1 opciót:

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /boot/vmlinuz26 root=/dev/... **i915.modeset=1**
initrd /boot/kernel26.img

```

győződj meg róla, hogy se "vga=...", se "nomodeset" nem szerepel a kernel sorban.

Ha bármikor le akard tiltani a KMS-t, csak át kell állítanod a `i915.modeset` opció értékét 0-ra a [GRUB](/index.php/GRUB "GRUB") `/boot/grub/menu.lst` fájljában. Nincs szükség másra.

```
# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /boot/vmlinuz26 root=/dev/... **i915.modeset=0**
initrd /boot/kernel26.img

```

a más videókártyáknál használatos "nomodeset" opció intel megfelelője az "i915.modeset=0".

A KMS másképp, a `menu.lst` szerkesztése nélkül is letiltható. Kapcsold be a számítógéped, és amikor megjelenik a GRUB, nyomj meg egy billentyűt a visszaszámlálás leállításához. Válaszd ki a menüből azt a kernelt, amit be akarsz tölteni (lehet, hogy már ki is van választva), majd nyomd le az "e" billentyűt a szerkesztéshez. Keresd ki azt a sort, ami a "kernel" szóval kezdődik, és nyomd le megint az "e"-t (ismét a szerkesztéshez). Így hozzá tudod adni a `i915.modeset` opciót, és 0 érték megadásával letilthatod a KMS-t. Nyomj entert, majd pedig "b"-t a bootoláshoz. Fontos, hogy ez csak ideiglenes módosítás, a következő indításkor újra engedélyezve lesz a KMS.

**Note:** Ha Intel GMA 950 kártya esetén a rendszer betöltődése során sötét képernyő fogad, akkor vagy telepítsd a 2.6.31.6-1 verziójú kernelt, vagy tiltsd le a modesetting-et egy kernel boot paraméterrel.

### Lásd még

*   [KMS](/index.php/KMS "KMS") — Arch wiki cikk a "kernel mode setting"-ről.
*   Arch Linux fórum: [Intel 945GM, Xorg, Kernel - performance](https://bbs.archlinux.org/viewtopic.php?pid=522665#p522665)

## Tippek és trükkök

### Átméretezés módjának beállítása

Ez néhány teljes képernyős alkalmazás esetén lehet hasznos.

```
xrandr --output LVDS1 --set PANEL_FITTING param

```

ahol <tt>param</tt> lehet:

*   <tt>center</tt>: a felbontás az eredeti marad, nem történik átméretezés
*   <tt>full</tt>: átméretezés történik úgy, hogy a teljes képernyőt kitöltse az alkalmazás
*   <tt>full_aspect</tt>: a lehető legnagyobbra növeli a felbontást a képarány megtartása mellett.

Ha az előző nem működik, megpróbálhatod ezt is:

```
xrandr --output LVDS1 --set "scaling mode" param

```

ahol a <tt>param</tt> a következők egyike: <tt>"Full"</tt>, <tt>"Center"</tt> vagy <tt>"Full aspect"</tt>.

### KMS probléma: a terminál nem tölti ki a képernyőt

A problémát valószínűleg az okozza, hogy a rendszer betöltődése során egy alacsony felbontású video port engedélyezésre kerül, és a terminál ehhez akalmazkodik. Javítása egyszerű, az i915 modul beállításával letiltjuk ezt a portot. Például add hozzá az alábbi opciót a `/boot/grub/menu.lst` fájl kernel sorához:

```
 video=SVIDEO-1:d

```

Ha ez nem működik, megpróbálhatsz másik video portot letiltani, például a TV1 vagy VGA1 elnevezésűt az SVIDEO-1 helyett.

## Támogatott hardverek

Itt megtalálod: [http://intellinuxgraphics.org/documentation.html](http://intellinuxgraphics.org/documentation.html).

## Hibaelhárítás

### A Glxgears alacsony teljesítményt mutat

Ha glxgears-t használsz a rendszered grafikus teljesítményének mérésre, akkor azt tapasztalhatod, hogy az alacsony (**60 FPS** körüli) értékeket mutat:

```
...
311 frames in 5.0 seconds = 61.973 FPS
311 frames in 5.0 seconds = 62.064 FPS
311 frames in 5.0 seconds = 62.026 FPS
...

```

Ennek oka nem az, hogy a rendszer ennyire kis teljesítményre lenne képes, hanem az, hogy grafikus rendszer által használt érték a **VSync**, azaz a kijelző képfrissítési gyorsasága.

**Note:** A glxgears nem olyan tesztprogram, mellyel rendszerek egymáshoz viszonyított teljesítményét lehetne mérni.

### Sötét képernyő a rendszer töltődése során, "Loading modules" után

Ha a KMS-t a korábban leírt később induló módban használod, és a rendszer töltődésekor a képernyő elsötétül a "Loading modules" szakasznál, akkor segíthet ha hozzáadod az i915 és intel_agp modulokat az initramfs-hoz. Lásd korábban: [KMS](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel").

Egy alternatív megoldás lehet az is, ha hozzáadod a következő opciót a `/boot/grub/menu.lst` fájl kernel sorához:

```
video=SVIDEO-1:d

```

### A laptophoz csatlakoztatott külső monitor 30 másodpercenként elsötétül

Ha a laptopodban Intel HD grafikus kártya van és a külső LCD monitor 30 másodpercenként elsötétül, akkor a kernel és a videó driver frissítése segíthet, mivel az xf86-video-intel 2.14.0-1 és a kernel 2.6.37-5 verziójában ez a hiba már nem áll fenn.