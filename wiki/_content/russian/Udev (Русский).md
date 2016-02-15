По функциональности _udev_ заменяет _hotplug_ и _hwdetect_.

Из [статьи о udev на Википедии](https://en.wikipedia.org/wiki/ru:Udev "wikipedia:ru:Udev"):

	_"udev — менеджер устройств для новых версий ядра Linux, являющийся преемником devfs, hotplug и HAL. Его основная задача — обслуживание файлов устройств в каталоге `/dev` и обработка всех действий, выполняемых в пространстве пользователя при добавлении/отключении внешних устройств, включая загрузку firmware."_

В целях обеспечения лучшей производительности _udev_ загружает модули ядра асинхронно, то есть параллельно, а не последовательно. В этом есть свой недостаток: _udev_ не сохраняет порядок загрузки модулей, он может отличаться от загрузки к загрузке. Если компьютер имеет несколько блочных устройств, это может привести к тому, что при случайном порядке загрузки им будут присваиваться случайные имена. Например, если к компьютеру подключены два жестких диска, `/dev/sda` может случайно становиться `/dev/sdb`. Дополнительную информацию об этом смотрите далее.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 О правилах udev](#.D0.9E_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB.D0.B0.D1.85_udev)
    *   [2.1 Написание своих правил](#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B2.D0.BE.D0.B8.D1.85_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB)
    *   [2.2 Список атрибутов устройства](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.B0.D1.82.D1.80.D0.B8.D0.B1.D1.83.D1.82.D0.BE.D0.B2_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
    *   [2.3 Проверка правил перед загрузкой](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.BE.D0.B9)
    *   [2.4 Загрузка новых правил](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB)
*   [3 Udisks](#Udisks)
*   [4 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 Доступ к программаторам и виртуальным COM-портам](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BA_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.B0.D1.82.D0.BE.D1.80.D0.B0.D0.BC_.D0.B8_.D0.B2.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.BC_COM-.D0.BF.D0.BE.D1.80.D1.82.D0.B0.D0.BC)
    *   [4.2 Выполнение команд при подключении USB-устройств](#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B8_USB-.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [4.3 Выполнение команд при подключении VGA-монитора](#.D0.92.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B8_VGA-.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80.D0.B0)
    *   [4.4 Определение новых накопителей eSATA](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.BE.D0.B2.D1.8B.D1.85_.D0.BD.D0.B0.D0.BA.D0.BE.D0.BF.D0.B8.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_eSATA)
    *   [4.5 Определение внутренних портов SATA как внешних](#.D0.9E.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.BD.D1.83.D1.82.D1.80.D0.B5.D0.BD.D0.BD.D0.B8.D1.85_.D0.BF.D0.BE.D1.80.D1.82.D0.BE.D0.B2_SATA_.D0.BA.D0.B0.D0.BA_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D1.85)
    *   [4.6 Установка постоянных имен устройств](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.BD.D1.8B.D1.85_.D0.B8.D0.BC.D0.B5.D0.BD_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
        *   [4.6.1 Видеоустройства](#.D0.92.D0.B8.D0.B4.D0.B5.D0.BE.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
        *   [4.6.2 Принтеры](#.D0.9F.D1.80.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.8B)
        *   [4.6.3 USB флеш-накопители](#USB_.D1.84.D0.BB.D0.B5.D1.88-.D0.BD.D0.B0.D0.BA.D0.BE.D0.BF.D0.B8.D1.82.D0.B5.D0.BB.D0.B8)
    *   [4.7 Пробуждение при активности USB-устройства](#.D0.9F.D1.80.D0.BE.D0.B1.D1.83.D0.B6.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.B0.D0.BA.D1.82.D0.B8.D0.B2.D0.BD.D0.BE.D1.81.D1.82.D0.B8_USB-.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0)
    *   [4.8 Генерирование событий](#.D0.93.D0.B5.D0.BD.D0.B5.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.BE.D0.B1.D1.8B.D1.82.D0.B8.D0.B9)
*   [5 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Добавление модулей в черный список](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D0.B2_.D1.87.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.81.D0.BF.D0.B8.D1.81.D0.BE.D0.BA)
    *   [5.2 udevd вылетает при загрузке](#udevd_.D0.B2.D1.8B.D0.BB.D0.B5.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5)
    *   [5.3 Неработоспособные устройства BusLogic могут вызывать зависание при загрузке системы](#.D0.9D.D0.B5.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.BE.D1.81.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D0.BD.D1.8B.D0.B5_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.B0_BusLogic_.D0.BC.D0.BE.D0.B3.D1.83.D1.82_.D0.B2.D1.8B.D0.B7.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [5.4 Устройство является съемным, однако не признается таковым](#.D0.A3.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2.D0.BE_.D1.8F.D0.B2.D0.BB.D1.8F.D0.B5.D1.82.D1.81.D1.8F_.D1.81.D1.8A.D0.B5.D0.BC.D0.BD.D1.8B.D0.BC.2C_.D0.BE.D0.B4.D0.BD.D0.B0.D0.BA.D0.BE_.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.B7.D0.BD.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D1.82.D0.B0.D0.BA.D0.BE.D0.B2.D1.8B.D0.BC)
    *   [5.5 Проблемы с автоматической загрузкой модулей аудиоустройств](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.BE.D0.B9_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2)
    *   [5.6 Поддержка дисководов IDE](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2.D0.BE.D0.B4.D0.BE.D0.B2_IDE)
    *   [5.7 Оптические дисководы имеют неверный group ID](#.D0.9E.D0.BF.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D0.B8.D1.81.D0.BA.D0.BE.D0.B2.D0.BE.D0.B4.D1.8B_.D0.B8.D0.BC.D0.B5.D1.8E.D1.82_.D0.BD.D0.B5.D0.B2.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_group_ID)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

В настоящий момент _udev_ включен в состав пакета [systemd](https://www.archlinux.org/packages/?name=systemd) и в системах Arch Linux устанавливается по умолчанию. Смотрите также `man systemd-udevd.service` для получения дополнительной информации.

## О правилах udev

Файлы правил _udev_ хранятся в каталоге `/etc/udev/rules.d/`, их имена должны оканчиваться на _.rules_. Правила, предоставляемые другими пакетами, помещаются в каталог `/usr/lib/udev/rules.d/`. При этом, если правила в этих каталогах имеют одинаковые имена, приоритет отдается файлам из `/etc/udev/rules.d/`.

### Написание своих правил

**Важно:** Чтобы смонтировать съемные устройства, не вызывайте `mount` из правил udev. В случае использования файловых систем FUSE, вы получите ошибку "Transport endpoint not connected". Вместо этого используйте [udisks](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udisks (Русский)"), который выполняет автомонтирование правильно.

*   Чтобы узнать, как создавать собственные правила, смотрите страницу в интернете [Написание правил udev](http://www.reactivated.net/writing_udev_rules.html).
*   Пример правила _udev_ можно найти в разделе [Примеры](http://www.reactivated.net/writing_udev_rules.html#example-printer) на той же странице.

Ниже приведен пример правила, которое создает символическую ссылку `/dev/video-cam1`, когда к компьютеру подключается веб-камера. Например, мы выяснили, что для подключенной камеры создан файл устройства `/dev/video2`. Причина, по которой мы создаем это правило, заключается в том, что при следующей загрузке веб-камере может быть присвоено другое имя, например, `/dev/video0`.

 `# udevadm info -a -p $(udevadm info -q path -n /dev/video2)` 

```
Udevadm info starts with the device specified by the devpath and then walks up the chain of parent devices. It prints for every device found, all possible attributes in the udev rules key format. A rule to match, can be composed by the attributes of the device and the attributes from one single parent device.

  looking at device '/devices/pci0000:00/0000:00:04.1/usb3/3-2/3-2:1.0/video4linux/video2':
    KERNEL=="video2"
    SUBSYSTEM=="video4linux"
    ...
  looking at parent device '/devices/pci0000:00/0000:00:04.1/usb3/3-2/3-2:1.0':
    KERNELS=="3-2:1.0"
    SUBSYSTEMS=="usb"
    ...
  looking at parent device '/devices/pci0000:00/0000:00:04.1/usb3/3-2':
    KERNELS=="3-2"
    SUBSYSTEMS=="usb"
    ...
    ATTRS{idVendor}=="05a9"
    ...
    ATTRS{manufacturer}=="OmniVision Technologies, Inc."
    ATTRS{removable}=="unknown"
    ATTRS{idProduct}=="4519"
    ATTRS{bDeviceClass}=="00"
    ATTRS{product}=="USB Camera"
    ...

```

**Обратите внимание:** Утилита _udevadm_ выводит информацию об устройствах, начиная с указанного устройства (`/dev/video2`), и затем, следуя по цепочке родительских устройств, выводит информацию о них. Кроме всего прочего, выводятся все возможные атрибуты устройств в формате, совместимом с _udev_. Правило для сопоставления может быть создано на основе этих атрибутов самого устройства или атрибутов родительского устройства.

Мы используем параметры веб-камеры `KERNEL=="video2"` и `SUBSYSTEM=="video4linux"`, затем мы возьмем идентификаторы производителя и изделия родительского USB-устройства `SUBSYSTEMS=="usb"`, `ATTRS{idVendor}=="05a9"` и `ATTRS{idProduct}=="4519"` для сопоставления:

 `/etc/udev/rules.d/83-webcam.rules` 

```
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", \
        ATTRS{idVendor}=="05a9", ATTRS{idProduct}=="4519", SYMLINK+="video-cam1"

```

В примере мы создали символическую ссылку, используя параметр `SYMLINK+="video-cam1"`. Мы можем также легко задать владельца (`OWNER="john"`), группу (`GROUP="video"`), или установить права доступа к ссылке (`MODE="0660"`). Однако, если вы намереваетесь создать правило, которое делает что-нибудь при удалении устройства, имейте в виду, что атрибуты устройства могут стать недоступны. В этом случае вам необходимо использовать специальный набор [переменных окружения](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)"). Чтобы отобразить эти переменные, выполните следующую команду при отсоединении устройства:

```
# udevadm monitor --environment --udev

```

В выводе команды вы увидите значения параметров устройства, например, `ID_VENDOR_ID` и `ID_MODEL_ID`, которые соответствуют использованным ранее идентификаторам производителя и изделия. Правило, которое использует переменные окружения устройства, может выглядеть следующим образом:

 `/etc/udev/rules.d/83-webcam-removed.rules` 

```
ACTION=="remove", SUBSYSTEM=="usb", ENV{ID_VENDOR_ID}=="05a9", ENV{ID_MODEL_ID}=="4519", RUN+="''/путь/до/вашего/скрипта''"

```

### Список атрибутов устройства

Чтобы вывести все атрибуты устройства, которые вы можете использовать в написании правил _udev_, выполните:

```
# udevadm info -a -n _имя_устройства_

```

Замените `_имя_устройства_` текущим именем файла устройства, например, `/dev/sda` или `/dev/ttyUSB0`.

Если вы не знаете имя файла устройства, вы можете также вывести все атрибуты по конкретному системному пути:

```
# udevadm info -a -p /sys/class/backlight/acpi_video0

```

### Проверка правил перед загрузкой

Используйте команду:

```
# udevadm test $(udevadm info -q path -n _имя_устройства_) 2>&1

```

Вы можете также указать прямой сисметный путь до устройства:

```
# udevadm test /sys/class/backlight/acpi_video0/

```

### Загрузка новых правил

_udev_ способен определять наличие изменений в файлах правил автоматически, поэтому изменения сразу вступают в силу без необходимости перезапуска _udev_. Однако, новые правила не будут применены сразу к уже подключенным устройствам. Устройства с возможностью горячей замены, например, устройства USB, могут быть просто переподключены для применения к ним новых правил. Также вы можете перезагрузить модули ядра `ohci-hcd` и `ehci-hcd`, что автоматически приведет к перезагрузке всех драйверов для каждого USB-устройства.

Если правила не перезагружаются автоматически, выполните:

```
# udevadm control --reload-rules

```

Чтобы вручную заставить _udev_ применить ваши правила, выполните:

```
# udevadm trigger

```

## Udisks

Смотрите статью [Udisks](/index.php/Udisks_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udisks (Русский)").

## Советы и рекомендации

### Доступ к программаторам и виртуальным COM-портам

Следующий набор правил даст возможность обычным пользователям (членам группы `users`) получить доступ к USB-программаторам для микроконтроллеров AVR [USBtinyISP (англ.)](http://www.ladyada.net/make/usbtinyisp/), виртуальным COM-портам (преобразователям интерфейса USB <-> UART) на основе популярной микросхемы [CP2102 (англ.)](http://www.silabs.com/products/interface/usbtouart), программаторам [Atmel AVR Dragon (англ.)](http://www.atmel.com/tools/AVRDRAGON.aspx?tab=overview) и [Atmel AVR ISP mkII (англ.)](http://www.atmel.com/tools/AVRISPMKII.aspx).

 `/etc/udev/rules.d/50-embedded_devices.rules` 

```
# USBtinyISP Programmer rules
SUBSYSTEMS=="usb", ATTRS{idVendor}=="1781", ATTRS{idProduct}=="0c9f", GROUP="users", MODE="0666"
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="0479", GROUP="users", MODE="0666"
# USBasp Programmer rules http://www.fischl.de/usbasp/
SUBSYSTEMS=="usb", ATTRS{idVendor}=="16c0", ATTRS{idProduct}=="05dc", GROUP="users", MODE="0666"

# Mdfly.com Generic (SiLabs CP2102) 3.3v/5v USB VComm adapter
SUBSYSTEMS=="usb", ATTRS{idVendor}=="10c4", ATTRS{idProduct}=="ea60", GROUP="users", MODE="0666"

#Atmel AVR Dragon (dragon_isp) rules
SUBSYSTEM=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2107", GROUP="users", MODE="0666"

#Atmel AVR JTAGICEMKII rules
SUBSYSTEM=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2103", GROUP="users", MODE="0666"

#Atmel Corp. AVR ISP mkII
SUBSYSTEM=="usb", ATTRS{idVendor}=="03eb", ATTRS{idProduct}=="2104", GROUP="users", MODE="0666"

```

Набор правил актуален на 31 октября 2012 года. Идентификаторы производителя и изделия для новых ревизий устройств могут быть другими.

### Выполнение команд при подключении USB-устройств

Смотрите статью [Выполнение команд при подключении USB-устройств](/index.php/Execute_on_USB_insert "Execute on USB insert") или [скрипт devmon wrapper](http://igurublog.wordpress.com/downloads/script-devmon/).

### Выполнение команд при подключении VGA-монитора

Создайте правило `/etc/udev/rules.d/95-monitor-hotplug.rules` со следующим содержимым, чтобы запустить [arandr](https://www.archlinux.org/packages/?name=arandr) при подключении VGA-монитора:

```
KERNEL=="card0", SUBSYSTEM=="drm", ENV{DISPLAY}=":0", ENV{XAUTHORITY}="/home/_username_/.Xauthority", RUN+="/usr/bin/arandr"

```

### Определение новых накопителей eSATA

Если ваш накопитель eSATA не был определен системой при подключении, вы можете перезагрузить систему, не отключая кабель устройства, либо, если перезагрузка нежелательна, выполнить:

```
# echo 0 0 0 | tee /sys/class/scsi_host/host*/scan

```

Еще один вариант заключается в использовании утилиты [scsiadd](https://aur.archlinux.org/packages/scsiadd/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"):

```
# scsiadd -s

```

Накопитель должен появиться в `/dev`. Если это не так, попробуйте выполнить:

```
# udevadm monitor

```

до и после вышеприведенных команд и посмотреть, происходит ли что-нибудь.

### Определение внутренних портов SATA как внешних

Если вы подключили eSATA-адаптер, система все еще будет распоздавать его как внутренний SATA-накопитель. [GNOME](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GNOME (Русский)") и [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") будут постоянно запрашивать пароль администратора. Следующее правило помечает все указанные SATA-порты как порты eSATA, благодаря чему обычные пользователи смогут подключать свой накопитель eSATA к этому порту как USB-накопитель без запроса пароля администратора:

 `/etc/udev/rules.d/10-esata.rules` 

```
DEVPATH=="/devices/pci0000:00/0000:00:1f.2/host4/*", ENV{UDISKS_SYSTEM}="0"

```

**Обратите внимание:** Узнать правильное значение параметра `DEVPATH` вы можете, используя следующие команды (вместо `/dev/sdb` укажите имя вашего устройства):

```
# udevadm info -q path -n /dev/sdb
/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

```
# find /sys/devices/ -name sdb
/sys/devices/pci0000:00/0000:00:1f.2/host4/target4:0:0/4:0:0:0/block/sdb

```

### Установка постоянных имен устройств

Из-за асинхронного способа загрузки модулей, они инициализируются в разном порядке от загрузки к загрузке. Это приводит к случайному переименованию устройств при каждом запуске. Чтобы задать постоянные имена вашим устройствам, можно создать специальное правило _udev_.

Смотрите также статьи [Постоянные имена для блочных устройств](/index.php/Persistent_block_device_naming "Persistent block device naming") для получения информации по блочным устройствам и [Настройка сети#Имена устройств](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#.D0.98.D0.BC.D0.B5.D0.BD.D0.B0_.D1.83.D1.81.D1.82.D1.80.D0.BE.D0.B9.D1.81.D1.82.D0.B2 "Настройка сети") — для сетевых устройств.

#### Видеоустройства

Процедура установки веб-камеры описана в статье [Настройка веб-камеры](/index.php/Webcam_Setup#Webcam_configuration "Webcam Setup").

Использование нескольких веб-камер может быть полезно, например, совместно с [motion](https://www.archlinux.org/packages/?name=motion) (программный детектор движения, который получает изображения с устройств _video4linux_ и/или веб-камер). При загрузке веб-камер им случайно присваиваются имена вида `/dev/video[0..n]`. Рекомендуемое решение состоит в создании символических ссылок с использованием правила _udev_ (как в примере [#Написание своих правил](#.D0.9D.D0.B0.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.B2.D0.BE.D0.B8.D1.85_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB)):

 `/etc/udev/rules.d/83-webcam.rules` 

```
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="05a9", ATTRS{idProduct}=="4519", SYMLINK+="video-cam1"
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="08f6", SYMLINK+="video-cam2"
KERNEL=="video[0-9]*", SUBSYSTEM=="video4linux", SUBSYSTEMS=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="0840", SYMLINK+="video-cam3"

```

**Обратите внимание:** Использование имен, отличных от `/dev/video*`, может помешать загрузке `v4l1compat.so`, и, возможно, `v4l2convert.so`

#### Принтеры

Если у вас несколько принтеров, им будут случайным образом присвоены имена вида `/dev/lp[0-9]`, что, например, может помешать серверу [CUPS](/index.php/CUPS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "CUPS (Русский)") правильно настроить устройства. Вы можете создать следующее правило, которое будет создавать постоянные символические ссылки в каталогах `/dev/lp/by-id` и `/dev/lp/by-path` подобно схеме, приведенной в статье [Постоянные имена для блочных устройств](/index.php/Persistent_block_device_naming "Persistent block device naming"):

 `/etc/udev/rules.d/60-persistent-printer.rules` 

```
ACTION=="remove", GOTO="persistent_printer_end"

# This should not be necessary
#KERNEL!="lp*", GOTO="persistent_printer_end"

SUBSYSTEMS=="usb", IMPORT{builtin}="usb_id"
ENV{ID_TYPE}!="printer", GOTO="persistent_printer_end"

ENV{ID_SERIAL}=="?*", SYMLINK+="lp/by-id/$env{ID_BUS}-$env{ID_SERIAL}"

IMPORT{builtin}="path_id"
ENV{ID_PATH}=="?*", SYMLINK+="lp/by-path/$env{ID_PATH}"

LABEL="persistent_printer_end"

```

#### USB флеш-накопители

USB флеш-накопители обычно содержат разделы, и метки разделов позволяют получить статичные имена устройств. Также этого можно достичь, создав правило udev.

Первым делом узнайте серийный номер и идентификаторы USB вашего устройства (если у вас несколько одинаковых устройств, убедитесь, что серийные номера на самом деле уникальны):

```
lsusb -v | grep -A 5 Vendor

```

Создайте правило udev для устройства, добавив следующее в файл в `/etc/udev/rules.d/`, например, `8-usbstick.rules`:

```
KERNEL=="sd*", ATTRS{serial}=="_серийный_номер_", ATTRS{idVendor}=="_id_поставщика_", ATTRS{idProduct}=="_id_устройства_" SYMLINK+="_имя_%n"

```

Замените, соответственно, `_серийный_номер_`, `_id_поставщика_`, `_id_устройства_` на реальные значения, а `_имя_` — на желаемое имя устройства, например, `/dev/sdd`. Специальная метка `%n` обозначает номер раздела, не удаляйте ее. Например, если у накопителя два раздела, будут созданы две символические ссылки.

Пересканируйте sysfs:

```
udevadm trigger

```

Проверьте содержимое `/dev`:

```
ls /dev

```

Вы должны увидеть одну или несколько созданных символических ссылок для вашего устройства.

### Пробуждение при активности USB-устройства

Первым делом, определите идентификаторы производителя и изделия вашего устройства:

 `# lsusb | grep Logitech`  `Bus 007 Device 002: ID 046d:c52b Logitech, Inc. Unifying Receiver` 

Теперь измените атрибут `power/wakeup` устройства и USB-контроллера, к которому оно подключено. В данном примере это `driver/usb7/power/wakeup`. Используйте следующее правило:

 `/etc/udev/rules.d/50-wake-on-device.rules` 

```
ACTION=="add", SUBSYSTEM=="usb", ATTRS{idVendor}=="046d", ATTRS{idProduct}=="c52b", ATTR{power/wakeup}="enabled", ATTR{driver/usb7/power/wakeup}="enabled"

```

**Обратите внимание:** Убедитесь также, что контроллер USB активирован в `/proc/acpi/wakeup`.

### Генерирование событий

Может быть полезно сгенерировать различные события udev. Например, вы хотите симулировать отключение USB-устройства на удаленной машине. В таких случаях, используйте `udevadm trigger`:

```
# udevadm trigger -v -t subsystems -c remove -s usb -a "idVendor=_id_поставщика_"

```

Эта команда симулирует отключение всех USB-устройств с указанным идентификатором поставщика `_id_поставщика_`.

## Решение проблем

### Добавление модулей в черный список

Иногда _udev_ может ошибочно загружать неправильные модули ядра. Чтобы избежать этого, вы можете добавить такие модули в черный список. Если модуль добавлен в этот список, _udev_ станет игнорировать его при загрузке (в том числе, если устройство подключено уже после загрузки системы).

Смотрите раздел [Добавление в черный список](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Blacklisting "Kernel modules (Русский)").

### udevd вылетает при загрузке

После миграции на LDAP или обновления системы, использующей LDAP, _udevd_ может начать аварийно завершаться в момент загрузки системы с сообщением "Starting UDev Daemon". Обычно это происходит потому, что _udevd_ пытается определить имя через LDAP, но не может, так как в этот момент еще не установлено подключение к сети.

Необходимо, чтобы все используемые в LDAP группы были продублированы локально. Получить имена групп, используемых в правилах _udev_, и имена групп, присутствующих в системе, можно командами:

```
# fgrep -r GROUP /etc/udev/rules.d/ /usr/lib/udev/rules.d | perl -nle '/GROUP\s*=\s*"(.*?)"/ && print $1;' | sort | uniq > udev_groups
# cut -f1 -d: /etc/gshadow /etc/group | sort | uniq > present_groups

```

Вывод будет записан в файлы `present_groups` и `udev_groups`. Чтобы увидеть различия, выполните построчное сравнение командой _diff_:

```
# diff -y present_groups udev_groups
...
network                                  <
nobody                               <
ntp                                  <
optical                                optical
power                                | pcscd
rfkill                               <
root                               root
scanner                                scanner
smmsp                                <
storage                                storage
...

```

В данном примере группа `pcscd` по какой-то причине отсутствует в системе. Все такие группы необходимо [добавить в систему](/index.php/Users_and_Groups_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B0.D0.BC.D0.B8 "Users and Groups (Русский)"). Также убедитесь, что имена всех локальных ресурсов разрешены, прежде чем возвращаться к LDAP. Файл `/etc/nsswitch.conf` должен содержать следующую строку:

```
group: files ldap

```

### Неработоспособные устройства BusLogic могут вызывать зависание при загрузке системы

Это баг в ядре Linux, на данный момент не исправленный.

### Устройство является съемным, однако не признается таковым

Создайте правило udev для конкретного устройства. Чтобы получить подробную информацию об устройстве вы можете либо использовать `ID_SERIAL`, либо `ID_SERIAL_SHORT` (не забудьте поменять `/dev/sdb` если нужно):

```
$ udevadm info _/dev/sdb_ | grep ID_SERIAL

```

Теперь создайте файл правила в `/etc/udev/rules.d/` и установите переменные либо для udisks, либо для udisks2.

Для udisks установите `UDISKS_SYSTEM_INTERNAL="0"`, которая пометит все устройства как съемные, и, таким образом, подходящие для автоматического монтирования. Смотрите подробности на странице [udisks(7)](http://udisks.freedesktop.org/docs/1.0.5/udisks.7.html).

 `/etc/udev/rules.d/50-external-myhomedisk.rules`  `ENV{ID_SERIAL_SHORT}=="_serial_number_", ENV{UDISKS_SYSTEM_INTERNAL}="0"` 

Для udisks2 установите `UDISKS_AUTO="1"`, чтобы пометить устройство для автоматического монтирования и `UDISKS_SYSTEM="0"`, чтобы пометить устройство как съемное. Смотрите подробности на странице [udisks(8)](http://udisks.freedesktop.org/docs/1.93.0/udisks.8.html).

 `/etc/udev/rules.d/99-removable.rules`  `ENV{ID_SERIAL_SHORT}=="_serial_number_", ENV{UDISKS_AUTO}="1", ENV{UDISKS_SYSTEM}="0"` 

Перезагрузите правила udev командой `udevadm control --reload`. Теперь ваше устройство будет распознаваться как съемное.

### Проблемы с автоматической загрузкой модулей аудиоустройств

Некоторые пользователи испытывают проблемы с загрузкой модулей звуковых устройств, для которых остались старые записи в `/etc/modprobe.d/sound.conf`. Чистка файла от таких записей может помочь.

**Обратите внимание:** Начиная с версии _udev_ 171, модули эмуляции OSS (`snd_seq_oss`, `snd_pcm_oss` и `snd_mixer_oss`) больше не загружаются автоматически.

### Поддержка дисководов IDE

Начиная с версии 170, _udev_ не поддерживает устройства CD-ROM/DVD-ROM, загружаемые как обычные IDE дисководы модулем `ide_cd_mod` и отображаемые в системе как `/dev/hd*`. Дисковод доступен только программам, которые обращаются к устройству напрямую, таким как _cdparanoia_, но невидим для более высокоуровневых программ, таких как KDE.

Причина, по которой загрузка модуля `ide_cd_mod` имеет приоритет перед другими модулями, например, `sr_mod`, может заключаться в том, что по какой-либо причине модуль `piix` загружается в вашем [initramfs](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mkinitcpio (Русский)"). В этом случае вы можете просто заменить его в файле `/etc/mkinitcpio.conf` на `ata_piix`.

### Оптические дисководы имеют неверный group ID

Если значение group ID вашего дисковода установлено как `disk`, но вы хотите, чтобы оно было `optical`, вам следует создать такое правило:

 `/etc/udev/rules.d` 

```
# permissions for IDE CD devices
SUBSYSTEMS=="ide", KERNEL=="hd[a-z]", ATTR{removable}=="1", ATTRS{media}=="cdrom*", GROUP="optical"

# permissions for SCSI CD devices
SUBSYSTEMS=="scsi", KERNEL=="s[rg][0-9]*", ATTRS{type}=="5", GROUP="optical"
```

## Смотрите также

*   [udev home page](https://www.kernel.org/pub/linux/utils/kernel/hotplug/udev/udev.html) — домашняя страница udev
*   [An Introduction to udev](https://www.linux.com/news/hardware/peripherals/180950-udev) — вводный материал по использованию udev
*   [udev mailing list information](http://vger.kernel.org/vger-lists.html#linux-hotplug) — информация по списку рассылки
*   [Scripting with udev](http://jasonwryan.com/blog/2014/01/20/udev/) — написание скриптов с udev
*   [Writing udev rules](http://www.reactivated.net/writing_udev_rules.html) — написание правил udev