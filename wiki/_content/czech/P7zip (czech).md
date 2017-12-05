p7zip je port příkazového řádku [7-Zip](https://en.wikipedia.org/wiki/7zip "wikipedia:7zip") pro systémy [POSIX](https://en.wikipedia.org/wiki/POSIX "wikipedia:POSIX") včetně Linuxu.

## Contents

*   [1 Instalace](#Instalace)
*   [2 Příklady](#P.C5.99.C3.ADklady)
*   [3 Rozdíly mezi binárními soubory 7z, 7za a 7zr](#Rozd.C3.ADly_mezi_bin.C3.A1rn.C3.ADmi_soubory_7z.2C_7za_a_7zr)
*   [4 Viz také](#Viz_tak.C3.A9)

## Instalace

Nainstalujte balíček [p7zip](https://www.archlinux.org/packages/?name=p7zip).

```
# pacman -S p7zip

```

Příkaz pro spuštění programu je následující:

```
$ 7z

```

## Příklady

Chcete-li extrahovat všechny soubory z archivu do aktuálního adresáře bez použití názvů adresářů, spusťte:

```
$ 7za e <nazev archivu>

```

Chcete-li extrahovat s plnými cestami, spusťte:

```
$ 7za x <archive name>

```

Chcete-li extrahovat do nového adresáře, spusťte:

```
$ 7za x -o<nazev slozky> <nazev archivu>

```

## Rozdíly mezi binárními soubory 7z, 7za a 7zr

*   7z používá zásuvné moduly pro zpracování archivů.
*   7za je samostatný spustitelný soubor. 7za zpracovává méně archivních formátů než 7z, ale nepotřebuje žádné další.
*   7zr je samostatný spustitelný soubor. 7zr zpracovává méně archivních formátů než 7z, ale nepotřebuje žádné další. 7zr je "odlehčená verze" 7za, která zpracovává pouze 7z archivy.

## Viz také

*   [Homepage.](http://p7zip.sourceforge.net/)
*   [7zip homepage.](http://www.7-zip.org/download.html)
*   [How to use 7zip on Linux command Line.](https://www.ibm.com/developerworks/community/blogs/6e6f6d1b-95c3-46df-8a26-b7efd8ee4b57/entry/how_to_use_7zip_on_linux_command_line144?lang=en)