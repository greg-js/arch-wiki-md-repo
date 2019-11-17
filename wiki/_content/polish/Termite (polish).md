[Termite](https://www.github.com/thestinger/termite) jest minimalnym [emulatorem terminala](/index.php/Category:Terminal_emulators "Category:Terminal emulators") opartym na [bibliotece VTE](https://developer.gnome.org/vte/unstable/). Jest to program "modalny", podobnym do [Vima](/index.php/Vim "Vim"), z trybem wstawiania i trybem wyboru, w którym klawisze mają różne funkcje.

Plik konfiguracyjny umożliwia zmianę kolorów i ustawienia kilkanaście opcji. Termite obsługuje przezroczystość wraz z 256 kolorami i prawdziwymi paletami kolorów (16 milionów kolorów). Termite ma podobny wygląd do terminala [urxvt](/index.php/Urxvt "Urxvt").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacja](#Instalacja)
*   [2 Używanie](#Używanie)
*   [3 Konfiguracja](#Konfiguracja)
    *   [3.1 Czcionka](#Czcionka)
    *   [3.2 Kolory](#Kolory)
*   [4 Transparency](#Transparency)
*   [5 Rozwiązywanie problemów](#Rozwiązywanie_problemów)
    *   [5.1 Ctrl+Shift+t](#Ctrl+Shift+t)
    *   [5.2 Błąd zdalnego SSH](#Błąd_zdalnego_SSH)
*   [6 Zobacz również](#Zobacz_również)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [termite](https://www.archlinux.org/packages/?name=termite) lub [termite-git](https://aur.archlinux.org/packages/termite-git/). Jeżeli korzystasz z tilling window managera dla Waylanda możesz zainstalować [termite-nocsd](https://aur.archlinux.org/packages/termite-nocsd/) żeby pozbyć się client side decoration.

## Używanie

Termite domyślnie uruchamia się w trybie wstawiania. Tekst może byc zaznaczony za pomocą myszki lub za pomocą klawiszy trybu wyboru. W trybie wstawiania, `Ctrl+Shift+c` służy do kopiowania zaznaczonego tekstu do schowka [X](/index.php/X "X"), `Ctrl+Shift+v` do wklejenia. `Ctrl+Tab` rozpoczyna dokończenie przewijania, a `Ctrl+Shift+Góra`/`Ctrl+Shift+Dół` przewija ekran w górę lub w dół.

`Ctrl+Shift+Spacja` wchodzi w tryb wyboru, podobny do normalnego trybu vima. Wiele komend jest zapożyczonych z [Vima](/index.php/Vim "Vim"), na przykład `v` dla trybu wizualnego, `Shift+v` dla trybu linii wizualnej, `Ctrl+v` dla bloku wizualnego, `y`, aby skopiować ("yank") wybrany tekst, `/` i `?` do wyszukiwania, `w`, `b`, `^`, `$` dla ruchu i `Escape`, aby wrócić do trybu domyślnego trubu wstawiania.

## Konfiguracja

Termite szuka plików konfiguracyjnych w `$XDG_CONFIG_HOME/termite/config`, `~/.config/termite/config`, `$XDG_CONFIG_DIRS/termite/config` i `/etc/xdg/termite.cfg`. Plik konfiguracyjny służy do zmiany opcji, takich jak czcionka, kolory, wskazówki dotyczące okien itp. Składnia pliku konfiguracyjnego została zainspirowana przez [specyfikację wpisów pulpitu XDG](https://specifications.freedesktop.org/desktop-entry-spec/latest/) plików [.desktop](/index.php/.desktop ".desktop") (zainspirowane plikami z Microsoft Windows ".ini") z trzema sekcjami: *[options]*, *[colors]* i *[hints]*.

Aby rozpocząć dostosowywanie termite'a, najpierw skopiuj podstawowy plik przykładowy do swojego katalogu domowego:

```
 cp /etc/xdg/termite/config ~/.config/termite/config

```

### Czcionka

Czcionki są określone w formacie `font=<nazwa_czcionki> <wielkość_czcionki>` w sekcji *[options]*. `<nazwa_czcionki>` jest określona zgodnie z [fontconfig](/index.php/Fontconfig "Fontconfig"), a nie [Xft](/index.php/X_Logical_Font_Description "X Logical Font Description"). Użyj `fc-list`, aby zobaczyć, które czcionki są dostępne w systemie (zobacz także [Font configuration#Font paths](/index.php/Font_configuration#Font_paths "Font configuration")).

 `~/.config/termite/config` 
```
[options]
font = Monospace 9
font = xos4 Terminus 12px
font = Droid Sans Mono 8
```

### Kolory

Kolory składają się z 24-bitowej wartości szesnastkowej (np. `#007bff`) lub wektora rgba (np. `rgba (0, 123, 255, 0.5)`). Prawidłowe właściwości kolorów to `foreground`, `foreground_bold`, `foreground_dim`, `background`, `cursor` i `colorN` (gdzie N jest liczbą całkowitą od zera do 254, używane do przypisania 24-bitowej wartości koloru do koloru N terminala).

 `~/.config/termite/config` 
```
[colors]
background = #070723
foreground = #b4b5d3
```

Niesamowita kolekcja schematów kolorów termite znajduje się tutaj: [https://github.com/khamer/base16-termite/tree/master/themes](https://github.com/khamer/base16-termite/tree/master/themes)

## Transparency

Termite od wersji 9, obsługuje prawdziwą przezroczystość za pomocą definicji kolorów, które określają wartość kanału alfa [[1]](https://github.com/thestinger/termite/issues/191). Wymaga jednak to uruchomienia kompozytora, na przykład [Compton](/index.php/Compton "Compton"). Większość kompozytorów nie wymaga specjalnej konfiguracji, aby Termite używał przezroczystości.

 `~/.config/termite/config` 
```
[colors]
background = rgba(7, 7, 35, 0.8)
```

**Note:** W [i3](/index.php/I3 "I3"), w zestakowanym/kart układzie, pokazuje wszystkie okna "ułożone" jeden na drugim, w kolejności, w jakiej znajdowały się ostatnio na pierwszym planie, zamiast pokazywania pulpitu (okno główne) bezpośrednio za Termite. Wynika to z ponownego ustawiania okna i3 zamiast ukrywania niewidocznych okien w trybie kafelkowania. Możesz skonfigurować swojego kompozytora, aby okno z `_NET_WM_STATE=_NET_WM_STATE_HIDDEN` było w pełni przezroczyste, aby rozwiązać ten problem. Na przykład w przypadku użycia Comptona `~/.compton.conf` 
```
opacity-rule = [
  "0:_NET_WM_STATE@:32a *= '_NET_WM_STATE_HIDDEN'"
];
```

## Rozwiązywanie problemów

### Ctrl+Shift+t

Jeśli otwarcie nowej karty przez `Ctrl+Shift+t` kończy się niepowodzeniem z `no directory uri set`, uruchom `/etc/profile.d/vte.sh`. Zobacz [GNOME/Tips and tricks#New terminals adopt current directory](/index.php/GNOME/Tips_and_tricks#New_terminals_adopt_current_directory "GNOME/Tips and tricks").

Jeśli nadal to się nie udaje, upewnij się, że [nazwa hosta](/index.php/HOSTNAME "HOSTNAME") jest poprawna. Zobacz [hostname(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7).

### Błąd zdalnego SSH

Kiedy Termite używa zdalnego połączenia SSH, czasami pojawia się błąd: *Error opening terminal: xterm-termite.* lub *Open terminal failed: missing or unsuitable terminal: xterm-termite.'*

Ten błąd może wystąpić podczas próby edycji pliku za pomocą vima lub nano. Aby rozwiązać ten problem, należy wykonać to polecenie w systemie zdalnym:

```
$ export TERM=xterm-color

```

Alternatywnie postępuj zgodnie z instrukcjami na [GitHub](https://github.com/thestinger/termite#terminfo) Termite'a, jak poniżej. Umożliwi to korzystanie z wszystkich funkcji termite'a podczas korzystania z SSH, podczas gdy powyższe może nie umożliwić tego.[[2]](https://github.com/thestinger/termite/issues/229#issuecomment-250659169)

Zainstaluj [termite-terminfo](https://www.archlinux.org/packages/?name=termite-terminfo) na swoim zdalnym systemie.

Na Arch Linuxie:

```
pacman -S termite-terminfo

```

Na innych systemach:

```
wget [https://raw.githubusercontent.com/thestinger/termite/master/termite.terminfo](https://raw.githubusercontent.com/thestinger/termite/master/termite.terminfo)
tic -x termite.terminfo

```

## Zobacz również

*   [README Termite'a na GitHubie](https://github.com/thestinger/termite/blob/master/README.rst)