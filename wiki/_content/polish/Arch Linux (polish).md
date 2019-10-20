Arch Linux jest niezależnie tworzoną dystrybucją ogólnego przeznaczenia GNU/Linux dla komputerów z procesorami serii x86-64 wszechstronną na tyle aby pełnić dowolne postawione przed nim zadania. Proces tworzenia systemu skupia się na prostocie, minimalizmie i czystości kodu. Arch jest instalowany jako minimalistyczny system bazowy, który może zostać skonfigurowany przez użytkownika, aby spełniał rolę idealnego środowiska pracy. Pozwala na zainstalowanie wyłącznie niezbędnych narzędzi aby umożliwić szybką i bezproblemową pracę. Narzędzia konfiguracyjne działające poprzez interfejs graficzny nie są oficjalnie udostępniane. Bazuje na modelu ciągłych wydań, dostarczając najnowsze stabilne wersje większości oprogramowania.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Historia](#Historia)
*   [2 Prostota](#Prostota)
*   [3 Nowoczesność](#Nowoczesność)
*   [4 Zarządzanie Pakietami](#Zarządzanie_Pakietami)
*   [5 Integracja Źródeł](#Integracja_Źródeł)
*   [6 Społeczność](#Społeczność)
*   [7 Podsumowanie](#Podsumowanie)

## Historia

Arch Linux został stworzony z inicjatywy kanadyjskiego programisty Judda Vineta. Pierwsza wersja systemu Arch Linux 0.1 ujrzała światło dzienne 11 marca 2002 roku. Pomimo faktu iż Arch Linux jest dystrybucją kompletnie niezależną, inspirację czerpie z prostoty innych dystrybucji takich jak [Slackware](http://slackware.com), [CRUX](http://www.crux.nu) oraz [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"). W 2007 roku, Judd Vinet porzucił stanowisko Projekt Lidera i został zastąpiony przez amerykańskiego programistę Aarona Griffina.

Zobacz także: [Historia Archa](/index.php?title=History_of_Arch_Linux_(Polski)&action=edit&redlink=1 "History of Arch Linux (Polski) (page does not exist)").

## Prostota

Podążając filozofią [Droga Archa](/index.php/The_Arch_Way_(Polski) "The Arch Way (Polski)"), Arch Linux stara się być lekką, elastyczną i prostą Uniksopodobną dystrybucją. Minimalistyczne środowisko (pozbawione GUI), skompilowane dla procesorów z rodziny x86-64, dostarczane jest podczas instalacji. Zamiast oferowania kompletnej dystrybucji, z której w późniejszym czasie użytkownik zmuszony jest do usuwania niechcianych pakietów, Arch oferuje możliwość stworzenia i dostosowania systemu od podstaw co pozwala na przemianę minimalistycznego konsolowego systemu w potężny system z całą masą wodotrysków. To użytkownik decyduje czym jego system się stanie.

## Nowoczesność

Arch Linux stara się dostarczać najnowsze stabilne wydania oprogramowania, gdy tylko jest pewność, że nie mają one złego wpływu na działanie reszty systemu. Arch Linux jest systemem "ciągłych wydań", co oznacza, że wystarczy raz zainstalować system, a następnie korzystać z ciągłych uaktualnień, bez konieczności ponownego przechodzenia przez proces instalacyjny wraz z każdym kolejnym wydaniem systemu. Używając jednej komendy sprawiamy, że nasz system zostanie zaktualizowany do najnowszej wersji. Precyzując, Arch Linux nie dostarcza wydań co jakiś czas, tak jak niektóre inne dystrybucje (np. Ubuntu czy Fedora), a obraz instalacyjny jest migawką stanu pakietów na dzień jego utworzenia.

Arch obsługuje wiele najnowszych funkcji dostępnych użytkownikom systemów z rodziny GNU/Linux, takich jak nowoczesne systemy plików (Ext4, Reiser, XFS, JFS, BTRFS), LVM2/EVMS, softwarową obsługa RAID, udev oraz initcpio. Wszelkie nowości z oficjalnego jądra wprowadzane są do systemu tak szybko jak jest to możliwe.

## Zarządzanie Pakietami

Zarządzanie Archem odbywa się przy pomocy prostego w obsłudze narzędzia [pacman](/index.php/Pacman_(Polski) "Pacman (Polski)"), które jest w stanie zaktualizować system przy pomocy jednego polecenia. [Pacman](/index.php/Pacman_(Polski) "Pacman (Polski)") napisany został przy pomocy języka "C". Podobnie jak cały Arch, tak i jego menedżer pakietów został stworzony by być lekkim, prostym i bardzo szybkim. Dodatkowo Arch udostępnia także [Arch Build System](/index.php/Arch_Build_System_(Polski) "Arch Build System (Polski)"), narzędzie umożliwiające proste budowanie i instalowanie pakietów prosto ze źródeł, które także mogą być aktualizowane przy pomocy jednej komendy. Nic nie stoi na przeszkodzie by przy jego pomocy przebudować cały system.

[Oficjalne Repozytoria](/index.php?title=Official_Repositories_(Polski)&action=edit&redlink=1 "Official Repositories (Polski) (page does not exist)") Archa, wspierające architekturę x84-64, udostępniają tysiące pakietów wysokiej jakości, których zadaniem jest spełnienie Twoich oczekiwań. Arch stara się poszerzać wspólnotę użytkowników, oferując takie rozwiązania jak [Repozytorium Użytkowników Archa](/index.php/Arch_User_Repository_(Polski) "Arch User Repository (Polski)"), które zawiera tysiące przygotowanych przez użytkowników PKGBUILD'ów (skryptów służących do kompilacji oraz instalacji pakietów poprzez użycie aplikacji "makepkg"). Dodatkowo każdy użytkownik może w prosty sposób sam zbudować i zarządzać swoim własnym repozytorium.

## Integracja Źródeł

Oprogramowanie Archa dostarczane jest w czystej postaci (z ang. *vanilla*), z bezpośrednich źródeł, na zasadach które ustalił twórca aplikacji. Łatanie poszczególnych aplikacji stosowane jest tylko w szczególnych przypadkach w celu zapobiegnięcia awarii systemu czy niezgodności z pakietami, które mogą się czasem pojawiać w przypadku systemów opartych na modelu ciągłych wydań.

## Społeczność

Społeczność Archa jest naprawdę niezawodną, żywą i otwartą na nowych członków grupą. Wszyscy "Archersi" są zachęcani do pomocy w rozwoju dystrybucji. Każda pomoc jest mile widziana, zarówno pomoc w rozwoju oprogramowania głównego, opieka nad pakietami, raportowanie i usuwanie [błędów](https://bugs.archlinux.org/), usprawnianie [Dokumentacji Archa](/index.php/Main_page_(Polski) "Main page (Polski)"), pomoc innym użytkownikom lub wyrażanie własnych opinii na [forum](https://bbs.archlinux.org/), [lista mailingowa](https://mailman.archlinux.org/mailman/listinfo/), [Kanały IRC'owe](/index.php?title=IRC_Channels_(Polski)&action=edit&redlink=1 "IRC Channels (Polski) (page does not exist)") , czy też udostępnianie swojej wiedzy bądź aplikacji. Arch Linux jest systemem operacyjnym wybieranym przez użytkowników na całym świecie, istnieje wiele [Społeczności Międzynarodowych](/index.php?title=International_Communities_(Polski)&action=edit&redlink=1 "International Communities (Polski) (page does not exist)"), które oferują swoją pomoc oraz dostarczają dokumentację systemu w wielu różnych językach.

Zainteresuj się rozdziałem [Jak pomóc](/index.php/Getting_involved_(Polski) "Getting involved (Polski)"), jeśli jesteś zainteresowany zostaniem aktywnym członkiem społeczności.

## Podsumowanie

Podsumowując: Arch Linux jest wszechstronną, a zarazem prostą dystrybucją, której zadaniem jest zaspokojenie potrzeb jak największej liczby użytkowników Linuksa. Arch Linux idealnie sprawdza się na serwerach jak i na stacjach roboczych, będąc jednocześnie potężnym i prostym w obsłudze systemem. To Ty obierasz drogę, którą dalej będzie podążał Twój system. Jeśli właśnie taka jest Twoja wizja systemu z rodziny GNU/Linux, jesteś mile widziany w społeczności Arch Linux. Zachęcamy także do aktywnego działania na rzecz tej dystrybucji. Witamy!