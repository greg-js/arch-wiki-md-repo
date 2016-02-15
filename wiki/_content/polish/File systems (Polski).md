| **Streszczenie**  |
| Przegląd dostępnych systemów plików. |
| **Powiązane artykuły** |
| [Partycjonowanie](/index.php/Partitioning_(Polski) "Partitioning (Polski)") |

Za [Wikipedia](https://en.wikipedia.org/wiki/pl:System_plik%C3%B3w "wikipedia:pl:System plików"):

	_System plików - metoda przechowywania plików, zarządzania plikami, informacjami o tych plikach, tak by dostęp do plików i danych w nich zgromadzonych był łatwy dla użytkownika systemu._

Poszczególne partycje mogą używać jednego z wielu dostępnych systemów plików. Każdy z nich ma zalety, wady i unikalne cechy. Poniżej znajduje się jedynie krótki opis dostępnych systemów plików; dostępne są linki do wikipedii, które dostarczą więcej informacji.

## Contents

*   [1 Rodzaje systemów plików](#Rodzaje_system.C3.B3w_plik.C3.B3w)
    *   [1.1 Księgowanie](#Ksi.C4.99gowanie)
*   [2 Formatowanie partycji](#Formatowanie_partycji)
    *   [2.1 Przygotowanie](#Przygotowanie)
    *   [2.2 Krok 1: usunięcie starych partycji i stworzenie nowych](#Krok_1:_usuni.C4.99cie_starych_partycji_i_stworzenie_nowych)
    *   [2.3 Krok 2: utworzenie systemu plików](#Krok_2:_utworzenie_systemu_plik.C3.B3w)
        *   [2.3.1 W konsoli](#W_konsoli)
    *   [2.4 Narzędzia graficzne](#Narz.C4.99dzia_graficzne)

## Rodzaje systemów plików

*   [ext2](https://en.wikipedia.org/wiki/pl:ext2 "wikipedia:pl:ext2") **Second Extended Filesystem (Drugi rozszerzony system plików)** to szeroko przyjęty, dojrzały system plików GNU/Linuksa, który jest bardzo stabilny. Jego wadą jest to, że nie posiada wsparcia księgowania (zobacz poniżej) i barier. Brak księgowania może być przyczyną utraty danych w razie utraty zasilania lub błędu systemu. Użyty na partycjach `/` i `/home` może być uciążliwy, ponieważ jego sprawdzenie zajmuje dużo czasu. System plików ext2 może zostać przekonwertowany na ext3.
*   [ext3](https://en.wikipedia.org/wiki/pl:ext3 "wikipedia:pl:ext3") **Third Extended Filesystem (Trzeci rozszerzony system plików)** to rozszerzenie systemu ext2 o wsparcie księgowania i barier zapisu. Jest kompatybilny wstecz z ext2, dokładnie przetestowany i niezwykle stabilny.
*   [ext4](https://en.wikipedia.org/wiki/pl:ext4 "wikipedia:pl:ext4") **Fourth Extended Filesystem (Czwarty rozszerzony system plików)** to system plików częściowo kompatybilny z ext2 i ext3\. Obsługuje woluminy o rozmiarze do 1 eksabajta (tzn. 1 048 576 terabajtów) i pliki o rozmiarze do 16 terabajtów. Zwiększa limit ilości podkatalogów z 32 000 w ext3 do 64 000\. Oferuje także możliwość defragmentacji online.
*   [ReiserFS](https://en.wikipedia.org/wiki/ReiserFS "wikipedia:ReiserFS") (V3) Księgujący system plików zaprojektowany przez Hansa Reisera. Używa interesującej metody obsługi danych bazującej na niecodziennym algorytmie. ReiserFS jest uważany za bardzo szybki, szczególnie w przypadku obsługi wielu małych plików. ReiserFS jest szybki przy formatowaniu, jednak stosunkowo wolny przy montowaniu. Całkiem dojrzały i stabilny, jednak nie jest już aktywnie rozwijany. Uważany za dobry wybór dla partycji `/var`.
*   [JFS](https://en.wikipedia.org/wiki/pl:JFS "wikipedia:pl:JFS") **Journaled File System** stworzony przez IBM był pierwszym systemem plików z księgowaniem. Przed przeniesieniem do GNU/Linux przez wiele lat był rozwijany dla systemu operacyjnego IBM AIX®. JFS używa najmniej zasobów procesora ze wszystkim systemów plików. Jest bardzo szybki przy formatowaniu, montowaniu i sprawdzaniu (przez fsck). JFS oferuje dobrą wydajność szczególnie przy użyciu planisty I/O deadline. Nie jest tak szeroko wspierany jak systemy ext czy ReiserFS, jest jednak bardzo dojrzały i stabilny.
    **Note:** System plików JFS nie może zostać zmniejszony przez narzędzia dyskowe takie jak **gparted**.

*   [XFS](https://en.wikipedia.org/wiki/pl:XFS "wikipedia:pl:XFS") to kolejny system plików z księgowaniem. Został stworzony przez Silicon Graphics dla systemu operacyjnego IRIX i przeniesiony do GNU/Linux. Oferuje bardzo dobrą wydajność przy obsłudze dużych plików i partycji, jest bardzo szybki przy formatowaniu i montowaniu. Przy obsługiwaniu wielu małych plików posiada mniejszą wydajność niż inne systemy plików. XFS jest bardzo dojrzały i umożliwia defragmentację online.
    **Note:** System plików XFS nie może zostać zmniejszony przez narzędzia dyskowe takie jak **gparted**.

*   [vfat](https://en.wikipedia.org/wiki/vfat "wikipedia:vfat") **Virtual File Allocation Table** to prosty system plików obsługiwany przez praktycznie wszystkie systemy operacyjne. Z tego powodu jest dobrym wyborem np. dla kart pamięci i do przenoszenia danych pomiędzy różnymi systemami. VFAT obsługuje długie nazwy plików.
*   [Btrfs](/index.php?title=Btrfs_(Polski)&action=edit&redlink=1 "Btrfs (Polski) (page does not exist)") znany także jako "Better FS" (Lepszy FS), **Btrfs** to nowy system plików posiadający cechy podobne do świetnego systemu plików [ZFS](https://en.wikipedia.org/wiki/ZFS "wikipedia:ZFS") Sun/Oracle'a. Obejmują one migawki, obsługa programowego RAID bez mdadm, sumy konrolne, kopie przyrostowe i kompresję w locie pozwalającą na zwiększenie wydajności i zaoszczędzenie miejsca. Btrfs jest uważany za niestabilny (stan na sierpień 2012), został jednak włączony do źródeł kernela jako eksperymentalny. Btrfs jest przyszłym głównym systemem plików GNU/Linuksa i jest oferowany jako opcja podczas instalacji większości dystrybucji.
*   [nilfs2](https://en.wikipedia.org/wiki/pl:nilfs2 "wikipedia:pl:nilfs2") **New Implementation of a Log-structured File System (Nowa implementacja systemu plików o strukturze logu)** został stworzony przez NTT. Przechowuje wszystkie dane w formacie ciągłym (jak plik logu), gdzie dane są tylko dopisywane i nigdy nadpisywane. Został zaprojektowany aby zmniejszyć czas dostępu do danych i zminimalizować ryzyko utraty danych po błędzie systemu.
*   [Swap](/index.php?title=Swap_(Polski)&action=edit&redlink=1 "Swap (Polski) (page does not exist)") to system plików używany na partycjach wymiany.
*   NTFS - System plików używany przez Windows. Można go zamontować używając [NTFS-3G](/index.php?title=NTFS-3G_(Polski)&action=edit&redlink=1 "NTFS-3G (Polski) (page does not exist)").

### Księgowanie

Wszystkie powyższe systemy z wyjątkiem ext2 używają [[Wikipedia:pl:Księgowanie_(informatyka)|księgowania]. Księgowanie zapewnia ochronę przed błędami za pomocą zmian do dziennika zanim zostaną wprowadzone do systemu plików. W przypadku błędu systemu lub zaniku zasilania, takie systemy są szybciej montowane i mniej podatne na uszkodzenia. Dziennik znajduje się w zarezerwowanej przestrzeni systemu plików.

Nie wszystkie metody księgowania są takie same. Tylko ext3 i ext4 oferują księgowanie danych (ang. data-mode journalling), które księguje zarówno dane, jak i metadane. Księgowanie danych powoduje zmniejszenie wydajności i nie jest włączone domyślnie. Inne systemy plików oferują tylko księgowanie metadanych (ang. ordered-mode journalling). Podczas gdy każde księgowanie przywróci system plików do poprawnego stanu po błędzie, księgowanie danych oferuje lepszą ochronę przed zepsuciem i utratą danych. Jest to kompromis dotyczący wydajności systemu, ponieważ księgowanie danych wymaga dwóch operacji: zapisu do dziennika i potem na dysk. Wydajność i bezpieczeństwo powinny być brane pod uwagę przy wyborze systemu plików.

## Formatowanie partycji

**Warning:** Formatowanie niszczy dane znajdujące się na urządzeniu, pamiętaj o sporządzeniu kopii ważnych danych.

**Note:** Autorzy tego artykułu nie odpowiadają za utratę danych, uszkodzenia sprzętu i inne problemy wynikłe ze stosowania się do tego artykułu.

### Przygotowanie

Zanim zaczniesz, musisz znać nazwę urządzenia nadaną przez system Linux. Dyski twarde i pendrive'y są nazywane `/dev/sd_x_`, gdzie "x" to mała litera, a partycje są nazywane `/dev/sd_xY_`, gdzie "Y" to numer.

Jeśli urządzenie, które chcesz sformatować jest zamontowane, pojawi się w kolumnie _MOUNTPOINT_ po wydaniu polecenia:

```
$ lsblk

```

Jeśli urządzenie nie jest zamontowane:

```
# mount /dev/sd_xY_ /jakis/katalog

```

Żeby je odmontować, możesz użyć _umount_ na katalogu gdzie zamontowałeś(aś) urządzenie:

```
# umount /jakis/katalog

```

**Note:** Twoje urządzenie musi być odmontowane aby je sformatować i utworzyć system plików.

### Krok 1: usunięcie starych partycji i stworzenie nowych

Do tego możesz użyć `fdisk` (dla MBR) lub `gdisk` (dla GPT):

```
# fdisk /dev/_<urzadzenie>_

```

**Note:** Wpisz `m`, aby uzyskać listę dostępnych komend.

### Krok 2: utworzenie systemu plików

#### W konsoli

Aby stworzyć system plików, musisz użyć `mkfs`:

```
# mkfs -t ext4 /dev/_<partycja>_

```

`mkfs` to nakładka na różne narzędzia `mkfs._typ_`. Musisz zainstalować pakiety dostarczające narzędzia dla systemów plików, które chcesz użyć:

*   [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) dostarcza `btrfs`
*   [e2fsprogs](https://www.archlinux.org/packages/?name=e2fsprogs) dostarcza `ext2`, `ext3` i `ext4`
*   [jfsutils](https://www.archlinux.org/packages/?name=jfsutils) dostarcza `jfs`
*   [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g) dostarcza `ntfs`
*   [reiserfsprogs](https://www.archlinux.org/packages/?name=reiserfsprogs) dostarcza `reiserfs`
*   [dosfstools](https://www.archlinux.org/packages/?name=dosfstools) dostarcza `vfat` (znany także jako `msdos`)
*   [xfsprogs](https://www.archlinux.org/packages/?name=xfsprogs) dostarcza `xfs`

### Narzędzia graficzne

Dostępnych jest kilka narzędzi graficznych do zarządzania partycjami:

*   [GParted](http://gparted.sourceforge.net/) (GTK) jest dostępny w [extra]
*   [gnome-disk-utility](https://www.archlinux.org/packages/?name=gnome-disk-utility)
*   [KDE Partition Manager](http://www.kde-apps.org/content/show.php/KDE+Partition+Manager?content=89595) (KDE/Qt) jest dostępny w [AUR](/index.php/AUR_(Polski) "AUR (Polski)")