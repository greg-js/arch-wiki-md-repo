**Состояние перевода:** На этой странице представлен перевод статьи [Bluetooth mouse](/index.php/Bluetooth_mouse "Bluetooth mouse"). Дата последней синхронизации: 2015-09-30\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Bluetooth_mouse&diff=0&oldid=394963).

Ссылки по теме

*   [Bluetooth (Русский)](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)")
*   [Bluez4](/index.php/Bluez4 "Bluez4")
*   [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate")

В этой статье описывается, как настроить [bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)")-мышь из командной строки, не прибегая к графическим приложениям.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Инструкции для Bluez5](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BA.D1.86.D0.B8.D0.B8_.D0.B4.D0.BB.D1.8F_Bluez5)
*   [3 Инструкции для Bluez4](#.D0.98.D0.BD.D1.81.D1.82.D1.80.D1.83.D0.BA.D1.86.D0.B8.D0.B8_.D0.B4.D0.BB.D1.8F_Bluez4)
    *   [3.1 Модули ядра](#.D0.9C.D0.BE.D0.B4.D1.83.D0.BB.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [3.2 Проверка](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0)
    *   [3.3 Настройка bluetooth-мыши](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_bluetooth-.D0.BC.D1.8B.D1.88.D0.B8)
    *   [3.4 Поиск мыши](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [3.5 Соединение с мышью](#.D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BC.D1.8B.D1.88.D1.8C.D1.8E)
*   [4 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 Тормоза мыши](#.D0.A2.D0.BE.D1.80.D0.BC.D0.BE.D0.B7.D0.B0_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [4.2 Проблемы с bluetooth-адаптером USB](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_bluetooth-.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80.D0.BE.D0.BC_USB)

## Установка

Установите пакет [bluez](https://www.archlinux.org/packages/?name=bluez), содержащий текущий bluetooth-стек (Bluez5) для Linux. Также может понадобиться установить пакет [bluez-utils](https://www.archlinux.org/packages/?name=bluez-utils), который предоставляет утилиту *bluetoothctl*. Для получения дополнительной информации смотрите статью [Bluetooth](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)").

Если вам необходимо работать со старым bluetooth-стеком (Bluez4), установите пакет [bluez4](https://aur.archlinux.org/packages/bluez4/). Для получения более подробной информации прочтите статью [Bluez4](/index.php/Bluez4 "Bluez4").

**Важно:** Bluez4 устарел! Вместо него настоятельно рекомендуется использовать Bluez5

## Инструкции для Bluez5

**Совет:** Убедитесь, что bluetooth-демон запущен, прежде чем продолжить.

Bluez5 предоставляет утилиту *bluetoothctl*, которая имеет простой интерфейс для настройки bluetooth-подключений.

Вот пример подключения bluetooth-мыши с помощью *bluetoothctl*:

```
# bluetoothctl
[bluetooth]# list
Controller <MAC-адрес контроллера> BlueZ 5.5 [default]
[bluetooth]# select <MAC-адрес контроллера>
[bluetooth]# power on
[bluetooth]# scan on
[bluetooth]# agent on
[bluetooth]# devices
Device <MAC-адрес мыши> Name: Bluetooth Mouse
[bluetooth]# pair <MAC-адрес мыши>
[bluetooth]# trust <MAC-адрес мыши>
[bluetooth]# connect <MAC-адрес мыши>

```

Для того, чтобы подключать девайс при загрузке, вам может понадобиться создать правило [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)"). Смотрите [Bluetooth (Русский)#Bluetoothctl](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Bluetoothctl "Bluetooth (Русский)") для дополнительной информации.

**Совет:** В случае, если вы использовали USB Bluetooth донгл и переместили его в другой USB порт, вам может понадобиться удалить MAC адрес мыши в *bluetoothctl* командой *remove <mouse mac>* и повторить всю процедуру заново.

## Инструкции для Bluez4

### Модули ядра

Если служба bluetooth запущена через systemd, то дополнительные действия не требуются. Если же модуль не загружен, попробуйте выполнить следующую команду:

```
# modprobe -v btusb bluetooth hidp l2cap

```

Это загрузит необходимые модули ядра, если они не загрузились автоматически.

### Проверка

Следующая команда отобразит ваш bluetooth-адаптер:

 `# hciconfig` 
```
hci0:  Type: BR/EDR  Bus: USB
       BD Address: 00:22:43:E1:82:E0  ACL MTU: 1021:8  SCO MTU: 64:1
       UP RUNNING PSCAN 
       RX bytes:1062273 acl:62061 sco:0 events:778 errors:0
       TX bytes:1825 acl:11 sco:0 commands:39 errors:0

```

### Настройка bluetooth-мыши

Описанный здесь метод настройки состоит из трех этапов, в следующем порядке:

1.  Рассказать компьютеру о bluetooth мыши.
2.  Дать мыши права для соединения.
3.  Рассказать мыши о компьютере.

### Поиск мыши

Сперва вы должны сделать мышь видимой. Для этого некоторые модели требуют нажатия на кнопку. Затем выполните следующую команду:

 `# hcitool scan` 
```
Scanning ...
        00:07:61:F5:5C:3D       Logitech Bluetooth Mouse M555b

```

MAC-адрес вашей мыши выглядит примерно как `12:34:56:78:9A:BC`. Иногда его можно узнать из документации к мыши, либо он может быть указан на самой мыши.

### Соединение с мышью

Чтобы выполнить поиск устройств (вам может понадобиться использовать `su -c` или `sudo`):

```
hidd --search
hcitool inq

```

Чтобы подключить устройство:

```
hidd --connect <bdaddr>

```

Чтобы показать устройства, подключенные в данный момент:

```
hidd --show

```

Мышь должна появиться в этом списке. Если это не так, нажмите кнопку сброса на мыши, чтобы сделать её видимой.

**Примечание:** Если у вас загружен модуль ipw3945 (это wifi на компьютерах HP), bluetooth работать не будет.

## Решение проблем

### Тормоза мыши

Если вы наблюдаете тормоза мыши, вы можете попробовать увеличить частоту опроса. Смотрите [Mouse polling rate](/index.php/Mouse_polling_rate "Mouse polling rate") для дополнительной информации.

### Проблемы с bluetooth-адаптером USB

Если у вас проблемы с адаптером USB, можете попробовать выполнить:

```
# modprobe -v rfcomm

```

Сейчас вы должны получить устройство `hci0` с помощью команды:

```
# hcitool dev

```

Иногда устройство не активируется автоматически. Попробуйте поднять интерфейс с помощью:

```
# hciconfig hci0 up

```

и выполнить поиск устройств, как описано выше.