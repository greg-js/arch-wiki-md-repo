[Dolphin](https://www.kde.org/applications/system/dolphin/) je výchozí správce souborů [KDE](/index.php/KDE "KDE").

## Contents

*   [1 Instalace](#Instalace)
    *   [1.1 Porovnání souborů](#Porovn.C3.A1n.C3.AD_soubor.C5.AF)
    *   [1.2 Náhledy souborů](#N.C3.A1hledy_soubor.C5.AF)
*   [2 Použití](#Pou.C5.BEit.C3.AD)
    *   [2.1 Otvíraný Terminál](#Otv.C3.ADran.C3.BD_Termin.C3.A1l)
    *   [2.2 KIO Slaves](#KIO_Slaves)
*   [3 Viz také](#Viz_tak.C3.A9)

## Instalace

Nainstalujte balíček [dolphin](https://www.archlinux.org/packages/?name=dolphin).

```
# pacman -S dolphin

```

Pro podporu správy verzí a podporu [Dropbox](/index.php/Dropbox "Dropbox") nainstalujte [dolphin-plugins](https://www.archlinux.org/packages/?name=dolphin-plugins).

```
# pacman -S dolphin-plugins

```

### Porovnání souborů

Dialog "Porovnat soubory" závisí na balíčku [kompare](https://www.archlinux.org/packages/?name=kompare). Případně můžete porovnávat soubory v jakémkoli nástroji diff (například meld) výběrem dvou souborů, klepnutím pravým tlačítkem myši, výběrem otevřít pomocí a potom volbou nástroje diff.

### Náhledy souborů

*   [kdegraphics-thumbnailers](https://www.archlinux.org/packages/?name=kdegraphics-thumbnailers): Soubory obrázků
*   [kimageformats](https://www.archlinux.org/packages/?name=kimageformats): Soubory Gimpu xcf
*   [kdesdk-thumbnailers](https://www.archlinux.org/packages/?name=kdesdk-thumbnailers): Pluginy pro náhledy systemu
*   [ffmpegthumbs](https://www.archlinux.org/packages/?name=ffmpegthumbs): Video soubory (založeno na ffmpeg)
*   [raw-thumbnailer](https://www.archlinux.org/packages/?name=raw-thumbnailer): `.raw` soubory
*   [taglib](https://www.archlinux.org/packages/?name=taglib) : Audio soubory
*   [kde-thumbnailer-apk](https://aur.archlinux.org/packages/kde-thumbnailer-apk/): Balíčky aplikací pro Android - aap - **A**ndroid **a**pplication **p**ackage
*   [kde-thumbnailer-blender](https://aur.archlinux.org/packages/kde-thumbnailer-blender/): Soubory aplikace Blender
*   [kde-thumbnailer-epub](https://aur.archlinux.org/packages/kde-thumbnailer-epub/): Soubory electronických knih

## Použití

### Otvíraný Terminál

Dolphin a další aplikace KDE ve výchozím nastavení používají [konsole](https://www.archlinux.org/packages/?name=konsole). Chcete-li změnit výchozí emulátor terminálu, spusťte příkaz `kcmshell5 componentchooser` a zvolte *Emulátor terminálu > Použít jiný terminálový program*.

### KIO Slaves

Dolphin používá pro přístup k síti, koši a další funkcím *KIO slaves*, na rozdíl od správců souborů [GTK+](/index.php/GTK%2B "GTK+"), kteří používají [GVFS](/index.php/GVFS "GVFS"). Dostupné protokoly jsou zobrazeny v liště Místa (editovatelný režim)[[1]](https://docs.kde.org/stable/en/applications/dolphin/location-bar.html#location-bar-editable). Chcete-li je rychle označit, klikněte pravým tlačítkem myši na pracovní plochu a vyberte možnost "Přidat do míst".

## Viz také

*   [Wikipedia:Dolphin (file manager)](https://en.wikipedia.org/wiki/Dolphin_(file_manager) "wikipedia:Dolphin (file manager)")
*   [KDE userbase: Dolphin](https://userbase.kde.org/Dolphin)
*   [Dolphin Handbook](https://docs.kde.org/stable/en/applications/dolphin/index.html)