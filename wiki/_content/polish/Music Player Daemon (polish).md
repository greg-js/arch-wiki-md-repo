**MPD** (**M**usic **P**layer **D**aemon) jest to lekki i szybki odtwarzacz dźwięku działający na zasadzie serwer-klient. MPD uruchamia się w tle jako usługa systemowa (daemon). Posiada obsługę playlist, zarządza muzyką na podstawie bazy danych. Do obsługi potrzebny będzie jeden z klientów czyli program obsługujący serwer mpd.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalacja MPD](#Instalacja_MPD)
*   [2 Konfiguracja MPD](#Konfiguracja_MPD)
    *   [2.1 Konfiguracja lokalna](#Konfiguracja_lokalna)
    *   [2.2 Konfiguracja globalna](#Konfiguracja_globalna)
        *   [2.2.1 Katalog muzyki](#Katalog_muzyki)
        *   [2.2.2 Zmiana użytkownika](#Zmiana_użytkownika)
    *   [2.3 Wszystkie opcje konfiguracji](#Wszystkie_opcje_konfiguracji)
        *   [2.3.1 Pliki i katalogi](#Pliki_i_katalogi)
        *   [2.3.2 Podstawowe ustawienia MPD](#Podstawowe_ustawienia_MPD)
        *   [2.3.3 Zachowywanie symbolicznych linków](#Zachowywanie_symbolicznych_linków)
        *   [2.3.4 Zeroconf / Avahi](#Zeroconf_/_Avahi)
        *   [2.3.5 Kontrola dostępu](#Kontrola_dostępu)
        *   [2.3.6 Wyjście dźwięku](#Wyjście_dźwięku)
        *   [2.3.7 Normalizacja lub obsługa replaygain](#Normalizacja_lub_obsługa_replaygain)
        *   [2.3.8 Wewnętrzne bufory MPD](#Wewnętrzne_bufory_MPD)
        *   [2.3.9 Limitacja zasobów](#Limitacja_zasobów)
        *   [2.3.10 Ustawienia TCP (keep alive)](#Ustawienia_TCP_(keep_alive))
        *   [2.3.11 Kodowanie znaków](#Kodowanie_znaków)
*   [3 Klienty](#Klienty)
    *   [3.1 Konsola](#Konsola)
    *   [3.2 Graficzne](#Graficzne)
    *   [3.3 Sieć](#Sieć)
*   [4 Linki zewnętrzne](#Linki_zewnętrzne)

## Instalacja MPD

Ostatnia stabilna wersja [mpd](https://www.archlinux.org/packages/?name=mpd) dostępna jest w [oficjalny repozytorium](/index.php?title=Official_repositories_(Polski)&action=edit&redlink=1 "Official repositories (Polski) (page does not exist)").

Wersje eksperymentalne/rozwojowe można znaleźć w [AUR](/index.php/AUR_(Polski) "AUR (Polski)"). Przykład: [mpd-git](/index.php/AUR "AUR")

## Konfiguracja MPD

MPD można używać lokalnie (na ustawieniach użytkownika), globalnie (ustawienia odnoszą się do wszystkich użytkowników), a także równolegle. Wybór kierunku zależy od przeznaczenia, przykładowo na komputerach domowych lepszym rozwiązaniem może okazać się konfiguracja lokalna.

Niezbędne katalogi i foldery do prawidłowego działania aplikacji:

```
database - baza danych muzyki
pid - plik w którym przechowywany jest identyfikator procesu
log - dziennik zdarzeń
state - obecnie odtwarzane
playlists - katalog z listami odtwarzania
sticker.sql - plik bazy danych z dodatkowymi danymi programów-klientów

```

Aby MPD mogło odtwarzać dźwięk, [ALSA](/index.php/ALSA "ALSA"), [PulseAudio](/index.php/PulseAudio "PulseAudio") lub [OSS](/index.php/OSS "OSS") muszą być prawidłowo skonfigurowane.

### Konfiguracja lokalna

MPD może być skonfigurowany na koncie użytkownika (zamiast typowej konfiguracji globalnej). Takie rozwiązanie ma swoje korzyści:

*   Pojedynczy katalog `~/.mpd` (lub jakikolwiek inny w `/home/$USER/`) będzie zawierał wszystkie pliki konfiguracyjne.
*   Łatwiej uniknąć problemów z uprawnieniami.

Aby rozpocząć: stwórz katalog dla niezbędnych plików i playlist; stwórz wszystkie wymagane pliki:

```
$ mkdir -p ~/.mpd/playlists
$ cp /usr/share/doc/mpd/mpdconf.example ~/.mpdconf
$ touch ~/.mpd/{database,log,state,pid,sticker.sql}

```

Edytuj `~/.mpdconf` i sprecyzuj położenie plików:

```
music_directory    "~/Muzyka"          # Zakomentuj jeśli XDG wskazuje na muzykę.
playlist_directory "~/.mpd/playlists"
db_file            "~/.mpd/database"
log_file           "~/.mpd/log"
pid_file           "~/.mpd/pid"
state_file         "~/.mpd/state"
sticker_file       "~/.mpd/sticker.sql"

```

Od teraz MPD może być uruchomione polecenie `mpd` (wpierw sprawdzi `~/.mpdconf`, później `~/etc/mpd.conf` [brak wsparcia dla katalogów konfiguracji XDG, jak `~/.config/mpd/mpd.conf`]). Aby sprecyzować położenie pliku:

```
mpd /path/to/mpd.conf

```

Aby uruchomić MPD po zalogowaniu, dodaj do `~/.profile` (lub innego [pliku Autostart](/index.php/Autostarting#Shells "Autostarting")):

```
# Uruchamianie MPD (jeżeli nie został już uruchomiony)
[ ! -s ~/.mpd/pid ] && mpd

```

Aby uruchomić wraz z X.org(iem), dodaj do [xprofile](/index.php/Xprofile "Xprofile") lub [xinitrc](/index.php/Xinitrc "Xinitrc"). Przez niektóre DE, pliki te są ignorowane (np. przez GNOME), zastąpić je można plikiem autostart (specyfikacja XDG) - tu: `~/.config/autostart/mpd.desktop`; to:

```
[Desktop Entry]
Encoding=UTF-8
Type=Application
Name=Music Player Daemon
Comment=Serwer odtwarzający muzykę
Exec=mpd
StartupNotify=false
Terminal=false
Hidden=false
X-GNOME-Autostart-enabled=false

```

### Konfiguracja globalna

**Warning:** Users of PulseAudio with a local mpd have to implement a [workaround](/index.php/Music_Player_Daemon/Tips_and_tricks#Local_(with_separate_mpd_user) "Music Player Daemon/Tips and tricks") in order to run mpd as its own user!

Domyślnie w Archu pliki MPD trzymane są tu: `/var/lib/mpd`; domyślny użytkownik to *mpd*.

Edytuj `/etc/mpd.conf` aby ustawić:

```
music_directory       "/ścieżka/do/katalogu/z/muzyką"
playlist_directory    "/var/lib/mpd/playlists"
db_file               "/var/lib/mpd/mpd.db"
log_file              "syslog"
pid_file              "/run/mpd/mpd.pid"
state_file            "/var/lib/mpd/mpdstate"
user                  "mpd"

```

**Note:** Nie używaj znaku ~ jako skrótu do katalogu użytkownika. Wpierw jest czytana konfiguracja, później zaś są zbijane uprawnienia i ponownie jest wczytywana konfiguracja..

Ustawiliśmy właśnie MPD aby był uruchamiany na użytkowniku *mpd*, lecz właścicielem `/var/lib/mpd` jest *root*, możemy to zmienić:

```
# chown -R mpd /var/lib/mpd

```

Aby uruchomić MPD wykonaj:

```
# systemctl start mpd.service

```

Jeżeli chcesz by MPD było automatycznie uruchamiane przy każdym starcie systemu, wykonaj:

```
# systemctl enable mpd.service

```

#### Katalog muzyki

MPD potrzebuje uprawnień `+x` dla wszystkich rodziców katalogu muzyki. Jeżeli nie chcesz tego zmieniać, możesz podmontować swój katalog z muzyką pod katalog do którego MPD ma wystarczające uprawnienia.

```
# mkdir /var/lib/mpd/muzyka
# echo "/ścieżka/do/katalogu/muzyka /var/lib/mpd/muzyka none bind" >> /etc/fstab
# mount -a

```

Sprawdź [dyskusję na forum (en)](https://bbs.archlinux.org/viewtopic.php?id=86449).

Dodatkowym wyjściem byłoby stworzenie symbolicznego linku do `/var/lib/mpd/muzyka`.

```
# mkdir /var/lib/mpd/muzyka
# ln -s /ścieżka/do/katalogu/muzyka /var/lib/mpd/muzyka/

```

Pamiętaj o uprawnieniach we wnętzu katalogu.

#### Zmiana użytkownika

**Note:** Wymagane tylko przy zmianie domyślnego użytkownika!

Zmiana grupy w której uruchamiany jest mpd może powodować błędy typu:

*   output: Failed to open "My ALSA Device"
*   [alsa]: Failed to open ALSA device "default": No such file or directory
*   player_thread: problems opening audio device while playing "Song Name.mp3"

Dzieje się tak, dlatego że domyślnie MPD jest członkiem grupy *audio*, a pliki w `/dev/snd/` też są w grupie *audio*, co jest dobre ale nie koniecznie prawdziwe w przypadku innego użytkownika. Więc dodaj go do grupy *audio*:

```
# gpasswd -a mpd audio

```

### Wszystkie opcje konfiguracji

Plik `/etc/mpd.conf` jest podzielony na kategorie, spolszczone opcje podane są kategoriami w kolejności takiej samej jak w pliku konfiguracyjnym. Opcje dostępne w wersji 0.17.5 lub nowszej.

#### Pliki i katalogi

*   **music_directory** - opcja do ustawienia katalogu z muzyką, która zostanie dodana do bazy MPD. W przypadku zakomentowania, MPD doda katalog XDG, w razie braku tegoż, dodawanie muzyki do MPD będzie dostępne tylko poprzez protokół `file://`;
*   **playlist_directory** - lokalizacja katalogu dla wewnętrznych playlist MPD;
*   **db_file** - lokalizacja pliku bazy danych;
*   **log_file** - lokalizacja pliku z rejestrem zdarzeń. Ta opcja jest dobra przy usuwaniu problemów, ilość szczegółów zależy od ustawień opcji: `log_level`. Gdy opcja ma wartość `"syslog"`, wtedy używany będzie systemowy rejestrator zdarzeń;
*   **pid_file** - jeżeli życzysz sobie używać `mpd --kill` do zatrzymywania mpd, musisz podać ścieżkę do pliku w którym mpd zapisze swój identyfikator procesu;
*   **state_file** - jeżeli życzysz sobie obsługi sesji (zapisuje stan odtwarzania utworu, playlistę, odtwarzanie/pauza, itp.), podaj ścieżkę do pliku do którego mpd będzie zapisywał te informacje, a po ponownym uruchomieniu sesja zostanie przywrócona;
*   **sticker_file** - lokalizacja pliku bazy danych z dodatkowymi informacjami przylepionymi do utworów.

#### Podstawowe ustawienia MPD

*   **user** - jeżeli uruchomiony z konta root, MPD porzuci przywileje roota i uruchomi się jako podany użytkownik. Jeżeli uruchomiony z konta użytkownika, mpd będzie pracować jako ten użytkownik. Odradzane jest by mpd posiadało pełne przywileje roota;
*   **group** - ta opcja ustawia grupę podstawową na której będzie działał MPD. Jeżeli nie sprecyzowane, używana będzie podstawowa grupa użytkownika. Pożyteczne gdy MPD aby mieć uprawnienia do używania karty dźwiękowej, musi być w grupie "audio";
*   **bind_to_address** - adres i port nasłuchiwany przez mpd. Wybierz jedno z poniższych:

```
bind_to_address      "127.0.0.1"   # nasłuchuj tylko lokalnie
bind_to_address      "any"          # nasłuchuj też zdalnie
bind_to_address      "/ścieżka/socket" # nasłuchuj lokalnie na pliku socket

```

*   **port** - port na którym ma być prowadzony nasłuch;
*   **log_level** - kontrola poziomu logowanych informacji. Można użyć:
    *   **"default"** - domyślnie
    *   **"secure"** - komunikaty bezpieczeństwa
    *   **"verbose"** - rozbudowane informacje (polecane do rozwiązywania problemów)
*   **gapless_mp3_playback** - odtwarzanie bez odstępów (gapless playback). Jeżeli masz problemy z dźwiękiem, wyłącz tą opcję albo użyj programu [vbrfix](http://www.willwap.co.uk/Programs/vbrfix.php);
*   **restore_paused** - ustawienie tej opcji spowoduje że MPD po starcie będzie pauzował odtwarzanie;
*   **save_absolute_paths_in_playlists** - ta opcja spowoduje zapis playlist tak by można było z nich korzystać w innych programach;
*   **metadata_to_use** - opcja określa które meta-dane będą importowane do muzycznej bazy danych (działa tylko przy dodawaniu nowych). Dostępne meta-dane to:
    *   **artist** - artysta
    *   **album** - album
    *   **title** - tytuł
    *   **track** - numer utworu
    *   **name**
    *   **genre** - gatunek muzyczny (ale nie styl)
    *   **date** - rok wydania
    *   **composer** - kompozytor
    *   **performer** - wykonawca
    *   **comment** -komentarz
    *   **disc** - numer płyty
    *   **musicbrainz_artistid** - id artysty w serwisie musicbrainz
    *   **musicbrainz_albumid** - id albumu w serwisie musicbrainz
    *   **musicbrainz_albumartistid** - id artysty albumu w serwisie musicbrainz
    *   **musicbrainz_trackid** - id utworu w serwisie musicbrainz
*   **auto_update** - automatyczne aktualizuj, gdy pliki w katalogu z muzyką zostały zmodyfikowane;
*   **auto_update_depth** - głębokość podkatalogów, które będą obserwowane po uaktywnieniu opcji `auto_update`. Dla 0 podkatalogi nie będą obserwowane, jedynie pliki w katalogu głównym. Domyślnie zakomentowane co oznacza brak limitów.

#### Zachowywanie symbolicznych linków

*   **follow_outside_symlinks** - ustaw tą opcje na `"yes"` jeśli chcesz by MPD podążał za linkami do zewnętrznych katalogów;
*   **follow_inside_symlinks** - ustaw tą opcję na `"yes"` jeśli chcesz by MPD traktował linki do wewnętrznych katalogów tak jak linki do zewnętrznych.

#### Zeroconf / Avahi

*   **zeroconf_enabled** - jeśli ustawione na `"yes"`, MPD będzie publikować informacje za pomocą Zeroconf/Avahi;
*   **zeroconf_name** - unikatowa nazwa dla MPD, którą będzie przedstawiał się w sieci.

#### Kontrola dostępu

*   **password** - MPD może wymagać od użytkownika podanie hasła. Możesz ustawić jedno lub więcej haseł. Możesz podać co ten użytkownik będzie mógł robić, a co zostanie mu zabronione. Po zalogowaniu się z użyciem danego `"[hasła]@[użytkownik będzie mógł to],[to],[to]"`;
*   **default_permissions** - domyślne ustawienia dla nie zalogowanych użytkowników. Ta opcja określa na co pozwalasz nie zalogowanym użytkownikom. Domyślnie wszyscy użytkownicy mają pełny dostęp do MPD jeżeli żadne hasło nie zostało określone powyżej. W przeciwnym wypadku nie mają żadnego dostępu aby to zmienić ustaw tą opcję.

#### Wyjście dźwięku

MPD obsługuje wiele typów wyjść dźwięku, potrafi jednocześnie wysyłać dźwięk na wiele wyjść. Możesz ustawić jedno lub więcej, jeśli tego nie zrobisz, MPD będzie próbował każdorazowo przy uruchomieniu automatycznie ustawiać wyjście..

*   **audio_output{}** - W swoich klamrach zawiera: nazwę, typ i opcje dostępne dla danego typu. Zobacz [przykłady konfiguracji](http://mpd.wikia.com/wiki/Configuration#Audio_Outputs). Opis niektórych opcji z przykładów:
    *   **type** - typ wyjścia;
    *   **name** - twoja nazwa dla wyjścia;
    *   **device** (opcjonalne) - urządzenie alsa, np: `hw:0,0` dla pierwszej karty i pierwszego wejścia ALSAy;
    *   **format** (opcjonalne) - zawartość opcji: `"próbkowanie:głębia:kanały"`;
    *   **mixer_type** (opcjonalne) - ściszanie/pogłaśnianie realizowane `"hardware"` (sprzętowo), `"software"` (programowo), `"none"` (brak);
    *   **use_mmap** (opcjonalne) - jeżeli chcesz używać alsa_mmap, ustaw na `"yes"`;
    *   **auto_resample** (opcjonalne) - jeśli chcesz wyłączyć automatyczne konwertowanie próbkowania dźwięku, ustaw na `"no"`;
    *   **mixer_control** (opcjonalne) - nazwa suwaka który będzie przesuwany podczas ściszania/pogłaśniania (domyślnie `"master"`), wymaga `mixer_type` ustawionego na `"hardware"`.

Ustawienia ogólne dla konwertowania i jego jakości:

*   **audio_output_format** - wszystkie dekodowane dźwięki będą konwertowane do tego formatu zanim zostaną wysłane do wyjścia dźwięku. Zawartość opcji: `"próbkowanie:głębia:kanały"`;
*   **samplerate_converter** - ustaw jakość konwertowania próbkowania, możliwe opcje:
    *   **Best Sinc Interpolator** - najlepsza jakość ale najwolniejsze
    *   **Medium Sinc Interpolator** - średnia jakość
    *   **Fastest Sinc Interpolator** - szybkość ponad jakość
    *   **ZOH Interpolator** - jakieś ubogie
    *   **Linear Interpolator** - i jeszcze bardziej
    *   **internal** - wbudowane, kiepskie

#### Normalizacja lub obsługa replaygain

*   **replaygain** - ustaw obsługę [replaygain](http://www.replaygain.org) na `"off"` (wyłączona), `"track"` (utwór), `"album"` (album);
*   **replaygain_preamp** - przycisz lub pogłośnić pliki o podaną ilość decybeli. Obsługa replaygain musi być włączona, a plik musi zawierać niezbędne tagi;
*   **volume_normalization** - wyciszanie w locie, tak aby wszystkie pliki miały podobny poziom hałasu, poprzednik replaygain. Jeśli chcesz włączyć, ustaw na `"yes"`.

#### Wewnętrzne bufory MPD

*   **audio_buffer_size** - rozmiar buforu dekodowanego dźwięku, nie zmieniaj jeśli dalej nie wiesz co to robi;
*   **buffer_before_play** - minimalny rozmiar zapełnionego buforu w procentach, przed rozpoczęciem odtwarzania.

#### Limitacja zasobów

Za pomocą tych ustawień można zmniejszyć zużycie zasobów. Te opcje powinny być na tyle małe by nie spowodować zagrożeń bezpieczeństwa.

*   **connection_timeout** - czas (w sec.) bezczynności połączenia po którym zostanie ono zamknięte;
*   **max_connections** - maksymalna ilość równoległych połączeń;
*   **max_playlist_length** - maksymalna wielkość playlisty;
*   **max_command_list_size** - maksymalna długość listy poleceń;
*   **max_output_buffer_size** - maksymalny rozmiar buforu wyjścia.

#### Ustawienia TCP (keep alive)

Tylko dla klientów podłączonych przy pomocy systemów obsługujących tą funkcję. Pozwala wykryć systemy, które nie zamknęły połączenia, a nie są dostępne w sieci.

To nie jest zazwyczaj konieczne lecz może się przydać dla połączeń typu wifi, które lubią rwać połączenia. W połączeniu z `max_connections` może doprowadzić do zapełnienia limitu uniemożliwiając na nowe połączenia.

*   **tcp_keep_alive** - ustaw na `"yes"` aby włączyć keepalive;
*   **tcp_keep_alive_idle** - czas nieaktywności, po upływie którego, połączenie zostanie sprawdzone;
*   **tcp_keep_alive_interval** - czas każdego kolejnego sprawdzania po `tcp_keep_alive_idle`;
*   **tcp_keep_alive_count** - liczba nieudanych prób zanim połączenie zostanie zamknięte.

#### Kodowanie znaków

Jeżeli nazwy plików lub katalogów nie są wyświetlane prawidłowo, możesz tu, to zmienić. W większości przypadków powinno wystarczyć `"ISO-8859-1"` lub `"UTF-8"`. Musisz ponownie stworzyć bazę danych aby twoje ustawienia zostały zapisane (użyj mpd --create-db).

*   **filesystem_charset** - kodowanie dla systemu plików;
*   **id3v1_encoding** - kodowanie meta-danych.

## Klienty

Do obsługi MPD potrzebny jest oddzielny klient. Zobacz listę klientów na [mpd wiki](http://mpd.wikia.com/wiki/Clients). Popularne to:

### Konsola

*   **mpc** — Prosty klient w duchu KISS. Dostępne są wszystkie podstawowe funkcje

	[http://mpd.wikia.com/wiki/Client:Mpc](http://mpd.wikia.com/wiki/Client:Mpc) || [mpc](https://www.archlinux.org/packages/?name=mpc)

*   **ncmpc** — Klient oparty o bibliotekę Ncurses

	[http://mpd.wikia.com/wiki/Client:Ncmpc](http://mpd.wikia.com/wiki/Client:Ncmpc) || [ncmpc](https://www.archlinux.org/packages/?name=ncmpc)

*   **[ncmpcpp](/index.php/Ncmpcpp "Ncmpcpp")** — Niemalże identyczny klon ncmpc, z kilkoma dodatkowymi funkcjami jak: edytor tagów, wyszukiwarka

	[http://unkart.ovh.org/ncmpcpp/](http://unkart.ovh.org/ncmpcpp/) || [ncmpcpp](https://www.archlinux.org/packages/?name=ncmpcpp)

*   **pms** — Wysoce rozbudowany i funkcjonalny klient Ncurses

	[http://pms.sourceforge.net/](http://pms.sourceforge.net/) || [pmus](https://aur.archlinux.org/packages/pmus/)

*   **vimpc** — Klient oparty o Ncurses z obsługą w stylu edytora vi

	[http://sourceforge.net/projects/vimpc/](http://sourceforge.net/projects/vimpc/) || [vimpc](https://aur.archlinux.org/packages/vimpc/)

### Graficzne

*   **Ario** — Bogaty w funkcje klient GTK2, wygląd inspirowany Rythmboxem

	[http://ario-player.sourceforge.net/](http://ario-player.sourceforge.net/) || [ario](https://www.archlinux.org/packages/?name=ario)

*   **QmpdClient** — Klient napisany przy użyciu Qt 4.x

	[http://bitcheese.net/wiki/QMPDClient](http://bitcheese.net/wiki/QMPDClient) || [qmpdclient](https://www.archlinux.org/packages/?name=qmpdclient)

*   **Sonata** — Elegancki program napisany w Python i GTK+

	[http://sonata.berlios.de/](http://sonata.berlios.de/) || [sonata](https://www.archlinux.org/packages/?name=sonata)

*   **gmpc** — Klient w GTK2\. Projektowany by być lekkim, łatwym, a przy okazji dostarczać wszystkie opcje MPD. Użytkownicy mogą wybierać kilka różnych metod przeglądania bazy muzycznej, rozszerzać opcje wtyczkami.

	[http://gmpc.wikia.com/wiki/Gnome_Music_Player_Client](http://gmpc.wikia.com/wiki/Gnome_Music_Player_Client) || [gmpc](https://aur.archlinux.org/packages/gmpc/)

*   **Cantata** — Bogaty w opcje, z dużą swobodą konfiguracji interfejsu, klient MPD dla KDE4

	[https://code.google.com/p/cantata/](https://code.google.com/p/cantata/) || [cantata-qt](https://aur.archlinux.org/packages/cantata-qt/)

### Sieć

*   **Patchfork** — Aplikacja internetowa do obsługi MPD, napisana w PHP i Ajaxie

	[http://mpd.wikia.com/wiki/Client:Pitchfork](http://mpd.wikia.com/wiki/Client:Pitchfork) || [patchfork-git](https://aur.archlinux.org/packages/patchfork-git/).

## Linki zewnętrzne

*   [Strona domowa (en)](http://www.musicpd.org/)
*   [Forum MPD (en)](http://forum.musicpd.org/)
*   [Dokumentacja MPD (en)](http://www.musicpd.org/doc/user/)
*   [Opis na wikipedii (pl)](https://pl.wikipedia.org/wiki/Music_Player_Daemon)