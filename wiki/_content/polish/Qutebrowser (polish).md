[qutebrowser](https://github.com/qutebrowser/qutebrowser) jest przeglądarką skoncentrowaną na klawiaturze opierającą się na Pythonie i PyQt5.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Podstawowe użycie](#Podstawowe_użycie)
    *   [2.1 Konfiguracja użytkownika](#Konfiguracja_użytkownika)
        *   [2.1.1 Konfiguracja w Qutebrowser](#Konfiguracja_w_Qutebrowser)
    *   [2.2 Skróty klawiszowe](#Skróty_klawiszowe)
    *   [2.3 Odtwarzanie wideo](#Odtwarzanie_wideo)
*   [3 Porady i wskazówki](#Porady_i_wskazówki)
    *   [3.1 Włącz sprawdzanie pisowni](#Włącz_sprawdzanie_pisowni)
    *   [3.2 Zmniejsz odciski przeglądarki](#Zmniejsz_odciski_przeglądarki)
        *   [3.2.1 Ustaw pospolity agent użytkownika](#Ustaw_pospolity_agent_użytkownika)
        *   [3.2.2 Ustaw pospolity nagłówek HTTP_ACCEPT](#Ustaw_pospolity_nagłówek_HTTP_ACCEPT)
        *   [3.2.3 Wyłącz czytanie z płótna](#Wyłącz_czytanie_z_płótna)
        *   [3.2.4 Wyłączanie WebGL](#Wyłączanie_WebGL)
    *   [3.3 Zarządzanie sesjami jak w dwb](#Zarządzanie_sesjami_jak_w_dwb)
    *   [3.4 Blokowanie stron](#Blokowanie_stron)
*   [4 Zobacz również](#Zobacz_również)

## Instalacja

[Zainstaluj](/index.php/Zainstaluj "Zainstaluj") pakiet [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser) albo [qutebrowser-git](https://aur.archlinux.org/packages/qutebrowser-git/).

## Podstawowe użycie

Użyj `:` aby dostać się do wiersza poleceń. Możesz użyć `Tab` żeby autouzupełnić.

Przy pierwszym uruchomieniu qutebrowser, strona szybkiego startu się pojawia. Jest ona później dostępna przez `:help`. Zobacz [ściągawke](https://qutebrowser.org/img/cheatsheet-big.png) ze skrótami klawiszowymi.

### Konfiguracja użytkownika

Qutebrowser może być skonfigurowane przez interfejs, wiersz poleceń qutebrowser lub skrypt Pythona. Własna dokumentacja qutebrowsera wyjaśnia w detalach jak skonfigurować qutebrowser tymi trzema metodami. Żeby otworzyć strone pomocy, wpisz `:help` i potem wybierz `Configuring qutebrowser`.

Żeby odnaleść ścieżke gdzie plik konfiguracyjny jest zlokalizowany, otwórz specjalną strone `qute://version`. Na Arch Linuxie, ten plik zazwyczaj znajduje się w `$XDG_CONFIG_HOME/qutebrowser/`. Konfiguracja stworzona przez qutebrowser będzie znajdować się w `autoconfig.yml` (który nie powinien być dotykany przez użytkownika) a skrypt Pythona użytkownika znajduje się w `config.py`.

#### Konfiguracja w Qutebrowser

Żeby skonfigurować pojedyńczą rzecz możesz poprostu wpisać `:set` i imie nazwy elementu konfiguracji i nowej wartości do której chcesz ustawić. Na przykład możesz napisać

```
:set auto_save.session true

```

żeby otworzyć poprzednie karty kiedy otworzysz spowrotem qutebrowser.

Żeby otworzyć interfejs ustawien qutebrowsera, wpisz

```
:set

```

bez żadnych dodatkowych argumentów. Tam możesz zedytować różne ustawienia korzystająć z interfejsu. Kiedy skończysz napisz `:set` ponownie żeby zapisać swoją konfiguracje.

Dla przykładu pod `url.searchengines` możesz ustawić swoją wyszukiwarke. Jeśli jeszcze nie zmieniłeś tego ustawienia wcześniej to powinno ono wyglądać tak

```
{"DEFAULT": "https://duckduckgo.com/?q={}"}

```

To ustawi DuckDuckGo jako twoją domyślną wyszukiwarke. Symbol zastępczy `{}` będzie zastąpiony twoim wynikiem wyszukiwania. Żeby dodać skrót do szybkiego wyszukiwania w Arch Wiki możesz użyć

```
{"DEFAULT": "https://duckduckgo.com/?q={}", "wa": "https://wiki.archlinux.org/?search={}"}

```

Jak opisane przez komentarz w intefejsie qutebrowser, możesz przeszukać Arch Wiki wpisując `o wa <searchterm>`. Zauważ że argumenty potrzebne przez wyszukiwarki różnią się. Dla przykładu żeby ustawić Startpage użyj `https://www.startpage.com/do/metasearch.pl?query={}`

### Skróty klawiszowe

Skróty klawiszowe siedzą w `$XDG_CONFIG_HOME/qutebrowser/keys.conf`.

Możesz zedytować skróty klawiszowe bezpośrednio z przeglądarki korzystając z `:bind *key* *command*` lub możesz bezpośrednio w pliku. Zauważ że tam jest dużo skrótów klawiszowych. Jeżeli zauważysz opóźnienie na swoim ustawionym skrócie klawiszowym, prawdopodobnie jest to z powodu że istnieje skrót klawiszowy korzystający z tego samego pierwszego klawisza.

### Odtwarzanie wideo

Zobacz [Browser plugins#Multimedia playback](/index.php/Browser_plugins#Multimedia_playback "Browser plugins").

## Porady i wskazówki

### Włącz sprawdzanie pisowni

Pierw, pobierz właściwy słownik używając skrypt `dictcli.py` który przychodzi załączony z qutebrowser.

Dla przykładu, dla Polskiego (PL):

```
# /usr/share/qutebrowser/scripts/dictcli.py install pl-PL

```

Skrypt ma również inne funkcje, mogą być wyświetlone wpisując `--help`.

Potem ustaw w qutebrowser:

```
:set spellcheck.languages ["pl-PL"]

```

### Zmniejsz odciski przeglądarki

Strony mogą być w stanie zidentyfikować ciebie bazując na zebranych informacjach jak rozmiar ekranu, agent użytkownika, nagłówki HTTP_ACCEPT i więcej. Zobacz [[1]](https://panopticlick.eff.org/) dla więcej informacji jak i również przetestowania wyjątkowości twojej przeglądarki. Poniżej jest kilka małych króków które mogą być podjęte żeby nasza instalacja qutebrowsera była bardziej pospolita.

Dodatkowo zobacz [Firefox/Privacy#Configuration](/index.php/Firefox/Privacy#Configuration "Firefox/Privacy") dla więcej pomysłów.

#### Ustaw pospolity agent użytkownika

Kilkanaście agentów użytkownika jest do wybrania jako opcje gdy wpiszemy `set content.headers.user_agent`. Kolejnym bardziej pospolitym agentem użytkownika jest:

```
Mozilla/5.0 (Windows NT 6.1; rv:52.0) Gecko/20100101 Firefox/52.0

```

**Note:**

*   Zmiana `Linux x86_64` na nie-Linuxową platforme może stworzyć twoją przeglądarke bardziej unikatową, odkiedy strony mogą również zdobyć twoją platforme przez Javascript i to nie może być zmienione w qutebrowser.
*   Zmiana twojego agenta użytkownika z domyślnego może uniemożliwić prawidłowe działanie niektórych witryn. Dla przykładu, CAPTCHA wspomni że twoja przeglądarka nie jest wspierana jeżeli agent użytkownika jest zapisany jako nieaktualna przeglądarka.

#### Ustaw pospolity nagłówek HTTP_ACCEPT

Następujący jest pospolitym nagłówkiem HTTP_ACCEPT (domyślny Firefoxa). Wpisz te komendy w wierszu polecenia

```
set content.headers.accept_language en-US,en;q=0.5
set content.headers.custom '{"accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"}'

```

#### Wyłącz czytanie z płótna

Ta opcja nie jest obecnie dostępna w qutebrowserze inaczej niż określając ją w wierszu poleceń jak:

```
$ qutebrowser --qt-flag disable-reading-from-canvas

```

Zobacz [issue #2235](https://github.com/qutebrowser/qutebrowser/issues/2235) dla więcej informacji.

**Note:** Niektóre strony zależą na czytaniu z płutna dla czytania zawartości i innych właściwości. Dodanie tej opcji może spowodować nie działanie tych stron. [[2]](https://github.com/qutebrowser/qutebrowser/issues/2908).

#### Wyłączanie WebGL

Ustaw `content.webgl` na `false` żeby wyłączyć WebGL.

### Zarządzanie sesjami jak w dwb

Żeby ustawić qutebrowser, żeby zarządzać sieciami bardziej jak w [dwb](/index.php/Dwb "Dwb") z flagą `--restore` opcją (wiele jednocześnie aktywnych sesji), możesz użyć [ten skrypt](https://github.com/ayekat/dotfiles/blob/master/bin/qutebrowser). Korzysta on z `--basedir` żeby oddzielić dane, cache i śrowisko wykonawcze dla każdej sesji, zostawiając konfiguracje podzieloną.

### Blokowanie stron

Ustaw `c.content.host_blocking.lists.append( str(config.configdir) + "/blockedHosts")` w swoim `config.py` i stwórz plik nazwany `blockedHosts` w tym samym folderze co twój plik konfiguracyjny. Wprowadź strony które chciałbyś zablokować, jedną pod drugą; `127.0.0.1 www.google.com` dla przykładu. To zachowa wbudowaną liste adblocka dodając twoją obok. Zrestartuj qutebrowser `:restart` i wpisz `:adblock-update`. Żeby usunąć liste wbudowaną w qutebrowser usuń `~/.local/share/qutebrowser/blocked-hosts`.

## Zobacz również

*   [Repozytorium na GitHubie](https://github.com/qutebrowser/qutebrowser)
*   [Strona główna](https://qutebrowser.org/)
*   [Wątek BBS](https://bbs.archlinux.org/viewtopic.php?id=191076)
*   [Przykład nowego configu](https://bitbucket.org/jasonwryan/shiv/src/tip/.config/qutebrowser/config.py)