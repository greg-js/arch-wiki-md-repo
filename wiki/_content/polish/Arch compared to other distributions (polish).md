<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Wstęp](#Wstęp)
*   [2 Dystrybucje graficzne](#Dystrybucje_graficzne)
    *   [2.1 Ubuntu](#Ubuntu)
    *   [2.2 Fedora](#Fedora)
    *   [2.3 Debian](#Debian)
    *   [2.4 Mandriva](#Mandriva)
    *   [2.5 openSUSE](#openSUSE)
    *   [2.6 Fedora](#Fedora_2)
    *   [2.7 PCLinuxOS](#PCLinuxOS)
*   [3 Dystrybucje źródłowo-bazowe](#Dystrybucje_źródłowo-bazowe)
    *   [3.1 Gentoo](#Gentoo)
*   [4 Dystrybucje minimalistyczne](#Dystrybucje_minimalistyczne)
    *   [4.1 CRUX](#CRUX)
    *   [4.2 Slackware](#Slackware)

## Wstęp

Na tej stronie przedstawione zostały różnice i podobieństwa Archa w stosunku do najpopularniejszych dystrybucji GNU/Linux. Należy jednak pamiętać, że najlepszym sposobem na porównanie Archa z innymi dystrybucjami, będzie zainstalowanie go i przetestowanie.

Zebrane poniżej informacje mają na celu dostarczenie potencjalnemu użytkownikowi podstawowej wiedzy na temat różnic między dystrybucjami.

## Dystrybucje graficzne

Dystrybucje graficzne mają wiele uproszczeń. Arch jest inny od którejkolwiek z nich. Jest oparty na konsoli, linii komend. Jest dystrybucją lepszą, jeśli chcesz naprawdę nauczyć się Linuksa. Dystrybucje graficzne wypuszczane są razem z instalatorami GUI (np. Anaconda w Fedorze) oraz z autokonfiguratorami w systemie. W Archu konfiguracja odbywa się poprzez edytowanie odpowiednich plików konfiguracyjnych.

### Ubuntu

Ubuntu jest bardzo szybko rozwijającą się dystrybucją, tworzoną zarówno dla zaawansowanych użytkowników jak i zwykłych "klikaczy". Ma bardzo prosty w obsłudze instalator i całą gamę autokonfiguratorów. Arch natomiast tworzony jest w myśl zasady KISS. Nowy użytkownik Archa może pomyśleć, że system ten cechuje nadmierna surowość, jednak pozwala to na bardzo dokładną kontrolę systemu. Oba projekty mają bardzo odmienne cele i są skierowane do innych użytkowników. Arch jest przeznaczony dla użytkowników, którzy chcą sami zbudować sobie system, Ubuntu natomiast oferuje system, który ma być dystrybucją dla wszystkich.

### Fedora

Fedora jest dystrybucją uboczną Red Hat'a, stale zyskującą na popularności. Powodem takiego stanu rzeczy jest potężna społeczność (świetne wsparcie), oraz spora ilość pakietów binarnych. Podobnie, jak w innych dystrybucjach używających RPM, zarządzanie pakietami jest problematyczne. Arch posiada system portów, Fedora nie. Za to oferuje zarówno graficzny jak i tekstowy instalator. Fedora znana jest z innowacyjnych rozwiązań, np. integracji SELinux i GCJ w skompilowanych pakietach, aby oddalić potrzebę korzystania z JRE Sun'a. Fedora słynie również z braku wsparcia dla MP3, przestrzegając rozwiązań patentowych.

Arch jest nastawiony bardziej na prostotę, elegancję, lekkość i umożliwienie użytkownikowi stabilnej pracy na systemie, natomiast Fedora skupia się bardziej na rozwój i innowacje systemowe. Należy jednak zaznaczyć, że nie oznacza to iż Fedora jest systemem niestabilnym.

### Debian

Debian jest projektem o liczniejszej społeczności, oferującym ponad 20.000 pakietów binarnych. Arch ma mniej dostępnych pakietów, jednakże stworzenie własnej paczki jest o wiele prostsze niż w Debianie. Arch posiada nowsze pakiety w repozytoriach (często w current Archa są nowsze pakiety niż w testing Debiana!). Choć oba systemy posiadają wysokiej jakości zarządzanie pakietami, Debian nie oferuje systemu portów, opierając się raczej na jego ogromych repozytoriach binarnych.

Debian jest dostępny dla wielu architektur, w tym alpha, arm, hppa, i386, x86_64, ia64, m68k, mips, mipsel, powerpc, s390 i sparc. Deweloperzy Debiana skupiają się bardziej na stabilności systemu.

### Mandriva

Mandriva (wcześniej Mandrake) zdobyła sławę dzięki swojemu instalatorowi. To bardzo prosta w użytkowaniu dystrybucja, która po dłuższym używaniu może wprawiać użytkownika w bliżej-nieokreślone-stany. Kolejnym problemem jest to, że bazuje na pakietach RPM. Arch pozwala na dużo więcej wolności w konfiguracji, ale jest mniej przyjazny zwykłemu użytkownikowi.

### openSUSE

openSUSE posiada doskonały system administracji systemem zwany Yast, za pomocą którego w łatwy sposób można skonfigurować prawie wszystko co się dzieje w naszym systemie. Arch nie oferuje takiego narzędzia zgodnie z The Arch Way. SUSE jest polecany mniej doświadczonym, zupełnie początkującym użytkownikom, bądź tym, którzy chcą prostszego życia oczekując działającego systemu zaraz po zainstalowaniu.

### Fedora

Fedora jest projektem rozwijanym przez Fedora Project i finansowanym głównie przez Red Hat. Charakteryzuje się sporą społecznością, która chętnie pomaga nowym użytkownikom. Używa pakietów RPM, którymi zarządza się menedżerem yum, jednakże oficjalne narzędzie graficzne (PackageKit) jest również dostępne w repozytoriach. W Archu oficjalnym menedżerem pakietów jest Pacman, zaś wszelakie graficzne narzędzia są nieoficjalne.

Dystrybucja zawiera tylko wolne oprogramowanie, które nie budzi żadnych zastrzeżeń licencyjnych i patentowych, ale powstały repozytoria z kodekami i zamkniętymi sterownikami. Arch jest bardziej pobłażliwy.

Fedora oferuje zarówno graficzny i tekstowy instalator, który zainstaluje wybrane środowisko graficzne. Arch zainstalować można wyłącznie dzięki tekstowemu instalatorowi, po czym uzyskamy tylko system bazowy.

Na koniec kolejna różnica pomiędzy Fedorą, a Archem - pierwsza dystrybucja wydawana jest cyklicznie, natomiast druga jest dystrybucją rolling-realase. Obrazy są wydawane w celu wyłącznie uaktualnienia obrazu instalacyjnego raz lub dwa razy w roku.

### PCLinuxOS

PCLinuxOS jest oparte na popularnej dystrybucji Mandriva. Określany jest jako system "prosty", chociaż jego definicja prostoty jest inna niż definicja Archa. Arch został zaprojektowany jako system, który można dostosować sobie od podstaw i i jest ukierunkowany do bardziej zaawansowanych użytkowników. PCLOS korzysta z menedżera pakietów Apt jako otoczki do pakietów RPM.

## Dystrybucje źródłowo-bazowe

### Gentoo

Ponieważ Arch jest dystrybucją opartą na pakietach binarnych, nie jest tak czasochłonny jak Gentoo. Gentoo posiada jednak więcej pakietów i pozwala na dokładne wybranie wersji programu jaką chcemy zainstalować. Arch pozwala na instalacje zarówno pakietów binarnych jak i ze źródeł. Gentoo działa na większej ilości maszyn (i386, AMD64, PowerPC, PowerPC 64, SPARC, DEC Alpha, ARM, MIPS, PA-RISC, S390, IA-64), pozwala na dokładne dostosowanie każdego z pakietów do naszych potrzeb. Arch jest dostępny jedynie dla architektur i686 oraz x86_64 (dostępne są również nieoficjalne porty na PPC oraz i586). Nie ma żadnych dowodów, że Gentoo jest szybsze od Archa, czy odwrotnie. Ponieważ zarówno instalacja Gentoo i Archa polega na instalowaniu najpierw systemu podstawowego, uważane są za wysoce konfigurowalne. Użytkownicy Gentoo generalnie powinni czuć się komfortowo w Archu.

## Dystrybucje minimalistyczne

### CRUX

Arch Linux wzorowany jest na CRUX. Judd przedstawił kiedyś dokładne różnice:

Używałem CRUX'a zanim zacząłem budować Archa. Arch poczatkowo niczym sie nie różnił. Potem napisałem Pacmana, żeby zastąpić nimi moje bashowe pseudo-menedżery pakietów (zbudowałem Archa jako LFS). Są to zatem dwie różne dystrybucje, ale technicznie rzecz biorąc sa bardzo podobne. [...]

### Slackware

Zarówno Slackware jak i Arch są "prostymi" dystrybucjami. Obie dystrybucje koncentrują się na prostocie i minimaliźmie. W obu wykorzystywane są skrypty startowe wzorowane na BSD. Arch posiada Pacmana, który pozwala na o wiele prostsze zarządzanie pakietami oraz oferuje automatyczne rozwiązywanie zależności w przeciwieństwie do standardowych narzędzi Slackware.

Slackware wydaje się być bardziej konserwatywny, preferowane są w nim stabilne wersje programów. Dzięki temu, że kompilowany jest dla i486, działa również na starszych maszynach. Arch jest dystrybucją rolling-release, podczas gdy Slackware stawia większy nacisk na stabilne i sprawdzone pakiety. Dlatego też Arch jest bardzo dobrym systemem dla tych użytkowników Slackware, którym brakuje narzędzia do zarządzania pakietami albo zawsze świeżych pakietów. (Nieoficjalne) System SlackBuild jest bardzo podobny do Arch User Repository.