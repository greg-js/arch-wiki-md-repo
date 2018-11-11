Related articles

*   [List of applications/Other#Application launchers](/index.php/List_of_applications/Other#Application_launchers "List of applications/Other")

[Rofi](https://github.com/DaveDavenport/rofi) jest przełącznikiem okien, dialogiem uruchamiania, launcherem ssh i zamiennikiem [dmenu](/index.php/Dmenu "Dmenu"), który zaczął się jako klon [simpleswitcher](https://github.com/seanpringle/simpleswitcher), napisany przez [Sean Pringle](https://github.com/seanpringle), a następnie rozszerzony przez [Dave Davenport](https://github.com/DaveDavenport).

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
*   [3 Ikony programów](#Ikony_program.C3.B3w)
*   [4 Rofi jak zastępca dmenu](#Rofi_jak_zast.C4.99pca_dmenu)
*   [5 Niestandardowe motywy](#Niestandardowe_motywy)
    *   [5.1 Oficjalne motywy](#Oficjalne_motywy)

## Instalacja

[Zainstaluj](/index.php/Help:Reading#Installation_of_packages "Help:Reading") pakiet [rofi](https://www.archlinux.org/packages/?name=rofi).

## Konfiguracja

Obecnie są trzy metody ustawiania konfiguracji:

*   Lokalna konfiguracja. Normalnie, zależąc na XDG, w `~/.config/rofi/config`. Ten plik korzysta z formatu Xresources.
*   Xresources: Metoda przechowywania kluczowych wartości w Xserver.
*   Opcje wiersza poleceń

Więc

```
rofi -combi-modi window,drun,ssh -theme solarized -font "hack 10" -show combi

```

może być wyrażone w pliku konfiguracyjnym tak:

```
rofi.combi-modi:    window,drun,ssh
rofi.theme:         solarized
rofi.font:          hack 10
rofi.modi:          combi

```

Żeby zobaczyć pełną liste opcji które możesz włożyć do Xresources lub do twojego pliku konfigruacyjnego, uruchom `rofi -dump-Xresources`

**Note:** i3 użytkownicy powinni pamiętać, że umieszczanie przecinków w konfiguracji i3 może powodować problemy. Aby stworzyć skrót klawiszowy, aby uruchomić rofi, użyj pliku konfiguracyjnego lub zastąp przecinki na `#` , dla przykładu `rofi -combi-modi window#drun#ssh`

## Ikony programów

Żeby ikony programów się wyświetały rofi musi być włączone w trybie drun a nie run

```
rofi -show drun -show-icons

```

albo dodaj do pliku konfiguracyjnego i uruchom jako `rofi -show drun`

```
rofi.show-icons: true

```

Rofi automatycznie wybierze twój wybrany motyw ikon. Jeżeli chcesz ustawić ręcznie motyw ikon wpisz

```
rofi -show drun -show-icons -drun-icon-theme NAZWA_MOTYWU_IKON

```

## Rofi jak zastępca dmenu

Jeśli rofi zostanie wywołane jako dmenu (przez link symboliczny), rofi działa jak dmenu. Możesz zainstalować [rofi-dmenu](https://aur.archlinux.org/packages/rofi-dmenu/), które łączy dmenu z rofi. Wtedy programy, które wywołują dmenu ze skryptu (np. passmenu z [pass](/index.php/Pass "Pass")) będą używać rofi zamiast dmenu.

Jeżeli preferujesz wygląd dmenu, to przybliży wygląd do niego:

```
rofi -show run -modi run -location 1 -width 100 \
		 -lines 2 -line-margin 0 -line-padding 1 \
		 -separator-style none -font "mono 10" -columns 9 -bw 0 \
		 -disable-history \
		 -hide-scrollbar \
		 -color-window "#222222, #222222, #b1b4b3" \
		 -color-normal "#222222, #b1b4b3, #222222, #005577, #b1b4b3" \
		 -color-active "#222222, #b1b4b3, #222222, #007763, #b1b4b3" \
		 -color-urgent "#222222, #b1b4b3, #222222, #77003d, #b1b4b3" \
		 -kb-row-select "Tab" -kb-row-tab ""

```

## Niestandardowe motywy

Możesz przejrzeć i zaaplikować motyw dla rofi korzystając z

```
 rofi-theme-selector

```

Zmiany mogą być zapisane do twojego [pliku .Xresources](/index.php/X_resources "X resources") (wymaga pakietu [xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb)). Żeby zaaplikować zmiany załaduj ponownie plik .Xresources korzystając z `xrdb -load ~/.Xresources`

Możesz również samemu zmienić kolory rofi w pliku konfiguracyjnym w prosty sposób, dla przykładu

```
rofi.color-window: #070723, #007bff, #070723
rofi.color-normal: #070723, #007bff, #070723, #007bff, #070723
rofi.color-urgent: #070723, #007bff, #070723, #070723, #007bff
rofi.color-active: #070723, #007bff, #070723, #070723, #007bff

```

### Oficjalne motywy

Zobacz oficjalne repozytorium [rofi-themes](https://github.com/DaveDavenport/rofi-themes) na GitHubie dla listy niestandardowych motywów.

Pobierz jeden z motywów .rasi i przerzuć go do katalogu `~/.config/rofi/`. Potem załaduj motyw korzystając z wiersza poleceń

```
 rofi <opcje> -theme przykładowy-motyw

```

lub zamieść w swoim pliku konfiguracyjnym

```
 rofi.theme: przykładowy-motyw

```