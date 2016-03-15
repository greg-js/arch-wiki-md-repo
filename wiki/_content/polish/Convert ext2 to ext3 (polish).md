*Jeśli zainstalowałeś Archa na systemie plików ext2, dobrym pomysłem byłoby włączenie księgowania i konwersja na system plików ext3\. Księgowanie zapewnia szereg korzyści.*

1\. Zidentyfikuj partycję przezanaczoną do konwersji przez sprawdzenie pliku **/etc/fstab** i wyjścia polecenia **mount**.

2\. Dodaj dziennik do partycji:

```
sudo tune2fs -j PARTYCJA

```

Gdzie PARTYCJA to /dev/hda1, /dev/sda1, /dev/discs/disc0/part1, itd.

2\. Otwórz **/etc/fstab** i zmień *ext2* na *ext3* dla konwertowanej partycji.

Na przykład:

```
/dev/sda3 / ext2 defaults 0 1

```

zmienia się na:

```
/dev/sda3 / ext3 defaults 0 1

```

3\. Dodaj moduł ext3 do **/etc/mkinitcpio.conf**

```
MODULES="ext3"

```

4\. Przebuduj obraz initrd (dla standardowego jądra):

```
sudo mkinitcpio -p linux

```

Zobacz też: [Migrating from ext3 to ext4](/index.php/Ext4#Migrating_from_ext2.2Fext3_to_ext4 "Ext4")