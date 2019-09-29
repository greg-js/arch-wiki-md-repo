Ссылки по теме

*   [Software access point](/index.php/Software_access_point "Software access point")
*   [Ad-hoc networking](/index.php/Ad-hoc_networking "Ad-hoc networking")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")
*   [Wireless bonding](/index.php/Wireless_bonding "Wireless bonding")
*   [Network Debugging](/index.php/Network_Debugging "Network Debugging")
*   [Bluetooth](/index.php/Bluetooth "Bluetooth")

Основную статью по настройке сети можно найти на странице [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети").

Настройка беспроводного соединения происходит в два этапа. На первом этапе необходимо определить и установить правильный драйвер сетевого интерфейса (обычно драйвер находится на установочном носителе, но иногда его приходится устанавливать вручную), после чего произвести настройку. Второй этап заключается в выборе способа управления беспроводными соединениями. В этой статье описаны оба этапа, а также представлены ссылки на утилиты управления беспроводными соединениями.

В разделе [#iw](#iw) описана ручная настройка беспроводного интерфейса / локальной сети посредством утилиты [iw](https://www.archlinux.org/packages/?name=iw). В статье [Настройка сети#Сетевые менеджеры](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#Сетевые_менеджеры "Настройка сети") вы найдёте список программ (в том числе и с графическим интерфейсом), которые используются для автоматического управления сетевым интерфейсом. В них реализована поддержка сетевых профилей, что бывает удобно при частой смене беспроводных сетей (как это бывает, например, с ноутбуками).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Драйвер устройства](#Драйвер_устройства)
    *   [1.1 Проверка состояния драйвера](#Проверка_состояния_драйвера)
    *   [1.2 Установка драйвера/прошивки](#Установка_драйвера/прошивки)
*   [2 Утилиты](#Утилиты)
    *   [2.1 Сравнение iw и wireless_tools](#Сравнение_iw_и_wireless_tools)
*   [3 iw](#iw)
    *   [3.1 Определение имени интерфейса](#Определение_имени_интерфейса)
    *   [3.2 Определение состояния интерфейса](#Определение_состояния_интерфейса)
    *   [3.3 Включение интерфейса](#Включение_интерфейса)
    *   [3.4 Обнаружение точек доступа](#Обнаружение_точек_доступа)
    *   [3.5 Выбор режима работы](#Выбор_режима_работы)
    *   [3.6 Соединение с точкой доступа](#Соединение_с_точкой_доступа)
*   [4 Wi-Fi Protected Access](#Wi-Fi_Protected_Access)
    *   [4.1 WPA2 Personal](#WPA2_Personal)
    *   [4.2 WPA2 Enterprise](#WPA2_Enterprise)
        *   [4.2.1 eduroam](#eduroam)
        *   [4.2.2 Ручная/автоматическая настройка](#Ручная/автоматическая_настройка)
            *   [4.2.2.1 wpa_supplicant](#wpa_supplicant)
            *   [4.2.2.2 NetworkManager](#NetworkManager)
            *   [4.2.2.3 connman](#connman)
            *   [4.2.2.4 netctl](#netctl)
        *   [4.2.3 Проблемы](#Проблемы)
            *   [4.2.3.1 MS-CHAPv2](#MS-CHAPv2)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Предостережения Rfkill](#Предостережения_Rfkill)
    *   [5.2 Уважение управляющего домена](#Уважение_управляющего_домена)
    *   [5.3 Просмотр логов](#Просмотр_логов)
    *   [5.4 Энергосбережение](#Энергосбережение)
    *   [5.5 Не удалось получить IP адрес](#Не_удалось_получить_IP_адрес)
    *   [5.6 Connection always times out](#Connection_always_times_out)
        *   [5.6.1 Lowering the rate](#Lowering_the_rate)
        *   [5.6.2 Понижение txpower](#Понижение_txpower)
        *   [5.6.3 Setting rts and fragmentation thresholds](#Setting_rts_and_fragmentation_thresholds)
    *   [5.7 Внезапные отключения](#Внезапные_отключения)
        *   [5.7.1 Причина #1](#Причина_#1)
        *   [5.7.2 Причина #2](#Причина_#2)
        *   [5.7.3 Причина #3](#Причина_#3)
*   [6 Решение проблем с драйверами и прошивками](#Решение_проблем_с_драйверами_и_прошивками)
    *   [6.1 wlan-ng](#wlan-ng)
    *   [6.2 rt2x00](#rt2x00)
    *   [6.3 RT2500](#RT2500)
    *   [6.4 RT61](#RT61)
    *   [6.5 RT73](#RT73)
    *   [6.6 madwifi](#madwifi)
    *   [6.7 ath5k](#ath5k)
    *   [6.8 ath9k](#ath9k)
    *   [6.9 rtl8723bu](#rtl8723bu)
    *   [6.10 ipw2100 and ipw2200](#ipw2100_and_ipw2200)
    *   [6.11 ipw3945 and ipw4965](#ipw3945_and_ipw4965)
    *   [6.12 ipw3945 (Альтернативный метод)](#ipw3945_(Альтернативный_метод))
    *   [6.13 orinoco](#orinoco)
    *   [6.14 ndiswrapper](#ndiswrapper)
    *   [6.15 prism54](#prism54)
    *   [6.16 ACX100/111](#ACX100/111)
    *   [6.17 BCM43XX](#BCM43XX)
    *   [6.18 b43](#b43)
    *   [6.19 rtl8187](#rtl8187)
    *   [6.20 zd1211rw](#zd1211rw)
    *   [6.21 Тестирование установки](#Тестирование_установки)
*   [7 Смотрите также](#Смотрите_также)

## Драйвер устройства

Стандартное ядро Arch Linux имеет модульную архитектуру, поэтому многие драйверы для аппаратного обеспечения расположены на жёстком диске и доступны как [модули](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0 "Модули ядра"). При загрузке менеджер устройств [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") определяет аппаратное обеспечение вашего компьютера и загружает соответствующие модули (драйверы), в результате чего создаётся сетевой *интерфейс*.

Некоторым беспроводным устройствам для работы помимо драйвера необходима ещё и прошивка. Во входящем в группу [base](https://www.archlinux.org/groups/x86_64/base/) пакете [linux-firmware](https://www.archlinux.org/packages/?name=linux-firmware) содержится большое количество образов прошивок, однако проприетаные прошивки в него не входят и должны устанавливаться отдельно. Подробное описание установки дано в разделе [#Установка драйвера/прошивки](#Установка_драйвера/прошивки).

**Примечание:** Если нужный модуль не был загружен менеджером udev при старте системы, просто [загрузите его вручную](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Управление_модулями_вручную "Модули ядра"). Иногда udev может загружать более одного драйвера для устройства, что приведёт к конфликту и помешает успешному конфигурированию. В этом случае [запретите загрузку](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0#Запрет_загрузки "Модули ядра") ненужного модуля.

### Проверка состояния драйвера

Чтобы проверить, загрузился ли драйвер сетевой карты, посмотрите на вывод команд `lspci -k` или `lsusb -v` (в зависимости от того, подключена карта по шине PCI(e) или через USB-порт). Вы должны увидеть используемые драйверы ядра, например:

 `$ lspci -k` 
```
06:00.0 Network controller: Intel Corporation WiFi Link 5100
	Subsystem: Intel Corporation WiFi Link 5100 AGN
	Kernel driver in use: iwlwifi
	Kernel modules: iwlwifi

```

**Примечание:** Если ваша сетевая карта является USB-устройством, выполнение `dmesg | grep usbcore` должно выдать что-то похожее на `usbcore: registered new interface driver rtl8187`.

Также проверьте вывод команды `ip link`, чтобы убедиться, что [сетевой интерфейс](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8#Сетевые_интерфейсы "Настройка сети") был создан; обычно название беспроводного интерфейса начинается с буквы "w", например, `wlp2s1`. Затем включите интерфейс командой

```
# ip link set *интерфейс* up

```

Например, если интерфейс называется `wlan0`, команда примет вид `ip link set wlan0 up`.

Если вы получили сообщение об ошибке `SIOCSIFFLAGS: No such file or directory` (Нет такого файла или каталога), то скорее всего для функционирования вашего беспроводного устройства необходима соответствующая прошивка.

Проверьте сообщения ядра на предмет загрузки прошивки:

 `$ dmesg | grep firmware` 
```
[   7.148259] iwlwifi 0000:02:00.0: loaded firmware version 39.30.4.1 build 35138 op_mode iwldvm

```

Если там нет интересующей вас информации, проверьте сообщения подробного вывода, относящиеся к определённому вами ранее модулю (в примере ниже `iwlwifi`):

 `$ dmesg | grep iwlwifi` 
```
[   12.342694] iwlwifi 0000:02:00.0: irq 44 for MSI/MSI-X
[   12.353466] iwlwifi 0000:02:00.0: loaded firmware version 39.31.5.1 build 35138 op_mode iwldvm
[   12.430317] iwlwifi 0000:02:00.0: CONFIG_IWLWIFI_DEBUG disabled
...
[   12.430341] iwlwifi 0000:02:00.0: Detected Intel(R) Corporation WiFi Link 5100 AGN, REV=0x6B

```

Если модуль ядра загрузился успешно и интерфейс запущен, можете пропустить следующий раздел.

### Установка драйвера/прошивки

Проверьте, находится ли ваша сетевая карта в числе поддерживаемых:

*   Изучите таблицу [существующих драйверов Linux для беспроводных устройств](https://wireless.wiki.kernel.org/en/users/drivers). Перейдя на страницу определённого драйвера вы найдёте список поддерживаемых устройств. Также можно посмотреть [список идентификаторов Wi-Fi устройств в Linux](https://wikidevi.com/wiki/List_of_Wi-Fi_Device_IDs_in_Linux).
*   В [Ubuntu Wiki](https://help.ubuntu.com/community/WifiDocs/WirelessCardsSupported) есть хороший список беспроводных карт и информация об их поддержке ядром Linux или драйвером пространства пользователя (включая название драйвера).
*   Проверьте ваше устройство на сайте [Linux Wireless Support](http://linux-wless.passys.nl/) или по реестру [hardware compatibility list](http://www.linuxquestions.org/hcl/index.php?cat=10), в котором также содержится список поддерживаемого ядром оборудования.

Если ваша беспроводная карта есть в одном из списков выше, перейдите в раздел [#Решение проблем с драйверами и прошивками](#Решение_проблем_с_драйверами_и_прошивками). В нём содержатся инструкции по установке драйверов и прошивок на некоторые редкие беспроводные карты. Затем [проверьте состояние драйвера](#Проверка_состояния_драйвера) снова.

Если вашей беспроводной карты нет в списках, то скорее всего она поддерживается только в Windows (некоторые Broadcom, 3com и др.). В этом случае вы можете воспользоваться [#ndiswrapper](#ndiswrapper).

## Утилиты

Управление беспроводными сетевыми интерфейсами, как и всеми прочими, осуществляется посредством входящей в пакет [iproute2](https://www.archlinux.org/packages/?name=iproute2) утилиты *ip*.

Для настройки беспроводного соединения необходим определённый набор программ. Для этих целей подойдет либо [сетевой менеджер](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Сетевые_менеджеры "Network configuration (Русский)"), либо один из следующих пакетов:

| Утилита | Пакет | [WEXT](https://wireless.wiki.kernel.org/en/developers/documentation/wireless-extensions) | [nl80211](https://wireless.wiki.kernel.org/en/developers/documentation/nl80211) | WEP | WPA/WPA2 | [Archiso](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archiso (Русский)") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) |
| [wireless_tools](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Tools.html) | [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools) | Да | Нет | Да | Нет | Да |
| [iw](https://wireless.kernel.org/en/users/Documentation/iw) | [iw](https://www.archlinux.org/packages/?name=iw) | Нет | Да | Да | Нет | Да |
| [WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA supplicant (Русский)") | [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) | Да | Да | Да | Да | Да |
| [iwd](/index.php/Iwd "Iwd") | [iwd](https://www.archlinux.org/packages/?name=iwd) | Нет | Да | Да | Да | Да |

1.  Устарела.

Имейте в виду, что некоторые сетевые карты поддерживают только WEXT.

### Сравнение iw и wireless_tools

Ниже представлено сравнение некоторых команд утилит *iw* и *wireless_tools*. Дополнительные примеры можно найти в статье о [замене iwconfig на iw](http://wireless.kernel.org/en/users/Documentation/iw/replace-iwconfig).

| Команда *iw* | Команда *wireless_tools* | Описание |
| iw dev *wlan0* link | iwconfig *wlan0* | Получение состояния соединения. |
| iw dev *wlan0* scan | iwlist *wlan0* scan | Сканирование доступных точек доступа. |
| iw dev *wlan0* set type ibss | iwconfig *wlan0* mode ad-hoc | Установка режима работы *ad-hoc*. |
| iw dev *wlan0* connect *ваш_essid* | iwconfig *wlan0* essid *ваш_essid* | Подключение к открытой сети. |
| iw dev *wlan0* connect *ваш_essid* 2432 | iwconfig *wlan0* essid *ваш_essid* freq 2432M | Подключение к открытой сети с указанием канала. |
| iw dev *wlan0* connect *ваш_essid* key 0:*ваш_ключ* | iwconfig *wlan0* essid *ваш_essid* key *ваш_ключ* | Подключение к сети с WEP шифрованием шестнадцатеричным ключом. |
| iwconfig *wlan0* essid *ваш_essid* key s:*ваш_ключ* | Подключение к сети с WEP шифрованием ASCII-ключом. |
| iw dev *wlan0* set power_save on | iwconfig *wlan0* power on | Включение режима энергосбережения. |

## iw

**Примечание:**

*   Большая часть представленных ниже команд должна выполняться с [правами root](/index.php/Users_and_groups "Users and groups"). При выполнении от лица обычного пользователя некоторые команды (например, *iw list*) завершат работу без ошибки, но сгенерированный ими вывод либо окажется некорректным, либо будет отсутствовать вовсе.
*   В зависимости от вашего аппаратного обеспечения и типа шифрования некоторые перечисленные ниже шаги могут оказаться не нужны. Некоторые сетевые карты требуют включения интерфейса и/или поиска точки доступа перед привязкой к ней и получением IP-адреса. Возможно, придётся немного поэкспериментировать. Например, пользователи с WPA/WPA2 могут попытаться активировать беспроводную сеть напрямую с шага [#Соединение с точкой доступа](#Соединение_с_точкой_доступа).

В примерах ниже беспроводное устройство с названием `*интерфейс*` устанавливает соединение с точкой доступа Wi-Fi `*ваш_essid*`. Замените названия на свои.

### Определение имени интерфейса

**Совет:** В [официальной документации](http://wireless.kernel.org/en/users/Documentation/iw) утилиты *iw* можно найти дополнительные примеры.

Чтобы узнать название беспроводного интерфейса, выполните:

```
$ iw dev

```

Название интерфейса будет указано после слова "Interface". Например, `wlan0`.

### Определение состояния интерфейса

Чтобы проверить состояние соединения, выполните:

```
$ iw dev *интерфейс* link

```

Статистическую информацию (количество tx/rx байт, мощность сигнала и т.д.) можно получить, введя команду:

```
$ iw dev *интерфейс* station dump

```

### Включение интерфейса

**Совет:** В большинстве случаев выполнять эти действия не требуется.

Некоторые карты требуют включения интерфейса перед использованием *iw* или *wireless_tools*.

```
# ip link set *интерфейс* up

```

**Примечание:** Если получена ошибка вида `RTNETLINK answers: Operation not possible due to RF-kill`, убедитесь, что аппаратный переключатель находится в положении *on*. Дополнительную информацию вы найдёте в разделе [#Предостережения Rfkill](#Предостережения_Rfkill).

Чтобы убедиться, что интерфейс включён, выполните:

 `$ ip link show *интерфейс*`  `3: wlan0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state DOWN mode DORMANT group default qlen 1000 link/ether 12:34:56:78:9a:bc brd ff:ff:ff:ff:ff:ff` 

На включённое состояние интерфейса указывает слово `UP` в `BROADCAST,MULTICAST,UP,LOWER_UP`, а не надпись `state DOWN`.

### Обнаружение точек доступа

Чтобы просмотреть список доступных точек доступа, выполните:

```
# iw dev *интерфейс* scan | less

```

**Примечание:** Если в результате появилось сообщение `Interface does not support scanning` (Интерфейс не поддерживает сканирование), то скорее всего вы забыли установить прошивку. В некоторых случаях это сообщение может появиться, если вы выполнили команду не от имении root.

**Совет:** В зависимости от местоположения вам может понадобиться настроить правильное имя управляющего домена, чтобы увидеть все доступные сети.

Обратите внимание на следующие поля:

*   **SSID**: название сети.
*   **Signal**: мощность беспроводного излучения в единицах dBm (например, от -100 до 0). Более близкие к нулю значения означают лучший сигнал. На основании отображаемой мощности можно получить представление о покрытии сети.
*   **Security**: напрямую не указывается; проверьте строку, которая начинается с `capability`. Если там содержится указание `Privacy`, например, `capability: ESS Privacy ShortSlotTime (0x0411)`, то ваша сеть как-то защищена.
    *   Если вы видите информационный блок `RSN`, то сеть защищена протоколом [Robust Security Network](https://en.wikipedia.org/wiki/ru:IEEE_802.11i-2004 "wikipedia:ru:IEEE 802.11i-2004"), также известным как WPA2.
    *   Если вы видите информационный блок `WPA`, то сеть защищена протоколом [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/ru:WPA "wikipedia:ru:WPA").
    *   В блоках `RSN` и `WPA` может быть указана следующая информация:
        *   **Group cipher:** принимает значения TKIP, CCMP, both, others.
        *   **Pairwise ciphers:** принимает значения TKIP, CCMP, both, others. Может отличаться от значения в Group cipher.
        *   **Authentication suites:** принимает значения PSK, 802.1x, others. Для домашнего маршрутизатора вы скорее всего обнаружите здесь значение PSK (то есть пароль). В университетах вероятнее всего будет сеть 802.1x, что требует логин и пароль. Тогда вам потребуется узнать, какое используется управление ключами (например, EAP), и какой способ инкапсуляции (например, PEAP). Подробную информацию можно найти в разделе [#WPA2 Enterprise](#WPA2_Enterprise) и статье [Wikipedia:Authentication protocol](https://en.wikipedia.org/wiki/Authentication_protocol "wikipedia:Authentication protocol").
    *   Если вы не видите ни `RSN`, ни `WPA`, но есть раздел `Privacy`, то используется защитный протокол WEP.

### Выбор режима работы

Возможно, будет необходимо выбрать подходящий режим работы беспроводной карты. Например, если вы хотите подключиться к [сети ad-hoc](/index.php/Ad-hoc_networking "Ad-hoc networking"), то нужно установить режим работы `ibss`:

```
# iw dev *интерфейс* set type ibss

```

**Примечание:** Смена режима работы на некоторых картах может потребовать отключения беспроводного интерфейса (`ip link set *интерфейс* down`).

### Соединение с точкой доступа

Необходимо привязать устройство к точке доступа и ввести ключ в зависимости от типа шифрования:

*   **Без шифрования** `# iw dev interface connect *"ваш_essid"*` 
*   **WEP**
    *   С использованием шестнадцатеричного ключа (формат ключа определится автоматически, поскольку WEP-ключ имеет фиксированную длину): `# iw dev *интерфейс* connect *"ваш_essid"* key 0:your_key` 
    *   С использованием ASCII-ключа, указав третий ключ в качестве ключа по умолчанию (ключи нумеруются с нуля, всего возможно до четырёх ключей): `# iw dev *интерфейс* connect *"ваш_essid"* key d:2:your_key` 

Вне зависимости от использованного способа, проверьте соединение:

```
# iw dev *интерфейс* link

```

## Wi-Fi Protected Access

### WPA2 Personal

WPA2 Personal, или WPA2-PSK — одна из реализаций технологии [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/ru:WPA "wikipedia:ru:WPA").

Выполнить вход в сеть WPA2 Personal можно посредством утилит [WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA supplicant (Русский)") или [iwd](/index.php/Iwd "Iwd"), а также с помощью [сетевого менеджера](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Сетевые_менеджеры "Network configuration (Русский)"). Если вы вошли в данную сеть впервые, то для создания нормально функционирующего соединения необходимо выполнить привязку IP-адреса(-ов) и маршрутов либо [вручную](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Статический_IP-адрес "Network configuration (Русский)"), либо с помощью [DHCP](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#DHCP "Network configuration (Русский)")-клиента.

Ниже описано подключение к сети WPA2 Personal с помощью [WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA supplicant (Русский)"). В частности, этот способ используется при установке Arch Linux по беспроводной сети. Все необходимые команды уже включены в live-сессию.

Сначала выполните шифрование пароля маршрутизатора:

```
# wpa_passphrase *ваш_essid* *ваш_пароль* > /etc/wpa_supplicant/*ваш_essid.conf*

```

Перед запуском wpa_supplicant убедитесь, что соединение существует:

```
# wpa_supplicant -c /etc/wpa_supplicant/*ваш_essid.conf* -i *ваше_беспроводное_устройство*

```

Возможно, вы увидите сообщения об ошибках, но в конце должно появиться сообщение "connected" ("соединено"). Если это так, то нажмите <Ctrl>-c и запустите wpa_supplicant в фоне (background):

```
# wpa_supplicant -B -c /etc/wpa_supplicant/*ваш_essid.conf* -i *ваше_беспроводное_устройство*

```

Наконец, необходимо выполнить привязку IP-адреса. Если вы используете DHCP, выполните:

```
# dhclient *ваше_беспроводное_устройство*

```

На этом настройка беспроводного соединения завершена.

### WPA2 Enterprise

*WPA2 Enterprise* — ещё одна реализация технологии [Wi-Fi Protected Access](https://en.wikipedia.org/wiki/ru:WPA "wikipedia:ru:WPA"). Она предлагает лучшую безопасность и управление ключами по сравнению с *WPA2 Personal*, а также дополнительную функциональность корпоративного типа вроде VLAN и [NAP](https://en.wikipedia.org/wiki/ru:%D0%97%D0%B0%D1%89%D0%B8%D1%82%D0%B0_%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%B0_%D0%BA_%D1%81%D0%B5%D1%82%D0%B8 "wikipedia:ru:Защита доступа к сети"). Для работы этой технологии требуется внешний аутентификационный сервер, [RADIUS](https://en.wikipedia.org/wiki/ru:RADIUS "wikipedia:ru:RADIUS"), обрабатывающий попытки аутентификации пользователей. Это отличает Enterprise-режим от режима Personal, которому не требуется ничего кроме маршрутизатора или точки доступа с одним паролем для всех пользователей.

Корпоративный (Enterprise) режим осуществляет подключение пользователей к сети посредством имени пользователя и пароля и/или цифрового сертификата. Поскольку каждый пользователь обладает уникальным динамическим ключом шифрования, это также позволяет предотвратить отслеживание пользователей в беспроводной сети и усилить шифрование.

Ниже описана настройка [сетевых клиентов](/index.php/List_of_applications#Network_managers "List of applications"), соединяющихся с беспроводной точкой доступа в режиме WPA2 Enterprise. Информацию о настройке самой точки доступа можно найти в статье [Software access point#RADIUS](/index.php/Software_access_point_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#RADIUS "Software access point (Русский)").

**Примечание:** Корпоративный режим требует более сложной настройки клиента, в то время как режим Personal требует только введения пароля по запросу. Клиентам скорее всего придется установить CA-сертификат сервера (плюс сертификаты пользователей при использовании EAP-TLS), а затем вручную настроить безопасность и аутентификацию по протоколу 802.1X.

Сравнение протоколов сведено в [таблицу](http://deployingradius.com/documents/protocols/compatibility.html).

**Важно:** Существует возможность использовать WPA2 Enterprise без проверки CA-сертификата сервера, однако использовать её не стоит. Без аутентификации точки доступа соединение может стать объектом атаки "человек посередине" ("man-in-the-middle"). Хотя "рукопожатия" обычно зашифрованы, передача пароля чаще всего производится открытым текстом или посредством ненадёжного протокола [#MS-CHAPv2](#MS-CHAPv2). В результате клиент может послать пароль чужой точке доступа, которая станет выполнять роль посредника (proxy) в соединении, прослушивая весь передаваемый через неё трафик.

#### eduroam

[eduroam](https://en.wikipedia.org/wiki/ru:eduroam "wikipedia:ru:eduroam") — международный роуминговый сервис на основе WPA2 Enterprise для лиц, занятых в сфере научно-исследовательской деятельности, высшего образования и дополнительного профессионального образования.

**Примечание:**

*   Перед применением любых настроек, предложенных в этом разделе, рекомендуется сначала проверить их со специалистами вашего учреждения. Предложенные здесь профили настроек предлагаются безо всяких гарантий на предмет работоспособности или соответствия каким-либо требованиям безопасности.
*   При хранении профилей соединения в незашифрованном виде рекомендуется оставить только доступ на чтение для root, выполнив команду `# chmod 600 *профиль*`.

**Совет:** Настройки для утилит [NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)") и [#wpa_supplicant](#wpa_supplicant) можно сгенерировать с помощью [eduroam Configuration Assistant Tool](https://cat.eduroam.org/).

#### Ручная/автоматическая настройка

##### wpa_supplicant

[WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Расширенное_использование "WPA supplicant (Русский)") настраивается напрямую в его файле настроек или посредством интерфейса; используется вместе с клиентом DHCP. Примеры настроек приведены в файле `/usr/share/doc/wpa_supplicant/wpa_supplicant.conf`.

##### NetworkManager

[NetworkManager](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)") может генерировать профили WPA2 Enterprise с помощью [графических интерфейсов](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Графические_интерфейсы "NetworkManager (Русский)"). Утилиты *nmcli* и *mntui* эту возможность не поддерживают, но работают с готовыми профилями.

##### connman

[ConnMan](/index.php/ConnMan "ConnMan") требует создания отдельного файла настроек перед [соединением](/index.php/ConnMan#Wi-Fi "ConnMan") с беспроводной сетью. Подробности можно найти в руководстве [connman-service.config(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connman-service.config.5) и в статье [Connman#Connecting to eduroam](/index.php/ConnMan#Connecting_to_eduroam_.28802.1X.29 "ConnMan").

##### netctl

[netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)") может использовать настройки [#wpa_supplicant](#wpa_supplicant) посредством блоков `WPAConfigSection=`. Детали вы найдёте в руководстве [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5).

**Важно:** В настройках netctl особые правила использования кавычек: обратите внимание на раздел `SPECIAL QUOTING RULES` в [netctl.profile(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.profile.5).

**Совет:** Можно разрешить произвольный сертификат, добавив строку `'ca_cert="/path/to/special/certificate.cer"'` в блоке `WPAConfigSection`.

#### Проблемы

##### MS-CHAPv2

Беспроводные сети WPA2-Enterprise, полагающиеся на аутентификацию MSCHAPv2 type-2 с использованием PEAP иногда требуют установки [pptpclient](https://www.archlinux.org/packages/?name=pptpclient) помимо стандартного [ppp](https://www.archlinux.org/packages/?name=ppp). [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)"), однако, работает "из коробки" без ppp-mppe. В любом случае, использование MSCHAPv2 не рекомендуется из-за ненадежности этого протокола, но другого варианта часто просто нет.

## Решение проблем

В этом разделе содержатся основные рекомендации по решению проблем, не связанных непосредственно с драйверами и прошивками. Для получения такой информации смотрите следующий раздел [#Решение проблем с драйверами и прошивками](#Решение_проблем_с_драйверами_и_прошивками).

### Предостережения Rfkill

Многие лэптопы имеют аппаратный переключатель (или кнопку) для выключения беспроводной карты, однако, она может быть также заблокировани и ядром. Этим можно управлять через rfkill. Используйте *rfkill*, чтобы посмотреть текущий статус:

 `# rfkill list` 
```
0: phy0: Wireless LAN
	Soft blocked: yes
	Hard blocked: yes

```

Если карта *заблокирована аппаратно*, используйте переключатель (кнопку), чтобы разблокировать её. Если же карта заблокирована не *аппаратно*, a *программно*, используйте следующую команду:

```
# rfkill unblock wifi

```

**Примечание:** Возможно, при нажатии аппаратной кнопки карта из состояния *hard-blocked* и *soft-unblocked* перейдёт в состояние *hard-unblocked* и *soft-blocked* (i.e. the *soft-blocked* bit is just switched no matter what). Это можно исправить, отрегулировав некоторые опции [модуля ядра](/index.php/Kernel_modules_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel modules (Русский)") `rfkill`

Дополнительная информация: [http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill](http://askubuntu.com/questions/62166/siocsifflags-operation-not-possible-due-to-rf-kill)

### Уважение управляющего домена

The [regulatory domain](https://en.wikipedia.org/wiki/IEEE_802.11#Regulatory_domains_and_legal_compliance "wikipedia:IEEE 802.11"), or "regdomain", is used to reconfigure wireless drivers to make sure that wireless hardware usage complies with local laws set by the FCC, ETSI and other organizations. Regdomains use [ISO 3166-1 alpha-2 country codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2 "wikipedia:ISO 3166-1 alpha-2"). For example, the regdomain of the United States would be "US", China would be "CN", etc.

Regdomains affect the availability of wireless channels. In the 2.4GHz band, the allowed channels are 1-11 for the US, 1-14 for Japan, and 1-13 for most of the rest of the world. In the 5GHz band, the rules for allowed channels are much more complex. In either case, consult [this list of WLAN channels](https://en.wikipedia.org/wiki/List_of_WLAN_channels "wikipedia:List of WLAN channels") for more detailed information.

Regdomains also affect the limit on the [effective isotropic radiated power (EIRP)](https://en.wikipedia.org/wiki/Equivalent_isotropically_radiated_power "wikipedia:Equivalent isotropically radiated power") from wireless devices. This is derived from transmit power/"tx power", and is measured in [dBm/mBm (1dBm=100mBm) or mW (log scale)](https://en.wikipedia.org/wiki/DBm "wikipedia:DBm"). In the 2.4GHz band, the maximum is 30dBm in the US and Canada, 20dBm in most of Europe, and 20dB-30dBm for the rest of the world. In the 5GHz band, maximums are usually lower. Consult the [wireless-regdb](http://git.kernel.org/cgit/linux/kernel/git/linville/wireless-regdb.git/tree/db.txt) for more detailed information (EIRP dBm values are in the second set of brackets for each line).

Misconfiguring the regdomain can be useful - for example, by allowing use of an unused channel when other channels are crowded, or by allowing an increase in tx power to widen transmitter range. However, **this is not recommended** as it could break local laws and cause interference with other radio devices.

To configure the regdomain, install [crda](https://www.archlinux.org/packages/?name=crda) and [wireless-regdb](https://www.archlinux.org/packages/?name=wireless-regdb) and reboot (to reload the `cfg80211` module and all related drivers). Check the boot log to make sure that CRDA is being called by `cfg80211`:

```
$ dmesg | grep cfg80211

```

The current regdomain can be set to the United States with:

```
# iw reg set US

```

And queried with:

```
$ iw reg get

```

**Note:** Your device may be set to country "00", which is the "world regulatory domain" and contains generic settings. If this cannot be unset, CRDA may be misconfigured.

However, setting the regdomain may not alter your settings. Some devices have a regdomain set in firmware/EEPROM, which dictates the limits of the device, meaning that setting regdomain in software [can only increase restrictions](http://wiki.openwrt.org/doc/howto/wireless.utilities#iw), not decrease them. For example, a CN device could be set in software to the US regdomain, but because CN has an EIRP maximum of 20dBm, the device will not be able to transmit at the US maximum of 30dBm.

For example, to see if the regdomain is being set in firmware for an Atheros device:

```
$ dmesg | grep ath:

```

For other chipsets, it may help to search for "EEPROM", "regdomain", or simply the name of the device driver.

To see if your regdomain change has been successful, and to query the number of available channels and their allowed transmit power:

```
$ iw list | grep -A 15 Frequencies:

```

A more permanent configuration of the regdomain can be achieved through editing `/etc/conf.d/wireless-regdom` and uncommenting the appropriate domain. `wpa_supplicant` can also use a regdomain in the `country=` line of `/etc/wpa_supplicant.conf`.

It is also possible to configure the [cfg80211](http://wireless.kernel.org/en/developers/Documentation/cfg80211) kernel module to use a specific regdomain by adding, for example, `options cfg80211 ieee80211_regdom=EU` to `/etc/modprobe.d/modprobe.conf`. However, this is part of the [old regulatory implementation](http://wireless.kernel.org/en/developers/Regulatory#The_ieee80211_regdom_module_parameter).

For further information, read the [wireless.kernel.org regulatory documentation](http://wireless.kernel.org/en/developers/Regulatory/).

### Просмотр логов

A good first measure to troubleshoot is to analyze the system's logfiles first. In order not to manually parse through them all, it can help to open a second terminal/console window and watch the kernels messages with

```
$ dmesg -w

```

while performing the action, e.g. the wireless association attempt.

When using a tool for network management, the same can be done for systemd with

```
# journalctl -f 

```

Frequently a wireless error is accompanied by a deauthentication with a particular reason code, for example:

```
wlan0: deauthenticating from XX:XX:XX:XX:XX:XX by local choice (reason=3)

```

Looking up [the reason code](http://www.aboutcher.co.uk/2012/07/linux-wifi-deauthenticated-reason-codes/) might give a first hint.

The individual tools used in this article further provide options for more detailed debugging output, which can be used in a second step of the analysis, if required.

### Энергосбережение

Смотрите раздел [Энергосбережение#Сетевые интерфейсы](/index.php/Power_saving#Network_interfaces "Power saving").

### Не удалось получить IP адрес

*   Если получение IP адреса неоднократно не удаётся при использовании клиента по умолчанию [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd), попробуйте установить и использовать [dhclient](https://www.archlinux.org/packages/?name=dhclient) вместо него. Не забудьте выбрать *dhclient* как первичный DHCP клиент в вашем [менеджере соединений](#Автоматическая_настройка)!

*   Если вы можете получить IP для проводного интерфейса, но не можете для беспроводного, попробуйте отключить энергосберегающие функции вашей беспроводной карты:

```
# iwconfig wlan0 power off

```

*   Если вы получаете timeout ошибку из-за *waiting for carrier* проблемы, возможно вам понадобится установить канал в `auto` для конкретного устройства:

```
# iwconfig wlan0 channel auto

```

Перед тем как изменить канал на автоматический, убедитесь что вы опустили беспроводной интерфейс. После того, как поменяете канал, можете опять поднять интерфейс.

### Connection always times out

The driver may suffer from a lot of tx excessive retries and invalid misc errors for some unknown reason, resulting in a lot of packet loss and keep disconnecting, sometimes instantly. Following tips might be helpful.

#### Lowering the rate

Try setting lower rate, for example 5.5M:

```
# iwconfig wlan0 rate 5.5M auto

```

Fixed option should ensure that the driver does not change the rate on its own, thus making the connection a bit more stable:

```
# iwconfig wlan0 rate 5.5M fixed

```

#### Понижение txpower

Вы можете попробовать понизить мощность передатчика. Это может сберегать энергию:

```
# iwconfig wlan0 txpower 5

```

Установите значение от `0` до `20`, `auto` или `off`.

#### Setting rts and fragmentation thresholds

Default iwconfig options have rts and fragmentation thresholds off. These options are particularly useful when there are many adjacent APs or in a noisy environment.

The minimum value for fragmentation value is 256 and maximum is 2346\. In many windows drivers the maximum is the default value:

```
# iwconfig wlan0 frag 2346

```

For rts minimum is 0, maximum is 2347\. Once again windows drivers often use maximum as the default:

```
# iwconfig wlan0 rts 2347

```

### Внезапные отключения

#### Причина #1

If dmesg says `wlan0: deauthenticating from MAC by local choice (reason=3)` and you lose your Wi-Fi connection, it is likely that you have a bit too aggressive power-saving on your Wi-Fi card[[2]](http://us.generation-nt.com/answer/gentoo-user-wireless-deauthenticating-by-local-choice-help-204640041.html). Try disabling the wireless card's power-saving features:

```
# iwconfig wlan0 power off

```

See [Power saving](/index.php/Power_saving "Power saving") for tips on how to make it permanent (just specify `off` instead of `on`).

If your card does not support `iwconfig wlan0 power off`, check the **BIOS** for power management options. Disabling PCI-Express power management in the BIOS of a Lenovo W520 resolved this issue.

#### Причина #2

If you are experiencing frequent disconnections and dmesg shows messages such as

`ieee80211 phy0: wlan0: No probe response from AP xx:xx:xx:xx:xx:xx after 500ms, disconnecting`

try changing the channel bandwidth to `20MHz` through your router's settings page.

#### Причина #3

On some laptop models with hardware rfkill switches (e.g., Thinkpad X200 series), due to wear or bad design, the switch (or its connection to the mainboard) might become loose over time resulting in seemingly random hardblocks/disconnects when you accidentally touch the switch or move the laptop. There is no software solution to this, unless your switch is electrical and the BIOS offers the option to disable the switch. If your switch is mechanical (most are), there are lots of possible solutions, most of which aim to disable the switch: Soldering the contact point on the mainboard/wifi-card, glueing or blocking the switch, using a screw nut to tighten the switch or removing it altogether.

## Решение проблем с драйверами и прошивками

Здесь описаны подобности о том, как можно получить драйверы для вашего устройства. Вы можете обнаружить, что для вас есть несколько вариантов, помните, что вы можете найти здесь [HCL](http://www.linuxquestions.org/hcl/index.php?cat=10%7CLQ) помощь в выборе лучшего драйвера.

Здесь, возможно, описаны не все драйвера. Смотрите англоязычную версию статьи для получения информации по другим картам.

#### wlan-ng

```
pacman -S wlan-ng26 wlan-ng26-utils

```

Для wlan-ng вам не нужна утилита wireless-tools как сказано выше. Вместо них вам нужны утилиты из пакета wlan-ng26-utils: wlancfg и wlanctl-ng.

#### rt2x00

Для чипсетов Ralink (как rt2500,rt61,rt73 др.). Совместимы с wpa_supplicant, используют wext как интерфейс драйвера. Этот драйвер сейчас (в 2.6.24) является частью ядра и может быть загружен вручную например так...

 `modprobe rt2500pci` 

(замените при необходимости на rt2500pci например, т.е. rt2400pci, rt2500usb, rt61pci, rt73usb)

Для некоторых чипов необходимы прошивки (firmware). Смотри [rt2x00 статью wiki](/index.php/Using_the_new_rt2x00_beta_driver "Using the new rt2x00 beta driver").

#### RT2500

Для чипсетов Ralink PCI/PCMCIA основанных rt2500 сериях (первое поколение чипов Ralink с поддержкой 802.11g).

 `pacman -S rt2500` 

Поддержка стандартной утилиты iwconfig для шифрования WEP соединений, также могут быть использованы другие стандартные утилиты. wpa_supplicant не поддерживает стандартный wext интерфейс. Драйвер поддерживает WPA (использую встроенное шифрование), но не стандартными способами. Разрабатываемая версия wpa_supplicant (0.6.x) включает в себя поддержку специальных технологий и это может негативно сказаться на WPA соединениях, устанавливаемых вручную через iwpriv команды. Смотрите [эти инструкции](http://rt2400.cvs.sourceforge.net/*checkout*/rt2400/source/rt2500/Module/iwpriv_usage.txt) для подробностей. Некоторые применимые методы для RT61 и RT73 ниже.

#### RT61

Для PCI/PCMCIA карт, основанных на чипе Ralink следующего поколения 802.11g (включена поддержка проприетарных MIMO функций). Смотри [RT61 статью wiki](/index.php/RT61_Wireless "RT61 Wireless").

#### RT73

Для USB устройств, основанных на чипах Ralink следующих поколений 802.11g (включена поддержка проприетарных MIMO функций). Смотри [RT73 статью wiki](/index.php/RT73_Wireless "RT73 Wireless").

#### madwifi

```
pacman -S madwifi

```

Модуль называется <tt>ath_pci</tt>. Чтобы его использовать, Вы должны в rc.conf убрать загрузку ath5k и добавить два модуля madwifi:

```
MODULES=(!ath5k ath_hal ath_pci ... ...)

```

Некоторым пользователям, возможно, при загрузке драйвера madwifi придется использовать код региона. Это связано с использованием каналов и частот, легальных для конкретной страны/региона. Для России, например, вы должны загрузить этот модуль так:

```
modprobe ath_pci countrycode=643

```

Вы можете проверить настройки, использую команду <tt>iwlist</tt>. Смотрите <tt>man iwlist</tt> и [CountryCode page on the MadWifi wiki](http://madwifi-project.org/wiki/UserDocs/CountryCode) . Для использования этих настроек при загрузке, добавьте следующую строку в <tt>/etc/modprobe.d/modprobe.conf</tt>:

```
options ath_pci countrycode=643

```

ATTENTION: Возможно, Вам придётся удалить код страны/региона, если устройство ath0 не будет создано (kernel 2.6.21)!

Особенностью драйверов madwifi является то, что переключение в режим ad-hoc осуществляется двумя командами:

```
wlanconfig ath0 destroy
wlanconfig ath0 create wlandev wifi0 wlanmode adhoc

```

#### ath5k

Планируется, что с течением времени ath_pci станет частью истории, и его заменит ath5k. Для использования этого открытого драйвера добавьте его загрузку в rc.conf:

```
MODULES=(ath5k ... ...)

```

Проверьте, что в секции MODULES отсутствуют параметры ath_hal и ath_pci.

#### ath9k

ath9k - это официальный драйвер компании Atheros для карт с новейшими 802.11n чипсетами (максимальная пропускная способность около 180 Мб/с). Чтобы просмотреть весь список поддерживаемого оборудования, проверьте [supported chipsets](http://wireless.kernel.org/en/users/Drivers/ath9k).

Доступные режимы: Station, AP и Adhoc.

ath9k включен в состав ядра, начиная с версии 2.6.27\. Для дискуссий по поддержке и разработке создан [mailing list](https://lists.ath9k.org/mailman/listinfo/ath9k-devel).

#### rtl8723bu

В текущем ядре драйвер для `rtl8723bu` не рабочий. Для решения проблемы требуется самостоятельная сборка модуля из исходников, либо установка из AUR. Исходники можете найти в [GitHub репозитории](https://github.com/lwfinger/rtl8723bu). Пакеты из AUR [rtl8723bu-git](https://aur.archlinux.org/packages/rtl8723bu-git/), либо [rtl8723bu-git-dkms](https://aur.archlinux.org/packages/rtl8723bu-git-dkms/)

#### ipw2100 and ipw2200

Смотря какой чипсет у вас имеется, используйте следующее:

```
pacman -S ipw2100-fw

```

или:

```
pacman -S ipw2200-fw

```

Вам необходимо перезагрузиться, чтобы изменения были приняты.

#### ipw3945 and ipw4965

Новые драйверы Intel [iwlwifi project](http://intellinuxwireless.org/?p=iwlwifi) работают с обоими чипсетами и включены в ядра v2.6.24 и выше. Просто установите прошивки:

```
pacman -S iwlwifi-3945-ucode

```

или:

```
pacman -S iwlwifi-4965-ucode

```

Если MOD_AUTOLOAD установлено в yes в /etc/rc.conf (так по умолчанию). Просто перезагрузитесь и проверьте, что драйверы работают с помощью ***ifconfig*** из терминала. Теперь можно сканировать сети через wlan0.

Если вы хотите, чтобы драйвера загружались вручную при загрузке добавьте их в строку MODULES:

```
nano /etc/rc.conf

```

в строке MODULES=(), добавьте **iwl3945** или **iwl4965** в список, в зависимости от вашего чипсета.

CTRL + X, Y для закрытия и сохранения.

Теперь драйверы должны быть загружены после перезагрузки и при запуске 'ifconfig' из терминала вы увидите, что там появился новый сетевой интерфейс **wlan0**.

Note: если драйверы iwlwifi, являющиеся "экспериментальными", не работают, знайте, что драйверы NETw4x32 работают отлично через ndiswrapper.

#### ipw3945 (Альтернативный метод)

***Note:** Этот драйвер ipw3945 должен входить в проект Intel's iwlwifi.*

 `pacman -S ipw3945` 

Это должно установить ipw3945-ucode, ipw3945, и ipw3945d (daemon).

Для инициализации устройства при загрузке отредактируйте...

 `nano /etc/rc.conf` 

в строке modules=(), добавьте ipw3945 в список

в строке daemons=(), добавьте ipw3945d в список (он должно быть ПЕРЕД network и dhcdbd/networkmanager в списке)

CTRL + X, Y для закрытия и сохранения.

Модуль ipw3945 должен быть загружен в процессе "Loading Modules.." и "Starting IPW3945d" должен появиться в ходе загрузки демона, и должен присутствовать интерфейс ethX.

Обновление: На моём HP nc6320 Bluetooth не соединяется, пока не выгрузишь модуль ipw3945.

#### orinoco

Часть, которая идёт с пакетом ядра и уже должна быть установлена.

#### ndiswrapper

Ndiswrapper не настоящий драйвер, но с ним вы можете использовать неродные Linux драйвера для ваших беспроводных устройств. Это очень помогает во многих ситуациях. Для использования его у вас должны быть *.inf файл из windows-драйверов (*.sys файл также должен присутствовать в этой же директории). Для установки ndiswrapper вам необходимо проделать следующие шаги:

Установить ndiswrapper используя pacman:

 `pacman -S ndiswrapper ndiswrapper-utils` 

*Note:* Beyond kernel-ядру необходим пакет ndiswrapper-beyond вместо ndiswrapper!

*Note:* Если у вас на машине нет доступа в интернет, вы можете скачать эти пакеты заранее к себе на компьютер с одного из зеркал, таких как [http://www2.cddc.vt.edu/linux/distributions/archlinux/extra/os/i686/](http://www2.cddc.vt.edu/linux/distributions/archlinux/extra/os/i686/) . (Note: это устаревшее зеркало, лучше использовать [ftp://ftp.archlinux.org/core/os/i686/](ftp://ftp.archlinux.org/core/os/i686/) ) Вам необходим пакет ndiswrapper (или ndiswrapper-beyond как было сказано выше) и пакет ndiswrapper-utils. Также вы можете скачать последнее ядро kernel26 (или beyond), т.к. на CD не всегда последнее ядро.

Когда установка завершена, выполните следующие шаги для настройки ndiswrapper.

```
ndiswrapper -i filename.inf
ndiswrapper -l
ndiswrapper -m
depmod -a
```

Сейчас установка ndiswrapper полностью завершена; вам только необходимо отредактировать /etc/rc.conf для загрузки модуля при старте системы (ниже приведён мой простейший конфиг; у вас может немного отличаться):

 `MODULES=(ndiswrapper snd-intel8x0 !usbserial)` 

Важно убедиться, что ndiswrapper присутствует в этом списке, также добавить другие необходимые модули. Лучший способ проверить, что ndiswrapper загружен:

```
modprobe ndiswrapper
iwconfig
```

и wlan0 должен присутствовать. Посмотрите следующую страницу при обнаружении проблем: [Установка Ndiswrapper](http://ndiswrapper.sourceforge.net/joomla/index.php?/component/option,com_openwiki/Itemid,33/id,installation/).

#### prism54

Скачайте файлы прошивки (firmware) для вашей карточки [с этого сайта](http://www.prism54.org/). Переименуйте файл прошивки в 'isl3890'. Если не существует, создайте директорию /lib/firmware и поместите файл 'isl3890' туда. Это должно быть сделано. ([forum source](https://bbs.archlinux.org/viewtopic.php?t=16569&start=0&postdays=0&postorder=asc&highlight=siocsifflags+such+file++directory))

#### ACX100/111

Установите пакеты 'tiacx' и 'tiacx-firmware' из репозитория core.

```
pacman -S tiacx tiacx-firmware

```

Драйвер должен сказать, какая прошивка (firmware) ему необходима; проверьте /var/log/messages.log или через команду dmesg. Переместите прошивку в '/lib/firmware'. Я делаю так:

```
ln -s /usr/share/tiacx/acx111_2.3.1.31/tiacx111c16 /lib/firmware

```

Hint: Если драйвер захламляет лог ядра, например потому, что запущен Kismet, вы должны добавить следующее в /etc/modprobe.d/modprobe.conf:

```
options acx debug=0

```

#### BCM43XX

Пользователи, у которых чипсет из серии Broadcom 43xx имеют альтернативу ndiswrapper'у. В Ядре версии 2.6.17, драйвер bcm43xx представлен.

1.  Запустите `iwconfig` или `hwd -s` для того, чтобы удостовериться, что драйвер загружен. Мой вывод hwd -s выглядит примерно так: `Network    : Broadcom Corp.|BCM94306 802.11g NIC module: unknown` 

Список поддерживаемого оборудования можно найти здесь [here](http://bcm43xx.berlios.de/?go=devices).

1.  Запустите `pacman -S bcm43xx-fwcutter` для установки прошивки.
2.  Скачайте драйвера для Windows для вашей карточки откуда вы скачивали прошивку.
3.  Распаковать драйвера с страницы Dell можно через Windows или под WINE (это .exe файл который распаковывается в C:\Dell\[driver numbers]). Или можете попробывать скачать [[3]](http://downloads.openwrt.org/sources/wl_apsta-3.130.20.0.o) или [[4]](http://freewebs.com/ronserver/bcm43xx.tar.gz). Я просто сохранил файлы на рабочий стол; вам это не надо после следующего шага.
4.  Запустите `bcm43xx-fwcutter -w /lib/firmware /home/<user>/Desktop/wl_apsta.o` Сначала необходимо сначала создать директорию /lib/firmware.
5.  Перезагрузитесь, и нормально настройте соединение. Вы можете добавить модуль bcm43xx в секцию modules в вашем rc.conf. Удачи!

#### b43

**Данный драйвер плохо работает с BCM4312 (возможны зависания при загрузке системы), для данной карты лучше использовать [broadcom-wl](/index.php/Broadcom_BCM4312 "Broadcom BCM4312") из aur**

Этот драйвер - преемник драйвера bcm43xx и он включен в ядро 2.6.24.

1.  Запустите `hwd -s` для определения вашей карты. Мой вывод hwd -s выглядит примерно так: `Network    : BCM4318 [AirForce One 54g] 802.11g Wireless LAN Controller module: unknown` 

Список поддерживаемого оборудования находится [здесь](http://wireless.kernel.org/en/users/Drivers/b43).

1.  Установите fwcutter из репозитория core: `pacman -S b43-fwcutter` 
2.  Скачайте проприетарную версию драйверов Broadcom: `wget http://downloads.openwrt.org/sources/broadcom-wl-4.150.10.5.tar.bz2` 
3.  Далее: `tar xjf broadcom-wl-4.150.10.5.tar.bz2`  `cd broadcom-wl-4.150.10.5/driver`  `b43-fwcutter -w /lib/firmware/ wl_apsta_mimo.o` 
4.  Перезагрузитесь, и нормально настройте ваше оборудование. Вы также можете добавить модуль b43 в секцию modules в ваш rc.conf. Удачи!

#### rtl8187

Смотри [rtl8187 wiki page](/index.php/Rtl8187_wireless "Rtl8187 wireless").

#### zd1211rw

[zd1211rw](http://zd1211.wiki.sourceforge.net/) драйвер для ZyDAS ZD1211 802.11b/g USB WLAN чипсетов и он включен в ядро, в настоящее время. Смотри список поддерживаемого оборудования [здесь](http://www.linuxwireless.org/en/users/Drivers/zd1211rw/devices). Только вам необходимо сначала установить файлы прошивки:

 `pacman -S zd1211-firmware` 

### Тестирование установки

После загрузки вашего драйвера запустите

```
iwconfig

```

и посмотрите, появился ли интерфейс беспроводного соединения (wlanX)

## Смотрите также

*   [The Linux Wireless project](http://wireless.kernel.org/) — документация по беспроводной (IEEE-802.11) подсистеме Linux
*   [Aircrack-ng guide on installing drivers](http://aircrack-ng.org/doku.php?id=install_drivers) — установка драйверов для беспроводных сетевых интерфейсов