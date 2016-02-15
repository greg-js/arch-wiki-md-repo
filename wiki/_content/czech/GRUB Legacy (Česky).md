## Contents

*   [1 Úvod](#.C3.9Avod)
    *   [1.1 Poznámky](#Pozn.C3.A1mky)
*   [2 Bootování instalačního CD](#Bootov.C3.A1n.C3.AD_instala.C4.8Dn.C3.ADho_CD)
    *   [2.1 Připojení současné instalace](#P.C5.99ipojen.C3.AD_sou.C4.8Dasn.C3.A9_instalace)
    *   [2.2 Přeinstalování GRUBu](#P.C5.99einstalov.C3.A1n.C3.AD_GRUBu)
        *   [2.2.1 Chyby](#Chyby)

## Úvod

V tomto návodu je popsán postup při přeinstalovájí GRUBu pomocí instalačního CD Arch linuxu.

### Poznámky

*   Jako zařízení je použito <tt>hda1</tt>.

*   Návod je určen těm, ktěři používají IDE zařízení, ne SCSI nebo SATA. Pro ně je nutné patřičně nahradit SCSI a SATA cesty a zařízení.

## Bootování instalačního CD

První, co potřebujete je [instalační CD](https://www.archlinux.org/download.php). Je možné použít jakékoliv instalační CD, ale ideální je poslení verze.

Nabootujte z CD, jako by jste dělali instalaci Arch linuxu (**NEPOUŽÍVEJTE** <tt>root= option</tt>) a přejděte k dalšímu kroku.

### Připojení současné instalace

Nyní je třeba připojit současnou instalaci Arch linux. Postup je následující:

*   Poznámka: je třeba vědět jaké jsou vaše diskové oddíly a souborové systémy, v návodu je použito zařízení <tt>hda1</tt> jako root oddíl se souborovým systémem <tt>ext3</tt>.

```
cd /
mount -t ext3   /dev/hda1 /mnt          
mount -t proc   proc      /mnt/proc
mount -t sysfs  sys       /mnt/sys
mount -o bind   /dev      /mnt/dev

chroot /mnt /bin/bash

```

Nyní se můžete přihlásit jako root do současné instalace. Přejděme k dalšímu kroku!

### Přeinstalování GRUBu

Upravte soubor <tt>/boot/grub/menu.lst</tt> a přesvěčte se, že je vše v pořádku. V případě, že tomu tak je, použijte příkaz:

```
grub-install /dev/hda

```

Tento příkaz by měl proběhnout úspěšně, jestliže jste dodrželi předchozí postup (pakliže se objevily nějaké chyby, čtěte níže). To je vše. Restatujte počítač:

```
cd /
umount -a
exit
cd /
umount -a
reboot

```

#### Chyby

Jestliže se vám objeví chyba <tt>The file /boot/grub/stage1 not read correctly</tt>, je třeba zkontrolovat soubory <tt>/etc/mtab</tt> a <tt>/etc/fstab</tt> a poté znovu spustit grub-install.

Objeví-li se vám chyba <tt>sed: can't read /boot/grub/device.map: No such file or directory</tt>, znamená to, že musíte použít přepínač --recheck v příkazu grub-install.

```
 grub-install --recheck /dev/sda

```

Snad se vše zadařilo a vy si můžete opět spustit svou oblíbenou distribuci. V případě jiných chyb, zrestartuje počítač a zkuste vše znovu od začátku.