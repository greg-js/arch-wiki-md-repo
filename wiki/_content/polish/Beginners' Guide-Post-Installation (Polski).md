**Tip:** To część wielostronicowego artykułu Przewodnik Początkującego. **[Kliknij tutaj](/index.php/Beginners%27_guide_(Polski) "Beginners' guide (Polski)")** jeśli wolisz czytać przewodnik w całości.

## Contents

*   [1 Post-Installation](#Post-Installation)
    *   [1.1 Aktualizacja](#Aktualizacja)
        *   [1.1.1 Synchronizacja i aktualizacja systemu używając pacmana](#Synchronizacja_i_aktualizacja_systemu_u.C5.BCywaj.C4.85c_pacmana)
        *   [1.1.2 Zapoznanie się z pacmanem](#Zapoznanie_si.C4.99_z_pacmanem)
        *   [1.1.3 /etc/pacman.conf](#.2Fetc.2Fpacman.conf)
            *   [1.1.3.1 Repozytoria pakietów](#Repozytoria_pakiet.C3.B3w)
            *   [1.1.3.2 AUR](#AUR)
        *   [1.1.4 Mirrory](#Mirrory)
            *   [1.1.4.1 Wybranie aktualnych mirrorów](#Wybranie_aktualnych_mirror.C3.B3w)
            *   [1.1.4.2 Użycie najszybszych mirrorów](#U.C5.BCycie_najszybszych_mirror.C3.B3w)
            *   [1.1.4.3 Odświeżenie listy pakietów](#Od.C5.9Bwie.C5.BCenie_listy_pakiet.C3.B3w)
        *   [1.1.5 Inicjalizacja weryfikacji pakietów](#Inicjalizacja_weryfikacji_pakiet.C3.B3w)
        *   [1.1.6 Aktualizacja systemu](#Aktualizacja_systemu)
            *   [1.1.6.1 Ignorowanie pakietów](#Ignorowanie_pakiet.C3.B3w)
            *   [1.1.6.2 Model ciągłego wydania Archa](#Model_ci.C4.85g.C5.82ego_wydania_Archa)
    *   [1.2 Dodawanie użytkownika](#Dodawanie_u.C5.BCytkownika)
        *   [1.2.1 Metoda interaktywna](#Metoda_interaktywna)
        *   [1.2.2 Metoda nieinteraktywna](#Metoda_nieinteraktywna)
        *   [1.2.3 Usuwanie konta użytkownika](#Usuwanie_konta_u.C5.BCytkownika)
        *   [1.2.4 Więcej informacji](#Wi.C4.99cej_informacji)

## Post-Installation

**Gratulujemy i witamy w twoim nowym systemie Arch Linux!**

Twój nowy system Arch Linux to funkcjonalne środowisko GNU/Linux gotowe do personalizacji. Możesz zbudować elegancki zbiór potrzebnych Ci narzędzi lub cokolwiek chcesz czy potrzebujesz do swoich celów.

Zaloguj się na konto roota. Przeprowadzimy konfiguracją pacmana i aktualizację systemu jako root.

**Note:** Konsole wirtualne 1-6 są dostępne. Możesz przełączać się między nimi używając `Alt+F1...F6`

### Aktualizacja

#### Synchronizacja i aktualizacja systemu używając pacmana

Teraz zaktualizujemy system używając [pacmana](/index.php/Pacman_(Polski) "Pacman (Polski)"). Pacman to menedżer pakietów (**pac**kage **man**ager) Arch Linuksa. Zarządza całym systemem pakietów i pozwala na instalację, usunięcie, downgrade pakietu (korzystając z cache), zarządzanie własnoręcznie skompilowanymi pakietami, automatyczne rozwiązywanie zależności, lokalne i zdalne szukanie, i wiele więcej. Pacman będzie używany do ściągnięcia pakietów z zewnętrznego repozytorium i ich instalacji w twoim systemie.

#### Zapoznanie się z pacmanem

Pacman to najlepszy przyjaciel użytkownika Archa. Nauczenie się, jak używać **pacman**a jest mocno zalecane. Spróbuj:

 `$ man pacman` 
**Tip:** Jeśli uważasz linie tekstu za zbyt długie, możesz wyeksportować zmienną `$MANWIDTH`: `# export MANWIDTH=80` 

Po więcej informacji, zobacz stronę [Pacman](/index.php/Pacman_(Polski) "Pacman (Polski)") lub przeczytaj [Pacman rosetta](/index.php/Pacman_rosetta "Pacman rosetta"), jeśli szukasz porównania działania pacmana z innymi menedżerami pakietów.

#### /etc/pacman.conf

Żeby wprowadzić zmiany dotyczące wyboru repozytoriów lub opcji pacmana, edytuj `pacman.conf`:

```
# nano /etc/pacman.conf

```

Repozytoria są opisane niżej; włącz wybrane repozytoria usuwając # z początku linii 'Include =' i '[repozytorium]'.

##### Repozytoria pakietów

[Repozytorium](https://en.wikipedia.org/wiki/software_repository Arch Linuksa (deweloperzy i [Zaufani Użytkownicy](/index.php?title=Trusted_Users_(Polski)&action=edit&redlink=1 "Trusted Users (Polski) (page does not exist)")) opiekują się pakietami w oficjalnych repozytoriach, zawierającymi niezbędne i popularne oprogramowanie, łatwo dostępne za pomocą [pacmana](/index.php/Pacman_(Polski) "Pacman (Polski)"). Ten artykuł opisuje tylko oficjalne repozytoria. Zobacz [Oficjalne repozytoria](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)") po więcej informacji dotyczących szczegółów i zawartości każdego repozytorium.

**Note:** Gdy wybierasz repozytoria, upewnij się, że odblokowałeś tak linie nagłówkową `[*repo_name*]`, jak i pozostałe linie, w przeciwnym wypadku repozytorium pozostanie pominięte przy aktualizacji! To bardzo powszechny błąd. Przykładowy wpis powinien wyglądać tak, jak poniżej.

Większość użytkowników powinna wybrać [core], [extra] i [community]. Jeśli chcesz używać aplikacji 32-bitowych w systemie 64-bitowym, włącz repozytorium [multilib] dodając te linie do `/etc/pacman.conf`:

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

Jeżeli zależy Ci na oprogramowaniu niedostępnym bezpośrednio z pacmana, powinieneś zainteresować się [AUR](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)").

##### AUR

**[Arch User Repository](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)")** (Repozytorium Użytkowników Archa, AUR) zawiera gałęzie [community] i [unsupported]. Inaczej niż inne gałęzie, [unsupported] nie zawiera binarnych pakietów i nie może być używane bezpośrednio przez pacmana. Ta gałąź to zbiór skryptów [PKGBUILD](/index.php/PKGBUILD_(Polski) "PKGBUILD (Polski)") napisancyh przez użytkowników Archa służacych do budowania pakietów ze źródeł z użyciem [Arch Build System](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)"). Oprogramowanie z [unsupported] zwykle nie jest dostępne w innych repozytoriach. Kiedy pakiet z [unsupported] zbierze wystarczająco dużo głosów, może zostać przeniesiony do [community], jeśli jeden z [Zaufanych użytkowinków](/index.php?title=Trusted_Users_(Polski)&action=edit&redlink=1 "Trusted Users (Polski) (page does not exist)") jest chętny do zaadoptowania go.

**Note:** Dostępnych jest wiele nakładek na pacmana (**[AUR Helpers_(Polski)](/index.php?title=AUR_Helpers_(Polski)&action=edit&redlink=1 "AUR Helpers (Polski) (page does not exist)")**), które umożliwiają transparentny dostęp do AUR.

#### Mirrory

Te same pakiety Archa są przechowywane na wielu serwerach na całym świecie. Wybrane mirrory są wypisane w `/etc/pacman.d/mirrorlist` i uporządkowane według priorytetu. Początkowo `/etc/pacman.d/mirrorlist` zawiera listę wszystkich dostępnych mirrorów, z których część powinna zostać włączona aby przejść dalej.

**Note:** Jeśli twój nośnik instalacyjny jest stary, plik `mirrorlist` może być przestarzały, co może powodować problemy przy aktualizacji Arch Linuksa z użyciem pacmana (zobacz [FS#22510](https://bugs.archlinux.org/task/22510)). Dlatego polecane jest uzyskanie aktualnej listy mirrorów w sposób opisany poniżej.

##### Wybranie aktualnych mirrorów

[Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/) pokazuje różne paraemtry mirrorów, takie jak problemy z siecią, zbiorem pakietów, czas ostatniej synchronizacji, itp. [Mirrorlist Generator](https://archlinux.org/mirrorlist/) używa tych informacji do automatycznej oceny mirrorów znajdujących się najbliżej ciebie według tego, jak są aktualne. Wygenerowana lista może być wstawiona do pliku `/etc/pacman.d/mirrorlist`. Możesz oczywiście odkomentować dowolny mirror (usuń '#' z początku wpisu, aby go odkomentować).

Zobacz [Oficjalne Repozytoria](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)"), by dowiedzieć się więcej, m.in. szczegółów nt zawartości każdego z repozytoriów.

##### Użycie najszybszych mirrorów

Aby użyć najszybszych mirrorów, odwołaj się do [Mirrors_(Polski)#Sortowanie mirrorów](/index.php?title=Mirrors_(Polski)&action=edit&redlink=1 "Mirrors (Polski) (page does not exist)").

##### Odświeżenie listy pakietów

Po edycji repozytoriów powinieneś zaktualizować listę pakietów wywołując `pacman` z opcjami `-Sy`. Jeżeli tego nie zrobisz, otrzymasz komunikat "warning: database file for 'multilib' does not exist" podczas kolenego skorzystania z pacmana.

Zmuś pacmana do odświeżenia wszystkich list pakietów z nowego pliku mirrorlist używając:

 `# pacman -Syy` 

Użycie dwóch parametrów `--refresh` lub `-y` zmusza pacmana do odświeżenia wszystkich list pakietów, nawet jeśli uważa je za aktualne. Uruchomienie `pacman -Syy` *przy każdej zmianie mirrorów*, jest dobrą praktyką i oszczędzi wielu problemów.

**Note:** Część problemów zgłaszanych na [forum Arch Linuksa](https://bbs.archlinux.org/) dotyczy problemów z siecią, które nie pozwalają pacmanowi na odświeżenie/aktualizację repozytoriów (zobacz [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) i [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728)). W natywnej instalacji Archa, te problemy mogą zostać rozwiązane przez zmianę programu do pobierania danych używanego przez pacmana (zobacz [Improve Pacman Performance_(Polski)](/index.php?title=Improve_Pacman_Performance_(Polski)&action=edit&redlink=1 "Improve Pacman Performance (Polski) (page does not exist)") po więcej szczegółów). W przypadku Archa będącego gościem w [VirtualBox](/index.php?title=VirtualBox_(Polski)&action=edit&redlink=1 "VirtualBox (Polski) (page does not exist)"), rozwiązaniem jest użycie "Host interface" zamiast "NAT" w ustawieniach maszyny.

#### Inicjalizacja weryfikacji pakietów

Aby zainicjować weryfikację pakietów, możesz postępować według [poniższych kroków](https://www.archlinux.org/news/having-pacman-verify-packages/). Zobacz [Pacman-key](/index.php?title=Pacman-key_(Polski)&action=edit&redlink=1 "Pacman-key (Polski) (page does not exist)") po więcej informacji.

 `$ pacman-key --init` 

Aby wygenerować główny klucz (master key), [potrzebna jest entropia](/index.php?title=Pacman-key_(Polski)&action=edit&redlink=1 "Pacman-key (Polski) (page does not exist)"). Powinieneś(aś) naciskać losowe klawisze, ruszać myszą lub przełączyć się do innej konsoli i uruchomić obciążającą dysk komendę, przykładowo `ls -R /`. Po zakończeniu komendy pacman-key, uruchom to polecenie, aby skonfigurować inne klucze.

 `$ pacman-key --populate archlinux` 

Zweryfikuj [Master Signing Keys](https://www.archlinux.org/master-keys/) będąc pytanym(ą), ponieważ są one używane do podpisywania (a przez to zaufania) wszystkich innych kluczy opiekunów pakietów.

#### Aktualizacja systemu

**Warning:** Aktualizacje systemu powinny być przeprowadzane z ostrożnością. Bardzo ważne jest przeczytanie [tego](https://bbs.archlinux.org/viewtopic.php?id=57205) przed kontynuacją.

Deweloperzy często dostarczają ważne informacje dotyczące konfiguracji i modyfikacji dotyczących znanych usterek. Użytkownik Arch Linuksa powinien zpoznać się z tymi treściami przed dokonaniem aktualizacji:

*   [Aktualności Archa](https://archlinux.org/news/). Jeśli nie przeczytałeś(aś) tego przed aktualizacją i napotkałeś błąd, przeczytaj aktualności *zanim* napiszesz post lub zapytanie na forum!
*   [Lista mailingowa arch-announce](https://archlinux.org/pipermail/arch-announce/).

Zsynchronizuj, odśwież, i zaktualizuj cały system używając:

 `# pacman -Syu` 

lub:

 `# pacman --sync --refresh --sysupgrade` 

Pacman ściągnie świeżą kopię listy pakietów z serwerów, które zdefiniowałeś(aś) w `/etc/pacman.conf` i przeprowadzi wszystkie dostępne aktualizacje. Możesz zostać zapytany(a) o aktualizację samego pacmana jako pierwszego. W takim przypadku, wpisz yes, a po zakończeniu ponów polecenie `pacman -Syu`.

Uruchom system ponownie, jeśli nastąpiła aktualizacja kernela.

**Note:** Sporadycznie, podcas aktualizacji mogą nastąpić zmiany w konfiguracji wymagające interwencji użytkownika; przeczytaj wyjście pacmana po wszystkie potrzebne informacje. Przeczytaj [Pliki pacnew i pacsave](/index.php?title=Pacnew_and_Pacsave_Files_(Polski)&action=edit&redlink=1 "Pacnew and Pacsave Files (Polski) (page does not exist)") po więcej szczegółów.

Wyjście pacmana zapisywane jest w `/var/log/pacman.log`.

Zobacz [FAQ](/index.php?title=FAQ_(Polski)&action=edit&redlink=1 "FAQ (Polski) (page does not exist)") po odpowiedzi na najczęściej zadawane pytania dotyczące aktualizacji i zarządzania pakietami.

##### Ignorowanie pakietów

Po uruchomieniu polecenia `pacman -Syu`, cały system zostanie zaktualizowany. Można jednak uniemożliwić przeprowadzenie aktualizacji wybranego pakietu. Typowym scenariuszem może być aktualizacja pakietu, która sprawia problemy z resztą systemu. W takim przypadku, dostępne są dwie opcje; wskaż pakiet(y) jako przeznaczone do pominięcia używając parametru `--ignore` (zobacz `pacman -S --help` po szczegóły) lub trwale oznacz pakiet jako ignorowany dopisując go do linii `IgnorePkg` w pliku `/etc/pacman.conf`. Po więcej informacji, zobacz stronę [Pacman](/index.php/Pacman_(Polski) "Pacman (Polski)").

Pamiętaj, że administrator powinien aktualizować **cały** system używając `pacman -Syu`, zamiast aktualizować wybrane pakiety. Możesz odejść od tego postępowania jeśli chcesz, wiedz jednak, że wiąże się to z większą szansą nieprawidłowego działania systemu lub nawet jego zepsuciem. Większość problemów wynika z selektywnej aktualizacji, ninestandardowej kompilacji i nieprawidłowej instalacji oprogramowania. Użycie `IgnorePkg` w `/etc/pacman.conf` jest więc niezalecane i powinno być stosowane oszczędnie, i jeśli wiesz co robisz. Używanie `IgnorePkg` jest analogiczne do "utraty gwarancji".

##### Model ciągłego wydania Archa

Pamiętaj, że Arch jest dystrybucją **ciągłego wydania**. Oznacza to, że użytkownik nie musi reinstalować lub przeprowadzać skomplikowanych aktualizacji do najnowszego wydania. Uruchamianie `pacman -Syu` cyklicznie (i pamiętanie o powyższym ostrzeżeniu) utrzymuje cały system aktualnym. Pamiętaj o **ponownym uruchomieniu**, jeśli nastąpiła aktualizacja jądra.

### Dodawanie użytkownika

**Warning:** Linux jest środowiskiem wieloużytkownikowym. Nie powinieneś(aś) używać konta roota do codziennych zadań, jest to zła i bardzo niebezpieczna praktyka: konto roota powinno być używane tylko do administracji.

Dodaj konto zwykłego użytkownika, używając jednej z następujących metod. W tym przykładzie stworzymy użytkownika *archie*:

#### Metoda interaktywna

 `# adduser` 

Zostaniesz poproszony(a) o wprowadzenie kilku informacji w sposób interaktywny:

```
Login name for new user []: **archie**

User ID ('UID') [ defaults to next available ]:

Initial group [ users ]:

Additional groups (comma separated) []: **audio,games,lp,optical,power,scanner,storage,video**

Home directory [ /home/archie ]:

Shell [ /bin/bash ]:

Expiry date (YYYY-MM-DD) []:

```

Jak pokazano w przykładzie, powinieneś(aś) wprowadzić dane tylko w *Login name* (Login) i *Additional groups* (Dodatkowe grupy), pozostawiając resztę pól pustą.

Lista *Additional groups* (Dodatkowych grup) w przykładzie jest typowa dla komputera domowego, jest więc polecana dla początkujacych:

*   **audio** - do działań związanych z kartą dźwiękową i powiązanym oprogramowaniem
*   **games** - do możliwości zapisu dla gier
*   **lp** - do zarządzania drukowaniem
*   **optical** - do zarządzania napędami optycznymi
*   **power** - do zezwalania na interakcję z opcjami zasilania (np. wyłączanie dedykowanym przyciskiem)
*   **scanner** - do używania skanera
*   **storage** - do zarządzania urządzeniami przechowującymi dane
*   **video** - do działań związanych z grafiką i akceleracją sprzętową

Po więcej informacji o wypisanych i innych grupach, zobacz [Groups_(Polski)#User groups](/index.php?title=Groups_(Polski)&action=edit&redlink=1 "Groups (Polski) (page does not exist)").

Następnie zostanie wyświetlony podgląd nowego konta i możliwość anulowania lub kontynuowania operacji: po naciśnięciu `Enter` konto zostanie stworzone i zostaniesz poproszony(a) o podanie dodatkowych, opcjonalncyh informacji o nowym użytkowniku (np. imię i nazwisko). Potem zostaniesz poproszony(a) o ustawienie hasła do konta.

#### Metoda nieinteraktywna

 `# useradd -m -g users -G audio,games,log,lp,optical,power,scanner,storage,video -s /bin/bash archie` 

Bedziesz musiał(a) ustawić hasło do konta używając `passwd`. Możesz wprowadzić dodatkowe informacje używajac `chfn`.

Można też użyć:

```
# useradd -m -g users -G wheel -s /bin/bash *archie*

```

Użytkownik dostanie wszelakie prawa przysługujące grupie wheel.

#### Usuwanie konta użytkownika

W razie błędu lub gdy chcesz usunąć konto, użyj `userdel`:

 `# userdel -r [nazwaużytkownika]` 

Opcja `-r` usunie także katalog domowy użytkownika wraz z zawartością i jego skrzynkę mailową.

#### Więcej informacji

Przeczytaj [Użytkownicy i grupy](/index.php?title=Users_and_Groups_(Polski)&action=edit&redlink=1 "Users and Groups (Polski) (page does not exist)") po dalsze informacje. Jeśli chcesz zmienić nazwę swojego lub innego użytkownika, przeczytaj stronę [Zmiana nazwy użytkownika](/index.php?title=Change_username_(Polski)&action=edit&redlink=1 "Change username (Polski) (page does not exist)"). Możesz też sprawdzić strony man: `usermod(8)` i `gpasswd(8)`.