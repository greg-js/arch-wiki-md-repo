Ссылки по теме

*   [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)")
*   [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Network bridge](/index.php/Network_bridge "Network bridge")
*   [Настройка сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D1%81%D0%B5%D1%82%D0%B8 "Настройка сети")
*   [Настройка беспроводной сети](/index.php/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%B1%D0%B5%D1%81%D0%BF%D1%80%D0%BE%D0%B2%D0%BE%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D0%B5%D1%82%D0%B8 "Настройка беспроводной сети")
*   [Category:Network configuration (Русский)](/index.php/Category:Network_configuration_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Network configuration (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd"). Дата последней синхронизации: 9 февраля 2020\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Systemd-networkd&diff=0&oldid=595945).

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
        *   [2.1.1 [Match]](#[Match])
        *   [2.1.2 [Link]](#[Link])
        *   [2.1.3 [Network]](#[Network])
        *   [2.1.4 [Address]](#[Address])
        *   [2.1.5 [Route]](#[Route])
        *   [2.1.6 [DHCP]](#[DHCP])
    *   [2.2 Файлы netdev](#Файлы_netdev)
        *   [2.2.1 [Match]](#[Match]_2)
        *   [2.2.2 [Netdev]](#[Netdev])
    *   [2.3 Файлы link](#Файлы_link)
        *   [2.3.1 [Match]](#[Match]_3)
        *   [2.3.2 [Link]](#[Link]_2)
*   [3 Использование с контейнерами](#Использование_с_контейнерами)
    *   [3.1 Простая DHCP-сеть](#Простая_DHCP-сеть)
    *   [3.2 DHCP-сеть с отдельными IP-адресами](#DHCP-сеть_с_отдельными_IP-адресами)
        *   [3.2.1 Интерфейс моста](#Интерфейс_моста)
        *   [3.2.2 Привязка Ethernet к мосту](#Привязка_Ethernet_к_мосту)
        *   [3.2.3 Сеть моста](#Сеть_моста)
        *   [3.2.4 Добавление моста в команду запуска контейнера](#Добавление_моста_в_команду_запуска_контейнера)
        *   [3.2.5 Результат](#Результат)
        *   [3.2.6 Замечания](#Замечания)
    *   [3.3 Сеть со статическими IP-адресами](#Сеть_со_статическими_IP-адресами)
*   [4 Советы и рекомендации](#Советы_и_рекомендации)
    *   [4.1 Интеграция сетевого интерфейса и рабочего стола](#Интеграция_сетевого_интерфейса_и_рабочего_стола)
    *   [4.2 Назначение IP-адреса на основании SSID](#Назначение_IP-адреса_на_основании_SSID)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 Службы монтирования при неудачной загрузке](#Службы_монтирования_при_неудачной_загрузке)
    *   [5.2 systemd-resolved не может найти локальный домен](#systemd-resolved_не_может_найти_локальный_домен)
    *   [5.3 Подключённый компьютер не использует мост](#Подключённый_компьютер_не_использует_мост)
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

Файлы настроек могут находиться в следующих каталогах (в порядке увеличения приоритета):

*   `/usr/lib/systemd/network` — системный сетевой каталог.
*   `/run/systemd/network` — runtime-каталог сетевых программ.
*   `/etc/systemd/network` — локальный каталог системного администрирования.

Существуют три типа файлов настройки.

*   Файлы ***.network*** — настройки (профили) сетевых интерфейсов.
*   Файлы ***.netdev*** — настройки (профили) виртуальных сетевых интерфейсов.
*   Файлы ***.link*** — настройки, которые использует менеджер устройств [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") при обнаружении нового интерфейса.

Для этих файлов действуют следующие правила:

*   Профиль активируется, если совпали **все** условия в разделе `[Match]`.
*   Если в разделе `[Match]` не указано ничего, то профиль применяется для всех устройств (можно сравнить с подстановочным символом `*`).
*   Файлы настроек сортируются по названиям и обрабатываются в лексическом порядке, независимо от каталога, в котором они расположены.
*   Файлы с одинаковыми названиями заменяют друг друга — в порядке приоритета каталогов, в которых они находятся.

**Совет:**

*   Чтобы не дать системе использовать файл настроек в `/usr/lib/systemd/network`, в том числе и после обновления, создайте в каталоге `/etc/systemd/network` символическую ссылку на `/dev/null` с таким же именем.
*   В значениях параметров можно использовать подстановочный символ `*`. Например, шаблон `en*` будет соответствовать любому Ethernet-интерфейсу.
*   Согласно [этому сообщению](https://mailman.archlinux.org/pipermail/arch-general/2014-March/035381.html), сетевые настройки контейнера лучше задавать файлами networkd *внутри контейнера*.
*   Systemd понимает значения `1, true, yes, on` как логическое *true*, а `0, false, no, off` — как *false*.

### Файлы network

В network-файлах задаются сетевые настройки, чаще всего — для серверов и контейнеров.

Файлы *.network* могут содержать разделы `[Match]`, `[Link]`, `[Network]`, `[Address]`, `[Route]` и `[DHCP]`. Ниже приведены основные параметры для каждого раздела. Подробнее смотрите [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5).

#### [Match]

Наиболее распространенные ключи для поиска совпадающего устройства:

| Параметр | Описание | Возможные значения | Значение по умолчанию |
| `Name=` | Поиск интерфейса по названию, например: `en*`. Символ `!` в начале инвертирует результаты поиска. | Разделённые пробелами названия интерфейсов (можно указывать шаблоны с подстановочными символами в стиле командной оболочки), логическое отрицание (`!`). |
| `MACAddress=` | Поиск интерфейса по MAC-адресу, например: `MACAddress=01:23:45:67:89:ab 00-11-22-33-44-55 AABB.CCDD.EEFF` | Разделённые пробелами MAC-адреса в шестнадцатеричном формате; в качестве внутреннего разделителя в адресах можно использовать двоеточия, дефисы и точки. |
| `Host=` | Поиск по имени хоста или machine ID. | Имя хоста (в том числе в виде шаблона), [machine ID](https://jlk.fjfi.cvut.cz/arch/manpages/man/machine-id.5.en) |
| `Virtualization=` | Проверка на работу в виртуальном окружении. `Virtualization=false` — для хост-системы, `Virtualization=true` — для работы в контейнере или виртуальной машине. Есть возможность проверить тип виртуализации и реализацию. | булевские, логическое отрицание (`!`), тип (`vm` и `container`), реализация (`qemu`, `kvm`, `zvm`, `vmware`, `microsoft`, `oracle`, `xen`, `bochs`, `uml`, `bhyve`, `qnx`, `openvz`, `lxc`, `lxc-libvirt`, `systemd-nspawn`, `docker`, `podman`, `rkt`, `wsl`, `acrn`) |

#### [Link]

*   `MACAddress=` — [замена MAC-адреса](/index.php/MAC_address_spoofing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Способ_1:_systemd-networkd "MAC address spoofing (Русский)").
*   `MTUBytes=` — большее значение MTU (например, при использовании [jumbo frames](/index.php/Jumbo_frames "Jumbo frames")) может повысить скорость передачи данных.
*   `Multicast=` — [групповая передача](https://en.wikipedia.org/wiki/ru:%D0%9C%D1%83%D0%BB%D1%8C%D1%82%D0%B8%D0%B2%D0%B5%D1%89%D0%B0%D0%BD%D0%B8%D0%B5 "wikipedia:ru:Мультивещание") для интерфейса(-ов).

#### [Network]

| Параметр | Описание | Допустимые значения | Значение по умолчанию |
| `DHCP=` | Поддержка DHCPv4- и/или DHCPv6-клиента. | булевское, `ipv4`, `ipv6`. | `false` |
| `DHCPServer=` | Запуск сервера DHCPv4. | булевское | `false` |
| `MulticastDNS=` | Поддержка [multicast DNS](https://tools.ietf.org/html/rfc6762). Если задать значение `resolve`, то включится только разрешение имён, но не регистрация и объявление хостов/служб. | булевское, `resolve` | `false` |
| `DNSSEC=` | Поддержка DNSSEC. Если задать значение `allow-downgrade`, то DNSSEC будет автоматически отключаться в не-DNSSEC сетях, что повысит совместимость. | булевское, `allow-downgrade` | `false` |
| `DNS=` | Адрес [DNS](/index.php/DNS "DNS")-сервера. Может указываться больше одного раза. | [`inet_pton`](http://man7.org/linux/man-pages/man3/inet_pton.3.html) |
| `Domains=` | Список доменов, которые должны разрешаться с использованием DNS-сервера ([подробнее](https://www.freedesktop.org/software/systemd/man/systemd.network.html#Domains=)) | имя домена (в том числе с символом (`~`) в начале) |
| `IPForward=` | Пересылка входящих пакетов на другой интерфейс в соответствии с таблицей маршрутизации. | булевское, `ipv4`, `ipv6` | `false` |
| `IPv6PrivacyExtensions=` | Использование временных IPv6-адресов в соответствии с [RFC 4941](https://tools.ietf.org/html/rfc4941). Если задать значение `prefer-public`, то privacy extensions включатся, но предпочтение будет отдаваться использованию публичных адресов, а не временных. Если задать значение `kernel`, то будут использоваться настройки ядра. | булевское, `prefer-public`, `kernel` | `false` |

#### [Address]

*   `Address=` — статический адрес интерфейса. Если не используется DHCP, то эта опция **обязательна**.

#### [Route]

*   `Gateway=` — адрес шлюза. Если не используется DHCP, то эта опция **обязательна**.
*   `Destination=` — префикс сети назначения.

Если параметр `Destination` не задан, то используется маршрут по умолчанию.

**Совет:** Если в разделах `[Address]` и `[Route]` заданы только параметры `Address=` и `Gateway=` соответственно, то для краткости оба эти параметра можно перенести в раздел `[Network]`.

#### [DHCP]

| Параметр | Описание | Допустимые значения | Значение по умолчанию |
| `UseDNS=` | Объявление DNS-сервера при работе DHCP-сервера. | булевское | `true` |
| `Anonymize=` | Если задать значение `true`, посылаемые DHCP-серверу параметры будут соответствовать [RFC7844](https://tools.ietf.org/html/rfc7844) (Anonymity Profiles for DHCP Clients) для сокрытия идентифицирующей информации. | булевское | `false` |
| `UseDomains=` | Использование полученного от DHCP-сервера домена в качестве адреса для DNS-поиска. Если задать значение `route`, полученное доменное имя будет использоваться только для маршрутизации DNS-запросов, но не для поиска. Эта опция может повлиять на локальное разрешение имён с помощью [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"). | булевское, `route` | `false` |

### Файлы netdev

В файлах netdev описывается создание виртуальных сетевых интерфейсов. В нём два раздела, `[Match]` и `[NetDev]`. Ниже приведены некоторые важные параметры. Подробнее смотрите [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5).

#### [Match]

*   `Host=` — поиск по имени хоста.
*   `Virtualization=` — проверка на виртуализацию.

#### [Netdev]

Наиболее распространенные ключи:

*   `Name=` — имя интерфейса. Опция **обязательна**.
*   `Kind=` — вид интерфейса. Например, *bridge*, *bond*, *vlan*, *veth*, *sit* и т.д. Опция **обязательна**.

### Файлы link

Файлы link выступают в качестве альтернативы пользовательским правилам [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") и применяются при обнаружении менеджером нового устройства. Файл состоит из двух разделов, `[Match]` и `[Link]`. Ниже приведены основные параметры обоих разделов. Подробнее смотрите [systemd.link(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.link.5).

**Совет:** Для выявления проблем с *.link*-файлами используйте команду `# udevadm test-builtin net_setup_link /sys/*путь/к/сетевому/устройству*` .

#### [Match]

*   `MACAddress=` — поиск по MAC-адресу.
*   `Host=` — поиск по имени хоста.
*   `Virtualization=` — проверка на виртуализацию.
*   `Type=` — поиск по типу интерфейса (например, vlan).

#### [Link]

*   `MACAddressPolicy=` — использование постоянных или же случайных адресов.
*   `MACAddress=` — использование конкретного адреса.

**Примечание:** Настроек в системном файле `/usr/lib/systemd/network/99-default.link`, как правило, в большинстве случаев вполне достаточно.

## Использование с контейнерами

В [systemd](https://www.archlinux.org/packages/?name=systemd) входит заранее настроенная служба `systemd-networkd.service`. Необходимо [включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустить](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") этот юнит на хосте и в контейнере.

При отладке сетевых настроек также понадобятся пакеты [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [net-tools](https://www.archlinux.org/packages/?name=net-tools) и [iproute2](https://www.archlinux.org/packages/?name=iproute2).

Если вы собираетесь в качестве средства контейнеризации использовать [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn"), то добавьте загрузочные параметры в строку `ExecStart` файла юнита `systemd-nspawn@.service`. Подробнее о параметрах смотрите [systemd-nspawn(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-nspawn.1).

Если вы хотите использовать DHCP для автоматической настройки DNS, то включите `systemd-resolved` и создайте символическую ссылку `/run/systemd/resolve/resolv.conf` на файл `/etc/resolv.conf`. Подробнее смотрите [systemd-resolved.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.service.8).

Перед началом настройки сети контейнера сделайте следующее:

*   отключите все службы [netctl](/index.php/Netctl_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Netctl (Русский)") (на хосте и контейнере), [dhcpcd](/index.php/Dhcpcd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dhcpcd (Русский)") (на хосте и контейнере), systemd-networkd (только в контейнере) и `systemd-nspawn@.service` (только на хосте). Это позволит избежать конфликтов и упростит отладку.
*   включите [пересылку пакетов](/index.php/Internet_sharing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Разрешите_пересылку_пакетов "Internet sharing (Русский)"), чтобы контейнер имел доступ в интернет. Убедитесь, что в файлах *.network* пересылка не отключена, потому что с параметром `IPForward=1` `systemd-networkd` отключит пересылку для указанного интерфейса, даже если она разрешена глобально для всей системы.
*   убедитесь, что правила [iptables](/index.php/Iptables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Iptables (Русский)") не блокируют трафик.
*   убедитесь, что после запуска демона команда `networkctl` выводит список сетевых интерфейсов.

В примерах ниже:

*   вывод команды `ip a` будет ограничен только рассматриваемыми интерфейсами.
*   *хост* будет означать вашу основную ОС, а *контейнер* — гостевую виртуальную машину.
*   все названия сетевых интерфейсов и IP-адреса приведены в качестве примера.

### Простая DHCP-сеть

Эта настройка включит DHCP для хоста и контейнера. В этом случае обе системы будут иметь одинаковый IP, поскольку они разделяют один и тот же интерфейс.

 `/etc/systemd/network/*мой_DHCP*.network` 
```
[Match]
Name=en*

[Network]
DHCP=ipv4

```

Затем [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") `systemd-networkd.service` в контейнере.

Разумеется, `en*` можно заменить полным названием вашего Ethernet-интерфейса, который можно узнать командой `ip link`.

*   на хосте и в контейнере:

 `$ ip a` 
```
2: enp7s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.72/24 brd 192.168.1.255 scope global enp7s0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever

```

По умолчанию DHCP-сервер назначает хосту временное (transient) имя. Чтобы этого не происходило, задайте параметр `UseHostname=false` в разделе `[DHCPv4]`:

 `/etc/systemd/network/*мой_DHCP*.network` 
```
[DHCPv4]
UseHostname=false

```

Если вы не хотите настраивать DNS в файле `/etc/resolv.conf` и желаете полагаться только на DHCP в этом вопросе, [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") `systemd-resolved.service` и создайте символическую ссылку `/etc/resolv.conf` на файл `/run/systemd/resolve/resolv.conf`:

```
# ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf

```

Подробнее смотрите [systemd-resolved.service(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.service.8).

**Примечание:** Если вы подключились к системному разделу через `arch-chroot`, то символическую ссылку необходимо создать именно на нём, а не в chroot-окружении. В противном случае arch-chroot создаст ссылку на файл в live-окружении.

### DHCP-сеть с отдельными IP-адресами

#### Интерфейс моста

Первым делом необходимо создать виртуальный интерфейс моста. С помощью systemd создаём устройство-мост `br0`:

 `/etc/systemd/network/*мой_мост*.netdev` 
```
[NetDev]
Name=br0
Kind=bridge
```

[Перезапустите](/index.php/%D0%9F%D0%B5%D1%80%D0%B5%D0%B7%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Перезапустите") `systemd-networkd.service`, чтобы настройки вступили в силу.

*   на хосте и контейнере:

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default 
    link/ether ae:bd:35:ea:0c:c9 brd ff:ff:ff:ff:ff:ff

```

Обратите внимание, что интерфейс `br0` обнаружен, но он всё ещё выключен (DOWN).

#### Привязка Ethernet к мосту

Следующий шаг — выполнить привязку реального сетевого интерфейса к виртуальному мосту. В примере ниже мы привязываем любой интерфейс, название которого совпадает с шаблоном `en*`.

 `/etc/systemd/network/*привязка*.network` 
```
[Match]
Name=en*

[Network]
Bridge=br0
```

Выбранному проводному интерфейсу не должно быть назначено никакого IP-адреса, поскольку для привязки необходим интерфейс без оного. Если необходимо, отредактируйте файл `/etc/systemd/network/*мой_Eth*.network` соответствующим образом.

#### Сеть моста

Теперь, поскольку мост создан и привязан к существующему сетевому интерфейсу, необходимо создать настройки IP. Это определяется в файле *.network*:

 `/etc/systemd/network/*мой_мост*.network` 
```
[Match]
Name=br0

[Network]
DHCP=ipv4
```

#### Добавление моста в команду запуска контейнера

Поскольку мы собираемся назначить отдельные IP-адреса для хоста и контейнера, то нужно отделить сеть контейнера от хоста. Чтобы это сделать, добавьте параметр `--network-bridge=br0` к команде запуска контейнера.

```
# systemd-nspawn --network-bridge=br0 -bD */путь/к/контейнеру*

```

#### Результат

*   для хоста

 `$ ip a` 
```
3: br0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default 
    link/ether 14:da:e9:b5:7a:88 brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.87/24 brd 192.168.1.255 scope global br0
       valid_lft forever preferred_lft forever
    inet6 fe80::16da:e9ff:feb5:7a88/64 scope link 
       valid_lft forever preferred_lft forever
6: vb-*мой_контейнер*: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP group default qlen 1000
    link/ether d2:7c:97:97:37:25 brd ff:ff:ff:ff:ff:ff
    inet6 fe80::d07c:97ff:fe97:3725/64 scope link 
       valid_lft forever preferred_lft forever

```

*   для контейнера

 `$ ip a` 
```
2: host0: <BROADCAST,MULTICAST,ALLMULTI,AUTOMEDIA,NOTRAILERS,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 5e:96:85:83:a8:5d brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.73/24 brd 192.168.1.255 scope global host0
       valid_lft forever preferred_lft forever
    inet6 fe80::5c96:85ff:fe83:a85d/64 scope link 
       valid_lft forever preferred_lft forever

```

#### Замечания

*   теперь задан один IP-адрес для интерфейса `br0` на хосте, и один для интерфейса `host0` в контейнере.
*   появилось два новых интерфейса: `vb-*мой_контейнер*` на хосте и `host0` в контейнере. Это результат опции `--network-bridge=br0`, которая включает в себя другую — `--network-veth`, которая создаёт виртуальный Ethernet-канал между хостом и контейнером.
*   DHCP-адрес интерфейса `host0` был выдан на основании файла `/usr/lib/systemd/network/80-container-host0.network`.

*   на хосте

 `$ brctl show` 
```
bridge name	bridge id		STP enabled	interfaces
br0		8000.14dae9b57a88	no		enp7s0
							vb-*мой_контейнер*

```

Выше показано, что в системе есть мост с двумя связанными интерфейсами.

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

А здесь видно, что были активированы интерфейсы `br0` и `host0` с отдельными IP-адресами и шлюзом по умолчанию 192.168.1.254\. Адрес шлюза был автоматически назначен systemd-networkd.

 `$ cat /run/systemd/resolve/resolv.conf` 
```
nameserver 192.168.1.254

```

### Сеть со статическими IP-адресами

Настройка статического IP-адреса может быть удобной в случае развёртывания веб-сервисов (например, FTP, http, SSH). Если в файле `/usr/lib/systemd/network/99-default.link` задан параметр `MACAddressPolicy=persistent` (значение по умолчанию), то устройствам будут назначены постоянные MAC-адреса. Следовательно, будет несложно настроить маршрутизацию сервисов от шлюза на разные интерфейсы.

Выполните следующие настройки:

*   на хосте

Настройка очень похожа на настройку [#DHCP-сеть с отдельными IP-адресами](#DHCP-сеть_с_отдельными_IP-адресами). Во-первых, нужно создать виртуальный мост и привязать к нему физический интерфейс. Эта делается с помощью двух файлов настроек, содержание которых аналогично файлам из раздела о DHCP.

```
/etc/systemd/network/*мой_мост*.netdev
/etc/systemd/network/*мой_Eth*.network

```

Далее, необходимо настроить IP и DNS для моста. Пример настройки:

 `/etc/systemd/network/*мой_мост*.network` 
```
[Match]
Name=br0

[Network]
DNS=192.168.1.254
Address=192.168.1.87/24
Gateway=192.168.1.254

```

*   на контейнере

Первым делом нужно избавиться от файла `/usr/lib/systemd/network/80-container-host0.network`, в котором содержится конфигурация DHCP для сетевого интерфейса контейнера по умолчанию. Чтобы сделать изменение постоянным (например, даже после обновления пакета [systemd](https://www.archlinux.org/packages/?name=systemd)), создайте символическую ссылку с таким же именем на `/dev/null`. Это замаскирует файл `/usr/lib/systemd/network/80-container-host0.network` поскольку файлы с тем же именем в каталоге `/etc/systemd/network` имеют приоритет перед `/usr/lib/systemd/network`. Однако если вы хотите, чтобы у хоста был статический IP-адрес, а у контейнера — выданный DHCP динамический, то этот файл нужно оставить.

```
# ln -sf /dev/null /etc/systemd/network/80-container-host0.network

```

Наконец, настройте статический IP для стандартного сетевого интерфейса `host0` и [запустите/включите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5/%D0%B2%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Запустите/включите") службу `systemd-networkd.service` в контейнере. Пример конфигурации:

 `/etc/systemd/network/*мой_вирт_Eth*.network` 
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

### Службы монтирования при неудачной загрузке

Если при автозапуске службы вроде [Samba](/index.php/Samba "Samba")/[NFS](/index.php/NFS_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NFS (Русский)") загружаются слишком рано, до запуска сетевых служб, то стоит [включить](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `systemd-networkd-wait-online.service`. Тем не менее, такое случается достаточно редко, потому что чаще всего сетевые демоны запускются даже без настроенной сети.

### systemd-resolved не может найти локальный домен

[systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") не может осуществить поиск локального домена по одному имени хоста, даже с параметрами `UseDomains=yes` и `Domains=[domain-list]` в файле *.network*, причём в файле `resolv.conf` задано `search [domain-list]`. Выполните `networkctl status` или `resolvectl status` чтобы убедиться, что домены поиска действительно используются.

Возможные решения:

*   Отключите [LLMNR](/index.php/Systemd-resolved#LLMNR "Systemd-resolved"), чтобы systemd-resolved мог работать с DNS-суффиксами.
*   Проверьте базу данных `hosts` в файле `/etc/nsswitch.conf` (например, удалите параметр `[!UNAVAIL=return]` для службы `resolve`).
*   Переключитесь на использование полных доменных имён.
*   Используйте файл `/etc/hosts` для разрешения имён хостов.
*   Воспользуйтесь службой `dns` библиотеки glibc вместо службы входящей в systemd службы `resolve`.

### Подключённый компьютер не использует мост

Первый компьютер подключён к двум локальным сетям. Второй — ещё к одной сети и к первому компьютеру через мост. Выполните следующие команды, чтобы второй компьютер получил доступ к сетям первого за мостовым интерфейсом:

```
# sysctl net.bridge.bridge-nf-filter-pppoe-tagged=0
# sysctl net.bridge.bridge-nf-filter-vlan-tagged=0
# sysctl net.bridge.bridge-nf-call-ip6tables=0
# sysctl net.bridge.bridge-nf-call-iptables=0
# sysctl net.bridge.bridge-nf-call-arptables=0

```

## Смотрите также

*   [systemd.networkd man page](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html)
*   [Tom Gundersen, main systemd-networkd developer, G+ home page](https://plus.google.com/u/0/+TomGundersen/posts)
*   [Tom Gundersen posts on Core OS blog](https://coreos.com/blog/intro-to-systemd-networkd/)
*   [How to set up systemd-networkd with wpa_supplicant](https://bbs.archlinux.org/viewtopic.php?pid=1393759#p1393759) (WonderWoofy's walkthrough on Arch forums)