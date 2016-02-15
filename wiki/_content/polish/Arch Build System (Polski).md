## Contents

*   [1 Czym jest ABS?](#Czym_jest_ABS.3F)
*   [2 Dlaczego warto korzystać z ABS?](#Dlaczego_warto_korzysta.C4.87_z_ABS.3F)
*   [3 Instalacja ABS](#Instalacja_ABS)
*   [4 Konfiguracja](#Konfiguracja)
    *   [4.1 /etc/abs.conf](#.2Fetc.2Fabs.conf)
    *   [4.2 /etc/makepkg.conf](#.2Fetc.2Fmakepkg.conf)
*   [5 Tradycyjna metoda instalacji pakietów bez używania ABS](#Tradycyjna_metoda_instalacji_pakiet.C3.B3w_bez_u.C5.BCywania_ABS)

## Czym jest ABS?

ABS to skrót od Arch Build System. Jest to coś na kształt portów. Porty to pomysł realizowany głównie w systemach rodziny *BSD. Jest to hierarchiczny zbiór plików ułatwiający ściąganie, rozpakowywanie, nakładanie łat, kompilację i instalację programów. ABS jest czymś na kształt portów, ponieważ zamiast instalować, buduje pakiet binarny. Taki plik może być potem zainstalowany lub usunięty programem [Pacman](/index.php/Pacman_(Polski) "Pacman (Polski)"). W ABS znajdują się tylko PKGBUILDy oficjalnie tworzone przez programistów Archa. Istnieje też zbiór PKGBUILDów tworzonych przez społeczność i nazywa się [Arch User Repository](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)"). Znajomość ABS nie jest niezbędna przy korzystaniu z systemu Arch Linux, jednak w wielu przypadkach może być bardzo przydatna.

## Dlaczego warto korzystać z ABS?

Arch Build System jest wykorzystywany do:

*   Kompilacji lub przebudowań pakietów z jakiegokolwiek powodu;
*   Instalacji nowych pakietów ze źródeł, które nie są jeszcze dostępne w repozytoriach;
*   Dostosowania istniejących pakietów do swoich potrzeb;
*   Przebudowy całego systemu przy użyciu flag kompilatora;
*   Kompilacji jądra systemu.

## Instalacja ABS

Aby zacząć używać ABS, musisz najpierw zainstalować pakiety:

```
# pacman -S abs base-devel

```

## Konfiguracja

### `/etc/abs.conf`

Edytujemy plik `/etc/abs.conf` i wybieramy repozytoria ("!" oznacza niekorzystanie z danego repozytorium):

```
REPOS=(core extra community !testing)

```

Następnie, jako root, wpisujemy polecenie:

```
# abs

```

Utworzone zostało drzewo ABS w katalogu `/var/abs`:

```
| -- core/
|     || -- base/
|     ||     || -- acl/
|     ||     ||     || -- PKGBUILD
|     ||     || -- attr/
|     ||     ||     || -- PKGBUILD
|     ||     || -- ...
|     || -- devel/
|     ||     || -- abs/
|     ||     ||     || -- PKGBUILD
|     ||     || -- autoconf/
|     ||     ||     || -- PKGBUILD
|     ||     || -- ...
|     || -- ...
| -- extra/
|     || -- daemons/
|     ||     || -- acpid/
|     ||     ||     || -- PKGBUILD
|     ||     ||     || -- ...
|     ||     || -- apache/
|     ||     ||     || -- ...
|     ||     || -- ...
|     || -- ...
| -- community/
|     || -- ...

```

Powyższe polecenie powinno być wykonywane okresowo, aby zachować synchronizację z oficjalnymi repozytoriami.

Aby pobrać wybrany pakiet:

```
# abs nazwa_repozytorium / nazwa_pakietu

```

### `/etc/makepkg.conf`

Globalne zmienne środowiskowe i flagi kompilatora określone są w pliku `/etc/makepkg.conf`. Ustawienia domyślne są zoptymalizowane pod architektury i686 i x86_64.

## Tradycyjna metoda instalacji pakietów bez używania ABS

**Note:** Zawsze należy przeczytać plik `INSTALL`, jak pakiet powinien być zbudowany i zainstalowany. Poniższa metoda nie jest zalecana dla wszystkich pakietów.

**Warning:** Powyższa metoda oczywiście nadal używana jest na Arch Linuksie. Jednakże, jeśli nie jesteś ostrożny, pliki mogą zostać rozproszone po całym systemie plików. Używaj tej metody, jeśli wiesz co robisz.

Jeśli nie czujesz się jeszcze pewny w ręcznym kompilowaniu oprogramowania ze źródeł,wiedz, że większość pakietów (ale nie wszystkie) może być budowana ze źródeł w tradycyjny sposób:

*   Pobierz wybrane przez siebie archiwum źródłowe pakietu.
*   Rozpakuj je:

```
$ tar -xzf nazwa_pakietu.tar.gz
$ tar -xjf nazwa_pakietu.tar.bz2
$ tar -xvzf nazwa_pakietu.tar.xz

```

*   Wejdź do rozpakowanego katalogu:

```
$ cd nazwa_katalogu (nazwa_pakietu)

```

*   Tu możesz skonfigurować pakiet, jeśli tego chcesz. Ogólnie rzecz biorąc, istnieje skrypt o nazwie `configure` w katalogu źródłowym, który służy do dokonania ustawień dla `make` oraz sprawdzenia, czy środowisko, w którym jest uruchomiony zawiera potrzebne biblioteki do kompilacji. Skrypt jest zwykle tworzony w sposób automatyczny przy pomocy narzędzi z pakietu `autoconf`. W takim razie uruchamiamy polecenie:

```
$ ./configure

```

Lub

```
$ ./configure --prefix=/usr/local

```

Jeżeli chcesz dodać swoje opcje do powyższego polecenia, spróbuj najpierw zrozumieć, jak to polecenie działa:

```
$ ./configure --help

```

*   Przyszedł czas na kompilację:

```
$ make

```

*   Następnie wydajesz polecenie instalacji:

```
# make install

```

*   Jeżeli będziesz chciał usunąć pakiet, wchodzisz do katalogu z źródłami i wpisujesz w swoim terminalu:

```
# make uninstall

```