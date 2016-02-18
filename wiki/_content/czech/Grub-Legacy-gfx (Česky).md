[grub-gfx](https://aur.archlinux.org/packages/grub-gfx/) je opatchovaná verze GRUBu s podporou obrázků na pozadí bootovací obrazovky.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Nastavení](#Nastaven.C3.AD)
*   [3 Splash images](#Splash_images)
*   [4 Problémy](#Probl.C3.A9my)
    *   [4.1 Černá obrazovka; žádné menu; blikající prompt](#.C4.8Cern.C3.A1_obrazovka.3B_.C5.BE.C3.A1dn.C3.A9_menu.3B_blikaj.C3.ADc.C3.AD_prompt)
*   [5 Malá kolekce GRUB splash screens](#Mal.C3.A1_kolekce_GRUB_splash_screens)

## Instalace

[grub-gfx](https://aur.archlinux.org/packages/grub-gfx/) je komunitní balík, proto zkontroluj, jestli v `/etc/[pacman.conf](/index.php/Pacman "Pacman")` nemáš u `[community]` znak sharp # (# comment).

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Záloha konfiguračního souboru menu.lst. (Během instalace se záloha provede automaticky, takže jenom pro jistotu.)

```
# cp /boot/grub/menu.lst /boot/grub/menu.lst.bak

```

Stažení a instalace [grub-gfx](https://aur.archlinux.org/packages/grub-gfx/). Tento krok odstraní [grub](https://www.archlinux.org/packages/?name=grub), pokud jej používáté.

```
# pacman -S grub-gfx

```

Po uspěšné instalaci uprav `/boot/grub/menu.lst` podle `menu.lst.bak`. Pokud nechceš vše nastavovat znovu, můžeš použít svůj starý menu.lst (viz. dále).

## Nastavení

Jediná změna, která se provede je přidání rádky `splashimage`. Ve svém novém `/boot/grub/menu.lst` tedy můžeš vidět:

```
# general configuration:
timeout   5
default   0
color light-blue/black light-cyan/blue
splashimage /boot/grub/arch.xpm.gz

```

Pokud tedy chceš použít svůj starý `menu.lst`, přidej do něj řádek s splashimage.

**Note:** Pokud máš `/boot` v samotném oddílu, pak použij:
```
splashimage /grub/arch.xpm.gz

```

Nakonec je nutné přepsat současný GRUB bootloader. Pokud nevíš jak na to viz. [GRUB](/index.php/GRUB "GRUB"). Při standartní instalaci by stačilo něco takového:

```
# grub-install /dev/sda

```

## Splash images

Splash images musí mít rozlišení 640x480, typ souboru `.xpm.gz`, barevná hloubka 14 barev.

Přidej svůj nový splash image do (i.e. `/boot/grub/`), uprav svůj `menu.lst`. Po restartu by si měl vidět svůj novy splash image.

## Problémy

### Černá obrazovka; žádné menu; blikající prompt

Pokud něco takového nastane, system by měl i tak nabootovat. Zkontroluj cestu ke svému splash image v `menu.lst`. Pamatuj, že pokud máš pro `/boot` vzlášť vytvořený diskový oddíl, musí `splashimage` řádek vypadat takto: `splashimage /grub/arch.xpm.gz`. Dále musíš mít svůj splash screen ve správném adresáři.

## Malá kolekce GRUB splash screens

[Collection of GRUB splashes](http://www.schultz-net.dk/grub.html)