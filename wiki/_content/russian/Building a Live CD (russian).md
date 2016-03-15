## Contents

*   [1 Зачем создавать Live CD?](#.D0.97.D0.B0.D1.87.D0.B5.D0.BC_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.B2.D0.B0.D1.82.D1.8C_Live_CD.3F)
*   [2 Прежде чем начать, вам потребуется](#.D0.9F.D1.80.D0.B5.D0.B6.D0.B4.D0.B5_.D1.87.D0.B5.D0.BC_.D0.BD.D0.B0.D1.87.D0.B0.D1.82.D1.8C.2C_.D0.B2.D0.B0.D0.BC_.D0.BF.D0.BE.D1.82.D1.80.D0.B5.D0.B1.D1.83.D0.B5.D1.82.D1.81.D1.8F)
*   [3 Детали](#.D0.94.D0.B5.D1.82.D0.B0.D0.BB.D0.B8)
    *   [3.1 Загрузитесь с помощью Arch Linux CD installer и установите базовые пакеты](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.B8.D1.82.D0.B5.D1.81.D1.8C_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_Arch_Linux_CD_installer_.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D0.B5_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
    *   [3.2 Установите isolinux. Скопируйте его с Live CD](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D0.B5_isolinux._.D0.A1.D0.BA.D0.BE.D0.BF.D0.B8.D1.80.D1.83.D0.B9.D1.82.D0.B5_.D0.B5.D0.B3.D0.BE_.D1.81_Live_CD)
    *   [3.3 Создайте один miniroot образ](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.B9.D1.82.D0.B5_.D0.BE.D0.B4.D0.B8.D0.BD_miniroot_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7)
    *   [3.4 Заключение](#.D0.97.D0.B0.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
*   [4 Дополнительная информация:](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D1.8F:)

### Зачем создавать Live CD?

Часто бывает удобно иметь под рукой версию Arch Linux, работающую полностью с CD. Live CD может использоваться для восстановления вашей системы, для проверки новых машин или оборудования на совместимость с GNU/Linux, для создания демонстрационного диска для показа ваших проектов и многого другого.

### Прежде чем начать, вам потребуется

1.  Для создания iso-образа, форматирования файловой системы и для изменения размера образа, вам понадобятся пакеты "cdrtools" и "e2fsprogs".

```
pacman -S cdrtools
pacman -S e2fsprogs

```

1.  Также вам понадобится создать на жестком диске
    1.  1 раздел для установки дистрибутива
    2.  1 директория на вашем активном разделе, чтобы сохранить образ для записи на диск.
2.  CD-RW диск для записи и проверки разных версий образов, и пишущий привод.
3.  Установить пакет для записи CD (если вы не знаете, что выбрать, устанавливайте "k3b").

```
pacman -S k3b

```

или

```
pacman -S brasero

```

### Детали

Для примера, в этой статье мы рассмотрим создание mini Arch Linux Live CD (110MB). Он основан на базовых пакетах, установленных с помощью Arch Linux's CD installer версии 0.5

#### Загрузитесь с помощью Arch Linux CD installer и установите базовые пакеты

Установив пакеты, установите ядро, но не устанавливайте загрузчик. Также вы можете копировать образ вашего собсвенного ядра (<tt>/boot/vmlinuz</tt>), и соответствующих ему модулей (<tt>/lib/modules/2.x.x</tt>) с вашей системы. Чтобы загрузиться в новую систему, настройте соответствующим образом ваш загрузчик.

**Совет:** Для проверки на наличие ошибок в процессе загрузки, примонтируйте раздел с новой системой в ваш Arch Linux и исправьте следующие строчки в файле <tt>/etc/rc.local</tt> для приостановки системы перед аутентификацей пользователя:

```
echo "Press any key to continue..."
read KEY

```

**Внимание:** Не забудьте убрать паузу!!

В вашей системе, в <tt>/root</tt> создайте каталог "*mylivecd*" и два подкаталога: "*isolinux*" и "*system*" (вы можете использовать свои имена).

```
# cd /root
# mkdir mylivecd
# cd mylivecd
# mkdir isolinux
# mkdir system

```

#### Установите isolinux. Скопируйте его с Live CD

1.  Загрузите "*isolinux.bin*" и "*boot.cat*" в каталог <tt>/root/mylivecd/isolinux/</tt> :

[http://amlug.bliss-solutions.org/live-cd/distfiles/0.5.1/isolinux/](http://amlug.bliss-solutions.org/live-cd/distfiles/0.5.1/isolinux/)

1.  Создайте загрузочное сообщение "*boot.msg*" (текстовый файл) и запишите туда краткое описание вашего live CD. Сохраните этот файл в <tt>/root/mylivecd/isolinux/</tt>.

Пример <tt>boot.msg</tt>:

```
This is a Live CD test ver. 0.1.
F1 - boot message
F2 - package list

 Press Enter

```

1.  Создайте "*isolinux.cfg*" и поместите туда следующий текст. Сохраните файл в <tt>/root/mylivecd/isolinux/</tt>

```
prompt 1
timeout 0
display boot.msg
F1 boot.msg
F2 package.txt
default vmlinuz initrd=miniroot.gz init=/sbin/init ramdisk_size=100000 load_ramdisk=1 prompt_ramdisk=0 vga=788 root=/dev/ram0

```

#### Создайте один miniroot образ

Miniroot загружается в оперативную память во время загрузки и действует также как и на HD. Используйте файловую систему Ext2.

**Внимание:** Настройка miniroot зависит от <tt>/etc/inittab</tt>, <tt>/etc/rc.sysinit</tt>, <tt>/etc/rc.multi</tt>, и <tt>/etc/rc.shutdown</tt>. Перед созданием miniroot-образа, внимательно изучите эти файлы и продумайте как они могут быть изменены при необходимости. В каталоге <tt>/sbin</tt> вам понадобятся слеующие файлы:
[http://amlug.bliss-solutions.org/live-cd/distfiles/0.5.1/miniroot/init/sbin/](http://amlug.bliss-solutions.org/live-cd/distfiles/0.5.1/miniroot/init/sbin/)

1.  Создайте текстовый файл "*miniroot*" в <tt>/root/mylivecd</tt> с файловой системой Ext2\. Размер образа зависит от того, как много пакетов вы собираетесь включить в него. В нашем примере мы создадим образ 15.8MB. Рекомендуется создавать образ как можно меньше. Когда будете готовы, примонтируйте образ например в <tt>/mnt/image</tt>

```
# cd /root/mylivecd
# touch miniroot
# mkfs.ext2 miniroot 15840 (press "y" for each question)
# mkdir /mnt/image
# mount -t auto -o loop miniroot /mnt/image
# rm -R /mnt/image/lost+found

```

**Внимание:** Если вы хотите поменять размер, используйте следующие команды (для уменьшения размера до 11.5MB):

```
# e2fsck -f miniroot (press "y" for /lost+found not found.  Create<y>?)
# resize2fs miniroot 11520

```

1.  Примонтируйте раздел с новой системой. Копируйте файлы и каталоги из нового раздела в <tt>/mnt/image</tt>

```
# mkdir /mnt/tmp
# mount /dev/hda3 /mnt/tmp
# cp -Ra /mnt/tmp/bin /mnt/image/
# cp -Ra /mnt/tmp/etc /mnt/image/
# cp -Ra /mnt/tmp/sbin /mnt/image/
# cp -Ra /mnt/tmp/tmp /mnt/image/
# cp -Ra /mnt/tmp/var /mnt/image/

```

1.  Копируйте <tt>/usr</tt>, <tt>/lib/modules/2.x.x/</tt>, <tt>/lib/modules/evms/</tt>, <tt>/lib/modules/security/</tt> в <tt>/root/mylivecd/system/</tt> :

```
# cp -Ra /mnt/tmp/usr /root/mylivecd/system/
# cp -Ra /mnt/tmp/opt /root/mylivecd/system/
# mkdir /root/mylivecd/system/lib
# cp -Ra /mnt/tmp/lib/modules /root/mylivecd/system/lib/
# cp -Ra /mnt/tmp/lib/evms /root/mylivecd/system/lib/
# cp -Ra /mnt/tmp/lib/security /root/mylivecd/system/lib/

```

**Внимание:** : Если <tt>/bin</tt> и <tt>/sbin</tt> слишком велики вы можете попробовать использовать busybox: [http://www.busybox.net/](http://www.busybox.net/) **Или** использовать временные папки, которые будут удалены или переименованы при загрузке <tt>/rc.sysinit</tt>. Здесь пример как это можно сделать: [http://amlug.bliss-solutions.org/live-cd/distfiles/0.5.1/miniroot/init/sbin/rc.sysinit](http://amlug.bliss-solutions.org/live-cd/distfiles/0.5.1/miniroot/init/sbin/rc.sysinit)

1.  Создайте следующие каталоги в <tt>/mnt/image</tt> и копируйте <tt>/mnt/tmp/lib</tt> файлы в <tt>/mnt/image/lib/</tt> (не копируйте <tt>/mnt/tmp/lib/module</tt>, <tt>~/lib/evms</tt> и <tt>~/lib/security)</tt>:

```
# cd /mnt/image
# mkdir dev
# mkdir home
# mkdir lib
# mkdir mnt/cdrom
# mkdir mnt/floppy
# mkdir root
# mkdir proc
# mkdir lib/modules
# cd /mnt/tmp/lib/
# cp -a l* /mnt/image/lib/

```

1.  С каталогами <tt>/usr</tt> и <tt>/opt</tt> создайте ссылки в <tt>/mnt/image/</tt>. Также создайте ссылку на <tt>/system/lib/modules/2.x.x/</tt>. Копируйте образ ядра в <tt>/root/mylivecd/isolinux/</tt>:

```
# cd /mnt/image
# ln -sf /mnt/cdrom/system/usr usr
# ln -sf /mnt/cdrom/system/opt opt
# cd /mnt/image/lib/modules/
# ln -sf /mnt/cdrom/system/lib/modules/2.4.22 2.4.22
# cd /mnt/image/lib/
# ln -sf /mnt/cdrom/system/lib/evms evms
# ln -sf /mnt/cdrom/system/lib/security security
# cp /mnt/tmp/boot/vmlinuz /root/mylivecd/isolinux/

```

1.  Исправьте <tt>/mnt/image/etc/fstab как показано здесь:</tt>

```
/dev/root      /      ext2    defaults 0 0
none           /proc  proc    defaults 0 0
/dev/floppy/0          /mnt/floppy   auto      user,rw,noauto,unhide     0      0
/dev/cdroms/cdrom0     /mnt/cdrom   iso9660   ro,user,noauto,unhide  0      0

```

1.  Добавьте следующие строчки в файл <tt>rc.sysinit</tt> (после строки: <tt>stat_busy "Mounting Local Filesystems"</tt>) в <tt>/mnt/image/etc/</tt>. Это позволит чтение файлов из каталога /system с CD.

```
/bin/mount /dev/cdroms/cdrom0 /mnt/cdrom -o ro -t iso9660

```

1.  Сожмите miniroot и поместите miniroot.gz в /root/mylivecd/isolinux/

```
# cd /root/mylivecd/
# umount /mnt/image
# gzip -c miniroot >> miniroot.gz
# mv miniroot.gz isolinux/

```

1.  Перед компиляцией, переместите <tt>/root/mylivecd/miniroot</tt> в безопасное место. Создайте временный каталог для iso образа (не внутри <tt>/mylivecd</tt>). Выполните следующий код (не забудьте "." в конце строки):

```
# cd /root/mylivecd
# mkdir /root/isotmp

```

1.  Создайте ISO:

```
mkisofs -o /root/isotmp/test-livecd-0.1.iso -R -V "Test 0.1" \
-T -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot \
-boot-load-size 4 -boot-info-table -A "Test Live CD 0.1" .

```

#### Заключение

Надеемся это руководство помогло вам. Удачи!

* * *

### Дополнительная информация:

Исходные коды и содержимое AMLUG Live CD: [http://www.amlug.net/new-projects/forum/index.php?showforum=23](http://www.amlug.net/new-projects/forum/index.php?showforum=23)

Создание Live CD в других дистрибутивах: [http://www.babytux.org/articles/howto/how2livecd.php](http://www.babytux.org/articles/howto/how2livecd.php)

* * *