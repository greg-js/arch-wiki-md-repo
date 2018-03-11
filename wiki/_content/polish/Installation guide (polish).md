Ten dokument jest przewodnikiem do instalacji [Arch Linuxa](/index.php/Arch_Linux_(Polski) "Arch Linux (Polski)") z sytemu live uruchomionego oficjalnym obrazem instalacyjnym. Przed instalacją, zalecane jest przejrzenie [najczęściej zadawanych pytań (FAQ)](/index.php/FAQ "FAQ"). Dla konwencji użytych w tym dokumencie, zobacz stronę [Help:Reading](/index.php/Help:Reading "Help:Reading"). Należy również wziąć pod uwagę, że wszystkie linki na tej stronie prowadzą do ich angielskich wersji.

Dla dokładniejszych instrukcji, zobacz odpowiednie artykuły [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") lub [strony podręcznika](/index.php/Man_page "Man page") poszczególnych programów, oba podlinkowane w tym przewodniku. Zobacz stronę podręcznika [archlinux(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/archlinux.7) dla ogólny opis konfiguracji. Dla interaktywnej pomocy, dostępne jest [forum](https://bbs.archlinux.org/) oraz [kanał IRC](/index.php/IRC_channel "IRC channel").

## Contents

*   [1 Przed instalacją](#Przed_instalacj.C4.85)
    *   [1.1 Układ klawiatury](#Uk.C5.82ad_klawiatury)
        *   [1.1.1 Polski układ klawiatury](#Polski_uk.C5.82ad_klawiatury)
    *   [1.2 Zweryfikuj tryb uruchomionego systemu](#Zweryfikuj_tryb_uruchomionego_systemu)
    *   [1.3 Połącz się z Internetem](#Po.C5.82.C4.85cz_si.C4.99_z_Internetem)
    *   [1.4 Zaktualizuj systemowy zegar](#Zaktualizuj_systemowy_zegar)
    *   [1.5 Partycjonuj dyski](#Partycjonuj_dyski)
    *   [1.6 Formatowanie partycji](#Formatowanie_partycji)
    *   [1.7 Zamontuj system plików](#Zamontuj_system_plik.C3.B3w)
*   [2 Instalacja](#Instalacja)
    *   [2.1 Wybierz serwery lustrzane](#Wybierz_serwery_lustrzane)
    *   [2.2 Instalacja pakietów z grupy *base*](#Instalacja_pakiet.C3.B3w_z_grupy_base)
*   [3 Konfiguracja systemu](#Konfiguracja_systemu)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Strefa czasowa](#Strefa_czasowa)
    *   [3.4 Język](#J.C4.99zyk)
    *   [3.5 Nazwa hosta](#Nazwa_hosta)
    *   [3.6 Konfiguracja sieci](#Konfiguracja_sieci)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Hasło użytkownika root](#Has.C5.82o_u.C5.BCytkownika_root)
    *   [3.9 Program rozruchowy](#Program_rozruchowy)
*   [4 Uruchom ponownie](#Uruchom_ponownie)
*   [5 Po instalacji](#Po_instalacji)

## Przed instalacją

Arch Linux powinien być uruchamiany na dowolnej maszynie [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") z minimalną ilością 512 MB pamięci RAM. Podstawowa instalacja pakietów z grupy [base](https://www.archlinux.org/groups/x86_64/base/) powinna zająć mniej, niż 800 MB miejsca na dysku. Jako iż proces instalacji musi pobrać pakiety z zewnętrznego repozytorium, wymagane jest działające połączenie internetowe.

Pobierz i uruchom dysk instalacyjny jak opisane w kategorii [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch"). Zostaniesz zalogowany na pierwszej [wirtualnej konsoli](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console") jako użytkownik root z shell'em [Zsh](/index.php/Zsh "Zsh"); podstawowe komendy takie jak [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) mogą zostać [automatycznie dokończone po naciśnięciu przycisku TAB](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

By przejść do innej konsoli, by np. zobaczyć ten przewodnik programem [ELinks](/index.php/ELinks "ELinks") podczas instalacji użyj [skrótu](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*strzałka*`. By [edytować](/index.php/Textedit "Textedit") pliki konfiguracyjne, możesz użyć programów [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") i [vim](/index.php/Vim#Usage "Vim").

### Układ klawiatury

Domyślny [zestaw znaków w konsoli](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") to [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). By wyświetlić dostępne układy, wpisz w konsoli `ls /usr/share/kbd/keymaps/**/*.map.gz`. Aby zmodyfikować układ użyj odpowiedniej nazwy pliki w poleceniu [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), odrzucając ścieżkę i rozszerzenie. Dla przykładu, wpisz `loadkeys de-latin1`, by wybrać [niemiecki](https://en.wikipedia.org/wiki/File:KB_Germany.svg "w:File:KB Germany.svg") układ klawiatury

[Czcionki konsolowe](/index.php/Console_fonts "Console fonts") są zlokalizowane w `/usr/share/kbd/consolefonts/` i mogą być w podobny sposób ustawione poleceniem [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

#### Polski układ klawiatury

Aby ustawić polski układ klawiatury, wpisz `loadkeys pl`. Jeśli polskie znaki nie wyświetlają się poprawnie, wpisz `setfont Lat2-Terminus16.psfu.gz -m 8859-2`, by ustawić odpowiednią czcionkę w konsoli. W późniejszej części artykułu opisany zostanie sposób, by permanentnie ustawić polski układ i odpowiednią czcionkę.

### Zweryfikuj tryb uruchomionego systemu

Jeśli tryb UEFI jest uruchomiony na płycie głównej [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso "Archiso") [uruchomi](/index.php/Boot "Boot") Arch Linux z pomocą [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). By to zweryfikować, sprawdź zawartość folderu [efivars](/index.php/UEFI#UEFI_variables "UEFI"):

```
# ls /sys/firmware/efi/efivars

```

Jeśli ten folder nie istnieje, system może być uruchomiony w [BIOSie](https://en.wikipedia.org/wiki/BIOS "w:BIOS") lub trybie CSM. Odnieś się do podręcznika twojej płyty głównej dla detali.

### Połącz się z Internetem

Obraz instalacyjny [uruchamia](/index.php/Enable "Enable") [dhcpcd](/index.php/Dhcpcd "Dhcpcd") dla połączenia [przewodowego](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules). Możesz sprawdzić połączenie poleceniem:

```
# ping archlinux.org

```

Jeśli nie masz połączenia, [zatrzymaj](/index.php/Stop "Stop") usługę *dhcpcd* poleceniem `systemctl stop dhcpcd@`, `Tab` i sprawdź stronę [Network configuration](/index.php/Network_configuration "Network configuration").

Dla bezprzewodowych połączeń, [iw(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/iw.8), [wpa_supplicant(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wpa_supplicant.8) i [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") są dostępne. Zobacz stronę [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Zaktualizuj systemowy zegar

Użyh [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) by sprawdzić, czy systemowy zegar jest dokładny:

```
# timedatectl set-ntp true

```

By sprawdzić stan usługi, użyj `timedatectl status`.

### Partycjonuj dyski

Gdy rozpoznane przez system live, dyski są przypisane do *urządzeń blokowych (block devices)* takich jak `/dev/sda`. By zidentyfikować je, użyj [lsblk](/index.php/Lsblk "Lsblk") lub *fdisk* — wyniki kończące się `rom`, `loop` lub `airoot` mogą zostać zignorowane:

```
# fdisk -l

```

Następujące *partycje* (zakończone liczbą) są wymagane dla wybranego urządzenia:

*   Jedna partycja jako katalog główny (filesystem root) `/`.
*   Jeśli [UEFI](/index.php/UEFI "UEFI") jest włączone, [partycja systemowa EFI](/index.php/EFI_System_Partition "EFI System Partition").

[Przestrzeń wymiany](/index.php/Swap_space "Swap space") może być ustawiona na oddzielnej partycji lub [pliku wymiany](/index.php/Swap_file "Swap file").

By modyfikowć *tablice partycji*, użyj [fdisk](/index.php/Fdisk "Fdisk") lub [parted](/index.php/Parted "Parted"). Zobacz stronę [Partitioning](/index.php/Partitioning "Partitioning") po więcej informacji.

Jesli chcesz stworzyć *stacked block device* dla [LVM](/index.php/LVM "LVM"), [szyfrowania dysku](/index.php?title=Szyfrowania_dysku&action=edit&redlink=1 "Szyfrowania dysku (page does not exist)") lub [RAID](/index.php/RAID "RAID"), zrób to teraz.

### Formatowanie partycji

Po stworzeniu partycji, każda musi być sformatowana odpowiednim [systemem plików](/index.php/File_system "File system"). Na przykład, by sformatować partycję główną (/) na `/dev/*sda1*` na `*ext4*`, uruchom:

```
# mkfs.*ext4* /dev/*sda1*

```

Zobacz [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") po więcej informacji.

### Zamontuj system plików

[Zamontuj](/index.php/File_systems#Mount_a_file_system "File systems") system plikow na partycji głównej (/) na `/mnt`, na przykład:

```
# mount /dev/*sda1* /mnt

```

Stwórz punkty montowania dla pozostałych partycji i je zamontuj, na przykład:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) wykryje później zamontowane systemy plików i przestrzeń wymiany.

## Instalacja

### Wybierz serwery lustrzane

Pakiety do instalacji muszą być pobrane z [serwerów lustrzanych](/index.php/Mirrors "Mirrors"), które są zdefiniowane w pliku `/etc/pacman.d/mirrorlist`. W systemie live wszystkie serwery lustrzane są włączone i są sortowane przez ich status synchronizacji i szybkości w czasie, gdy obraz instalacyjny został utworzony.

Im wyżej serwer jest położony na liście, tym ma wyższy priorytet gdy pobierany jest pakiet. Możesz zedytować ten plik w odpowiedni sposób i przenieść najbliższy geograficznie serwer na górę listy, jednak powinno się wziąć pod uwagę inne krytria.

Ten plik zostanie później skopiowany do nowego systemu przez skrypt *pacstrap*, więc warto jest go dobrze skonfigurować.

### Instalacja pakietów z grupy *base*

Użyj skryptu [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) by zainstalować grupę pakietów [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

Ta grupa nie obejmuje wszystkich narzędzi ze środowiska live, takich jak [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs), czy specyficznego oprogramowania dla urządzeń bezprzewodowych; zobacz [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) dla porównania.

By [zainstalować](/index.php/Install "Install") pakiety i inne grupy takie jak [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), dodaj ich nazwy do polecenia *pacstrap* (rozdzielone spacją) lub do indywidualnych komend [menedżera pakietów pacman](/index.php/Pacman "Pacman") po wejściu w do środowiska [#Chroot](#Chroot).

## Konfiguracja systemu

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

Ta komenda zakłada, że zegar sprzętowy komputera jest ustawiony w [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"). Zobacz [Time#Time standard](/index.php/Time#Time_standard "Time") dla większej ilości informacji.

### Język

Odkomentuj `en_US.UTF-8 UTF-8`, `pl_PL.UTF-8 UTF-8` i inne wymagane [lokalizacje](/index.php/Locale "Locale") w pliku `/etc/locale.gen` i wygeneruj je poleceniem:

```
# locale-gen

```

Ustaw [zmienną](/index.php/Variable "Variable") `LANG` w pliku [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) odpowiednio, na przykład:

 `/etc/locale.conf`  `LANG=*pl_PL.UTF-8*` 

Jeśli zmieniłeś układ klawiatury, zapisz te zmiany w pliku [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

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

Nowo zainstalowany system nie ma żadnego połączenia z siecią uruchomionego domyślnie. Zobacz [Network configuration#Network managers](/index.php/Network_configuration#Network_managers "Network configuration").

Dla [sieci bezprzewodowych](/index.php/Wireless_configuration "Wireless configuration"), [zainstaluj](/index.php/Install "Install") pakiety [iw](https://www.archlinux.org/packages/?name=iw) i {{Pkg|wpa_supplicant} i wymagane [pakiety firmware](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless"). Opcjonalnie zainstaluj [dialog](https://www.archlinux.org/packages/?name=dialog) dla użycia *wifi-menu*.

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

Jeśli posiadasz procesor Intela, zainstaluj pakiet [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) i [uruchom aktualizacje mikrokodu](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode")

## Uruchom ponownie

Opuść środowisko chroot poleceniem `exit` lub naciskając `Ctrl+D`.

Opcjonalnie manualnie odmontuj wszystkie partycje poleceniem `unmount -R /mnt`: to pozwoli na sprawdzenie "zajętych" partycji i znalezienia przyczyny poleceniem [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Na koniec, uruchom ponownie maszynę wpisując `reboot`: pozostałe partycje pozostaną odmontowane automatycznie przez *systemd*. Pamiętaj, by usunąć medium instalacyjne i wtedy zaloguj się do nowego systemu jako użytkownik root.

## Po instalacji

Zobacz [General recommendations](/index.php/General_recommendations "General recommendations") dla możliwości zarządzania system i poradników po instalacji (takich jak instlacja graficznego interfejsu użytkownika, dźwięku, czy gładzika).

Dla listy aplikacji, które mogą się okazać przydatne, zobacz artykuł [List of applications](/index.php/List_of_applications "List of applications").