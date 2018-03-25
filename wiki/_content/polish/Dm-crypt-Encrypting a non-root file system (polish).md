Poniżej przedstawiono przykłady szyfrowania wtórnego, tj. Innego niż root, systemu plików z dm-crypt.

## Contents

*   [1 Overview](#Overview)
*   [2 Partycja](#Partycja)
    *   [2.1 Ręczne zakładanie i odmontowywanie](#R.C4.99czne_zak.C5.82adanie_i_odmontowywanie)
    *   [2.2 Automatyczne odblokowywanie i montowanie](#Automatyczne_odblokowywanie_i_montowanie)
        *   [2.2.1 Podczas startu systemu](#Podczas_startu_systemu)
        *   [2.2.2 Przy logowaniu użytkownika](#Przy_logowaniu_u.C5.BCytkownika)
*   [3 Loop device](#Loop_device)
    *   [3.1 Ręczne montowanie i odmontowywanie](#R.C4.99czne_montowanie_i_odmontowywanie)

## Overview

Szyfrowanie dodatkowego systemu plików zazwyczaj chroni tylko poufne dane, pozostawiając niezaszyfrowany system operacyjny i pliki programów. Jest to przydatne do szyfrowania zewnętrznego nośnika, takiego jak dysk USB, aby można go było bezpiecznie przenieść na inne komputery. Można również wybrać szyfrowanie zestawów danych osobno w zależności od tego, kto ma do nich dostęp.

Ponieważ [dm-crypt](/index.php/Dm-crypt "Dm-crypt") jest warstwą szyfrowania blokowego, szyfruje tylko pełne urządzenia, pełne partycje i urządzenia pętli. Szyfrowanie pojedynczych plików wymaga warstwy szyfrowania na poziomie systemu plików, takiej jak [eCryptfs](/index.php/ECryptfs "ECryptfs") lub [EncFS](/index.php/EncFS "EncFS"). Zobacz [Disk encryption (Polski)](/index.php/Disk_encryption_(Polski) "Disk encryption (Polski)"), aby uzyskać ogólne informacje na temat zabezpieczania prywatnych danych.

## Partycja

Ten przykład obejmuje szyfrowanie partycji `/home`, ale można ją zastosować do dowolnej innej porównywalnej partycji innej niż root, zawierającej dane użytkownika.

**Tip:** Możesz mieć katalog pojedynczego użytkownika `/home` na partycji lub utworzyć wspólną partycję dla wszystkich partycji użytkownika `/home`

Najpierw upewnij się, że partycja jest pusta (nie ma do niej podłączonego systemu plików). Usuń partycję i utwórz pustą, jeśli ma system plików. Następnie przygotuj partycję przez jej bezpieczne usunięcie, zobacz [Dm-crypt/Drive preparation#Secure erasure of the hard disk drive](/index.php/Dm-crypt/Drive_preparation#Secure_erasure_of_the_hard_disk_drive "Dm-crypt/Drive preparation").

Następnie ustaw nagłówek LUKS na

```
# cryptsetup *options* luksFormat --type luks2 *device*

```

Zamień urządzenie na poprzednio utworzoną partycję. zobacz [Dm-crypt/Device encryption (Polski)#Opcje szyfrowania z dm-crypt](/index.php/Dm-crypt/Device_encryption_(Polski)#Opcje_szyfrowania_z_dm-crypt "Dm-crypt/Device encryption (Polski)") po szczegóły, takie jak dostępne opcje.

Aby uzyskać dostęp do zaszyfrowanej partycji, odblokuj ją za pomocą urządzenia mapującego, używając:

```
# cryptsetup open *device* *name*

```

Po odblokowaniu partycji będzie ona dostępna pod adresem `/dev/mapper/*name*`. Teraz stwórz a [System plików](/index.php/File_system "File system") do wyboru z:

```
# mkfs.*fstype* /dev/mapper/*name*

```

Zamontuj system plików na `/home` lub jeśli powinien być dostępny tylko dla jednego użytkownika na `/home/*username*`, zobacz [#Ręczne montowanie i odmontowywanie](#R.C4.99czne_montowanie_i_odmontowywanie).

**Tip:** Odmontuj i zamontuj jeden raz, aby sprawdzić, czy mapowanie działa zgodnie z oczekiwaniami.

### Ręczne zakładanie i odmontowywanie

Aby zamontować partycję:

```
# cryptsetup open *device* *name*
# mount -t *fstype* /dev/mapper/*name* /mnt/home

```

Aby odmontować:

```
# umount /mnt/home
# cryptsetup close *name*

```

**Tip:** [GVFS](/index.php/GVFS "GVFS") can also mount encrypted partitions. One can use a file manager with gvfs support (e.g. [Thunar](/index.php/Thunar "Thunar")) to mount the partition, and a password dialog will pop-up. For other desktops, [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/) also provides a GUI.

### Automatyczne odblokowywanie i montowanie

Istnieją trzy różne rozwiązania do automatyzacji procesu odblokowywania partycji i montowania jej systemu plików.

#### Podczas startu systemu

Użycie pliku konfiguracyjnego `/etc/crypttab` powoduje automatyczne odblokowanie podczas uruchamiania systemu. Jest to zalecane rozwiązanie, jeśli chcesz użyć jednej wspólnej partycji na wszystkich partycjach domowych użytkownika lub automatycznie zamontować inne zaszyfrowane urządzenie blokowe.

Zobacz [Dm-crypt/System configuration#crypttab](/index.php/Dm-crypt/System_configuration#crypttab "Dm-crypt/System configuration") w przypadku odniesień i [Dm-crypt/System configuration#Mounting at boot time](/index.php/Dm-crypt/System_configuration#Mounting_at_boot_time "Dm-crypt/System configuration") na przykład skonfigurować.

#### Przy logowaniu użytkownika

Za pomocą *pam_exec* możliwe jest odblokowanie (*cryptsetup open*) partycja przy logowaniu użytkownika: jest to zalecane rozwiązanie, jeśli chcesz mieć katalog domowy pojedynczego użytkownika na partycji. zobacz [dm-crypt/Mounting at login](/index.php/Dm-crypt/Mounting_at_login "Dm-crypt/Mounting at login").

Odblokowanie przy logowaniu użytkownika jest również możliwe dzięki [pam_mount](/index.php/Pam_mount "Pam mount").

## Loop device

**Tip:** Należy zauważyć, że za pomocą losetup bezpośrednio można uniknąć całkowicie, wykonując alternatywną metodę:
```
# dd if=/dev/urandom of=key.img bs=20M count=1
# cryptsetup --align-payload=1 --hash=sha512 --cipher=serpent-xts-plain64 --key-size=512 -i 30000 luksFormat key.img
# cryptsetup open key.img lukskey
```

Za mało pliku dostaniesz `Requested offset is beyond real size of device /dev/loop0` błąd, ale jako przybliżone odniesienie tworzenie pliku 4MiB spowoduje jego pomyślne zaszyfrowanie. [[1]](https://wiki.gentoo.org/wiki/Custom_Initramfs#Encrypted_keyfile)

Urządzenie z pętlą umożliwia mapowanie urządzenia blokowego do pliku za pomocą standardowego narzędzia util-linux `losetup`. Plik może wówczas zawierać system plików, który może być używany podobnie jak każdy inny system plików. Wielu użytkowników wie [TrueCrypt](/index.php/TrueCrypt "TrueCrypt") jako narzędzie do tworzenia zaszyfrowanych kontenerów. Mniej więcej taką samą funkcjonalność można osiągnąć za pomocą systemu plików loopback zaszyfrowanego za pomocą LUKS i pokazano go w poniższym przykładzie.

Najpierw zacznij od utworzenia zaszyfrowanego kontenera, używając odpowiedniego [random number generator](/index.php/Random_number_generator "Random number generator")

```
# dd if=/dev/urandom of=/bigsecret bs=1M count=10

```

Spowoduje to utworzenie dużego pliku o rozmiarze 10 megabajtów.

**Note:** Aby uniknąć konieczności zmiany [rozmiaru kontenera](/index.php/Dm-crypt/Device_encryption#Loopback_filesystem "Dm-crypt/Device encryption") w późniejszym czasie, upewnij się, że jest większy niż całkowity rozmiar plików, które mają być zaszyfrowane, aby przynajmniej hostować powiązane metadane potrzebne w wewnętrznym systemie plików. Jeśli zamierzasz używać trybu LUKS, jego nagłówek metadanych wymaga od jednego do dwóch megabajtów.

Następnie utwórz węzeł device `/dev/loop0`, abyśmy mogli zamontować / używać naszego kontenera:

```
# losetup /dev/loop0 /bigsecret

```

**Note:** Jeśli to daje błąd `/dev/loop0: No such file or directory`, musisz najpierw załadować moduł jądra za pomocą `modprobe loop`. Obecnie urządzenia pętli (Kernel 3.2) są tworzone na żądanie. Poproś o nowe urządzenie z pętlą `# losetup -f`.

Odtąd procedura jest taka sama jak w przypadku [#Partycja](#Partycja), z wyjątkiem faktu, że kontener jest już randomizowany i nie będzie wymagał kolejnego bezpiecznego usunięcia.

**Tip:** Kontenery z dm-crypt mogą być bardzo elastyczne. Spójrz na funkcje i dokumentację [Tomb](/index.php/Tomb "Tomb"). Zapewnia *dm-crypt* szybką i elastyczną obsługę.

### Ręczne montowanie i odmontowywanie

Aby odmontować kontener:

```
# umount /mnt/secret
# cryptsetup close secret
# losetup -d /dev/loop0

```

Aby ponownie zamontować kontener:

```
# losetup /dev/loop0 /bigsecret
# cryptsetup open /dev/loop0 secret
# mount -t ext4 /dev/mapper/secret /mnt/secret

```