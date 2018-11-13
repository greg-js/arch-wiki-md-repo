From [Wikipedia:Logical Volume Manager (Linux)](https://en.wikipedia.org/wiki/Logical_Volume_Manager_(Linux) "wikipedia:Logical Volume Manager (Linux)"):

	LVM is a [logicznym menedżerem woluminów](https://en.wikipedia.org/wiki/logical_volume_management "wikipedia:logical volume management") dla [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel"); zarządza dyskami i podobnymi urządzeniami pamięci masowej.

## Contents

*   [1 LVM Building Blocks](#LVM_Building_Blocks)
*   [2 Zalety](#Zalety)
*   [3 Wady](#Wady)
*   [4 Instalowanie Arch Linux na LVM](#Instalowanie_Arch_Linux_na_LVM)
    *   [4.1 Utwórz partycje](#Utwórz_partycje)
    *   [4.2 Utwórz woluminy fizyczne](#Utwórz_woluminy_fizyczne)
    *   [4.3 Utwórz grupę woluminów](#Utwórz_grupę_woluminów)
    *   [4.4 Utwórz w jednym kroku](#Utwórz_w_jednym_kroku)
    *   [4.5 Utwórz woluminy logiczne](#Utwórz_woluminy_logiczne)
    *   [4.6 Twórz systemy plików i montowanie woliminów logicznych](#Twórz_systemy_plików_i_montowanie_woliminów_logicznych)
    *   [4.7 Skonfiguruj mkinitcpio](#Skonfiguruj_mkinitcpio)
    *   [4.8 Opcje jądra](#Opcje_jądra)
*   [5 Volume operations](#Volume_operations)
    *   [5.1 Zaawansowane opcje](#Zaawansowane_opcje)
    *   [5.2 Zmienianie wielkości woluminów](#Zmienianie_wielkości_woluminów)
        *   [5.2.1 woluminów fizycznych](#woluminów_fizycznych)
            *   [5.2.1.1 Growing](#Growing)
            *   [5.2.1.2 Shrinking](#Shrinking)
                *   [5.2.1.2.1 Move physical extents](#Move_physical_extents)
                *   [5.2.1.2.2 Zmień rozmiar woluminu fizycznego](#Zmień_rozmiar_woluminu_fizycznego)
                *   [5.2.1.2.3 Zmień rozmiar partycji](#Zmień_rozmiar_partycji)
        *   [5.2.2 Logical volumes](#Logical_volumes)
            *   [5.2.2.1 Growing or shrinking with lvresize](#Growing_or_shrinking_with_lvresize)
            *   [5.2.2.2 Rozszerzanie woluminu logicznego i systemu plików za jednym razem](#Rozszerzanie_woluminu_logicznego_i_systemu_plików_za_jednym_razem)
            *   [5.2.2.3 Zmiana rozmiaru systemu plików oddzielnie](#Zmiana_rozmiaru_systemu_plików_oddzielnie)
    *   [5.3 Remove logical volume](#Remove_logical_volume)
    *   [5.4 Dodaj wolumin fizyczny do grupy woluminów](#Dodaj_wolumin_fizyczny_do_grupy_woluminów)
    *   [5.5 Usuń partycję z grupy woluminów](#Usuń_partycję_z_grupy_woluminów)
    *   [5.6 Dezaktywuj grupę woluminów](#Dezaktywuj_grupę_woluminów)
*   [6 Typy woluminów logicznych](#Typy_woluminów_logicznych)
    *   [6.1 Migawki](#Migawki)
        *   [6.1.1 Konfiguracja](#Konfiguracja)
    *   [6.2 LVM cache](#LVM_cache)
        *   [6.2.1 Create cache](#Create_cache)
        *   [6.2.2 Usuń pamięć podręczną](#Usuń_pamięć_podręczną)
    *   [6.3 RAID](#RAID)
        *   [6.3.1 Konfiguracja RAID](#Konfiguracja_RAID)
        *   [6.3.2 Skonfiguruj mkinitcpio dla RAID](#Skonfiguruj_mkinitcpio_dla_RAID)
*   [7 Graficzna konfiguracja](#Graficzna_konfiguracja)
*   [8 Rozwiązywanie problemów](#Rozwiązywanie_problemów)
    *   [8.1 Zmiany, które mogą być wymagane ze względu na zmiany w domyślnych ustawieniach Arch-Linux](#Zmiany,_które_mogą_być_wymagane_ze_względu_na_zmiany_w_domyślnych_ustawieniach_Arch-Linux)
    *   [8.2 Komendy LVM nie działają](#Komendy_LVM_nie_działają)
    *   [8.3 Woluminy logiczne się nie wyświetlają](#Woluminy_logiczne_się_nie_wyświetlają)
    *   [8.4 LVM na nośnikach wymiennych](#LVM_na_nośnikach_wymiennych)
    *   [8.5 Zmiana rozmiaru sąsiedniego woluminu logicznego kończy się niepowodzeniem](#Zmiana_rozmiaru_sąsiedniego_woluminu_logicznego_kończy_się_niepowodzeniem)
    *   [8.6 Polecenie "grub-mkconfig" zgłasza błędy "unknown filesystem" errors](#Polecenie_"grub-mkconfig"_zgłasza_błędy_"unknown_filesystem"_errors)
    *   [8.7 Thinly-provisioned root volume device times out](#Thinly-provisioned_root_volume_device_times_out)
    *   [8.8 Opóźnienie przy wyłączaniu](#Opóźnienie_przy_wyłączaniu)
*   [9 Zobacz też](#Zobacz_też)

## LVM Building Blocks

Logical Volume Management wykorzystuje jądro [device-mapper](http://sources.redhat.com/dm/) funkcja zapewniająca system partycji niezależny od układu dysku. Za pomocą LVM można zarchiwizować pamięć i utworzyć "wirtualne partycje [extending/shrinking](#Resizing_volumes) łatwiejsze (z zastrzeżeniem potencjalnych ograniczeń systemu plików).

Wirtualne partycje umożliwiają dodawanie i usuwanie bez martwienia się o to, czy masz wystarczająco dużo sąsiadującej przestrzeni na danym dysku, oraz o złapanie fdiskowania używanego dysku (i zastanawiasz się, czy jądro używa starej lub nowej tabeli partycji), czy też przeniesienie innego przegródki na uboczu. Jest to rozwiązanie łatwe w zarządzaniu: LVM nie dodaje żadnych zabezpieczeń.

Basic building blocks of LVM:

	Physical volume (PV)

	Partycja na dysku twardym (lub nawet sam dysk lub plik sprzężenia zwrotnego), na którym można tworzyć grupy woluminów. Ma specjalny nagłówek i dzieli się na zakres fizyczny. Pomyśl o objętościach fizycznych jako dużych elementach konstrukcyjnych używanych do budowy dysku twardego.

	Volume group (VG)

	Grupa woluminów fizycznych używanych jako wolumin pamięci (jako jeden dysk). Zawierają woluminy logiczne. Pomyśl o grupach woluminów jako dyskach twardych.

	Logical volume (LV)

	*Partycja wirtualna/logiczna*, która znajduje się w grupie woluminów i składa się z obszarów fizycznych. Pomyśl o woluminach logicznych jako normalnych partycjach.

	Physical extent (PE)

	Najmniejszy rozmiar woluminu fizycznego, który można przypisać do woluminu logicznego (domyślnie 4 MiB). Pomyśl o rozmiarach fizycznych jako częściach dysków, które można przydzielić do dowolnej partycji.

Przykład:

```
**Physical disks**

  Disk1 (/dev/sda):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partition1 50 GiB (Physical volume) |Partition2 80 GiB (Physical volume)     |
    |/dev/sda1                           |/dev/sda2                               |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ |

  Disk2 (/dev/sdb):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Partition1 120 GiB (Physical volume)                 |
    |/dev/sdb1                                            |
    |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

```
**LVM logical volumes**

  Volume Group1 (/dev/MyStorage/ = /dev/sda1 + /dev/sda2 + /dev/sdb1):
     _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _
    |Logical volume1 15 GiB  |Logical volume2 35 GiB      |Logical volume3 200 GiB              |
    |/dev/MyStorage/rootvol  |/dev/MyStorage/homevol      |/dev/MyStorage/mediavol              |
    |_ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ |_ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _ _|

```

## Zalety

LVM zapewnia większą elastyczność niż zwykłe partycje dysku twardego:

*   Użyj dowolnej liczby dysków jako jednego dużego dysku.
*   Mieć woluminy logiczne rozciągnięte na kilku dyskach.
*   Twórz małe woluminy logiczne i zmieniaj ich rozmiar "dynamicznie" w miarę zapełniania.
*   Zmień wielkość woluminów logicznych, niezależnie od ich kolejności na dysku. Nie zależy od położenia LV w VG, nie ma potrzeby zapewnienia otaczającej dostępnej przestrzeni.
*   Zmień rozmiar/utwórz/usuń logiczne i fizyczne woluminy online. Systemy plików na nich nadal wymagają zmiany rozmiaru, ale niektóre (takie jak ext4) obsługują zmianę rozmiaru online.
*   Migracja online/na żywo LV używana przez usługi na różnych dyskach bez konieczności restartowania usług.
*   Migawki umożliwiają tworzenie kopii zapasowej zamrożonej kopii systemu plików, przy jednoczesnym ograniczeniu przestojów serwisowych do minimum.
*   Obsługa różnych urządzeń device-mapper, w tym przejrzyste szyfrowanie i buforowanie często używanych danych. Umożliwia to utworzenie systemu z (jednym lub więcej) dyskami fizycznymi (zaszyfrowanymi za pomocą LUKS) i [LVM on top](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") aby umożliwić łatwą zmianę rozmiaru i zarządzanie oddzielnymi woluminami (np `/`, `/home`, `/backup`, etc.) bez kłopotów z wielokrotnym wprowadzaniem klucza podczas startu.

## Wady

*   Dodatkowe kroki w konfiguracji systemu, bardziej skomplikowane.
*   Jeśli masz podwójne uruchamianie, zwróć uwagę, że system Windows nie obsługuje LVM; nie będzie można uzyskać dostępu do żadnych partycji LVM z systemu Windows.

## Instalowanie Arch Linux na LVM

You should create your LVM Volumes between the [partitioning](/index.php/Partitioning "Partitioning") and [formatting](/index.php/File_systems#Create_a_file_system "File systems") steps of the [installation procedure](/index.php/Installation_guide "Installation guide"). Zamiast bezpośrednio formatować partycję, która ma być głównym systemem plików, system plików zostanie utworzony wewnątrz woluminu logicznego (LV).

Upewnij się, że [lvm2](https://www.archlinux.org/packages/?name=lvm2) pakiet to [installed](/index.php/Install "Install").

Szybki przegląd:

*   Utwórz partycję(s), w której będą przechowywane twoje PV (s).
    *   Jeśli używasz tabeli partycji Master Boot Record, ustaw opcję [partition type ID](https://en.wikipedia.org/wiki/Partition_type "wikipedia:Partition type") do `8e` (typ partycji `Linux LVM` w *fdisk*).
    *   Jeśli używasz tabeli partycji GUID, ustaw opcję [partition type GUID](https://en.wikipedia.org/wiki/GUID_Partition_Table#Partition_type_GUIDs "wikipedia:GUID Partition Table") do `E6D6D379-F507-44C2-A23C-238F2A3DF928` (typ partycji `Linux LVM` w *fdisk* i `8e00` w *gdisk*).
*   Utwórz swoje woluminy fizyczne (PV). Jeśli masz jeden dysk, najlepiej jest po prostu utworzyć jeden PV w jednej dużej partycji. Jeśli masz wiele dysków, możesz utworzyć partycje na każdym z nich i utworzyć PV na każdej partycji.
*   Utwórz swoją grupę woluminów (VG) i dodaj do niej wszystkie PV.
*   Utwórz woluminy logiczne (LVs) wewnątrz tego VG.
*   kontynuuj [Installation guide#Format the partitions](/index.php/Installation_guide#Format_the_partitions "Installation guide").
*   Po przejściu do “Create initial ramdisk environment” w przewodniku instalacji, dodaj `lvm` hak do `/etc/mkinitcpio.conf` (patrz poniżej, aby uzyskać szczegółowe informacje).

**Warning:** `/boot` nie może znajdować się w LVM, gdy używa się programu ładującego, który nie obsługuje LVM; musisz utworzyć oddzielną partycję `/boot` i sformatować ją bezpośrednio. Tylko [GRUB](/index.php/GRUB "GRUB") jest znany z obsługi LVM.

### Utwórz partycje

Jeśli LVM musi być ustawiony na całym dysku, nie ma potrzeby tworzenia żadnych partycji.

W przeciwnym razie przed przystąpieniem do konfigurowania LVM [podziel](/index.php/Partition "Partition") dysk według potrzeb.

### Utwórz woluminy fizyczne

Aby wyświetlić listę wszystkich urządzeń, które można wykorzystać jako wolumin fizyczny:

```
# lvmdiskscan

```

**Warning:** Upewnij się, że wybierasz w odpowiednie urządzenie, poniższe polecenie spowoduje utratę danych!

Utwórz wolumin fizyczny na nich:

```
# pvcreate *DEVICE*

```

To polecenie tworzy nagłówek na każdym urządzeniu, dzięki czemu można go użyć do LVM. Jak określono w [#LVM Building Blocks](#LVM_Building_Blocks), *DEVICE* może być dyskiemk (na przykład `/dev/sda`), partycja (np. `/dev/sda2`) lub urządzenie loop back. Na przykład:

```
# pvcreate /dev/sda2

```

Możesz śledzić utworzone woluminy fizyczne za pomocą:

```
# pvdisplay

```

**Note:** Jeśli używasz dysku SSD bez wcześniejszego partycjonowania, użyj `pvcreate --dataalignment 1m /dev/sda` (for erase block size < 1 MiB), patrz np. [here](http://serverfault.com/questions/356534/ssd-erase-block-size-lvm-pv-on-raw-device-alignment)

### Utwórz grupę woluminów

Następnym krokiem jest utworzenie grupy woluminów na tym woluminie fizycznym.

Najpierw musisz utworzyć grupę woluminów na jednym z woluminów fizycznych:

```
# vgcreate <*volume_group*> <*physical_volume*>

```

Na przykład:

```
# vgcreate VolGroup00 /dev/sda2

```

Następnie dodaj do niego wszystkie inne woluminy fizyczne, które chcesz w nim umieścić:

```
# vgextend <*volume_group*> <*physical_volume*>
# vgextend <*volume_group*> <*another_physical_volume*>
# ...

```

Na przykład:

```
# vgextend VolGroup00 /dev/sdb1
# vgextend VolGroup00 /dev/sdc

```

Możesz śledzić, jak powiększa się grupa woluminów:

```
# vgdisplay

```

**Note:** Jeśli chcesz, możesz utworzyć więcej niż jedną grupę woluminów, ale wtedy cała pamięć nie będzie prezentowana jako jeden dysk.

### Utwórz w jednym kroku

LVM umożliwia łączenie tworzenia grupy woluminów i woluminów fizycznych w jednym prostym kroku. Na przykład, aby utworzyć grupę VolGroup00 z trzema wymienionymi wyżej urządzeniami, możesz uruchomić:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb1 /dev/sdc

```

To polecenie najpierw skonfiguruje trzy partycje jako woluminy fizyczne (jeśli to konieczne), a następnie utworzy grupę woluminów z trzema woluminami. Polecenie ostrzeże Cię, wykrywa istniejący system plików na dowolnym urządzeniu.

### Utwórz woluminy logiczne

**Tip:** Jeśli chcesz używać migawek, buforowania woluminów logicznych, woluminów logicznych lub macierzy lub RAID, zobacz [#Logical volumes](#Logical_volumes).

Teraz musimy utworzyć woluminy logiczne w tej grupie woluminów. Użytkownik tworzy wolumin logiczny za pomocą następnego polecenia, podając nazwę nowego woluminu logicznego, jego rozmiar i grupę woluminów, na której będzie on działał:

```
# lvcreate -L <*size*> <*volume_group*> -n <*logical_volume*>

```

Na przykład:

```
# lvcreate -L 10G VolGroup00 -n lvolhome

```

Spowoduje to utworzenie woluminu logicznego, do którego można uzyskać dostęp później `/dev/mapper/Volgroup00-lvolhome` lub `/dev/VolGroup00/lvolhome`. Podobnie jak w przypadku grup woluminów, podczas tworzenia możesz użyć dowolnej nazwy dla woluminu logicznego.

Można także określić jeden lub więcej woluminów fizycznych, aby ograniczyć miejsce, w którym LVM przydziela dane. Na przykład możesz utworzyć wolumin logiczny dla głównego systemu plików na małym dysku SSD i wolumin domowy na wolniejszym dysku mechanicznym. Wystarczy dodać fizyczne urządzenia głośności do wiersza poleceń, na przykład:

```
# lvcreate -L 10G VolGroup00 -n lvolhome /dev/sdc1

```

Jeśli chcesz wypełnić całe wolne miejsce w grupie woluminów, użyj następnego polecenia:

```
# lvcreate -l 100%FREE  <*volume_group*> -n <*logical_volume*>

```

Możesz śledzić utworzone woluminy logiczne za pomocą:

```
# lvdisplay

```

**Note:** Może być konieczne załadowanie modułu jądra "device-mapper" (`modprobe dm_mod'`) aby powyższe polecenia odniosły sukces.

**Tip:** Możesz zacząć od względnie małych woluminów logicznych i rozwinąć je później, jeśli zajdzie taka potrzeba. Dla uproszczenia pozostaw trochę wolnego miejsca w grupie woluminów, aby było miejsce na rozbudowę.

### Twórz systemy plików i montowanie woliminów logicznych

Twoje woluminy logiczne powinny teraz znajdować się w `/dev/mapper/` i `/dev/*YourVolumeGroupName*`. Jeśli nie możesz ich znaleźć, użyj kolejnych poleceń, aby wywołać moduł do tworzenia węzłów urządzeń i udostępnić grupy woluminów:

```
# modprobe dm_mod
# vgscan
# vgchange -ay

```

Teraz możesz tworzyć systemy plików na woluminach logicznych i montować je jako normalne partycje (jeśli instalujesz Arch Linuksa, zajrzyj do [montowania partycji](/index.php/Mount "Mount") po dodatkowe szczegóły):

```
# mkfs.<*fstype*> /dev/mapper/<*volume_group*>-<*logical_volume*>
# mount /dev/mapper/<*volume_group*>-<*logical_volume*> /<*mountpoint*>

```

Na przykład:

```
# mkfs.ext4 /dev/mapper/VolGroup00-lvolhome
# mount /dev/mapper/VolGroup00-lvolhome /home

```

**Warning:** Wybierając punkty montowania, wybierz nowo utworzone woluminy logiczne (użyj: `/dev/mapper/Volgroup00-lvolhome`). **Nie** wybieraj rzeczywistych partycji, na których zostały utworzone woluminy logiczne (nie używaj: `/dev/sda2`).

### Skonfiguruj mkinitcpio

In case your root filesystem is on LVM, you will need to enable the appropriate [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") hooks, otherwise your system might not boot. Enable:

W przypadku, gdy twój główny system plików jest na LVM, będziesz musiał włączyć odpowiednie haki [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"), inaczej twój system może się nie uruchomić. Włącz:

*   `udev` i `lvm2` dla domyślnych initramfs za pomocą busybox
*   `systemd` i `sd-lvm2` dla initramfs opartych na systemd

`udev` jest tam domyślnie. Edytuj plik i wstaw `lvm2` pomiędzy `block` i `filesystems` jak na przykład:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **udev** ... block **lvm2** filesystems)` 

Dla initramfs opartych na systemd:

 `/etc/mkinitcpio.conf`  `HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)` 

Następnie możesz kontynuować w normalnej instrukcji instalacji, [utwórz początkowy ramdysk](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")

**Tip:**

*   Haki `lvm2` i `sd-lvm2` są instalowane przez [lvm2](https://www.archlinux.org/packages/?name=lvm2), nie [mkinitcpio](https://www.archlinux.org/packages/?name=mkinitcpio). Jeśli uruchamiasz *mkinitcpio* w arch-chroot dla nowej instalacji, [lvm2](https://www.archlinux.org/packages/?name=lvm2) musi być zainstalowany wewnątrz *arch-chroot* dla *mkinitcpio*, aby znaleźć `lvm2` lub `sd-lvm2` hak. Jeśli [lvm2](https://www.archlinux.org/packages/?name=lvm2) stnieje tylko poza *arch-chroot*, *mkinitcpio* wyświetli `Error: Hook 'lvm2' cannot be found`.
*   Jeśli twój główny system plików jest na LVM RAID, zobacz [#Skonfiguruj mkinitcpio dla RAID](#Skonfiguruj_mkinitcpio_dla_RAID).

### Opcje jądra

Jeśli główny system plików znajduje się w woluminie logicznym, to `root=` [parametr jądra](/index.php/Kernel_parameter "Kernel parameter") musi być wskazany na zmapowane urządzenie, np `/dev/mapper/*vg-name*-*lv-name*`.

## Volume operations

### Zaawansowane opcje

Jeśli potrzebujesz monitorowania (potrzebne do migawek), możesz włączyć lvmetad. Dla tego zestawu `use_lvmetad = 1` w `/etc/lvm/lvm.conf`. To jest teraz domyślne.

Możesz ograniczyć woluminy, które są aktywowane automatycznie, ustawiając `auto_activation_volume_list` w `/etc/lvm/lvm.conf`. W razie wątpliwości pozostaw tę opcję wykomentowaną.

### Zmienianie wielkości woluminów

#### woluminów fizycznych

Po wydłużeniu lub zmniejszeniu rozmiaru urządzenia, które ma fizyczną objętość, musisz zwiększyć lub zmniejszyć PV za pomocą `pvresize`.

##### Growing

Aby rozwinąć PV na `/dev/sda1` po powiększeniu partycji, uruchom:

```
# pvresize /dev/sda1

```

To automatycznie wykryje nowy rozmiar urządzenia i rozszerzy PV do maksimum.

**Note:** To polecenie można wykonać, gdy wolumin jest w trybie online.

##### Shrinking

Aby zmniejszyć wolumin fizyczny przed zmniejszeniem jego podstawowego urządzenia, dodaj `--setphysicalvolumesize *size*` parametry do polecenia, *np.*:

```
# pvresize --setphysicalvolumesize 40G /dev/sda1

```

Powyższe polecenie może pozostawić Ci ten błąd:

```
 /dev/sda1: cannot resize to 25599 extents as later ones are allocated.
 0 physical volume(s) resized / 1 physical volume(s) not resized

```

Indeed `pvresize` will refuse to shrink a PV if it has allocated extents after where its new end would be. One needs to run [pvmove](#Move_physical_extents) beforehand to relocate these elsewhere in the volume group if there is sufficient free space.

###### Move physical extents

Przed przeniesieniem wolnych zakresów do końca woluminu należy uruchomić `pvdisplay -v -m` aby zobaczyć fizyczne segmenty. W poniższym przykładzie istnieje jeden wolumin fizyczny włączony `/dev/sdd1`, jedna grupa woluminów `vg1` i jeden wolumin logiczny `backup`.

 `# pvdisplay -v -m` 
```
    Finding all volume groups.
    Using physical volume(s) on command line.
  --- Physical volume ---
  PV Name               /dev/sdd1
  VG Name               vg1
  PV Size               1.52 TiB / not usable 1.97 MiB
  Allocatable           yes 
  PE Size               4.00 MiB
  Total PE              399669
  Free PE               153600
  Allocated PE          246069
  PV UUID               MR9J0X-zQB4-wi3k-EnaV-5ksf-hN1P-Jkm5mW

  --- Physical Segments ---
  Physical extent 0 to 153600:
    FREE
  Physical extent 153601 to 307199:
    Logical volume	/dev/vg1/backup
    Logical extents	1 to 153599
  Physical extent 307200 to 307200:
    FREE
  Physical extent 307201 to 399668:
    Logical volume	/dev/vg1/backup
    Logical extents	153601 to 246068

```

Przestrzeń wolną można podzielić na wolumen. Aby zmniejszyć objętość fizyczną, musimy najpierw przenieść wszystkie używane segmenty na początek.

Tutaj pierwszy wolny segment ma od 0 do 153600 i pozostawia nam 153601 wolnych zakresów. Możemy teraz przenieść ten numer segmentu z ostatniego zakresu fizycznego do pierwszego zakresu. Polecenie będzie zatem:

 `# pvmove --alloc anywhere /dev/sdd1:307201-399668 /dev/sdd1:0-92466` 
```
/dev/sdd1: Moved: 0.1 %
/dev/sdd1: Moved: 0.2 %
...
/dev/sdd1: Moved: 99.9 %
/dev/sdd1: Moved: 100,0%

```

**Note:**

*   to polecenie przenosi 92468 PE (399668-307200) **z** ostatniego segmentu **do** pierwszego segmentu. Jest to możliwe, ponieważ pierwszy segment obejmuje 153600 wolnych PE, które mogą zawierać przesunięte PE-92467.
*   opcja `--alloc anywhere` jest używana podczas przenoszenia PE wewnątrz tej samej partycji. W przypadku różnych partycji polecenie wyglądałoby mniej więcej tak: `# pvmove /dev/sdb1:1000-1999 /dev/sdc1:0-999` 
*   to polecenie może zająć dużo czasu (od jednej do dwóch godzin) w przypadku dużych woluminów. Dobrym pomysłem może być uruchomienie tego polecenia w sesji [Tmux](/index.php/Tmux "Tmux") lub [GNU Screen](/index.php/GNU_Screen "GNU Screen"). Każde niechciane zatrzymanie procesu może być śmiertelne.
*   po zakończeniu operacji uruchom program [fsck](/index.php/Fsck "Fsck"), aby upewnić się, że system plików jest prawidłowy.

###### Zmień rozmiar woluminu fizycznego

Gdy wszystkie wolne fizyczne segmenty będą w ostatnim fizycznym zakresie, uruchom `vgdisplay` i zobacz swój wolny PE.

Następnie możesz teraz ponownie uruchomić polecenie:

```
# pvresize --setphysicalvolumesize *size* *PhysicalVolume*

```

Zobacz wynik:

 `# pvs` 
```
  PV         VG   Fmt  Attr PSize    PFree 
  /dev/sdd1  vg1  lvm2 a--     1t     500g

```

###### Zmień rozmiar partycji

Na koniec, musisz zmniejszyć partycję za pomocą ulubionego [narzędzia do partycjonowania](/index.php/Partitioning#Partitioning_tools "Partitioning").

#### Logical volumes

**Note:** *lvresize* zapewnia mniej więcej takie same opcje, jak wyspecjalizowane polecenia `lvextend` i `lvreduce` pozwalając jednocześnie na wykonywanie obu typów operacji. Niezależnie od tego, wszystkie te narzędzia oferują `-r`/`--resizefs` opcja, która pozwala na zmianę rozmiaru systemu plików wraz z LV za pomocą [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) (*ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") supported). Dlatego może być łatwiej po prostu użyć `lvresize` dla obu operacji i użyć `--resizefs` aby trochę uprościć, chyba że masz określone potrzeby lub chcesz mieć pełną kontrolę nad procesem.

##### Growing or shrinking with lvresize

**Warning:** Podczas gdy powiększanie systemu plików może często odbywać się w trybie on-line (*tj.* Podczas instalacji), nawet w przypadku partycji głównej, zmniejszanie prawie zawsze będzie wymagało najpierw odmontowania systemu plików, aby zapobiec utracie danych. Upewnij się, że twój FS obsługuje to, co próbujesz zrobić.

Rozszerz wolumin logiczny *lv1* w grupie woluminów *vg1* o 2 GiB bez dotykania jego systemu plików:

```
# lvresize -L +2G vg1/lv1

```

Zmniejsz rozmiar `vg1/lv1` o 500 MB bez zmiany rozmiaru systemu plików

```
# lvresize -L -500M vg1/lv1

```

Ustaw `vg1/lv1` na 15 GiB i zmień jednocześnie rozmiar systemu plików:

```
# lvresize -L 15G -r vg1/lv1

```

**Note:** Only *ext2*, [ext3](/index.php/Ext3 "Ext3"), [ext4](/index.php/Ext4 "Ext4"), *ReiserFS* and [XFS](/index.php/XFS "XFS") [file systems](/index.php/File_systems "File systems") are supported. For a different type of file system look for the [appropriate utility](/index.php/File_systems#Types_of_file_systems "File systems").

Jeśli chcesz wypełnić całe wolne miejsce w grupie woluminów, użyj następującego polecenia:

```
# lvresize -l +100%FREE *vg*/*lv*

```

Zobacz [lvresize(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvresize.8) dla bardziej szczegółowych opcji.

##### Rozszerzanie woluminu logicznego i systemu plików za jednym razem

**Warning:** Not all file systems support resizing without loss of data and/or resizing online.

Rozszerz domyslny wolumin logiczny w grupie woluminów o 10 GiB

```
# lvresize -L +10G /dev/*volume-group*/*home* --resizefs

```

Alternatywnie z systemem plików XFS

```
# lvextend -L+10G /dev/*volume-group*/*home*
# xfs_growfs /home

```

Uwaga: *xfs_growfs* pobiera argument montowania jako argument. Zobacz [xfs_growfs(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xfs_growfs.8) dla bardziej szczegółowych opcji.

##### Zmiana rozmiaru systemu plików oddzielnie

Jeśli nie używasz `-r`/`--resizefs` opcja do `lvresize`, `lvextend` lub `lvreduce`, lub przy użyciu systemu plików nieobsługiwanego przez [fsadm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fsadm.8) (np. [Btrfs](/index.php/Btrfs "Btrfs"), [ZFS](/index.php/ZFS "ZFS")), musisz ręcznie zmienić rozmiar systemu plików przed zmniejszeniem LV lub po jego rozszerzeniu.

**Warning:** Nie wszystkie systemy plików obsługują zmianę rozmiaru bez utraty danych i / lub zmiany rozmiaru online.

Na przykład w systemie plików ext2/ext3/ext4:

```
# resize2fs *vg*/*lv*

```

rozszerzy FS do maksymalnego rozmiaru bazowego LV, podczas gdy

```
# resize2fs -M *vg*/*lv*

```

zmniejszy go do swojego minimalnego rozmiaru. Aby zmienić rozmiar na określony rozmiar, użyj:

```
# resize2fs *vg*/*lv* *NewSize*

```

### Remove logical volume

**Warning:** Przed usunięciem woluminu logicznego należy przenieść wszystkie dane, które mają pozostać w innym miejscu; w przeciwnym razie zostanie utracone!

Najpierw sprawdź nazwę woluminu logicznego, który chcesz usunąć. Możesz uzyskać listę wszystkich woluminów logicznych za pomocą:

```
# lvs

```

Następnie wyszukaj punkt montowania wybranego woluminu logicznego:

```
$ lsblk

```

Następnie odmontuj system plików na woluminie logicznym:

```
# umount /<*mountpoint*>

```

Na koniec usuń wolumin logiczny:

```
# lvremove <*volume_group*>/<*logical_volume*>

```

Na przykład:

```
# lvremove VolGroup00/lvolhome

```

Potwierdź, wpisując `y`.

Zaktualizuj `/etc/fstab`, jeśli to konieczne.

Możesz zweryfikować usunięcie woluminu logicznego, wpisując ponownie `lvs` jako root (patrz pierwszy krok tej sekcji).

### Dodaj wolumin fizyczny do grupy woluminów

Najpierw utwórz nowy wolumin fizyczny na urządzeniu blokowym, którego chcesz użyć, a następnie rozszerz swoją grupę woluminów

```
# pvcreate /dev/sdb1
# vgextend VolGroup00 /dev/sdb1

```

To oczywiście zwiększy całkowitą liczbę fizycznych elementów w grupie woluminów, które mogą być przydzielane przez woluminy logiczne według własnego uznania.

**Note:** Za dobrą formę uważa się tablicę partycji na nośniku pamięci poniżej LVM. Użyj odpowiedniego kodu typu: `8e` dla MBR i `8e00` dla partycji GPT.

### Usuń partycję z grupy woluminów

Jeśli utworzyłeś wolumin logiczny na partycji, [usuń](#Remove_logical_volume) go najpierw.

Wszystkie dane na tej partycji muszą zostać przeniesione na inną partycję. Na szczęście LVM ułatwia to:

```
# pvmove /dev/sdb1

```

Jeśli chcesz mieć dane na określonej objętości fizycznej, określ ją jako drugi argument dla `pvmove`:

```
# pvmove /dev/sdb1 /dev/sdf1

```

Następnie należy usunąć wolumin fizyczny z grupy woluminów:

```
# vgreduce myVg /dev/sdb1

```

Lub usuń wszystkie puste woluminy fizyczne:

```
# vgreduce --all vg0

```

I na koniec, jeśli chcesz użyć partycji na coś innego i chcesz uniknąć LVM myśląc, że partycja jest woluminem fizycznym:

```
# pvremove /dev/sdb1

```

### Dezaktywuj grupę woluminów

Po prostu wywołaj

```
# vgchange -a n my_volume_group

```

Spowoduje to dezaktywację grupy woluminów i umożliwi odmontowanie kontenera, w którym jest przechowywany.

## Typy woluminów logicznych

Oprócz prostych woluminów logicznych LVM obsługuje migawki, buforowanie woluminów logicznych, woluminy logiczne o cienkich wersjach i macierze RAID.

### Migawki

LVM pozwala wykonać migawkę systemu w znacznie bardziej wydajny sposób niż tradycyjne kopie zapasowe. Robi to skutecznie, stosując zasady COW (copy-on-write). Początkowa migawka zawiera po prostu twarde linki do i-węzłów rzeczywistych danych. Dopóki dane pozostają niezmienione, migawka zawiera jedynie wskaźniki i-węzłów, a nie same dane. Ilekroć modyfikujesz plik lub katalog, na który wskazuje migawka, LVM automatycznie klonuje dane, starą kopię, do której odwołuje się migawka, oraz nową kopię, do której odwołuje się Twój aktywny system. W ten sposób można wykonać migawkę systemu z 35 GiB danych przy użyciu zaledwie 2 GiB wolnej przestrzeni, o ile zmodyfikowano mniej niż 2 GiB (zarówno na oryginale, jak i na migawce). Aby móc tworzyć migawki, musisz mieć nieprzydzielone miejsce w grupie woluminów. Migawka, jak każdy inny wolumen, zajmie miejsce w grupie woluminów. Tak więc, jeśli zamierzasz używać migawek do tworzenia kopii zapasowej partycji root, nie przydzielaj 100% grupy woluminów dla woluminu logicznego root.

#### Konfiguracja

Buforowanie woluminów logicznych tworzy się podobnie jak normalne.

```
# lvcreate --size 100M --snapshot --name snap01 /dev/mapper/vg0-pv

```

Przy takim woluminie można zmodyfikować mniej niż 100 MB danych, zanim objętość migawki się zapełni.

Przywracanie zmodyfikowanego woluminu logicznego "pv" do stanu po zrobieniu migawki "snap01" można wykonać za pomocą

```
# lvconvert --merge /dev/mapper/vg0-snap01

```

W przypadku, gdy początkowy wolumin logiczny jest aktywny, scalanie nastąpi przy następnym ponownym uruchomieniu. (Scalanie można wykonać nawet z LiveCD)

Migawka nie będzie już istnieć po scaleniu.

Można również wykonać wiele migawek i każdy z nich można dowolnie łączyć z początkowym woluminem logicznym.

Migawkę można zamontować i zarchiwizować za pomocą narzędzia *dd* lub *tar*. Rozmiar pliku kopii zapasowej wykonanego przy pomocy dd będzie wielkości plików znajdujących się na woluminie migawki. Aby przywrócić, po prostu utwórz migawkę, zamontuj ją i napisz lub wyodrębnij do niej kopię zapasową, a następnie scal ją z punktem początkowym.

Migawki są używane przede wszystkim do zapewnienia zamrożonej kopii systemu plików do tworzenia kopii zapasowych; wykonanie kopii zapasowej trwającej dwie godziny zapewnia bardziej spójny obraz systemu plików niż bezpośrednie tworzenie kopii zapasowej partycji.

Zobacz [Create root filesystem snapshots with LVM](/index.php/Create_root_filesystem_snapshots_with_LVM "Create root filesystem snapshots with LVM") do automatyzacji tworzenia czystych migawek systemu plików root podczas uruchamiania systemu w celu tworzenia kopii zapasowych i przywracania.

[dm-crypt/Encrypting an entire system#LVM on LUKS](/index.php/Dm-crypt/Encrypting_an_entire_system#LVM_on_LUKS "Dm-crypt/Encrypting an entire system") i [dm-crypt/Encrypting an entire system#LUKS on LVM](/index.php/Dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM "Dm-crypt/Encrypting an entire system").

Jeśli masz woluminy LVM nie aktywowane przez [initramfs](/index.php/Initramfs "Initramfs"), [enable](/index.php/Enable "Enable") `lvm-monitoring.service`, który jest dostarczany przez [lvm2](https://www.archlinux.org/packages/?name=lvm2) pakiet.

### LVM cache

From [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7):

	Typ woluminu logicznego w pamięci podręcznej wykorzystuje mały i szybki LV, aby poprawić wydajność dużego i wolnego LV. Czyni to poprzez przechowywanie często używanych bloków na szybszym LV. LVM odnosi się do małego szybkiego LV jako puli pamięci podręcznej LV. Duża wolna LV nazywana jest początkową LV. Ze względu na wymagania z pamięci podręcznej dm (sterownik jądra), LVM dalej dzieli pulę pamięci podręcznej LV na dwa urządzenia - dane LH pamięci podręcznej i LV pamięci podręcznej. Dane Lache pamięci podręcznej to miejsca, w których kopie bloków danych są przechowywane od punktu początkowego LV w celu zwiększenia prędkości. Metadane pamięci podręcznej LV przechowuje informacje rozliczeniowe, które określają miejsce przechowywania bloków danych (np. W punkcie początkowym LV lub w danych Lache pamięci podręcznej). Użytkownicy powinni być zaznajomieni z tymi LV, jeśli chcą stworzyć najlepsze i najbardziej odporne buforowane woluminy logiczne. Wszystkie te powiązane LV muszą znajdować się w tym samym VG.

#### Create cache

Szybka metoda polega na utworzeniu PV (jeśli to konieczne) na szybkim dysku i dodaniu go do istniejącej grupy woluminów:

```
# vgextend dataVG /dev/sdx

```

Utwórz pulę pamięci podręcznej z automatycznymi metadanymi na sdb i przekonwertuj istniejący wolumin logiczny (dataLV) na wolumin w pamięci podręcznej, a wszystko to w jednym kroku:

```
# lvcreate --type cache --cachemode writethrough -L 20G -n dataLV_cachepool dataVG/dataLV /dev/sdx

```

Oczywiście, jeśli chcesz, aby pamięć podręczna była większa, możesz zmienić parametr `-L` na inny rozmiar.

**Note:** Cachemode ma dwie możliwe opcje:

*   `writethrough` zapewnia, że wszelkie zapisane dane będą przechowywane zarówno w puli pamięci podręcznej LV, jak i w punkcie początkowym LV. Utrata urządzenia związanego z pulą pamięci podręcznej LV w tym przypadku nie oznacza utraty jakichkolwiek danych;
*   `writeback` zapewnia lepszą wydajność, ale kosztem większego ryzyka utraty danych w przypadku awarii dysku używanego do buforowania.

Jeśli określony `--cachemode` nie jest wskazany, system przyjmie `writethrough` wartość domyśln

#### Usuń pamięć podręczną

Jeśli kiedykolwiek zajdzie potrzeba cofnięcia operacji tworzenia o jeden krok powyżej:

```
# lvconvert --uncache dataVG/dataLV

```

Spowoduje to zatwierdzenie wszystkich oczekujących zapisów w pamięci podręcznej z powrotem do początkowego LV, a następnie usunięcie pamięci podręcznej. Inne opcje są dostępne i opisane w [lvmcache(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmcache.7).

### RAID

From [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7):

	[lvm(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvm.8) RAID is a way to create a Logical Volume (LV) that uses multiple physical devices to improve performance or tolerate device failures. In LVM, the physical devices are Physical Volumes (PVs) in a single Volume Group (VG).

LVM RAID supports RAID 0, RAID 1, RAID 4, RAID 5, RAID 6 and RAID 10\. See [Wikipedia:Standard RAID levels](https://en.wikipedia.org/wiki/Standard_RAID_levels "wikipedia:Standard RAID levels") for details on each level.

#### Konfiguracja RAID

Utwórz woluminy fizyczne:

```
# pvcreate /dev/sda2 /dev/sdb2

```

Utwórz grupę woluminów na woluminach fizycznych:

```
# vgcreate VolGroup00 /dev/sda2 /dev/sdb2

```

Utwórz woluminy logiczne za pomocą `lvcreate --type *raidlevel*`, Zobacz [lvmraid(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvmraid.7) i [lvcreate(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lvcreate.8) aby uzyskać więcej opcji

```
# lvcreate --type RaidLevel [OPTIONS] -n Name -L Size VG [PVs]

```

Na przykład:

```
# lvcreate --type raid1 --mirrors 1 -L 20G -n myraid1vol VolGroup00 /dev/sda2 /dev/sdb2

```

utworzy wolumin logiczny o rozmiarze 20 GiB o nazwie "myraid1vol" w VolGroup00 na `/dev/sda2` i `/dev/sdb2`.

#### Skonfiguruj mkinitcpio dla RAID

Jeśli twój rootowy system plików znajduje się na LVM RAID dodatkowo do haków `lvm2` lub `sd-lvm2`, musisz dodać moduł `dm-raid` i odpowiednie moduły RAID (np. `raid0`, `raid1`, `raid10` i / lub `raid456`) do tablicy MODULES w pliku `mkinitcpio.conf`.

Dla initramfs opartych na busybox

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **udev** ... block **lvm2** filesystems)
```

Dla initramfs opartych na systemd:

 `/etc/mkinitcpio.conf` 
```
MODULES=(**dm-raid raid0 raid1 raid10 raid456**)
HOOKS=(base **systemd** ... block **sd-lvm2** filesystems)
```

## Graficzna konfiguracja

Nie ma "oficjalnego" narzędzia GUI do zarządzania woluminami LVM, ale [system-config-lvm](https://aur.archlinux.org/packages/system-config-lvm/) obejmuje większość typowych operacji i zapewnia proste wizualizacje stanu woluminu. Może automatycznie zmieniać rozmiar wielu systemów plików podczas zmiany rozmiaru woluminów logicznych.

## Rozwiązywanie problemów

### Zmiany, które mogą być wymagane ze względu na zmiany w domyślnych ustawieniach Arch-Linux

Parametr `use_lvmetad = 1` musi być ustawiony w pliku `/etc/lvm/lvm.conf`. To jest teraz domyślne - jeśli masz plik `lvm.conf.pacnew`, musisz scalić tę zmianę.

### Komendy LVM nie działają

*   Załaduj odpowiedni moduł:

```
# modprobe dm_mod

```

Moduł `dm_mod` powinien zostać załadowany automatycznie. Jeśli nie, możesz spróbować:

 `/etc/mkinitcpio.conf`  `MODULES=(dm_mod ...)` 

Będziesz musiał [zregenerować initramfs,](/index.php/Regenerate_the_initramfs "Regenerate the initramfs") aby zatwierdzić wprowadzone zmiany.

*   Wypróbuj wcześniejsze polecenia za pomocą *lvm*:

```
# lvm pvdisplay

```

### Woluminy logiczne się nie wyświetlają

Jeśli próbujesz zamontować istniejące woluminy logiczne, ale nie pojawiają się one w programie `lvscan`, możesz użyć następujących poleceń, aby je aktywować:

```
# vgscan
# vgchange -ay

```

### LVM na nośnikach wymiennych

Objawy

 `# vgscan` 
```
  Reading all physical volumes.  This may take a while...
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836585984: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 319836643328: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 0: Input/output error
  /dev/backupdrive1/backup: read failed after 0 of 4096 at 4096: Input/output error
  Found volume group "backupdrive1" using metadata type lvm2
  Found volume group "networkdrive" using metadata type lvm2

```

Przyczyna:

	Usuwanie zewnętrznego napędu LVM bez uprzedniej dezaktywacji grup woluminów. Zanim się rozłączysz, upewnij się, że:

```
# vgchange -an *volume group name*

```

Naprawiono: zakładając, że próbowałeś już aktywować grupę woluminów za pomocą `vgchange -ay *vg*`, i otrzymujesz błędy Input/output:

```
# vgchange -an *volume group name*

```

Odłącz dysk zewnętrzny i poczekaj kilka minut:

```
# vgscan
# vgchange -ay *volume group name*

```

### Zmiana rozmiaru sąsiedniego woluminu logicznego kończy się niepowodzeniem

W przypadku próby rozszerzenia błędów woluminu logicznego za pomocą:

```
" Insufficient suitable contiguous allocatable extents for logical volume "

```

Powodem jest to, że wolumin logiczny został utworzony z wyraźną, ciągłą polityką alokacji (opcje `-C y` lub `--alloc contiguous`) i brak sąsiadujących sąsiednich zakresów (Zobacz też [reference](http://www.hostatic.ro/2010/02/15/lvm-inherit-and-contiguous-policies/)).

Aby to naprawić, przed rozszerzeniem woluminu logicznego zmień jego strategię alokacji za pomocą polecenia lvchange `lvchange --alloc inherit <logical_volume>`. Jeśli chcesz zachować politykę alokacji przyległej, alternatywnym podejściem jest przeniesienie woluminu na obszar dysku z wystarczającymi swobodnymi zakresami (Zobacz [[1]](http://superuser.com/questions/435075/how-to-align-logical-volumes-on-contiguous-physical-extents)).

### Polecenie "grub-mkconfig" zgłasza błędy "unknown filesystem" errors

Pamiętaj, aby wcześniej usunąć woluminy migawek [generating grub.cfg](/index.php/GRUB#Generate_the_main_configuration_file "GRUB").

### Thinly-provisioned root volume device times out

Przy dużej liczbie migawek, `thin_check` działa przez wystarczająco długi czas, aby wyczekiwać na przekroczenie limitu czasu roota. Aby to zrekompensować, dodaj parametr startowy `rootdelay=60` jądra do konfiguracji programu ładującego.

### Opóźnienie przy wyłączaniu

Jeśli używasz RAID, migawek lub alokacji i masz opóźnienie przy wyłączaniu, upewnij się, że uruchomiono `lvm2-monitor.service`. Zobacz [FS#50420](https://bugs.archlinux.org/task/50420).

## Zobacz też

*   [LVM2 Resource Page](http://sourceware.org/lvm2/) on SourceWare.org
*   [LVM](http://wiki.gentoo.org/wiki/LVM) article at Gentoo wiki
*   [Ubuntu LVM Guide Part 1](http://www.tutonics.com/2012/11/ubuntu-lvm-guide-part-1.html)[Part 2 detals snapshots](http://www.tutonics.com/2012/12/lvm-guide-part-2-snapshots.html)
*   [Red Hat: Logical Volume Manager Administration](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Logical_Volume_Manager_Administration/index.html)