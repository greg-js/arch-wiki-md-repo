[surf](http://surf.suckless.org/) jest prostą przeglądarką internetową opartą na WebKit/GTK+. Jest w stanie wyświetlać strony internetowe i śledzić linki. Obsługuje protokół XEmbed, który umożliwia osadzenie jej w innej aplikacji. Ponadto można wskazać surf do innego URI, ustawiając jego XProperties.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
*   [3 Rozszerzone użycie](#Rozszerzone_u.C5.BCycie)
    *   [3.1 Poprawki i dodatkowe funkcje](#Poprawki_i_dodatkowe_funkcje)
    *   [3.2 Korzystanie z kart](#Korzystanie_z_kart)
*   [4 Rozwiązywanie problemów](#Rozwi.C4.85zywanie_problem.C3.B3w)
    *   [4.1 Niewyraźna czcionka na GitHubie](#Niewyra.C5.BAna_czcionka_na_GitHubie)
*   [5 Zobacz również](#Zobacz_r.C3.B3wnie.C5.BC)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [surf](https://www.archlinux.org/packages/?name=surf) lub [surf-git](https://aur.archlinux.org/packages/surf-git/) dla wersji "rozwojowej".

Opcjonalnie zainstaluj także pakiet [dmenu](https://www.archlinux.org/packages/?name=dmenu) dla paska adresu URL lub [rofi](https://www.archlinux.org/packages/?name=rofi), który jest kompatybily z dmenu.

## Konfiguracja

surf jest konfigurowany poprzez plik `config.h`. Przykładowy plik `config.def.h` jest dołączony do źródła i powinien być pomocny.

Podobnie jak w przypadku innych pakietów, takich jak [dwm](/index.php/Dwm "Dwm"), rozważ użycie Arch Build System ([ABS](/index.php/ABS "ABS")) i utrzymywanie własnego [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") ze źródłami i sumami md5 dla własnej konfiguracji i plików źródłowych.

## Rozszerzone użycie

### Poprawki i dodatkowe funkcje

Istnieje wiele stworzonych przez połeczność [poprawek](http://surf.suckless.org/patches/) dostępnych z oficjalnej witryny, które znacznie rozszerzają funkcjonalność surf. Poprawki można zastosować zarówno do źródłowego pliku `surf.c`, jak i pliku `config.h`:

```
$ cd src/surf-[version]/
$ patch -p1 < path/to/patch.diff

```

### Korzystanie z kart

Program [tabbed](https://www.archlinux.org/packages/?name=tabbed) może być użyty z surf żeby stworzyć prostą obsługe kart.

Podstawowa konfiguracja:

```
$ tabbed surf -e

```

Żeby osiągnąć efekt podobny do Firefoxa lub Chromium, gdy po zamknięciu ostatniej karty, przeglądarka sie zamyka, użyj zamiast tego:

```
$ tabbed -c surf -e

```

Zobacz stronę man aby uzyskać więcej informacji.

## Rozwiązywanie problemów

### Niewyraźna czcionka na GitHubie

Zainstaluj [ttf-freefont](https://www.archlinux.org/packages/?name=ttf-freefont) lub dodaj to do `~/.config/fontconfig/fonts.conf` wśrodku tagów fontconfig-tags:

```
 <selectfont>
   <rejectfont>
     <pattern>
       <patelt name="family">
         <string>Clean</string>
       </patelt>
     </pattern>
   </rejectfont>
 </selectfont>

```

## Zobacz również

*   [Oficjalna strona surf](http://surf.suckless.org/)
*   [dmenu](/index.php/Dmenu "Dmenu") - Prosty program uruchamiający aplikacje od twórców dwm
*   [Wątek o modyfikacji surf](https://bbs.archlinux.org/viewtopic.php?id=167804/)