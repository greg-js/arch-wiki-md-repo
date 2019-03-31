[lemonbar](https://github.com/LemonBoy/bar) jest lekkim paskiem opartym na [XCB](https://xcb.freedesktop.org/). Umożliwia on modyfikację koloru pierwszoplanowego (czcionki) razem ze zmianą koloru tła i wyrównania tekstu. Dostępnie jest również pełne wsparcie UTF-8 oraz zmniejszony memory footprint.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
*   [3 Użycie](#Użycie)
    *   [3.1 Kolory](#Kolory)
    *   [3.2 Wyrównanie tekstu](#Wyrównanie_tekstu)
    *   [3.3 Przykłady](#Przykłady)
    *   [3.4 Czcionki XFT](#Czcionki_XFT)
        *   [3.4.1 Ikony Font Awesome](#Ikony_Font_Awesome)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/).

## Konfiguracja

Konfiguracja lemonbar jest w całkowicie tworzona za pomocą `screenrc`'owego formatu tekstu i opcji linii komend. W starszych wersjach robiło się to poprzez edycję plików przed kompilowaniem.

Na stronie `man` aplikacji dostępny jest krótki przegląd opcji konfiguracji.

## Użycie

`lemonbar` nie wypisuje żadnych informacji sam z siebie. Żeby uzyskać w nim tekst trzeba stworzyć [potok](https://pl.wikipedia.org/wiki/Potok_(Unix)) (pipe). Poniższy przykład wypisze "Witaj Świecie!" w terminalu, aby wyświetlić komunikat na pasku uruchom `/droga/do/przykładu.sh | lemonbar`.

```
#!/bin/bash

# Wypisanie tekstu
echo "Witaj Świecie!"

```

Jeżeli chcesz, żeby tekst w lemonbarze był aktualizowany przez skrypt, musisz dodać opcję `-p` (n.p.: `/droga/do/przykładu.sh | lemonbar -p`). Zapobiega to wyłączaniu lemonbara po tym, jak standardowe wyjście zostaje zamknięte.

#### Kolory

`lemonbar` używa poniższych komend, żeby pokolorować tekst, tło i pod/nadkreślenie. Kolory mogą być ustalone za pomocą formatów `#RRGGBB`, `#AARRGGBB` (z kanałem alfa; kompozytor musi być włączony), lub `#RGB`.

Specjalny kolor `-` wskazuje na kolor domyślny (który jest ustawiany za pomocą opcji linii komend, domyślnie jest to biały tekst z czarnym tłem).

| Command | Meaning |
| `%{F*kolor*}` | Użyj *kolor* jako kolor czcionki/pierwszoplanowy |
| `%{B*kolor*}` | Użyj *kolor* jako kolor tła |
| `%{U*kolor*}` | Użyj *kolor* jako kolor pod/nadkreślenia tekstu |

#### Wyrównanie tekstu

`lemonbar` wspiera wyrównanie tekstu. Używa poniższych komend aby to osiągnąć.

| Command | Meaning |
| `%{l}` | Wyrównuje tekst to lewej |
| `%{c}` | Centruje tekst |
| `%{r}` | Wyrównuje tekst do prawej |

#### Przykłady

Poniższy przykład wypisuje datę i czas na środku paska, kolor czcionki to `żółty`, a kolor tła to `niebieski`.

`%{F-}` i `%{B-}` przywracają odpowiednio kolor czcionki i tła do ustawień domyślnych.

 `przykład.sh` 
```
#!/usr/bin/bash

# Definiowanie Zegara
Clock() {
        DATETIME=$(date "+%a %b %d, %T")

        echo -n "$DATETIME"
}

# Wypisanie Zegara
while true; do
        echo "%{c}%{F#FFFF00}%{B#0000FF} $(Clock) %{F-}%{B-}"
        sleep 1
done

```

Kolejny przykład pokazuje poziom naładowania baterii. Do użycia tego skryptu trzeba zainstalować [acpi](https://www.archlinux.org/packages/?name=acpi).

 `przykład.sh` 
```
#!/usr/bin/bash

#Definiowanie baterii
Battery() {
        BATPERC=$(acpi --battery | cut -d, -f2)
        echo "$BATPERC"
}

# Wypisywanie stanu naładowania
while true; do
        echo "%{r}$(Battery)"
        sleep 1;
done

```

#### Czcionki XFT

Domyślna wersja lemonbara nie wspiera czcionek XFT. Żeby użyć czcionek XFT trzeba zainstalować [lemonbar-xft-git](https://aur.archlinux.org/packages/lemonbar-xft-git/), który zastąpi [lemonbar-git](https://aur.archlinux.org/packages/lemonbar-git/).

Żeby użyć inną czcionkę w lemonbarze musisz dodać opcję `-f` do lemobara (n.p. `lemonbar -f "Roboto Medium"`).

##### Ikony Font Awesome

Z wsparciem XFT, możesz również dodać [ikony font-awesome](http://fontawesome.io/) do swojego paska. Musisz zainstalować [ttf-font-awesome](https://www.archlinux.org/packages/?name=ttf-font-awesome) przed użyciem ikon i dodać opcję `-f "Font Awesome"` do lemonbara. Proszę zapamiętaj, że musisz dodać jeszcze jedną czcionkę (n.p. `-f "Roboto Medium"`), żeby użyć znaki inne niż ikony z Font Awesome.

Przed dodaniem ikony do lemonbara musisz zobaczyć jej [id w unicodzie](http://fontawesome.io/icons/) i użyć je jako tekst. Poniżej pokazany jest skrypt, który wypisuje ikonę z id `f242`.

 `fontawesome.sh` 
```
#!/usr/bin/bash
echo -e "\uf242 Battery: 0"

```

Zauważ flagę `-e` w `echo`, jest ona niezbędna, żeby poprawnie wyświetlić symbol.

I odpowiadająca komenda lemonbara: `lemonbar -f "Roboto Medium" -f "Font Awesome"`