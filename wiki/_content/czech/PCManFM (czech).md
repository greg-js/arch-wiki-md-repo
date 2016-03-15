**PCManFM** je "extrémně rychlý, odlehčený, přesto funkčně bohatý správce souborů, podporující tabbed browsing". Zdroj: [PCManFM na sourceforge](http://pcmanfm.sourceforge.net/). PCManFM je výchozím správcem souborů v prostředí [LXDE](/index.php/LXDE "LXDE") (Lightweight X11 Desktop Environment).

## Contents

*   [1 Instalace](#Instalace)
*   [2 Připojování jednotek](#P.C5.99ipojov.C3.A1n.C3.AD_jednotek)
    *   [2.1 PCManFM2 a gvfs](#PCManFM2_a_gvfs)
*   [3 Problémy](#Probl.C3.A9my)
    *   [3.1 Chybějící ikony](#Chyb.C4.9Bj.C3.ADc.C3.AD_ikony)
    *   [3.2 Podpora zápisu a čtení NTFS](#Podpora_z.C3.A1pisu_a_.C4.8Dten.C3.AD_NTFS)
    *   [3.3 gnome-open otevírá dialog "Hledat" místo obsahu adresáře](#gnome-open_otev.C3.ADr.C3.A1_dialog_.22Hledat.22_m.C3.ADsto_obsahu_adres.C3.A1.C5.99e)
*   [4 Dostupné verze](#Dostupn.C3.A9_verze)
    *   [4.1 PCManFM2](#PCManFM2)
    *   [4.2 PCManFM 0.5.2](#PCManFM_0.5.2)
    *   [4.3 PCManFM Mod](#PCManFM_Mod)

## Instalace

Instalaci provedete příkazem:

```
# pacman -S pcmanfm

```

Dále je nutné nainstalovat gamin (gamin je náhradou za FAM, který vyžaduje spouštění jako démon), který monitoruje např. změny v souborech a adresářích. Je vyžadován pro spuštění PCManFM.

```
# pacman -S gamin

```

PCManFM spustíte příkazem:

```
$ pcmanfm

```

## Připojování jednotek

PCManFM umožňuje připojovat a odpojovat jednotky - jak manuálně, tak automaticky. Tato možnost je nabízena jako alternativa k CLI nástrojům, např. [pmount](https://aur.archlinux.org/packages/pmount/). Existuje několik 'aktuálních' verzí PCManFM (viz níže), které umožňují zvolit různé způsoby připojování jednotek.

### PCManFM2 a gvfs

Pokud preferujete použít Gnome Virtual FileSystem, PCManFM2 to umožňuje. Postup je stejný, jako v předchozím případě, ale je nutné nainstalovat další balíčky:

*   [gvfs](/index.php/Gvfs "Gvfs") (a závislosti);
*   (volitelné) gvfs-smb, gvfs-obexftp, gvfs-afc atd., aby bylo možné využít další možnosti.

## Problémy

### Chybějící ikony

Pokud používáte správce oken v desktopovém prostředí a chybí vám ikony pro soubory a adresáře, nainstalujte si téma ikon:

```
# pacman -S tango-icon-theme

```

Editujte soubor `~/.gtkrc-2.0` **nebo** `/etc/gtk-2.0/gtkrc` a přidejte do něj následující řádek:

```
gtk-icon-theme-name = "Tango"

```

### Podpora zápisu a čtení NTFS

Nainstalujte balíček ntfs-3g:

```
# pacman -S ntfs-3g

```

### gnome-open otevírá dialog "Hledat" místo obsahu adresáře

Odstraňte nebo přejmenujte soubor `/usr/share/applications/pcmanfm-find.desktop`. Pokud používáte pcmanfm-mod z AUR, odstraňte nebo přejmenujte soubor `/usr/share/applications/pcmanfm-mod-find.desktop`.

## Dostupné verze

V současné době existuje několik verzí PCManFM:

### PCManFM2

Existuje jako balíček "pcmanfm" v repozitáři extra. Aktuální git testovací verze je dostupná v repozitáři AUR jako [pcmanfm-git](https://aur.archlinux.org/packages.php?ID=33601). Původní autor PCManFM (Hon Jen Yee aka PCMan) přepisuje originální program, nyní je v testovací fázi. Tato verze bývá občas označována jako "pcmanfm2", ačkoliv je ve verzi 0.9.7 RC1\. Tato verze používá GVFS pro připojování a správu jednotek. Další informace viz [LXDE fórum](http://forum.lxde.org/viewforum.php?f=22).

### PCManFM 0.5.2

Originální pcmanfm (verze 0.5.2, která je dostupná jako "pcmanfm-gtk220" v repozitáři AUR)). Vývoj je ukončen a program není nadále původním autorem udržován. Tato verze pro připojování používá HAL. Další informace viz [stránka projektu](http://pcmanfm.sourceforge.net/intro.html).

### PCManFM Mod

PCManFM-Mod přidává uživatelsky definovatelné příkazy, další možnosti a opravy chyb originální verze PCManFM 0.5.2\. Tato verze se instaluje jako "pcmanfm-mod" a běží nezávisle na jiných verzích PCManFM, nainstalovaných v systému. Tato verze je stále vyžadována některými uživateli z důvodu vyšší stability než novější vyvíjená verze 0.9.x, menších závislostí na Gnome a použítím démona HAL místo gnome-vfs. PCManFM-Mod je dostupný v [AUR jako pcmanfm-mod](https://aur.archlinux.org/packages.php?ID=34819) a nebo [pcmanfm-mod-prov](https://aur.archlinux.org/packages/pcmanfm-mod-prov/). Další informace viz [IgnorantGuru's Blog](http://igurublog.wordpress.com/downloads/mod-pcmanfm/).