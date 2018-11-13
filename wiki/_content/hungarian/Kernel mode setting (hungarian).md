A Kernel Mode Setting (KMS) egy olyan eljárás, amivel a felbontás és színmélység a "kernel space"-ben állítható, és nem a "user-space"-ben.

A KMS engedélyezi a kijelző natív felbontását a framebufferben, és lehetővé teszi az azonnali parancssor váltásokat (tty). A KMS emellett elérhetővé teszi új technológiák alkalmazását (mint például a DRI2), ami így visszaszorítja az elavult eljárásokat és növeli a 3D-s teljesítményt. A "kernel-space"-ben alkalmazott energiatakarékosság is lehetővé válik.

2010 december 12\. óta az [intel](/index.php/Intel "Intel"), [nouveau](/index.php/Nouveau "Nouveau") és [radeon](/index.php/Radeon "Radeon") driverek minden chipkészlet esetében támogatják a KMS-t. Méghozzá automatikusan be van kapcsolva ezek esetében. A zárt-forrású [NVIDIA](/index.php/NVIDIA "NVIDIA") és [ATI Catalyst](/index.php/ATI_Catalyst "ATI Catalyst") driverek nem támogatják a KMS-t.

## Contents

*   [1 Háttér](#Háttér)
*   [2 Hibaelhárítás](#Hibaelhárítás)
    *   [2.1 Túl kicsik a betűk](#Túl_kicsik_a_betűk)
*   [3 Megjelenítési mód beállítása](#Megjelenítési_mód_beállítása)
*   [4 További források (angol)](#További_források_(angol))

## Háttér

Korábban a videókártya beállítása az X kiszolgáló feladata volt, így látványos grafikus effektusok virtuális terminálokban való megjelenítése nehézkes feladat volt. Emellett az X szerverről egy virtuális terminálra való váltáskor (Ctrl+Alt+F1) az X kiszolgálónak át kellett adnia a videó kártya vezérlését a kernelnek, ami így gyakran lassú, a képernyő villogásával járó folyamat volt. Hasonlóan "fájdalmas" volt az is, amikor a vezérlést visszakapta az X szerver (Ctrl+Alt+F7).

A Kernel Mode Setting-nek (KMS) köszönhetően a kernel képes a videókártya módjának vezérlésére, amivel látványos grafikus effektusok érhetők el a rendszer betöltése során, a virtuális parancssor és X kiszolgáló közti váltás gyors, és még sok más előny felsorolható.

A KMS egy új technológia, melyet még kísérleti stádiumban lévőnek tekintenek amiatt, hogy nem minden videókártya támogatja. Legtöbbjükkel azonban stabilan és jól használható, de mint minden új szoftvernek, ennek is lehetnek hibái.

## Hibaelhárítás

Fontos, hogy *bármilyen* beállítást is használsz, *mindig* töröld ki a "vga="-t a boot opciók közül, mivel ezek összeütközésbe kerülhetnek a KMS által szolgáltatott natív felbontással. Ki kell törölni minden "video=" részt is, mert olyan framebuffereket kapcsolnak be, amelyik összeütközésbe kerülhet a driverrel. Bármilyen más framebuffer drivert (mint például [uvesafb](/index.php/Uvesafb "Uvesafb")) le kell tiltani a KMS engedélyezése előtt.

### Túl kicsik a betűk

Látogasd meg a [changing the default font](/index.php/Fonts#Changing_the_default_font "Fonts") oldalt, mely leírja hogyan kell a parancssorod betűkészletét nagyobb méretűre cserélni. Az EXTRA tárolóban van egy Terminus elnevezésű betűkészlet, mely több méretben elérhető, nagyokban is.

## Megjelenítési mód beállítása

Az információk a [nouveau wiki](http://nouveau.freedesktop.org/wiki/KernelModeSetting) oldalról származnak:

A megjelenítési mód parancssorral (kernelben) érhető el. Sajnos a "video" elnevezésű parancssori opció nem valami jól dokumentált. Néhány töredékes információ az alábbi oldalakon található angolul:

*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/Documentation/fb/modedb.txt)
*   [http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c](http://cgit.freedesktop.org/nouveau/linux-2.6/tree/drivers/gpu/drm/drm_fb_helper.c)

A formátum: video=<conn>:<xres>x<yres>[M][R][-<bpp>][@<refresh>][i][m][eDd]

*   <conn>: csatlakozó, pl. DVI-I-1, a kernel log-ban nézz utána.
*   <xres> x <yres>: felbontás
*   M: CVT mód kiszámítása?
*   R: üresség csökkentése?
*   -<bpp>: színmélység
*   @<refresh>: frissítési frekvencia
*   i: "interlaced" ( nem-CVT mód)
*   m: határok?
*   e: kimenet "on"-ra kényszerítése
*   d: kimenet "off"-ra kényszerítése
*   D: digitális kimenet "on"-ra kényszerítése (pl. DVI-I csatlakozó)

A különböző kimenetek módjait a "video" opció többszöri beírásával lehet beállítani. Például a DVI kimenet 1024x768-as felbontásra, 85 Hz-es frissítési frekvenciára és a TV-out kikapcsolására való kényszerítése: video=DVI-I-1:1024x768@85 video=TV-1:d

## További források (angol)

[Mode-setting at Wikipedia](https://en.wikipedia.org/wiki/Mode-setting "wikipedia:Mode-setting")