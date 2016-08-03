[Ncmpcpp](http://unkart.ovh.org/ncmpcpp/) lub ncmpcpp jest klientem [mpd](/index.php/Mpd "Mpd") z interfejsem podobnym do tego w ncmpc, lecz dodatkowo posiada dużo ciekawych funkcji jak regex w wyszukiwarce, filtrowanie kolekcji, last.fm, sortowanie playlist, możliwość sortowanie w przeglądarce plików, edytor tagów, przeglądanie panelowe i inne.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Podstawowa konfiguracja](#Podstawowa_konfiguracja)
*   [3 Włączanie wizualizacji](#W.C5.82.C4.85czanie_wizualizacji)
*   [4 Podstawowe używanie](#Podstawowe_u.C5.BCywanie)
    *   [4.1 Uruchamianie ncmpcpp](#Uruchamianie_ncmpcpp)
    *   [4.2 Różne widoki](#R.C3.B3.C5.BCne_widoki)
    *   [4.3 Inne skróty](#Inne_skr.C3.B3ty)
    *   [4.4 Tryb odtwarzania](#Tryb_odtwarzania)
*   [5 Zmiana skrótów](#Zmiana_skr.C3.B3t.C3.B3w)
*   [6 Linki zewnętrzne](#Linki_zewn.C4.99trzne)

## Instalacja

[Zainstaluj](/index.php/Pacman_(Polski) "Pacman (Polski)") [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp) z [oficjalnego repozytorium](/index.php/Official_repositories "Official repositories").

## Podstawowa konfiguracja

Interfejs programu jest wysoce konfigurowalny. Edytuj `~/.ncmpcpp/config`, a jeżeli go nie masz, wpierw skopiuj domyślny:

```
cp /usr/share/doc/ncmpcpp/config ~/.ncmpcpp/config

```

Opcje:

*   **mpd_host** - powinno wskazywać na socket lub maszynę na której działa mpd, domyślnie: "localhost"
*   **mpd_port** - powinno wskazywać na port używany przez mpd, domyślnie: "6600"
*   **mpd_music_dir** - jeżeli mpd działa lokalnie, ten sam katalog który podałeś dla "music_directory" w pliku konfiguracyjnym mpd

Dla inspiracji, zobacz:

*   [Pliki konfiguracyjne i zrzuty ekranu na forum (en)](https://bbs.archlinux.org/viewtopic.php?id=66488)
*   [Zrzuty ekranu na stronie projektu (en)](http://unkart.ovh.org/ncmpcpp/screenshots.php)

## Włączanie wizualizacji

Dla działającej wizualizacji, musisz edytować plik konfiguracyjny mpd, by włączyć [szybką transformację Fouriera](https://pl.wikipedia.org/wiki/Szybka_transformacja_Fouriera), niezbędna dla wizualizacji:

```
audio_output {
    type                    "fifo"
    name                    "my_fifo"
    path                    "/tmp/mpd.fifo"
    format                  "44100:16:2"
}

```

Dodatkowo te linie muszą być ustawione w `~/.ncmpcpp/config`

```
visualizer_fifo_path = "/tmp/mpd.fifo"
visualizer_output_name = "my_fifo"
visualizer_sync_interval = "1"

```

I rodzaj wizualizacji do wyboru:

```
visualizer_type = "wave" (spectrum/wave)
visualizer_type = "spectrum" (spectrum/wave)

```

## Podstawowe używanie

### Uruchamianie ncmpcpp

Uruchom:

```
$ ncmpcpp

```

### Różne widoki

Częściowa lista widoków w ncmpcpp:

*   `0` - Zegar
*   `1` - Pomoc
*   `2` - Obecna playlista
*   `3` - Przeglądarka plików
*   `4` - Wyszukiwarka
*   `5` - Biblioteka
*   `6` - Edytor playlist
*   `7` - Edytor Tagów
*   `9` - Wizualizacja muzyki

### Inne skróty

*   `\` - Przełączanie między klasyczny a alternatywny widok
*   `#` - Wyświetlanie gęstości bitowej pliku
*   `i` - Pokaż informacje o pliku
*   `I` - Pokaż informacje o wykonawcy (zapisywane do `~/.ncmpcpp/artists/ARTIST.txt`)
*   `L` - Zmień stronę z bazą słów
*   `l` - Ściągnij słowa dla utworu, pokaż/ukryj

### Tryb odtwarzania

Zauważ, prawy górny róg w trybie alternatywnym:

```
1:40/4:16 1082 kbps                            ──┤ Criminal ├──                                       Vol: 98%
[playing]                             Disturbed - Indestructible (2008)                               **[-z-c--]**

```

I w trybie klasycznym:

```
─────────────────────────────────────────────────────────────────────────────────────────────────────────**[zc]**─

```

Odnoszą się do:

*   `r` - powtarzaj **[r-----]**
*   `z` - losowe **[-z----]**
*   `y` - tryb single **[--s---]**
*   `R` - tryb consume **[---c--]**
*   `x` - tryb crossfade **[----x-]**

Ostatni "-" jest aktywny tylko wtedy gdy użytkownik wymusi aktuializacje bazy danych klawiszem `u`.

## Zmiana skrótów

Lista klawiszy i ich funkcji dostępne jest pod klawiszem `1`. Użytkownik może je zmodyfikować, kopiując `/usr/share/doc/ncmpcpp/keys` do `~/.ncmpcpp/` i edytując.

**Note:** W nowszej wersji plik może znajdować się tutaj: `/usr/share/doc/ncmpcpp/bindings`

## Linki zewnętrzne

[dotshare.it configurations](http://dotshare.it/category/mpd/ncmpcpp/)