Этот документ описывает, как установить [Network UPS Tools (NUT)](http://networkupstools.org/). Network UPS Tools совместим с тысячами моделей ИБП. Можно проверить [Список совместимого оборудования](http://networkupstools.org/stable-hcl.html) чтобы увидеть, поддерживается ли ваш ИБП.

## Contents

*   [1 Установка Network UPS Tools](#Установка_Network_UPS_Tools)
*   [2 Конфигурация](#Конфигурация)
    *   [2.1 Конфигурация драйвера](#Конфигурация_драйвера)
        *   [2.1.1 Возможные проблемы](#Возможные_проблемы)
    *   [2.2 upsd конфигурация](#upsd_конфигурация)
    *   [2.3 upsmon конфигурация](#upsmon_конфигурация)
*   [3 NUT-Monitor](#NUT-Monitor)

## Установка Network UPS Tools

Вы можете [установить](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") network-ups-tools с помощью пакета [network-ups-tools](https://aur.archlinux.org/packages/network-ups-tools/).

## Конфигурация

NUT имеет 3 демона, связанных с ним:

*   Драйвер, который связывается с ИБП.
*   Сервер (upsd), который использует драйвер для сообщений о состоянии ИБП.
*   Демон мониторинга (upsmon), который контролирует сервер upsd и выполняет действия на основе полученной информации.

Идея состоит в том, что если у вас есть несколько систем, подключенных к ИБП, одна может сообщать о состоянии ИБП по сети, а другие могут отслеживать это состояние, запуская свои собственные действия upsmon. NUT имеет [обширную документацию по конфигурации](http://networkupstools.org/docs/user-manual.chunked/ar01s06.html#_configuring_and_using), здесь будет рассказано о простой настройке ИБП USB, а также соответствующего сервера и монитора, все в одной системе (обычная конфигурация рабочего стола).

### Конфигурация драйвера

Конфигурация здесь будет зависеть от типа вашего ИБП. Обратитесь к ранее упомянутому списку совместимости оборудования, чтобы узнать, какой драйвер, скорее всего, будет работать с вашим ИБП. Вы можете выполнить [nut-scanner(8)](http://networkupstools.org/docs/man/nut-scanner.html) который обнаружит NUT-совместимые устройства, подключенные к вашей системе.

Для многих ИБП, подключенных через USB, используйте драйвер [usbhid-ups(8)](http://networkupstools.org/docs/man/usbhid-ups.html). Для ИБП с последовательным портом используйте `port=/dev/ttySX`, где X - номер последовательного порта (Example:/dev/ttyS1). Для ИБП с портом USB используйте `port=auto`.

 `/etc/ups/ups.conf` 
```
...
[*upsname*]
    driver = usbhid-ups
    port = auto

```

Вы можете назвать устройство ИБП как угодно. [ups.conf(5)](http://networkupstools.org/docs/man/ups.conf.html)

Запустите драйвер от имени пользователя root с помощью `upsdrvctl start`. Если ошибок нет, вы должны увидеть подобное сообщение драйвера `usbhid-ups`:

```
Network UPS Tools - Generic HID driver 0.34 (2.4.1)
USB communication driver 0.31
Using subdriver: MGE HID 1.12
Detected EATON - Ellipse MAX 1100 [ADKK22008]

```

Если драйвер запускается неправильно, убедитесь, что вы выбрали правильный вариант для своего оборудования. Возможно, вам придется попробовать другие драйверы, изменив значение "driver=" value in ups.conf.

#### Возможные проблемы

Если вы получаете сообщение об ошибке, подобное этому:

```
Can't claim USB device [XXXX:YYYY]: could not detach kernel driver from
interface 0: Operation not permitted
Driver failed to start (exit status=1)
```

Или менее конкретный:

```
USB communication driver 0.33
No matching HID UPS found
Driver failed to start (exit status=1)
```

Скорее всего, это проблема с разрешениями и доступом к устройству. Вы можете исправить это, указав правило udev, которое устанавливает правильную группу:

 `/etc/udev/rules.d/50-ups.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="XXXX", ATTR{idProduct}=="YYYY", SYMLINK+="ups0", GROUP="nut"

```

Где `idVendor` и `idProduct` - производитель устройства и идентификатор продукта. Вы можете увидеть это либо в выводе ошибки`[XXXX:YYYY]` или с помощью `lsusb`.

**Примечание:** *SYMLINK* SYMLINK - это необязательное правило, добавление символической ссылки на устройство для удобства (в этом случае оно будет отображаться `/dev/ups0` при подключении).

**Примечание:** Группа *nut* добавляется пакетом NUT AUR. Если вы использовали другой метод установки (или, возможно, пакет был изменен), вам может потребоваться исправить группу. В качестве альтернативы вы также можете установить устройство, доступное любому `MODE="0666"`.

После этого перезагрузите и повторите правила udev, выполнив следующую команду:

 `# udevadm control --reload-rules && udevadm trigger` 

### upsd конфигурация

По умолчанию upsd слушает только localhost. Хотя это не обязательно, вы можете настроить upsd под свои задачи, отредактировав `/etc/ups/upsd.conf`. Просмотреть [upsd.conf(5)](http://networkupstools.org/docs/man/upsd.conf.html).

Вам нужно будет добавить пользователя для монитора, чтобы подключаться к серверу и выдавать команды. Просмотреть [upsd.users(5)](http://networkupstools.org/docs/man/upsd.users.html).

 `/etc/ups/upsd.users` 
```
...
[*upsuser*]
     password = *password*
     upsmon master
     actions = SET
     instcmds = ALL

```

На этом этапе у Вас должна быть возможность выполнить [start/enable](/index.php/Start/enable "Start/enable") `nut-server.service` который автоматически запустит nut-driver.

Если действия выполняться успешно, вы можете запустить `upsc <upsname>` что бы получить информацию от ИБП. Пример вывода из командной строки:

```
battery.charge: 100
battery.charge.low: 10
battery.charge.warning: 20
battery.mfr.date: CPS
battery.runtime: 5550
battery.runtime.low: 300
battery.type: PbAcid
battery.voltage: 13.5
battery.voltage.nominal: 12
device.mfr: CPS
device.model: UPS CP1000AVRLCD
device.type: ups
driver.name: usbhid-ups
driver.parameter.pollfreq: 30
driver.parameter.pollinterval: 2
driver.parameter.port: auto
driver.parameter.synchronous: no
driver.version: 2.7.4
driver.version.data: CyberPower HID 0.4
driver.version.internal: 0.41
input.transfer.high: 140
input.transfer.low: 90
input.voltage: 122.0
input.voltage.nominal: 120
output.voltage: 122.0
ups.beeper.status: disabled
ups.delay.shutdown: 20
ups.delay.start: 30
ups.load: 0
ups.mfr: CPS
ups.model: UPS CP1000AVRLCD
ups.productid: 0501
ups.realpower.nominal: 600
ups.status: OL
ups.test.result: Done and passed
ups.timer.shutdown: -60
ups.timer.start: 0
ups.vendorid: 0764

```

### upsmon конфигурация

Последний шаг - настроить upsmon для прослушивания upsd и выполнения действий при наступлении событий.

Добавьте следующую строку в `/etc/ups/upsmon.conf`:

```
MONITOR *upsname*@localhost 1 *upsduser* *password* master

```

Здесь *upsname* это имя ИБП, а *upsduser* и *password* - это пользователь и его пароль, который вы установили в `/etc/ups/upsd.user`.

Вы также можете настроить, какие оповещения отправляются, куда они отправляются, какие действия предпринимаются, когда батарея разряжена, и многое другое. Увидеть [upsmon.conf(5)](http://networkupstools.org/docs/man/upsmon.conf.html).

Затем [start/enable](/index.php/Start/enable "Start/enable") `nut-monitor.service`.

Ваш logs должн показывать upsmon запуск и мониторинг ИБП.

## NUT-Monitor

[NUT-Monitor](http://networkupstools.org/projects.html#_a_href_http_www_lestat_st_en_informatique_projets_nut_monitor_nut_monitor_a) графический пользовательский интерфейс для мониторинга и управления устройствами, подключенными к серверу Network UPS Tools.

Вы можете [устанавить](/index.php?title=%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%B0%D0%B2%D0%B8%D1%82%D1%8C&action=edit&redlink=1 "Устанавить (page does not exist)") nut-monitor с пакетом [nut-monitor](https://aur.archlinux.org/packages/nut-monitor/).

NUT-Monitor требует [pygtk](https://www.archlinux.org/packages/?name=pygtk) от [Python](/index.php/Python "Python").