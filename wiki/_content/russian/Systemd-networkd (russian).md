Ссылки по теме

*   [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)")
*   [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Network bridge](/index.php/Network_bridge "Network bridge")
*   [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети")
*   [Настройка беспроводной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети")
*   [Category:Network configuration (Русский)](/index.php/Category:Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Network configuration (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"). Дата последней синхронизации: 28 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd-networkd&diff=0&oldid=423358).

*systemd-networkd* — системный демон для управления сетевыми настройками. Его задачей является обнаружение и настройка сетевых устройств по мере их появления, а также создание виртуальных сетевых устройств. Эта служба особенно полезна при работе со сложными сетевыми настройками контейнера [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn") или виртуальной машины, но вполне подойдёт и для простых соединений.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Основы использования](#Основы_использования)
    *   [1.1 Обязательные службы и установки](#Обязательные_службы_и_установки)
    *   [1.2 Примеры настроек](#Примеры_настроек)
        *   [1.2.1 Проводной интерфейс с DHCP](#Проводной_интерфейс_с_DHCP)
        *   [1.2.2 Проводной интерфейс со статическим IP-адресом](#Проводной_интерфейс_со_статическим_IP-адресом)
        *   [1.2.3 Беспроводной интерфейс](#Беспроводной_интерфейс)
        *   [1.2.4 Проводные и беспроводные интерфейсы на одной машине](#Проводные_и_беспроводные_интерфейсы_на_одной_машине)
        *   [1.2.5 Переименование интерфейса](#Переименование_интерфейса)
*   [2 Файлы настроек](#Файлы_настроек)
    *   [2.1 Файлы network](#Файлы_network)
        *   [2.1.1 [Match] раздел](#[Match]_раздел)
        *   [2.1.2 [Network] раздел](#[Network]_раздел)
        *   [2.1.3 [Address] раздел](#[Address]_раздел)
        *   [2.1.4 [Route] раздел](#[Route]_раздел)
    *   [2.2 Файлы NetDev](#Файлы_NetDev)
        *   [2.2.1 [Match] раздел](#[Match]_раздел_2)
        *   [2.2.2 [Netdev] раздел](#[Netdev]_раздел)
    *   [2.3 Файлы link](#Файлы_link)
        *   [2.3.1 [Match] раздел](#[Match]_раздел_3)
        *   [2.3.2 [Link] раздел](#[Link]_раздел)
*   [3 Использование с контейнерами](#Использование_с_контейнерами)
    *   [3.1 Основная DHCP сеть](#Основная_DHCP_сеть)
    *   [3.2 DHCP с двумя различными IP](#DHCP_с_двумя_различными_IP)
        *   [3.2.1 Интерфейс моста](#Интерфейс_моста)
        *   [3.2.2 Привязать Ethernet для моста](#Привязать_Ethernet_для_моста)
        *   [3.2.3 Сетевой мост](#Сетевой_мост)
        *   [3.2.4 Добавить опцию для загрузки контейнера](#Добавить_опцию_для_загрузки_контейнера)
        *   [3.2.5 Результат](#Результат)
        *   [3.2.6 Уведомление](#Уведомление)
    *   [3.3 Статические IP-сети](#Статические_IP-сети)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 Интеграция сетевого интерфейса и рабочего стола](#Интеграция_сетевого_интерфейса_и_рабочего_стола)
    *   [4.2 Назначение IP-адреса на основании SSID](#Назначение_IP-адреса_на_основании_SSID)
*   [5 Решение проблем](#Решение_проблем)
*   [6 Смотрите также](#Смотрите_также)

## Основы использования

Пакет [systemd](https://www.archlinux.org/packages/?name=systemd) входит в базовую установку Arch. В нём содержится всё необходимое для работы с проводной сетью. Беспроводные сетевые интерфейсы настраиваются специализированными утилитами вроде [WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA supplicant (Русский)") или [iwd](/index.php/Iwd "Iwd").

### Обязательные службы и установки

Чтобы включить *systemd-networkd*, [запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `systemd-networkd.service`.

При необходимости также [запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `systemd-resolved.service`, которую приложения будут использовать для выполнения разрешения имён. Имейте в виду, что:

*   Cлужба [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") необходима, если в *.network*-файлах заданы параметры `DNS`.
*   C помощью этой службы можно также автоматически получать DNS-адреса от сетевого клиента DHCP.
*   Для правильной настройки DNS необходимо понимать, как взаимодействуют [resolve.conf](/index.php/Domain_name_resolution "Domain name resolution") и systemd-resolved; некоторые пояснения можно найти в статье [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved").
*   Также учтите, что systemd-resolved можно использовать без systemd-networkd.

### Примеры настроек

Настройки должны храниться в каталоге `/etc/systemd/network` в файлах с суффиксом *.network*. Подробнее смотрите [#Файлы настроек](#Файлы_настроек) и [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).

Systemd/udev автоматически назначает [постоянные](https://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames/) имена для обнаруженных Ethernet, WLAN и WWAN интерфейсов. Перечень интерфейсов можно увидеть командой `networkctl list`.

Чтобы изменения настроек вступили в силу необходимо будет [перезапустить](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") демон `systemd-networkd.service`.

**Примечание:**

*   Параметры в файлах настроек чувствительны к регистру.
*   В примерах ниже `enp1s0` — проводной интерфейс, а `wlp2s0` — беспроводной. Названия интерфейсов на вашей системе могут отличаться. Кроме того, могут использоваться подстановочные символы, например `Name=en*`.
*   Если вы хотите отключить IPv6, то изучите статью [IPv6#systemd-networkd](/index.php/IPv6_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#systemd-networkd_3 "IPv6 (Русский)").
*   Чтобы разрешить одновременно IPv4 **и** IPv6 DHCP-запросы, в разделе настроек `[Network]` нужно задать параметр `DHCP=yes`.

#### Проводной интерфейс с DHCP

 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

```

#### Проводной интерфейс со статическим IP-адресом

 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1
DNS=10.1.10.1
#DNS=8.8.8.8

```

Параметр `Address=` можно указать несколько раз, если необходимо настроить несколько IPv4 и IPv6 адресов. Подробнее смотрите [#Файлы network](#Файлы_network) и [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).

#### Беспроводной интерфейс

Беспроводной сетевой интерфейс нужно предварительно настроить приложением вроде [WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA supplicant (Русский)") или [iwd](/index.php/Iwd "Iwd"). После этого можно подключиться к беспроводной сети посредством systemd-networkd:

 `/etc/systemd/network/25-wireless.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

Если беспроводному интерфейсу назначен статический IP-адрес, то настройка полностью (за исключением названия интерфейса) совпадает с настройкой [проводного интерфейса](#Проводной_интерфейс_со_статическим_IP-адресом).

#### Проводные и беспроводные интерфейсы на одной машине

Когда в системе есть и проводной, и беспроводной интерфейсы, настройте директиву ядра metric, чтобы оно могло "на лету" определять, какой из интерфейсов использовать. В этом случае при отключении проводного соединения полного обрыва связи не произойдёт.

Ядро использует настройки метрик при выборе одного из возможных маршрутов для исходящих пакетов — например, при двух включённых сетевых интерфесах, проводном и беспроводном. Если вдруг одно из соединений прерывается, то второй вариант автоматически объявляется победителем. При этом полного разрыва соединения не происходит. Правда, для текущих процессов передачи данных не всегда всё так гладко, но, сторого говоря, это проблема другого уровня сетевой модели OSI.

**Примечание:** Параметр `Metric` используется для статических маршрутов, а `RouteMetric` — для динамической маршрутизации. Подробнее смотрите [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).
 `/etc/systemd/network/20-wired.network` 
```
[Match]
Name=enp1s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=10

```
 `/etc/systemd/network/25-wireless.network` 
```
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

[DHCP]
RouteMetric=20

```

#### Переименование интерфейса

Файлы *.link* можно использовать для назначения интерфейсу нового имени вместо [редактирования правил udev](/index.php/Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Смена_имени_интерфейса "Network configuration (Русский)"). Например, можно задать постоянное имя интерфейса для USB-to-Ethernet адаптера на основе его MAC-адреса, т.к. имена таким адаптерам обычно назначаются в зависимости от того, к какому USB-порту они подключены.

 `/etc/systemd/network/10-ethusb0.link` 
```
[Match]
MACAddress=12:34:56:78:90:ab

[Link]
Description=USB to Ethernet Adapter
Name=ethusb0
```

**Примечание:** Название пользовательского файла *.link* должно быть "меньше" (в лексическом смысле), чем название файла настроек по умолчанию `99-default.link`. Например, название `10-ethusb0.link` подходит, а `ethusb0.link` — нет.

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

Если вы используете *systemd-nspawn*, вам, возможно, потребуется изменить `systemd-nspawn@.service` и добавить параметры загрузки в строку `ExecStart`. Для исчерпывающего списка варианттов, обратитесь к [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1). Обратите внимание, если вы хотите, использовать автоматическую настройку DNS от DHCP, то Вам необходимо включить `systemd-resolved` и символьную ссылку `/run/systemd/resolve/resolv.conf` на `/etc/resolv.conf`. Для большей информации, смотрите `systemd-resolved.service(8)`.

Before you start to configure your container network, it is useful to:

*   disable all your [netctl](/index.php/Netctl "Netctl") services. This will avoid any potential conflicts with `systemd-networkd` and make all your configurations easier to test. Furthermore, odds are high you will end with few or even no [netctl](/index.php/Netctl "Netctl") activated profiles. The `netctl list` command will output a list of all your profiles, with the activated one being starred.
*   disable the `systemd-nspawn@.service` and use the `systemd-nspawn -bnD /path_to/your_container/` command as root to boot the container. To log off and shutdown inside the container `systemctl poweroff` is used as root. Once the network setting meets your requirements, [enable and start](/index.php/Systemd#Basic_systemctl_usage "Systemd") `systemd-nspawn@.service`
*   disable the `dhcpcd.service` if enabled on your system, since it activates *dhcpcd* on **all** interfaces
*   make sure you have no [netctl](/index.php/Netctl "Netctl") profiles activated in the container, and ensure that `systemd-networkd.service` is neither enabled nor started
*   make sure you do not have any [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") rules which can block traffic
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

Когда, [включен](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Включить_юнит_в_автозапуск_при_загрузке_системы "Systemd (Русский)") и запущен `systemd-networkd.service` в вашем контейнере.

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

Если вы не хотите настраивать DNS в `/etc/resolv.conf` и хотите полагаться на DHCP для его настройки, вам нужно [включить](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Включить_юнит_в_автозапуск_при_загрузке_системы "Systemd (Русский)") `systemd-resolved.service` и сделать символическую ссылку `/run/systemd/resolve/resolv.conf` на `/etc/resolv.conf`

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

## Советы и рекомендации

### Интеграция сетевого интерфейса и рабочего стола

Systemd-networkd не имеет встроенной функциональности для интерактивного управления сетевыми интерфейсами, ни через графическое приложение, ни через командную строку. Тем не менее, существует ряд утилит для отображения состояния сети, изменения настроек или получения уведомлений.

*   Утилита командной строки *networkctl* позволяет вывести информацию о сетевых интерфейсах.
*   Когда networkd настраивается с помощью [WPA supplicant](/index.php/WPA_supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA supplicant (Русский)"), утилитами *wpa_cli* и *wpa_gui* можно динамически настраивать WLAN-интерфейсы.
*   Плагин [networkd-notify-git](https://aur.archlinux.org/packages/networkd-notify-git/) выводит уведомления при изменениях в работе интерфейса (например, при установлении соединения или его завершении).
*   Демон [networkd-dispatcher](https://aur.archlinux.org/packages/networkd-dispatcher/) позволяет выполнять сценарии при изменении состояния интерфейса. Работает схожим образом с *NetworkManager-dispatcher*.
*   Отобразить информацию о DNS-сервере для systemd-resolved можно командой `resolvectl status`.

### Назначение IP-адреса на основании SSID

Может возникнуть ситуация, когда дома вы используете беспроводную сеть с DHCP, а на работе — беспроводную же сеть, но со статическим IP-адресом. Пример смешанных настроек приведён ниже.

**Примечание:** Номер в начале имени файла определяет порядок, в котором они будут обрабатываться. В разделе [Match] можно использовать параметры SSID, BSSID или оба одновременно.
 `/etc/systemd/network/24-wireless-office.network` 
```
# отдельные настройки для сети WiFi на работе
[Match]
Name=wlp2s0
SSID=название_точки_доступа
#BSSID=aa:bb:cc:dd:ee:ff

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1
DNS=10.1.10.1
#DNS=8.8.8.8

```
 `/etc/systemd/network/25-wireless-dhcp.network` 
```
# для остальных сетей используется DHCP
[Match]
Name=wlp2s0

[Network]
DHCP=ipv4

```

## Решение проблем

## Смотрите также

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)