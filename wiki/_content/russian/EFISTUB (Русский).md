**Состояние перевода:** На этой странице представлен перевод статьи [EFISTUB](/index.php/EFISTUB "EFISTUB"). Дата последней синхронизации: 2015-07-29\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=EFISTUB&diff=0&oldid=388777).

**Важно:** Был обнаружен баг, при котором загрузка EFISTUB могла не сработать в зависимости от версии ядра и модели материнской платы. Смотрите [FS#33745](https://bugs.archlinux.org/task/33745) и [[1]](https://bbs.archlinux.org/viewtopic.php?id=156670) для дополнительной информации.

Ядро Linux ([linux](https://www.archlinux.org/packages/?name=linux)>=3.3) поддерживает EFISTUB (EFI BOOT STUB) загрузку. Эта возможность позволяет прошивке EFI загружать ядро как обычное EFI приложение. Эта опция включена по умолчанию в стандартных ядрах Arch Linux, а также её можно активировать при помощи установки `CONFIG_EFI_STUB=y` в конфигурации ядра (смотрите [The EFI Boot Stub](https://www.kernel.org/doc/Documentation/efi-stub.txt) для дополнительной информации).

EFISTUB ядро может быть загружено непосредственно с помощью UEFI материнской платы или же посредственно с использованием [UEFI менеджера загрузки](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA%D0%B8#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D0.B8_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.B8.D0.B2.D0.B0.D1.8E.D1.89.D0.B8.D0.B5_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_UEFI "Загрузчики"). Последний рекомендуется использовать в том случае, если у вас есть несколько ядер/initramfs пар и загрузочное меню UEFI вашей материнской платы неудобное в использовании.

## Contents

*   [1 Настройка EFISTUB](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_EFISTUB)
    *   [1.1 Альтернативные точки монтирования для ESP](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D1.82.D0.BE.D1.87.D0.BA.D0.B8_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_ESP)
        *   [1.1.1 С помощью systemd](#.D0.A1_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_systemd)
        *   [1.1.2 С помощью incron](#.D0.A1_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_incron)
        *   [1.1.3 С помощью хука mkinitcpio](#.D0.A1_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D1.85.D1.83.D0.BA.D0.B0_mkinitcpio)
        *   [1.1.4 С помощью биндинга монтирования](#.D0.A1_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_.D0.B1.D0.B8.D0.BD.D0.B4.D0.B8.D0.BD.D0.B3.D0.B0_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Загрузка EFISTUB](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_EFISTUB)
    *   [2.1 Используя менеджер загрузки](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [2.2 Используя UEFI Shell](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_UEFI_Shell)
    *   [2.3 Используя непосредственно UEFI (efibootmgr)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_.D0.BD.D0.B5.D0.BF.D0.BE.D1.81.D1.80.D0.B5.D0.B4.D1.81.D1.82.D0.B2.D0.B5.D0.BD.D0.BD.D0.BE_UEFI_.28efibootmgr.29)

## Настройка EFISTUB

После создания [системного раздела EFI](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") вы должны выбрать точку монтирования для него. Самый простой способ - это смонтировать его в `/boot`, так как это позволит pacman непосредственно обновлять ядро, которое будет использовать EFI прошивка. Если вы пойдёте по этому пути, переходите к разделу [#Загрузка EFISTUB](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_EFISTUB).

**Обратите внимание:** Вы можете хранить ядро и initramfs не на ESP, если вы используете менеджер загрузки, у которого есть драйвер файловой системы для раздела, в котором они расположены, например [rEFInd](/index.php/REFInd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "REFInd (Русский)").

### Альтернативные точки монтирования для ESP

Если вы примонтируете Системный Раздел EFI куда-либо в другое место (например, в `/boot/efi`), вам нужно будет скопировать загружаемые файлы в эту директорию (здесь и далее будем обозначать её как `$esp`).

```
# mkdir $esp/EFI/arch
# cp /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-linux
# cp /boot/initramfs-linux.img $esp/EFI/arch/initramfs-linux.img
# cp /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-linux-fallback.img

```

Кроме того, вам нужно будет постоянно обновлять файлы на ESP при последующих обновлениях ядра. Если этого не делать, то система может перестать загружаться. Следующие далее разделы описывают механизмы автоматизации данных действий.

#### С помощью systemd

[Systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") умеет выполнять задания при наступлении событий. В данном случае используется возможность отслеживания изменений в определённой папке для синхронизации EFISTUB ядер и initramfs файлов при их обновлении в `/boot`.

 `/etc/systemd/system/efistub-update.path` 
```
[Unit]
Description=Copy EFISTUB Kernel to UEFISYS Partition

[Path]
PathChanged=/boot/initramfs-linux-fallback.img

[Install]
WantedBy=multi-user.target

```

**Обратите внимание:** Здесь используется отслеживание изменений в `initramfs-linux-fallback.img`, так как это последний файл, собранный с помощью mkinitcpio. Это сделано для того, чтобы избежать начала потенциальной гонки, когда systemd может копировать старые файлы до того, как все они будут собраны.
 `/etc/systemd/system/efistub-update.service` 
```
[Unit]
Description=Copy EFISTUB Kernel to UEFISYS Partition

[Service]
Type=oneshot
ExecStart=/usr/bin/cp -f /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-linux
ExecStart=/usr/bin/cp -f /boot/initramfs-linux.img $esp/EFI/arch/initramfs-linux.img
ExecStart=/usr/bin/cp -f /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-linux-fallback.img

```

Включите эти сервисы с помощью:

```
# systemctl enable efistub-update.path

```

Вам нужно будет перезагрузиться либо сказать systemd начать отслеживать папку с помощью:

```
# systemctl start efistub-update.path

```

#### С помощью incron

Чтобы запускать скрипт синхронизации EFISTUB ядра при обновлениях ядра можно использовать [incron](https://www.archlinux.org/packages/?name=incron).

 `/usr/local/bin/efistub-update.sh` 
```
#!/usr/bin/env bash
/usr/bin/cp -f /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-linux
/usr/bin/cp -f /boot/initramfs-linux.img $esp/EFI/arch/initramfs-linux.img
/usr/bin/cp -f /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-linux-fallback.img
```

**Обратите внимание:** Первый параметр `/boot/initramfs-linux-fallback.img` - это файл для отслеживания. Второй параметр `IN_CLOSE_WRITE` - это действие, которое надо отслеживать. Третий параметр `/usr/local/bin/efistub-update.sh` - это скрипт, который будет выполнен.
 `/etc/incron.d/efistub-update.conf`  `/boot/initramfs-linux-fallback.img IN_CLOSE_WRITE /usr/local/bin/efistub-update.sh` 

Чтобы использовать данный метод, включите сервис incrond:

```
# systemctl enable incrond.service

```

#### С помощью хука mkinitcpio

Mkinitcpio может сгенерировать хук, которому для работы не требуется демон системного уровня. Он порождает фоновый процесс, который ждёт генерации `vm-linuz`, `initramfs-linux.img` и `initramfs-linux-fallback.img` перед копированием файлов.

Добавьте `efistub-update` в список хуков в `/etc/mkinitcpio.conf`.

 `/usr/lib/initcpio/install/efistub-update` 
```
#!/usr/bin/env bash
build() {
	/root/watch.sh &
}

help() {
	cat <<HELPEOF
This hook waits for mkinitcpio to finish and copies the finished ramdisk and kernel to the ESP
HELPEOF
}
```
 `/root/watch.sh` 
```
#!/usr/bin/env bash

while [[ -d "/proc/$PPID" ]]; do
	sleep 1
done

/usr/bin/cp -f /boot/vmlinuz-linux $esp/EFI/arch/vmlinuz-linux
/usr/bin/cp -f /boot/initramfs-linux.img $esp/EFI/arch/initramfs-linux.img
/usr/bin/cp -f /boot/initramfs-linux-fallback.img $esp/EFI/arch/initramfs-linux-fallback.img

echo "Synced kernel with ESP"
```

#### С помощью биндинга монтирования

Вместо того, чтобы монтировать сам ESP раздел в `/boot`, вы можете примонтировать директорию ESP раздела в `/boot` используя bind mount (смотрите `mount(8)`). Это позволит pacman обновлять ядро непосредственно, в то же время оставляя организацию ESP на ваше усмотрение. Если это у вас работает, то данный способ является гораздо проще всех остальных, которые копируют файлы.

**Обратите внимание:** Для этого требуется ядро и загрузчик, совместимый с FAT32\. Это не проблема для обычных установок Arch, номожет быть проблемой для других дистрибутивов (а именно тех, которым требуются симлинки в `/boot`). Сообщение на форуме [[здесь](https://bbs.archlinux.org/viewtopic.php?pid=1331867#p1331867)].

Как и [прежде](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B5_.D1.82.D0.BE.D1.87.D0.BA.D0.B8_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.B4.D0.BB.D1.8F_ESP), скопируйте все загружаемые файлы в директорию на вашем ESP, но смонтируйте ESP **вне** `/boot` (например, в `/esp`). Затем примонтируемый каталог:

```
# mount --bind /esp/EFI/arch/ /boot

```

Если ваши файлы появились в `/boot`, как и ожидалось, отредактируйте ваш [Fstab](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)"), чтобы сделать монтирование постоянным:

 `/etc/fstab` 
```
/esp/EFI/arch /boot none defaults,bind 0 0

```

**Важно:** Вы *обязаны* использовать [параметр ядра](/index.php/%D0%9F%D0%B0%D1%80%D0%B0%D0%BC%D0%B5%D1%82%D1%80%D1%8B_%D1%8F%D0%B4%D1%80%D0%B0#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2 "Параметры ядра") `root=*system_root*` для того чтобы загружаться с использованием данного метода.

## Загрузка EFISTUB

**Важно:** Путь до Linux EFISTUB ядра initramfs должен быть относительным к корню Системного Раздела EFI. Например, если initramfs расположен в `$esp/EFI/arch/initramfs-linux.img`, то соответствующей UEFI строкой должна быть `initrd=/EFI/arch/initramfs-linux.img` или `initrd=\EFI\arch\initramfs-linux.img`. В следующих примерах будет предполагаться, что всё расположено в `$esp/`.

### Используя менеджер загрузки

Есть несколько UEFI менеджеров загрузки, которые могут предоставить дополнительные опции или упростить процесс загрузки UEFI, особенно если у вас есть несколько ядер/операционных систем. Смотрите [Загрузчики](/index.php/%D0%97%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D1%87%D0%B8%D0%BA%D0%B8 "Загрузчики") для дополнительной информации.

### Используя UEFI Shell

Есть возможность запускать EFISTUB ядро из UEFI Shell как обычное UEFI приложение. В этом случае параметры ядра передаются как обычные параметры запускаемому файлу EFISTUB ядра.

```
> fs0:
> /vmlinuz-linux root=PARTUUID=3518bb68-d01e-45c9-b973-0b5d918aae96 initrd=/initramfs-linux.img

```

Чтобы избежать необходимости каждый раз вспоминать все параметры вашего ядра, вы можете сохранить исполняемую команду в shell скрипт, например в `archlinux.nsh` на вашем Системном Разделе UEFI, а затем запустить её с помощью:

```
> fs0:
> archlinux

```

### Используя непосредственно UEFI (efibootmgr)

UEFI [разработан так, чтобы убрать необходимость](/index.php/UEFI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9C.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_UEFI "UEFI (Русский)") наличия промежуточных загрузчиков, таких как [GRUB](/index.php/GRUB_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB (Русский)"). Если ваша материнская плата имеет хорошую реализацию UEFI, есть возможность вставлять параметры ядра внутрь загрузочных записей UEFI и материнская плата сможет загружать непрсредственно Arch. Вы можете использовать `efibootmgr` чтобы модифицировать загрузочные записи вашей материнской платы изнутри Arch.

```
# efibootmgr -d /dev/sd**X** -p **Y** -c -L "Arch Linux" -l /vmlinuz-linux -u "root=**/dev/sda2** rw initrd=/initramfs-linux.img"

```

Где `X` и `Y` замените на соответсвующий диск и раздел, где находится ваш ESP. Измените параметр `root=`, чтобы он соответствовал корню вашего Linux (также можно использовать UUID диска).

**Или** с помощью действия [приостановки на диск](/index.php/Suspend_and_hibernate#Required_kernel_parameters "Suspend and hibernate"):

```
# efibootmgr -d /dev/sd**X** -p **Y** -c -L "Arch Linux" -l /vmlinuz-linux -u "root=**/dev/sda2** rw resume=**/dev/sda4** initrd=/initramfs-linux.img"

```

Измените параметр `resume=` на соответствующий вашему swap разделу, оставив остальные параметры такими, как описано выше.

Затем хорошей идеей будет выполнение

```
# efibootmgr -v

```

для проверки того, что получившаяся запись корректна.

**Важно:** Некоторые комбинации версий ядер и `efibootmgr` могут отказываться создавать новые загрузочные записи. Это может происходить из-за того что не хватает свободного места в NVRAM. Вы можете попробовать удалить какие-нибудь мусорные EFI файлы
```
# rm /sys/firmware/efi/efivars/dump-*

```
Или же, в качестве последней надежды, загрузитесь с параметром ядра `efi_no_storage_paranoia`. Вы также можете попробовать откатить efibootmgr до версии 0.11.0, если она доступна в вашем кеше. Эта версия работает с Linux версии 4.0.6\. Смотрите обсуждение ошибки [FS#34641](https://bugs.archlinux.org/task/34641) для дополнительной информации.

Чтобы задать порядок загрузки выполните:

```
# efibootmgr -o XXXX,XXXX

```

где XXXX - это номер, который появляется в выводе команды `efibootmgr` напротив каждой записи.

**Совет:** Сохраните где-нибудь команду для создания вашей загрузочной записи в шелл скрипте, который поможет вам при изменениях (например, когда вы захотите изменить параметры ядра).

Дополнительную информацию по efibootmgr смотрите в [UEFI (Русский)#efibootmgr](/index.php/UEFI_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#efibootmgr "UEFI (Русский)"). Пост на форуме [https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040](https://bbs.archlinux.org/viewtopic.php?pid=1090040#p1090040) .