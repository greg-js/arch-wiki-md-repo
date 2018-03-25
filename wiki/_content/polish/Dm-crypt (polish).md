Z projektu cryptsetup [wiki](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt):

	Device-mapper to infrastruktura jądra Linux 2.6 i 3.x, która zapewnia ogólny sposób tworzenia wirtualnych warstw urządzeń blokowych. Cel kryptografu Device-mapper zapewnia transparentne szyfrowanie urządzeń blokowych za pomocą interfejsu API kryptograficznego jądra. Użytkownik może zasadniczo określić jeden z szyfrów symetrycznych, tryb szyfrowania, klucz (o dowolnym dozwolonym rozmiarze), tryb generowania iv, a następnie użytkownik może utworzyć nowe urządzenie blokowe w / dev. Zapis do tego urządzenia będzie szyfrowany i odszyfrowywany. Możesz zamontować na nim swój system plików lub zawiesić urządzenie dm-crypt innym urządzeniem, takim jak wolumen RAID lub LVM. Podstawowa dokumentacja tabeli mapowania dm-crypt pochodzi ze źródła jądra, a najnowsza wersja jest dostępna w repozytorium git.

## Contents

*   [1 Typowy scenariuszs](#Typowy_scenariuszs)
*   [2 Drive preparation](#Drive_preparation)
*   [3 Szyfrowanie urządzenia](#Szyfrowanie_urz.C4.85dzenia)
*   [4 Konfiguracja systemu](#Konfiguracja_systemu)
*   [5 szyfrowanie partycji swap](#szyfrowanie_partycji_swap)
*   [6 Specialties](#Specialties)
*   [7 Zobacz też](#Zobacz_te.C5.BC)

## Typowy scenariuszs

W tej części przedstawiono powszechne scenariusze zastosowania "dm-crypt" do szyfrowania systemu lub poszczególnych punktów instalacji systemu plików. Jest to punkt wyjścia do zapoznania się z różnymi praktycznymi procedurami szyfrowania. W razie potrzeby scenariusze łączą się z innymi podstronami.

Zobacz [Dm-crypt/Encrypting a non-root file system (Polski)](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Polski) "Dm-crypt/Encrypting a non-root file system (Polski)") jeśli chcesz zaszyfrować urządzenie, które nie jest używane do uruchamiania systemu, takie jak [partycja](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Polski)#Partycja "Dm-crypt/Encrypting a non-root file system (Polski)") lub [loop device](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Polski)#Loop_device "Dm-crypt/Encrypting a non-root file system (Polski)").

Zobacz [Dm-crypt/Encrypting an entire system (Polski)](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski) "Dm-crypt/Encrypting an entire system (Polski)") jeśli chcesz zaszyfrować cały system, w szczególności partycję root. Uwzględniono kilka scenariuszy, w tym wykorzystanie "dm-crypt" z rozszerzeniem "LUKS", szyfrowanie i szyfrowanie w trybie "zwykłym" oraz "LVM".

## Drive preparation

[Dm-crypt/Drive preparation (Polski)](/index.php/Dm-crypt/Drive_preparation_(Polski) "Dm-crypt/Drive preparation (Polski)") dotyczy operacji takich jak [Dm-crypt/Drive preparation (Polski)#Bezpieczne usuwanie danych z dysku twardego](/index.php/Dm-crypt/Drive_preparation_(Polski)#Bezpieczne_usuwanie_danych_z_dysku_twardego "Dm-crypt/Drive preparation (Polski)") i *dm-crypt* specyficzne punkty do jego [partycjonowania](/index.php/Dm-crypt/Drive_preparation#Partitioning "Dm-crypt/Drive preparation").

## Szyfrowanie urządzenia

[Dm-crypt/Device encryption (Polski)](/index.php/Dm-crypt/Device_encryption_(Polski) "Dm-crypt/Device encryption (Polski)") obejmuje sposób ręcznego wykorzystania dm-crypt do szyfrowania systemu za pomocą komendy [cryptsetup](/index.php/Dm-crypt/Device_encryption#Cryptsetup_usage "Dm-crypt/Device encryption"). Obejmuje przykłady [opcji szyfrowania z dm-crypt,](/index.php/Dm-crypt/Device_encryption#Encryption_options_with_dm-crypt "Dm-crypt/Device encryption") zajmuje się tworzeniem [plików kluczy](/index.php/Dm-crypt/Device_encryption#Key_management "Dm-crypt/Device encryption"), poleceń LUKS dotyczących zarządzania kluczami oraz tworzenia [kopii zapasowych i przywracania](/index.php/Dm-crypt/Device_encryption#Backup_and_restore "Dm-crypt/Device encryption").

## Konfiguracja systemu

[Dm-crypt/System configuration](/index.php/Dm-crypt/System_configuration "Dm-crypt/System configuration") ilustruje, jak skonfigurować [mkinitcpio](/index.php/Dm-crypt/System_configuration#mkinitcpio "Dm-crypt/System configuration"), [boot loader](/index.php/Dm-crypt/System_configuration#Boot_loader "Dm-crypt/System configuration") i [crypttab](/index.php/Crypttab "Crypttab") plik podczas szyfrowania systemu.

## szyfrowanie partycji swap

[Dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption") obejmuje sposób dodania partycji wymiany do systemu szyfrowanego, jeśli jest to wymagane. Partycja wymiany musi być również zaszyfrowana, aby chronić dane wymieniane przez system. Ta część opisuje metody [without](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#Without_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") i [with](/index.php/Dm-crypt_with_LUKS/Swap_Encryption#With_suspend-to-disk_support "Dm-crypt with LUKS/Swap Encryption") suspend-to-disk support.

## Specialties

[Dm-crypt/Specialties](/index.php/Dm-crypt/Specialties "Dm-crypt/Specialties") zajmuje się operacjami specjalnymi, [zabezpieczenie niezaszyfrowanej partycji rozruchowej](/index.php/Dm-crypt/Specialties#Securing_the_unencrypted_boot_partition "Dm-crypt/Specialties"), [przy użyciu zaszyfrowanych plików kluczy GPG lub OpenSSL](/index.php/Dm-crypt/Specialties#Using_GPG.2C_LUKS.2C_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties"), metoda [uruchamiania i odblokowywania za pośrednictwem sieci](/index.php/Dm-crypt/Specialties#Remote_unlocking_of_the_root_.28or_other.29_partition "Dm-crypt/Specialties"), inna dla [konfiguracja discard/TRIM dla SSD](/index.php/Dm-crypt/Specialties#Discard.2FTRIM_support_for_solid_state_drives_.28SSD.29 "Dm-crypt/Specialties"), i sekcje dotyczące [Szyfrowanie hook i wiele dysków](/index.php/Dm-crypt/Specialties#The_encrypt_hook_and_multiple_disks "Dm-crypt/Specialties").

## Zobacz też

*   [dm-crypt](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) - The project homepage
*   [cryptsetup](https://gitlab.com/cryptsetup/cryptsetup) - The LUKS homepage and [FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions) - the main and foremost help resource.
*   [cryptsetup repository](https://git.kernel.org/cgit/utils/cryptsetup/cryptsetup.git/) and [release](https://www.kernel.org/pub/linux/utils/cryptsetup/) archive.
*   [DOXBOX](https://github.com/t-d-k/doxbox) - Supports unlocking LUKS encrypted volumes in Microsoft Windows.