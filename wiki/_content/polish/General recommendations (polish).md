Related articles

*   [Frequently asked questions (Polski)](/index.php/Frequently_asked_questions_(Polski) "Frequently asked questions (Polski)")
*   [Installation guide (Polski)](/index.php/Installation_guide_(Polski) "Installation guide (Polski)")
*   [List of applications](/index.php/List_of_applications "List of applications")

Ten dokument to zbiór popularnych artykułów i przydatnych informacji o dodawaniu funkcjonalności do zainstalowanego systemu Arch. Zakłada się, że czytelnicy przeczytali i wykonali instrukcje zawarte w [Installation guide (Polski)](/index.php/Installation_guide_(Polski) "Installation guide (Polski)") i zainstalowali podstawowy system. Zaznajomienie się z informacjami zawartymi w [#Administracja systemem](#Administracja_systemem) i [#Zarządzanie pakietami](#Zarządzanie_pakietami) jest *niezbędne* do zrozumienia innych sekcji tej strony i pozostałych stron na Wiki.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Administracja systemem](#Administracja_systemem)
    *   [1.1 Użytkownicy i grupy](#Użytkownicy_i_grupy)
    *   [1.2 Podniesienie uprawnień](#Podniesienie_uprawnień)
    *   [1.3 Zarządzanie usługami](#Zarządzanie_usługami)
    *   [1.4 Bieżąca konserwacja systemu](#Bieżąca_konserwacja_systemu)
*   [2 Zarządzanie pakietami](#Zarządzanie_pakietami)
    *   [2.1 pacman](#pacman)
    *   [2.2 Repozytoria](#Repozytoria)
    *   [2.3 Serwery lustrzane](#Serwery_lustrzane)
    *   [2.4 Arch Build System](#Arch_Build_System)
    *   [2.5 Arch User Repository](#Arch_User_Repository)
*   [3 Uruchamianie](#Uruchamianie)
    *   [3.1 Automatyczne rozpoznawanie sprzętu](#Automatyczne_rozpoznawanie_sprzętu)
    *   [3.2 Mikrokod](#Mikrokod)
    *   [3.3 Ukrywanie komunikatów rozruchowych](#Ukrywanie_komunikatów_rozruchowych)
    *   [3.4 Aktywacja Num Lock](#Aktywacja_Num_Lock)
*   [4 Graficzny interfejs użytkownika](#Graficzny_interfejs_użytkownika)
    *   [4.1 Serwer wyświetlania](#Serwer_wyświetlania)
    *   [4.2 Sterowniki graficzne](#Sterowniki_graficzne)
    *   [4.3 Środowiska pulpitu](#Środowiska_pulpitu)
    *   [4.4 Menedżery okien](#Menedżery_okien)
    *   [4.5 Menedżer wyświetlania](#Menedżer_wyświetlania)
*   [5 Zarządzanie energią](#Zarządzanie_energią)
    *   [5.1 Zdarzenia ACPI](#Zdarzenia_ACPI)
    *   [5.2 Skalowanie procesora](#Skalowanie_procesora)
    *   [5.3 Laptopy](#Laptopy)
    *   [5.4 Wstrzymanie i hibernacja](#Wstrzymanie_i_hibernacja)
*   [6 Multimedia](#Multimedia)
    *   [6.1 Dźwięk](#Dźwięk)
    *   [6.2 Wtyczki przeglądarek](#Wtyczki_przeglądarek)
    *   [6.3 Kodeki](#Kodeki)
*   [7 Sieć](#Sieć)
    *   [7.1 Synchronizacja zegara](#Synchronizacja_zegara)
    *   [7.2 Zabezpieczenia DNS](#Zabezpieczenia_DNS)
    *   [7.3 Konfigurowanie zapory sieciowej](#Konfigurowanie_zapory_sieciowej)
    *   [7.4 Udostępnianie zasobów (w tym plików)](#Udostępnianie_zasobów_(w_tym_plików))
*   [8 Urządzenia wejściowe](#Urządzenia_wejściowe)
    *   [8.1 Układy klawiatury](#Układy_klawiatury)
    *   [8.2 Przyciski myszki](#Przyciski_myszki)
    *   [8.3 Płytki dotykowe (tzw. touchpady) w laptopach](#Płytki_dotykowe_(tzw._touchpady)_w_laptopach)
    *   [8.4 Urządzenia typu TrackPoint](#Urządzenia_typu_TrackPoint)
*   [9 Optymalizacja](#Optymalizacja)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Zwiększanie wydajności](#Zwiększanie_wydajności)
    *   [9.3 Dyski SSD](#Dyski_SSD)
*   [10 Usługi systemowe](#Usługi_systemowe)
    *   [10.1 Indeksowanie plików i wyszukiwanie](#Indeksowanie_plików_i_wyszukiwanie)
    *   [10.2 Poczta lokalna](#Poczta_lokalna)
    *   [10.3 Drukowanie](#Drukowanie)
*   [11 Wygląd](#Wygląd)
    *   [11.1 Czcionki](#Czcionki)
    *   [11.2 Motywy GTK i Qt](#Motywy_GTK_i_Qt)
*   [12 Ulepszenia konsoli](#Ulepszenia_konsoli)
    *   [12.1 Aliasy](#Aliasy)
    *   [12.2 Alternatywne powłoki](#Alternatywne_powłoki)
    *   [12.3 Dodatki Bash](#Dodatki_Bash)
    *   [12.4 Kolorowy tekst w konsoli](#Kolorowy_tekst_w_konsoli)
    *   [12.5 Pliki skompresowane i archiwa](#Pliki_skompresowane_i_archiwa)
    *   [12.6 Monit konsoli](#Monit_konsoli)
    *   [12.7 Emacs shell](#Emacs_shell)
    *   [12.8 Obsługa myszy](#Obsługa_myszy)
    *   [12.9 Przewijanie tekstu w konsoli](#Przewijanie_tekstu_w_konsoli)
    *   [12.10 Zarządzanie sesją](#Zarządzanie_sesją)

## Administracja systemem

Ta sekcja mówi o zadaniach administracyjnych i zarządzaniu systemem. Jeśli chcesz dowiedzieć więcej, odwiedź [Core utilities](/index.php/Core_utilities "Core utilities") i [Category:System administration](/index.php/Category:System_administration "Category:System administration")

### Użytkownicy i grupy

Na nowej instalacji posiadasz tylko konto super-użytkownika, lepiej znanego jako "root". Logowanie się jako root przez dłuższy okres czasu, może nawet odsłanianie go przez [SSH](/index.php/SSH "SSH"), [jest niebezpieczne](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Zamiast tego, powinieneś stworzyć i używać do większości zadań nieuprzywilejowanego konta użytkownika, a konta root tylko do administracji systemem. Zobacz [Users and groups](/index.php/Users_and_groups "Users and groups") żeby uzyskać więcej informacji o tym, jak utworzyć i skonfigurować nowe konto użytkownika.

Grupy i użytkownicy są mechanizmem *kontroli dostępu*; administratorzy mogą dostosować członkostwo i właściwości grup żeby przyznać lub odmówić użytkownikom i usługom dostępu do zasobów systemu. Przeczytaj [Users and groups](/index.php/Users_and_groups "Users and groups") żeby uzyskać dodatkowe informacje dotyczące potencjalnych zagrożeń dla bezpieczeństwa.

### Podniesienie uprawnień

Komenda [su](/index.php/Su "Su") (ang. *substitute user*) umożliwia przyjęcie tożsamości innego użytkownika systemu (najczęściej root'a) z poziomu zalogowanego użytkownika, natomiast komenda [sudo](/index.php/Sudo "Sudo") (ang. *substitute user do*) tymczasowo podnosi uprawnienia dla pojedynczej komendy.

### Zarządzanie usługami

Arch Linux używa [systemd](/index.php/Systemd "Systemd") jako procesu [uruchamiającego](/index.php/Init "Init"). Jest on menadżerem systemu i usług dla Linuxa. Jeśli chcesz utrzymać swój system w dobrej kondycji, zalecane jest, aby poznać jego podstawy. Interakcje z *systemd* są wykonywane za pośrednictwem komendy *systemctl*. Przeczytaj [systemd](/index.php/Systemd "Systemd") żeby uzyskać więcej informacji.

### Bieżąca konserwacja systemu

Arch jest systemem o częstych aktualizacjach i zmianach w pakietach, więc użytkownicy muszą poświęcić trochę czasu na [konserwację systemu](/index.php/System_maintenance "System maintenance"), aby poprawić jego działanie i zwiększyć jego wydajność.

Ważne jest także zadbanie o bezpieczeństwo systemu. Przeczytaj [Security](/index.php/Security "Security") żeby dowiedzieć się jak zabezpieczyć swój system przed atakami.

## Zarządzanie pakietami

Ta sekcja zawiera pomocne informacje dotyczące zarządzania oprogramowaniem (pakietami). Odwiedź [Frequently asked questions (Polski)#Zarządzanie pakietami](/index.php/Frequently_asked_questions_(Polski)#Zarządzanie_pakietami "Frequently asked questions (Polski)") i [Category:Package management (Polski)](/index.php/Category:Package_management_(Polski) "Category:Package management (Polski)") aby dowiedzieć się więcej na ten temat.

**Note:** Należy prześledzić informacje o aktualizacjach pakietów, które wymagają interwencji użytkownika, *zanim* zostanie wszczęta aktualizacja. Zapisz się do [tej listy mailingowej](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) albo sprawdzaj stronę główną [[1]](https://www.archlinux.org/) przed każdą aktualizacją pakietów. Możesz też zasubskrybować [ten kanał RSS](https://www.archlinux.org/feeds/news/) albo śledzić [@archlinux](https://twitter.com/archlinux) na Twitterze.

### pacman

[pacman](/index.php/Pacman "Pacman") jest menedżerem pakietów w Arch Linux. Każdy użytkownik powinien zapoznać się z jego działaniem przed przystąpieniem do dalszej lektury artykułów na Wiki.

Przeczytaj [pacman tips](/index.php/Pacman_tips "Pacman tips") aby zapoznać się ze wskazówkami, jak usprawnić użytkowanie *pacmana* i zarządzanie pakietami w ogólności.

### Repozytoria

Zapoznaj się z [działem o oficjalnych repozytoriach](/index.php/Official_repositories "Official repositories") aby poznać szczegóły dotyczącego każdego z zarządzanych przez społeczność Arch repozytoriami.

Jeśli zainstalowałeś Arch Linux, ale masz zamiar używać aplikacji 32-bitowych, powinieneś włączyć repozytoria [multilib](/index.php/Multilib "Multilib").

[Nieoficjalne repozytoria użytkowników](/index.php/Unofficial_user_repositories "Unofficial user repositories") zawierają listę innych repozytoriów nieoficjalnych, zarządzanych przez użytkowników.

### Serwery lustrzane

Odwiedź stronę [Mirrors](/index.php/Mirrors "Mirrors"), aby w pełni wykorzystać potencjał serwerów lustrzanych i skonfigurować je w ten sposób, aby używać tych najszybszych i najświeższych. Jak wyjaśniono w artykule, zalecane jest aby śledzić stronę [Mirror Status](https://www.archlinux.org/mirrors/status/) lub [Mirror-Status](http://www.archlinux.de/?page=MirrorStatus) aby pozyskać listę serwerów, które zostały ostatnio zsynchronizowane.

### Arch Build System

*Ports* to system początkowo używany przez dystrybucje BSD, składający się ze skryptów kompilacji, które znajdują się w systemie lokalnym. Mówiąc najprościej, każdy port zawiera skrypt w katalogu intuicyjnie nazwanym na podstawie instalowalnej aplikacji.

Drzewo [ABS](/index.php/ABS "ABS") oferuje tę samą funkcjonalność, udostępniając skrypty budowania o nazwie [PKGBUILD](/index.php/PKGBUILD "PKGBUILD"), które są zawierają informacje dotyczące danego oprogramowania; skróty integralności, adres URL projektu, wersję, licencje i instrukcje budowania. PKGBUILD są następnie analizowane przez [makepkg](/index.php/Makepkg "Makepkg"), program generujący pakiety, którymi można łatwo zarządzać za pomocą *pacmana*.

Każda paczka w repozytoriach wraz z tymi znajdującymi się w AUR podlega kompilacji za pomocą „makepkg”.

### Arch User Repository

Podczas gdy drzewo ABS umożliwia tworzenie oprogramowania dostępnego w oficjalnych repozytoriach, [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) jest odpowiednikiem pakietów udostępnianych przez użytkowników. Jest to nieoficjalne repozytorium skryptów kompilacji dostępnych przez [interfejs sieciowy](https://aur.archlinux.org/) lub przez [pomocnika AUR](/index.php/AUR_helper "AUR helper").

## Uruchamianie

Ta sekcja zawiera informacje dotyczące procesu rozruchu. Przegląd procesu rozruchu Arch można znaleźć w [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). Aby uzyskać więcej informacji, zobacz [Category: Boot process](/index.php/Category:Boot_process "Category:Boot process").

### Automatyczne rozpoznawanie sprzętu

Sprzęt [domyślnie] powinien zostać automatyczne wykryty przez [udev](/index.php/Udev "Udev") podczas procesu rozruchu. Poprawę czasu rozruchu można uzyskać wyłączając automatyczne ładowanie modułu i ręcznie określając wymagane moduły, jak opisano w [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules"). Ponadto [Xorg](/index.php/Xorg "Xorg") powinien być w stanie automatycznie wykrywać wymagane sterowniki za pomocą udev, ale użytkownicy mogą również ręcznie skonfigurować serwer X.

### Mikrokod

Procesory mogą zawierać wadliwy kod [[2]](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), który jądro może poprawić, aktualizując *mikrokod* (ang. *microcode*) przy uruchomieniu systemu. Procesory Intel wymagają osobnego pakietu do tego celu. Szczegółowe informacje można znaleźć w [Microcode](/index.php/Microcode "Microcode").

### Ukrywanie komunikatów rozruchowych

Po zakończeniu rozruchu, ekran zostanie wyczyszczony i pojawi się monit z prośbą o zalogowanie, co uniemożliwi użytkownikom zbieranie informacji zwrotnych z procesu rozruchu. Zastosowanie wskazówek z artykułu [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") spowoduje pozostawienie informacji rozruchowych na ekranie.

### Aktywacja Num Lock

Num Lock to klawisz przełączania występujący w większości klawiatur. Aby aktywować przypisanie klawiszy numerycznych podczas uruchamiania, zapoznaj się z [Activating numlock on bootup](/index.php/Activating_numlock_on_bootup "Activating numlock on bootup").

## Graficzny interfejs użytkownika

Ta sekcja zawiera wskazówki dla użytkowników, którzy chcą uruchamiać aplikacje graficzne w swoim systemie. Zobacz [Category: X server](/index.php/Category:X_server "Category:X server"), aby uzyskać dodatkowe informacje.

### Serwer wyświetlania

[Xorg](/index.php/Xorg "Xorg") to publiczna, otwarta implementacja [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (zwykle X11 lub X). Jest niezbędny do uruchamiania aplikacji z graficznym interfejsem użytkownika (GUI), a większość użytkowników zapewne będzie chciała go zainstalować.

[Wayland](/index.php/Wayland "Wayland") to nowy, alternatywny protokół wyświetlania i dostępna jest jego implementacja referencyjna Weston. Domyślnie z Wayland korzysta między innymi [GNOME](/index.php/GNOME "GNOME"), choć serwer ten nie posiada jeszcze tak dobrego wsparcia jak [Xorg](/index.php/Xorg "Xorg") i może powodować problemy na niektórych sprzętach.

### Sterowniki graficzne

Domyślny sterownik ekranu „vesa” będzie działał z większością kart graficznych, ale wydajność grafiki można znacznie poprawić i przede wszystkim wykorzystać wszystkie funkcje karty graficznej, instalując odpowiedni sterownik dla kart [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel") lub [NVIDIA](/index.php/NVIDIA "NVIDIA").

### Środowiska pulpitu

Chociaż Xorg i Wayland stanowią podstawy do budowania środowiska graficznego, dodatkowe komponenty mogą być uznane za niezbędne, aby użytkownik w poczuł się w pełni komfortowo ze swoim systemem. [Środowiska pulpitu](/index.php/Desktop_environment "Desktop environment"), takie jak [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE") i [Xfce](/index.php/Xfce "Xfce") łączą w sobie szeroką gamę *klientów serwera X*, takich jak menedżer okien, panel, menedżer plików, emulator terminala, edytor tekstu, ikony i inne narzędzia. Użytkownicy o mniejszym doświadczeniu mogą chcieć zainstalować środowisko pulpitu, aby uzyskać dostęp do popularnych narzędzi i ułatwić korzystanie z komputera. Zobacz [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments"), aby uzyskać dodatkowe informacje.

### Menedżery okien

Rozwinięte środowisko pulpitu zapewnia pełny i spójny graficzny interfejs użytkownika, ale zwykle zużywa znaczną ilość zasobów systemowych. Użytkownicy, którzy chcą zmaksymalizować wydajność lub w inny sposób uprościć swój system, mogą zdecydować się na instalację [menedżera okien](/index.php/Window_manager "Window manager") i dodatkowe narzędzia niezbędne do pracy z komputerem. Większość środowisk pulpitu umożliwia także korzystanie z menedżera okien alternatywnego wobec tego domyślnie dostarczanego ze środowiskiem. [Dynamiczne](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [nakładalne](/index.php/Category:Stacking_WMs "Category:Stacking WMs") i [kafelkowe](/index.php/Category:Tiling_WMs "Category:Tiling WMs") menedżery okien różnią się w obsłudze rozmieszczenia okien.

### Menedżer wyświetlania

Większość środowisk pulpitu zawiera [menedżer wyświetlania](/index.php/Display_manager "Display manager") do automatycznego uruchamiania środowiska graficznego i zarządzania logowaniami użytkowników. Użytkownicy nieposiadający środowiska graficznego mogą zainstalować je osobno. Możesz również [bezpośrednio uruchomić serwer X](/index.php/Start_X_at_login "Start X at login") co stanowi prostą alternatywę dla menedżera wyświetlania.

## Zarządzanie energią

Ta sekcja może być przydatna dla właścicieli laptopów lub użytkowników szukających w inny sposób kontroli nad zarządzaniem energią. Aby uzyskać więcej informacji, zobacz [Category:Power management](/index.php/Category:Power_management "Category:Power management").

Zobacz [Power management](/index.php/Power_management "Power management"), aby uzyskać więcej informacji.

### Zdarzenia ACPI

Użytkownicy mogą skonfigurować sposób, w jaki system reaguje na zdarzenia ACPI, takie jak naciśnięcie przycisku zasilania lub zamknięcie pokrywy laptopa. Aby zapoznać się z nową (zalecaną) metodą zarządzania tymi zdarzeniami przy użyciu [systemd](/index.php/Systemd "Systemd"), zobacz [Zarządzanie energią za pomocą systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). Aby zapoznać się ze starą metodą, zobacz [acpid](/index.php/Acpid "Acpid").

### Skalowanie procesora

Nowoczesne procesory mogą zmniejszyć częstotliwość i napięcie w celu zmniejszenia zużycia ciepła i energii. Mniej ciepła prowadzi do cichszej pracy systemu i przedłuża żywotność sprzętu. Aby uzyskać szczegółowe informacje, zobacz stronę [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling").

### Laptopy

Artykuły dotyczące komputerów przenośnych wraz z przewodnikami instalacji dla konkretnych modeli znajdują się w [Category: Laptops](/index.php/Category:Laptops "Category:Laptops"). Aby uzyskać ogólny przegląd artykułów i zaleceń dotyczących laptopów, zobacz stronę [Laptop](/index.php/Laptop "Laptop").

### Wstrzymanie i hibernacja

Zobacz główny artykuł: [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Multimedia

[Kategoria Multimedia](/index.php/Category:Multimedia "Category:Multimedia") zawiera dodatkowe informacje.

### Dźwięk

[Dźwięk](/index.php/Sound "Sound") jest dostarczany przez sterowniki dźwięku dostarczane z jądrem:

*   [ALSA](/index.php/ALSA "ALSA") jest dołączony do jądra i jest zalecany, ponieważ zwykle działa on od razu (musi tylko zostać wyłączone [wyciszenie](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") jest realną alternatywą w sytuacji, gdy ALSA nie zadziała.

Użytkownicy mogą dodatkowo chcieć zainstalować i skonfigurować [serwer dźwięku](/index.php/Sound#Sound_servers "Sound"), taki jak [PulseAudio](/index.php/PulseAudio "PulseAudio"). Aby zapoznać się z kwestiami dotyczącymi zaawansowanej konfiguracji dźwięku zapoznaj się ze stroną [professional audio](/index.php/Professional_audio "Professional audio").

### Wtyczki przeglądarek

Aby uzyskać dostęp do niektórych treści internetowych, można zainstalować [wtyczki przeglądarek](/index.php/Browser_plugins "Browser plugins"), takie jak Adobe Acrobat Reader, Adobe Flash Player i Java.

### Kodeki

[Kodeki](/index.php/Codecs "Codecs") są wykorzystywane przez aplikacje multimedialne do kodowania lub dekodowania strumieni audio lub wideo. Aby odtwarzać zakodowane strumienie, użytkownicy muszą upewnić się, że zainstalowano odpowiedni kodek.

## Sieć

Ta sekcja jest ograniczona do najprostszych ustawień sieciowych. Przejdź do [Network configuration](/index.php/Network_configuration "Network configuration"), aby uzyskać pełny przewodnik. Aby uzyskać więcej informacji, zobacz kategorię [Category:Network](/index.php?title=Category:Network&action=edit&redlink=1 "Category:Network (page does not exist)").

### Synchronizacja zegara

[Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) to protokół do synchronizacji zegarów systemów komputerowych w sieciach danych z przełączanymi pakietami i zmiennymi opóźnieniami. Aby zapoznać się z implementacjami tego protokołu, zobacz [Time synchronization](/index.php/Time_synchronization "Time synchronization").

### Zabezpieczenia DNS

Aby zwiększyć bezpieczeństwo podczas przeglądania stron internetowych, płatności online, łączenia się z usługami [SSH](/index.php/SSH "SSH") i podobnych zadań, rozważ użycie oprogramowania klienckiego [DNSSEC](/index.php/DNSSEC "DNSSEC"), które może zatwierdzać podpisane rekordy [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") oraz [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") do szyfrowania ruchu DNS.

### Konfigurowanie zapory sieciowej

[Zapora sieciowa](/index.php/Firewall "Firewall") (ang. *firewall*) może zapewnić dodatkową ochronę sieci w systemie Linux. Chociaż standardowe jądro Arch jest w stanie używać [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter") oraz [iptables](/index.php/Iptables "Iptables"), rozwiązanie to nie jest domyślnie włączone. Zdecydowanie zaleca się skonfigurowanie jakiejś formy zapory sieciowej. Zapoznaj się ze stroną [Firewalls](/index.php/Firewalls "Firewalls"), aby wyszukać dostępne przewodniki.

### Udostępnianie zasobów (w tym plików)

Aby udostępnić pliki między komputerami w sieci, postępuj zgodnie z artykułami dotyczącymi [NFS](/index.php/NFS "NFS") lub [SSHFS](/index.php/SSHFS "SSHFS").

Użyj [Samba](/index.php/Samba "Samba"), aby dołączyć do sieci Windows. Aby skonfigurować urządzenie do korzystania z Active Directory, przeczytaj [Active Directory integration](/index.php/Active_Directory_integration "Active Directory integration").

Zobacz także [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Urządzenia wejściowe

Ta sekcja zawiera popularne wskazówki dotyczące konfiguracji urządzeń wejściowych takich jak myszka i klawiatura. Aby uzyskać więcej informacji, zobacz [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Układy klawiatury

Klawiatury w języku innym niż angielski lub w inny sposób niestandardowe mogą nie działać domyślnie (tak jest z polskim układem klawiatury). Niezbędne kroki w celu skonfigurowania układu klawiszy są różne dla konsoli wirtualnej i [Xorg](/index.php/Xorg "Xorg"). Skonfigurowanie polskiego układu klawiatury w konsoli zostało opisane w [Przewodniku instalacyjnym](/index.php/Installation_guide_(Polski) "Installation guide (Polski)"). Więcej informacji na temat konfiguracji układu klawiatury w Xorg znajdziesz w: [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg").

### Przyciski myszki

Może się okazać, że w bardziej zaawansowanych lub nietypowych myszkach, nie wszystkie przyciski działają prawidłowo. Przydatne instrukcje można znaleźć w [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Płytki dotykowe (tzw. touchpady) w laptopach

Wiele laptopów korzysta z urządzeń wskazujących [Synaptics](http://www.synaptics.com/) lub [ALPS](http://www.alps.com/) zwanych płytkami dotykowymi (ang. *touchpads*). Niektóre płytki dotykowe używają sterownika wejściowego Synaptics (zob. [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")).

### Urządzenia typu TrackPoint

Zobacz artykuł [TrackPoint](/index.php/TrackPoint "TrackPoint"), aby skonfigurować urządzenie typu TrackPoint.

## Optymalizacja

Ta sekcja ma na celu podsumowanie poprawek, narzędzi i dostępnych opcji przydatnych w celu poprawy wydajności systemu i aplikacji.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") to czynność polegająca na mierzeniu wydajności i porównywaniu wyników z wynikami innych systemów z pomocą ujednoliconej procedury.

### Zwiększanie wydajności

Artykuł [Improving performance](/index.php/Improving_performance "Improving performance") zawiera podsumowanie informacje dotyczących wydajności systemu Arch Linux.

### Dyski SSD

Artykuł [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") zawiera informacje dotyczące dysków półprzewodnikowych (SSD), w tym dotyczące ich konfiguracji celem zwiększenia żywotności.

## Usługi systemowe

Ta sekcja dotyczy tzw. [demonów](/index.php/Daemons "Daemons") (ang. *daemons*) czyli usług systemowych. Więcej informacji można znaleźć w [Category:Daemons](/index.php/Category:Daemons "Category:Daemons").

### Indeksowanie plików i wyszukiwanie

Większość dystrybucji udostępnia polecenie `locate`, które służy wyszukiwaniu plików w systemie. Aby uzyskać tę funkcjonalność w Arch Linux, należy zainstalować [mlocate](https://www.archlinux.org/packages/?name=mlocate). Po instalacji powinieneś uruchomić `updatedb`, aby zindeksować systemy plików.

### Poczta lokalna

Domyślna konfiguracja podstawowa nie zapewnia synchronizacji poczty. Aby skonfigurować „Postfix” do prostego dostarczania lokalnej skrzynki pocztowej, zobacz stronę [Postfix](/index.php/Postfix "Postfix"). Inne opcje to [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") i [fdm](/index.php/Fdm "Fdm").

### Drukowanie

[CUPS](/index.php/CUPS "CUPS") to system drukowania open source opracowany przez Apple. Zobacz [Category:Printers](/index.php/Category:Printers "Category:Printers"), aby zapoznać się z artykułami dotyczącymi konfiguracji drukarek.

## Wygląd

Ta sekcja zawiera informacje o tzw. wodotryskach (ang. *eye candy*), czyli funkcjach poprawiających wrażenia estetyczne. Aby uzyskać więcej informacji, zobacz [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Czcionki

Ponieważ w podstawowym systemie Arch zawarte są jedynie nieskalowalne czcionki bitmap, aby poprawić wygląd systemu, możesz zainstalować czcionki TrueType. Pakiet [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) zapewnia zestaw wysokiej jakości czcionek ogólnego zastosowania o dobrej obsłudze znaków [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode").

Więcej informacji na ten temat można znaleźć w artykułach [Fonts](/index.php/Fonts "Fonts") i [Font configuration](/index.php/Font_configuration "Font configuration").

Jeśli spędzasz dużo czasu w wierszu poleceń (tj. bez uruchamiania serwera X), możesz zmienić czcionkę używaną w konsoli, aby zwiększyć czytelność tekstu. Zobacz stronę [Linux console#Fonts](/index.php/Linux_console#Fonts "Linux console").

### Motywy GTK i Qt

Duża część aplikacji z interfejsem graficznym dla systemów Linux oparta jest na zestawach narzędzi [GTK+](/index.php/GTK%2B "GTK+") lub [Qt](/index.php/Qt "Qt"). Zapoznaj się z artykułem [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications"), aby znaleźć sposoby na poprawę wyglądu zainstalowanych programów i dostosowanie ich do własnych upodobań.

## Ulepszenia konsoli

Ta sekcja dotyczy niewielkich modyfikacji, które ułatwiają korzystanie z konsoli. Aby uzyskać więcej informacji, zobacz [Category:Shells](/index.php?title=Category:Shells&action=edit&redlink=1 "Category:Shells (page does not exist)").

### Aliasy

Aliasowanie polecenia lub jego grupy to sposób na zaoszczędzenie czasu podczas korzystania z konsoli. Jest to szczególnie pomocne w przypadku powtarzających się zadań, które nie wymagają znaczącej zmiany parametrów. Typowe aliasy oszczędzające czas można znaleźć w [Bash#Aliases](/index.php/Bash#Aliases "Bash"). Można je łatwo przenosić również do [zsh](/index.php/Zsh "Zsh").

### Alternatywne powłoki

[Bash](/index.php/Bash "Bash") to powłoka instalowana domyślnie w systemie Arch. Nośnik instalacyjny używa jednak [zsh](/index.php/Zsh "Zsh") z pakietem dodatkowym [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config). Zobacz [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell"), aby uzyskać więcej powłok.

### Dodatki Bash

Lista różnych ustawień Bash, w tym ustawień autouzupełniania, wyszukiwania historii i makr [Readline](/index.php/Readline "Readline"), jest dostępna w [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Kolorowy tekst w konsoli

Zapoznaj się z działem [Color output in console](/index.php/Color_output_in_console "Color output in console").

### Pliki skompresowane i archiwa

Pliki skompresowane lub archiwa są często spotykane w systemie GNU/Linux. [Tar](/index.php/Tar "Tar") jest jednym z najczęściej używanych narzędzi do archiwizacji, a użytkownicy powinni zapoznać się z jego składnią (na przykład pakiety Arch Linuxa to po prostu archiwum xzip). Zobacz [Bash# Functions](/index.php/Bash#_Functions "Bash") any uzyskać dodatkowe informacje.

### Monit konsoli

Monit konsoli (PS1) można w dużym stopniu dostosować. Zobacz [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") lub [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh"), jeśli używasz odpowiednio Bash lub Zsh.

### Emacs shell

Emacs jest znany z oferowania opcji wykraczających poza zwykłą edycję tekstu, jedną z nich jest zastąpienie powłoki wiersza poleceń. Skorzystaj z [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs"), aby uzyskać pomoc w naprawieniu kolorów w Emacs, w związku z włączeniem kolorowych znaków w konsoli.

### Obsługa myszy

Używanie myszy w konsoli np. do kopiowania i wklejania tekstu, może okazać się wygodniejsze niż tradycyjny tryb kopiowania [w ekranie GNU](/index.php/GNU_Screen "GNU Screen"). Szczegółowe instrukcje znajdują się w [General purpose mouse](/index.php/General_purpose_mouse "General purpose mouse").

### Przewijanie tekstu w konsoli

Aby móc zatrzymać tekst, który przeskoczył poza ekran i go odczytać, zapoznaj się ze stroną [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### Zarządzanie sesją

Używając multiplekserów terminali, takich jak [tmux](/index.php/Tmux "Tmux") lub [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programy można uruchamiać w sesjach składających się z kart i paneli, które można dowolnie odłączać, więc gdy użytkownik zakończy emulator terminala, zakończy serwer [X](/index.php/X "X") lub wyloguje się, programy powiązane z sesją będą działały w tle, dopóki serwer terminali multiplekserów będzie aktywny. Interakcja z programami wymaga przelogowania.