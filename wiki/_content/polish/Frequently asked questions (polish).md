Related articles

*   [Arch terminology](/index.php/Arch_terminology "Arch terminology")
*   [Arch User Repository#FAQ](/index.php/Arch_User_Repository#FAQ "Arch User Repository")
*   [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Ogólne](#Ogólne)
    *   [1.1 Czym jest Arch Linux?](#Czym_jest_Arch_Linux?)
    *   [1.2 Kiedy nie powinienem używać Arch Linux?](#Kiedy_nie_powinienem_używać_Arch_Linux?)
    *   [1.3 Jakie architektury obsługuje Arch?](#Jakie_architektury_obsługuje_Arch?)
    *   [1.4 Czy Arch przestrzega standardów systemu plików Linux Foundation Hierarchy Standard (FHS)?](#Czy_Arch_przestrzega_standardów_systemu_plików_Linux_Foundation_Hierarchy_Standard_(FHS)?)
    *   [1.5 Jestem zupełnie początkującym użytkownikiem systemu GNU/Linux. Czy powinienem używać Arch?](#Jestem_zupełnie_początkującym_użytkownikiem_systemu_GNU/Linux._Czy_powinienem_używać_Arch?)
    *   [1.6 Czy Arch Linux został zaprojektowany do użytku domowego czy jako serwer?](#Czy_Arch_Linux_został_zaprojektowany_do_użytku_domowego_czy_jako_serwer?)
    *   [1.7 Naprawdę lubię Arch Linux, ale zespół programistów powinien wdrożyć funkcję X](#Naprawdę_lubię_Arch_Linux,_ale_zespół_programistów_powinien_wdrożyć_funkcję_X)
    *   [1.8 Kiedy nowe wydanie zostanie udostępnione?](#Kiedy_nowe_wydanie_zostanie_udostępnione?)
    *   [1.9 Czy Arch Linux jest stabilną dystrybucją? Czy często się psuje?](#Czy_Arch_Linux_jest_stabilną_dystrybucją?_Czy_często_się_psuje?)
    *   [1.10 Arch potrzebuje więcej rozgłosu (tj. reklamy)](#Arch_potrzebuje_więcej_rozgłosu_(tj._reklamy))
    *   [1.11 Arch potrzebuje więcej programistów](#Arch_potrzebuje_więcej_programistów)
    *   [1.12 Dlaczego mój internet jest wolniejszy niż na innych systemach operacyjnych/dystrybucjach?](#Dlaczego_mój_internet_jest_wolniejszy_niż_na_innych_systemach_operacyjnych/dystrybucjach?)
    *   [1.13 Dlaczego Arch Linux używa całej mojej pamięci RAM?](#Dlaczego_Arch_Linux_używa_całej_mojej_pamięci_RAM?)
    *   [1.14 Gdzie się podziała cała moja wolna przestrzeń dyskowa?](#Gdzie_się_podziała_cała_moja_wolna_przestrzeń_dyskowa?)
*   [2 Zarządzanie pakietami](#Zarządzanie_pakietami)
    *   [2.1 Znalazłem błąd w pakiecie X. Co powinienem zrobić?](#Znalazłem_błąd_w_pakiecie_X._Co_powinienem_zrobić?)
    *   [2.2 Pakiety Arch powinny używać unikalnej konwencji nazewnictwa. Rozszerzenia *.pkg.tar.gz* i *.pkg.tar.xz* są za długie lub mylące](#Pakiety_Arch_powinny_używać_unikalnej_konwencji_nazewnictwa._Rozszerzenia_.pkg.tar.gz_i_.pkg.tar.xz_są_za_długie_lub_mylące)
    *   [2.3 Pacman potrzebuje biblioteki, aby inne aplikacje mogły łatwo uzyskać dostęp do informacji o pakiecie](#Pacman_potrzebuje_biblioteki,_aby_inne_aplikacje_mogły_łatwo_uzyskać_dostęp_do_informacji_o_pakiecie)
    *   [2.4 Pacman potrzebuje funkcji X!](#Pacman_potrzebuje_funkcji_X!)
    *   [2.5 Właśnie zainstalowałem pakiet X. Jak go uruchomić?](#Właśnie_zainstalowałem_pakiet_X._Jak_go_uruchomić?)
    *   [2.6 Dlaczego w oficjalnych repozytoriach jest tylko jedna wersja każdej biblioteki współdzielonej?](#Dlaczego_w_oficjalnych_repozytoriach_jest_tylko_jedna_wersja_każdej_biblioteki_współdzielonej?)
    *   [2.7 Co się stanie, jeśli uruchomię pełną aktualizację systemu, a aktualizacja zostanie udostępniona dla biblioteki współużytkowanej, ale nie dla zależnych od niej aplikacji?](#Co_się_stanie,_jeśli_uruchomię_pełną_aktualizację_systemu,_a_aktualizacja_zostanie_udostępniona_dla_biblioteki_współużytkowanej,_ale_nie_dla_zależnych_od_niej_aplikacji?)
    *   [2.8 Czy jest możliwe, że w repozytorium znajduje się poważna aktualizacja jądra i że niektóre pakiety sterowników nie zostały zaktualizowane?](#Czy_jest_możliwe,_że_w_repozytorium_znajduje_się_poważna_aktualizacja_jądra_i_że_niektóre_pakiety_sterowników_nie_zostały_zaktualizowane?)
    *   [2.9 Co zrobić przed aktualizacją?](#Co_zrobić_przed_aktualizacją?)
    *   [2.10 Wydano aktualizację pakietu, ale Pacman mówi, że system jest aktualny](#Wydano_aktualizację_pakietu,_ale_Pacman_mówi,_że_system_jest_aktualny)
    *   [2.11 Dystrybutor pakietu „X” wydał nową wersję. Jak długo potrwa aktualizacja pakietu Arch do tej nowej wersji?](#Dystrybutor_pakietu_„X”_wydał_nową_wersję._Jak_długo_potrwa_aktualizacja_pakietu_Arch_do_tej_nowej_wersji?)
    *   [2.12 Jeśli potrzebuję starszej wersji zainstalowanej biblioteki, czy mogę po prostu dowiązać symbolicznie do nowszej wersji?](#Jeśli_potrzebuję_starszej_wersji_zainstalowanej_biblioteki,_czy_mogę_po_prostu_dowiązać_symbolicznie_do_nowszej_wersji?)
    *   [2.13 Dlaczego w grupie podstawowej istnieją niepotrzebne pakiety (np. netctl)?](#Dlaczego_w_grupie_podstawowej_istnieją_niepotrzebne_pakiety_(np._netctl)?)
*   [3 Instalacja](#Instalacja)
    *   [3.1 Arch potrzebuje instalatora. Może instalator graficzny (GUI)?](#Arch_potrzebuje_instalatora._Może_instalator_graficzny_(GUI)?)
    *   [3.2 Zainstalowałem Arch i mam przed sobą wiersz poleceń! Co teraz?](#Zainstalowałem_Arch_i_mam_przed_sobą_wiersz_poleceń!_Co_teraz?)
    *   [3.3 Jakiego środowiska pulpitu lub menedżera okien powinienem użyć?](#Jakiego_środowiska_pulpitu_lub_menedżera_okien_powinienem_użyć?)
    *   [3.4 Co czyni Arch wyjątkowym spośród innych „minimalnych” dystrybucji?](#Co_czyni_Arch_wyjątkowym_spośród_innych_„minimalnych”_dystrybucji?)
*   [4 64-bit](#64-bit)
    *   [4.1 Jak ustalić, czy mój procesor jest zgodny z architekturą x86_64?](#Jak_ustalić,_czy_mój_procesor_jest_zgodny_z_architekturą_x86_64?)
    *   [4.2 Dlaczego 64-bity?](#Dlaczego_64-bity?)

## Ogólne

### Czym jest Arch Linux?

Przeczytaj artykuł o [Arch Linux](/index.php/Arch_Linux_(Polski) "Arch Linux (Polski)").

### Kiedy nie powinienem używać Arch Linux?

Prawdopodobnie nie powinieneś używać Arch Linux jeśli:

*   nie masz umiejętności / czasu / chęci aby używać dystrybucji GNU/Linux opartej na zasadzie „zrób to sam” - jeśli przeraża Cię sama myśl o korzystaniu z [wiersza poleceń (konsoli)](https://pl.m.wikipedia.org/wiki/Wiersz_polece%C5%84%7C), Arch Linux nie jest na razie dla Ciebie.
*   potrzebujesz obsługi architektury innej niż x86_64.
*   nie chcesz używać dystrybucji, która zapewnia tylko darmowe oprogramowanie zdefiniowane przez GNU.
*   uważasz, że system operacyjny powinien się skonfigurować sam, być od razu gotowy do użycia i zawierać na nośniku instalacyjnym pełny domyślny zestaw oprogramowania i środowisko komputerowe.
*   nie chcesz rozpowszechniać dystrybucji GNU/Linux.
*   jesteś zadowolony ze swojego obecnego systemu operacyjnego.

### Jakie architektury obsługuje Arch?

Arch obsługuje tylko architekturę x86_64 (czasami nazywaną amd64). Wsparcie dla i686 zostało porzucone w listopadzie 2017 r [[1]](https://www.archlinux.org/news/the-end-of-i686-support/).

Istnieją nieoficjalne porty dla architektury i686 [[2]](https://archlinux32.org/) i procesorów [ARM](https://en.wikipedia.org/wiki/architektura_ARM "wikipedia:architektura ARM") [[3]](http://archlinuxarm.org/), każdy z własną społecznością i kanałami komunikacji [[4]](http://ix.io/73w/irc).

### Czy Arch przestrzega standardów systemu plików Linux Foundation Hierarchy Standard (FHS)?

Arch Linux przestrzega hierarchii systemu plików dla systemów operacyjnych korzystających z menedżera usług [systemd](/index.php/Systemd "Systemd"). Wpisz komendę `man file-hierarchy`, aby uzyskać wyjaśnienie dotyczące hierarchii katalogów w systemie wraz z ich oznaczeniami. Przykładowo `/bin`, `/sbin` i `/usr/sbin` są symbolicznymi linkami do `/usr/bin` a `/lib` i `/lib64` to dowiązania symboliczne do `/usr/lib`.

### Jestem zupełnie początkującym użytkownikiem systemu GNU/Linux. Czy powinienem używać Arch?

Jeśli jesteś początkujący i chcesz korzystać z Arch Linux, będziesz musiał poświęcić czas na naukę nowego systemu i zaakceptować fakt, że Arch Linux jest zaprojektowany jako dystrybucja z kategorii „zrób to sam”. To użytkownik składa cały system w całość i go konfiguruje.

Domyślna i podstawowa instalacja Arch Linux nie zawiera żadnego środowiska pulpitu (okienek), a cała jej obsługa odbywa się (przynajmniej na początku) jedynie poprzez wiersz poleceń (konsolę). Arch nie zawiera żadnych domyślnych konfiguratorów. Oczywiście możesz później doinstalować całe spektrum oprogramowania (w tym środowiska pulpitu) znajdujące się w oficjalnych i nieoficjalnych repozytoriach Arch, w tym w [AUR](/index.php/AUR "AUR").

Zanim poprosisz o pomoc, przeszukaj Google, nasze forum oraz doskonałą dokumentację dostarczoną przez Arch Wiki. Zasoby te zostały udostępnione użytkownikom nie bez powodu. Zgromadzenie tych użytecznych informacji zajęło ochotnikom wiele tysięcy godzin.

Zobacz także [uwagi o zdobywaniu informacji na temat systemu](/index.php/Arch_terminology#RTFM "Arch terminology") oraz [Instrukcję instalacji](/index.php/Installation_guide_(Polski) "Installation guide (Polski)").

### Czy Arch Linux został zaprojektowany do użytku domowego czy jako serwer?

Arch Linux nie ma jednego określonego zastosowania. Jest on raczej przeznaczony dla określonego typu użytkownika. Arch jest skierowany do kompetentnych użytkowników, którzy zgadzają się z filozofią "zrób to sam" i którzy lubią dostosowywać system do własnych potrzeb. Dlatego w rękach członka docelowej bazy użytkowników, Arch Linux może być używany praktycznie do każdego celu. Wielu korzysta z Arch zarówno na swoich komputerach stacjonarnych, jak i na serwerach. Ponadto oczywiście strona archlinux.org działa na systemie Arch.

### Naprawdę lubię Arch Linux, ale zespół programistów powinien wdrożyć funkcję X

Zaangażuj się, przekaż społeczności swój kod lub rozwiązanie. Jeśli Twoje propozycje zostaną dobrze ocenione przez społeczność i zespół programistów, być może zostaną one włączone do systemu. Społeczność Arch rozwija się dzięki udostępnianiu kodu i narzędzi.

### Kiedy nowe wydanie zostanie udostępnione?

Arch Linux nie posiada wydań sensu stricto tak jak inne dystrybucje np. Ubuntu czy Fedora. Arch jest tzw. [wydaniem ciągłym (rolling release)](https://pl.wikipedia.org/wiki/Rolling_release).

Pliki instalacyjne np. w formie obrazu iso, to migawki stanu pakietów na dany moment. Obrazy te tworzone są i dostarczane zwykle w pierwszej połowie każdego miesiąca. Aktualizacje systemu dostarczane są na bieżąco.

### Czy Arch Linux jest stabilną dystrybucją? Czy często się psuje?

To użytkownik jest ostatecznie odpowiedzialny za stabilność własnego systemu. To on decyduje, kiedy uaktualnić system i w razie potrzeby wprowadza niezbędne zmiany w oprogramowaniu i konfiguracji. Jeśli użytkownik zwraca się do społeczności o pomoc, często udzielana jest ona odpowiednim czasie. Różnica między Arch Linux i innymi dystrybucjami pod tym względem polega na tym, że Arch jest dystrybucją typu „zrób to sam”. Oznacza to, że wszelkie pretensje co do awarii danego systemu są bezproduktywne i niepotrzebne, gdyż za wszystkie zmiany w konkretnym systemie nie są odpowiedzialni twórcy Arch Linux, a sam użytkownik.

Zobacz artykuł [System maintenance](/index.php/System_maintenance "System maintenance"), aby uzyskać wskazówki, jak uczynić system Arch Linux tak stabilnym, jak to możliwe.

### Arch potrzebuje więcej rozgłosu (tj. reklamy)

Arch Linux już dostaje dużo rozgłosu. Celem Arch Linux nie jest być wszechobecną i potężną dystrybucją. Dla twórców istotny jest zrównoważony wzrost rozpoznawalności systemu wśród docelowej grupy użytkowników.

### Arch potrzebuje więcej programistów

Pewnie tak. Zapraszamy do poświęcenia czasu na rozwój dystrybucji! Odwiedź [fora](https://bbs.archlinux.org), [IRC channels](/index.php/IRC_channels "IRC channels") lub [listy mailingowe](https://mailman.archlinux.org/mailman/listinfo/) i zobacz, co należy zrobić. Zaangażowanie się w forum to dobry początek.

### Dlaczego mój internet jest wolniejszy niż na innych systemach operacyjnych/dystrybucjach?

Czy Twoja sieć jest poprawnie skonfigurowana? Przeczytaj artykuł [Network configuration](/index.php/Network_configuration "Network configuration").

Zauważ też, że Arch Linux nie ma włączonej usługi [kształtowania ruchu sieciowego](https://en.wikipedia.org/wiki/Traffic_shaping "wikipedia:Traffic shaping"). Dlatego możliwe jest, że jeśli program w jakiś sposób w pełni wykorzysta przepustowość Twojego połączenia internetowego - niezależnie od tego, czy jest to połączenie P2P lub klasyczne połączenia klient-serwer - inne lokalne połączenia nie uzyskają wymaganej przepustowości, co powoduje poważne opóźnienia i przekroczenia limitu czasu. Spowolnienie mogą powodować także [zapory sieciowe](/index.php/Firewalls "Firewalls"), takie jak „Shorewall” lub „Vuurmuur”; istnieją również skrypty statyczne dla [iproute2](https://www.archlinux.org/packages/?name=iproute2) (takie jak [pochodne](http://serendipity.ruwenzori.net/index.php/2008/06/01/modified-wondershaper-for-better-voip-qos) „Wondershaper”), które umożliwiają modyfikacje sieci.

### Dlaczego Arch Linux używa całej mojej pamięci RAM?

Zasadniczo nieużywana pamięć RAM to zmarnowana pamięć RAM.

Wielu nowych użytkowników zauważa, że ​​jądro Linuksa traktuje pamięć inaczej, niż to się działo do tej pory. Ponieważ dostęp do danych z pamięci RAM jest znacznie szybszy niż z dysku twardego, jądro buforuje ostatnio dostępne dane w pamięci. Buforowane dane są usuwane tylko wtedy, gdy w systemie zaczyna brakować dostępnej pamięci i konieczne jest załadowanie nowych danych.

Możemy to sprawdzić za pomocą polecenia `free`:

 `$ free -h` 
```
              total        used        free      shared  buff/cache   available
Mem:           2.8G        1.1G        283M        224M        1.4G        1.2G
Swap:          3.0G        881M        2.1G

```

Należy zauważyć różnicę między pamięcią wolną (free) a dostępną (available). W powyższym przykładzie laptop z 2,8 GB całkowitej pamięci RAM wydaje się zużywać większość z zaledwie 283 MB wolnej pamięci. Jednak 1,4G to pamięć podręczna (buff/cache). Nadal dostępne jest 1,2G do uruchamiania nowych aplikacji. Szczegółowe informacje można znaleźć w `man free (1)`. Co z tego wszystkiego wynika? Wzrost wydajności!

Przeczytaj [| ten wspaniały artykuł](http://www.linuxjournal.com/article/2770), jeśli Twoja ciekawość została pobudzona. Istnieje również strona internetowa poświęcona wyjaśnieniu wszystkich tych kwestii: [http://www.linuxatemyram.com/](http://www.linuxatemyram.com/).

### Gdzie się podziała cała moja wolna przestrzeń dyskowa?

Odpowiedź na to pytanie zależy od Twojego systemu. Istnieje kilka [doskonałych narzędzi](/index.php/List_of_applications#Disk_usage_display "List of applications"), które mogą pomóc znaleźć odpowiedź na to pytanie.

## Zarządzanie pakietami

Zobacz strony [pacman (Polski)](/index.php/Pacman_(Polski) "Pacman (Polski)"), [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") i [Official repositories](/index.php/Official_repositories "Official repositories"), aby uzyskać więcej odpowiedzi.

### Znalazłem błąd w pakiecie X. Co powinienem zrobić?

Najpierw musisz dowiedzieć się, czy ten błąd jest z kategorii takich, które zespół Arch jest w stanie naprawić. Często tak nie jest (np. awarie Firefoksa mogą być winą zespołu Mozilli). Jeśli jest to problem z Arch Linux, możesz wykonać szereg kroków:

1.  Przeszukaj Google i fora w celu uzyskania informacji. Sprawdź, czy ktoś zauważył to samo co Ty.
2.  Opublikuj [raport o błędzie](/index.php/Bug_report "Bug report") ze szczegółowymi informacjami na [https://bugs.archlinux.org](https://bugs.archlinux.org).
3.  Jeśli chcesz, możesz napisać post na forum szczegółowo opisujący znaleziony błąd i wskazać, że już go zgłosiłeś. Pomoże to zapobiec zgłaszaniu tego samego błędu przez kilka osób.

### Pakiety Arch powinny używać unikalnej konwencji nazewnictwa. Rozszerzenia *.pkg.tar.gz* i *.pkg.tar.xz* są za długie lub mylące

Zostało to omówione na liście mailingowej Arch. Niektórzy proponowali rozszerzenie pliku *.pac*, ale nie planuje się zmiany nazwy rozszerzenia pakietu. Jak ujął to Tobias Kieslich, jeden z programistów Arch: *„Pakiet” to „archiwum gzipped” - „[xz]”! I można go otwierać, sprawdzać i modyfikować za pomocą dowolnej aplikacji obsługującej tar. Ponadto większość typów aplikacji automatycznie wykrywa typ MIME.*

### Pacman potrzebuje biblioteki, aby inne aplikacje mogły łatwo uzyskać dostęp do informacji o pakiecie

Pacman jest nakładką na [libalpm](https://www.archlinux.org/pacman/libalpm.3.html) - bibliotekę „Arch Linux Package Management” - która umożliwia alternatywne interfejsy, takie jak interfejs GUI.

### Pacman potrzebuje funkcji X!

Jeśli uważasz, że Twój pomysł coś wnosi, możesz przedyskutować go na [pacman-dev](https://lists.archlinux.org//listinfo/pacman-dev/). Sprawdź również [https://bugs.archlinux.org/index.php?project=3](https://bugs.archlinux.org/index.php?project=3) pod kątem istniejących propozycji zmian i funkcji.

Jednak najlepszym sposobem na dodanie funkcji do pacman lub Arch Linux jest jej samodzielne wdrożenie. Łatka lub kod może nie zostać oficjalnie zaakceptowany, ale inni mogą go ocenić, przetestować lub udoskonalić.

### Właśnie zainstalowałem pakiet X. Jak go uruchomić?

Jeśli używasz środowiska pulpitu takiego jak [KDE](/index.php/KDE "KDE") lub [GNOME](/index.php/GNOME "GNOME"), program powinien automatycznie pojawić się w menu. Jeśli próbujesz uruchomić program z terminala i nie znasz nazwy binarnej, użyj:

```
$ pacman -Qlq *nazwa_pakietu* | grep /usr/bin/

```

### Dlaczego w oficjalnych repozytoriach jest tylko jedna wersja każdej biblioteki współdzielonej?

Niektóre dystrybucje, takie jak np. Debian, mają różne wersje bibliotek współdzielonych spakowanych jako różne pakiety: `libfoo1`, `libfoo2`, `libfoo3` i tak dalej. W ten sposób można kompilować aplikacje dla różnych wersji `libfoo` zainstalowanych w tym samym systemie.

W przypadku dystrybucji takiej jak Arch oficjalnie obsługiwane są tylko najnowsze stabilne wersje pakietów. Porzucając obsługę przestarzałego oprogramowania, opiekunowie pakietów mogą spędzić więcej czasu na sprawdzenie, czy najnowsze wersje działają zgodnie z oczekiwaniami. Gdy tylko nowa wersja biblioteki współdzielonej stanie się dostępna, zostanie ona dodana do repozytoriów, a pakiety, których dotyczy problem, zostaną przebudowane tak, aby używać najnowszej wersji.

### Co się stanie, jeśli uruchomię pełną aktualizację systemu, a aktualizacja zostanie udostępniona dla biblioteki współużytkowanej, ale nie dla zależnych od niej aplikacji?

Coś takiego nie powinno się wydarzyć. Zakładając, że aplikacja o nazwie `foobaz` znajduje się w jednym z oficjalnych repozytoriów i z powodzeniem buduje się na nowej wersji biblioteki współdzielonej o nazwie `libbaz`, zostanie ona zaktualizowana wraz z `libbaz`. Jeśli jednak nie uda się jej skompilować, pakiet `foobaz` będzie zależny od wersji (np. *Libbaz 1.5*) i zostanie usunięty przez pacmana podczas aktualizacji `libbaz` z powodu konfliktu.

Jeśli `foobaz` to pakiet, który sam zbudowałeś i zainstalowałeś z AUR, powinieneś spróbować przebudować `foobaz` na nową wersję `libbaz`. Jeśli kompilacja się nie powiedzie, zgłoś błąd programistom `foobaz`.

### Czy jest możliwe, że w repozytorium znajduje się poważna aktualizacja jądra i że niektóre pakiety sterowników nie zostały zaktualizowane?

Nie, nie jest to możliwe. Ważnym aktualizacjom jądra (np. „Linux 3.5.0-1” do „linux 3.6.0-1”) zawsze towarzyszą przebudowy wszystkich obsługiwanych pakietów sterowników jądra. Z drugiej strony, jeśli masz zainstalowany nieobsługiwany pakiet sterowników, taki jak [catalyst](https://aur.archlinux.org/packages/catalyst/), to aktualizacja jądra może się zepsuć, jeśli nie przebudujesz go dla nowego jądra. Użytkownicy są odpowiedzialni za aktualizację wszelkich nieobsługiwanych pakietów sterowników, które zainstalowali.

### Co zrobić przed aktualizacją?

Postępuj zgodnie z sekcją [System maintenance#Upgrading the system](/index.php/System_maintenance#Upgrading_the_system "System maintenance").

### Wydano aktualizację pakietu, ale Pacman mówi, że system jest aktualny

Serwery lustrzane „Pacman” nie są natychmiast synchronizowane. Aktualizacja może potrwać 24 godziny. Jedynymi rozwiązaniami są cierpliwość lub użycie innego serwera lustrzanego. [MirrorStatus](https://www.archlinux.org/mirrors/status/) może pomóc w identyfikacji aktualnego serwera lustrzanego.

### Dystrybutor pakietu „X” wydał nową wersję. Jak długo potrwa aktualizacja pakietu Arch do tej nowej wersji?

Aktualizacje pakietów zostaną wydane, gdy będą gotowe. Określony czas może wynieść kilka godzin po wydaniu oficjalnym (upstream) gdy dotyczy niewielkiej aktualizacji błędów lub też nawet kilka tygodni po dużej aktualizacji dużej grupy pakietów. Czas od nowej wersji nadrzędnej do wydania przez Arch nowego pakietu zależy od konkretnych pakietów i dostępności opiekunów pakietów. Ponadto niektóre pakiety spędzają trochę czasu w repozytorium [testowym](/index.php/Testing "Testing"), co może wydłużyć czas do aktualizacji pakietu. Jeśli znajdziesz pakiet w oficjalnych repozytoriach, który jest nieaktualny, przejdź do strony tego pakietu na [stronie pakietów](https://www.archlinux.org/packages/) i oznacz go.

### Jeśli potrzebuję starszej wersji zainstalowanej biblioteki, czy mogę po prostu dowiązać symbolicznie do nowszej wersji?

Jeśli masz szczęście, może to działać przez jakiś czas. Nie jest to jednak właściwe rozwiązanie, ponieważ:

*   Biblioteki nie zmieniają wersji losowo - interfejs API/ABI prawdopodobnie się zmieni (możliwe, że z usuniętymi bitami), a to, czy zmiany te wpływają na użytkowanie biblioteki, jest kwestią przypadku.
*   Menedżer pakietów nie wyśledzi dowiązania symbolicznego. Początkujący, którzy natychmiast próbują włamać się do plików biblioteki systemowej, są najbardziej narażeni na dokonanie niepożądanej zmiany, której nie mogą zdiagnozować/naprawić, przed czym chroni menedżer pakietów.
*   Niewielka alternatywa zrzucenia starego pliku biblioteki do systemu plików, bez śledzenia, zostałaby zapomniana i nie zauważono by/nie usunięto potencjalnych błędów bezpieczeństwa.

Zamiast tego użyj/napisz [pakiet compat](https://aur.archlinux.org/packages/?SeB=n&K=compat), który zapewnia wymaganą wersję biblioteki.

### Dlaczego w grupie podstawowej istnieją niepotrzebne pakiety (np. netctl)?

Istnieją propozycje poprawy tego stanu rzeczy. Oto dyskusje z listy mailingowej:

[https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029435.html](https://lists.archlinux.org/pipermail/arch-dev-public/2019-January/029435.html)

[https://lists.archlinux.org/pipermail/arch-dev-public/2019-February/029452.html](https://lists.archlinux.org/pipermail/arch-dev-public/2019-February/029452.html)

## Instalacja

### Arch potrzebuje instalatora. Może instalator graficzny (GUI)?

Arch miał kiedyś instalator z tekstowym interfejsem użytkownika o nazwie Arch Installation Framework (AIF). Po [opuszczeniu go przez opiekuna pakietu](https://lists.archlinux.org/pipermail/arch-releng/2012-July/002628.html), został on [porzucony na rzecz Skryptów instalacyjnych Arch (Arch Install Scripts)](/index.php/Arch_Linux#Arch_Install_Scripts "Arch Linux").

Ponieważ instalacja od zera co do zasady nie zdarza się często (przeczytaj resztę tego artykułu, aby dowiedzieć się więcej o tym, co oznacza „wydanie ciągłe”), instalator graficzny nie jest priorytetem dla programistów ani użytkowników. [Instrukcja instalacji](/index.php/Installation_guide_(Polski) "Installation guide (Polski)") została w pełni zaktualizowana w celu wykorzystania wiersza poleceń (konsoli).

### Zainstalowałem Arch i mam przed sobą wiersz poleceń! Co teraz?

Zobacz [Zalecenia ogólne](/index.php/General_recommendations_(Polski) "General recommendations (Polski)").

### Jakiego środowiska pulpitu lub menedżera okien powinienem użyć?

Ponieważ wiele z nich jest dostępnych, użyj tego, który najbardziej Ci się podoba, w zależności od potrzeb. Zajrzyj do artykułów [Desktop environment](/index.php/Desktop_environment "Desktop environment") i [Window manager](/index.php/Window_manager "Window manager").

### Co czyni Arch wyjątkowym spośród innych „minimalnych” dystrybucji?

Zobacz [porównanie z innymi dystrybucjami](/index.php/Arch_compared_to_other_distributions_(Polski) "Arch compared to other distributions (Polski)").

## 64-bit

### Jak ustalić, czy mój procesor jest zgodny z architekturą x86_64?

Jeśli twój procesor jest kompatybilny z [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64"), będziesz mieć flagę `lm` ([tryb długi](https://en.wikipedia.org/wiki/tryb_d%C5%82ugi "wikipedia:tryb długi")) w `/proc/cpuinfo`. Na przykład:

```
$ grep -w lm /proc/cpuinfo

```

W systemie Windows skorzystanie z bezpłatnego oprogramowania [CPU-Z](http://www.cpuid.com/cpuz.php) pomoże ustalić, czy Twój procesor jest kompatybilny z 64-bitami. Procesory z zestawem instrukcji AMD „AMD64” lub rozwiązaniem Intela „EM64T” powinny być kompatybilne z wydaniami x86_64 i pakietami binarnymi.

### Dlaczego 64-bity?

W większości przypadków 64-bitowy system operacyjny jest szybszy i dodatkowo z natury bardziej bezpieczny ze względu na swoje właściwości [Randomizacja układu przestrzeni adresowej (ASLR)](https://en.wikipedia.org/wiki/Randomizacja_uk%C5%82adu_przestrzeni_adresowej "wikipedia:Randomizacja układu przestrzeni adresowej") w połączeniu z [Kod niezależny od pozycji (PIC)](https://en.wikipedia.org/wiki/Kod_niezale%C5%BCny_od_pozycji "wikipedia:Kod niezależny od pozycji") i [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit"), który nie jest dostępny w standardowym jądrze i686 z powodu wyłączenia PAE. Jeśli Twój komputer ma więcej niż 4 GB pamięci RAM, tylko 64-bitowy system operacyjny będzie mógł go w pełni wykorzystać.

Programiści również coraz mniej dbają o 32-bitowe („starsze”) procesory, ponieważ „nowe” procesory x86 zazwyczaj obsługują rozszerzenia 64-bitowe.

Istnieje wiele innych powodów, które moglibyśmy tutaj wymienić, a które świadczą o wyższości systemów 64-bitowych, ale między jądrem, przestrzenią użytkownika i poszczególnymi programami po prostu nie jest możliwe wyszczególnienie każdej rzeczy, którą 64-bit robi obecnie znacznie lepiej.