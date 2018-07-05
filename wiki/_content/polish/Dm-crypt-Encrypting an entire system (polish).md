Poniżej przedstawiono przykłady typowych scenariuszy pełnego szyfrowania systemu z dm-crypt. Wyjaśniają wszystkie adaptacje, które należy wykonać w normalnej procedurze instalacji. Wszystkie niezbędne narzędzia znajdują się na [installation image](https://www.archlinux.org/download/).

## Contents

*   [1 Przegląd](#Przegl.C4.85d)
*   [2 Prosty układ partycji z LUKS](#Prosty_uk.C5.82ad_partycji_z_LUKS)
    *   [2.1 Przygotowanie dysku](#Przygotowanie_dysku)
    *   [2.2 Preparing non-boot partitions](#Preparing_non-boot_partitions)
    *   [2.3 Przygotowanie partycji rozruchowej](#Przygotowanie_partycji_rozruchowej)
    *   [2.4 Mounting the devices](#Mounting_the_devices)
    *   [2.5 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio)
    *   [2.6 Konfiguracja programu rozruchowego](#Konfiguracja_programu_rozruchowego)
*   [3 LVM na LUKS](#LVM_na_LUKS)
    *   [3.1 Przygotowanie dysku](#Przygotowanie_dysku_2)
    *   [3.2 Przygotowywanie woluminów logicznych](#Przygotowywanie_wolumin.C3.B3w_logicznych)
    *   [3.3 Przygotowanie partycji rozruchowej](#Przygotowanie_partycji_rozruchowej_2)
    *   [3.4 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio_2)
    *   [3.5 Konfigurowanie boot loadera](#Konfigurowanie_boot_loadera)
*   [4 LUKS na LVM](#LUKS_na_LVM)
    *   [4.1 Przygotowanie dysku](#Przygotowanie_dysku_3)
    *   [4.2 Przygotowywanie woluminów logicznych](#Przygotowywanie_wolumin.C3.B3w_logicznych_2)
    *   [4.3 Przygotowanie partycji rozruchowej](#Przygotowanie_partycji_rozruchowej_3)
    *   [4.4 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio_3)
    *   [4.5 konfiguracjae boot loadera](#konfiguracjae_boot_loadera)
    *   [4.6 Konfigurowanie fstab i crypttab](#Konfigurowanie_fstab_i_crypttab)
    *   [4.7 Szyfrowanie woluminu logicznego /home](#Szyfrowanie_woluminu_logicznego_.2Fhome)
*   [5 LUKS na programowym RAID](#LUKS_na_programowym_RAID)
    *   [5.1 Przygotowanie dysku](#Przygotowanie_dysku_4)
    *   [5.2 Budowanie macierzy RAID](#Budowanie_macierzy_RAID)
    *   [5.3 Przygotowanie urządzeń blokowych](#Przygotowanie_urz.C4.85dze.C5.84_blokowych)
    *   [5.4 Konfiguracja boot loadera](#Konfiguracja_boot_loadera)
    *   [5.5 Tworzenie plików kluczy](#Tworzenie_plik.C3.B3w_kluczy)
    *   [5.6 Konfigurowanie systemu](#Konfigurowanie_systemu)
*   [6 Zwykły dm-crypt](#Zwyk.C5.82y_dm-crypt)
    *   [6.1 Przygotowanie dysku](#Przygotowanie_dysku_5)
    *   [6.2 Przygotowywanie partycji, które nie są uruchomione](#Przygotowywanie_partycji.2C_kt.C3.B3re_nie_s.C4.85_uruchomione)
    *   [6.3 Przygotowanie partycji rozruchowej](#Przygotowanie_partycji_rozruchowej_4)
    *   [6.4 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio_4)
    *   [6.5 Konfiguracja bootloadera](#Konfiguracja_bootloadera)
    *   [6.6 Po instalacji](#Po_instalacji)
*   [7 Szyfrowana partycja rozruchowa (GRUB)](#Szyfrowana_partycja_rozruchowa_.28GRUB.29)
    *   [7.1 Przygotowanie dysku](#Przygotowanie_dysku_6)
    *   [7.2 Przygotowywanie woluminów logicznych](#Przygotowywanie_wolumin.C3.B3w_logicznych_3)
    *   [7.3 Przygotowanie partycji rozruchowej](#Przygotowanie_partycji_rozruchowej_5)
    *   [7.4 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio_5)
    *   [7.5 Konfiguracja botladera](#Konfiguracja_botladera)
    *   [7.6 Konfigurowanie fstab i crypttab](#Konfigurowanie_fstab_i_crypttab_2)
*   [8 Btrfs subvolumes with swap](#Btrfs_subvolumes_with_swap)
    *   [8.1 Przygotowanie dysku](#Przygotowanie_dysku_7)
    *   [8.2 Przygotowanie partycji systemowej](#Przygotowanie_partycji_systemowej)
        *   [8.2.1 Utwórz kontener LUKS](#Utw.C3.B3rz_kontener_LUKS)
        *   [8.2.2 Odblokuj kontener LUKS](#Odblokuj_kontener_LUKS)
        *   [8.2.3 Sformatuj zmapowane urządzenie](#Sformatuj_zmapowane_urz.C4.85dzenie)
        *   [8.2.4 Zamontuj zmapowane urządzenie](#Zamontuj_zmapowane_urz.C4.85dzenie)
    *   [8.3 Tworzenie subwoluminów btrfs](#Tworzenie_subwolumin.C3.B3w_btrfs)
        *   [8.3.1 Układ](#Uk.C5.82ad)
        *   [8.3.2 Create top-level subvolumes](#Create_top-level_subvolumes)
        *   [8.3.3 Mount top-level subvolumes](#Mount_top-level_subvolumes)
        *   [8.3.4 Utwórz zagnieżdżone subvolumes](#Utw.C3.B3rz_zagnie.C5.BCd.C5.BCone_subvolumes)
        *   [8.3.5 Zamontuj ESP](#Zamontuj_ESP)
    *   [8.4 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio_6)
        *   [8.4.1 Utwórz plik klucza](#Utw.C3.B3rz_plik_klucza)
        *   [8.4.2 Edycja mkinitcpio.conf](#Edycja_mkinitcpio.conf)
    *   [8.5 Konfigurowanie botladera](#Konfigurowanie_botladera)
    *   [8.6 Konfiguracja swap](#Konfiguracja_swap)

## Przegląd

Zabezpieczenie głównego systemu plików to miejsce, w którym *dm-crypt* wyróżnia się pod względem cech, wydajności i wydajności. W przeciwieństwie do selektywnego szyfrowania systemów plików użytkownika innego niż root, zaszyfrowany system plików root może ukrywać informacje, takie jak zainstalowane programy, nazwy użytkowników wszystkich kont i popularne wektory wycieku danych, takie jak [mlocate](/index.php/Mlocate "Mlocate") i `/var/log/`. Co więcej, zaszyfrowany system plików root sprawia, że manipulowanie systemem jest o wiele trudniejsze, ponieważ wszystko oprócz programu [boot loader](/index.php/Boot_loader "Boot loader") i jądra jest szyfrowane.

Wszystkie scenariusze zilustrowane poniżej dzielą te zalety, inne ich wady i zalety, które je różnicują:

| Scenariusze | Zalety | Wady |
| [#Prosty układ partycji z LUKS](#Prosty_uk.C5.82ad_partycji_z_LUKS)

pokazuje podstawową i prostą konfigurację dla w pełni zaszyfrowanego rootu LUKS.

 | 

*   Proste partycjonowanie i konfiguracja

 | 

*   Nieelastyczny; miejsce na dysku do zaszyfrowania musi zostać wstępnie przydzielone

 |
| [#LVM na LUKS](#LVM_na_LUKS)

osiąga elastyczność partycjonowania za pomocą LVM w pojedynczej zaszyfrowanej partycji LUKS.

 | 

*   Proste partycjonowanie ze znajomością LVM
*   Tylko jeden klucz wymagany do odblokowania wszystkich woluminów (np. Łatwe przywrócenie ustawień z dysku)
*   Układ woluminów nie jest przezroczysty po zablokowaniu
*   Najłatwiejsza metoda na to[suspension to disk](/index.php/Dm-crypt/Swap_encryption#With_suspend-to-disk_support "Dm-crypt/Swap encryption")

 | 

*   LVM dodaje dodatkową warstwę odwzorowania i hook
*   Mniej przydatne, jeśli pojedyncza objętość powinna otrzymać oddzielny klucz

 |
| [#LUKS na LVM](#LUKS_na_LVM)

używa dm-crypt tylko po skonfigurowaniu LVM.

 | 

*   LVM może służyć do przechowywania zaszyfrowanych woluminów na wielu dyskach
*   Łatwe połączenie nie-szyfrowanych grup woluminów

 | 

*   Złożony; Zmiana woluminów wymaga również zmiany mapperów szyfrowania
*   Woluminy wymagają indywidualnych kluczy
*   Układ LVM jest przezroczysty po zablokowaniu

 |
| [#LUKS na programowym RAID](#LUKS_na_programowym_RAID)

używa dm-crypt tylko po skonfigurowaniu RAID.

 | 

*   Analogiczny do LUKS na LVM

 | 

*   Analogiczny do LUKS na LVM

 |
| [#Zwykły dm-crypt](#Zwyk.C5.82y_dm-crypt)

używa trybu zwykłego dm-crypt, tj. bez nagłówka LUKS i jego opcji dla wielu kluczy.
W tym scenariuszu są również używane urządzenia USB `/boot` i pamięć kluczy, która może być zastosowana do innych scenariuszy.

 | 

*   Odporność danych dla przypadków, w których nagłówek LUKS może być uszkodzony
*   Pozwala [Full Disk Encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption")
*   Pomaga w rozwiązywaniu [problemów](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") z dyskami SSD

 | 

*   Dbałość o wszystkie parametry szyfrowania jest wymagana
*   Pojedynczy klucz szyfrowania i brak opcji zmiany

 |
| [#Szyfrowana partycja rozruchowa (GRUB)](#Szyfrowana_partycja_rozruchowa_.28GRUB.29)

pokazuje, jak zaszyfrować partycję rozruchową za pomocą programu ładującego GRUB.
W tym scenariuszu używana jest również partycja ESP, którą można zastosować do innych scenariuszy.

 | 

*   Te same korzyści, co scenariusz, na którym opiera się instalacja (LVM na LUKS dla tego konkretnego przykładu)
*   Mniej danych pozostaje niezaszyfrowanych, tzn. Program ładujący i partycja ESP, jeśli są obecne

 | 

*   Te same wady, co scenariusz, na którym opiera się instalacja (LVM na LUKS dla tego konkretnego przykładu)
*   Bardziej skomplikowana konfiguracja
*   Nie obsługiwane przez inne bootloadery

 |
| [#Btrfs subvolumes with swap](#Btrfs_subvolumes_with_swap)

pokazuje, jak zaszyfrować [Btrfs](/index.php/Btrfs "Btrfs") system, w tym `/boot` katalog, również dodając partycję do swap, na sprzęcie UEFI.

 | 

*   Podobne zalety jak [#Szyfrowana partycja rozruchowa (GRUB)](#Szyfrowana_partycja_rozruchowa_.28GRUB.29)
*   Dostępność funkcji Btrfs

 | 

*   Podobne wady jak [#Szyfrowana partycja rozruchowa (GRUB)](#Szyfrowana_partycja_rozruchowa_.28GRUB.29)

 |

Chociaż wszystkie powyższe scenariusze zapewniają o wiele większą ochronę przed zagrożeniami zewnętrznymi niż zaszyfrowane systemy plików wtórnych, mają również wspólną wadę: każdy użytkownik posiadający klucz szyfrujący jest w stanie odszyfrować cały dysk, a zatem może uzyskać dostęp do danych innych użytkowników. Jeśli jest to niepokojące, możliwe jest użycie kombinacji narzędzia blokowego i ułożonego w stos szyfrowania systemu plików i czerpania korzyści z obu. Zobacz [Disk encryption](/index.php/Disk_encryption "Disk encryption"), aby zaplanować z wyprzedzeniem.

Zobacz [Dm-crypt/Drive preparation#Partitioning](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation") ogólny przegląd strategii partycjonowania używanych w scenariuszach.

Innym obszarem, który należy rozważyć, jest skonfigurowanie zaszyfrowanej partycji wymiany i jakiego rodzaju. Zobacz [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") dla alternatywy.

Jeśli spodziewasz się chronić dane systemu nie tylko przed kradzieżą fizyczną, ale także przed koniecznością zabezpieczenia przed logicznym manipulowaniem, zobacz [Dm-crypt/Specialties#Securing the unencrypted boot partition](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties") dla dalszych możliwości po wykonaniu jednego ze scenariuszy.

**Warning:** W żadnym scenariuszu nigdy nie używaj oprogramowania do naprawy systemu plików, takiego jak fsck bezpośrednio na zaszyfrowanym woluminie, lub zniszczy wszelkie sposoby odzyskania klucza używanego do odszyfrowania plików Takie narzędzia muszą być używane zamiast odszyfrowanego (otwartego) urządzenia.

## Prosty układ partycji z LUKS

Ten przykład obejmuje pełne szyfrowanie systemu za pomocą "dmcrypt" + LUKS w prostym układzie partycji:

```
+--------------------+--------------------------+--------------------------+
|Boot partition      |LUKS encrypted system     |Optional free space       |
|                    |partition                 |for additional partitions |
|/dev/sdaY           |/dev/sdaX                 |or swap to be setup later |
+--------------------+--------------------------+--------------------------+

```

Pierwsze kroki można wykonać bezpośrednio po uruchomieniu obrazu instalacyjnego Arch Linux.

### Przygotowanie dysku

Przed utworzeniem jakichkolwiek partycji powinieneś wiedzieć o znaczeniu i metodach bezpiecznego usuwania dysku, opisanych w [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Następnie utwórz potrzebne partycje, przynajmniej jedną dla `/` (e.g. `/dev/sdaX`) i `/boot` (`/dev/sdaY`). Zobacz [Partitioning](/index.php/Partitioning "Partitioning").

### Preparing non-boot partitions

Następujące polecenia tworzą i montują zaszyfrowaną partycję root. Odpowiadają one procedurze opisanej szczegółowo w [Dm-crypt/Encrypting a non-root file system#Partition](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Partition "Dm-crypt/Encrypting a non-root file system") (which, despite the title, *can* be applied to root partitions, as long as [mkinitcpio](#Konfigurowanie_mkinitcpio) and the [boot loader](#Configuring_the_boot_loader) are correctly configured). If you want to use particular non-default encryption options (e.g. cipher, key length), see the [encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") before executing the first command:

(który, pomimo tytułu, może być zastosowany do partycji root, o ile mkinitcpio i program ładujący są poprawnie skonfigurowane). Jeśli chcesz użyć określonych, innych niż domyślne opcji szyfrowania (np. Szyfr, długość klucza), zobacz [opcje szyfrowania](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") przed wykonaniem pierwszego polecenia:

```
# cryptsetup -y -v luksFormat /dev/sdaX
# cryptsetup open /dev/sdaX cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Sprawdź, czy mapowanie działa zgodnie z przeznaczeniem:

```
# umount /mnt
# cryptsetup close cryptroot
# cryptsetup open /dev/sdaX cryptroot
# mount /dev/mapper/cryptroot /mnt

```

Jeśli utworzyłeś oddzielne partycje (e.g. `/home`), kroki te muszą zostać dostosowane i powtórzone dla nich wszystkich, z wyjątkiem `/boot`. Zobacz [Dm-crypt/Encrypting a non-root file system#Automated unlocking and mounting](/index.php/Dm-crypt/Encrypting_a_non-root_file_system#Automated_unlocking_and_mounting "Dm-crypt/Encrypting a non-root file system"), jak radzić sobie z dodatkowymi partycjami podczas startu.

Zauważ, że każde urządzenie blokowe wymaga własnego hasła. Może to być niewygodne, ponieważ skutkuje oddzielnym hasłem, które należy wprowadzić podczas rozruchu. Alternatywą jest użycie pliku klucza przechowywanego w partycji systemowej, aby odblokować oddzielną partycję za pośrednictwem `crypttab`. zobacz [Dm-crypt/Device encryption#Using LUKS to format partitions with a keyfile](/index.php/Dm-crypt/Device_encryption#Using_LUKS_to_format_partitions_with_a_keyfile "Dm-crypt/Device encryption") po instrukcje.

### Przygotowanie partycji rozruchowej

To, co musisz skonfigurować, to nieszyfrowana partycja rozruchowa, która jest potrzebna dla zaszyfrowanego katalogu głównego. Dla standardowej partycji MBR / non-EFI / boot, na przykład wykonaj:

```
# mkfs.ext4 /dev/sdaY
# mkdir /mnt/boot
# mount /dev/sdaY /mnt/boot

```

### Mounting the devices

At [Installation guide#Mount the file systems](/index.php/Installation_guide#Mount_the_file_systems "Installation guide") you will have to mount the mapped devices, not the actual partitions. Of course `/boot`, which is not encrypted, will still have to be mounted directly.

Afterwards continue with the installation procedure up to the mkinitcpio step.

W Przewodniku instalacji # Zainstaluj systemy plików, w których będziesz musiał zamontować odwzorowane urządzenia, a nie rzeczywiste partycje. Oczywiście / boot, który nie jest szyfrowany, będzie musiał być montowany bezpośrednio.

Następnie kontynuuj procedurę instalacji aż do kroku mkinitcpio.

### Konfigurowanie mkinitcpio

Dodaj `keyboard`, `keymap` i `encrypt` haki do [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). Jeśli domyślna mapa klawiszy US jest dla Ciebie w porządku, możesz pominąć `keymap` hak.

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** ... filesystems ...)` 

Depending on which other hooks are used, the order may be relevant. See [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Konfiguracja programu rozruchowego

Aby odblokować zaszyfrowaną partycję root przy starcie, program ładujący musi ustawić następujące parametry boot loadera:

```
cryptdevice=UUID=*<device-UUID>*:cryptroot root=/dev/mapper/cryptroot

```

Zobacz [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") po szczegóły..

The `*<device-UUID>*` refers to the UUID of `/dev/sdaX`. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

## LVM na LUKS

Prostą metodą jest ustawienie LVM na górze zaszyfrowanej partycji zamiast na odwrót. Technicznie LVM jest skonfigurowany w jednym dużym szyfrowanym systemie blokowym. W związku z tym LVM nie jest przezroczysta, dopóki urządzenie blokujące nie zostanie odblokowane, a podstawowa struktura woluminu zostanie odblokowana i zamontowana podczas rozruchu.

Układ dysku w tym przykładzie to:

```
+-----------------------------------------------------------------------+ +----------------+
| Logical volume1       | Logical volume2       | Logical volume3       | |                |
|/dev/mapper/MyVol-swap |/dev/mapper/MyVol-root |/dev/mapper/MyVol-home | | Boot partition |
|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _| | (may be on     |
|                                                                       | | other device)  |
|                        LUKS encrypted partition                       | |                |
|                          /dev/sdaX                                    | | /dev/sdbY      |
+-----------------------------------------------------------------------+ +----------------+

```

**Warning:** This method does not allow you to span the logical volumes over multiple disks easily; see [Dm-crypt/Specialties#Modifying the encrypt hook for multiple partitions](/index.php/Dm-crypt/Specialties#Modifying_the_encrypt_hook_for_multiple_partitions "Dm-crypt/Specialties").

**Tip:** Tdwa warianty tej konfiguracji:

*   Instrukcje na [dm-crypt/Specialties#Encrypted system using a detached LUKS header](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties") użyj tej konfiguracji z odłączonym nagłówkiem LUKS na urządzeniu USB, aby uzyskać z nim dwuetapowe uwierzytelnienie.
*   Instrukcje na [Pavel Kogan's blog](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/) pokaż, jak zaszyfrować `/boot` partycji, zachowując ją na głównej partycji LUKS podczas korzystania z GRUB-a.

### Przygotowanie dysku

Przed utworzeniem jakichkolwiek partycji powinieneś powinnaś wiedzieć o znaczeniu i metodach bezpiecznego usuwania dysku, opisanych w [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Korzystając z bootloadera [GRUB](/index.php/GRUB "GRUB") razem z [GPT](/index.php/GPT "GPT"), utwórz partycję rozruchową systemu BIOS, jak wyjaśniono w [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB").

Utwórz partycję do zamontowania w `/boot` typu `8300` o wielkości 100 MB lub większej.

Utwórz partycję typu `8E00`, która później będzie zawierała zaszyfrowany kontener.

Utwórz zaszyfrowany kontener LUKS na partycji "systemowej". Wprowadź dwukrotnie wybrane hasło.

```
# cryptsetup luksFormat /dev/*sdaX*

```

Aby uzyskać więcej informacji o dostępnych opcjach cryptsetup, zobacz [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") przed powyższym poleceniem.

Otwórz kontener:

```
# cryptsetup open /dev/*sdaX* cryptolvm

```

Odszyfrowany kontener jest teraz dostępny pod adresem `/dev/mapper/cryptolvm`.

### Przygotowywanie woluminów logicznych

Utwórz wolumin fizyczny na otwartym kontenerze LUKS:

```
# pvcreate /dev/mapper/cryptolvm

```

Utwórz nazwę grupy woluminów `MyVol` (lub cokolwiek chcesz), dodając do niego wcześniej utworzoną wolumin fizyczny:

```
# vgcreate MyVol /dev/mapper/cryptolvm

```

Utwórz wszystkie swoje woluminy logiczne w grupie woluminów:

```
# lvcreate -L 8G MyVol -n swap
# lvcreate -L 15G MyVol -n root
# lvcreate -l 100%FREE MyVol -n home

```

Sformatuj systemy plików na każdym woluminie logicznym:

```
# mkfs.ext4 /dev/mapper/MyVol-root
# mkfs.ext4 /dev/mapper/MyVol-home
# mkswap /dev/mapper/MyVol-swap

```

Zamontuj swoje systemy plików:

```
# mount /dev/mapper/MyVol-root /mnt
# mkdir /mnt/home
# mount /dev/mapper/MyVol-home /mnt/home
# swapon /dev/mapper/MyVol-swap

```

### Przygotowanie partycji rozruchowej

The bootloader loads the kernel, [initramfs](/index.php/Initramfs "Initramfs"), and its own configuration files from the `/boot` directory. This directory must be located on a separate unencrypted filesystem.

Program ładujący ładuje jądro, initramfs i własne pliki konfiguracyjne z katalogu `/boot`. Ten katalog musi znajdować się w oddzielnym niezaszyfrowanym systemie plików.

Utwórz system plików Ext2 na partycji przeznaczonej dla `/boot`. Dowolny system plików, który może odczytać bootloader, jest odpowiedni.

```
# mkfs.ext2 /dev/*sdbY*

```

Utwórz katalog `/mnt/boot`:

```
# mkdir /mnt/boot

```

Zamontuj partycję na `/mnt/boot`:

```
# mount /dev/*sdbY* /mnt/boot

```

Następnie kontynuuj procedurę instalacji aż do kroku `mkinitcpio`

### Konfigurowanie mkinitcpio

Dodaj `keyboard`, `encrypt` i `lvm2` haki do [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** **lvm2** ... filesystems ...)` 

Zobacz [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") dla szczegółów i innych haczyków, których możesz potrzebować.

### Konfigurowanie boot loadera

Aby odblokować zaszyfrowaną partycję root przy starcie, program ładujący musi ustawić następujący boot loadera:

```
cryptdevice=UUID=*device-UUID*:cryptolvm root=/dev/mapper/MyVol-root

```

The `*<device-UUID>*` refers to the UUID of `/dev/sdaX`. See [Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming") for details.

See [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") for details.

## LUKS na LVM

Aby użyć szyfrowania na [LVM](/index.php/LVM "LVM"), woluminy LVM są najpierw konfigurowane, a następnie wykorzystywane jako baza dla zaszyfrowanych partycji. W ten sposób możliwa jest również kombinacja zaszyfrowanych i nieszyfrowanych woluminów partycji.

**Tip:** Unlike [#LVM na LUKS](#LVM_na_LUKS), this method allows normally spanning the logical volumes over multiple disks.

Poniższy krótki przykład tworzy LUKS na instalacji LVM i miesza się w użyciu pliku klucza dla partycji / home i tymczasowych woluminów krypt dla / tmp i / swap. Ten ostatni jest uważany za pożądany z punktu widzenia bezpieczeństwa, ponieważ żadne potencjalnie wrażliwe dane tymczasowe nie przeżywają ponownego uruchomienia komputera, gdy szyfrowanie zostanie ponownie zainicjowane. Jeśli masz doświadczenie z LVM, będziesz mógł zignorować / zastąpić LVM i inne szczegóły zgodnie z twoim planem. Jeśli chcesz rozłożyć wolumin logiczny na wielu dyskach podczas konfiguracji, procedura do tego została opisana w [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

### Przygotowanie dysku

Schemat partycjonowania:

```
+----------------+-----------------------------------------------------------------------+
|                | LUKS encrypted volume | LUKS encrypted volume | LUKS encrypted volume |
|                | /dev/mapper/swap      | /dev/mapper/root      | /dev/mapper/home      |
|                |_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|
|                | Logical volume1       | Logical volume2       | Logical volume3       |
|                |/dev/mapper/MyVol-swap |/dev/mapper/MyVol-root |/dev/mapper/MyVol-home |
|                |_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|_ _ _ _ _ _ _ _ _ _ _ _|
| Boot partition |                                                                       |
|   /dev/sda1    |                               /dev/sda2                               |
+----------------+-----------------------------------------------------------------------+

```

Randomise `/dev/sda2` zgodnie z [Dm-crypt/Drive preparation#dm-crypt wipe on an empty disk or partition](/index.php/Dm-crypt/Drive_preparation#dm-crypt_wipe_on_an_empty_disk_or_partition "Dm-crypt/Drive preparation").

### Przygotowywanie woluminów logicznych

```
# pvcreate /dev/sda2
# vgcreate MyVol /dev/sda2
# lvcreate -L 10G -n lvroot MyVol
# lvcreate -L 500M -n swap MyVol
# lvcreate -L 500M -n tmp MyVol
# lvcreate -l 100%FREE -n home MyVol

```

```
# cryptsetup luksFormat -c aes-xts-plain64 -s 512 /dev/mapper/MyVol-lvroot
# cryptsetup open /dev/mapper/MyVol-lvroot root
# mkfs.ext4 /dev/mapper/root
# mount /dev/mapper/root /mnt

```

Więcej informacji o opcjach szyfrowania można znaleźć w [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption"). Zauważ, że `/home` zostanie zaszyfrowane [#Encrypting logical volume /home](#Encrypting_logical_volume_.2Fhome). Further, zauważ, że jeśli kiedykolwiek będziesz miał dostęp do zaszyfrowanego katalogu głównego z Arch-ISO, powyższe `open` akcja pozwoli ci po [Pojawia się LVM](/index.php/LVM#Logical_Volumes_do_not_show_up "LVM").

### Przygotowanie partycji rozruchowej

```
# dd if=/dev/zero of=/dev/sda1 bs=1M status=progress
# mkfs.ext4 /dev/sda1
# mkdir /mnt/boot
# mount /dev/sda1 /mnt/boot

```

Teraz po skonfigurowaniu zaszyfrowanego partycjonowania LVM nadszedł czas na instalację: [Arch Install Scripts](/index.php/Installation_guide#Mount_the_file_systems "Installation guide").

### Konfigurowanie mkinitcpio

Dodaj `keyboard`, `lvm2` i `encrypt` haki do [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **lvm2** **encrypt** ... filesystems ...)` 

Zobacz [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") po szczegóły i inne haki, które mogą być potrzebne.

### konfiguracjae boot loadera

Aby odblokować zaszyfrowaną partycję root przy starcie, program ładujący musi ustawić następujące parametry boot loadera :

```
cryptdevice=/dev/mapper/MyVol-lvroot:root root=/dev/mapper/root

```

Zobacz [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") po szczegóły.

### Konfigurowanie fstab i crypttab

 `/etc/fstab` 
```
/dev/mapper/root        /       ext4            defaults        0       1
/dev/sda1               /boot   ext4            defaults        0       2
/dev/mapper/tmp         /tmp    tmpfs           defaults        0       0
/dev/mapper/swap        none    swap            sw              0       0

```

The following crypttab options will re-encrypt the temporary filesystems each reboot:

Następujące opcje [crypttab](/index.php/Crypttab "Crypttab") ponownie zaszyfrują tymczasowe pliki przy każdym ponownym uruchomieniu komputera:

 `/etc/crypttab` 
```
swap	/dev/mapper/MyVol-swap	/dev/urandom	swap,cipher=aes-xts-plain64,size=256
tmp	/dev/mapper/MyVol-tmp	/dev/urandom	tmp,cipher=aes-xts-plain64,size=256

```

### Szyfrowanie woluminu logicznego /home

Since this scenario uses LVM as the primary and dm-crypt as secondary mapper, each encrypted logical volume requires its own encryption. Yet, unlike the temporary filesystems configured with volatile encryption above, the logical volume for `/home` should be persistent, of course. The following assumes you have rebooted into the installed system, otherwise you have to adjust paths. To safe on entering a second passphrase at boot for it, a [keyfile](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") is created:

Ponieważ ten scenariusz używa LVM jako podstawowej i dm-crypt jako programu odwzorowującego wtórnego, każdy zaszyfrowany wolumin logiczny wymaga własnego szyfrowania. Jednak, inaczej niż w przypadku tymczasowych systemów plików skonfigurowanych powyżej z użyciem szyfrowania ulotnego, wolumin logiczny dla `/home` powinien być oczywiście stały. Poniższe założenie zakłada ponowne uruchomienie systemu, w przeciwnym razie trzeba dostosować ścieżki. Aby zabezpieczyć się przed wprowadzeniem drugiego hasła podczas uruchamiania, tworzony jest plik [klucza](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption"):

```
# mkdir -m 700 /etc/luks-keys
# dd if=/dev/random of=/etc/luks-keys/home bs=1 count=256 status=progress

```

Wolumin logiczny jest zaszyfrowany:

```
# cryptsetup luksFormat -v -s 512 /dev/mapper/MyVol-home /etc/luks-keys/home
# cryptsetup -d /etc/luks-keys/home open /dev/mapper/MyVol-home home
# mkfs.ext4 /dev/mapper/home
# mount /dev/mapper/home /home

```

The encrypted mount is configured in [crypttab](/index.php/Crypttab "Crypttab"):

 `/etc/crypttab` 
```
home	/dev/mapper/MyVol-home   /etc/luks-keys/home

```
 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

i konfiguracja jest zakończona.

Jeśli chcesz rozszerzyć wolumin logiczny dla `/home` (lub dowolnego innego woluminu) w późniejszym czasie, ważne jest, aby pamiętać, że część zaszyfrowana LUKS musi również zostać zmieniona. Aby zobaczyć procedurę, patrz [Dm-crypt/Specialties#Expanding LVM on multiple disks](/index.php/Dm-crypt/Specialties#Expanding_LVM_on_multiple_disks "Dm-crypt/Specialties").

## LUKS na programowym RAID

Ten przykład jest oparty na konfiguracji dla laptopa wyposażonego w dwa dyski SSD o jednakowej wielkości oraz dodatkowy dysk twardy dla pamięci masowej. Efektem końcowym jest oparte na LUKS pełne szyfrowanie dysku (w tym `/boot`) dla wszystkich dysków, z dyskami SSD w macierzy RAID0 i pliki kluczy używane do odblokowania całego szyfrowania po podaniu GRUB poprawnego hasła przy starcie. Obsługa formatów TRIM jest włączona na dyskach SSD, ale warto zapoznać się ze szczegółowymi informacjami na temat bezpieczeństwa [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties") przed rozważeniem skorzystania z tego.

This setup utilizes a very simplistic partitioning scheme, with all the available RAID storage being mounted at `/` (no separate `/boot` partition), and the decrypted HDD being mounted at `/mnt/data`. It is also worth mentioning that the system in this example boots in BIOS mode and the drives are partitioned with [GPT](/index.php/Partitioning "Partitioning") partitions.

Ta konfiguracja wykorzystuje bardzo uproszczony schemat partycjonowania, przy czym wszystkie dostępne pamięci RAID są montowane w / (brak oddzielnej partycji rozruchowej), a odszyfrowany dysk HDD jest montowany w {ic|/mnt/data}}. Warto również wspomnieć, że system w tym przykładzie uruchamia się w trybie BIOS, a dyski są partycjonowane przy użyciu partycji GPT.

Należy pamiętać, że regularne kopie zapasowe są bardzo ważne w tej konfiguracji. Jeśli którakolwiek z dysków SSD ulegnie awarii, dane zawarte w macierzy RAID będą praktycznie niemożliwe do odzyskania. Możesz wybrać inny poziom RAID, jeśli twoja odporność na uszkodzenia jest dla ciebie ważna.

W tej konfiguracji szyfrowanie nie jest zaprzeczeniem.

W celu wykonania poniższych instrukcji stosuje się następujące urządzenia blokowe:

```
/dev/sda = first SSD
/dev/sdb = second SSD
/dev/sdc = HDD

```

Pamiętaj, aby zastąpić je odpowiednimi oznaczeniami urządzeń do konfiguracji, ponieważ mogą się one różnić.

### Przygotowanie dysku

Przed utworzeniem jakichkolwiek partycji powinieneś powinnaś wiedzieć o znaczeniu i metodach bezpiecznego usuwania dysku, opisanych w [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Korzystając z bootloadera GRUB razem z GPT, utwórz partycję rozruchową systemu BIOS, jak wyjaśniono w systemach GRUB # BIOS. W przypadku tej konfiguracji obejmuje to partycję 1M dla "rozruchu BIOS" w `/dev/sda1`, a pozostałe miejsce na dysku jest podzielone na partycje dla "Linux RAID" w `/dev/sda2`.

Po utworzeniu partycji na `/dev/sda`, można użyć następujących komend do sklonowania ich do `/dev/sdb`.

```
# sfdisk -d /dev/sda > sda.dump
# sfdisk /dev/sdb < sda.dump

```

Dysk twardy jest przygotowywany z pojedynczą partycją Linuksa obejmującą cały dysk w `/dev/sdc1`.

### Budowanie macierzy RAID

Utwórz macierz RAID dla dysków SSD. Ten przykład wykorzystuje RAID 0, możesz chcieć wykorzystać inny poziom w oparciu o twoje preferencje lub wymagania.

```
# mdadm --create --verbose --level=0 --metadata=1.2 --raid-devices=2 /dev/md0 /dev/sda2 /dev/sdb2

```

### Przygotowanie urządzeń blokowych

Jak wyjaśniono w przygotowaniu [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"), dyski są wymazywane losowymi danymi z wykorzystaniem `/dev/zero` oraz kryptograficznym z losowym kluczem. Alternatywnie możesz użyć `dd` z `/dev/random` lub `/dev/urandom`, ale będzie to znacznie wolniejsze

```
# cryptsetup open --type plain /dev/md0 container --key-file /dev/random
# dd if=/dev/zero of=/dev/mapper/container bs=1M status=progress
# cryptsetup close container

```

I powtórz powyższe na HDD (`/dev/sdc1` w tym przykładzie).

Skonfiguruj szyfrowanie dla `/dev/md0`:

```
# cryptsetup -y -v luksFormat -c aes-xts-plain64 -s 512 /dev/md0
# cryptsetup open /dev/md0 cryptroot
# mkfs.ext4 /dev/mapper/cryptroot
# mount /dev/mapper/cryptroot /mnt

```

I powtórz dla HDD:

```
# cryptsetup -y -v luksFormat -c aes-xts-plain64 -s 512 /dev/sdc1
# cryptsetup open /dev/sdc1 cryptdata
# mkfs.ext4 /dev/mapper/cryptdata
# mkdir -p /mnt/mnt/data
# mount /dev/mapper/cryptdata /mnt/mnt/data

```

### Konfiguracja boot loadera

Skonfiguruj GRUB dla zaszyfrowanego systemu, edytując plik `/etc/defaults/grub`, wykonując następujące czynności. Zauważ, że opcja: `:allow-discards` umożliwia obsługę TRIM na SSD, jeśli nie chcesz jej używać, powinieneś to pominąć.

```
GRUB_CMDLINE_LINUX="cryptdevice=/dev/md0:cryptroot:allow-discards root=/dev/mapper/cryptroot"
GRUB_ENABLE_CRYPTODISK=y

```

Zobacz [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") i [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB") po szczegółowe informacje.

Dokończ instalację GRUB na obu dyskach SSD (w rzeczywistości instalacja będzie działać tylko na `/dev/sda`).

```
# grub-install --target=i386-pc /dev/sda
# grub-install --target=i386-pc /dev/sdb
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Tworzenie plików kluczy

Kolejne kroki nie pozwalają na dwukrotne wpisanie hasła podczas startu systemu (raz GRUB może odblokować szyfrowanie, a drugi raz, gdy initramfs przejmuje kontrolę nad systemem). Odbywa się to poprzez utworzenie pliku klucza do szyfrowania i dodanie go do obrazu initramfs, aby umożliwić szyfrowanie haka, aby odblokować urządzenie root. zobacz [dm-crypt/Device encryption#With a keyfile embedded in the initramfs](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") po szczegółowe informacje.

*   Utwórz plik [klucza](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") i dodaj klucz do `/dev/md0`.

*   Utwórz kolejny plik kluczy dla dysku twardego ((`/dev/sdc1`), aby można go było odblokować podczas rozruchu. Dla wygody pozostaw powyższe hasło w miejscu, ponieważ może to ułatwić odzyskiwanie, jeśli kiedykolwiek będziesz tego potrzebować. Edytuj `/etc/crypttab`, aby odszyfrować dysk twardy podczas startu. Zobacz [dm-crypt/Device encryption#Unlocking a secondary partition at boot](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

### Konfigurowanie systemu

Edytuj [/etc/fstab](/index.php/Fstab "Fstab"), aby zamontować urządzenia blokujące cryptroot i cryptdata; jeśli nie włączasz obsługi TRIM, usuń opcję montowania:

```
/dev/mapper/cryptroot  /           ext4    rw,noatime,discard  0   1 
/dev/mapper/cryptdata  /mnt/data   ext4    defaults            0   2  

```

Zapisz konfigurację RAID:

```
# mdadm --detail --scan > /etc/mdadm.conf 

```

Edytuj plik [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"), aby dołączyć swój plik kluczy i dodaj odpowiednie haki:

```
FILES=(/crypto_keyfile.bin)
HOOKS=( ... **keyboard** **keymap** block **mdadm_udev** **encrypt** filesystems ... )

```

Zobacz [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") po szczegóły

## Zwykły dm-crypt

W przeciwieństwie do LUKS, tryb zwykły dm-crypt nie wymaga nagłówka na zaszyfrowanym urządzeniu: ten scenariusz wykorzystuje tę funkcję do ustawienia systemu na niepodzielonym na partycje, zaszyfrowanym dysku, który będzie nieodróżnialny od dysku wypełnionego losowymi danymi, co może pozwolić na [deniable encryption](https://en.wikipedia.org/wiki/Deniable_encryption "wikipedia:Deniable encryption"). Zobacz też [wikipedia:Disk encryption#Full disk encryption](https://en.wikipedia.org/wiki/Disk_encryption#Full_disk_encryption "wikipedia:Disk encryption").

Zauważ, że jeśli szyfrowanie całego dysku nie jest wymagane, metody korzystające z LUKS opisane w powyższych sekcjach są lepszymi opcjami zarówno dla szyfrowania systemowego, jak i zaszyfrowanych partycji. Funkcje LUKS takie jak zarządzanie kluczami z wieloma hasłami / plikami kluczy lub ponowne szyfrowanie urządzenia w miejscu są niedostępne w trybie zwykłym.

*Plain* dm-crypt encryption can be more resilient to damage than LUKS, because it does not rely on an encryption master-key which can be a single-point of failure if damaged.

Zwykłe szyfrowanie dm-crypt może być bardziej odporne na uszkodzenia niż LUKS, ponieważ nie opiera się na kluczu szyfrującym, który może być pojedynczym punktem awarii, jeśli jest uszkodzony. Jednak użycie trybu zwykłego wymaga również ręcznej konfiguracji opcji szyfrowania, aby uzyskać taką samą siłę kryptograficzną. Zobacz też [Disk encryption#Cryptographic metadata](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption"). Stosując tryb "zwykły" można również rozważyć, jeśli chodzi o problemy wyjaśnione w [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties").

**Tip:** Jeśli twoim celem jest szyfrowanie bez nagłówka, ale nie masz pewności co do braku wyprowadzania klucza w trybie "zwykłym", to dwie alternatywy to:

*   [tcplay](/index.php/Tcplay "Tcplay"), który oferuje szyfrowanie bez nagłówków, ale z funkcją PBKDF2, lub
*   tryb dm-crypt LUKS z odłączonym nagłówkiem za pomocą "cryptsetup" `--header` opcja. Nie można go używać ze standardowym hakiem "szyfruj", ale hakiem [may be modified](/index.php/Dm-crypt/Specialties#Encrypted_system_using_a_detached_LUKS_header "Dm-crypt/Specialties").

Scenariusz wykorzystujący dwie pamięci USB:

*   jeden dla urządzenia rozruchowego, który pozwala również na przechowywanie opcji wymaganych do otwarcia / odblokowania zwykłego szyfrowanego urządzenia w konfiguracji modułu ładującego, ponieważ wpisanie ich na każdym rozruchu byłoby podatne na błędy;
*   drugi dla pliku kluczy szyfrujących, zakładając, że jest przechowywany jako nieprzetworzone bity, aby w oczach nieświadomego napastnika, który mógłby uzyskać klucz usb, klucz szyfrowania pojawi się jako dane losowe, zamiast być widocznym jako normalny plik. Zobacz też [Wikipedia:Security through obscurity](https://en.wikipedia.org/wiki/Security_through_obscurity "wikipedia:Security through obscurity"), follow [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") to prepare the keyfile.

Układ dysku to:

```
+--------------------+------------------+--------------------+ +---------------+ +---------------+
|Volume 1:           |Volume 2:         |Volume 3:           | |Boot device    | |Encryption key |
|                    |                  |                    | |               | |file storage   |
|root                |swap              |home                | |/boot          | |(unpartitioned |
|                    |                  |                    | |               | |in example)    |
|/dev/store/root     |/dev/store/swap   |/dev/store/home     | |/dev/sdY1      | |/dev/sdZ       |
|--------------------+------------------+--------------------| |---------------| |---------------|
|disk drive /dev/sdaX encrypted using plain mode and LVM     | |USB stick 1    | |USB stick 2    |
+------------------------------------------------------------+ +---------------+ +---------------+

```

**Tip:**

*   Możliwe jest również użycie pojedynczego klucza usb poprzez bezpośrednie skopiowanie pliku klucza do initram. Przykładowy plik kluczy `/etc/keyfile` zostanie skopiowany do obrazu initram przez ustawienie `FILES=(/etc/keyfile)` w `/etc/mkinitcpio.conf`. Sposób instruowania `encrypt` do odczytu pliku klucza w obrazie initram `rootfs:` prefiks przed nazwą pliku, np. `cryptkey=rootfs:/etc/keyfile`.
*   inną opcją jest użycie hasła z dobrom [entropią](/index.php/Disk_encryption#Choosing_a_strong_passphrase "Disk encryption").

### Przygotowanie dysku

Ważne jest, aby zamapowane urządzenie było wypełnione danymi. W szczególności dotyczy to zastosowania scenariusza, które stosujemy tutaj. Zobacz [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation") i [Dm-crypt/Drive preparation#dm-crypt specific methods](/index.php/Dm-crypt/Drive_preparation#dm-crypt_specific_methods "Dm-crypt/Drive preparation")

### Przygotowywanie partycji, które nie są uruchomione

Zobacz [Dm-crypt/Device encryption#Encryption options for plain mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_plain_mode "Dm-crypt/Device encryption") szczegółowe informacje.

Korzystanie z urządzenia `/dev/sd*X*`, z szyfrem twofish-xts z 512-bitowym rozmiarem klucza i przy użyciu pliku klucza mamy następujące opcje dla tego scenariusza:

 `# cryptsetup --hash=sha512 --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sd*Z* --key-size=512 open --type=plain /dev/sdX enc` 

W przeciwieństwie do szyfrowania za pomocą LUKS, powyższe polecenie musi być wykonane "w całości" za każdym razem, gdy konieczne jest ponowne ustanowienie mapowania, dlatego ważne jest, aby pamiętać szczegóły szyfrowania, hasza i pliku klucza.

Możemy teraz sprawdzić, czy wpis mapowania został wprowadzony `/dev/mapper/enc`:

```
# fdisk -l

```

Następnie ustawiamy woluminy logiczne [LVM](/index.php/LVM "LVM") na zmapowanym urządzeniu. Zobacz[LVM#Installing Arch Linux on LVM](/index.php/LVM#Installing_Arch_Linux_on_LVM "LVM") po dalsze szczegóły:

```
# pvcreate /dev/mapper/enc
# vgcreate store /dev/mapper/enc
# lvcreate -L 20G store -n root
# lvcreate -L 10G store -n swap
# lvcreate -l 100%FREE store -n home

```

Formatujemy i montujemy je oraz aktywujemy partycję swap zobacz [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") po dalsze szczegóły:

```
# mkfs.ext4 /dev/store/root
# mkfs.ext4 /dev/store/home
# mount /dev/store/root /mnt
# mkdir /mnt/home
# mount /dev/store/home /mnt/home
# mkswap /dev/store/swap
# swapon /dev/store/swap

```

### Przygotowanie partycji rozruchowej

The `/boot` partition can be installed on the standard vfat partition of a USB stick, if required. But if manual partitioning is needed, then a small 200MB partition is all that is required. Create the partition using a [partitioning tool](/index.php/Partitioning#Partitioning_tools "Partitioning") of your choice.

Partycję `/boot` można zainstalować na standardowej partycji vfat USB-Stick, jeśli jest taka potrzeba. Ale jeśli potrzebne jest ręczne partycjonowanie, wystarczy mała partycja 200 MB. Utwórz partycję za pomocą wybranego [narzędzia do partycjonowania.](/index.php/Partitioning#Partitioning_tools "Partitioning")

Wybieramy system plików, który nie jest zapisywany w dzienniku, aby zachować pamięć flash partycji `/boot`, jeśli nie została jeszcze sformatowana jako vfat:

```
# mkfs.ext2 /dev/sd*Y*1
# mkdir /mnt/boot
# mount /dev/sd*Y*1 /mnt/boot

```

### Konfigurowanie mkinitcpio

Dodaj `keyboard`, `encrypt` i `lvm2` haki do [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** **lvm2** ... filesystems ...)` 

Zobacz [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") do dalszych szczegółów i innych haczyków, które możesz potrzebować.

### Konfiguracja bootloadera

Aby uruchomić zaszyfrowaną partycję root, botlader musi ustawić następujące parametry jądra:

```
cryptdevice=/dev/sd*X*:enc cryptkey=/dev/sd*Z*:0:512 crypto=sha512:twofish-xts-plain64:512:0:

```

**Note:** Jeśli używasz sd-encrypt zamiast szyfrowania, użyj odpowiednio opcji określonych w ' systemd-cryptsetup-generator(8)*.*

Zobacz [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") po dalsze szczegóły i inne parametry, których możesz potrzebować.

**Tip:** Jeśli używasz GRUB-a, możesz zainstalować go na tym samym USB co partycję `/boot`:
```
# grub-install --recheck /dev/sd*Y*

```

### Po instalacji

Możesz chcieć usunąć pendrive USB po uruchomieniu. Ponieważ partycja `/boot` zazwyczaj nie jest potrzebna, opcja noauto może zostać dodana do odpowiedniej linii w `/etc/fstab`:

 `/etc/fstab` 
```
# /dev/sd*Yn*
/dev/sd*Yn* /boot ext2 **noauto**,rw,noatime 0 2

```

Jednakże, gdy wymagana jest aktualizacja jądra lub programu ładującego, partycja `/boot` musi być obecna i zamontowana. Ponieważ pozycja w `fstab` już istnieje, można ją zamontować po prostu za pomocą:

```
# mount /boot

```

## Szyfrowana partycja rozruchowa (GRUB)

Ta konfiguracja wykorzystuje ten sam układ i konfigurację partycji dla partycji głównej systemu, co poprzednia sekcja #[#LVM na LUKS](#LVM_na_LUKS), z dwiema wyraźnymi różnicami:

1.  Konfiguracja jest przeprowadzana dla systemu [UEFI](/index.php/UEFI "UEFI") i
2.  Specjalna funkcja programu bodladera GRUB służy do dodatkowego szyfrowania partycji rozruchowej `/boot`. Zobacz też [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB").

Układ dysku w tym przykładzie to:

```
+---------------+----------------+----------------+----------------+----------------+
|ESP partition: |Boot partition: |Volume 1:       |Volume 2:       |Volume 3:       |
|               |                |                |                |                |
|/boot/efi      |/boot           |root            |swap            |home            |
|               |                |                |                |                |
|               |                |/dev/store/root |/dev/store/swap |/dev/store/home |
|/dev/sdaX      |/dev/sdaY       +----------------+----------------+----------------+
|**un**encrypted    |LUKS encrypted  |/dev/sdaZ encrypted using LVM on LUKS             |
+---------------+----------------+--------------------------------------------------+

```

**Tip:** Wszystkie scenariusze mają służyć jako przykłady. Możliwe jest oczywiście zastosowanie obu powyższych dwóch etapów instalacji również w innych scenariuszach. Zobacz także warianty połączone w [#LVM na LUKS](#LVM_na_LUKS).

**Note:** You can use `cryptboot` script from [cryptboot](https://aur.archlinux.org/packages/cryptboot/) package for simplified encrypted boot management (mounting, unmounting, upgrading packages) and as a defense against [Evil Maid](https://www.schneier.com/blog/archives/2009/10/evil_maid_attac.html) attacks with [UEFI Secure Boot](/index.php/Secure_Boot#Using_your_own_keys "Secure Boot"). For more informations and limitations see [cryptboot project](https://github.com/xmikos/cryptboot) page.

### Przygotowanie dysku

Przed utworzeniem jakichkolwiek partycji powinieneś powinnaś wiedzieć o znaczeniu metod bezpiecznego usuwania dysku, opisanych w [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation").

Utwórz [partycję systemową EFI](/index.php?title=Partycj%C4%99_systemow%C4%85_EFI&action=edit&redlink=1 "Partycję systemową EFI (page does not exist)") o odpowiednim rozmiarze, później zostanie zamontowana w `/boot/efi`.

Utwórz partycję do zamontowania w `/boot` typu `8300` o wielkości 100 MB lub więcej.

**Tip:** When using the [GRUB](/index.php/GRUB "GRUB") bootloader together with a BIOS/[GPT](/index.php/GPT "GPT"), create a BIOS Boot Partition as explained in [GRUB#BIOS systems](/index.php/GRUB#BIOS_systems "GRUB") instead of the ESP.

Utwórz partycję typu `8E00`, który później będzie zawierał zaszyfrowany kontener.

Utwórz zaszyfrowany kontener LUKS na partycji "systemowej".

```
# cryptsetup luksFormat /dev/*sdaZ*

```

Aby uzyskać więcej informacji o dostępnych opcjach cryptsetup, zobacz [LUKS encryption options](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") przed powyższym poleceniem.

Twój układ partycji powinien wyglądać podobnie do tego:

 `# gdisk /dev/sda` 
```
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI System
   2         1050624         1460223   200.0 MiB   8300  Linux filesystem
   3         1460224        41943006   19.3 GiB    8E00  Linux LVM

```

Otwórz kontener:

```
# cryptsetup open /dev/*sdaZ* lvm

```

Odszyfrowany kontener jest teraz dostępny pod adresem `/dev/mapper/lvm`.

### Przygotowywanie woluminów logicznych

Woluminy logiczne LVM tego przykładu są zgodne z dokładnym układem w poprzednim scenariuszu. Dlatego prosimy postępować zgodnie z instrukcjami [Preparing the logical volumes](#Preparing_the_logical_volumes) lub dostosuj je według potrzeb.

### Przygotowanie partycji rozruchowej

Program ładujący ładuje jądro [initramfs](/index.php/Initramfs "Initramfs"), i jego własne pliki konfiguracyjne z katalogu `/boot` directory.

Najpierw utwórz kontener LUKS, w którym będą znajdować się i instalowane pliki:

```
# cryptsetup luksFormat /dev/sda*Y*

```

Następnie otwórz:

```
# cryptsetup open /dev/sda*Y* cryptboot

```

Utwórz system plików na partycji przeznaczonej dla `/boot`. Dowolny system plików, który może odczytać bootloader, jest odpowiedni:

```
# mkfs.ext2 /dev/mapper/*cryptboot*

```

Utwórz katalog `/mnt/boot`:

```
# mkdir /mnt/boot

```

Zamontuj partycję na `/mnt/boot`:

```
# mount /dev/mapper/*cryptboot* /mnt/boot

```

Utwórz punkt montowania dla [EFI system partition](/index.php/EFI_system_partition "EFI system partition") w `/boot/efi` w celu zapewnienia zgodności z `grub-install` i zamontuj:

```
# mkdir /mnt/boot/efi
# mount /dev/*sdaX* /mnt/boot/efi

```

W tym momencie powinieneś mieć następujące partycje i woluminy logiczne wewnątrz `/mnt`

 `$ lsblk` 
```
NAME              	  MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINT
sda                       8:0      0   200G  0 disk
├─sda1                    8:1      0   512M  0 part  /boot/efi
├─sda2                    8:2      0   200M  0 part
│ └─boot		  254:0    0   198M  0 crypt /boot
└─sda3                    8:3      0   100G  0 part
  └─lvm                   254:1    0   100G  0 crypt
    ├─MyStorage-swapvol   254:2    0     8G  0 lvm   [SWAP]
    ├─MyStorage-rootvol   254:3    0    15G  0 lvm   /
    └─MyStorage-homevol   254:4    0    77G  0 lvm   /home

```

Następnie kontynuuj procedurę instalacji aż do kroku mkinitcpio.

### Konfigurowanie mkinitcpio

Dodaj `keyboard`, `encrypt` i `lvm2` haki do [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"):

 `/etc/mkinitcpio.conf`  `HOOKS=(... **keyboard** **keymap** block **encrypt** **lvm2** ... filesystems ...)` 

Zobacz [dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") for details and other hooks that you may need.

### Konfiguracja botladera

Skonfiguruj GRUB, aby rozpoznał zaszyfrowaną partycję `/boot` LUKS i odblokuj zaszyfrowaną partycję root przy starcie:

 `/etc/default/grub` 
```
GRUB_CMDLINE_LINUX="... cryptdevice=UUID=*<device-UUID>*:lvm ..."
GRUB_ENABLE_CRYPTODISK=y
```

Zobacz [Dm-crypt/System configuration#Boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") i [GRUB#Boot partition](/index.php/GRUB#Boot_partition "GRUB") do dalszych szczegółów. `*<device-UUID>*` odnosi się do UUID z `/dev/sdaZ` (partycja przechowująca lvm zawierający główny system plików). Zobacz[Persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming").

Wygeneruj plik [konfiguracyjny](/index.php/GRUB#Generate_the_main_configuration_file "GRUB") GRUB i [zainstaluj](/index.php/GRUB#Installation_2 "GRUB") na zamontowanym ESP:

```
# grub-mkconfig -o /boot/grub/grub.cfg
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=grub --recheck

```

Jeśli zakończy się to bezbłędnie, GRUB powinien poprosić o hasło, aby odblokować partycję `/boot` po następnym uruchomieniu.

### Konfigurowanie fstab i crypttab

Ta sekcja opisuje dodatkową konfigurację pozwalającą systemowi **zamontować** zaszyfrowane `/boot`

Podczas gdy GRUB prosi o hasło, aby odblokować zaszyfrowane `/boot` po powyższych instrukcjach odblokowanie partycji nie jest przekazywane do initramfs. Stąd, `/boot` nie będzie dostępne po ponownym uruchomieniu systemu, ponieważ `encrypt` hook tylko odblokowuje root systemu.

Jeśli używałeś skryptu "genfstab" podczas instalacji, zostanie wygenerowany `/etc/fstab` wpisy dla `/boot` i `/boot/efi` montuj punkty już, ale system nie odnajdzie device mapper dla partycji rozruchowej. Aby go udostępnić, dodaj go do [crypttab](/index.php/Crypttab "Crypttab"). Na przykład:

 `/etc/crypttab` 
```
cryptboot  /dev/sdaY      none        luks

```

sprawi, że system ponownie poprosi o podanie hasła (to znaczy, że musisz wprowadzić je dwukrotnie przy starcie systemu: raz dla GRUB i raz dla systemd init). Aby uniknąć podwójnego wpisu dotyczącego odblokowania `/boot`, postępuj zgodnie z instrukcjami na stronie [Dm-crypt/Device encryption#Keyfiles](/index.php/Dm-crypt/Device_encryption#Keyfiles "Dm-crypt/Device encryption") do:

1.  Stwórz [randomtext keyfile](/index.php/Dm-crypt/Device_encryption#Storing_the_keyfile_on_a_filesystem "Dm-crypt/Device encryption"),
2.  Dodaj plik klucza do pliku (`/dev/sdaY`) [boot partition's LUKS header](/index.php/Dm-crypt/Device_encryption#Configuring_LUKS_to_make_use_of_the_keyfile "Dm-crypt/Device encryption") and
3.  Sprawdź wpis `/etc/fstab` i dodaj linię `/etc/crypttab` do [unlock it automatically at boot](/index.php/Dm-crypt/Device_encryption#Unlocking_a_secondary_partition_at_boot "Dm-crypt/Device encryption").

Jeśli z jakiegoś powodu plik klucza nie odblokuje partycji rozruchowej, systemd zrestartuje się, aby poprosić o hasło do odblokowania, a jeśli jest to poprawne, kontynuuj uruchamianie.

**Tip:** Opcjonalne kroki poinstalacyjne:

*   Warto rozważyć dodanie programu ładującego GRUB do listy ignorowanych plików `/etc/pacman.conf` w celu uzyskania szczególnej kontroli, kiedy bootloader (który zawiera własne moduły szyfrujące) jest aktualizowany.
*   Jeśli chcesz zaszyfrować partycję `/boot`, aby zabezpieczyć się przed zagrożeniami związanymi z nieuprawnionym dostępem, pomoc dla [mkinitcpio-chkcryptoboot](/index.php/Dm-crypt/Specialties#mkinitcpio-chkcryptoboot "Dm-crypt/Specialties")

## Btrfs subvolumes with swap

Poniższy przykład tworzy pełne szyfrowanie systemowe za pomocą LUKS przy użyciu subwoluminów [Btrfs](/index.php/Btrfs "Btrfs") do [simulate partitions](/index.php/Btrfs#Mounting_subvolumes "Btrfs").

Jeśli używasz UEFI, to [EFI system partition](/index.php/EFI_system_partition "EFI system partition") (ESP) jest wymagane. `/boot` może znajdować się na `/` i być zaszyfrowane; jednak samo ESP nie może być zaszyfrowane. W tym przykładowym układzie ESP jest `/dev/sda*Y*` i jest zamontowany w `/boot/efi`. `/boot` sama znajduje się na partycji systemowej, `/dev/sda*X*`.

Ponieważ `/boot` znajduje się na zaszyfrowanej `/`, [GRUB](/index.php/GRUB "GRUB") musi być użyty jako bootloader, ponieważ tylko GRUB może załadować moduły niezbędne do odszyfrowania `/boot` (e.g., crypto.mod, cryptodisk.mod and luks.mod) [[1]](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/).

Dodatkowo wyświetlana jest opcjonalna zwykła, zaszyfrowana partycja [swap](/index.php/Swap "Swap").

**Warning:** Nie używaj [swap file](/index.php/Swap_file "Swap file") zamiast osobnej partycji, ponieważ może to spowodować utratę danych. zobacz [Btrfs#Swap file](/index.php/Btrfs#Swap_file "Btrfs").

```
+--------------------------+--------------------------+--------------------------+
|ESP                       |System partition          |Swap partition            |
|**un**encrypted               |LUKS-encrypted            |plain-encrypted           |
|                          |                          |                          |
|/boot/efi                 |/                         |                          |
|/dev/sda*Y*                 |/dev/sda*X*                 |/dev/sda*Z*                 |
|--------------------------+--------------------------+--------------------------+

```

### Przygotowanie dysku

**Note:** Nie można używać partycji btrfs, jak opisano w [Btrfs#Partitionless Btrfs disk](/index.php/Btrfs#Partitionless_Btrfs_disk "Btrfs") podczas korzystania z LUKS. Należy użyć tradycyjnego partycjonowania, nawet jeśli jest to po prostu utworzenie jednej partycji.

Przed utworzeniem jakichkolwiek partycji powinieneś wiedzieć o znaczeniu i metodach bezpiecznego usuwania dysku, opisanych w [Dm-crypt/Drive preparation](/index.php/Dm-crypt/Drive_preparation "Dm-crypt/Drive preparation"). Jeśli używasz [UEFI](/index.php/UEFI "UEFI") stworzyć [EFI system partition](/index.php/EFI_system_partition "EFI system partition") o odpowiednim rozmiarze. Zostanie on później zamontowany w `/boot/efi`. Jeśli masz zamiar utworzyć zaszyfrowaną partycję wymiany, utwórz dla niej partycję, ale nie oznaczaj jej jako "swap", ponieważ z partycją będzie używana zwykły "dm-crypt".

Utwórz potrzebne partycje, przynajmniej jedną dla `/` (e.g. `/dev/sda*X*`). zobacz [Partitioning](/index.php/Partitioning "Partitioning") article.

### Przygotowanie partycji systemowej

#### Utwórz kontener LUKS

Śledzić [dm-crypt/Device encryption#Encrypting devices with LUKS mode](/index.php/Dm-crypt/Device_encryption#Encrypting_devices_with_LUKS_mode "Dm-crypt/Device encryption") ustawić `/dev/sda*X*` dla LUKS. Zobacz [Dm-crypt/Device encryption#Encryption options for LUKS mode](/index.php/Dm-crypt/Device_encryption#Encryption_options_for_LUKS_mode "Dm-crypt/Device encryption") zanim to zrobisz, aby wyświetlić listę opcji szyfrowania.

#### Odblokuj kontener LUKS

Teraz wykonaj [Dm-crypt/Device encryption#Unlocking/Mapping LUKS partitions with the device mapper](/index.php/Dm-crypt/Device_encryption#Unlocking.2FMapping_LUKS_partitions_with_the_device_mapper "Dm-crypt/Device encryption") aby odblokować kontener LUKS i zmapować go.

#### Sformatuj zmapowane urządzenie

Przejdź do sformatowania zmapowanego urządzenia zgodnie z opisem w [Btrfs#File system on a single device](/index.php/Btrfs#File_system_on_a_single_device "Btrfs"), gdzie `*/dev/partition*`jest nazwą zmapowanego urządzenia (tj., `cryptroot`) i **not** `/dev/sda*X*`.

#### Zamontuj zmapowane urządzenie

W końcu, [mount](/index.php/Mount "Mount") teraz sformatowane urządzenie mapowane (tzn. `/dev/mapper/cryptroot`) do `/mnt`.

**Tip:** Możesz chcieć użyć `compress=lzo` opcja montowania. zobacz [Btrfs#Compression](/index.php/Btrfs#Compression "Btrfs") po więcej informacji.

### Tworzenie subwoluminów btrfs

#### Układ

[Subvolumes](/index.php/Btrfs#Subvolumes "Btrfs") będą używane do symulacji partycji, ale będą również tworzone inne (zagnieżdżone) podwiliny. Oto częściowa reprezentacja tego, co wygeneruje następujący przykład:

```
subvolid=5 (/dev/sda*X*)
   |
   ├── @ (mounted as /)
   |       |
   |       ├── /bin (directory)
   |       |
   |       ├── /home (mounted @home subvolume)
   |       |
   |       ├── /usr (directory)
   |       |
   |       ├── /.snapshots (mounted @snapshots subvolume)
   |       |
   |       ├── /var/cache/pacman/pkg (nested subvolume)
   |       |
   |       ├── ... (other directories and nested subvolumes)
   |
   ├── @snapshots (mounted as /.snapshots)
   |
   ├── @home (mounted as /home)
   |
   └── @... (additional subvolumes you wish to use as mount points)

```

Ta sekcja jest zgodna z [Snapper#Suggested filesystem layout](/index.php/Snapper#Suggested_filesystem_layout "Snapper"), który jest najbardziej przydatny w połączeniu z [Snapper](/index.php/Snapper "Snapper"). Powinieneś także skonsultować się [Btrfs Wiki SysadminGuide#Layout](https://btrfs.wiki.kernel.org/index.php/SysadminGuide#Layout).

#### Create top-level subvolumes

Tutaj używamy konwencji prefiksowania `@` do subwolumowania nazw, które będą używane jako punkty montowania, oraz `@` będzie subvolume, które jest zamontowane jako `/`.

Śledząc [Btrfs#Creating a subvolume](/index.php/Btrfs#Creating_a_subvolume "Btrfs") artykuł, utwórz subvolumes w `/mnt/@`, `/mnt/@snapshots`, i `/mnt/@home`.

Utwórz teraz wszystkie dodatkowe subvolumes, które chcesz teraz wykorzystać jako punkty podłączenia.

#### Mount top-level subvolumes

Odmontuj partycję systemową na `/mnt`.

Teraz zamontuj nowo utworzony `@` subvolume, które będzie służyć jako `/` do `/mnt` używając `subvol=` opcje montowania. Zakładając, że zmapowane urządzenie ma nazwę `cryptroot`, polecenie wyglądałoby jak:

```
# mount -o compress=lzo,subvol=@ /dev/mapper/cryptroot /mnt

```

Zobacz [Btrfs#Mounting subvolumes](/index.php/Btrfs#Mounting_subvolumes "Btrfs") for more details.

Zamontuj także inne subvolumes do odpowiednich punktów montowania `@home` do `/mnt/home` i `@snapshots` do `/mnt/.snapshots`.

#### Utwórz zagnieżdżone subvolumes

utwórz dowolne subvolumes, których **nie** chcesz mieć podczas robienia migawki `/`. Na przykład prawdopodobnie nie chcesz robić migawek `/var/cache/pacman/pkg`. Te podwilumny będą zagnieżdżone pod `@` subvolume, ale równie łatwo mogłoby zostać stworzone wcześniej na tym samym poziomie co `@` zgodnie z własnymi preferencjami.

ponieważ `@` subvolume jest zamontowany w `/mnt` będziesz musiał [create a subvolume](/index.php/Create_a_subvolume "Create a subvolume") w `/mnt/var/cache/pacman/pkg` dla tego przykładu. Może być konieczne najpierw utworzenie katalogów macierzystych.

Inne katalogi, z którymi możesz to zrobić, to `/var/abs`, `/var/tmp`, i `/srv`.

#### Zamontuj ESP

Jeśli wcześniej przygotowano partycję systemową EFI, utwórz jej punkt podłączenia i zamontuj go teraz.

**Note:** Btrfs snapshots wykluczą `/boot/efi`, ponieważ nie jest to system plików btrfs.

Na etapie [[Installation guide#Install Pacstrap, [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) musi być zainstalowany jako dodatek do grupy podstawowej.

### Konfigurowanie mkinitcpio

#### Utwórz plik klucza

Aby GRUB otworzył partycję LUKS bez konieczności dwukrotnego wpisywania hasła przez użytkownika, użyjemy pliku klucza osadzonego w initramfs. Śledzić [Dm-crypt/Device encryption#With a keyfile embedded in the initramfsupewnij](/index.php/Dm-crypt/Device_encryption#With_a_keyfile_embedded_in_the_initramfs "Dm-crypt/Device encryption") się, że dodasz klucz `/dev/sda*X*` na *luksAddKey* step.

#### Edycja mkinitcpio.conf

Po utworzeniu, dodaniu i osadzeniu klucza, jak opisano powyżej, dodaj `encrypt` hak do [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf") jak również wszelkie inne haki, których potrzebujesz. Zobacz [Dm-crypt/System configuration#mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration") dla szczegółowych informacji. Pamiętaj, aby zregenerować początkowy RAMdysk po zakończeniu.

**Tip:** Możesz dodać `BINARIES=(/usr/bin/btrfs)` dla Twojej `mkinitcpio.conf`. Zobacz [Btrfs#Corruption recovery](/index.php/Btrfs#Corruption_recovery "Btrfs") article.

### Konfigurowanie botladera

Zaistaluj [GRUB](/index.php/GRUB "GRUB") do `/dev/sda`. Następnie edytuj `/etc/default/grub` zgodnie z instrukcją [GRUB#Encryption](/index.php/GRUB#Encryption "GRUB") artykułu, zgodnie z instrukcjami dla zaszyfrowanego katalogu głównego i partycji rozruchowej. Na koniec wygeneruj plik konfiguracyjny GRUB.

### Konfiguracja swap

Jeśli utworzyłeś partycję, która ma być używana do szyfrowanej wymiany, teraz jest czas na jej skonfigurowanie. Postępuj zgodnie z instrukcjami na [Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

Po wykonaniu tego kroku kontynuuj konfigurację systemu zgodnie z ustawieniami [installation guide](/index.php/Installation_guide#Reboot "Installation guide").