Dle [Wikipedia](https://en.wikipedia.org/wiki/Kodek "wikipedia:Kodek") jde o zařízení nebo počítačový program, který dokáže transformovat datový proud (stream) nebo signál.

Kodeky obecně využívají multimediální aplikace pro kódování nebo dekódování zvukových nebo video streamů. Aby bylo možné přehrávat kódované streamy, musí uživatel zajistit, že je nainstalován vhodný kodek.

## Contents

*   [1 Kodeky Gstreamer](#Kodeky_Gstreamer)
*   [2 Užitečné multimediální přehrávače](#Užitečné_multimediální_přehrávače)
    *   [2.1 VLC](#VLC)
    *   [2.2 MPlayer](#MPlayer)
*   [3 Další zdroje](#Další_zdroje)
    *   [3.1 codecs-all z archlinuxfr](#codecs-all_z_archlinuxfr)
    *   [3.2 Přehrávání videí s posledními kodeky RealMedia (RV10...RV40)](#Přehrávání_videí_s_posledními_kodeky_RealMedia_(RV10...RV40))

## Kodeky Gstreamer

Pokud shledáte, že nemůžete přehrávat běžné zvukové (jako třeba MP3) nebo video soubory, možná nemáte nainstalované správné kodeky pro jejich přehrávání. Multimediální přehrávěče používající backend **gstreamer** (jako třeba Totem) budou schopny přehrát většinu multimediálních souborů po instalaci těchto kodeků:

```
# pacman -S gstreamer0.10-bad gstreamer0.10-ugly gstreamer0.10-ffmpeg gstreamer0.10-ugly-plugins

```

V případě, že chcete nainstalovat **všechny** kodeky pro Gstreamer, můžete použít následující příkaz (za předpokladu, že máte nainstalován awk):

```
# pacman -S `pacman -Ss gstreamer | grep -e '^extra/gstreamer0.10' | awk '{print $1}'`

```

**Note:** Balík **codecs** je zastaralý a není nadále potřeba!

## Užitečné multimediální přehrávače

### VLC

Stále můžete shledat, že některé soubory (hlavně video soubory Windows) se v Totemu nepřehrají správně. **VLC** je víceúčelový multimediální přehrávač, jenž má mnoho vlastních kodeků a může ty záludné video soubory zvládnout, stejně jako DVD filmy s menu.

```
# pacman -S vlc

```

### MPlayer

Mplayer též přehraje mnoho souborů. Zjišťuji, že občas přehraje věci, které se nepřehrají ve VLC.

```
# pacman -S mplayer

```

Je zde také užitečný plugin, který integruje mplayer do webových prohlížečů. Nainstalujete ho pomocí:

```
# pacman -S mplayer-plugin

```

## Další zdroje

### codecs-all z archlinuxfr

Repozitář archlinuxfr poskytuje balíček codecs-all, který se zdá kompletnější než běžný balíček codecs z oficiálních repozitářů Arch Linuxu.

### Přehrávání videí s posledními kodeky RealMedia (RV10...RV40)

Přehrávání videí zakódovaných posledními kodeky RealMedia vám pravděpodobně selže, hlavně když přicházejí v exotických formátech jako kontejner Matroska kontejnery (to jest video soubory *.mkv). FFmpeg podporuje RV kodeky nativně, jelikož jsou tyto kodeky postupně reverse-engineerovány. Můžete zkusit nainstalovat ffmpegs-svn z AUR.

Další možnost je jít na [http://www.mplayerhq.hu/design7/dload.html](http://www.mplayerhq.hu/design7/dload.html). Někde vprostřed stránky můžete stáhnout balíčky s binárními kodeky. Zvolte vhodný pro svoji architekturu a stáhněte jej (v čase psaní tohoto článku verze 20071007 obsahuje cook.so, drvc.so a sipr.so). Rozbalte soubory a - jako root - je zkopírujte do /usr/lib/codecs. Pravděpodobně budete muset nechat přepsat stávající soubory.