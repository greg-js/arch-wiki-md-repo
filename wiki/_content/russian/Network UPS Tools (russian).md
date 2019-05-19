**Состояние перевода:** На этой странице представлен перевод статьи [Network UPS Tools](/index.php/Network_UPS_Tools "Network UPS Tools"). Дата последней синхронизации: 15 мая 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Network_UPS_Tools&diff=0&oldid=573292).

Эта статья описывает установку [Network UPS Tools (NUT)](https://networkupstools.org/). Он совместим с тысячами моделей ИБП, полный список которых доступен в [списке совместимого оборудования](https://networkupstools.org/stable-hcl.html).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка](#Настройка)
    *   [2.1 Настройка драйвера](#Настройка_драйвера)
        *   [2.1.1 Ошибка "Can't claim USB device"](#Ошибка_"Can't_claim_USB_device")
    *   [2.2 Настройка upsd](#Настройка_upsd)
    *   [2.3 Настройка upsmon](#Настройка_upsmon)
*   [3 NUT-Monitor](#NUT-Monitor)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [network-ups-tools](https://aur.archlinux.org/packages/network-ups-tools/).

## Настройка

У NUT есть 3 связанных с ним демона:

*   Драйвер, который связывается с ИБП.
*   Сервер (upsd), который использует драйвер для сообщений о состоянии ИБП.
*   Демон мониторинга (upsmon), который контролирует сервер upsd и выполняет действия на основе полученной информации.

Идея состоит в том, что если существует несколько систем, подключенных к ИБП, одна может сообщать о состоянии ИБП по сети, а другие могут отслеживать это состояние, запуская свои собственные действия upsmon. У NUT есть [обширная документация по конфигурации](https://networkupstools.org/docs/user-manual.chunked/ar01s06.html#_configuring_and_using), здесь же будет рассказано о простой настройке USB-ИБП, а также соответствующего сервера и монитора в одной системе (обычная конфигурация рабочего места).

### Настройка драйвера

Конфигурация зависит от типа используемого ИБП. Обратитесь к ранее упомянутому списку совместимого оборудования (Hardware Compatibility List), чтобы узнать, какой драйвер, скорее всего, будет работать с вашим ИБП. Также можно запустить утилиту [nut-scanner(8)](https://networkupstools.org/docs/man/nut-scanner.html) для обнаружения подключённых устройств, совместимых с NUT.

Для многих ИБП, подключенных по USB, используется драйвер [usbhid-ups(8)](https://networkupstools.org/docs/man/usbhid-ups.html). Для ИБП с последовательным портом используйте `port=/dev/ttySX`, где X — номер последовательного порта (например: /dev/ttyS1). Для ИБП с USB-портом используйте `port=auto`.

 `/etc/ups/ups.conf` 
```
...
[*upsname*]
    driver = usbhid-ups
    port = auto

```

Назвать ИБП можно любым удобным именем. [ups.conf(5)](https://networkupstools.org/docs/man/ups.conf.html)

Запустите драйвер от root-пользователя с помощью команды `upsdrvctl start`. Если ошибок нет, вы увидете подобное сообщение при использовании драйвера `usbhid-ups`:

```
Network UPS Tools - Generic HID driver 0.34 (2.4.1)
USB communication driver 0.31
Using subdriver: MGE HID 1.12
Detected EATON - Ellipse MAX 1100 [ADKK22008]

```

Если же драйвер запускается с ошибками, убедитесь, что выбран правильный вариант для вашего оборудования. Возможно, вам придется попробовать другие драйверы, изменив значение "driver=" в ups.conf.

#### Ошибка "Can't claim USB device"

Если вы получаете сообщение об ошибке, подобное этому:

```
Can't claim USB device [XXXX:YYYY]: could not detach kernel driver from
interface 0: Operation not permitted
Driver failed to start (exit status=1)
```

Или менее конкретное:

```
USB communication driver 0.33
No matching HID UPS found
Driver failed to start (exit status=1)
```

Скорее всего, это проблема с разрешениями доступа к устройству. Её можно исправить, указав udev-правило для установки корректной группы:

 `/etc/udev/rules.d/50-ups.rules` 
```
SUBSYSTEM=="usb", ATTR{idVendor}=="XXXX", ATTR{idProduct}=="YYYY", SYMLINK+="ups0", GROUP="nut"

```

Где `idVendor` и `idProduct` — производитель устройства и идентификатор продукта. Данную информацию можно найти в выводе ошибки `[XXXX:YYYY]` или с помощью `lsusb`.

**Примечание:** *SYMLINK* — необязательное правило для добавление символической ссылки на устройство для удобства (в данном случае оно отобразиться как `/dev/ups0` при подключении).

**Примечание:** Группа *nut* добавляется пакетом NUT из AUR. При использовании другого метода установки (или, возможно, изменении пакета) может потребоваться исправить группу. Также можно сделать устройство доступным для всех пользователей `MODE="0666"`.

После этого обновите и перезагрузите правила udev, выполнив следующую команду:

 `# udevadm control --reload-rules && udevadm trigger` 

### Настройка upsd

По умолчанию upsd слушает только localhost, что отлично подходит для наших целей. Хотя это необязательно, также можно настроить upsd под свои задачи, отредактировав файл `/etc/ups/upsd.conf`. Смотрите [upsd.conf(5)](https://networkupstools.org/docs/man/upsd.conf.html) для получения более подробной информации.

Для этого требуется добавить пользователя, чтобы монитор мог подключаться к серверу и выполнять команды. См. [upsd.users(5)](https://networkupstools.org/docs/man/upsd.users.html) для получения более подробной информации.

 `/etc/ups/upsd.users` 
```
...
[*upsuser*]
     password = *password*
     upsmon master
     actions = SET
     instcmds = ALL

```

На этом этапе должна быть возможность [запустить](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D1%8C "Запустить") и [включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D1%8C "Включить") службу `nut-server.service`, которая автоматически запустит nut-driver.

При успешном запуске можно выполнить команду `upsc <upsname>` для получения информации от ИБП. Пример вывода:

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

### Настройка upsmon

Последний шаг — настроить upsmon для прослушивания upsd и выполнения действий при наступлении определённых событий.

Добавьте следующую строку в файл `/etc/ups/upsmon.conf`:

```
MONITOR *upsname*@localhost 1 *upsduser* *password* master

```

*upsname* — это имя ИБП, а *upsduser* и *password* — пользователь и его пароль, который вы установили в `/etc/ups/upsd.user`.

Также можно настроить, какие оповещения отправляются и куда, какие действия предпринимаются при разряженном аккумуляторе и многое другое. Смотрите [upsmon.conf(5)](https://networkupstools.org/docs/man/upsmon.conf.html) для получения более подробной информации.

Затем [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `nut-monitor.service`.

В логах должен отобразиться запуск upsmon и мониторинг ИБП.

## NUT-Monitor

[NUT-Monitor](https://networkupstools.org/projects.html#_a_href_http_www_lestat_st_en_informatique_projets_nut_monitor_nut_monitor_a) — графический пользовательский интерфейс для мониторинга и управления устройствами, подключенными к серверу Network UPS Tools.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") nut-monitor с помощью пакета [nut-monitor](https://aur.archlinux.org/packages/nut-monitor/).