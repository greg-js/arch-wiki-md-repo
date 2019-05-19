Przed zaszyfrowaniem dysku zaleca się bezpieczne wymazanie dysku poprzez nadpisanie całego dysku losowymi danymi. Aby zapobiec atakom kryptograficznym lub niepożądanemu [odzyskiwaniu plików](/index.php/File_recovery "File recovery"), dane te są idealnie nie do odróżnienia od danych później napisanych przez dm-crypt. Aby uzyskać bardziej wyczerpującą dyskusję zobacz [Disk encryption (Polski)#Przygotowanie dysku](/index.php/Disk_encryption_(Polski)#Przygotowanie_dysku "Disk encryption (Polski)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Bezpieczne usuwanie danych z dysku twardego](#Bezpieczne_usuwanie_danych_z_dysku_twardego)
    *   [1.1 Metody ogólne](#Metody_ogólne)
    *   [1.2 Metody specyficzne dla dm-crypt](#Metody_specyficzne_dla_dm-crypt)
        *   [1.2.1 dm-crypt wymazuje pusty dysk lub partycję](#dm-crypt_wymazuje_pusty_dysk_lub_partycję)
        *   [1.2.2 dm-crypt czyści po instalacji wolne miejsce](#dm-crypt_czyści_po_instalacji_wolne_miejsce)
        *   [1.2.3 Wytrzyj nagłówek LUKS](#Wytrzyj_nagłówek_LUKS)
*   [2 Partycjonowanie](#Partycjonowanie)
    *   [2.1 Partycje fizyczne](#Partycje_fizyczne)
    *   [2.2 Ułożone urządzenia blokowe](#Ułożone_urządzenia_blokowe)
    *   [2.3 Btrfs subvolumes](#Btrfs_subvolumes)
    *   [2.4 Boot partition (GRUB)](#Boot_partition_(GRUB))

## Bezpieczne usuwanie danych z dysku twardego

Podczas wybierania metody bezpiecznego usuwania dysku twardego należy pamiętać, że należy to zrobić tylko raz, dopóki dysk jest używany jako dysk zaszyfrowany.

**Warning:** Dokonaj odpowiednich kopii zapasowych cennych danych przed uruchomieniem!

**Note:** Podczas usuwania dużej ilości danych proces może potrwać od kilku godzin do kilku dni.

**Tip:**

*   Proces wypełniania zaszyfrowanego dysku może potrwać nawet dzień, zanim zostanie ukończony na dysku wieloterabajtowym. Aby nie pozostawić maszyny bezużytecznej podczas pracy, warto ją wykonać z systemu już zainstalowanego na innym dysku, a nie z systemu instalacji Arch na żywo.
*   W przypadku dysków [SSD](/index.php/SSD "SSD"), aby zminimalizować artefakty pamięci podręcznej [pamięci flash](/index.php/Securely_wipe_disk#Flash_memory "Securely wipe disk"), rozważ wykonanie [czyszczenia komórki SSD](/index.php/SSD_memory_cell_clearing "SSD memory cell clearing") przed wykonaniem poniższych instrukcji.

### Metody ogólne

Aby uzyskać szczegółowe instrukcje na temat usuwania i przygotowania dysku, przeczytaj [Bezpiecznie wymaż dysk](/index.php/Securely_wipe_disk "Securely wipe disk").

### Metody specyficzne dla dm-crypt

Poniższe dwie metody są specyficzne dla dm-crypt i są wymienione, ponieważ są bardzo szybkie i mogą być wykonywane również po konfiguracji partycji.

[cryptsetup FAQ](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects) opisuje bardzo prostą procedurę użycia istniejącej woluminu dm-crypt do usunięcia całej dostępnej wolnej przestrzeni na bazowym urządzeniu blokowym za pomocą losowych danych, działając jako prosty generator liczb pseudolosowych. Ma również chronić przed ujawnieniem wzorców użytkowania. Dzieje się tak dlatego, że zaszyfrowane dane są praktycznie nie do odróżnienia od przypadkowych.

#### dm-crypt wymazuje pusty dysk lub partycję

Najpierw utwórz tymczasowy zaszyfrowany kontener na partycji (`sdXY`) lub pełny dysk (`sdX`) do zaszyfrowania, np. przy użyciu domyślnych parametrów szyfrowania i losowego klucza za pośrednictwem `--key-file /dev/{u}random` opcja (patrz także [Random number generation](/index.php/Random_number_generation "Random number generation")):

```
# cryptsetup open --type plain /dev/sdXY container --key-file /dev/random

```

Po drugie, sprawdź, czy istnieje:

 `# fdisk -l` 
```
Disk /dev/mapper/container: 1000 MB, 1000277504 bytes
...
Disk /dev/mapper/container does not contain a valid partition table
```

Przetrzyj pojemnik zerami. Użycie funkcji `if=/dev/urandom` nie jest wymagane, ponieważ do losowości wykorzystywany jest szyfr.

 `# dd if=/dev/zero of=/dev/mapper/container status=progress`  `dd: writing to ‘/dev/mapper/container’: No space left on device` 
**Tip:**

*   Używanie *dd* z opcją `bs=`, np. `bs=1M`, jest często używany w celu zwiększenia przepustowości operacji na dysku.
*   Aby wykonać sprawdzenie operacji, wyzeruj partycję przed utworzeniem pojemnika czyszczenia. Po poleceniu czyszczenia `blockdev --getsize64 */dev/mapper/container*`może być użyty do uzyskania dokładnego rozmiaru kontenera jako root. Teraz można użyć do sprawdzenia, czy czyszczenie zastąpiło wyzerowane sektory, np. `od -j *containersize - blocksize*` aby zobaczyć czy czyszczenie dobiegło końca.

Na koniec zamknij tymczasowy kontener:

```
# cryptsetup close container

```

Podczas szyfrowania całego systemu, kolejnym krokiem jest [#Partitioning](#Partitioning). Jeśli szyfrujesz tylko partycję, kontynuuj [dm-crypt/Encrypting a non-root file system (Polski)#Partycja](/index.php/Dm-crypt/Encrypting_a_non-root_file_system_(Polski)#Partycja "Dm-crypt/Encrypting a non-root file system (Polski)").

#### dm-crypt czyści po instalacji wolne miejsce

Użytkownicy, którzy nie mieli czasu na procedurę czyszczenia przed [instalacją](/index.php/Dm-crypt/Encrypting_an_entire_system "Dm-crypt/Encrypting an entire system"), może osiągnąć podobny efekt po uruchomieniu zaszyfrowanego systemu i zamontowaniu systemów plików. Należy jednak rozważyć, czy dany system plików mógł skonfigurować zarezerwowane miejsce, np. dla użytkownika root lub innego [disk quota](/index.php/Disk_quota "Disk quota") mechanizm, który może ograniczyć czyszczenie nawet w przypadku wykonywania przez użytkownika root: niektóre części podstawowego urządzenia blokowego mogą nie zostać w ogóle zapisane.

Aby wykonać operację czyszczenia, tymczasowo wypełnij pozostałą wolną przestrzeń partycji, pisząc do pliku wewnątrz zaszyfrowanego kontenera:

 `# dd if=/dev/zero of=/file/in/container status=progress`  `dd: writing to ‘/file/in/container’: No space left on device` 

Sync the cache to disk and then delete the file to reclaim the free space.

```
# sync
# rm /file/in/container

```

Powyższy proces należy powtórzyć dla każdego utworzonego bloku partycji i systemu plików. Na przykład konfiguracja [LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system"), proces musi zostać wykonany dla każdego woluminu logicznego.

#### Wytrzyj nagłówek LUKS

Partycje sformatowane za pomocą dm-crypt/LUKS zawierają nagłówek z użytymi opcjami szyfrowania i krypt, które są określane jako `dm-mod` podczas otwierania bloku. Po nagłówku rozpoczyna się faktyczna losowa partycja danych. W związku z tym, przy ponownym instalowaniu na już losowym napędzie lub demontażu jednego (np. Sprzedaż komputera, przełączanie napędów itd.) Może to być wystarczające, aby wyczyścić nagłówek partycji, zamiast nadpisywać cały dysk - który może być długim procesem.

Wyczyszczenie nagłówka LUKS spowoduje usunięcie klucza głównego zaszyfrowanego PBKDF2 (AES), soli i tak dalej.

**Note:** Ważne jest, aby pisać na zaszyfrowanej partycji LUKS (`/dev/sdX**1**` w tym przykładzie) a nie bezpośrednio do węzła urządzenia dysków. Konfiguruje szyfrowanie jako warstwę odwzorowującą urządzenia na innych, np. LVM na LUKS na macierzy RAID powinien następnie odpowiednio napisać do RAID.

Nagłówek z jedną domyślną pamięcią kluczy o wielkości 256 bitów ma rozmiar 1024 KB. Zaleca się również nadpisanie pierwszego 4KiB napisanego przez dm-crypt, więc trzeba wyczyścić 1028 KB. To jest `1052672` bajtów.

Aby użyć przesunięcia punktu zerowego:

```
# head -c 1052672 /dev/urandom > */dev/sdX1*; sync

```

Dla 512-bitowej długości klucza (na przykład dla aes-xts-plain z 512-bitowym kluczem) nagłówek zajmuje 2 MB. Nagłówek LUKS2 4MiB.

Jeśli masz wątpliwości, po prostu bądź hojny i nadpisaj pierwsze 10 MB.

```
# dd if=/dev/urandom of=*/dev/sdX1* bs=512 count=20480

```

**Note:** Kopie zapasowe danych nagłówka mogą zostać uratowane, ale system plików prawdopodobnie został uszkodzony, ponieważ pierwsze zaszyfrowane sektory zostały nadpisane. Zobacz dalsze sekcje, jak wykonać kopię zapasową kluczowych bloków nagłówka.

Podczas wycierania nagłówka losowymi danymi wszystko, co pozostało na urządzeniu, jest zaszyfrowane. W przypadku dysku SSD może wystąpić wyjątek z powodu bloków pamięci podręcznej używanych przez dyski SSD. Teoretycznie może się zdarzyć, że nagłówek był w nich buforowany jakiś czas wcześniej, a ta kopia może być nadal dostępna po wyczyszczeniu oryginalnego nagłówka. Ze względów bezpieczeństwa należy wykonać bezpieczne wymazywanie dysku SSD z dysku SSD (procedura proszę zobaczysz [FAQ 5.19](https://gitlab.com/cryptsetup/cryptsetup/wikis/FrequentlyAskedQuestions#5-security-aspects)).

## Partycjonowanie

Ta sekcja ma zastosowanie tylko podczas szyfrowania całego systemu. Po tym, jak napęd został (i) bezpiecznie nadpisany, właściwy schemat partycjonowania będzie musiał zostać dokładnie wybrany, biorąc pod uwagę wymagania dm-crypt oraz efekty, jakie różne wybory będą miały na zarządzanie systemem wynikowym.

Ważne jest, aby od razu zauważyć, że w [prawie](#Boot_partition_(GRUB)) każdym przypadku musi istnieć osobna partycja dla / boot, która musi pozostać niezaszyfrowana, ponieważ bootloader musi uzyskać dostęp do katalogu / boot, gdzie załaduje moduły initramfs / encryption potrzebne do załadowania reszta systemu (szczegóły patrz [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")). Jeśli to podniesie obawy dotyczące bezpieczeństwa, patrz

Kolejnym ważnym czynnikiem, który należy wziąć pod uwagę, jest sposób obsługi obszaru wymiany i zawieszenia systemu, patrz [dm-crypt/Swap encryption](/index.php/Dm-crypt/Swap_encryption "Dm-crypt/Swap encryption").

### Partycje fizyczne

W najprostszym przypadku zaszyfrowane warstwy mogą być oparte bezpośrednio na fizycznych partycjach; zobacz Partycjonowanie metod ich tworzenia. Podobnie jak w systemie niezaszyfrowanym, wystarczająca jest partycja główna, oprócz innej dla `/boot` jak wspomniano wyżej. Ta metoda pozwala decydować, które partycje szyfrować, a które pozostawić niezaszyfrowane, i działa tak samo bez względu na liczbę dysków. Możliwe będzie również dodawanie lub usuwanie partycji w przyszłości, ale zmiana rozmiaru partycji będzie ograniczona wielkością hosta dysku. Na koniec zwróć uwagę, że do otwarcia każdej zaszyfrowanej partycji wymagane są osobne hasła lub klucze, mimo że można to zautomatyzować podczas uruchamiania z użyciem `crypttab` plik, patrz [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration").

### Ułożone urządzenia blokowe

Jeśli potrzebna jest większa elastyczność, dm-crypt może współistnieć z innymi urządzeniami blokowymi, takimi jak [LVM](/index.php/LVM "LVM") i [RAID](/index.php/RAID "RAID"). Zaszyfrowane pojemniki mogą znajdować się poniżej lub na innych urządzeniach blokowych:

*   Jeśli urządzenia LVM / RAID zostaną utworzone na wierzchu zaszyfrowanej warstwy, będzie można swobodnie dodawać, usuwać i zmieniać rozmiary systemów plików tej samej zaszyfrowanej partycji, a tylko jeden klucz lub hasło będzie wymagane dla nich wszystkich. Ponieważ zaszyfrowana warstwa znajduje się na partycji fizycznej, nie będzie możliwe wykorzystanie możliwości LVM i RAID do obsługi wielu dysków.
*   Jeśli zaszyfrowana warstwa zostanie utworzona na urządzeniach LVM / RAID, nadal będzie możliwa reorganizacja systemów plików w przyszłości, ale z dodatkową złożonością, ponieważ warstwy szyfrowania będą musiały zostać odpowiednio dostosowane. Ponadto do otwarcia każdego zaszyfrowanego urządzenia będą wymagane osobne hasła lub klucze. Jest to jednak jedyny wybór w przypadku systemów, które wymagają zaszyfrowanych systemów plików, aby obejmowały wiele dysków.

### Btrfs subvolumes

Wbudowana funkcja [podpolumn Btrfs](/index.php/Btrfs#Subvolumes "Btrfs") może być używana z dm-crypt, całkowicie zastępując potrzebę LVM, jeśli nie są wymagane żadne inne systemy plików. Należy jednak pamiętać, że pliki wymiany nie są obsługiwane przez brtrfs, więc jeśli wymagana jest partycja wymiany, konieczna jest szyfrowana partycja wymiany.

### Boot partition (GRUB)

Zobacz [dm-crypt/Encrypting an entire system (Polski)#Szyfrowana partycja rozruchowa (GRUB)](/index.php/Dm-crypt/Encrypting_an_entire_system_(Polski)#Szyfrowana_partycja_rozruchowa_(GRUB) "Dm-crypt/Encrypting an entire system (Polski)").