Nejdříve je třeba nainstalovat [GRUB](/index.php/GRUB "GRUB"):

```
 pacman -S grub

```

Dalším krokem je formátování diskety:

```
 fdformat /dev/fd0
 mke2fs /dev/fd0

```

Nyní připojíme disketu:

```
 mount -t ext2 /dev/fd0 /mnt/fl

```

a nainstalujeme na ni GRUB:

```
 grub-install --root-directory=/mnt/fl '(fd0)'

```

Překopírujeme soubor /boot/grub/menu.lst na disketu:

```
 cp /boot/grub/menu.lst /mnt/fl/boot/grub/menu.lst

```

A nakonec disketu odpojíme:

```
 umount /mnt/fl

```

Hotovo! Měli by jste být schopni po restartu počítače spusti grub z diskety. Samozřejmě musíte mít v BIOSu nastaveno správné pořadí bootování.