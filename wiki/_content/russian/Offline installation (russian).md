**Состояние перевода:** На этой странице представлен перевод статьи [Offline installation](/index.php/Offline_installation "Offline installation"). Дата последней синхронизации: 4 декабря 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Offline_installation&diff=0&oldid=558330).

Ссылки по теме

*   [Offline installation of packages (Русский)](/index.php/Offline_installation_of_packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Offline installation of packages (Русский)")
*   [Archiso offline](/index.php/Archiso_offline "Archiso offline")

Если вы хотите установить [Archiso (Русский)](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") (например, [официальный ежемесячный выпуск](https://www.archlinux.org/download/)) без подключения к интернету или если вы не хотите загружать пакеты снова:

Сначала следуйте инструкциям [руководства по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Installation guide (Русский)"), а потом пропустите разделы от [Соединение с Интернетом](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Соединение_с_Интернетом "Installation guide (Русский)") до [Установка основных пакетов](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_основных_пакетов "Installation guide (Русский)").

## Contents

*   [1 Установка archiso в новый корень](#Установка_archiso_в_новый_корень)
*   [2 Chroot и настройка базовой системы](#Chroot_и_настройка_базовой_системы)
    *   [2.1 Восстановление конфигурации journald](#Восстановление_конфигурации_journald)
    *   [2.2 Удаление особых правил udev](#Удаление_особых_правил_udev)
    *   [2.3 Отключение и удаление служб, созданных archiso](#Отключение_и_удаление_служб,_созданных_archiso)
    *   [2.4 Удаление особых скриптов Live среды](#Удаление_особых_скриптов_Live_среды)
    *   [2.5 Импорт ключей archlinux](#Импорт_ключей_archlinux)
    *   [2.6 Настройка системы](#Настройка_системы)

## Установка archiso в новый корень

Вместо того, чтобы устанавливать пакеты с помощью `pacstrap` (которые будут пытаться загрузить из удаленных репозиториев), скопируйте *всё* в live среду в новый корень:

```
# cp -ax / /mnt

```

**Примечание:** Опция (`-x`) исключает некоторые специальные каталоги, так как они не должны копироваться в новый корень.

Затем скопируйте образ ядра в новый корень, чтобы сохранить целостность новой системы:

```
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux

```

После этого сгенерируйте fstab, как описано в [руководстве по установке#Fstab](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Fstab "Installation guide (Русский)").

## Chroot и настройка базовой системы

Далее, сделать операцию chroot в вашей вновь установленной системы:

```
# arch-chroot /mnt /bin/bash

```

**Примечание:** Перед выполнением других шагов [руководства по установке#Настройка системы](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка_системы "Installation guide (Русский)") (например, локаль, раскладка клавиатуры и т.д.) необходимо избавиться от следов Live среды (другими словами, настройка archiso, которая не соответствует Live среде).

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

Некоторые файлы служб создаются для Live среды, отключите их и удалите файлы, поскольку они не нужны в новой системе:

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

### Удаление особых скриптов Live среды

Есть некоторые скрипты, которые установлены в live системе скриптами archiso, которые не нужны для новой системы:

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

### Импорт ключей archlinux

Чтобы использовать официальные репозитории, нам нужно импортировать главные ключи archlinux ([pacman/Package signing (Русский)#Инициализация связки ключей](/index.php/Pacman/Package_signing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Инициализация_связки_ключей "Pacman/Package signing (Русский)")). Этот шаг обычно делается с помощью pacstrap, но может быть достигнут с помощью

```
# pacman-key --init
# pacman-key --populate archlinux

```

**Примечание:** Клавиатура или мышь должны быть подключёнными для генерации энтропии и ускорения первого шага.

### Настройка системы

Теперь вы можете выполнить пропущенные шаги раздела [руководства по установке#Настройка системы](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка_системы "Installation guide (Русский)") (установка локали, часовой пояс, имя хоста и т.д.) и завершить установку, создав исходный ramdisk, как описано в [руководстве по установке#Initramfs](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Initramfs "Installation guide (Русский)").