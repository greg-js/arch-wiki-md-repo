**Состояние перевода:** На этой странице представлен перевод статьи [Offline installation](/index.php/Offline_installation "Offline installation"). Дата последней синхронизации: 4 декабря 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Offline_installation&diff=0&oldid=558330).

Ссылки по теме

*   [Offline installation of packages (Русский)](/index.php/Offline_installation_of_packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Offline installation of packages (Русский)")
*   [Archiso offline](/index.php/Archiso_offline "Archiso offline")

Если вы хотите установить [Archiso (Русский)](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") (например, [официальный ежемесячный выпуск](https://www.archlinux.org/download/)) без подключения к интернету или если вы не хотите загружать пакеты снова:

Сначала следуйте инструкциям статьи [Руководство по установке](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5 "Руководство по установке"), а затем пропустите разделы от [Соединения с Интернетом](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Соединение_с_Интернетом "Installation guide (Русский)") до [Установки основных пакетов](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_основных_пакетов "Installation guide (Русский)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка archiso в новый корень](#Установка_archiso_в_новый_корень)
*   [2 Chroot и настройка базовой системы](#Chroot_и_настройка_базовой_системы)
    *   [2.1 Восстановление конфигурации journald](#Восстановление_конфигурации_journald)
    *   [2.2 Удаление особых правил udev](#Удаление_особых_правил_udev)
    *   [2.3 Отключение и удаление служб, созданных archiso](#Отключение_и_удаление_служб,_созданных_archiso)
    *   [2.4 Удаление особых скриптов live-среды](#Удаление_особых_скриптов_live-среды)
    *   [2.5 Импорт ключей archlinux](#Импорт_ключей_archlinux)
    *   [2.6 Настройка системы](#Настройка_системы)

## Установка archiso в новый корень

Вместо того, чтобы устанавливать пакеты с помощью `pacstrap` (которые будут загружаться из удалённых репозиториев), скопируйте *всё* в live-среду в новый корень:

```
# cp -ax / /mnt

```

**Примечание:** Опция (`-x`) исключает некоторые специальные каталоги, которые не должны копироваться в новый корень.

Затем скопируйте образ ядра в новый корень, чтобы сохранить целостность новой системы:

```
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux

```

После этого сгенерируйте fstab, как описано в разделе [Руководство по установке#Fstab](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5#Fstab "Руководство по установке").

## Chroot и настройка базовой системы

Далее, выполните операцию chroot в вашей вновь установленной системы:

```
# arch-chroot /mnt /bin/bash

```

**Примечание:** Перед выполнением следующих шагов раздела [Руководство по установке#Настройка системы](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5#Настройка_системы "Руководство по установке") (например, локаль, раскладка клавиатуры и т.д.) необходимо избавиться от следов live-среды (другими словами, настройка archiso, которая не соответствует live-среде).

### Восстановление конфигурации journald

[Эта настройка archiso](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n19) приведёт к сохранению системного журнала в ОЗУ, а это означает, что журнал после перезагрузки будет недоступен:

```
# sed -i 's/Storage=volatile/#Storage=auto/' /etc/systemd/journald.conf

```

### Удаление особых правил udev

[Это правило udev](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) автоматически запускает dhcpcd, если есть какие-либо проводные сетевые интерфейсы.

```
# rm /etc/udev/rules.d/81-dhcpcd.rules

```

### Отключение и удаление служб, созданных archiso

Некоторые файлы служб создаются для live-среды – отключите их и удалите файлы, поскольку они не нужны в новой системе:

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

### Удаление особых скриптов live-среды

Существуют некоторые скрипты, установленные скриптами archiso в live-системе, которые не нужны для новой системы:

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

### Импорт ключей archlinux

Чтобы использовать официальные репозитории, нужно импортировать главные ключи archlinux ([pacman/Package signing (Русский)#Инициализация связки ключей](/index.php/Pacman/Package_signing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Инициализация_связки_ключей "Pacman/Package signing (Русский)")). Этот шаг обычно делается с помощью pacstrap, но может быть выполнен с помощью

```
# pacman-key --init
# pacman-key --populate archlinux

```

**Примечание:** Подключите клавиатуру или мышь для генерации энтропии и ускорения первого шага.

### Настройка системы

Теперь вы можете выполнить пропущенные шаги раздела [Руководство по установке#Настройка системы](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5#Настройка_системы "Руководство по установке") (установка локали, часовой пояс, имя хоста и т.д.) и завершить установку, создав исходный ramdisk, как описано в разделе [Руководство по установке#Initramfs](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5#Initramfs "Руководство по установке").