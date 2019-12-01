Ten dokument jest przewodnikiem do instalacji [Arch Linuxa](/index.php/Arch_Linux_(Polski) "Arch Linux (Polski)") z systemu live uruchomionego z oficjalnym obrazem instalacyjnym (iso). Przed instalacją, zalecane jest przejrzenie [najczęściej zadawanych pytań (FAQ)](/index.php/Frequently_asked_questions_(Polski) "Frequently asked questions (Polski)"). Dla konwencji użytych w tym dokumencie, zobacz stronę [Help:Reading](/index.php/Help:Reading "Help:Reading"). Należy również wziąć pod uwagę, że większość linków na tej stronie prowadzi do ich angielskich wersji.

Dla dokładniejszych instrukcji, zobacz odpowiednie artykuły [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") lub [strony podręcznika](/index.php/Man_page "Man page") poszczególnych programów, oba podlinkowane w tym przewodniku. Zobacz stronę podręcznika [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7) aby zapoznać się z ogólnym opisem konfiguracji. Można też szukać pomocy innych użytkowników Arch Linuksa, online poprzez [forum](https://bbs.archlinux.org/) oraz [kanał IRC](/index.php/IRC_channel "IRC channel"). Powodzenia!

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Wstęp](#Wstęp)
*   [2 Przed instalacją](#Przed_instalacją)
    *   [2.1 Układ klawiatury](#Układ_klawiatury)
        *   [2.1.1 Polski układ klawiatury](#Polski_układ_klawiatury)
    *   [2.2 Zweryfikuj tryb uruchomionego systemu](#Zweryfikuj_tryb_uruchomionego_systemu)
    *   [2.3 Połącz się z Internetem](#Połącz_się_z_Internetem)
        *   [2.3.1 Połączenie przewodowe (kabel Ethernet)](#Połączenie_przewodowe_(kabel_Ethernet))
        *   [2.3.2 Połączenie bezprzewodowe WIFI](#Połączenie_bezprzewodowe_WIFI)
    *   [2.4 Zaktualizuj systemowy zegar](#Zaktualizuj_systemowy_zegar)
    *   [2.5 Wybierz serwery lustrzane](#Wybierz_serwery_lustrzane)
    *   [2.6 Przygotowanie dysków i partycji](#Przygotowanie_dysków_i_partycji)
        *   [2.6.1 Partycjonowanie dysków i modyfikacja tablicy partycji](#Partycjonowanie_dysków_i_modyfikacja_tablicy_partycji)
            *   [2.6.1.1 Przykładowe układy partycji](#Przykładowe_układy_partycji)
        *   [2.6.2 Formatowanie partycji](#Formatowanie_partycji)
*   [3 Instalacja](#Instalacja)
    *   [3.1 Montowanie systemu plików](#Montowanie_systemu_plików)
    *   [3.2 Instalacja podstawowego systemu](#Instalacja_podstawowego_systemu)
    *   [3.3 Fstab](#Fstab)
    *   [3.4 Chroot](#Chroot)
    *   [3.5 Strefa czasowa](#Strefa_czasowa)
    *   [3.6 Język](#Język)
    *   [3.7 Nazwa hosta](#Nazwa_hosta)
    *   [3.8 Konfiguracja sieci](#Konfiguracja_sieci)
    *   [3.9 Instalacja pakietów dodatkowych](#Instalacja_pakietów_dodatkowych)
    *   [3.10 Initramfs](#Initramfs)
    *   [3.11 Hasło użytkownika root](#Hasło_użytkownika_root)
    *   [3.12 Program rozruchowy](#Program_rozruchowy)
    *   [3.13 Uruchom ponownie](#Uruchom_ponownie)
*   [4 Po instalacji](#Po_instalacji)

## Wstęp

Arch Linux powinien działać na dowolnej maszynie z 64-bitowym procesorem ([x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64")). Podstawowa instalacja zawierająca pakiety takie jak pakiet [base](https://www.archlinux.org/packages/?name=base), jądro systemu GNU/Linux oraz podstawowe pakiety do obsługi systemu jak menedżer oprogramowania, sterowniki sprzętu i programy do obsługi sieci, powinna zająć mniej niż 800 MB miejsca na dysku.

**Ponieważ proces instalacji musi pobrać pakiety z zewnętrznego repozytorium, wymagane jest działające połączenie internetowe.**

## Przed instalacją

Pobierz i uruchom dysk instalacyjny zgodnie instrukcją zawartą w artykule [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch"). Po uruchomieniu systemu live, zostaniesz zalogowany na pierwszej [wirtualnej konsoli](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console") jako użytkownik root z shell'em [Zsh](/index.php/Zsh "Zsh").

Podstawowe komendy takie jak [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) mogą zostać [automatycznie dokończone po naciśnięciu przycisku TAB](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

By przejść do innej konsoli, np. aby zobaczyć ten przewodnik w programie [ELinks](/index.php/ELinks "ELinks"), podczas instalacji użyj [skrótu](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*strzałka*`. By [edytować](/index.php/Textedit "Textedit") pliki konfiguracyjne, możesz użyć konsolowych edytorów tekstu takich jak [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") lub [vim](/index.php/Vim#Usage "Vim").

### Układ klawiatury

**Note:** Te zmiany dotyczą jedynie środowiska instalacyjnego i nie zostaną zapisane w docelowym systemie.

Domyślny [układ klawiatury w konsoli](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") to układ amerykański - [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). By wyświetlić dostępne układy klawiatury, wpisz w konsoli `ls /usr/share/kbd/keymaps/**/*.map.gz`. Aby zmienić układ, użyj odpowiedniej nazwy układu w poleceniu [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1) (bez rozszerzenia pliku).

[Czcionki konsolowe](/index.php/Console_fonts "Console fonts") są zlokalizowane w `/usr/share/kbd/consolefonts/` i mogą być w podobny sposób ustawione poleceniem [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

#### Polski układ klawiatury

Aby ustawić polski układ klawiatury, wpisz:

```
# loadkeys pl

```

Jeśli polskie znaki diakrytyczne (ą, ę, ł itp.) nie wyświetlają się poprawnie, wpisz:

```
# setfont Lat2-Terminus16.psfu.gz -m 8859-2

```

Powyższa komenda ustawia czcionkę z polskimi znakami diakrytycznymi w konsoli. W późniejszej części artykułu opisany zostanie sposób, by permanentnie ustawić polski układ i odpowiednią czcionkę.

### Zweryfikuj tryb uruchomionego systemu

Jeśli Twój komputer korzysta z trybu UEFI [UEFI](/index.php/UEFI "UEFI"), obraz instalacyjny [uruchomi](/index.php/Boot "Boot") Arch Linux z pomocą [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). By zweryfikować obecność systemu UEFI, sprawdź zawartość folderu [efivars](/index.php/UEFI#UEFI_variables "UEFI") następującą komendą:

```
# ls /sys/firmware/efi/efivars

```

Jeśli ten folder nie istnieje, system może być uruchomiony w [BIOSie](https://en.wikipedia.org/wiki/BIOS "w:BIOS") lub trybie CSM (bez UEFI).

Brak lub istnienie trybu UEFI będzie mieć wpływ na partycjonowanie dysku przed instalacją oraz sposób instalacji i konfiguracji programu rozruchowego.

### Połącz się z Internetem

**Note:** Te zmiany dotyczą jedynie środowiska instalacyjnego i nie zostaną zapisane w docelowym systemie.

#### Połączenie przewodowe (kabel Ethernet)

Połączenie przewodowe (po kablu Ethernet) powinno działać bez dodatkowych czynności. Obraz instalacyjny [uruchamia](/index.php/Enable "Enable") [dhcpcd](/index.php/Dhcpcd "Dhcpcd") dla połączenia [przewodowego](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules). Możesz sprawdzić połączenie poleceniem:

```
# ping archlinux.org

```

Jeśli nie masz połączenia, [zatrzymaj](/index.php/Stop "Stop") usługę *dhcpcd* poleceniem `systemctl stop dhcpcd@`, `Tab` i sprawdź stronę [Network configuration](/index.php/Network_configuration "Network configuration").

#### Połączenie bezprzewodowe WIFI

Dla bezprzewodowych połączeń, [iw(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iw.8), [wpa_supplicant(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) i [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") są dostępne. Zazwyczaj należy wpisać komendę `wifi-menu`, która przekieruje do wyboru sieci WIFI.

```
# wifi-menu

```

Jeśli masz problemy z połączeniem z siecią bezprzewodową, zapoznaj się ze stroną [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Zaktualizuj systemowy zegar

**Note:** Te zmiany dotyczą jedynie środowiska instalacyjnego i nie zostaną zapisane w docelowym systemie.

Użyj [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) by sprawdzić, czy systemowy zegar jest dokładny:

```
# timedatectl set-ntp true

```

By sprawdzić stan usługi, użyj `timedatectl status`.

### Wybierz serwery lustrzane

Pakiety do instalacji muszą być pobrane z [serwerów lustrzanych](/index.php/Mirrors "Mirrors"), które są zdefiniowane w pliku `/etc/pacman.d/mirrorlist`. W systemie live wszystkie serwery lustrzane są włączone i są sortowane przez ich status synchronizacji i szybkości w czasie, gdy obraz instalacyjny został utworzony.

Im wyżej serwer jest położony na liście, tym ma wyższy priorytet gdy pobierany jest pakiet. Możesz zedytować ten plik w odpowiedni sposób i przenieść najbliższy geograficznie serwer na górę listy, jednak powinno się wziąć pod uwagę inne krytria.

Ten plik zostanie później skopiowany do nowego systemu przez skrypt *pacstrap*, więc warto jest go dobrze skonfigurować.

### Przygotowanie dysków i partycji

**Warning:** Przed przystąpieniem do partycjonowania i formatowania, zapoznaj się z odpowiednimi działami Arch Wiki dotyczącymi [systemów plików](/index.php/File_systems "File systems"), [partycjonowania](/index.php/Partitioning "Partitioning") i montowania partycji, aby uniknąć problemów takich jak utrata danych. Jeśli nie instalujesz systemu na pustym dysku, koniecznie wykonaj kopię zapasową plików i dotychczasowego systemu.

Rozpoznane przez system live dyski są przypisane do *urządzeń blokowych (block devices)* takich jak `/dev/sda`. By zidentyfikować je, użyj [lsblk](/index.php/Lsblk "Lsblk") lub *fdisk* — wyniki kończące się `rom`, `loop` lub `airoot` mogą zostać zignorowane:

```
# fdisk -l

```

Zostaną wyświetlone wykryte dyski oraz powiązane z nimi partycje (zakończone liczbą), np. z dyskiem */dev/sda* mogą być powiązane partycje */dev/sda1*, */dev/sda2* itd.

#### Partycjonowanie dysków i modyfikacja tablicy partycji

Następujące [partycje](/index.php/Partition "Partition") są *wymagane*:

*   Jedna partycja główna z punktem montowania root `/`.
*   Jeżeli system działa z [UEFI](/index.php/UEFI "UEFI"), konieczne jest utworzenie (lub zachowanie) [partycji EFI](/index.php/EFI_system_partition "EFI system partition").

Jeśli chcesz utworzyć urządzenia [LVM](/index.php/LVM "LVM"), [zaszyfrować system](/index.php/Dm-crypt "Dm-crypt") lub [RAID](/index.php/RAID "RAID"), zrób to teraz.

**Note:** Jeżeli masz już przygotowane partycje, które zostaną użyte do instalacji i nie zamierzasz ich modyfikować, przejdź do następnego działu - Formatowanie partycji.

##### Przykładowe układy partycji

| BIOS z [MBR](/index.php/MBR "MBR") |
| Punkt montowania | Partycja | [Typ partycji](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") | Sugerowany rozmiar |
| `/mnt` | `/dev/sd*X*1` | Linux | Reszta urządzenia (dysku) |
| [SWAP] | `/dev/sd*X*2` | Partycja wymiany (SWAP) | Ponad 512 MiB |
| UEFI z [GPT](/index.php/GPT "GPT") |
| Punkt montowania | Partycja | [Typ partycji](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") | Sugerowany rozmiar |
| `/mnt/boot` albo `/mnt/efi` | `/dev/sd*X*1` | [Partycja systemowa EFI](/index.php/EFI_system_partition "EFI system partition") | 260–512 MiB |
| `/mnt` | `/dev/sd*X*2` | Partycja główna root (/) | Reszta urządzenia (dysku) |
| [SWAP] | `/dev/sd*X*3` | Partycja wymiany (SWAP) | Ponad 512 MiB |

Zapoznaj się ze stroną [dotyczącą przykładowych układów partycjonowania](/index.php/Partitioning#Example_layouts "Partitioning").

#### Formatowanie partycji

Jeżeli nie utworzyłeś nowych partycji i chcesz użyć dotychczasowych, konieczne jest jedynie sformatowanie partycji / (root).

Jeśli utworzyłeś nowe partycje, po ich utworzeniu, każda musi być sformatowana odpowiednim [systemem plików](/index.php/File_system "File system").

Na przykład, by sformatować partycję główną (/) na `/dev/*sda1*` na `*ext4*`, uruchom:

```
# mkfs.*ext4* /dev/*sda1*

```

Zobacz [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") po więcej informacji.

## Instalacja

### Montowanie systemu plików

**Note:** Poniżej pokazano jedynie przykładowe komendy. Upewnij się, że wiesz co robisz i montujesz partycje zgodnie z ich układem na Twoim twardym dysku.

[Zamontuj](/index.php/File_systems#Mount_a_file_system "File systems") system plikow na partycji głównej (/) na `/mnt`, na przykład:

```
# mount /dev/*sda1* /mnt

```

Stwórz punkty montowania dla pozostałych partycji i je zamontuj, na przykład, jeśli posiadasz oddzielną partycję na pliki użytkownika *home*, możesz użyć:

```
# mkdir /mnt/*home*
# mount /dev/*sda2* /mnt/*home*

```

W przypadku systemów z [UEFI](/index.php/UEFI "UEFI"), zamontuj [partycję rozruchową](/index.php/EFI_system_partition "EFI system partition"). Na przykład:

```
# mkdir /mnt/*boot/efi*
# mount */dev/sda4* /mnt/*boot/efi*

```

Rozważ również zamontowanie partycji na [przestrzeń wymiany](/index.php/Swap "Swap"). Na przykład:

```
# swapon */dev/sda3*

```

Polecenie [genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) wykryje po zainstalowaniu systemu zamontowane systemy plików i przestrzeń wymiany.

### Instalacja podstawowego systemu

**Warning:** **Informacja dla osób instalujących system po raz kolejny lub dokonujących reinstalacji:** Od października 2019 roku grupa pakietów *base* została zastąpiona pojedynczym pakietem [base](https://www.archlinux.org/packages/?name=base), który nie zawiera wielu podstawowych pakietów, między innymi [jądra systemu](/index.php/Kernel "Kernel"). Pakiety te powinny zostać dodatkowo zainstalowane, chyba, że wiesz co robisz. Więcej: [https://www.archlinux.org/news/base-group-replaced-by-mandatory-base-package-manual-intervention-required/](https://www.archlinux.org/news/base-group-replaced-by-mandatory-base-package-manual-intervention-required/).

Użyj skryptu [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) by zainstalować podstawowy system:

```
# pacstrap /mnt base linux linux-firmware

```

Powyższa komenda NIE zainstaluje wszystkich narzędzi ze środowiska live - zainstalowana zostanie jedynie paczka [base](https://www.archlinux.org/packages/?name=base), jądro systemu [linux](https://www.archlinux.org/packages/?name=linux) oraz podstawowe sterowniki sprzętu ([linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware)).

**Note:** Pakiet [linux](https://www.archlinux.org/packages/?name=linux) zawiera jądro w domyślnej najnowszej wersji uznawanej za stabilną. Zamiast niego można zainstalować jądro w wersji LTS [linux-lts](https://www.archlinux.org/packages/?name=linux-lts) - starsze ale o dłuższym okresie wsparcia i teoretycznie sprawiające mniej kłopotów albo inną wersję jądra dostępną z oficjalnych repozytoriów. Więcej dowiesz się [tutaj.](/index.php/Kernel "Kernel")

W wyniku wykonania powyższej komendy przede wszystkim NIE zostaną zainstalowane takie pakiety jak:

*   edytor tekstu (taki jak [vim](https://www.archlinux.org/packages/?name=vim) lub [nano](https://www.archlinux.org/packages/?name=nano)), który konieczny będzie do edytowania plików konfiguracyjnych;
*   narzędzia do obsługi [systemów plików](/index.php/File_systems "File systems") (np. [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) dla *ext4* czy [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) dla *btrfs*);
*   narzędzia do obsługi dysków [RAID](/index.php/RAID "RAID") i [LVM](/index.php/LVM "LVM");
*   pakiety dostępu do dokumentacji ([man-db](https://www.archlinux.org/packages/?name=man-db) i [man-pages](https://www.archlinux.org/packages/?name=man-pages));
*   [program rozruchowy](/index.php/Arch_boot_process#Boot_loader "Arch boot process") taki jak [grub](https://www.archlinux.org/packages/?name=grub) czy [refind-efi](https://www.archlinux.org/packages/?name=refind-efi);
*   pakiety do połączenia z siecią (między innymi [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) i [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)) czy jej obsługi (np. [dialog](https://www.archlinux.org/packages/?name=dialog) umożliwiający uruchomienie *wifi-menu*).

By [zainstalować](/index.php/Install "Install") dodatkowe pakiety i inne grupy takie jak edytor tekstu, sterowniki, program rozruchowy lub grupę [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) (zawierającą pakiety niezbędne do instalacji oprogramowania z [AUR](/index.php/AUR "AUR")), dodaj ich nazwy do polecenia *pacstrap* (rozdzielone spacją) np. `pacstrap /mnt base base-devel linux linux-firmware nano usbutils e2fsprogs dhcpcd` lub do indywidualnych komend [menedżera pakietów pacman](/index.php/Pacman "Pacman") po wejściu w do środowiska [#Chroot](#Chroot) np. `pacman -S base-devel nano usbutils e2fsprogs dhcpcd`.

### Fstab

Wygeneruj plik [fstab](/index.php/Fstab "Fstab") (użyj `-U` lub `-L` by zdefiniować wpisy przez [UUID](/index.php/UUID "UUID") lub etykiety):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

Sprawdź gotowy plik w `/mnt/etc/fstab` i zedytuj go w razie błędów.

### Chroot

[Wejdź przez chroot](/index.php/Change_root "Change root") do nowego systemu:

```
# arch-chroot /mnt

```

Po wejściu do *chroot* zostanie otwarty wiersz poleceń Twojego systemu. Każda komenda będzie miała wpływ na zainstalowany system, a wszelkie zmiany w systemie zostaną zapisane.

### Strefa czasowa

Ustaw [strefę czasową](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Dla Polski polecenie będzie wyglądało w następujący sposób:

```
# ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

```

Uruchom [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) by wygenerować `/etc/adjtime`:

```
# hwclock --systohc

```

Ta komenda zakłada, że zegar sprzętowy komputera jest ustawiony w [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"). Zobacz [System time#Time standard](/index.php/System_time#Time_standard "System time") dla większej ilości informacji.

### Język

Otwórz w swoim edytorze tekstu plik `/etc/locale.gen` i odkomentuj w nim (usuń z początku wiersza znak `#`) następujące wpisy: `en_US.UTF-8 UTF-8`, `pl_PL.UTF-8 UTF-8` i inne wymagane [lokalizacje](/index.php/Locale "Locale"). Następnie wygeneruj obsługę języków poleceniem:

```
# locale-gen

```

Ustaw [zmienną](/index.php/Variable "Variable") `LANG` w pliku [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) odpowiednio, na przykład:

 `/etc/locale.conf`  `LANG=*pl_PL.UTF-8*` 

Jeśli zmieniłeś układ klawiatury, zapisz te zmiany w pliku [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*pl*` 

Jeżeli chcesz, by w konsoli była możliwość wprowadzania polskich znaków, plik [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) ma wygladać w następujący sposób:

 `/etc/vconsole.conf` 
```
KEYMAP=pl
FONT=Lat2-Terminus16.psfu.gz
FONT_MAP=8859-2
```

### Nazwa hosta

Stwórz plik [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5):

 `/etc/hostname` 
```
*mojanazwahosta*

```

Przemyśl dodanie wpisu do pliku [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1       localhost.localdomain               localhost
::1             localhost.localdomain               localhost
**127.0.1.1	*mojanazwahosta*.localdomain	    *mojanazwahosta***

```

Zobacz również: [Network configuration#Set the hostname](/index.php/Network_configuration#Set_the_hostname "Network configuration").

### Konfiguracja sieci

Aby skonfigurować połączenie z siecią na stałe zobacz [Network configuration#Network management](/index.php/Network_configuration#Network_management "Network configuration").

Nowo zainstalowany system nie ma żadnego połączenia z siecią uruchomionego domyślnie. Do połączenia z siecią niezbędny będzie pakiet [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) i uruchomienie odpowiedniej usługi.

Dla [sieci bezprzewodowych](/index.php/Wireless_configuration "Wireless configuration"), [zainstaluj](/index.php/Install "Install") pakiety [iw](https://www.archlinux.org/packages/?name=iw) i [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) i wymagane [pakiety firmware](/index.php/Wireless#Installing_driver/firmware "Wireless"). Opcjonalnie zainstaluj [dialog](https://www.archlinux.org/packages/?name=dialog) dla użycia *wifi-menu*.

### Instalacja pakietów dodatkowych

Jak już wskazano wcześniej, komenda `pacstrap /mnt base linux linux-firmware` nie zainstaluje niektórych pakietów, które mogą okazać się niezbędne do działania systemu.

Takimi pakietami mogą okazać się:

*   edytor tekstu (taki jak [vim](https://www.archlinux.org/packages/?name=vim) lub [nano](https://www.archlinux.org/packages/?name=nano)), który konieczny będzie do edytowania plików konfiguracyjnych;
*   narzędzia do obsługi [systemów plików](/index.php/File_systems "File systems") (np. [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) dla *ext4* czy [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) dla *btrfs*);
*   narzędzia do obsługi dysków [RAID](/index.php/RAID "RAID") i [LVM](/index.php/LVM "LVM");
*   pakiety dostępu do dokumentacji ([man-db](https://www.archlinux.org/packages/?name=man-db) i [man-pages](https://www.archlinux.org/packages/?name=man-pages));
*   [program rozruchowy](/index.php/Arch_boot_process#Boot_loader "Arch boot process") taki jak [grub](https://www.archlinux.org/packages/?name=grub) czy [refind-efi](https://www.archlinux.org/packages/?name=refind-efi);
*   pakiety do połączenia z siecią (między innymi [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) i [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant)) czy jej obsługi (np. [dialog](https://www.archlinux.org/packages/?name=dialog) umożliwiający uruchomienie *wifi-menu*).

Pozostając w środowisku [Chroot](/index.php/Chroot "Chroot") pakiety te można doinstalować jeszcze przed pierwszym uruchomieniem systemu, korzystając z menedżera pakietów [*pacman*](/index.php/Pacman_(Polski) "Pacman (Polski)"). Należy też pamiętać o ich wcześniejszym skonfigurowaniu, jeśli jest taka potrzeba (np. w przypadku programu rozruchowego typu [grub](https://www.archlinux.org/packages/?name=grub)).

### Initramfs

Stworzenie nowego *initramfs* jest zazwyczaj nie wymagane, gdyż polecenie [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") było uruchomione podczas instalacji pakietu [linux](https://www.archlinux.org/packages/?name=linux) poleceniem *pacstrap*.

Dla specjalnych konfiguracji, zmodyfikuj plik [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) i stwórz obraz initramfs:

```
# mkinitcpio -p linux

```

### Hasło użytkownika root

Ustaw [hasło](/index.php/Password "Password") dla użytkownika root:

```
# passwd

```

### Program rozruchowy

Zobacz [Category:Boot loaders](/index.php/Category:Boot_loaders "Category:Boot loaders") dla możliwych wyborów i konfiguracji.

Jeśli posiadasz procesor Intela, zainstaluj pakiet [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) i [uruchom aktualizacje mikrokodu](/index.php/Microcode#Early_loading "Microcode").

### Uruchom ponownie

**Warning:** **Uwaga!** Przed ponownym uruchomieniem upewnij się, że zainstalowane są podstawowe pakiety umożliwiające dalszą konfigurację systemu. Przede wszystkim upewnij się, że system posiada [jądro](/index.php/Kernel "Kernel"), pakiety do połączenia z [internetem](/index.php/Network_configuration "Network configuration"), sterowniki sprzętu (zazwyczaj wystarczy pakiet [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware)), pakiety od obsługi [systemu plików](/index.php/File_systems "File systems"), bez których system może nie odczytać danych z dysku, [edytor tekstu](/index.php/Category:Text_editors "Category:Text editors") oraz zainstalowany i skonfigurowany [program rozruchowy](/index.php/Category:Boot_loaders "Category:Boot loaders"). W przeciwnym wypadku system może nie uruchomić się prawidłowo lub jego konfiguracja będzie utrudniona lub niemożliwa. Zawsze jednak możesz użyć środowiska [chroot](/index.php/Chroot "Chroot") z dysku instalacyjnego by doinstalować brakujące pakiety bez konieczności ponownej instalacji całego systemu.

Opuść środowisko chroot poleceniem `exit` lub naciskając `Ctrl+D`.

Opcjonalnie manualnie odmontuj wszystkie partycje poleceniem `unmount -R /mnt`, co pozwoli na sprawdzenie "zajętych" partycji i znalezienia przyczyny poleceniem [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Na koniec, uruchom ponownie maszynę wpisując `reboot`. Pozostałe partycje zostaną odmontowane automatycznie przez *systemd*. Pamiętaj, by po wyłączeniu systemu, usunąć nośnik instalacyjny. Po uruchomieniu nowozainstalowanego systemu zaloguj się koncie *root*, aby dokończyć konfigurację systemu.

## Po instalacji

Zobacz [General recommendations (Polski)](/index.php/General_recommendations_(Polski) "General recommendations (Polski)") dla możliwości zarządzania system i poradników po instalacji (takich jak instalacja graficznego interfejsu użytkownika, dźwięku, czy gładzika).

Dla listy aplikacji, które mogą się okazać przydatne, zobacz artykuł [List of applications](/index.php/List_of_applications "List of applications").