<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Wstęp](#Wstęp)
*   [2 Użycie](#Użycie)
    *   [2.1 Aktualizacja systemu](#Aktualizacja_systemu)
    *   [2.2 Instalacja pakietów](#Instalacja_pakietów)
    *   [2.3 Usuwanie pakietów](#Usuwanie_pakietów)
    *   [2.4 Zapytania do bazy danych](#Zapytania_do_bazy_danych)
    *   [2.5 Powód instalacji pakietu](#Powód_instalacji_pakietu)
    *   [2.6 Czyszczenie cache](#Czyszczenie_cache)
    *   [2.7 Downgrade pakietów](#Downgrade_pakietów)
        *   [2.7.1 Archiwa Archa](#Archiwa_Archa)
            *   [2.7.1.1 Arch Linux Archive](#Arch_Linux_Archive)
            *   [2.7.1.2 Arch Linux Historical Archive](#Arch_Linux_Historical_Archive)
    *   [2.8 Inne użycie](#Inne_użycie)
*   [3 Konfiguracja Pacmana](#Konfiguracja_Pacmana)
    *   [3.1 Podstawowe opcje](#Podstawowe_opcje)
    *   [3.2 Repozytoria](#Repozytoria)
    *   [3.3 Optymalizacja Pacmana](#Optymalizacja_Pacmana)
*   [4 Pacman GUI](#Pacman_GUI)
*   [5 Nakładki na Pacmana](#Nakładki_na_Pacmana)
    *   [5.1 Powerpill](#Powerpill)
*   [6 Narzędzia Pacmana](#Narzędzia_Pacmana)

## Wstęp

Menedżer pakietów Pacman to jedna z wyróżniających cech Arch Linuksa. Łączy w sobie prosty format pakietów binarnych z łatwym w użyciu [ABS](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)"). Pacman umożliwia łatwe zarządzanie i dostosowywanie pakietów, zarówno tych z oficjalnego repozytorium Archa, jak i tych z repozytorium tworzonego przez użytkowników - [AUR](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)").

Pacman pozwala na utrzymanie aktualności systemu przez synchronizację listy pakietów z głównym serwerem, powodując tym samym, że utrzymanie systemu dla znającego się na bezpieczeństwie administratora jest trywialne. Poza tym pozwala na ściągnięcie/zainstalowanie kompletnego pakietu z zależnościami prostym poleceniem.

Pacman jest zarówno menedżerem pakietów binarnych, jak i źródłowych. To połączenie pomysłów z Gentoo, Debiana i Slackware, stworzone, by być jednym z najbardziej rozbudowanych menedżerów pakietów, który jednocześnie pozostaje łatwy w użyciu. Pacman potrafi pobierać, instalować i uaktualniać pakiety ze zdalnych oraz lokalnych repozytoriów, z pełną obsługą zależności. Ponadto ma łatwe do opanowania narzędzia do tworzenia własnych pakietów. Napisany w C, wykorzystujący format [tar](https://pl.wikipedia.org/wiki/Tar_(informatyka)).

## Użycie

Pełna lista operacji, które można przeprowadzać z użyciem Pacmana: [pacman(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pacman.8).

**Tip:** Użyteczna ściągawka dla tych, którzy przyzwyczaili się do menadżerów pakietow z innych dystrybucji [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta").

### Aktualizacja systemu

Możesz zsynchronizować bazę pakietów oraz zaktualizować swój system wykorzystując łączenie parametrów:

```
# pacman -Syu

```

**Warning:** Zaleca sie używanie tych parametrów zawsze razem, żeby uniknać prób aktualizowania systemu w oparciu o nieaktualną listę pakietów. Może to prowadzić m.in. do problemów z zależnościami. Podobnie przed każdą instalacją pakietu dobrze jest zsynchronizować lokalną bazę z repozytorium.

### Instalacja pakietów

Aby zainstalować/zaktualizować jeden bądź kilka pakietów (razem z zależnościami), użyj następującej komendy:

```
# pacman -S nazwa_pakietu1 nazwa_pakietu2

```

Czasem jest więcej niż jedna wersja pakietu w różnych repozytoriach (np. extra i testing). Możesz określić, którą chcesz zainstalować:

```
# pacman -S extra/nazwa_pakietu
# pacman -S testing/nazwa_pakietu

```

Żeby zainstalować kilka pakietów, które mają cześć nazwy taką samą:

```
# pacman -S plasma-{desktop,mediacenter,nm}
# pacman -S plasma-{workspace{,-wallpapers},pa}

```

### Usuwanie pakietów

Aby usunąć pojedynczy pakiet, zostawiając wszystkie jego zależności:

```
# pacman -R nazwa_pakietu

```

Żeby usunąć pakiet wraz z wszystkimi zależnościami, które nie są wymagane przez inne pakiety:

```
# pacman -Rs nazwa_pakietu

```

Żeby usunąć pakiet wraz z wszystkimi zależnościami, które nie są wymagane przez inne pakiety i konfiguracją:

```
# pacman -Rns nazwa_pakietu

```

**Note:** Domyślnie usuwając aplikację pacman zapisuje ważne pliki konfiguracyjne z rozszerzeniem *pacsave*. Opcja `-n` zapobiega tworzeniu takich plików, ale nie ma wpływu na pliki konfiguracyjne, które tworzą niektóre programy (np. jako dotfiles w katalogu home).

Żeby usunąć pakiet wraz z wszystkimi zależnościami i wszystkimi pakietami, które zależą od usuwanego pakietu:

```
# pacman -Rsc 

```

**Warning:** Rekursywna operacja, która może usunąć wiele potencjalnie potrzebnych innym aplikacjom pakietów.

### Zapytania do bazy danych

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

Aby sprawdzić, które pakiety przestały być zależnościami innych (tzw. sieroty):

```
# pacman -Qdt

```

### Powód instalacji pakietu

Baza danych pacmana dzieli zainstalowane pakiety wg powodu/przyczyny (*reason*), dla jakiego zostały zainstalowane:

*   **explicite zainstalowane** (*explicitly-installed*): pakiety, które bezpośrednio zostały zainstalowane komendą `pacman -S` albo `-U`;
*   **zależności**: pakiety, które chociaż nie zostały bezpośrednio zainstalowane ww. komendą, to zostały implicite zainstalowane, bo były wymagane przez inny pakiet, który był instalowany bezpośrednio.

Jeżeli chcemy explicite instalowany pakiet zainstalować jako pakiet zależny, możemy wymusić to komendą:

```
 # pacman -S --asdeps *nazwa_pakietu*

```

**Tip:** Instalowanie opcjonalnych dependencji z użyciem `-–asdeps` skutkuje tym, że w sytuacji, gdy będziemy usuwać osierocone pakiety, pacman usunie też takie pozostawione opcjonalne zależności.

W czasie reinstalacji pakietu, domyślnie powód instalacji pakietu pozostaje niezmieniony. Listę explicite zainstalowanych pakietów możemy zobaczyć stosując `pacman -Qe`, listę pakietów oznaczonych jako zależności: `pacman -Qd`. Zmiana ustawień celu instalacji jest możliwa po zastosowaniu:

```
 # pacman -D –-asdeps *nazwa_pakietu*
 # pacman -D --asexplicit *nazwa_pakietu*

```

**Note:** Odradza się używanie `–-asdeps` i `–-asexplicit` razem z upgradem, np. `pacman -Syu *nazwa_pakietu* -–asdeps`. To zmieni ustawienia powodu nie tylko dla instalowanego pakietu, ale także dla tych upgradowanych.

### Czyszczenie cache

Pacman przechowuje ściągnięte pakiety w katalogu `/var/cache/pacman/pkg` i nie usuwa automatycznie odinstalowanych wersji. Dzięki temu można:

1.  Przeprowadzić downgrade pakietu (powrót do starszych wersji, jeżeli zajdzie taka potrzeba), bez konieczności szukania poprzednich wersji w repozytoriach takich jak np. Arch Linux Archive.
2.  Przy ponownej instalacji raz ściągniętego i odinstalowanego pakietu nie trzeba go ponownie ściągać.

Konieczne jest jednak okresowe czyszczenie cache'a, tak żeby jego rozmiar nie urósł nadmiernie. Skrypt *paccache* z pakietu [pacman-contrib](https://www.archlinux.org/packages/?name=pacman-contrib) usuwa starsze wersje pakietów poza (domyślnie) trzema ostatnimi.

```
 # paccache –r

```

Pacman ma też swoje własne *build-in* narzędzia do czyszczenia cache’a i plików z repozytoriów, które nie są już wymienione w `/etc/pacman.conf` . Pacman nie ma jednak opcji pozostawienia pewnej ilości starszych wersji. Jego działanie jest agresywniejsze niż *paccache*. Żeby usunąć wszystkie pakiety, które nie są aktualnie zainstalowane razem z nieużywanymi plikami sync database:

```
 # pacman –Sc 

```

### Downgrade pakietów

Powodów do dezaktualizacji pakietu dostarczyć mogą m.in. błędy w aktualnej wersji pakietu lub brak oczekiwanej funkcjonalności. Korzysta się z tej opcji także wtedy, gdy pakiet został zainstalowany eksperymentalnie. Niezależnie od przyczyny, użytkownik zazwyczaj woli wrócić do starszej wersji niż czekać na nową, poprawioną - zajmuje to mniej czasu i jest teoretycznie mniej kłopotliwe.

Dezaktualizacja jednego pakietu w myśl zależności może "pociągnąć" ich więcej. Przykładowo, gdy zainstalowałeś dużą ilość eksperymentalnych i testowych paczek i wyedytowałeś sporą część plików konfiguracyjnych, może być prościej zainstalować system od nowa niż próbować dezaktualizację.

Tak czy inaczej, musisz pamiętać o kilku sprawach:

*   Po pierwsze, możliwe, że będziesz musiał zdezaktualizować więcej niż 1 lub 2 pakiety. Wymagane biblioteki często zmieniają się z wersją programu i ich funkcjonalność może różnić się w stosunku do poprzedniej wersji.
*   Po drugie, musisz sprawdzić, czy potrzebne pliki zostały usunięte z systemu i jeśli tak, czy możesz je pobrać z innego źródła. Repozytoria Archa są aktualizowane bez pozostawiania poprzednich wersji.
*   Po trzecie, musisz być ostrożny ze zmianami w plikach konfiguracyjnych oraz skryptami. Na chwilę obecną będziemy polegać na Pacmanie, dopóki nie będziemy musieli ominąć pewnych zabezpieczeń, włącznie z nadpisywaniem plików.

Pierwsze miejsce, do którego powinieneś się udać w poszukiwaniu poprzedniej wersji pakietu jest `/var/cache/pacman/pkg` na Twoim komputerze i sprawdzenie, czy został tam zachowany. Warunek jest tylko jeden - jeżeli nie wyczyściłeś pamięci podręcznej Pacmana (`pacman -Scc`). Jeśli go znalazłeś, zainstaluj go za pomocąpolecenia:

```
# pacman -U nazwa_pakietu.pkg.tar.xz

```

Upewnij się, że jest to starsza wersja, a nie ta obecna w systemie. Polecenie usunie zainstalowany pakiet i zastąpi go tym wskazanym przez Ciebie. Nie przywróci automatycznie starych wersji zależności - musisz to zrobić ręcznie przed samym programem. Możesz także zignorować wymagane wersje bibliotek za pomocą przełącznika `d`. Na przykład:

```
# pacman -Ud nazwa_pakietu-starsza_wersja.pkg.tar.xz

```

Jednak, prawdopodobnie wpłynie to negatywnie na stabilność systemu.

Sprawdź nieaktualne serwery. Możesz sprawdzić konkretnie które to są ze [strony monitorującej stan serwerów](https://www.archlinux.de/?page=MirrorStatus;orderby=syncdelay;sort=1).

Gdy już poosiadasz wybraną wersję pakietu, możesz już usunąć najnowszą wersję pakietu X za pomocą polecenia

```
# pacman -Rd nazwa_pakietu

```

a następnie zainstalać starszą paczkę używając polecenia:

```
# pacman -U nazwa_pakietu.pkg.tar.xz

```

#### Archiwa Archa

Jeżeli nie znalazłeś starszej wersji pakietu w systemie, możesz skorzystać z dostępnych archiwów.

##### Arch Linux Archive

[Arch Linux Archive (ALA)](https://archive.archlinux.org/), znane wcześniej pod nazwą Arch Linux Rollback Machine (ARM), przechowuje oficjalne snapshoty repozytoriów, obrazy iso i pliki tarball. Może zostać wykorzystane do:

*   Downgrade do poprzedniej wersji pakietu (np. kiedy najnowsza nie działa poprawnie);
*   Odtworzenia wszystkich pakietów w stanie z pewnego konkretnego momentu (np. kiedy system nie działa, chcę wrócić do stanu sprzed dwóch miesięcy);
*   Znalezienie poprzedniej wersji obrazu ISO.

##### Arch Linux Historical Archive

Co jakiś czas stare pakiety są usuwane z bieżącego archiwum ALA i przesuwane do [dedykowanego archiwum w serwisie archive.org](https://archive.org/details/archlinuxarchive).

**Rekompilacja pakietu**

W najgorszym przypadku, jeśli nie znajdziesz nigdzie swojego pakietu, będziesz musiał skompilować starszą wersję samodzielnie. Będziesz potrzebował pliku PKGBUILD pakietu. Możesz go stworzyć samodzielnie, edytować dostarczony przez [ABS](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)") lub poszukać go [tutaj](https://www.archlinux.org/packages/).

### Inne użycie

Pacman jest rozbudowanym narzędziem, dlatego daje ci jeszcze inne możliwości.

Pobranie pakietu bez instalowania go:

```
# pacman -Sw nazwa_pakietu

```

Instalowanie pakietu, który jest na dysku (już pobrany):

```
# pacman -U /ścieżka/do/pakietu/nazwa_pakietu.pkg.tar.gz

```

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
XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u             # Określasz, z jakiego menedżera pobierania plików będzie korzystał Pacman
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

 `/etc/pacman.conf`  `XferCommand = /usr/bin/wget -c --passive-ftp -c %u` 

*   aria2

Jest to menedżer pobierania obsługujący wstrzymywanie i pobieranie segmentowe. Segmentowe znaczy, że tworzy kilka połączeń z serwerem (lub kilkoma) w tym samym czasie,czego efektem jest krótszy czas pobrania pakietu.

```
# pacman -S aria2

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/aria2c –no-conf -c -s 2 -m 2 -d / -o %o %u` 

*   snarf

```
# pacman -S snarf

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/snarf -N %u` 

*   lftp

```
# pacman -S lftp

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/lftp -c pget %u` 

*   axel

```
# pacman -S axel

```

Następnie dodajemy do sekcji `[options]` w pliku `/etc/pacman.conf`:

 `/etc/pacman.conf`  `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u` 

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