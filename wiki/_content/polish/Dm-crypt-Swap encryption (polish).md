W zależności od wymagań można zastosować różne metody szyfrowania partycji [swap](/index.php/Swap "Swap"). które są opisane poniżej. Konfiguracja, w której szyfrowanie swapowe jest re-inicjalizowane przy ponownym uruchomieniu (z nowym szyfrowaniem) zapewnia lepszą ochronę danych, ponieważ pozwala uniknąć wrażliwych fragmentów plików, które mogły zostać zamienione dawno temu bez nadpisywania. Jednak ponowne szyfrowanie swapu również uniemożliwia korzystanie z hibernacji

## Contents

*   [1 Bez wsparcia dla hibernacji](#Bez_wsparcia_dla_hibernacji)
    *   [1.1 UUID i LABEL](#UUID_i_LABEL)
*   [2 Z obsługą hibernacji](#Z_obsługą_hibernacji)
    *   [2.1 LVM na LUKS](#LVM_na_LUKS)
    *   [2.2 mkinitcpio hook](#mkinitcpio_hook)
    *   [2.3 Używanie pliku wymiany](#Używanie_pliku_wymiany)
*   [3 Znane problemy](#Znane_problemy)

## Bez wsparcia dla hibernacji

W systemach, w których wykonuje się hibernację nie jest pożądaną funkcją, można ustawić `/etc/crypttab` aby odszyfrować partycję wymiany z losowym hasłem z zwykłym dm-crypt podczas startu systemu. Losowe hasło jest odrzucane podczas zamykania, pozostawiając tylko zaszyfrowane, niedostępne dane w urządzeniu wymiany.

Aby włączyć tę funkcję, po prostu odkomentuj linię zaczynającą się od `swap` w `/etc/crypttab`. Zmień parametr `<device>` na nazwę twojego urządzenia wymiany, na przykład będzie wyglądał mniej więcej tak:

 `/etc/crypttab` 
```
# <name>  <device>     <password>     <options>
swap      /dev/sd*X#*    /dev/urandom   swap,cipher=aes-xts-plain64,size=256
```

Spowoduje to mapowanie `/dev/sd*X#*` na `/dev/mapper/swap` jako partycję wymiany, która może być dodana w `/etc/fstab` jak zwykły swap. Jeśli wcześniej była nieszyfrowana partycja wymiany, nie zapomnij jej wyłączyć - lub użyj jej wpisu [fstab](/index.php/Fstab "Fstab"), zmieniając urządzenie na `/dev/mapper/swap`. Domyślne opcje powinny być wystarczające dla większości zastosowań. Aby zapoznać się z innymi opcjami i objaśnieniem każdej kolumny, zobacz [crypttab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/crypttab.5) oraz [point cryptsetup FAQ 2.3](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup).

**Warning:** cała zawartość nazwanego urządzenia zostanie trwale usunięta. Niebezpieczne jest używanie prostego nazewnictwa jądra dla urządzenia wymiennego, ponieważ ich kolejność nazywania (np. `/dev/sda`, `/dev/sdb`) zmienia się po każdym uruchomieniu. Dostępne są następujące opcje:

*   Używaj ścieżek `by-id` i `by-path`. Oba są jednak podatne na zmiany sprzętowe. Zobacz [Persistent block device naming#by-id and by-path](/index.php/Persistent_block_device_naming#by-id_and_by-path "Persistent block device naming").
*   Użyj nazwy woluminu logicznego [LVM](/index.php/LVM "LVM").
*   Użyj metody opisanej w [#UUID i LABEL](#UUID_i_LABEL). Etykiety i [UUIDS](/index.php/Persistent_block_device_naming#by-uuid "Persistent block device naming") nie mogą być używane bezpośrednio ze względu na odtwarzanie i ponowne szyfrowanie urządzenia zamieniającego na każdym rozruchu z `mkswap`, zobacz [https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#2-setup) cryptsetup FAQ].

Aby użyć stałego nazewnictwa urządzeń `by-id` zamiast zwykłego nazewnictwa jądra, najpierw należy zidentyfikować urządzenie wymiany:

 `# find -L /dev/disk -samefile /dev/*sdaX*` 
```
/dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-part*X*
/dev/disk/by-id/wwn-0x60015ee0000b237f-part*X*

```

Następnie użyj jako trwałego odwołania dla partycji przykładowej `/dev/sd*X#*` (jeśli dwa wyniki zostaną zwrócone jak wyżej, wybierz jeden z nich):

 `/etc/crypttab` 
```
# <name>  <device>                                                         <password>     <options>
swap      /dev/disk/by-id/ata-WDC_WD2500BEVT-22ZCT0_WD-WXE908VF0470-partX  /dev/urandom   swap,cipher=aes-cbc-essiv:sha256,size=256
```

Po ponownym uruchomieniu, aby aktywować szyfrowaną wymianę, zauważysz, że uruchomione `swapon -s` pokazuje dla niego dowolny wpis mapowania urządzenia (np. `/dev/dm-1`, podczas gdy komenda `lsblk` pokazuje **crypt** w kolumnie FSTYPE. Ze względu na świeże szyfrowanie każdego rozruchu, UUID dla `/dev/mapper/swap` będzie się zmieniać za każdym razem.

**Note:** Jeśli partycja wybrana do zamiany była poprzednio partycją LUKS, to crypttab nie zastąpi partycji, aby utworzyć partycję wymiany. Jest to środek bezpieczeństwa zapobiegający utracie danych w wyniku przypadkowej błędnej identyfikacji partycji wymiany w crypttab. Aby użyć takiej partycji, nagłówek LUKS musi zostać nadpisany jeden raz. [LUKS header must be overwritten](/index.php/Dm-crypt/Drive_preparation#Wipe_LUKS_header "Dm-crypt/Drive preparation")

### UUID i LABEL

Niebezpieczne jest używanie zamiany przy użyciu crypttab z prostymi nazwami urządzeń jądra, takimi jak `/dev/sdX#` lub nawet `/dev/disk/by-id/ata-SERIAL-partX` Niewielka zmiana nazw urządzeń lub układu partycjonowania i `/etc/crypttab` spowoduje wyświetlenie cennych danych podczas następnego rozruchu. To samo, jeśli korzystasz z PARTUUID, a następnie decydujesz się użyć tej partycji na coś innego, nie usuwając najpierw wpisu cryptTab.

Bardziej wiarygodne jest zidentyfikowanie właściwej partycji przez nadanie jej prawdziwego identyfikatora UUID lub LABEL. Domyślnie to nie działa, ponieważ dm-crypt i `mkswap` po prostu nadpisują dowolną zawartość na tej partycji, która usunie również UUID i LABEL; jednak możliwe jest określenie przesunięcia wymiany. Pozwala to na utworzenie bardzo małego, pustego, fałszywego systemu plików, który nie ma innego celu niż zapewnienie trwałego identyfikatora UUID lub LABEL do szyfrowania swap.

Utwórz [system plików](/index.php/Filesystem "Filesystem") z etykietą do wyboru:

```
# mkfs.ext2 -L *cryptswap* /dev/sd*X#* 1M

```

Niezwykły parametr po nazwie urządzenia ogranicza rozmiar systemu plików do 1 MiB, pozostawiając miejsce na zaszyfrowaną wymianę za nim.

 `# blkid /dev/sdX#`  `/dev/sdX#: LABEL="cryptswap" UUID="b72c384e-bd3c-49aa-b7a7-a28ea81a2605" TYPE="ext2"` 

Dzięki temu `/dev/sdX#` można łatwo zidentyfikować za pomocą UUID lub LABEL, niezależnie od tego, jak zmieni się nazwa urządzenia, a nawet numer partycji w przyszłości. Pozostały tylko pozycje `/etc/crypttab` i `/etc/fstab`:

 `/etc/crypttab` 
```
# <name> <device>         <password>    <options>
swap     LABEL=*cryptswap*  /dev/urandom  swap,offset=2048,cipher=aes-xts-plain64,size=512
```

Zauważ przesunięcie: to 2048 sektorów po 512 bajtów, czyli 1 MiB. W ten sposób zaszyfrowana wymiana nie wpłynie na LABEL / UUID systemu plików, a wyrównanie danych również się uda.

 `/etc/fstab` 
```
# <filesystem>    <dir>  <type>  <options>  <dump>  <pass>
/dev/mapper/swap  none   swap    defaults   0       0
```

Korzystając z tej konfiguracji, cryptswap spróbuje użyć partycji z odpowiednim LABELEM, niezależnie od tego, jaka może być jego nazwa. Jeśli zdecydujesz się użyć partycji do czegoś innego, przez sformatowanie jej również zniknie etykieta Cryptswap LABEL, więc cryptswap nie zastąpi jej podczas następnego rozruchu.

## Z obsługą hibernacji

Aby móc wznowić działanie po zawieszeniu komputera na dysku (hibernacja), należy zachować nienaruszoną przestrzeń wymiany. Dlatego wymagana jest wcześniejsza partycja wymiany LUKS lub plik, który można zapisać na dysku lub ręcznie wprowadzić przy uruchomieniu.

Następujące trzy metody są alternatywami do konfiguracji szyfrowanej wymiany dla hibernacji. Jeśli zastosujesz którąś z nich, pamiętaj, że krytyczne dane wymieniane przez system mogą potencjalnie pozostać w swapie przez długi okres (tj. Do momentu, gdy zostanie nadpisany). Aby zmniejszyć to ryzyko, rozważ utworzenie zadania systemowego, które ponownie szyfruje wymianę, np. za każdym razem, gdy system przechodzi do regularnego wyłączenia, wraz z wybraną metodą.

### LVM na LUKS

Prostym sposobem na zrealizowanie szyfrowanej wymiany z obsługą suspend-to-disk jest użycie zamiennego urządzenia [LVM](/index.php/LVM "LVM") na tej samej warstwie szyfrowania, co wolumin główny, dzięki czemu obie są otwierane podczas `encrypt` podczas startu. Postępuj zgodnie z instrukcjami na [Dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") a następnie po prostu [skonfiguruj wymagane parametry jądra](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate").

Zakładając, że ustawiłeś LVM na LUKS z woluminem logicznym swap (na przykład `/dev/MyStorage/swap`), wystarczy dodać wznowienie [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hook i dodać parametr jądra `resume=/dev/MyStorage/swap` do swojego programu ładującego. W przypadku [GRUB](/index.php/GRUB "GRUB") można to zrobić, dołączając ją do zmiennej `GRUB_CMDLINE_LINUX_DEFAULT` w `/etc/default/grub`.

 `/etc/default/grub`  `GRUB_CMDLINE_LINUX_DEFAULT="... resume=/dev/MyStorage/swap"` 

następnie uruchom `grub-mkconfig -o /boot/grub/grub.cfg` aby zaktualizować plik konfiguracyjny GRUB. Aby dodać mkinitcpio hook, edytuj następujący wiersz w pliku `mkinitcpio.conf`

 `/etc/mkinitcpio.conf`  `HOOKS=(... encrypt lvm2 **resume** ... filesystems ...)` 

następnie [zregeneruj initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

### mkinitcpio hook

**Note:** Ta sekcja ma zastosowanie tylko w przypadku używania haka do `encrypt`, który może odblokować tylko jedno urządzenie ([FS#23182](https://bugs.archlinux.org/task/23182)). Przy `sd-encrypt` wiele urządzeń może zostać odblokowanych (zobacz [Dm-crypt/System configuration#Using sd-encrypt hook](/index.php/Dm-crypt/System_configuration#Using_sd-encrypt_hook "Dm-crypt/System configuration")), ale automatyczne wykrywanie wymiany nie jest jeszcze dostępne. [systemd issue 4878](https://github.com/systemd/systemd/issues/4878)

Jeśli urządzenie zamieniające znajduje się na innym urządzeniu niż w systemie plików root, nie zostanie otwarte przez `encrypt` hook, tzn. Wznowienie nastąpi przed użyciem `/etc/crypttab`, dlatego wymagane jest utworzenie haka w /etc/mkinitcpio.conf, aby otworzyć urządzenie LUKS wymiany przed wznowieniem.

Jeśli chcesz użyć partycji, która jest aktualnie używana przez system, musisz ją najpierw wyłączyć:

```
# swapoff /dev/<device>

```

Upewnij się także, że usuniesz linię z `/etc/crypttab` wskazującą na to urządzenie.

Jeśli używasz ponownie istniejącej [partycji](/index.php/Partition "Partition") wymiany i jeśli partycja znajduje się w tabeli partycji GPT, musisz użyć gdisk, aby ustawić [atrybut partycji](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_entries_.28LBA_2-33.29 "wikipedia:GUID Partition Table") `63` "nie automount" na nim. Zapobiegnie to wykrywaniu przez system-gpt-auto-generator i włączaniu partycji podczas rozruchu.

Poniższa konfiguracja ma tę wadę, że podczas każdego rozruchu trzeba ręcznie wstawić dodatkowe hasło dla partycji wymiany.

**Warning:** Nie używaj tej konfiguracji z plikiem klucza, jeśli `/boot` nie jest zaszyfrowany. Przeczytaj o zgłoszonym tutaj [problemie](https://wiki.archlinux.org/index.php?title=Talk:Dm-crypt&oldid=255742#Suspend_to_disk_instructions_are_insecure). Ewentualnie użyj pliku klucza zaszyfrowanego gnupg zgodnie z [https://bbs.archlinux.org/viewtopic.php?id=120181](https://bbs.archlinux.org/viewtopic.php?id=120181)

Aby sformatować zaszyfrowany kontener dla partycji wymiany, utwórz klucz dla hasła użytkownika z pamięcią ustawień.

```
# cryptsetup luksFormat --type luks2 /dev/<device>

```

Otwórz partycję w `/dev/mapper`:

```
# cryptsetup open /dev/<device> swapDevice

```

Utwórz system plików wymiany wewnątrz zmapowanej partycji:

```
# mkswap /dev/mapper/swapDevice

```

Teraz musisz utworzyć hak, aby otworzyć swap podczas startu systemu. Możesz zainstalować i skonfigurować plik [mkinitcpio-openswap](https://aur.archlinux.org/packages/mkinitcpio-openswap/) lub postępować zgodnie z poniższymi instrukcjami. Utwórz plik przechwytujący zawierający polecenie open:

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    cryptsetup open /dev/<device> swapDevice
}

```

aby otworzyć urządzenie wymiany, wpisując hasło lub

 `/etc/initcpio/hooks/openswap` 
```
run_hook ()
{
    ## Optional: To avoid race conditions
    x=0;
    while [ ! -b /dev/mapper/<root-device> ] && [ $x -le 10 ]; do
       x=$((x+1))
       sleep .2
    done
    ## End of optional

    mkdir crypto_key_device
    mount /dev/mapper/<root-device> crypto_key_device
    cryptsetup open --key-file crypto_key_device/<path-to-the-key> /dev/<device> swapDevice
    umount crypto_key_device
}

```

do otwierania urządzenia wymiennego przez ładowanie pliku z zaszyfrowanego urządzenia root.

Na niektórych komputerach mogą wystąpić warunki wyścigu, gdy mkinitcpio spróbuje zamontować urządzenie przed procesem odszyfrowywania i wyliczenie urządzenia zostanie zakończone. Skomentowany blok opcjonalny opóźni proces rozruchu do 2 sekund, dopóki urządzenie główne nie będzie gotowe do zamontowania.

**Note:** Jeśli jest wymagana zamiana dysków SSD (Solid State Disk) i Discard / TRIM, opcja `--allow-discards` musi zostać dodana do linii cryptsetup w powyższym haku openswap. Zobacz [Dm-crypt/Specialties#Discard/TRIM support for solid state drives (SSD)](/index.php/Dm-crypt/Specialties#Discard/TRIM_support_for_solid_state_drives_(SSD) "Dm-crypt/Specialties") lub [SSD](/index.php/SSD "SSD") aby uzyskać więcej informacji na temat discard. Dodatkowo musisz dodać opcję montowania "discard" do wpisu fstab dla urządzenia wymiennego.

Następnie utwórz i edytuj plik konfiguracyjny przechwytywania:

 `/etc/initcpio/install/openswap` 
```
build ()
{
   add_runscript
}
help ()
{
cat<<HELPEOF
  This opens the swap encrypted partition /dev/<device> in /dev/mapper/swapDevice
HELPEOF
}

```

Dodaj hook `openswap` w tablicy HOOKS w pliku `/etc/mkinitcpio.conf`, przed `filesystem` ale po `encrypt`. Nie zapomnij dodać `resume` hak po `openswap`.

```
HOOKS=(... encrypt openswap resume filesystems ...)

```

[Regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

Dodaj zmapowaną partycję do `/etc/fstab`, dodając następujący linie

```
/dev/mapper/swapDevice swap swap defaults 0 0

```

Skonfiguruj system, aby wznowić działanie z `/dev/mapper/swapDevice`. Na przykład, jeśli używasz [GRUB](/index.php/GRUB "GRUB")-a z obsługą hibernacji jądra, dodaj parametr jądra `resume=/dev/mapper/swapDevice` do GRUB, dołączając go do zmiennej `GRUB_CMDLINE_LINUX_DEFAULT` w `/etc/default/grub`. Linia jądra z zaszyfrowanymi partycjami root i swap może wyglądać następująco:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/swapDevice ro

```

W czasie rozruchu hak `openswap` otworzy partycję wymiany, aby wznowić jądro. Jeśli używasz specjalnych haków do wznowienia ze stanu hibernacji, upewnij się, że są one umieszczone po `openswap` w tablicy `HOOKS`. Zauważ, że z powodu otwierania initrd, w tym przypadku nie ma wpisu dla swapDevice w `/etc/crypttab`.

### Używanie pliku wymiany

Plik swap może być użyty do zarezerwowania przestrzeni wymiany w obrębie istniejącej partycji i może być również ustawiony na partycji zaszyfrowanego bloku blokowego. Po wznowieniu z pliku wymiany, hak `resume` musi zostać dostarczony z hasłem, aby odblokować urządzenie, w którym znajduje się plik wymiany.

**Warning:** [Btrfs](/index.php/Dm-crypt/Drive_preparation#Btrfs_subvolumes "Dm-crypt/Drive preparation") nie obsługuje plików wymiany. Nieprzestrzeganie tego ostrzeżenia może spowodować uszkodzenie systemu plików. Podczas gdy plik wymiany może być używany na [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") po zamontowaniu przez loop device, spowoduje to poważnie pogorszoną wydajność swap .

Aby go utworzyć, najpierw wybierz zmapowaną partycję (np. `/dev/mapper/rootDevice`), której zamontowany system plików (np. `/`) Zawiera wystarczająco dużo wolnego miejsca, aby utworzyć plik wymiany o pożądanym rozmiarze.

Teraz [utwórz plik wymiany](/index.php/Swap#Swap_file_creation "Swap") (np. `/swapfile` wewnątrz zamontowanego systemu plików wybranej zmapowanej partycji. Pamiętaj, aby aktywować go za pomocą `swapon`, a następnie dodać go do pliku `/etc/fstab`. Zauważ, że poprzednia zawartość pliku wymiany pozostaje przezroczysta po ponownym uruchomieniu.

Skonfiguruj system, aby wznowić działanie z wybranej zmapowanej partycji. Na przykład, jeśli użyjesz [GRUB](/index.php/GRUB "GRUB")-a z obsługą hibernacji jądra, dodaj `resume=` wybraną zmapowaną partycję i `resume_offset=` zobacz polecenie obliczania poniżej do linii jądra w twojej konfiguracji GRUB (zazwyczaj w `/etc/default/grub`). Linia z zaszyfrowaną partycją root może wyglądać następująco:

```
kernel /vmlinuz-linux cryptdevice=/dev/sda2:rootDevice root=/dev/mapper/rootDevice resume=/dev/mapper/rootDevice resume_offset=123456789 ro

```

`resume_offset` pliku wymiany wskazuje na początek (zakres zero) pliku i można go zidentyfikować w następujący sposób:

```
# filefrag -v /swapfile | awk '{if($1=="0:"){print $4}}'

```

Dodaj hak do `resume` do pliku `etc/mkinitcpio.conf` i ponownie [wygeneruj initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs"):

```
HOOKS=(... encrypt **resume** ... filesystems ...)

```

Jeśli użyjesz klawiatury USB do wprowadzenia hasła odszyfrowania, moduł `keyboard` musi pojawić się przed hakiem do `encrypt`, jak pokazano poniżej. W przeciwnym razie nie będzie można uruchomić komputera, ponieważ nie można wprowadzić hasła deszyfrowania w celu odszyfrowania partycji root systemu Linux! (Jeśli nadal masz ten problem po dodaniu `keyboard`, wypróbuj `usbinput`, ale jest to przestarzałe).

```
HOOKS=(... **keyboard** encrypt ...)

```

## Znane problemy

*   `Stopped (with error) /dev/dm-1` in logs. See [systemd issue 1620](https://github.com/systemd/systemd/issues/1620).