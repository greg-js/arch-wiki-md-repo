Partycjonowanie dysku pozwala na logiczny podział dostępnej przestrzeni dyskowej na sekcje, które mogą być używane niezależnie od siebie.

Cały dysk twardy może być dostępny jako jedna partycja lub można podzielić dostępne miejsce na kilka partycji. Różne możliwości wymagają utworzenia wielu partycji, np. dual- lub multi-booting, czy utworzenie partycji wymiany (swap). W innych przypadkach partycjonowanie jest używane jako środek podziału danych, np. utworzenie osobnych partycji dla plików audio i video. Najczęściej używane układy partycji zostały omówione poniżej.

Każda partycja musi zostać [sformatowana](/index.php/File_systems_(Polski) "File systems (Polski)") przed użyciem.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tablica partycji](#Tablica_partycji)
    *   [1.1 Master Boot Record](#Master_Boot_Record)
    *   [1.2 GUID Partition Table](#GUID_Partition_Table)
    *   [1.3 Wybór pomiędzy GPT i MBR](#Wybór_pomiędzy_GPT_i_MBR)
*   [2 Układ Partycji](#Układ_Partycji)
    *   [2.1 Jedna partycja](#Jedna_partycja)
    *   [2.2 Oddzielanie partycji](#Oddzielanie_partycji)
    *   [2.3 Punkty montowania](#Punkty_montowania)
        *   [2.3.1 Partycja Główna (root)](#Partycja_Główna_(root))
        *   [2.3.2 /boot](#/boot)
        *   [2.3.3 /home](#/home)
        *   [2.3.4 /var](#/var)
        *   [2.3.5 /tmp](#/tmp)
        *   [2.3.6 Swap](#Swap)
        *   [2.3.7 Rozmiary partycji](#Rozmiary_partycji)
*   [3 Użycie GPT - nowoczesna metoda](#Użycie_GPT_-_nowoczesna_metoda)
    *   [3.1 Użycie gdisk](#Użycie_gdisk)
*   [4 Użycie MBR - stara metoda](#Użycie_MBR_-_stara_metoda)
    *   [4.1 Użycie fdisk](#Użycie_fdisk)

## Tablica partycji

Informacje o partycjach są przechowywane w tablicy partycji. Są dwa formaty: klasyczny [Master Boot Record](/index.php?title=Master_Boot_Record_(Polski)&action=edit&redlink=1 "Master Boot Record (Polski) (page does not exist)") i nowszy [GUID Partition Table](/index.php?title=GUID_Partition_Table_(Polski)&action=edit&redlink=1 "GUID Partition Table (Polski) (page does not exist)") , który jest ulepszoną wersją pozbawioną kilku ograniczeń.

### Master Boot Record

[Wikipedia:Master boot record](https://en.wikipedia.org/wiki/Master_boot_record "wikipedia:Master boot record")

MBR standardowo obsługiwał utworzenie maksymalnie 4 partycji. Później dodano możliwość tworzenia rozszerzonych i logicznych partycji, umożliwiając obejście tego problemu.

Są więc 3 typy partycji:

*   Główna
*   Rozszerzona
    *   Logiczna

**Partycje główne** mogą być bootowalne i mają limit do maks. czterech partycji na dysk lub urządzenie RAID. Jeśli układ partycji wymaga więcej niż 4 partycji należy użyć partycji rozszerzonej zawierającej partycje logiczne. Partycja rozszerzona może być traktowana jako miejsce przechowywania partycji logicznych. Dysk twardy może zawierać tylko jedną partycję rozszerzoną. Partycja rozszerzona jest oznaczona jako partycja główna, więc oprócz niej można utworzyć jeszcze 3 partycje główne. Nie ma natomiast limitu liczby partycji logicznych w partycji rozszerzonej. Jeśli zamierzasz uruchamiać system w trybie dual-boot z systemem Windows będzie on wymagał jednej (lub 2 w przypadku Windows Vista i nowszych) osobnych partycji głównych.

Powszechnie używa się 3 partycji głównych (*sda1, sda2, sda3*) oraz jednej rozszerzonej (sda4). Partycje logiczne na *sda4* są oznaczane jako *sda5, sda6*, itd.

### GUID Partition Table

[Wikipedia:GUID Partition Table](https://en.wikipedia.org/wiki/GUID_Partition_Table "wikipedia:GUID Partition Table")

Jest tu tylko jeden typ partycji, **główna**. Nie ma tu limitu liczby partycji.

### Wybór pomiędzy GPT i MBR

[GUID Partition Table](/index.php?title=GUID_Partition_Table_(Polski)&action=edit&redlink=1 "GUID Partition Table (Polski) (page does not exist)") (GPT) jest alternatywnym, nowoczesnym stylem partycjonowania. Jest następcą starego już [Master Boot Record](/index.php?title=Master_Boot_Record_(Polski)&action=edit&redlink=1 "Master Boot Record (Polski) (page does not exist)") (MBR). GPT ma kilka zalet względem MBR.

Przy wyborze zazwyczaj kieruje się:

*   Jeśli używasz grub legacy (starej wersji) jako bootloader, musisz użyć MBR.
*   Jeśli używasz dual-boot z systemem Windows, musisz użyć MBR.
    *   Jednak jeśli używasz 64-bitowego Windowsa z UEFI zamiast BIOS-u, należy użyć GPT.
*   Jeśli nie używasz żadnego z powyższych zaleca się użycie GPT, powieważ jest nowocześniejszy.
*   Jeśli używasz [UEFI](/index.php?title=Unified_Extensible_Firmware_Interface_(Polski)&action=edit&redlink=1 "Unified Extensible Firmware Interface (Polski) (page does not exist)") zaleca się użyć GPT, ponieważ oprogramowanie UEFI może nie zezwolić na uruchomienie UEFI-MBR.

## Układ Partycji

Nie ma ściśle określonych reguł podziału dysku na partycje. Układ partycji jest dyktowany przez różne kwestie, takie jak wymarzona elastyczność, szybkość, czy bezpieczeństwo, a także limity narzucone przez ilość miejsca na dysku. Jest to bardzo osobisty wybór. Jeśli zamierzasz używać dual boot Arch Linuksa i Windows zobacz [Dual Boot Windows i Arch Linux](/index.php?title=Windows_and_Arch_Dual_Boot_(Polski)&action=edit&redlink=1 "Windows and Arch Dual Boot (Polski) (page does not exist)").

Oto kilka typów układów partycji:

### Jedna partycja

To najprostszy schemat, który powinien wystarczyć w większości wypadków. [Plik wymiany](/index.php?title=Swapfile_(Polski)&action=edit&redlink=1 "Swapfile (Polski) (page does not exist)") można łatwo utworzyć i zmieniać jego rozmiar do potrzeb. Najczęściej zaczyna się tworząc pojedynczą partycję `/` i wtedy oddziela inne zależnie od wymagań, jak RAID, szyfrowanie itp.

### Oddzielanie partycji

Oddzielanie ścieżki jako partycji pozwala na wybór pomiędzy różnymi systemami plików i punktami montowania. Można również utworzyć w ten sposób partycję do współdzielenia plików między systemami operacyjnymi.

### Punkty montowania

Dla różnych partycji jest wiele możliwych wyborów punktów montowania, a decyzja, które z nich wybrać jest narzucona przez aktualne potrzeby.

#### Partycja Główna (root)

Jest to najważniejszy punkt montowania, miejsce, gdzie główny system plików zostaje zamontowany i każdy inny system plików wychodzi. Wszystkie pliki i foldery są ukazywane w folderze root `/`, nawet, jeśli są na innym nośniku. Zawartość katalogu głównego, musi być odpowiednia do rozruchu, przywracania, odzyskiwania i/lub naprawy systemu. W związku z tym niektóre foldery nie mogą być umieszczone na osobnych partycjach.

Partycja `/` jest potrzebna i najważniejsza. Inne partycje mogą być przez nią zastąpione.

**Warning:** Foldery niezbędne do uruchomienia systemu (oprócz */boot*) muszą być na tej samej partycji co `/` lub wcześnie montowane przy użyciu [initramfs](/index.php?title=Initramfs_(Polski)&action=edit&redlink=1 "Initramfs (Polski) (page does not exist)"). Te foldery to `/etc` i `/usr`.

#### /boot

Na partycji `/boot` przechowywane jest jądro (kernel) systemu, ramdisk, jak również pliki konfiguracyjne bootloadera. Zawiera również dane ładowane przed startem jądra. `/boot` nie jest wymagany do pracy w systemie, ale tylko podczas uruchamiania systemu i aktualizacji kernela (tworzenia ramdisku)

Oddzielna partycja `/boot` jest wymagana jeśli używasz RAID0 (stripe).

#### /home

W folderze {ic|/home}} przechowywane są pliki konfiguracyjne użytkowników, cache, dane aplikacji i pliki multimedialne.

Oddzielenie `/home` pozwala na zmiany w partycji `/`, ale system może być przeinstalowany bez utraty danych z `/home` nawet, jeśli nie jest na osobnej partycji - należy usunąć inne foldery i wykonać pacstrap.

Nie powinieneś używać folderów `/home` na kilku różnych dystrybucjach linuksa, ponieważ używają innych (niekompatybilnych) wersji oprogramowania i łatek. Zamiast tego można utworzyć partycję do współdzielenia plików lub ostatecznie różne foldery domowe użytkowników na partycji `/home`.

#### /var

W folderze `/var` przechowywane są zmienne dane, takie jak katalogi i pliki buforowane, dane logowania i administracyjne, cache [pacmana](/index.php/Pacman_(Polski) "Pacman (Polski)"), dane [ABS](/index.php?title=ABS_(Polski)&action=edit&redlink=1 "ABS (Polski) (page does not exist)") itp. Jest używana na przykład do buforowania czy tworzenia logów, więc jest często odczytywana i zapisywana. Używanie `/var` jako osobnej partycji zapobiega wyczerpaniu się miejsca na dysku z powodu nadmiaru logów itp.

**Note:** `/var` zawiera wiele małych plików. Powinno się to uwzględnić przy wyborze systemu plików, jeśli jest to osobna partycja.

#### /tmp

Domyślnie jest to osobna partycja montowana jako *tmpfs* przez systemd.

#### Swap

Partycja wymiany ([swap](/index.php?title=Swap_(Polski)&action=edit&redlink=1 "Swap (Polski) (page does not exist)")) to pamięć, która może być użyta jako wirtualny RAM. Powinno się brać pod uwagę również [plik wymiany](/index.php?title=Swapfile_(Polski)&action=edit&redlink=1 "Swapfile (Polski) (page does not exist)"), ponieważ nie ma praktycznie żadnej różnicy w wydajności, ale jest znacznie łatwiejsza do modyfikowania. Partycja swap *prawdopodobnie* może być współdzielona między kilkoma systemami, ale nie wtedy, kiedy używa się hibernacji.

**Note:** Stary sposób wyznaczania potrzebnej wielkości swap z używaną pamięcią ram podczas używania [suspend-to-disk](/index.php?title=Suspend_to_Disk_(Polski)&action=edit&redlink=1 "Suspend to Disk (Polski) (page does not exist)") nie jest już poprawny. Standardowa metoda uśpienia używa obrazu 40% dostępnego ramu. Nawet z [TuxOnIce](/index.php?title=TuxOnIce_(Polski)&action=edit&redlink=1 "TuxOnIce (Polski) (page does not exist)") po kompresji nie jest używane więcej niż 70%.[[1]](http://tuxonice.net/features)

#### Rozmiary partycji

**Note:** Poniżej zostały podane tylko przykłady; Nie ma jednej twardej reguły dotyczącej rozmiaru.

Rozmiary partycji są zależne od preferencji użytkownika, ale poniższe informacje mogą być przydatne:

	/boot - 200 MB 

	Ta partycja wymaga około 100mb, ale jeśli zamierzasz używać kilku kerneli lepszym wyborem jest użycie 200-300mb.

	/ - 15-20 GB 

	Tradycyjnie zawiera folder `/usr`, który może zajmować dużo miejsca, zależnie od ilości zainstalowanego oprogramowania. 15-20gb powinno być wystarczające dla typowego użytkownika.

	/var - 8-12 GB 

	Będzie zawierał m.in. [ABS](/index.php?title=ABS_(Polski)&action=edit&redlink=1 "ABS (Polski) (page does not exist)") tree i cache [pacmana](/index.php?title=Pacman_(Polski&action=edit&redlink=1 "Pacman (Polski (page does not exist)"). Zachowywanie starszych paczek jest przydatne, pozwala na downgrade (dezaktualizację), jednak w rezultacie szybko zapełnia się danymi. Cache pacmana szczególnie rośnie podczas aktualizacji i instalowania nowych aplikacji. Mimo wszystko może być bezpiecznie wyczyszczony w razie braku miejsca. Generalnie 8-12gb powinno wystarczyć dla większości użytkowników.

	/home - [zależnie] 

	To głównie miejsce przechowywania danych użytkownika, pobierań i multimediów. W systemie desktopowym `/home` jest najczęściej największą partycją.

	swap - [zależnie] 

	Dawniej rozmiar partycji swap był 2 razy większy niż ilość posiadanego RAMu. Kiedy komputery zaczęły posiadać coraz większą ilość RAMu ta reguła stała się przestarzała. Na maszynach posiadających do 512MB RAMu ta reguła jest właściwa. Jeśli posiada się 1024MB lib więcej można tworzyć mniejsze partycje swap lub nawet w ogóle ich nie tworzyć. W przypadku posiadania 2GB RAMu i więcej partycja swap nie jest wymagana.

	/data - [zależnie] 

	Można utworzyć tą partycję do współdzielenia różnych plików dla wszystkich użytkowników. Używanie w tym celu partycji `/home` również jest możliwe.

**Note:** Jeśli jest taka możliwość, dodanie dodatkowych 25% miejsca do każdego systemu plików będzie tworzyło bufor dla przyszłego wykorzystania i zapobiegania fragmentacji.

## Użycie GPT - nowoczesna metoda

### Użycie gdisk

Jeśli chcesz użyć GPT, narzędziem przeznaczonym do edycji tablicy partycji jest *gdisk*. Może wykonać wyrównanie partycji automatycznie do sektora 2048KiB (lub 1024KiB) co powinno być kompatybilne z większością SSD jeśli nie z wszystkimi. GNU Parted również wspiera GPT, ale jest [trudniejszy w obsłudze](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=601813). Płyta instalacyjna Archa zawiera gdisk. Jeśli będziesz potrzebować tego później w zainstalowanym systemie wystarczy pobrać paczkę [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk).

Podstawowe użycie *gdisk*:

*   Uruchom *gdisk* na swoim dysku jako root (*dysk* to na przykład `/dev/sda`):

```
# gdisk *dysk*

```

*   Jeśli dysk jest nowy lub chcesz zacząć od nowa, stwórz pustą tablicę partycji GUID używając komendy `o`.
*   Utwórz nową partycję wpisując komendę `n` (Główna/pierwsza partycja).
*   Zakładając, że partycja jest nowa, *gdisk* da jej największe możliwe wyrównanie. W przeciwnym razie, wybierze największą moc z dwóch, które będą dzielić wszystkie przesunięcia partycji.
*   Jeśli startujesz z sektora przed 2048 *gdisk* automatycznie przesunie początek partycji na 2048 sektor dysku. Gwarantuje to wyrównanie do 2048 sektorów (sektor to 512b, to jest wyrównanie do 1024KiB które powinno być odpowiednie dla każdego bloku pamięci NAND na SSD).
*   Użyj oznaczenia `+*x*{M,G}` do rozszerzenia partycji o *x* megabajtów lub gigabajtów, a jeśli wybierasz rozmiar który nie jest wielokrotnością wyrównania (1024KiB), *gdisk* zmniejszy rozmiar do najbliższej wielokrotności. Przykładowo, jeśli chcesz utworzyć partycję o rozmiarze 15GiB, wpisujesz `+15G`
*   Wybierz identyfikator typu partycji, domyślnie `Linux/Windows data` (kod`0700`), powinien być odpowiedni. Wciśnij `L` by zobaczyć listę kodów. Jeśli planujesz używać LVM wybierz `Linux LVM` (`8e00`).
*   Utwórz inne partycje w podobny sposób.
*   Zapisz tablicę partycji na dysku i wyjdź wpisując komendę `w`.
*   Sformatuj nową partycję z pomocą [file system](/index.php/File_systems_(Polski) "File systems (Polski)").

**Note:**

*   Żeby uruchomić dysk spartycjonowany jako GPT na komputerze z BIOS musisz utworzyć, najlepiej na początku dysku [BIOS boot partition](/index.php/GRUB2#GUID_Partition_Table_(GPT)_specific_instructions "GRUB2") bez systemu plików i typem partycji `BIOS boot` lub `bios_grub` (`EF02`) dla bootowania z dysku przy użyciu [GRUB](/index.php?title=GRUB_(Polski)&action=edit&redlink=1 "GRUB (Polski) (page does not exist)"). Dla [Syslinux](/index.php?title=Syslinux_(Polski)&action=edit&redlink=1 "Syslinux (Polski) (page does not exist)"),musisz utworzyć partycję `bios_grub`, ale musi być oddzielona od partycji `/boot` i mieć włączoną opcję `Legacy BIOS Bootable partition` attribute for that partition (using *gdisk*).
*   [GRUB Legacy](/index.php?title=GRUB_Legacy_(Polski)&action=edit&redlink=1 "GRUB Legacy (Polski) (page does not exist)") nie wspiera GPT, należy użyć [BURG](/index.php/BURG "BURG"), GRUB lub Syslinux.

**Warning:** Jeśli planujesz dual boot z systemem Windows w trybie BIOSu (to jedyna opcja dla 32-bitowych wersji Windows i 64-bitowego Windowsa XP) **nie** używaj GPT ponieważ Windows **nie** wspiera uruchamiania z dysku GPT w komputerze z BIOSem. Będziesz musiał użyć partycjonowania MBR i startowania w trybie BIOSu jak opisano poniżej. To ograniczenie nie dotyczy nowoczesnych 64-bitowych wersji Windows w trybie UEFI.

## Użycie MBR - stara metoda

Dla MBR narzędziem do modyfikowania tablicy partycji jest *fdisk*. Ostatnie wersje *fdiska* nie obsługują przestarzałego systemu wyświetlania cylindrów jako domyślna jednostka, jak również domyślnej kompatybilności z MS-DOS. Najnowsza wersja automatycznie wyrówna partycję do 2048 lub 1024 sektorów, co powinno działać ze wszystkimi rozmiarami EBS które są używane przez producentów dysków SSD. To oznacza, że opcje domyślne ustawią ci odpowiednie wyrównanie.

Pamiętaj, że dawniej *fdisk* używał cylindrów jako domyślna jednostka, i utrzymując dziwactwa potrzebne do kompatybilności z MS-DOS mieszały w wyrównaniu SSD. Można więc znaleźć w internecie dużo poradników z lat 2008-2009 opisujących długą drogę do poprawnych ustawień. W najnowszym *fdisku* wszystko jest znacznie prostsze, tak jak opisano w tym poradniku.

### Użycie fdisk

*   Uruchom *fdisk* na twoim dysku jako root (*dysk* to np. `/dev/sda`):

```
# fdisk *dysk*

```

*   Jeśli dysk jest nowy, lub chcesz zacząć od początku, utwórz nową tablicę partycji komendą `o`.
*   Utwórz nową partycję komendą `n` (typ-główna/pierwsza partycja partycja).
*   Użyj komendy `+*x*G` by rozszerzyć partycję o x gigabajtów. Przykładowo, by utworzyć 15GiB partycję wpisz `+15G`
*   Zmień identyfikator (id) typu partycji z domyślnego Linux (`type 83`) na wybrany poprzez użycie komendy `t`. To tylko opcjonalny krok, w razie gdyby użytkownik np. chciał utworzyć inny typ partycji, swap, NTFS, LVM itp. Listę typów partycji można wywołać komendą `l`.
*   Ustaw resztę partycji jak wyżej.
*   Zapisz tablicę partycji na dysk i wyjdź używając komendy `w`.
*   Sformatuj nowe partycje na [file system](/index.php/File_systems_(Polski) "File systems (Polski)").