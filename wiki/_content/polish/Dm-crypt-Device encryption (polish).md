W tej sekcji opisano sposób ręcznego wykorzystania *dm-crypt* z linii poleceń w celu zaszyfrowania systemu.

## Contents

*   [1 Przygotowanie](#Przygotowanie)
*   [2 Wykorzystanie Cryptsetup](#Wykorzystanie_Cryptsetup)
    *   [2.1 Hasła i klucze programu Cryptsetup](#Has.C5.82a_i_klucze_programu_Cryptsetup)
*   [3 Opcje szyfrowania z dm-crypt](#Opcje_szyfrowania_z_dm-crypt)
    *   [3.1 Opcje szyfrowania dla trybu LUKS](#Opcje_szyfrowania_dla_trybu_LUKS)
    *   [3.2 Opcje szyfrowania dla trybu zwykłego](#Opcje_szyfrowania_dla_trybu_zwyk.C5.82ego)
*   [4 Szyfrowanie urządzeń za pomocą cryptsetup](#Szyfrowanie_urz.C4.85dze.C5.84_za_pomoc.C4.85_cryptsetup)
    *   [4.1 Szyfrowanie urządzeń w trybie LUKS](#Szyfrowanie_urz.C4.85dze.C5.84_w_trybie_LUKS)
        *   [4.1.1 Formatowanie partycji LUKS](#Formatowanie_partycji_LUKS)
            *   [4.1.1.1 Używanie LUKS do formatowania partycji za pomocą pliku kluczy](#U.C5.BCywanie_LUKS_do_formatowania_partycji_za_pomoc.C4.85_pliku_kluczy)
        *   [4.1.2 Odblokowywanie / mapowanie partycji LUKS za pomocą device mapper](#Odblokowywanie_.2F_mapowanie_partycji_LUKS_za_pomoc.C4.85_device_mapper)
    *   [4.2 Szyfrowanie urządzeń w trybie zwykłym](#Szyfrowanie_urz.C4.85dze.C5.84_w_trybie_zwyk.C5.82ym)
*   [5 Działania Cryptsetup specyficzne dla LUKS](#Dzia.C5.82ania_Cryptsetup_specyficzne_dla_LUKS)
    *   [5.1 Zarządzanie kluczami](#Zarz.C4.85dzanie_kluczami)
        *   [5.1.1 Dodawanie kluczy LUKS](#Dodawanie_kluczy_LUKS)
        *   [5.1.2 Usuwanie kluczy LUKS](#Usuwanie_kluczy_LUKS)
    *   [5.2 Kopia zapasowa i przywracanie](#Kopia_zapasowa_i_przywracanie)
        *   [5.2.1 Kopia zapasowa za pomocą cryptsetup](#Kopia_zapasowa_za_pomoc.C4.85_cryptsetup)
        *   [5.2.2 Przywracanie za pomocą cryptsetup](#Przywracanie_za_pomoc.C4.85_cryptsetup)
        *   [5.2.3 Ręczne tworzenie kopii zapasowych i przywracanie](#R.C4.99czne_tworzenie_kopii_zapasowych_i_przywracanie)
    *   [5.3 Ponowne szyfrowanie urządzeń](#Ponowne_szyfrowanie_urz.C4.85dze.C5.84)
        *   [5.3.1 Zaszyfruj niezaszyfrowany system plików](#Zaszyfruj_niezaszyfrowany_system_plik.C3.B3w)
        *   [5.3.2 Ponowne szyfrowanie istniejącej partycji LUKS](#Ponowne_szyfrowanie_istniej.C4.85cej_partycji_LUKS)
*   [6 Zmiana rozmiaru zaszyfrowanych urządzeń](#Zmiana_rozmiaru_zaszyfrowanych_urz.C4.85dze.C5.84)
    *   [6.1 Loopback filesystem](#Loopback_filesystem)
*   [7 Pliki kluczy](#Pliki_kluczy)
    *   [7.1 Rodzaje plików kluczy](#Rodzaje_plik.C3.B3w_kluczy)
        *   [7.1.1 hasło](#has.C5.82o)
        *   [7.1.2 randomtext](#randomtext)
        *   [7.1.3 binary](#binary)
    *   [7.2 Tworzenie pliku kluczy z losowymi znakami](#Tworzenie_pliku_kluczy_z_losowymi_znakami)
        *   [7.2.1 Przechowywanie pliku klucza w systemie plików](#Przechowywanie_pliku_klucza_w_systemie_plik.C3.B3w)
            *   [7.2.1.1 Bezpieczne nadpisywanie zapisanych plików kluczy](#Bezpieczne_nadpisywanie_zapisanych_plik.C3.B3w_kluczy)
        *   [7.2.2 Przechowywanie pliku kluczy w ramfs](#Przechowywanie_pliku_kluczy_w_ramfs)
    *   [7.3 Konfigurowanie LUKS do korzystania z pliku klucza](#Konfigurowanie_LUKS_do_korzystania_z_pliku_klucza)
    *   [7.4 Ręczne odblokowywanie partycji przy użyciu pliku klucza](#R.C4.99czne_odblokowywanie_partycji_przy_u.C5.BCyciu_pliku_klucza)
    *   [7.5 Odblokowywanie dodatkowej partycji podczas rozruchu](#Odblokowywanie_dodatkowej_partycji_podczas_rozruchu)
    *   [7.6 Odblokowywanie partycji głównej podczas rozruchu](#Odblokowywanie_partycji_g.C5.82.C3.B3wnej_podczas_rozruchu)
        *   [7.6.1 Z plikiem kluczy przechowywanym na zewnętrznym nośniku](#Z_plikiem_kluczy_przechowywanym_na_zewn.C4.99trznym_no.C5.9Bniku)
            *   [7.6.1.1 Konfigurowanie mkinitcpio](#Konfigurowanie_mkinitcpio)
            *   [7.6.1.2 Konfigurowanie parametrów jądra](#Konfigurowanie_parametr.C3.B3w_j.C4.85dra)
        *   [7.6.2 Z plikiem kluczy osadzonym w initramfs](#Z_plikiem_kluczy_osadzonym_w_initramfs)

## Przygotowanie

Przed użyciem [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup), zawsze upewnij się, że `dm_crypt` [kernel module](/index.php/Kernel_module "Kernel module") jest załadowany.

## Wykorzystanie Cryptsetup

Cryptsetup to narzędzie linii poleceń służące do komunikacji z *dm-crypt* w celu tworzenia, uzyskiwania dostępu i zarządzania zaszyfrowanymi urządzeniami. Narzędzie zostało później rozszerzone, aby obsługiwać różne typy szyfrowania, które opierają się na narzędziu do mapowania jądra systemu Linux i modułach kryptograficznych. Najbardziej znaczącym rozszerzeniem było rozszerzenie Linux Unified Key Setup (LUKS), które przechowuje wszystkie potrzebne informacje dotyczące instalacji dla dm-crypt na samym dysku i streszcza zarządzanie partycjami i kluczami w celu poprawy łatwości użytkowania. Urządzenia dostępne za pośrednictwem urządzenia odwzorowującego urządzenia nazywane są urządzeniami blokowymi. W celu uzyskania dalszych informacji zobacz [Disk encryption#Block device encryption](/index.php/Disk_encryption#Block_device_encryption "Disk encryption").

Narzędzie jest używane w następujący sposób:

```
# cryptsetup <OPTIONS> <action> <action-specific-options> <device> <dmname>

```

Ma skompilowane ustawienia domyślne dla opcji i trybu szyfrowania, które będą używane, jeśli w wierszu poleceń nie określono żadnych innych. Spójrz na

```
$ cryptsetup --help 

```

który wyświetla opcje, akcje i domyślne parametry trybów szyfrowania w tej kolejności. Pełną listę opcji można znaleźć na stronie podręcznika. Ponieważ różne parametry są wymagane lub opcjonalne, w zależności od trybu szyfrowania i działania, poniższe sekcje wskazują dalej różnice. Szyfrowanie Blockdevice jest szybkie, ale szybkość też ma duże znaczenie. Ponieważ zmiana szyfru urządzenia blokowego po konfiguracji jest trudna, ważne jest wcześniejsze sprawdzenie wydajności dm-crypt dla poszczególnych parametrów:

```
$ cryptsetup benchmark 

```

może podać wskazówki dotyczące wyboru algorytmu i klucza przed instalacją. Jeśli niektóre szyfry AES przodują ze znacznie większą przepustowością, to prawdopodobnie jest sprzętową obsługą CPU.

**Tip:** Podczas uczenia możesz chcieć ćwiczyć szyfrowanie wirtualnego dysku twardego na [maszynie wirtualnej](/index.php/Virtual_machine "Virtual machine").

### Hasła i klucze programu Cryptsetup

Szyfrowane urządzenie blokowe jest chronione kluczem. Klucz jest albo:

*   hasło: patrz [Security#Passwords](/index.php/Security#Passwords "Security").
*   plik klucza, patrz [#Keyfiles](#Keyfiles).

Oba typy kluczy mają domyślne maksymalne rozmiary: hasła mogą zawierać do 512 znaków, a pliki kluczy do 8192 kiB.

Ważnym rozróżnieniem LUKS na uwagę w tym momencie jest to, że klucz jest używany do odblokowania klucza głównego urządzenia zaszyfrowanego LUKS i może być zmieniony przy dostępie root. Inne tryby szyfrowania nie obsługują zmiany klucza po konfiguracji, ponieważ nie używają klucza głównego do szyfrowania. Zobacz [Disk encryption#Block device encryption](/index.php/Disk_encryption#Block_device_encryption "Disk encryption") po dalsze szczegóły.

## Opcje szyfrowania z dm-crypt

*Cryptsetup* obsługuje różne tryby operacyjne szyfrowania do użycia z *dm-crypt*. Najczęstszym (i domyślnym) jest

*   `--type luks`

Pozostałe są

*   `--type plain` do używania w trybie zwykłym dm-crypt,
*   `--type loopaes` dla loopaes tryb Legacy, i
*   `--type tcrypt` dla [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") tryb zgodności.

Podstawowe opcje kryptograficzne dla szyfrów i skrótów są dostępne dla wszystkich trybów i polegają na kryptograficznych funkcjach jądra. Wszystkie ładowane w czasie wykonywania można wyświetlać za pomocą

```
$ less /proc/crypto 

```

i są dostępne do użycia jako opcje. Jeśli lista jest krótka, należy wykonać test porównawczy `cryptsetup benchmark`, który uruchomi ładowanie dostępnych modułów.

Poniżej przedstawiono opcje szyfrowania dla dwóch pierwszych trybów. Zwróć uwagę, że tabele zawierają opcje używane w odpowiednich przykładach w tym artykule, a nie wszystkie dostępne.

### Opcje szyfrowania dla trybu LUKS

*cryptsetup* służąca do skonfigurowania nowego urządzenia dm-crypt w trybie szyfrowania LUKS to luksFormat. W przeciwieństwie do nazwy oznacza to, że nie formatuje urządzenia, ale ustawia nagłówek urządzenia LUKS i szyfruje klucz główny z żądanymi opcjami kryptograficznymi.

Ponieważ LUKS jest domyślnym trybem szyfrowania,

```
# cryptsetup -v luksFormat *device*

```

to wszystko, czego potrzeba, aby stworzyć nowe urządzenie LUKS z domyślnymi parametrami ((`-v` jest opcjonalne). Dla porównania możemy ręcznie określić domyślne opcje:

```
# cryptsetup -v --cipher aes-xts-plain64 --key-size 256 --hash sha256 --iter-time 2000 --use-urandom --verify-passphrase luksFormat *device*

```

Wartości domyślne są porównywane z przykładem kryptograficznie wyższego opisu w poniższej tabeli wraz z towarzyszącymi komentarzami:

| Opcje | Domyślne ustawienia Cryptsetup 1.7.0 | Przykład | Komentarz |
| --cipher

-c

 | `aes-xts-plain64` | `aes-xts-plain64` | [Release 1.6.0](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.6/v1.6.0-ReleaseNotes) changed the defaults to an AES [cipher](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") in [XTS](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory") mode (see item 5.16 [of the FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)). It is advised against using the previous default `--cipher aes-cbc-essiv` because of its known [issues](https://en.wikipedia.org/wiki/Disk_encryption_theory#Cipher-block_chaining_.28CBC.29 "wikipedia:Disk encryption theory") and practical [attacks](http://www.jakoblell.com/blog/2013/12/22/practical-malleability-attack-against-cbc-encrypted-luks-partitions/) against them. |
| --key-size

-s

 | `256` | `512` | By default a 256 bit key-size is used. Note however that [XTS splits the supplied key in half](https://en.wikipedia.org/wiki/Disk_encryption_theory#XEX-based_tweaked-codebook_mode_with_ciphertext_stealing_.28XTS.29 "wikipedia:Disk encryption theory"), so to use AES-256 instead of AES-128 you have to set the XTS key-size to `512`. |
| --hash

-h

 | `sha256` | `sha512` | Hash algorithm used for [key derivation](/index.php/Disk_encryption#Cryptographic_metadata "Disk encryption"). Release 1.7.0 changed defaults from `sha1` to `sha256` "*not for security reasons [but] mainly to prevent compatibility problems on hardened systems where SHA1 is already [being] phased out*"[[1]](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.7/v1.7.0-ReleaseNotes). The former default of `sha1` can still be used for compatibility with older versions of *cryptsetup* since it is [considered secure](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) (see item 5.20). |
| --iter-time

-i

 | `2000` | `5000` | Number of milliseconds to spend with PBKDF2 passphrase processing. Release 1.7.0 changed defaults from `1000` to `2000` to "*try to keep PBKDF2 iteration count still high enough and also still acceptable for users.*"[[2]](https://www.kernel.org/pub/linux/utils/cryptsetup/v1.7/v1.7.0-ReleaseNotes). This option is only relevant for LUKS operations that set or change passphrases, such as *luksFormat* or *luksAddKey*. Specifying 0 as parameter selects the compiled-in default.. |
| --use-{u,}random | `--use-urandom` | `--use-random` | Selects which [random number generator](/index.php/Random_number_generator "Random number generator") to use. Quoting the cryptsetup manual page: "In a low-entropy situation (e.g. in an embedded system), both selections are problematic. Using /dev/urandom can lead to weak keys. Using /dev/random can block a long time, potentially forever, if not enough entropy can be harvested by the kernel." |
| --verify-passphrase

-y

 | Yes | - | Default only for luksFormat and luksAddKey. No need to type for Arch Linux with LUKS mode at the moment. |

Jeśli chcesz zagłębić się w funkcje kryptograficzne LUKS, to [LUKS specification](https://gitlab.com/cryptsetup/cryptsetup/wikis/Specification) (na przykład jego dodatki) jest zasobem.

**Tip:** Przewiduje się, że nagłówek LUKS otrzyma kolejną ważną wersję w odpowiednim czasie. Jeśli jesteś zainteresowany planami, twórcy' [devconfcz2016](https://mbroz.fedorapeople.org/talks/DevConf2016/devconf2016-luks2.pdf) (pdf) prezentacja podsumowuje.

### Opcje szyfrowania dla trybu zwykłego

W trybie zwykłym dm-crypt na urządzeniu nie ma klucza głównego, dlatego nie ma potrzeby konfigurowania go. Zamiast tego opcje szyfrowania, które należy zastosować, są używane bezpośrednio do utworzenia odwzorowania między zaszyfrowanym dyskiem a nazwanym urządzeniem. Mapowanie można utworzyć na partycji lub na pełnym urządzeniu. W tym drugim przypadku nie jest wymagana nawet tablica partycji.

Aby utworzyć mapowanie w trybie zwykłym z domyślnymi parametrami cryptsetup:

```
# cryptsetup <options> open --type plain <device> <dmname>

```

Wykonanie go spowoduje podanie hasła, które powinno mieć bardzo wysoką entropię. Poniżej porównanie domyślnych parametrów z przykładem w [dm-crypt/Encrypting an entire system_(Polski)#Zwykły dm-crypt](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Zwyk.C5.82y_dm-crypt "Dm-crypt/Encrypting an entire system (Polski)")

| Option | Cryptsetup 1.7.0 defaults | Example | Comment |
| --hash

-h

 | `ripemd160` | - | The hash is used to create the key from the passphrase; it is not used on a keyfile. |
| --cipher

-c

 | `aes-cbc-essiv:sha256` | `twofish-xts-plain64` | The cipher consists of three parts: cipher-chainmode-IV generator. Please see [Disk encryption#Ciphers and modes of operation](/index.php/Disk_encryption#Ciphers_and_modes_of_operation "Disk encryption") for an explanation of these settings, and the [DMCrypt documentation](https://gitlab.com/cryptsetup/cryptsetup/wikis/DMCrypt) for some of the options available. |
| --key-size

-s

 | `256` | `512` | The key size (in bits). The size will depend on the cipher being used and also the chainmode in use. Xts mode requires twice the key size of cbc. |
| --offset

-o

 | `0` | `0` | The offset from the beginning of the target disk (in bytes) from which to start the mapping |
| --key-file

-d

 | default uses a passphrase | `/dev/sd*Z*` (or e.g. `/boot/keyfile.enc`) | The device or file to be used as a key. See [#Keyfiles](#Keyfiles) for further details. |
| --keyfile-offset | `0` | `0` | Offset from the beginning of the file where the key starts (in bytes). This option is supported from *cryptsetup* 1.6.7 onwards. |
| --keyfile-size

-l

 | `8192kB` | - (default applies) | Limits the bytes read from the key file. This option is supported from *cryptsetup* 1.6.7 onwards. |

Używając urządzenia `/dev/sd*X*`, powyższy przykład z prawej kolumny daje:

```
# cryptsetup --cipher=twofish-xts-plain64 --offset=0 --key-file=/dev/sd*Z* --key-size=512 open --type=plain /dev/sdX enc

```

W przeciwieństwie do szyfrowania za pomocą LUKS, powyższe polecenie musi być wykonane w pełni za każdym razem, gdy konieczne jest ponowne ustanowienie mapowania, dlatego ważne jest, aby pamiętać szczegóły szyfrowania, hasza i pliku klucza. Możemy teraz sprawdzić, czy mapowanie zostało wykonane:

```
# fdisk -l

```

Wpis powinien już istnieć `/dev/mapper/enc`.

## Szyfrowanie urządzeń za pomocą cryptsetup

W tej sekcji pokazano, jak wykorzystać opcje tworzenia nowych zaszyfrowanych urządzeń blokowych i uzyskiwania dostępu do nich ręcznie.

**Warning:** GRUB does not support LUKS2 headers. Therefore, if you plan to [unlock an encrypted boot partition with GRUB](/index.php/GRUB#Boot_partition "GRUB"), do not specify `luks2` for the type parameter on encrypted boot partitions.

### Szyfrowanie urządzeń w trybie LUKS

#### Formatowanie partycji LUKS

Aby ustawić partycję jako zaszyfrowaną partycję LUKS wykonaj:

```
# cryptsetup luksFormat --type luks2 *device*

```

Zostaniesz poproszony o podanie hasła i jego weryfikację.

Zobacz [#Encryption options for LUKS mode](#Encryption_options_for_LUKS_mode) dla opcji wiersza poleceń.

Możesz sprawdzić wyniki za pomocą:

```
# cryptsetup luksDump *device*

```

Zauważysz, że stos nie tylko pokazuje informacje nagłówka szyfrowania, ale także miejsca na klucze używane na partycji LUKS.

Poniższy przykład utworzy zaszyfrowaną partycję root na {{ic|/dev/sda1} przy użyciu domyślnego szyfrowania AES w trybie XTS z efektywnym 256-bitowym szyfrowaniem

```
# cryptsetup -s 512 luksFormat --type luks2 /dev/sda1

```

##### Używanie LUKS do formatowania partycji za pomocą pliku kluczy

Podczas tworzenia nowej zaszyfrowanej partycji LUKS, plik klucza może być powiązany z partycją podczas jej tworzenia za pomocą:

```
# cryptsetup luksFormat --type luks2 *device* */path/to/mykeyfile*

```

Zobacz [#Keyfiles](#Keyfiles) aby uzyskać instrukcje dotyczące generowania plików kluczy i zarządzania nimi.

#### Odblokowywanie / mapowanie partycji LUKS za pomocą device mapper

Po utworzeniu partycji LUKS można je odblokować.

Proces odblokowania zmapuje partycje do nowej nazwy urządzenia za pomocą urządzenia odwzorowującego. To ostrzega o tym jądrze `*device*` jest faktycznie zaszyfrowanym urządzeniem i powinno być adresowane za pomocą LUKS przy użyciu `/dev/mapper/*dm_name*` aby nie nadpisywać zaszyfrowanych danych. Aby chronić się przed przypadkowym nadpisaniem, przeczytaj o możliwościach [backup the cryptheader](#Backup_and_restore) po zakończeniu konfiguracji.

Aby otworzyć zaszyfrowaną partycję LUKS:

```
# cryptsetup open *device* *dm_name*

```

Zostaniesz poproszony o hasło, aby odblokować partycję. Zwykle nazwa odwzorowana przez urządzenie jest opisowa dla funkcji zamapowanej partycji. Na przykład poniższe odblokowuje partycję luks `/dev/sda1` i odwzorowuje go na urządzenie odwzorowujące urządzenie o nazwie `cryptroot`:

```
# cryptsetup open /dev/sda1 cryptroot 

```

Po otwarciu adres urządzenia głównego partycji będzie `/dev/mapper/cryptroot` zamiast partycji (np. `/dev/sda1`).

Aby skonfigurować LVM na wierzchu warstwy szyfrowania, plik urządzenia dla zaszyfrowanej grupy woluminów może być podobny `/dev/mapper/cryptroot` zamiast `/dev/sda1`. LVM będzie następnie nadawać dodatkowe nazwy wszystkim utworzonym woluminom logicznym, np. `/dev/mapper/lvmpool-root` i `/dev/mapper/lvmpool-swap`.

Aby zapisać zaszyfrowane dane w partycji, należy uzyskać do nich dostęp za pomocą nazwy zmapowanej urządzenia. Pierwszym etapem dostępu będzie zazwyczaj [utworzenie systemu plików](/index.php/File_systems#Create_a_file_system "File systems"). Na przykład:

```
 # mkfs -t ext4 /dev/mapper/cryptroot

```

Urządzenie `/dev/mapper/cryptroot` może być [zamontowany](/index.php/Mount "Mount") jak każda inna partycja.

Aby zamknąć kontener luks, odmontuj partycję i wykonaj następujące czynności:

```
# cryptsetup close cryptroot

```

### Szyfrowanie urządzeń w trybie zwykłym

Stworzenie i późniejszy dostęp do *dm-crypt* Szyfrowania w trybie zwykłym wymaga nie więcej niż korzystania z *cryptsetup* `open` akcję z poprawnymi [parametrami](#Opcje_szyfrowania_dla_trybu_zwyk.C5.82ego). Poniżej pokazano, że z dwoma przykładami urządzeń innych niż root, ale dodaje dziwnie, układając je w stos (tj. Drugi jest tworzony wewnątrz pierwszego). Oczywiście układanie szyfrowania podwaja się narzutowo. Oto przykład użycia innego przykładu użycia opcji szyfrowania.

Otwórz akcję z poprawnymi parametrami.

Pierwszy program odwzorowujący jest tworzony z domyślnymi ustawieniami "cryptsetup", jak opisano w lewej kolumnie tabeli powyżej

 `# cryptsetup --type plain -v open /dev/sdaX plain1` 
```
Enter passphrase: 
Command successful.

```

Teraz dodajemy do niego drugie urządzenie blokowe, używając różnych parametrów szyfrowania oraz z (opcjonalnym) offsetem, tworzymy system plików i montujemy go

 `# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10  open /dev/mapper/plain1 plain2`  `Enter passphrase:`  `# lsblk -p` 
```
 NAME                                                     
 /dev/sda                                     
 ├─/dev/sdaX          
 │ └─/dev/mapper/plain1     
 │   └─/dev/mapper/plain2              
 ...

```

```
# mkfs -t ext2 /dev/mapper/plain2
# mount -t ext2 /dev/mapper/plain2 /mnt
# echo "This is stacked. one passphrase per foot to shoot." > /mnt/stacked.txt

```

Zamykamy stos, aby sprawdzić, czy dostęp działa

```
# cryptsetup close plain2
# cryptsetup close plain1

```

Najpierw spróbujmy bezpośrednio otworzyć system plików:

```
# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10 open /dev/sdaX plain2

```
 `# mount -t ext2 /dev/mapper/plain2 /mnt` 
```
mount: wrong fs type, bad option, bad superblock on /dev/mapper/plain2,
      missing codepage or helper program, or other error

```

Dlaczego to nie zadziałało? Ponieważ blok startowy "plain2" (`10`) is still encrypted with the cipher from "plain1". It can only be accessed via the stacked mapper. The error is arbitrary though, trying a wrong passphrase or wrong options will yield the same. dla *dm-crypt* tryb zwykły, `open` akcja nie spowoduje błędu.

Ponowna próba w prawidłowej kolejności:

```
# cryptsetup close plain2    # dysfunctional mapper from previous try

```
 `# cryptsetup --type plain open /dev/sdaX plain1` 
```
Enter passphrase:

```
 `# cryptsetup --type plain --cipher=serpent-xts-plain64 --hash=sha256 --key-size=256 --offset=10 open /dev/mapper/plain1 plain2`  `Enter passphrase:`  `# mount /dev/mapper/plain2 /mnt && cat /mnt/stacked.txt` 
```
This is stacked. one passphrase per foot to shoot.

```

*dm-crypt* poradzi sobie ze skumulowanym szyfrowaniem w niektórych mieszanych trybach. Na przykład tryb LUKS może być ustawiony w stosie na maperze ""plain1". Nagłówek zostałby zaszyfrowany wewnątrz "plain1", gdy jest zamknięty.

Available for plain mode only is the option `--shared`. With it a single device can be segmented into different non-overlapping mappers. We do that in the next example, using a *loopaes* compatible cipher mode for "plain2" this time:

 `# cryptsetup --type plain --offset 0 --size 1000 open /dev/sdaX plain1`  `Enter passphrase:`  `# cryptsetup --type plain --offset 1000 --size 1000 --shared --cipher=aes-cbc-lmk --hash=sha256 open /dev/sdaX plain2`  `Enter passphrase:`  `# lsblk -p` 
```
NAME                    
dev/sdaX                    
├─/dev/sdaX               
│ ├─/dev/mapper/plain1     
│ └─/dev/mapper/plain2     
...

```

Jak pokazuje devicetree, oba znajdują się na tym samym poziomie, tj. Nie są ułożone w stos, a "plain2" można otwierać indywidualnie.

## Działania Cryptsetup specyficzne dla LUKS

### Zarządzanie kluczami

Możliwe jest zdefiniowanie do 8 różnych kluczy na partycję LUKS. Umożliwia to użytkownikowi tworzenie kluczy dostępu do składowania kopii zapasowej: W tak zwanym kluczowym zabezpieczeniu, jeden klucz jest używany do codziennego użytku, drugi jest przechowywany w depozycie, aby uzyskać dostęp do partycji w przypadku, gdy dzienne hasło zostało zapomniane lub plik klucza jest zagubiony / uszkodzony. Również inny klucz-gniazdo może być użyty do przyznania dostępu do partycji użytkownikowi poprzez wydanie drugiego klucza, a następnie ponowne jego unieważnienie.

Po utworzeniu zaszyfrowanej partycji tworzona jest początkowa partia klawiszy 0 (jeśli żadna inna nie została określona ręcznie). Dodatkowe keyslots są ponumerowane od 1 do 7\. Które keyslots są używane można zobaczyć poprzez wydanie

 `# cryptsetup luksDump /dev/<device> | grep BLED` 
```
Key Slot 0: ENABLED
Key Slot 1: ENABLED
Key Slot 2: ENABLED
Key Slot 3: DISABLED
Key Slot 4: DISABLED
Key Slot 5: DISABLED
Key Slot 6: DISABLED
Key Slot 7: DISABLED

```

Gdzie <urządzenie> jest woluminem zawierającym nagłówek LUKS. To i wszystkie poniższe polecenia w tej sekcji również działają na pliki kopii zapasowej nagłówka.

#### Dodawanie kluczy LUKS

Dodanie nowych keyslots odbywa się za pomocą cryptsetup z akcją `luksAddKey`. Dla bezpieczeństwa zawsze, to jest również dla już odblokowanych urządzeń, należy poprosić o ważny istniejący klucz ("dowolne hasło") przed wprowadzeniem nowego:

 `# cryptsetup luksAddKey /dev/<device> (/path/to/<additionalkeyfile>)` 
```
Enter any passphrase:
Enter new passphrase for key slot:
Verify passphrase: 

```

Jeżeli `/path/to/<additionalkeyfile>` jest podana, cryptsetup doda nowy klucz dla <additionalkeyfile>. W przeciwnym razie nowe hasło zostanie wyświetlone dwukrotnie. Aby użyć istniejącego "pliku klucza" do autoryzacji akcji, należy `--key-file` or `-d` opcja, po której następuje "stary" plik <keyfile>, spróbuje odblokować wszystkie dostępne klucze keysfile:

```
# cryptsetup luksAddKey /dev/<device> (/path/to/<additionalkeyfile>) -d /path/to/<keyfile>

```

Jeśli zamierza się używać wielu kluczy i zmieniać lub odwoływać je, to `--key-slot` lub `-S` Opcja ta może być użyta do określenia gniazda:

 `# cryptsetup luksAddKey /dev/<device> -S 6` 
```
Enter any passphrase: 
Enter new passphrase for key slot: 
Verify passphrase:

```
 `# cryptsetup luksDump /dev/sda8 | grep 'Slot 6'` 
```
Key Slot 6: ENABLED

```

Aby pokazać powiązaną akcję w tym przykładzie, od razu decydujemy się zmienić klucz:

 `# cryptsetup luksChangeKey /dev/<device> -S 6` 
```
Enter LUKS passphrase to be changed: 
Enter new LUKS passphrase:

```

przed dalszym usuwaniem.

#### Usuwanie kluczy LUKS

Istnieją trzy różne działania mające na celu usuwanie kluczy z nagłówka:

*   `luksRemoveKey` służy do usunięcia klucza, określając jego hasło/plik-klucza.
*   `luksKillSlot` można użyć do usunięcia klucza z określonego gniazda klucza (przy użyciu innego klucza). Oczywiście jest to niezwykle przydatne, jeśli zapomniałeś hasła, zgubiłeś plik klucza lub nie masz do niego dostępu.
*   `luksErase` służy do szybkiego usuwania "aktywnych" kluczy.

**Warning:**

*   Wszystkie powyższe czynności można wykorzystać do nieodwracalnego usunięcia ostatniego aktywnego klucza do zaszyfrowanego urządzenia!
*   Polecenie `luksErase` zostało dodane w wersji 1.6.4, aby szybko uzyskać dostęp do urządzenia Nuke. Ta czynność nie spowoduje wyświetlenia prawidłowego hasła! Nie spowoduje to [wyczyszczenia nagłówka LUKS](/index.php/Dm-crypt/Drive_preparation#Wipe_LUKS_header "Dm-crypt/Drive preparation"), ale wszystkich kluczy jednocześnie, a zatem nie będzie można odzyskać dostępu, chyba że masz poprawną kopię zapasową nagłówka LUKS.

Dla powyższego ostrzeżenia dobrze jest wiedzieć, że klucz, który chcemy zachować, jest ważny. Łatwym sprawdzeniem jest odblokowanie urządzenia za pomocą opcji `-v`, która określa, który slot zajmuje:

 `# cryptsetup -v open /dev/<device> testcrypt` 
```
Enter passphrase for /dev/<device>: 
Key slot 1 unlocked.
Command successful.

```

Teraz możemy usunąć klucz dodany w poprzednim podsekcji za pomocą jego hasła:

 `# cryptsetup luksRemoveKey /dev/<device>` 
```
Enter LUKS passphrase to be deleted:

```

Gdybyśmy użyli tego samego hasła dla dwóch klawiszy, pierwszy slot zostałby teraz wyczyszczony. Ponowne wykonanie go spowoduje usunięcie drugiego.

Alternatywnie możemy określić kluczowy slot:

 `# cryptsetup luksKillSlot /dev/<device> 6` 
```
Enter any remaining LUKS passphrase:

```

Należy pamiętać, że w obu przypadkach potwierdzenie nie było wymagane.

 `# cryptsetup luksDump /dev/sda8 | grep 'Slot 6'` 
```
Key Slot 6: DISABLED

```

Aby powtórzyć powyższe ostrzeżenie: jeśli to samo hasło zostało użyte w kluczowym gnieździe 1 i 6, obie karty zniknęłyby teraz.

### Kopia zapasowa i przywracanie

Jeśli nagłówek zaszyfrowanej partycji LUKS zostanie zniszczony, nie będzie można odszyfrować danych. Jest to tak samo dylemat, jak zapomnienie hasła lub uszkodzenie pliku klucza używanego do odblokowania partycji. Uszkodzenia mogą pojawić się z własnej winy podczas ponownej partycjonowania dysku w późniejszym czasie lub przez programy innych producentów błędnie interpretujące tabelę partycji. Dlatego posiadanie kopii zapasowej nagłówka i przechowywanie go na innym dysku może być dobrym pomysłem.

**Note:** Jeśli zostanie naruszone hasło główne zaszyfrowanych partycji LUKS, musisz odwołać je na "każdej" kopii kryptografu, nawet kopii zapasowej. W przeciwnym razie do odtępienia powiązanej partycji można użyć kopii kopii zapasowej kryptografu wykorzystującego przejęte hasło. Zobacz [LUKS FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#6-backup-and-data-recovery) for further details.

#### Kopia zapasowa za pomocą cryptsetup

Cryptsetup' `luksHeaderBackup` Działanie przechowuje binarną kopię zapasową nagłówku LUKS i obszaru keyslot:

```
# cryptsetup luksHeaderBackup /dev/<device> --header-backup-file /mnt/<backup>/<file>.img

```

gdzie <device> to partycja zawierająca wolumin LUKS.

**Tip:** Możesz także utworzyć kopię zapasową nagłówka zwykłego tekstu w ramfs i zaszyfrować go w przykładzie za pomocą gpg przed zapisaniem do trwałej kopii zapasowej, wykonując następujące polecenia.

```
# mkdir /root/<tmp>/
# mount ramfs /root/<tmp>/ -t ramfs
# cryptsetup luksHeaderBackup /dev/<device> --header-backup-file /root/<tmp>/<file>.img
# gpg2 --recipient <User ID> --encrypt /root/<tmp>/<file>.img 
# cp /root/<tmp>/<file>.img.gpg /mnt/<backup>/
# umount /root/<tmp>

```

**Warning:** Tmpfs można zamienić na twardy dysk, jeśli brakuje pamięci, więc nie jest to zalecane tutaj.

#### Przywracanie za pomocą cryptsetup

**Warning:** Przywrócenie niewłaściwego nagłówka lub przywrócenie go do niezaszyfrowanej partycji spowoduje utratę danych! Akcja nie może sprawdzić, czy nagłówek jest rzeczywiście "poprawny" dla tego konkretnego urządzenia.

Aby uniknąć przywrócenia złego nagłówka, możesz upewnić się, że działa, używając go zdalnie `--header` pierwszy:

 `# cryptsetup -v --header /mnt/<backup>/<file>.img open /dev/<device> test` 
```
Key slot 0 unlocked.
Command successful.

```

```
# mount /dev/mapper/test /mnt/test && ls /mnt/test 
# umount /mnt/test 
# cryptsetup close test 

```

Po pomyślnym sprawdzeniu można wykonać przywracanie:

```
# cryptsetup luksHeaderRestore /dev/<device> --header-backup-file ./mnt/<backup>/<file>.img

```

Teraz wszystkie obszary keyslot są nadpisywane; tylko aktywne keyslots z pliku kopii zapasowej są dostępne po wydaniu polecenia.

#### Ręczne tworzenie kopii zapasowych i przywracanie

Nagłówek zawsze znajduje się na początku urządzenia, a kopia zapasowa może być również wykonywana bez dostępu do "cryptsetup". Najpierw musisz znaleźć offset dla zaszyfrowanej partycji:

 `# cryptsetup luksDump /dev/<device> | grep "Payload offset"` 
```
Payload offset:	4040

```

Po drugie sprawdź rozmiar sektora dysku

 `# fdisk -l /dev/<device> | grep "Sector size"` 
```
Sector size (logical/physical): 512 bytes / 512 bytes

```

Teraz, gdy znasz wartości, możesz wykonać kopię zapasową nagłówka za pomocą prostej komendy dd:

```
# dd if=/dev/<device> of=/path/to/<file>.img bs=512 count=4040

```

i przechowuj go bezpiecznie.

Przywracanie można następnie wykonać przy użyciu tych samych wartości, co podczas tworzenia kopii zapasowej:

```
# dd if=./<file>.img of=/dev/<device> bs=512 count=4040

```

### Ponowne szyfrowanie urządzeń

The [cryptsetup](https://www.archlinux.org/packages/?name=cryptsetup) ppakiet zawiera narzędzie "cryptsetup-reencrypt". Może być użyty do konwersji istniejącego niezaszyfrowanego systemu plików na zaszyfrowany LUKS (opcja `--new`) i trwale usunąć szyfrowanie LUKS (`--decrypt`) z urządzenia. Jak sama nazwa wskazuje, może być również użyty do ponownego zaszyfrowania istniejącego zaszyfrowanego urządzenia LUKS, jednak ponowne szyfrowanie nie jest możliwe w przypadku odłączonego nagłówka LUKS lub innych trybów szyfrowania (na przykład w trybie zwykłym). W celu ponownego szyfrowania można zmienić [#Opcje szyfrowania dla trybu LUKS](#Opcje_szyfrowania_dla_trybu_LUKS). *cryptsetup-reencrypt*Działania można wykonywać tylko dla niezamontowanych urządzeń. Zobacz [cryptsetup-reencrypt(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cryptsetup-reencrypt.8) po więcej informacji.

Jednym z zastosowań ponownego szyfrowania może być ponowne zabezpieczenie danych po złamaniu hasła lub [pliku klucza](#Keyfiles) i nie można mieć pewności, że nie otrzymano żadnej kopii nagłówka LUKS. Na przykład, jeśli tylko hasło zostało naruszone, ale nie nastąpił fizyczny dostęp do urządzenia, wystarczy zmienić odpowiednie hasło / klucz tylko ([#Zarządzanie kluczami](#Zarz.C4.85dzanie_kluczami)).

**Warning:** Zawsze upewnij się, że "kopia zapasowa" jest dostępna i sprawdź dokładnie opcje, które określisz przed użyciem narzędzia!

Poniżej przedstawiono przykład szyfrowania niezaszyfrowanej partycji systemu plików i ponownego szyfrowania istniejącego urządzenia LUKS.

#### Zaszyfruj niezaszyfrowany system plików

Nagłówek szyfrowania LUKS jest zawsze przechowywany na początku dysku. Ponieważ istniejącemu systemowi plików zwykle przydzielane są wszystkie sektory partycji, pierwszym krokiem jest zmniejszenie go, aby zrobić miejsce dla nagłówka LUKS.

[Domyślny](#Opcje_szyfrowania_dla_trybu_LUKS) szyfr LUKS nagłówka wymaga `4096` 512-bajtowych sektorów. Sprawdziliśmy już miejsce i utrzymujemy prostotę, zmniejszając istniejący system plików `ext4` na `/dev/sdaX` do jego obecnego możliwego minimum:

```
# umount /mnt

```
 `# e2fsck -f /dev/sdaX` 
```
e2fsck 1.43-WIP (18-May-2015)
Pass 1: Checking inodes, blocks, and sizes
...
/dev/sda6: 12/166320 files (0.0% non-contiguous), 28783/665062 blocks

```
 `# resize2fs -M /dev/sdaX` 
```
resize2fs 1.43-WIP (18-May-2015)
Resizing the filesystem on /dev/sdaX to 26347 (4k) blocks.
The filesystem on /dev/sdaX is now 26347 (4k) blocks long.

```

Teraz zaszyfrujemy go, używając domyślnego szyfru, którego nie musimy jawnie określać. Uwaga: nie ma jeszcze opcji (jeszcze) do podwójnego sprawdzenia hasła przed rozpoczęciem szyfrowania, należy uważać, aby nie pomylić:

 `# cryptsetup-reencrypt /dev/sdaX --new  --reduce-device-size 4096S` 
```
WARNING: this is experimental code, it can completely break your data.
Enter new passphrase: 
Progress: 100,0%, ETA 00:00, 2596 MiB written, speed  37,6 MiB/s

```

Po zakończeniu szyfrowanie zostało wykonane na pełną partycję, tj. Nie tylko przestrzeń, do której skrócił się system plików (`sdaX` ma `2.6GiB` a procesor użyty w tym przykładzie nie ma instrukcji sprzętowych AES). Ostatnim krokiem jest ponowne rozszerzenie systemu plików zaszyfrowanego urządzenia, aby zajęło dostępne miejsce:

 `# cryptsetup open /dev/sdaX recrypt` 
```
Enter passphrase for /dev/sdaX: 
...

```
 `# resize2fs /dev/mapper/recrypt` 
```
resize2fs 1.43-WIP (18-May-2015)
Resizing the filesystem on /dev/mapper/recrypt to 664807 (4k) blocks.
The filesystem on /dev/mapper/recrypt is now 664807 (4k) blocks long.

```

```
# mount /dev/mapper/recrypt /mnt

```

i gotowe.

#### Ponowne szyfrowanie istniejącej partycji LUKS

W tym przykładzie istniejące urządzenie LUKS jest ponownie szyfrowane.

**Warning:** Dokładnie sprawdź, czy poprawnie określasz opcje szyfrowania dla funkcji *cryptsetup-reencrypt* i *nigdy* nie re-szyfruj bez **niezawodnej kopii zapasowej**! Od września 2015 narzędzie **akceptuje** nieprawidłowe opcje i uszkadza nagłówek LUKS, jeśli nie jest używane poprawnie!

Aby ponownie zaszyfrować urządzenie za pomocą istniejących opcji szyfrowania, nie trzeba ich określać. Prosty:

 `# cryptsetup-reencrypt /dev/sdaX` 
```

WARNING: this is experimental code, it can completely break your data.
Enter passphrase for key slot 0: 
Progress: 100,0%, ETA 00:00, 2596 MiB written, speed  36,5 MiB/s

```

wykonuje to.

Możliwym przypadkiem jest ponowne szyfrowanie urządzeń LUKS, które mają nieaktualne opcje szyfrowania. Oprócz powyższego ostrzeżenia o prawidłowym określeniu opcji, możliwość zmiany nagłówka LUKS może być również ograniczona przez jego rozmiar. Na przykład, jeśli urządzenie zostało początkowo zaszyfrowane przy użyciu szyfrowania w trybie CBC i klucza 128-bitowego, nagłówek LUKS będzie o połowę mniejszy od wspomnianych {{ic|4096} sektorów:

 `# cryptsetup luksDump /dev/sdaX |grep -e "mode" -e "Payload" -e "MK bits"` 
```
Cipher mode:   	cbc-essiv:sha256
Payload offset:	**2048**
MK bits:       	128

```

O ile możliwe jest uaktualnienie szyfrowania takiego urządzenia, jest to obecnie możliwe tylko w dwóch etapach. Najpierw ponownie zaszyfruj z tymi samymi opcjami szyfrowania, ale używając `--reduce-device-size` opcja utworzenia dodatkowej przestrzeni dla większego nagłówka LUKS. Po drugie, ponownie sprowadź całe urządzenie z żądanym szyfrem. Z tego powodu i faktu, że kopia zapasowa powinna być tworzona w każdym przypadku, tworzenie nowego, świeżego urządzenia zaszyfrowanego do przywrócenia jest zawsze szybszą opcją.

## Zmiana rozmiaru zaszyfrowanych urządzeń

Jeśli urządzenie pamięciowe zaszyfrowane za pomocą dm-crypt jest klonowane (za pomocą narzędzia takiego jak dd) do innego większego urządzenia, podstawowe urządzenie dm-crypt musi zostać powiększone, aby wykorzystać całą przestrzeń.

W tym przykładzie urządzeniem docelowym jest /dev/sdX2, zostanie użyta cała dostępna przestrzeń obok partycji:

```
# cryptsetup luksOpen /dev/sdX2 sdX2
# cryptsetup resize sdX2

```

Następnie należy zmienić rozmiar podstawowego systemu plików.

### Loopback filesystem

Zakładając, że zaszyfrowany system plików loopback jest zamontowany w `/mnt/secret`, na przykład następujący [dm-crypt/Encrypting a non-root file system (Polski)#Loop device](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Polski)#Loop_device "Dm-crypt/Encrypting a non-root file system (Polski)"), najpierw odmontuj zaszyfrowany kontener:

```
# umount /mnt/secret
# cryptsetup close secret
# losetup -d /dev/loop0

```

Następnie rozwiń plik kontenera o rozmiar danych, które chcesz dodać:

**Warning:** Be careful to really use **two** `>`, or you will override your current container.

```
# dd if=/dev/urandom bs=1M count=1024 | cat - >> /bigsecret

```

Teraz zmapuj kontener na loop device:

```
# losetup /dev/loop0 /bigsecret
# cryptsetup open /dev/loop0 secret

```

Następnie zmień rozmiar zaszyfrowanej części kontenera na maksymalny rozmiar pliku kontenera:

```
# cryptsetup resize secret

```

Na koniec przeprowadź test systemu plików i, jeśli jest w porządku, zmień jego rozmiar (przykład dla ext2/3/4):

```
# e2fsck -f /dev/mapper/secret
# resize2fs /dev/mapper/secret

```

Możesz teraz ponownie zamontować kontener:

```
# mount /dev/mapper/secret /mnt/secret

```

## Pliki kluczy

**Note:** TW tej sekcji opisano użycie pliku klucza tekstowego w postaci zwykłego tekstu. Jeśli chcesz zaszyfrować plik klucza, co daje dwuetapowe uwierzytelnianie, Zobacz [Using GPG or OpenSSL Encrypted Keyfiles](/index.php/Dm-crypt/Specialties#Using_GPG.2C_LUKS.2C_or_OpenSSL_Encrypted_Keyfiles "Dm-crypt/Specialties") po szczegóły, ale proszę, przeczytaj ten rozdział.

**Co to jest plik klucza?**

Plik klucza to plik, którego dane są używane jako hasło do odblokowania zaszyfrowanego woluminu. Oznacza to, że jeśli taki plik zostanie utracony lub zmieniony, odszyfrowanie woluminu może być niemożliwe.

**Tip:** Zdefiniuj hasło oprócz pliku klucza, aby uzyskać kopię zapasową dostępu do zaszyfrowanych woluminów w przypadku utraty lub zmiany zdefiniowanego pliku klucza.

**Dlaczego warto użyć pliku klucza?**

Istnieje wiele rodzajów plików kluczy. Każdy rodzaj użytego pliku klucza ma zalety i wady:

### Rodzaje plików kluczy

#### hasło

Jest to plik klucza zawierający proste hasło. Zaletą tego typu pliku kluczy jest to, że jeśli plik zostanie utracony, zawarte w nim dane są znane i, miejmy nadzieję, łatwo zapamiętane przez właściciela zaszyfrowanego woluminu. Jednak wadą jest to, że nie dodaje żadnego zabezpieczenia przed wprowadzeniem hasła podczas początkowego uruchomienia systemu.

Przykład: `1234`

**Note:** Plik klucza zawierający frazę hasła nie może zawierać znaku nowej linii. Jedną z opcji jest utworzenie go za pomocą
```
# echo -n 'your_passphrase' > /path/to/<keyfile>
# chown root:root /path/to/<keyfile>; chmod 400 /path/to/<keyfile>

```

#### randomtext

Jest to plik klucza zawierający blok losowych znaków. Zaletą tego typu pliku kluczy jest to, że jest on znacznie bardziej odporny na ataki słownikowe niż proste hasło. W tej sytuacji można wykorzystać dodatkową moc plików kluczy, która jest długością używanych danych. Ponieważ nie jest to ciąg przeznaczony do zapamiętania przez osobę do wpisu, trywialne jest tworzenie plików zawierających tysiące losowych znaków jako klucz. Wadą jest to, że jeśli ten plik zostanie utracony lub zmieniony, najprawdopodobniej dostęp do zaszyfrowanego woluminu bez kopii zapasowej hasła będzie niemożliwy.

Przykład: `fjqweifj830149-57 819y4my1-38t1934yt8-91m 34co3;t8y;9p3y-`

#### binary

Jest to plik binarny, który został zdefiniowany jako plik klucza. Podczas identyfikowania plików jako kandydatów do pliku klucza zaleca się wybrać pliki, które są stosunkowo statyczne, takie jak zdjęcia, muzyka, klipy wideo. Zaletą tych plików jest to, że pełnią podwójną funkcję, co może utrudnić identyfikację ich jako plików kluczy. Zamiast pliku tekstowego z dużą ilością losowego tekstu, plik klucza będzie wyglądać jak zwykły plik obrazu lub klip muzyczny przypadkowego obserwatora. Wadą jest to, że jeśli ten plik zostanie utracony lub zmieniony, najprawdopodobniej dostęp do zaszyfrowanego woluminu bez kopii zapasowej hasła będzie niemożliwy. Dodatkowo istnieje teoretyczna utrata losowości w porównaniu z losowo wygenerowanym plikiem tekstowym. Wynika to z faktu, że obrazy, filmy i muzyka mają pewien nierozerwalny związek między sąsiednimi bitami danych, które nie istnieją dla pliku tekstowego. Jest to jednak kontrowersyjne i nigdy nie zostało publicznie wykorzystane.

Przykład: obrazy, tekst, wideo ...

### Tworzenie pliku kluczy z losowymi znakami

#### Przechowywanie pliku klucza w systemie plików

Plik klucza może mieć dowolną treść i rozmiar.

Tutaj `dd` służy do generowania pliku kluczy o 2048 losowych bajtach, przechowując go w pliku `/etc/mykeyfile`

```
# dd bs=512 count=4 if=/dev/urandom of=/etc/mykeyfile

```

Jeśli planujesz przechowywać plik klucza na urządzeniu zewnętrznym, możesz po prostu zmienić plik wyjściowy na odpowiedni katalog:

```
# dd bs=512 count=4 if=/dev/urandom of=/media/usbstick/mykeyfile

```

Aby odmówić dostępu innym użytkownikom `root`:

```
# chmod 600 /etc/mykeyfile

```

##### Bezpieczne nadpisywanie zapisanych plików kluczy

Jeśli przechowujesz tymczasowy plik kluczy na fizycznym urządzeniu magazynującym i chcesz go usunąć, pamiętaj, aby nie tylko usunąć plik klucza później, ale użyj czegoś podobnego

```
# shred --remove --zero mykeyfile

```

aby go bezpiecznie zastąpić. W przypadku nadmiernie obciążonych systemów plików, takich jak FAT lub ext2, będzie to wystarczające, natomiast w przypadku kronikowania systemów plików, sprzętu pamięci flash i innych przypadków zdecydowanie zaleca się [wyczyszczenie całego dysku](/index.php/Securely_wipe_disk "Securely wipe disk").

#### Przechowywanie pliku kluczy w ramfs

Alternatywnie możesz zamontować ramfs do tymczasowego przechowywania pliku klucza:

```
# mkdir /root/myramfs
# mount ramfs /root/myramfs/ -t ramfs
# cd /root/myramfs

```

Zaletą jest to, że znajduje się on w pamięci RAM, a nie na dysku fizycznym, dlatego nie można go odzyskać po odmontowaniu ramfów. Po skopiowaniu pliku klucza do innego bezpiecznego i trwałego systemu plików, odmontuj pliki ramfs ponownie

```
# umount /root/myramfs

```

### Konfigurowanie LUKS do korzystania z pliku klucza

Dodaj keylot dla pliku klucza do nagłówka LUKS:

 `# cryptsetup luksAddKey /dev/sda2 /etc/mykeyfile` 
```
Enter any LUKS passphrase:
key slot 0 unlocked.
Command successful.

```

### Ręczne odblokowywanie partycji przy użyciu pliku klucza

Użyj opcji `--key-file` podczas otwierania urządzenia LUKS:

```
# cryptsetup open /dev/sda2 *dm_name* --key-file /etc/mykeyfile

```

### Odblokowywanie dodatkowej partycji podczas rozruchu

Jeśli plik klucza dla dodatkowego systemu plików jest przechowywany w zaszyfrowanym katalogu głównym, jest bezpieczny, gdy system jest wyłączony, ale można go pobrać, aby automatycznie odblokować gniazdo podczas rozruchu za pośrednictwem [crypttab](/index.php/Crypttab "Crypttab"). Od pierwszego przykładu powyżej przy użyciu [UUID](/index.php/UUID "UUID"):

 `/etc/crypttab` 
```
home    UUID=<UUID identifier>    /etc/mykeyfile

```

jest wszystko potrzebne do odblokowania, i

 `/etc/fstab` 
```
/dev/mapper/home        /home   ext4        defaults        0       2

```

do montowania urządzenia blokowego LUKS z wygenerowanym plikiem klucza.

**Tip:** Jeśli wolisz używać trybu blokowego `--plain` mode, opcje szyfrowania niezbędne do jego odblokowania są określone w `/etc/crypttab`. W takim przypadku należy zastosować systemowe obejście, o którym mowa w [crypttab](/index.php/Crypttab "Crypttab").

### Odblokowywanie partycji głównej podczas rozruchu

Jest to po prostu kwestia skonfigurowania [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") w celu włączenia niezbędnych modułów lub plików i skonfigurowania parametru jądra [cryptkey](/index.php/Dm-crypt/System_configuration#cryptkey "Dm-crypt/System configuration"), aby wiedział, gdzie znaleźć plik klucza.

Poniżej przedstawiono dwa przypadki:

1.  Używanie pliku kluczy przechowywanego na nośniku zewnętrznym (tutaj pamięć USB)
2.  Używanie pliku klucza osadzonego w initramfs

#### Z plikiem kluczy przechowywanym na zewnętrznym nośniku

##### Konfigurowanie mkinitcpio

Musisz dodać moduł do swojego `/etc/mkinitcpio.conf`dla systemu plików napędu (`vfat` moduł w poniższym przykładzie):

```
MODULES=(vfat)

```

W tym przykładzie zakłada się, że używasz dysku USB sformatowanego w systemie FAT (`vfat` moduł). Zastąp te nazwy modułów, jeśli używasz innego systemu plików na dysku USB (np. `ext2`) lub inną codepage. Jeśli skarga dotyczy złej superbloku i złej strony kodowej przy starcie, potrzebny jest dodatkowy moduł codepage do załadowania. Na przykład możesz potrzebować `nls_iso8859-1`moduł dla `iso8859-1` codepage.

Jeśli masz klawiaturę inną niż amerykańska, może okazać się użyteczne załadowanie układu klawiatury przed monitem o wprowadzenie hasła w celu odblokowania partycji głównej podczas rozruchu. Do tego będziesz potrzebował `keymap` hak przed `encrypt`.

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

##### Konfigurowanie parametrów jądra

Dodaj następujące opcje do [kernel parameters](/index.php/Kernel_parameters "Kernel parameters") jeśli używasz `encrypt` hak. Jeśli używasz `sd-encrypt` Zobacz [dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration").

```
cryptdevice=/dev/*<partition1>*:root cryptkey=/dev/*<partition2>*:<fstype>:<path>

```

Na przykład:

```
cryptdevice=/dev/sda3:root cryptkey=/dev/sdb1:vfat:/keys/secretkey

```

Choosing a plain filename for your key provides a bit of 'security through obscurity', but be aware the kernel command line is recorded in the kernel's log (*dmesg*). The keyfile can not be a hidden file, that means the filename must not start with a dot, or the `encrypt` hook will fail to find the keyfile during the boot process. Alternatively, one could hide the keyfile between the partitions and use:

```
cryptkey=/dev/sdb1:offset:size

```

Zaletą jest to, że trudniej jest przypadkowo usunąć klucz.

Nazwa węzłów urządzeń, takich jak `/dev/sdb1`, nie ma gwarancji, że pozostanie takie samo podczas restartu. Bardziej niezawodny jest dostęp do urządzenia z [trwałym nazwaniem urządzeń blokowych](/index.php/Persistent_block_device_naming "Persistent block device naming") udev. Aby upewnić się, że szyfrowany klucz znajdzie plik klucza podczas odczytu go z zewnętrznego urządzenia pamięci masowej, należy użyć nazw stałych urządzeń blokowych. Zobacz artykuł na temat [trwałych nazw urządzeń blokowych](/index.php/Persistent_block_device_naming "Persistent block device naming").

#### Z plikiem kluczy osadzonym w initramfs

**Warning:** Użyj wbudowanego pliku klucza tylko **wtedy**, gdy wcześniej dysponujesz jakąś formą mechanizmu uwierzytelniania, który wystarczająco zabezpiecza plik klucza. W przeciwnym razie nastąpi automatyczne odszyfrowanie, całkowicie eliminując cel szyfrowania urządzenia blokowego.

Ta metoda pozwala na użycie specjalnie nazwanego pliku klucza, który zostanie osadzony w pliku [initramfs](/index.php/Initramfs "Initramfs") i odbierane przez `encrypt` [hookaby](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") odblokować główny system plików (`cryptdevice`) automatycznie. Może być przydatne zastosowanie podczas korzystania z [GRUB early cryptodisk](/index.php/GRUB#Boot_partition "GRUB") w celu uniknięcia wprowadzania dwóch haseł podczas rozruchu.

Zaszyfrowanie pozwala użytkownikowi określić plik klucza za pomocą parametru jądra `cryptkey`: w przypadku initramfs, składnia to rootfs: `rootfs:*path*` Zobacz [dm-crypt/System configuration#cryptkey](/index.php/Dm-crypt/System_configuration#cryptkey "Dm-crypt/System configuration"). Poza tym ten parametr jądra jest domyślnie używany `/crypto_keyfile.bin`, a jeśli initramfs zawiera poprawny klucz o tej nazwie, deszyfrowanie nastąpi automatycznie bez potrzeby konfiguracji `cryptkey` parametr.

Jeśli korzystasz z `sd-encrypt` zamiast `encrypt`, określ lokalizację pliku klucza za pomocą parametru jądra `rd.luks.key`. Zobacz [dm-crypt/System configuration#rd.luks.key](/index.php/Dm-crypt/System_configuration#rd.luks.key "Dm-crypt/System configuration").

[Wygeneruj plik klucza](#Tworzenie_pliku_kluczy_z_losowymi_znakami), nadaj mu odpowiednie uprawnienia i [dodaj go jako klucz LUKS](#Dodawanie_kluczy_LUKS):

```
# dd bs=512 count=4 if=/dev/urandom of=/crypto_keyfile.bin
# chmod 000 /crypto_keyfile.bin
# chmod 600 /boot/initramfs-linux*
# cryptsetup luksAddKey /dev/sdX# /crypto_keyfile.bin

```

**Warning:** Kiedy uprawnienia initramfs są ustawione na 644 (domyślnie), wszyscy użytkownicy będą mogli zrzucić plik klucza. Upewnij się, że uprawnienia są nadal 600, jeśli zainstalujesz nowe jądro.

Dołącz klucz do [mkinitcpio's FILES array](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio"):

 `/etc/mkinitcpio.conf`  `FILES=(/crypto_keyfile.bin)` 

Wreszcie [zregeneruj initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Przy następnym ponownym uruchomieniu należy tylko raz wpisać hasło do odszyfrowania kontenera.

([source](http://www.pavelkogan.com/2014/05/23/luks-full-disk-encryption/#bonus-login-once))