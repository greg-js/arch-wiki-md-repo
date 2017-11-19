Ссылки по теме

*   [File systems](/index.php/File_systems "File systems")
*   [Ext3](/index.php/Ext3 "Ext3")

Ext4 - результат эволюции файловой системы ext3\. Ext4 в сравнении с ext3 сильнее улучшена, чем ext3 по сравнению с ext2\. В ext3 практически просто добавили журналирование, а ext4 изменена более кардинально. В результате получилась ФС с улучшенным дизайном, производительностью, стабильностью, и расширенными возможностями.

Source: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

## Contents

*   [1 Создание раздела ext4 с нуля](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0_ext4_.D1.81_.D0.BD.D1.83.D0.BB.D1.8F)
*   [2 Миграция с ext3 на ext4 без потери данных](#.D0.9C.D0.B8.D0.B3.D1.80.D0.B0.D1.86.D0.B8.D1.8F_.D1.81_ext3_.D0.BD.D0.B0_ext4_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.BE.D1.82.D0.B5.D1.80.D0.B8_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85)
    *   [2.1 Монтировать ext3 как ext4 без конвертирования](#.D0.9C.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D1.82.D1.8C_ext3_.D0.BA.D0.B0.D0.BA_ext4_.D0.B1.D0.B5.D0.B7_.D0.BA.D0.BE.D0.BD.D0.B2.D0.B5.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [2.1.1 Обоснование](#.D0.9E.D0.B1.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
        *   [2.1.2 Сам процесс](#.D0.A1.D0.B0.D0.BC_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81)
    *   [2.2 Конвертирование ext3 в ext4](#.D0.9A.D0.BE.D0.BD.D0.B2.D0.B5.D1.80.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_ext3_.D0.B2_ext4)
        *   [2.2.1 Обоснование](#.D0.9E.D0.B1.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_2)
        *   [2.2.2 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [2.2.3 Сам процесс](#.D0.A1.D0.B0.D0.BC_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81_2)
        *   [2.2.4 Migrating files to extents](#Migrating_files_to_extents)
*   [3 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.1 Удаление зарезервированных блоков](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D1.80.D0.B5.D0.B7.D0.B5.D1.80.D0.B2.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.B1.D0.BB.D0.BE.D0.BA.D0.BE.D0.B2)
*   [4 Возможные проблемы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [4.1 Kernel Panic](#Kernel_Panic)
    *   [4.2 Потеря данных](#.D0.9F.D0.BE.D1.82.D0.B5.D1.80.D1.8F_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85)
        *   [4.2.1 E4rat](#E4rat)

## Создание раздела ext4 с нуля

1.  Обновите систему: `pacman -Syu`
2.  Отформатируйте раздел: `mkfs.ext4 /dev/sdxY` (замените `sdxY` устройством, которое собрались форматировать (например `sda1`))
3.  Монтируйте раздел
4.  Добавьте пункт в `/etc/fstab`, в качестве типа ФС укажите ext4

**Tip:** Прочитайте ман по mkfs.ext4 для других опций; редактируйте `/etc/mke2fs.conf` чтобы изменить/посмотреть стандартные опции.

## Миграция с ext3 на ext4 без потери данных

Есть два способа:

*   монтировать ext3 как ext4 без конвертирования (совместимость)
*   конвертировать раздел ext3 в ext4 (производительность)

Оба способа описаны ниже.

### Монтировать ext3 как ext4 без конвертирования

#### Обоснование

Компромисс между полным преобразованием в ext4 и использованием ext3 это монтирование ext3 как ext4.

**Плюсы:**

*   Совместимость (ФС может быть монтирована как ext3 и ext4) – Это позволит пользователю читать ФС с дистрибьютивами/программами не поддерживающими ext4 (например Windows с драйвером для ext3)
*   Увеличенная производительность (менее производительно чем полное конвертирование) – Подробности: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

**Минусы:**

*   Используются не все возможности ext4

**Примечание:** Не считая относительной новизны ext4 (которую можно рассматривать как риск), **однако крупных недостатков у этой техники нет**.

#### Сам процесс

1.  Отредактируйте `/etc/fstab` и поменяйте тип ФС с ext3 на ext4 для раздела, который хотите монтировать как ext4.
2.  Размонтируйте раздел/разделы, и снова примонтируйте.
3.  Готово.

### Конвертирование ext3 в ext4

#### Обоснование

To experience the benefits of ext4, an irreversible conversion process must be completed.

**Плюсы:**

*   Лучшая производительность и все новые фичи ext4 – Подробности: [Ext4 - Linux Kernel Newbies](http://kernelnewbies.org/Ext4)

**Минусы:**

*   Только чтение доступно из под windows (Ext2Explore), т.к. сейчас нет драйверов для записи.
*   Необратимость (Откат с ext4 до ext3 невозможен)

#### Требования

**Примечание:** Патч ext4 по умолчанию включен в пакет grub для Archlinux (по крайней мере на момент написания, но скорей всего он будет включен и позже). В противном случае можно установить grub2.

**Важно:** Загрузка с ext4 "официально" не поддерживается grub, и в grub2 в процессе разработке. While GRUB does currently work, the 'safe' option is to boot from an ext2 or ext3 /boot partition. **Вы были предупреждены!**

**Примечание:** Рекомендуется использовать последний релиз Archlinux. Дистрибьютивы старее 2008.06 поставляются со старой версией `e2fsprogs`, но это решается с помощью `pacman -S e2fsprogs`. Кстати, [SystemRescueCd >= 1.1.4](http://www.sysresccd.org/Download) содержит соответствующую версию, полезно иметь при себе liveCD.

#### Сам процесс

Следующие инструкции были обновлены из [http://ext4.wiki.kernel.org/index.php/Ext4_Howto](http://ext4.wiki.kernel.org/index.php/Ext4_Howto) и [https://bbs.archlinux.org/viewtopic.php?id=61602](https://bbs.archlinux.org/viewtopic.php?id=61602), они были проверены и подтверждены автором 16-ого января 2009 года.

*   **Обновитесь!** Обновите систему, чтобы все пакеты были последних версий: `pacman -Syu`
*   **[Резервное копирование!](/index.php/Backup_programs_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Backup programs (Русский)")** Скопируйте все данные с интересующего вас ext3 раздела. не смотря на то, что ext4 считается стабильным, это его довольно молодая и непроверенная ФС. Кроме того это руководство было протестировано на довольно "простой" системе, невозможно предсказать поведение множества программ установленных различными пользователями.
*   Редактируйте `/etc/fstab` и смините тип ФС с ext3 на ext4 для интересующих вас разделов.

**Важно:** ext4 обратно совместима с ext3 пока расширения(?) и другие новые опции не включены. Вы сможете использовать ваш раздел как ext3 вплоть до следующего шага! После следующего шага ОС/программы не поддерживающие ext4 не смогут работать с вашим разделом.

*   Процесс конвертации `e2fsprogs` не может быть осуществлен, пока раздел монтирован. Если речь идет о корневом разделе (/), самы простой способ это загрузиться с liveCD/USB или другого диска/раздела.
    *   Загрузитесь с live раздела (если необходимо).
    *   Для каждого раздела, который необходимо конвертировать:
        *   Убедитесь, что раздел **НЕ** монтирован
        *   Запустите `tune2fs -O extents,uninit_bg,dir_index /dev/the_partition` (где `/dev/the_partition` это интересующий нас раздел, например `/dev/sda1`)
        *   Запустите `fsck -fDp /dev/the_partition`

**Примечание:** Пользователь **ДОЛЖЕН** проверить раздел с помощью fsck, иначе раздел будет не читабилен! Запуск fsck нужен чтобы вернуть ФС в непротиворечивое(consistent) состояние. **Обязательно обнаружатся ошибки** -- это ожидается, так и должно быть. Параметр '-f' "говорит" fsck проверить раздел на ошибки даже если он кажется ему правельным. Параметр '-p' заставляет fsck автоматически устранять ошибки (иначе пользователю будет задан вопрос относительно каждой ошибки). Возможно вам придется запустить fsck -f вместо fsck -fp.

*   Перезапустите Arch Linux!

**Важно:** Если вы конвертировали ваш корневой (/) раздел, при загрузки может произойти kernel panic. Если это случилось, просто загрузитесь используя аварийный (fallback) ramdisk и пересоздайте дефолтный ramdisk: `mkinitcpio -p linux`

#### Migrating files to extents

**Важно:** Do **NOT** use the following method with Mercurial repository that have been cloned locally, as doing so will corrupt the repository. It might also corrupt other hard link in the filesystem.

Even though the filesystem is now converted to ext4, all files that have been written before the conversion do not yet take advantage of the new *extents* of ext4, which will improve large file performance and reduce fragmentation and filesystem check time. In order to fully take advantage of ext4, all files would have to be rewritten on disk. A utility called *e4defrag* is being developed and will take care of this task ; however, it is not yet ready for production.

Fortunately, it is possible to use the *chattr* program, which will cause the kernel to rewrite the file using extents. It is possible to run this command on all files and directories of one partition (e.g. if /home is on a dedicated partition): (Must be run as root)

```
find /home -xdev -type f -print0 | xargs -0 chattr +e
find /home -xdev -type d -print0 | xargs -0 chattr +e

```

It is recommended to test this command on a small number of files first, and check if everything is going all right. It may also be useful to check the filesystem after conversion.

Using the *lsattr* command, it is possible to check that files are now using *extents*. The letter 'e' should appear in the attribute list of the listed files.

## Советы и рекомендации

### Удаление зарезервированных блоков

По умолчанию 5% ФС помечено как зарезервированное для пользователя root. Для современных дисков большого объема это более чем необходимо, особенно если раздел используется для системных файлов. Обычно безопасно можно снизить процент резервированных блоков, если раздел

*   Очень большой (например больше 50 Гб)
*   Не используется для системных файлов

Можно воспользоваться tune2fs для этого. Следующая команда устанавливает процент зарезервированных блоков на диске /dev/sdXY равным 1%:

```
tune2fs -m 1 /dev/sdXY

```

## Возможные проблемы

### Kernel Panic

One problem this author encountered was a kernel panic after converting the root (/) partition to ext4\. This is because the initial ramdisk was detecting the partition as 'ext4dev', rather than 'ext4'. It was a simple matter to boot with the 'fallback' initial ramdisk and re-create the 'default' initial ramdisk :

*   Remount the root partition in read-write mode; assuming 'XXX' is your root partition :

```
# mount /dev/XXX / -o remount,rw

```

*   Manually mount the boot partition on /boot if it is on a separate partition.
*   Re-create the ramdisk :

```
# mkinitcpio -p linux

```

During the creation process, `mkinitcpio` correctly detected and included ext4 modules in the initial ramdisk.

### Потеря данных

Некоторые из ранних пользователей ext4 столкнулись с потерей данных после жесткой перезагрузки (отключение питания или reset на системном блоке). Подробнее описано [Ext4 data loss; explanations and workarounds](http://www.h-online.com/open/Ext4-data-loss-explanations-and-workarounds--/news/112892).

С выходом ядра версии 2.6.30 ext4 считается безопасной. Некоторые патчи улучшили "стойкость", однако слегка снизили производительность. Можно использовать новую опцию монтирования `auto_da_alloc`) чтобы отключить подобное поведение. Подробнее: [Linux 2 6 30 - Filesystems performance improvements](http://kernelnewbies.org/Linux_2_6_30#head-329ba44b44a7f58c98ae22b8f2730418cdd6630d).

Для ядра старше 2.6.30 (<2.6.30), в качестве превентивной меры, можно добавить `rootflags=data=ordered` в строку связанную с `kernel` в файле `menu.lst` для grub.

#### E4rat

[E4rat](/index.php/E4rat "E4rat") это программа, разработанная для ext4\. Она следит за файлами, используемыми при загрузке системы, и оптимизирует их расположение на диске, чтобы уменьшить время доступа к ним, и подгружает их в самом начале процесса загрузки.