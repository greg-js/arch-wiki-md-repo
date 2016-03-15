W nowym wydaniu Archa AIF (Arch Installation Framework) nie jest już dostarczany wraz z [Nośnikiem instalacyjnym 2012.07.15](https://www.archlinux.org/news/install-media-20120715-released/). W miejsce przestarzałego rozwiązania wprowadzone nowe [skrypty instalacyjne Archa](https://github.com/falconindy/arch-install-scripts), których zadaniem jest pomoc w instalacji nowego systemu. Ten artykuł stworzony jest po to, by przybliżyć proces korzystania z tych skryptów. Aby uzyskać opis procesu instalacji i postinstalacji nakierowany na początkującego użytkownika, zapoznaj się z [Poradnikiem początkującego](/index.php/Beginners%27_guide_(Polski) "Beginners' guide (Polski)").

## Contents

*   [1 Pobieranie](#Pobieranie)
*   [2 Układ klawiatury](#Uk.C5.82ad_klawiatury)
*   [3 Partycjonowanie dysku](#Partycjonowanie_dysku)
*   [4 Formatowanie partycji](#Formatowanie_partycji)
*   [5 Montowanie partycji](#Montowanie_partycji)
*   [6 Podłączenie do sieci](#Pod.C5.82.C4.85czenie_do_sieci)
    *   [6.1 Sieć bezprzewodowa](#Sie.C4.87_bezprzewodowa)
*   [7 Instalacja systemu podstawowego](#Instalacja_systemu_podstawowego)
*   [8 Instalacja programu rozruchowego](#Instalacja_programu_rozruchowego)
    *   [8.1 GRUB](#GRUB)
    *   [8.2 Syslinux](#Syslinux)
*   [9 Konfiguracja systemu](#Konfiguracja_systemu)
*   [10 Zakończenie instalacji](#Zako.C5.84czenie_instalacji)

## Pobieranie

Nowy obraz ISO dystrybucji Arch Linux możesz pobrać ze [strony pobierania Archa](https://www.archlinux.org/download/).

*   Zamiast sześciu różnych obrazów instalacyjnych, dostarczamy teraz jedynie jeden obraz, który pozwala na uruchomienie środowiska instalacyjnego (zarówno i686 jak i x86_64), które to z kolei pozwoli nam na zainstalowanie naszego systemu, pobierając niezbędne pakiety z sieci. Medium instalacyjne zawierające repozytoria [core] nie jest już dostępne.
*   Obrazy instalacyjne posiadają podpis i mocno zalecane jest sprawdzenie ich przed pierwszym użyciem. Jeśli posiadasz już dystrybucję Arch, możesz to zrobić wpisując w konsoli `pacman-key -v <iso-file>.sig` .
*   Pobrany obraz możesz wypalić na płycie CD, możesz go zamontować jako obraz ISO lub zapisać na pamięci przenośnej przy pomocy narzędzi takich jak `dd`. Jest to zalecane jedynie w przypadku nowych instalacji, użytkownicy posiadający już system Arch Linux mogą wykonać aktualizację systemu przy użyciu komendy `pacman -Syu`.

## Układ klawiatury

Dla wielu różnych krajów oraz różnych języków dostępne są różne mapy klawiatur. Przy pomocy polecenia `loadkeys pl` ustawisz standardowy polski typ klawiatury. Jeśli jesteś zainteresowany innym układem klawiatury, niezbędne pliki znajdziesz w `/usr/share/kbd/keymaps/` (możesz pominąć podawanie ścieżki i rozszerzenia pliku gdy używasz komendy `loadkeys`).

## Partycjonowanie dysku

Zajrzyj do działu [Partycjonowanie dysku](/index.php/Partitioning_(Polski) "Partitioning (Polski)") w celu zasięgnięcia dodatkowych informacji.

## Formatowanie partycji

Zajrzyj do działu [Formatowanie partycji](/index.php/File_systems_(Polski)#Formatowanie_partycji "File systems (Polski)") w celu zasięgnięcia dodatkowych informacji.

Jeśli używasz (U)EFI, prawdopodobnie będziesz potrzebować dodatkowej partycji, na której będziesz mógł umieścić systemową partycję UEFI. Więcej możesz przeczytać w artykule [UEFI](/index.php?title=Unified_Extensible_Firmware_Interface_(Polski)&action=edit&redlink=1 "Unified Extensible Firmware Interface (Polski) (page does not exist)").

## Montowanie partycji

Następnym krokiem jest zamontowanie głównej partycji w `/mnt`, najprostszym sposobem jest wpisanie w konsoli `mount /dev/sdXY /mnt`, gdzie X jest literą dysku, a Y numerem partycji. Dodatkowo musimy utworzyć nowe katalogi dla pozostałych partycji (`/mnt/boot`, `/mnt/home`, itp.), jeśli chcesz, by zostały wykryte przez `genfstab`.

## Podłączenie do sieci

Zakładając, że masz do czynienia z połączeniem przewodowym, uruchomienie `dhclient` lub `dhcpcd` powinno być wystarczające do nawiązania połączenia. W przypadku występowania problemów, więcej informacji znajdziesz w dziale [Konfiguracja sieci](/index.php?title=Configuring_network_(Polski)&action=edit&redlink=1 "Configuring network (Polski) (page does not exist)").

### Sieć bezprzewodowa

W przypadku sieci bezprzewodowych zapoznaj się z artykułem [Sieci bezprzewodowe](/index.php?title=Wireless_Setup_(Polski)&action=edit&redlink=1 "Wireless Setup (Polski) (page does not exist)") oraz z [Netcfg](/index.php/Netcfg#Configuration_.28Polski.29 "Netcfg"), w celu uzyskania informacji na temat uzyskania połączenia ze swoim punktem dostępowym.

## Instalacja systemu podstawowego

Przed rozpoczęciem instalacji możesz zechcieć dostosować plik `/etc/pacman.d/mirrorlist` umieszczając najlepsze serwery lustrzane na szczycie listy. Kopia tego pliku zostanie zainstalowana przy użyciu `pacstrap`, więc gra jest warta świeczki. Edytować ten plik możesz także już po skończonej instalacji przy użyciu narzędzia `rankmirrors`.

Używając skryptu [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in) zainstalujemy system bazowy. Jeśli jesteś zainteresowany korzystaniem z [AUR](/index.php/AUR_(Polski) "AUR (Polski)") lub [ABS](/index.php?title=ABS_(Polski)&action=edit&redlink=1 "ABS (Polski) (page does not exist)"), możesz także zainstalować rozszerzenie systemu bazowego dla deweloperów - "base devel".

```
# pacstrap /mnt base base-devel

```

Pozostałe pakiety także mogą być zainstalowane przy pomocy powyższej komendy (poszczególne pakiety powinny być oddzielone spacją).

## Instalacja programu rozruchowego

### [GRUB](/index.php?title=GRUB2_(Polski)&action=edit&redlink=1 "GRUB2 (Polski) (page does not exist)")

*   Dla BIOS-u:

```
# pacstrap /mnt grub-bios

```

*   Dla UEFI (w rzadkich przypadkach musisz użyć `grub-efi-i386` zamiast):

```
# pacstrap /mnt grub-efi-x86_64

```

*   Instalacja GRUB-a ma miejsce po wchrootowaniu się do systemu.

### [Syslinux](/index.php?title=Syslinux_(Polski)&action=edit&redlink=1 "Syslinux (Polski) (page does not exist)")

```
# pacstrap /mnt syslinux

```

## Konfiguracja systemu

Wygeneruj plik [fstab](/index.php?title=Fstab_(Polski)&action=edit&redlink=1 "Fstab (Polski) (page does not exist)") przy użyciu poniższej komendy (jeśli preferujesz używanie UUID lub etykiet, użyj odpowiednio parametrów `-U` lub `-L`):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Następnie chrootujemy się do naszego nowo zainstalowanego środowiska:

```
# arch-chroot /mnt

```

*   Wprowadź nazwę hosta do `/etc/hostname`.
*   Podlinkuj `/etc/localtime` do `/usr/share/zoneinfo/Strefa/Podstrefa`. Zamień `Strefa` oraz `Podstrefa` zgodnie ze swoimi wymaganiami. Dla przykładu:

```
# ln -s /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

```

*   Usuń znak komentarza `#` w odpowiednich miejscach w pliku `/etc/locale.gen`, a następnie wygeneruj locale przy użyciu `locale-gen`.
*   Zmień ustawienia [locale](/index.php/Locale#Setting_system-wide_locale_.28Polski.29 "Locale") w pliku `/etc/locale.conf`.
*   Ustaw polską czcionkę i układ klawiatury w `/etc/vconsole.conf`. Standardowe ustawienie dla klawiatury qwerty:

```
KEYMAP=pl2
FONT=Lat2-Terminus16

```

*   Wedle własnych potrzeb skonfiguruj plik `/etc/mkinitcpio.conf` (zobacz [mkinitcpio](/index.php?title=Mkinitcpio_(Polski)&action=edit&redlink=1 "Mkinitcpio (Polski) (page does not exist)")), a następnie wygeneruj początkowy RAM przy pomocy polecenia:

```
# mkinitcpio -p linux

```

*   Skonfiguruj program rozruchowy. Jeśli potrzebujesz pomocy, zajrzyj do poradnika [GRUB2](/index.php/GRUB2 "GRUB2"); jeśli korzystasz z innego bootloadera, skorzystaj z opcji „szukaj”.

*   Ustaw hasło dla użytkownika root przy pomocy polecenia `passwd`.

## Zakończenie instalacji

Jeśli wciąż jesteś w środowisku chroot, wpisz w konsoli `exit` lub skorzystaj z kombinacji klawiszy `Ctrl+D`. Poprzednio montowaliśmy potrzebne partycje, przed wykonaniem resetu systemu należy je odmontować. Możesz to zrobić wpisując polecenie:

```
# umount /mnt/{boot,home,}

```

Uruchom ponownie komputer i Twój system jest wstępnie gotowy. Teraz możesz go skonfigurować zgodnie z [Poradnikiem początkującego](/index.php/Beginners%27_Guide/Post-Installation_(Polski) "Beginners' Guide/Post-Installation (Polski)").