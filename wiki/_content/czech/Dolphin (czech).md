[Dolphin](https://www.kde.org/applications/system/dolphin/) je výchozí správce souborů [KDE](/index.php/KDE "KDE").

## Contents

*   [1 Instalace](#Instalace)
    *   [1.1 Porovnání souborů](#Porovnání_souborů)
    *   [1.2 Náhledy souborů](#Náhledy_souborů)
*   [2 Použití](#Použití)
    *   [2.1 Otvíraný Terminál](#Otvíraný_Terminál)
    *   [2.2 KIO Slaves](#KIO_Slaves)
*   [3 Řešení problémů](#Řešení_problémů)
    *   [3.1 Názvy zařízení zobrazené jako "X GiB Harddrive"](#Názvy_zařízení_zobrazené_jako_"X_GiB_Harddrive")
    *   [3.2 Transparentní fonty](#Transparentní_fonty)
    *   [3.3 Nesprávné zobrazení barvy pozadí ve složce](#Nesprávné_zobrazení_barvy_pozadí_ve_složce)
*   [4 Další zdroje](#Další_zdroje)

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

Aktivace zobrazení náhledů požadovaného typu souboru: Nastavení > Nastavit 'Dolphin'... > Obecné > Náhledy.

## Použití

### Otvíraný Terminál

Dolphin a další aplikace KDE ve výchozím nastavení používají [konsole](https://www.archlinux.org/packages/?name=konsole). Chcete-li změnit výchozí emulátor terminálu, spusťte příkaz `kcmshell5 componentchooser` a zvolte *Emulátor terminálu > Použít jiný terminálový program*.

### KIO Slaves

Dolphin používá pro přístup k síti, koši a další funkcím *KIO slaves*, na rozdíl od správců souborů [GTK+](/index.php/GTK%2B "GTK+"), kteří používají [GVFS](/index.php/GVFS "GVFS"). Dostupné protokoly jsou zobrazeny v liště Místa (editovatelný režim)[[1]](https://docs.kde.org/stable/en/applications/dolphin/location-bar.html#location-bar-editable). Chcete-li je rychle označit, klikněte pravým tlačítkem myši na pracovní plochu a vyberte možnost "Přidat do míst".

## Řešení problémů

### Názvy zařízení zobrazené jako "X GiB Harddrive"

Vytvořte štítek souborového systému nebo štítek oddílu a Dolphin zobrazí tento štítek v seznamu zařízení místo velikosti. Viz. [Persistent block device naming#by-label](/index.php/Persistent_block_device_naming#by-label "Persistent block device naming").

### Transparentní fonty

Písmo v rámečcích pro výběr může být při použití stylu GTK+ Qt transparentní. Nativní styly Qt, jako například Cleanlooks a Oxygen, nejsou ovlivněny.

### Nesprávné zobrazení barvy pozadí ve složce

Když spustíte Dolphin jinde než v Plasma, je možné, že barva pozadí v podokně zobrazení složek neodpovídá systémovému tématu Qt. Důvodem je to, že Dolphin přečte barvu pozadí složky ze sekce `[Colors:View]` v `~/.config/kdeglobals`. Změňte tedy v následujícím řádku hodnoty R,G,B na ty které upřednostňujete:

 `~/.config/kdeglobals` 
```
...
[Colors:View]
BackgroundNormal=23,24,24
...

```

## Další zdroje

*   [Wikipedia:Dolphin (file manager)](https://en.wikipedia.org/wiki/Dolphin_(file_manager) "wikipedia:Dolphin (file manager)")
*   [KDE userbase: Dolphin](https://userbase.kde.org/Dolphin)
*   [Dolphin Handbook](https://docs.kde.org/stable/en/applications/dolphin/index.html)