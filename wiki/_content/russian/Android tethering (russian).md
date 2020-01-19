[Тетеринг](https://en.wikipedia.org/wiki/ru:%D0%A2%D0%B5%D1%82%D0%B5%D1%80%D0%B8%D0%BD%D0%B3 "wikipedia:ru:Тетеринг") - это раздача интернета на компьютер со смартфона с помощью его сетевого подключения. USB-модем и точка доступа Wi-Fi точки доступа поддерживаются изначально с Android Froyo (2.2). В более старых версиях ОС Android большинство неофициальных ПЗУ имеют эту функцию.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Точка доступа Wi-Fi](#Точка_доступа_Wi-Fi)
*   [2 USB модем](#USB_модем)
    *   [2.1 Что вам понадобится](#Что_вам_понадобится)
    *   [2.2 Порядок действий](#Порядок_действий)
*   [3 USB-модем с OpenVPN](#USB-модем_с_OpenVPN)
    *   [3.1 Необходимые инструменты](#Необходимые_инструменты)
        *   [3.1.1 Настройка телефонного соединения в Arch Linux](#Настройка_телефонного_соединения_в_Arch_Linux)
    *   [3.2 Процедура](#Процедура)
    *   [3.3 Исправление проблем](#Исправление_проблем)
        *   [3.3.1 DNS](#DNS)
        *   [3.3.2 NetworkManager](#NetworkManager)
*   [4 Модем через Bluetooth](#Модем_через_Bluetooth)
*   [5 Подключение через прокси-сервер SOCKS](#Подключение_через_прокси-сервер_SOCKS)
    *   [5.1 Необходимые инструменты](#Необходимые_инструменты_2)
    *   [5.2 инструкции](#инструкции)
        *   [5.2.1 Tetherbot](#Tetherbot)
        *   [5.2.2 Proxoid](#Proxoid)

## Точка доступа Wi-Fi

Использование телефона Android в качестве точки доступа Wi-Fi (с использованием 3G) стало доступным по умолчанию с момента выхода Froyo (Android 2.2) без необходимости иметь root права на телефоне. Более того, этот метод быстро разряжает батарею, и в отличие от USB, приводит к интенсивному нагреву. Смотри : **menu/wireless & networks/Internet tethering/Wi-Fi access point**

## USB модем

### Что вам понадобится

*   Root доступ на телефоне (для старых версий Android, Froyo (Android 2.2) и ещё более ранних это можно сделать из коробки.)
*   USB кабель для подключения смартфона к компьютеру

### Порядок действий

*   Отключите ваш компьютер от всех беспроводных и проводных сетей
*   Подключите телефон к компьютеру с помощью USB кабеля (режим подключения USB -- Медиа устройство, Монтирование SD карты или Только зарядка -- это не важно, но обратите внимание, что вы не сможете поменять режим подключения USB во время тетеринга)
*   Включите режим USB-модем на телефоне. Обычно эта настройка находится так `Настройка --> Беспроводные сети --> Ещё --> Режим модема` (или `Tethering & portable hotspot`, на некоторых версиях)
*   Убедитесь, что USB интерфейс распознан системой с помощью следующей команды:

	 `$ ip link` 

	Вы должны увидеть `usb0` или `enp?s??u?` устройство в вашем списка (например, здесь это устройство enp0s20u3).

 `# ip link` 
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: enp4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP mode DEFAULT group default qlen 1000
    link/ether ##:##:##:##:##:## brd ff:ff:ff:ff:ff:ff
3: wlp2s0: <BROADCAST,MULTICAST> mtu 1500 qdisc mq state DOWN mode DEFAULT group default qlen 1000
    link/ether ##:##:##:##:##:## brd ff:ff:ff:ff:ff:ff
5: enp0s20u3: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN mode DEFAULT group default qlen 1000
    link/ether ##:##:##:##:##:## brd ff:ff:ff:ff:ff:ff

```

**Примечание:** Вы должны использовать своё имя устройство при выполнении этих команд.

**Важно:** Название устройства может меняться при подключении к другому usb порту. Вы можете [изменить название устройства](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Change_device_name "Network configuration (Русский)"), чтобы создать уникальное имя для вашего устройства к какому бы usb порту вы ни подключились.

*   Последним шагом является [настройка сетевого соединения](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Configure_the_IP_address "Network configuration (Русский)") на данном интерфейсе.

## USB-модем с OpenVPN

Этот метод работает для любой старой версии Android и не требует ни прав root, ни модификаций в телефоне (он также подходит для Android 2.2 и новее, но больше не требуется).

Он не требует изменений в вашем браузере. На самом деле, весь сетевой трафик прозрачно обрабатывается для любого приложения ПК (кроме пингов ICMP). Он несколько интенсивно потребляет процессор при высоких нагрузках (скорость передачи данных 500 кбайт/с может занимать более 50% телефонного процессора на мощном Acer Liquid).

### Необходимые инструменты

Для Arch вам нужно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_пакетов "Pacman (Русский)") пакет [openvpn](https://www.archlinux.org/packages/?name=openvpn). Также необходимо установить Android SDK (который можно получить [здесь](http://developer.android.com/sdk/index.html) или из AUR). На телефоне вам нужно приложение [azilink](http://code.google.com/p/azilink/), которое представляет собой NAT на базе Java, который будет взаимодействовать с OpenVPN на вашем компьютере.

#### Настройка телефонного соединения в Arch Linux

После того, как вы установили Android SDK, чтобы использовать предоставленные инструменты, ваш телефон должен быть правильно настроен в [udev](/index.php/Udev "Udev"), и вы должны предоставить пользователю Linux права. В противном случае вам могут потребоваться привилегии root для использования Android SDK, что не рекомендуется. Чтобы выполнить эту настройку, включите отладку USB на телефоне (обычно в меню «Настройки» -> «Приложения -> Разработка -> USB-отладка»), подключите его к ПК с помощью USB-кабеля и выполните команду {ic|lsusb}}. Устройство должно быть в списке. Пример вывода для телефона Acer Liquid:

```
Bus 001 Device 006: ID **0502**:3202 Acer, Inc. 

```

Затем создайте следующий файл, заменив *ciri* на ваше собственное имя пользователя Linux, и *0502* на идентификатор поставщика вашего телефона:

 `/etc/udev/rules.d/51-android.rules` 
```
SUBSYSTEM=="usb", ATTR(idVendor)=="0502", MODE="0666" OWNER="ciri"

```

Как root выполните команду `udevadm control restart` (или перезагрузите компьютер), чтобы применить изменения.

Теперь выполните на вашем Linux-ПК команду `adb shell` из Android SDK в качестве обычного (не root) пользователя: вы должны получить приглашение unix «на телефоне».

### Процедура

Запустите приложение AziLink в телефоне и выберите «О программе» внизу, чтобы получить инструкции, которые в основном:

1.  Вам нужно будет включить отладку USB на телефоне, если она еще не была включена (обычно в меню «Настройки» -> «Приложения» -> «Разработка» -> «Отладка USB»).
2.  Подключите телефон с помощью кабеля USB к ПК.
3.  Запустите AziLink и убедитесь, что в верхней части окна отмечена опция **Активная служба**.
4.  Выполните на своем ПК Linux следующие команды:

	 `$ adb forward tcp:41927 tcp:41927` 

	 `# openvpn AziLink.ovpn` 

 `AziLink.ovpn` 
```
dev tun
remote 127.0.0.1 41927 tcp-client
ifconfig 192.168.56.2 192.168.56.1
route 0.0.0.0 128.0.0.0
route 128.0.0.0 128.0.0.0
socket-flags TCP_NODELAY
keepalive 10 30
dhcp-option DNS 192.168.56.1

```

### Исправление проблем

#### DNS

Вам может потребоваться вручную обновить содержимое [resolv.conf](/index.php/Resolv.conf "Resolv.conf") до

 `/etc/resolv.conf` 
```
nameserver 192.168.56.1

```

#### NetworkManager

Если вы используете NetworkManager, вам может потребоваться остановить его перед запуском OpenVPN.

## Модем через Bluetooth

Android (по крайней мере, начиная с 4.0, возможно, ранее) может предоставить персональную сеть Bluetooth (PAN) в режиме точки доступа.

NetworkManager может выполнить это действие и самостоятельно обработать инициализацию сети; Обратитесь к его документации для получения более подробной информации.

В качестве альтернативы: убедитесь, что вы можете подключить свой компьютер и устройство Android, как описано в [Bluetooth (Русский)](/index.php/Bluetooth_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bluetooth (Русский)"), затем, заменяя адрес устройства (здесь задан как `AA_BB_CC_DD_EE_FF`), выполните:

 `$ dbus-send --system --type=method_call --dest=org.bluez /org/bluez/hci0/dev_AA_BB_CC_DD_EE_FF org.bluez.Network1.Connect string:'nap'` 

Это создаст сетевой интерфейс `bnep0`. В заключение, [настройте сетевое соединение](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Настройка_IP-адреса "Network configuration (Русский)") на этом интерфейсе; Android по умолчанию предлагает DHCP.

## Подключение через прокси-сервер SOCKS

С этим методом привязка достигается путем переадресации порта с телефона на ПК. Это подходит только для просмотра. Для Firefox вам следует установить параметру **network.proxy.socks_remote_dns** значение **true** в **about:config** ( адресная строка )

### Необходимые инструменты

*   [android-sdk](https://aur.archlinux.org/packages/android-sdk/) и [android-sdk-platform-tools](https://aur.archlinux.org/packages/android-sdk-platform-tools/) из [AUR](/index.php/AUR "AUR") и [android-udev](https://www.archlinux.org/packages/?name=android-udev) из [official repositories (Русский)](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)")
*   Кабель USB для подключения вашего телефона к ПК
*   Один из двух: [Tetherbot](http://graha.ms/androidproxy/) или [Proxoid](https://code.google.com/p/proxoid/)

### инструкции

#### Tetherbot

Следуйте инструкциям в разделе **Using the Socks Proxy** на странице [[1]](http://graha.ms/androidproxy/).

#### Proxoid

Следуйте инструкциям, приведенным в следующих разделах [link](http://androidcommunity.com/forums/f23/android-usb-tethering-for-linux-using-proxoid-24875/)