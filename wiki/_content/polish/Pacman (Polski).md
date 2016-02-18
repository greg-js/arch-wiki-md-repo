## Contents

*   [1 Wstęp](#Wst.C4.99p)
*   [2 Instalacja pakietów](#Instalacja_pakiet.C3.B3w)
*   [3 Usuwanie pakietów](#Usuwanie_pakiet.C3.B3w)
*   [4 Aktualizacja systemu](#Aktualizacja_systemu)
*   [5 Zapytania do bazy danych](#Zapytania_do_bazy_danych)
*   [6 Inne użycie](#Inne_u.C5.BCycie)
*   [7 Downgrade pakietów](#Downgrade_pakiet.C3.B3w)
*   [8 Konfiguracja Pacmana](#Konfiguracja_Pacmana)
    *   [8.1 Podstawowe opcje](#Podstawowe_opcje)
    *   [8.2 Repozytoria](#Repozytoria)
    *   [8.3 Optymalizacja Pacmana](#Optymalizacja_Pacmana)
*   [9 Pacman GUI](#Pacman_GUI)
*   [10 Nakładki na Pacmana](#Nak.C5.82adki_na_Pacmana)
    *   [10.1 Powerpill](#Powerpill)
*   [11 Narzędzia Pacmana](#Narz.C4.99dzia_Pacmana)

## Wstęp

Menedżer pakietów Pacman to jedna z głównych atrakcji Arch Linuksa. Łączy w sobie prosty format pakietów binarnych z łatwym w użyciu [ABS](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)"). Pacman umożliwia łatwe zarządzanie i dostosowywanie pakietów, które są brane z oficjalnego repozytorium Archa oraz repozytorium tworzonego przez użytkowników - [AUR](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)"). Pacman pozwala na utrzymanie aktualności systemu przez synchronizację listy pakietów z głównym serwerem, powodując tym samym, że utrzymanie systemu dla znającego się na bezpieczeństwie administratora jest trywialne. Poza tym pozwala na ściągnięcie/zainstalowanie kompletnego pakietu z zależnościami prostym poleceniem.

Pacman jest zarówno menedżerem pakietów binarnych, jak i źródłowych. To połączenie pomysłów z Gentoo, Debiana i Slackware, stworzone, by być jednym z najbardziej rozbudowanych menedżerów pakietów, który jednocześnie pozostaje łatwy w użyciu. Pacman potrafi pobierać, instalować i uaktualniać pakiety ze zdalnych oraz lokalnych repozytoriów, z pełną obsługą zależności. Ponad to ma łatwe do opanowania narzędzia do tworzenia własnych pakietów.

## Instalacja pakietów

Przed instalacją i aktualizacją pakietów dobrze jest zsynchronizować lokalną bazę pakietów z repozytorium:

```
# pacman -Syu

```

Aby zainstalować/zaktualizować jeden bądź kilka pakietów (razem z zależnościami), użyj następującej komendy:

```
# pacman -S nazwa_pakietu1 nazwa_pakietu2

```

Czasem jest więcej niż jedna wersja pakietu w różnych repozytoriach (np. extra i testing). Możesz określić, którą chcesz zainstalować:

```
# pacman -S extra/nazwa_pakietu
# pacman -S testing/nazwa_pakietu

```

## Usuwanie pakietów

Aby usunąć pojedynczy pakiet, zostawiając wszystkie jego zależności:

```
# pacman -R nazwa_pakietu

```

Żeby usunąć pakiet wraz z wszystkimi zależnościami, które nie są wymagane przez inne pakiety:

```
# pacman -Rs nazwa_pakietu

```

Żeby usunąć pakiet wraz z wszystkimi zależnościami i konfiguracją:

```
# pacman -Rns nazwa_pakietu

```

## Aktualizacja systemu

Możesz zsynchronizować bazę pakietów oraz zaktualizować swój system wykorzystując łączenie parametrów:

```
# pacman -Syu

```

## Zapytania do bazy danych

Pacman potrafi przeszukiwać bazę pakietów dla podanego słowa kluczowego. Możesz wpisać część nazwy pakietu, a wyświetlą się wszystkie pakiety, które zawierają podany ciąg znaków. Aby odszukac pakiet w repozytoriach:

```
# pacman -Ss nazwa_pakietu

```

Jeśli znasz nazwę pakietu, którego szukasz, możesz wyświetlić o nim informacje:

```
# pacman -Si nazwa_pakietu

```

Możesz wyświetlić listę pakietów w danym repozytorium:

```
# pacman -Sl nazwa_repozytorium

```

Tak wyświetlisz grupy pakietów (np. gnome):

```
# pacman -Sg

```

Tak zaś wyświetlisz pakiety należące do danej grupy:

```
# pacman -Sg nazwa_grupy

```

Aby odszukac pakiet tylko wśród zainstalowanych:

```
# pacman -Qs nazwa_pakietu

```

Jeśli znasz nazwę zainstalowanego pakietu, możesz wyświetlić o nim informacje:

```
# pacman -Qi nazwa_pakietu

```

Aby sprawdzić, które pakiety przestały być zależnościami innych:

```
# pacman -Qdt

```

## Inne użycie

Pacman jest rozbudowanym narzędziem, dlatego daje ci jeszcze inne możliwości.

Pobranie pakietu bez instalowania go:

```
# pacman -Sw nazwa_pakietu

```

Instalowanie pakietu, który jest na dysku (już pobrany):

```
# pacman -U /ścieżka/do/pakietu/nazwa_pakietu.pkg.tar.gz

```

Czyszczenie pamięci podręcznej pacmana (`/var/cache/pacman/pkg`):

```
# pacman -Scc

```

## Downgrade pakietów

Powodami do dezaktualizacji (wśród wielu innych) okazać się mogą błędy w aktualnej wersji pakietu czy brak funkcjonalności, a także gdy pakiet został zainstalowany eksperymentalnie. Niezależnie od przyczyny, użytkownik zazwyczaj woli wrócić do starszej wersji niż czekać na nową, poprawioną - zajmuje to mniej czasu i jest teoretycznie mniej kłopotliwe.

Dezaktualizacja jednego pakietu w myśl zależności może "pociągnąć" ich więcej. Przykładowo, gdy zainstalowałeś dużą ilość eksperymentalnych i testowych paczek i wyedytowałeś sporą część plików konfiguracyjnych, może być prościej zainstalować system od nowa niż próbować dezaktualizację.

Tak czy inaczej, musisz pamiętać o kilku sprawach:

*   Po pierwsze, możliwe, że będziesz musiał zdezaktualizować więcej niż 1 lub 2 pakiety. Wymagane biblioteki często zmieniają się z wersją programu i ich funkcjonalność może różnić się w stosunku do poprzedniej wersji.
*   Po drugie, musisz sprawdzić, czy potrzebne pliki zostały usunięte z systemu i jeśli tak, czy możesz je pobrać z innego źródła. Repozytoria Archa są aktualizowane bez pozostawiania poprzednich wersji.
*   Po trzecie, musisz być ostrożny ze zmianami w plikach konfiguracyjnych oraz skryptami. Na chwilę obecną będziemy polegać na Pacmanie, dopóki nie będziemy musieli ominąć pewnych zabezpieczeń, włącznie z nadpisywaniem plików.

Wiedz, że te problemy są jednymi z najważniejszych punktów na liście do zrobienia Deweloperów Pacmana. Koncepcja Arch Rolback Machine będzie rozwijana i wciąż czekamy na włączenie tego mechanizmu do menedżera pakietów. Kiedy to nastąpi, całość będzie zautomatyzowana, lecz do tej pory, kieruj się poniższymi instrukcjami.

Pierwsze miejsce, do którego powinieneś się udać w poszukiwaniu poprzedniej wersji pakietu jest `/var/cache/pacman/pkg` na Twoim komputerze i sprawdzenie, czy został tam zachowany. Warunek jest tylko jeden - jeżeli nie wyczyściłeś pamięci podręcznej Pacmana (`pacman -Scc`). Jeśli go znalazłeś, zainstaluj go za pomocąpolecenia:

```
# pacman -U nazwa_pakietu.pkg.tar.xz

```

Upewnij się, że jest to starsza wersja, a nie ta obecna w systemie. Polecenie usunie zainstalowany pakiet i zastąpi go tym wskazanym przez Ciebie. Nie przywróci automatycznie starych wersji zależności - musisz to zrobić ręcznie przed samym programem. Możesz także zignorować wymagane wersje bibliotek za pomocą przełącznika `d`. Na przykład:

```
# pacman -Ud nazwa_pakietu-starsza_wersja.pkg.tar.xz

```

Jednak, prawdopodobnie wpłynie to negatywnie na stabilność systemu.

Jeśli nie znalazłeś starszej wersji w swoim systemie, sprawdź nieaktualne serwery. Możesz sprawdzić konkretnie które to są ze [strony monitorującej stan serwerów](https://www.archlinux.de/?page=MirrorStatus;orderby=syncdelay;sort=1). Możesz także sprawdzić jeden z poniższych (Stan na dzień 2 czerwca 2010 roku.)

*   [mirrors.sohu.com](http://mirrors.sohu.com/archlinux/)
*   [archlinux.umflint.edu](http://archlinux.umflint.edu/)
*   [schlunix.org](http://schlunix.org/?page_id=11)

Gdy już poosiadasz wybraną wersję pakietu, możesz już usunąć najnowszą wersję pakietu X za pomocą polecenia

```
# pacman -Rd nazwa_pakietu

```

a następnie zainstalać starszą paczkę używając polecenia:

```
# pacman -U nazwa_pakietu.pkg.tar.xz

```

**ARM**

[Arch Rollback Machine](http://arm.konnichi.com/) (ARM) przechowuje stare wersje pakietów na bieżąco od listopada 2009 roku. Działa również na zasadzie repozytorium, lecz z podawaniem konkretnej daty. Jeśli jesteś ciekaw, czy znajdziesz tam odpowiednią wersję programów, możesz użyć [wyszukiwarki](http://arm.konnichi.com/search/).

Budowa nie powinna nikomu sprawić problemu:

```
Server=[http://arm.konnichi.com/rok/miesiąc/dzień/repozytorium/os/architektura-procesora](http://arm.konnichi.com/rok/miesiąc/dzień/repozytorium/os/architektura-procesora)

```

*   repozytorium - core/extra/community/testing/community-testing
*   architektura-procesora - i686/x86_64

Kiedy już przygotujesz odpowiedni wpis, umieść go w odpowiedniej sekcji pliku `/etc/pacman.conf`, na przykład:

 `/etc/pacman.conf` 
```
[core]
Server=[http://arm.konnichi.com/2010/04/28/core/os/x86_64](http://arm.konnichi.com/2010/04/28/core/os/x86_64)
Include = /etc/pacman.d/mirrorlist
```

Wpis musi być koniecznie umiejscowiony między nazwą repozytorium, a zewnętrzną listą serwerów lustrzanych. Następnie zsynchronizuj bazę dostępnych pakietów za pomocą ponizszego polecenia i zdezaktualizuj wybrany pakiet.

```
# pacman -Syyu

```

**Rekompilacja pakietu**

W najgorszym przypadku, jeśli nie znajdziesz nigdzie swojego pakietu, będziesz musiał skompilować starszą wersję samodzielnie. Będziesz potrzebował pliku PKGBUILD pakietu. Możesz go stworzyć samodzielnie, edytować dostarczony przez [ABS](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)") lub poszukać go [tutaj](https://www.archlinux.org/packages/).

## Konfiguracja Pacmana

Plik konfiguracyjny pacmana to `/etc/pacman.conf`. Są tam dwie główne sekcje:

### Podstawowe opcje

Podstawowe opcje Pacmana są w sekcji [options].

 `/etc/pacman.conf` 
```
[options]
#RootDir     = /
#DBPath      = /var/lib/pacman/
#CacheDir    = /var/cache/pacman/pkg/
LogFile     = /var/log/pacman.log                                 # Ściezka do pliku z logami Pacmana.
HoldPkg     = pacman glibc
SyncFirst   = pacman                                              # Określasz, jakie pakiety sa najpierw aktualizowane.
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u             # Określasz, z jakiego menedżera pobierania plików będzie korzystał Pacman
IgnorePkg   = nazwa_pakietu                                       # Określasz, które pakiety nie powinny być aktualizowane.
IgnoreGroup = nazwa_grupy                                         # Określasz, które grupy pakietów nie powinny być aktualizowane.
#NoUpgrade   =
#NoExtract   =
#NoPassiveFtp
#UseSyslog
ShowSize                                                          # Opcja pokazuje sumę MB do ściągnięcia.
#UseDelta
#TotalDownload
```

### Repozytoria

Repozytorium to umieszczony na dowolnym serwerze zbiór pakietów, które można pobrać i zainstalować za pomocą Pacmana. Twórcy dystrybucji utrzymują zbiór oficjalnych repozytoriów skopiowanych dodatkowo w szeregu mirrorów (także w Polsce), jednak każdy może utworzyć własne.

Aby zacząć korzystać z repozytorium, należy dodać odpowiedni wpis do pliku `/etc/pacman.conf`. Natomiast lista serwerów, wykorzystywanych przy oficjalnych repozytoriach, znajduje się w `/etc/pacman.d/mirrorlist`. Spis wszystkich serwerów można znaleźć na stronie [MirrorStatus](https://www.archlinux.de/?page=MirrorStatus). Dodatkowo możliwe jest posegregowanie listy serwerów od najszybszego do najwolniejszego. Wpierw wchodzimy do `/etc/pacman.d`, a następnie wybieramy plik z listą serwerów:

```
# rankmirrors mirrorlist

```

W tym wypadku posegreguje nam listę mirrorów. Po zakończeniu całego procesu program pokaże nam w konsoli posegregowaną listę repozytoriów, którą na przykład możemy zapisać do pliku `/etc/pacman.d/mirrorlist-rankmirrors`. Zostaje nam tylko zmiana w `/etc/pacman.conf` wierszy:

```
Include = /etc/pacman.d/mirrorlist

```

na

```
Include = /etc/pacman.d/mirrorlist-rankmirrors

```

i możemy cieszyć się szybkimi (albo i nie) mirrorami.

Lista mirrorów znajduje się w pakiecie [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist).

```
# pacman -S --force pacman-mirrorlist

```

Oficjalne repozytoria:

*   [core]

Repozytorium [core] można znaleźć w `.../core/os/i686` lub `.../core/os/x86_64` na dowolnym mirrorze Archa. Zawiera ono podstawowe paczki Archa i kilka dodatkowych niezbędnych programów, jak edytor tekstu czy program ładujący.

*   [extra]

Repozytorium [extra] można znaleźć w `.../extra/os/i686` bądź `.../extra/os/x86_64` na dowolnym mirrorze Archa. Zawiera ono wszystkie paczki nie znajdujące się w core, gdyż nie są potrzebne do podstawowego uruchomienia systemu. Przykładowo można tutaj znaleźć paczki z GNOME i KDE.

*   [community]

Repozytorium [community] można znaleźć w `.../community/os/i686` lub `.../community/os/x86_64` na dowolnym mirrorze Archa. Jest ono zarządzane przez TU - Zaufanych użytkowników i jest częścią AUR. Zawiera paczki będące częścią AUR, które mają dużą ilość głosów i zostały zaakceptowane przez TU.

*   [community-testing]

Repozytorium [community-testing] można znaleźć w `.../community-testing/os/i686` lub `.../community-testing/os/x86_64` na dowolnym mirrorze Archa. Tu znajdują się testowe pakiety, które po pewnym czasie powinny trafić do repozytorium [community]. Niezalecane początkującym.

*   [testing]

Repozytorium [testing] można znaleźć w `.../testing/os/i686` lub `.../testing/os/x86_64` na dowolnym mirrorze Archa. Zawiera ono paczki które kandydują do repozytoriów [core] bądź [extra]. Używając [testing] można napotkać się z konfliktami nazw pakietów. Jeśli zamierzasz je uaktywnić, musi być ono jako pierwsze repozytorium w `/etc/pacman.conf`. Bądź ostrożny. Twój system może ulec awarii po aktualizacji systemu z włączonym tym właśnie repozytorium. Tylko doświadczeni użytkownicy powinni go używać.

*   [gnome-unstable]

Testowe, teoretycznie niestabilne pakiety dla środowiska GNOME. Niezalecane początkującym.

*   [kde-unstable]

Testowe, teoretycznie niestabilne pakiety dla środowiska KDE. Niezalecane początkującym.

### Optymalizacja Pacmana

**Baza danych**

Pacman trzyma wszystkie informacje o pakietach w małych plikach, po jednym na pakiet. Przyśpieszenie bazy danych znacznie redukuje czas - przykładowo przeszukiwania lub rozwiązywania zależności. Najbezpieczniejszą i najprostszą metodą jest wykonanie poleceniea:

```
# pacman-optimize && sync

```

**Prędkość pobierania pakietów**

Prędkość pobierania pakietów może być większa dzięki używaniu niestandardowych menedżerów pobierania. Domyślnie Pacman korzysta z własnego i wbudowanego, jednak nic nie stoi na przeszkodzie, by go zastąpić innym programem.

*   wget

```
# pacman -S wget

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/wget -c --passive-ftp -c %u` 

*   aria2

Jest to menedżer pobierania obsługujący wstrzymywanie i pobieranie segmentowe. Segmentowe znaczy, że tworzy kilka połączeń z serwerem (lub kilkoma) w tym samym czasie,czego efektem jest krótszy czas pobrania pakietu.

```
# pacman -S aria2

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/aria2c –no-conf -c -s 2 -m 2 -d / -o %o %u` 

*   snarf

```
# pacman -S snarf

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/snarf -N %u` 

*   lftp

```
# pacman -S lftp

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/lftp -c pget %u` 

*   axel

```
# pacman -S axel

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u` 

## Pacman GUI

Najpopularniejszym GUI dla Pacmana w przypadku GNOME jest [GtkPacman](https://aur.archlinux.org/packages.php?ID=8027). Jego zalety to prostota i stabilność. W przypadku KDE zalecany jest [Shaman](https://aur.archlinux.org/packages.php?ID=15422).

## Nakładki na Pacmana

**Note:** Za nakładki na Pacmana z innych źródeł, niż oficjalne repozytoria, deweloperzy nie ponoszą odpowiedzialności.

### Powerpill

Powerpill jest nakładką na Pacmana, napisaną przez [Xyne](http://xyne.archlinux.ca/), która przyspiesza jego działanie przy użyciu pakietu aria2c.

Przykład działania: Podczas aktualizacji systemu [`pacman-Syu`] wynik zawiera 20 pakietów ważących łącznie 200 MB. W przypadku Pacmana może być pobierany tylko jeden plik w danej chwili. Natomiast dzięki Powerpill będą one pobierane równocześnie, nierzadko z większą prędkością (w zależności od posiadanego łącza, dostępności pakietów na serwerach, a także obciążenia serwera).

Pakiet znajduje się w [community], zatem wystarczy wydać w konsoli poniższe polecenie:

```
# pacman -S powerpill

```

Konfiguracja Powerpill znajduje się w pliku `/etc/powerpill.conf`.

Składnia poleceń Powerpill jest bardzo podobna do tych w Pacmanie, np.:

*   Aby zaktualizować system, wystarczy wpisać:

```
# powerpill -Syu

```

*   Aby zainstalować pakiet:

```
# powerpill -S nazwa_pakietu

```

Domyślnie Powerpill jest skonfigurowany do używania narzędzia Reflector, które pomaga ustawić najszybsze mirrory. Zalecane jest zrobienie kopii zapasowej:

```
# mv /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

Poniższe polecenie wybierze 5 najszybszych mirrorów i umieści odpowiednie wpisy w `/etc/pacman.d/mirrorlist` nadpisując wcześniejszą zawartość:

```
# reflector -f 5 -r -o /etc/pacman.d/mirrorlist

```

Zobacz również:

*   [- Xyne's Arch Linux Stuff - Powerpill](http://xyne.archlinux.ca/projects/powerpill)

## Narzędzia Pacmana

Innymi narzędziami [nieobowiązkowymi] do obsługi Pacmana są:

*   [ArchUp](https://aur.archlinux.org/packages.php?ID=35792)
*   [Chase](https://aur.archlinux.org/packages.php?ID=29567)
*   [Pacman Notifier](https://aur.archlinux.org/packages.php?ID=15193)