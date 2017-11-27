Ссылки по теме

*   [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Network bridge](/index.php/Network_bridge "Network bridge")
*   [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети")
*   [Настройка беспроводной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети")

**Состояние перевода:** На этой странице представлен перевод статьи [Systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"). Дата последней синхронизации: 28 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd-networkd&diff=0&oldid=423358).

*systemd-networkd* - это системный демон, который управляет сетевыми настройками. По мере появления он обнаруживает и настраивает сетевые устройства, также может создавать виртуальные сетевые устройства. Эта служба может быть особенно полезной для установки сложных сетевых настроек, для контейнера управляемым [Systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") или для виртуальных машин. А также отлично работает на простом соединении.

## Contents

*   [1 Основы использования](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D1.8B_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [1.1 Обязательные службы и установки](#.D0.9E.D0.B1.D1.8F.D0.B7.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D1.8B_.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [1.2 Примеры настроек](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
        *   [1.2.1 Проводной адаптер с DHCP](#.D0.9F.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80_.D1.81_DHCP)
        *   [1.2.2 Проводной адаптер использующий статический IP](#.D0.9F.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8E.D1.89.D0.B8.D0.B9_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_IP)
        *   [1.2.3 Беспроводной адаптер](#.D0.91.D0.B5.D1.81.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80)
        *   [1.2.4 Проводные и беспроводные адаптеры на одной машине](#.D0.9F.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D1.8B.D0.B5_.D0.B8_.D0.B1.D0.B5.D1.81.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D1.8B.D0.B5_.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80.D1.8B_.D0.BD.D0.B0_.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.BC.D0.B0.D1.88.D0.B8.D0.BD.D0.B5)
        *   [1.2.5 IPv6 расширения конфиденциальности](#IPv6_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B4.D0.B5.D0.BD.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
*   [2 Файлы настроек](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
    *   [2.1 Файлы network](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_network)
        *   [2.1.1 [Match] раздел](#.5BMatch.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB)
        *   [2.1.2 [Network] раздел](#.5BNetwork.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB)
        *   [2.1.3 [Address] раздел](#.5BAddress.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB)
        *   [2.1.4 [Route] раздел](#.5BRoute.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB)
    *   [2.2 Файлы NetDev](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_NetDev)
        *   [2.2.1 [Match] раздел](#.5BMatch.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_2)
        *   [2.2.2 [Netdev] раздел](#.5BNetdev.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB)
    *   [2.3 Файлы link](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_link)
        *   [2.3.1 [Match] раздел](#.5BMatch.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB_3)
        *   [2.3.2 [Link] раздел](#.5BLink.5D_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB)
*   [3 Использование с контейнерами](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.B9.D0.BD.D0.B5.D1.80.D0.B0.D0.BC.D0.B8)
    *   [3.1 Основная DHCP сеть](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D0.B0.D1.8F_DHCP_.D1.81.D0.B5.D1.82.D1.8C)
    *   [3.2 DHCP с двумя различными IP](#DHCP_.D1.81_.D0.B4.D0.B2.D1.83.D0.BC.D1.8F_.D1.80.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D0.BC.D0.B8_IP)
        *   [3.2.1 Интерфейс моста](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81_.D0.BC.D0.BE.D1.81.D1.82.D0.B0)
        *   [3.2.2 Привязать Ethernet для моста](#.D0.9F.D1.80.D0.B8.D0.B2.D1.8F.D0.B7.D0.B0.D1.82.D1.8C_Ethernet_.D0.B4.D0.BB.D1.8F_.D0.BC.D0.BE.D1.81.D1.82.D0.B0)
        *   [3.2.3 Сетевой мост](#.D0.A1.D0.B5.D1.82.D0.B5.D0.B2.D0.BE.D0.B9_.D0.BC.D0.BE.D1.81.D1.82)
        *   [3.2.4 Добавить опцию для загрузки контейнера](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.B8.D1.82.D1.8C_.D0.BE.D0.BF.D1.86.D0.B8.D1.8E_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.B9.D0.BD.D0.B5.D1.80.D0.B0)
        *   [3.2.5 Результат](#.D0.A0.D0.B5.D0.B7.D1.83.D0.BB.D1.8C.D1.82.D0.B0.D1.82)
        *   [3.2.6 Уведомление](#.D0.A3.D0.B2.D0.B5.D0.B4.D0.BE.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [3.3 Статические IP-сети](#.D0.A1.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_IP-.D1.81.D0.B5.D1.82.D0.B8)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Основы использования

Пакет [systemd](https://www.archlinux.org/packages/?name=systemd) является частью установки Arch по умолчанию, и содержит все необходимые файлы для работы в проводной сети. Беспроводные адаптеры могут быть установлены другими службами, такими как [wpa_supplicant](/index.php/Wpa_supplicant "Wpa supplicant"), они будут рассмотрены далее в этой статье.

### Обязательные службы и установки

Чтобы использовать *systemd-networkd*, [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") следующие две службы и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") их работу при загрузке системы:

*   `systemd-networkd.service`
*   `systemd-resolved.service`

**Примечание:** *systemd-resolved* на самом деле требуется, только если вы указали записи DNS в файлах *.network* или если вы хотите получить адреса DNS от DHCP клиента networkd.

Для совместимости с [resolv.conf](/index.php/Resolv.conf "Resolv.conf"), удалите или переименуйте существующий файл и создайте следующую символическую ссылку:

```
# ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

Для того, чтобы использовать локальную DNS-заглушку распознающую *systemd-resolved* (и, следовательно, использовать LLMNR и DNS слияние каждого интерфейса), замените `dns` с `resolve` в `/etc/nsswitch.conf`:

```
hosts: files **resolve** myhostname

```

Смотрите [systemd-resolved(8)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8), [resolved.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5) и [Systemd README](https://github.com/systemd/systemd/blob/master/README#L205).

**Примечание:** Systemd's `resolve` не может найти локальный домен, когда дается только имя хоста, даже когда `UseDomains=yes` или `Domains=[domain-list]` присутствует в соответствующем файле `.network`, и что файл производит ожидаемый `search [domain-list]` в `resolv.conf`. Если вы столкнулись с этой проблемой:

*   Переключитесь на использование полного доменного имени
*   Используйте разрешения имен хостов `/etc/hosts`
*   Откатитесь назад, используя glibc's `dns` вместо systemd's `resolve`

### Примеры настроек

Все настройки этого раздела хранятся в `foo.network` в `/etc/systemd/network`. Для получения полного списка опций и порядка обработки, см. [#Файлы настроек](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA) и страницу man `systemd.network`.

Systemd/udev автоматически назначает предсказуемые, стабильные имена сетевого интерфейса для всех локальных Ethernet, WLAN, и WWAN интерфейсов. Воспользуйтесь `networkctl list`, - список устройств в системе.

После внесения изменений в файл настройки, перезагрузите демон networkd.

```
# systemctl restart systemd-networkd 

```

**Примечание:** В приведенных ниже примерах, **enp1s0** это проводной адаптер, а **wlp2s0** беспроводной адаптер. Эти имена могут быть другими в разных системах.

#### Проводной адаптер с DHCP

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

```

#### Проводной адаптер использующий статический IP

 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1

```

Для больших вариантов, таких как сети с указанием DNS-серверов и широковещательного адреса, смотрите страницу man `systemd.network(5)`.

#### Беспроводной адаптер

Для того, чтобы подключиться к беспроводной сети с *systemd-networkd*, беспроводной адаптер настраивается с другой службой, например потребуется [wpa_supplicant](/index.php/Wpa_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wpa supplicant (Русский)"). В этом примере, соответствующий файл службы Systemd, которая должна быть включена в `wpa_supplicant@wlp2s0.service`.

 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

Если беспроводной адаптер имеет статический IP-адрес, настройка является такой же (кроме имени интерфейса) как в [проводном адаптере](#.D0.9F.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B9_.D0.B0.D0.B4.D0.B0.D0.BF.D1.82.D0.B5.D1.80_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8E.D1.89.D0.B8.D0.B9_.D1.81.D1.82.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_IP).

#### Проводные и беспроводные адаптеры на одной машине

Такая настройка проводной и беспроводной связи DHCP IP (использующих **Metric** директивы) даст возможность ядру решать на лету, какой из них использовать. Таким образом, когда проводное соединение отключено, никакого обрыва соединения не будет.

Маршрут метрики ядра (также как настройка *ip*) решает, какой маршрут использовать для исходящих пакетов, в тех случаях, когда установлено несколько **Match**. Это происходит в том случае, когда оба устройства (проводное и беспроводное) в системе имеют активные соединения. Чтобы разорвать связь, ядро использует метрики. Если одно из соединений завершается, другое автоматически выигрывает без наличия разрывов (текущие трансферты могут до сих пор не справиться с этим хорошо, но это в другом слое OSI).

**Примечание:** Опция **Metric** для статических маршрутов, а опция **RouteMetric** для не использующих статические маршруты.
 `/etc/systemd/network/*wired*.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10

```
 `/etc/systemd/network/*wireless*.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20

```

#### IPv6 расширения конфиденциальности

**Примечание:** Broken on v228 [https://github.com/systemd/systemd/issues/2242](https://github.com/systemd/systemd/issues/2242)

## Файлы настроек

Файлы настроек расположены в `/usr/lib/systemd/network`, в динамическом каталоге выполнения сети `/run/systemd/network` и локальном каталоге сетевого администрирования `/etc/systemd/network`. Файлы в `/etc/systemd/network` имеют самый высокий приоритет.

Существуют три типа файлов настройки.

*   **.network** файлы. Они будут применять сетевую настройку для *matching* (совпадения) устройства
*   **.netdev** файлы. Они создадут *virtual network device* для среды *matching*
*   **.link** файлы. Когда появится сетевое устройство, [udev](/index.php/Udev "Udev") сначала посмотрит *matching* файла **.link**

Все они следуют тем же правилам:

*   Если **все** условия в `[Match]` разделе совпали, профиль будет активирован
*   Пустая секция `[Match]` означает, что профиль будет применяться в любом случае (можно сравнить с шуткой `*`)
*   Каждая запись с синтаксисом `NAME=VALUE` является ключевой
*   все файлы настроек вместе сортируются и обрабатываются в лексическом порядке, независимо от каталога, в котором они живут
*   файлы с одинаковым именем сменяют друг друга

**Совет:**

*   переопределить системный файл `/usr/lib/systemd/network` на постоянную основу (то есть даже после обновления) можно поместив файл с таким же именем в каталог `/etc/systemd/network` и создав для него символьную ссылку в `/dev/null`
*   символ `*` можно использовать в `VALUE` (например, значению `en*` будет соответствовать любое устройство Ethernet)
*   в соответствии с информацией, данной в [этом сообщении Arch-general](https://mailman.archlinux.org/pipermail/arch-general/2014-March/035381.html), лучше всего выставлять параметры для конкретных сетевых контейнеров *внутри контейнера* при помощи файлов **networkd**

### Файлы network

Эти файлы направлены на установку переменных сетевых настроек, в основном для серверов и контейнеров.

Ниже приводится основная структура файла `*МойПрофиль*.network`:

 `/etc/systemd/network/*МойПрофиль*.network` 
```
[Match]
*вертикальный список ключей*

[Network]
*вертикальный список ключей*

[Address]
*вертикальный список ключей*

[Route]
*вертикальный список ключей*

```

#### [Match] раздел

Наиболее распространенные ключи:

*   `Name=` имя устройства (например Br0, enp4s0, en*)
*   `Host=` имя хоста машины
*   `Virtualization=` проверить, является ли система выполненной в виртуализированной среде или нет. `Virtualization=no` ключ будет применяться только на вашей машине, в то время как `Virtualization=yes` применяются к любому контейнеру или VM.

#### [Network] раздел

Наиболее распространенные ключи:

*   `DHCP=` включает поддержку [DHCPv4](https://en.wikipedia.org/wiki/ru:DHCP "wikipedia:ru:DHCP") и/или DHCPv6\. Принимает: `yes`, `no`, `ipv4` или `ipv6`
*   `DNS=` является [DNS](https://en.wikipedia.org/wiki/ru:DNS "wikipedia:ru:DNS") адрес сервера. Вы можете указать этот параметр более одного раза
*   `Bridge=` это имя моста, чтобы добавить ссылку на
*   `IPForward=` по умолчанию `no`. Это разрешает IP forwarding, выполняя пересылку в соответствии с таблицей маршрутизации и необходим для настройк [Internet sharing](/index.php/Internet_sharing "Internet sharing"). Заметим, что включение `IPForward=` относится ко *всем* сетевым интерфейсам.
*   `Domains=` список доменов, используемых для разрешения имен DNS хоста.

Для подробностей, смотрите `systemd.network(5)`.

#### [Address] раздел

Большинство общих ключ в разделе `[Address]`:

*   `Address=` статический **IPv4** или **IPv6** адрес и его длина префикса, разделенных символом `/` (например `192.168.1.90/24`). Эта опция **обязательна**, если не используется DHCP

#### [Route] раздел

Большинство общих ключ в разделе `[Route]`:

*   `Gateway=` это адрес шлюза вашей машины. Эта опция **обязательна** если не используется DHCP.

Обратитесь к `systemd.network(5)` для исчерпывающего списка ключей.

**Совет:** you can put the `Address=` and `Gateway=` keys in the `[Network]` section as a short-hand if `Address=` contains only an Address key and `Gateway=` section contains only a Gateway key

### Файлы NetDev

Эти файлы будут создавать виртуальные сетевые устройства.

Ниже приводится основная структура файла*Mydevice*.netdev:

 `/etc/systemd/network/*MyDevice*.netdev` 
```
[Match]
*вертикальный список ключей*

[NetDev]
*вертикальный список ключей*

```

#### [Match] раздел

Большинство общих ключ в `Host=` и `Virtualization=`

#### [Netdev] раздел

Наиболее распространенные ключи:

*   `Name=` это имя интерфейса, используемое при создании netdev. Эта опция **обязательна**
*   `Kind=` это вид netdev. Например, поддерживаются: *bridge*, *bond*, *vlan*, *veth*, *sit*, и т.д. Эта опция **обязательна**

Чтобы увидеть исчерпывающий перечень ключей, обратитесь к странице справочного руководства `systemd.netdev(5)`

### Файлы link

Эти файлы являются альтернативой пользовательским правилам [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") и будут применяться при как появлении устройства.

Ниже приводится основная структура файла *МоеУстройство*.link:

 `/etc/systemd/network/*МоеУстройство*.link` 
```
[Match]
*вертикальный список ключей*

[Link]
*вертикальный список ключей*

```

Раздел `[Match]` будет определять, если данный связующий файл может быть применён к данному устройству, когда раздел `[Link]` определяет настройку устройства.

#### [Match] раздел

Наиболее распространенные ключи `MACAddress=`, `Host=` и `Virtualization=`.

`Type=` тип устройства (например vlan)

#### [Link] раздел

Наиболее распространенные ключи:

`MACAddressPolicy=` либо *persistent* когда оборудование имеет постоянный MAC-адрес (должно быть на большинстве аппаратных) или *random*, который даёт случайный MAC-адрес устройства.

`MACAddress=` должен использоваться, когда не указан `MACAddressPolicy=`

**Примечание:** Системе, как правило, `/usr/lib/systemd/network/99-default.link` достаточно для большинства случаев.

## Использование с контейнерами

Служба доступна с [systemd](https://www.archlinux.org/packages/?name=systemd) >= 210\. Хотите сипользовать [#Основы использования systemctl|включение и запуск](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") `systemd-networkd.service` на хосте и контейнере.

Для отладки, настоятельно рекомендуется [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") пакеты [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [net-tools](https://www.archlinux.org/packages/?name=net-tools) и [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Если вы используете *systemd-nspawn*, вам, возможно, потребуется изменить `systemd-nspawn@.service` и добавить параметры загрузки в строку `ExecStart`. Для исчерпывающего списка варианттов, обратитесь к [systemd-nspawn(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1). Обратите внимание, если вы хотите, использовать автоматическую настройку DNS от DHCP, то Вам необходимо включить `systemd-resolved` и символьную ссылку `/run/systemd/resolve/resolv.conf` на `/etc/resolv.conf`. Для большей информации, смотрите `systemd-resolved.service(8)`.

Before you start to configure your container network, it is useful to:

*   disable all your [netctl](/index.php/Netctl "Netctl") services. This will avoid any potential conflicts with `systemd-networkd` and make all your configurations easier to test. Furthermore, odds are high you will end with few or even no [netctl](/index.php/Netctl "Netctl") activated profiles. The `netctl list` command will output a list of all your profiles, with the activated one being starred.
*   disable the `systemd-nspawn@.service` and use the `systemd-nspawn -bnD /path_to/your_container/` command as root to boot the container. To log off and shutdown inside the container `systemctl poweroff` is used as root. Once the network setting meets your requirements, [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-nspawn@.service`
*   disable the `dhcpcd.service` if enabled on your system, since it activates *dhcpcd* on **all** interfaces
*   make sure you have no [netctl](/index.php/Netctl "Netctl") profiles activated in the container, and ensure that `systemd-networkd.service` is neither enabled nor started
*   make sure you do not have any [iptables](/index.php/Iptables "Iptables") rules which can block traffic
*   * make sure *packet forwarding* is [enabled](/index.php/Internet_sharing#Enable_packet_forwarding "Internet sharing") if you want to let containers access the internet. Make sure that your `.network` file does not accidentally turn off forwarding because if you do not have a `IPForward=1` setting in it, `systemd-networkd` will turn off forwarding on this interface, even if you have it enabled globally.
*   when the daemon is started the systemd `networkctl` command displays the status of network interfaces.

}}

For the set-up described below,

*   we will limit the output of the `ip a` command to the concerned interfaces
*   we assume the *host* is your main OS you are booting to and the *container* is your guest virtual machine
*   all interface names and IP addresses are only examples

}}

### Основная DHCP сеть

Такая настройка включит DHCP IP для хоста и контейнера. В этом случае, обе системы будут иметь одинаковый IP, поскольку они разделяют одни и те же интерфейсы.

 `/etc/systemd/network/*MyDhcp*.network` 
```
[Match]
Name=en*

[Network]
DHCP=ipv4

```

Когда, [включен](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D1.8E.D0.BD.D0.B8.D1.82_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B "Systemd (Русский)") и запущен `systemd-networkd.service` в вашем контейнере.

Вы, конечно, можете заменить `en*` на полное имя вашего сетевого устройства, получив его на выходе команды `ip link`.

*   на хосте и контейнере:

 `$ ip a` 
```
2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.72/24 brd 192.168.1.255 scope global enp7s0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever

```

По умолчанию имя хоста, полученное от DHCP-сервера будет использоваться в качестве переходного хоста.

Чтобы изменить его добавьте `UseHostname=false` в раздел `[DHCPv4]`

 `/etc/systemd/network/*MyDhcp*.network` 
```
[DHCPv4]
UseHostname=false

```

Если вы не хотите настраивать DNS в `/etc/resolv.conf` и хотите полагаться на DHCP для его настройки, вам нужно [включить](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B8.D1.82.D1.8C_.D1.8E.D0.BD.D0.B8.D1.82_.D0.B2_.D0.B0.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B5_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B "Systemd (Русский)") `systemd-resolved.service` и сделать символическую ссылку `/run/systemd/resolve/resolv.conf` на `/etc/resolv.conf`

```
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

Для подробной информации смотрите `systemd-resolved.service(8)`.

### DHCP с двумя различными IP

#### Интерфейс моста

Создайте интерфейс виртуального мост

 `/etc/systemd/network/*MyBridge*.netdev` 
```
[NetDev]
Name=br0
Kind=bridge

```

На хосте и контейнере:

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default 
    link/ether ae:bd:35:ea:0c:c9 brd ff:ff:ff:ff:ff:ff

```

Обратите внимание что интерфейс br0 в списке, но не работает (DOWN).

#### Привязать Ethernet для моста

Измените `/etc/systemd/network/*MyDhcp*.network`, чтобы удалить DHCP, мосту необходим интерфейс для привязки не с IP, а также добавьте ключ, чтобы связать это устройство для BR0, давайте изменим свое название на одно более актуальное.

 `/etc/systemd/network/*MyEth*.network` 
```
[Match]
Name=en*

[Network]
Bridge=br0

```

#### Сетевой мост

Создание сетевого профиля для моста

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DHCP=ipv4

```

#### Добавить опцию для загрузки контейнера

Поскольку мы хотим, дать выделенный IP для хоста и контейнера, мы должны *Отключить* сеть контейнера от хоста. Чтобы сделать это, добавьте опцию `--network-bridge=br0` в вашу команду загрузки контейнера.

```
# systemd-nspawn --network-bridge=br0 -bD /path_to/my_container

```

#### Результат

*   на хосте

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.87/24 brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever
6: vb-*MyContainer*: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP group default qlen 1000
    link/ether d2:7c:97:97:37:25 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::d07c:97ff:fe97:3725/64 scope link 
       valid_lft forever preferred_lft forever

```

*   на контейнере

 `$ ip a` 
```
2: host0: <BROADCAST,MULTICAST,ALLMULTI,AUTOMEDIA,NOTRAILERS,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 5e:96:85:83:a8:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.73/24 brd 192.168.1.255 scope global host0
       valid_lft forever preferred_lft forever
    inet6 fe80::5c96:85ff:fe83:a85d/64 scope link 
       valid_lft forever preferred_lft forever

```

#### Уведомление

*   we have now one IP address for Br0 on the host, and one for host0 in the container
*   two new interfaces have appeared: `vb-*MyContainer*` in the host and `host0` in the container. This comes as a result of the `--network-bridge=br0` option. This option *implies* another option, `--network-veth`. This means a *virtual Ethernet link* has been created between host and container.
*   the DHCP address on `host0` comes from the system `/usr/lib/systemd/network/80-container-host0.network` file.
*   на хосте

 `$ brctl show` 
```
bridge name	bridge id		STP enabled	interfaces
br0		8000.14dae9b57a88	no		enp7s0
							vb-*MyContainer*

```

Приведенный выше вывод команды подтверждает, что мы имеем мост с двумя переплетёнными/связанными интерфейсами.

*   на хосте

 `$ ip route` 
```
default via 192.168.1.254 dev br0 
192.168.1.0/24 dev br0  proto kernel  scope link  src 192.168.1.87

```

*   на контейнере

 `$ ip route` 
```
default via 192.168.1.254 dev host0 
192.168.1.0/24 dev host0  proto kernel  scope link  src 192.168.1.73

```

the above command outputs confirm we have activated `br0` and `host0` interfaces with an IP address and Gateway 192.168.1.254\. The gateway address has been automatically grabbed by *systemd-networkd*

 `$ cat /run/systemd/resolve/resolv.conf` 
```
nameserver 192.168.1.254

```

### Статические IP-сети

Установка статического IP для каждого устройства может быть полезна в случае развертывания веб-служб (например, FTP, HTTP, SSH). Each device will keep the same MAC address across reboots if your system `/usr/lib/systemd/network/99-default.link` file has the `MACAddressPolicy=persistent` option (it has by default). Thus, you will easily route any service on your Gateway to the desired device. First, we shall get rid of the system `/usr/lib/systemd/network/80-container-host0.network` file. To do it in a permanent way (e.g even after upgrades), do the following on container. This will mask the file `/usr/lib/systemd/network/80-container-host0.network` since files of the same name in `/etc/systemd/network` take priority over `/usr/lib/systemd/network`.

```
# ln -sf /dev/null /etc/systemd/network/80-container-host0.network

```

Then, [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-networkd` on your container.

The needed configuration files:

*   на хосте

```
/etc/systemd/network/*MyBridge*.netdev
/etc/systemd/network/*MyEth*.network

```

Измените *MyBridge*.network

 `/etc/systemd/network/*MyBridge*.network` 
```
[Match]
Name=br0

[Network]
DNS=192.168.1.254
Address=192.168.1.87/24
Gateway=192.168.1.254

```

*   на контейнере

 `/etc/systemd/network/*MyVeth*.network` 
```
[Match]
Name=host0

[Network]
DNS=192.168.1.254
Address=192.168.1.94/24
Gateway=192.168.1.254

```

## Смотрите также

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)