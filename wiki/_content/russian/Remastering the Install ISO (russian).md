**Состояние перевода:** На этой странице представлен перевод статьи [Remastering the Install ISO](/index.php/Remastering_the_Install_ISO "Remastering the Install ISO"). Дата последней синхронизации: 19 августа 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Remastering_the_Install_ISO&diff=0&oldid=536226).

Ссылки по теме

*   [Archiso (Русский)](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)")

Ремастеринг официального установочного ISO образа Arch Linux не является необходимым для большинства приложений. Однако, это может быть желательно в некоторых случаях.

*   Основное оборудование не поддерживается базовой установкой. (Редко)
*   Установка на машине, не поддерживающей интернет.
*   Развертывание Arch Linux на многих аналогичных машинах, требующих такой же процедуры установки.

Поскольку эти ISO являются загрузочными, они также могут использоваться для восстановления системы, тестирования, демонстрации проектов и т.д.

## Contents

*   [1 Archiso](#Archiso)
*   [2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
    *   [2.1 Как это работает](#.D0.9A.D0.B0.D0.BA_.D1.8D.D1.82.D0.BE_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82)
    *   [2.2 Распаковка ISO](#.D0.A0.D0.B0.D1.81.D0.BF.D0.B0.D0.BA.D0.BE.D0.B2.D0.BA.D0.B0_ISO)
    *   [2.3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [2.3.1 Редактирование системы x86_64](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_x86_64)
        *   [2.3.2 Редактирование системы i686](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B_i686)
        *   [2.3.3 Изменение загрузочного образа EFI](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_EFI)
    *   [2.4 Создание нового ISO](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_ISO)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Archiso

Часто предпочтительнее пересобирать установку ISO с помощью [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)"), вместо ремастеринга существующего ISO.

## Вручную

### Как это работает

Корень файловой live системы хранится в `arch/x86_64/airootfs.sfs` в ISO. Ядро и initramfs находятся в `arch/boot/x86_64`.

При загрузке initramfs будет искать устройство, с которого он был загружен с помощью его метки, например `ARCH_201410`, и смонтирует корневую файловую систему для архитектуры x86_64.

### Распаковка ISO

Чтобы переделать Arch Linux ISO, вам понадобится копия исходного ISO-образа. Загрузите его со страницы [загрузок](https://www.archlinux.org/download/)

Теперь создайте новый каталог для монтирования ISO:

```
# mkdir /mnt/archiso

```

Смонтируйте ISO к этому каталогу (из-за специфики ISO, результат доступен только для чтения):

```
# mount -t iso9660 -o loop /path/to/archISO /mnt/archiso

```

Скопируйте содержимое в другой каталог, где они могут быть отредактированы:

```
$ cp -a /mnt/archiso ~/customiso

```

**Примечание:** Убедитесь, что `customiso` не существует заранее, иначе это создаст подкаталог `archiso` внутри `customiso`

### Настройка

#### Редактирование системы x86_64

Перейдите в каталог системы x86_64:

```
 $ cd ~/customiso/arch/x86_64

```

Unsquash `airootfs.sfs` (для `squashfs-root`):

```
 $ unsquashfs airootfs.sfs

```

**Примечание:** Для этого вам нужен пакет [squashfs-tools](https://www.archlinux.org/packages/?name=squashfs-tools).

Если вам необходимо запустить `mkinitcpio` без `arch-chroot`, тогда нужно временно скопировать ядро:

```
$ cp ../boot/x86_64/vmlinuz squashfs-root/boot/vmlinuz-linux

```

Теперь вы можете изменить содержимое системы в `squashfs-root`. Вы также можете сделать chroot в эту систему для установки пакетов и т.д.:

```
 # arch-chroot squashfs-root /bin/bash

```

**Примечание:** `arch-chroot` является частью пакета [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts)

**Примечание:** Если скрипт `arch-chroot` недоступен в вашей системе (например, при ремастеризации дистрибутивов на основе arch), смонтируйте файловые системы api и скопируйте данные DNS. Для получения допольнительной информации смотрите статью [Chroot#Использование chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_chroot "Change root (Русский)").

Чтобы иметь возможность устанавливать пакеты, вы должны инициализировать pacman keyring:

```
 (chroot) # pacman-key --init
 (chroot) # pacman-key --populate archlinux

```

**Примечание:** Этот шаг может занять довольно долгое время, будьте терпеливыми. (Для получения допольнительной информации смотрите статью [Pacman-Key](/index.php/Pacman/Package_signing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.BD.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B2.D1.8F.D0.B7.D0.BA.D0.B8_.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.B9 "Pacman/Package signing (Русский)"))

Если обновлено ядро или initrd, необходимы дополнительные шаги. В этом случае вам нужно установить [archiso](https://www.archlinux.org/packages/?name=archiso) внутри chroot и изменить содержимое `/etc/mkinitcpio.conf`:

```
 (chroot) # pacman -Syu --force archiso linux
 (chroot) # nano /etc/mkinitcpio.conf

```

Измените строку `HOOKS="...` на:

```
 HOOKS="base udev memdisk archiso_shutdown archiso archiso_loop_mnt archiso_pxe_common archiso_pxe_nbd archiso_pxe_http archiso_pxe_nfs archiso_kms block pcmcia filesystems keyboard"

```

Теперь обновите initramfs:

```
 (chroot) # mkinitcpio -p linux

```

Когда вы закончите, создайте список всех установленных пакетов, очистите кеш pacman и выйдите из chroot:

```
 (chroot) # LANG=C pacman -Sl | awk '/\[installed\]$/ {print $1 "/" $2 "-" $3}' > /pkglist.txt
 (chroot) # pacman -Scc
 (chroot) # exit

```

Если вы обновили ядро или initramfs, переместите их в систему и удалите резервные initramfs (установочный ISO не использует это):

```
 $ mv squashfs-root/boot/vmlinuz-linux ~/customiso/arch/boot/x86_64/vmlinuz
 $ mv squashfs-root/boot/initramfs-linux.img ~/customiso/arch/boot/x86_64/archiso.img
 $ rm squashfs-root/boot/initramfs-linux-fallback.img

```

Переместите список пакетов:

```
 $ mv squashfs-root/pkglist.txt ~/customiso/arch/pkglist.x86_64.txt

```

Теперь заново создайте `airootfs.sfs`:

```
 $ rm airootfs.sfs
 $ mksquashfs squashfs-root airootfs.sfs

```

**Примечание:** В ежемесячном установочном ISO используется параметр `-comp xz` для `mksquashfs`, чтобы значительно уменьшить размер, но это также занимает больше времени

Очистка:

```
 # rm -r squashfs-root

```

Теперь обновите контрольную сумму MD5 `airootfs.sfs`:

```
 $ md5sum airootfs.sfs > airootfs.md5

```

#### Редактирование системы i686

#### Изменение загрузочного образа EFI

Если вы обновили ядро или initramfs и хотите загрузиться в EFI-системах, обновите загрузочный образ EFI. Вам понадобится пакет [dosfstools](https://www.archlinux.org/packages/?name=dosfstools), поскольку загрузочный образ EFI является файловой системой `FAT16`.

```
 $ mkdir mnt
 # mount -t vfat -o loop ~/customiso/EFI/archiso/efiboot.img mnt
 # cp ~/customiso/arch/boot/x86_64/vmlinuz mnt/EFI/archiso/vmlinuz.efi
 # cp ~/customiso/arch/boot/x86_64/archiso.img mnt/EFI/archiso/archiso.img

```

Если вы видите ошибки `Нет места на устройстве`, вам может потребоваться изменить размер `efiboot.img`. Вы также можете создать новый `efiboot.img` и скопировать старые файлы (замените `50` на необходимый размер).

```
 $ dd if=/dev/zero bs=1M count=50 of=efiboot-new.img
 $ mkfs.fat -n "ARCHISO_EFI" efiboot-new.img
 $ mkdir new
 # mount -t fat -o loop efiboot-new.img new
 $ cp -r mnt/* new/
 # umount new mnt
 $ mv efiboot-new.img ~/customiso/EFI/archiso/efiboot.img

```

И используйте новый `efiboot.img`, как указано выше.

### Создание нового ISO

Создайте новый образ ISO с `genisoimage`, который является частью пакета [cdrtools](https://www.archlinux.org/packages/?name=cdrtools), в качестве символической ссылки на `mkisofs`.

```
$ genisoimage -l -r -J -V "ARCH_201209" -b isolinux/isolinux.bin -no-emul-boot -boot-load-size 4 -boot-info-table -c isolinux/boot.cat -o ../arch-custom.iso ./

```

**Примечание:** Метка ISO должна оставаться такой же, как оригинальная метка (в данном случае `ARCH_201209`) для успешной загрузки образа.

**Примечание:** Варианты `-b` и `-c` ожидают пути относительно корня ISO

Полученный образ ISO загрузится только с CD, DVD или BD. Для загрузки с USB-накопителя или жесткого диска ему нужна функция [isohybrid](http://www.syslinux.org/wiki/index.php/Isohybrid). Это может быть достигнуто путем постобработки ISO с помощью программы isohybrid, включенной в пакет [syslinux](https://www.archlinux.org/packages/?name=syslinux). Официально версия установленного SYSLINUX должна быть такой же, как версия /isolinux/isolinux.bin в ISO. Неизвестно, существуют ли действительно несовместимые комбинации версий.

Альтернатива genisoimage plus isohybrid может быть получена из xorriso run mkarchiso.

```
$ iso_label="ARCH_201209"
$ xorriso -as mkisofs \
       -iso-level 3 \  
       -full-iso9660-filenames \
       -volid "${iso_label}" \
       -eltorito-boot isolinux/isolinux.bin \
       -eltorito-catalog isolinux/boot.cat \
       -no-emul-boot -boot-load-size 4 -boot-info-table \
       -isohybrid-mbr ~/customiso/isolinux/isohdpfx.bin \
       -output arch-custom.iso \ 
       ~/customiso

```

Опция -isohybrid-mbr нуждается в файле шаблона [MBR](/index.php/Partitioning_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Partitioning (Русский)"). Скорее всего, в исходном ISO уже есть такой файл /isolinux/isohdpfx.bin, который соответствует версии SYSLINUX, используемой в ISO. Только если этот файл отсутствует в скопированном содержимом ISO, он должен быть вырезан из исходного файла ISO-образа, прежде чем выполняется надстройка xorriso:

```
$ dd if=/path/to/archISO bs=512 count=1 of=~/customiso/isolinux/isohdpfx.bin

```

Если исходный ISO поддерживает загрузку через EFI, это может быть активировано в новом ISO, вставив следующие опции между строками "-isohybrid-mbr ..." и "-output ...":

```
       -eltorito-alt-boot \
       -e EFI/archiso/efiboot.img \
       -no-emul-boot -isohybrid-gpt-basdat \

```

Файл /EFI/archiso/efiboot.img является файлом образа файловой системы FAT. Если в исходном ISO отсутствует, то в этом ISO не было поддержки EFI.

Вновь созданный образ ISO `arch-custom.iso` находится в домашнем каталоге. Вы можете записать образ ISO на USB-накопитель, как описано в [USB-накопитель](/index.php/USB_flash_installation_media_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "USB flash installation media (Русский)"). В качестве альтернативы вы можете записать ISO-образ на CD, DVD или BD с помощью вашего предпочтительного программного обеспечения. В Arch, это описано в [статье об записи образа ISO](/index.php/Optical_disc_drive_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D0.B6.D0.B8.D0.B3_ISO-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_.D0.BD.D0.B0_CD.2C_DVD_.D0.B8.D0.BB.D0.B8_BD "Optical disc drive (Русский)").

## Смотрите также

*   [http://www.knoppix.net/wiki/KnoppixRemasteringHowto](http://www.knoppix.net/wiki/KnoppixRemasteringHowto)
*   [http://syslinux.zytor.com/iso.php](http://syslinux.zytor.com/iso.php)
*   [http://busybox.net/](http://busybox.net/)
*   [Linux Live Kit](http://www.linux-live.org/)