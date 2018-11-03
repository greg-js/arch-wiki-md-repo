**Fstab** (ang. *file systems table*) – plik konfiguracyjny, znajdujący się w katalogu /etc, który zawiera informacje na temat podłączonych do systemu [urządzeń blokowych](/index.php/Block_device "Block device") (przede wszystkim dysków twardych), ich [partycji](/index.php/Partitioning_(Polski) "Partitioning (Polski)") oraz sposobu, w jakim urządzenia oraz partycje mają zostać [zamontowane](/index.php/Mounting "Mounting") podczas [rozruchu komputera](/index.php/Arch_boot_process "Arch boot process"). Wymienione w pliku urządzenia mogą zostać podłączone do systemu lokalnie (z uruchamianego komputera) lub zdalnie (z innego komputera w sieci).

Każda partycja poszczególnego urządzenia blokowego jest w tym pliku opisana w oddzielnej linii. Linia taka zawiera definicję partycji wraz z parametrami. Wszystkie prawidłowe definicje z pliku zostają automatycznie przekształcone w działające partycje przez [systemd](/index.php/Systemd "Systemd"), podczas rozruchu komputera lub podczas ponownego załadowania tego menedżera systemu.

Domyślna konfiguracja fstab uruchamia wpierw automatycznie program [fsck](/index.php/Fsck "Fsck"), a następnie montuje partycje jeszcze przed uruchomieniem usług, które wymagają ich zamontowania. Systemd automatycznie upewnia się, że partycja zdalna z system plików, takim jak [NFS](/index.php/NFS "NFS") lub [Samba](/index.php/Samba "Samba"), jest uruchamiana dopiero po skonfigurowaniu sieci. Dlatego lokalne i zdalne partycje, poprawnie określone w `/ etc / fstab`, powinny działać natychmiast po zakończeniu rozruchu komputera.

Komenda systemowa `mount` używa definicji z pliku fstab, podczas podłączania do działającego komputera urządzenia blokowego (np. czytnika dysków), sprawdzając zawarte w niej parametry. Jeżeli podczas montowania urządzenia wykryta zostanie definicja w pliku fstab, zostaną użyte wymienione w niej parametry.

Systemowa strona man [fstab(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fstab.5) opisuje, w jaki sposób prawidłowo zdefiniować partycje dysków twardych, innych urządzeń blokowych lub zdalnych systemów plików.

## Użycie

Przykładowy wpis w pliku `/etc/fstab`, stosujący nazwy urządzeń używane przez [jądro](/index.php/Kernel "Kernel"), montujący podczas startu systemu trzy partycje jednego twardego dysku:

 `/etc/fstab` 
```
# <device>             <dir>         <type>    <options>             <dump> <fsck>
/dev/sda1              /             ext4      noatime               0      1
/dev/sda2              none          swap      defaults              0      0
/dev/sda3              /home         ext4      noatime               0      2
```

*   `<device>` – definiuje urządzenie blokowe, jego konkretną partycję lub zdalny system plików, które mają zostać zamontowane.
*   `<dir>` – określa katalog, do którego montujemy urządzenie.
*   `<type>` – określa typ [systemu plików](/index.php/File_systems_(Polski) "File systems (Polski)").
*   `<options>` – określa dodatkowe opcje montowania, zobacz [mount(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mount.8#FILESYSTEM-INDEPENDENT_MOUNT_OPTIONS) oraz [ext4(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ext4.5#MOUNT_OPTIONS).
*   `<dump>` – określa, czy partycja będzie sprawdzana przez [dump(8)](http://linux.die.net/man/8/dump). Ten parametr jest zwykle ustawiony na `0`, co uniemożliwia sprawdzenie.
*   `<fsck>` – określa kolejność sprawdzania partycji przez program [fsck](/index.php/Fsck "Fsck"). Dla partycji głównej parametr ten powinien zostać ustawiony na `1`. Pozostałe partycje powinny mieć go ustawione na `2` lub też, gdy partycja nie ma być sprawdzana, na `0`.